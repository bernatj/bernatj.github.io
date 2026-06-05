---
layout: page
permalink: /forecast/
title: Live Forecast
nav: true
nav_order: 7
---

This page shows the latest **AI-based weather forecast** and **attribution signal** generated with [FourCastNetv2](https://arxiv.org/abs/2202.11214), updated daily. Forecasts are initialised from ERA5 reanalysis and run under both **factual** (current climate) and **counterfactual** (pre-industrial) conditions. The attribution signal — the difference between the two — quantifies how much anthropogenic climate change is affecting current conditions.

---

### Latest Forecast
{: .mt-3}

*Forecast initialisation date: <span id="forecast-date">–</span>*

---

#### 2-metre Temperature — Attribution Signal (Factual − Counterfactual)

<div class="row mt-3">
  <div class="col-12 col-md-6">
    <p class="text-center text-muted small">Day +3</p>
    {% include figure.liquid path="assets/img/forecast/t2m_attribution_day3.png" class="img-fluid rounded z-depth-1" zoomable=true alt="T2m attribution signal day +3" %}
  </div>
  <div class="col-12 col-md-6">
    <p class="text-center text-muted small">Day +5</p>
    {% include figure.liquid path="assets/img/forecast/t2m_attribution_day5.png" class="img-fluid rounded z-depth-1" zoomable=true alt="T2m attribution signal day +5" %}
  </div>
</div>

---

#### 500 hPa Geopotential Height — Factual Forecast

<div class="row mt-3">
  <div class="col-12 col-md-6">
    <p class="text-center text-muted small">Day +3</p>
    {% include figure.liquid path="assets/img/forecast/z500_factual_day3.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Z500 factual forecast day +3" %}
  </div>
  <div class="col-12 col-md-6">
    <p class="text-center text-muted small">Day +5</p>
    {% include figure.liquid path="assets/img/forecast/z500_factual_day5.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Z500 factual forecast day +5" %}
  </div>
</div>

---

<p class="text-muted small">
Forecasts are generated with FourCastNetv2 initialised from ERA5 reanalysis. Counterfactual conditions are obtained by subtracting the CMIP6 multi-model mean anthropogenic signal from the ERA5 initial state (pseudo-global-warming approach). See <a href="https://doi.org/10.1029/2025EF006453">Jiménez-Esteve et al. (2025)</a> for the full methodology.
</p>
