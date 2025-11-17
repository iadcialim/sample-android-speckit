# Android App Constitution

This constitution defines the **non-negotiable principles** for this Android application.  
Every Spec, Plan, Task, and code change **must comply** with these rules. Where there is a conflict, **the constitution wins**.

---

## 1. Project Purpose & Scope

1. The application is a **modern, native Android app** built primarily with **Kotlin** and **Jetpack libraries**.
2. We prioritise:
   - **Correctness** over speed of delivery.
   - **Maintainability and readability** over cleverness.
   - **User trust, privacy, and security** over growth metrics.
3. All functionality must be **spec-driven**:
   - Features start from a written **spec** and **plan** before implementation.
   - Code must not diverge from the accepted spec without updating the spec first.

---

## 2. Platform, Tech Stack & Dependencies

1. **Language & Tooling**
   - Kotlin is the primary language.
   - Gradle **Kotlin DSL** for build scripts.
   - Android Studio: latest stable version.
2. **UI & Architecture Libraries**
   - **Jetpack Compose** is the default UI toolkit.
   - Use **Jetpack Navigation** or the agreed navigator.
3. **Coroutines & Async**
   - **Kotlin Coroutines** for async work.
   - Use **Flow/StateFlow/SharedFlow** for reactive streams.
4. **Dependency Injection**
   - **Hilt** (or agreed DI framework) is the single DI solution.
   - No manual service locators or custom singletons.
5. **Dependencies**
   - Prefer **Jetpack** and well-maintained libraries.
   - No abandoned or experimental dependencies.
   - Every new dependency must:
     - Have a clear purpose.
     - Be recorded in the spec/plan.
     - Be approved in review.

---

## 3. Architecture & Module Boundaries

1. **Overall Architecture**
   - Use **Clean Architecture with MVVM**.
   - Clear separation:
     - **Presentation** – UI, ViewModels
     - **Domain** – use cases, pure business logic
     - **Data** – repositories, local + remote sources
2. **Modules**
   - `:app` – entry point, DI setup, no business logic.
   - `:feature:<name>` – screens + viewmodels for each feature.
   - `:core:model` – shared models.
   - `:core:data` – shared network/local abstractions.
   - `:core:common` – minimal utilities and base abstractions.
3. **Unidirectional Data Flow**
   - UI observes **immutable state**.
   - Events flow upward from UI → ViewModel → domain.
4. **Layering Rules**
   - Presentation → Domain → Data.
   - Domain must not depend on Android or Data frameworks.

---

## 4. UI/UX & Design System

1. **Design System**
   - Based on **Material Design 3**.
   - All colours, typography, and spacing come from a **central design system**.
   - No hard-coded values in composables.
2. **Composable Best Practices**
   - Composables must be:
     - Small, reusable, and purposeful.
     - Accept a `Modifier` as the first param with `Modifier` default.
     - Free of side effects except via `LaunchedEffect` / effect APIs.
3. **UX Consistency**
   - Handling for loading, empty, and error states must be consistent.
4. **Accessibility**
   - Screens must support:
     - Content descriptions.
     - Minimum tap target sizes.
     - Colour contrast.
     - Dynamic font sizes.

---

## 5. State Management & Data Handling

1. **State Principles**
   - Single source of truth per screen.
   - Immutable UI state classes.
2. **Error Handling**
   - Handle errors gracefully with:
     - User-friendly messaging.
     - Structured logging.
3. **Offline & Failure Modes**
   - Plan for:
     - Intermittent connectivity.
     - Caching.
     - Retries/backoff.
   - Failure modes must be documented in the spec.

---

## 6. Testing & Quality Gates

1. **Testing Pyramid**
   - Unit tests for domain logic & ViewModels.
   - UI tests for key flows.
   - Integration tests for repositories where valuable.
2. **Coverage**
   - Critical logic must be tested.
   - New code must not reduce overall trend.
3. **Test Quality**
   - Tests must be deterministic.
   - No real network calls in unit tests.
4. **CI Requirements**
   - Build fails on:
     - Test failures.
     - Lint/static analysis issues.
     - Formatting errors.

---

## 7. Code Style, Linting & Documentation

1. **Code Style**
   - Follow Kotlin coding conventions.
   - Use **Ktlint/Spotless**—don't fight the formatter.
2. **Linting**
   - Android Lint must be enabled.
   - No blanket suppressions.
3. **Documentation**
   - KDoc for public APIs and complex logic.
   - Every feature needs:
     - `spec.md`
     - `plan.md`
     - A short architecture note for tricky flows.
4. **Naming**
   - Names must reflect intent.
   - Package/module structure follows features + layers.

---

## 8. Security, Privacy & Compliance

1. **Data Protection**
   - Sensitive data stored only when needed and encrypted.
   - No secrets in source control.
2. **Network Security**
   - HTTPS is mandatory.
   - Certificate pinning for sensitive endpoints.
3. **Authentication**
   - Use **OIDC/OAuth2 + PKCE** for secure flows.
   - Do not log tokens.
4. **Privacy**
   - No PII in logs.
   - Analytics must comply with privacy standards.

---

## 9. Performance, Reliability & Observability

1. **Performance**
   - Avoid blocking main thread.
   - Structured concurrency.
   - Respect performance budgets.
2. **Resource Management**
   - Avoid unnecessary allocations.
   - Clean up lifecycle-aware components.
3. **Observability**
   - Structured logs.
   - Meaningful analytics events.
4. **Crash-free Experience**
   - Crashes are top-priority issues.

---

## 10. Analytics, Feature Flags & Configuration

1. **Analytics**
   - Defined in spec before implementation.
   - Must answer real business questions.
2. **Feature Flags**
   - Prefer server-driven flags.
   - Each flag must have a sunset plan.
3. **Configuration**
   - No hard-coded environment values.
   - Build variants reflect environments.

---

## 11. Collaboration, PRs & Review Process

1. **Pull Requests**
   - Small, focused, tied to a specific task or spec.
   - PR must describe:
     - Spec/plan reference.
     - Tests added.
     - Risks and user-visible changes.
2. **Code Reviews**
   - Look for:
     - Correctness.
     - Architectural alignment.
     - Security/performance.
     - Clarity.
3. **Breaking Changes**
   - Must be reflected in the spec.
4. **Knowledge Sharing**
   - Pairing recommended for complex features.
   - Architectural decisions must be documented.

---

## 12. AI & SpecKit Usage

1. **AI as Assistant**
   - AI tools help with scaffolding and exploration.
   - Human engineers must validate everything.
2. **Spec-Driven Workflow**
   - Always begin with:
     - `/specify`
     - `/plan`
     - `/tasks`
   - Implementation starts only after approval.
3. **Constitution as Hard Constraint**
   - AI output must never violate this constitution.
4. **Auditability**
   - PRs should acknowledge substantial AI-assisted code.

---

## 13. Governance & Change Process

1. **Amendments**
   - Modified only through discussion with senior engineers.
   - Must be documented (ADR).
2. **Conflict Resolution**
   - If a spec conflicts with this constitution:
     - Update the spec, or
     - Propose a constitution amendment.
3. **Enforcement**
   - CI, reviews, and architecture checks enforce rules.
   - Repeated violations indicate process improvements are needed.

---
