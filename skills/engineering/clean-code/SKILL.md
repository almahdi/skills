---
name: clean-code
description: >
  Pragmatic software design discipline enforcing YAGNI, KISS, DRY, and SOLID in
  priority order so simplicity gates abstraction. Supports intensity levels:
  lite, full (default), ultra. Use on any coding task: writing, refactoring,
  reviewing, or designing software architecture, classes, functions, modules, or
  interfaces. Also use whenever the user mentions "clean-code", "clean code",
  "SOLID", "DRY", "KISS", "YAGNI", "single responsibility", "dependency
  inversion", "code quality", or invokes /clean-code.
argument-hint: "[lite|full|ultra]"
metadata:
  author: "Ali Almahdi (@almahdi)"
  license: "MIT"
  category: "engineering"
---

# Clean Code

Good code is simple, clear, and purposeful. Apply classic software engineering principles in strict priority order so simplicity gates abstraction. Never use a design principle as an excuse to build enterprise bloat.

## Persistence

Active on every coding response for the rest of the session. Do not drift back into premature abstraction or god functions after a few turns.

Default level is **full**. Switch levels with `/clean-code lite|full|ultra`. Turn off only when the user says `"stop clean-code"` or `"normal mode"`, confirm in one line, and return to default behavior.

---

## The priority ladder

Principles conflict when applied blindly. Resolve every conflict by climbing this ladder in order. Earlier rungs always outrank later rungs:

```text
[1. YAGNI] -> [2. KISS] -> [3. DRY (when earned)] -> [4. SOLID (when complexity demands it)]
```

### 1. YAGNI: You aren't gonna need it

Do not build functionality or structure until a concrete requirement demands it today.

- **Build for current requirements, not hypothetical futures.** Resist "just in case" flags, hooks, and extension points.
- **No single-implementation interfaces.** Do not extract an `IPaymentGateway` or `AbstractRepository` when only one concrete implementation exists and no test boundary requires it.
- **No configuration systems before configurability is needed.** Hardcode a named constant until a second environment or caller needs a different value.
- **Measure before optimizing.** Write the straightforward algorithm first; optimize only when a profiler or known scale constraint proves a bottleneck.

Bad: Creating `UserFactory`, `IUserRepository`, and `AbstractUserValidator` for a single CRUD endpoint.
Good: One `createUser` function and one concrete data call until a second storage backend or test seam is needed.

### 2. KISS: Keep it simple

Once a feature earns its existence, build it the simplest way that works.

- **Reach for built-ins first.** Use existing codebase helpers, standard library functions, and native framework components before writing custom utilities or adding external dependencies.
- **Write self-explanatory code.** Clear variable and function names replace comments that explain *what* the code does. Reserve comments for *why* a non-obvious decision was made.
- **Prefer flat over nested.** Use guard clauses and early returns instead of deep `if/else` pyramids.
- **Break down large units.** Split oversized functions, components, or modules into smaller, focused pieces that fit on one screen.

Bad: A 60-line custom date formatter with regex parsing.
Good: `Intl.DateTimeFormat` or the standard library's native date formatting in two lines.

### 3. DRY: Don't repeat yourself, when earned

Every piece of domain knowledge should have a single, unambiguous representation in the system, once the pattern is real.

- **Wait for the Rule of Three.** Two similar blocks of code can stay separate if they might evolve in different directions. Extract shared logic on the third repetition, or immediately when two places encode the exact same business rule that must never drift apart.
- **Never DRY by adding boolean mode flags.** If merging two functions requires `doWork(data, isSpecialCase = true)`, keep them as two separate functions and share only the small pure helper underneath.
- **Reuse across layers cleanly.** Extract repeated UI patterns into reusable components, shared state patterns into composable hooks or mixins, and pure calculations into focused utility functions.

Bad: Merging `createAdminUser` and `registerGuestUser` into one 90-line function full of `if (isAdmin)` branches.
Good: Two small entry functions that both call a pure `hashPassword` helper.

### 4. SOLID: Structure for code that grows

Apply SOLID principles to keep growing modules maintainable, testable, and decoupled without violating YAGNI or KISS.

#### Single responsibility: SRP
Each module, class, or function should have one primary reason to change.
- Separate presentation and UI rendering from business rules.
- Keep data repositories and API clients focused strictly on data transport and persistence.
- Isolate input parsing and validation from domain execution.

Bad: A UI component or HTTP handler that validates raw input, runs SQL queries, formats currency, and sends an email.
Good: A handler that validates the request, calls a domain function, and returns the formatted response.

#### Open/closed: OCP
Modules should be open for extension without modifying proven core logic, once multiple variants exist.
- When a second or third variant arrives, replace growing `switch` or `if/else` chains with a lookup map, strategy function, or shared contract.
- Add new behavior by registering a new handler or implementation rather than editing working code paths.

Bad: Editing a 200-line `calculateShipping` function every time a new carrier is added.
Good: A `carriers` map or `ShippingMethod` contract where adding `FedEx` or `DHL` means adding one self-contained entry.

#### Liskov substitution: LSP
Any implementation of a contract or subtype must be substitutable for its base type without surprises.
- Honor the base contract's input assumptions, return guarantees, and error behavior.
- Never override a method to throw `NotImplementedError` or silently do nothing because the base interface is too broad. Fix the interface instead.

Bad: A `ReadOnlyFileStore` extending `FileStore` that throws an exception when `save()` is called.
Good: Separate `ReadableStore` and `WritableStore` contracts so read-only implementations never fake write methods.

#### Interface segregation: ISP
Callers should never depend on methods they do not use.
- Define narrow, role-specific interfaces at the consumer's boundary rather than passing god objects.
- Keep function signatures minimal: pass `{ id, email }` instead of the entire 40-field `UserContext` when only two fields are read.

Bad: A single `Worker` interface requiring `work()`, `eat()`, and `sleep()` that forces automated jobs to implement dummy `eat()` and `sleep()` methods.
Good: Small contracts like `Runnable` and `Schedulable`, implemented only where needed.

#### Dependency inversion: DIP
High-level domain policy should not hardcode low-level I/O details.
- Pass external boundaries such as the database, network client, clock, filesystem, or third-party SDKs in as parameters or constructor arguments so domain logic stays pure and easy to test.
- Only introduce a formal interface at seams that cross I/O boundaries or have multiple real implementations. Pure internal helpers can be called directly.

Bad: A billing domain service that instantiates `new StripeProductionClient()` and calls `Date.now()` deep inside a calculation loop.
Good: Passing `paymentGateway` and `now` into the billing service so tests can pass a fake gateway and a fixed timestamp.

---

## Intensity levels

| Level | Behavior |
| :--- | :--- |
| **lite** | Follow the priority ladder naturally when writing code. If the user's existing code or prompt has a structural smell or premature abstraction, point it out in one short note without blocking. |
| **full** | Enforce the full priority ladder from YAGNI and KISS through DRY and SOLID. Keep responsibilities separated, inject real I/O boundaries, reuse existing codebase utilities, and refuse single-implementation interfaces or flag-driven DRY traps. Default. |
| **ultra** | Strict architectural discipline. Challenge speculative requirements before writing code, split god functions and mixed-responsibility modules on contact, and refactor touched seams to clean, testable boundaries in the same pass. |

Example prompt: "Add a notification service that sends an email when an order ships, and make it extensible for SMS and push later."

- **lite.** Builds the email notification function with a clean signature `(order, mailer)` and notes: "Kept this as a direct function for email; we can extract a multi-channel `Notifier` interface when SMS is actually added."
- **full.** Implements `sendOrderShippedEmail(order, mailer)` with domain formatting separated from the SMTP transport call. Skips the speculative SMS/push plugin framework until a second channel is in scope.
- **ultra.** Ships a pure message builder plus a single injected `sendEmail` boundary, deletes any unused notification scaffolding in the touched module, and adds a fast unit check with a fake sender.

---

## When not to abstract

Never use clean-code principles to justify:
1. **Pass-through middlemen.** A service class whose only job is forwarding every call unchanged to a repository violates KISS. Delete the middleman.
2. **One-line helpers called once.** Splitting a readable 15-line function into six 2-line private functions forces the reader to jump around the file. Keep cohesive sequential steps together until a piece is reused or complex enough to name on its own.
3. **Premature generics.** Type parameters with only one concrete type, such as `Processor<T>` only ever used as `Processor<Order>`, add noise without safety.
4. **Mocks for pure code.** Use dependency injection for I/O and stateful boundaries, not to mock simple data transformations or standard library calls.

---

## Composing with other skills

Clean Code governs **structural design and code organization**. It pairs cleanly with your other active skills:

- **With `ponytail`.** Ponytail cuts unnecessary lines and dependencies; `clean-code` makes sure the lines you keep have clear names, clean I/O seams, and a single responsibility. When both are active, YAGNI and KISS lead.
- **With `caveman`, `unslop`, or `i-have-adhd`.** Those skills shape how you write prose and structure chat responses. `clean-code` shapes the code inside the blocks.
- **With `orchestrate`.** Implementer subagents follow the priority ladder when writing chunks; reviewer subagents check diffs against YAGNI, KISS, DRY, and SOLID.
- **With `ember`.** Record major boundary and abstraction choices in `.memory/decisions/` when introducing a new architectural seam.
