# Microsoft Copilot vs Claude for work: the open-source layer decides

Claude is now sold into Microsoft 365, so the choice between Claude and Microsoft Copilot is no longer a choice between two separate tools. Both vendors sell an assistant that sits in the same apps. What separates them, and what neither hands over, is the layer underneath the assistant: the agent definitions, the permissions and the memory. Kortix is the open-source AI Operating System that puts that layer in a git repo the company owns.

## What Microsoft Copilot is sold as

Microsoft Copilot is an add-on plan, and Microsoft's licensing page still requires one of a long list of qualifying Microsoft 365 subscriptions before a company can buy it ([Microsoft Learn, checked October 2026](https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-licensing)). Copilot Chat comes with an eligible subscription at no extra cost. The add-on sells a Microsoft-hosted AI assistant to the people on those plans.

Copilot Studio is the build surface sold beside it. Microsoft calls it "a platform for creating and managing custom agents, workflows, and apps with no code" and lists 1,500+ data connectors, MCP servers, multi-agent orchestration, a Dev-Test-Prod lifecycle with version control and approval gates, audit logs that flow into Microsoft Purview, and budgets with usage limits ([Copilot Studio product page, checked October 2026](https://www.microsoft.com/en-us/copilot/products/copilot-studio)). That is a serious governance story for anything that stays inside Microsoft's tenant.

## What Claude is sold as

Anthropic sells Claude as a subscription: Free, Pro, Max 5x, Max 20x, Team and Enterprise ([Claude pricing, checked October 2026](https://claude.com/pricing)). The feature table marks "Claude for Microsoft 365", "Claude for Microsoft Outlook" and "Claude in Chrome" as available on Pro, Max, Team and Enterprise, and not on Free.

Claude's Microsoft 365 product is a set of add-ins. Microsoft's marketplace listing describes a sidebar in Excel, PowerPoint and Word that carries context across apps, tracks every cell it changes in a workbook, lands Word edits as tracked changes, and works inside a company's slide master. It is generally available on all paid Claude plans ([Microsoft Marketplace listing, checked October 2026](https://marketplace.microsoft.com/en-us/product/wa200010725)). The Claude subscription is hosted, and its pricing page lists no self-hosted plan.

## Where the two overlap

The overlap is real and recent. A company that already pays for Microsoft 365 can put Claude in the same ribbon where Copilot lives, priced per seat, with no new Microsoft tenant. A company that pays for Claude can add Copilot without removing Claude. For a person editing a document, the two products now compete for the same click.

The overlap stops at the surface. Claude's Microsoft 365 product helps one person work in the file in front of them. Copilot Studio is where an organization defines agents, publishes them into Teams and Microsoft Copilot, and governs a release. Microsoft's Copilot Studio page sells the lifecycle and the audit trail. Anthropic's pricing page sells the seat.

That difference decides what a model change costs. When the assistant is a seat, switching means moving people. When the agent is a definition inside a vendor's tenant, switching means rebuilding the definition. The second cost is the one to price before the pilot ends.

## What each costs

| What you buy | Listed price, checked October 2026 | What it covers |
|---|---|---|
| Microsoft 365 Copilot add-on | $30 per user/month, paid yearly | Assistant in Microsoft 365 apps; needs a qualifying plan |
| Copilot Studio credits | $200 per 25,000-credit pack/month | Agent actions across channels |
| Copilot Studio pay-as-you-go | Metered at the end of the month | Same features, no upfront pack |
| Claude Pro | $20/month, or $17/month billed annually | Claude apps; Microsoft 365 add-ins included |
| Claude Max | From $100/month | 5x or 20x Pro usage |
| Claude Team | $25/seat/month, or $20 annual | Shared workspace; admin controls |
| Claude Enterprise | $20/seat/month annual, 20-seat minimum, plus usage at API rates | SSO, SCIM and audit logs |

Sources: [Microsoft Copilot enterprise pricing](https://www.microsoft.com/en-us/copilot/pricing/enterprise), [Copilot Studio product page](https://www.microsoft.com/en-us/copilot/products/copilot-studio), [Claude pricing](https://claude.com/pricing), all checked October 2026.

A seat and a credit meter measure different things. The Copilot add-on is priced per person, and the qualifying Microsoft 365 plan is a prerequisite, so the real entry cost starts with a subscription a company may already own. Copilot Studio then bills agent work separately. Microsoft sells tenant-wide packs of 25,000 Copilot Credits at $200 per pack per month, offers a pay-as-you-go meter with no upfront commitment, and includes usage of agents published to Microsoft 365 Copilot in the Microsoft 365 Copilot licence ([Copilot Studio product page](https://www.microsoft.com/en-us/copilot/products/copilot-studio)).

Claude prices seats too, and Enterprise puts usage on top at API rates. Team runs from 2 to 150 people, with standard seats at $25 a month or $20 on annual billing and premium seats at $100 or $125. Max is the individual power tier, from $100 a month for five times Pro usage.

Neither bill answers the ownership question. A credit pack is capacity rented from Microsoft. A Claude seat is a subscription rented from Anthropic. In both cases the agent's definition, its grants and its memory sit on the vendor's side of the line.

## What neither vendor hands over

Microsoft is direct about where the agent lives. Its guide to moving Copilot Studio agents onto Entra Agent ID says "Copilot Studio manages the agent code, credentials, and deployment lifecycle" and that there is no automated or in-place migration path for an existing agent identity. The same guide lists "No configuration portability" among the risks: agent topics, knowledge sources, and settings must be manually recreated in the new agent ([Microsoft Entra Agent ID, checked October 2026](https://learn.microsoft.com/en-us/entra/agent-id/migrate-copilot-studio-agents-to-agent-id)). A platform upgrade that stays inside Microsoft already costs a rebuild.

Anthropic's pricing page tells the same story in a quieter way. Memory, skills and connectors are features of a plan. SSO starts at Team; SCIM, audit logs and custom retention at Enterprise. The Microsoft 365 add-ins put Claude in the document, and the account is where the context lives. Nothing on the pricing page describes a file a company can export, diff or run against a different model.

Kortix takes the other side of that line. A Kortix project is a git repo with `kortix.yaml` at its root. Agents, skills, memory, tools, triggers and connectors are files in it ([Kortix docs, checked October 2026](https://kortix.com/docs)). One isolated sandbox per session. Each session has its own isolated machine and branch. The starter manifest says what that means in practice:

```yaml
# Kortix project manifest. Source of truth for project-wide config that
# lives in git alongside the code.
kortix_version: 2

agents:
  kortix:
    file: agents/kortix.md
    connectors: all
    secrets: all
    kortix_permissions: all
    skills: all
```

The excerpt is the header and default agent of the starter file ([starter `kortix.yaml`, checked October 2026](https://github.com/kortix-ai/suna/blob/dev/packages/starter/templates/base/kortix.yaml)). Behavior lives in `agents/kortix.md`. The manifest holds the grants: which connectors, which secrets, which permissions, which skills. A second agent in the same manifest gets no connectors and no secrets because it reads untrusted transcripts, and its comment gives the reason: "nothing to exfiltrate." A grant left out resolves to none.

That file is also the review surface. Session work reaches `main` through a change request. Merge is default-deny for agents. A person reads the diff before the new permission, prompt or connector grant lands. The company keeps the definition, the record and the rollback in one history it can inspect. Open source. Read it, fork it, audit it.

## The decision, in one table

| Decision | Kortix | Microsoft Copilot | Claude |
|---|---|---|---|
| Open source | Yes | No | No |
| Self-host | Yes | No | No listed option |
| Model choice | Any provider, your keys | Models offered in Studio, Microsoft-mediated | Anthropic models |
| Review gate | Change request; merge default-deny for agents | Studio approval gates | Admin controls at Team and Enterprise; no definition review documented |
| Config lives | Files in your git repo | Microsoft tenant | Claude account or workspace |

The row that matters most is the last one. The first four are features a buyer can compare in a meeting. The last one decides what happens on the day the company changes its mind about a model, a vendor or a price.

## Keeping both models

A mixed fleet is the normal outcome. Copilot stays for the people whose work lives in Outlook and Excel. Claude stays for the team that prefers it, or for the tasks where its output fits better. The cost is two seat bills, plus whichever agent meter the work runs on. Kortix supplies the layer both can call.

Kortix is model-agnostic per agent: any model provider with your own keys. A drafting agent can run on one model while a review agent runs on another, and the choice is part of the agent's configuration rather than a workspace-wide setting. Claude access comes in as an Anthropic API key; Kortix does not sign in with a Claude subscription. The subscription paths it supports are ChatGPT and an OpenCode Console account.

The practical effect is that model choice becomes a change a team can test and revert. Run the same task through two agents on two models, compare the diffs, and keep the one that wins. The prompt, the grants and the memory stay put while the model underneath changes.

## What a migration involves

Moving an agent layer out of either vendor means rewriting definitions, then proving the new ones work. Four steps cover most of the work.

1. Inventory the agents, their instructions, knowledge sources and connectors. Microsoft's own guidance says these do not carry over, so the inventory is the migration plan.
2. Write each agent's behavior into an `agents/<name>.md` file and its grants into the manifest. A grant the manifest does not name resolves to none.
3. Move secrets into the project's secret store, never into the repo. The manifest carries names and grants, not values.
4. Connect the channels and run one agent end to end before touching the rest. Keep the old agent alive until the new one has produced work a person has reviewed.

The first agent to move is the one that must leave the vendor boundary, or the one whose model choice matters most. The rest can follow at the pace of review.

## Where to go next

The line-by-line comparison of Kortix and Microsoft Copilot is at [Kortix vs Copilot](https://opensourcecopilotalternative.com/kortix-vs-copilot). Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. [Try Kortix](https://kortix.com).
