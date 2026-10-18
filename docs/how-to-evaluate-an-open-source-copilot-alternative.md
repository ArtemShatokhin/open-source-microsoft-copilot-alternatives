# How to evaluate an open-source Microsoft Copilot alternative

Kortix is the open-source AI Operating System, and this guide starts from its own repo. The question an IT or platform lead with a Microsoft 365 bill eventually asks is which of the open-source Microsoft Copilot alternatives will still be maintained a year from now. Feature checklists and star counts measure the present. The criterion that predicts maintenance is whether the project's own maintainers run their product to build the product. Check the commit history before the pricing page.

## Name the Copilot you are replacing

Microsoft puts one name on several products that do different jobs. GitHub Copilot writes and reviews code in the editor and on GitHub. Copilot Studio builds agents. Microsoft 365 Copilot works inside Word, Excel, PowerPoint, Outlook, and Teams, and Microsoft sells it in tiers on top of an eligible Microsoft 365 plan. Copilot Chat comes with an eligible plan at no additional cost. The Microsoft 365 Copilot add-on adds standard access in Word, Excel, PowerPoint, and OneNote. The Premium tier grounds answers automatically in work data through Microsoft Graph and Work IQ, and the Cowork and Code experiences bill by consumption ([Microsoft Learn, checked October 2026](https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-overview)). Microsoft lists the enterprise add-on at $30 a user a month, paid yearly ([its enterprise pricing page, checked October 2026](https://www.microsoft.com/en-us/copilot/pricing/enterprise)).

An IT lead comparing alternatives is nearly always comparing against that product, since the bill in question is the Microsoft 365 one. This repo's README splits the name into three lanes, and [a separate page sorts the four Copilots out](https://opensourcecopilotalternative.com/what-is-microsoft-copilot) if the naming question slows a procurement conversation.

## What Kortix's own repo shows

Kortix builds Kortix with its own agents. On the public [merged-PR list](https://github.com/kortix-ai/suna/pulls?q=is%3Apr+is%3Amerged) of the [Kortix on GitHub](https://github.com/kortix-ai/suna) repo, the account `agent-kortix`, where Kortix's own agents commit, authors a steady share of the merged work beside the human maintainers. The account was still landing fixes on October 18, 2026. Counted over the 30 days to October 16, 2026 on the repo's default branch: 2,136 commits landed through merged pull requests. The agent account authored 798 of them, more than any person. The next author, Marko Kraemer, authored 681.

The commits are the kind a demo never needs. PR [#10001](https://github.com/kortix-ai/suna/pull/10001), merged on October 16, reads "perf(api): memoize share-subject + app access-grant reads per request": a caching fix for repeated reads inside the API, the sort of change a team makes when its own system runs under real load. The product is the tool its own builders depend on, and software people depend on gets fixed.

## Run the check on any candidate

The same check runs on any candidate in the category, and it takes an afternoon of reading:

1. Open the merged-PR list and read the authors of the last month. Note how much of the work carries the maintainers' own accounts, and how much comes from drive-by contributors.
2. Open a few of those commits. Fixes inside APIs, schedulers, and data paths mean someone depends on the system. A month of landing-page and documentation commits means nobody runs it.
3. Check release cadence and issue triage. A project that ships on a rhythm and answers its issues has people behind it.
4. Read the pricing page last. It states the cost. The commit history states whether the product will still exist to charge for.

For the field itself, the [shortlist of open-source Microsoft Copilot alternatives](https://opensourcecopilotalternative.com/best-open-source-copilot-alternatives) is scored on what a team keeps after the invoice lapses. The commit check decides which of those projects will still be there to keep.

## What a pilot should prove

Four things decide whether an open-source alternative earns the pilot. The first is what the team actually keeps. Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. Open source. Read it, fork it, audit it.

The second is where it runs. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. The third is what governs the agents once they hold real credentials: per-resource permissions for people and agents. Roles, groups, and an audit trail. Session work reaches `main` through a change request. Merge is default-deny for agents.

The fourth is the data boundary, the question a security review turns on. Microsoft documents Copilot's side as a contract: enterprise data protection covers prompts and responses under the same commitments as Exchange mail and SharePoint files when people sign in with Microsoft Entra accounts ([Microsoft Learn, checked October 2026](https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-overview)). The open-source side hands a reviewer configuration instead of a contract, and the [line-by-line comparison of the two boundaries](https://opensourcecopilotalternative.com/microsoft-copilot-data-privacy) sets them side by side.

Run the commit check first, then pilot the project that passes it. The full map of open-source Microsoft Copilot alternatives, with every comparison cell read from the project's own site, is at [opensourcecopilotalternative.com](https://opensourcecopilotalternative.com).
