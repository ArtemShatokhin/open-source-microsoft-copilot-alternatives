# Agent management at org scale comes down to who owns the repo

Agent management at org scale is running many agents across a company while staying able to say who may reach what, what each one did, and where the rules live, and the open-source route to it begins with one question: who owns the repo? On Microsoft's Copilot stack the answer is Microsoft; on an open-source route it is you, and the difference shows up in three places.

## What agent management at org scale means

Microsoft Copilot Cowork is an AI-powered agentic system that carries out multi-step tasks across Microsoft 365, and "you approve each action before it happens" ([Copilot Cowork overview, Microsoft Learn, checked October 2026](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork)). The unit of control is one person's session.

Org-scale management asks a different one: which agent may reach which system, who reviews the work before it lands, and where does the record live? Microsoft's answers live in two admin surfaces. Agents built in Copilot Studio are managed in the Agent Registry of the Microsoft 365 admin center, where an admin can "enable, disable, assign, block, or remove agents for your organization" ([manage agents, Microsoft Learn, checked October 2026](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps)). Power Platform data policies govern what those agents may reach; maker audit logs land in Microsoft Purview, and agent activity is watched in Sentinel ([Copilot Studio security and governance, checked October 2026](https://learn.microsoft.com/en-us/microsoft-copilot-studio/security-and-governance)).

## The three locations that decide governance

Governance in this lane comes down to three locations: where agent definitions live, where credentials live, and where the work record lives. Whoever holds those three holds the governance, whatever the console offers.

In Microsoft's stack the platform holds the definitions. Microsoft's guide for moving agents to Entra Agent ID states that "Copilot Studio manages the agent code, credentials, and deployment lifecycle" ([Microsoft Entra Agent ID, Microsoft Learn, checked October 2026](https://learn.microsoft.com/en-us/entra/agent-id/migrate-copilot-studio-agents-to-agent-id)). In an open-source setup the definition is a file. A Kortix project is a git repo with `kortix.yaml` at its root, and an agent is a markdown file plus a governance block in that manifest ([Kortix docs](https://kortix.com/docs), [starter manifest](https://github.com/kortix-ai/suna/blob/dev/packages/starter/templates/base/kortix.yaml)).

Credentials are equally plain: the same guide's comparison table reads "Copilot Studio manages credentials on your behalf" ([Microsoft Entra Agent ID](https://learn.microsoft.com/en-us/entra/agent-id/migrate-copilot-studio-agents-to-agent-id)). OpenWork, a desktop alternative built on OpenCode, keeps keys with the person: your own API key or local models, with shared connections configured in Den, its team control plane ([OpenWork's repository, checked October 2026](https://github.com/different-ai/openwork)). Kortix draws the line where a reviewer can check it: connector credentials are brokered server-side and never enter the machine ([Kortix docs](https://kortix.com/docs)).

The work record is what an audit asks for later. Microsoft writes agent activity into its own compliance services, Purview and Sentinel ([Copilot Studio security and governance](https://learn.microsoft.com/en-us/microsoft-copilot-studio/security-and-governance)). Kortix keeps two: commits and change requests in git history you own, plus the runtime's record beside them. Per-resource permissions for people and agents. Roles, groups, and an audit trail.

## The three locations, side by side

| What decides governance | Kortix | Microsoft's Copilot stack | OpenWork |
|---|---|---|---|
| Where definitions live | Files in the repo you own, reviewed as diffs | Platform-managed; agents listed in the admin-center registry | Local workspace files; capabilities shared through Den |
| Where credentials live | Brokered server-side; they never enter the machine | Copilot Studio manages credentials on your behalf | Your own API keys; shared connections in Den |
| Where the work record lives | Git history you own, beside the audit trail | Audit logs in Purview and Sentinel | On the person's desktop; Den is the team control plane |

The build-or-buy decision in this lane is which places you want the three in.

## What owning the repo looks like day to day

The git log of the repo Kortix builds itself from shows the model running at scale: [Kortix on GitHub](https://github.com/kortix-ai/suna). Over the 30 days to October 16, 2026, 787 of the 2,085 commits that landed on the trunk were authored by Kortix Agent, the account Kortix's own agents commit under (`agent@kortix.ai`). No person wrote more. The next author, Marko Kraemer, wrote 665. Counted from the public history: first-parent commits on the `dev` trunk, reproducible by any reader.

A demo never needs a caching fix inside its own API. Pull request [#10001](https://github.com/kortix-ai/suna/pull/10001), merged on October 16, reads "perf(api): memoize share-subject + app access-grant reads per request," authored by the same agent account. An agent workforce that size leaves a commit log, and the log doubles as the management surface.

Session work reaches `main` through a change request, and merge is default-deny for agents. A person reads each diff before it lands, including a proposal an agent makes about its own instructions.

Least privilege is per agent: a markdown file for behavior, plus separate grants for connectors, secrets, permissions, and skills in each agent's own block. The starter manifest shows both ends: its default agent is granted everything, and its second agent, the harness-reflector, holds the widest permission grant with no connector or secret grant at all, because it reads untrusted transcripts. Its comment gives the reason: "nothing to exfiltrate" ([the starter manifest](https://github.com/kortix-ai/suna/blob/dev/packages/starter/templates/base/kortix.yaml)). A grant left out resolves to none.

The grants are lines in a file anyone with repo access can open, and a bad rule is reverted like any other commit. Governance you can inspect before the first agent runs: that is what the open-source claim buys here.

## When a hosted stack is still the right call

If your data, identities, and compliance already live in Microsoft 365, and admins already run Entra, Purview, and Sentinel, Microsoft's controls are enforced by people you pay for today. Microsoft Agent 365 requires a license for each person, per its own documentation ([Microsoft Entra Agent ID](https://learn.microsoft.com/en-us/entra/agent-id/migrate-copilot-studio-agents-to-agent-id)). For an organization with no one to run its own repo, the trade is reasonable.

The trade costs the same three locations. Agent definitions become platform-managed code, so a platform change means recreating agents. Credentials become something Microsoft's docs tell you not to inspect or manage. The work record becomes audit logs you query through Microsoft's compliance services, at whatever depth they expose. None of that is a defect in the hosted product; it is the cost of keeping the three locations on someone else's side.

## Where to go next

The policy-as-git model, agent by agent, is worked through on [the Copilot agent management page](https://opensourcecopilotalternative.com/copilot-agent-management). [The Microsoft Copilot for Teams page](https://opensourcecopilotalternative.com/microsoft-copilot-for-teams) takes the same idea to the place people already work. Kortix is the open-source AI Operating System, and in this lane the repo is where its governance lives. [Try Kortix](https://kortix.com).
