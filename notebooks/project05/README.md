# Project 05: ensemble_branton.ipynb - Ensemble Machine Learning – Wine Quality Classification

**Author:** Branton Dawson  
**Date:** November 20, 2025  
**Status:** COMPLETED

- NOTEBOOK LINK: [Ensemble ML, Wine Quality](https://github.com/bjdawson23/applied-ml-branton/blob/main/notebooks/project05/ensemble_branton.ipynb)

**Project Overview**

This notebook demonstrates ensemble machine learning techniques by classifying wine quality using multiple ensemble algorithms. The project compares Random Forest and Voting Classifier approaches to understand how combining multiple models improves prediction performance on the UCI Wine Quality dataset.

## applied-ml-branton

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

### Dataset Source

We use the Wine Quality Dataset made available by the UCI Machine Learning Repository.

- UCI Repository: <https://archive.ics.uci.edu/ml/datasets/Wine+Quality>

Data originally published by:
P. Cortez, A. Cerdeira, F. Almeida, T. Matos and J. Reis.  
Modeling wine preferences by data mining from physicochemical properties.  
In Decision Support Systems, Elsevier, 47(4):547–553, 2009.

Direct download link to raw csv:
<https://archive.ics.uci.edu/ml/machine-learning-databases/wine-quality/winequality-red.csv>

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

**Note on best practices:**

`uvx` runs the latest version of a tool in an isolated cache, outside the virtual environment.
This keeps the project light and simple, but behavior can change when the tool updates.
For fully reproducible results, or when you need to use the local `.venv`, use `uv run` instead.

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

---

## Project Overview: Ensemble Learning for Wine Quality Classification

This notebook demonstrates ensemble machine learning techniques by predicting wine quality categories using multiple ensemble algorithms. The project systematically compares Random Forest and Voting Classifier approaches to understand how combining multiple models improves classification performance and generalization.

### Objective: Multi-Model Ensemble Analysis

- **Dataset**: UCI Wine Quality (Red Wine) - 1,599 samples with 11 physicochemical features
- **Target Variable**: `quality` (original: 0-10 scale) → simplified to 3 categories: Low (0-4), Medium (5-6), High (7-8)
- **Algorithms**: Random Forest (100 trees), Voting Classifier (Random Forest + Logistic Regression + K-Nearest Neighbors)
- **Evaluation Metrics**: Accuracy, Precision, Recall, F1 Score (weighted average for multi-class)
- **Goal**: Determine which ensemble approach provides best balance between accuracy and generalization

### Feature Set: Wine Physicochemical Properties

The dataset includes 11 input features representing wine chemistry:

1. **fixed acidity** - mostly tartaric acid concentration
2. **volatile acidity** - acetic acid content (vinegar taste indicator)
3. **citric acid** - adds freshness and flavor complexity
4. **residual sugar** - remaining sugar after fermentation
5. **chlorides** - salt content affecting taste
6. **free sulfur dioxide** - microbial protection agent
7. **total sulfur dioxide** - sum of free and bound forms
8. **density** - related to sugar and alcohol content
9. **pH** - acidity level (lower = more acidic)
10. **sulphates** - antioxidant and stabilizer
11. **alcohol** - percent alcohol by volume

All features used in modeling without additional feature engineering or selection.

### Performance Summary - Ensemble Classification Results

| Model | Train Accuracy | Test Accuracy | Train F1 | Test F1 | Accuracy Gap | F1 Score Gap | Performance Notes |
|:------|:---------------|:--------------|:---------|:--------|:-------------|:-------------|:------------------|
| **Random Forest (100)** | 100.00% | **88.75%** | 100.00 | **86.61** | 11.25% | 13.39% | 🏆 **Highest accuracy but overfits** |
| **Voting (RF + LR + KNN)** | 91.71% | 85.94% | 89.94 | 82.81 | **5.78%** | **7.13%** | ✅ **Best generalization** |

#### 🏆 Key Performance Insights

1. **Random Forest**: Achieved highest test accuracy (88.75%) but showed significant overfitting
   - Perfect training scores (100%) indicate memorization of training patterns
   - Large gaps (11.25% accuracy, 13.39% F1) between train/test suggest poor generalization
   - May not perform consistently on completely new wine samples

2. **Voting Classifier**: Better balance between performance and generalization
   - Lower test accuracy (85.94%) but much smaller train-test gaps
   - Heterogeneous ensemble (tree + linear + instance-based) captures diverse patterns

### Technical Accomplishments

- **Ensemble Method Comparison**: Implemented homogeneous (Random Forest) vs. heterogeneous (Voting) ensembles
- **Automatic Data Acquisition**: Built-in dataset download from UCI repository for reproducibility
- **Multi-class Classification**: Transformed 10-point quality scale into 3 balanced categories
- **Comprehensive Evaluation**: Confusion matrices, accuracy, precision, recall, F1 scores for all models
- **Generalization Analysis**: Gap calculations between train and test metrics to detect overfitting
- **Visualization Suite**: Confusion matrix heatmaps and comparative bar charts for model performance

### Key Learning Outcomes & Insights

#### **Overfitting vs. Generalization Trade-off**

1. **High Accuracy Isn't Everything**: Random Forest's 88.75% test accuracy came with 11.25% overfitting gap
2. **Generalization Matters**: Voting Classifier's 5.78% gap suggests more reliable real-world performance
3. **Ensemble Diversity Benefits**: Combining different model types (RF + LR + KNN) reduces individual model biases
4. **Perfect Training Scores Warning**: 100% training accuracy indicates potential memorization, not learning

#### **Algorithm-Specific Insights**

- **Random Forest**: Powerful but prone to overfitting without proper regularization (max_depth, min_samples_split)
- **Voting Classifier**: Soft voting (probability averaging) leverages each model's confidence levels

#### **Classification-Specific Lessons**

1. **Class Imbalance Challenge**: Wine quality follows normal distribution (concentrated around medium ratings)
2. **F1 Score Importance**: More informative than accuracy for imbalanced multi-class problems
3. **Confusion Matrix Insights**: Shows which quality categories are commonly confused
4. **Gap Analysis Value**: Train-test gaps reveal model reliability better than test scores alone

### Challenges Faced & Solutions

- **Class Imbalance**: Fewer low (≤4) and high (≥7) quality samples - **Impact**: Models struggle with extreme categories
- **Feature Selection**: Used all 11 chemistry variables without domain expertise - **Future work**: Feature importance analysis needed
- **Overfitting Detection**: Random Forest achieved perfect training scores - **Solution**: Implemented gap calculations to quantify
- **Model Complexity**: No hyperparameter tuning performed - **Limitation**: Both models used default parameters

### Dataset Challenges Identified

- Subjective human ratings introduce inherent noise
- Normal distribution creates class imbalance (most wines are medium quality)

**Feature**:

- 11 physicochemical features capture wine chemistry comprehensively
- Missing contextual features (grape variety, vintage year, winery, price point)

### Future Improvements & Next Steps

- **Feature Engineering**: Create ratio features (alcohol/sugar, acidity/pH) to capture complex interactions
- **Feature Selection**: Use feature importance analysis to identify most predictive chemistry variables

**Research Extensions:**

1. **White Wine Comparison**: Apply same ensemble methods to white wine dataset
2. **Regression Approach**: Predict exact quality scores (0-10) instead of categories
3. **Feature Importance**: Identify which chemistry variables most influence quality ratings

---
