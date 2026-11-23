---
name: engineering-resume
description: Create, review and improve engineering CVs, résumés and German Lebensläufe using r/EngineeringResumes guidelines, with German rules for German CVs and LaTeX + Markdown output. Use when the user asks to write, critique, score, rewrite or polish a CV, résumé, Lebenslauf or its bullet points for a technical role.
---

# Engineering Resume

Three modes — **Create**, **Review**, **Improve** — on one shared rule base distilled from the
r/EngineeringResumes wiki, plus German Lebenslauf rules. Drafts and reports are Markdown; the
final document is LaTeX compiled to PDF.

## 1. Choose the rule set

Decide before anything else, and say which one you picked in one line:

1. The user names a target language or market ("for a German employer", "US job") → use that.
2. A job posting is given → its language decides.
3. Otherwise the CV's own language decides (Create mode: ask, default to the user's language).

| Rule set | Read |
|---|---|
| **EN** (US/Canada-style résumé) | `references/formatting.md`, `references/sections.md`, `references/bullets.md` |
| **DE** (Lebenslauf) | `references/german-lebenslauf.md` first, then the same three files — its table overrides them. If the **berlin-job-search** skill is available, also read its `references/applications-germany.md`; it wins on German application conventions |

English CV for a German employer: EN rules, but keep phone and city in the header and add a
Languages line with the German level.

## 2. Pick the mode

| User intent | Mode |
|---|---|
| "Write / build / start my CV", no existing CV | **Create** |
| "Review / critique / score / what's wrong with my CV" | **Review** |
| "Rewrite / improve / fix / polish / shorten", or after a Review | **Improve** |
| Tailor to one specific job posting, cover letter, Anschreiben, ATS check against a posting | Hand off to **berlin-job-search** (`/apply`) if available; otherwise do Improve with the posting as input |

### Reading an existing CV
- PDF: `pdftotext -layout cv.pdf -` for text; also render page 1 to an image
  (`pdftoppm -png -r 80 -f 1 -l 1 cv.pdf page`) and look at it — layout problems are invisible in text.
- DOCX: `pandoc cv.docx -t markdown`, or the docx skill if available. LaTeX/Markdown: read directly.

## 3. Create

1. Ask for: target role(s) and seniority, rule set, and existing material (LinkedIn export, old
   CV, notes). Use what exists before asking more.
2. Pick the section order from `sections.md` for the user's career stage.
3. Interview role by role with the prompts in `bullets.md` → "Finding content". One role at a
   time; brain-dump first, then cut.
4. Draft in Markdown from `templates/resume-en.md` or `templates/lebenslauf-de.md`. Mark
   anything unconfirmed `[?]`.
5. Self-check the draft against `references/review-checklist.md`; fix before showing.
6. Show the draft plus the list of `[?]` items. After confirmation, render (§6).

## 4. Review

1. Read the CV (text **and** page image). Determine career stage and target role; ask only if
   the target role can't be inferred.
2. Score against `references/review-checklist.md`, using the report format at its end.
3. Rank findings by impact on getting an interview — content problems (duties instead of
   impact, weak first bullets, missing target-role signal) usually outrank cosmetic ones.
4. For the 3–5 weakest bullets, give before → after rewrites; mark needed facts `[?]`.
5. Write the report to `cv-review-<YYYY-MM-DD>.md` next to the CV when working in a folder;
   otherwise reply inline. Offer Improve as the next step.

## 5. Improve

1. Start from a Review (run one silently if none exists) so changes are justified.
2. Rewrite in place, section by section, following `bullets.md`. Keep every fact the user
   gave; do not add employers, tools, numbers or responsibilities they didn't state.
3. Where a number would strengthen a bullet, ask for it; never estimate. Use scope or audience
   when no number exists.
4. Fit the page budget by cutting the least relevant content, never by shrinking type or margins.
5. Show a before/after table for changed bullets, then render (§6).

## 6. Render to PDF

1. Copy `templates/resume-en.tex` or `templates/lebenslauf-de.tex` to the working folder as
   `<Firstname>-<Lastname>-CV-EN.tex` / `<Vorname>-<Nachname>-Lebenslauf.tex`; fill it from the
   Markdown draft. Escape LaTeX specials (`%`, `&`, `#`, `_`, `$`). Use `--` for date ranges.
2. Build: `latexmk -pdf -interaction=nonstopmode <file>.tex` (fallback: `pdflatex` twice).
3. Verify, and fix before handing over:
   - page count matches the budget (`pdfinfo`)
   - render pages to PNG and look: no orphan words on bullet second lines, no overflow,
     no hyphenation, dates aligned
   - text is selectable and in reading order (`pdftotext -layout`)
4. If no TeX is installed: on macOS `brew install --cask mactex-no-gui` (full), or
   `brew install --cask basictex` then `sudo tlmgr install enumitem titlesec latexmk`.
   If the user doesn't want TeX, deliver the Markdown and stop.
5. Optional ATS check: if berlin-job-search is available, run its `scripts/ats_check.py` on the PDF.

## 7. Working with berlin-job-search

When both skills are installed, they share one fact file: berlin-job-search's
`job-search/cv.md` (master CV, single source of facts).

| Task | Who does what |
|---|---|
| Review a CV, no posting | This skill's Review mode → berlin-job-search `scripts/ats_check.py <pdf> --type cv` |
| Build or refresh the master CV | This skill's Improve mode → write `job-search/cv.md` in the shape of `templates/resume-en.md` (same as berlin-job-search `assets/cv-template-en.md`) → render general EN/DE PDFs (§6) |
| Profile, job search, posting evaluation | berlin-job-search (`/setup`, `/jobs`, `/evaluate`) |
| Tailor to a posting (`/apply`) | berlin-job-search runs the workflow. If this skill is loaded during it: apply `references/bullets.md` (EN) or `references/german-lebenslauf.md` (DE) in the writer pass, add checklist sections E and F to its reviewer pass, and offer a LaTeX render (§6) of the final CV followed by `ats_check.py --jd` |

berlin-job-search wins on German application conventions, truthfulness and safety; this skill
wins on bullet wording and layout. When the user supplies a new fact, add it to
`job-search/cv.md` first so later applications can use it.

For guaranteed use during `/apply`, put these rules in the workspace's `CLAUDE.md`. A
command's own instructions take priority over skills that happen to be loaded.

## Rules that always apply

- **Honesty:** never invent or inflate. Every claim traces to something the user said or
  wrote. List open `[?]` items at the end of every draft.
- **Privacy:** CVs are personal data. Don't commit them to public repos; keep test CVs out of git.
- Explain a rule in one short clause when it changes the user's text, so they learn the pattern.
- The wiki's rules are strong defaults, not laws: if the user deliberately breaks one
  (e.g. keeps a photo on a German CV), note the trade-off once and follow their choice.

## Files

| File | Use |
|---|---|
| `references/formatting.md` | Layout, typography, length, dates, ATS (EN) |
| `references/sections.md` | Order, header, experience, projects, education, skills, senior/career-change (EN) |
| `references/bullets.md` | Bullet shape, formulas, verbs, interview prompts, honesty |
| `references/german-lebenslauf.md` | DE overrides and German bullet style |
| `references/review-checklist.md` | Scored checklist + report format |
| `templates/*.md` | Markdown draft shapes (compatible with berlin-job-search templates) |
| `templates/*.tex` | LaTeX templates, tested with pdflatex |
