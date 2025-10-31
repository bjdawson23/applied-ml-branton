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
  - ml01_branton.ipynb - **COMPLETED** - California Housing Price Prediction
  - README.md - instructions - modify this to present your lab project

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

This project includes demo code.
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

## Project 01: ml01_branton.ipynb - California Housing Price Prediction

**Author:** Branton Dawson  
**Date:** October 23, 2025  
**Status:** COMPLETED

### Project Overview

This notebook demonstrates a complete machine learning regression workflow using the California housing dataset to predict median house prices.

#### Dataset Analysis: California Housing Dataset

- **Data Source**: Scikit-learn's built-in California housing dataset
- **Objective**: Predict median house prices based on housing characteristics
- **Features**: 8 numerical features including median income, house age, average rooms, etc.
- **Target**: Median house value in hundreds of thousands of dollars
- **Sample Size**: 20,640 housing districts in California

#### Technical Implementation

- **Data Loading**: Used `fetch_california_housing()` from scikit-learn
- **Data Exploration**: Comprehensive analysis of features, distributions, and correlations
- **Data Preprocessing**: Feature scaling and data cleaning
- **Model Training**: Linear regression implementation
- **Model Evaluation**: Multiple metrics including R², MAE, and RMSE
- **Visualization**: Scatter plots, histograms, and correlation matrices

#### Key Technical Skills Demonstrated

1. **Data Loading and Exploration**
   - Loading datasets from scikit-learn
   - Pandas DataFrame manipulation
   - Statistical summary analysis

2. **Data Visualization**
   - Matplotlib and Seaborn integration
   - Correlation heatmaps
   - Distribution plots and scatter matrices

3. **Machine Learning Pipeline**
   - Train/test data splitting
   - Linear regression model training
   - Performance evaluation using multiple metrics

4. **Model Performance Evaluation**
   - R-squared (R²): Coefficient of determination
   - Mean Absolute Error (MAE): Average absolute prediction error
   - Root Mean Squared Error (RMSE): Standard deviation of prediction errors

#### Learning Outcomes

- **Regression Analysis**: Understanding of supervised learning for continuous target variables
- **Feature Analysis**: Identifying relationships between housing characteristics and prices
- **Model Evaluation**: Using appropriate metrics to assess regression model performance
- **End-to-End Workflow**: Complete machine learning project from data loading to evaluation

This project serves as a foundation for understanding regression analysis and provides practical experience with the entire machine learning workflow using real-world housing data.

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
