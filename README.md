```
### AI-Integrated Challenge Analysis — Mandatory

Treat Synixon as an AI-integrated security challenge, not merely a conventional web application.

1. Identify every endpoint, workflow, model repository, or backend component that uses AI/LLMs or AI-driven authorization decisions.
2. Determine which security decisions are made by deterministic application code and which depend on model outputs.
3. Analyze how natural-language instructions, model context, input validation, trust boundaries, and output handling affect the challenge.
4. Test relevant AI-specific weaknesses only within the authorized CTF scope, alongside conventional web vulnerabilities and access-control flaws.
5. Do not assume that an AI-related vulnerability exists merely because an AI model repository or AI functionality is present. Verify the actual implementation and behavior before drawing conclusions.
6. Build a reproducible Python solver based on verified findings, with bounded retries, clear diagnostics, and verification of each required step.
7. Preserve the original challenge state wherever possible. Avoid unnecessary account changes, destructive operations, and automated flag submissions.
8. Document the confirmed exploit chain, the evidence supporting each step, environmental dependencies, and any conditions that may prevent the solver from working in a fresh challenge instance.

The objective is to understand how AI integration changes the attack surface and challenge difficulty, rather than relying exclusively on ordinary web enumeration.
```
