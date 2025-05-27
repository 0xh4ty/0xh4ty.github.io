---
title: "Don’t Trust the Callback: A Hacker’s Guide to Reentrancy"
date: "2025-05-25"
author: "0xh4ty"
---

## Introduction

Reentrancy is not just an attack vector in smart contracts. It is a behavioral flaw that mirrors recursive logic but emerges from control being transferred to an external contract mid-execution. Unlike traditional software where locks, thread-local storage, and shared state protections exist, smart contracts must defend themselves explicitly.

This post will break down the concept of reentrancy, dissect real attack patterns, and show how to exploit and prevent them. It will cover three types of reentrancy attacks: **Single Function**, **Cross-Function**, and **Cross-Contract**.

## What Is Reentrancy?

At a high level, reentrancy is when a contract calls an external contract which then reenters back into the original contract *before* the original function completes and the internal state is properly updated. This leads to violations of contract assumptions, enabling exploits like draining funds, bypassing auth, or causing denial of service.

It is not a loop. It is a state machine hijack.

## Why It Happens in Smart Contracts

* No implicit locking or thread-local state
* Mutable storage that isn't updated until after external calls
* Developers violating Checks-Effects-Interactions

## Types of Reentrancy Attacks

### 1. Single Function Reentrancy

This is the simplest form. One function updates state *after* making an external call, which lets an attacker repeatedly reenter and exploit the stale state.

**Real-World Example**: [The DAO Hack (2016)](https://www.coindesk.com/markets/2016/06/18/understanding-the-dao-attack/)

**Blog Used**: [Pessimistic's Breakdown](https://blog.pessimistic.io/reentrancy-attacks-on-smart-contracts-distilled-7fed3b04f4b6)

### 2. Cross-Function Reentrancy

This occurs when multiple functions share mutable state, and one function allows reentrancy into another before the state is properly locked or updated.

**Observed Pattern**:

* Shared state across functions
* A reentrant call triggers a second function that manipulates the same variables

**Codebase Studied**: [Cross-function.sol](https://github.com/uni-due-syssec/eth-reentrancy-attack-patterns/blob/master/cross-function.sol)

### 3. Cross-Contract Reentrancy

This is more complex. Contract A interacts with Contract B before updating its own state. Contract B is attacker-controlled and reenters A through a separate call or callback.

**Attack Path**:

* Contract A calls B (e.g., token swap or callback)
* B calls back into A before A finalizes state

**Reference Code & Blog**:

* [Inspex GitHub Repo](https://github.com/InspexCo/cross-contract-reentrancy)
* [Inspex Blog](https://inspexco.medium.com/cross-contract-reentrancy-attack-402d27a02a15)

## Fixing Reentrancy

### General Defenses

* Use **Checks-Effects-Interactions**: update state before external calls.
* Add **Reentrancy Guards** (mutex-like pattern):

```solidity
bool private locked;
modifier noReentrant() {
    require(!locked, "Reentrant call");
    locked = true;
    _;
    locked = false;
}
```

### For Each Type:

* **Single Function**: update internal state before external calls.
* **Cross-Function**: use reentrancy guards on all relevant functions.
* **Cross-Contract**:

  * Don’t trust user-supplied contract addresses
  * Whitelist approved contracts
  * Avoid making external calls mid-function

## Final Thoughts

Reentrancy is not a vulnerability. It’s a capability. The exploit arises when developers leave state unprotected and make premature external calls. The key to avoiding it is understanding **where control can be lost**.

By learning from real-world exploits and practicing on open-source codebases, you build an instinct for dangerous patterns. Avoid blind trust in callbacks. Always assume the worst and code defensively.

This blog is my distilled learning from multiple sources, broken down and remixed into something any smart contract auditor can internalize and act on.

Stay paranoid. Stay precise.
