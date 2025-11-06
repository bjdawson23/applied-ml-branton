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

## Project 03: ml03_branton.ipynb - Classification Model Comparison

**Author:** Branton Dawson  
**Date:** November 6, 2025  
**Status:** COMPLETED

### Project Overview

This notebook demonstrates advanced classification techniques by comparing three different algorithms on the Titanic survival prediction task. The project systematically evaluates Decision Trees, Support Vector Machines, and Neural Networks across multiple feature combinations.

#### Objective: Multi-Algorithm Classification Analysis

- **Dataset**: Titanic survival data (891 passengers)
- **Algorithms**: Decision Tree Classifier, Support Vector Machine (SVM), Neural Network (MLP)
- **Feature Cases**: Three different feature combinations tested for each algorithm
- **Goal**: Determine optimal model-feature combinations for classification tasks

#### Feature Engineering & Selection

**Case 1: Simple Binary Feature**
- **Features**: `alone` (binary: traveling alone vs. with family)
- **Rationale**: Test social dynamics theory in survival scenarios
- **Analysis**: 50.6% survival with family vs. 30.4% alone

**Case 2: Continuous Demographic Feature** 
- **Features**: `age` (continuous numerical)
- **Rationale**: Age represents physical capability and social priority ("children first")
- **Analysis**: Clear age patterns - Children (58.0%), Adults (35.3%), Seniors (22.7%)

**Case 3: Complex Feature Interaction**
- **Features**: `age` + `family_size` (multi-dimensional)
- **Rationale**: Combine demographic and social context factors
- **Analysis**: Family sizes 2-4 show 55-72% survival vs. 30% for solo travelers

### Performance Summary - Classification Results

| Model Type | Case | Features Used | Accuracy | Precision | Recall | F1-Score | Notes |
|------------|------|---------------|----------|-----------|--------|----------|-------|
| **Decision Tree** | 1 | alone | **63%** | 61% | 62% | 61% | 🏆 Best generalization, minimal overfitting |
| | 2 | age | 61% | 57% | 53% | 50% | Poor survivor recall (17%) |
| | 3 | age + family_size | 59% | 55% | 54% | 54% | Significant overfitting evident |
| **SVM (RBF)** | 1 | alone | **63%** | 61% | 62% | 61% | Matches Decision Tree performance |
| | 2 | age | 63% | 67% | 53% | 45% | ⚠️ Terrible survivor recall (7%!) |
| | 3 | age + family_size | 63% | 67% | 53% | 45% | No improvement from added features |
| **Neural Network** | 3 | age + family_size | **66%** | 64% | 62% | 63% | 🏆 Highest accuracy achieved |

#### **🏆 Performance Rankings:**
1. **Neural Network (Case 3)**: 66% accuracy - Best overall performance
2. **Decision Tree & SVM (Case 1)**: 63% accuracy - Tied for simple features  
3. **Decision Tree (Case 2)**: 61% accuracy - Moderate performance

### Technical Accomplishments

- **Multi-Algorithm Implementation**: Successfully deployed three different ML algorithms
- **Systematic Feature Testing**: Rigorous evaluation across multiple feature combinations
- **Model Comparison**: Comprehensive performance analysis with multiple metrics
- **Overfitting Detection**: Identified and analyzed training vs. test performance gaps
- **Visualization Techniques**: Decision trees, support vectors, and neural network decision boundaries
- **Class Imbalance Handling**: Proper stratified train/test splitting

### Key Learning Outcomes & Insights

#### **Critical Discovery: Model-Feature Complexity Matching**

1. **Simple Features → Simple Models**: Decision Tree and SVM excel with basic features (`alone`)
2. **Complex Features → Advanced Models**: Neural Networks perform best with feature interactions
3. **Feature Addition Paradox**: More features can hurt simple models but help complex ones

#### **Algorithm-Specific Insights**

- **Decision Trees**: Most reliable across all cases, best for interpretability
- **SVM**: Excellent for simple features but struggles with class imbalance on complex features  
- **Neural Networks**: Superior for complex feature relationships, requires proper architecture

#### **Practical Machine Learning Lessons**

1. **Overfitting Patterns**: Training accuracy ≠ real-world performance
2. **Evaluation Metrics**: Accuracy alone insufficient - examine precision/recall individually
3. **Feature Engineering Impact**: Quality over quantity in feature selection
4. **Algorithm Selection**: Match model sophistication to data complexity

### Challenges Faced & Solutions

- **SVM Class Imbalance**: 7% survivor recall in complex cases - solved by recognizing algorithm limitations
- **Overfitting Management**: Decision Trees showed 77% training vs 59% test accuracy - demonstrated need for simpler models
- **Performance Interpretation**: High overall accuracy masked poor minority class detection
- **Feature Complexity**: Learned that feature interactions require appropriate model complexity

### Future Improvements & Next Steps

**Immediate Enhancements:**
- Add gender and passenger class features (likely strongest predictors)
- Hyperparameter tuning for all algorithms
- Cross-validation for robust performance estimates

**Advanced Techniques:**
- Ensemble methods (Random Forest, Gradient Boosting)
- Feature interaction analysis with polynomial features
- SHAP analysis for model interpretability

**Research Extensions:**
- External validation on similar disaster datasets
- Deep learning architectures for complex feature relationships

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
