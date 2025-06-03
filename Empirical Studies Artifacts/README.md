# ASEArtefacts

This repo contains the artefacts for our ASE 2025 Disjoint Assertion Tangle (DAT) Smell paper.

---

## Survey Questions
The survey structure and questions can be found in the `Developer Preference Survey.pdf` in the root directory.

---

## Survey Results
The results of the developer survey can be found in the following files in the root directory:
- `(Students) Unit Test Style Preference Study (Original Responses).xlsx`
- `(Industry) Unit Test Style Preference Study (Original Responses).xlsx`

**Note:** For survey questions {1,4,5,6} Style 2 is our refactored style by U2W and for questions {2, 3} Style 1 is our refactored style by U2W.

---

## Tool
Here is the link to another anonymous repo containing our tool: [https://anonymous.4open.science/r/Untangle2Weave-39E7/README.md](https://anonymous.4open.science/r/Untangle2Weave-39E7/README.md)

---

## Pull Requests
Anonymous links to the PRs we raised can be found below:

**Accepted/Merged:**
- [PR 7512](https://anonymous.4open.science/pr/7512)
- [PR B3C2](https://anonymous.4open.science/pr/B3C2)
- [PR 8EF7](https://anonymous.4open.science/pr/8EF7)
- [PR 4205](https://anonymous.4open.science/pr/4205)
- [PR 1E44](https://anonymous.4open.science/pr/1E44)
- [PR A8B8](https://anonymous.4open.science/pr/A8B8)
- [PR 696B](https://anonymous.4open.science/pr/696B)
- [PR 784D](https://anonymous.4open.science/pr/784D)
- [PR 366D](https://anonymous.4open.science/pr/366D)
- [PR 0F21](https://anonymous.4open.science/pr/0F21)
- [PR 27BF](https://anonymous.4open.science/pr/27BF)
- [PR DBBB](https://anonymous.4open.science/pr/DBBB)
- [PR 3800](https://anonymous.4open.science/pr/3800)
- [PR C043](https://anonymous.4open.science/pr/C043)
- [PR 1E41](https://anonymous.4open.science/pr/1E41)
- [PR F23C](https://anonymous.4open.science/pr/F23C)

**Pending/Open:**
- [PR E667](https://anonymous.4open.science/pr/E667)
- [PR 5BD8](https://anonymous.4open.science/pr/5BD8)

**Rejected/Closed:**
- [PR 6015](https://anonymous.4open.science/pr/6015)

---

## Aggregated & Project Wise Results of Running U2W on 49 Subjects
The results of the tool on 49 subject projects can be found in the `Reports.xlsx` in the root directory. The report sheet contains consolidated results and each repository has its separate sheet for in-depth analysis.

---

## Project Wise Original And Refactored Test Files
Original smelly test files and their automated refactored versions through our tool can be found in the `OriginalAndRefactoredTestFiles` folder in the root directory.

For all our subject projects we have maintained the same directory structure as the original projects. The refactored test files are in the same directory as the original test files, with the same file names but with the following suffixes:
- `_Purified` for assertion cluster based separated tests
- `_Parameterized` for merged parameterized unit tests