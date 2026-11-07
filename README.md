# Low-Level Design (LLD) Study Library

**Simple explanations · Practical examples · UML and flowcharts · Interview preparation**  
**Author: Jayesh Sharma**

A structured set of beginner-friendly notes based on the first **43 videos** of the [Concept && Coding — Low Level Design from Basics to Advanced playlist](https://www.youtube.com/playlist?list=PL6W8uoQQ2c61X_9e6Net0WdYZidm7zooW).

> These notes are independently written study material. They explain the concepts in plain language and use original examples and diagrams; they are not a transcript or a reproduction of the videos.

## How to use this library

1. Start with the foundations and learn how to turn requirements into objects and responsibilities.
2. Study SOLID before memorising design patterns.
3. Learn each pattern by understanding the problem it solves, its structure, and its trade-offs.
4. Read the case studies and practise drawing the class and sequence diagrams yourself.
5. For every design, ask: what changes frequently, what must remain stable, and what can fail concurrently?

## Contents

| Chapter | Topics |
|---|---|
| [01 — LLD Foundations](01-foundations/README.md) | LLD vs HLD, design workflow, OOP, UML, SOLID |
| [02 — Design Patterns](02-design-patterns/README.md) | Creational, structural and behavioural patterns |
| [03 — Object Modelling & Concurrency](03-object-modeling-and-concurrency/README.md) | HashMap internals, booking concurrency, locking, thread safety |
| [04 — LLD Case Studies](04-case-studies/README.md) | Parking lot, games, elevator, rental, logging, booking, ATM, Splitwise and more |
| [05 — Algorithms & Design Exercises](05-algorithms-and-exercises/README.md) | Debt simplification, coupons, inventory, cache and payment design |
| [06 — Interview Playbook](06-interview-playbook/README.md) | Requirement checklist, design sequence, review checklist, questions |
| [Video Index](VIDEO_INDEX.md) | Mapping of playlist videos 1–43 to these notes |

## Learning path

`Requirements → Use cases → Entities → Responsibilities → Relationships → Interfaces → Interactions → Edge cases → Tests`

## Diagram conventions

Diagrams use Mermaid. GitHub renders Mermaid blocks directly. If viewing locally, use a Markdown preview extension that supports Mermaid.

## Language

The source playlist examples are primarily Java-oriented. The notes focus on language-independent design and use C++-friendly terminology/examples where useful. The same object model can be implemented in Java, C++, C# or Python.

## Source

[Concept && Coding — LLD playlist](https://www.youtube.com/playlist?list=PL6W8uoQQ2c61X_9e6Net0WdYZidm7zooW)

---
*Distributed Systems Study Library · Author: Jayesh Sharma*
