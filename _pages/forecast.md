---
layout: page
permalink: /forecast/
title: Live Forecast
nav: true
nav_order: 7
---

Daily **6-day AI weather forecasts** (Pangu-Weather) initialised from ERA5 reanalysis,
run under both **factual** (current climate) and **counterfactual** (pre-industrial, PGW) conditions.
The **ACC signal** (Factual − PGW) quantifies how much anthropogenic climate change affects the current forecast,
averaged over the 2–5 day lead window (leads 48, 72, 96, 120 h).
Stippled dots mark grid points **not significant** at p < 0.05 (paired t-test across the four leads).
Z500 contours from the factual forecast are overlaid on ACC signal maps.

See <a href="https://doi.org/10.1029/2025EF006453" target="_blank">Jiménez-Esteve et al. (2025)</a> for the full methodology.

---

### 2 m Temperature (T2M)
{: .mt-4}

#### Factual forecast — 2–5 day mean
{% include figure.liquid path="assets/img/forecast/latest_pangu_t2m_factual.png" class="img-fluid rounded z-depth-1" zoomable=true alt="T2M factual forecast" %}

#### ACC signal (Factual − PGW)
{% include figure.liquid path="assets/img/forecast/latest_pangu_t2m_acc_signal.png" class="img-fluid rounded z-depth-1" zoomable=true alt="T2M ACC signal" %}

---

### 850 hPa Temperature (T850)
{: .mt-4}

#### Factual forecast — 2–5 day mean
{% include figure.liquid path="assets/img/forecast/latest_pangu_t850_factual.png" class="img-fluid rounded z-depth-1" zoomable=true alt="T850 factual forecast" %}

#### ACC signal (Factual − PGW)
{% include figure.liquid path="assets/img/forecast/latest_pangu_t850_acc_signal.png" class="img-fluid rounded z-depth-1" zoomable=true alt="T850 ACC signal" %}

---

### 500 hPa Geopotential Height (Z500)
{: .mt-4}

#### Factual forecast — 2–5 day mean
{% include figure.liquid path="assets/img/forecast/latest_pangu_z500_factual.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Z500 factual forecast" %}

#### ACC signal (Factual − PGW)
{% include figure.liquid path="assets/img/forecast/latest_pangu_z500_acc_signal.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Z500 ACC signal" %}

---

<p class="text-muted small mt-4">
<em>Last updated: 2025-11-15 18:00 UTC</em> &nbsp;·&nbsp;
Forecasts generated with <a href="https://github.com/198808xc/Pangu-Weather" target="_blank">Pangu-Weather</a>.
Counterfactual conditions use the CMIP6 multi-model mean warming delta subtracted from the ERA5 initial state
(pseudo-global-warming approach).
</p>
