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

## Phase 1 — Repository  ✅ (license still open)
- [x] Local folder `~/privatespace/engineering-resumes-skill` with skeleton
- [x] `git init`, first commit
- [x] Chris: create **empty public** repo `cpannwitz/engineering-resumes-skill` on github.com
      (no README/license, so the first push is clean)
- [x] Claude: attach repo, add remote, push
- [ ] Choose a license (MIT suggested for the code/skill text)

## Phase 2 — Skill design (decisions)
- [ ] Scope of modes: Create / Review / Improve (+ tailor-to-job-posting inside Improve?)
- [x] **One skill, language-driven rules** (decided 2026-11-23): the CV's language — or the
      target language/market if given — selects the rule set. English → wiki rules
      (US/Canada). German → Lebenslauf conventions (`references/german-lebenslauf.md`),
      with the wiki's content advice (bullets, impact, skills) still applying where it fits.
- [x] **Output: LaTeX + Markdown** (decided 2026-11-23): LaTeX template for the final PDF
      (local TeX via brew), Markdown for quick drafts and review reports.
- [ ] Input formats for Review: PDF, DOCX, Markdown, pasted text.

## Phase 3 — Write the skill
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
- [ ] Distill wiki → references (paraphrased, with source links)
- [ ] Workflows: Create (interview → draft), Review (checklist → findings ranked by impact),
      Improve (rewrite bullets, before/after)
- [ ] Use `skill-creator` guidance for the description/trigger wording

## Phase 4 — Test
- [ ] Run Review on Chris's own CVs (English + German PDFs from the job-search project);
      keep test files in git-ignored `test-cvs/`
- [ ] Run Create from scratch with a fictional profile
- [ ] Iterate on SKILL.md until results are consistent; commit each iteration

## Phase 5 — Publish
- [ ] README: what it does, install, examples, credits
- [ ] Make the repo a Claude Code plugin marketplace (`.claude-plugin/marketplace.json`)
      so others can install with `/plugin marketplace add cpannwitz/engineering-resumes-skill`
- [ ] Optional: submit to community skill/plugin directories
- [ ] Optional: tell r/EngineeringResumes mods (they may want to link it — or object)

## Related
- TickTick 💼Work › "Install Claude Code Skill berlin-job-search" — runs in parallel;
  shares the LaTeX CV templates and the Dresden job-search angle.
