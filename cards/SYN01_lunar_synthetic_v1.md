# SYN01_lunar_synthetic_v1: exploratory

> Synthetic: does lunar phase improve 24h change forecasts beyond calendar controls?

Generated 2026-11-20T10:37:10Z · commit `ed474831fd4095acae7563ef0a3dc6b18367ed09` · config `7c78896071cae241` · data as of 2026-11-20T06:38:25.054240+00:00

| field | value |
| --- | --- |
| evidence state | **exploratory** |
| split | discovery |
| run | `SYN01_lunar_synthetic_v1__20261120T072435__baa096a7` (2026-11-20T07:24:40.822461+00:00) |
| spec hash | `2a70f00891cd2535cbbfd0b17e1e7b86b535860626377e6fdd4f02ddd280c6f1` |
| code commit | `07c6580f85f05b6fc4fff0a816217f9ba6223bd3-dirty` · seed 5 |
| primary metric | `mae:controls_plus_astrology_vs_controls_only`: 0.0207508 vs baseline 0.0213313 |
| primary delta | -0.000581 [95% CI -0.000789, -0.000294] (negative = astrology better), 5027 rows |
| distinct episodes | 17 vs minimum 12 (meets minimum); sky episodes 17 |
| out-of-sample window | 2024-08-14T00:00:00+00:00 .. 2025-11-23T00:00:00+00:00 (5 folds, discovery, embargo 1 d) |
| birth convention | not_applicable |
| coverage | 5027 scored of 6049 rows; 100 units, 33 events |

## Placebo ranks

Rank 1 = the real sky beat every placebo sky. Decision placebo: block_sky_shift.

| placebo kind | rank | placebos | empirical p | winning-variant rank | winning p |
| --- | ---: | ---: | ---: | ---: | ---: |
| sky_shift | 3 | 20 | 0.143 | 3 | 0.143 |
| block_sky_shift (decision) | 1 | 20 | 0.0476 | 1 | 0.0476 |

Degenerate sky-shift columns: `a__moon_phase_sin` (0.99), `a__moon_phase_cos` (0.99), `a__moon_illumination` (0.99)

## Multiple testing

| field | value |
| --- | --- |
| family | synthetic_lunar |
| trials_in_family | 1 |
| placebo_empirical_p | 0.0476 |
| winning_variant | controls_plus_astrology |
| winning_empirical_p | 0.0476 |
| bonferroni_alpha | 0.05 |
| survives_bonferroni | True |
| min_attainable_p | 0.0476 |
| decision_placebo | block_sky_shift |

## Universe filters (ledger)

| filter | value |
| --- | --- |
| categories | `all` |
| exclude_families | `['crypto_intraday']` |
| min_volume_usd | `0` |
| venue | `polymarket_global` |
| window | `{'end': '2025-12-31T23:59:59+00:00', 'start': '2024-01-01T00:00:00+00:00'}` |

## All comparisons

| comparison | model | base | delta | 95% CI |
| --- | ---: | ---: | ---: | --- |
| `mae:controls_plus_astrology_vs_controls_only` | 0.0207508 | 0.0213313 | -0.000581 | [-0.000789, -0.000294] |
| `mae:astrology_only_vs_market_only` | 0.0207508 | 0.0213313 | -0.000581 | [-0.000789, -0.000294] |
| `mae:controls_plus_shuffled_astrology_vs_controls_only` | 0.0213313 | 0.0213313 | -1.98e-08 | [-4.86e-08, 1.41e-08] |
| `mae:calendar_only_vs_market_only` | 0.0213313 | 0.0213313 | 2.97e-09 | [-4.88e-08, 5.79e-08] |
| `mae:controls_only_vs_market_only` | 0.0213313 | 0.0213313 | 3.99e-08 | [-3.16e-08, 1.23e-07] |
| `mae:abs_price_change_24h:controls_plus_astrology_vs_controls_only` | 0.0130157 | 0.0130158 | -3.93e-08 | [-9.55e-08, 1.6e-08] |

## Known limitations

- universe.min_volume_usd=0 assumed applied by the features stage (not re-checked here)
- f__log_volume_7d: 8% missing (median-imputed with indicator)
- f__abs_change_7d: 12% missing (median-imputed with indicator)
- scored out-of-sample rows: 5027 of 6049 (83%); 5 folds
- sky-shift placebos are degenerate for a__moon_illumination (R2 0.990), a__moon_phase_cos (R2 0.990), a__moon_phase_sin (R2 0.990): the shifted columns lie in the linear span of the real ones (a shift only rotates lunar phase; shifts near whole lunations barely change anything); decisions use block sky-shift placebos (each lunar cycle, or event when no cycle key, gets its own randomly drawn pre-registered shift); the plain sky-shift rank is still reported
- secondary targets get bootstrap CIs only (no placebo ranking)

---
Readings are symbolic: cards and charts illustrate measured data and are not forecasts. No experiment in the ledger has shown predictive evidence.
