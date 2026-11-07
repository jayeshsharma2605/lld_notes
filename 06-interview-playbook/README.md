# 06 — LLD Interview Playbook

## 1. Start with requirements, not classes

Use questions such as:
- Who are the actors?
- What are the main use cases?
- What is the expected scale or workload if it affects the design?
- What is explicitly out of scope?
- Which rules must never be violated?
- Are operations synchronous or asynchronous?
- Can two users modify the same resource at the same time?

## 2. A 45-minute design structure

| Time | Activity |
|---:|---|
| 0–5 min | Clarify scope and assumptions |
| 5–10 min | List use cases and core entities |
| 10–20 min | Draw class diagram and assign responsibilities |
| 20–30 min | Walk through main sequence and state changes |
| 30–37 min | Handle errors, concurrency and edge cases |
| 37–45 min | Discuss trade-offs, extensibility and tests |

Adjust the time to the interviewer's direction; do not rush into code before the model is clear.

## 3. Class responsibility template

For each class, answer:
- What does it own?
- What does it know?
- What does it do?
- Which invariants does it protect?
- Which other objects does it depend on?
- What should not be its responsibility?

Avoid anemic domain models where all behaviour sits in one service, but do not force every tiny operation into a separate class either.

## 4. Design review checklist

### Correctness
- Are invalid state transitions prevented?
- Are identifiers and money represented safely?
- Are duplicate requests handled?
- Are boundary conditions covered?

### Extensibility
- What is likely to vary?
- Is a stable interface useful here?
- Can a new implementation be added without modifying unrelated code?

### Concurrency
- What is shared mutable state?
- What must be atomic?
- Is locking process-local or shared across instances?
- What happens after a timeout or crash?

### Maintainability
- Are names clear?
- Are responsibilities cohesive?
- Are dependencies easy to replace in tests?
- Are patterns solving a real problem?

## 5. Common interview mistakes

- Treating every noun as a class.
- Putting all logic in a Manager or Service class.
- Using inheritance where composition is better.
- Applying every GoF pattern in one solution.
- Ignoring failure paths and concurrent requests.
- Forgetting object lifecycle and ownership.
- Using floating-point values for currency.
- Not explaining trade-offs.

## 6. How to present a design

Use this sequence:

1. “Let me confirm the requirements and assumptions.”
2. “These are the main use cases.”
3. “These are the core domain objects and their responsibilities.”
4. “This diagram shows how they relate.”
5. “Let me walk through the main request.”
6. “Here is how I handle a failure or concurrent request.”
7. “These are the trade-offs and possible extensions.”

## 7. Revision questions

1. What is the difference between association, aggregation and composition?
2. Explain LSP with an example that violates it.
3. When would you choose Strategy over State?
4. Adapter vs Decorator vs Proxy?
5. Factory Method vs Abstract Factory?
6. Why is a local mutex insufficient for multiple service instances?
7. How would you prevent double booking?
8. How do you make payment retries safe?
9. What is the role of a value object?
10. How would you test a state machine?
