# H01_lunar_phase_v1: underpowered

> Does continuous lunar phase improve 24h probability-change forecasts beyond calendar and market controls?

Generated 2026-11-20T10:37:10Z · commit `ed474831fd4095acae7563ef0a3dc6b18367ed09` · config `7c78896071cae241` · data as of 2026-11-20T06:38:25.054240+00:00

| field | value |
| --- | --- |
| evidence state | **underpowered** |
| split | discovery |
| run | `H01_lunar_phase_v1__20261120T072924__18f59359` (2026-11-20T07:29:52.113476+00:00) |
| spec hash | `f4f2e97184ed1b46ee44d774ff16b8330364120aadde994118089026c3c896cb` |
| code commit | `07c6580f85f05b6fc4fff0a816217f9ba6223bd3-dirty` · seed 0 |
| primary metric | `mae:controls_plus_astrology_vs_controls_only`: 0.00889117 vs baseline 0.00889104 |
| primary delta | 1.28e-07 [95% CI 5.79e-09, 2.27e-07] (negative = astrology better), 112136 rows |
| distinct episodes | 18 vs minimum 20 (below minimum); sky episodes 18 |
| out-of-sample window | 2024-08-10T00:00:00+00:00 .. 2025-12-30T00:00:00+00:00 (5 folds, discovery, embargo 1 d) |
| birth convention | not_applicable |
| coverage | 112136 scored of 135111 rows; 1329 units, 463 events |

## Placebo ranks

Rank 1 = the real sky beat every placebo sky. Decision placebo: block_sky_shift.

| placebo kind | rank | placebos | empirical p | winning-variant rank | winning p |
| --- | ---: | ---: | ---: | ---: | ---: |
| sky_shift | 21 | 20 | 1 | 21 | 1 |
| block_sky_shift (decision) | 21 | 20 | 1 | 21 | 1 |

Degenerate sky-shift columns: `a__moon_phase_sin` (0.985), `a__moon_phase_cos` (0.98), `a__moon_illumination` (0.98)

## Multiple testing

| field | value |
| --- | --- |
| family | lunar_phase |
| trials_in_family | 1 |
| placebo_empirical_p | 1 |
| winning_variant | controls_plus_astrology |
| winning_empirical_p | 1 |
| bonferroni_alpha | 0.05 |
| survives_bonferroni | False |
| min_attainable_p | 0.0476 |
| decision_placebo | block_sky_shift |

## Universe filters (ledger)

| filter | value |
| --- | --- |
| categories | `all` |
| exclude_families | `['crypto_intraday']` |
| min_volume_usd | `1000` |
| venue | `polymarket_global` |
| window | `{'end': '2025-12-31T23:59:59+00:00', 'start': '2024-01-01T00:00:00+00:00'}` |

## All comparisons

| comparison | model | base | delta | 95% CI |
| --- | ---: | ---: | ---: | --- |
| `mae:controls_plus_astrology_vs_controls_only` | 0.00889117 | 0.00889104 | 1.28e-07 | [5.79e-09, 2.27e-07] |
| `mae:astrology_only_vs_market_only` | 0.00889216 | 0.00889201 | 1.48e-07 | [2.44e-08, 2.49e-07] |
| `mae:controls_plus_shuffled_astrology_vs_controls_only` | 0.00889105 | 0.00889104 | 5.83e-09 | [-1.27e-08, 2.28e-08] |
| `mae:calendar_only_vs_market_only` | 0.00889206 | 0.00889201 | 4.51e-08 | [-1.07e-07, 2.13e-07] |
| `mae:controls_only_vs_market_only` | 0.00889104 | 0.00889201 | -9.7e-07 | [-1.35e-06, -6e-07] |

## Known limitations

- underpowered: 18 distinct episodes < 20 pre-registered minimum
- universe filter (families/window) removed 17754 of 249114 rows
- universe.min_volume_usd=1000 assumed applied by the features stage (not re-checked here)
- spec controls features not in panel: underlying_return_1d
- f__log_volume_7d: 100% missing (median-imputed with indicator)
- family sports_futures is 68% of rows
- scored out-of-sample rows: 112136 of 135111 (83%); 5 folds
- sky-shift placebos are degenerate for a__moon_illumination (R2 0.980), a__moon_phase_cos (R2 0.980), a__moon_phase_sin (R2 0.985): the shifted columns lie in the linear span of the real ones (a shift only rotates lunar phase; shifts near whole lunations barely change anything); decisions use block sky-shift placebos (each lunar cycle, or event when no cycle key, gets its own randomly drawn pre-registered shift); the plain sky-shift rank is still reported

## Dataset

- name: `lunar_daily`
- saved_name: `lunar_daily_v1`
- experiment_id: `H01_lunar_phase_v1`
- built_at: `2026-11-20T07:28:23.202831+00:00`
- panel_sha256: `a29cd148e1bcf5efb9bd8e7d6a0b98d6ebe90d95a382f4dce87e59d0371f5bec`
- project_config_sha256: `7c78896071cae241bc5978a5131a6586c38f4ccd394eadb2a0093cdb1187b238`
- spec_hash: `f4f2e97184ed1b46ee44d774ff16b8330364120aadde994118089026c3c896cb`
- panel_version: `panels_v1`

---
Readings are symbolic: cards and charts illustrate measured data and are not forecasts. No experiment in the ledger has shown predictive evidence.
