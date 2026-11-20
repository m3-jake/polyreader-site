# H09_market_opening_chart_v2: no_effect_detected

> Does a market's opening-for-trading chart predict its calibration error or activity beyond listing schedule controls? (second trial: reachable power gate, 40 placebos)

Generated 2026-11-20T10:37:10Z · commit `ed474831fd4095acae7563ef0a3dc6b18367ed09` · config `7c78896071cae241` · data as of 2026-11-20T06:38:25.054240+00:00

| field | value |
| --- | --- |
| evidence state | **no_effect_detected** |
| split | discovery |
| run | `H09_market_opening_chart_v2__20261120T081103__1cf102d4` (2026-11-20T08:12:25.262337+00:00) |
| spec hash | `37a964dac09d4d2c9cdfce943dfcebd9a7a430e6036f2d2fdf8a7359c81f94eb` |
| code commit | `a18a38bcbcb6b8fe53a98165c5dcb1c1d85c2433-dirty` · seed 0 |
| primary metric | `mae:controls_plus_astrology_vs_controls_only`: 0.206497 vs baseline 0.206496 |
| primary delta | 8.13e-07 [95% CI -6.43e-07, 2.18e-06] (negative = astrology better), 1316 rows |
| distinct episodes | 50 vs minimum 40 (meets minimum); sky episodes 97 |
| out-of-sample window | 2024-04-30T14:38:29.175328+00:00 .. 2025-11-10T22:33:00+00:00 (5 folds, discovery, embargo 1 d) |
| birth convention | accepting_orders_timestamp |
| coverage | 1316 scored of 1581 rows; 1581 units, 629 events |

## Placebo ranks

Rank 1 = the real sky beat every placebo sky. Decision placebo: block_sky_shift.

| placebo kind | rank | placebos | empirical p | winning-variant rank | winning p |
| --- | ---: | ---: | ---: | ---: | ---: |
| sky_shift | 41 | 40 | 1 | 41 | 1 |
| block_sky_shift (decision) | 41 | 40 | 1 | 41 | 1 |

Degenerate sky-shift columns: `a__moon_phase_sin` (0.997), `a__moon_phase_cos` (0.996)

## Multiple testing

| field | value |
| --- | --- |
| family | entity_chart |
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
| window | `{'end': '2025-12-31T23:59:59+00:00', 'start': '2022-01-01T00:00:00+00:00'}` |

## All comparisons

| comparison | model | base | delta | 95% CI |
| --- | ---: | ---: | ---: | --- |
| `mae:controls_plus_astrology_vs_controls_only` | 0.206497 | 0.206496 | 8.13e-07 | [-6.43e-07, 2.18e-06] |
| `mae:astrology_only_vs_market_only` | 0.22274 | 0.217449 | 0.00529 | [-0.00225, 0.0119] |
| `mae:controls_plus_shuffled_astrology_vs_controls_only` | 0.206496 | 0.206496 | 1.48e-08 | [-3.28e-07, 3.92e-07] |
| `mae:calendar_only_vs_market_only` | 0.220302 | 0.217449 | 0.00285 | [-0.00425, 0.0111] |
| `mae:controls_only_vs_market_only` | 0.206496 | 0.217449 | -0.011 | [-0.0327, 0.00807] |
| `mae:log_total_volume:controls_plus_astrology_vs_controls_only` | 3.84875 | 3.09499 | 0.754 | [0.0689, 1.63] |

## Known limitations

- universe filter (families/window) removed 1 of 2197 rows
- universe.min_volume_usd=1000 assumed applied by the features stage (not re-checked here)
- spec controls features not in panel: creator_type
- 17% of rows before 2024 (thin liquidity; acceptingOrdersTimestamp absent, startDate rewritten on old markets)
- scored out-of-sample rows: 1316 of 1581 (83%); 5 folds
- sky-shift placebos are degenerate for a__moon_phase_cos (R2 0.996), a__moon_phase_sin (R2 0.997): the shifted columns lie in the linear span of the real ones (a shift only rotates lunar phase; shifts near whole lunations barely change anything); decisions use block sky-shift placebos (each lunar cycle, or event when no cycle key, gets its own randomly drawn pre-registered shift); the plain sky-shift rank is still reported
- secondary targets get bootstrap CIs only (no placebo ranking)

## Dataset

- name: `market_opening`
- saved_name: `market_opening_v1`
- experiment_id: `H09_market_opening_chart_v1`
- built_at: `2026-11-20T07:28:18.041465+00:00`
- panel_sha256: `fc07818e3856d3745eb2531e0d72f98935780b752fa60e9193f931dacf1e880c`
- project_config_sha256: `7c78896071cae241bc5978a5131a6586c38f4ccd394eadb2a0093cdb1187b238`
- spec_hash: `96cab799006c5ea0166ebe2303c1b1dce666154b79455f1c8948797b722fdd1e`
- panel_version: `panels_v1`

---
Readings are symbolic: cards and charts illustrate measured data and are not forecasts. No experiment in the ledger has shown predictive evidence.
