# ai-note-taking-app

An AI note-taking application for higher-education lecture capture: record a lecture,
transcribe it, and turn the transcript into study material a student can read, search,
and revise from.

Nothing is built yet. This repository currently holds the project's intent, its
boundaries, and the contract agents follow while working here.

## Why this exists

A student in a lecture is doing three things at once: listening, watching the slides,
and writing. When that is not possible — because of a disability, a language gap, or
simply the pace of the lecture — the notes that come out are thin. The accommodation
that usually replaces them, a person paid to take notes, is expensive for the
university and slow for the student to receive. A plain transcript is not the same
thing as a set of notes a student can study from.

**A missed sentence should not become a lost lecture.** That is the problem this
project exists to close.

A hypothetical example, to make it concrete: a student with a hearing impairment sits
through a long economics lecture. The recording is clear, and a transcript of it exists
by the evening, but the transcript is thousands of words of spoken language with no
structure. What the student needs is the arguments the lecturer made, the definition of
each term, and a way to jump back to the moment where the exam-relevant example was
given. Turning the first artifact into the second is the work this project aims to do.

## What this project is

An application for higher-education lecture capture. It records lecture audio, produces
a timestamped transcript, and turns that transcript into structured study material.

It serves two people:

- **The student**, who studies from the notes and needs them searchable and revisable
  across a term.
- **The university accessibility or disability-services office**, which arranges
  note-taking accommodations and needs a dependable, auditable record that one exists.

What it is not:

- Not a general-purpose consumer note app. It is aimed at the lecture-capture and
  note-taking accommodation market in higher education.
- Not a decision about a university's accommodation policy. Institutions set the rules
  for recording and for student data; the app operates inside them.
- Not a shipped product. There is no implementation in this repository yet, and no
  feature below should be read as existing.

## What you can make or use

All of the following is **planned**, not built:

- A timestamped transcript of a lecture, from in-person or online capture.
- Structured notes generated from that transcript, rather than a flat wall of text.
- Derived study material, such as summaries and question-and-answer sets for revision.
- Notes attached to slides, with a link from a note back to the moment in the audio.
- Stored notes that can be searched and revisited across a term.

The intended reader of the first release is the student; the accessibility office is
the intended buyer.

## How it works

The mechanism below is a plausible pipeline, not a chosen architecture. No design
document has been written and no approach has been benchmarked.

1. Capture the lecture audio, in person or online.
2. Transcribe it into timestamped text.
3. Segment the transcript and generate structured notes from each segment.
4. Derive study material, such as summaries and question-and-answer sets.
5. Tie the notes back to the slides and to the audio moment they came from.
6. Store everything so it can be searched and revisited across a term.

Which capture, transcription, and language-model approach to use — and whether each is
feasible on the target platforms at acceptable cost and accuracy — are open questions.

## Evidence and boundaries

| Claim | What the evidence supports | What it does not establish | Source |
| --- | --- | --- | --- |
| This project targets lecture capture and note-taking accommodations in higher education. | An owner decision recorded when the repository was created. | That the market is reachable, priced correctly, or free of competitors. | Owner statement of goal, 2026-10-09 |
| A capture-to-study-material pipeline is the intended shape. | Nothing yet; it is an open question. | Which approach is feasible, at what cost or accuracy. | No architecture search has been performed |
| No part of the product exists. | The repository contains no implementation. | Nothing about what the product will eventually do. | This repository at the commit you are reading |

Boundaries:

- No numbers appear in this README. Accuracy, latency, pricing, and market-size figures
  stay out until a committed artifact or an external source supports them.
- Lecture recording and student data are handled under the rules the buyer's institution
  sets. This project does not decide those rules.
- Competitor behaviour, where it appears, is described only from public sources.

## Try it

There is nothing to run yet. The smallest useful next step is to read how the project
is framed:

- [`PROJECT.md`](PROJECT.md) — the project contract and its main goal.
- [`.content-system/project-brief.json`](.content-system/project-brief.json) — the
  audience, problem, intended solution, and the boundaries above, in machine-readable
  form.

## Working in this repository

This repository is an adopter of a pinned agent stack: external tools that govern how
work is recorded, validated, and delivered here. Nothing is vendored — each component
is pinned to a certified commit and cloned at validation time.

| Component | Role | Owns |
| --- | --- | --- |
| ACS | Multi-agent hot-loader so concurrent agents share one coordination surface | `.coord/` |
| PCM | Task continuity and progression | `PROJECT.md`, `checkpoints/`, `tasks/`, `HANDOFF.md` |
| Content system | Project brief, brand language, review rubric | `.content-system/` |
| OIO | Issue-log surface and triage | `.oio/`, `.github/ISSUE_TEMPLATE/` |

The certified version set is published by the release train
(`Pukujan/agent-stack-train`) and mirrored in [`stack-manifest.json`](stack-manifest.json).
When one component moves, all four move together.

- [`AGENTS.md`](AGENTS.md) is the operating contract for agents working here.
- [`.github/workflows/acs-gates.yml`](.github/workflows/acs-gates.yml) defines the checks
  that run on every pull request and on every push to `main`. It fails closed: the stack
  manifest is checked against the release train, then the continuity state, the content
  adapter, the hot-loader assignment, and the issue-log surface are each validated in
  turn. `gates` is the required status check on `main`.
- [`.github/workflows/auto-merge.yml`](.github/workflows/auto-merge.yml) arms GitHub's
  native auto-merge on pull requests from the repository owner. A PR merges itself once
  `gates` passes; it only arms auto-merge and never bypasses it.
