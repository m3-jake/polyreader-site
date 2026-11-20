# H01_lunar_phase_v2: underpowered

> Does continuous lunar phase improve 24h probability-change forecasts beyond calendar and market controls? (second trial: earlier window start, 40 placebos)

Generated 2026-11-20T10:37:10Z · commit `ed474831fd4095acae7563ef0a3dc6b18367ed09` · config `7c78896071cae241` · data as of 2026-11-20T06:38:25.054240+00:00

| field | value |
| --- | --- |
| evidence state | **underpowered** |
| split | discovery |
| run | `H01_lunar_phase_v2__20261120T081001__1e2f1f45` (2026-11-20T08:10:59.654779+00:00) |
| spec hash | `9ef827fd8330a127f8e2541c5dcd5ec2d1c30bd497351347bddbb27be781038b` |
| code commit | `a18a38bcbcb6b8fe53a98165c5dcb1c1d85c2433-dirty` · seed 0 |
| primary metric | `mae:controls_plus_astrology_vs_controls_only`: 0.00890467 vs baseline 0.00890465 |
| primary delta | 1.81e-08 [95% CI -8.28e-08, 1.13e-07] (negative = astrology better), 117320 rows |
| distinct episodes | 19 vs minimum 20 (below minimum); sky episodes 19 |
| out-of-sample window | 2024-07-18T00:00:00+00:00 .. 2025-12-30T00:00:00+00:00 (5 folds, discovery, embargo 1 d) |
| birth convention | not_applicable |
| coverage | 117320 scored of 145732 rows; 1442 units, 537 events |

## Placebo ranks

Rank 1 = the real sky beat every placebo sky. Decision placebo: block_sky_shift.

| placebo kind | rank | placebos | empirical p | winning-variant rank | winning p |
| --- | ---: | ---: | ---: | ---: | ---: |
| sky_shift | 41 | 40 | 1 | 41 | 1 |
| block_sky_shift (decision) | 41 | 40 | 1 | 41 | 1 |

Degenerate sky-shift columns: `a__moon_phase_sin` (0.987), `a__moon_phase_cos` (0.985), `a__moon_illumination` (0.985)

## Multiple testing

| field | value |
| --- | --- |
| family | lunar_phase |
| trials_in_family | 2 |
| placebo_empirical_p | 1 |
| winning_variant | controls_plus_astrology |
| winning_empirical_p | 1 |
| bonferroni_alpha | 0.025 |
| survives_bonferroni | False |
| min_attainable_p | 0.0244 |
| decision_placebo | block_sky_shift |

## Universe filters (ledger)

| filter | value |
| --- | --- |
| categories | `all` |
| exclude_families | `['crypto_intraday']` |
| min_volume_usd | `1000` |
| venue | `polymarket_global` |
| window | `{'end': '2025-12-31T23:59:59+00:00', 'start': '2023-01-01T00:00:00+00:00'}` |

## All comparisons

| comparison | model | base | delta | 95% CI |
| --- | ---: | ---: | ---: | --- |
| `mae:controls_plus_astrology_vs_controls_only` | 0.00890467 | 0.00890465 | 1.81e-08 | [-8.28e-08, 1.13e-07] |
| `mae:astrology_only_vs_market_only` | 0.00890582 | 0.0089058 | 1.83e-08 | [-8.27e-08, 1.13e-07] |
| `mae:controls_plus_shuffled_astrology_vs_controls_only` | 0.00890462 | 0.00890465 | -2.81e-08 | [-8.95e-08, 3.99e-08] |
| `mae:calendar_only_vs_market_only` | 0.00890586 | 0.0089058 | 6.25e-08 | [-3.14e-07, 4.37e-07] |
| `mae:controls_only_vs_market_only` | 0.00890465 | 0.0089058 | -1.15e-06 | [-1.64e-06, -5.88e-07] |

## Known limitations

- underpowered: 19 distinct episodes < 20 pre-registered minimum
- universe filter (families/window) removed 17754 of 259735 rows
- universe.min_volume_usd=1000 assumed applied by the features stage (not re-checked here)
- spec controls features not in panel: underlying_return_1d
- f__log_volume_7d: 100% missing (median-imputed with indicator)
- f__abs_change_7d: 6% missing (median-imputed with indicator)
- 7% of rows before 2024 (thin liquidity; acceptingOrdersTimestamp absent, startDate rewritten on old markets)
- family sports_futures is 63% of rows
- scored out-of-sample rows: 117320 of 145732 (81%); 5 folds
- sky-shift placebos are degenerate for a__moon_illumination (R2 0.985), a__moon_phase_cos (R2 0.985), a__moon_phase_sin (R2 0.987): the shifted columns lie in the linear span of the real ones (a shift only rotates lunar phase; shifts near whole lunations barely change anything); decisions use block sky-shift placebos (each lunar cycle, or event when no cycle key, gets its own randomly drawn pre-registered shift); the plain sky-shift rank is still reported

## Dataset

- name: `lunar_daily`
- saved_name: `lunar_daily_v2`
- experiment_id: `H01_lunar_phase_v2`
- built_at: `2026-11-20T08:09:21.293449+00:00`
- panel_sha256: `fae52f9559d2350784c7d8e4aab21dd752fbdfb979a9d6d13872898e6220a7b8`
- project_config_sha256: `7c78896071cae241bc5978a5131a6586c38f4ccd394eadb2a0093cdb1187b238`
- spec_hash: `9ef827fd8330a127f8e2541c5dcd5ec2d1c30bd497351347bddbb27be781038b`
- panel_version: `panels_v1`

---
Readings are symbolic: cards and charts illustrate measured data and are not forecasts. No experiment in the ledger has shown predictive evidence.
