---
layout: page
title: "Safety Incident & Near-Miss Pattern Mining — Methanex Hackathon"
description: NLP/Clustering/Google Cloud (Vertex AI)/RAG/Gemini/Dash/Plotly/Full-Stack Dashboard
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
  }
  [data-theme="dark"]{
    --card-bg:#0f172a; --card-border:#233047; --muted:#94a3b8;
    --badge-bg:rgba(255,255,255,.08); --badge-border:rgba(255,255,255,.12);
  }

  .wrap{max-width:1100px;margin:0 auto;padding:0 0 1rem}
  .section{margin:2.2rem 0;contain:content;position:relative}
  .lead{font-size:1.05rem;line-height:1.7}
  .muted{color:var(--muted)}
  .badge{display:inline-block;padding:.35rem .6rem;border-radius:2rem;background:var(--badge-bg);border:1px solid var(--badge-border);margin:.15rem .2rem;font-size:.85rem;color:var(--global-text-color)}
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
  th,td{padding:.6rem .65rem;border-bottom:1px solid var(--card-border)}
  th{text-align:left}
  .toc a{display:block;padding:.2rem 0}
  .arch-box{background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:1.2rem;margin:.75rem 0;box-shadow:0 2px 12px rgba(0,0,0,.04)}
  .arch-box h4{margin:0 0 .5rem;color:var(--accent)}
  .arch-row{display:flex;gap:1rem;flex-wrap:wrap}
  .arch-row .arch-box{flex:1 1 200px}
  .cluster-tag{display:inline-block;padding:.3rem .55rem;border-radius:.4rem;background:#002C77;color:#fff;font-size:.82rem;margin:.2rem}
</style>

<div class="wrap">
  <p class="lead">
    <strong>Author:</strong> Regan Yin &nbsp;|&nbsp;
    <strong>Team:</strong> Bubble Team — Reg Lei, Jeffrey Sun, Cayden Li, Regan Yin, Jiale Guan<br>
    <strong>Event:</strong> UBC MBAn Hackathon 2026 &nbsp;|&nbsp;
    <strong>Client:</strong> Methanex Corporation<br>
    A full-stack analytics dashboard and RAG-powered AI Safety Analyst that transforms 5 years of
    unstructured incident records into actionable prevention intelligence.
  </p>

  <p>
    <a href="https://github.com/Regan-Yin/Hackathon_Project_Incident_mining_Methanex" target="_blank" rel="noopener">
      View on GitHub &rarr;
    </a>
  </p>

  <div class="toc section">
    <h3>Contents</h3>
    <a href="#executive-summary">Executive Summary</a>
    <a href="#stack">Tech Stack</a>
    <a href="#problem">Problem Statement</a>
    <a href="#methodology">Step-by-Step Methodology</a>
    <a href="#architecture">Technical Architecture</a>
    <a href="#clusters">NLP Clusters &amp; Early Warning</a>
    <a href="#ai-analyst">AI Safety Analyst (RAG + Gemini)</a>
    <a href="#dashboard">Dashboard Features</a>
    <a href="#code-highlights">Selected Code Highlights</a>
    <a href="#findings">Key Findings &amp; Recommendations</a>
    <a href="#run">How to Run Locally</a>
  </div>

  <!-- ======== EXECUTIVE SUMMARY ======== -->
  <div id="executive-summary" class="section">
    <h2>Executive Summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Dataset</div><div><strong>203 incidents &middot; 1,659 actions</strong></div></div>
      <div class="card"><div class="muted">Timespan</div><div><strong>2019 &ndash; 2024</strong></div></div>
      <div class="card"><div class="muted">Locations</div><div><strong>10+ sites</strong></div></div>
      <div class="card"><div class="muted">NLP Clusters</div><div><strong>7 risk scenarios</strong></div></div>
      <div class="card"><div class="muted">AI Model</div><div><strong>Gemini 2.5 Flash</strong></div></div>
    </div>
    <p class="lead" style="margin-top:1rem">
      Methanex collects vast amounts of safety records, but they are reviewed case-by-case, making
      recurring patterns hard to spot. We built an end-to-end pipeline that clusters events via NLP,
      quantifies risk with an Early Warning Index, and deploys a Dash-based executive dashboard
      alongside a Generative-AI advisor that retrieves similar historical incidents in real time.
    </p>
  </div>

  <!-- ======== TECH STACK ======== -->
  <div id="stack" class="section">
    <h2>Tech Stack</h2>
    <span class="badge">Python</span>
    <span class="badge">Dash</span>
    <span class="badge">Plotly</span>
    <span class="badge">Pandas / NumPy</span>
    <span class="badge">Google Cloud Platform</span>
    <span class="badge">Vertex AI</span>
    <span class="badge">Gemini 2.5 Flash</span>
    <span class="badge">Vector Search (Matching Engine)</span>
    <span class="badge">Text Embeddings (text-embedding-004)</span>
    <span class="badge">Cloud Storage</span>
    <span class="badge">LangChain</span>
    <span class="badge">NLP / Clustering</span>
    <span class="badge">RAG</span>
    <span class="badge">CSS (Custom Corporate Theme)</span>
  </div>

  <!-- ======== PROBLEM STATEMENT ======== -->
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
    </ol>
  </div>

  <!-- ======== METHODOLOGY ======== -->
  <div id="methodology" class="section">
    <h2>Step-by-Step Methodology</h2>

    <h3>Step 1 &mdash; Data Ingestion &amp; Preprocessing</h3>
    <p>
      Raw, messy text narratives and structured fields were cleaned and standardized.
      Key temporal and categorical variables (<code>year</code>, <code>category_type</code>,
      <code>risk_level</code>, <code>severity</code>) were extracted to build a solid analytical
      foundation.
    </p>

    <h3>Step 2 &mdash; NLP Pattern Mining &amp; Clustering</h3>
    <p>
      Using <strong>Vertex AI text-embedding-004</strong>, we converted incident narratives
      (title + setting + what happened + root causes) into high-dimensional vectors, then applied
      clustering to group events into 7 distinct, actionable "Risk Scenario" clusters.
      The mapping was saved as <code>case_cluster_map.csv</code>.
    </p>

    <h3>Step 3 &mdash; Severity Driver Analysis</h3>
    <p>
      We mapped each cluster against the ratio of <strong>Incidents</strong> (realized harm)
      to <strong>Near-Misses</strong> (free lessons). This allowed us to statistically identify which
      operational areas are high-potential risks that bypass current safety barriers.
    </p>
    <p>
      A composite <strong>Early Warning Index</strong> was formulated:
    </p>
    <p style="text-align:center;font-style:italic;color:var(--accent)">
      EWI = (Near-miss rate) &times; (High-priority share within near-misses) &times; log(1 + n_cases)
    </p>
    <p>
      This prioritizes clusters where near-misses are frequent, serious, and occur at meaningful scale.
    </p>

    <h3>Step 4 &mdash; Full-Stack MVP Deployment</h3>
    <p>
      We elevated localized Python scripts into a live MVP using <strong>Dash + Plotly</strong>
      with a custom Methanex corporate CSS theme and deployed it to the web so stakeholders could
      dynamically explore trends and drill into data themselves.
    </p>
  </div>

  <!-- ======== ARCHITECTURE ======== -->
  <div id="architecture" class="section">
    <h2>Technical Architecture</h2>
    <p>A modular design supports both the dashboard and the AI advisor while maintaining strong governance.</p>

    <div class="arch-row">
      <div class="arch-box">
        <h4>Data Sources</h4>
        <ul>
          <li>500+ pages incident records in PDF</li>
          <li>Cleaned CSVs: <code>events_clean.csv</code>, <code>actions_clean.csv</code></li>
          <li>NLP cluster map: <code>case_cluster_map.csv</code></li>
        </ul>
      </div>
      <div class="arch-box">
        <h4>Processing</h4>
        <ul>
          <li>Text extraction &amp; structuring</li>
          <li>Vertex AI embeddings (text-embedding-004)</li>
          <li>Clustering &amp; metrics/KPIs</li>
          <li>Trend &amp; driver analysis</li>
        </ul>
      </div>
      <div class="arch-box">
        <h4>Analytics Layer</h4>
        <ul>
          <li>NLP pattern mining</li>
          <li>Early Warning Index</li>
          <li>Priority scoring (Risk + Severity)</li>
          <li>Evidence-based GenAI workflow</li>
        </ul>
      </div>
      <div class="arch-box">
        <h4>Experiences</h4>
        <ul>
          <li>Executive dashboard (KPI tiles, charts, heatmaps)</li>
          <li>Interactive cluster explorer</li>
          <li>GenAI Safety Analyst (RAG)</li>
          <li>CSV export &amp; data portal</li>
        </ul>
      </div>
    </div>

    <div class="arch-box" style="margin-top:1rem">
      <h4>Governance &amp; Controls</h4>
      <div style="display:flex;gap:1.5rem;flex-wrap:wrap;font-size:.92rem">
        <span>Role-based access</span>
        <span>PII redaction</span>
        <span>Human curation of &ldquo;gold&rdquo; guidance</span>
        <span>Audit trails</span>
        <span>Model monitoring (drift + quality)</span>
      </div>
    </div>
  </div>

  <!-- ======== NLP CLUSTERS ======== -->
  <div id="clusters" class="section">
    <h2>NLP Clusters &amp; Early Warning</h2>
    <p>
      We grouped 203 events using narrative text into <strong>7 clusters</strong> with searchable keywords:
    </p>

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
          <td>Multi-energy LOTO checklist + &ldquo;try-actuate&rdquo; verification</td>
        </tr>
        <tr>
          <td>2</td><td><span class="cluster-tag">Office Electrical / Ergonomics</span></td>
          <td>WFH/office safety: power bars, cords, trips, strains</td>
          <td>Basic office safety standards + housekeeping checklist</td>
        </tr>
        <tr>
          <td>3</td><td><span class="cluster-tag">Line Work / Piping Containment</span></td>
          <td>Pipes/valves not fully depressurized &rarr; release</td>
          <td>Standard line-break procedure + pressure confirmation</td>
        </tr>
        <tr>
          <td>4</td><td><span class="cluster-tag">Field Safety: Height / Confined Space</span></td>
          <td>Elevated work or confined space, often contractor tasks</td>
          <td>Permit-to-work discipline + contractor supervision</td>
        </tr>
        <tr>
          <td>5</td><td><span class="cluster-tag">Cyber-Physical Control Disruption</span></td>
          <td>Unauthorized access affects controls &rarr; process deviation</td>
          <td>Access hardening + segmentation + two-person rule</td>
        </tr>
        <tr>
          <td>6</td><td><span class="cluster-tag">HR / Privacy Exposure</span></td>
          <td>Sensitive HR info exposed (overheard calls, visible screens)</td>
          <td>Privacy-by-default + secure sharing rules</td>
        </tr>
      </tbody>
    </table>

    <h3 style="margin-top:1.5rem">Priority &amp; Early Warning Scoring</h3>
    <p>Each event is scored by combining risk level and severity:</p>
    <div class="grid-2">
      <div class="arch-box">
        <h4>Risk Level Encoding</h4>
        <ul><li>High = 2</li><li>Medium = 1</li><li>Low = 0</li></ul>
      </div>
      <div class="arch-box">
        <h4>Severity Encoding</h4>
        <ul><li>Serious / Major = 3</li><li>Potentially Significant = 2</li><li>Minor = 1</li></ul>
      </div>
    </div>
    <p>
      <strong>Priority = Risk + Severity</strong> (Low: 0–2, Medium: 2–4, High: &ge;4).
      The Early Warning Index then aggregates across clusters to rank the most urgent areas of focus.
    </p>
  </div>

  <!-- ======== AI SAFETY ANALYST ======== -->
  <div id="ai-analyst" class="section">
    <h2>AI Safety Analyst (RAG + Gemini)</h2>
    <p>
      The AI tab lets frontline users describe a situation in plain language and receive
      instant, evidence-based analysis. The pipeline works as follows:
    </p>
    <ol>
      <li><strong>Embed user query</strong> using Vertex AI <code>text-embedding-004</code>.</li>
      <li><strong>Vector Search</strong> via GCP Matching Engine retrieves the top 10 most similar
          historical incidents from the indexed corpus.</li>
      <li><strong>Gemini 2.5 Flash</strong> generates a structured analysis
          (predicted risk/severity, root cause, suggested actions) using the retrieved context.</li>
      <li>Results are displayed with a <strong>typewriter animation</strong> and an expandable table of
          the 10 source events for transparency.</li>
    </ol>

    <div class="code"><pre><code class="language-python">def analyze_new_event(hypothesis_text, events_df):
    """Finds Top 10 similar events via GCP Vector Search and generates analysis."""
    embeddings_model = TextEmbeddingModel.from_pretrained("text-embedding-004")
    query_vector = embeddings_model.get_embeddings([hypothesis_text])[0].values

    endpoint = aiplatform.MatchingEngineIndexEndpoint(index_endpoint_name=ENDPOINT_ID)
    response = endpoint.find_neighbors(
        deployed_index_id=DEPLOYED_INDEX_ID,
        queries=[query_vector],
        num_neighbors=10
    )

    top_10_ids = [neighbor.id for neighbor in response[0]]
    top_10_events = events_df[events_df['event_id'].isin(top_10_ids)]

    context = "TOP 10 HISTORICAL METHANEX EVENTS:\n\n"
    for idx, (_, row) in enumerate(top_10_events.iterrows(), 1):
        context += f"Event {idx}:\n"
        for col in top_10_events.columns:
            value = row[col]
            if pd.notna(value):
                context += f"  {col}: {value}\n"
        context += "\n"

    prompt = f"""You are an expert Process Safety Engineer for Methanex EPSSC.
    Analyze the following hypothetical incident/near-miss report based strictly
    on the historical events provided.

    Hypothetical Event Input:
    {hypothesis_text}

    {context}

    Provide your analysis STRICTLY in the following format:
    ### Predicted Risk Level & Severity
    ### Potential Root Cause
    ### Suggested Actions
    """

    llm = ChatVertexAI(model_name="gemini-2.5-flash", temperature=0.2)
    ai_response = llm.invoke(prompt)
    return ai_response.content, top_10_events</code></pre></div>
  </div>

  <!-- ======== DASHBOARD FEATURES ======== -->
  <div id="dashboard" class="section">
    <h2>Dashboard Features</h2>
    <p>
      The Dash application (<code>app.py</code>, ~860 lines) delivers a production-quality
      executive dashboard with three main tabs:
    </p>

    <h3>Tab 1 &mdash; Performance Dashboard</h3>
    <ul>
      <li><strong>Animated KPI tiles</strong> (total cases, incident volume, near-miss conversion, high-risk %, severe cases) with client-side JavaScript counter animations.</li>
      <li><strong>Overview sub-tab:</strong> bar charts by category type, risk level; line chart over time; stacked year breakdown; top primary classifications; filterable data table with CSV export.</li>
      <li><strong>Clusters sub-tab:</strong> case count ranking, per-cluster drilldown with donut chart, AI-extracted top terms &amp; example incidents, ESG performance metrics, root-cause &amp; corrective-action themes.</li>
      <li><strong>Early Warning Dashboard:</strong> ranked EWI bar chart, counts heatmap (incidents/near-misses/high-priority), rates heatmap (near-miss rate, HP within NM, HP within Inc).</li>
    </ul>

    <h3>Tab 2 &mdash; Event Intelligence</h3>
    <ul>
      <li>Sortable, filterable data portal with native search and CSV export for all historical events.</li>
    </ul>

    <h3>Tab 3 &mdash; AI Safety Analyst</h3>
    <ul>
      <li>Free-text input for describing a hypothetical hazard scenario.</li>
      <li>RAG-powered analysis with typewriter animation and source-event transparency.</li>
      <li>Expandable top-10 similar events table with individual CSV export.</li>
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

    <h3>Early Warning Index Computation</h3>
    <div class="code"><pre><code class="language-python">def calc_priority(r, s):
    """Priority = Risk level score + Severity score"""
    r_score = 2 if 'high' in str(r).lower() else (1 if 'medium' in str(r).lower() else 0)
    s_score = 3 if ('major' in str(s).lower() or 'serious' in str(s).lower()) \
              else (2 if 'significant' in str(s).lower() else 1)
    return r_score + s_score

# Per-cluster EWI aggregation
ewi_df['priority_score'] = ewi_df.apply(
    lambda x: calc_priority(x.get(risk_col, ''), x.get(sev_col, '')), axis=1
)
ewi_df['is_hp'] = ewi_df['priority_score'] >= 4
ewi_df['is_nm'] = ewi_df[cat_col].str.lower().isin(['near miss', 'nearmiss', 'near_miss'])

agg['ewi'] = (agg['near_miss_rate']/100.0) \
            * (agg['hp_within_nm']/100.0) \
            * np.log1p(agg['n_cases'])</code></pre></div>

    <h3>GCP Vector Search Index Setup</h3>
    <div class="code"><pre><code class="language-python">model = TextEmbeddingModel.from_pretrained("text-embedding-004")
texts = events_df['rag_content'].tolist()

# Batch embedding to stay under token limits
for i in range(0, len(texts), 25):
    batch_results = model.get_embeddings(texts[i:i+25])
    embeddings.extend([emb.values for emb in batch_results])

# Create Vertex AI Vector Search index
my_index = aiplatform.MatchingEngineIndex.create_tree_ah_index(
    display_name="methanex_safety_index",
    contents_delta_uri=f"gs://{BUCKET_NAME}/index_data",
    dimensions=768,
    approximate_neighbors_count=10,
    distance_measure_type="DOT_PRODUCT_DISTANCE"
)

# Deploy to public endpoint
my_index_endpoint = aiplatform.MatchingEngineIndexEndpoint.create(
    display_name="methanex_safety_endpoint",
    public_endpoint_enabled=True
)
my_index_endpoint.deploy_index(index=my_index, deployed_index_id="methanex_deployed_index")</code></pre></div>

    <h3>Client-Side KPI Counter Animation (JavaScript)</h3>
    <div class="code"><pre><code class="language-javascript">function animateValue(id, start, end, duration, isPercent) {
    let obj = document.getElementById(id);
    let startTime = null;
    const step = (timestamp) => {
        if (!startTime) startTime = timestamp;
        const progress = Math.min((timestamp - startTime) / duration, 1);
        const easeProgress = 1 - Math.pow(1 - progress, 3);  // cubic ease-out
        let current = easeProgress * (end - start) + start;
        if (isPercent) obj.innerHTML = current.toFixed(1) + "%";
        else obj.innerHTML = Math.floor(current);
        if (progress < 1) window.requestAnimationFrame(step);
    };
    window.requestAnimationFrame(step);
}</code></pre></div>
  </div>

  <!-- ======== FINDINGS ======== -->
  <div id="findings" class="section">
    <h2>Key Findings &amp; Recommendations</h2>
    <ul>
      <li><strong>Focus on dominant clusters:</strong> The Pareto analysis module shows which operational clusters
          account for the highest volume of reports.</li>
      <li><strong>Target high-severity ratios:</strong> Prioritize prevention on clusters with a high ratio of
          <em>Incidents</em> to <em>Near-Misses</em>, where current defenses are frequently failing.</li>
      <li><strong>Proactive monitoring:</strong> Timeline trend analysis lets Methanex spot emerging risks
          (e.g., a spike in IT/AI-related exposures in 2024) before they become systemic.</li>
      <li><strong>Faster learning loop:</strong> Incident &rarr; insight &rarr; prevention focus cycle is
          accelerated by the AI advisor's real-time retrieval and structured recommendations.</li>
      <li><strong>Consistent access:</strong> All lessons learned are searchable, reducing time-to-guidance for
          frontline users.</li>
    </ul>
  </div>

  <!-- ======== HOW TO RUN ======== -->
  <div id="run" class="section">
    <h2>How to Run Locally</h2>

    <h3>Repository Structure</h3>
    <div class="code"><pre><code>methanex-safety-intelligence/
├── data/
│   ├── events_clean.csv
│   ├── actions_clean.csv
│   └── case_cluster_map.csv
├── assets/
│   └── style.css
├── app.py                   # Main Dash application (~860 lines)
├── rag_engine.py            # Vertex AI / Gemini RAG module
├── setup_cloud.py           # One-time GCP Vector Search setup
├── data_processing.py       # Data loading & visualization helpers
├── requirements.txt
├── .env.example
└── README.md</code></pre></div>

    <h3>Prerequisites</h3>
    <ol>
      <li>Create a GCP project and enable the Vertex AI API.</li>
      <li>Configure Vertex AI Vector Search (index + endpoint).</li>
      <li>Create a service account, download its JSON key as <code>gcp-key.json</code>.</li>
      <li>Copy <code>.env.example</code> to <code>.env</code> and fill in your GCP project ID, location,
          endpoint IDs, and bucket name.</li>
    </ol>

    <h3>Run</h3>
    <div class="code"><pre><code class="language-bash">pip install -r requirements.txt

# First time only — set up the vector search index (~60 min)
python setup_cloud.py

# Launch the dashboard
python app.py
# Navigate to http://127.0.0.1:8050/</code></pre></div>
  </div>

</div>
