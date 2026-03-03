---
applyTo: "**"
---

# General Instructions for GitHub Copilot

## Purpose

This workspace is dedicated to **learning Android development** by following the [Android Developers training courses](https://developer.android.com/courses). The primary goal of this repository is to **support and accelerate the user's learning journey**, not to build production-ready software.

When assisting in this workspace, always keep the educational context in mind. Prioritize clarity and understanding over brevity.

---

## Code Style & Quality

- Write code that is **clean, readable, and well-structured**.
- Follow the **latest Android and Kotlin best practices** (e.g., Jetpack Compose, ViewModel, StateFlow, etc.).
- Prefer idiomatic Kotlin over verbose or Java-style patterns.
- Keep functions small and focused on a single responsibility.
- Use meaningful names for variables, functions, and classes.

---

## Comments

- **Always write comments in both English and Japanese.**
- Place the English comment first, followed by the Japanese translation on the next line.
- Comments should explain the *why*, not just the *what*.

### Example

```kotlin
// Initialize the ViewModel for this screen
// このスクリーン用の ViewModel を初期化する
val viewModel: MyViewModel = viewModel()

// Collect the UI state as a Compose State
// UI の状態を Compose の State として収集する
val uiState by viewModel.uiState.collectAsState()
```

---

## Responding to User Instructions

When the user asks you to implement something or solve a problem, **do not jump straight to a single solution**. Instead:

1. **Present multiple approaches** (at least 2–3 options when applicable).
2. **Compare the options** clearly — highlight trade-offs such as simplicity, performance, testability, and alignment with best practices.
3. **Make a recommendation** and explain *why* that approach is preferred in the current learning context.

### Example Format

> **Option A: [Name]**
> - Description of the approach
> - ✅ Pros / ❌ Cons
>
> **Option B: [Name]**
> - Description of the approach
> - ✅ Pros / ❌ Cons
>
> **Recommendation:** Option A is recommended because ...

This approach helps the user understand the reasoning behind decisions and learn how to evaluate trade-offs independently.

---

## General Reminders

- This workspace is for **learning**, so always be willing to add extra explanation when it aids understanding.
- When introducing a new concept or API, briefly explain what it does and why it is used.
- Avoid over-engineering. Prefer the simplest solution that demonstrates the concept clearly.
