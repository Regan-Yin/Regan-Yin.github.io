---
layout: page
title: JobTracker Offer Kitty - Local-First macOS Job Application Tracker
description: SwiftUI/macOS/SQLite/GRDB/ZIPFoundation/Local-first desktop product engineering
img: assets/img/JobTracker/jobtracker_offer_kitty_icon.png
importance: 0
category: work
related_publications: false
---

<style>
  :root{
    --card-bg:#ffffff; --card-border:#e5e7eb; --muted:#6b7280;
    --badge-bg:rgba(0,0,0,.04); --badge-border:rgba(0,0,0,.08);
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
  .kpi .card{flex:1 1 190px;background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:.9rem;box-shadow:0 2px 12px rgba(0,0,0,.06);color:var(--global-text-color)}
  .kpi .card .muted{color:var(--muted)}
  figure{margin:0}
  figure img{display:block;width:100%;height:auto;max-width:100%;border-radius:.75rem;box-shadow:0 6px 18px rgba(0,0,0,.08)}
  figure figcaption{color:var(--muted);font-size:.9rem;margin-top:.5rem}
  .grid-2{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:1rem}
  .toc a{display:block;padding:.2rem 0}
  table{width:100%;border-collapse:collapse;font-size:.95rem}
  th,td{padding:.6rem .65rem;border-bottom:1px solid var(--card-border)}
  th{text-align:left}
</style>

<div class="wrap">
  <p class="lead">
    <strong>Author:</strong> Regan Yin &nbsp;|&nbsp;
    <strong>Platform:</strong> macOS 14+ (Apple Silicon ready) &nbsp;|&nbsp;
    <strong>Version:</strong> 1.0.0<br>
    A local-first desktop app to track job applications from your own document folders,
    with SQLite persistence, structured workflow tracking, analytics views, and export support.
  </p>

  <p>
    <a href="https://github.com/Regan-Yin/JobTracker_Offer_Kitty" target="_blank" rel="noopener">View on GitHub &rarr;</a>
  </p>

  <div class="toc section">
    <h3>Contents</h3>
    <a href="#executive-summary">Executive Summary</a>
    <a href="#stack">Tech Stack</a>
    <a href="#scope">MVP Scope</a>
    <a href="#architecture">Architecture</a>
    <a href="#features">Product Features</a>
    <a href="#privacy">Privacy, Security, and License</a>
    <a href="#run">How to Run Locally</a>
  </div>

  <div id="executive-summary" class="section">
    <h2>Executive Summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Build Target</div><div><strong>Swift 5.10+ / macOS 14+</strong></div></div>
      <div class="card"><div class="muted">Persistence</div><div><strong>SQLite (GRDB)</strong></div></div>
      <div class="card"><div class="muted">Document Support</div><div><strong>.docx parsing + .doc metadata</strong></div></div>
      <div class="card"><div class="muted">Core Principle</div><div><strong>Local-first, manual override first</strong></div></div>
      <div class="card"><div class="muted">Views</div><div><strong>Overview / Applications / Companies / Exports / Settings</strong></div></div>
    </div>
    <p class="lead" style="margin-top:1rem">
      JobTracker Offer Kitty turns unstructured job-material folders into structured company and application records.
      It prioritizes conservative inference, high transparency, and quick manual correction, so users keep full control
      over data quality while still getting dashboards, reminders, and exportable results.
    </p>
  </div>

  <div id="stack" class="section">
    <h2>Tech Stack</h2>
    <span class="badge">SwiftUI</span>
    <span class="badge">Swift Concurrency (async/await)</span>
    <span class="badge">SQLite</span>
    <span class="badge">GRDB</span>
    <span class="badge">ZIPFoundation</span>
    <span class="badge">Swift Package Manager</span>
    <span class="badge">macOS-native local app architecture</span>
  </div>

  <div id="scope" class="section">
    <h2>MVP Scope</h2>
    <div class="grid-2">
      <div>
        <h4>In Scope</h4>
        <ul>
          <li>User-selected root folder scan with recursive parsing.</li>
          <li>Artifact classification for application materials (.docx/.doc).</li>
          <li>Role and company inference with confidence-aware rules.</li>
          <li>Manual CRUD, duplicate suggestions, and merge workflows.</li>
          <li>Analytics dashboards, KPI cards, reminders, and CSV export.</li>
          <li>Fully local storage and operation without paid APIs.</li>
        </ul>
      </div>
      <div>
        <h4>Out of Scope (MVP)</h4>
        <ul>
          <li>Email/Outlook ingestion and mailbox automation.</li>
          <li>LinkedIn scraping or browser automation.</li>
          <li>Cloud sync and multi-user collaboration.</li>
          <li>ML/LLM-based classification in core pipeline.</li>
          <li>OCR-heavy document extraction.</li>
        </ul>
      </div>
    </div>
  </div>

  <div id="architecture" class="section">
    <h2>Architecture</h2>
    <table>
      <thead>
        <tr><th>Layer</th><th>Implementation</th><th>Purpose</th></tr>
      </thead>
      <tbody>
        <tr><td>App Shell</td><td>SwiftUI + AppState</td><td>Navigation, theme, onboarding, global state</td></tr>
        <tr><td>Data Ingestion</td><td>FolderScanner + IngestionService</td><td>Scan files, classify artifacts, infer role/application records</td></tr>
        <tr><td>Domain Logic</td><td>Classifier, normalizer, scoring, dedupe/merge services</td><td>Transform signals into trackable entities with validation</td></tr>
        <tr><td>Persistence</td><td>AppDatabase + GRDB repositories</td><td>Store companies, applications, tasks, and export artifacts</td></tr>
        <tr><td>UI Features</td><td>Overview/Applications/Companies/Exports/Settings</td><td>Operations, analytics, review, and output</td></tr>
      </tbody>
    </table>
  </div>

  <div id="features" class="section">
    <h2>Product Features</h2>
    <ul>
      <li><strong>Onboarding scan:</strong> one-time folder selection + immediate structured ingest.</li>
      <li><strong>Application funnel tracking:</strong> stage/outcome/last-failed-stage data model.</li>
      <li><strong>Company intelligence:</strong> mapping fields for industry and company size.</li>
      <li><strong>Duplicate governance:</strong> suggest duplicates, never auto-merge silently.</li>
      <li><strong>Export readiness:</strong> CSV outputs for external analysis and reporting.</li>
      <li><strong>Low-ops deployment:</strong> local app build path with optional packaging script.</li>
    </ul>
  </div>

  <div id="privacy" class="section">
    <h2>Privacy, Security, and License</h2>
    <ul>
      <li><strong>Privacy:</strong> no telemetry or cloud sync in core features; data remains local on device.</li>
      <li><strong>Storage path:</strong> <code>~/Library/Application Support/JobTracker/jobtracker.sqlite</code>.</li>
      <li><strong>Security posture:</strong> dependency-based local build with no hidden remote backend.</li>
      <li><strong>License:</strong> non-commercial community license in repository; commercial use requires permission.</li>
    </ul>
  </div>

  <div id="run" class="section">
    <h2>How to Run Locally</h2>
    <pre><code class="language-bash">git clone https://github.com/Regan-Yin/JobTracker_Offer_Kitty.git
cd JobTracker_Offer_Kitty
swift package resolve
swift build
open .build/debug/JobTracker</code></pre>
    <p class="muted">Optional packaging script: <code>Scripts/package_mac_app.sh</code> for building a distributable <code>.app</code> and zip package.</p>
  </div>
</div>
