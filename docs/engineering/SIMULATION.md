# Simulation Strategy

## Purpose

Simulation is used to reduce engineering uncertainty before building or modifying physical hardware.

Simulation is **not** treated as ground truth.

For this project, simulation should primarily help answer questions about:

* kinematics
* reachable workspace
* joint requirements
* mechanism complexity
* collision risk
* stirring trajectory feasibility
* vessel coverage
* joint motion
* actuator loading trends
* camera placement and visibility
* compliance concepts
* interaction with simplified materials

The goal is to use simulation to make better physical experiments and design decisions.

Simulation should not become a substitute for physical testing.

---

# Core Principle

The project should progress from simple, trustworthy simulation toward more complex and uncertain simulation only when necessary.

Preferred order:

1. geometric analysis
2. kinematic simulation
3. collision and workspace simulation
4. trajectory analysis
5. rigid-body interaction
6. simplified resistance/compliance models
7. particle or fluid-like simulation
8. physical calibration
9. increasingly realistic cooking experiments

Do not begin with realistic food simulation.

---

# Simulation Philosophy

## Simulate Questions, Not the Entire Product

Every simulation should answer a defined engineering question.

Examples:

* Can a 2-DOF architecture reach enough of the pot?
* Does adding a third DOF substantially improve useful coverage?
* Can the utensil maintain useful orientation near the vessel wall?
* Does a proposed linkage collide with the pot rim?
* Which stirring trajectory produces the greatest geometric coverage?
* Does passive vertical compliance reduce peak loads?
* Is a camera location likely to provide useful visibility?

Avoid building detailed simulation infrastructure without a decision it is intended to inform.

---

# Simulation Is Not Evidence of Real Food Performance by Itself

Cooking materials are difficult to simulate accurately.

Real foods may exhibit:

* changing viscosity
* non-Newtonian behavior
* shear thinning
* particle suspension
* granular behavior
* adhesion
* friction
* clumping
* phase changes
* temperature dependence
* evaporation
* heterogeneous ingredients
* interaction with vessel surfaces

Therefore:

> A simulated material should be treated as an engineering model, not as a claim that the simulation accurately reproduces a specific food.

Prefer language such as:

> "SIM-MAT-003 is a high-resistance material model."

rather than:

> "SIM-MAT-003 is risotto."

When possible, simulated material behavior should eventually be calibrated against repeatable physical benchmark materials documented in:

`docs/experiments/TEST_MATERIALS.md`

---

# Proposed Simulation Toolchain

## Robot Description

A URDF or equivalent robot description should be maintained for candidate mechanisms where appropriate.

Possible location:

```text
software/simulation/
├── README.md
├── urdf/
│   ├── smart_stirrer.urdf
│   └── meshes/
├── isaac/
│   ├── scenes/
│   ├── scripts/
│   └── materials/
├── tests/
└── results/
```

The URDF should initially contain only the detail required for kinematic and collision analysis.

Do not model cosmetic detail unless it affects:

* geometry
* mass
* inertia
* collisions
* workspace
* sensing
* thermal behavior

---

## Primary Simulator

Current candidate:

**NVIDIA Isaac Sim**

Potential uses include:

* articulation simulation
* URDF import
* rigid-body physics
* collision testing
* joint-state analysis
* virtual camera placement
* particle-based material approximations
* automated simulation experiments

The simulator choice is not permanently fixed.

Alternative tools may be used if they are better suited to a specific question.

---

# Simulation Validation Ladder

## Level 0 — Mathematical Analysis

Use analytical or numerical calculations without a full physics simulator.

Examples:

* forward kinematics
* inverse kinematics
* workspace calculation
* link-length optimization
* Jacobian analysis
* geometric pot coverage
* basic torque estimates

This should be preferred whenever it can answer the question adequately.

---

## Level 1 — Kinematic Simulation

Model:

* links
* joints
* joint limits
* utensil geometry
* representative vessel geometry

Primary questions:

* Where can the tool reach?
* What orientations can it achieve?
* What parts of the vessel cannot be reached?
* Which joint limits become restrictive?
* Are additional DOFs useful?

---

## Level 2 — Collision Simulation

Add collision geometry for:

* vessel
* rim
* utensil
* links
* central housing
* mounting structure

Investigate:

* arm-to-pot collisions
* utensil-to-vessel collisions
* self-collisions
* housing interference
* unusable configurations
* safe joint limits

---

## Level 3 — Trajectory Coverage

Test candidate stirring trajectories.

Initial candidate trajectories may include:

* constant-radius circular motion
* eccentric circles
* spirals
* radial sweeps
* figure-eight paths
* wall-following paths
* center sweeps
* alternating patterns

Define a geometric vessel coverage metric.

Possible method:

1. divide the usable vessel area into a grid
2. track utensil influence over time
3. calculate percentage of cells reached
4. measure revisit frequency
5. identify persistent dead zones

Metrics may include:

* total coverage percentage
* coverage uniformity
* maximum dead-zone area
* time to achieve target coverage
* path length
* joint travel
* joint velocity
* required orientation changes

---

## Level 4 — Simplified Mechanical Resistance

Before attempting realistic fluids, test simplified resistance models.

Possible models:

* spring forces
* damping
* friction
* rigid obstacles
* compliant contacts
* distributed resistance

Questions may include:

* Does compliance reduce peak joint loads?
* What happens when the utensil encounters an obstacle?
* Does the mechanism recover from a jam?
* Is active vertical motion necessary?
* Could passive compliance replace an actuator?

This level may provide higher-value information than complex food simulation.

---

## Level 5 — Simplified Material Interaction

Particle, fluid-like, or granular simulation may be introduced after the robot and trajectory questions are reasonably understood.

Possible material classes:

### SIM-MAT-001 — Low Resistance Fluid

Purpose:

* baseline material displacement
* flow visualization
* utensil-path comparison

---

### SIM-MAT-002 — High Resistance Homogeneous Material

Purpose:

* investigate qualitative differences caused by increased material resistance
* compare trajectories
* compare tool geometries

---

### SIM-MAT-003 — Granular Material

Purpose:

* investigate tool interaction with discrete particles
* identify dead zones
* evaluate displacement patterns

---

### SIM-MAT-004 — Mixed Material

Possible combination of:

* fluid-like particles
* larger particles or rigid bodies

Purpose:

* approximate chunky or heterogeneous cooking scenarios

These material IDs represent simulation classes, not specific foods.

---

# Physical Calibration

Simulation should eventually be compared against repeatable physical experiments.

A useful calibration experiment should attempt to reproduce the same:

* vessel geometry
* utensil geometry
* stirring path
* speed
* material class
* starting conditions

Physical measurements may include:

* motor current
* average torque
* peak torque
* stalls
* tool deflection
* trajectory error
* material displacement
* mixing time
* coverage pattern

Simulation parameters may then be adjusted to produce qualitatively or quantitatively similar behavior where feasible.

---

# Simulation-to-Reality Expectations

The project should distinguish three levels of simulation confidence.

## Qualitative

Simulation predicts trends.

Example:

> Architecture A reaches substantially more of the vessel than Architecture B.

This may be useful even without perfect physical calibration.

---

## Semi-Quantitative

Simulation approximately reproduces measured trends or relative magnitudes.

Example:

> Increasing material resistance produces approximately the same relative increase in motor loading observed experimentally.

---

## Quantitative

Simulation accurately predicts measured real-world values within an established error range.

This level requires deliberate validation and should never be assumed.

---

# Initial Simulation Metrics

Candidate metrics include:

## Kinematic Metrics

* reachable vessel area
* reachable vessel volume
* reachable utensil orientation range
* minimum/maximum joint angles
* proximity to joint limits
* singularity risk
* required joint travel

## Trajectory Metrics

* vessel coverage percentage
* coverage uniformity
* dead-zone size
* time to target coverage
* path length
* joint motion required
* trajectory smoothness

## Mechanical Metrics

* estimated joint torque
* peak force
* contact force
* tool deflection
* obstacle recovery
* collision count

## Complexity Metrics

* number of actuated DOFs
* number of passive joints
* mechanism size
* required actuator count
* required sensor count
* estimated control complexity

No single metric should define the preferred architecture.

---

# Candidate Architecture Comparison

Candidate mechanisms should be compared beginning with the simplest.

Possible sequence:

* 1-DOF rotary stirrer baseline
* 2-DOF architecture
* 3-DOF architecture
* 4-DOF architecture
* current approximately 5-DOF concept
* alternative constrained mechanisms

Each added DOF should answer:

1. What capability does this DOF provide?
2. Is that capability required?
3. Can passive mechanics provide it instead?
4. Does simulation show meaningful improvement?
5. Can physical experiments validate that improvement?
6. What cost and failure modes does it add?

---

# Initial Simulation Experiments

## SIM-001 — Kinematic Architecture Comparison

### Objective

Determine how mechanical complexity affects usable stirring workspace.

### Primary Question

What is the minimum number and arrangement of DOFs required to provide useful stirring coverage of a representative vessel?

### Candidate Architectures

At minimum compare:

* single-axis rotary baseline
* simple 2-DOF architecture
* candidate 3-DOF architecture
* current articulated concept

### Initial Outputs

* reachable workspace
* vessel coverage
* tool orientation capability
* collisions
* required joint ranges
* identified dead zones

### Decision Informed

Which architectures are worth physically prototyping.

---

## SIM-002 — Stirring Trajectory Coverage

### Objective

Compare geometric effectiveness of different stirring paths.

### Candidate Paths

* circular
* eccentric circular
* spiral
* radial sweep
* figure eight
* wall-following
* hybrid paths

### Initial Outputs

* coverage percentage
* coverage uniformity
* dead zones
* trajectory length
* required joint motion

### Decision Informed

Which trajectories should be evaluated in physical experiments.

---

## SIM-003 — Compliance and Obstacle Interaction

### Objective

Determine whether active vertical control is necessary when the utensil encounters resistance or obstacles.

### Compare

* rigid tool
* passive compliant tool
* actively controlled vertical DOF

### Decision Informed

Whether another actuator is justified.

---

# Camera Simulation

Camera simulation should initially be used for geometry and visibility rather than machine learning.

Questions:

* Can the camera see the full useful pot area?
* Which regions are occluded by the arm?
* How much does the utensil obstruct the view?
* How strongly does mounting location affect visibility?
* What field of view is required?

Do not make computer vision part of the critical path until the mechanical stirring system has demonstrated value.

---

# Simulation Documentation

Every substantial simulation experiment should record:

* simulation ID
* date
* engineering question
* model version
* relevant Git commit
* mechanism configuration
* vessel geometry
* utensil geometry
* material model, if applicable
* simulation parameters
* assumptions
* outputs
* interpretation
* limitations
* resulting decision or next experiment

Simulation results should be reproducible whenever practical.

---

# Known Risks

Simulation-specific risks include:

* unrealistic contact parameters
* inaccurate mass/inertia estimates
* inaccurate motor models
* unrealistic food/material physics
* timestep sensitivity
* particle-model artifacts
* incorrect friction assumptions
* overconfidence in visually convincing simulation
* excessive time spent building simulation infrastructure
* optimizing the design for the simulator rather than the real product

A visually realistic result is not automatically an accurate result.

---

# Current Status

**Stage:** Early feasibility.

No simulation architecture or food/material model has yet been validated.

Current priority:

1. define candidate mechanism architectures
2. build simple kinematic representations
3. define representative vessel geometry
4. establish coverage metrics
5. run SIM-001
6. use findings to inform the first physical test rig

---

# Open Questions

* Which simulation platform is best for the first architecture studies?
* Should the canonical robot description begin as URDF or another format?
* What representative pot geometries should be modeled first?
* How should useful vessel coverage be mathematically defined?
* What utensil influence radius should be used in coverage calculations?
* Which candidate mechanisms should be included in SIM-001?
* Which physical measurements can realistically calibrate later material simulation?
* At what stage does particle/fluid simulation provide enough value to justify its complexity?
