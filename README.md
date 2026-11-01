# Hands dirty, code clean!
## About myself
I'm an engineer who bridges the gap between hardware and software—combining mechatronics with modern development practices to build embedded systems that actually work in the real world.
My Background

## How I found my way
My journey started with a bachelor's in `Mechanical Engineering`, where I focused on mechatronics. From there, I pursued a master's in `Robotics, Cognition, and Intelligence`, diving deep into control techniques, reinforcement learning, and autonomous driving. My thesis explored trajectory tracking for linear systems using reinforcement learning—work I completed as part of BMW's master scholarship program.
Through my studies, I discovered something important: while talented software developers are plentiful, fewer combine coding skills with genuine understanding of hardware and electronic systems. That's where I found my niche.

## Personal carrer
I've spent my career in embedded software development, working on systems where software meets power electronics. I've developed for battery management systems and high-voltage DC/DC converters (800V), and I'm currently back again on ADAS ECU systems where reliability and precision aren't optional.

I approach problems with both hands-on practical knowledge and clean code principles. Whether it's debugging a circuit or optimizing an algorithm, I believe in understanding the full picture.

## Beyond Engineering
I stay active through different kind of sports like running, swimming, fitness, skiing, volleyball, soccer and much more. 

I wrench on cars in my spare time and take on DIY woodworking projects equipping some areas of my appartment. For me, working with my hands — whether with tools or code  — keeps me grounded.

I value down-to-earth collaboration, clean organization, and thoughtful work that considers both people and the planet. Engineering is problem-solving, but it's also about doing things the right way.

## What you'll find within my GitHub account

My embedded software is split into small repositories.

**Generic repositories** (shared building blocks, no project code):
- [emb-ci](https://github.com/t0biasm/emb-ci): reusable CI workflows, the propagation and canary bot
- [emb-toolchain](https://github.com/t0biasm/emb-toolchain): compilers and Bazel toolchains (AVR8, C2000, host LLVM)
- [emb-platform](https://github.com/t0biasm/emb-platform): MCU support for AVR8 and C2000, incl. the FreeRTOS port

**Projects:**
- [prj-sumobot](https://github.com/t0biasm/prj-sumobot): sumo robot "Black Magic" (ATmega32U4), with an Arduino Leonardo kick-off application
- [prj-tif2838](https://github.com/t0biasm/prj-tif2838): application for the TI F28P65x evaluation board (C2000)

### How a project is set up
- The generic repositories are git submodules at the root of the project (`emb-toolchain/`, `emb-platform/`), pinned to a commit. Bazel refers to them by module name, e.g. `@emb_platform//...`.
- `emb-project.toml` in the project root declares which submodule follows which branch (`track`) and how updates are applied: `auto` (fast-forward after a green CI) or `pr` (a pull request). Submodules that are not listed stay frozen.
- The project's CI is a short workflow that calls the reusable workflow of `emb-ci`, pinned to a tag.
- To add a project: create `prj-<name>` with the repository topic `emb-project`, add the submodules, `MODULE.bazel` overrides, `emb-project.toml` and the CI workflow, install the bot app and protect `main`.

### How the projects stay generic
- Generic repositories contain no project code, and projects contain no toolchain or MCU code. Shared changes are made once and used everywhere.
- A push to a generic repository moves the submodule pointer in each project that follows it, but only after that project's CI is green with the new commit. Otherwise nothing changes and an issue is opened.
- A pull request in a generic repository first builds the dependent projects with the PR's commit (the canary). A failing project blocks the merge.
- Every change goes through a pull request, and `main` is protected everywhere.
