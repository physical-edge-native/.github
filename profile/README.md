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

## Repositories

| Repository | Role | Status |
|---|---|---|
| [dyne](https://github.com/physical-edge-native/dyne) | Toolchain: deploys physical models as WebAssembly to microcontrollers, with a deterministic simulator and bit-exact verification | research prototype |
| physics-sim *(name TBD)* | Physical simulation without GPUs, built from many cooperating local solvers | started 2026-11 |

## Principles

1. Small computing devices are embedded in physical space.
2. Devices of different makers and owners cooperate through a common interface.
3. Devices split the physics among themselves, communicating only with neighbours.
4. The centre does not disappear: large models handle the global picture, the swarm handles the local one.

Supported by the IPA MITOU IT program (FY2026).
