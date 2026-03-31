---
title: "About Me"
date: "2025-03-31"
author: "0xh4ty"
description: "Systems programming, security research, and distributed systems engineering."
---

## Welcome

I’m **0xh4ty**, a systems programmer and security researcher focused on understanding how systems behave, where they fail, and how they can be broken.

This blog is a record of that exploration. It covers security research, reverse engineering, blockchain systems, and the design and implementation of low-level and distributed systems. The goal is not just to use systems, but to understand them deeply enough to reason about their behavior under real constraints.

## Path

I started in Web2 security and spent a couple of years building a foundation in penetration testing and web exploitation. During this time, I earned the HTB Certified Web Exploitation Specialist (CWES) certification and developed a working understanding of common vulnerability classes and exploitation patterns.

Over time, I structured my learning to build intuition across layers of abstraction, moving from higher-level systems toward lower-level and more complex environments:

Web application security -> Web3 security (Ethereum) -> Rust programming -> Web3 security (Solana) -> Reverse engineering -> Distributed systems engineering

Each transition increased both complexity and depth. The progression moved from exploiting application logic, to reasoning about on-chain state machines, to writing systems code, to analyzing compiled binaries, and finally to designing systems that must remain correct under concurrency, failure, and adversarial conditions.

I am currently pursuing a Master of Computer Applications (MCA), while continuing to focus heavily on hands-on systems work outside of formal coursework.

## Work

My work sits at the intersection of systems and security, with an emphasis on understanding failure modes and building intuition through direct interaction with real systems.

- Reproducing real-world smart contract vulnerabilities
- Writing exploit proof-of-concepts and validating attack surfaces
- Reverse engineering Linux binaries using Ghidra and GDB
- Contributing to open source compiler-adjacent tooling
- Building a Solidity language server for Emacs
- Developing a Rust-based static site generator that powers this blog

I focus on depth over breadth. The goal is to understand invariants, constraints, and edge cases rather than relying on surface-level patterns.

## Approach

I treat systems as artifacts that can be taken apart and studied. This involves reading code, tracing execution, inspecting memory layouts, and rebuilding simplified models to verify understanding.

Whenever possible, I prefer:
- Writing small reproductions instead of relying on theory alone
- Validating assumptions through debugging and instrumentation
- Studying real implementations instead of abstract descriptions

This approach helps build intuition that transfers across domains such as security, distributed systems, and low-level programming.

## Tooling

- **Operating System:** Linux
- **Primary Language:** Rust
- **Editor and Workflow:** Emacs

My tooling choices are driven by control, visibility, and the ability to inspect system behavior closely.

## Current Focus

My current focus is **distributed systems engineering**.

This includes building and understanding systems that deal with state replication, consistency, failure handling, and coordination across nodes. I am particularly interested in how these systems behave under partial failure and adversarial conditions.

Alongside this, I continue to work on:
- Reverse engineering
- Vulnerability discovery
- Strengthening low-level systems intuition

## Contact

- GitHub: [github.com/0xh4ty](https://github.com/0xh4ty)
- Twitter: [twitter.com/0xh4ty](https://twitter.com/0xh4ty)

---

This blog exists to document my journey in systems programming and security research and to share what I learn along the way.

If you are working on similar problems or following a similar path, feel free to reach out.
