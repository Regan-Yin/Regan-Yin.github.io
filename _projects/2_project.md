---
layout: page
title: U.S. House Election Data Visualisation Project
description: US Election/Data Analytics/Data Visualisation/Web Scrapping/Web App with Dash/Beautiful Soup/Selenium
img: assets/img/US_Election/us-house.jpg
importance: 3
category: work
related_publications: false
---

<style>
  .proj-wrapper{max-width:1100px;margin:0 auto}
  .lead{font-size:1.05rem;line-height:1.6}
  .badge-pill{display:inline-block;padding:.35rem .6rem;border-radius:2rem;background:#f2f2f2;margin:.15rem .2rem;font-size:.85rem}
  .section{margin:2.2rem 0}
  .code{background:#0b0f19;color:#e8e8e8;border-radius:.6rem;padding:1rem 1.2rem;overflow:auto;font-size:.9rem}
  .kpi{display:flex;gap:1rem;flex-wrap:wrap;margin:.5rem 0 1.25rem}
  .kpi .card{flex:1 1 180px;background:#fafafa;border:1px solid #eee;border-radius:.75rem;padding:.9rem}
  .muted{color:#666}
  figure img{max-width:100%;height:auto;border-radius:.75rem;box-shadow:0 6px 18px rgba(0,0,0,.07)}
  figure figcaption{color:#666;font-size:.9rem;margin-top:.4rem}
  .toc a{display:block;padding:.2rem 0}
  
  /* Adaptive tokens */
  :root{
    --kpi-card-bg: #ffffff;
    --kpi-card-border: #e5e7eb;
    --kpi-muted: #6b7280;
    --badge-bg: rgba(0,0,0,.04);
    --badge-border: rgba(0,0,0,.08);
  }
  [data-theme="dark"]{
    --kpi-card-bg: #0f172a;     /* slate-900 */
    --kpi-card-border: #233047; /* darker border */
    --kpi-muted: #94a3b8;       /* slate-400 */
    --badge-bg: rgba(255,255,255,.08);
    --badge-border: rgba(255,255,255,.12);
  }

  /* KPI cards */
  .kpi{display:flex;gap:1rem;flex-wrap:wrap;margin:.5rem 0 1.25rem}
  .kpi .card{
    flex:1 1 180px;
    background:var(--kpi-card-bg);
    border:1px solid var(--kpi-card-border);
    border-radius:.75rem;
    padding:.9rem;
    box-shadow:0 2px 12px rgba(0,0,0,.06);
    color:var(--global-text-color);
  }
  .kpi .card .muted{color:var(--kpi-muted)}

  /* Tech stack badges */
  .badge-pill{
    display:inline-block;padding:.35rem .6rem;border-radius:2rem;
    background:var(--badge-bg);border:1px solid var(--badge-border);
    margin:.15rem .2rem;font-size:.85rem;color:var(--global-text-color);
  }
</style>

<div class="proj-wrapper">
  <p class="lead">
    <strong>Author:</strong> Regan C.H. Yin &nbsp; | &nbsp; <strong>Special thanks:</strong> Andy Chan, Daniel Lau<br>
    An interactive analytics tool that lets users explore the 2022 U.S. House election at state and district levels.
    It combines robust <em>web scraping</em> (Selenium + BeautifulSoup), <em>data processing</em> (Pandas) and <em>visualisation</em> (Dash + Plotly).
  </p>

  <div class="toc section">
    <h3>Contents</h3>
    <a href="#executive-summary">Executive Summary</a>
    <a href="#stack">Tech Stack & Roles</a>
    <a href="#objectives">Objectives</a>
    <a href="#procedure">Code Writing Procedure (End-to-End)</a>
    <a href="#outcomes">Final Outcomes</a>
    <a href="#reflections">Reflections & Next Steps</a>
    <a href="#run">How to Run Locally</a>
  </div>

  <figure class="section">
    <img src="{{ '/assets/img/US_Election/Capscreen_of_Dash.png' | relative_url }}" alt="US House 2022 interactive dashboard screenshot">
    <figcaption>Interactive Dash app: Choropleth map + party vote distributions + district winners.</figcaption>
  </figure>

  <div id="executive-summary" class="section">
    <h2>Executive Summary</h2>
    <div class="kpi">
      <div class="card"><div class="muted">Scope</div><div><strong>US House 2022</strong></div></div>
      <div class="card"><div class="muted">Total Seats</div><div><strong>435</strong></div></div>
      <div class="card"><div class="muted">Headline</div><div><strong>R 222 · D 213</strong></div></div>
      <div class="card"><div class="muted">Interactivity</div><div><strong>Hover/Filter &amp; Linked Charts</strong></div></div>
    </div>
    <p class="lead">
      The project delivers a clean, performant dashboard to compare party performance, vote distributions and district-level winners.
      It automates data ingestion from public election pages, cleans and aggregates results, then renders them in an
      intuitive interface suitable for analysts and the general public alike.
    </p>
  </div>

  <div id="stack" class="section">
    <h2>Tech Stack &amp; Roles</h2>
    <span class="badge-pill">Python</span>
    <span class="badge-pill">Selenium</span>
    <span class="badge-pill">BeautifulSoup</span>
    <span class="badge-pill">Pandas</span>
    <span class="badge-pill">Dash (JupyterDash)</span>
    <span class="badge-pill">Plotly Express</span>
    <p class="muted mt-2">End-to-end by Regan: scraping, data engineering, visual design, and app integration.</p>
  </div>

  <div id="objectives" class="section">
    <h2>Objectives</h2>
    <ul>
      <li>Provide a user-friendly, interactive view of the 2022 U.S. House election.</li>
      <li>Enable state &amp; district-level comparisons of winners and voting patterns.</li>
      <li>Demonstrate a full pipeline: scraping → cleaning → feature engineering → dashboard.</li>
    </ul>
  </div>

  <div id="procedure" class="section">
    <h2>Code Writing Procedure (End-to-End)</h2>

    <h3>Part I — Web Scraping</h3>
    <p><strong>Libraries:</strong> <code>selenium</code>, <code>bs4</code> (BeautifulSoup), <code>webdriver_manager</code>, <code>pandas</code>.</p>
    <ol>
      <li><strong>Driver setup.</strong> Configure Chrome with lightweight options, initialise <code>webdriver.Chrome()</code>.</li>
      <li><strong>State mapping.</strong> Define a <code>state_dict</code> of full state names → USPS codes.</li>
      <li><strong>Core function.</strong> Implement <code>get_election_data(driver, state)</code>:
        <ul>
          <li>Parse page source via BeautifulSoup.</li>
          <li>Handle two layouts: multi-district vs single-district states.</li>
          <li>Extract <em>district</em>, <em>candidate</em>, <em>party</em>, <em>incumbent</em>, <em>votes</em>, <em>percent</em>.</li>
          <li>Normalise party labels (R/D/Ind./Libertarian/Green).</li>
        </ul>
      </li>
      <li><strong>State enumeration.</strong> Visit the index page to collect the 50 state links, then iterate each state’s House page; click “expand” buttons when present to reveal all candidates.</li>
      <li><strong>Tabular output.</strong> Convert nested lists → <code>DataFrame</code> with columns:
        <em>State</em>, <em>State Code</em>, <em>District</em>, <em>Party</em>, <em>Candidate</em>, <em>Incumbent</em>, <em>Vote</em>, <em>Pct%</em>;
        persist to <code>house.csv</code>.</li>
    </ol>

    <div class="code"><pre><code class="language-python"># sketch of the core scraping pieces
from selenium import webdriver
from bs4 import BeautifulSoup
import pandas as pd

state_dict = {"Alabama":"AL", "Alaska":"AK", ...}

def get_election_data(driver, state):
    soup = BeautifulSoup(driver.page_source, "html.parser")
    result = []
    # handle multi- and single-district layouts, normalise parties & incumbency
    # append rows: [state, state_code, district, party, name, incumbent, votes, pct]
    return result

# build state list from index, loop each state house page, click expand when present
rows = []
for state in state_list:
    driver.get(f"https://www.politico.com/2022-election/results/{state.lower().replace(' ','-')}/house/")
    rows += get_election_data(driver, state)

house = pd.DataFrame(rows, columns=["State","State Code","District","Party","Candidate","Incumbent","Vote","Pct%"])
house.to_csv("house.csv", index=False)</code></pre></div>

    <h3>Part II — Data Cleaning &amp; Feature Engineering</h3>
    <ul>
      <li>Sanitise numeric fields: remove commas; coerce <code>Vote</code> to <code>int</code>, <code>Pct%</code> to <code>float</code> (0–1).</li>
      <li>For each state: compute <em>Total Seats</em>, <em>Total Votes</em>, <em>Won Seats</em> (Republican seat count), party vote sums, and <em>Rep. Won Seats %</em>; infer <em>Won Party</em>.</li>
      <li>Output an aggregated <code>seat_won</code> table for the map + summary charts.</li>
    </ul>

    <div class="code"><pre><code class="language-python">import pandas as pd
house = pd.read_csv("house.csv")
house["Vote"] = pd.to_numeric(house["Vote"].str.replace(",",""), errors="coerce").dropna().astype(int)
house["Pct%"] = house["Pct%"].str.rstrip("%").astype(float)/100.0

seat_rows = []
for (state, code), g in house.groupby(["State","State Code"]):
    total_seats = g["District"].nunique()
    total_votes = g["Vote"].sum()
    won_seats = sum(g.groupby("District").apply(lambda x: x.loc[x["Pct%"].idxmax(),"Party"])=="Republican")
    republican_votes = g.loc[g["Party"]=="Republican","Vote"].sum()
    democratic_votes = g.loc[g["Party"]=="Democratic","Vote"].sum()
    libertarian_votes = g.loc[g["Party"].str.contains("Libertarian", na=False),"Vote"].sum()
    seat_rows.append({
        "State":state,"State Code":code,"Total Seats":total_seats,"Total Votes":total_votes,
        "Won Seats":won_seats,"Republican Votes":republican_votes,"Democratic Votes":democratic_votes,
        "Libertarian Votes":libertarian_votes,"Rep. Won Seats %":round(won_seats/total_seats*100,2),
        "Won Party":"Republican" if won_seats > total_seats/2 else "Democratic"
    })
seat_won = pd.DataFrame(seat_rows)</code></pre></div>

    <h3>Part III — Dash App (Map + Linked Charts)</h3>
    <ul>
      <li><strong>Layout:</strong> Title, KPI line (435 seats; R 222 / D 213), USA choropleth (state code), and two right-hand panels:
        party vote distribution &amp; district winner bars, both responding to map hover.</li>
      <li><strong>Top/Bottom 25:</strong> Radio selector renders ranked bar charts for % of Republican seats.</li>
      <li><strong>Callbacks:</strong> one for map hover → updates two panels; one for the Top/Bottom toggle.</li>
    </ul>

    <div class="code"><pre><code class="language-python">from jupyter_dash import JupyterDash
from dash import html, dcc, Input, Output
import plotly.express as px

app = JupyterDash(__name__)
app.layout = html.Div([...])  # map + linked charts + toggle

@app.callback(
    [Output("choropleth_map","figure"), Output("bar_chart","figure"), Output("district_bar_chart","figure")],
    Input("choropleth_map","hoverData")
)
def update_panels(hover):
    # build map from seat_won; when hovering a state, slice seat_won & house
    # return: map fig, party vote bar, district winner bar
    ...

@app.callback(Output("top-bottom-25-bar-chart","figure"), Input("toggle-chart","value"))
def update_top_bottom(sel):
    # select nlargest/nsmallest on 'Rep. Won Seats %', render bar chart
    ...</code></pre></div>
  </div>

  <div id="outcomes" class="section">
    <h2>Final Outcomes</h2>
    <ul>
      <li>Fully working, interactive dashboard with linked views (map ↔ state &amp; district panels).</li>
      <li>Cleaned dataset (<code>house.csv</code>) and engineered summary table (<code>seat_won</code>).</li>
      <li>Insight surfaces: party dominance by state, competitiveness, and distribution of winners across districts.</li>
    </ul>
  </div>

  <div id="reflections" class="section">
    <h2>Reflections &amp; Next Steps</h2>
    <p><strong>What went well:</strong> Reliable scraping across heterogeneous layouts; concise visual grammar; responsive callbacks.</p>
    <p><strong>Challenges:</strong> Dynamic pages &amp; sporadic missing party tags required defensive parsing; hover-driven UX needed careful defaults.</p>
    <p><strong>Roadmap:</strong> Add Senate/Presidential modules; deploy Dash app to a managed host; integrate trendlines and forecasting.</p>
  </div>

  <div id="run" class="section">
    <h2>How to Run Locally</h2>
    <ol>
      <li>Create and activate a Python 3.10+ environment.</li>
      <li><code>pip install selenium webdriver-manager beautifulsoup4 pandas jupyter-dash dash plotly</code></li>
      <li>Run the scraper to produce <code>house.csv</code>, then start the Dash app (JupyterDash or pure Dash).</li>
      <li>Open the served URL (e.g., <code>http://127.0.0.1:805x</code>).</li>
    </ol>
  </div>

</div>