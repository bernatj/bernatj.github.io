---
layout: page
permalink: /forecast/
title: Live Forecast
nav: true
nav_order: 7
---

Daily **6-day AI weather forecasts** initialised from ERA5 reanalysis, run under both
**factual** (current climate) and **counterfactual** (pre-industrial, PGW) conditions.
The **ACC signal** = Factual &minus; PGW, averaged over 13 initializations all verifying at the
same target date (lead times 2&ndash;5 days). Stippled dots mark grid points **not significant**
at p &lt; 0.05 (paired t-test across initializations). Z500 factual contours are overlaid.

See <a href="https://doi.org/10.1029/2025EF006453" target="_blank">Jiménez-Esteve et al. (2025)</a> for methodology.

---

<style>
.fc-btn       { padding:8px 22px; border:none; border-radius:6px; cursor:pointer; font-size:14px; background:#e9ecef; color:#444; transition:.15s; }
.fc-btn.active      { background:#1a73e8; color:#fff; font-weight:600; }
.fc-date-btn  { padding:5px 14px; border:none; border-radius:5px; cursor:pointer; font-size:12px; background:#e9ecef; color:#444; transition:.15s; }
.fc-date-btn.active { background:#0f9d58; color:#fff; font-weight:600; }
.forecast-img { max-width:100%; border-radius:6px; box-shadow:0 2px 8px rgba(0,0,0,.12); display:block; }
.fc-pair      { display:flex; gap:14px; flex-wrap:wrap; align-items:flex-start; margin:8px 0 24px; }
.fc-pair > div { flex:1; min-width:280px; }
</style>

<!-- Model selector -->
<div style="display:flex;flex-wrap:wrap;gap:10px;margin:20px 0 10px;align-items:center;">
  <span style="font-size:13px;font-weight:600;color:#555;min-width:52px;">Model:</span>
  <button id="btn-pangu" class="fc-btn active" onclick="selectModel('pangu')">Pangu-Weather</button>
  <button id="btn-fcnv2" class="fc-btn"        onclick="selectModel('fcnv2')">FourCastNet v2</button>
  <button id="btn-multi" class="fc-btn"        onclick="selectModel('multi')">Multi-model mean</button>
</div>

<!-- Date selector -->
<div style="display:flex;flex-wrap:wrap;gap:8px;margin:0 0 28px;align-items:center;">
  <span style="font-size:13px;font-weight:600;color:#555;min-width:52px;">Date:</span>
  <!-- DATE_BUTTONS_START -->
  <!-- LATEST_INIT:2025111518 -->
  <button class="fc-date-btn active" onclick="selectDate('2025111518')">2025-11-15 18Z &#9733;</button>
  <!-- DATE_BUTTONS_END -->
</div>

<h3 style="margin-top:4px;">850 hPa Temperature &mdash; Attribution Signal</h3>
<div class="fc-pair">
  <div class="forecast-fig" data-key="t850_acc_signal">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Global</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_t850_acc_signal.png" alt="T850 ACC signal global">
  </div>
  <div class="forecast-fig" data-key="t850_acc_signal_europe">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Europe</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_t850_acc_signal_europe.png" alt="T850 ACC signal Europe">
  </div>
</div>

<hr>

<h3>500 hPa Geopotential Height &mdash; Attribution Signal</h3>
<div class="fc-pair">
  <div class="forecast-fig" data-key="z500_acc_signal">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Global</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_z500_acc_signal.png" alt="Z500 ACC signal global">
  </div>
  <div class="forecast-fig" data-key="z500_acc_signal_europe">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Europe</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_z500_acc_signal_europe.png" alt="Z500 ACC signal Europe">
  </div>
</div>

<script>
var latestInit   = '2025111518';
var currentModel = 'pangu';
var currentDate  = '2025111518';

function selectModel(m) {
  currentModel = m;
  document.querySelectorAll('.fc-btn').forEach(function(b) {
    b.classList.toggle('active', b.id === 'btn-' + m);
  });
  updateImages();
}

function selectDate(dateKey) {
  currentDate = dateKey;
  document.querySelectorAll('.fc-date-btn').forEach(function(b) {
    var onclick = b.getAttribute('onclick') || '';
    b.classList.toggle('active', onclick.indexOf("'" + dateKey + "'") !== -1);
  });
  updateImages();
}

function updateImages() {
  document.querySelectorAll('.forecast-fig').forEach(function(div) {
    var key = div.getAttribute('data-key');
    var img = div.querySelector('img');
    if (!img) return;
    var src;
    if (currentDate === latestInit) {
      src = '/assets/img/forecast/latest_' + currentModel + '_' + key + '.png';
    } else {
      src = '/assets/img/forecast/archive/' + currentDate + '/' +
            currentModel + '_' + key + '_' + currentDate + '.png';
    }
    img.setAttribute('src', src);
  });
}
</script>

---

<p class="text-muted small mt-4">
<em>Last updated: 2025-11-15 18:00 UTC</em> &nbsp;&middot;&nbsp;
Counterfactual conditions use the CMIP6 multi-model mean warming delta subtracted from ERA5
(pseudo-global-warming approach).
</p>
