# STAT 4310 Regression Project

**Authors:** Thomas Linden, Louis Mestas, Luis Garcia, Emanuel Padilla, Eugene Kazi, Edgar Pineda

## Contribution Edits
To earn credit for your contribution, please make edits to the `presentation.Rmd` file and include the following comment format in your code where you made changes:

To find issues that need to be resolve search code for the following keywords:

- `NEEDS REVEIW:` 
  - Should include a description of the issue and a proposed solution.
  - Once the issue is resolved, change the keyword to `RESOLVED:`and include a brief description of how the issue was resolved along with the date of resolution and your name.
  - **IF YOU FIND AN ISSUE THAT NEEDS TO BE RESOLVED, PLEASE ADD A COMMENT IN THE CODE WITH THE KEYWORD `NEEDS REVIEW:` AND A DESCRIPTION OF THE ISSUE AND PROPOSED SOLUTION.\
  Again, ONCE THE ISSUE IS RESOLVED, CHANGE THE KEYWORD TO `RESOLVED:` AND INCLUDE A BRIEF DESCRIPTION OF HOW THE ISSUE WAS RESOLVED ALONG WITH THE DATE OF RESOLUTION AND YOUR NAME.**\
- `TODO:` 
  - Should include a description of the task that needs to be completed and should only be assigned by  TLindenIII (Thomas Linden(Project Group Leader)) and/or by louismestas or edgpineda18 via approval of TLindenIII.
  - Once the task is completed, change the keyword to `COMPLETED:` and include a brief description of how the task was completed along with the date of completion and your name.
  - **IF YOU HAVE A TASK THAT NEEDS TO BE COMPLETED, PLEASE ADD A COMMENT IN THE CODE WITH THE KEYWORD `TODO:` AND A DESCRIPTION OF THE TASK and notify TLindenIII, louismestas, or edgpineda18.\
  Again, ONCE THE TASK IS COMPLETED, CHANGE THE KEYWORD TO `COMPLETED:` AND INCLUDE A BRIEF DESCRIPTION OF HOW THE TASK WAS COMPLETED ALONG WITH THE DATE OF COMPLETION AND YOUR NAME.**


A `xaringan` slide presentation covering two applied regression datasets
(**HousePrices** and **CASchools**) plus a finance application using six NYSE
stocks benchmarked against the S&P 500.

---

## Repo structure

```
stat4310-project/
├── presentation.Rmd          # Main slide deck source
├── project-presentation.css  # Custom xaringan theme (required)
├── renv.lock                 # Locked package versions
├── renv/                     # renv scaffolding (auto-generated)
├── .gitignore
└── README.md
```

> **Note:** The `renv/library/` folder is excluded from Git (it can be
> hundreds of MB). Running `renv::restore()` re-installs everything locally
> from `renv.lock`.

---

## Prerequisites

| Requirement | Version |
|---|---|
| R | ≥ 4.2 |
| RStudio | ≥ 2022.07 (recommended) |
| `renv` package | any recent version |

Install `renv` once if you don't have it:

```r
install.packages("renv")
```

---

## Quick start

### 1 — Clone the repo

```bash
git clone https://github.com/<your-username>/stat4310-project.git
cd stat4310-project
```

Or use **File → New Project → Version Control → Git** inside RStudio and
paste the repo URL.

### 2 — Restore all packages

Open the project in RStudio (double-click `stat4310-project.Rproj` if
present, or `File → Open Project`), then in the R console run:

```r
renv::restore()
```

This reads `renv.lock` and installs every package at the exact version used
to build the project. It may take a few minutes the first time.

> **Arch Linux users:** if the `faraway` or `lme4` install fails, you may
> need the Fortran compiler first:
> ```bash
> sudo pacman -S gcc-fortran
> ```

### 3 — Render the slides

In RStudio, open `presentation.Rmd` and click **Knit**, or run:

```r
rmarkdown::render("presentation.Rmd")
```

This will:
1. Pull live close prices from Yahoo Finance (2023–2025) via `quantmod`
2. Run all model-selection, CV, bootstrap, and CAPM code
3. Produce `presentation.html` — open it in any browser

> **Heads-up on live data:** the finance section fetches real-time prices
> each time you knit. Results will update as more 2025 trading days become
> available; minor differences from the original rendered output are expected.

---

## Viewing without running

If you just want to see the slides without installing R:

1. Download `presentation.html` from the repo
2. Open it in any modern browser — no server or R needed

The HTML file is self-contained and includes all plots.

---

## Key packages

| Package | Purpose |
|---|---|
| `xaringan` | Slide rendering |
| `AER` | HousePrices and CASchools datasets |
| `quantmod` + `zoo` | Yahoo Finance data and rolling stats |
| `lmtest` | Breusch-Pagan and Durbin-Watson tests |
| `car` | Regression diagnostics |
| `broom` | Tidy model output |
| `ModelMetrics` | RMSE / MAE helpers |
| `MASS` | `stepAIC()` |

All versions are pinned in `renv.lock`.

---

## Troubleshooting

**`renv::restore()` asks to activate — say yes.**  
renv creates a project-local library so your system packages are not affected.

**Yahoo Finance rate-limit error during knit.**  
Wait a minute and re-knit; `getSymbols()` occasionally hits a throttle on
first use.

**Slides look unstyled.**  
Make sure `project-presentation.css` is in the same folder as
`presentation.Rmd`. The theme file is required for the custom colors and
layout.

**`xaringan` slides open but show a blank first slide.**  
This is normal — the first slide uses `class: center, middle, inverse` which
renders as a dark title card. Press the right arrow to advance.

---

## Reproducing from scratch (no renv)

If you prefer not to use renv, install packages manually:

```r
install.packages(c(
  "xaringan", "AER", "MASS", "car", "lmtest",
  "ModelMetrics", "broom", "knitr", "quantmod", "zoo"
))
```

Then knit `presentation.Rmd` as normal.
