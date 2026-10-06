# BE559

Student-facing Jupyter Book for BE 559 (Foundations of Biomedical Data Science and Machine Learning), modeled on the [EK125 book](https://github.com/BU-EK125/EK125) and following its conventions.

    pip install jupyter-book==1.0.2
    jb build .

Pushing to `main` deploys `_build/html` to GitHub Pages (`.github/workflows/deploy.yml`). Every PR is built and previewed by `pr-check`.

## What belongs here

Lecture notes and homework **problem statements** only. Never add solutions, exams, quizzes, WIP notebooks, or instructor versions of the homework. A page left out of `_toc.yml` is still built to a public URL, so if it shouldn't be public, don't add it to this repo.

## Layout

- `modules/moduleN.md`: module overview. Lecture notes (`lectures/LectureN.M.md`) nest under it as `sections:`.
- `homework/HWN.ipynb`: one page per module, with the source's parts preserved as `## Homework N.M` headings. It is its own top-level chapter in `_toc.yml`, right after its module.
- `lectures/pdf_src/` and `homework/_src/` are local-only source material (gitignored, excluded from the build).

## Conventions (as in EK125)

- **Homework scaffolds:** every student code cell is a blank `# Your code here`. Only provided code stays filled (helper functions, classes, and demonstrations the text walks through). Target figures a problem says to reproduce may keep their output.
- **Common mistakes:** use `🚩 **Common mistake:** ...`, only for a real, specific, common error tied to the material right there.
- **Cross-references:** use full absolute URLs (`https://depasquale-lab.github.io/BE559/lectures/LectureN.M.html#anchor`). Relative links break. Get the real anchor from the built HTML (`grep -oE '<section id="[^"]*"' _build/html/lectures/LectureN.M.html`).
- **Archive, never delete:** superseded public content moves to `archive/` (excluded from the build).
- **Tags:** `raises-exception` for cells that should error; `skip-execution` for cells that must not be re-run.
- **Verify the build** (`jb build .`) before opening a PR, and don't merge without an explicit go-ahead.

Differences from EK125: notebooks are **not** executed at build time (`execute_notebooks: "off"`), because homework needs Colab, PyTorch downloads, and remote data. The target figures in them are baked outputs.

## Known gaps

- Lecture notes exist only for Modules 1 and 3.
- Homework 4 part 4 is unpublished (the source has no task text).
- `appendix/syllabus.md` describes Spring 2026. If it becomes stale, ask before rewriting its dates.
