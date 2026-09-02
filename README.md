<!--
SPDX-License-Identifier: AGPL-3.0-or-later
Commercial license available
© Concepts 1996–2026 Miroslav Šotek. All rights reserved.
© Code 2020–2026 Miroslav Šotek. All rights reserved.
ORCID: 0009-0009-3560-0851
Contact: www.anulum.li | protoscience@anulum.li
SCPN Lattice Fusion Core — README
-->

# SCPN Lattice Fusion Core

Governed device-family repository for lattice-confinement fusion research
within the SCPN Reactor Systems Research Group. This repository is the
designated owner of device-level truth for the namespaced extension
configuration `scpn.reactor_systems:lattice_confinement_fusion` of the
SCPN Phase Orchestrator reactor registry (release `1.1.0`, prepared by the
group as a namespaced extension of the 32 built-in configurations and
carried in the family map as a pending release until the orchestrator
lands it).

**Evidence maturity: `architecture_only`.** No reactor capability is
implemented: the repository holds the device boundary, its ecosystem
contracts, the device-owned CONTROL adapter specification and the
validation tooling that enforces the truthfulness of that state. The
capability and claim inventories are empty and verified by the domain
validator.

## Scope

This repository owns, for the lattice-confinement device family:

- the device boundary: plant and experiment truth, exposure lifecycle, and
  configuration policy for systems in which hydrogen isotopes are loaded at
  high density into a metal lattice (deuterated erbium, titanium and
  similar hydrides), the lattice's conduction and shell electrons screen
  the Coulomb barrier, and a small fraction of the fuel is made hot by an
  external driver — in the only reproduced experiments on file,
  photoneutrons and photodissociated deuterons from bremsstrahlung above
  the deuteron photodissociation threshold (NASA Glenn, 2020);
- host-lattice and loading semantics as device truth: metal and
  stoichiometry, loading ratio, temperature and hydride state; driver
  declarations (electron-beam endpoint energy, photon spectrum, dose and
  exposure geometry); screening-potential declarations as inputs with
  their published ranges, never as claims;
- diagnostic semantics, reference frames, and clock identity declarations
  (neutron and gamma spectrometry around an exposure, counting windows,
  activation cool-down);
- actuator-response model boundaries and the declared safety envelope
  (radiation, activation, hydride handling);
- the device-owned CONTROL adapter specification;
- the binding to the SCPN Phase Orchestrator reactor registry (release
  `1.1.0`, digest
  `6741f25892d81b24aa621ee4f56b5e785e8323eca6ccf9d9009ce2c8e53f4912`);
- the machine-readable domain manifest `reactor-domain.json` and the derived
  Studio portfolio descriptor (integration state `not_federated`).

## Explicit exclusions

- **Accelerator beam-on-target reaction kinematics**:
  `SCPN-BEAM-TARGET-CORE`. The lattice family's projectiles are secondary
  particles produced inside a cold dense fuel by a photon driver, not a
  beam-defined kinematics.
- **Muon-catalysed fusion**: `SCPN-MUON-FUSION-CORE`.
- **Fission blankets and hybrid plant systems**:
  `SCPN-FUSION-FISSION-HYBRID-CORE`.
- **Thermal plasma confinement of every kind**: the magnetic, inertial and
  magneto-inertial device families of the group.
- **Solver mathematics and validation evidence**: `SCPN-FUSION-CORE` until
  an exact surface passes the reactor family migration gate; no solver code
  exists in, or was copied into, this repository.
- **Typed signal semantics and comparability**: `SCPN-PHASE-ORCHESTRATOR`
  (review-only output; never actuation).
- **Control admission and action formation**: `SCPN-CONTROL` is the sole
  software authority that forms an admitted `ControlAction`.
- **Machine protection**: independent systems retain the final veto.
- **Portfolio presentation, identity, entitlement, and execution gating**:
  `SCPN-STUDIO`.

## Non-claims

This repository is not machine-ready, not safety-certified, and not
reactor-ready. It contains no implemented solver, no controller, no
benchmark result, no experimental correlation, no dataset, and no
deployable artefact, and no parameter describes or validates any real
apparatus. No anomalous or unexplained nuclear process is declared: the
only physics this family declares is the screened tunnelling of
driver-produced hot projectiles in a cold deuterated lattice as published
in the sources it cites, and every future model carries that statement.
Host-metal, loading and driver choices are configuration facets, not
separate claims. No capability has reached any evidence-maturity state.

## Architecture

The five-surface boundary and the position of this repository in the SCPN
ecosystem are defined in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) and
fixed by
[`docs/adr/0001-repository-boundary.md`](docs/adr/0001-repository-boundary.md).
The threat model is in [`docs/THREAT_MODEL.md`](docs/THREAT_MODEL.md); the
CONTROL adapter contract is in
[`docs/CONTROL_ADAPTER_SPECIFICATION.md`](docs/CONTROL_ADAPTER_SPECIFICATION.md).

## Validation

Every gate currently active in this repository is listed in
[`VALIDATION.md`](VALIDATION.md). The local sequence is:

```bash
make lint        # ruff check + ruff format --check
make typecheck   # mypy --strict tools tests
make test        # pytest with 100 % statement and branch coverage on tools/
make validate    # domain manifest, descriptor, and inventory checks
make preflight   # the full fail-closed gate sequence
```

## Security

See [`SECURITY.md`](SECURITY.md) for the supported states and the private
reporting route (protoscience@anulum.li).

## Licensing

AGPL-3.0-or-later for the public repository, with a commercial licence
available (see [`NOTICE.md`](NOTICE.md)). Licence texts are under
[`LICENSES/`](LICENSES/); machine-readable licensing metadata follows
REUSE 3.x (`REUSE.toml`).

## Citation

Citation metadata is provided in [`CITATION.cff`](CITATION.cff). No release,
version, or DOI exists yet; cite the repository state you inspected.
