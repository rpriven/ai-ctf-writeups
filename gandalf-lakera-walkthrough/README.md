# Gandalf Walkthrough: Defeating a Prompt-Defended LLM

## Table of Contents
- [Introduction](#introduction)
- [Challenge Structure](#challenge-structure)
- [Techniques Used](#techniques-used)
- [Level-by-Level Walkthrough](#level-by-level-walkthrough)
- [Real-World Implications](#real-world-implications)
- [Resources & Further Reading](#resources--further-reading)

## Introduction

[Gandalf.lakera.ai](https://gandalf.lakera.ai) is an interactive AI security challenge designed to demonstrate the vulnerabilities and defense mechanisms of Large Language Models (LLMs). Created by Lakera, this platform features an AI assistant named "Gandalf" that guards a secret password, challenging users to employ various prompt engineering techniques to extract it.

The challenge premise is straightforward yet profoundly educational: your goal is to devise creative prompts that can convince, trick, or manipulate Gandalf into revealing its secret password. This simulates real-world scenarios where malicious actors might attempt to circumvent AI safeguards to extract sensitive information or bypass content policies.

This writeup documents effective strategies for defeating Gandalf's defenses, explains the underlying principles that make these approaches work, and highlights the broader implications for AI safety and security. By understanding how these vulnerabilities can be exploited, developers can better design robust defense mechanisms for their own AI systems.

## Challenge Structure

The Gandalf challenge consists of seven distinct levels (1–7), each progressively more difficult than the last. Each level introduces new defensive mechanisms that Gandalf employs to protect its password, requiring increasingly sophisticated prompt engineering tactics to overcome.

Level 1 starts with basic defenses that can be bypassed with simple techniques, while the later levels incorporate advanced protection mechanisms such as input filtering, content monitoring, instruction priority systems, and context-aware defenses.

Fundamentally, Gandalf works by having two sets of instructions: the visible instructions that users can see, and hidden system prompts that establish the rules and boundaries Gandalf should follow. These prompt defenses act as guardrails, instructing the model to avoid revealing the password regardless of user inputs. The challenge is to find creative ways to circumvent these defenses — inputs that confuse the model, reframe the context, exploit reasoning flaws, or otherwise create scenarios where the model inadvertently reveals the protected information.

## Techniques Used

A running glossary of the techniques applied across the levels. Each is a general prompt-injection primitive, not a Gandalf-specific trick — they recur throughout LLM security testing.

| Technique | What it does |
|-----------|--------------|
| **Direct request** | Simply ask for the protected data. The baseline; works only against undefended models. |
| **Implied familiarity** | Speak as though the secret was already shared ("thanks for your help!"), exploiting the model's lack of true conversation memory and its drive for conversational coherence. |
| **False presupposition** | Embed the disclosure as an assumed fact the model then plays along with. |
| **Encoding / obfuscation** | Ask for the secret transformed — leetspeak, ROT13, base64 — to slip past filters that only match the literal string. |
| **Sequential (character-by-character) extraction** | Request the secret one letter or chunk at a time so no single response trips a "contains the password" check. |
| **Statelessness exploitation** | Exploit that the defender (filter/censor model) evaluates each response in isolation while the attacker accumulates state across turns. |
| **Indirect inference** | Never ask for the secret — ask for a riddle whose answer *is* the secret, then ask for the answer. Intent-detection misses it because no request looks malicious. |
| **Keyword-filter evasion** | Encode trigger words ("p4ssw0rd") so an input filter blocking the literal term still passes the prompt through. |
| **Layer misdirection** | Bury the extraction inside an unrelated creative task (e.g. an acrostic poem) so the true objective is obscured from both input and output checks. |

## Level-by-Level Walkthrough

- [Level 1: Direct Retrieval](./level-1.md)
- [Level 2: Social Engineering](./level-2.md)
- [Level 3: Encoding and Obfuscation Bypass](./level-3.md)
- [Level 4: Sequential Information Extraction](./level-4.md)
- [Level 5: Encoding-Based Prompt Injection](./level-5.md)
- [Level 6: Indirect Inference and Riddle Solving](./level-6.md)
- [Level 7: Multi-Layered Defenses and Advanced Prompt Engineering](./level-7.md)

> **Level 8 (Gandalf the White v2.0):** the bonus level, combining every prior defense. Writeup in progress — see [Resources](#resources--further-reading) to try it yourself in the meantime.

## Real-World Implications

Every level of Gandalf is a compressed lesson in a defense pattern that appears in production AI systems — and why each one, used alone, fails.

- **"Instruction-only" guardrails are not security (Levels 1–2).** Telling a model "don't reveal X" is a suggestion, not a boundary. Any system that relies on a system prompt as its *only* control over sensitive data is one clever reframing away from disclosure. Treat the model as untrusted with anything it's merely *told* to protect.
- **String-matching filters protect the representation, not the secret (Levels 3, 5).** A post-generation filter that blocks the literal password does nothing against encodings, ciphers, or character-by-character spelling — the model still *knows* the secret and will happily transform it. Output filtering must operate on meaning, not exact strings, and even then it is a backstop, not a primary control.
- **Stateless moderation loses to stateful attackers (Level 4).** When a censor model judges each response independently, an attacker who accumulates information across turns wins. Defenses need conversation-level accounting of *cumulative* disclosure, not per-message checks.
- **Intent detection ≠ information-flow control (Level 6).** A guard that asks "is the user trying to extract the secret?" misses attacks where no individual message looks malicious (ask for a riddle, then its answer). You have to reason about what the system's *outputs* can be combined to reveal, not just what the input appears to want.
- **Defense-in-depth raises cost, not certainty (Level 7).** Stacking every filter together makes attacks harder and more expensive — the realistic goal — but a determined attacker chaining misdirection and incremental extraction still gets through. Design assuming the guardrail will eventually be beaten; minimize what a successful extraction actually exposes.

**The through-line for builders:** never put data in a model's context that would cause real harm if disclosed, unless an *external* control (not the model's own compliance) makes disclosure impossible. Prompt-level defenses raise the cost of an attack; they do not close it.

## Resources & Further Reading

- [Gandalf by Lakera](https://gandalf.lakera.ai) — try the challenge yourself
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — LLM01 is Prompt Injection
- [Lakera: "Who is Gandalf?"](https://www.lakera.ai/blog/who-is-gandalf) — the creators on how the game works and what they learned
- [MITRE ATLAS](https://atlas.mitre.org/) — adversarial threat landscape for AI systems
- [Simon Willison on prompt injection](https://simonwillison.net/series/prompt-injection/) — ongoing analysis of why this class of attack is hard to fix

---
*Educational and defensive use only. Gandalf is a public, sanctioned security game created by Lakera.*
