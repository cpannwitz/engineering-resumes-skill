# engineering-resumes-skill

A Claude Code skill to **create, review and improve** engineering CVs — English résumés and
German Lebensläufe — based on the guidelines of the
[r/EngineeringResumes wiki](https://www.reddit.com/r/EngineeringResumes/wiki/index/).

- **Create** — interviews you role by role and drafts a CV in Markdown
- **Review** — scores your CV against a 10-area checklist and ranks fixes by impact
- **Improve** — rewrites bullets (impact, metrics, strong verbs) without inventing anything
- **Language-aware** — English CVs follow the wiki (US/Canada style); German CVs follow
  Lebenslauf conventions (tabular, MM/YYYY, Sprachen with CEFR levels, optional photo)
- **LaTeX output** — clean single-column templates for EN and DE, compiled and checked for
  page count, orphan words and hyphenation

## Install (Claude Code)

```text
/plugin marketplace add cpannwitz/engineering-resumes-skill
/plugin install engineering-resumes@engineering-resumes
```

Then: *"Review my CV"* (attach or point to a PDF), *"Help me write a résumé for backend roles"*,
or *"Überarbeite meinen Lebenslauf"*.

PDF output needs a TeX installation, e.g. `brew install --cask mactex-no-gui` on macOS
(or BasicTeX plus `sudo tlmgr install enumitem titlesec latexmk`).

## Works well with

[berlin-job-search](https://github.com/umutyesildal/berlin-job-search) — job search in Germany,
posting evaluation, tailoring to a posting (`/apply`), Anschreiben and ATS checks. When it is
installed, this skill defers to it for German application conventions and posting-specific
tailoring. Both share berlin-job-search's `job-search/cv.md` as the master CV. To make `/apply`
use this skill's bullet rules and LaTeX output reliably, add the rules from SKILL.md §7 to the
`CLAUDE.md` of the folder you run the job search in.

## Layout

```
skills/engineering-resume/
  SKILL.md                    workflows: rule-set choice, Create, Review, Improve, render
  references/                 formatting, sections, bullets, german-lebenslauf, review-checklist
  templates/                  resume-en.{md,tex}, lebenslauf-de.{md,tex}
```

## Credits

Guidelines summarised and adapted from the r/EngineeringResumes community wiki; see
[NOTICE.md](NOTICE.md). Not affiliated with Reddit or the subreddit moderators.

## License

MIT
