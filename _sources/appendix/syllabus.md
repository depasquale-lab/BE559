# Syllabus

**BE 559: Foundations of Biomedical Data Science and Machine Learning (Spring 2026)**

| | |
|---|---|
| Instructors | Michael Economo (mne@bu.edu) and Brian DePasquale (bddepasq@bu.edu) |
| TA | Isaac Boyd (ipboyd@bu.edu) |
| Class | T/Th 1:30–3:15, CGS 515 |
| Recitation | F 2:30–3:35, ERB 203 |
| Programming help | F 3:35–4:25, ERB 203 |
| Office hours | By appointment. 24 Cummington Mall, Room 201 (Economo); 44 Cummington Mall, Room 411E (DePasquale) |
| Course documents | Blackboard (https://learn.bu.edu) |

## Course description

This course covers conceptual and practical aspects of data science and introductory machine learning for biomedical engineers. It is a foundational course in data analytics for BME Ph.D. students, designed to follow a graduate-level introductory programming course and to prepare students for graduate-level courses and research on more advanced applications of machine learning and data science. It covers the theory and practical applications of hypothesis testing, model fitting and parameter estimation, classification, clustering, dimensionality reduction, and machine learning.

## Course goals

The course takes a practical approach to the analysis of biomedical data, with three goals.

1. Students become familiar with the theoretical background of different analysis methods, so they understand why certain methods are appropriate in certain contexts and why others are not.
2. Students acquire hands-on skills for analyzing biomedical data, including data management, algorithm development, and proper codebase development. These prepare them for independent research projects in academia and industry.
3. Students learn to interpret, visualize, and summarize the results of an analysis. Applying analysis methods is only half the challenge of scientific discovery; the third goal is to train students to collect results into a format that lets discoveries be shared with and understood by other researchers.

## Prerequisites

- BE 601 (Linear Algebra), or equivalent familiarity with linear algebra (linear systems of equations, eigendecomposition, bases, orthogonality, matrix decomposition, etc.)
- BE 604 (Statistics & Numerical Methods), or equivalent familiarity with probability and statistics (random variables, conditional and marginal probability, Bayes' rule, etc.)
- ENG BE 500 (Programming Fundamentals for Biomedical Engineering Data Analysis with Python), or equivalent programming experience

## Textbook

*Pattern Recognition and Machine Learning*, and various other texts (all freely available in PDF form on Blackboard).

## Grading and exercises

Grades are largely determined by weekly coding/analysis assignments, which together make up 50% of the course grade. The remaining 50% is based on a final exam.

Programming exercises are completed in Python using Google Colab notebooks. Assignments are distributed through Blackboard, and solutions are submitted (in `.ipynb` format) electronically via GradeScope on or before the due date. Collaboration on homework is allowed (and encouraged!), but the submitted work must be your own. The best way to fill out answers in Colab is to create a copy of the provided template (File > Save Copy in Drive) and populate your answers in the copy.

## Collaboration and plagiarism

Plagiarized assignments receive a grade of zero. Students found to have plagiarized assignments or provided their assignments to others may receive a failing grade in the course and/or a referral to the College of Engineering Academic Conduct Committee. If you are unsure whether an action is acceptable, ask!

**Do:**

- Verbally exchange tips and insights about coding, concepts from class, or anything else that is unclear. This can include looking at short segments of code together, discussing why certain solutions work, and debugging.

**Don't:**

- Electronically share code and other work with other students.
- Copy and paste another student's work (even with variable names, etc. altered).
- Copy and paste code from other sources (e.g., StackOverflow) that you do not fully understand.

## Late work

For all homework assignments, scores are reduced by 25% if turned in within one week of the due date, and by 50% if turned in more than one week late.

## Final exam

The final exam is held during the course's scheduled exam slot (May 5th, 3pm). It consists of short-answer questions aimed at assessing conceptual comprehension of the covered topics.

## Recitation and programming help

Recitations cover questions from lecture, example problems from the week's material, and an introduction to the homework. An optional programming help session follows, reviewing basic programming concepts and supporting those learning advanced packages (e.g., TensorFlow, PyTorch, SciPy).

## Course topics

**Module 1: Hypothesis testing**
Intro to Python; review of probability; review of statistics; introduction to hypothesis testing; parametric vs. non-parametric statistics; multiple comparisons; resampling-based statistical methods; advanced methods.

**Module 2: Regression and model fitting**
Fitting models to data; likelihood functions and maximum likelihood solutions; basics of optimization; linear regression; logistic regression; regularization; Bayes' rule; Bayesian perspective link to regularization; model validation, AIC, generalizability, cross-validation.

**Module 3: Classification and clustering**
Types of errors; receiver-operating characteristic (ROC) curves; linear discriminant analysis (LDA); Bayesian classifiers; expectation maximization (EM); K-means; K-nearest neighbors (K-NN); hierarchical clustering; distance measures; advanced methods.

**Module 4: Dimensionality reduction**
Linear algebra review (bases, eigendecomposition, etc.); principal components analysis; LDA (higher dimensional); revisiting regression in light of PCA (PLS, PCR, Ridge); revisiting expectation maximization; factor analysis; advanced methods.

**Module 5: Neural networks**
Gradient descent and re-introducing optimization; automatic differentiation; the backpropagation algorithm; programming neural networks; neural network loss functions and information theory.

## Tentative course schedule

| Week | Date | Tue lecture | Thu lecture | Notes | Lecturer |
|---|---|---|---|---|---|
| 1 | 1/20, 1/22 | 1.1 | 1.2 | | Mike |
| 2 | 1/27, 1/29 | 1.3 | 1.4 | | Mike |
| 3 | 2/3, 2/5 | 1.5 | 1.6 | | Mike |
| 4 | 2/10, 2/13 | 2.1 | 2.2 | 2/10: HW1 due @ noon | Brian |
| 5 | 2/19 | — | 2.3 | | Brian |
| 6 | 2/24, 2/26 | 2.4 | 2.5 | | Brian |
| 7 | 3/3, 3/5 | 3.1 | 3.2 | 3/3: HW2 due @ noon | Mike |
| 8 | | | | Spring break | |
| 9 | 3/17, 3/19 | 3.3 | 3.4 | | Mike |
| 10 | 3/24, 3/26 | 3.5 | 4.1 | | Mike/Brian |
| 11 | 3/31, 4/2 | 4.2 | 4.3 | 3/31: HW3 due @ noon | Brian |
| 12 | 4/7, 4/9 | 4.4 | 4.5 | | Brian |
| 13 | 4/14, 4/16 | 4.6 | 4.7 | | Brian |
| 14 | 4/21, 4/23 | 5.1 | 5.2 | 4/21: HW4 due @ noon | Brian |
| 15 | 4/28, 4/30 | 5.3 | review | | Brian |
| 16 | 5/5 | Final exam (3–5pm) | | | |
