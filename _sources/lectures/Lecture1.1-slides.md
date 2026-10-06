# Lecture 1.1a: Course Introduction

**Foundations of Biomedical Data Science and Machine Learning**
Lecture 1.1: Course introduction, probability, and statistics

## What's on tap

1. What is BE559?
2. How is the course going to work?
3. Intro to Python
4. Review of probability and statistics

## What is BE 559?

**Course description:** This course will cover conceptual and practical aspects of data science and introductory machine learning for biomedical engineers. This course serves as a foundational course in data analytics for BME Ph.D. students. It is designed to follow a graduate-level introductory programming course and will prepare students for graduate-level courses and research focused on more advanced applications of machine learning and data science. This course will cover the theory and practical applications of hypothesis testing, model fitting and parameter estimation, classification, clustering, dimensionality reduction, and machine learning.

Phrases emphasized (highlighted) on the slides:

- "follow a graduate-level introductory programming course"
- "theory and practical applications"
- "hypothesis testing, model fitting and parameter estimation, classification, clustering, dimensionality reduction, and machine learning"

> **Figure:** A flow diagram of three rounded boxes joined by right-pointing blue arrows. Box 1: "Python / Lin. Alg. / Prob+Stat". Box 2: "This class". Box 3: "Advanced ML courses".

### Modules and topics

> **Figure:** The flow diagram is shown beside a two-column table, "Module & Lectures" and "Topics". In a later slide a blue arrow labeled "First 6 Lectures" points to the Module 1 row.

| Module | Topics |
|---|---|
| Module 1 - Hypothesis testing (first 6 lectures) | Intro to Python; Review of probability; Review of statistics; Introduction to Hypothesis testing; Parametric vs. non-parametric statistics; Multiple comparisons; Resampling-based statistical methods; Advanced methods |
| Module 2 - Regression and model fitting | Fitting models to data; Likelihood functions/Maximum likelihood solutions; Basics of optimization; Linear regression; Python functions; Logistic regression; Regularization; Bayes' Rule; Bayesian perspective link to regularization; Model validation, AIC, generalizability, cross-validation |
| Module 3 - Classification and clustering | Types of errors; Receiver-operating characteristic (ROC) curves; Linear discriminant analysis (LDA); Bayesian classifiers; Expectation maximization (EM); K-means; K-nearest neighbors (K-NN); Hierarchical clustering; Distance measures; Advanced methods |
| Module 4 - Dimensionality reduction | Linear algebra review (bases, eigendecomposition, etc.); Principal components analysis; LDA (higher dimensional); Revisiting expectation maximization; Factor analysis; Advanced methods |
| Module 5 - Neural networks | Gradient descent/re-introduce optimization; Automatic differentiation; Backpropagation algorithm; Programming neural networks; Neural network loss functions and information theory |

### Tentative course schedule (Spring 2026)

| Week | Date | Tues lecture | Thurs lecture | Notes | Lecturer |
|---|---|---|---|---|---|
| Week 1 | 1/20, 1/22 | 1.1 | 1.2 | | Mike |
| Week 2 | 1/27, 1/29 | 1.3 | 1.4 | | Mike |
| Week 3 | 2/3, 2/5 | 1.5 | 1.6 | | Mike |
| Week 4 | 2/10, 2/13 | 2.1 | 2.2 | 2/10: HW1 due @ noon | Brian |
| Week 5 | 2/19 | — | 2.3 | | Brian |
| Week 6 | 2/24, 2/26 | 2.4 | 2.5 | | Brian |
| Week 7 | 3/3, 3/5 | 3.1 | 3.2 | 3/3: HW2 due @ noon | Mike |
| Week 8 | | | | Spring Break | |
| Week 9 | 3/17, 3/19 | 3.3 | 3.4 | | Mike |
| Week 10 | 3/24, 3/26 | 3.5 | 4.1 | | Mike/Brian |
| Week 11 | 3/31, 4/2 | 4.2 | 4.3 | 3/31: HW3 due @ noon | Brian |
| Week 12 | 4/7, 4/9 | 4.4 | 4.5 | | Brian |
| Week 13 | 4/14, 4/16 | 4.6 | 4.7 | | Brian |
| Week 14 | 4/21, 4/23 | 5.1 | 5.2 | 4/21: HW4 due @ noon | Brian |
| Week 15 | 4/28, 4/30 | 5.3 | review | | Brian |
| Week 16 | 5/5 | Final Exam (3-5pm) | | | |

## How is the course going to work?

**Prerequisites:** BE 601 (Linear Algebra), or equivalent familiarity with linear algebra (e.g., linear systems of equations, eigendecomposition, bases, orthogonality, matrix decomposition, etc.), and BE 604 (Statistics & Numerical Methods) or equivalent familiarity with probability and statistics (e.g., random variables, conditional and marginal probability, Bayes' rule, etc.). ENG BE 500 (Programming Fundamentals for Biomedical Engineering Data Analysis with Python) or equivalent programming experience.

**Grading & exercises:** Student grades will largely be determined by weekly coding/analysis assignments that will together comprise 50% of the course grade. The remaining 50% will be based on a final exam.

Programming exercises are to be completed in Python using Google Colab notebooks. Course assignments will be distributed by Blackboard and solutions are to be submitted (in .ipynb format) electronically via GradeScope on or before the assigned due date. Collaboration on the homework is allowed (and encouraged!) but your submitted work must be your own (see below). The best way to fill out answers in google colab is to create a copy of the provided homework template (File > Save Copy in Drive), and then use this copy to populate your answers to the questions.

**Collaboration/plagiarism:** Plagiarized assignments will be assigned a zero grade. Students found to have plagiarized assignments or provided their assignments to others may receive a failing grade in the course and/or a referral to the College of Engineering Academic Conduct Committee. Below is clarification about what IS and what IS NOT acceptable. If you are uncertain if actions are acceptable or unacceptable, please ask us!

- **DO:** Verbally exchange tips and insights about coding, concepts from class, or anything else that is unclear. This could include looking at short segments of code together, discussing why certain solutions work, and debugging.
- **DON'T:** *Electronically share code and other work with other students.* Copy and paste work of another student (even with variable names, etc. altered!). Copy and paste code from other sources (e.g StackOverflow) that you do not fully understand.

**Policy for late work:** For all homework assignments, scores will be reduced by 25% if turned in within one week of the scheduled due date. Scores will be reduced by 50% if turned in more than one week late.

**Recitation and programming help:** Recitations will cover questions from lecture, example problems from the week's material, and introduce homework material. Then, there will be an optional programming help session where we will review basic programming concepts and provide support for those learning advanced programming packages (e.g., Tensorflow, PyTorch, SciPy, etc.).

**Textbook:** Pattern Recognition and Machine Learning (Bishop; PDF) and various other texts (all freely available in PDF form).

## Source material

> **Figure:** Book covers and title pages: *Pattern Recognition and Machine Learning* (Christopher M. Bishop); *Beginning Statistics* (Schafer and Zhang, v. 1.0); *Introduction to Statistics*, Online Edition (primary author and editor David M. Lane); *The Elements of Statistical Learning: Data Mining, Inference, and Prediction* (Trevor Hastie, Robert Tibshirani, Jerome Friedman). A following slide overlays red text in a box: "These are all free as PDFs!"

## Course logistics on Blackboard

> **Figure:** Screenshot of a Blackboard course home page (a course shown as "BE700 A2 Advanced Topics in Biomedical Engineering (Spring 2024)", used as an example). Left menu: Home Page, Information, Textbooks, Lectures, Recitations, Homeworks, Tools. The main pane shows "My Announcements" (none in the last 7 days) and "My Tasks" (no tasks due).

> **Figure:** Same screenshot with a red arrow pointing at "Information". The Information page lists "Course syllabus" with the note "Everything you need!"

> **Figure:** Same screenshot with a red arrow pointing at "Tools". The Tools page shows the Gradescope logo with the text "This is where to turn your homework in!"

## Intro to Python

> **Figure:** The Python logo above a terminal window. The command `python pretty_print.py` prints a dictionary `{'num_list1': [1, 2, 3], 'num_list2': [3, 4, 5]}`, the tuple `(1, 2, 3, 4)`, and `False True` (colored red and green).

> **Figure:** Screenshot of the Spyder IDE: file/outline tree on the left, a code editor (plugin.py) in the center, a Variable Explorer on the upper right listing variables by name, type, size, and value, and a plots pane on the lower right showing a 3D surface plot and a polar bar chart.

> **Figure:** Screenshot of a Jupyter notebook titled "Running Code". Text explains that the notebook is an interactive environment for writing and running code, with sections "Code cells allow you to enter and run code" (run with Shift-Enter or the play button; example cells `a = 10` and `print(a)` giving `10`; Alt-Enter runs the cell and inserts a new one below, Ctrl-Enter runs the cell and enters command mode) and "Managing the Kernel" (code runs in a separate process called the Kernel, which can be interrupted or restarted; example cell `import time; time.sleep(10)`).

> **Figure:** Screenshot of a Google Colab "Welcome To Colaboratory" notebook, "Getting started" section. It explains that a Colab notebook is an interactive environment that lets you write and execute code. Example code cells: `seconds_in_a_day = 24 * 60 * 60` giving `86400`, and `seconds_in_a_week = 7 * seconds_in_a_day` giving `604800`. The text notes that Colab notebooks combine executable code and rich text (images, HTML, LaTeX), are stored in Google Drive, and can be shared; Colab notebooks are Jupyter notebooks hosted by Colab.

### Coding resources

- Intro to colab notebooks
  - https://colab.research.google.com/
- Intro to Python
  - https://colab.research.google.com/github/jckantor/CBE30338/blob/master/docs/01.02-Python-Basics.ipynb
- Numpy for Matlab users
  - https://numpy.org/doc/stable/user/numpy-for-matlab-users.html

## Review of probability and statistics

### Module 1: Statistics!

> **Figure:** Three memes comparing statistics and machine learning. (1) Scooby-Doo unmasking: a figure labeled "MACHINE LEARNING" is unmasked ("Let's see who you really are!") to reveal "STATISTICS". (2) Two-panel "Drake" format: the top panel (rejecting) is labeled "Statistics", the bottom (approving) is labeled "Machine learning". (3) Four-panel comic: a person looks at a cracked "statistics" label, then puts it in a frame, then it is labeled "Machine Learning", and finally the framed crack is labeled "Artificial intelligence" while the person presents it to a crowd.

(The slides then repeat the module table, with the "First 6 Lectures" arrow pointing at Module 1.)
