# U2W (Untangling to Weave) DAT Test Smell Refactoring and Detection Tool

This repository contains the complete set of artifacts for our ASE 2025 paper on **Disjoint Assertion Tangle (DAT) Smell** detection and refactoring in unit tests.

---

## Repository Structure

### 📁 [U2W Source Code](https://github.com/spideruci/U2W/tree/main/U2W%20Source%20Code#readme)
Contains the complete source code and implementation of **U2W (Untangle to Weave)** - our program analysis-based tool that automatically detects and refactors Disjoint Assertion Tangles in unit tests.

**What's included:**
- Complete Java source code for the U2W tool
- Main executable file (`Untangle2Weave.java`)
- LLM Enhancement module for post-refactoring improvements
- Detailed usage instructions and examples
- Configuration options for different execution modes

### 📁 [Empirical Studies Artifacts](https://github.com/spideruci/U2W/tree/main/Empirical%20Studies%20Artifacts#readme)
Contains all research artifacts, data, and results from our comprehensive empirical evaluation of the DAT smell and U2W tool effectiveness.

**What's included:**
- Developer survey questions and methodology (`Developer Preference Survey.pdf`)
- Complete survey responses from 34 software engineers and 15 students:
    - `(Industry) Unit Test Style Preference Study (Original Responses).xlsx`
    - `(Students) Unit Test Style Preference Study (Original Responses).xlsx`
- Tool evaluation results across 49 open-source projects (`Reports.xlsx`)
- Original and refactored test files from all subject projects (`OriginalAndRefactoredTestFiles/`)
- Anonymous links to 19 submitted pull requests (16 accepted by maintainers) - see [README](https://github.com/spideruci/U2W/tree/main/Empirical%20Studies%20Artifacts#readme) for complete list

---

## Quick Start

1. **To use the U2W tool**: Navigate to the [U2W Source Code](https://github.com/spideruci/U2W/tree/main/U2W%20Source%20Code#readme) folder and follow the setup instructions
2. **To explore research data**: Check the [Empirical Studies Artifacts](https://github.com/spideruci/U2W/tree/main/Empirical%20Studies%20Artifacts#readme) folder for survey results, evaluation data, and example refactorings

---

## Research Highlights

- **95.9%** of evaluated projects contained DAT smell
- **36.33%** average reduction in executable test-code lines after refactoring
- **1,713** parameterized unit tests generated with average **5.85** value sets per test
- **78.9%** acceptance rate for submitted pull requests based on U2W refactorings
