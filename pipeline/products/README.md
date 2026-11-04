# MVROC pipeline products — summary

Result of the MVROC pipeline run of **4 November 2026**.

Input observations: `code/data/obs_sbn_X05_full.parquet` (downloaded **12 October 2026**; 8 078 546 rows). Candidate light curves (MOC) from `code/figures/figures_MOI`.

| File | Format | Rows | Role |
|---|---|---:|---|
| `code/data/obs_sbn_X05_full.parquet` | Parquet | 8 078 546 | Original Rubin MPC observations (12 October 2026) |
| `db_vro_mpc.csv` | CSV | 300 952 | Rubin ↔ MPC equivalence |
| `db_mvroc_orbits.csv` | CSV | 298 225 | Orbital elements per MPC object |
| `db_mvroc_state.parquet` | Parquet | 8 021 267 | Per-observation geometry + H |
| `db_mvroc_moi.parquet` | Parquet | 1 962 044 obs<br>(8 000 objects) | MOI observations (objects in `figures/figures_nobs`; same columns as the source parquet) |
| `db_mvroc_moc.csv` | CSV | 703 | MOC: objects with candidate light curves (visual selection) |
| `db_mvroc_sol.csv` | CSV | 1 092 | Rotation solutions (one row / solution) |
| `mvroc_catalogue.csv` | CSV | 1 092 | Public catalogue join (one row / solution) |

---

## `db_vro_mpc.csv`

Equivalence table from pipeline step 2 (Rubin–MPC cross-match).

| Column | Meaning |
|---|---|
| `provid_vro` | Rubin provisional designation |
| `provid_mpc` | Matched MPC designation |
| `permid` | Permanent number when available |
| `match_kind` | `numbered` or `provisional` |
| `n_vro_for_mpc` | How many Rubin ids map to this MPC designation |

**Counts:** 300 951 unique `provid_vro`, 297 966 unique `provid_mpc`. About 2 986 MPC objects gather two Rubin provids.

---

## `db_mvroc_orbits.csv`

Orbital elements at the reported epoch for each `provid_mpc` (pipeline step 3).

| Column | Unit | Meaning |
|---|---|---|
| `provid_vro` | | One Rubin id attached to the orbit row |
| `provid_mpc` | | MPC designation (unique key) |
| `permid` | | Permanent number |
| `epoch_tdb` | TDB | Epoch of the elements |
| `a` | au | Semimajor axis |
| `e` | | Eccentricity |
| `q` | au | Perihelion distance |
| `incl` | deg | Inclination |
| `node` | deg | Longitude of ascending node |
| `peri` | deg | Argument of perihelion |
| `M` | deg | Mean anomaly |

---

## `db_mvroc_state.parquet`

One row per observation with geometry and absolute magnitude (pipeline steps 4–5).
Primary key: observation `id`.

| Column | Unit | Meaning |
|---|---|---|
| `id` | | Observation id from the Rubin MPC table (~99.3% filled) |
| `provid_vro` | | Rubin designation |
| `provid_mpc` | | Matched MPC designation |
| `permid` | | Permanent number |
| `obstime` | UTC | Observation time |
| `obs_et` | s | Ephemeris time |
| `deltat` | d | Days from orbital epoch to observation (TDB) |
| `r` | au | Heliocentric distance |
| `delta` | au | Geocentric distance |
| `alpha` | deg | Phase angle |
| `mag` | mag | Apparent magnitude |
| `H` | mag | Absolute magnitude (G = 0.15) |
| `flag_updated` | | Recompute flag for incremental updates |

Size on disk ≈ 472 MB. `*.parquet` is gitignored.

---

## `db_mvroc_moi.parquet`

**MOI — MVROC Objects of Interest.** Objects processed in
`code/figures/figures_nobs` (including `updateH/`), i.e. the N_obs ≥ 100
selection of the pipeline — **not** the visually selected rotation candidates
(those are MOC).

One row per observation. Columns are exactly those of the source file
`code/data/obs_sbn_X05_full.parquet` (90 columns). This build:

| Quantity | Value |
|---|---|
| Distinct objects (`provid_mpc`) | 8 000 |
| Distinct `provid` | 8 010 |
| Observation rows | 1 962 044 |
| File size | ≈ 143 MB |

Ten MPC designations gather two Rubin `provid` each; counting unique `provid_mpc` gives 8 000 physical objects.

Photometric periods, colours, and shape fits are **not** stored here; they
appear later in `db_mvroc_moc.csv`, `db_mvroc_sol.csv`, and `mvroc_catalogue.csv`.

---

## `db_mvroc_moc.csv`

**MOC — MVROC Objects with Candidate light curves.** Objects whose folded light
curves were retained after visual review (703 asteroids in this build).

Columns: `provid`, `n_obs`, `n_solutions`, `solutions`, `periods_h`,
`p_rot_dem_h`, `selection`.

**Sample (this build):** N_obs from 100 to 765 (median 351).
Photometry span 2025-04-22 → 2026-04-15.

---

## `db_mvroc_sol.csv`

MVROC Solutions: one row per retained rotation period (1 092 solutions for the
703 MOC objects). Includes fold diagnostics, colours from the joint fit, and
shape-fit parameters (contact binary + ellipsoid).

| Solutions per object | Objects |
|---:|---:|
| 1 | 386 |
| 2 | 248 |
| 3 | 66 |
| 4 | 3 |

**Period range:** 0.063–44.1 h (median ≈ 4.85 h).

Classification columns `tags`, `Q`, and `use_band` are reserved (empty in this
build; see `code/CLASSIFICATION.md`).

---

## `mvroc_catalogue.csv`

End product of the pipeline: **one row per solution**, with the full object
information described in `CATALOGUE.md` joined onto each solution.

| Quantity | Value |
|---|---|
| Rows (solutions) | 1 092 |
| Columns | 137 |
| Unique objects | 703 |
| Orbits filled (`a`) | 100% |
| H_r filled | 98.8% |
| Shape `q_sph_k` filled | 99.5% |
| Greenstreet period match | 56 objects |
| SBDB `rot_per` match | 18 objects |

### Column blocks

1. **Identification** — `provid`, `solution_id`, `permid`, `mpc_designation`
2. **Observations** — `epoch_utc_ini/end`, `n_obs`, `n_obs_u` … `n_obs_y`
3. **Orbit** — `epoch_tdb`, `a`, `e`, `q`, `incl`, `node`, `peri`, `M`
4. **Mean absolute magnitudes** — `H_u` … `H_y`
5. **Phase-corrected colours** — `u-g`, `u-r`, `g-r`, `r-i`, `i-z`, `z-y` (+ `_err`)
6. **Voted period** — `p_rot_dem_h`, `votes_dem`, `n_series_dem`, `bands_dem`, `periods_dem_h`
7. **Adopted solution** — `p_rot_h`, `chi2_nu`, `power`, `amp*`, `span_alias`, …
8. **Multiband Lk** — reserved (`p_rot_multi_*`, …); empty in this build
9. **Shape** — spheres (`q_sph_k`, `phi_sph_deg_k`, …) and ellipsoid (`b_over_a_k`, …)
10. **Classification** — `tags`, `Q`, `use_band` (empty until tagging)
11. **Reflectance** — `{b}-r_spec`, `R_b`, `n_b_spec` for b ∈ {g, i, z, y}
12. **SBDB** — `H_sbdb`, `albedo_sbdb`, `rot_per_sbdb`, taxonomy, …
13. **Greenstreet** — `rot_per_lsm_gst`, `rot_per_fr_gst`
14. **Dynamics** — `res_*` reserved (all NaN)

For the detailed meaning of each catalogue column, see
[`CATALOGUE.md`](../../CATALOGUE.md) at the repository root.
For the pipeline steps that produce these tables, see
[`code/PIPELINE.md`](../../code/PIPELINE.md).
