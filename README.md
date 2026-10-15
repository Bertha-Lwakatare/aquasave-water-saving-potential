# 💧 AquaSave — Making potential water savings resonate with oneself

## Project Overview

AquaSave analyses real shower water consumption and shows how much water could be saved with simple, efficient shower habits. It uses anonymised meter data from the **HSB Living Lab**: it detects individual shower events, compares the observed consumption (status quo) with an efficient AquaSave scenario, and turns the difference into something people can picture.

Instead of abstract litres or cubic metres, the app translates saved water into everyday comparisons, such as kilometres run, cakes baked or days of drinking water for a child. Users pick the comparison that speaks to them most.

The analysis lives in a Jupyter notebook. The results are wrapped in a custom-styled **Gradio** web app that can be shared through a temporary public link for demos and presentations.

## What This Project Offers

- **Data-based shower analysis:** shower events are reconstructed from 10-minute meter readings and split by warm and cold water, time of day and bathroom type.
- **An efficient shower baseline:** the AquaSave scenario combines flow reduction, a shower length limit and a water cap per shower, with comfort minimums so no shower is cut unrealistically short.
- **Personal estimates:** users can work with the AquaSave data or enter their own shower length and flow.
- **Default or custom scenarios:** keep the study values or set your own with sliders.
- **Savings "spoken in your language":** results are converted into relatable comparisons per day, week, month or year.
- **A polished app:** a three-step Gradio interface with its own theme, logo and light/dark mode support.

## Technologies Used

- Python
- pandas, NumPy (data preparation and event detection)
- Matplotlib, SciPy (visualisation and distributions)
- Gradio (web app, custom theme and CSS)
- Pillow (logo processing)
- Jupyter Notebook

## How It Works

1. **Load and clean the data**
   - Reads the HSB Living Lab water consumption data (anonymised).
   - Keeps rows without an apartment number, because they contain a large share of shower consumption. The analysis is therefore based on events rather than apartments.

2. **Detect shower events**
   - Readings in the same room belong to one shower; a new event starts after a gap of more than 10 minutes.
   - Each event gets its total litres, warm and cold litres, estimated duration and time of day.

3. **Build the AquaSave scenario**
   - Applies a flow reduction, a shower length limit and a water cap per shower.
   - Keeps the number of showers the same; only the water per shower goes down.
   - Never reduces a shower below a minimum amount of water or a minimum length.

4. **Compare status quo and AquaSave**
   - Calculates the water saved per shower, per period of the day and in total.
   - Exports the results (`showers.csv`, `app_meta.json`, `lenses.csv`) for the app.

5. **Launch the app**
   - **Page 1:** pick a comparison topic.
   - **Page 2 – Shower details:** describe your showers and household.
   - **Page 3 – Shower Optimisation:** choose the default AquaSave scenario or set your own values.
   - **Page 4 – Results:** status quo vs. AquaSave and your savings in everyday terms.

## Example: Results Page

![AquaSave results page](figures/AquaSave%20Result.png)

## Live Demo

🔗 **Try the app:** [Open AquaSave](https://547aeb3ad7998f2462.gradio.live)

Note: The public link is temporary (about one week) and only works while the app is running.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Bertha-Lwakatare/aquasave-water-saving-potential.git
cd aquasave-water-saving-potential
```

### 2. Create a virtual environment and install the dependencies

```bash
python -m venv .aquasave

# Windows (PowerShell)
.aquasave\Scripts\Activate.ps1

pip install -r requirements.txt
```

### 3. Add your API key

The key is not included in this repository, so you need to use your own. In the root of the project, create a file named `.env` containing:

```
GROQ_API_KEY=<insert your key here>
```

Replace the placeholder with your own value, with no quotes and no spaces around the `=`.

### 4. Run the notebook

Open `AquaSave_script.ipynb` in Jupyter or VS Code and run all cells. The notebook cleans the data, detects the shower events, builds the AquaSave scenario and exports the files the app needs.

### 5. Start the app

Gradio prints a local address and a public `gradio.live` link.

## Limitations

- Durations are estimated from 10-minute meter readings, so short showers can't be measured precisely.
- Some shower rooms only have a cold-water sensor; their warm water is set to 0. It is unclear if they have no hot water sensor or no hot water supply at all.
- Groups with fewer than 30 showers use factors instead of their own averages, which makes those estimates less precise.
- The data comes from a single living lab, so results may differ for other buildings and households.
- The everyday comparisons are approximations based on published sources and are meant to illustrate, not to be exact.

## Data

The analysis uses the anonymised **HSB Living Lab water consumption dataset**. The raw data is not included in this repository.

## Conclusion

AquaSave shows how real consumption data can be turned into a tool that makes water savings tangible. Detecting shower events, building a realistic efficient baseline and translating the savings into everyday comparisons helps people see what small changes in their shower habits could achieve. Future improvements could include more buildings, seasonal patterns and the energy saved by using less hot water. Validation is also essential before increasing the scope to relating water savings to monetary comparisons (which people may be more motivated by)
