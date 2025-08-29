---
layout: page
title: Predictive Models for Heart Disease Diagnosis
description: Health Care/Data Mining/Logistic Regression/Data Visualization/Machine Learning/
img: assets/img/HeartAttack/heart_attack_concept.jpg
importance: 3
category: work
---

<style>
  /* ---- Dark-mode friendly tokens ---- */
  :root{
    --card-bg:#ffffff; --card-border:#e5e7eb; --muted:#6b7280;
    --badge-bg:rgba(0,0,0,.04); --badge-border:rgba(0,0,0,.08);
  }
  [data-theme="dark"]{
    --card-bg:#0f172a; --card-border:#233047; --muted:#94a3b8;
    --badge-bg:rgba(255,255,255,.08); --badge-border:rgba(255,255,255,.12);
  }

  /* ---- Layout & spacing (prevents overlaps) ---- */
  .wrap{max-width:1100px;margin:0 auto;padding:0 0 1rem}
  .section{margin:2rem 0; contain: content; position:relative}
  .lead{font-size:1.05rem;line-height:1.7}
  .muted{color:var(--muted)}
  .badge{display:inline-block;padding:.35rem .6rem;border-radius:2rem;background:var(--badge-bg);border:1px solid var(--badge-border);margin:.15rem .2rem;font-size:.85rem}
  .kpi{display:flex;gap:1rem;flex-wrap:wrap}
  .kpi .card{flex:1 1 220px;background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:1rem;box-shadow:0 2px 12px rgba(0,0,0,.06)}

  /* ---- Media: figures are block, responsive, with safe margins ---- */
  .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:1rem}
  figure{margin:0}
  figure img{display:block;width:100%;height:auto;max-width:100%;border-radius:.75rem;box-shadow:0 6px 18px rgba(0,0,0,.08)}
  figure figcaption{color:var(--muted);font-size:.9rem;margin-top:.5rem;word-break:break-word}

  /* ---- Code blocks: scrollable, no overlay ---- */
  .code{background:#0b0f19;color:#e8e8e8;border-radius:.6rem;padding:1rem 1.2rem;overflow:auto;font-size:.9rem;line-height:1.55;box-shadow:0 4px 16px rgba(0,0,0,.18)}
  pre{margin:0;white-space:pre;overflow:auto}
  code{word-break:normal}

  /* Simple table style */
  table{width:100%;border-collapse:collapse;font-size:.95rem}
  th,td{padding:.6rem .65rem;border-bottom:1px solid var(--card-border)}
</style>

<div class="wrap">
  <p class="lead">
    End-to-end ML pipeline on BRFSS 2020: data understanding & preprocessing, model selection
    (Decision Tree, Logistic Regression, KNN, Naïve Bayes), 10-fold CV, and cost-sensitive
    decision thresholding (FN » FP) tailored to healthcare risk.
  </p>

  <div class="section">
    <h3>Contents</h3>
    <ul>
      <li><a href="#executive-summary">Executive Summary</a></li>
      <li><a href="#stack">Tech Stack</a></li>
      <li><a href="#data">Data Preparation</a></li>
      <li><a href="#models">Modeling & Tuning</a></li>
      <li><a href="#threshold">Cost-Sensitive Thresholding</a></li>
      <li><a href="#evaluation">Evaluation</a></li>
      <li><a href="#code">Selected Code</a></li>
      <li><a href="#conclusion">Conclusion & Future Work</a></li>
    </ul>
  </div>

  <div id="executive-summary" class="section">
    <h2>Executive Summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Dataset</div><div><strong>BRFSS 2020 (CDC)</strong></div></div>
      <div class="card"><div class="muted">Task</div><div><strong>Heart disease classification</strong></div></div>
      <div class="card"><div class="muted">Split</div><div><strong>Train/Test = 60/40 (rs=42, stratified)</strong></div></div>
      <div class="card"><div class="muted">Objective</div><div><strong>Minimize False Negatives</strong> (Recall↑)</div></div>
      <div class="card"><div class="muted">Best Model</div><div><strong>Logistic Regression</strong> after threshold tuning</div></div>
    </div>
  </div>

  <div id="stack" class="section">
    <h2>Tech Stack</h2>
    <span class="badge">Python</span>
    <span class="badge">NumPy</span>
    <span class="badge">Pandas</span>
    <span class="badge">scikit-learn</span>
    <span class="badge">Matplotlib</span>
    <span class="badge">Seaborn</span>
  </div>

  <div id="data" class="section">
    <h2>Data Preparation</h2>
    <ul>
      <li><strong>Target:</strong> <code>_MICHD</code> (CHD/MI ever; map 2→0).</li>
      <li><strong>Cleaning:</strong> drop vars &gt;90% null; handle special codes (7/9/77/98/99/777/999);
          min-max scale numeric; one-hot encode categoricals.</li>
      <li><strong>Split:</strong> 60/40 train/test, <code>random_state=42</code>, stratified.</li>
    </ul>
    <!-- ONLY the two frequency charts here -->
    <div class="grid">
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_HDFreq.png' | relative_url }}" alt="Heart disease frequency">
        <figcaption>Heart disease frequency (overall).</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_HDFreqSex.png' | relative_url }}" alt="Heart disease frequency by sex">
        <figcaption>Frequency by sex.</figcaption>
      </figure>
    </div>
  </div>

  <div id="models" class="section">
    <h2>Modeling & Tuning</h2>
    <p>Compare Decision Tree, Logistic Regression, KNN, and Naïve Bayes. Hyperparameters via 10-fold CV with recall emphasis (KNN uses accuracy to avoid k=1 overfit).</p>
    <ul>
      <li><strong>Decision Tree:</strong> tune <code>max_depth</code>, <code>max_leaf_nodes</code>.</li>
      <li><strong>Logistic Regression:</strong> <code>penalty='l1'</code>, <code>solver='saga'</code>, <code>max_iter=2000</code>, grid over <code>C</code>.</li>
      <li><strong>KNN:</strong> grid over <code>n_neighbors</code>; best around <code>k=8</code>.</li>
      <li><strong>Naïve Bayes:</strong> Gaussian / Bernoulli based on encoding.</li>
    </ul>
  </div>

  <div id="threshold" class="section">
    <h2>Cost-Sensitive Thresholding</h2>
    <p>Total cost = <code>100×FN + 10×FP</code>. Scan thresholds over [0,1] and select the minimum-cost point. Optimal thresholds used: DT=0.09, LR=0.08, NB=0.08, KNN=0.01.</p>
    <!-- ONLY the four cost curves here -->
    <div class="grid">
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_LRCostCurve.png' | relative_url }}" alt="Logistic Regression cost curve">
        <figcaption>LR: Cost vs threshold (optimal ≈ 0.08).</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_DesTreeCostCurve.png' | relative_url }}" alt="Decision Tree cost curve">
        <figcaption>Decision Tree: Cost vs threshold (optimal ≈ 0.09).</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_NBCostCurve.png' | relative_url }}" alt="Naïve Bayes cost curve">
        <figcaption>Naïve Bayes: Cost vs threshold (optimal ≈ 0.08).</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_KNNCostCurve.png' | relative_url }}" alt="KNN cost curve">
        <figcaption>KNN: Cost vs threshold (optimal ≈ 0.01).</figcaption>
      </figure>
    </div>
  </div>

  <div id="evaluation" class="section">
    <h2>Evaluation</h2>
    <p>Report Accuracy, Precision, Recall, MAE, and Confusion Matrix before/after thresholding. Post-threshold, LR achieves the highest recall and lowest total cost.</p>
    <table>
      <thead><tr><th>Model</th><th>Opt. Threshold</th><th>Notes</th></tr></thead>
      <tbody>
        <tr><td>Logistic Regression</td><td>0.08</td><td>Best recall & lowest cost after tuning.</td></tr>
        <tr><td>Decision Tree</td><td>0.09</td><td>Competitive recall with tuning.</td></tr>
        <tr><td>Naïve Bayes</td><td>0.08</td><td>High baseline recall; cost improved.</td></tr>
        <tr><td>KNN (k=8)</td><td>0.01</td><td>Low threshold needed; recall trails LR.</td></tr>
      </tbody>
    </table>

    <!-- ONLY the four PRC plots here -->
    <div class="grid" style="margin-top:1rem">
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_LRPRC.png' | relative_url }}" alt="LR PRC">
        <figcaption>Logistic Regression: Precision–Recall Curve.</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_DesTreePRC.png' | relative_url }}" alt="Decision Tree PRC">
        <figcaption>Decision Tree: Precision–Recall Curve.</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_NBPRC.png' | relative_url }}" alt="Naïve Bayes PRC">
        <figcaption>Naïve Bayes: Precision–Recall Curve.</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/HeartAttack/project3_KNNPRC.png' | relative_url }}" alt="KNN PRC">
        <figcaption>KNN: Precision–Recall Curve.</figcaption>
      </figure>
    </div>
  </div>

  <div id="code" class="section">
    <h2>Selected Code</h2>

    <h3>Train/Test Split & Target</h3>
    <div class="code"><pre><code class="language-python">from sklearn.model_selection import train_test_split

y = df["_MICHD"].replace({2: 0})   # 1 = CHD/MI ever; 0 = otherwise
X = df.drop(columns=["_MICHD"])

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.40, random_state=42, stratify=y
)</code></pre></div>

    <h3>Recall-Focused CV & Threshold Search</h3>
    <div class="code"><pre><code class="language-python">from sklearn.model_selection import GridSearchCV
from sklearn.linear_model import LogisticRegression
import numpy as np

# Logistic Regression (recall-first)
lr = LogisticRegression(penalty="l1", solver="saga", max_iter=2000)
grid = {"C": [0.5, 1, 1.4142, 2, 3]}
lr_cv = GridSearchCV(lr, grid, scoring="recall", cv=10, n_jobs=-1).fit(X_train, y_train)
lr_best = lr_cv.best_estimator_.fit(X_train, y_train)

def min_cost_threshold(y_true, proba, fn_cost=100, fp_cost=10):
    best_t, best_c = 0.5, float("inf")
    for t in np.linspace(0, 1, 501):
        yhat = (proba >= t).astype(int)
        fp = ((yhat==1) & (y_true==0)).sum()
        fn = ((yhat==0) & (y_true==1)).sum()
        c = fn_cost*fn + fp_cost*fp
        if c &lt; best_c: best_t, best_c = t, c
    return best_t, best_c

t_opt, _ = min_cost_threshold(y_test.values, lr_best.predict_proba(X_test)[:,1])</code></pre></div>
  </div>

  <div id="conclusion" class="section">
    <h2>Conclusion & Future Work</h2>
    <p>
      Cost-aware thresholding aligns the model with clinical priorities (catch more positives).
      Logistic Regression performed best after tuning. Next: calibrate probabilities, explore
      cost-sensitive learners and class-imbalance remedies, and validate on external cohorts.
    </p>
  </div>
</div>
