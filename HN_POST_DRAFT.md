# HN Post Draft

## Title

Show HN: Railspike — an approval-gated file workflow for AI-assisted feature work

## Body

AI coding assistants can produce changes faster than a team can review their scope, assumptions, and verification. I made Railspike to put small, explicit review gates around feature work without turning it into a large agent framework.

Railspike is a set of Markdown instruction files. An assistant produces a concise assessment when needed, a feature description, and a staged plan; the user explicitly approves each step. Only after Step 3 does implementation begin on a feature branch. The approved planning docs are committed first, and each implementation stage gets its own commit plus an updated verification summary.

The intended audience is people using Codex, Claude Code, or Copilot on feature work where reviewability matters. It adds process, so it is probably excessive for a trivial edit or a one-line fix.

The [quick start](https://github.com/gulkily/railspike#quick-start) covers installation, the first prompt, and the approval loop.

This is not an autonomous-agent framework, a replacement for engineering judgment, or a universal process. It does not prevent hallucinations or guarantee a good design; it makes the decisions, risks, approval points, and verification record easier to inspect.

I would especially value feedback on: are the approval gates useful in practice, where does this feel too rigid, and which assistant integrations would make it more useful?
