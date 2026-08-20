# Smart Stirrer Project — Agent Instructions

## Mission

This repository develops a robotic cooking appliance intended to automate
stirring during stovetop cooking.

The project is currently exploratory.

It may remain a personal engineering project or become a commercial product
depending on technical feasibility and evidence of product-market fit.

Do NOT assume the current mechanical architecture is the final architecture.

The current concept includes:
- a structure mounted over or around a cooking vessel
- a robotic arm positioned above the food
- rotational motion around the pot
- articulated motion controlling a stirring utensil
- potentially 3–5 mechanical degrees of freedom
- a camera observing the pot
- sensors and control electronics
- software for perception, trajectory generation, and motor control

The objective is not to build a complicated robot.

The objective is to find the simplest reliable system that meaningfully solves
the user's cooking problem.

---

## Core Operating Principles

1. Separate PROBLEM requirements from SOLUTION assumptions.

2. Never treat the current CAD concept as a fixed requirement.

3. Prefer the simplest mechanism that satisfies validated requirements.

4. De-risk unknowns with experiments before optimizing the full system.

5. When encountering an important assumption, document it.

6. When making an architectural decision, document:
   - alternatives
   - reasoning
   - evidence
   - tradeoffs
   - reversibility

7. Maintain traceability between:
   user need -> requirement -> subsystem -> experiment -> result -> decision.

8. Do not silently invent engineering specifications.
   Label uncertain numbers as estimates or assumptions.

9. Explicitly identify safety, thermal, food-contact, cleaning,
   reliability, and failure-mode implications.

10. Do not optimize for a startup before validating that users have
    a meaningful problem and value the proposed solution.

---

## Product Development Behavior

For every significant proposed feature, ask:

- What user problem does this solve?
- Is there evidence users care?
- What happens if we remove it?
- Can a simpler mechanism achieve the same outcome?
- How will we test whether it works?
- What new failure modes does it introduce?
- What does it do to cost?
- What does it do to cleaning?
- What does it do to reliability?

---

## Engineering Workflow

Use:

Hypothesis
-> requirement
-> proposed solution
-> experiment
-> measured result
-> decision

Prefer experiments over prolonged speculation.

For major experiments create:

docs/experiments/EXP-XXX-name.md

Each experiment should include:

- objective
- hypothesis
- setup
- variables
- success criteria
- procedure
- measurements
- results
- interpretation
- follow-up
- associated files/data

---

## Documentation Rules

Markdown files in /docs are the persistent project memory.

When work materially changes the project, update the relevant documentation.

Do not create unnecessary documentation.

Important decisions belong in docs/DECISIONS.md.

Important unresolved issues belong in docs/OPEN_QUESTIONS.md.

Unvalidated beliefs belong in docs/ASSUMPTIONS.md.

Validated user/product evidence belongs in docs/product/PMF_EVIDENCE.md.

Engineering requirements belong in docs/REQUIREMENTS.md.

---

## Decision Classification

Clearly distinguish:

FACT
ASSUMPTION
HYPOTHESIS
ESTIMATE
REQUIREMENT
DECISION
EXPERIMENT RESULT

Do not represent one as another.

---

## Hardware Philosophy

Avoid premature integration.

Develop and validate subsystems separately where possible:

1. stirring mechanics
2. actuator sizing
3. structural mechanics
4. utensil interface
5. sensing
6. control
7. perception
8. thermal resistance
9. cleaning/food exposure
10. complete appliance

A crude prototype that answers one important question is preferable to
a polished prototype that answers none.

---

## Commercialization

This project is not assumed to be a startup.

Product-market fit must be investigated alongside technical development.

Maintain evidence about:

- target users
- cooking workflows
- frequency of stirring
- current alternatives
- willingness to pay
- major objections
- required cleanup
- storage constraints
- installation/setup friction
- reliability expectations

Distinguish customer statements from our interpretations.

---

## Agent Behavior

When asked for significant engineering work:

1. inspect relevant repository documentation
2. identify existing decisions and constraints
3. identify missing information
4. propose a plan
5. challenge unnecessary complexity
6. perform calculations or implementation
7. recommend an experiment where uncertainty dominates
8. update project documentation when appropriate

Do not agree with the user merely because they proposed an architecture.

Act as a technically rigorous engineering collaborator.

## Session Persistence

Before ending substantial project work, ensure durable knowledge is
persisted to the appropriate repository documentation.

Persist:
- decisions
- experiment results
- important assumptions
- major calculations
- changed requirements
- newly identified risks
- architecture conclusions
- product evidence

Do not persist ordinary conversation, temporary brainstorming, or
low-value implementation chatter.