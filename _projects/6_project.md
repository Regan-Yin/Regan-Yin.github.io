---
layout: page
title: Agentic Movie Recommender
description: Agentic AI/RAG/Ollama Cloud/DSPy/GEPA/TMDB/Python — preference-first recommendations with strict latency and output contracts
img: assets/img/movie_recommender/movie-recommender.png
importance: -1
category: work
related_publications: false
---

<style>
  :root{
    --card-bg:#ffffff; --card-border:#e5e7eb; --muted:#6b7280;
    --badge-bg:rgba(0,0,0,.04); --badge-border:rgba(0,0,0,.08);
    --accent:#7c3aed; --accent-2:#0ea5e9;
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
  .badge-v2{background:rgba(14,165,233,.12);border-color:rgba(14,165,233,.35);color:var(--accent-2);font-weight:600}
  .kpi{display:flex;gap:1rem;flex-wrap:wrap}
  .kpi .card{flex:1 1 180px;background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:.9rem;box-shadow:0 2px 12px rgba(0,0,0,.06);color:var(--global-text-color)}
  .kpi .card .muted{color:var(--muted)}
  figure{margin:0}
  figure img{display:block;width:100%;height:auto;max-width:100%;border-radius:.75rem;box-shadow:0 6px 18px rgba(0,0,0,.08)}
  figure figcaption{color:var(--muted);font-size:.9rem;margin-top:.5rem}
  .grid-2{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:1rem}
  .toc a{display:block;padding:.2rem 0}
  table{width:100%;border-collapse:collapse;font-size:.95rem}
  th,td{padding:.6rem .65rem;border-bottom:1px solid var(--card-border);vertical-align:top}
  th{text-align:left;color:var(--accent);background:var(--badge-bg)}
  .callout{background:rgba(124,58,237,.08);border-left:4px solid var(--accent);border-radius:.5rem;padding:.85rem 1rem;margin:1rem 0;font-size:.95rem}
  pre{margin:0;overflow:auto}
  .code{background:#0b0f19;color:#e8e8e8;border-radius:.6rem;padding:1rem 1.2rem;overflow:auto;font-size:.88rem;line-height:1.55}
</style>

<div class="wrap">

  <p>
    <span class="badge badge-v2">Course project</span>
    <span class="badge">RAG + LLM + DSPy/GEPA</span>
  </p>

  <p class="lead">
    <strong>Author:</strong> Regan Yin<br>
    <strong>Course:</strong> BAMS 521 — Agentic AI (UBC Sauder)<br>
    A <strong>preference-first</strong> movie recommender over a TMDB top-1000 CSV: deterministic retrieval and ranking in Python, <strong>Ollama Cloud</strong> (<code>gemma4:31b-cloud</code>) for final selection and copy, plus corrective retry and a deterministic fallback so every call returns a valid <code>tmdb_id</code> and a persuasive description within course limits.
  </p>

  <p>
    <a href="https://github.com/Regan-Yin/agentic-movie-recommender" target="_blank" rel="noopener">View on GitHub &rarr;</a>
  </p>

  <figure class="section">
    <img src="{{ '/assets/img/movie_recommender/movie-recommender.png' | relative_url }}" alt="Agentic movie recommender interface preview">
    <figcaption class="muted">Project preview — UI and recommendation flow.</figcaption>
  </figure>

  <div class="toc section">
    <h3>Contents</h3>
    <a href="#executive-summary">Executive summary</a>
    <a href="#requirements">Grader requirements</a>
    <a href="#stack">Tech stack</a>
    <a href="#pipeline">Pipeline</a>
    <a href="#design">Design choices</a>
    <a href="#eval">Evaluation &amp; tuning</a>
    <a href="#run">How to run</a>
  </div>

  <div id="executive-summary" class="section">
    <h2>Executive summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Latency budget</div><div><strong>≤ 20 s</strong> (13 s primary + 4 s retry + fallback)</div></div>
      <div class="card"><div class="muted">Description</div><div><strong>≤ 500 chars</strong>, sentence-aware trim</div></div>
      <div class="card"><div class="muted">Candidate pool</div><div><strong>350 titles</strong> from CSV (top slice)</div></div>
      <div class="card"><div class="muted">LLM</div><div><strong>gemma4:31b-cloud</strong> via Ollama</div></div>
      <div class="card"><div class="muted">Tuning</div><div><strong>DSPy + GEPA</strong> on a weighted metric</div></div>
    </div>
    <p class="lead" style="margin-top:1rem">
      The system behaves as a <strong>retrieval-augmented re-ranker</strong>: lexical and keyword-heavy RAG pulls a strong shortlist, hybrid scoring encodes preferences over watch history (including explicit conflict handling), and the LLM only chooses one ID and writes the pitch. Invalid IDs, history collisions, or timeouts fall back to a <strong>hash-stable</strong> deterministic description so outputs stay spec-compliant.
    </p>
  </div>

  <div id="requirements" class="section">
    <h2>Enforced contracts (course / grader)</h2>
    <div class="callout">
      <code>get_recommendation(preferences, history, history_ids)</code> must return a dict with keys <code>tmdb_id</code> (int) and <code>description</code> (str). The ID must sit in the offline pool, must never duplicate watch history, descriptions must respect the character cap, API keys load from the environment — not the source tree.
    </div>
    <table>
      <thead>
        <tr><th>Requirement</th><th>Where it lives</th></tr>
      </thead>
      <tbody>
        <tr><td>Valid <code>tmdb_id</code> in pool</td><td>Post-LLM validation, retry, then fallback</td></tr>
        <tr><td>No history repeats</td><td>Retrieval de-dup, prompt rules, final check</td></tr>
        <tr><td>20 s wall clock</td><td>Timeouts + instant fallback path</td></tr>
        <tr><td>500-char descriptions</td><td>Constants + sanitizer + smart truncation</td></tr>
      </tbody>
    </table>
  </div>

  <div id="stack" class="section">
    <h2>Tech stack</h2>
    <span class="badge">Python</span>
    <span class="badge">pandas</span>
    <span class="badge">Ollama Cloud</span>
    <span class="badge">DSPy</span>
    <span class="badge">GEPA</span>
    <span class="badge">Streamlit (app)</span>
    <span class="badge">TMDB CSV (offline corpus)</span>
  </div>

  <div id="pipeline" class="section">
    <h2>Pipeline</h2>
    <ol class="lead">
      <li><strong>Normalize inputs</strong> — strip, dedupe, type-coerce preferences and history.</li>
      <li><strong>Preference analysis</strong> — genre weights, blocked genres, tone/mood expansions.</li>
      <li><strong>RAG retrieval (~100)</strong> — lexical + overview/tagline/keywords + quality, with conflict and block penalties.</li>
      <li><strong>Hybrid re-rank (~14)</strong> — preference beats history; bonuses for tone/title fit.</li>
      <li><strong>LLM pick + JSON</strong> — strict prompt, banned marketing phrases, pivot guidance when history conflicts with preferences.</li>
      <li><strong>Corrective retry</strong> — one short retry if the model violates pool or history rules.</li>
      <li><strong>Deterministic fallback</strong> — template × hook variety keyed by hash for stable, fluent copy without the model.</li>
      <li><strong>Sanitize</strong> — strip markdown, labels, banned phrases; truncate at sentence boundaries.</li>
    </ol>
  </div>

  <div id="design" class="section">
    <h2>Design highlights</h2>
    <div class="grid-2">
      <div>
        <ul class="lead">
          <li><strong>Preference over history</strong> — explicit conflict genres (e.g. romance in history vs “pure thriller” ask) reduce scores and nudge the model to pivot in one clause.</li>
          <li><strong>Tone vocabulary</strong> — alias maps lift intent (“slow-burn”, “twist”, “feel-good”) beyond raw genres.</li>
          <li><strong>Negative constraints</strong> — “no horror” style phrases become hard scoring penalties plus prompt rules.</li>
          <li><strong>No live TMDB at inference</strong> — keeps latency predictable; TMDB API optional for offline eval generation only.</li>
        </ul>
      </div>
      <div>
        <ul class="lead">
          <li><strong>Process-local cache</strong> on normalized inputs for fast repeat calls.</li>
          <li><strong>GEPA output</strong> — winning prompt fragments persist in <code>dspy_gepa_best_config.json</code> and load in <code>llm.py</code>.</li>
        </ul>
      </div>
    </div>
  </div>

  <div id="eval" class="section">
    <h2>Evaluation and tuning</h2>
    <p class="lead">
      Quality is driven by a <strong>weighted automated metric</strong> (genre alignment, quality priors, description length bucket, specificity vs filler, history-acknowledgement bonus, penalties for banned fluff) plus hard gates on pool and history membership. <code>dspy_gepa_benchmark.py</code> runs a style sweep, then <strong>GEPA</strong> reflection on prompt instructions using structured metric feedback, and writes the best configuration for production inference.
    </p>
  </div>

  <div id="run" class="section">
    <h2>How to run</h2>
    <p class="lead">Clone the repo, create a virtual environment, install requirements, and set <code>OLLAMA_API_KEY</code>. Use <code>python llm.py</code> for the CLI, <code>python test.py</code> for the course tests, and optionally <code>dspy_gepa_benchmark.py</code> to regenerate tuned prompts.</p>
    <div class="code"><pre>git clone https://github.com/Regan-Yin/agentic-movie-recommender.git
cd agentic-movie-recommender
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
export OLLAMA_API_KEY=your_key_here
python llm.py --preferences "Sci-fi with a smart twist" --history "Inception"
python test.py</pre></div>
    <p class="muted">Full flags, zip submission layout, and metric tables are documented in the <a href="https://github.com/Regan-Yin/agentic-movie-recommender/blob/main/README.md" target="_blank" rel="noopener">repository README</a>.</p>
  </div>

</div>
