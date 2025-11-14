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

## Project 04: ml04_branton.ipynb - Regression Analysis for Fare Prediction

**Author:** Branton Dawson  
**Date:** November 13, 2025  
**Status:** COMPLETED

### Project Overview

This notebook demonstrates comprehensive regression modeling techniques by predicting Titanic passenger fares using multiple algorithms and feature combinations. The project systematically compares Linear Regression, Polynomial Regression, Ridge Regression, and Elastic Net models to understand continuous target prediction challenges.

#### Objective: Multi-Model Regression Analysis

- **Dataset**: Titanic passenger data (891 passengers after cleaning)
- **Target Variable**: `fare` (continuous - amount paid for journey)
- **Algorithms**: Linear Regression, Polynomial Regression (degrees 3 & 6), Ridge Regression, Elastic Net
- **Feature Cases**: Four different feature combinations tested across all models
- **Goal**: Determine optimal model-feature combinations for fare prediction and understand regression complexity trade-offs

#### Feature Engineering & Selection

#### Case 1: Single Demographic Feature

- **Features**: `age` (continuous numerical)
- **Rationale**: Test if passenger age correlates with fare (premium accommodations for older passengers)
- **Challenge**: Age alone shows weak correlation with fare pricing

#### Case 2: Social Context Feature

- **Features**: `family_size` (engineered: sibsp + parch + 1)
- **Rationale**: Family groups might pay different rates or get group discounts
- **Challenge**: Individual booking decisions override family size patterns

#### Case 3: Combined Demographic Features

- **Features**: `age` + `family_size` (multi-dimensional)
- **Rationale**: Combine life stage and social context for richer prediction
- **Challenge**: More features don't always improve simple linear relationships

#### Case 4: Socioeconomic Indicators

- **Features**: `sex` + `class` (gender + passenger class)
- **Rationale**: Direct socioeconomic factors that determined 1912 ticket pricing
- **Analysis**: Class structure (1st > 2nd > 3rd) and gender-based social patterns

### Performance Summary - Regression Results

| Model Type | Features | R² Score | RMSE | MAE | Performance Notes |
|------------|----------|----------|------|-----|-------------------|
| **Linear Regression** | age | ~0.01 | ~49.5 | ~35.2 | Poor - age weakly predicts fare |
| | family_size | ~0.02 | ~49.3 | ~35.1 | Minimal improvement over age alone |
| | age + family_size | ~0.03 | ~49.1 | ~34.9 | Slight improvement but still weak |
| | **sex + class** | **~0.55** | **~33.5** | **~23.8** | 🏆 **Best performance - class drives fare** |
| **Ridge Regression** | age | ~0.01 | ~49.5 | ~35.2 | No overfitting to regularize |
| **Elastic Net** | age | ~0.01 | ~49.5 | ~35.2 | Regularization provides no benefit |
| **Polynomial (degree 3)** | age | ~0.02 | ~49.2 | ~35.0 | Minimal improvement over linear |
| **Polynomial (degree 6)** | age | ~0.01 | ~49.7 | ~35.4 | ⚠️ **Overfitting - worse than cubic** |

#### 🏆 Performance Rankings

1. **Linear Regression (sex + class)**: R² ~0.55 - Clear winner, captures fare structure
2. **Polynomial degree 3**: R² ~0.02 - Marginal improvement for age-based models
3. **All other combinations**: R² <0.03 - Poor performance, weak feature relationships

### Technical Accomplishments

- **Comprehensive Model Comparison**: Implemented 4 different regression algorithms
- **Regularization Analysis**: Tested Ridge and Elastic Net for overfitting prevention
- **Polynomial Complexity Study**: Compared degree 3 vs degree 6 polynomial features
- **Feature Impact Assessment**: Systematic evaluation of demographic vs. socioeconomic features
- **Overfitting Detection**: Identified when model complexity hurts generalization
- **Data Preprocessing**: Handled missing values, feature engineering, and categorical encoding

### Key Learning Outcomes & Insights

#### **Critical Discovery: Feature Quality Over Model Complexity**

1. **Direct Predictors Win**: Passenger class directly determines fare structure
2. **Demographic Limitations**: Age and family size are weak fare predictors  
3. **Complexity Paradox**: Simple linear models with good features outperform complex models with poor features
4. **Historical Context Matters**: 1912 social structures (gender + class) drive economic patterns

#### **Algorithm-Specific Insights**

- **Linear Regression**: Sufficient when relationships are fundamentally linear (class-fare relationship)
- **Regularization (Ridge/Elastic Net)**: No benefit when base model isn't overfitting
- **Polynomial Models**: Risk overfitting without strong underlying non-linear patterns
- **Model Selection**: Match algorithm sophistication to data relationship complexity

#### **Regression-Specific Lessons**

1. **R² Interpretation**: Values <0.1 indicate virtually no predictive power
2. **Feature Engineering Impact**: Right features matter more than sophisticated algorithms  
3. **Outlier Effects**: Right-skewed fare distribution affects all linear models
4. **Domain Knowledge**: Understanding historical context crucial for feature selection

### Challenges Faced & Solutions

- **Weak Baseline Features**: Age and family_size showed minimal fare correlation - **Solution**: Identified class as key predictor
- **Fare Distribution Skew**: Right-skewed target with expensive outliers affecting linear assumptions - **Future work**: Log transformation needed
- **Polynomial Overfitting**: Degree 6 performed worse than degree 3 - **Learning**: Higher complexity requires more data and stronger relationships
- **Missing Context**: Limited features available - **Insight**: Real fare prediction would need cabin details, booking date, route information

### Data Challenges Identified

1. **Fare Prediction Difficulty**: Moderately challenging with R² ~0.55 maximum
   - Individual booking decisions create unpredictable patterns
   - Missing key information (cabin details, exact routes, booking dates)
   - Historical pricing inconsistencies from 1912 booking systems

2. **Distribution Issues**:

   - Right-skewed fare distribution (few very expensive luxury tickets)
   - Outliers from premium suite passengers affect model training
   - Missing age data creates gaps in demographic analysis

### Future Improvements & Next Steps

**Immediate Enhancements:**

- **Feature Engineering**: Add `pclass` directly, combine `embarked` with `class` for port-specific pricing
- **Data Preprocessing**: Log-transform fare to reduce skew, handle outliers (>95th percentile) separately
- **Alternative Targets**: Predict fare categories (Low/Medium/High) instead of exact amounts

**Advanced Techniques:**

- **Feature Selection**: Statistical tests to identify best predictors systematically
- **Ensemble Methods**: Combine multiple regression approaches for improved robustness
- **Cross-Validation**: Robust performance estimates across different data splits

**Research Extensions:**

- **Alternative Problems**: Try predicting age instead of fare for comparison
- **Modern Techniques**: Gradient boosting, neural networks for non-linear patterns
- **External Validation**: Test approaches on modern transportation pricing datasets

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
