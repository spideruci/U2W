# 🧪 U2W: Untangle to Weave Disjoint Assertion Tangles in Unit Tests

**U2W** is a program analysis-based tool that automatically detects and refactors a novel test-code smell called **Disjoint Assertion Tangles (DAT)** — where a single test method verifies multiple logically unrelated behaviors.
Note: Main file is `Untangle2Weave.java`
---

## What It Does
- - **New Update for Major Revision**: Scripts added with capabilities to collect production methods called under test and track LOC for all tests across repo. These would enable us to detect Eager and Verbos test smells to draw conclusions across existing test smells.

- **Detects** test methods exhibiting Disjoint Assertion Tangles (DAT), which hinder test readability, maintainability, and fault isolation.
- **Refactors** such tests into smaller, focused test methods to improve structure and clarity.
- **Recognizes and leverages** duplication by identifying structurally similar tests.
- **Generates parameterized unit tests (PUTs)** to reduce redundancy and enable scalable, extensible test design.


---

## Backed by Research

U2W was evaluated on **42,334 tests across 49 open-source projects**, revealing:
- **DAT smell in 95.9%** of subject projects,
- Over **3,638 smelly tests refactored**,
- **1,713 PUTs generated**, with an average of **5.85** value sets per test,
- **36.33% average reduction** in executable test-code lines.

To validate its effectiveness:
- A **user study with 34 software engineers and 15 students** confirmed the practical utility of U2W,
- **19 pull requests** were submitted based on the tool's refactorings, with **15 accepted** by project maintainers.

These results demonstrate that U2W can significantly improve test-suite quality with minimal developer intervention.

---

## To Run This Tool

U2W can be run locally or integrated into your CI/CD pipeline. Follow these steps:

### Prerequisites
- **Java 11 or higher**: Ensure you have the JDK installed and set up on your system
- Clone this repository to your local machine

### Input and Output
- **INPUT**: Path to Java repository/repositories
- **OUTPUT**: Creates new test files as recommendations in the same directory as the input files
- **2 files generated per input**:
    1. Separated test file
    2. Parameterized test file (if structurally similar tests are found)

### Running Modes

U2W supports the following execution modes:

| Mode | Description |
|------|-------------|
| `detectin` | Detect DATs (Duplicate and Almost-duplicate Tests) in a single file |
| `detect` | Detect DATs in a single repository |
| `allrepo` | Detect DATs in multiple repositories |
| `fixInRepo` | Detect and fix DATs in a single repository with XLSX report generation |
| `fixInAllRepoWithXLSXReport` | Detect and fix DATs in multiple repositories with XLSX report generation |

### Configuration

For fix modes with XLSX report generation, you can specify the output location:
- Navigate to `Untangle2Weave.java` in the main method
- Update the `outputFilePath` variable with your desired output directory

### Usage

To run U2W, provide the input path followed by one of the execution modes:

```bash
# Detect in Single repository
java -jar Untangle2Weave.jar /path/to/java/repo detect

# Detect in Multiple repositories (comma-separated)
java -jar Untangle2Weave.jar /path/to/repo1,/path/to/repo2,/path/to/repo3 allrepo

# Fix in single repo with report generation
java -jar Untangle2Weave.jar /path/to/java/repo fixInRepo

# Fix in multiple repo with report generation
java -jar Untangle2Weave.jar /path/to/java/repo,/path/to/repo2 fixInAllRepoWithXLSXReport
```

The LLM Enhancement module has been build to be run as a separate step after the refactoring step. It can be run by running the java file refactor2refresh.TestEnhancer.java and providing the path to the refactored test file as an argument.

##### Note
The logs / code might refer to DAT smell as Assertion Pasta, since it was the old name for the same smell.