---
layout: page
permalink: /research/dana-adam-2026/
title: DANA Adam — October 2026
description: Rapid AI-based climate-change attribution of the DANA Adam extreme rainfall event (17–20 October 2026)
nav: false
---

<p style="font-size: 1.05em;">
<strong>Rapid attribution assessment</strong> · B. Jiménez-Esteve, D. Barriopedro, R. García-Herrera · IGEO (CSIC–UCM) · 2 November 2026<br>
<a href="https://digital.csic.es/handle/10261/448760" target="_blank">📄 Full report (PDF) at Digital.CSIC →</a>
</p>

From 17 to 20 October 2026, **DANA Adam**, a high-impact cut-off low named by AEMET on 16 October, brought extreme rainfall to eastern Spain and the western Mediterranean, particularly La Safor (Valencia) and Marina Alta (Alicante). AVAMET recorded about 723 mm at Forna (l'Atzúbia) during the episode, almost all of it on 18 and 19 October.

We used ECMWF's AI Forecasting System (**AIFS**) to quantify the influence of climate change on this event, comparing forecasts under present-day and pre-industrial climate conditions.

**Key findings**

- On **18 October**, the peak precipitation day, regional rainfall was **16% higher** in the present-day climate than in a world without anthropogenic influences.
- Over the full **60-hour episode**, climate change increased precipitation by **8%**.
- The intensification is associated with increased atmospheric moisture (~10–15% more total-column water), but changes in rainfall timing, spatial distribution and local circulation also influence the response.
- These results are specific to the observed event; they do not assess changes in its likelihood or in local-scale precipitation extremes.

---

## The event

An upper-level trough extended into France on 17 October and developed into a cut-off low over western France by 18 October. Southwesterly flow aloft and moist northeasterly flow near the surface favoured heavy precipitation along the eastern Iberian coast. On 19 October the low moved towards the Bay of Biscay and precipitation extended towards Catalonia and the Gulf of Lion, before the system weakened and moved east on 20–21 October.

{% include figure.liquid path="assets/img/dana_adam2026_era5_precip_z500.png" class="img-fluid rounded z-depth-1" zoomable=true caption="ERA5 daily precipitation (shading, mm) and daily-mean 500 hPa geopotential height (contours, dam) during 16–21 October 2026. The dashed box is the attribution region (38–42°N, 1°W–3.5°E)." %}

---

## Method

We apply the **forecast-based storyline attribution** approach developed in [Jiménez-Esteve et al. (2025)](https://doi.org/10.1029/2025EF006453) and [Jiménez-Esteve et al. (2026)](https://doi.org/10.1088/2752-5295/ae714b), and previously used for the October 2024 Valencia floods ([Barriopedro et al., 2025](https://doi.org/10.1175/BAMS-D-25-0049.1)). AIFS Single v1.0 forecasts initialized from ERA5 (factual) are compared with forecasts from initial states in which the anthropogenic climate-change signal has been removed (counterfactual, pre-industrial), following the pseudo-global warming technique. The counterfactual uses the 30-model CMIP6 mean difference between 2010–2040 (SSP5-8.5) and 1850–1900 (1.53 K colder). Forecasts are initialized every six hours (35 initializations per experiment), and factual and counterfactual runs are compared at lead times of 24–96 h.

AIFS captures the coastal concentration and timing of the 18 October rain band well: the box-mean daily accumulation is 27.6 mm, close to the ERA5 value of 27.3 mm. The grid-cell maximum is underestimated (92.5 vs 116.3 mm), so the assessment is regional and should not be extrapolated to the most intense local rainfall.

{% include figure.liquid path="assets/img/dana_adam2026_aifs_factual_eval.png" class="img-fluid rounded z-depth-1" zoomable=true caption="18 October 2026 (00–24 UTC), the peak precipitation day: ERA5 and factual AIFS forecasts at 24–120 h lead times. Grey contours: 500 hPa geopotential height (dam); magenta: mean sea-level pressure (hPa). Dashed box: attribution region." %}

---

## Attribution results

| Metric             | Factual (mm) | Counterfactual (mm) | Difference (mm) | Relative change |
| ------------------ | -----------: | ------------------: | --------------: | --------------: |
| 18 Oct box mean    |         27.6 |                23.8 |            +3.7 |        **+16%** |
| 18 Oct box maximum |         92.5 |                81.1 |           +11.4 |            +15% |
| 60-h box mean      |         50.5 |                46.8 |            +3.6 |         **+8%** |
| 60-h box maximum   |        127.1 |               116.2 |           +10.9 |             +9% |

The precipitation enhancement develops during the peak phase, reaching about +1.5 mm per six hours around 18 October 12 UTC. Later, during 19 October, precipitation declines earlier in the factual forecasts, partly offsetting the peak-day increase and reducing the episode response from +16% to +8%.

{% include figure.liquid path="assets/img/dana_adam2026_precip_timeseries_boxmean.png" class="img-fluid rounded z-depth-1" zoomable=true caption="Six-hour box-mean precipitation from ERA5, factual (CTRL) and counterfactual (PGW) AIFS forecasts, and their paired difference. Shading: 10th–90th percentile range across the 13 lead times (24–96 h). Right: event (60 h) and peak-day totals. The p-values shown should not be interpreted as independent-sample significance tests, since lagged forecasts are correlated." %}

The response is spatially heterogeneous: on 18 October, precipitation increases along the Valencian coast and the adjacent Balearic Sea, with decreases further inland. These changes occur in a warmer (~2 K at 850 hPa) and moister atmosphere, broadly consistent with Clausius–Clapeyron scaling, while changes in vertical motion, sea-level pressure and low-level winds suggest local dynamical adjustments that may partly offset the thermodynamic intensification.

{% include figure.liquid path="assets/img/dana_adam2026_acc_maps_peakday.png" class="img-fluid rounded z-depth-1" zoomable=true caption="Peak precipitation day, 18 October 2026: factual-minus-counterfactual changes in (a) accumulated precipitation, (b) total-column water, (c) 500 hPa vertical velocity (positive = weaker ascent), (d) sea-level pressure, (e) 850 hPa wind speed and (f) 850 hPa temperature. Contours show factual fields; stippling indicates p ≥ 0.05 (Welch test on lagged forecasts)." %}

An independent weather model, alternative PGW perturbations, gauge/radar evaluation and a moisture-budget analysis would add robustness to these results. See the [full report](https://digital.csic.es/handle/10261/448760) for details.
