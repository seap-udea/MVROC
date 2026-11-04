# MVROC pipeline products — summary

Snapshot of the tables under `pipeline/products/` for the first catalogue build.
Generated from the files present in this directory (Rubin MPC release used in the
pipeline docs; MOI selection from `code/figures/figures_MOI`).

| File | Format | Rows | Role |
|---|---|---:|---|
| `db_vro_mpc.csv` | CSV | 300 952 | Rubin ↔ MPC equivalence |
| `info_vro_mpc.md` | Markdown | — | Cross-match report |
| `db_mvroc_orbits.csv` | CSV | 298 225 | Orbital elements per MPC object |
| `db_mvroc_state.parquet` | Parquet | 8 021 267 | Per-observation geometry + \(H\) |
| `db_mvroc_moi.csv` | CSV | 703 | Objects of interest (one row / object) |
| `db_mvroc_moc.csv` | CSV | 703 | Objects with candidate light curves |
| `db_mvroc_sol.csv` | CSV | 1 092 | Rotation solutions (one row / solution) |
| `mvroc_catalogue.csv` | CSV | 1 092 | Public catalogue join (one row / solution) |

Rebuild with `python pipeline/build_products.py` from the repository root.

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

**Counts:** 300 951 unique `provid_vro`, 297 966 unique `provid_mpc`. About 2 986 MPC objects gather two Rubin provids (see `info_vro_mpc.md`).

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
| `H` | mag | Absolute magnitude (\(G=0.15\)) |
| `flag_updated` | | Recompute flag for incremental updates |

Size on disk ≈ 472 MB. `*.parquet` is gitignored.

---

## `db_mvroc_moi.csv`

MVROC Objects of Interest: asteroids with \(N_{\mathrm{obs}}\ge 100\) that passed visual
folding selection (703 objects). One row per object, with observation window,
voted period, preferred harmonic fold, colours, and the list of kept solutions.

**Sample:** \(N_{\mathrm{obs}}\) from 100 to 765 (median 351). Photometry span
2025-04-22 → 2026-04-15.

Main column groups: `epoch_utc_*`, `n_obs_*`, democratic vote (`p_rot_dem_h`,
`votes_dem`, …), preferred fold (`p_rot_h`, `chi2_nu`, …), colours (`g-r`, …),
and `solutions` / `periods_h` / `n_solutions`.

---

## `db_mvroc_moc.csv`

MVROC Objects with Candidate light curves after visual review. Same 703 objects
as MOI, slimmed to selection metadata:

`provid`, `n_obs`, `n_solutions`, `solutions`, `periods_h`, `p_rot_dem_h`, `selection`.

---

## `db_mvroc_sol.csv`

MVROC Solutions: one row per retained rotation period (1 092 solutions for 703
objects). Includes fold diagnostics, colours from the joint fit, and shape-fit
parameters (contact binary + ellipsoid).

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
| \(H_r\) filled | 98.8% |
| Shape `q_sph_k` filled | 99.5% |
| Greenstreet period match | 56 objects |
| SBDB `rot_per` match | 18 objects |

### Column blocks

1. **Identification** — `provid`, `solution_id`, `permid`, `mpc_designation`
2. **Observations** — `epoch_utc_ini/end`, `n_obs`, `n_obs_{u,g,r,i,z,y}`
3. **Orbit** — `epoch_tdb`, `a`, `e`, `q`, `incl`, `node`, `peri`, `M`
4. **Mean absolute magnitudes** — `H_u` … `H_y`
5. **Phase-corrected colours** — `u-g`, `u-r`, `g-r`, `r-i`, `i-z`, `z-y` (+ `_err`)
6. **Voted period** — `p_rot_dem_h`, `votes_dem`, `n_series_dem`, `bands_dem`, `periods_dem_h`
7. **Adopted solution** — `p_rot_h`, `chi2_nu`, `power`, `amp*`, `span_alias`, …
8. **Multiband Lk** — reserved (`p_rot_multi_*`, …); empty in this build
9. **Shape** — spheres (`q_sph_k`, `phi_sph_deg_k`, …) and ellipsoid (`b_over_a_k`, …)
10. **Classification** — `tags`, `Q`, `use_band` (empty until tagging)
11. **Reflectance** — `{b}-r_spec`, `R_{b}`, `n_{b}_spec` for \(b\in\{g,i,z,y\}\)
12. **SBDB** — `H_sbdb`, `albedo_sbdb`, `rot_per_sbdb`, taxonomy, …
13. **Greenstreet** — `rot_per_lsm_gst`, `rot_per_fr_gst`
14. **Dynamics** — `res_*` reserved (all NaN)

For the detailed meaning of each catalogue column, see
[`CATALOGUE.md`](../../CATALOGUE.md) at the repository root.
For the pipeline steps that produce these tables, see
[`code/PIPELINE.md`](../../code/PIPELINE.md).
