python data structures
html
Michael Ee shared this file. Want to do more with it?
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Python Data Structures — A Refined Mental Model</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:ital,wght@0,300;0,400;0,500;1,300&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,700;1,9..144,300&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #0e0e0e;
    --paper: #f5f0e8;
    --cream: #ede8dc;
    --rule: #c8c0b0;
    --accent-red: #c0392b;
    --accent-blue: #1a4a7a;
    --accent-gold: #b8860b;
    --accent-green: #2d6a4f;
    --accent-orange: #c45e1a;
    --muted: #6b6560;
    --code-bg: #1e1e1e;
    --code-text: #d4d0c8;
  }
﻿
  * { box-sizing: border-box; margin: 0; padding: 0; }
﻿
  body {
    background: var(--paper);
    color: var(--ink);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    line-height: 1.6;
    padding: 48px 24px 80px;
  }
﻿
  /* PAGE HEADER */
  .page-header {
    max-width: 900px;
    margin: 0 auto 64px;
    border-bottom: 2px solid var(--ink);
    padding-bottom: 32px;
  }
  .page-header .eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 12px;
  }
  .page-header h1 {
    font-family: 'Fraunces', serif;
    font-size: clamp(36px, 6vw, 64px);
    font-weight: 700;
    line-height: 1.05;
    letter-spacing: -0.02em;
  }
  .page-header h1 em {
    font-style: italic;
    font-weight: 300;
    color: var(--accent-blue);
  }
  .page-header .subtitle {
    margin-top: 16px;
    max-width: 560px;
    color: var(--muted);
    font-size: 15px;
    line-height: 1.7;
  }
﻿
  /* SECTION WRAPPER */
  .section {
    max-width: 900px;
    margin: 0 auto 72px;
  }
  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
    border-left: 3px solid var(--accent-red);
    padding-left: 12px;
    margin-bottom: 8px;
  }
  .section-title {
    font-family: 'Fraunces', serif;
    font-size: 28px;
    font-weight: 700;
    margin-bottom: 6px;
    letter-spacing: -0.01em;
  }
  .section-intro {
    color: var(--muted);
    font-size: 14px;
    max-width: 620px;
    margin-bottom: 28px;
    line-height: 1.7;
  }
﻿
  /* ─── AXIS 1: DEPENDENCY CHAIN ─── */
  .chain {
    display: flex;
    align-items: stretch;
    gap: 0;
    overflow-x: auto;
    padding-bottom: 4px;
  }
  .chain-node {
    flex: 1;
    min-width: 140px;
    border: 1.5px solid var(--ink);
    background: var(--cream);
    padding: 20px 16px 16px;
    position: relative;
    animation: fadeUp 0.5s ease both;
  }
  .chain-node:not(:first-child) { border-left: none; }
  .chain-node:nth-child(1) { animation-delay: 0.0s; }
  .chain-node:nth-child(2) { animation-delay: 0.1s; }
  .chain-node:nth-child(3) { animation-delay: 0.2s; }
  .chain-node:nth-child(4) { animation-delay: 0.3s; }
  .chain-node:nth-child(5) { animation-delay: 0.4s; }
﻿
  .chain-node .layer-badge {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    background: var(--ink);
    color: var(--paper);
    display: inline-block;
    padding: 2px 7px;
    margin-bottom: 10px;
  }
  .chain-node .node-name {
    font-family: 'Fraunces', serif;
    font-size: 17px;
    font-weight: 700;
    margin-bottom: 4px;
  }
  .chain-node .node-code {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--accent-blue);
    margin-bottom: 10px;
    line-height: 1.5;
  }
  .chain-node .node-desc {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.6;
  }
  .chain-arrow {
    display: flex;
    align-items: center;
    padding: 0 2px;
    color: var(--accent-red);
    font-size: 20px;
    font-weight: bold;
    flex-shrink: 0;
    z-index: 2;
    position: relative;
  }
  .built-on-tag {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    background: var(--accent-green);
    color: white;
    padding: 2px 6px;
    display: inline-block;
    margin-top: 6px;
  }
﻿
  /* ─── AXIS 2: PROBLEM MATRIX ─── */
  .problem-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    gap: 1px;
    background: var(--ink);
    border: 1.5px solid var(--ink);
  }
  .problem-card {
    background: var(--cream);
    padding: 20px 18px;
    animation: fadeUp 0.5s ease both;
  }
  .problem-card:nth-child(1) { animation-delay: 0.05s; }
  .problem-card:nth-child(2) { animation-delay: 0.1s; }
  .problem-card:nth-child(3) { animation-delay: 0.15s; }
  .problem-card:nth-child(4) { animation-delay: 0.2s; }
  .problem-card:nth-child(5) { animation-delay: 0.25s; }
  .problem-card:nth-child(6) { animation-delay: 0.3s; }
  .problem-card:nth-child(7) { animation-delay: 0.35s; }
﻿
  .problem-card .struct-name {
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    font-weight: 500;
    color: var(--accent-blue);
    margin-bottom: 4px;
  }
  .problem-card .question {
    font-family: 'Fraunces', serif;
    font-style: italic;
    font-size: 14px;
    color: var(--ink);
    margin-bottom: 10px;
    line-height: 1.4;
  }
  .problem-card .when-use {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.6;
    margin-bottom: 10px;
  }
  .problem-card .code-eg {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    background: var(--ink);
    color: #a8d8a8;
    padding: 6px 8px;
    line-height: 1.6;
  }
  .tag {
    display: inline-block;
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 2px 6px;
    margin-right: 4px;
    margin-top: 8px;
  }
  .tag-mutable   { background: #2d6a4f; color: white; }
  .tag-immutable { background: #b8860b; color: white; }
  .tag-unordered { background: #c0392b; color: white; }
  .tag-ordered   { background: #1a4a7a; color: white; }
  .tag-numpy     { background: #5a4fcf; color: white; }
  .tag-pandas    { background: #c45e1a; color: white; }
﻿
  /* ─── AXIS 3: DIMENSIONALITY ─── */
  .dim-row {
    display: grid;
    grid-template-columns: 80px 1fr;
    gap: 0;
    border: 1.5px solid var(--ink);
    margin-bottom: -1px;
    animation: fadeUp 0.5s ease both;
    background: var(--cream);
  }
  .dim-row:nth-child(1) { animation-delay: 0.05s; }
  .dim-row:nth-child(2) { animation-delay: 0.1s; }
  .dim-row:nth-child(3) { animation-delay: 0.15s; }
  .dim-row:nth-child(4) { animation-delay: 0.2s; }
﻿
  .dim-label {
    background: var(--ink);
    color: var(--paper);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-family: 'Fraunces', serif;
    font-size: 22px;
    font-weight: 700;
    border-right: 1.5px solid var(--ink);
    gap: 2px;
  }
  .dim-label span {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    font-weight: 400;
    color: var(--rule);
    letter-spacing: 0.1em;
  }
  .dim-content {
    padding: 16px 20px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    align-items: center;
  }
  .dim-content .what {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.6;
  }
  .dim-content .what strong {
    font-weight: 500;
    color: var(--ink);
    display: block;
    font-family: 'Fraunces', serif;
    font-size: 15px;
    margin-bottom: 3px;
  }
  .dim-content .dim-code {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    background: var(--ink);
    color: #a8d8a8;
    padding: 8px 10px;
    line-height: 1.8;
  }
﻿
  /* ─── FLOW SECTION ─── */
  .flow-strip {
    background: var(--ink);
    color: var(--paper);
    padding: 32px 36px;
    border: 1.5px solid var(--ink);
  }
  .flow-strip h3 {
    font-family: 'Fraunces', serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 20px;
    color: var(--paper);
  }
  .flow-steps {
    display: flex;
    gap: 0;
    flex-wrap: wrap;
  }
  .flow-step {
    flex: 1;
    min-width: 160px;
    padding: 16px 18px;
    border-right: 1px solid #333;
    animation: fadeUp 0.5s ease both;
  }
  .flow-step:last-child { border-right: none; }
  .flow-step:nth-child(1) { animation-delay: 0.05s; }
  .flow-step:nth-child(2) { animation-delay: 0.12s; }
  .flow-step:nth-child(3) { animation-delay: 0.19s; }
  .flow-step:nth-child(4) { animation-delay: 0.26s; }
﻿
  .flow-step .step-num {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--accent-red);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 6px;
  }
  .flow-step .step-title {
    font-family: 'Fraunces', serif;
    font-size: 15px;
    color: var(--paper);
    margin-bottom: 6px;
  }
  .flow-step .step-code {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: #a8d8a8;
    line-height: 1.7;
    margin-bottom: 8px;
  }
  .flow-step .step-note {
    font-size: 11px;
    color: #888;
    line-height: 1.5;
  }
﻿
  /* ─── WRITTEN GUIDE ─── */
  .guide {
    max-width: 900px;
    margin: 0 auto 40px;
    border-top: 2px solid var(--ink);
    padding-top: 48px;
  }
  .guide-title {
    font-family: 'Fraunces', serif;
    font-size: 32px;
    font-weight: 700;
    margin-bottom: 32px;
    letter-spacing: -0.01em;
  }
  .guide-title em { font-style: italic; font-weight: 300; color: var(--accent-blue); }
﻿
  .guide-block {
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 32px;
    margin-bottom: 40px;
    padding-bottom: 40px;
    border-bottom: 1px solid var(--rule);
    animation: fadeUp 0.5s ease both;
  }
  .guide-block:nth-child(2) { animation-delay: 0.05s; }
  .guide-block:nth-child(3) { animation-delay: 0.1s; }
  .guide-block:nth-child(4) { animation-delay: 0.15s; }
  .guide-block:nth-child(5) { animation-delay: 0.2s; }
  .guide-block:nth-child(6) { animation-delay: 0.25s; }
﻿
  @media (max-width: 600px) {
    .guide-block { grid-template-columns: 1fr; gap: 12px; }
  }
﻿
  .guide-num {
    font-family: 'Fraunces', serif;
    font-size: 72px;
    font-weight: 700;
    color: var(--cream);
    line-height: 1;
    -webkit-text-stroke: 2px var(--rule);
    text-stroke: 2px var(--rule);
    user-select: none;
  }
  .guide-body h4 {
    font-family: 'Fraunces', serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 8px;
  }
  .guide-body p {
    font-size: 14px;
    color: var(--muted);
    line-height: 1.8;
    margin-bottom: 12px;
  }
  .guide-body .callout {
    background: var(--cream);
    border-left: 3px solid var(--accent-blue);
    padding: 10px 14px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--accent-blue);
    line-height: 1.7;
    margin-top: 10px;
  }
  .guide-body .warning {
    border-left-color: var(--accent-red);
    color: var(--accent-red);
  }
﻿
  /* FOOTER */
  .footer {
    max-width: 900px;
    margin: 0 auto;
    padding-top: 32px;
    border-top: 1px solid var(--rule);
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 8px;
  }
﻿
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }
﻿
  /* scrollbar */
  ::-webkit-scrollbar { height: 4px; }
  ::-webkit-scrollbar-track { background: var(--cream); }
  ::-webkit-scrollbar-thumb { background: var(--rule); }
</style>
</head>
<body>
﻿
<!-- ══════════════════════════════════════════ HEADER -->
<header class="page-header">
  <div class="eyebrow">Python Data Structures — Revised Mental Model</div>
  <h1>From Atoms<br>to <em>Abstractions</em></h1>
  <p class="subtitle">A three-axis framework for understanding Python data structures: the dependency chain, the problem each solves, and how dimensionality maps onto numerical libraries.</p>
</header>
﻿
<!-- ══════════════════════════════════════════ AXIS 1 -->
<section class="section">
  <div class="section-label">Axis 1</div>
  <div class="section-title">The Dependency Chain</div>
  <p class="section-intro">Everything in numpy and pandas ultimately rests on Python's primitive types. This is the actual build-up — each layer is constructed from what came before.</p>
﻿
  <div class="chain">
    <div class="chain-node">
      <div class="layer-badge">Layer 0</div>
      <div class="node-name">Primitives</div>
      <div class="node-code">int, float, bool<br>str, complex</div>
      <div class="node-desc">Atomic values. Immutable. Everything is built from these.</div>
    </div>
    <div class="chain-arrow">→</div>
    <div class="chain-node">
      <div class="layer-badge">Layer 1</div>
      <div class="node-name">Built-in Collections</div>
      <div class="node-code">list, tuple<br>dict, set</div>
      <div class="node-desc">Pure Python containers holding any mix of objects. Flexible but slow for maths.</div>
    </div>
    <div class="chain-arrow">→</div>
    <div class="chain-node">
      <div class="layer-badge">Layer 2</div>
      <div class="node-name">ndarray</div>
      <div class="node-code">np.array([1,2,3])</div>
      <div class="node-desc">Typed, fixed-size array. Built in C on top of Python lists. Fast numerical ops.</div>
      <span class="built-on-tag">built on: list + C</span>
    </div>
    <div class="chain-arrow">→</div>
    <div class="chain-node">
      <div class="layer-badge">Layer 3</div>
      <div class="node-name">Series</div>
      <div class="node-code">pd.Series([10,20])</div>
      <div class="node-desc">A labelled 1D ndarray. Adds an index on top of numpy.</div>
      <span class="built-on-tag">built on: ndarray</span>
    </div>
    <div class="chain-arrow">→</div>
    <div class="chain-node">
      <div class="layer-badge">Layer 4</div>
      <div class="node-name">DataFrame</div>
      <div class="node-code">pd.DataFrame({...})</div>
      <div class="node-desc">A dict of Series sharing one index. Your spreadsheet in Python.</div>
      <span class="built-on-tag">built on: Series × n</span>
    </div>
  </div>
</section>
﻿
<!-- ══════════════════════════════════════════ AXIS 2 -->
<section class="section">
  <div class="section-label">Axis 2</div>
  <div class="section-title">The Problem Each Solves</div>
  <p class="section-intro">Don't classify structures — ask what question they answer. The right structure becomes obvious when you think in problems, not categories.</p>
﻿
  <div class="problem-grid">
    <div class="problem-card">
      <div class="struct-name">list</div>
      <div class="question">"I need a sequence I can grow or modify"</div>
      <div class="when-use">Ordered collection of any types. Your go-to default. Append, pop, slice.</div>
      <div class="code-eg">items = [1, "a", True]<br>items.append(4)</div>
      <span class="tag tag-mutable">mutable</span>
      <span class="tag tag-ordered">ordered</span>
    </div>
    <div class="problem-card">
      <div class="struct-name">tuple</div>
      <div class="question">"I need a fixed record or multiple return values"</div>
      <div class="when-use">Immutable. Use for coordinates, DB rows, function returns. Slightly faster than list.</div>
      <div class="code-eg">point = (3, 4)<br>x, y = get_coords()</div>
      <span class="tag tag-immutable">immutable</span>
      <span class="tag tag-ordered">ordered</span>
    </div>
    <div class="problem-card">
      <div class="struct-name">dict</div>
      <div class="question">"I need fast lookup by name or key"</div>
      <div class="when-use">O(1) key access. Ordered by insertion since Python 3.7, but don't rely on it for logic.</div>
      <div class="code-eg">scores = {"alice": 95}<br>scores["alice"]  # → 95</div>
      <span class="tag tag-mutable">mutable</span>
      <span class="tag tag-ordered">ordered*</span>
    </div>
    <div class="problem-card">
      <div class="struct-name">set</div>
      <div class="question">"I need unique items or fast membership tests"</div>
      <div class="when-use">O(1) 'in' checks. Great for deduplication, intersection, difference.</div>
      <div class="code-eg">seen = {1, 2, 3}<br>4 in seen  # → False</div>
      <span class="tag tag-mutable">mutable</span>
      <span class="tag tag-unordered">unordered</span>
    </div>
    <div class="problem-card">
      <div class="struct-name">np.ndarray</div>
      <div class="question">"I need fast maths over large arrays"</div>
      <div class="when-use">Vectorised ops run in C. Homogeneous type only. No Python loop needed.</div>
      <div class="code-eg">a = np.array([1,2,3])<br>a * 2  # → [2,4,6]</div>
      <span class="tag tag-mutable">mutable</span>
      <span class="tag tag-numpy">numpy</span>
    </div>
    <div class="problem-card">
      <div class="struct-name">pd.Series</div>
      <div class="question">"I need a labelled 1D array with an index"</div>
      <div class="when-use">Like ndarray but each element has a label. One column of a DataFrame.</div>
      <div class="code-eg">s = pd.Series([10,20],<br>  index=["a","b"])</div>
      <span class="tag tag-mutable">mutable</span>
      <span class="tag tag-pandas">pandas</span>
    </div>
    <div class="problem-card">
      <div class="struct-name">pd.DataFrame</div>
      <div class="question">"I need a table with named columns and rows"</div>
      <div class="when-use">The workhorse for data analysis. Think spreadsheet with superpowers.</div>
      <div class="code-eg">df = pd.DataFrame({<br>  "A":[1,2],"B":[3,4]})</div>
      <span class="tag tag-mutable">mutable</span>
      <span class="tag tag-pandas">pandas</span>
    </div>
  </div>
</section>
﻿
<!-- ══════════════════════════════════════════ AXIS 3 -->
<section class="section">
  <div class="section-label">Axis 3</div>
  <div class="section-title">Dimensionality</div>
  <p class="section-intro">This is where numpy clicks. Shape is everything. The same ndarray type handles all four levels — only the shape changes.</p>
﻿
  <div class="dim-row">
    <div class="dim-label">0D<span>scalar</span></div>
    <div class="dim-content">
      <div class="what"><strong>Scalar</strong>A single value. No axis to index into. Technically a 0-D ndarray — distinct from a Python int.</div>
      <div class="dim-code">x = np.array(42)<br>x.shape  # → ()<br>x.ndim   # → 0</div>
    </div>
  </div>
  <div class="dim-row">
    <div class="dim-label">1D<span>vector</span></div>
    <div class="dim-content">
      <div class="what"><strong>Vector</strong>A sequence of values along one axis. A pd.Series is always 1D. Shape: (n,)</div>
      <div class="dim-code">v = np.array([1,2,3])<br>v.shape  # → (3,)<br>v[0]     # → 1</div>
    </div>
  </div>
  <div class="dim-row">
    <div class="dim-label">2D<span>matrix</span></div>
    <div class="dim-content">
      <div class="what"><strong>Matrix</strong>Rows × columns. A pd.DataFrame is 2D. The core of most data science work. Shape: (rows, cols)</div>
      <div class="dim-code">m = np.array([[1,2],[3,4]])<br>m.shape  # → (2, 2)<br>m[0, 1]  # → 2</div>
    </div>
  </div>
  <div class="dim-row">
    <div class="dim-label">3D+<span>tensor</span></div>
    <div class="dim-content">
      <div class="what"><strong>Tensor</strong>Multiple matrices stacked. Images (H×W×channels), video, deep learning weights. Shape: (batch, rows, cols)</div>
      <div class="dim-code">t = np.zeros((10,28,28))<br>t.shape  # → (10, 28, 28)<br># e.g. 10 greyscale images</div>
    </div>
  </div>
</section>
﻿
<!-- ══════════════════════════════════════════ DATA FLOW -->
<section class="section">
  <div class="section-label">Bonus: Data Flow</div>
  <div class="section-title">How the Layers Connect in Practice</div>
  <p class="section-intro">In real code, data almost always flows upward through the layers. Understanding these conversions is more useful than memorising definitions.</p>
﻿
  <div class="flow-strip">
    <h3>A common real-world data pipeline</h3>
    <div class="flow-steps">
      <div class="flow-step">
        <div class="step-num">Step 01</div>
        <div class="step-title">Python list</div>
        <div class="step-code">data = [1, 2, 3, 4]</div>
        <div class="step-note">Raw data. Mixed types OK. Slow for maths.</div>
      </div>
      <div class="flow-step">
        <div class="step-num">Step 02</div>
        <div class="step-title">numpy array</div>
        <div class="step-code">arr = np.array(data)<br># shape: (4,)</div>
        <div class="step-note">Typed, vectorised. Now you can do fast maths.</div>
      </div>
      <div class="flow-step">
        <div class="step-num">Step 03</div>
        <div class="step-title">pandas Series</div>
        <div class="step-code">s = pd.Series(arr)<br># labelled 1D</div>
        <div class="step-note">Gains an index. Can be named, sliced by label.</div>
      </div>
      <div class="flow-step">
        <div class="step-num">Step 04</div>
        <div class="step-title">pandas DataFrame</div>
        <div class="step-code">df = pd.DataFrame(<br>  {"col": s})</div>
        <div class="step-note">Multiple Series as columns. Full table for analysis.</div>
      </div>
    </div>
  </div>
</section>
﻿
<!-- ══════════════════════════════════════════ WRITTEN GUIDE -->
<div class="guide">
  <div class="guide-title">The Written <em>Accompaniment</em></div>
﻿
  <div class="guide-block">
    <div class="guide-num">01</div>
    <div class="guide-body">
      <h4>Primitives are the foundation — but they're not "simple"</h4>
      <p>Python's primitive types (int, float, str, bool, complex) are immutable objects, not raw memory values like in C. When you write <code>x = 42</code>, Python creates an object in memory and binds the name <code>x</code> to it. This matters because two variables can point to the same object — something that surprises beginners when they first mutate a list they thought they'd "copied".</p>
      <div class="callout">Key insight: In Python, variables are names that reference objects — not boxes that contain values. This is why <code>a = b = []</code> gives you one list with two names, not two lists.</div>
    </div>
  </div>
﻿
  <div class="guide-block">
    <div class="guide-num">02</div>
    <div class="guide-body">
      <h4>Mutability is about identity, not content</h4>
      <p>The mutable/immutable distinction trips people up because it's about whether the <em>object itself</em> can change — not whether the variable can be reassigned. A tuple is immutable: you can't change what's inside it. A list is mutable: you can append, remove, sort in place.</p>
      <p>The practical consequence: mutable objects can be modified inside functions and the change will be visible outside. Immutable ones cannot.</p>
      <div class="callout warning">Watch out: dict is mutable and ordered (since Python 3.7), but "ordered" means insertion order — not sorted order. Don't rely on ordering for logic; use it only for predictability.</div>
    </div>
  </div>
﻿
  <div class="guide-block">
    <div class="guide-num">03</div>
    <div class="guide-body">
      <h4>numpy's ndarray is a fundamentally different kind of container</h4>
      <p>A Python list can hold anything — integers, strings, other lists, functions. An ndarray holds one type only (int32, float64, etc.), and that homogeneity is what makes it fast. The actual data lives in a contiguous block of memory, so numpy can pass it directly to C routines without any Python overhead per element.</p>
      <p>This is why <code>np.array([1,2,3]) * 2</code> is orders of magnitude faster than a Python for-loop — the multiplication happens in C across the whole array at once.</p>
      <div class="callout">Rule of thumb: if you're doing numerical computation on more than a handful of values, reach for ndarray. If you're storing mixed or irregular data, stay with a list or dict.</div>
    </div>
  </div>
﻿
  <div class="guide-block">
    <div class="guide-num">04</div>
    <div class="guide-body">
      <h4>pandas is numpy with labels and convenience</h4>
      <p>A pd.Series is essentially a numpy 1D array with an index (row labels). A pd.DataFrame is a dictionary of Series that all share the same index. This is not a metaphor — you can access the underlying numpy array of any DataFrame column via <code>df["col"].values</code>.</p>
      <p>The label system is what makes pandas powerful for data analysis: you can align data by label automatically, slice by name instead of position, and group/merge by meaningful keys rather than integer offsets.</p>
      <div class="callout">Dependency chain: list → ndarray → Series → DataFrame. pandas is never replacing numpy — it's sitting on top of it. When pandas is slow, the solution is often to drop down to numpy operations directly.</div>
    </div>
  </div>
﻿
  <div class="guide-block">
    <div class="guide-num">05</div>
    <div class="guide-body">
      <h4>Dimensionality is a shape property, not a type property</h4>
      <p>Scalar, vector, matrix, and tensor are not different types in numpy — they're the same ndarray type with different <code>.shape</code> tuples. A scalar has shape <code>()</code>, a vector <code>(n,)</code>, a matrix <code>(m, n)</code>, a 3D tensor <code>(p, m, n)</code>. You manipulate shape with <code>reshape()</code>, <code>squeeze()</code>, and <code>expand_dims()</code>.</p>
      <p>Understanding this is essential for deep learning, where mismatched tensor shapes are the most common source of errors.</p>
      <div class="callout">Practice this: create a 1D array of 12 numbers and try reshaping it to (3,4), (4,3), (2,2,3), and (1,12). They all contain the same data — just viewed differently.</div>
    </div>
  </div>
﻿
  <div class="guide-block">
    <div class="guide-num">06</div>
    <div class="guide-body">
      <h4>User-defined structures are algorithms, not just containers</h4>
      <p>Stack, Queue, Tree, and Graph aren't really about how data is stored — they're about the <em>rules of access</em>. A Stack is a list where you only interact with the top (LIFO). A Queue is a list where you add to the back and remove from the front (FIFO). Python gives you <code>collections.deque</code> as an efficient queue — you don't build one from scratch.</p>
      <p>Trees and graphs are relationship structures, implemented in Python using dicts and lists of references — not a built-in type. They appear in search algorithms, network analysis, and any hierarchical data problem.</p>
      <div class="callout">For production code: use <code>collections.deque</code> for queues, a plain list for stacks, and libraries like <code>networkx</code> for graphs. Build your own only when learning the algorithm itself.</div>
    </div>
  </div>
﻿
</div>
﻿
<!-- FOOTER -->
<footer class="footer">
  <span>Python Data Structures — Refined Mental Model</span>
  <span>3 axes: dependency · problem · dimensionality</span>
</footer>
﻿
</body>
</html>
We use cookies to provide, improve, protect and promote our services. Visit our Privacy Policy and Privacy Policy FAQs to learn more. You can manage your personal preferences, including your ‘Do not sell or share my personal data to third parties’ setting using the “Customize cookies” button below.
