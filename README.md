<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>XAUm Smart DCA Calculator — Matrixdock</title>
<link href="https://fonts.googleapis.com/css2?family=Tenor+Sans&family=DM+Mono:wght@300;400;500&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;1,9..144,300;1,9..144,400&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0A0800;
  --bg2: #0F0C00;
  --surface: #141000;
  --surface2: #1A1500;
  --surface3: #221C00;
  --gold: #C8973A;
  --gold2: #E8B84B;
  --gold3: #F5D06A;
  --gold-dim: #6B5120;
  --gold-glow: rgba(200,151,58,0.12);
  --text: #F2ECD8;
  --text2: #9A9078;
  --text3: #5A5238;
  --green: #5DBF8A;
  --green2: #3A9E6A;
  --red: #E05555;
  --border: rgba(200,151,58,0.15);
  --border2: rgba(200,151,58,0.08);
}

*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}

body {
background: var(–bg);
color: var(–text);
font-family: ‘DM Mono’, monospace;
font-size: 13px;
line-height: 1.6;
min-height: 100vh;
overflow-x: hidden;
}

/* GRAIN */
body::before {
content:’’;
position:fixed;
inset:0;
pointer-events:none;
z-index:999;
opacity:0.03;
background-image:url(“data:image/svg+xml,%3Csvg viewBox=‘0 0 512 512’ xmlns=‘http://www.w3.org/2000/svg’%3E%3Cfilter id=‘n’%3E%3CfeTurbulence type=‘fractalNoise’ baseFrequency=‘0.8’ numOctaves=‘4’ stitchTiles=‘stitch’/%3E%3C/filter%3E%3Crect width=‘100%25’ height=‘100%25’ filter=‘url(%23n)’/%3E%3C/svg%3E”);
}

/* BG GLOW */
body::after {
content:’’;
position:fixed;
top:-20%;left:30%;
width:60%;height:60%;
background:radial-gradient(ellipse, rgba(200,151,58,0.04) 0%, transparent 70%);
pointer-events:none;
z-index:0;
}

/* HEADER */
header {
padding: 48px 64px 0;
position: relative;
z-index: 1;
border-bottom: 1px solid var(–border);
padding-bottom: 40px;
display: flex;
justify-content: space-between;
align-items: flex-end;
}

.header-left {}

.brand {
display: flex;
align-items: center;
gap: 12px;
margin-bottom: 20px;
}

.brand-mark {
width: 32px; height: 32px;
background: linear-gradient(135deg, var(–gold-dim), var(–gold));
display: flex;
align-items: center;
justify-content: center;
font-size: 16px;
}

.brand-name {
font-family: ‘Tenor Sans’, sans-serif;
font-size: 13px;
letter-spacing: 4px;
text-transform: uppercase;
color: var(–gold);
}

h1 {
font-family: ‘Fraunces’, serif;
font-size: clamp(36px, 5vw, 64px);
font-weight: 300;
line-height: 1;
letter-spacing: -1px;
color: var(–text);
}

h1 em {
font-style: italic;
color: var(–gold2);
}

.header-sub {
font-size: 12px;
color: var(–text3);
margin-top: 12px;
max-width: 480px;
line-height: 1.8;
}

.header-right {
text-align: right;
}

.live-price {
background: var(–surface2);
border: 1px solid var(–border);
padding: 16px 24px;
margin-bottom: 0;
}

.live-label {
font-size: 9px;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–text3);
margin-bottom: 6px;
}

.live-value {
font-family: ‘Fraunces’, serif;
font-size: 32px;
font-weight: 300;
color: var(–gold2);
line-height: 1;
margin-bottom: 4px;
}

.live-change {
font-size: 11px;
color: var(–green);
}

/* MAIN LAYOUT */
.main {
position: relative;
z-index: 1;
padding: 48px 64px;
display: grid;
grid-template-columns: 420px 1fr;
gap: 32px;
align-items: start;
}

/* INPUT PANEL */
.input-panel {
position: sticky;
top: 32px;
}

.panel-title {
font-size: 9px;
letter-spacing: 4px;
text-transform: uppercase;
color: var(–gold-dim);
margin-bottom: 24px;
display: flex;
align-items: center;
gap: 10px;
}

.panel-title::after {
content:’’;
flex-grow:1;
height:1px;
background:var(–border);
}

/* INPUT GROUPS */
.input-group {
margin-bottom: 28px;
}

.input-label {
font-size: 9px;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–text3);
margin-bottom: 10px;
display: flex;
justify-content: space-between;
align-items: center;
}

.input-label span {
font-family: ‘Fraunces’, serif;
font-size: 18px;
font-style: italic;
color: var(–gold2);
letter-spacing: 0;
text-transform: none;
}

/* SLIDER */
.slider-wrap {
position: relative;
padding: 8px 0;
}

input[type=range] {
width: 100%;
height: 2px;
background: var(–surface3);
outline: none;
border: none;
-webkit-appearance: none;
cursor: pointer;
position: relative;
}

input[type=range]::-webkit-slider-thumb {
-webkit-appearance: none;
width: 18px; height: 18px;
border-radius: 50%;
background: var(–gold);
border: 2px solid var(–bg);
box-shadow: 0 0 12px rgba(200,151,58,0.5);
transition: transform 0.2s, box-shadow 0.2s;
}

input[type=range]::-webkit-slider-thumb:hover {
transform: scale(1.2);
box-shadow: 0 0 20px rgba(200,151,58,0.7);
}

.slider-track {
position: absolute;
left: 0; top: 50%;
transform: translateY(-50%);
height: 2px;
background: linear-gradient(90deg, var(–gold-dim), var(–gold));
pointer-events: none;
transition: width 0.1s;
}

.slider-marks {
display: flex;
justify-content: space-between;
margin-top: 8px;
}

.slider-mark {
font-size: 9px;
color: var(–text3);
letter-spacing: 1px;
}

/* NUMBER INPUT */
.number-input-wrap {
display: flex;
align-items: center;
background: var(–surface2);
border: 1px solid var(–border);
transition: border-color 0.2s;
}

.number-input-wrap:focus-within {
border-color: var(–gold);
}

.input-prefix {
padding: 12px 16px;
font-size: 13px;
color: var(–gold);
border-right: 1px solid var(–border);
background: var(–surface3);
font-family: ‘Fraunces’, serif;
font-style: italic;
}

input[type=number] {
flex-grow: 1;
background: transparent;
border: none;
outline: none;
color: var(–text);
font-family: ‘DM Mono’, monospace;
font-size: 14px;
padding: 12px 16px;
}

input[type=number]::-webkit-inner-spin-button,
input[type=number]::-webkit-outer-spin-button {
-webkit-appearance: none;
}

/* FREQUENCY TOGGLE */
.freq-toggle {
display: grid;
grid-template-columns: 1fr 1fr 1fr;
gap: 1px;
background: var(–border);
}

.freq-btn {
background: var(–surface2);
padding: 10px;
text-align: center;
font-size: 11px;
letter-spacing: 1px;
color: var(–text3);
cursor: pointer;
transition: all 0.2s;
text-transform: uppercase;
}

.freq-btn.active {
background: rgba(200,151,58,0.12);
color: var(–gold2);
}

.freq-btn:hover:not(.active) {
background: var(–surface3);
color: var(–text2);
}

/* SCENARIO TOGGLE */
.scenario-toggle {
display: grid;
grid-template-columns: 1fr 1fr 1fr;
gap: 1px;
background: var(–border);
margin-bottom: 28px;
}

.scenario-btn {
background: var(–surface2);
padding: 12px 8px;
text-align: center;
font-size: 10px;
letter-spacing: 1px;
color: var(–text3);
cursor: pointer;
transition: all 0.2s;
text-transform: uppercase;
line-height: 1.4;
}

.scenario-btn.active {
background: rgba(200,151,58,0.1);
color: var(–gold);
border-top: 2px solid var(–gold);
}

/* CALCULATE BTN */
.calc-btn {
width: 100%;
padding: 16px;
background: linear-gradient(135deg, var(–gold-dim), var(–gold));
color: var(–bg);
font-family: ‘Tenor Sans’, sans-serif;
font-size: 12px;
letter-spacing: 4px;
text-transform: uppercase;
border: none;
cursor: pointer;
transition: all 0.3s;
margin-top: 8px;
position: relative;
overflow: hidden;
}

.calc-btn::after {
content:’’;
position:absolute;
inset:0;
background:linear-gradient(135deg, transparent, rgba(255,255,255,0.1), transparent);
transform:translateX(-100%);
transition:transform 0.5s;
}

.calc-btn:hover {
background: linear-gradient(135deg, var(–gold), var(–gold3));
box-shadow: 0 0 30px rgba(200,151,58,0.3);
}

.calc-btn:hover::after {
transform: translateX(100%);
}

/* RESULTS PANEL */
.results-panel {}

/* MILESTONE CARDS */
.milestones {
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 12px;
margin-bottom: 28px;
}

.milestone {
background: var(–surface);
border: 1px solid var(–border);
padding: 20px;
position: relative;
overflow: hidden;
transition: all 0.3s;
}

.milestone:hover {
border-color: rgba(200,151,58,0.35);
transform: translateY(-2px);
}

.milestone::before {
content:’’;
position:absolute;
top:0;left:0;right:0;
height:2px;
background:linear-gradient(90deg, var(–gold-dim), var(–gold), transparent);
}

.milestone-oz {
font-family: ‘Fraunces’, serif;
font-size: 28px;
font-weight: 300;
color: var(–gold2);
line-height: 1;
margin-bottom: 4px;
}

.milestone-label {
font-size: 9px;
letter-spacing: 2px;
text-transform: uppercase;
color: var(–text3);
margin-bottom: 14px;
}

.milestone-months {
font-family: ‘Fraunces’, serif;
font-size: 22px;
color: var(–text);
margin-bottom: 2px;
}

.milestone-months-label {
font-size: 10px;
color: var(–text3);
margin-bottom: 12px;
}

.milestone-value {
font-family: ‘DM Mono’, monospace;
font-size: 12px;
color: var(–green);
}

/* SUMMARY BAR */
.summary-bar {
background: var(–surface2);
border: 1px solid var(–border);
padding: 20px 24px;
display: grid;
grid-template-columns: repeat(4, 1fr);
gap: 0;
margin-bottom: 28px;
}

.summary-item {
text-align: center;
padding: 0 16px;
border-right: 1px solid var(–border);
}

.summary-item:last-child { border-right: none; }

.summary-label {
font-size: 9px;
letter-spacing: 2px;
text-transform: uppercase;
color: var(–text3);
margin-bottom: 8px;
}

.summary-value {
font-family: ‘Fraunces’, serif;
font-size: 22px;
font-weight: 300;
color: var(–text);
line-height: 1;
}

.summary-value.gold { color: var(–gold2); }
.summary-value.green { color: var(–green); }
.summary-value.red { color: var(–red); }

/* CHART AREA */
.chart-card {
background: var(–surface);
border: 1px solid var(–border);
padding: 24px;
margin-bottom: 28px;
}

.chart-header {
display: flex;
justify-content: space-between;
align-items: flex-start;
margin-bottom: 24px;
}

.chart-title {
font-size: 9px;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–text3);
}

.chart-legend {
display: flex;
gap: 16px;
}

.legend-item {
display: flex;
align-items: center;
gap: 6px;
font-size: 10px;
color: var(–text3);
}

.legend-dot {
width: 8px; height: 2px;
border-radius: 1px;
}

.chart-wrap {
height: 240px;
position: relative;
}

canvas { width:100%!important; }

/* PROJECTION TABLE */
.proj-table-card {
background: var(–surface);
border: 1px solid var(–border);
padding: 24px;
margin-bottom: 28px;
}

.proj-table {
width: 100%;
border-collapse: collapse;
}

.proj-table th {
font-size: 9px;
letter-spacing: 2px;
text-transform: uppercase;
color: var(–text3);
text-align: left;
padding: 8px 12px;
border-bottom: 1px solid var(–border);
font-weight: 400;
}

.proj-table td {
padding: 11px 12px;
border-bottom: 1px solid var(–border2);
font-size: 12px;
color: var(–text2);
}

.proj-table tr:last-child td { border-bottom: none; }
.proj-table tr:hover td { background: var(–surface2); }

.proj-table td:first-child {
font-family: ‘Fraunces’, serif;
font-size: 15px;
color: var(–gold);
font-style: italic;
}

.proj-table .positive { color: var(–green); }
.proj-table .negative { color: var(–red); }

/* INSIGHT BOX */
.insight {
background: linear-gradient(135deg, rgba(200,151,58,0.06), rgba(200,151,58,0.02));
border: 1px solid rgba(200,151,58,0.2);
padding: 20px 24px;
display: flex;
gap: 16px;
align-items: flex-start;
margin-bottom: 12px;
}

.insight-icon { font-size: 20px; flex-shrink:0; margin-top:2px; }

.insight-text {
font-size: 12px;
color: var(–text2);
line-height: 1.8;
}

.insight-text strong { color: var(–gold2); }

/* FOOTER */
footer {
position: relative;
z-index: 1;
padding: 32px 64px;
border-top: 1px solid var(–border);
display: flex;
justify-content: space-between;
align-items: center;
font-size: 10px;
color: var(–text3);
}

.footer-disclaimer { max-width: 500px; line-height: 1.7; }

/* ANIMATIONS */
@keyframes countUp {
from { opacity: 0; transform: translateY(8px); }
to { opacity: 1; transform: translateY(0); }
}

.animate-in {
animation: countUp 0.4s ease forwards;
}

/* SCROLLBAR */
::-webkit-scrollbar { width: 3px; }
::-webkit-scrollbar-track { background: var(–bg); }
::-webkit-scrollbar-thumb { background: var(–gold-dim); }

/* RESPONSIVE */
@media(max-width:1100px) {
header { padding: 32px; flex-direction: column; align-items: flex-start; gap: 24px; }
.main { padding: 32px; grid-template-columns: 1fr; }
.input-panel { position: static; }
.milestones { grid-template-columns: 1fr 1fr; }
footer { padding: 24px 32px; flex-direction: column; gap: 12px; text-align: center; }
}

@media(max-width:600px) {
header { padding: 24px; }
.main { padding: 24px; }
.milestones { grid-template-columns: 1fr; }
.summary-bar { grid-template-columns: 1fr 1fr; }
.summary-item:nth-child(2) { border-right: none; }
.summary-item:nth-child(3) { border-top: 1px solid var(–border); }
h1 { font-size: 32px; }
.live-value { font-size: 24px; }
}
</style>

</head>
<body>

<!-- HEADER -->

<header>
  <div class="header-left">
    <div class="brand">
      <div class="brand-mark">⬡</div>
      <div class="brand-name">Matrixdock · XAUm</div>
    </div>
    <h1>Smart <em>DCA</em><br>Calculator</h1>
    <p class="header-sub">Plan your gold accumulation journey. See exactly when you'll reach your target — and what it'll be worth across multiple price scenarios.</p>
  </div>
  <div class="header-right">
    <div class="live-price">
      <div class="live-label">● Live Gold Price — XAU/USD</div>
      <div class="live-value" id="livePrice">$3,042.80</div>
      <div class="live-change" id="liveChange">▲ +0.84% today</div>
    </div>
  </div>
</header>

<!-- MAIN -->

<div class="main">

  <!-- INPUT PANEL -->

  <div class="input-panel">
    <div class="panel-title">Your DCA Settings</div>

```
<!-- Investment Amount -->
<div class="input-group">
  <div class="input-label">
    Investment per period
    <span id="investDisplay">$200</span>
  </div>
  <div class="slider-wrap">
    <div class="slider-track" id="investTrack"></div>
    <input type="range" id="investSlider" min="50" max="5000" step="50" value="200" oninput="updateInvest(this.value)">
  </div>
  <div class="slider-marks">
    <span class="slider-mark">$50</span>
    <span class="slider-mark">$1,000</span>
    <span class="slider-mark">$2,500</span>
    <span class="slider-mark">$5,000</span>
  </div>
</div>

<!-- Frequency -->
<div class="input-group">
  <div class="input-label">Purchase Frequency</div>
  <div class="freq-toggle">
    <div class="freq-btn" onclick="setFreq('weekly',this)">Weekly</div>
    <div class="freq-btn active" onclick="setFreq('monthly',this)">Monthly</div>
    <div class="freq-btn" onclick="setFreq('quarterly',this)">Quarterly</div>
  </div>
</div>

<!-- Target -->
<div class="input-group">
  <div class="input-label">
    Target Holdings
    <span id="targetDisplay">5 oz</span>
  </div>
  <div class="slider-wrap">
    <div class="slider-track" id="targetTrack"></div>
    <input type="range" id="targetSlider" min="1" max="100" step="1" value="5" oninput="updateTarget(this.value)">
  </div>
  <div class="slider-marks">
    <span class="slider-mark">1 oz</span>
    <span class="slider-mark">25 oz</span>
    <span class="slider-mark">50 oz</span>
    <span class="slider-mark">100 oz</span>
  </div>
</div>

<!-- Starting Holdings -->
<div class="input-group">
  <div class="input-label">Current XAUm Holdings (oz)</div>
  <div class="number-input-wrap">
    <div class="input-prefix">oz</div>
    <input type="number" id="currentHoldings" min="0" max="1000" step="0.01" value="0" placeholder="0.00" oninput="calculate()">
  </div>
</div>

<!-- Price Scenario -->
<div class="input-group">
  <div class="input-label">Gold Price Scenario</div>
  <div class="scenario-toggle">
    <div class="scenario-btn" onclick="setScenario('bear',this)">Bear<br><span style="color:var(--red);font-size:9px;">−10% / yr</span></div>
    <div class="scenario-btn active" onclick="setScenario('base',this)">Base<br><span style="color:var(--gold);font-size:9px;">+8% / yr</span></div>
    <div class="scenario-btn" onclick="setScenario('bull',this)">Bull<br><span style="color:var(--green);font-size:9px;">+20% / yr</span></div>
  </div>
</div>

<button class="calc-btn" onclick="calculate()">Calculate My Gold Journey</button>
```

  </div>

  <!-- RESULTS PANEL -->

  <div class="results-panel" id="results">

```
<!-- MILESTONES -->
<div class="panel-title">Milestone Targets</div>
<div class="milestones" id="milestones">
  <!-- filled by JS -->
</div>

<!-- SUMMARY BAR -->
<div class="summary-bar">
  <div class="summary-item">
    <div class="summary-label">Total Invested</div>
    <div class="summary-value gold" id="totalInvested">—</div>
  </div>
  <div class="summary-item">
    <div class="summary-label">Gold Accumulated</div>
    <div class="summary-value" id="totalOz">—</div>
  </div>
  <div class="summary-item">
    <div class="summary-label">Portfolio Value</div>
    <div class="summary-value green" id="finalValue">—</div>
  </div>
  <div class="summary-item">
    <div class="summary-label">Total Return</div>
    <div class="summary-value green" id="totalReturn">—</div>
  </div>
</div>

<!-- CHART -->
<div class="chart-card">
  <div class="chart-header">
    <div class="chart-title">Accumulation Projection</div>
    <div class="chart-legend">
      <div class="legend-item">
        <div class="legend-dot" style="background:var(--gold);"></div>
        Portfolio Value
      </div>
      <div class="legend-item">
        <div class="legend-dot" style="background:var(--text3);"></div>
        Amount Invested
      </div>
    </div>
  </div>
  <div class="chart-wrap">
    <canvas id="projChart"></canvas>
  </div>
</div>

<!-- PROJECTION TABLE -->
<div class="proj-table-card">
  <div style="font-size:9px;letter-spacing:3px;text-transform:uppercase;color:var(--text3);margin-bottom:20px;">Year-by-Year Projection</div>
  <table class="proj-table">
    <thead>
      <tr>
        <th>Period</th>
        <th>oz Accumulated</th>
        <th>Total Invested</th>
        <th>Portfolio Value</th>
        <th>Gain / Loss</th>
        <th>Return %</th>
      </tr>
    </thead>
    <tbody id="projTableBody">
    </tbody>
  </table>
</div>

<!-- INSIGHTS -->
<div id="insights"></div>
```

  </div>
</div>

<!-- FOOTER -->

<footer>
  <div class="footer-disclaimer">
    ⚠️ This calculator is for illustrative purposes only. Past performance is not indicative of future results. Gold prices are volatile. This is not financial advice. XAUm is available to accredited investors only. Always read the full product documentation before investing.
  </div>
  <div style="text-align:right;">
    <div style="color:var(--gold);margin-bottom:4px;letter-spacing:2px;font-size:9px;text-transform:uppercase;">Powered by</div>
    <div style="font-family:'Fraunces',serif;font-size:16px;font-style:italic;color:var(--text2);">Matrixdock · XAUm</div>
  </div>
</footer>

<script>
// ─── STATE ───
let frequency = 'monthly';
let scenario = 'base';
let goldPrice = 3042.80;
const scenarioRates = { bear: -0.10, base: 0.08, bull: 0.20 };
const freqMultiplier = { weekly: 52, monthly: 12, quarterly: 4 };
const freqLabel = { weekly: 'wk', monthly: 'mo', quarterly: 'qtr' };

// ─── LIVE PRICE TICK ───
setInterval(() => {
  goldPrice += (Math.random() - 0.49) * 1.2;
  document.getElementById('livePrice').textContent = '$' + goldPrice.toFixed(2);
  const change = ((goldPrice - 2917.20) / 2917.20 * 100);
  const el = document.getElementById('liveChange');
  el.textContent = (change >= 0 ? '▲ +' : '▼ ') + Math.abs(change).toFixed(2) + '% today';
  el.style.color = change >= 0 ? 'var(--green)' : 'var(--red)';
}, 4000);

// ─── SLIDER UPDATES ───
function updateInvest(v) {
  document.getElementById('investDisplay').textContent = '$' + Number(v).toLocaleString();
  updateSliderTrack('investSlider','investTrack',50,5000);
  calculate();
}

function updateTarget(v) {
  document.getElementById('targetDisplay').textContent = v + ' oz';
  updateSliderTrack('targetSlider','targetTrack',1,100);
  calculate();
}

function updateSliderTrack(sliderId, trackId, min, max) {
  const slider = document.getElementById(sliderId);
  const track = document.getElementById(trackId);
  const pct = (slider.value - min) / (max - min) * 100;
  track.style.width = pct + '%';
}

function setFreq(f, el) {
  frequency = f;
  document.querySelectorAll('.freq-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  calculate();
}

function setScenario(s, el) {
  scenario = s;
  document.querySelectorAll('.scenario-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  calculate();
}

// ─── CORE CALCULATION ───
function calculate() {
  const investPerPeriod = parseFloat(document.getElementById('investSlider').value);
  const targetOz = parseFloat(document.getElementById('targetSlider').value);
  const currentOz = parseFloat(document.getElementById('currentHoldings').value) || 0;
  const periodsPerYear = freqMultiplier[frequency];
  const annualRate = scenarioRates[scenario];
  const ratePerPeriod = Math.pow(1 + annualRate, 1/periodsPerYear) - 1;

  let currentPrice = goldPrice;
  let ozAccumulated = currentOz;
  let totalInvested = currentOz * goldPrice;
  const periods = [];
  let targetReached = {};
  const milestoneTargets = [1, Math.ceil(targetOz * 0.25), Math.ceil(targetOz * 0.5), targetOz];
  const uniqueMilestones = [...new Set([1, Math.max(1, Math.round(targetOz/4)), Math.max(2, Math.round(targetOz/2)), targetOz])];

  // Run simulation — max 600 periods (50 years)
  for (let p = 1; p <= 600; p++) {
    currentPrice *= (1 + ratePerPeriod);
    const ozBought = investPerPeriod / currentPrice;
    ozAccumulated += ozBought;
    totalInvested += investPerPeriod;

    // Record milestones
    uniqueMilestones.forEach(m => {
      if (!targetReached[m] && ozAccumulated >= m) {
        targetReached[m] = {
          periods: p,
          invested: totalInvested,
          value: ozAccumulated * currentPrice,
          oz: ozAccumulated,
          price: currentPrice
        };
      }
    });

    // Store yearly snapshots
    if (p % periodsPerYear === 0) {
      periods.push({
        year: p / periodsPerYear,
        oz: ozAccumulated,
        invested: totalInvested,
        value: ozAccumulated * currentPrice,
        price: currentPrice
      });
    }

    if (ozAccumulated >= targetOz && periods.length >= 1) break;
    if (periods.length >= 30) break;
  }

  const final = periods[periods.length - 1];
  const gain = final.value - final.invested;
  const returnPct = ((final.value / final.invested) - 1) * 100;

  // Update summary
  document.getElementById('totalInvested').textContent = '$' + Math.round(final.invested).toLocaleString();
  document.getElementById('totalOz').textContent = final.oz.toFixed(2) + ' oz';
  document.getElementById('finalValue').textContent = '$' + Math.round(final.value).toLocaleString();
  const retEl = document.getElementById('totalReturn');
  retEl.textContent = (gain >= 0 ? '+' : '') + '$' + Math.round(Math.abs(gain)).toLocaleString() + ' (' + returnPct.toFixed(0) + '%)';
  retEl.className = 'summary-value ' + (gain >= 0 ? 'green' : 'red');

  // Update milestones
  const msEl = document.getElementById('milestones');
  const msData = uniqueMilestones.slice(0,3);
  msEl.innerHTML = msData.map(m => {
    const d = targetReached[m];
    if (!d) return '';
    const mos = Math.round(d.periods / (periodsPerYear / 12));
    const label = mos < 12 ? mos + ' months' : (mos/12).toFixed(1) + ' years';
    const gain = d.value - d.invested;
    return `<div class="milestone animate-in">
      <div class="milestone-oz">${m} oz</div>
      <div class="milestone-label">target</div>
      <div class="milestone-months">${label}</div>
      <div class="milestone-months-label">to reach goal</div>
      <div class="milestone-value">${gain >= 0 ? '+' : ''}$${Math.round(gain).toLocaleString()} gain</div>
    </div>`;
  }).join('');

  // Update table
  const tbody = document.getElementById('projTableBody');
  tbody.innerHTML = periods.map(p => {
    const gain = p.value - p.invested;
    const ret = ((p.value / p.invested) - 1) * 100;
    return `<tr>
      <td>Year ${p.year}</td>
      <td>${p.oz.toFixed(3)} oz</td>
      <td>$${Math.round(p.invested).toLocaleString()}</td>
      <td>$${Math.round(p.value).toLocaleString()}</td>
      <td class="${gain >= 0 ? 'positive' : 'negative'}">${gain >= 0 ? '+' : ''}$${Math.round(Math.abs(gain)).toLocaleString()}</td>
      <td class="${ret >= 0 ? 'positive' : 'negative'}">${ret >= 0 ? '+' : ''}${ret.toFixed(1)}%</td>
    </tr>`;
  }).join('');

  // Draw chart
  drawProjectionChart(periods);

  // Insights
  generateInsights(periods, investPerPeriod, targetOz, final, returnPct);
}

// ─── CHART ───
function drawProjectionChart(periods) {
  const canvas = document.getElementById('projChart');
  const ctx = canvas.getContext('2d');
  const W = canvas.offsetWidth || 600;
  const H = 240;
  canvas.width = W * devicePixelRatio;
  canvas.height = H * devicePixelRatio;
  canvas.style.width = W + 'px';
  canvas.style.height = H + 'px';
  ctx.scale(devicePixelRatio, devicePixelRatio);

  const pad = {t:16,r:16,b:36,l:72};
  const cW = W - pad.l - pad.r;
  const cH = H - pad.t - pad.b;

  const values = periods.map(p => p.value);
  const invested = periods.map(p => p.invested);
  const allVals = [...values, ...invested];
  const minV = 0;
  const maxV = Math.max(...allVals) * 1.08;

  const xScale = i => pad.l + (i / (periods.length - 1)) * cW;
  const yScale = v => pad.t + (1 - (v - minV) / (maxV - minV)) * cH;

  // Grid lines
  ctx.strokeStyle = 'rgba(255,255,255,0.04)';
  ctx.lineWidth = 1;
  for (let i = 0; i <= 4; i++) {
    const y = pad.t + (i / 4) * cH;
    ctx.beginPath(); ctx.moveTo(pad.l, y); ctx.lineTo(pad.l + cW, y); ctx.stroke();
    const val = maxV - (i / 4) * maxV;
    ctx.fillStyle = 'rgba(255,255,255,0.2)';
    ctx.font = `10px DM Mono`;
    ctx.textAlign = 'right';
    ctx.fillText('$' + (val >= 1000 ? (val/1000).toFixed(0) + 'k' : Math.round(val)), pad.l - 6, y + 3);
  }

  // X axis labels
  ctx.fillStyle = 'rgba(255,255,255,0.2)';
  ctx.font = '9px DM Mono';
  ctx.textAlign = 'center';
  const step = Math.max(1, Math.floor(periods.length / 5));
  periods.forEach((p, i) => {
    if (i % step === 0 || i === periods.length - 1) {
      ctx.fillText('Yr ' + p.year, xScale(i), H - pad.b + 16);
    }
  });

  // Invested area
  ctx.beginPath();
  invested.forEach((v, i) => i === 0 ? ctx.moveTo(xScale(i), yScale(v)) : ctx.lineTo(xScale(i), yScale(v)));
  ctx.lineTo(xScale(invested.length - 1), yScale(0));
  ctx.lineTo(xScale(0), yScale(0));
  ctx.closePath();
  ctx.fillStyle = 'rgba(255,255,255,0.04)';
  ctx.fill();

  // Invested line
  ctx.beginPath();
  invested.forEach((v, i) => i === 0 ? ctx.moveTo(xScale(i), yScale(v)) : ctx.lineTo(xScale(i), yScale(v)));
  ctx.strokeStyle = 'rgba(255,255,255,0.2)';
  ctx.lineWidth = 1.5;
  ctx.setLineDash([4, 4]);
  ctx.stroke();
  ctx.setLineDash([]);

  // Value gradient fill
  const grad = ctx.createLinearGradient(0, pad.t, 0, pad.t + cH);
  grad.addColorStop(0, 'rgba(200,151,58,0.25)');
  grad.addColorStop(1, 'rgba(200,151,58,0)');
  ctx.beginPath();
  values.forEach((v, i) => i === 0 ? ctx.moveTo(xScale(i), yScale(v)) : ctx.lineTo(xScale(i), yScale(v)));
  ctx.lineTo(xScale(values.length - 1), pad.t + cH);
  ctx.lineTo(xScale(0), pad.t + cH);
  ctx.closePath();
  ctx.fillStyle = grad;
  ctx.fill();

  // Value line
  ctx.beginPath();
  values.forEach((v, i) => i === 0 ? ctx.moveTo(xScale(i), yScale(v)) : ctx.lineTo(xScale(i), yScale(v)));
  ctx.strokeStyle = 'var(--gold)';
  ctx.lineWidth = 2.5;
  ctx.stroke();

  // End dot
  const lastX = xScale(values.length - 1);
  const lastY = yScale(values[values.length - 1]);
  ctx.beginPath(); ctx.arc(lastX, lastY, 5, 0, Math.PI * 2);
  ctx.fillStyle = 'var(--gold2)'; ctx.fill();
  ctx.beginPath(); ctx.arc(lastX, lastY, 9, 0, Math.PI * 2);
  ctx.strokeStyle = 'rgba(200,151,58,0.4)'; ctx.lineWidth = 2; ctx.stroke();
}

// ─── INSIGHTS ───
function generateInsights(periods, investPerPeriod, targetOz, final, returnPct) {
  const container = document.getElementById('insights');
  const insights = [];
  const periodsPerYear = freqMultiplier[frequency];

  // Cost avg insight
  const avgPrice = final.invested / final.oz;
  const priceDiff = ((goldPrice - avgPrice) / avgPrice * 100);
  insights.push({
    icon: '📊',
    text: `Your average buy price across the entire DCA period would be <strong>$${avgPrice.toFixed(0)}</strong> per oz — that's <strong>${Math.abs(priceDiff).toFixed(1)}% ${priceDiff < 0 ? 'below' : 'above'}</strong> today's spot price. DCA smooths out price volatility over time.`
  });

  // Compounding insight
  if (returnPct > 0) {
    const goldGain = ((scenarioRates[scenario] * 100)).toFixed(0);
    insights.push({
      icon: '🥇',
      text: `In the <strong>${scenario}</strong> scenario (gold ${goldGain > 0 ? '+' : ''}${goldGain}%/yr), your <strong>$${Math.round(final.invested).toLocaleString()}</strong> invested would grow to <strong>$${Math.round(final.value).toLocaleString()}</strong> — a return of <strong>+${returnPct.toFixed(0)}%</strong>. The power of compounding gold appreciation.`
    });
  }

  // Emerging market insight
  insights.push({
    icon: '🌍',
    text: `Investing <strong>$${investPerPeriod.toLocaleString()}</strong> per ${freqLabel[frequency]} is within reach for millions of savers in West Africa, South Asia, and Southeast Asia — where gold has been the primary store of value for generations. XAUm makes this accessible on-chain, globally, with $1 minimums.`
  });

  container.innerHTML = insights.map(i => `
    <div class="insight">
      <div class="insight-icon">${i.icon}</div>
      <div class="insight-text">${i.text}</div>
    </div>
  `).join('');
} but

// ─── INIT ───
window.addEventListener('load', () => {
  updateSliderTrack('investSlider','investTrack',50,5000);
  updateSliderTrack('targetSlider','targetTrack',1,100);
  calculate();
});

window.addEventListener('resize', () => {
  calculate();
});
</script>

</body>
</html>
