# Genre and Platform as Predictors of North American Video Game Sales

This repository follows a semester-long data science project from question to model: a research proposal, a cleaned and audited working dataset, a visualization study with honest and deliberately misleading plots.

> **Research question:** Can a game's genre and platform be used to predict its North American sales, among VGChartz-tracked titles released through 2020 on platforms with at least 100 tracked titles?

---

## Key Findings So Far

- **Platform separates titles more than genre does.** Median North American sales range from 0.04M (PC) to 0.42M (Atari 2600) across platforms, compared with 0.06M to 0.15M across genres.
- **Each is a weak predictor on its own.** The middle 50% of titles in nearly every genre and platform overlap heavily, so knowing a game's category narrows down its sales only a little.
- **Sales are heavily right-skewed.** On a log scale, North American sales form a single, roughly symmetric bell centered at the median (0.12M), while a few blockbusters pull the mean up to 0.27M.
- **Critic scores are too incomplete to use.** Only 29.8% of titles have a critic score, so `Critic_Score` was ruled out as a control variable.
- **Early years reflect selection bias.** Before 1995, only a handful of titles per year were tracked, mostly hits, which inflates their medians. From 1995 to 2015, median sales per title stay stable.

---

## Data

| | |
|---|---|
| **Primary dataset** | [Video Games Sales (VGChartz)](https://www.kaggle.com/datasets/lamskdna/video-games-sales/data) on Kaggle, Apache 2.0: 64,016 rows × 12 columns |
| **Secondary dataset** | [Video Games Sales as at 22 Dec 2016](https://www.kaggle.com/datasets/sidtwr/videogames-sales-dataset) on Kaggle, used in the Phase 2 join exercise |
| **Target** | `NA_Sales`: North American sales, in millions of units |
| **Features** | `Genre`, `Platform` |

### From raw data to working dataset

| Step | Phase | Rows |
|---|---|---|
| Raw VGChartz export | 1 | 64,016 |
| Converted sales columns from text to numbers; dropped rows with no `NA_Sales` (51,659) | 2 | 12,357 |
| Dropped duplicate `Title + Platform` keys (9) | 2 | **12,348** → `phase2_working.csv` |
| Dropped leakage columns: `Total_Sales` (computed from the target), and `JP_Sales`, `PAL_Sales` and `Other_Sales` (recorded at the same time as the target) | 3 | 12,348 |
| Dropped 7 genres with fewer than 100 titles (155 titles) | 3 | 12,193 |
| Dropped 11 platforms with fewer than 100 titles (162 titles), including the Wii U, which fell to 94 after the genre filter | 3 | **12,031** → `phase3_working.csv` |

The final working dataset has **13 genres and 18 platforms**, each with at least 100 tracked titles.

---

## Repository Structure

```
CS577-Project/
├── Phase 1/                                       # Dataset & research proposal
│   └── GroupSix_Aaron_Sergio_Phase1.pdf
├── Phase 2/                                       # Data preparation, joins, audit, cleaning
│   ├── GroupSix_Aaron_Sergio_Phase2.ipynb
│   ├── VideoGames_Sales.csv                       # Raw primary dataset
│   ├── Video_Games_Sales_as_at_22_Dec_2016.csv    # Raw secondary dataset
│   └── phase2_working.csv                         # Phase 2 working dataset
├── Phase 3/                                       # Visualization and model case
│   ├── Group6_Aaron_Sergio_Phase3.ipynb
│   └── phase3_working.csv                         # Phase 3 working dataset
├── LICENSE
└── README.md
```

---

## Project Phases

| Phase | Focus | Status |
|---|---|---|
| **1** | Dataset and research proposal: question, source, planned EDA, anticipated challenges | ✅ Complete |
| **2** | Data preparation: second-dataset join, structure / granularity / scope / temporality / faithfulness audit, cleaning, corruption stress test | ✅ Complete |
| **3** | Visualization: eight-plot portfolio, plot upgrades, misleading-plot "lie detector," hero figure, model case | ✅ Complete |

### Inside the Phase 3 notebook

| Part | Contents |
|---|---|
| 0 | What changed from Phase 2: the question's scope and the dataset cleaning |
| 1 | Composite portfolio of eight plots, coverage table, and two upgraded plots |
| 2 | Two deliberately misleading plots, their honest fixes, and a plot-review checklist |
| 3 | Hero figure answering the research question |
| 4 | The model case: target, shape evidence, linear vs. forest, leakage, baseline |
| 5 | An honest data story |

---

## How to Run

**Requirements:** Python 3 with Jupyter.

```bash
pip install pandas numpy matplotlib seaborn jupyter
pip install cufflinks "plotly<6"   # used only by the Phase 2 notebook
```

**Run order:**

1. **Phase 2:** open `Phase 2/GroupSix_Aaron_Sergio_Phase2.ipynb` and run all cells. It reads the two raw CSVs and writes `phase2_working.csv`.
2. **Phase 3:** open `Phase 3/Group6_Aaron_Sergio_Phase3.ipynb` from inside the `Phase 3/` folder and choose **Kernel → Restart & Run All**. It reads `../Phase 2/phase2_working.csv`, rebuilds `phase3_working.csv` in Part 0, and uses it for every later part.

Both working datasets are already committed, so each notebook can also be run on its own.

---

## Tools

Python · pandas · NumPy · Matplotlib · seaborn · Jupyter

---

## Team

**Aaron:** Wrote the detection attempt for Sergio's misleading plot in the Part 2 swap, and help with the coverage table, synthesis, and the plot-review checklist. He build the model case in Part 4, covering the target and task type, the shape evidence, the linear-versus-forest decision, and the baseline. He also wrote the honest data story in Part 5.

**Sergio:** Cleaned the Phase 3 working dataset in Part 0 and documented each change, and help with the coverage table, systhesis, and the plot-review checklist. He rebuild the two weakest plots, and wrote the detection attempt for Aaron's misleading plot. He also designed the hero figure in Part 3, with it's caption and the principle table. 

---

## AI Usage

Claude was used to correct the syntax in the plotting of the before and after weakest plot in the two panel stack format in part 1B.

---
