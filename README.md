# AI CTF / Challenge Writeups

Hands-on writeups from AI security capture-the-flag challenges — prompt injection, jailbreaks, and the defenses that try to stop them. Each writeup documents what worked, *why* it worked at the model level, and what the failure teaches defenders building real LLM applications.

I write these from the builder's side of the table: I build and harden AI agents, and breaking guarded models is how I pressure-test the guardrails I put on my own. These are the attacks I want my systems to survive.

## Challenges

| Challenge | Focus | Status |
|-----------|-------|--------|
| [Gandalf (Lakera)](./gandalf-lakera-walkthrough) | Prompt injection across 7 escalating defense layers | Complete (L1–L7) |

## Why these exist

Prompt injection is the [#1 risk on the OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/). Every technique in these writeups maps to a real vulnerability class in production AI systems — and every level Gandalf loses is a lesson in why "just tell the model not to" is not a security control.

---
*Writeups by [rpriven](https://github.com/rpriven). Educational and defensive use only — all challenges are public, sanctioned security games.*
