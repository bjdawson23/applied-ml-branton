# applied-ml-branton

## Lab 2 Example (Howell)

Starter files for the example labs:

- notebooks/example02 folder

Lab 2 Example: Working with data, visualizations, splitting

This data set will be our friend. It is pretty small, but still has some interesting characteristics.
Our goal in this lab is to do an initial exploration and prepare it for use by a model. 

Work in a folder. Include a README.md, notebook, and data file (Howell.csv) together in a notebooks/ folder specifically for example lab 2. 
Section 

1. Import and Inspect the Data

1.2 Check for missing values and display summary statistics

2.1 Explore data patterns and distributions 

Create Scatter Plots
Create a scatter plot of height vs weight:
Color the scatter plot by gender:

We would like to be able to distinguish male from female in this graph. Replace the plt.scatter
line with the following two lines. Update the labels.

Create another plot where you display age vs height. Use gender for the color.   At what age does the character of the plot change? 

2.2 Handle missing values and clean data

Add a new Feature: BMI

Split Data by Age

Plot with masking

Section 3. Split the Data for Training and Testing
Basic Train/Test split
Compute the ratio of male/female for

Stratified Train/Test split
Stratification is a technique that ensures the training and test sets maintain a class distribution similar to the original dataset, which helps prevent bias and improves the reliability of model evaluation. ​

Present your fractions to 3 decimal places. 
For example, the ratio in the original full data set is
Male = 0.474
Female = 0.526

Using the basic split:

    What are the fractions of male and female for the training set?
    What are the fractions of male and female for the test set?
    Does the test set have a similar male-to-female ratio as the training set?
    Why might this matter when evaluating model performance?
    How close are the values to the original fractions?

Using the stratified split:

    What are the fractions of male and female for the training set?
    What are the fractions of male and female for the test set?
    Does the test set have a similar male-to-female ratio as the training set?
    How close are the values to the original fractions?

Comparison

    Why does preserving class balance improve model evaluation and generalization?
    How much closer are the stratified split ratios to the original dataset ratios compared to the basic split?
    When should we split using the stratified approach?
    What types of models might benefit more from stratification?

## Folders for Projects

## Update this README as you work

Add commands to run additional scripts as you work through the course (update the path and file name as needed).

```shell
git add .
git commit -m "describe your change in quotes"
git push -u origin main
```
