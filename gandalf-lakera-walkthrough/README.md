# Gandalf Walkthrough: Defeating a Prompt-Defended LLM

## Table of Contents
- Introduction
- Challenge Structure
- Techniques Used
- Level-by-Level Walkthrough
- Real-World Implications
- Resources & Further Reading

## Introduction

[Gandalf.lakera.ai](https://gandalf.lakera.ai) is an interactive AI security challenge designed to demonstrate the vulnerabilities and defense mechanisms of Large Language Models (LLMs). Created by Lakera, this platform features an AI assistant named "Gandalf" that guards a secret password, challenging users to employ various prompt engineering techniques to extract it.

The challenge premise is straightforward yet profoundly educational: your goal is to devise creative prompts that can convince, trick, or manipulate Gandalf into revealing its secret password. This simulates real-world scenarios where malicious actors might attempt to circumvent AI safeguards to extract sensitive information or bypass content policies.

This writeup aims to document effective strategies for defeating Gandalf's defenses, explain the underlying principles that make these approaches work, and highlight the broader implications for AI safety and security. By understanding how these vulnerabilities can be exploited, developers can better design robust defense mechanisms for their own AI systems.

## Challenge Structure

The Gandalf challenge consists of seven distinct levels (1-7), each progressively more difficult than the last. Each level introduces new defensive mechanisms that Gandalf employs to protect its password, requiring increasingly sophisticated prompt engineering tactics to overcome.

Level 1 starts with basic defenses that can be bypassed with simple techniques, while the later levels incorporate advanced protection mechanisms such as input filtering, content monitoring, instruction priority systems, and context-aware defenses.

The difficulty progression serves as an excellent educational journey through the evolution of prompt injection attacks and defenses in modern LLMs.

Fundamentally, Gandalf works by having two sets of instructions: the visible instructions that users can see, and hidden system prompts that establish the rules and boundaries Gandalf should follow. These prompt defenses act as guardrails, instructing the model to avoid revealing the password regardless of user inputs. The challenge for participants is to find creative ways to circumvent these defenses by crafting inputs that confuse the model, reframe the context, exploit reasoning flaws, or otherwise create scenarios where the model inadvertently reveals the protected information.

## Level-by-Level Walkthrough

- [Level 1: Direct Retrieval](https://github.com/rpriven/ai-ctf-writeups/blob/main/gandalf-lakera-walkthrough/level-1.md)
- [Level 2: Social Engineering](https://github.com/rpriven/ai-ctf-writeups/blob/main/gandalf-lakera-walkthrough/level-2.md)
- [Level 3: Encoding and Obfuscation Bypass](https://github.com/rpriven/ai-ctf-writeups/blob/main/gandalf-lakera-walkthrough/level-3.md)
- [Level 4: Retrieval](https://github.com/rpriven/ai-ctf-writeups/blob/main/gandalf-lakera-walkthrough/level-4.md)
- [Level 5: Retrieval](https://github.com/rpriven/ai-ctf-writeups/blob/main/gandalf-lakera-walkthrough/level-5.md)
- [Level 6: Retrieval](https://github.com/rpriven/ai-ctf-writeups/blob/main/gandalf-lakera-walkthrough/level-6.md)
- [Level 7: Retrieval](https://github.com/rpriven/ai-ctf-writeups/blob/main/gandalf-lakera-walkthrough/level-7.md)

## Real-World Implications
- How these techniques apply to actual AI systems
- Defensive considerations
- Ethical use of these methods

## Resources and Further Reading
- Similar challenges
- Academic papers on prompt injection
- Tools for AI security testing

