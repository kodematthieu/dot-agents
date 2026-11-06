# Lens: Decision / Systems Analysis

Use when choosing among competing architectures, strategies, or designs with real tradeoffs under uncertainty.

## Decision Procedure

1. **Frame the Choice:** State the concrete decision to be made, who/what it binds, fixed constraints (non-negotiable bounds), and the 2–4 evaluation criteria that actually dominate the outcome.
2. **Construct Genuinely Distinct Options:** Include the **status quo / do-nothing baseline**, the **smallest viable intervention**, and materially different structural approaches—not strawman variants of one preferred answer.
3. **Classify Reversibility (One-Way vs. Two-Way Doors):**
   - **Two-way doors** (reversible at low cost): optimize for learning speed and simplicity; decide quickly.
   - **One-way doors** (public contracts, data schemas, security boundaries, irreversible lock-in): optimize for durability and explicit blast-radius containment.
4. **Assess Value of Information (VoI):** Ask whether the dominant uncertainty can be resolved faster by a bounded benchmark, prototype, or query than by extended theoretical debate.
5. **Stress-Test Beyond the Happy Path:** Evaluate each option under tail conditions—traffic spikes, partial dependency failure, operator error, adversarial input, and maintenance 12 months later.

## Output Contract (`Decision Summary`)

- **Decision & Constraints:** What is being chosen and under what hard limits.
- **Viable Options & Tradeoff Matrix:** Concise comparison across dominating axes (e.g., Speed vs. Accuracy, Efficiency vs. Resilience, Cost vs. Quality, Reversibility vs. Completeness), separating empirical facts from value preferences.
- **Recommended Option:** Name one primary recommendation when evidence supports it, or state clearly why options remain tied pending a specific preference weight.
- **Load-Bearing Assumptions & Reversal Trigger:** What must remain true for this choice to hold, and what concrete metric or observation would justify switching to the runner-up.
- **Smallest Disconfirming Check:** The cheapest test or validation step to run before irreversible commitment.
