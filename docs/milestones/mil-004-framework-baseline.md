# MIL-004 Framework baseline

## Metadata
| Key | Value |
| --- | --- |
| ID | MIL-004 |
| CrossReference | [BC-001], [PP-001], [MIL-003] |
| Language | en |
| Domain | education |

## Version History
| Date | Status | Author | Reviewer | Change | Commit |
| --- | --- | --- | --- | --- | --- |
| 2026-11-16 | Accepted | Jens Tirsvad Nielsen | AI as stand-in for S01 | Initial version; accepted with the Go verdict of the review record (autonomous, not independent) | [ddaac3b] |

---

## Purpose

This gate decides whether the project has the baseline of the framework: the adopted framework release, the README in the framework template with an appendix that lists only the documents of the repository, licence and project URL metadata, the editor settings of the baseline, the environment template of the framework, a traceability matrix that follows the new documents, a passing test suite, an updated plan and reviewed documents, merged to the default branch with a green build. The wiki in English, Danish and Bahasa Malaysia was the same on the host as in the folder; this gate checks it again against the current checklist and makes one change: it moves the generator comment from the first line of the sidebar to its end, so that the sidebar starts with its title as the checklist requires. The work is delivered on the branch `mil-004-framework-baseline` and one pull request. It changes no behaviour of the program, the notebook or the data.

## Deliverable

A merged pull request that holds: the updated Business Case, Project Plan, Traceability Matrix and Artifact Registry, this milestone and the review records of the changed documents and of the wiki; the README without the private framework files in its appendix; `pyproject.toml` with the author and the project URLs (it already has the licence expression, the licence file and a build requirement that reads it); `.editorconfig` and `.env.example` of the framework baseline; the framework release adopted by the project; and the sidebar `docs/wiki/_Sidebar.md` with its generator `scripts/make_wiki.py`, changed only in the position of the generator comment. The program (`src/`), the tests (`tests/`), the other scripts, the dataset (`data/`), the notebook (`notebooks/`), the chart images (`docs/images/`) and the wiki pages do not change.

## Go / No-Go Criteria

| # | Criterion (objectively checkable) | Go | No-Go |
| --- | --- | --- | --- |
| 1 | BC-001, PP-001 and MIL-004 each have an `Accepted` Version History row and a review record with the verdict `Go`, and the wiki has a review record | Verdicts as stated | Any missing or `No-Go` |
| 2 | `python -m pytest` runs offline and `git diff origin/main --stat -- src tests data notebooks docs/images` lists no file; the diff of `scripts` and `docs/wiki` lists only `scripts/make_wiki.py` and `docs/wiki/_Sidebar.md` | Exit code 0 (111 passed) and the diffs as stated | Any failure or any other change |
| 3 | `docs/wiki/` has `_Sidebar.md` and the ten English pages (Home, Getting-Started, Step-1 to Step-7, Summary) in en, da and ms (30 pages), directly in the folder, each page starting with the language line, and the sidebar starts with the title in bold, has one list of the English pages and the Languages section last (the generator comment stands after it); the published wiki is the same as the folder after the merge | 30 pages, the sidebar and the same content on the host | A page or language missing, a subfolder, a sidebar of another shape, a page without the language line first or a difference on the host |
| 4 | `framework/scripts/check-readme.sh`, `check-languages.sh`, `check-qc-tags.sh` and `check-editorconfig.sh` run, and the OpenGrep check of the pull request reports no finding | Exit code 0, 0 findings | Any failure or finding |
| 5 | `pyproject.toml` has the licence expression `AGPL-3.0-only` and `license-files`, requires a setuptools version that reads the licence expression, and sets the author and the project URLs for the repository, the documentation and the issue tracker | All set | Any missing |
| 6 | `.env.example` is tracked and holds empty placeholders only (the program reads no `.env` file; the framework scripts read it); `git ls-files .env` is empty | Present, no real value, nothing listed | Missing, a real value present, `.env` tracked |
| 7 | `docs/sqa/traceability-matrix.md` lists every document of the project, the milestones MIL-001 to MIL-004 and the wiki included, with its upstream and downstream links and its last review | One row per document | A document missing |
| 8 | All CI checks of the pull request | Green | Red or pending |
| 9 | The pull request carries one `Closes #N` line per task of this milestone | Every issue is closed after the merge | An issue stays open |

## Dependencies

| Depends on | Reason |
| --- | --- |
| [MIL-003] accepted | Baselines the finished program, its tests, its notebook, its README, its screenshots and its wiki |

## Traceability

| Business Case objective / KPI / user story | Reference |
| --- | --- |
| Objectives 1 to 6 | Criterion 2 (the behaviour is unchanged and its tests pass) |
| Objective 7 | Criteria 1, 3, 4, 5, 6, 7 and 9 (documents, wiki, README, metadata, environment template, traceability matrix and issues) |
| Success criterion 7 | Criteria 1, 2, 3, 4 and 8 |

## Ownership

| Role | Stakeholder ID (SA) |
| --- | --- |
| Owner | S01 |
| Approving reviewer | S01 (AI as stand-in, autonomous mode, not independent) |

## Target Date

2026-11-23: one week after the start, as the Business Case constraint for this milestone requires.

## Tasks

| # | Task | Summary | Needs its own Use Case/User Story? | Reference |
| --- | --- | --- | --- | --- |
| 1 | Adopt the framework release | Move the `framework/` submodule to the newest release, track `.gitmodules` (lowercase repository URL), install the skills and hooks, add the framework baseline `.editorconfig` and bring `.env.example` to the framework's template, so the project follows the same rules as the other projects of the portfolio. | No | BC-001 objective 7 |
| 2 | Update and review the planning documents | Add this milestone to the Business Case and Project Plan, update the Traceability Matrix, set the domain of the changed documents and of the registry to education, name the PlantUML server in the Artifact Registry and review each changed document against its QC checklist, so the plan-first gate is met. | No | BC-001 objective 7 |
| 3 | Check the wiki against the current checklist | Compare the sidebar and the 30 pages with the wiki checklist of the adopted framework release, move the generator comment from the first line of the sidebar to its end (in the generator `scripts/make_wiki.py` and in `_Sidebar.md`), read the published wiki back from the host after the merge and add a review record for the wiki. | No | BC-001 objectives 4 and 7 |
| 4 | Bring the README to the framework template | Keep the text of the README, describe the framework files in the overview, name the licence expression, and give the appendix only the documents that are in the repository, so the README is complete and checkable. | No | BC-001 objectives 4 and 7 |
| 5 | Complete the package metadata | Check that `pyproject.toml` already has the licence expression, `license-files` and a setuptools version that reads it, and add the author and the repository, documentation and issue tracker URLs, so package tools can read them. | No | BC-001 objective 7 |

---

[BC-001]: ../business-case.md
[PP-001]: ../project-plan.md
[MIL-003]: ./mil-003-notebook-and-docs.md
[ddaac3b]: https://git.tirsystem.com/Tirsvad-Udemy-100-days-of-code/079-Nobel-Prize-Analysis/commit/ddaac3b73f27f28e349288470599ebadb04e7c41
