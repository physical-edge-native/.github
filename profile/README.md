# Physical-Edge Native Architecture

**Making a physical space computable by the many small devices already in it.**

Sensors and microcontrollers are spreading through buildings, machines and
robots. Physical-Edge Native Architecture studies how such devices — cheap,
heterogeneous, owned by different parties — can cooperate *only with their
neighbours* to sense, simulate and predict the physics of the space they share,
while large central models keep doing what they are good at: global reasoning.

Its central question: **when classical numerical solvers and small learned
models are mixed across many devices, and devices join or leave while running,
can the coupled computation be guaranteed to stay stable and accurate?**

## What "computable" means here

The computation is shaped like the space it describes:

1. **Shaped like the space.** The space is split into regions, each with its own
   small solver (classical or learned). Regions exchange only the values at
   their shared borders.
2. **Runs anywhere.** The same regional solver runs on a PC or cluster
   ([barye](https://github.com/physical-edge-native/barye)) or on a small device
   placed inside that region ([dyne](https://github.com/physical-edge-native/dyne)).
3. **Verifiable.** A solution split over many regions matches the single-solver
   solution bit for bit, and stability conditions at the borders can be checked
   when solvers of different kinds are mixed.
4. **Reconfigurable while running.** Regions can join, leave or change size
   without stopping the computation.

## Repositories

| Repository | Role | Status |
|---|---|---|
| [dyne](https://github.com/physical-edge-native/dyne) | Toolchain: deploys physical models as WebAssembly to microcontrollers, with a deterministic simulator and bit-exact verification | research prototype |
| [barye](https://github.com/physical-edge-native/barye) | Physical simulation without GPUs, built from many cooperating local solvers on CPUs; targets 3D field physics (waves, heat, airflow) next to existing robot simulators | started 2026-11 |

## Related approaches

- **Domain decomposition in CFD and numerical libraries** (e.g. OpenFOAM, PETSc)
  splits the domain the same way, but as one tightly coupled computation on a
  cluster. Placing regions on devices inside the space and reconfiguring them
  while running are outside their scope.
- **Robot simulators** (e.g. Isaac Lab, MuJoCo) focus on rigid bodies, contact,
  robots and rendering. Barye is meant to be used *alongside* them for the field
  physics they do not cover, not to replace them.
- **Physical reservoir computing** lets a physical medium itself perform a
  computation for a given task. It answers a different question: it does not
  produce a model of the space's state that can be inspected, verified or used
  for what-if predictions.

## Principles

1. Small computing devices are embedded in physical space.
2. Devices of different makers and owners cooperate through a common interface.
3. Devices split the physics among themselves, communicating only with neighbours.
4. The centre does not disappear: large models handle the global picture, the swarm handles the local one.

Supported by the IPA MITOU IT program (FY2026).
