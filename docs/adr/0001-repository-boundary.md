<!--
SPDX-License-Identifier: AGPL-3.0-or-later
Commercial license available
© Concepts 1996–2026 Miroslav Šotek. All rights reserved.
© Code 2020–2026 Miroslav Šotek. All rights reserved.
ORCID: 0009-0009-3560-0851
Contact: www.anulum.li | protoscience@anulum.li
SCPN Lattice Fusion Core — ADR 0001
-->

# ADR 0001 — Repository boundary and ownership

**Status:** accepted (2026-09-02)

**Deciders:** project owner (direct instruction of 2026-09-02); SCPN Reactor
Systems Research Group standard, section "Reserved extension projects"

## Context

The SCPN reactor portfolio assigns every built-in configuration of the SCPN
Phase Orchestrator reactor registry (release `1.0.0`, 32 configurations) to
exactly one device-family repository. Lattice-confinement fusion has no
built-in configuration: the family standard reserved the name
`SCPN-LATTICE-FUSION-CORE` and set three conditions for creating it — a
namespaced registry extension accepted by the orchestrator, a producer and
evidence class defined by the research group, and an owner-approved
boundary. On 2026-09-02 the owner directed the creation of the repository;
the group prepared registry release `1.1.0` with the namespaced extension
`scpn.reactor_systems:lattice_confinement_fusion` (family `extension`,
built-ins untouched), recorded it as pending in the family map, and
defined the producer and evidence class in its bootstrap plan.

## Decision

1. `SCPN-LATTICE-FUSION-CORE` owns exactly one registry configuration, the
   namespaced extension `scpn.reactor_systems:lattice_confinement_fusion`,
   and pins the prepared release `1.1.0` and its digest; the validator
   cross-checks the pin against the family map's pending block until the
   orchestrator lands the release.
2. The repository owns device-level truth only: host-lattice and loading
   configuration policy (metal, stoichiometry, loading ratio, temperature,
   hydride state), driver declarations (bremsstrahlung endpoint energy,
   spectrum, dose, exposure geometry; other driver classes as
   declarations), screening-potential declarations as inputs with their
   published ranges, exposure lifecycle semantics with activation and
   hydride hazard records, neutron- and gamma-anchored diagnostic and
   clock declarations, actuator-response model boundaries, the
   safety-envelope declaration, and the device-owned CONTROL adapter
   specification.
3. Accelerator beam-on-target reaction kinematics stay with
   `SCPN-BEAM-TARGET-CORE` (the lattice family's projectiles are secondary
   particles inside a cold dense fuel); muon catalysis with
   `SCPN-MUON-FUSION-CORE`; fission blankets with
   `SCPN-FUSION-FISSION-HYBRID-CORE`; thermal confinement of every kind
   with the magnetic, inertial and magneto-inertial families.
4. The family declares no anomalous or unexplained nuclear process. Its
   physics is the screened tunnelling of driver-produced hot projectiles
   in a cold deuterated lattice as published (Pines et al. and Steinetz et
   al., Phys. Rev. C 101 (2020) 044609 and 044610, NASA technical
   publications 20205001617 and 20205001616); every model landing carries
   that statement as a non-claim.
5. Solver mathematics remains in `SCPN-FUSION-CORE` until an exact surface
   passes the family migration gate. No solver code is copied here.
6. Typed semantics remain in `SCPN-PHASE-ORCHESTRATOR` (review-only).
   Admission and `ControlAction` formation remain exclusively in
   `SCPN-CONTROL`. Machine protection remains independent with the final
   veto. Presentation remains in `SCPN-STUDIO`; this project is
   `not_federated`.
7. The repository starts, and remains until evidenced otherwise, at
   `architecture_only` with empty capability and claim inventories.

## Alternatives considered

- **Folding the family into `SCPN-BEAM-TARGET-CORE`** (a driver produces
  projectiles that react with a target): rejected — the reacting
  projectiles are not a beam of declared kinematics, the fuel is the
  lattice itself, and the family's defining quantity is the screening
  environment, absent from the beam-target boundary.
- **A built-in registry configuration** instead of a namespaced
  extension: rejected — the standard's route for reserved projects is the
  namespaced extension, which leaves the 32 built-ins and every existing
  pin untouched.
- **Waiting for the orchestrator to land the release first**: rejected by
  the owner's instruction; the prepared release is pinned exactly and the
  family map carries it as pending, so the eventual landing is a re-pin
  only if the digest differs.

## Consequences

The family map gains one planned repository and one namespaced
assignment; the orchestrator receives a prepared patch and lands the
release under its own gates; until then this repository validates against
the pending block. Every later capability is a separately evidenced
landing under this boundary; the non-claim of item 4 is permanent.
