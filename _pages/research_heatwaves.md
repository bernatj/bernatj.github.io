---
layout: page
permalink: /research/heatwaves/
title: Heatwaves
nav: false
---

Heatwaves are prolonged periods of unusually high temperatures and are among the deadliest weather extremes, with impacts ranging from excess mortality to wildfires, crop losses and strain on energy and water systems. They are typically driven by persistent high-pressure systems — atmospheric blocks and amplified subtropical ridges — that bring subsidence, clear skies and warm-air advection, and their intensity is often amplified by land–atmosphere feedbacks such as dry soils. Anthropogenic warming has made heatwaves more frequent and intense, and understanding their dynamics, predictability and attribution is key to anticipating their impacts.

In [Jiménez-Esteve et al. (2025)](https://doi.org/10.1029/2025EF006453) we show how AI-based weather prediction models can accelerate the climate-change attribution of heatwaves, running forecasts under factual (present-day) and counterfactual (pre-industrial) conditions to quantify the human influence on individual events as they unfold.

---

### Pacific Northwest Heatwave — June 2021

In late June 2021 an extraordinary heatwave struck the Pacific Northwest of the United States and western Canada, shattering temperature records by wide margins — 49.6 °C in Lytton (British Columbia), a Canadian national record, and 46.7 °C in Portland (Oregon) — and was linked to hundreds of heat-related deaths. The event was produced by an exceptionally strong, quasi-stationary ridge (an "omega block") over the region, with the jet stream deflected far to the north.

The animation shows the evolution of the event in the ERA5 reanalysis from 24 June to 3 July 2021: 500 hPa geopotential height contours (588 dam in bold), 850 hPa temperature (shaded above 16 °C, 26 °C contour in red) and the 300 hPa jet stream (shaded above 30 m/s, with wind arrows and the 40 m/s isotach in blue). The panel below tracks the 850 hPa temperature averaged over the blue box (45–55°N, 125–115°W; 24 h running mean), which climbs to close to 30 °C at the end of June before the ridge breaks down in early July.

{% include video.liquid path="assets/video/heatwave_pnw2021_era5_z500_t850_jet300_24jun_to_03jul.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false loop=false %}

Running FourCastNet-v2, Pangu-Weather and NeuralGCM from factual and counterfactual (pre-industrial) initial conditions gives the anthropogenic climate change (ACC) signal of the event:

{% include figure.liquid path="assets/img/heatwave_pnw2021_acc_signal_t850_ai_models.png" class="img-fluid rounded z-depth-1" zoomable=true caption="Climate change signal in 850 hPa temperature (factual minus counterfactual forecasts) for the 2021 Pacific Northwest heatwave in three AI weather models, averaged over forecasts with lead times of 1–5 days valid during the peak of the event (28–30 June 2021). Blue box: heatwave region; green contours: mean 500 hPa geopotential height of the factual forecasts; hatching: signal not statistically significant (p &gt; 0.05). Adapted from Jiménez-Esteve et al. (2025), Fig. 2." %}

---

### Iberian Heatwave — August 2018

In early August 2018 the Iberian Peninsula experienced one of its most intense heatwaves on record, with maximum temperatures above 45 °C in parts of Portugal and southwestern Spain. The event was driven by the advection of very hot air from North Africa under a persistent subtropical ridge over the Iberian Peninsula.

The animation shows the evolution of the event in ERA5 from 30 July to 8 August 2018, with the same fields as above. The panel below tracks the 850 hPa temperature averaged over the blue box (36–43°N, 9°W–3°E; 24 h running mean), with the heatwave period (1–7 August) shaded.

{% include video.liquid path="assets/video/heatwave_iberia2018_era5_z500_t850_jet300_30jul_to_08aug.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false loop=false %}

The same attribution experiment for the Iberian heatwave:

{% include figure.liquid path="assets/img/heatwave_iberia2018_acc_signal_t850_ai_models.png" class="img-fluid rounded z-depth-1" zoomable=true caption="Climate change signal in 850 hPa temperature (factual minus counterfactual forecasts) for the 2018 Iberian heatwave in three AI weather models, averaged over forecasts with lead times of 1–5 days valid during the peak of the event (1–6 August 2018). Blue box: heatwave region; green contours: mean 500 hPa geopotential height of the factual forecasts; hatching: signal not statistically significant (p &gt; 0.05). Adapted from Jiménez-Esteve et al. (2025), Fig. 2." %}
