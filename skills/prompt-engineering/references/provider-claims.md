# Provider claims and current documentation

Load this when a prompt design decision depends on how a specific provider, model, or runtime behaves.

## Rule

Encode a provider-specific behavior only after checking it against that provider's current primary documentation. State the version or date you checked. If you cannot verify it, mark it as a hypothesis to test rather than a fact.

## Claims that are commonly wrong

- **Context window sizes.** Model context limits change and differ per model and per endpoint. Do not copy a number from a blog post or an older release note.
- **Caching behavior and pricing.** Cache boundaries, minimum prefix length, retention windows, and discounts are provider-specific and frequently revised. Measure them in your own traffic; do not derive savings from a formula.
- **Reasoning controls.** Effort levels, thinking budgets, and reasoning toggles differ per provider and per model family, and their effect on latency and cost is not linear. Test empirically.
- **Structured output support.** Native JSON schema enforcement, tool calling, and constrained decoding vary. Valid syntax does not establish correct or authorized values. Validate at the application boundary.
- **Tool call protocol shapes.** Parallel calls, tool choice modes, and schema strictness differ. Confirm the current API shape before encoding it.
- **Role and message precedence.** System, developer, and user roles exist in some form almost everywhere, but precedence rules, ordering behavior, and whether roles are actually enforced differ by API.

## What to record

- Provider and endpoint, model identifier, and documentation version or retrieval date.
- The specific behavior being relied on, quoted or paraphrased from the primary source.
- Which parts are guaranteed by the provider and which are your inference.
- How you will verify it in your own environment before relying on it.

## Model adaptation

Do not assume a particular model family, private reasoning format, context size, cache behavior, or tool-call protocol. Do not request hidden reasoning traces or provider-managed thought signatures. Use provider-specific controls only when they are configured and documented for the active environment.

If the prompt must work across several providers, isolate provider-specific behavior behind an application-side adapter or schema rather than embedding conditional instructions in one large prompt.