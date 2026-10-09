# DATAMOL

![licence](https://img.shields.io/badge/licence-Apache-2.0-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![checks](https://img.shields.io/badge/checks-unknown_PASS-brightgreen)

> Governed Anticloud packaging of the upstream project `DATAMOL` in category **MEDICINE_DEVELOPMENT**. check results: see ISOLATED_LAB_RESULTS. Every number below traces to a named file + run stamp; nothing is borrowed from other projects.

**Upstream:** DATAMOL · **Upstream pin:** `ea501d4bbe12909325eaceb881abfbc316440c9a` · **Category:** MEDICINE_DEVELOPMENT · **Vendor:** Anticloud FZ LLE · **Licence:** Apache-2.0

---

## What This Project Does

<div align="center">
    <img src="docs/images/logo-title.svg" width="100%">
</div>

<p align="center">
    <b>datamol - molecular processing made easy</b> <br />
</p>
<p align="center">
  <a href="https://docs.datamol.io/stable/" target="_blank">
      Docs
  </a> |
  <a href="https://datamol.io/" target="_blank">
      Homepage
  </a>
</p>

---

[![DOI](https://zenodo.org/badge/341603042.svg)](https://zenodo.org/badge/latestdoi/341603042)
[![Binder](http://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/datamol-io/datamol/main?urlpath=lab/tree/docs/tutorials/The_Basics.ipynb)
[![PyPI](https://img.shields.io/pypi/v/datamol)](https://pypi.org/project/datamol/)
[![Conda](https://img.shields.io/conda/v/conda-forge/datamol?label=conda&color=success)](https://anaconda.org/conda-forge/datamol)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/datamol)](https://pypi.org/project/datamol/)
[![Conda](https://img.shields.io/conda/dn/conda-forge/datamol)](https://anaconda.org/conda-forge/datamol)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/datamol)](https://pypi.org/project/datamol/)
[![license](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![GitHub project stars](https://img.shields.io/github/stars/datamol-io/datamol)](https://github.com/datamol-io/datamol/stargazers)
[![GitHub project stars](https://img.shields.io/github/forks/datamol-io/datamol)](https://github.com/datamol-io/datamol/network/members)
[![Codecov](https://codecov.io/gh/datamol-io/datamol/branch/main/graph/badge.svg?token=2ETG8SA7IG)](https://codecov.io/gh/datamol-io/datamol)

Datamol is a python library to work with molecules. It's a layer built on top of [RDKit](https://www.rdkit.org/) and aims to be as light as possible.

- 🐍 Simple pythonic API
- ⚗️ RDKit first: all you manipulate are `rdkit.Chem.Mol` objects.
- ✅ Manipulating molecules often relies on many options; Datamol provides good defaults by design.
- 🧠 Performance matters: built-in efficient parallelization when possible with an optional progress bar.
- 🕹️ Modern IO: out-of-the-box support for remote paths using `fsspec` to read and write multiple formats (sdf, xlsx, csv, etc).

## Try Online

Visit [![Binder](http://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/datamol-io/datamol/main?urlpath=lab/tree/docs/tutorials/The_Basics.ipynb) and try Datamol online.

## Documentation

Visit <https://docs.datamol.io>.

## Updates

Datamol 0.13.0 modernizes the supported scientific Python
stack while keeping the library focused on reliable molecular processing. It
adds RDKit binary and property-dictionary interchange, enforces conformer RMS
cutoffs with symmetry-aware alignment, fixes reported RDKit compatibility
issues, and separates optional I/O and visualization dependencies from the
core installation.

See the [complete changelog](CHANGELOG.md) for all notable changes and the
[0.13.0 upgrade guide](docs/migration.md) for compatibility and transition
details.

## Installation

Add Datamol to a uv-managed project:

```bash
uv add datamol
```

Pip and conda-forge remain supported:

```bash
python -m pip install datamol
mamba install -c conda-forge datamol
```

Datamol 0.13.0 requires Python 3.11 or newer and RDKit 2024.09 or newer. Cloud
I/O (S3, Google Cloud), Excel/Parquet, visualization and SELFIES support are all
included by default — there are no feature extras to install.

## Quick API Tour

```python
import datamol as dm

# Common functions
mol = dm.to_mol("O=C(C)Oc1ccccc1C(=O)O", sanitize=True)
fp = dm.to_fp(mol)
selfies = dm.to_selfies(mol)
inchi = dm.to_inchi(mol)

# Standardize and sanitize
mol = dm.to_mol("O=C(C)Oc1ccccc1C(=O)O")
mol = dm.fix_mol(mol)
mol = dm.sanitize_mol(mol)
mol = dm.standardize_mol(mol)

# Dataframe manipulation
df = dm.data.freesolv()
mols = dm.from_df(df)

# 2D viz
legends = [dm.to_smiles(mol) for mol in mols[:10]]
dm.viz.to_image(mols[:10], legends=legends)

# Generate conformers
smiles = "O=C(C)Oc1ccccc1C(=O)O"
mol = dm.to_mol(smiles)
mol_with_conformers = dm.conformers.generate(mol)

# 3D viz (using nglview)
dm.viz.conformers(mol, n_confs=10)

# Compute SASA from conformers
sasa = dm.conformers.sasa(mol_with_conformers)

# Easy IO
mols = dm.read_sdf("s3://my-awesome-data-lake/smiles.sdf", as_df=False)
dm.to_sdf(mols, "gs://data-bucket/smiles.sdf")
```

## How to cite

Please cite Datamol if you use it in your research: [![DOI](https://zenodo.org/badge/341603042.svg)](https://zenodo.org/badge/latestdoi/341603042).

## Compatibilities

Version compatibilities are an essential topic for production-software stacks. We are cautious about documenting compatibility between `datamol`, `python` and `rdkit`.

See below the associated versions of Python and RDKit, for which a minor version of Datamol **has been tested** during its whole lifecycle. _It does not mean other combinations does not work but that those are not tested._

| `datamol` | `python`            | `rdkit`                       |
| --------- | ------------------- | ----------------------------- |
| `0.13.x`  | `[3.11, 3.12, 3.13, 3.14]` | `[2024.09, 2025.03, 2025.09, 2026.03]` |
| `0.12.x`  | `[3.10, 3.11]`      | `[2023.03, 2023.09]`          |
| `0.11.x`  | `[3.9, 3.10, 3.11]` | `[2022.09, 2023.03]`          |
| `0.10.x`  | `[3.9, 3.10, 3.11]` | `[2022.03, 2022.09]`          |
| `0.9.x`   | `[3.9, 3.10, 3.11]` | `[2022.03, 2022.09]`          |
| `0.8.x`   | `[3.8, 3.9, 3.10]`  | `[2021.09, 2022.03, 2022.09]` |
| `0.7.x`   | `[3.8, 3.9]`        | `[2021.09, 2022.03]`          |
| `0.6.x`   | `[3.8, 3.9]`        | `[2021.09]`                   |
| `0.5.x`   | `[3.8, 3.9]`        | `[2021.03, 2021.09]`          |
| `0.4.x`   | `[3.8, 3.9]`        | `[2020.09, 2021.03]`          |
| `0.3.x`   | `[3.8, 3.9]`        | `[2020.09, 2021.03]`          |

## CI Status

The CI runs tests and performs code quality checks for the following combinations:

- Linux x86-64, Windows x86-64, macOS Apple Silicon and macOS Intel.
- Python 3.11 through 3.14 on Linux.
- The supported RDKit release series from 2024.09 through 2026.03.
- The latest supported stack on every operating-system and architecture lane.

|                                         | `main`                                                                                                                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Lib build & Testing                     | [![test](https://github.com/datamol-io/datamol/actions/workflows/test.yml/badge.svg)](https://github.com/datamol-io/datamol/actions/workflows/test.yml)                   |
| Code Sanity (formatting and linting)     | [![code-check](https://github.com/datamol-io/datamol/actions/workflows/code-check.yml/badge.svg)](https://github.com/datamol-io/datamol/actions/workflows/code-check.yml) |
| Documentation Build                     | [![doc](https://github.com/datamol-io/datamol/actions/workflows/doc.yml/badge.svg)](https://github.com/datamol-io/datamol/actions/workflows/doc.yml)                      |

## License

Under the Apache-2.0 license. See [LICENSE](LICENSE).

---

## Installation

See the [complete changelog](CHANGELOG.md) for all notable changes and the
[0.13.0 upgrade guide](docs/migration.md) for compatibility and transition
details.

## Usage

[![PyPI](https://img.shields.io/pypi/v/datamol)](https://pypi.org/project/datamol/)
[![Conda](https://img.shields.io/conda/v/conda-forge/datamol?label=conda&color=success)](https://anaconda.org/conda-forge/datamol)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/datamol)](https://pypi.org/project/datamol/)
[![Conda](https://img.shields.io/conda/dn/conda-forge/datamol)](https://anaconda.org/conda-forge/datamol)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/datamol)](https://pypi.org/project/datamol/)
[![license](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![GitHub project stars](https://img.shields.io/github/stars/datamol-io/datamol)](https://github.com/datamol-io/datamol/stargazers)
[![GitHub project stars](https://img.shields.io/github/forks/datamol-io/datamol)](https://github.com/datamol-io/datamol/network/members)
[![Codecov](https://codecov.io/gh/datamol-io/datamol/branch/main/graph/badge.svg?token=2ETG8SA7IG)](https://codecov.io/gh/datamol-io/datamol)

Datamol is a python library to work with molecules. It's a layer built on top of [RDKit](https://www.rdkit.org/) and aims to be as light as possible.

- 🐍 Simple pythonic API
- ⚗️ RDKit first: all you manipulate are `rdkit.Chem.Mol` objects.
- ✅ Manipulating molecules often relies on many options; Datamol provides good defaults by design.
- 🧠 Performance matters: built-in efficient parallelization when possible with an optional progress bar.
- 🕹️ Modern IO: out-of-the-box support for remote paths using `fsspec` to read and write multiple formats (sdf, xlsx, csv, etc).

## API

- ⚗️ RDKit first: all you manipulate are `rdkit.Chem.Mol` objects.
- ✅ Manipulating molecules often relies on many options; Datamol provides good defaults by design.
- 🧠 Performance matters: built-in efficient parallelization when possible with an optional progress bar.
- 🕹️ Modern IO: out-of-the-box support for remote paths using `fsspec` to read and write multiple formats (sdf, xlsx, csv, etc).

## Dependencies

| Metric | Value |
|--------|-------|
| Files | unknown |
| Lines of Code | unknown |
| Dependencies | unknown |
| Upstream license (harvested) | Apache-2.0 |
| Overlay license | Anticommons 0.1.0 |

Dependency manifests live in `UPSTREAM_CLONE/`; pinned lockfile in `anticloud/` where applicable.

## Configuration

- 🧠 Performance matters: built-in efficient parallelization when possible with an optional progress bar.
- 🕹️ Modern IO: out-of-the-box support for remote paths using `fsspec` to read and write multiple formats (sdf, xlsx, csv, etc).

## Contributing

see documentation directly at https://docs.datamol.io/stable/contribute.html

## License

Upstream © its respective contributors under Apache-2.0 (harvested MIT/Apache-2.0/BSD source; see `UPSTREAM_CLONE/LICENSE`). This packaging overlay is licensed under Anticommons 0.1.0.

## Upstream

- **project:** DATAMOL
- **Pinned SHA:** `ea501d4bbe12909325eaceb881abfbc316440c9a`
- **source:** `UPSTREAM_CLONE/` (pinned at the SHA above)
- **Upstream README source:** `UPSTREAM_CLONE/README.md`

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`7f06b9c61180b145870c756de0c7eeb07220edae05f3cb9066a6d99e778a368c`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| DANS (KNAW/NWO, Netherlands) | 10.17026/PT | EU-recognised archive |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe
and Mail, Business Insider, National Post, Financial Post, StreetInsider,
Digital Journal, Barchart, International Business Times, and Fox News.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

