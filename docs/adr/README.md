# Architecture Decision Records (ADR)

## Why ADRs exist

Every meaningful technical decision in this project is recorded as an ADR. An ADR
answers five questions (Law of Traceability in `docs/mentor-constitution.md`):

- Why does it exist?
- What problem does it solve?
- What alternatives existed?
- Why was this solution chosen?
- What would happen if it disappeared?

Interviewers love ADRs: they prove you did not copy a tutorial — you made **decisions**.

## When to write one

Write an ADR when you (or the mentor) make a decision that:

- changes how the project works (e.g., moving Git earlier),
- introduces or removes a tool (e.g., Docker, UFW, Oracle Cloud Free Tier),
- chooses between valid alternatives (e.g., GitHub Actions vs GitLab CI),
- has lasting consequences for the repository or the server.

Do **not** write an ADR for routine tasks ("installed a text editor").

## Index

| # | Status | Title |
|---|---|---|
| 0001 | Accepted | [Version control from day one](0001-version-control-from-day-one.md) |
| 0002 | Accepted | [Mirror repositories on GitHub and GitLab](0002-mirror-repos-github-gitlab.md) |
| 0003 | Accepted | [Zero-cost cloud strategy](0003-zero-cost-cloud-strategy.md) |
| 0004 | Accepted | [Professional DevOps Junior curriculum](0004-professional-devops-junior-curriculum.md) |

## Naming & workflow

1. Copy `_template.md` → `NNNN-short-description.md` (zero-padded number).
2. Fill in the sections.
3. Update the index table above.
4. Reference the ADR from the lab document where the decision happens.
5. It becomes part of the session commit.

> Decisions can be **Proposed → Accepted → Superseded**. Superseding an ADR requires a
> new ADR that references the old one.
