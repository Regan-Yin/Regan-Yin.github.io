---
layout: page
title: Predictive Models for Heart Disease Diagnosis
description: Health Care/Data Mining/Logistic Regression/Data Visualization/Machine Learning/
img: assets/img/heart_attack_concept.jpg
importance: 3
category: work
---

<style>
  /* Page-only theming that adapts to al-folio's light/dark toggle */
  :root{
    --card-bg: #ffffff;
    --card-border: #e5e7eb;
    --muted: #6b7280;
    --badge-bg: rgba(0,0,0,.04);
    --badge-border: rgba(0,0,0,.08);
  }
  [data-theme="dark"]{
    --card-bg: #0f172a;
    --card-border: #233047;
    --muted: #94a3b8;
    --badge-bg: rgba(255,255,255,.08);
    --badge-border: rgba(255,255,255,.12);
  }
  .wrap{max-width:1100px;margin:0 auto}
  .lead{font-size:1.05rem;line-height:1.6}
  .muted{color:var(--muted)}
  .badge{display:inline-block;padding:.35rem .6rem;border-radius:2rem;background:var(--badge-bg);border:1px solid var(--badge-border);margin:.15rem .2rem;font-size:.85rem}
  .section{margin:2rem 0}
  .kpi{display:flex;gap:1rem;flex-wrap:wrap}
  .kpi .card{flex:1 1 220px;background:var(--card-bg);border:1px solid var(--card-border);border-radius:.75rem;padding:1rem;box-shadow:0 2px 12px rgba(0,0,0,.06)}
  figure img{max-width:100%;height:auto;border-radius:.75rem;box-shadow:0 6px 18px rgba(0,0,0,.08)}
  figure figcaption{color:var(--muted);font-size:.9rem;margin-top:.4rem}
  .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:1rem}
  .code{background:#0b0f19;color:#e8e8e8;border-radius:.6rem;padding:1rem 1.2rem;overflow:auto;font-size:.9rem}
  pre{margin:0}
  .toc a{display:block;padding:.2rem 0}
  table{width:100%;border-collapse:collapse;font-size:.95rem}
  th,td{padding:.5rem .6rem;border-bottom:1px solid var(--card-border)}
</style>

<div class="wrap">
  <p class="muted">Course: ISOM 3360 · Team: SHI Yushan, CHEN Jinghui, LUK Yin Lee, YIN Chakhei</p>

  <h1>Predictive Models for Heart Disease Diagnosis</h1>
  <p class="lead">
    An end-to-end ML pipeline to predict heart disease using the 2020 BRFSS dataset:
    data understanding & preprocessing, model selection (Decision Tree, Logistic Regression, KNN, Naïve Bayes),
    hyperparameter tuning with cross-validation, and cost-sensitive decision thresholding tailored to healthcare risk.
    Key project details and results are drawn from the final report PDF. :contentReference[oaicite:0]{index=0}
  </p>

  <div class="toc section">
    <h3>Contents</h3>
    <a href="#executive-summary">Executive Summary</a>
    <a href="#stack">Tech Stack & Roles</a>
    <a href="#data">Data Preparation</a>
    <a href="#models">Modeling & Tuning</a>
    <a href="#threshold">Cost-Sensitive Thresholding</a>
    <a href="#evaluation">Evaluation</a>
    <a href="#gallery">Figure Gallery</a>
    <a href="#code">Selected Code Snippets</a>
    <a href="#conclusion">Conclusion & Future Work</a>
  </div>

  <figure class="section">
    <img src="{{ '/assets/img/project3_LRPRC.png' | relative_url }}" alt="Logistic Regression Precision-Recall Curve">
    <figcaption>Precision–Recall Curve (Logistic Regression). :contentReference[oaicite:1]{index=1}</figcaption>
  </figure>

  <div id="executive-summary" class="section">
    <h2>Executive Summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Dataset</div><div><strong>BRFSS 2020 (CDC)</strong></div></div>
      <div class="card"><div class="muted">Task</div><div><strong>Heart disease classification</strong></div></div>
      <div class="card"><div class="muted">Split</div><div><strong>Train/Test = 60/40 (rs=42)</strong> :contentReference[oaicite:2]{index=2}</div></div>
      <div class="card"><div class="muted">Objective</div><div><strong>Minimize False Negatives</strong> (Recall↑)</div></div>
      <div class="card"><div class="muted">Best Model (post-threshold)</div><div><strong>Logistic Regression</strong> (highest recall & lowest cost) :contentReference[oaicite:3]{index=3}</div></div>
    </div>
    <p class="lead">
      We build and compare four supervised models. Guided by clinical risk, we penalize false negatives
      more heavily (FN cost 100 vs FP cost 10) and search decision thresholds that minimize total cost. :contentReference[oaicite:4]{index=4}
    </p>
  </div>

  <div id="stack" class="section">
    <h2>Tech Stack & Roles</h2>
    <span class="badge">Python</span>
    <span class="badge">NumPy</span>
    <span class="badge">Pandas</span>
    <span class="badge">scikit-learn</span>
    <span class="badge">Matplotlib</span>
    <span class="badge">Seaborn</span>
    <p class="muted">End-to-end: data cleaning, EDA, feature processing, model training & evaluation, reporting.</p>
  </div>

  <div id="data" class="section">
    <h2>Data Preparation</h2>
    <ul>
      <li><strong>Source:</strong> CDC BRFSS 2020; target label <code>_MICHD</code> (ever reported CHD/MI). :contentReference[oaicite:5]{index=5}</li>
      <li><strong>Cleaning:</strong> drop vars with &gt;90% nulls; handle special codes (7/9/77/98/99/777/999) by mode/mean/zero per variable type; min-max normalize numerical features; one-hot encode categoricals. :contentReference[oaicite:6]{index=6}</li>
      <li><strong>Split:</strong> test size 40%, random_state 42. :contentReference[oaicite:7]{index=7}</li>
    </ul>
    <div class="grid">
      <figure>
        <img src="{{ '/assets/img/project3_HDFreq.png' | relative_url }}" alt="Heart disease frequency">
        <figcaption>Heart disease prevalence in sample (≈8.5%). :contentReference[oaicite:8]{index=8}</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/project3_HDFreqSex.png' | relative_url }}" alt="Heart disease frequency by sex">
        <figcaption>Sex distribution & prevalence. :contentReference[oaicite:9]{index=9}</figcaption>
      </figure>
    </div>
  </div>

  <div id="models" class="section">
    <h2>Modeling & Tuning</h2>
    <p>We evaluate four algorithms: Decision Tree, Logistic Regression, K-Nearest Neighbors, and Naïve Bayes. Hyperparameters are tuned with 10-fold cross-validation; recall is emphasized due to clinical risk. :contentReference[oaicite:10]{index=10}</p>
    <ul>
      <li><strong>Decision Tree:</strong> tune <code>max_depth</code>, <code>max_leaf_nodes</code> (best ≈ depth=13, leaf=150). :contentReference[oaicite:11]{index=11}</li>
      <li><strong>Logistic Regression:</strong> <code>C</code>, <code>penalty='l1'</code>, <code>solver='saga'</code>, <code>max_iter=2000</code>. :contentReference[oaicite:12]{index=12}</li>
      <li><strong>KNN:</strong> best <code>k</code> by accuracy (k=8) to avoid k=1 overfitting. :contentReference[oaicite:13]{index=13}</li>
      <li><strong>Naïve Bayes:</strong> limited tunables; used default Gaussian/Bernoulli form as per data encoding. :contentReference[oaicite:14]{index=14}</li>
    </ul>
  </div>

  <div id="threshold" class="section">
    <h2>Cost-Sensitive Thresholding</h2>
    <p>
      We define total cost = <code>100×FN + 10×FP</code> and search the probability threshold that minimizes it for each model.
      Optimal thresholds found in the report: DT=0.09, LR=0.08, NB=0.08, KNN=0.01. :contentReference[oaicite:15]{index=15}
    </p>
    <div class="grid">
      <figure>
        <img src="{{ '/assets/img/project3_LRCostCurve.png' | relative_url }}" alt="LR cost curve">
        <figcaption>Logistic Regression cost curve vs threshold. :contentReference[oaicite:16]{index=16}</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/project3_DesTreeCostCurve.png' | relative_url }}" alt="Decision Tree cost curve">
        <figcaption>Decision Tree cost curve vs threshold. :contentReference[oaicite:17]{index=17}</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/project3_NBCostCurve.png' | relative_url }}" alt="Naive Bayes cost curve">
        <figcaption>Naïve Bayes cost curve vs threshold. :contentReference[oaicite:18]{index=18}</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/project3_KNNCostCurve.png' | relative_url }}" alt="KNN cost curve">
        <figcaption>KNN cost curve vs threshold. :contentReference[oaicite:19]{index=19}</figcaption>
      </figure>
    </div>
  </div>

  <div id="evaluation" class="section">
    <h2>Evaluation</h2>
    <p>We report Accuracy, Precision, Recall, MAE, Confusion Matrix before/after applying optimal thresholds. Post-threshold, Logistic Regression achieves the highest recall and lowest total cost among the four models. :contentReference[oaicite:20]{index=20}</p>
    <table>
      <thead><tr><th>Model</th><th>Opt. Threshold</th><th>Note</th></tr></thead>
      <tbody>
        <tr><td>Logistic Regression</td><td>0.08</td><td>Best recall & lowest cost (post-threshold). :contentReference[oaicite:21]{index=21}</td></tr>
        <tr><td>Decision Tree</td><td>0.09</td><td>Competitive recall after thresholding. :contentReference[oaicite:22]{index=22}</td></tr>
        <tr><td>Naïve Bayes</td><td>0.08</td><td>High baseline recall; cost improved with thresholding. :contentReference[oaicite:23]{index=23}</td></tr>
        <tr><td>KNN (k=8)</td><td>0.01</td><td>Very low threshold needed; recall still trails LR. :contentReference[oaicite:24]{index=24}</td></tr>
      </tbody>
    </table>
    <div class="grid" style="margin-top:1rem">
      <figure>
        <img src="{{ '/assets/img/project3_LRPRC.png' | relative_url }}" alt="LR PRC">
        <figcaption>LR Precision–Recall Curve. :contentReference[oaicite:25]{index=25}</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/project3_DesTreePRC.png' | relative_url }}" alt="Decision Tree PRC">
        <figcaption>Decision Tree Precision–Recall Curve. :contentReference[oaicite:26]{index=26}</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/project3_NBPRC.png' | relative_url }}" alt="Naive Bayes PRC">
        <figcaption>Naïve Bayes Precision–Recall Curve. :contentReference[oaicite:27]{index=27}</figcaption>
      </figure>
      <figure>
        <img src="{{ '/assets/img/project3_KNNPRC.png' | relative_url }}" alt="KNN PRC">
        <figcaption>KNN Precision–Recall Curve. :contentReference[oaicite:28]{index=28}</figcaption>
      </figure>
    </div>
  </div>

  <div id="gallery" class="section">
    <h2>Figure Gallery (all images)</h2>
    <div class="grid">
      <figure><img src="{{ '/assets/img/project3_DesTreeCostCurve.png' | relative_url }}" alt="DT cost"><figcaption>project3_DesTreeCostCurve.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_DesTreePRC.png' | relative_url }}" alt="DT PRC"><figcaption>project3_DesTreePRC.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_HDFreq.png' | relative_url }}" alt="HD Freq"><figcaption>project3_HDFreq.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_HDFreqSex.png' | relative_url }}" alt="HD Freq by Sex"><figcaption>project3_HDFreqSex.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_KNNCostCurve.png' | relative_url }}" alt="KNN cost"><figcaption>project3_KNNCostCurve.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_KNNPRC.png' | relative_url }}" alt="KNN PRC"><figcaption>project3_KNNPRC.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_LRCostCurve.png' | relative_url }}" alt="LR cost"><figcaption>project3_LRCostCurve.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_LRPRC.png' | relative_url }}" alt="LR PRC"><figcaption>project3_LRPRC.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_NBCostCurve.png' | relative_url }}" alt="NB cost"><figcaption>project3_NBCostCurve.png</figcaption></figure>
      <figure><img src="{{ '/assets/img/project3_NBPRC.png' | relative_url }}" alt="NB PRC"><figcaption>project3_NBPRC.png</figcaption></figure>
    </div>
  </div>

  <div id="code" class="section">
    <h2>Selected Code Snippets</h2>

    <h3>Train/Test Split & Target</h3>
    <div class="code"><pre><code class="language-python">import pandas as pd
from sklearn.model_selection import train_test_split

# Assume df is the cleaned BRFSS dataset with _MICHD as label
y = df["_MICHD"].replace({2:0})        # positive=1 (CHD/MI ever), negative=0
X = df.drop(columns=["_MICHD"])

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.40, random_state=42, stratify=y
)</code></pre></div>
    <p class="muted">Split choice matches the project report (40% test, rs=42). :contentReference[oaicite:29]{index=29}</p>

    <h3>Grid Search (Recall-focused)</h3>
    <div class="code"><pre><code class="language-python">from sklearn.model_selection import GridSearchCV
from sklearn.tree import DecisionTreeClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.neighbors import KNeighborsClassifier

dt = DecisionTreeClassifier(random_state=42)
dt_grid = {"max_depth":[7,9,11,13,15], "max_leaf_nodes":[50,100,150,200]}
dt_cv = GridSearchCV(dt, dt_grid, scoring="recall", cv=10, n_jobs=-1).fit(X_train, y_train)

lr = LogisticRegression(penalty="l1", solver="saga", max_iter=2000)
lr_grid = {"C":[0.5,1,1.4142,2,3]}
lr_cv = GridSearchCV(lr, lr_grid, scoring="recall", cv=10, n_jobs=-1).fit(X_train, y_train)

knn = KNeighborsClassifier()
knn_grid = {"n_neighbors":[3,5,8,11]}
knn_cv = GridSearchCV(knn, knn_grid, scoring="accuracy", cv=10, n_jobs=-1).fit(X_train, y_train)  # avoid k=1 overfit</code></pre></div>
    <p class="muted">Hyperparameter choices & CV strategy per report (recall-first; KNN by accuracy to avoid k=1). :contentReference[oaicite:30]{index=30}</p>

    <h3>Cost-Sensitive Threshold Search</h3>
    <div class="code"><pre><code class="language-python">import numpy as np

def min_cost_threshold(y_true, proba, fn_cost=100, fp_cost=10):
    thr, best_cost, best_t = np.linspace(0,1,501), float("inf"), 0.5
    for t in thr:
        yhat = (proba >= t).astype(int)
        fp = np.sum((yhat==1) & (y_true==0))
        fn = np.sum((yhat==0) & (y_true==1))
        cost = fn_cost*fn + fp_cost*fp
        if cost &lt; best_cost: best_cost, best_t = cost, t
    return best_t, best_cost

# Example for logistic regression:
lr_best = lr_cv.best_estimator_.fit(X_train, y_train)
lr_proba = lr_best.predict_proba(X_test)[:,1]
t_opt, c_min = min_cost_threshold(y_test.values, lr_proba, fn_cost=100, fp_cost=10)</code></pre></div>
    <p class="muted">Report uses FN:100 vs FP:10 and finds optimal thresholds ~0.08–0.09 across models. :contentReference[oaicite:31]{index=31}</p>

    <h3>Precision–Recall Curve (example)</h3>
    <div class="code"><pre><code class="language-python">from sklearn.metrics import precision_recall_curve
import matplotlib.pyplot as plt

prec, rec, th = precision_recall_curve(y_test, lr_proba)
plt.figure(); plt.plot(rec, prec); plt.xlabel("Recall"); plt.ylabel("Precision"); plt.title("LR PRC"); plt.show()</code></pre></div>
  </div>

  <div id="conclusion" class="section">
    <h2>Conclusion & Future Work</h2>
    <p>
      Logistic Regression offered the best recall and lowest cost after cost-aware thresholding,
      aligning with our clinical objective to reduce missed cases. Next steps: calibrate probabilities,
      explore class-imbalance strategies (e.g., focal loss, cost-sensitive learners), and evaluate with
      external validation cohorts to assess generalizability. :contentReference[oaicite:32]{index=32}
    </p>
  </div>
</div>