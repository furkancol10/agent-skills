# Style guide (all report agents)

## Writing
- First sentence of every section and subsection states the point, with a number when one exists.
- Items x attributes go in tables; prose carries reasoning only.
- Sentences under 25 words. Plain wording; no emoji, no marketing tone.
- Headings: `##` section (starts a page), `###` subsection, `####` rarely. No deeper.
- Relative paths only, e.g. `src/cli.py`. Replace home-directory paths with the repo-relative form.
- Code and long identifiers go in backticks; table cells stay short (CSS wraps them).
- Diagrams and timelines: write a spec block (nodes, edges, labels, order) in a fenced block tagged `diagram-spec`; the editor draws them as inline SVG and removes the spec.

## Facts discipline
- A number appears only if it is in `rapor/facts.md` or you ran the command and cite it as `(kaynak: dosya | komut)`.
- Anything unconfirmed is written "doğrulanmadı" with what would verify it.
- Scores and judgments are labeled as assessment ("değerlendirme"), with the evidence that supports each.
- Facts labeled "oturum ölçümü" are quoted as such, not as repository facts.
- Contradiction between your text and facts.md: facts.md wins; fix your text.
