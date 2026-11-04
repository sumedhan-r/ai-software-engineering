# Design Philosophy

Agent: read this before writing or reviewing any source code outside of tests.

---

## Rules

**DP-1 — No assert statements in source code.**
Rule: `assert` is not permitted outside of `tests/`. Use an explicit conditional raise instead.
Why: Python (and most runtimes) strip assert statements when running with optimisations enabled — a production container image will silently skip them. An assert that is meant to guard against invalid state becomes invisible at runtime.
In code: any `assert` found outside `tests/` is a violation. Replace with `if not <condition>: raise <Error>("<message>")`.

**DP-2 — A new private method needs a stated design reason.**
Rule: do not create a private method unless it has a design reason that can be written down, such as a distinct invariant worth naming.
Why: agents tend to create private methods with little design justification. A private method called from exactly one place is often just the function split in two. It adds indirection without adding reuse, and it encourages reviewers to skip auditing the logic because it looks like an internal detail.
In code: a private method with a single caller and no distinct invariant worth naming is a candidate to inline. If the method is kept, the calling function's docstring or a comment must state why the separation exists.

**DP-3 — Treat shallow private methods as a code smell requiring justification.**
Note: this rule is not yet fully settled. Shallow private methods — one or two lines, trivially named, called once — are a recurring indicator of over-decomposition. A Python `@staticmethod` can be an acceptable form when the logic is purely transformational and has no dependency on instance or class state, but that should be the explicit justification, not the default. Flag any shallow private method in review and ask whether it earns its indirection.

**DP-4 — A shared function must be generic and deep.**
Rule: a function shared across features has at least two real callers today and no caller-specific flags or mode parameters.
Why: a shared function that branches on who called it puts several behaviours behind one name. That raises interface complexity without any real reuse.
In code: a boolean or mode parameter, or an `if caller == ...` branch, inside a shared function is a violation. In review, also ask whether the name describes what the function does rather than who calls it, and whether its interface is clearly simpler than its implementation.

---

## Don't

- Do not use `assert` to validate function arguments, enforce invariants, or handle error cases in source code.
- Do not extract a private method solely to reduce the line count of a function.
- Do not accept a `@staticmethod` without confirming it has no hidden coupling to the class it sits in.
- Do not add a boolean or mode parameter to a shared function to serve one caller.
