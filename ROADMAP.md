<!--
SPDX-License-Identifier: AGPL-3.0-or-later
Commercial license available
© Concepts 1996–2026 Miroslav Šotek. All rights reserved.
© Code 2020–2026 Miroslav Šotek. All rights reserved.
ORCID: 0009-0009-3560-0851
Contact: www.anulum.li | protoscience@anulum.li
SCPN Lattice Fusion Core — ROADMAP
-->

# Roadmap

Planned work and implemented capability are kept strictly separate. Anything
listed under "Planned" carries no implementation, no code, and no claim in
this repository until it appears in the capability inventory with evidence.

## Implemented (repository infrastructure, not reactor capability)

- Domain manifest (`reactor-domain.json`) with validator, pinning the
  prepared registry release `1.1.0` and validating it against the family
  map's pending block.
- Derived Studio portfolio descriptor (`not_federated`) with drift check.
- Generated capability inventory (truthfully empty) with drift check.
- CONTROL adapter specification (contract only, no implementation).
- Local and workflow gate definitions (lint, typing, tests, coverage,
  REUSE, typographical check, commit-trailer guard, workflow modularity
  guard, security audit, SBOM, documentation checks).

## Planned (no implementation exists; ordering is not a commitment)

1. **Device configuration model** — typed configuration policy for the
   family (host metal and stoichiometry, loading ratio and temperature,
   driver class with endpoint energy, spectrum and dose, exposure
   geometry) with the published screening-potential ranges as a
   documented advisory, targeting `computational_prototype`.
2. **Diagnostic and clock semantics** — declared driver-field, sample-state,
   neutron and gamma spectrometry channels with driver-anchored clock
   identities, aligned with the SCPN Phase Orchestrator observability
   catalogue.
3. **Level-0 device physics** — closed forms of the published screening
   model (screened Gamow factor, enhancement of the astrophysical factor,
   hot-fuel fraction from photodissociation and photoneutron scattering)
   evaluated on the validated configuration and anchored to the sources'
   printed numbers, with native parity; planned before code in the group's
   family plan.
4. **Safety-envelope declaration** — machine-readable operational envelope
   (dose, endpoint, sample thermal, activation, hydride handling) consumed
   by the CONTROL adapter contract.
5. **CONTROL adapter implementation** — device-owned adapter against the
   published specification, with replay fixtures and HIL evidence,
   targeting `control_research_ready` only after replay and HIL
   acceptance.
6. **Facility-data correlation** — preregistered acceptance contracts
   against identified published experimental data, targeting
   `experiment_correlated` per capability.

## Not planned in this repository

Beam-defined reaction kinematics, muon catalysis, fission blankets,
thermal plasma confinement of every kind, generic controller mathematics,
machine-protection logic, any direct actuation path, and any claim of an
anomalous or unexplained nuclear process.
