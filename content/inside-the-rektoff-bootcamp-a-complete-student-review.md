---
title: "Inside the Rektoff Bootcamp: A Complete Student Review"
date: "2025-12-02"
author: "0xh4ty"
description: "A detailed review of my experience in Cohort #2 of the Rektoff Solana x Rust Security Bootcamp. This post covers the structure, instructors, curriculum, capstone audit, and the skills I gained, along with practical suggestions for future students."
---

![Jacket On Jacket Off Image](../assets/img/JacketOnJacketOff_image.png)

## Introduction

Hello and welcome. I hope you are doing well. Around four months ago, I decided to learn Solana security and began studying the Rust Programming Language Book. Two months later, I had the opportunity to join Cohort #2 of the Rektoff Solana x Rust Security Bootcamp, a program fully funded by the Solana Foundation. This blog post is a complete review of that experience, along with a set of suggestions to help future students get the most value out of the bootcamp.

Let’s get started.

## Bootcamp Structure and Timeline

The Rektoff bootcamp runs for eight weeks and is divided into two modules. The first module covers Rust theory and fundamentals. The second module focuses on Solana security, tooling, and practical auditing techniques.

Each module lasts for three weeks and includes three live sessions per week: two lectures and one office hours session with the instructor. All live sessions are recorded and uploaded to the bootcamp’s Notion workspace, along with transcriptions and summaries for review.

During Module 2, we also had guest lectures from two engineers working on Solana framework and tooling, as well as a Solana auditor active in the ecosystem. These sessions added practical context from real-world security work.

After Module 2 ends, students receive a capstone project: an intentionally vulnerable Solana protocol to audit over two weeks. This final phase brings together all the concepts learned in the bootcamp and simulates a real audit environment.

When pre-reads are provided, you are expected to go through them before the lecture so you can follow the material more effectively. After each lecture, quizzes are assigned to reinforce the concepts covered, and these must be completed before the deadlines.

## Instructors and Teaching Style

The first module on Rust theory and fundamentals was taught by [Daniel Cumming](https://x.com/danielkcumming) from Runtime Verification. His teaching style focuses on removing any sense of “magic” from the language. If you mention an observed behavior, he will point you to the exact line in the Rust compiler or standard library that explains it. His lectures emphasize building a rigorous foundation in discrete mathematics and computer systems, and that mindset comes through clearly in how he teaches.

The second module on Solana security and tooling was taught by [M4rio](https://x.com/m4rio_eth) from Cantina. His approach is centered on developing attacker intuition. Instead of abstract theory, he shows how he reasons about programs, how he approaches an unfamiliar codebase, how he identifies weak assumptions, and how he moves quickly without losing correctness. The focus is on learning real attacker workflows and internalizing the pace and mindset required in audit environments.

## Student Support and Operations

The operations side of the bootcamp was handled by [Lucas Hygate](https://ca.linkedin.com/in/lucas-hygate-34492518a) from DefiSafety, who managed scheduling, announcements, deadlines, and all student-facing coordination. He was consistently responsive on Slack and made it clear that students could reach out whenever they were stuck, facing time constraints, or dealing with personal issues that affected progress.

Throughout the bootcamp, he checked in with students individually, clarified expectations around quizzes and the capstone, and ensured that everyone had what they needed to stay on track. From an operations standpoint, the experience was smooth, predictable, and well-organized, which made it easier to focus fully on the technical content.

## Cohort Environment and Community

All bootcamp discussions take place in a private Slack workspace that includes students, instructors and alumni. This is where you ask questions, clarify concepts and interact with others working through the same material. Most days you will see active conversation, with people sharing insights and helping each other solve problems.

## Who This Bootcamp Is For

The Rektoff team expects applicants to have basic Rust knowledge. If you already know Solana or Anchor, following the pace becomes easier, but it is not a strict requirement. The cohort usually includes students, developers and EVM auditors, so the backgrounds are diverse. They also aim for geographical diversity, and you will see participants from many parts of the world.

The primary trait they look for is commitment. The bootcamp is fully funded, and they select people they believe will actively contribute to the Solana ecosystem. Because of that, the selection process is competitive and highly selective.

## Curriculum and Learning Experience

The curriculum is structured to promote autonomy rather than hand-holding. The pre-reads and supporting material are clear, well-chosen, and easy to digest, but you are expected to do the reasoning yourself. Quizzes reinforce the concepts covered in lectures and include both MCQs and working questions that require a solid understanding of the material. If you approach them with incorrect assumptions, the instructor’s feedback will make those gaps obvious.

Although the bootcamp officially expects around 5–10 hours of weekly commitment, in practice that is not enough. You will need closer to 30 hours per week to review the material, study before and after lectures, write quiz solutions, and handle occasional technical issues without falling behind.

During Module 2, you are expected to spot bugs live during the lectures. I failed to catch almost all of them in real time, so I practiced by revisiting the exercise code after each session and attempting to find the issues on my own. This turned out to be extremely helpful and strengthened my ability to reason about vulnerabilities without guidance.

## The Capstone: Your First Real Audit

This is where everything comes together. All the theory from Module 1 and the hands-on practice from Module 2 converge in the capstone. You are expected to find as many issues as you can and write PoCs for a subset of them. If you’ve been putting in steady work during the first six weeks, the capstone becomes much more manageable.

I was genuinely surprised by how naturally I could reason about the code and spot issues. Even though the capstone is an intentionally vulnerable program and not a production-grade protocol, it is still an excellent exercise that captures the core workflow of a real audit. I enjoyed the entire process.

The instructors also walk you through how to structure and format your report in one of the lectures, so you will know exactly what is expected when preparing your report.

## What Makes the Bootcamp Hard

Coming in with only basic Rust knowledge and no Solana or Anchor experience, I faced three main difficulties.

First, the jump from Module 1 to Module 2 is significant. Module 1 focuses on Rust internals and systems-level reasoning, while Module 2 shifts abruptly into Solana security and auditing. Although we were given a week to learn Solana and Anchor before Module 2 began, that time is not enough if you only commit 5–10 hours per week.

Second, I ran into version mismatches between Rust Analyzer and Anchor, which slowed me down more than expected. These kinds of setup issues can cost hours if you are unlucky.

Third, the Solana ecosystem relies heavily on writing tests in TypeScript. Since I had no JavaScript or TypeScript background, I chose to write tests in Rust during Module 2. The documentation for the Rust anchor-client was outdated, so I had to figure things out by reading the source code and experimenting. I later submitted a pull request to update the documentation. If you are reading this in the future, the updated documentation will probably be available.

## How My Skills Improved

There is a clear knowledge delta from learning Rust internals, the Solana execution model, and the Anchor framework, but I will focus instead on the specific hard skills that improved during the bootcamp.

First, I became much more comfortable approaching unfamiliar codebases and treating the code itself as the single source of truth when trying to understand a mechanism. Second, I started to develop my own methodology for hunting bugs instead of relying on preset checklists. Third, I made progress in tracing execution flows at a deeper level. I am still far from perfect at it, but the improvement is noticeable.

## The Jobs Program

Rektoff offers an optional jobs program for students who want career support. If you opt in, you receive individualized feedback on your resume, guidance on how to position your skills, and help identifying opportunities that match your trajectory. The team is selective and realistic about placements, and they focus on preparing you to operate at a professional level rather than promising shortcuts.

It is not a guaranteed placement pipeline, but it is a strong support system if you are actively building toward a career in Solana security.

## Suggestions for Future Students

### What to Know Going In

If you plan to apply and you have no prior Rust, Solana, or Anchor experience, I strongly recommend reading the [Rust Programming Language Book](https://doc.rust-lang.org/stable/book/) from start to finish before the bootcamp begins. It will save you a lot of time and prevent you from getting overwhelmed once the pace increases.

Do not expect to become job ready or an elite auditor immediately after the bootcamp. Two months is a short period, and the goal is not mastery but acceleration. The realistic outcome is that you learn enough fundamentals and workflow discipline to continue improving on your own.

The best mindset is to think in the long term. Focus on absorbing the concepts, habits, and reasoning patterns that you can carry forward in your career rather than chasing short-term outcomes. The instructors provide a strong foundation, and your job is to internalize it and keep building after the bootcamp ends.

### How to Approach Module 1

Module 1 is theory heavy, but its purpose is to ground you in the foundational computer science concepts that prevent the language from feeling magical later. You will learn how static, stack and heap memory work, how Rust interacts with each of these memory regions, and why certain patterns exist in the language.

Everything you learn here applies beyond Solana security. These fundamentals show up in systems programming, backend engineering, high-performance code, and security work in general. Your main goal in this module should be to develop a clear and accurate mental model of how Rust behaves at a low level so that the rest of the bootcamp builds on solid ground.

### How to Approach Module 2

Module 2 focuses on developing an attacker’s mindset and becoming comfortable operating in ambiguity and uncertainty. The only reliable way to build this mindset is through practice. You might not catch vulnerabilities during the live sessions, and that is completely normal. Go back after each lecture, revisit the exercise code, and explore different ways the logic could break. Treat every function as something you are trying to exploit, not something you are trying to understand passively.

This is also the stage where you should start practicing writing PoCs. If you already know JavaScript or TypeScript, follow the common path and write PoCs in TypeScript. If you do not have experience with either, writing PoCs in Rust using the anchor-client is a perfectly valid alternative. The important thing is to build the habit of translating a vulnerability into a reproducible exploit.

### How to Approach the Capstone

If you focused on learning the things I mentioned above, then the capstone will feel much easier to handle. At this stage, there are two things you should prepare for. First, you need a basic methodology so you are not approaching the codebase randomly. Decide how you will map the protocol, how you will track assumptions and how you will prioritize suspicious areas. Second, you must manage your time across the three stages of the capstone: finding bugs, writing PoCs for the important ones and preparing the final report. Managing these steps steadily and in sequence makes the whole process far more controlled.

### How to Approach the Grind

Treat the bootcamp seriously enough that you stay disciplined with the pace. You will have a few off days, but that is normal. Recover quickly and keep moving. If you intend to be casual about it or might drop out midway, it is better not to apply at all because someone else who is committed could have used that spot.

Make sure you finish each lecture’s material before the next session. Every lecture builds on the previous one, and falling behind creates a compounding effect that is hard to recover from. Staying aligned with the pace will make the entire bootcamp smoother.

Finally, ask good questions. A good question is one you arrive at after doing your own investigation, forming a hypothesis and getting stuck. These questions get solved quickly, either by instructors or by other students. Shallow questions with no effort behind them tend to get ignored.

## Final Thoughts

Looking back at the last two months, the Rektoff bootcamp ended up being one of the most worthwhile learning experiences I have gone through. The structure, the instructors and the environment push you in the right ways. The biggest value for me was not a specific topic or technique but the shift in how I reason about programs, how I approach unfamiliar code and how I think during ambiguity.

The only thing you will lack after going through the bootcamp will be speed. The only way to improve speed is through practice and deeper knowledge, and my focus after the bootcamp will be on that specific aspect.

More details about the bootcamp can be found on their [website](https://www.rektoff.xyz/bootcamp).

See you in the next one. Thanks for reading.
