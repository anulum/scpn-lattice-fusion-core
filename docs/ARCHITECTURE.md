<!--
SPDX-License-Identifier: AGPL-3.0-or-later
Commercial license available
© Concepts 1996–2026 Miroslav Šotek. All rights reserved.
© Code 2020–2026 Miroslav Šotek. All rights reserved.
ORCID: 0009-0009-3560-0851
Contact: www.anulum.li | protoscience@anulum.li
SCPN Lattice Fusion Core — Architecture
-->

# Architecture

## Purpose and evidence state

`SCPN-LATTICE-FUSION-CORE` is the device-family owner for
lattice-confinement fusion research in the SCPN Reactor Systems Research
Group portfolio. The repository is `architecture_only`: every section below
describes boundaries and contracts; no implemented reactor capability
exists, and the capability and claim inventories are generated, empty, and
drift-checked.

## The five-surface boundary

1. **Governing physics** — fusion of hydrogen isotopes loaded at high
   density into a metal lattice (deuterated erbium, titanium and similar
   hydrides). The lattice's conduction and shell electrons screen the
   Coulomb barrier, raising the tunnelling probability of a reacting pair
   by a screening potential energy of tens to hundreds of electronvolts
   in the published estimates; a small fraction of the fuel is made hot by
   an external driver — in the only reproduced experiments on file,
   photoneutrons and photodissociated deuterons produced by bremsstrahlung
   above the 2.226 MeV deuteron photodissociation threshold — and reacts
   with the cold, dense, screened bulk. The defining physics is therefore
   screened tunnelling of driver-produced projectiles in a cold fuel, not a
   thermal plasma and not a beam-defined kinematics. No anomalous process
   is declared.
2. **Primary driver and energy delivery** — an electron accelerator with
   a braking target producing the bremsstrahlung field (endpoint energy,
   current, spectrum, dose rate) and the exposure geometry that places the
   loaded samples in it; alternative drivers (neutron sources, ion
   sources) are declared as driver classes, never as claims.
3. **Plant and shot lifecycle** — exposure-oriented lifecycle: hydride
   loading and characterisation, irradiation window, counting window,
   activation cool-down and sample retirement. Device-level hazard
   semantics cover the radiation field, activation of samples and
   fixtures, and hydride handling (pyrophoricity, hydrogen release).
4. **Diagnostic, reference-frame, and clock model** — exposure-cave
   coordinate conventions, driver-field monitors, neutron and gamma
   spectrometry channels with declared energy calibration and counting
   windows, and clock identities anchored to the driver's on/off events.
5. **Solver, evidence, and control-contract boundary** — versioned seams
   towards `SCPN-FUSION-CORE`, review-only semantics towards
   `SCPN-PHASE-ORCHESTRATOR`, and the device-owned CONTROL adapter
   specification towards `SCPN-CONTROL`.

## Position in the SCPN ecosystem

```
SCPN-FUSION-CORE ──(versioned seams, none active)──► SCPN-LATTICE-FUSION-CORE
                                                            │
                          reactor registry 1.1.0 ◄──── manifest pin
                                                            │
SCPN-PHASE-ORCHESTRATOR ◄──(review-only semantics)──────────┤
                                                            │
SCPN-CONTROL ◄──(adapter specification, no actuation)───────┤
                                                            │
SCPN-STUDIO ◄──(derived descriptor, not_federated)──────────┘

SCPN-CONTROL ──admitted ControlAction──► independent machine protection ──► plant
```

The reactor registry configuration this repository owns is a namespaced
extension (`scpn.reactor_systems:lattice_confinement_fusion`, family
`extension`) prepared by the research group for registry release `1.1.0`
under the family standard's route for reserved projects; the family map
carries that release as pending until the orchestrator lands and
acknowledges it, and this manifest pins the prepared release and digest.

## Repository layout

| Path | Role |
|---|---|
| `reactor-domain.json` | portable source of project identity and contracts |
| `studio/portfolio-descriptor.json` | derived Studio descriptor, `not_federated` |
| `capability-inventory.json` | generated, truthfully empty inventory |
| `docs/CONTROL_ADAPTER_SPECIFICATION.md` | device-owned adapter contract |
| `docs/THREAT_MODEL.md` | assets, trust boundaries, misuse paths |
| `docs/adr/0001-repository-boundary.md` | boundary decision record |
| `papers/` | authoritative manuscript collection (empty until a manuscript exists) |
| `tools/` | validators, derivation tools, workflow guard, preflight orchestrator |
| `tests/` | statement- and branch-complete tests for `tools/` |
| `.github/workflows/` | read-only CI definitions (no publication) |

## Contract surfaces and versioning

- `reactor-domain.json` follows schema `scpn.reactor-domain.v1`; unknown
  schemas are rejected by consumers.
- The Studio descriptor is derived deterministically and embeds the
  manifest's SHA-256; manual edits are detected as drift.
- The CONTROL adapter contract is specification-only at `0.1.0-spec`.
- SPO binding is fixed to reactor registry `1.1.0`, digest
  `6741f25892d81b24aa621ee4f56b5e785e8323eca6ccf9d9009ce2c8e53f4912`
  (the prepared group extension release); the validator cross-checks it
  against the family map's pending block until the release lands, and
  against the map's source registry afterwards.

## What would change this architecture

Landing of registry `1.1.0` by the orchestrator (a re-pin only if its
digest differs from the prepared one), acceptance of a FUSION solver seam
through the family migration gate, ratification of an SPO
`ControlIntent`-class contract, or Studio federation after a real
capability passes producer and consumer gates — each recorded as a
versioned contract change in a new ADR.
