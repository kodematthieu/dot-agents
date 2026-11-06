# Lens: Formal verification

One optional Axiom lens. Use when the user asks about correctness or safety properties and the problem is amenable.

- State the definitions of the system and its states precisely.
- State the property to be checked, in a form that could fail.
- List assumptions the property depends on.
- Describe candidate counterexamples and the conditions under which they occur.
- Provide executable checker commands only when the checker and tool are actually available; otherwise identify them clearly as suggestions.

Formal notation is not itself proof. A model that was not checked proves nothing.