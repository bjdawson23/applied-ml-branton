# Branton - Heart Disease Classification Analysis

**Author:** Branton Dawson  
**Date:** November 10, 2025  
**Status:** COMPLETED

## Project Files

- **[ml_classification_branton.ipynb](./ml_classification_branton.ipynb)** - **COMPLETED** - Heart Disease Classification Analysis
- **README.md** - Project documentation and analysis summary

## Project Overview

This notebook demonstrates a comprehensive machine learning classification analysis comparing **Decision Tree** and **Support Vector Machine (SVM)** algorithms for heart disease prediction. The project systematically evaluates both algorithms across three different cardiovascular risk features using the UCI Heart Disease dataset.

### Key Features

- **Dataset**: UCI Heart Disease Dataset (303 patients, 14 features)
- **Target**: Binary classification (heart disease presence/absence)
- **Algorithms**: Decision Tree Classifier vs Support Vector Machine (RBF kernel)
- **Feature Analysis**: Individual feature comparison across three cases
- **Methodology**: Stratified train-test splits with comprehensive performance evaluation

## Analysis Structure

The notebook is organized into six comprehensive sections:

1. **Data Import & Inspection** - Loading and examining the UCI Heart Disease dataset
2. **Data Exploration & Preparation** - EDA, missing value handling, and feature engineering
3. **Feature Selection & Justification** - Strategic selection of three key cardiovascular features
4. **Decision Tree Classification** - Training and evaluating Decision Tree models
5. **Alternative Classifier (SVM)** - Implementing and comparing SVM performance
6. **Final Thoughts & Insights** - Comprehensive analysis and clinical implications

## Feature Cases Analyzed

### Case 1: Age Group (Categorical)
- **Feature**: `age_group` - Binned age categories (29-80 years, 5 groups)
- **Rationale**: Age is a primary cardiovascular risk factor
- **Performance**: 63.3% accuracy (both DT and SVM)

### Case 2: Cholesterol Level (Categorical)  
- **Feature**: `chol_level` - Cholesterol risk categories (normal, borderline, high, very high)
- **Rationale**: Cholesterol directly impacts cardiovascular health
- **Performance**: 60.0% accuracy (both DT and SVM)

### Case 3: Maximum Heart Rate (Continuous)
- **Feature**: `thalach` - Maximum heart rate achieved during exercise
- **Rationale**: Functional indicator of cardiac fitness and capacity
- **Performance**: **Best results** - SVM: 68.3%, Decision Tree: 61.7%

## Key Findings

### Model Performance Summary
- **Overall Winner**: SVM with thalach feature (68.3% accuracy)
- **Most Predictive Feature**: Maximum heart rate (thalach)
- **Algorithm Insights**: SVM excels with continuous features, Decision Trees provide interpretability

### Clinical Implications
- **Functional assessments** (exercise capacity) may be more predictive than traditional risk factors
- **Age remains consistently important** across all modeling approaches
- **Cholesterol alone insufficient** for accurate heart disease prediction

### Technical Insights

- **Feature engineering impact**: Proper binning significantly affects categorical feature performance  
- **Algorithm-feature interaction**: Different algorithms extract varying information from same features
- **Non-linear relationships**: SVM's RBF kernel captures complex physiological patterns better than tree splits

## How to Run the Analysis

### Prerequisites
```bash
# Required Python packages (automatically installed with environment setup)
pandas>=1.5.0
numpy>=1.21.0  
matplotlib>=3.5.0
seaborn>=0.11.0
scikit-learn>=1.1.0
```

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/bjdawson23/applied-ml-branton.git
   cd applied-ml-branton
   ```

2. **Set up the Python environment**
   ```bash
   uv venv
   uv python pin 3.12
   uv sync --extra dev --extra docs --upgrade
   ```

3. **Activate the environment**
   - **Windows (PowerShell)**: `.\.venv\Scripts\activate`
   - **macOS/Linux/WSL**: `source .venv/bin/activate`

4. **Launch Jupyter and open the notebook**
   ```bash
   jupyter notebook notebooks/ml_classification/ml_classification_branton.ipynb
   ```

### Running the Analysis
- Execute cells sequentially from top to bottom
- The notebook automatically downloads the UCI Heart Disease dataset
- Total runtime: approximately 2-3 minutes
- All visualizations and results will be generated inline

## Future Enhancements

### Potential Improvements
- **Multi-feature models**: Combine age, cholesterol, and heart rate simultaneously
- **Advanced algorithms**: Random Forest, Gradient Boosting, Neural Networks
- **Cross-validation**: Implement k-fold CV for more robust performance estimates
- **Feature interactions**: Analyze synergistic effects between cardiovascular risk factors
- **External validation**: Test on independent heart disease datasets

### Clinical Applications
- **Risk stratification**: Develop scoring systems for cardiovascular risk assessment
- **Personalized medicine**: Tailor treatments based on individual risk profiles  
- **Screening protocols**: Optimize which tests to prioritize for early detection
- **Population health**: Identify high-risk demographic groups for targeted interventions

## Dataset Information

**UCI Heart Disease Dataset**
- **Source**: UCI Machine Learning Repository
- **URL**: https://archive.ics.uci.edu/ml/machine-learning-databases/heart-disease/processed.cleveland.data
- **Size**: 303 patients with 14 cardiovascular features
- **Target**: Heart disease presence (0 = no disease, 1+ = disease present)
- **Missing Values**: Minimal (<2% of data) - handled by dropping affected rows

### Dataset Features
The dataset includes comprehensive cardiovascular measurements:
- **Demographics**: age, sex
- **Clinical**: chest pain type (cp), resting blood pressure (trestbps), cholesterol (chol), fasting blood sugar (fbs)
- **Diagnostic**: resting ECG (restecg), exercise-induced angina (exang), ST depression (oldpeak), slope, vessels colored (ca), thalassemia (thal)
- **Functional**: maximum heart rate achieved (thalach)

## Results Summary

| Feature | Algorithm | Accuracy | Key Insight |
|---------|-----------|----------|-------------|
| age_group | Decision Tree | 63.3% | Age remains consistently predictive |
| age_group | SVM | 63.3% | Both algorithms perform equally |
| chol_level | Decision Tree | 60.0% | Cholesterol alone insufficient |
| chol_level | SVM | 60.0% | Categorical binning may be suboptimal |  
| **thalach** | **Decision Tree** | **61.7%** | **Continuous features show promise** |
| **thalach** | **SVM** | **68.3%** | **Best overall performance** |

---

## Original Assignment Context (Archived)

Your Jupyter Notebook must follow a structured format with clearly numbered second-level headings and reflection remarks after each section.

Start your notebook professionally with:

    a single top-level title
    your name (or alias)
    the date
    a brief introduction that describes the problem and the dataset.
    Import the external Python libraries used (e.g., pandas, numpy, matplotlib, seaborn, sklearn).

Tasks to Complete the Assignment

    Create a GitHub repository named ml_classification_yourname.
    Upload your dataset to a data folder in the repository.
    Develop a Jupyter Notebook (classification_yourname.ipynb) structured as outlined above.
    Complete and write reflections for each section as you work.
    Write a README.md summarizing your project, dataset, and findings (see below).
    Review a classmate’s project and provide feedback in peer_review.md (see below).

README.md (Required)

Include a professional README.md that introduces your project. Include:

    a clickable link to your notebook file.
    a clickable link to your your peer review Markdown file.
    Instructions on how to set up your virtual environment and run your notebook locally.

Peer Review (Required)

Review one other GitHub repository and provide feedback on:

    Clarity & Organization (Is the notebook structured and easy to follow?)
    Feature Selection & Justification (Do the chosen features make sense given the objectives?)
    Model Performance & Comparisons (Are the results and comparisons clearly explained?)
    Reflection Quality (Are insights well thought out?)

Submission: Submit a short peer review document in your own repository titled peer_review.md.
The peer review must contain a clickable Markdown link to the notebook (.ipynb) file reviewed along with your personal, well-organized and presented 4-pont review. Provide specifics - both positive and constructive feedback. Suggest improvements where possible and explain why a different choice might be useful as well. Focus on actionable suggestions that the author could realistically implement.
4-point Repository Checklist

Verify your repository contains:

[ ] Jupyter Notebook with proper name, numbered sections and reflections.
[ ] README.md (see above) [ ] Dataset, stored in a data folder.
[ ] Peer Review (peer_review.md).

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

- notebooks/project03 folder:
  - ml03_branton.ipynb - **COMPLETED** - Classification model comparison project
  - README.md - project documentation and performance analysis

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
