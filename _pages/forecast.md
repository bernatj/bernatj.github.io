---
layout: page
permalink: /forecast/
title: AI-forecast-based Attribution
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
/* Widen content for this page */
.post-content, .page-content { max-width: 1400px !important; }

.fc-btn       { padding:8px 22px; border:none; border-radius:6px; cursor:pointer; font-size:14px; background:#e9ecef; color:#444; transition:.15s; }
.fc-btn.active      { background:#1a73e8; color:#fff; font-weight:600; }
.fc-date-btn  { padding:5px 14px; border:none; border-radius:5px; cursor:pointer; font-size:12px; background:#e9ecef; color:#444; transition:.15s; }
.fc-date-btn.active { background:#0f9d58; color:#fff; font-weight:600; }
.forecast-img { max-width:100%; border-radius:6px; box-shadow:0 2px 8px rgba(0,0,0,.12); display:block; cursor:zoom-in; }
.fc-pair      { display:flex; gap:14px; flex-wrap:wrap; align-items:flex-start; margin:8px 0 24px; }
.fc-pair > div { flex:1; min-width:280px; }

/* Lightbox */
#fc-lightbox {
  display:none; position:fixed; top:0; left:0; width:100%; height:100%;
  background:rgba(0,0,0,.88); z-index:9999; cursor:zoom-out;
}
#fc-lightbox img {
  max-width:95%; max-height:95%; position:absolute;
  top:50%; left:50%; transform:translate(-50%,-50%);
  border-radius:6px; box-shadow:0 4px 30px rgba(0,0,0,.5);
}
</style>

<!-- Lightbox overlay -->
<div id="fc-lightbox" onclick="this.style.display='none'">
  <img id="fc-lightbox-img" src="" alt="">
</div>

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
  <!-- LATEST_INIT:2026061700 -->
  <button class="fc-date-btn active" onclick="selectDate('2026061900')">2026-06-19 00Z &#9733;</button>
  <button class="fc-date-btn" onclick="selectDate('2026061818')">2026-06-18 18Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061812')">2026-06-18 12Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061806')">2026-06-18 06Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061800')">2026-06-18 00Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061718')">2026-06-17 18Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061712')">2026-06-17 12Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061706')">2026-06-17 06Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061700')">2026-06-17 00Z</button>
  <button class="fc-date-btn" onclick="selectDate('2026061618')">2026-06-16 18Z</button>
  <!-- DATE_BUTTONS_END -->
</div>

<h3 style="margin-top:4px;">2 m Temperature &mdash; Attribution Signal</h3>
<div class="fc-pair">
  <div class="forecast-fig" data-key="t2m_acc_signal">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Global</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_t2m_acc_signal.png" alt="T2m ACC signal global" onclick="zoomImg(this)">
  </div>
  <div class="forecast-fig" data-key="t2m_acc_signal_europe">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Europe</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_t2m_acc_signal_europe.png" alt="T2m ACC signal Europe" onclick="zoomImg(this)">
  </div>
</div>

<hr>

<h3>850 hPa Specific Humidity &mdash; Attribution Signal <small style="font-size:13px;color:#888;">(Pangu only)</small></h3>
<div id="q850-section" class="fc-pair">
  <div class="forecast-fig" data-key="q850_acc_signal">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Global</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_q850_acc_signal.png" alt="Q850 ACC signal global" onclick="zoomImg(this)">
  </div>
  <div class="forecast-fig" data-key="q850_acc_signal_europe">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Europe</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_q850_acc_signal_europe.png" alt="Q850 ACC signal Europe" onclick="zoomImg(this)">
  </div>
</div>
<div id="q850-unavail" style="display:none;color:#888;font-style:italic;margin-bottom:24px;">
  Q850 not available for this model.
</div>

<hr>

<h3>500 hPa Geopotential Height &mdash; Attribution Signal</h3>
<div class="fc-pair">
  <div class="forecast-fig" data-key="z500_acc_signal">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Global</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_z500_acc_signal.png" alt="Z500 ACC signal global" onclick="zoomImg(this)">
  </div>
  <div class="forecast-fig" data-key="z500_acc_signal_europe">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Europe</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_z500_acc_signal_europe.png" alt="Z500 ACC signal Europe" onclick="zoomImg(this)">
  </div>
</div>

<hr>

<h3>Mean Sea Level Pressure &mdash; Attribution Signal</h3>
<div class="fc-pair">
  <div class="forecast-fig" data-key="msl_acc_signal">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Global</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_msl_acc_signal.png" alt="MSL ACC signal global" onclick="zoomImg(this)">
  </div>
  <div class="forecast-fig" data-key="msl_acc_signal_europe">
    <p style="margin:0 0 4px;font-size:12px;color:#666;">Europe</p>
    <img class="forecast-img" src="/assets/img/forecast/latest_pangu_msl_acc_signal_europe.png" alt="MSL ACC signal Europe" onclick="zoomImg(this)">
  </div>
</div>

<script>
var latestInit   = '2026061900';
var currentModel = 'pangu';
var currentDate  = '2026061900';
var Q850_MODELS  = ['pangu'];

function zoomImg(img) {
  document.getElementById('fc-lightbox-img').src = img.src;
  document.getElementById('fc-lightbox').style.display = 'block';
}

function selectModel(m) {
  currentModel = m;
  document.querySelectorAll('.fc-btn').forEach(function(b) {
    b.classList.toggle('active', b.id === 'btn-' + m);
  });
  var hasQ850 = Q850_MODELS.indexOf(m) !== -1;
  document.getElementById('q850-section').style.display  = hasQ850 ? '' : 'none';
  document.getElementById('q850-unavail').style.display  = hasQ850 ? 'none' : '';
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
<em>Last updated: 2026-06-17 00:00 UTC</em> &nbsp;&middot;&nbsp;
Counterfactual conditions use the CMIP6 multi-model mean warming delta subtracted from ERA5
(pseudo-global-warming approach).
</p>
