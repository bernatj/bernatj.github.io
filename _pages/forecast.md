---
layout: page
permalink: /forecast/
title: Live Forecast
nav: true
nav_order: 7
---

Daily **6-day AI weather forecasts** initialised from ERA5 reanalysis, run under both
**factual** (current climate) and **counterfactual** (pre-industrial, PGW) conditions.
The **ACC signal** = Factual − PGW, averaged over the 2–5 day lead window (48, 72, 96, 120 h).
Stippled dots: **not significant** at p < 0.05.  Z500 factual contours are overlaid.

See <a href="https://doi.org/10.1029/2025EF006453" target="_blank">Jiménez-Esteve et al. (2025)</a> for methodology.

---

<!-- Model selector -->
<div style="display:flex; gap:10px; margin:20px 0 28px;">
  <button id="btn-pangu" onclick="selectModel('pangu')"
    style="padding:8px 22px; background:#1a73e8; color:#fff; border:none; border-radius:6px; cursor:pointer; font-weight:600; font-size:14px;">
    Pangu-Weather
  </button>
  <button id="btn-fcnv2" onclick="selectModel('fcnv2')"
    style="padding:8px 22px; background:#e9ecef; color:#444; border:none; border-radius:6px; cursor:pointer; font-size:14px;">
    FourCastNet v2
  </button>
</div>

<!-- Pangu-Weather maps -->
<div id="model-pangu">

### 850 hPa Temperature — Attribution Signal
{: .mt-3}

**Global**
{% include figure.liquid path="assets/img/forecast/latest_pangu_t850_acc_signal.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Pangu T850 ACC signal global" %}

**Europe**
{% include figure.liquid path="assets/img/forecast/latest_pangu_t850_acc_signal_europe.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Pangu T850 ACC signal Europe" %}

---

### 500 hPa Geopotential Height — Attribution Signal
{: .mt-3}

**Global**
{% include figure.liquid path="assets/img/forecast/latest_pangu_z500_acc_signal.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Pangu Z500 ACC signal global" %}

**Europe**
{% include figure.liquid path="assets/img/forecast/latest_pangu_z500_acc_signal_europe.png" class="img-fluid rounded z-depth-1" zoomable=true alt="Pangu Z500 ACC signal Europe" %}

</div>

<!-- FourCastNet v2 maps -->
<div id="model-fcnv2" style="display:none;">

### 850 hPa Temperature — Attribution Signal
{: .mt-3}

**Global**
{% include figure.liquid path="assets/img/forecast/latest_fcnv2_t850_acc_signal.png" class="img-fluid rounded z-depth-1" zoomable=true alt="FCNv2 T850 ACC signal global" %}

**Europe**
{% include figure.liquid path="assets/img/forecast/latest_fcnv2_t850_acc_signal_europe.png" class="img-fluid rounded z-depth-1" zoomable=true alt="FCNv2 T850 ACC signal Europe" %}

---

### 500 hPa Geopotential Height — Attribution Signal
{: .mt-3}

**Global**
{% include figure.liquid path="assets/img/forecast/latest_fcnv2_z500_acc_signal.png" class="img-fluid rounded z-depth-1" zoomable=true alt="FCNv2 Z500 ACC signal global" %}

**Europe**
{% include figure.liquid path="assets/img/forecast/latest_fcnv2_z500_acc_signal_europe.png" class="img-fluid rounded z-depth-1" zoomable=true alt="FCNv2 Z500 ACC signal Europe" %}

</div>

<script>
function selectModel(m) {
  ['pangu','fcnv2'].forEach(function(n) {
    document.getElementById('model-'+n).style.display = (m===n) ? 'block' : 'none';
    var b = document.getElementById('btn-'+n);
    b.style.background = (m===n) ? '#1a73e8' : '#e9ecef';
    b.style.color      = (m===n) ? '#fff'    : '#444';
    b.style.fontWeight = (m===n) ? '600'     : '400';
  });
}
</script>

---

<p class="text-muted small mt-4">
<em>Last updated: 2026-06-08 12:00 UTC</em> &nbsp;·&nbsp;
Counterfactual conditions use the CMIP6 multi-model mean warming delta subtracted from ERA5
(pseudo-global-warming approach).
</p>
