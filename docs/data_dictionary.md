<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Data Dictionary — MTA Major Incidents (2025)</title>
  <style>
    :root{
      --text:#111827; --muted:#6b7280; --bg:#ffffff; --card:#f9fafb;
      --border:#e5e7eb; --accent:#2563eb;
    }
    body{font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Arial,sans-serif;
      color:var(--text); background:var(--bg); margin:0; padding:24px; line-height:1.55;}
    .container{max-width:900px; margin:0 auto;}
    h1{font-size:28px; margin:0 0 8px;}
    .sub{color:var(--muted); margin:0 0 18px;}
    .badge{display:inline-block; padding:4px 10px; border:1px solid var(--border);
      border-radius:999px; background:var(--card); font-size:12px; color:var(--muted); margin-right:8px;}
    .section{margin:22px 0;}
    .card{background:var(--card); border:1px solid var(--border); border-radius:12px; padding:16px;}
    h2{font-size:18px; margin:0 0 10px;}
    h3{font-size:15px; margin:16px 0 6px;}
    code{background:#eef2ff; padding:2px 6px; border-radius:6px; font-family: ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono",monospace;}
    ul{margin:8px 0 0 22px;}
    .field{border-top:1px solid var(--border); padding-top:12px; margin-top:12px;}
    .meta{display:grid; grid-template-columns: 160px 1fr; gap:8px 14px; margin-top:10px;}
    .meta b{color:var(--muted); font-weight:600;}
    .footer{margin-top:26px; font-size:12px; color:var(--muted);}
    a{color:var(--accent); text-decoration:none;}
    a:hover{text-decoration:underline;}
  </style>
</head>

<body>
  <div class="container">
    <h1>📘 Data Dictionary</h1>
    <p class="sub">
      <span class="badge">Project: MTA Major Incidents Analysis (2025)</span>
      <span class="badge">Source: MTA (NY Open Data)</span>
      <span class="badge">Coverage: NYC Subway</span>
    </p>

    <div class="section card">
      <h2>Dataset Overview</h2>
      <p>
        This dataset captures <b>major NYC subway service incidents</b> reported by NYC Transit.
        Each record represents the <b>count of major incidents</b> for a given subway line, month,
        incident category, and day type (weekday vs weekend).
      </p>

      <div class="meta">
        <b>Time Period</b><div>January 2025 – November 2025</div>
        <b>Granularity</b><div>Month × Subway Line × Category × Day Type</div>
        <b>Metric</b><div>Major incident count</div>
      </div>
    </div>

    <div class="section card">
      <h2>Field Definitions</h2>

      <div class="field">
        <h3><code>month</code></h3>
        <p><b>Type:</b> Date (YYYY-MM-DD)</p>
        <p>
          The month in which major incidents are reported. Dates are standardized to the first day
          of the month for aggregation.
        </p>
        <p><b>Example:</b> <code>2025-01-01</code></p>
      </div>

      <div class="field">
        <h3><code>division</code></h3>
        <p><b>Type:</b> Text</p>
        <p>
          Indicates subway division:
        </p>
        <ul>
          <li><b>A Division:</b> Numbered lines (1–7)</li>
          <li><b>B Division:</b> Lettered lines (A–Z)</li>
        </ul>
        <p><b>Example:</b> <code>B Division</code></p>
      </div>

      <div class="field">
        <h3><code>line</code></h3>
        <p><b>Type:</b> Text</p>
        <p>The specific subway line where the incident occurred.</p>
        <p><b>Possible values include:</b></p>
        <p>
          <code>1, 2, 3, 4, 5, 6, 7, A, C, E, B, D, F, M, G, J, Z, L, N, Q, R, W, S</code>
        </p>
        <p><b>Example:</b> <code>E</code></p>
      </div>

      <div class="field">
        <h3><code>day_type</code></h3>
        <p><b>Type:</b> Integer</p>
        <p>Indicates whether incidents occurred on a weekday or weekend.</p>
        <ul>
          <li><code>1</code> = Weekday</li>
          <li><code>2</code> = Weekend</li>
        </ul>
        <p><b>Note:</b> Converted to <code>day_type_label</code> during analysis for readability.</p>
      </div>

      <div class="field">
        <h3><code>day_type_label</code> (Derived)</h3>
        <p><b>Type:</b> Text</p>
        <p>Human-readable label created during data cleaning.</p>
        <p><b>Values:</b> <code>Weekday</code>, <code>Weekend</code></p>
      </div>

      <div class="field">
        <h3><code>category</code></h3>
        <p><b>Type:</b> Text</p>
        <p>Classification of the major incident.</p>
        <p><b>Categories include:</b></p>
        <ul>
          <li><code>Track</code></li>
          <li><code>Signals</code></li>
          <li><code>Persons on Trackbed / Police / Medical</code></li>
          <li><code>Subway Car</code></li>
          <li><code>Stations and Structure</code></li>
          <li><code>Other</code></li>
        </ul>
      </div>

      <div class="field">
        <h3><code>count</code></h3>
        <p><b>Type:</b> Integer</p>
        <p>The number of major incidents recorded for the given combination of month, line, category, and day type.</p>
        <p><b>Example:</b> <code>6</code></p>
      </div>
    </div>

    <div class="section card">
      <h2>Notes & Limitations</h2>
      <ul>
        <li>Data reflects <b>reported major incidents only</b>; minor delays are excluded.</li>
        <li>Counts are <b>aggregated monthly</b>, not event-level.</li>
        <li>“ALL LINES” entries may appear during aggregation and were excluded from line-specific comparisons.</li>
        <li>Dataset does not include ridership, so results are not normalized by passengers.</li>
      </ul>
    </div>

    <div class="section card">
      <h2>How This Was Used</h2>
      <ul>
        <li>Exploratory Data Analysis (EDA)</li>
        <li>Trend analysis by month and subway line</li>
        <li>Category-level disruption patterns</li>
        <li>Weekday vs weekend comparison</li>
        <li>Written synthesis (without relying on dashboards)</li>
      </ul>
    </div>

    <p class="footer">
      Tip: If you’re posting this on GitHub Pages, save as <code>index.html</code>.
    </p>
  </div>
</body>
</html>
