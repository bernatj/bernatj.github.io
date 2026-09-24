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
.fc-btn[disabled]   { opacity:.4; cursor:not-allowed; }
.fc-var-btn   { padding:7px 18px; border:none; border-radius:6px; cursor:pointer; font-size:14px; background:#e9ecef; color:#444; transition:.15s; }
.fc-var-btn.active  { background:#0f9d58; color:#fff; font-weight:600; }
.fc-var-btn[disabled] { opacity:.4; cursor:not-allowed; }
.fc-row       { display:flex; flex-wrap:wrap; gap:10px; margin:14px 0; align-items:center; }
.fc-row > .fc-label { font-size:13px; font-weight:600; color:#555; min-width:64px; }
.forecast-img { max-width:100%; border-radius:6px; box-shadow:0 2px 8px rgba(0,0,0,.12); display:block; cursor:zoom-in; }
.fc-pair      { display:flex; gap:14px; flex-wrap:wrap; align-items:flex-start; margin:8px 0 12px; }
.fc-pair > div { flex:1; min-width:280px; }

/* Time slider */
.fc-slider-box { margin:6px 0 28px; padding:12px 16px 8px; border-radius:8px; background:#f4f6f8; }
.fc-slider-top { display:flex; flex-wrap:wrap; gap:10px; align-items:center; margin-bottom:6px; }
.fc-step-btn  { width:34px; height:30px; border:none; border-radius:5px; cursor:pointer; font-size:14px; background:#dfe3e7; color:#333; }
.fc-step-btn:hover { background:#cfd5db; }
#fc-date-label { font-size:14px; font-weight:600; color:#333; }
#fc-init-label { font-size:12px; color:#777; }
#fc-slider    { width:100%; accent-color:#0f9d58; cursor:pointer; margin:4px 0 0; }
#fc-ticks     { position:relative; height:26px; font-size:11px; color:#777; margin:0 8px; }
#fc-ticks span { position:absolute; transform:translateX(-50%); white-space:nowrap; text-align:center; line-height:1.15; }

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
<div class="fc-row">
  <span class="fc-label">Model:</span>
  <button id="btn-pangu" class="fc-btn active" onclick="selectModel('pangu')">Pangu-Weather</button>
  <button id="btn-fcnv2" class="fc-btn"        onclick="selectModel('fcnv2')">FourCastNet v2</button>
  <button id="btn-multi" class="fc-btn"        onclick="selectModel('multi')">Multi-model mean</button>
</div>

<!-- Variable selector -->
<div class="fc-row">
  <span class="fc-label">Variable:</span>
  <button id="var-t2m"  class="fc-var-btn active" onclick="selectVar('t2m')">T2m</button>
  <button id="var-t850" class="fc-var-btn"        onclick="selectVar('t850')">T850</button>
  <button id="var-q850" class="fc-var-btn"        onclick="selectVar('q850')" title="Specific humidity at 850 hPa. FourCastNet v2 saves relative humidity natively; its Q850 is derived from RH and temperature.">Q850</button>
  <button id="var-rh850" class="fc-var-btn"       onclick="selectVar('rh850')" title="Relative humidity at 850 hPa. Pangu-Weather saves specific humidity natively; its RH850 is derived from Q and temperature.">RH850</button>
  <button id="var-z500" class="fc-var-btn"        onclick="selectVar('z500')">Z500</button>
  <button id="var-msl"  class="fc-var-btn"        onclick="selectVar('msl')">MSLP</button>
</div>
<p style="font-size:12.5px;color:#888;margin:2px 0 0;">
  Q850/RH850, native vs derived: FourCastNet v2's counterfactual perturbs relative humidity
  directly (smooth, like temperature), so its <strong>Q850 is derived</strong> and inherits
  fine-scale structure from the local temperature field. Pangu-Weather's counterfactual perturbs
  specific humidity directly, so its <strong>RH850 is derived</strong> the same way. That
  fine-scale structure is real physics (relative humidity depends exponentially on local
  temperature &mdash; the Clausius&ndash;Clapeyron relation), not noise, but the model's own
  native variable is the cleaner climatological signal to trust.
</p>

<!-- Region selector -->
<div class="fc-row">
  <span class="fc-label">Region:</span>
  <button id="region-global" class="fc-btn active" onclick="selectRegion('global')">Global</button>
  <button id="region-europe" class="fc-btn"        onclick="selectRegion('europe')">Europe</button>
</div>

<!-- View selector -->
<div class="fc-row">
  <span class="fc-label">View:</span>
  <button id="view-acc_signal" class="fc-btn active" onclick="selectView('acc_signal')">Attribution Signal</button>
  <button id="view-init_delta" class="fc-btn"        onclick="selectView('init_delta')" title="The Factual − PGW perturbation applied to the initial condition">Initial-Condition Perturbation</button>
</div>

<!-- Counterfactual selector -->
<div class="fc-row">
  <span class="fc-label">Counterfactual:</span>
  <span style="font-size:12px;color:#888;margin-right:2px;">Present Day (PD) &minus; Pre-Industrial (PI):</span>
  <button id="cf-default" class="fc-btn active" onclick="selectCF('default')" title="PD (1980-2014) minus PI (1850-1900), CMIP6 10-model mean: 0.86 K global mean">PD 1980&ndash;2014 (+0.9&nbsp;K)</button>
  <button id="cf-ssp585-2010-2040" class="fc-btn" onclick="selectCF('ssp585-2010-2040')" title="PD (2010-2040, SSP5-8.5) minus PI (1850-1900), CMIP6 30-model mean: 1.53 K global mean — a larger, more recent warming signal than the default">PD 2010&ndash;2040, SSP5-8.5 (+1.5&nbsp;K)</button>
</div>
<p style="font-size:12.5px;color:#888;margin:2px 0 0;">
  Both counterfactuals are defined the same way &mdash; a CMIP6 multi-model-mean warming delta,
  <strong>Present Day minus Pre-Industrial (1850&ndash;1900)</strong>, subtracted from ERA5 to build the
  pseudo-global-warming initial condition. They differ only in which period stands in for "Present Day"
  and which CMIP6 models feed the ensemble mean &mdash; see the table below.
</p>

<h3 id="fc-title" style="margin-top:14px;">2 m Temperature &mdash; Attribution Signal</h3>
<div class="fc-pair">
  <div>
    <img id="fc-img" class="forecast-img" src="" alt="ACC signal" onclick="zoomImg(this)">
  </div>
</div>

<!-- Time slider -->
<div class="fc-slider-box">
  <div class="fc-slider-top">
    <button class="fc-step-btn" onclick="stepDate(-1)" title="Previous (left arrow)">&#9664;</button>
    <button class="fc-step-btn" id="fc-play" style="width:64px;" onclick="togglePlay()" title="Play / pause">Play</button>
    <button class="fc-step-btn" onclick="stepDate(1)" title="Next (right arrow)">&#9654;</button>
    <span id="fc-date-label"></span>
    <span id="fc-init-label"></span>
  </div>
  <input type="range" id="fc-slider" min="0" max="0" step="1" value="0" aria-label="Forecast verification date">
  <div id="fc-ticks"></div>
</div>

<script>
// DATES_START (rewritten daily by update_website.py; oldest first, keys are verification times YYYYMMDDHH)
var fcDates = ['2026091318', '2026091400', '2026091406', '2026091412', '2026091418', '2026091500', '2026091506', '2026091512', '2026091518', '2026091600', '2026091606', '2026091612', '2026091618', '2026091700', '2026091706', '2026091712', '2026091718', '2026091800', '2026091806', '2026091812'];
// DATES_END

var currentModel  = 'pangu';
var currentVar    = 't2m';
var currentRegion = 'global';
var currentView   = 'acc_signal';
var currentCF     = 'default';
var currentIdx    = fcDates.length - 1;
var playTimer     = null;

var VAR_TITLES = {
  t2m:   '2 m Temperature',
  t850:  '850 hPa Temperature',
  q850:  '850 hPa Specific Humidity',
  rh850: '850 hPa Relative Humidity',
  z500:  '500 hPa Geopotential Height',
  msl:   'Mean Sea Level Pressure'
};
var VIEW_TITLES = {
  acc_signal: 'Attribution Signal',
  init_delta: 'Initial-Condition Perturbation'
};
var CF_TITLES = {
  'default':           'PD 1980&ndash;2014 &minus; PI, +0.9 K global mean (default)',
  'ssp585-2010-2040':  'PD 2010&ndash;2040 (SSP5-8.5) &minus; PI, +1.5 K global mean'
};

function fmt(key) {
  return key.slice(0,4) + '-' + key.slice(4,6) + '-' + key.slice(6,8) + ' ' + key.slice(8,10) + ' UTC';
}
function initOf(key) {
  var d = new Date(Date.UTC(+key.slice(0,4), +key.slice(4,6)-1, +key.slice(6,8), +key.slice(8,10)) - 48*3600*1000);
  var p = function(n) { return (n < 10 ? '0' : '') + n; };
  return d.getUTCFullYear() + '-' + p(d.getUTCMonth()+1) + '-' + p(d.getUTCDate()) + ' ' + p(d.getUTCHours()) + 'Z';
}
var IMAGES_BASE = 'https://bernatj.github.io/ai-attribution-forecast-images';
function imgSrc(model, v, view, kind, cf, key) {
  // Both views shown on this page (acc_signal, init_delta) depend on the counterfactual, so a
  // non-default choice inserts a tag before the date, matching update_website.py's copy_alt_images().
  var cfTag = cf === 'default' ? '' : ('_' + cf);
  return IMAGES_BASE + '/archive/' + key + '/' + model + '_' + v + '_' + view + kind + cfTag + '_' + key + '.png';
}
function regionKind(r) { return r === 'europe' ? '_europe' : ''; }

function zoomImg(img) {
  document.getElementById('fc-lightbox-img').src = img.src;
  document.getElementById('fc-lightbox').style.display = 'block';
}

function updateImages() {
  var key = fcDates[currentIdx];
  document.getElementById('fc-img').src = imgSrc(currentModel, currentVar, currentView, regionKind(currentRegion), currentCF, key);
  document.getElementById('fc-title').innerHTML = VAR_TITLES[currentVar] + ' &mdash; ' + VIEW_TITLES[currentView] +
    ' <small style="font-size:14px;color:#888;">(' + CF_TITLES[currentCF] + ')</small>';
  var star = currentIdx === fcDates.length-1 ? '  ★ latest' : '';
  if (currentView === 'init_delta') {
    document.getElementById('fc-date-label').textContent = 'Init ' + initOf(key) + star;
    document.getElementById('fc-init-label').textContent = 'perturbation applied at lead 0 h (Factual − PGW)';
  } else {
    document.getElementById('fc-date-label').textContent = 'Valid ' + fmt(key) + star;
    document.getElementById('fc-init-label').textContent = 'main init ' + initOf(key) + ' (lead 48 h)';
  }
  document.getElementById('fc-slider').value = currentIdx;
}

// Preload every date for the current model/variable/view/region so scrubbing is instant.
function preloadAll() {
  var kind = regionKind(currentRegion);
  fcDates.forEach(function(k) {
    (new Image()).src = imgSrc(currentModel, currentVar, currentView, kind, currentCF, k);
  });
}

function selectModel(m) {
  currentModel = m;
  document.querySelectorAll('.fc-btn[id^="btn-"]').forEach(function(b) { b.classList.toggle('active', b.id === 'btn-' + m); });
  updateImages(); preloadAll();
}

function selectVar(v) {
  currentVar = v;
  document.querySelectorAll('.fc-var-btn').forEach(function(b) { b.classList.toggle('active', b.id === 'var-' + v); });
  updateImages(); preloadAll();
}

function selectRegion(r) {
  currentRegion = r;
  document.querySelectorAll('.fc-btn[id^="region-"]').forEach(function(b) { b.classList.toggle('active', b.id === 'region-' + r); });
  updateImages(); preloadAll();
}

function selectView(v) {
  currentView = v;
  document.querySelectorAll('.fc-btn[id^="view-"]').forEach(function(b) { b.classList.toggle('active', b.id === 'view-' + v); });
  updateImages(); preloadAll();
}

function selectCF(cf) {
  currentCF = cf;
  document.querySelectorAll('.fc-btn[id^="cf-"]').forEach(function(b) { b.classList.toggle('active', b.id === 'cf-' + cf); });
  updateImages(); preloadAll();
}

function setIdx(i) {
  currentIdx = Math.max(0, Math.min(fcDates.length - 1, i));
  updateImages();
}
function stepDate(d) { setIdx(currentIdx + d); }

function togglePlay() {
  var btn = document.getElementById('fc-play');
  if (playTimer) { clearInterval(playTimer); playTimer = null; btn.textContent = 'Play'; return; }
  btn.textContent = 'Pause';
  if (currentIdx >= fcDates.length - 1) setIdx(0);
  playTimer = setInterval(function() {
    if (currentIdx >= fcDates.length - 1) { togglePlay(); return; }
    stepDate(1);
  }, 700);
}

function buildTicks() {
  var box = document.getElementById('fc-ticks');
  box.innerHTML = '';
  var n = fcDates.length;
  var mo = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  fcDates.forEach(function(k, i) {
    if (k.slice(8,10) !== '00' && i !== 0 && i !== n-1) return;      // label each day at 00 UTC, plus both ends
    var lbl = (+k.slice(6,8)) + ' ' + mo[+k.slice(4,6)-1] + (k.slice(8,10) !== '00' ? ' ' + k.slice(8,10) + 'Z' : '');
    var s = document.createElement('span');
    s.style.left = (n > 1 ? 100 * i / (n-1) : 0) + '%';
    s.textContent = lbl;
    box.appendChild(s);
  });
}

document.getElementById('fc-slider').max = fcDates.length - 1;
document.getElementById('fc-slider').addEventListener('input', function() { setIdx(+this.value); });
document.addEventListener('keydown', function(e) {
  if (e.target && (e.target.tagName === 'INPUT' && e.target.type !== 'range')) return;
  if (e.key === 'ArrowLeft')  { stepDate(-1); e.preventDefault(); }
  if (e.key === 'ArrowRight') { stepDate(1);  e.preventDefault(); }
});
buildTicks();
updateImages();
preloadAll();
</script>

---

<p class="text-muted small mt-4">
<em>Last updated: 2026-09-16 12:00 UTC</em> &nbsp;&middot;&nbsp;
Counterfactual conditions subtract a CMIP6 multi-model-mean warming delta from ERA5
(pseudo-global-warming approach). Both counterfactuals below are defined the same way &mdash;
<strong>Present Day (PD) minus Pre-Industrial (PI, 1850&ndash;1900)</strong> &mdash; and differ only in
which period defines "Present Day" and which CMIP6 models go into the ensemble mean.
</p>

<table style="width:100%; max-width:900px; border-collapse:collapse; font-size:13px; margin:8px 0 20px;">
  <thead>
    <tr style="border-bottom:2px solid #ccc; text-align:left;">
      <th style="padding:6px 10px 6px 0;">Counterfactual</th>
      <th style="padding:6px 10px;">Definition</th>
      <th style="padding:6px 10px;">Global mean</th>
      <th style="padding:6px 0;">CMIP6 models</th>
    </tr>
  </thead>
  <tbody>
    <tr style="border-bottom:1px solid #e5e5e5; vertical-align:top;">
      <td style="padding:8px 10px 8px 0;"><strong>Default</strong></td>
      <td style="padding:8px 10px;">PD (1980&ndash;2014) &minus; PI (1850&ndash;1900)</td>
      <td style="padding:8px 10px;">+0.86&nbsp;K</td>
      <td style="padding:8px 0;">
        <details>
          <summary style="cursor:pointer;color:#555;">10 models</summary>
          <span style="color:#666;">AWI-CM-1-1-MR, BCC-CSM2-MR, CAMS-CSM1-0, CanESM5-1, CMCC-CM2-HR4,
          CMCC-CM2-SR5, CMCC-ESM2, EC-Earth3-CC, EC-Earth3-Veg, EC-Earth3-Veg-LR</span>
        </details>
      </td>
    </tr>
    <tr style="vertical-align:top;">
      <td style="padding:8px 10px 8px 0;"><strong>SSP5-8.5, 2010&ndash;2040</strong></td>
      <td style="padding:8px 10px;">PD (2010&ndash;2040, SSP5-8.5) &minus; PI (1850&ndash;1900)</td>
      <td style="padding:8px 10px;">+1.53&nbsp;K</td>
      <td style="padding:8px 0;">
        <details>
          <summary style="cursor:pointer;color:#555;">30 models</summary>
          <span style="color:#666;">AWI-CM-1-1-MR, BCC-CSM2-MR, CAMS-CSM1-0, CIESM, CMCC-CM2-SR5, CMCC-ESM2,
          CNRM-CM6-1-HR, CNRM-ESM2-1, CanESM5, CanESM5-CanOE, E3SM-1-1, EC-Earth3, EC-Earth3-Veg,
          EC-Earth3-Veg-LR, FGOALS-g3, GISS-E2-1-G, HadGEM3-GC31-LL, HadGEM3-GC31-MM, INM-CM4-8, INM-CM5-0,
          IPSL-CM6A-LR, KACE-1-0-G, MIROC6, MPI-ESM1-2-HR, MPI-ESM1-2-LR, NESM3, NorESM2-LM, NorESM2-MM,
          TaiESM1, UKESM1-0-LL</span>
        </details>
      </td>
    </tr>
  </tbody>
</table>
