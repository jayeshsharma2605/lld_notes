# 42 — Memento Pattern

**Playlist lesson:** 42 of 43  
**Author:** Jayesh Sharma

## 1. Core idea

Memento captures an object's state so it can be restored later without exposing its internal representation. A caretaker stores snapshots; the originator restores them.

## 2. Design workflow

```mermaid
flowchart TD
 A[Understand requirement]-->B[Identify objects and responsibilities]
 B-->C[Define interfaces and relationships]
 C-->D[Walk through the main scenario]
 D-->E[Check edge cases and tests]
```

## 3. Example and design decisions

For editor undo, consider snapshot memory cost, immutable snapshots, deltas, checkpoint frequency and sensitive data.

## 4. What to remember

- Start from requirements and use cases, not from a pattern name.
- Give each class a clear responsibility and protect its invariants.
- Prefer composition and focused interfaces when they reduce coupling.
- Identify error paths, object lifecycle and concurrent access where relevant.

## 5. Interview practice

Explain the design in two minutes. Draw the key classes and one sequence. State one trade-off and one test for an edge case.

## 6. C++ implementation hints

- Use RAII and smart pointers according to ownership.
- Inject dependencies through constructors instead of relying on global state.
- Use const-correct interfaces and explicit state types.
- Test normal flow, invalid input, boundaries and failure handling.

---
*LLD Study Library · Author: Jayesh Sharma*
