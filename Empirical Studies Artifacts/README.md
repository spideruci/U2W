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

## Pull Requests
Anonymous links to the PRs we raised can be found below:

**Accepted/Merged:**
- [PR 1](https://github.com/apache/incubator-seata/pull/7286)
- [PR 2](https://github.com/apache/incubator-seata/pull/7167)
- [PR 3](https://github.com/apache/amoro/pull/3450)
- [PR 4](https://github.com/apache/amoro/pull/3453)
- [PR 5](https://github.com/apache/amoro/pull/3454)
- [PR 6](https://github.com/apache/amoro/pull/3455)
- [PR 7](https://github.com/apache/amoro/pull/3456)
- [PR 8](https://github.com/apache/amoro/pull/3510)
- [PR 9](https://github.com/apache/amoro/pull/3511)
- [PR 10](https://github.com/apache/amoro/pull/3512)
- [PR 11](https://github.com/apache/amoro/pull/3513)
- [PR 12](https://github.com/apache/incubator-seata/pull/7160)
- [PR 13](https://github.com/apache/incubator-seata/pull/7287)
- [PR 14](https://github.com/apache/incubator-seata/pull/7294)
- [PR 15](https://github.com/apache/incubator-seata/pull/7295)
- [PR 16](https://github.com/apache/incubator-xtable/pull/703)

**Pending/Open:**
- [PR 17](https://github.com/apache/commons-net/pull/328)
- [PR 18](https://github.com/apache/incubator-baremaps/pull/958)

**Rejected/Closed:**
- [PR 19](https://github.com/jhy/jsoup/pull/2269)

---

## Aggregated & Project Wise Results of Running U2W on 49 Subjects
The results of the tool on 49 subject projects can be found in the `Reports.xlsx` in the root directory. The report sheet contains consolidated results and each repository has its separate sheet for in-depth analysis.

---

## Project Wise Original And Refactored Test Files
Original smelly test files and their automated refactored versions through our tool can be found in the `OriginalAndRefactoredTestFiles` folder in the root directory.

For all our subject projects we have maintained the same directory structure as the original projects. The refactored test files are in the same directory as the original test files, with the same file names but with the following suffixes:
- `_Purified` for assertion cluster based separated tests
- `_Parameterized` for merged parameterized unit tests