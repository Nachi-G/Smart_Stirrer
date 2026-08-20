# Physical Test Materials

## Purpose

This document defines repeatable physical materials used to test the Smart Stirrer independently of specific recipes.

The goal is to create controlled benchmark materials that allow different:

* mechanisms
* motors
* utensils
* trajectories
* speeds
* compliance strategies
* control methods

to be compared under approximately repeatable conditions.

These materials are engineering test media.

They are not intended to perfectly reproduce individual foods.

Actual cooking experiments will eventually be required.

---

# Why Standardized Test Materials Matter

Cooking with real food introduces many uncontrolled variables.

Examples:

* ingredient ratios
* temperature
* cooking time
* water loss
* ingredient size
* batch variation
* starch release
* fat content
* phase changes

If every mechanism test uses a different batch of food, it becomes difficult to determine whether performance changed because of the robot or because of the test material.

Standardized benchmark materials should therefore be used during early engineering development.

---

# Test Material Principles

Preferred test materials should be:

* inexpensive
* repeatable
* easy to prepare
* easy to measure
* reasonably safe
* representative of a useful mechanical behavior
* available consistently
* practical to dispose of or reuse where appropriate

Whenever possible, preparation should be defined by measurable quantities rather than visual judgment.

Examples:

Prefer:

> 1000 g water + X g thickener

over:

> Add thickener until it looks like sauce.

---

# Material Identification

Each standardized material receives an ID.

Format:

```text
MAT-###
```

Variants may use additional suffixes.

Example:

```text
MAT-002-L
MAT-002-M
MAT-002-H
```

representing low, medium, and high resistance versions of a material family.

---

# Initial Material Library

## MAT-001 — Water Baseline

### Purpose

Provide a low-resistance baseline.

### Material

Water.

### Primary Uses

* verify basic mechanism operation
* visualize gross fluid displacement
* identify excessive splashing
* evaluate utensil paths
* compare stirring speeds
* establish baseline motor current
* validate experimental instrumentation

### Advantages

* highly repeatable
* inexpensive
* easy cleanup
* consistent properties
* safe for early testing

### Limitations

Water is not representative of many important cooking tasks.

It provides very little resistance and should not be used alone to validate:

* actuator sizing
* heavy stirring performance
* jam resistance
* thick-food behavior
* compliance requirements

---

## MAT-002 — Controlled Thickened Fluid

### Purpose

Create a family of homogeneous materials with controllable resistance.

### Candidate Material

Water mixed with a controlled quantity of food-safe thickener such as xanthan gum.

Exact formulations are TBD and should be experimentally characterized before becoming standardized.

### Proposed Variants

```text
MAT-002-L — low resistance
MAT-002-M — medium resistance
MAT-002-H — high resistance
```

### Primary Uses

* actuator load comparison
* trajectory comparison
* tool geometry testing
* current/torque measurement
* speed testing
* mixing-pattern visualization
* simulation calibration

### Required Documentation

Once formulations are established, document:

* water mass
* thickener mass
* preparation method
* mixing procedure
* rest time
* temperature
* batch size
* usable test duration
* disposal procedure

### Important Note

Do not assume mixture concentration directly corresponds to a specific food.

This material is intended to provide controlled mechanical resistance.

---

## MAT-003 — Granular Test Material

### Purpose

Test interaction with discrete particles.

### Candidate Materials

Possible candidates include:

* dry rice
* dry beans
* food-safe polymer test media

Final material TBD.

### Primary Uses

* obstacle interaction
* utensil penetration
* particle displacement
* dead-zone identification
* tool geometry comparison
* investigation of passive compliance
* investigation of vertical motion requirements

### Limitations

A dry granular material does not reproduce the fluid behavior of cooking mixtures.

Its value is primarily mechanical.

---

## MAT-004 — Heterogeneous Fluid + Solids

### Purpose

Introduce discrete objects into a fluid or thickened base.

### Candidate Composition

TBD.

Possible structure:

```text
base material
+
controlled quantity of standardized particles
```

### Primary Uses

* chunky-material interaction
* jam behavior
* utensil obstruction
* compliance testing
* trajectory robustness
* peak-load testing

### Important Requirement

Particle:

* size
* mass
* count
* shape

should eventually be standardized.

---

# Future Material Classes

These should not be developed until necessary.

Possible future classes include:

## Adhesive Material

Used to investigate:

* vessel-wall scraping
* utensil coating
* drag
* cleanup

---

## High-Resistance Paste

Used for:

* peak torque testing
* gearbox evaluation
* structural deflection
* overload protection

---

## Mixed Granular Suspension

Used for:

* complex ingredient interaction
* particle circulation
* dead-zone behavior

---

## Temperature-Controlled Material

Used later when temperature effects become important.

This should only be introduced once room-temperature testing can no longer answer the relevant question.

---

# Physical Testing Progression

Testing should generally progress in this order:

```text
empty vessel
    ↓
water
    ↓
controlled thickened material
    ↓
granular material
    ↓
heterogeneous benchmark material
    ↓
representative real foods
    ↓
actual cooking
```

Not every experiment requires every material.

Use the simplest material capable of answering the engineering question.

---

# Preparation Record

Every experimental batch should record:

```text
Material ID:
Batch ID:
Date:
Operator:
Water mass:
Additive mass:
Particle mass/count:
Preparation procedure:
Mixing time:
Rest time:
Temperature:
Container/vessel:
Notes:
```

Example batch identifier:

```text
MAT-002-M-B007
```

---

# Environmental Conditions

Properties may change with temperature and time.

Where relevant, record:

* material temperature
* ambient temperature
* time since preparation
* previous stirring history
* evaporation
* contamination
* reuse count

Early tests do not need laboratory-grade environmental control.

However, uncontrolled variables should be acknowledged.

---

# Vessel Standardization

Material comparisons require consistent vessel geometry.

Each test should record the vessel ID.

Example:

```text
VESSEL-001
```

Relevant properties include:

* inner diameter
* bottom diameter
* height
* wall curvature
* material
* coating
* usable fill volume

Different vessel geometries should eventually be tested deliberately rather than accidentally.

---

# Utensil Standardization

Each stirring tool should receive an ID.

Example:

```text
TOOL-001
```

Record:

* geometry
* width
* length
* thickness
* material
* flexibility
* orientation
* mounting method

Small differences in tool geometry may strongly affect test results.

---

# Standard Test Configuration

A complete physical test configuration should be identifiable using something similar to:

```text
EXP-004
MAT-002-M-B007
VESSEL-001
TOOL-003
TRAJ-002
SPEED-003
MECH-P002
```

This makes later comparisons possible.

---

# Candidate Measurements

Depending on the experiment, collect:

## Mechanical

* average motor current
* peak motor current
* estimated average torque
* estimated peak torque
* stalls
* overload events
* joint position error
* structural deflection
* utensil deflection
* collisions

## Stirring Performance

* coverage
* dead zones
* mixing time
* material redistribution
* particle displacement
* wall scraping
* bottom scraping
* visible circulation

## Operational

* noise
* splashing
* material climbing the utensil
* material entering joints
* cleanup difficulty

---

# Mixing Uniformity Experiments

Eventually, mixing performance should be measured objectively.

Possible approaches include:

* adding a controlled color tracer
* placing standardized particles in known positions
* measuring redistribution over time
* video tracking
* image-based concentration analysis

The specific method is TBD.

A visually appealing vortex does not necessarily mean good stirring performance.

---

# Torque and Motor Current

Motor current may provide a useful proxy for mechanical resistance.

Where possible, record:

* unloaded motor current
* baseline current in water
* mean current during test
* peak current
* current distribution over time
* stall current events

Do not assume current directly equals utensil force without calibration.

Eventually, load cells, torque sensors, or other instrumentation may be introduced if justified.

---

# Connection to Simulation

Physical benchmark materials may be paired with simulation material models.

Example:

```text
MAT-001
↕
SIM-MAT-001

MAT-002-M
↕
SIM-MAT-002
```

The goal is not necessarily exact simulation.

Useful comparisons may include:

* relative load
* relative mixing behavior
* particle redistribution
* dead-zone location
* response to speed changes
* response to trajectory changes

Simulation should be calibrated to measured physical behavior where practical.

---

# Real Food Validation

Benchmark materials cannot replace actual food testing.

Once the mechanism demonstrates useful performance with standardized test media, representative foods should be selected.

Food selection should cover different stirring problems.

Possible future categories:

* thin sauce
* thick sauce
* starch-heavy mixture
* particulate sauté
* thick porridge-like material
* sticky material
* heterogeneous mixture

Specific recipes should be chosen based on actual customer use cases rather than engineering convenience alone.

---

# Safety

Only use test materials appropriate for the current equipment and environment.

Consider:

* splashing
* hot liquids
* biological spoilage
* electrical equipment
* motor exposure
* contamination
* slippery spills
* rotating mechanisms
* loose particles

When the system is not food-safe, do not consume materials used in experiments.

---

# Cleanup as a Measurement

Cleanup is part of product performance.

For later prototypes, record:

* components requiring cleaning
* cleaning time
* disassembly required
* inaccessible residue
* material entering joints or mechanisms
* dishwasher compatibility where relevant
* difficulty relative to manually stirring

A mechanism that stirs effectively but is unpleasant to clean may fail as a product.

---

# Initial Recommended Test Set

Do not build a large material library immediately.

Start with:

## MAT-001

Water baseline.

## MAT-002

One controlled thickened-fluid formulation.

## MAT-003

One simple granular or chunky-material benchmark.

Expand only when an experiment requires a behavior these cannot represent.

---

# Initial Physical Experiment

## EXP-001 — Baseline Stirring Motion Comparison

### Objective

Determine whether nontrivial stirring motion provides measurable advantages over simple rotary stirring.

### Candidate Comparisons

At minimum:

* circular rotary path
* one alternative non-circular path

Additional trajectories should only be added if practical.

### Initial Test Materials

Begin with:

* MAT-001
* one MAT-002 formulation

### Candidate Measurements

* geometric coverage
* dead zones
* motor current
* mixing time
* splashing
* repeatability

### Primary Decision

Whether additional trajectory freedom appears valuable enough to justify more complex mechanism development.

---

# Information Still Required

Before standardizing MAT-002 or later materials, determine:

* exact formulation
* preparation method
* batch size
* stability over time
* repeatability between batches
* cleanup requirements
* whether viscosity or another physical property should eventually be measured directly

Do not invent these values.

They should be established experimentally.