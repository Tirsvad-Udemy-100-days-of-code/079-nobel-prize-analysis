# Business Case

## Metadata
| Key | Value |
| --- | --- |
| ID | BC-001 |
| CrossReference | [SA-001], [PP-001], [MIL-004] |
| Language | en |
| Domain | education |

## Version History
| Date | Status | Author | Reviewer | Change | Commit |
| --- | --- | --- | --- | --- | --- |
| 2026-11-12 | Deprecated | Jens Tirsvad Nielsen | AI as stand-in for S01 | Initial version | [23ad5bb] |
| 2026-11-14 | Deprecated | Jens Tirsvad Nielsen | AI as stand-in for S01 | Udemy screenshots replaced by own-word lecture summaries (copyright) | [cdfa062] |
| 2026-11-16 | Accepted | Jens Tirsvad Nielsen | S01 (AI as stand-in) | Added objective 7, success criterion 7, a scope item, an out-of-scope item, a risk, assumptions and constraints for the baseline milestone MIL-004; set the domain to education; reviewed in autonomous mode, not independent<br>Reviewed in RC-011: Go | pending |

---

## Executive Summary

This project turns the Day 79 assignment of Udemy's "100 Days of Code: The Complete Python Pro Bootcamp" (analysing the Nobel Prize with Plotly, Matplotlib and Seaborn) into a readable, runnable Python repository. It delivers a tested Python package that answers the assignment's questions about the prizes awarded from 1901 to 2020, a Jupyter notebook that follows the eight lecture steps, a README and a three-language wiki (English, Danish, Bahasa Malaysia) with one screenshot per lecture step. The project proceeds because it is small, has a fixed source and serves both the course participant and the people who compare solutions.

## Methodological and Standards Foundation

The project follows the SQA and QC framework mounted at `framework/`: artifacts are reviewed against their QC checklists, and quality criteria are tagged with ISO/IEC 25010:2023 characteristics. Domain modelling follows Larman's *Applying UML and Patterns* where a design artifact is needed. Source code follows the Python conventions of the `coding-conventions` skill and the layering of the `clean-architecture` skill. Source comments use Doxygen.

## Problem Statement

The assignment ships as one Google Colab notebook with unstructured cells, no tests and a dependency on Colab's pre-installed packages. A participant who wants to keep the work, share it or compare it with others has no runnable repository, no installation instructions, no explanation of what each step teaches and no evidence that the answers are correct.

## Business Opportunity

A clean repository makes the solution reusable as a reference for other course participants and as a portfolio piece, and it records what was learned in each lecture step in three languages.

## Objectives

1. Answer the assignment questions (dataset shape, duplicates and NaN values, prize categories, women laureates, prizes over time, top 20 countries, research organisations and cities, laureate age) with functions that carry the assignment's names.
2. Provide a Jupyter notebook that reproduces every lecture step, including the charts.
3. Provide automated tests that check each answer against the dataset.
4. Provide a README with set-up, run and test instructions, and a wiki in English, Danish and Bahasa Malaysia that explains what each lecture step teaches, with Linux and Windows guides.
5. Provide a short summary of each lecture step, written in our own words, in the README and the wiki. Udemy screenshots are not used because they may be copyrighted.
6. Publish the repository with a description and topics.
7. Bring the finished project to the common baseline of the framework: the adopted framework release, a README that lists only the documents of the repository, licence and project URL metadata, the editor settings of the baseline, an `.env.example` in the framework's form, a wiki sidebar that starts with its title and a traceability matrix that follows the new documents ([MIL-004]).

## Scope

### In Scope

- The eight Day 79 lecture steps: goals, cleaning, categories and women laureates (bar and donut charts), prizes over time, choropleth map and top countries, sunburst of research locations, laureate age, summary.
- A Python package under `src/`, tests under `tests/`, the notebook and the dataset supplied with the lecture.
- `pyproject.toml`, a Python `.gitignore`, a Doxyfile, a `.venv` set-up guide, README and wiki.
- A local scan with opengrep before every push.
- The baseline milestone [MIL-004]: the framework release, the README without the private framework files in its appendix, project URL metadata, `.editorconfig`, `.env.example`, the wiki sidebar with its generator comment moved below the title, a traceability matrix that follows the new documents and the review records. It changes no behaviour of the program.

### Out of Scope

- Other days of the bootcamp.
- A web or desktop user interface.
- Updating the dataset beyond the 2020 snapshot supplied with the lecture.
- Hosting the notebook in Google Colab.
- Any change to `src/`, `tests/`, the notebook, the dataset, `docs/images/` or the wiki pages in the baseline milestone [MIL-004], except the position of the generator comment in `docs/wiki/_Sidebar.md` and in its generator `scripts/make_wiki.py`. That milestone runs the tests only.

## Expected Benefits

### Tangible Benefits

- A repository that runs with a few commands and passes its tests.
- Eight step summaries and a three-language wiki that can be reused for later days.

### Intangible Benefits

- Understanding of data cleaning, grouping, merging and charting with Pandas, Plotly, Matplotlib and Seaborn.
- A pattern for turning a course notebook into tested code.

## Strategic Alignment

The project supports the course participant's goal of completing the bootcamp with work that is worth sharing, and it practises the framework's plan-first workflow on a small project.

## Success Criteria

| # | Criterion | Target | Measure |
| --- | --- | --- | --- |
| 1 | Assignment questions answered | All challenge questions answered; values equal the lecture's (962 rows, 16 columns, first prize 1901, last year 2020) | automated tests pass |
| 2 | Notebook runs | 100 % of cells execute without error from a fresh `.venv` | `jupyter nbconvert --execute` exits 0 |
| 3 | Documentation languages | 3 of 3 wiki languages with the same page set | file listing of `docs/wiki/` |
| 4 | Lecture summaries | 8 of 8 lecture steps have a summary in the README and the wiki; no Udemy screenshot is stored | README and `docs/wiki/` pages; file listing of `docs/images/` |
| 5 | Security scan | 0 findings from opengrep before each push | opengrep exit code |
| 6 | Dependencies | Runtime dependencies limited to those the charts need (pandas, numpy, plotly, matplotlib, seaborn) | `pyproject.toml` |
| 7 | The baseline milestone is done (objective 7) | `framework/scripts/check-readme.sh`, `check-languages.sh`, `check-qc-tags.sh` and `check-editorconfig.sh` exit with code 0, `python -m pytest` passes, 100 % of the continuous integration (CI) checks of the pull request of [MIL-004] pass | The script exit codes and the pull request status on the git host |

## Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| The dataset is not available locally (it is a Udemy resource) | Tests cannot assert the real values | S01 supplies `nobel_prize_data.csv`; until then tests run on a small synthetic fixture and the real-value tests are skipped and reported |
| The dataset or the course material licence forbids republishing | The repository must be private or the data removed | The README names the source; S01 decides whether the data file is committed |
| A lecture value differs because of a different library version | A test fails | Tests assert exact values from the supplied snapshot; `pyproject.toml` pins minimum versions only |
| Chart images drift from the code | The documentation misleads | One script regenerates the code-made chart images |
| A token leaks into the repository | Account compromise | `.env` is ignored by git, is never read by the project code and is never printed |
| The documents of the baseline milestone [MIL-004] change documents that were accepted earlier, and an AI stand-in for S01 reviews them | A defect is missed because the review is not independent | Every review record of the baseline says `Mode: autonomous, not independent`, `src/`, `tests/`, the notebook and the data are not changed, the tests run before and after, and the end-of-run summary lists the reviews for challenge |

## Assumptions

- S01 is the Product Owner, developer and reviewer; the AI acts as stand-in reviewer in autonomous mode.
- The dataset supplied with the lecture is the only data source.
- Python 3.13 is installed on the machine of S01.
- The Product Owner (PO) language is English. The PO domain is education since [MIL-004] (it was IT until then; the documents that [MIL-004] does not change keep the domain `it`, see the Open Issues of [PP-001]).

## Constraints

- Target completion: 2026-11-12 (one working day plus review).
- Python 3.13 or newer, a local `.venv`, configuration in `pyproject.toml`.
- Folder structure `src/`, `tests/`, `docs/`.
- One branch and one pull request per milestone.
- Runtime dependencies only where needed.
- The baseline milestone [MIL-004] starts 2026-11-16 and is finished within one week, by 2026-11-23. For [MIL-004] only, an AI stand-in for S01 reviews and accepts the changed documents.

## Cost–Benefit Assessment

| Costs | Benefits |
| --- | --- |
| About one working day of effort by S01 with AI assistance; no licence or hosting cost | A shareable, tested reference solution and a three-language explanation; the justification is qualitative because the project has no revenue |

## Stakeholders

| Stakeholder ID (SA) | Interest in this project |
| --- | --- |
| S01 | Completes the assignment and owns the result |
| S02 | Runs and compares the code |
| S03 | Browses the repository for ideas |

## Recommendation

Proceed — the scope is small, the source is fixed and the result serves all three stakeholders.

---

[SA-001]: ./stakeholder-analysis.md
[23ad5bb]: https://git.tirsystem.com/Tirsvad-Udemy-100-days-of-code/079-Nobel-Prize-Analysis/commit/23ad5bbc2f45375d6f19cfe3fcb6a3fbe9c9c97b
[cdfa062]: https://git.tirsystem.com/Tirsvad-Udemy-100-days-of-code/079-Nobel-Prize-Analysis/commit/cdfa062047dac9523db6e6f4a91d257a78922bf0
[PP-001]: ./project-plan.md
[MIL-004]: ./milestones/mil-004-framework-baseline.md
