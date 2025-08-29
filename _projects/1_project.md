---
layout: page
title: Detecting Insider Signals - Multi-Modal Analysis of Executive Behavior in Earnings Calls
description: NLP/FinBert/WhisperX/Business Analysis/Big Data/Machine Learning
img: assets/img/InsiderTrading.png
importance: 1
category: work
related_publications: false
---

<p><strong>Author:</strong> Regan Yin<br>
<strong>Acknowledgment:</strong> Special thanks to Prof. Yi Yang (HKUST ISOM) for supporting the FinBERT fine-tuning and providing valuable model insights.</p>
<hr>
<h2>Project Overview</h2>
<p>This repository presents a multi-modal analytical framework for evaluating executive communication during earnings calls. The system integrates audio processing, sentiment classification, and stock price analysis to uncover behavioral signals that may correlate with abnormal stock movements.</p>
<p>The pipeline incorporates:</p>
<ul>
  <li>Audio transcription using Whisper.cpp</li>
  <li>Financial sentiment extraction using FinBERT (fine-tuned)</li>
  <li>Abnormal return computation via event study methodology</li>
  <li>Statistical and visual analysis via Dash</li>
</ul>
<hr>
<h2>Directory Structure</h2>
<pre><code>Sentiment_Analysis_Models/
├── earning_call_auto_downloader/
│   ├── auto_downloader.py
│   └── audio/
│
├── FinBERT_Project/
│   ├── analyze_calls.py
│   ├── dash_app.py
│   ├── metadata_update.py
│   ├── metadata.json
│   ├── transcript/
│   └── report/
│       ├── sentiment_summary.csv
│       ├── event_study.csv
│       ├── price_change.csv
│       ├── corr_heatmap.jpg
│       ├── scatter_with_reg.jpg
│       ├── event_study_plot.jpg
│       ├── classification_report.txt
│       └── granger.txt
│
├── whisper.cpp/
│   ├── build/bin/
│   │   ├── whisper-cli
│   │   └── batch_transcribe.sh
│   ├── audio_input/
│   ├── transcripts/
│   └── models/
│
├── README_Whisper.md
└── README.md
</code></pre>
<hr>
<h2>Environment Setup</h2>
<h3>Install Python dependencies</h3>
<pre><code class="language-bash">pip install -r requirements.txt
</code></pre>
<p>Required packages include:</p>
<ul>
  <li>torch</li>
  <li>transformers</li>
  <li>pandas</li>
  <li>numpy</li>
  <li>yfinance</li>
  <li>statsmodels</li>
  <li>scikit-learn</li>
  <li>plotly</li>
  <li>dash</li>
</ul>
<hr>
<h2>Whisper.cpp Setup (macOS/Linux)</h2>
<p>Install dependencies:</p>
<pre><code class="language-bash">brew install cmake ffmpeg git
</code></pre>
<p>Clone and build:</p>
<pre><code class="language-bash">git clone https://github.com/ggerganov/whisper.cpp
cd whisper.cpp
cmake -B build
cmake --build build --config Release
</code></pre>
<p>Download the model:</p>
<pre><code class="language-bash">sh ./models/download-ggml-model.sh small.en
</code></pre>
<p>Place audio files into <code>audio_input/</code>, then run:</p>
<pre><code class="language-bash">cd build/bin
./batch_transcribe.sh
</code></pre>
<p>Output transcripts will be saved in <code>transcripts/</code>.</p>
<hr>
<h2>Workflow Execution</h2>
<h3>Step 1: Download Audio and Market Data</h3>
<pre><code class="language-bash">cd earning_call_auto_downloader
python auto_downloader.py
</code></pre>
<p>Downloads earnings call recordings (if available) and T-1 to T+1 historical prices.</p>
<h3>Step 2: Update Metadata</h3>
<pre><code class="language-bash">cd ../FinBERT_Project
python metadata_update.py
</code></pre>
<p>Automatically updates <code>metadata.json</code> using the transcript filenames.</p>
<h3>Step 3: Run Sentiment Analysis and Event Study</h3>
<pre><code class="language-bash">python analyze_calls.py
</code></pre>
<p>This script:</p>
<ul>
  <li>Applies FinBERT to each transcript</li>
  <li>Outputs sentiment scores (<code>sentiment_summary.csv</code>)</li>
  <li>Computes CAR and returns (<code>event_study.csv</code>, <code>price_change.csv</code>)</li>
  <li>Outputs supporting plots and statistical results in <code>report/</code></li>
</ul>
<h3>Step 4: Launch Dashboard</h3>
<pre><code class="language-bash">python dash_app.py
</code></pre>
<p>Access the interactive dashboard via browser:</p>
<ul>
  <li>Sentiment correlation scatter plots</li>
  <li>CAR trends by company</li>
  <li>Heatmaps and diagnostics</li>
</ul>
<hr>
<h2>Extending the Project</h2>
<h3>Add More Companies</h3>
<ol>
  <li>Place additional audio files in <code>audio_input/</code></li>
  <li>Transcribe with <code>batch_transcribe.sh</code></li>
  <li>Move transcript <code>.json</code> files to <code>FinBERT_Project/transcript/</code></li>
  <li>Run <code>metadata_update.py</code> to refresh metadata</li>
  <li>Run <code>analyze_calls.py</code> to recompute sentiment and returns</li>
</ol>
<h3>Full-Market Automation</h3>
<ul>
  <li>Add a list of tickers to <code>auto_downloader.py</code></li>
  <li>Implement batch crawling scripts (e.g., using SEC EDGAR or APIs)</li>
  <li>Store metadata/results in a structured database for scaling</li>
</ul>
<hr>
<h2>Outputs</h2>
<p>All results are saved in <code>FinBERT_Project/report/</code>:</p>
<ul>
  <li><code>sentiment_summary.csv</code> – FinBERT sentiment results</li>
  <li><code>event_study.csv</code> – Event study abnormal returns</li>
  <li><code>price_change.csv</code> – Daily changes (T+0, T+1)</li>
  <li><code>classification_report.txt</code> – Logistic regression summary</li>
  <li><code>granger.txt</code> – Granger causality test output</li>
  <li><code>*.jpg</code> – Visualizations (correlation heatmap, CAR chart, scatter plot)</li>
</ul>
<hr>
<h2>Limitations</h2>
<ul>
  <li>Sample size is currently limited; expansion is required for significance</li>
  <li>Logistic regression is underpowered due to sparse training labels</li>
  <li>Sentiment detection may misclassify Q&A segments without speaker identification</li>
</ul>
<hr>
<h2>Future Improvements</h2>
<ul>
  <li>Integrate diarization via Whisper <code>-tdrz</code> models</li>
  <li>Extract audio features (pitch, pauses) using Librosa</li>
  <li>Ensemble FinBERT with other financial sentiment models</li>
  <li>Support parallel transcript processing with multiprocessing</li>
  <li>Export results to SQL or NoSQL backends</li>
</ul>
<hr>
<h2>Citation</h2>
<pre><code>Yin, R. (2025). Multi-Modal Sentiment Analysis on Earnings Calls.
</code></pre>
