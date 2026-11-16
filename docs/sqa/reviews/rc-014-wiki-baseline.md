# Review Record: Wiki against QC-WIKI-001

## Metadata
| Key | Value |
| --- | --- |
| ID | RC-014 |
| CrossReference | [WIKI], [QC-WIKI-001] |

## Version History
| Date | Status | Author | Reviewer | Change | Commit |
| --- | --- | --- | --- | --- | --- |
| 2026-11-16 | Accepted | Jens Tirsvad Nielsen | AI as stand-in for S01 | Initial review record; verdict Go-with-conditions (autonomous, not independent) | pending |

---

## Artifact Under Review

- Instance reviewed: [WIKI]
- Checklist used: [QC-WIKI-001]
- Scope: full review
- Language and domain: en, da, ms / education (a wiki is not an artifact with Language and Domain rows)
- Language reviewer: none (the stand-in reads English and knows the education domain)
- Mode: autonomous, not independent (AI as stand-in for S01)

## Checklist Results

| # | Criterion | Status | Evidence/Notes |
| --- | --- | --- | --- |
| 1 | The wiki has a `_Sidebar.md`, because the host lists subpages only through it | Pass | docs/wiki/_Sidebar.md exists. |
| 2 | The sidebar starts with the wiki's title in bold, then one list of the pages in the primary language (English), `Home` first | Pass | The sidebar starts with the wiki title in bold (Nobel Prize Analysis), then one list of the ten English pages with Home first. Before this change the generator comment stood before the title; it now stands at the end of the file. |
| 3 | The page list holds a link to every English page of the wiki, and no link points to a page that does not exist | Pass | The list links Home, Getting-Started, Step-1 to Step-7 and Summary; each of these files exists in docs/wiki/, no other English page exists, and a mechanical check found no broken link between pages. |
| 4 | A `**Related**` section follows the page list only when the wiki has related wikis (for example the checklists wiki for a framework wiki); each entry is a link to that wiki's Home. A wiki with nothing related has no such section | Pass | The wiki has no related wiki, so the sidebar has no Related section. |
| 5 | A `**Languages**` section is the last section of the sidebar. It has one line per language, the language written in that language, linking to that language's `Home` page | Pass | The Languages section is the last section and has one line each for English, Dansk and Bahasa Melayu, linking to Home, Home-da and Home-ms. |
| 6 | The sidebar does not repeat the page list per language | Pass | The page list appears once. |
| 7 | A sidebar produced by a generator carries a comment that says so and names the generator; the generator is changed, not the page | Pass | The sidebar is produced by `scripts/make_wiki.py` and carries a comment that names the generator; the comment now stands at the end of the file so the title stays first, and the generator was changed together with the page. |
| 8 | The wiki has a `Languages` line on each page (criterion 11), so the sidebar is not the only way to switch language | Pass | Each page has the language line as its first line. |
| 9 | Every wiki exists in English and, as a minimum, in the language the project's registry names as the PO language; further languages are added on top, never instead of English | Pass | English (the PO language) exists, with Danish and Bahasa Malaysia on top. |
| 10 | Every English page has a page in each other language of the wiki: the page sets are identical | Pass | Each of the ten English pages has a Danish (-da) and a Malay (-ms) page; the three sets are identical (30 pages, plus the sidebar). |
| 11 | Every page starts with the language line, with the current language in bold and a link to the same page in each other language | Pass | Every page starts with the language line with the current language in bold and a link to the same page in each other language (checked mechanically). |
| 12 | A page in a language other than English is named `<Page>-<code>.md`, with a BCP 47 code; English has no suffix | Pass | Danish pages end in -da.md and Malay pages in -ms.md; English pages have no suffix. |
| 13 | Code blocks, commands, file names and IDs stay in English in every language | Pass | The fenced code blocks and image links of each English page were compared mechanically with the Danish and the Malay page: every command, file name and URL in them is identical (0 mismatches in 10 pages). |
| 14 | The sidebar, every page and every link were checked on the published wiki after the change, not only in the repository | Pending | 30 of 31 files were identical on the host before this change (the host listed the 30 pages and `_Sidebar`); the sidebar changes in this milestone (the generator comment moves to the end) and is published only by the merge. Every page name linked from the sidebar exists in the folder and on the host. The comparison is repeated after the merge. |
| 15 | A change to the layout rules (sections, order, naming) is made in the generator or template and in this checklist's source rules together | Pass | The position of the comment was changed in the generator `scripts/make_wiki.py` and in the generated sidebar together; no other layout rule changed. |
| 16 | The wiki folder (`docs/wiki/`) is flat: every page, `Home.md` and `_Sidebar.md` included, is directly in it, and languages are told apart by file name, never by a subfolder | Pass | All pages and `_Sidebar.md` are directly in docs/wiki/; no subfolder exists (the screenshots are in docs/images/ and are shown by their URL on the host). |

## Overall Verdict

Go-with-conditions — every Mandatory criterion passes except criterion 14, which is Pending. Before this change all 31 files of `docs/wiki/` (30 pages and the sidebar) were compared with the published wiki on the host and were identical. This milestone moves the generator comment from the first line of `_Sidebar.md` to its end (and in the generator), so the sidebar of the folder differs from the published one until the merge publishes it; the published wiki is read back after the merge and the result is reported in the pull request and the end-of-run summary. A delta review closes criterion 14 if S01 wants it recorded.

## Action Items

| Action | Owner | Due |
| --- | --- | --- |
| Read the published sidebar and the pages back after the merge (QC-WIKI-001 criterion 14) | S01 | 2026-11-23 |

---

[WIKI]: ../../wiki/
[QC-WIKI-001]: ../../../framework/qc/artifacts/qc-wiki.md
