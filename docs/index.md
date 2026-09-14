---
title: AI Systems Engineering
layout: default
---

# AI Systems Engineering

**A master's course on the system, not the model.** One three-hour block a week for
fourteen weeks, built for working professionals. This page describes the course as it
is designed. Semester-specific material lives in a separate repository each term.

**Current offering:** [Fall 2026](https://github.com/aise-stthomas/f2026)

---

## What the course is about

Most AI projects fail somewhere between the demo and the second month in production.
Not because the model was bad, but because the system around it was built on
assumptions that classic software engineering takes for granted and AI systems violate.

> Classic software engineering assumes components meet a specification. AI components
> are stochastic, their specification lives in data rather than code, they drift
> without anyone editing them, and they now take actions in the world. AI Systems
> Engineering is the discipline of building reliable systems out of parts like that.

Its subject is what changes when a component is stochastic rather than merely buggy,
when the specification lives in data rather than code, when the system decays without
anyone editing it, and when the component takes actions on your behalf.

You will measure, ship, make agentic, break, secure, and operate one live system over
the semester, a support-ticket triage and resolution agent, replacing its parts with
your own as the course teaches them. You will also learn to design an AI system out
loud, under time pressure, against an explicit rubric: the skill a design review
demands, and the one a design interview measures.

**The editorial gate.** Every topic must answer: *what is different about this because
there is a model in the loop?* If the answer is "nothing," it is a prerequisite, not a
lecture. The full argument is in the [course thesis](course-thesis.md).

## The five differences

1. **The component is stochastic, not buggy.** There is no fix, only a shifted
   distribution. Testing becomes evaluation; every requirement becomes a rate.
2. **The specification lives in data, not code.** The prompt, the retrieved context,
   the tool descriptions, and weights you likely do not control are the spec, and they
   need the versioning, contracts, and provenance that code already has.
3. **The system is non-stationary, and partly not yours.** The world drifts, the users
   adapt, and the vendor changes the model under you.
4. **Familiar engineering tools are used differently.** Queues, tracing, CI, and
   orchestration all change shape when inference is slow, expensive, and probabilistic.
5. **Agent engineering is genuinely new.** The loop, tool dispatch, durable execution,
   three-party authorization, and containment have no classic-software analogue.

## Who it is for

Working professionals in a master's program, hybrid: roughly half in the room, half
online, in the same block. The course assumes you have a job where some of this will be
useful on Monday, and that your time is genuinely scarce.

- **Prerequisites.** Comfortable Python. The command line. Have trained or called a
  model before. Can read an HTTP API.
- **Not required.** A software engineering background, distributed systems, or any
  cloud, container, or orchestration experience. The Systems Toolkit primers close
  those gaps, and the project scaffold supplies the infrastructure.
- **Workload cap.** Five hours a week outside class: about 1.5 hours of reading and
  3.5 hours of project work. If you are consistently over, that is a bug in the course.
- **Cost to you.** Nothing. Projects run on a course-provided cloud lab account and a
  free-tier model API.

## What you will be able to do

1. **Design** an AI system end to end against explicit requirements, and defend the
   design in a review, including passing an AI system design interview.
2. **Reason about stochastic components** as a distribution rather than a defect, and
   build systems that remain correct while a component is wrong.
3. **Build an evaluation harness** with slices, a measured noise floor, and a validated
   judge, for single-shot models and for multi-step agent trajectories, and gate a
   release on it.
4. **Treat data and context as engineering artifacts** with contracts, provenance, and
   consistency guarantees.
5. **Explain and implement the agent mechanism from scratch**: the loop, tool dispatch
   over a real capability protocol, context management, durable execution, without a
   framework.
6. **Reason about the integration and trust layer**: discovery, description,
   invocation, versioning, and three-party authorization, with current protocols as
   instances rather than the subject.
7. **Threat-model and harden an agentic system**, including prompt injection, the
   confused-deputy problem, and containment.
8. **Operate a live AI system**: trace it, detect drift, define SLOs on a probabilistic
   system, and run an incident.

## The design framework

Introduced in the first week, used every week, and the rubric for both exams. Each
step has four published level descriptors in the [design review rubric](rubric.md), and
the [reference design](reference-design.md) shows all seven steps at level 4.

| # | Step | What it covers |
|---|---|---|
| 1 | **Scope and requirements** | Users, decisions, functional and nonfunctional requirements, scale, latency budget, cost budget. Rates with owners. |
| 2 | **Frame the AI task** | The decision the model makes, the I/O contract, and whether it should be a model at all. |
| 3 | **Metrics** | Business metric to online proxy to offline metric, plus guardrails. |
| 4 | **Data** | Sources, labels, freshness, privacy, the feedback loop. |
| 5 | **High-level architecture** | Components, data flow, where the model lives, sync versus async. |
| 6 | **Deep dive** | Retrieval and ranking, the agent loop, the integration layer. |
| 7 | **Failure, scale, and operations** | What breaks, monitoring, drift, rollout, cost at scale. |

## How a week works

A three-hour block, hybrid, built for people who worked all day.

| Segment | What happens |
|---|---|
| **Failure of the Week** | One real, documented AI system failure, analyzed against the framework. Which step did they skip? |
| **Lecture** | About seventy minutes, with a break. |
| **Design Studio** | Build a design in pairs, then review it as a group against the rubric. |
| **Lab** | Read-and-run, finishable in the hour, independent of the projects. |
| **Homework** | Ten multiple-choice questions on the studio scenario and the lab, due before the next block. |

Labs and projects are different things. Labs are in-class, one per week, tuned to that
week's lecture, and independent of each other. Projects are outside class, cumulative,
and build one system.

The studio runs in three formats: **greenfield design** most weeks, **peer mock
interviews** twice, and **system audit** twice. Most of you will inherit an AI system
before you design one, and auditing is the skill nobody teaches.

## The fourteen weeks

1. Why AI systems fail differently
2. Requirements, risk, and designing for mistakes
3. Architecture and the trade space
4. Data as specification, and retrieval
5. Evaluation I: offline
6. Evaluation II: online, and shipping a change
7. Serving, inference economics, and scheduling on scarce capacity
8. Checkpoint and project clinic
9. Agents I: the mechanism
10. Agents II: state, orchestration, and delegation
11. The integration and trust layer
12. Security and safety for agentic systems
13. Operating a live AI system
14. Demos and final

## The project

You receive, in the first week, a **working** support-ticket triage and resolution
agent: a ticket simulator, an agent loop, tools exposed through a capability server, a
deployment, a trace logger. It is deliberately naive. Over four projects you replace
its AI-specific parts with your own. Each project ships with the reference solution
for the previous one, so nobody builds on a broken base.

| Project | You replace or add |
|---|---|
| **P1 — Measure it** | Eval harness: golden set, slices, noise floor, validated judge, blind-spot register |
| **P2 — Ship it** | Eval gate in CI, canary with kill switch, cost model, telemetry |
| **P3 — Make it act** | Your own agent loop and orchestrator: discovery and dispatch over the capability server, budgets, checkpoint and resume, approval gate, scoped token |
| **P4 — Break it, run it** | Hardening after the red team, SLOs, tracing, game-day postmortem |

Projects are done in pairs, about twelve hours each. Full specifications, the scaffold
contents, and the budgets are in the [projects document](projects.md).

## Assessment

| Component | Weight |
|---|---|
| Weekly homework | 10% |
| Projects (4) | 40% |
| Checkpoint exam | 20% |
| Final exam | 15% |
| Demo and defense | 15% |

Labs and studios are not graded directly. The weekly homework verifies both. The demo
and defense is the one assessment nobody can game.

**AI tools** are encouraged on every lab and project and not permitted on the two
exams. For any project you must be able to explain any line of your submission in a
five-minute live walkthrough. The third project additionally prohibits agent
frameworks, because the point is the mechanism.

## Systems Toolkit

Self-paced primers, twenty to thirty minutes each, for the infrastructure the course
treats as prerequisite. Three are required because a project depends on them; the rest
are take-what-you-need.

1. Structured logging, metrics, and tracing *(required for P2)*
2. Reading a provider's inference API as a wire format *(required for P3)*
3. Delegated authorization: tokens and scopes *(required for P3)*
4. Serverless deployment: functions, queues, and a key-value store
5. Containers and images
6. Message queues and pub/sub
7. DAG orchestrators
8. Approximate nearest-neighbor indexes and similarity search
9. Reading a container-orchestrator deployment definition

## Texts

No required purchase. The target text is the book under development alongside this
course. Until its chapters are drafted, selected chapters from:

- Kaestner, *Machine Learning in Production*
- Huyen, *Designing Machine Learning Systems* and *AI Engineering*
- Aminian and Xu, *Machine Learning System Design Interview*
- Google, *Site Reliability Engineering*, selected chapters
- Capability-protocol specifications, read as primary sources

## Course documents

- [Course thesis](course-thesis.md). The editorial spine: what is different about AI
  systems, and the gate every topic must pass.
- [Design review rubric](rubric.md). Seven steps by four levels, the standard the
  studios and exams grade against.
- [Reference design](reference-design.md). The project system through all seven
  steps at level 4.
- [Common system components](common-system-components.md). A one-page vocabulary
  for the parts that show up in AI system designs.
- [Projects, scaffold, and budgets](projects.md). The four cumulative pair projects.
- [Full syllabus](syllabus.md). Week-by-week topics, readings, labs, and policies.
