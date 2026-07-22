# Supply Shock Data Pipeline — Setup Instructions

This notebook models how oil supply disruptions cascade to aviation.
It discovers world events automatically from open data sources, checks
whether they caused a real physical disruption, and shows which countries
and airports are most at risk.

No API keys are required to run it.

---

## What you need before starting

- A computer running **macOS, Windows, or Linux**
- An internet connection (the notebook downloads data on first run)
- About 15 minutes for the one-time setup

---

## Step 1 — Install Python

You need Python 3.9 or newer.

**Check if you already have it:**
Open a terminal (Mac: search for "Terminal"; Windows: search for "Command Prompt") and type:

```
python3 --version
```

If it says `Python 3.9` or higher, skip to Step 2.

If not, download Python from **https://www.python.org/downloads** and install it.
During installation on Windows, check the box that says **"Add Python to PATH"**.

---

## Step 2 — Download the notebook

Go to:

**https://github.com/jemairaa/Code-to-copy**

Click the green **Code** button → **Download ZIP** → unzip the folder somewhere on your computer (e.g. your Desktop).

Or if you have git installed:

```
git clone https://github.com/jemairaa/Code-to-copy.git
```

---

## Step 3 — Install the required packages

Open a terminal, navigate to the folder you just downloaded, and run:

```
pip install pandas requests wbgapi comtradeapicall pycountry python-dotenv pyarrow openpyxl xlrd jupyterlab
```

This installs everything the notebook needs. It may take a few minutes.

If `pip` is not found, try `pip3` instead.

---

## Step 4 — Download the JODI oil data (one manual step)

One data source cannot be downloaded automatically because it requires
agreeing to terms on a website.

1. Go to: **https://www.jodidata.org/oil/database/data-downloads.aspx**
2. Download the file called **"World Database"** (it will be a `.csv` file)
3. Create a folder called `data_cache` inside the Code-to-copy folder
4. Place the downloaded CSV inside that folder and rename it to:

```
jodi_oil_world.csv
```

The notebook will still run without this file — it will just skip the
production data layer and note that the file is missing.

---

## Step 5 — Open the notebook

In your terminal, from inside the Code-to-copy folder, run:

```
jupyter lab
```

A browser window will open. Click on **Supply_Shock_Data_Pipeline.ipynb**
to open the notebook.

---

## Step 6 — Run it

In the Jupyter menu bar click:

**Kernel → Restart Kernel and Run All Cells**

The notebook will run top to bottom, downloading and caching data as it goes.
The first run takes a few minutes. After that, cached data is reused
(each source refreshes on its own schedule — daily, weekly, or monthly
depending on how often that source publishes new data).

The output appears at the bottom: a ranked list of current world events
that may be affecting oil supply, followed by a full trace showing which
countries and airports are most exposed.

---

## What each data source provides

| Source | What it tells the notebook |
|---|---|
| GDELT | Which events are dominating global news right now |
| IMF PortWatch | How many tanker ships are actually moving through each chokepoint |
| EIA (US Energy Dept.) | Oil prices, US crude stockpiles, jet fuel price |
| JODI | How much crude oil each country produces |
| UN Comtrade | Which countries buy crude from which exporters |
| World Bank | Economic data (GDP, oil dependence) per country |
| World Bank Pink Sheet | Monthly commodity prices |
| GPR Index | Geopolitical risk level (how much conflict is in the news) |
| OurAirports | Airport locations and sizes by country |

All sources are free and publicly available. No account or API key is needed.

---

## Troubleshooting

**"Module not found" error** — run the pip install command from Step 3 again.

**"jupyter: command not found"** — try `python3 -m jupyter lab` instead.

**Notebook runs but some sections show no data** — this is normal for
JODI (if you skipped Step 4) or if an external API is temporarily unavailable.
The notebook handles missing data gracefully and will note what is missing.

**Data looks old** — delete the `data_cache` folder and run again to force
a fresh download of everything.

---

## Questions

Contact the analyst who shared this with you, or open an issue at:
https://github.com/jemairaa/Code-to-copy
