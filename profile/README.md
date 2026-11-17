# Physical-Edge Native Architecture

**Making a physical space computable by the many small devices already in it.**

Sensors and microcontrollers are spreading through buildings, machines and
robots. Physical-Edge Native Architecture studies how such devices — cheap,
heterogeneous, owned by different parties — can cooperate *only with their
neighbours* to sense, simulate and predict the physics of the space they share,
while large central models keep doing what they are good at: global reasoning.

## Why: the assumptions behind it

The architecture is a proposal for a future in which the following hold. We
state them openly so that each can be questioned.

**Assumptions about the world**

1. **Devices of different owners share a space.** The heating maker's sensors,
   the lighting system and the occupants' own gadgets sit in the same room. No
   single party is in a position to collect everyone's raw data — which is why
   the architecture does not assume that all data goes to one centre.
2. **Small computers become cheap enough to be placed throughout a space**,
   running on batteries or harvested energy.
3. **Many physical fields of interest are governed by coupling between
   neighbouring points** (heat, air quality, slow airflow, waves).
4. **Sending data over radio tends to cost more than computing locally.**
5. **Global reasoning stays with large central models.** The centre does not
   disappear.

**What we expect to follow**

- Devices will split the physics of their space among themselves, each
  computing its own region and communicating only with its neighbours.

**What that requires — the question this project works on**

- When classical numerical solvers and small learned models from different
  makers are coupled across devices, and devices join or leave while running,
  the coupled computation must stay stable (it must not diverge) and its error
  must stay within a known bound. *Can that be guaranteed, and checked?*

## What "computable" means here

The computation is shaped like the space it describes. The four properties
below follow from the principles in the next section:

1. **Shaped like the space.** The space is split into regions, each with its own
   small solver (classical or learned). Regions exchange only the values at
   their shared borders.
2. **Runs anywhere.** The same regional solver runs on a small device placed
   inside its region or on a PC, with identical results.
3. **Verifiable.** A solution split over many regions matches the single-solver
   solution bit for bit, and stability conditions at the borders can be checked
   when solvers of different kinds are mixed.
4. **Reconfigurable while running.** Regions can join, leave or change size
   without stopping the computation.

## Principles

1. **Computation is placed where the physics is.** The device that measures a
   region computes that region, and devices communicate only with their
   neighbours.
2. **Different components meet only through contracts at their borders.** Local
   components that differ in maker, owner and kind — classical solvers, learned
   models, and in future physical or quantum devices — are connected only
   through what is agreed at their shared borders: what is exchanged, the
   stability condition, the error bound, and how it is checked. Components are
   kept isolated: one hosted on another owner's device should reach nothing
   beyond its contract (in dyne, solvers run as WebAssembly, which cannot touch
   memory outside its own or call anything it has not been granted).
3. **Keeping those contracts is checkable.** Where components are digital and
   deterministic, the check is bit-for-bit equality; where they are not, it is
   an error bound.
4. **The centre does not disappear.** Raw sensor data never goes to the centre.
   Normally a summary of the state does; when a forecast faster than real time
   is needed, the state the devices have already fitted to their measurements is
   handed over with identical bits, so that a central computer can join
   temporarily, compute ahead with the same solvers, and leave again.

## Limits we state up front

- **A speed limit set by the network.** With neighbour-only exchange,
  information crosses one region per exchange. To follow a field in real time,
  region size ÷ exchange delay must exceed the speed at which the physics
  propagates — a CFL-like condition on the network. With today's radio delays
  this rules out real-time tracking of fast phenomena such as sound, and leaves
  slow fields (indoor heat, CO2, humidity). Slow fields can often be computed by
  a single device; the value of many devices lies in sensing spread through the
  field, not in raw compute.
- **Bit-exact under message loss, at the cost of delay.** Results stay identical
  to the single-solver solution because devices wait for missing messages; loss
  therefore turns into delay.
- **Honest devices only, for now.** Current guarantees assume that every device
  is honest and only faults occur (message loss, delay, devices leaving). Trust
  between devices of different owners — authentication, rejecting implausible
  border values, tolerance of malicious devices — is future work.
- **No claim of superiority** over centralised or GPU-based setups. This is
  groundwork for a time when edge computing is woven into physical spaces.

## Repositories

| Repository | Role | Status |
|---|---|---|
| [dyne](https://github.com/physical-edge-native/dyne) | Toolchain: deploys physical models as WebAssembly to microcontrollers, keeps them fitted to sensor data, and verifies results bit for bit against a deterministic simulator; includes native solvers for PCs (reference solutions, fast simulation of many devices) | research prototype |
| [barye](https://github.com/physical-edge-native/barye) | Former CPU-side simulation environment, merged into dyne in 2026-11 | archived |

## Related approaches

- **Amorphous, spatial and aggregate computing** (e.g. field calculus) program
  many locally communicating devices placed in space. They mostly target
  coordination (gradients, consensus, routing) with self-stabilisation
  guarantees; numerical accuracy and stability of physical solvers are not their
  focus.
- **Distributed estimation of physical fields on sensor networks** (e.g.
  distributed Kalman filters for fields governed by partial differential
  equations) shares the region-by-region structure; it is mostly studied in
  theory and simulation rather than on device swarms.
- **Domain decomposition in CFD and numerical libraries** (e.g. OpenFOAM, PETSc)
  splits the domain the same way, but as one tightly coupled computation on a
  cluster. Placing regions on devices inside the space and reconfiguring them
  while running are outside their scope. For detailed studies, dyne aims to
  export its state *to* such tools rather than compete with them.
- **Robot simulators** (e.g. Isaac Lab, MuJoCo) focus on rigid bodies, contact,
  robots and rendering; field physics is largely outside their scope.
- **Physical reservoir computing** lets a physical medium itself perform a
  computation for a given task. It answers a different question: it does not
  produce a model of the space's state that can be inspected, verified or used
  for what-if predictions.

The individual elements above all have prior work. What this project studies is
their combination on real device swarms, with numerical guarantees.

Supported by the IPA MITOU IT program (FY2026).
