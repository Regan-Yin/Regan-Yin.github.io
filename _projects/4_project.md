---
layout: page
title: "Safety Incident & Near-Miss Pattern Mining — Methanex Hackathon"
description: TF-IDF RAG/Ollama Cloud/DSPy + GEPA Prompt Optimization/Dash/Plotly/Cloud Run/Full-Stack Dashboard
img: assets/img/Methanex/hackathon_team_presentation.jpeg
importance: 1
category: work
related_publications: false
---

<style>
  :root{
    --card-bg:#ffffff; --card-border:#e5e7eb; --muted:#6b7280;
    --badge-bg:rgba(0,0,0,.04); --badge-border:rgba(0,0,0,.08);
    --accent:#002C77; --accent-green:#8CC63F; --accent-cyan:#44A0C8;
    --good:#0a7d3e; --bad:#9b2c2c;
  }
  [data-theme="dark"]{
    --card-bg:#0f172a; --card-border:#233047; --muted:#94a3b8;
    --badge-bg:rgba(255,255,255,.08); --badge-border:rgba(255,255,255,.12);
    --good:#34d399; --bad:#fca5a5;
  }

  .wrap{max-width:1100px;margin:0 auto;padding:0 0 1rem}
  .section{margin:2.2rem 0;contain:content;position:relative}
  .lead{font-size:1.05rem;line-height:1.7}
  .muted{color:var(--muted)}
  .badge{display:inline-block;padding:.35rem .6rem;border-radius:2rem;background:var(--badge-bg);border:1px solid var(--badge-border);margin:.15rem .2rem;font-size:.85rem;color:var(--global-text-color)}
  .badge-v2{background:rgba(140,198,63,.15);border-color:rgba(140,198,63,.4);color:var(--good);font-weight:600}
  .kpi{display:flex;gap:1rem;flex-wrap:wrap}
  .kpi .card{flex:1 1 180px;background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:.9rem;box-shadow:0 2px 12px rgba(0,0,0,.06);color:var(--global-text-color)}
  .kpi .card .muted{color:var(--muted)}
  figure{margin:0}
  figure img{display:block;width:100%;height:auto;max-width:100%;border-radius:.75rem;box-shadow:0 6px 18px rgba(0,0,0,.08)}
  figure figcaption{color:var(--muted);font-size:.9rem;margin-top:.5rem}
  .grid-2{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:1rem}
  .code{background:#0b0f19;color:#e8e8e8;border-radius:.6rem;padding:1rem 1.2rem;overflow:auto;font-size:.88rem;line-height:1.55}
  pre{margin:0;white-space:pre;overflow:auto}
  code{word-break:normal}
  table{width:100%;border-collapse:collapse;font-size:.95rem}
  th,td{padding:.6rem .65rem;border-bottom:1px solid var(--card-border);vertical-align:top}
  th{text-align:left;color:var(--accent);background:var(--badge-bg)}
  .toc a{display:block;padding:.2rem 0}
  .arch-box{background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:1.2rem;margin:.75rem 0;box-shadow:0 2px 12px rgba(0,0,0,.04)}
  .arch-box h4{margin:0 0 .5rem;color:var(--accent)}
  .arch-row{display:flex;gap:1rem;flex-wrap:wrap}
  .arch-row .arch-box{flex:1 1 200px}
  .cluster-tag{display:inline-block;padding:.3rem .55rem;border-radius:.4rem;background:#002C77;color:#fff;font-size:.82rem;margin:.2rem}
  .pipeline{display:flex;flex-direction:column;gap:.4rem;margin:.6rem 0 1rem}
  .pipeline .step{background:var(--card-bg);border:1px solid var(--card-border);border-left:4px solid var(--accent-cyan);border-radius:.5rem;padding:.7rem .9rem;font-size:.95rem}
  .pipeline .step strong{color:var(--accent)}
  .pipeline .arrow{align-self:center;color:var(--muted);font-size:1.1rem}
  .v-tag-old{display:inline-block;padding:.1rem .45rem;border-radius:.3rem;background:rgba(155,44,44,.12);color:var(--bad);font-size:.78rem;font-weight:600;margin-right:.3rem}
  .v-tag-new{display:inline-block;padding:.1rem .45rem;border-radius:.3rem;background:rgba(10,125,62,.12);color:var(--good);font-size:.78rem;font-weight:600;margin-right:.3rem}
  .model-row{display:grid;grid-template-columns:auto 1fr auto;gap:.5rem .9rem;padding:.4rem 0;border-bottom:1px dashed var(--card-border);align-items:center;font-size:.92rem}
  .model-row:last-child{border-bottom:none}
  .model-row code{background:var(--badge-bg);padding:.1rem .4rem;border-radius:.3rem;font-size:.85rem}
  .pill-good{color:var(--good);font-weight:600;font-size:.85rem}
  .pill-warn{color:#b45309;font-weight:600;font-size:.85rem}
  .callout{background:rgba(68,160,200,.08);border-left:4px solid var(--accent-cyan);border-radius:.5rem;padding:.8rem 1rem;margin:1rem 0;font-size:.95rem}
  .callout.warn{background:rgba(245,158,11,.08);border-left-color:#f59e0b}
  .callout.good{background:rgba(140,198,63,.1);border-left-color:var(--accent-green)}
</style>

<div class="wrap">

  <p>
    <span class="badge badge-v2">v2 — Apr 2026</span>
    <span class="badge">Migrated from Vertex AI to Ollama Cloud + DSPy/GEPA</span>
  </p>

  <p class="lead">
    <strong>Author:</strong> Regan Yin &nbsp;|&nbsp;
    <strong>Team:</strong> Bubble Team — Reg Lei, Jeffrey Sun, Cayden Li, Regan Yin, Jiale Guan<br>
    <strong>Event:</strong> UBC MBAn Hackathon 2026 &nbsp;|&nbsp;
    <strong>Client:</strong> Methanex Corporation<br>
    A full-stack analytics dashboard and LLM-powered AI Safety Analyst that turns 5 years of unstructured
    incident records into actionable prevention intelligence — now <strong>fully reproducible at zero cost</strong>
    on the free Ollama Cloud tier with a DSPy + GEPA-tuned prompt and graceful corpus-only fallback.
  </p>

  <p>
    <a href="https://github.com/Regan-Yin/Hackathon_Project_Incident_mining_Methanex" target="_blank" rel="noopener">
      View on GitHub &rarr;
    </a>
    &nbsp;|&nbsp;
    <a href="http://ilovemethanex.ca" target="_blank" rel="noopener">
      Live MVP Dashboard &rarr;
    </a>
  </p>

  <div class="toc section">
    <h3>Contents</h3>
    <a href="#executive-summary">Executive Summary</a>
    <a href="#stack">Tech Stack</a>
    <a href="#problem">Problem Statement</a>
    <a href="#v2-architecture">v2 Architecture (Apr 2026)</a>
    <a href="#v1-vs-v2">v1 vs v2 — Why We Migrated</a>
    <a href="#methodology">Step-by-Step Methodology</a>
    <a href="#clusters">NLP Clusters &amp; Early Warning</a>
    <a href="#ai-analyst">AI Safety Analyst (RAG + Cascading LLM)</a>
    <a href="#dspy-gepa">DSPy + GEPA Prompt Optimization</a>
    <a href="#dashboard">Dashboard Features</a>
    <a href="#code-highlights">Selected Code Highlights</a>
    <a href="#deploy">Cloud Run Deployment</a>
    <a href="#findings">Key Findings &amp; Recommendations</a>
    <a href="#run">How to Run Locally</a>
  </div>

  <!-- ======== EXECUTIVE SUMMARY ======== -->
  <div id="executive-summary" class="section">
    <h2>Executive Summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Dataset</div><div><strong>203 incidents · 1,659 actions</strong></div></div>
      <div class="card"><div class="muted">Timespan</div><div><strong>2019 – 2024</strong></div></div>
      <div class="card"><div class="muted">NLP Clusters</div><div><strong>7 risk scenarios</strong></div></div>
      <div class="card"><div class="muted">LLM Cascade</div><div><strong>4 free models</strong></div></div>
      <div class="card"><div class="muted">Cost to Reproduce</div><div><strong style="color:var(--good)">$0</strong></div></div>
      <div class="card"><div class="muted">Cold-start</div><div><strong>&lt; 5 s</strong> (TF-IDF in-memory)</div></div>
    </div>
    <p class="lead" style="margin-top:1rem">
      Methanex collects vast amounts of safety records, but they are reviewed case-by-case, making
      recurring patterns hard to spot. We built an end-to-end pipeline that clusters events via NLP,
      quantifies risk with an Early Warning Index, and deploys a Dash-based executive dashboard
      alongside a generative-AI advisor. <strong>v2 ships a complete re-architecture</strong>: TF-IDF
      retrieval + an Ollama Cloud LLM cascade with a DSPy + GEPA-tuned system instruction, all
      packaged into a Dockerized Cloud Run image that scales to zero.
    </p>
  </div>

  <!-- ======== TECH STACK ======== -->
  <div id="stack" class="section">
    <h2>Tech Stack</h2>
    <h4 style="margin:.6rem 0 .3rem;color:var(--accent)">Core (v2)</h4>
    <span class="badge">Python 3.11</span>
    <span class="badge">Dash</span>
    <span class="badge">Plotly</span>
    <span class="badge">Pandas / NumPy</span>
    <span class="badge">scikit-learn (TF-IDF)</span>
    <span class="badge">Ollama Cloud</span>
    <span class="badge">DSPy 2.6+</span>
    <span class="badge">GEPA 0.0.4+</span>
    <span class="badge">Gunicorn</span>
    <span class="badge">Docker</span>
    <span class="badge">Google Cloud Run</span>

    <h4 style="margin:1rem 0 .3rem;color:var(--accent)">LLM Cascade</h4>
    <span class="badge"><code>gpt-oss:20b-cloud</code></span>
    <span class="badge"><code>gemini-3-flash-preview:cloud</code></span>
    <span class="badge"><code>gpt-oss:120b-cloud</code></span>
    <span class="badge"><code>qwen3-coder:480b-cloud</code></span>

    <h4 style="margin:1rem 0 .3rem;color:var(--muted)">Legacy v1 (archived under <code>legacy_rag_engine/</code>)</h4>
    <span class="badge">Vertex AI</span>
    <span class="badge">Gemini 2.5 Flash</span>
    <span class="badge">Vector Search (Matching Engine)</span>
    <span class="badge">text-embedding-004</span>
    <span class="badge">Cloud Storage</span>
    <span class="badge">LangChain</span>
  </div>

  <!-- ======== PROBLEM ======== -->
  <div id="problem" class="section">
    <h2>Problem Statement</h2>
    <p>
      Safety records contain rich lessons, but reviewing them case-by-case makes recurring scenarios hard to
      spot and slows frontline guidance. Our challenge was to bridge the gap between raw, localized safety
      narratives and <em>systemic business intelligence</em>:
    </p>
    <ol>
      <li>Identify patterns and clusters of similar events (e.g., AI system failures, LOTO gaps, HR privacy exposures).</li>
      <li>Understand the factors driving higher severity (actual incidents) versus high-potential warnings (near-misses).</li>
      <li>Provide data-driven recommendations on where to focus prevention efforts and training.</li>
      <li>Let an investigator paste a hypothetical "what happened" snippet and immediately get a grounded,
          structured AI risk assessment with comparable historical cases.</li>
    </ol>
  </div>

  <!-- ======== v2 ARCHITECTURE ======== -->
  <div id="v2-architecture" class="section">
    <h2>v2 Architecture (Apr 2026)</h2>
    <p>
      The end-to-end pipeline is composed of four production-ready layers, all running locally in a single
      Dockerized Dash app:
    </p>

    <div class="pipeline">
      <div class="step"><strong>1. Dash UI &amp; Plotly visuals</strong> &mdash; <code>app.py</code> renders the executive dashboard, KPI tiles, cluster explorer, Early Warning module, and the AI Safety Analyst tab.</div>
      <div class="arrow">▼</div>
      <div class="step"><strong>2. Retrieval (TF-IDF)</strong> &mdash; <code>safety_analyst.retrieve_similar_events()</code> performs cosine similarity over an in-memory TF-IDF matrix (1–2 grams, sublinear TF, 20k features) built once at import time over the 2019–2024 events corpus. Top-<em>k</em> = 10.</div>
      <div class="arrow">▼</div>
      <div class="step"><strong>3. Prompt assembly</strong> &mdash; The retrieved cases are formatted into a compact <code>historical_context</code> block and fused with a strict-JSON schema hint plus the <strong>GEPA-tuned system instruction</strong> loaded from <code>dspy_gepa_best_config.json</code> at import.</div>
      <div class="arrow">▼</div>
      <div class="step"><strong>4. Cascading Ollama Cloud LLM call</strong> &mdash; <code>gpt-oss:20b-cloud</code> → <code>gemini-3-flash-preview:cloud</code> → <code>gpt-oss:120b-cloud</code> → <code>qwen3-coder:480b-cloud</code>. Each model is consulted only if the previous one timed out, returned empty content, produced unparseable JSON, or was missing too many schema keys.</div>
      <div class="arrow">▼</div>
      <div class="step"><strong>5. JSON sanitization &amp; gap-fill</strong> &mdash; The 6-key payload is normalized: labels coerced to canonical vocabularies, unicode bullets stripped, <code>suggested_actions</code> renumbered, <code>best_practices</code> rendered as a clean list. If 1–2 sections are missing, they are merged from the deterministic corpus fallback rather than discarding the LLM output.</div>
      <div class="arrow">▼</div>
      <div class="step"><strong>6. Markdown rendering</strong> &mdash; Final response is composed for the Dash typewriter effect, annotated with the model used and the average TF-IDF similarity of the retrieved cases.</div>
    </div>

    <div class="callout good">
      <strong>Reliability:</strong> If <em>every</em> cascade model fails, the deterministic corpus-only fallback
      composes a complete, well-formatted report directly from the top-5 similar cases (modal labels, deduped
      root causes, recorded actions, and lessons). The UI always renders something useful — annotated with
      <em>"LLM unavailable — response generated deterministically from the historical corpus."</em>
    </div>
  </div>

  <!-- ======== v1 vs v2 ======== -->
  <div id="v1-vs-v2" class="section">
    <h2>v1 vs v2 — Why We Migrated</h2>
    <p>
      The original Vertex AI / Gemini stack delivered great results during the hackathon but had a hard
      reproducibility cost: it required a billed GCP project, two long-running endpoints, and a service
      account key. v2 keeps the same public API (<code>analyze_new_event(text, events_df, k)</code>) so the
      Dash app needed only a one-line import swap, but the underlying engine is rebuilt around free,
      open-weight tooling.
    </p>

    <table>
      <thead>
        <tr><th>Concern</th><th><span class="v-tag-old">v1</span> Vertex AI / Gemini</th><th><span class="v-tag-new">v2</span> Ollama Cloud + DSPy/GEPA</th></tr>
      </thead>
      <tbody>
        <tr><td>Retrieval</td><td><code>MatchingEngineIndexEndpoint.find_neighbors()</code></td><td>Local TF-IDF on <code>events_clean.csv</code></td></tr>
        <tr><td>Embeddings</td><td><code>text-embedding-004</code> (Vertex, paid)</td><td>None — TF-IDF, $0</td></tr>
        <tr><td>LLM</td><td><code>gemini-2.5-flash</code> via <code>langchain_google_vertexai</code></td><td>Free-tier Ollama Cloud cascade</td></tr>
        <tr><td>Prompt</td><td>Hand-written</td><td>DSPy + GEPA reflective optimization</td></tr>
        <tr><td>Cold-start</td><td>30–45 min one-time GCP index build</td><td>&lt; 5 s in-memory TF-IDF build</td></tr>
        <tr><td>Cloud deploy</td><td>Vertex endpoints (always-on)</td><td>Cloud Run + Docker (scale-to-zero)</td></tr>
        <tr><td>Cost to reproduce</td><td>GCP project + billing + endpoint hosting</td><td><strong style="color:var(--good)">Zero</strong> — free Ollama key only</td></tr>
        <tr><td>Failure mode</td><td>Hard 5xx if GCP quota / billing fails</td><td>Cascading retry → deterministic corpus fallback</td></tr>
      </tbody>
    </table>

    <p style="margin-top:1rem">
      Anyone can now clone the repo, paste a free Ollama Cloud API key into <code>.env</code>, and run the
      dashboard locally <em>without GCP, billing accounts, or service-account keys</em>.
    </p>
  </div>

  <!-- ======== METHODOLOGY ======== -->
  <div id="methodology" class="section">
    <h2>Step-by-Step Methodology</h2>

    <h3>Step 1 — Data Ingestion &amp; Preprocessing</h3>
    <p>
      Raw, messy text narratives and structured fields were cleaned and standardized.
      Key temporal and categorical variables (<code>year</code>, <code>category_type</code>,
      <code>risk_level</code>, <code>severity</code>) were extracted to build a solid analytical
      foundation.
    </p>

    <h3>Step 2 — NLP Pattern Mining &amp; Clustering</h3>
    <p>
      Incident narratives (title + setting + what-happened + root-causes) were embedded and clustered
      to group events into 7 distinct, actionable "Risk Scenario" clusters. The mapping was saved as
      <code>case_cluster_map.csv</code> and is now consumed directly by the dashboard's filters.
    </p>

    <h3>Step 3 — Severity Driver Analysis &amp; Early Warning Index</h3>
    <p>
      Each cluster is mapped against the ratio of <strong>Incidents</strong> (realized harm) to
      <strong>Near-Misses</strong> (free lessons), and a composite Early Warning Index is computed:
    </p>
    <p style="text-align:center;font-style:italic;color:var(--accent)">
      EWI = (Near-miss rate) × (High-priority share within near-misses) × log(1 + n_cases)
    </p>
    <p>This prioritizes clusters where near-misses are frequent, serious, and occur at meaningful scale.</p>

    <h3>Step 4 — Generative AI Safety Analyst</h3>
    <p>
      A free-text input is TF-IDF retrieved against the corpus, fused into a strict-JSON RAG prompt,
      and sent through the Ollama Cloud cascade. The system instruction was tuned by DSPy + GEPA on a
      stratified eval set; missing schema sections are auto-filled from the deterministic corpus fallback.
    </p>

    <h3>Step 5 — Cloud Run Deployment</h3>
    <p>
      A slim Python 3.11 Dockerfile binds <code>gunicorn</code> to <code>$PORT</code> with 1 worker × 8
      threads and a 120s timeout. <code>.gcloudignore</code> excludes the legacy folder, dev artifacts,
      and the eval-cases dump so production images stay lean.
    </p>
  </div>

  <!-- ======== NLP CLUSTERS ======== -->
  <div id="clusters" class="section">
    <h2>NLP Clusters &amp; Early Warning</h2>
    <p>We grouped 203 events into <strong>7 clusters</strong> with searchable keywords:</p>

    <table>
      <thead>
        <tr><th>#</th><th>Cluster</th><th>Scenario</th><th>Primary Prevention Lever</th></tr>
      </thead>
      <tbody>
        <tr>
          <td>0</td><td><span class="cluster-tag">AI Monitoring / Decision-Support Errors</span></td>
          <td>AI alarms/recommendations mislead operations</td>
          <td>Human-in-the-loop verification + drift monitoring</td>
        </tr>
        <tr>
          <td>1</td><td><span class="cluster-tag">Stored Energy / LOTO Gaps</span></td>
          <td>Hydraulic/pneumatic stored energy during maintenance</td>
          <td>Multi-energy LOTO checklist + "try-actuate" verification</td>
        </tr>
        <tr>
          <td>2</td><td><span class="cluster-tag">Office Electrical / Ergonomics</span></td>
          <td>WFH/office safety: power bars, cords, trips, strains</td>
          <td>Basic office safety standards + housekeeping checklist</td>
        </tr>
        <tr>
          <td>3</td><td><span class="cluster-tag">Line Work / Piping Containment</span></td>
          <td>Pipes/valves not fully depressurized → release</td>
          <td>Standard line-break procedure + pressure confirmation</td>
        </tr>
        <tr>
          <td>4</td><td><span class="cluster-tag">Field Safety: Height / Confined Space</span></td>
          <td>Elevated work or confined space, often contractor tasks</td>
          <td>Permit-to-work discipline + contractor supervision</td>
        </tr>
        <tr>
          <td>5</td><td><span class="cluster-tag">Cyber-Physical Control Disruption</span></td>
          <td>Unauthorized access affects controls → process deviation</td>
          <td>Access hardening + segmentation + two-person rule</td>
        </tr>
        <tr>
          <td>6</td><td><span class="cluster-tag">HR / Privacy Exposure</span></td>
          <td>Sensitive HR info exposed (overheard calls, visible screens)</td>
          <td>Privacy-by-default + secure sharing rules</td>
        </tr>
      </tbody>
    </table>

    <h3 style="margin-top:1.5rem">Priority Scoring</h3>
    <p>Each event combines a risk-level score and a severity score:</p>
    <div class="grid-2">
      <div class="arch-box">
        <h4>Risk Level Encoding</h4>
        <ul><li>High = 2</li><li>Medium = 1</li><li>Low = 0</li></ul>
      </div>
      <div class="arch-box">
        <h4>Severity Encoding</h4>
        <ul><li>Serious / Major = 3</li><li>Potentially Significant = 2</li><li>Minor / Near Miss = 1</li></ul>
      </div>
    </div>
    <p>
      <strong>Priority = Risk + Severity</strong> (Low: 0–2, Medium: 2–4, High: ≥4).
      The Early Warning Index then aggregates across clusters to rank the most urgent areas of focus.
    </p>
  </div>

  <!-- ======== AI SAFETY ANALYST ======== -->
  <div id="ai-analyst" class="section">
    <h2>AI Safety Analyst (RAG + Cascading LLM)</h2>
    <p>
      The AI tab lets frontline users describe a situation in plain language and receive instant,
      evidence-based analysis. The pipeline is a TF-IDF RAG followed by a fault-tolerant LLM cascade.
    </p>

    <h3>Free-tier Ollama Cloud cascade</h3>
    <div class="arch-box">
      <div class="model-row">
        <code>gpt-oss:20b-cloud</code>
        <span>Primary — clean 6-key JSON, deterministic, lowest latency.</span>
        <span class="pill-good">~5 s</span>
      </div>
      <div class="model-row">
        <code>gemini-3-flash-preview:cloud</code>
        <span>Fallback #1 — usually clean; occasional truncation.</span>
        <span class="pill-good">~9 s</span>
      </div>
      <div class="model-row">
        <code>gpt-oss:120b-cloud</code>
        <span>Fallback #2 — big reasoning, content + thinking both populated.</span>
        <span class="pill-good">~9 s</span>
      </div>
      <div class="model-row">
        <code>qwen3-coder:480b-cloud</code>
        <span>Fallback #3 — very high quality, slow.</span>
        <span class="pill-warn">~80 s</span>
      </div>
    </div>
    <p class="muted" style="font-size:.9rem">
      Each model is consulted only if the previous one raised, returned empty content, or produced
      unparseable / heavily-incomplete JSON. The lineup is overridable via <code>OLLAMA_MODEL</code> and
      <code>OLLAMA_FALLBACK_MODELS</code>.
    </p>

    <h3>Strict JSON output contract</h3>
    <p>The model is constrained to emit exactly six keys, each normalized post-hoc by <code>safety_analyst.py</code>:</p>
    <table>
      <thead><tr><th>Key</th><th>Domain / Format</th></tr></thead>
      <tbody>
        <tr><td><code>risk_level</code></td><td>One of <code>Low</code>, <code>Medium</code>, <code>High</code></td></tr>
        <tr><td><code>severity</code></td><td>One of <code>Minor</code>, <code>Potentially Significant</code>, <code>Serious</code>, <code>Major</code>, <code>Near Miss</code></td></tr>
        <tr><td><code>category_type</code></td><td>One of <code>Incident</code>, <code>Near Miss</code>, <code>Other</code></td></tr>
        <tr><td><code>root_cause</code></td><td>2–4 sentence paragraph grounded in the retrieved cases</td></tr>
        <tr><td><code>suggested_actions</code></td><td>3–5 numbered actions, each <code>"N. &lt;sentence&gt;. Owner: &lt;role&gt;. Timing: &lt;Immediate / &lt;30 days / 30-90 days / &gt;90 days&gt;. Verification: &lt;text&gt;."</code></td></tr>
        <tr><td><code>best_practices</code></td><td>2–3 short lessons drawn from the corpus</td></tr>
      </tbody>
    </table>

    <div class="callout">
      <strong>Reasoning-model quirk handled:</strong> <code>gpt-oss:120b</code> often returns
      <code>message.content == ""</code> when <code>format="json"</code> is forced and instead places
      the JSON object inside <code>message.thinking</code>. The engine reads both fields and picks the
      one that actually contains a JSON object, instead of failing and falling through.
    </div>
  </div>

  <!-- ======== DSPy + GEPA ======== -->
  <div id="dspy-gepa" class="section">
    <h2>DSPy + GEPA Prompt Optimization</h2>
    <p>
      The system instruction shipped in <code>dspy_gepa_best_config.json</code> was produced by
      <code>dspy_gepa_benchmark.py</code> — a self-contained driver that tunes the prompt against the
      <em>actual</em> analyst pipeline (TF-IDF + Ollama). The flow:
    </p>
    <ol>
      <li>Build a <strong>stratified eval set</strong> from <code>events_clean.csv</code> (5 input styles ×
          3 categories): keywords, title, snippet, mini-report, full report.</li>
      <li><strong>Sweep four hand-authored prompt styles</strong> (<code>balanced</code>,
          <code>strict_format</code>, <code>evidence_grounded</code>, <code>operational</code>) against the
          live analyzer pipeline and pick the best.</li>
      <li>Wrap a <code>dspy.ChainOfThought</code> module around the strict-JSON signature.</li>
      <li>Run <code>dspy.GEPA</code> with a high-temperature reflection LM and a structured metric that
          scores label exactness, action structure, root-cause grounding, length, and best-practices quality.</li>
      <li>Persist the winning system instruction. The next <code>python app.py</code> picks it up automatically.</li>
    </ol>

    <h3>Composite metric (used both as the GEPA objective and for native scoring)</h3>
    <p style="text-align:center;font-style:italic;color:var(--accent)">
      score = 0.22·risk + 0.20·severity + 0.16·category + 0.16·root_cause + 0.18·actions + 0.08·best_practices
    </p>
    <ul>
      <li><strong>Label scores</strong> are exact-match with ordinal partial credit (severity tiers earn
          credit for adjacent buckets).</li>
      <li><strong>Root cause</strong> is jointly scored on length [80–600 chars] and token grounding against
          the gold <code>root_causes</code> + <code>lessons</code> columns.</li>
      <li><strong>Action structure</strong> rewards numbered formatting plus the presence of
          <em>Owner / Timing / Verification</em> markers.</li>
    </ul>

    <h3>The "winner" — <code>operational</code> style</h3>
    <p>
      After the sweep + GEPA reflection, the <code>operational</code> prompt style won.
      <code>dspy_gepa_best_config.json</code> contains the resulting instruction with explicit
      decision policy, output contract, formatting rules, and anti-pattern guards (e.g.,
      <em>no unicode bullets, no marketing filler, root cause must identify the underlying factor
      not restate the incident</em>).
    </p>

    <h3>Re-tuning</h3>
    <div class="code"><pre><code class="language-bash"># Quickest sanity check (~5 min on free-tier Ollama Cloud)
python dspy_gepa_benchmark.py --num-cases 24 --auto light

# Better quality (~20-30 min)
python dspy_gepa_benchmark.py --num-cases 36 --auto medium

# Just dump the eval cases without running GEPA
python dspy_gepa_benchmark.py --prepare-only</code></pre></div>
  </div>

  <!-- ======== DASHBOARD FEATURES ======== -->
  <div id="dashboard" class="section">
    <h2>Dashboard Features</h2>
    <p>
      The Dash application (<code>app.py</code>, ~860 lines) delivers a production-quality
      executive dashboard with three main tabs:
    </p>

    <h3>Tab 1 — Performance Dashboard</h3>
    <ul>
      <li><strong>Animated KPI tiles</strong> (total cases, incident volume, near-miss conversion, high-risk %, severe cases) with client-side JavaScript counter animations.</li>
      <li><strong>Overview sub-tab:</strong> bar charts by category type and risk level; line chart over time; stacked year breakdown; top primary classifications; filterable data table with CSV export.</li>
      <li><strong>Clusters sub-tab:</strong> case-count ranking, per-cluster drilldown with donut chart, AI-extracted top terms &amp; example incidents, ESG performance metrics, root-cause &amp; corrective-action themes.</li>
      <li><strong>Early Warning Dashboard:</strong> ranked EWI bar chart, counts heatmap (incidents / near-misses / high-priority), rates heatmap (near-miss rate, HP within NM, HP within Inc).</li>
    </ul>

    <h3>Tab 2 — Event Intelligence</h3>
    <ul>
      <li>Sortable, filterable data portal with native search and CSV export for all historical events.</li>
    </ul>

    <h3>Tab 3 — AI Safety Analyst</h3>
    <ul>
      <li>Free-text input for describing a hypothetical hazard scenario.</li>
      <li>Cascading LLM analysis with typewriter animation and source-event transparency.</li>
      <li>Expandable top-10 similar events table with individual CSV export.</li>
      <li>Response is annotated with the model used and the average TF-IDF similarity of the retrieved cases.</li>
    </ul>

    <h3>Global Filters</h3>
    <ul>
      <li><strong>Year range slider</strong> (2019–2024)</li>
      <li><strong>Cluster dropdown</strong> (multi-select)</li>
      <li><strong>High-risk-only toggle</strong></li>
    </ul>
  </div>

  <!-- ======== CODE HIGHLIGHTS ======== -->
  <div id="code-highlights" class="section">
    <h2>Selected Code Highlights</h2>

    <h3>TF-IDF retrieval (replaces Vertex Vector Search)</h3>
    <div class="code"><pre><code class="language-python">def _build_tfidf(df):
    corpus = [_row_to_doc(r) for _, r in df.iterrows()]
    vec = TfidfVectorizer(
        stop_words="english",
        ngram_range=(1, 2),
        max_df=0.95,
        min_df=1,
        sublinear_tf=True,
        max_features=20000,
    )
    return vec, vec.fit_transform(corpus)

VECTORIZER, EVENT_MATRIX = _build_tfidf(EVENTS_DF)

def retrieve_similar_events(query, k=10):
    qvec = VECTORIZER.transform([query])
    sims = cosine_similarity(qvec, EVENT_MATRIX).ravel()
    idx = np.argsort(sims)[::-1][:k]
    out = EVENTS_DF.iloc[idx].copy()
    out["similarity"] = np.round(sims[idx], 4)
    return out.reset_index(drop=True)</code></pre></div>

    <h3>Cascading Ollama Cloud call with thinking-channel fallback</h3>
    <div class="code"><pre><code class="language-python">def _ollama_chat(prompt, system, model=None):
    """Reasoning models (gpt-oss:120b) often emit empty `content` when
    format='json' is forced and put the JSON inside `thinking`. Read both
    and prefer the channel that actually contains a JSON object."""
    client = Client(host=OLLAMA_API_BASE,
                    headers={"Authorization": f"Bearer {OLLAMA_API_KEY}"},
                    timeout=LLM_TIMEOUT_S)
    response = client.chat(
        model=model or OLLAMA_MODEL,
        messages=[{"role": "system", "content": system},
                  {"role": "user",   "content": prompt}],
        format="json",
        options={"temperature": 0.2, "num_predict": 2500},
    )
    content  = (response.message.content  or "").strip()
    thinking = (response.message.thinking or "").strip()
    if not content and thinking:                     return thinking
    if content and "{" not in content and "{" in thinking:  return thinking
    return content</code></pre></div>

    <h3>Cascading retry + corpus gap-fill</h3>
    <div class="code"><pre><code class="language-python">candidate_models = [OLLAMA_MODEL, *OLLAMA_FALLBACK_MODELS]
payload, used_model, merged_fields = None, None, []

for model in candidate_models:
    try:
        normalized, _ = _try_llm(prompt, model)
        missing = [f for f in _REQUIRED_LLM_FIELDS if not normalized.get(f)]
        if len(missing) > MAX_MISSING_FIELDS_BEFORE_FULL_FALLBACK:
            raise RuntimeError(f"missing too many sections: {missing}")
        if missing:                                  # 1-2 missing -> merge
            fb = fallback_response(top_k)
            for fld in missing: normalized[fld] = fb[fld]
            merged_fields = missing
        payload, used_model = normalized, model
        break
    except Exception as exc:
        log.warning("%s failed: %s", model, exc); continue

if payload is None:                                  # every model died
    payload = fallback_response(top_k)               # deterministic corpus-only</code></pre></div>

    <h3>DSPy signature for GEPA optimization</h3>
    <div class="code"><pre><code class="language-python">class AnalyzeSafetyEvent(dspy.Signature):
    """Methanex EPSSC safety analyst: predict labels and write a structured
    report grounded in retrieved historical cases. Strict-JSON output."""

    incident_input:     str = dspy.InputField(desc="User report (keywords / snippet / full).")
    historical_context: str = dspy.InputField(desc="TF-IDF retrieved similar cases.")
    style_guide:        str = dspy.InputField(desc="Stylistic guidance for the response.")

    risk_level:        str = dspy.OutputField(desc='"Low" | "Medium" | "High".')
    severity:          str = dspy.OutputField(desc='"Minor" | "Potentially Significant" | "Serious" | "Major" | "Near Miss".')
    category_type:     str = dspy.OutputField(desc='"Incident" | "Near Miss" | "Other".')
    root_cause:        str = dspy.OutputField(desc="2-4 sentences grounded in historical context.")
    suggested_actions: str = dspy.OutputField(desc="3-5 numbered actions w/ Owner / Timing / Verification.")
    best_practices:    str = dspy.OutputField(desc="2-3 short bullet lessons from the corpus.")</code></pre></div>

    <h3>Composite GEPA metric with structured feedback</h3>
    <div class="code"><pre><code class="language-python">def metric_from_payload(case, payload):
    risk = _label_score(payload["risk_level"], case.gold_risk, VALID_RISK)
    sev  = _label_score(payload["severity"],   case.gold_severity, VALID_SEVERITY)
    cat  = _label_score(payload["category_type"], case.gold_category, VALID_CATEGORY)
    rc   = 0.5*_length_score(payload["root_cause"], 80, 600) \
         + 0.5*_grounding_score(payload["root_cause"],
                                case.gold_root_cause, case.gold_lessons)
    act  = _action_score(payload["suggested_actions"])
    bp   = 0.6*_length_score(payload["best_practices"], 50, 480) \
         + 0.4*_grounding_score(payload["best_practices"], "", case.gold_lessons)

    final = 0.22*risk + 0.20*sev + 0.16*cat + 0.16*rc + 0.18*act + 0.08*bp
    feedback = (f"risk={risk:.2f}, sev={sev:.2f}, cat={cat:.2f}, "
                f"rc_ground={rc:.2f}, action_struct={act:.2f}, bp={bp:.2f}. "
                "Match risk/severity/category EXACTLY. Each action MUST contain "
                "Owner, Timing, AND Verification. Ground root cause in retrieved cases.")
    return final, feedback</code></pre></div>
  </div>

  <!-- ======== CLOUD RUN ======== -->
  <div id="deploy" class="section">
    <h2>Cloud Run Deployment</h2>
    <p>
      A slim Python 3.11 image binds <code>gunicorn</code> to <code>$PORT</code> with 1 worker × 8 threads
      and a 120s timeout. The Ollama key is wired in via Secret Manager so no credentials live in the image:
    </p>
    <div class="code"><pre><code class="language-bash">PROJECT_ID=your-gcp-project
REGION=us-west1

# 1. Build &amp; push to Artifact Registry
gcloud builds submit \
  --tag $REGION-docker.pkg.dev/$PROJECT_ID/methanex/epssc-dashboard:latest

# 2. Stash the Ollama key in Secret Manager
gcloud secrets create OLLAMA_API_KEY --data-file=- &lt;&lt;&lt; "&lt;paste-your-key&gt;"

# 3. Deploy with the secret mounted as an env var
gcloud run deploy methanex-epssc \
  --image $REGION-docker.pkg.dev/$PROJECT_ID/methanex/epssc-dashboard:latest \
  --region $REGION \
  --allow-unauthenticated \
  --update-secrets OLLAMA_API_KEY=OLLAMA_API_KEY:latest \
  --memory 1Gi --cpu 1 --concurrency 40 --timeout 180</code></pre></div>

    <p class="muted" style="font-size:.92rem">
      <code>.gcloudignore</code> excludes the entire <code>legacy_rag_engine/</code> folder, local
      <code>.env</code> files, caches, virtualenvs, notebooks, and the dev-only
      <code>dspy_gepa_eval_cases.json</code> so production uploads stay lean.
    </p>
  </div>

  <!-- ======== FINDINGS ======== -->
  <div id="findings" class="section">
    <h2>Key Findings &amp; Recommendations</h2>
    <ul>
      <li><strong>Focus on dominant clusters:</strong> The Pareto module shows which operational clusters
          account for the highest volume of reports and highest combined Risk × Severity priority.</li>
      <li><strong>Target high-severity ratios:</strong> Clusters with a high <em>Incident-to-Near-Miss</em>
          conversion rate (e.g., AI Monitoring &amp; Decision-Support Errors in 2024) are vulnerabilities
          where current defenses are frequently failing — those should be the top investment areas.</li>
      <li><strong>Proactive monitoring:</strong> The timeline module surfaces emerging risks (e.g., a 2024
          spike in IT/AI-related exposures) before they become systemic hazards.</li>
      <li><strong>Grounded triage at the desk:</strong> The Generative AI Safety Analyst gives any
          investigator a structured, corpus-grounded triage of a free-text incident in seconds — including
          the top-10 most similar historical events for cross-reference.</li>
      <li><strong>Resilience built-in:</strong> The cascading LLM + deterministic corpus fallback means the
          dashboard is never silently broken — every response is annotated with its source.</li>
    </ul>
  </div>

  <!-- ======== HOW TO RUN ======== -->
  <div id="run" class="section">
    <h2>How to Run Locally</h2>

    <h3>Repository Structure</h3>
    <div class="code"><pre><code>methanex-safety-intelligence/
│
├── app.py                          # Dash dashboard (UI, KPIs, AI Analyst tab)
├── safety_analyst.py               # NEW v2 — TF-IDF + Ollama Cloud RAG engine
├── dspy_gepa_benchmark.py          # NEW v2 — DSPy + GEPA prompt-optimization driver
├── dspy_gepa_best_config.json      # NEW v2 — persisted GEPA-tuned system instruction
├── dspy_gepa_eval_cases.json       # NEW v2 — stratified eval cases (reproducibility)
│
├── Dockerfile                      # NEW v2 — Cloud Run production image
├── .gcloudignore                   # NEW v2 — excludes legacy / dev files from deploy
├── .env.example                    # Updated — Ollama Cloud + optional legacy vars
├── requirements.txt                # Updated — Ollama, DSPy, GEPA, gunicorn
│
├── data/
│   ├── events_clean.csv            # Cleaned 2019-2024 event corpus
│   ├── actions_clean.csv           # Cleaned recommended actions
│   ├── case_cluster_map.csv        # NLP-generated cluster mappings
│   ├── case_priority_scores.csv
│   ├── cluster_profile_sorted.csv
│   ├── cluster_summary_with_terms_examples.csv
│   └── near_miss_early_warning_dashboard.csv
│
├── assets/
│   ├── style.css                   # Methanex corporate CSS
│   ├── logo.svg
│   └── favicon.ico
│
├── legacy_rag_engine/              # ARCHIVED — Vertex AI / Gemini v1 stack
│   ├── README.md                   # Why this folder exists + how to re-enable
│   ├── rag_engine.py               # Original Vertex Vector Search RAG
│   ├── setup_cloud.py              # One-time GCP index/endpoint bootstrap
│   ├── data_processing.py          # Historical KPI helper (no longer imported)
│   └── gcp-key.json                # Template service-account JSON
│
├── LICENSE
└── README.md</code></pre></div>

    <h3>Three commands — zero GCP required</h3>
    <div class="code"><pre><code class="language-bash">git clone https://github.com/Regan-Yin/Hackathon_Project_Incident_mining_Methanex.git
cd Hackathon_Project_Incident_mining_Methanex

python3.11 -m venv .venv &amp;&amp; source .venv/bin/activate
pip install -r requirements.txt

# Get a free Ollama Cloud key at https://ollama.com/settings/keys
cp .env.example .env
# Paste your key into OLLAMA_API_KEY=...

python app.py
# → http://127.0.0.1:8050/</code></pre></div>

    <p>
      Open the <strong>Generative AI Safety Analyst</strong> tab, paste any short snippet (e.g.,
      <em>"Operator slipped near unsealed valve during night shift"</em>), and within ~5–10 s you'll see
      a predicted <strong>Risk / Severity / Category</strong>, a grounded <strong>Root Cause</strong>
      paragraph, 3–5 structured <strong>Suggested Actions</strong>, 2–3 corpus-derived
      <strong>Best Practices</strong>, and the <strong>Top 10 Similar Historical Events</strong> table.
    </p>

    <div class="callout warn">
      If the LLM is unreachable, the same UI still renders — the deterministic corpus-only fallback fills
      every section and the response is annotated <em>"LLM unavailable — response generated
      deterministically from the historical corpus."</em>
    </div>
  </div>

</div>
