---
layout: page
title: Answer Sheet Toolkit - Keyboard-First macOS Answer Sheet App
description: SwiftUI/macOS/MVVM/Keyboard-first grid/Mock exam timer/XLSX export/Local-first desktop product engineering
img: assets/img/AnswerSheetToolkit/answer_sheet_toolkit.png
importance: -2
category: work
related_publications: false
---

<style>
  :root{
    --card-bg:#ffffff; --card-border:#e5e7eb; --muted:#6b7280;
    --badge-bg:rgba(0,0,0,.04); --badge-border:rgba(0,0,0,.08);
    --accent:#1e293b; --accent-2:#f59e0b;
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
  .badge-v2{background:rgba(245,158,11,.14);border-color:rgba(245,158,11,.4);color:var(--accent-2);font-weight:600}
  .kpi{display:flex;gap:1rem;flex-wrap:wrap}
  .kpi .card{flex:1 1 190px;background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:.9rem;box-shadow:0 2px 12px rgba(0,0,0,.06);color:var(--global-text-color)}
  .kpi .card .muted{color:var(--muted)}
  figure{margin:0}
  figure img{display:block;width:100%;height:auto;max-width:100%;border-radius:.75rem;box-shadow:0 6px 18px rgba(0,0,0,.08)}
  figure figcaption{color:var(--muted);font-size:.9rem;margin-top:.5rem}
  .grid-2{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:1rem}
  .toc a{display:block;padding:.2rem 0}
  table{width:100%;border-collapse:collapse;font-size:.95rem}
  th,td{padding:.6rem .65rem;border-bottom:1px solid var(--card-border);vertical-align:top}
  th{text-align:left}
  pre{margin:0;overflow:auto}
</style>

<div class="wrap">

  <p>
    <span class="badge badge-v2">Personal project</span>
    <span class="badge">Native macOS (SwiftUI)</span>
  </p>

  <p class="lead">
    <strong>Author:</strong> Regan Yin &nbsp;|&nbsp;
    <strong>Platform:</strong> macOS 14+ (Apple Silicon ready) &nbsp;|&nbsp;
    <strong>Stack:</strong> SwiftUI + MVVM<br>
    A clean, <strong>keyboard-first</strong> macOS app for recording the answers from
    multiple-choice paper exams — built around a fast answer grid, a configurable
    mock-exam timer, and clean export to Excel and the clipboard.
  </p>

  <p>
    <a href="https://github.com/Regan-Yin/AnswerSheetToolkit" target="_blank" rel="noopener">View on GitHub &rarr;</a>
  </p>

  <figure class="section">
    <img src="{{ '/assets/img/AnswerSheetToolkit/answer_sheet_toolkit.png' | relative_url }}" alt="Answer Sheet Toolkit — keyboard-first answer grid and mock exam timer">
    <figcaption class="muted">Answer Sheet Toolkit — create, fill, focus, perform.</figcaption>
  </figure>

  <div class="toc section">
    <h3>Contents</h3>
    <a href="#executive-summary">Executive Summary</a>
    <a href="#stack">Tech Stack</a>
    <a href="#features">Features</a>
    <a href="#architecture">Architecture</a>
    <a href="#packaging">Packaging &amp; Distribution</a>
    <a href="#run">How to Build &amp; Run</a>
  </div>

  <div id="executive-summary" class="section">
    <h2>Executive Summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Build Target</div><div><strong>Swift 5.9+ / macOS 14+</strong></div></div>
      <div class="card"><div class="muted">Input Model</div><div><strong>Keyboard-first answer grid</strong></div></div>
      <div class="card"><div class="muted">Timer</div><div><strong>Count-up / count-down mock exam</strong></div></div>
      <div class="card"><div class="muted">Export</div><div><strong>.xlsx + clipboard (TSV)</strong></div></div>
      <div class="card"><div class="muted">Persistence</div><div><strong>JSON in Application Support</strong></div></div>
    </div>
    <p class="lead" style="margin-top:1rem">
      Answer Sheet Toolkit makes recording multiple-choice answers fast and frictionless.
      Type <code>A</code>–<code>D</code> to fill, <code>Tab</code> / <code>Shift+Tab</code> to move,
      and the grid auto-fits the most "square" layout for any question count. A dependency-free
      XLSX writer keeps the app lightweight, while runtime localization and theming keep it polished.
    </p>
  </div>

  <div id="stack" class="section">
    <h2>Tech Stack</h2>
    <span class="badge">SwiftUI</span>
    <span class="badge">MVVM</span>
    <span class="badge">AppKit (KeyCaptureView)</span>
    <span class="badge">Custom XLSX writer</span>
    <span class="badge">ZIP archiving</span>
    <span class="badge">JSON persistence</span>
    <span class="badge">Localization (EN / 简体中文)</span>
  </div>

  <div id="features" class="section">
    <h2>Features</h2>
    <div class="grid-2">
      <div>
        <ul class="lead">
          <li><strong>Answer sheet management</strong> — create, rename, delete, and switch between multiple sheets.</li>
          <li><strong>Keyboard-first grid</strong> — type <code>A</code>–<code>D</code> to fill; <code>Tab</code> / <code>Shift+Tab</code> navigate; <code>Delete</code> clears; <code>Esc</code> exits answering mode.</li>
          <li><strong>Smart layout</strong> — set total questions and the grid auto-fits the most "square" shape (e.g. 85 → 10 × 9), or set rows / questions-per-row directly.</li>
          <li><strong>Configurable choices</strong> — restrict input to a subset such as A–D, snapshotted per sheet.</li>
        </ul>
      </div>
      <div>
        <ul class="lead">
          <li><strong>Mock exam mode</strong> — count-up or count-down timer with editable duration and optional start delay; freezes on completion.</li>
          <li><strong>Export</strong> — one click to <code>.xlsx</code> or the clipboard (TSV) with in-app success/failure notifications.</li>
          <li><strong>Persistence</strong> — sheets and settings stored as JSON in Application Support.</li>
          <li><strong>Localization &amp; theming</strong> — English and Simplified Chinese; System, Light, Dark, and Light Amber themes.</li>
        </ul>
      </div>
    </div>
  </div>

  <div id="architecture" class="section">
    <h2>Architecture</h2>
    <p class="lead">The app follows <strong>MVVM</strong> with a single coordinating <code>AppStore</code>.</p>
    <table>
      <thead>
        <tr><th>Layer</th><th>Implementation</th><th>Purpose</th></tr>
      </thead>
      <tbody>
        <tr><td>Models</td><td>AppSettings, AnswerSheet, AnswerEntry, ThemeMode, LanguageMode, MockTimerMode</td><td>Core domain types and configuration</td></tr>
        <tr><td>Logic</td><td>AnswerValidator, GridNavigator</td><td>Pure, testable helpers for input and navigation</td></tr>
        <tr><td>Services</td><td>Persistence, XLSXWriter, ZipArchive, clipboard, localization, theming</td><td>Side-effecting services and dependency-free export</td></tr>
        <tr><td>ViewModels</td><td>AppStore, AnswerSheetEditorViewModel, MockExamTimerViewModel, SettingsViewModel, ExportViewModel</td><td>State and behavior coordination</td></tr>
        <tr><td>Views</td><td>SwiftUI views + AppKit KeyCaptureView</td><td>UI plus reliable Tab / Shift+Tab key handling</td></tr>
      </tbody>
    </table>
  </div>

  <div id="packaging" class="section">
    <h2>Packaging &amp; Distribution</h2>
    <ul class="lead">
      <li><strong>One-step packaging:</strong> <code>./scripts/package.sh</code> builds a Release <code>.app</code> and packages it as a drag-to-Applications <code>.dmg</code> and a <code>.zip</code> (outputs land in <code>dist/</code>).</li>
      <li><strong>Testing:</strong> comprehensive unit and UI tests cover models, logic, services, view models, and end-to-end keyboard flows.</li>
      <li><strong>Gatekeeper note:</strong> the build is unsigned; for frictionless distribution, sign with a Developer ID certificate and notarize with <code>notarytool</code>.</li>
    </ul>
  </div>

  <div id="run" class="section">
    <h2>How to Build &amp; Run</h2>
    <pre><code class="language-bash">git clone https://github.com/Regan-Yin/AnswerSheetToolkit.git
cd AnswerSheetToolkit
open AnswerSheetToolkit.xcodeproj
# Select the AnswerSheetToolkit scheme and press Run (Cmd+R)

# Or from the command line:
xcodebuild build -scheme AnswerSheetToolkit -destination 'platform=macOS'
xcodebuild test  -scheme AnswerSheetToolkit -destination 'platform=macOS'</code></pre>
    <p class="muted">Full build, packaging, and architecture notes are documented in the <a href="https://github.com/Regan-Yin/AnswerSheetToolkit/blob/main/README.md" target="_blank" rel="noopener">repository README</a>.</p>
  </div>

</div>
