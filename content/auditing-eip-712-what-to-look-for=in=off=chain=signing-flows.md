---
title: "Auditing EIP-712: What to Look For in Off-Chain Signing Flows"
date: "2025-06-08"
author: "0xh4ty"
description: "How to audit EIP-712 smart contracts for signature replay, forgery, and off-chain signing bugs. Covers common mistakes in EIP-712 and ERC20Permit implementations."
---

## Introduction

EIP-712 is a standard designed to make off-chain signing of structured data both secure and user-friendly. It is used extensively in the Ethereum ecosystem, especially in DeFi protocols where actions such as token approvals are signed off-chain to save gas. A prominent example of this is the ERC20 `permit()` function introduced by EIP-2612, which allows token holders to approve transfers without sending an on-chain transaction.

However, incorrect implementations of EIP-712 are a rich source of vulnerabilities. Improper handling of signed data can lead to serious bugs, including signature replay attacks and signature forgery. This post explores this bug class in depth.

## The Basics of EIP-712

EIP-712 defines how to sign typed structured data in a way that prevents signature ambiguity. This makes signatures context-specific, reducing the risk of misuse across different domains or contracts.

EIP-2612 extends ERC20 with `permit()`, `nonces()`, and `DOMAIN_SEPARATOR()` to enable gasless approvals. The permit flow relies on strict adherence to EIP-712 to prevent misuse.

## Observed Patterns

* Static or missing DOMAIN\_SEPARATOR. Signature replay across contracts or chains.
* No nonce. Signature replay on same contract leading to funds drain.
* No deadline. Signature valid forever allowing delayed replay attacks.
* Wrong struct hashing (typeHash) because of wrong order leading to DoS.
* Using abi.encodePacked in place of abi.encode causing DoS.
* Skipping \x19\x01 prefix. Signature mismatch and DoS.
* Missing signer != address(0) check. Signature forgery via ecrecover returning address(0).
* Custom permit() instead of using OpenZeppelin ERC20Permit—often the root of these mistakes.

## Vulnerable Code Patterns

### Static DOMAIN\_SEPARATOR (missing chainId and address(this))

```solidity
bytes32 public constant DOMAIN_SEPARATOR = keccak256(
    abi.encode(
        keccak256("EIP712Domain(string name,string version)"),
        keccak256(bytes("TokenName")),
        keccak256(bytes("1"))
    )
);
```

### No nonce in permit struct or no increment of nonces\[owner]

```solidity
bytes32 structHash = keccak256(
    abi.encode(
        PERMIT_TYPEHASH,
        owner,
        spender,
        value,
        deadline // missing nonce!
    )
);

// Missing: _nonces[owner]++;
```

### No deadline check

```solidity
// Missing: require(block.timestamp <= deadline, "expired");
```

### Wrong struct hashing (typeHash)

```solidity
bytes32 public constant PERMIT_TYPEHASH = keccak256(
    "Permit(address owner,address spender,uint256 deadline,uint256 value)" // wrong order and missing nonce
);
```

### Using abi.encodePacked instead of abi.encode

```solidity
bytes32 structHash = keccak256(
    abi.encodePacked(
        PERMIT_TYPEHASH,
        owner,
        spender,
        value,
        nonce,
        deadline
    )
);
```

### Skipping \x19\x01 prefix

```solidity
bytes32 digest = keccak256(
    abi.encodePacked(
        DOMAIN_SEPARATOR,
        structHash
    )
);
```

### Missing signer != address(0) check

```solidity
address signer = ecrecover(digest, v, r, s);
// Missing: require(signer != address(0), "invalid sig");
require(signer == owner, "invalid sig");
```

### Rolling custom permit() instead of importing OpenZeppelin ERC20Permit

```solidity
contract MyToken is ERC20, IERC20Permit {
    // Manual DOMAIN_SEPARATOR, manual nonces, manual ecrecover — risky
}
```

## Exploit Ideas

* Replay a signature on a different contract if DOMAIN\_SEPARATOR is static or missing chainId/address(this).
* Replay a signature multiple times on the same contract if nonce is missing or not incremented.
* Use a signature after its intended lifetime if deadline is missing or deadline check is not enforced.
* Craft a malicious signature with reordered or missing fields to exploit wrong struct hashing.
* Trigger signature mismatch DoS by skipping the \x19\x01 prefix.
* Forge a signature by passing random (v, r, s) that makes ecrecover return address(0), combined with owner == address(0) in permit.
* Target poorly written custom permit() implementations that deviate from OpenZeppelin ERC20Permit standard.

## How to Fix

* Use OpenZeppelin ERC20Permit implementation and avoid writing custom permit() functions.
* If writing custom permit(), strictly follow EIP-712 and EIP-2612 specifications.
* DOMAIN\_SEPARATOR must include chainId and address(this), and must be dynamic if chainId can change.
* Always include nonce in the struct hash and increment nonce on each successful permit().
* Always include deadline in the struct hash and enforce require(block.timestamp <= deadline).
* Use correct PERMIT\_TYPEHASH with exact field order and types per EIP-2612.
* Use abi.encode, not abi.encodePacked.
* Always build digest as keccak256("\x19\x01" || DOMAIN\_SEPARATOR || structHash).
* Always check require(signer != address(0), "invalid sig") after ecrecover.
* Always check require(owner != address(0), "invalid owner") to prevent permit() to/from address(0).
* Audit any custom permit() implementation carefully.

## References and Further Reading

* [EIP-712 Typed structured data hashing and signing](https://eips.ethereum.org/EIPS/eip-712)
* [EIP-2612 Permit Extension for EIP-20 Signed Approvals](https://eips.ethereum.org/EIPS/eip-2612)
* [OpenZeppelin ERC20Permit.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/ERC20Permit.sol)

## Conclusion

Not only the variants covered in this post, but there are over 20 known variants caused by broken EIP-712 implementations.

Broken EIP-712 implementations are one of the most common and dangerous bug classes in DeFi smart contracts. The financial impact of a signature replay attack can be devastating. Strict adherence to the standard and using well-audited libraries like OpenZeppelin ERC20Permit is the best way to avoid these pitfalls.
