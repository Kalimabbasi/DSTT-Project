# Results Summary

All improvements are relative to the base-paper LSTM (`Baseline_LSTM`); 18 clean buildings unless stated. Significance uses Holm-adjusted Wilcoxon p < 0.05.

## Gap 1 — Feature enrichment
- `Base+Lag168h`: +9.1% mean MAE (CI 4.7–13.5), 7/8 buildings; Holm p = 0.35.
- `Phys_LSTM`: +4.6% mean / +5.7% median, 15/18 buildings (17/20 on all 20); Holm p = 0.35.
- Context, Cyclic, ResidScore, Psychrometric: +1.4% to +2.2%, CIs span zero. `Base+WeatherExtra`: −4.6%.

## Gap 2 — Transfer learning
- `Global_Transfer_LSTM`: MAE 42.39 vs 50.83 (+10.1% mean, +13.2% median), 15/18 buildings, Holm p = 0.008; Friedman mean rank 1.78 (best).
- `Pooled_Base_LSTM`: −102% mean (−18.9% median); `Pooled_Phys_LSTM`: −25.9% mean; `Global_NoMeta_LSTM`: −0.25%.
- `ZeroShot_Pooled_Phys_LSTM`: tested on 3 buildings only (1/3 improved).

## Gap 3 — Weather-noise robustness and conformal intervals
- Median MAE at σ = 0/2/4: Baseline 48.5/54.6/67.5; Phys 47.0/50.6/60.6; Phys_NoiseAug 44.8/46.0/49.3; NoWeather 58.6 constant.
- Degradation at σ = 4: Baseline 39.2%, Phys 28.8%, Phys_NoiseAug 10.0%.
- 90% conformal coverage at σ = 4: static calibration Baseline 76.2%, Phys 78.7%, NoiseAug 84.1%; noise-matched 90.1%, 90.1%, 88.8% (wider intervals, e.g. Baseline 199 → 297).
- Rolling 28-day calibration keeps coverage ≈ 86–87% with narrower intervals than noise-matched.

## Benchmarks
- Random Forest ≈ baseline (−5.8%, n.s.); Ridge −12.9% (sig.); Naive-168h −15.2% (n.s.); Naive-24h −73.1% (sig.).

## Anomaly handling (appendix, 20 buildings)
- IF, LOF, IF+LOF, Consensus, Sanitized all worse than baseline (−6% to −18% MAE); LOF, IF+LOF, Sanitized significantly worse (raw p ≤ 0.001).
- `Hybrid_Phys_Anomaly_LSTM` +6.9% (15/20), similar to `Phys_LSTM` alone (+5.3%).
- Every model has higher MAE on regime-transition days than steady days; Hybrid has the smallest gap (45.4 → 46.3).
