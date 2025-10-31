# applied-ml-branton

> Use this repo to start a professional Python project.

- Additional instructions: See the [pro-analytics-02](https://denisecase.github.io/pro-analytics-02/) guide.
- Project organization: [STRUCTURE](./STRUCTURE.md)
- Build professional skills:
  - **Environment Management**: Every project in isolation
  - **Code Quality**: Automated checks for fewer bugs
  - **Documentation**: Use modern project documentation tools
  - **Testing**: Prove your code works
  - **Version Control**: Collaborate professionally

---

## About this Repository

Starter files for the example labs:

- notebooks/example01 folder
- notebooks/example02 folder

## Folders for Projects

Each project will be completed in its own folder.

- notebooks/project01 folder:
  - ml01.ipynb - COMPLETE THIS
  - ml01.py - working script with just the code
  - README.md - instructions - modify this to present your lab project

- notebooks/project02 folder:
  - ml01_branton.ipynb - **COMPLETED** - Comprehensive data analysis project
  - README.md - project documentation and analysis summary

---

## WORKFLOW 1. Set Up Machine

Proper setup is critical.
Complete each step in the following guide and verify carefully.

- [SET UP MACHINE](./SET_UP_MACHINE.md)

---

## WORKFLOW 2. Set Up Project

After verifying your machine is set up, set up a new Python project by copying this template.
Complete each step in the following guide.

- [SET UP PROJECT](./SET_UP_PROJECT.md)

It includes the critical commands to set up your local environment (and activate it):

```shell
uv venv
uv python pin 3.12
uv sync --extra dev --extra docs --upgrade
uv run pre-commit install
uv run python --version
```

**Windows (PowerShell):**

```shell
.\.venv\Scripts\activate
```

**macOS / Linux / WSL:**

```shell
source .venv/bin/activate
```

---

## WORKFLOW 3. Daily Workflow

Please ensure that the prior steps have been verified before continuing.
When working on a project, we open just that project in VS Code.

### 3.1 Git Pull from GitHub

Always start with `git pull` to check for any changes made to the GitHub repo.

```shell
git pull
```

### 3.2 Run Checks as You Work

This mirrors real work where we typically:

1. Update dependencies (for security and compatibility).
2. Clean unused cached packages to free space.
3. Use `git add .` to stage all changes.
4. Run ruff and fix minor issues.
5. Update pre-commit periodically.
6. Run pre-commit quality checks on all code files (**twice if needed**, the first pass may fix things).
7. Run tests.

In VS Code, open your repository, then open a terminal (Terminal / New Terminal) and run the following commands one at a time to check the code.

```shell
git pull
uv sync --extra dev --extra docs --upgrade
uv cache clean
git add .
uvx ruff check --fix
uvx pre-commit autoupdate
uv run pre-commit run --all-files
git add .
uv run pytest
```

NOTE: The second `git add .` ensures any automatic fixes made by Ruff or pre-commit are included before testing or committing.
Running `uv run pre-commit run --all-files` twice may be helpful if the first time doesn't pass. 

<details>
<summary>Click to see a note on best practices</summary>

`uvx` runs the latest version of a tool in an isolated cache, outside the virtual environment.
This keeps the project light and simple, but behavior can change when the tool updates.
For fully reproducible results, or when you need to use the local `.venv`, use `uv run` instead.

</details>

### 3.3 Build Project Documentation

Make sure you have current doc dependencies, then build your docs, fix any errors, and serve them locally to test.

```shell
uv run mkdocs build --strict
uv run mkdocs serve
```

- After running the serve command, the local URL of the docs will be provided. To open the site, press **CTRL and click** the provided link (at the same time) to view the documentation. On a Mac, use **CMD and click**.
- Press **CTRL c** (at the same time) to stop the hosting process.

### 3.4 Execute

This project includes demo code and completed analysis notebooks.
Run the demo Python modules to confirm everything is working.

In VS Code terminal, run:

```shell
uv run python notebooks/project01/ml01.py
```

A new window with charts should appear. Close the window to finish the execution.
If this works, your project is ready! If not, check:

- Are you in the right folder? (All terminal commands are to be run from the root project folder.)
- Did you run the full `uv sync --extra dev --extra docs --upgrade` command?
- Are there any error messages? (ask for help with the exact error)

## Project 02: ml01_branton.ipynb - Comprehensive Data Analysis

**Author:** Branton Dawson  
**Date:** October 30-31, 2025  
**Status:** COMPLETED

### Project Overview

This notebook demonstrates comprehensive data analysis techniques using two datasets:

#### Primary Analysis: Titanic Dataset

- **Data Exploration**: Loaded and explored 891 passenger records with 15 features
- **Missing Value Handling**: Implemented median imputation for age, mode imputation for embark_town
- **Feature Engineering**: Created family_size feature, converted categorical variables to numeric
- **Visualization**: Generated scatter matrices, histograms, and count plots for pattern analysis
- **Class Imbalance Analysis**: Identified 38% survival vs 62% mortality, gender imbalance (65% male)
- **Train/Test Splitting**: Compared basic vs stratified splitting methods
- **Key Findings**: 74.2% female survival vs 18.9% male survival rate

#### Bonus Analysis: Pima Indians Diabetes Dataset

- **Dataset**: 768 patient records with 9 medical features
- **Feature Analysis**: Detailed explanation of medical measurements and their significance
- **Class Distribution**: 65.1% no diabetes, 34.9% diabetes
- **Feature Engineering**: Created age ranges and BMI categories
- **Splitting Comparison**: Demonstrated superior performance of stratified splitting (0.2% deviation vs 2.8%)

### Technical Accomplishments

- **Data Preprocessing**: Missing value imputation, categorical encoding
- **Exploratory Data Analysis**: Statistical summaries, correlation analysis, visualization
- **Feature Engineering**: Created meaningful derived features
- **Model Preparation**: Proper train/test splitting with stratification
- **Class Imbalance Handling**: Identified and addressed distribution issues
- **Comparative Analysis**: Side-by-side evaluation of different datasets and methods

### Key Learning Outcomes

1. **Stratified Sampling**: Maintains class proportions better than random splitting
2. **Feature Importance**: Gender, class, and fare are strongest Titanic survival predictors
3. **Medical Data Analysis**: Glucose and BMI are primary diabetes risk factors
4. **Data Quality**: Proper handling of missing values is crucial for model performance
5. **Visualization**: Effective plots reveal hidden patterns in data distributions

## Update this README as you work

Add commands to run additional scripts as you work through the course (update the path and file name as needed).

---

### 3.5 Git add-commit-push to GitHub

Anytime we make working changes to code is a good time to git add-commit-push to GitHub.

1. Stage your changes with git add.
2. Commit your changes with a useful message in quotes.
3. Push your work to GitHub.

```shell
git add .
git commit -m "describe your change in quotes"
git push -u origin main
```

This will trigger the GitHub Actions workflow and publish your documentation via GitHub Pages.

### 3.6 Modify and Debug

With a working version safe in GitHub, start making changes to the code.

Before starting a new session, remember to do a `git pull` and keep your tools updated.

Each time forward progress is made, remember to git add-commit-push.
