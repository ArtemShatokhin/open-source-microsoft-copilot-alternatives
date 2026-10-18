# Open-source Copilot Studio alternatives for agents that leave Microsoft

If your Copilot Studio agents keep hitting the edge of the Microsoft ecosystem, the open-source Copilot Studio alternatives split on one point. Who owns the agent's definition, its credentials and its runtime after the move? Copilot Studio builds agents inside Microsoft 365. The switch becomes a platform decision the moment agents act outside Microsoft, and there the credits, credentials and runtime change hands. Keep Copilot Studio while the work stays inside Microsoft 365. Once the agent's center of gravity moves outside, pick the platform that keeps those three on your side of the line. In the open-source field, Kortix is that platform, Botpress is the hosted studio equivalent, LangGraph and LangChain are the libraries underneath, and Vellum Assistant is a personal runtime.

## What Copilot Studio does well

Microsoft Copilot Studio is Microsoft's graphical, low-code studio for building and managing AI-powered agents and workflows. It publishes them into Microsoft Teams, Microsoft Copilot, websites and mobile apps ([Microsoft Learn, checked October 2026](https://learn.microsoft.com/en-us/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)). The product page adds 1,500+ pre-built data connectors, MCP servers, multi-agent orchestration, and a dev-test-prod lifecycle with version control and approval gates ([product page, checked October 2026](https://www.microsoft.com/en-us/copilot/products/copilot-studio)).

The billing is consumption. Agents consume Copilot Credits. Microsoft's licensing guidance defines them as "a measure of the time and effort required for an agent to retrieve information, respond to prompts, and perform tasks through actions". The decrement depends on task complexity ([licensing guidance, checked October 2026](https://www.microsoft.com/licensing/guidance/microsoft-copilot-studio)). Three numbers matter. A Copilot Studio license costs $200 per pack per month, billed annually. One pack is 25,000 Copilot Credits a month, and unused credits do not roll over. The pay-as-you-go meter bills $0.01 per credit with no up-front commitment. The Copilot Studio User License for people building and managing agents is $0.

## Where the boundary bites

Teams call the problem "too limited outside the Microsoft ecosystem." The limit is the boundary itself, not one missing feature. A Copilot Studio agent runs as a service in Microsoft's cloud, holds its configuration in Microsoft's tenant, and bills every action in Copilot Credits. Inside Microsoft 365 that design is an advantage.

Move the agent's work outside that world and the same design reads differently. Actions against systems Microsoft does not host consume credits just the same. The guidance counts actions, workflows and custom skills wherever they lead. Credentials for those systems pass through Microsoft's platform, and the runtime stays Microsoft's. Data residency, model choice and capacity become decisions you negotiate instead of files you set.

That is when a studio becomes a platform decision. Two studios can match on features and stop matching where ownership splits.

## What each open-source alternative hands you

| Option | What it hands you | Where it runs | License |
|---|---|---|---|
| Kortix | Agents, skills, memory and connectors in one git repo you own | Kortix Cloud, your VPC, or on-prem | Open source |
| Botpress | A hosted studio; the MIT repo holds integrations and dev tools | Botpress Cloud; v12 self-hostable | MIT (repo); AGPL-3.0 (v12) |
| LangGraph / LangChain | Orchestration libraries for your own application | Your own app and infrastructure | MIT |
| Vellum Assistant | A runtime for one personal assistant | Managed on Vellum Platform, or self-hosted | MIT |

**Kortix** is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers ([Kortix on GitHub](https://github.com/kortix-ai/suna)). This repository's three-lane map puts Kortix in lane 3, agent management at org scale. In this lane its row rests on a narrower fact: the agent is files. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. Any model provider with your own keys. Session work reaches `main` through a change request, and merge is default-deny for agents.

**Botpress** is the closest structural match in this lane. Its repository calls it "the open-source hub to build & deploy GPT/LLM Agents", and the product includes Botpress Studio, its hosted studio for conversational agents ([botpress/botpress, checked October 2026](https://github.com/botpress/botpress)). The catch is the repository: its code is integrations, the CLI and SDK, and example bots. Building bots in code that way "is in no way a replacement for the Botpress Studio". The self-hostable v12 line is a separate repository under AGPL-3.0, last pushed in April 2025 ([botpress/v12](https://github.com/botpress/v12)). Botpress's homepage now leads with customer-support agents and a helpdesk product ([botpress.com, checked October 2026](https://botpress.com)).

**LangGraph and LangChain** are libraries. LangGraph is a low-level orchestration framework for building, managing, and deploying long-running, stateful agents. LangChain is the companion framework that standardizes model providers, tools and retrievers behind it ([langgraph](https://github.com/langchain-ai/langgraph), [langchain](https://github.com/langchain-ai/langchain), both checked October 2026). Both repositories are MIT and shipping; LangGraph's 1.2.16 release landed on October 16, 2026. The overlap with Copilot Studio is the orchestration layer itself, and LangGraph's README names durable execution, human-in-the-loop oversight and memory among its features. The visual prototyping surface in the ecosystem, LangSmith Studio, belongs to LangChain's commercial LangSmith product. A team that needs a canvas needs a different row.

**Vellum Assistant** is a personal AI assistant, and its README describes one. It "evolves with you", carries eight memory types, and reaches you on macOS, Windows, iOS, Slack, Telegram and email ([vellum-ai/vellum-assistant, checked October 2026](https://github.com/vellum-ai/vellum-assistant)). It is MIT, runs as a managed runtime on the Vellum Platform or self-hosted, and it connects Anthropic, OpenAI, Gemini and local models through Ollama. As a Copilot Studio equivalent it does not qualify: the unit it builds and governs is one person's assistant, not a studio where a team designs and publishes business agents.

## What owning the agent changes

Ownership shows up in files. The starter manifest in the Kortix repository says so in its own header. It is the "source of truth for project-wide config that lives in git alongside the code." Agent behavior, "description, model, mode, temperature, permission, the prompt itself", lives entirely in the agent's `.md` file ([the starter manifest](https://github.com/kortix-ai/suna/blob/dev/packages/starter/templates/base/kortix.yaml)). In Copilot Studio the agent is configuration inside Microsoft's tenant and executes on Microsoft's cloud. In a file-based platform it is a file your team can diff and restore.

Migration from Copilot Studio is a rebuild. The studio holds the definitions, so the work is re-stating each agent's instructions, topics, knowledge sources and connections in the new platform's format, then pointing the same channels at the new runtime. Move one agent first: the one that must leave the Microsoft boundary.

## Where to look next

The [full lane-2 comparison of open-source Copilot Studio alternatives](https://opensourcecopilotalternative.com/copilot-studio-alternatives) keeps the table current. The [line-by-line Copilot Studio vs Kortix comparison](https://opensourcecopilotalternative.com/copilot-studio-vs-kortix) works through the boundary question cell by cell. If your agents' center of gravity has already crossed the line, [try Kortix](https://kortix.com).
