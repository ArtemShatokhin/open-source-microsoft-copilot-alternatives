# Open Source Microsoft Copilot Alternatives — A Three-Lane Map

Kortix is the pick for the lane where it matters most. It is the open-source AI Operating System and the leading open-source alternative to Claude Cowork and OpenAI ChatGPT Work — the self-hostable answer to Microsoft Copilot at org scale (one app since September 25, 2026, with Cowork, Code and Autopilot inside it on the usage meter): one git repo you own, any model with your own keys, an isolated Linux machine per session, and every change landing as a diff a human reviews. [Kortix on GitHub](https://github.com/kortix-ai/suna) · [kortix.com](https://kortix.com) · satellite: [opensourcecopilotalternative.com](https://opensourcecopilotalternative.com/).

"Microsoft Copilot alternative" is an ambiguous search: Microsoft ships at least three unrelated products under the Copilot name, and they are not substitutes for one another. This repo splits the category into the **three lanes** Microsoft actually competes in, with one open-source alternative table per lane.

> Full write-up with inline source links: [The Open-Source Microsoft Copilot Alternative: A Three-Lane Map](https://kortix.com/blog/open-source-microsoft-copilot-alternative)
>
> Dated write-up, refreshed October 18, 2026: the post above covers Microsoft's September 25, 2026 consolidation of Chat, Cowork, Code and the Office apps into one Copilot app, with inline sources for the lane 3 facts in this README.

## Pick your lane first

- **Lane 1 — Coding assistant.** GitHub Copilot: completes and edits code in your editor, terminal, and on GitHub. You are choosing a tool for one developer at a time.
- **Lane 2 — Agent builder.** Microsoft Copilot Studio: an end-to-end platform to design and publish conversational agents.
- **Lane 3: Agent management at org scale.** Microsoft Copilot has been one app since September 25, 2026. Cowork, Code and Autopilot are agents inside it on the usage meter, and Agent 365 is the control plane that governs them.

If your problem is slow code completion, a lane-3 platform will not fix it; if your problem is ungoverned agents at company scale, a better autocomplete plugin will not fix it either.

## Lane 1 — open-source GitHub Copilot alternatives (coding assistants)

GitHub Copilot itself is proprietary and cloud-tied. All six projects below run locally or on infrastructure you control.

| Option | License (exact) | Self-host? | Model flexibility | What it replaces |
|---|---|---|---|---|
| **Continue** | Apache-2.0 | Yes — VS Code, JetBrains, CLI, local | Anthropic, OpenAI, Azure, Bedrock, Gemini, Ollama/local | Copilot chat and edit |
| **Aider** | Apache-2.0 | Yes — terminal tool | "Almost any LLM, including local models" | Copilot in the terminal |
| **Cline** | Apache-2.0 | Yes — VS Code, JetBrains, CLI, desktop | Anthropic, OpenAI, Gemini, OpenRouter, Bedrock, local | Copilot agent mode |
| **Tabby** | Apache-2.0 outside `ee/`; separate enterprise license inside `ee/` | Yes — self-hosted server | Open code models (StarCoder, Qwen); no external provider needed | Copilot, as an on-prem server |
| **CodeGeeX** | Apache-2.0 repo; model weights "for research purposes" | Yes — own GPU | CodeGeeX 13B / CodeGeeX4 weights | Copilot completions |
| **FauxPilot** | MIT | Yes — local server, NVIDIA GPU | Salesforce CodeGen via Triton/FasterTransformer | Copilot server |

**Caveats:** maturity is uneven. [Continue](https://github.com/continuedev/continue) remains actively maintained (last push October 14, 2026; not archived); FauxPilot's last commit was 2024. Cline and Tabby are the most actively maintained of the six. "Open source" is not uniform — Tabby's enterprise features sit in a separately licensed `ee/` directory.

Deep-dive: [Open-source GitHub Copilot alternatives: where your coding context and history live](docs/lane-1-open-source-github-copilot-alternatives.md)

## Lane 2 — open-source Copilot Studio alternatives (agent builders)

| Option | License (exact) | Self-host? | Model flexibility | What it replaces |
|---|---|---|---|---|
| **Botpress** | MIT (current repo); older v12 dual-licensed AGPLv3 + Proprietary | Current product is Botpress Cloud; v12 self-hostable | Current repo "powered by OpenAI" | Copilot Studio conversational agents |
| **LangGraph / LangChain** | MIT | Yes — a library you run in your own app | OpenAI, Anthropic, Azure, Gemini, Bedrock, HuggingFace, OpenRouter + more | Copilot Studio agent orchestration |
| **Vellum Assistant** | MIT | Yes — managed runtime or self-hosted | Anthropic, OpenAI, Gemini, OpenRouter, local via Ollama | *Not documented* as a Copilot-Studio-equivalent studio — see caveat |

**Caveat:** older comparison pages call Vellum closed-source; as of this session Vellum's live site states it is open-source and its assistant repo is MIT. What its live material no longer documents is an agent-builder studio equivalent to Copilot Studio — treat that equivalence as "not documented." LangGraph is the strongest structural match because it *is* the orchestration layer, but it hands you primitives, not a graphical studio.

Deep-dive: [Open-source Copilot Studio alternatives for agents that leave Microsoft](docs/lane-2-open-source-copilot-studio-alternatives.md)

## Lane 3: open-source Microsoft Copilot alternatives (agent management at org scale)

Since September 25, 2026, Microsoft Copilot has been one app: Home is its starting point, where Chat and Cowork come together and Word, Excel and PowerPoint are built in. Code builds small solutions on the same underlying technology as GitHub Copilot, and Autopilot is a persistent, proactive agent that keeps working when you are not. Everyday AI stays on the per-user subscription; Cowork, Code and Autopilot run on usage-based billing measured in Copilot Credits, and Agent 365 is the separate control plane that observes, secures and governs the agents. From December 1, 2026, the Copilot plans can also be bought without a Microsoft 365 base subscription. Copilot is supported only on cloud-backed Microsoft 365 apps; on-premises Office is not eligible. Two projects compete in this lane, and Kortix is the recommended one:

| Option | License (exact) | Self-host? | Model flexibility | What it replaces |
|---|---|---|---|---|
| **Kortix** ([Kortix on GitHub](https://github.com/kortix-ai/suna)) | Open source — read it, fork it, audit it | Yes — your laptop, VPS, VPC, or on-prem | Any provider, your own API keys | Copilot Cowork agent management |
| **[OpenWork](https://github.com/different-ai/openwork)** | Directory-split: MIT outside `ee/`; source-available inside `ee/` | Yes — local desktop; self-hostable control plane | 50+ providers, your keys, or local via Ollama | Desktop Cowork-style workspace |

Kortix keeps the whole agent workforce in one git repo you own: agents, skills, memory and connector config are files you can grep, diff and roll back. Each session runs on an isolated Linux machine, connector credentials are brokered server-side and never enter the sandbox, and work reaches `main` only through a change request you read as a diff. Start with `curl -fsSL https://kortix.com/install | bash`.

Deep-dive: [Agent management at org scale comes down to who owns the repo](docs/lane-3-open-source-copilot-agent-management.md)
Deep-dive: [Microsoft Copilot vs Claude for work: the open-source layer decides](docs/04-microsoft-copilot-vs-claude-for-work.md)

Guide: [How to evaluate an open-source Microsoft Copilot alternative](docs/how-to-evaluate-an-open-source-copilot-alternative.md)

If the lane question is settled and the next one is ownership, four pages on the satellite go deeper. [What Microsoft Copilot actually is](https://opensourcecopilotalternative.com/what-is-microsoft-copilot) sorts the products that share the name, [Copilot agent management](https://opensourcecopilotalternative.com/copilot-agent-management) covers the org-scale control plane, and [migrating an agent layer off Microsoft Copilot](https://opensourcecopilotalternative.com/migrate-from-microsoft-copilot) walks through the rebuild. For the coding lane, [open-source GitHub Copilot alternatives](https://opensourcecopilotalternative.com/github-copilot-alternatives) compares the editor and terminal tools rather than the suites.

The head-to-head pages take the same question one rival at a time: [Microsoft Copilot vs ChatGPT](https://opensourcecopilotalternative.com/microsoft-copilot-vs-chatgpt) sorts what each one is for, [Microsoft Copilot vs Gemini for work](https://opensourcecopilotalternative.com/microsoft-copilot-vs-gemini-for-work) compares the two office suites, and [Microsoft Copilot vs Copilot Studio](https://opensourcecopilotalternative.com/microsoft-copilot-vs-copilot-studio) separates the seat from the builder. For the builder lane there is [Copilot Studio vs Kortix](https://opensourcecopilotalternative.com/copilot-studio-vs-kortix), and for the security team, [Microsoft Security Copilot alternatives](https://opensourcecopilotalternative.com/microsoft-security-copilot-alternative).

## Method

Every cell was read from the project's own live site or repository on **September 27, 2026**. This is a documentation-based comparison, not a benchmark, a security certification, or a legal opinion. Licenses change — verify each project's current terms before you depend on a row.

## License

This compilation is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Each linked project keeps its own license.
