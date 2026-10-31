# UC mucosal score comparison workflow

Version **0.1.1** accompanies the manuscript *Information overlap and conditional outcome associations among public mucosal transcriptomic scores in ulcerative colitis*. Authors: Sheng Yao and Xiang Pan. The workflow compares fixed published scores and their conditional outcome associations; it does not train a new predictor.

Repository: https://github.com/zjupanx-hub/uc-mucosal-score-comparison

The repository distributes the workflow as `UC_code_public_v0.1.1.zip` with top-level license, citation and access files. Download and extract that archive first. Paths below refer to the extracted `uc-mucosal-score-comparison/` directory. `RELEASE_MANIFEST.json` lists files inside that directory; `DISTRIBUTION.json` at the repository root records the downloadable archive's checksum.

## Contents and data access

This repository contains the unchanged accepted core/PURSUIT calculation scripts, fixed analysis plans, dependency locks, input paths and checksums, twelve aggregate source-data tables (13 CSV files, including the original and English versions of the Data S12 role table), source citations and computational verification records. The original main cohorts are [UNIFI GSE206285](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE206285), [PROgECT GSE212849](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE212849) and [PURSUIT GSE92415](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE92415).

`DATA_INPUTS.csv` lists the 34 exact required input/acceptance files. Patient-level matrices and linked metadata, frozen third-party gene sets and patient-level acceptance snapshots are supplied separately in the complete reviewer-input kit. Their source terms remain applicable. The code repository and a fresh GEO download alone do not recreate all curated joins or frozen recipes. An actual access destination for that full kit is still being arranged; this repository does not claim to supply it.

## Layout and environment

`review_entry.py` is the common entry point. The original core is in `UC最小复跑包与初稿_2026-10-30/package/`; the separate extension is in `UC_PURSUIT有限临床调整_2026-10-30/`. Dependency versions and Windows wheel hashes are in the core folder's `requirements.lock.txt` and `requirements_windows_hashes.txt`.

The accepted configuration is Windows, Python 3.12.14 and R 4.6.1 with the locked twenty Python packages; R models use base R. Other systems or software versions have not been validated. The complete reviewer kit `UC_reviewer_kit_v0.1.1.zip` includes offline Windows wheels and a standalone common directory. Extract it to a fresh location and retain its exact curated inputs and input manifests. The older nested archive layout is unnecessary for this standalone kit.

## Execution with the complete reviewer kit

From the extracted common directory, install the offline environment without fitting models, using the actual Python and Rscript locations:

```powershell
& './UC最小复跑包与初稿_2026-10-30/package/setup_and_run.ps1' -PythonExe 'C:/path/to/python.exe' -RscriptExe 'C:/Program Files/R/R-4.6.1/bin/Rscript.exe' -EnvironmentOnly
& './UC最小复跑包与初稿_2026-10-30/package/.venv/Scripts/python.exe' -I -X utf8 ./review_entry.py --root . --mode preflight
& './UC最小复跑包与初稿_2026-10-30/package/.venv/Scripts/python.exe' -I -X utf8 ./review_entry.py --root . --mode all --rscript 'C:/Program Files/R/R-4.6.1/bin/Rscript.exe'
```

`preflight` checks required paths and hashes without fitting models. `all` runs the core scoring/statistics/UNIFI model/figure/acceptance stages and then PURSUIT preparation, models, independent numerical verification and summary. Use a fresh working directory without prior output markers. `--mode core` or `--mode pursuit` selects a workflow; `--help` lists the supported options.

## Verification and scientific scope

Accepted core calculations comprise 12,978 patient readouts, 144 endpoint estimates, correlation structures, 66 deterministic models, 30,000 bootstrap fits and 3,640 leave-one-out fits. PURSUIT separately comprises 53 deterministic models, 30,000 bootstrap fits and 590 leave-one-out fits. Scores and scaling remain fixed during regression resampling. Leave-one-out fits measure influence, not predictive cross-validation. Historical Figure 5B estimates are retained/redrawn; upstream discovery and training pipelines are not recreated.

During release preparation, the complete input kit was restored to a fresh directory, its exact files checked, twenty locked packages installed offline, scientific libraries imported and R 4.6.1 verified. This packaging check did not repeat all accepted model fits or supply new independent clinical validation. The release keeps scientific source scripts byte-identical to the accepted calculations.

## Licenses and citation

Original workflow code and documentation use the [MIT license](LICENSE). Authors' aggregate outputs in `aggregate_source_data/` use [CC BY 4.0](LICENSE_DATA.md). Third-party inputs and external software retain their original licenses. See `DATA_ACCESS.txt`, `LICENSE_STATUS.txt` and `PUBLICATION_STATUS.txt` for scope. Use `CITATION.cff` for the software and retain citations in `provenance/References_IBD.ris`. No DOI is assigned here.
