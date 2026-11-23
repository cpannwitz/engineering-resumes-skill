# Plan — Claude Code Skill from the EngineeringResumes Wiki

TickTick: 💼Work › "Create Claude Code Skill of EngineeringResumes Wiki" (due 2026-11-23)

Goal: a public, git-tracked Claude Code skill that **creates, reviews and improves** a CV/Lebenslauf,
built on the r/EngineeringResumes wiki. Optional: publish it so others can install it.

---

## Phase 0 — Source material  ✅
- [x] Save the wiki into `source/` (Claude can't fetch reddit.com). Options:
      browser "Save as" → PDF/HTML, or copy the page text into `source/wiki-index.md`.
      Include linked sub-pages that matter (e.g. bullet-writing / template pages).
- [ ] `source/` is git-ignored: the wiki is third-party content. The skill **paraphrases**
      the rules in our own words and links back — no verbatim copy in the public repo.

## Phase 1 — Repository  ✅
- [x] Local folder `~/privatespace/engineering-resumes-skill` with skeleton
- [x] `git init`, first commit
- [x] Chris: create **empty public** repo `cpannwitz/engineering-resumes-skill` on github.com
      (no README/license, so the first push is clean)
- [x] Claude: attach repo, add remote, push
- [x] License: MIT (same as berlin-job-search)

## Phase 2 — Skill design (decisions)
- [x] Scope of modes: Create / Review / Improve; job-posting tailoring is delegated to
      berlin-job-search `/apply` (see Companion skill)
- [x] **One skill, language-driven rules** (decided 2026-11-23): the CV's language — or the
      target language/market if given — selects the rule set. English → wiki rules
      (US/Canada). German → Lebenslauf conventions (`references/german-lebenslauf.md`),
      with the wiki's content advice (bullets, impact, skills) still applying where it fits.
- [x] **Output: LaTeX + Markdown** (decided 2026-11-23): LaTeX template for the final PDF
      (local TeX via brew), Markdown for quick drafts and review reports.
- [x] Input formats for Review: PDF (text + page image), DOCX (pandoc), Markdown/LaTeX, pasted text

## Companion skill — berlin-job-search
Repo: https://github.com/umutyesildal/berlin-job-search (MIT, v0.2.0). Installed separately in
Claude Code; our skill complements it instead of duplicating it.

| Concern | Owner |
|---|---|
| CV craft: layout, section order, bullet formula, action verbs, review checklist (wiki) | **engineering-resume** |
| LaTeX output (final PDF via local TeX) | **engineering-resume** |
| Germany-specific rules: Lebenslauf conventions, photo/personal data, Anschreiben, submission, Arbeitszeugnis (`references/applications-germany.md`) | **berlin-job-search** |
| Job search, posting evaluation, tailoring to a posting (`/apply`), ATS check (`ats_check.py`), Markdown→PDF render, tracking | **berlin-job-search** |

- German mode: if berlin-job-search is installed, defer to its `applications-germany.md` for
  Lebenslauf conventions and apply our wiki-based content rules on top. Ship a short fallback
  `references/german-lebenslauf.md` for users without it (adapt with MIT attribution in NOTICE.md
  if we reuse its wording).
- "Tailor to a posting" → hand off to berlin-job-search `/apply` rather than rebuilding it.
- Reuse its `assets/cv-template-en.md` / `lebenslauf-template-de.md` structure as the Markdown
  shape, so drafts move between both skills without conversion.
- Open: can our LaTeX template be a render target for its `/apply` output? (relates to the
  TickTick task "Install Claude Code Skill berlin-job-search").

## Phase 3 — Write the skill  ✅ v0.1.0
Layout (progressive disclosure — SKILL.md stays short, details live in references/):
```
skills/engineering-resume/
  SKILL.md                     # when to use, workflow per mode, pointers to references
  references/
    formatting.md              # layout, fonts, length, section order, ATS notes
    bullets.md                 # bullet formula, action verbs, quantifying impact
    sections.md                # summary, skills, experience, projects, education
    review-checklist.md        # scored checklist used by Review mode
    german-lebenslauf.md       # DE-specific deltas (if in scope)
  templates/
    resume.tex                 # LaTeX template (or link to recommended one)
    resume.md
```
- [x] Distill wiki → references (paraphrased, with source links)
- [x] Workflows: Create (interview → draft), Review (checklist → findings ranked by impact),
      Improve (rewrite bullets, before/after)
- [x] Description/trigger wording
- [x] LaTeX templates compile with pdflatex (no babel/mathdesign needed, BasicTeX-friendly)

## Phase 4 — Test
- [x] Run Review on Chris's own CVs (English + German PDFs from the job-search project);
      keep test files in git-ignored `test-cvs/`
      - EN reviewed 2026-11-23 (6/22) → found gap: studies without degree → rule added
      - DE pending: German CV still has placeholder bullets for the current role
- [ ] Install the plugin locally from GitHub and test it inside Claude Code (Chris)
- [ ] Run Create from scratch with a fictional profile
- [ ] Iterate on SKILL.md until results are consistent; commit each iteration

## Phase 5 — Publish
- [x] README: what it does, install, examples, credits
- [x] Make the repo a Claude Code plugin marketplace (`.claude-plugin/marketplace.json`)
      so others can install with `/plugin marketplace add cpannwitz/engineering-resumes-skill`
- [ ] Optional: submit to community skill/plugin directories
- [ ] Optional: tell r/EngineeringResumes mods (they may want to link it — or object)

## Related
- TickTick 💼Work › "Install Claude Code Skill berlin-job-search" — runs in parallel;
  shares the LaTeX CV templates and the Dresden job-search angle.
