---
name: proje-teslim-raporu
description: Detaylı proje teslim/devir raporu PDF üretir (ajan ekibiyle). Kullan - "proje raporu", "teslim raporu", "iş teslimi gibi detaylı rapor", "proje PDF raporu", "handover report", "project report pdf", "delivery report". Mimari, teknolojiler, test sonuçları, puanlı kalite değerlendirmesi, riskler, yol haritası içerir.
---

# Proje teslim raporu (PDF)

Report language: the user's (default Turkish). The main session is the **conductor**: it plans, spawns, reviews. It writes no report content. Fixes go back to an agent.

Agent rules: pass `model` + `effort` on every spawn. Sonnet medium by default; sonnet high for evaluative/editor work. Never haiku, never xhigh/max, never two opus in parallel. Parallel agents own disjoint files. Every brief ends with: "Report in ≤150 words." Agents never run destructive git commands.

Every agent brief names: `<P>` project path, `<R>` = `<P>/rapor`, `<S>` = this skill dir, language, audience, and says "read `<S>/references/style-guide.md` first".

## 1. Scope (conductor)

Confirm with the user: project path, audience, language, section set (default below; section 10 optional), report title, any user-provided facts (label them "oturum ölçümü"). Then:

```bash
mkdir -p <P>/rapor/{parts,build/out,assets}
cp <S>/scripts/* <P>/rapor/build/ ; cp <S>/assets/report.css <P>/rapor/assets/
printf 'rapor/parts/\nrapor/build/out/\n' >> <P>/.gitignore
```

## 2. Fact sheet (sonnet medium)

Brief: "Write `<R>/facts.md` for project `<P>`: repo stats (files, LOC, commits), test count via the project's own runner (run it, record command + output line), versions from lockfiles, eval/benchmark results each with file reference, and the user-provided facts below (labeled 'oturum ölçümü'). One line per fact: `- fact: value (source: file | command)`. Unverifiable items go under `## Doğrulanmadı`. Do not edit project files. Facts: <conductor's list>."

Done when every number has a source and test count comes from an actual run.

## 3. Section team (parallel)

Default sections:

| NN | Section | Model/effort |
|---|---|---|
| 01 | Proje tanımı ve kapsam | sonnet medium |
| 02 | Mimari (+ diagram spec) | sonnet medium |
| 03 | Teknolojiler | sonnet medium |
| 04 | Geliştirme süreci (+ timeline spec) | sonnet medium |
| 05 | Değerlendirme ve testler | sonnet medium |
| 06 | Çok yönlü kalite değerlendirmesi (puanlı) | sonnet high |
| 07 | Sınırlamalar ve riskler | sonnet medium |
| 08 | Alternatif teknolojiler | sonnet high |
| 09 | Yol haritası (+ roadmap spec) | sonnet high |
| 10 | CV ve portföy değeri (optional) | sonnet medium |
| 11 | Ekler | sonnet medium |

Group into agents of 2-4 sections (keep evaluative 06/08/09 on high agents). Each agent owns only its `parts/sNN.md` files. Brief template:

> Write `<R>/parts/sNN.md` for sections <list> of a project report on `<P>`. Language: <lang>. Audience: <aud>. Read `<S>/references/style-guide.md`, then the section briefs for your sections in `<S>/references/section-briefs.md`, then `<R>/facts.md`. Use only facts.md numbers or cite file/command. Each file starts with `## <NN>. <Title>` (h2). Inspect the project source as needed. Done when every required table in your section brief exists and every number is traceable. Report in ≤150 words.

## 4. Editor (sonnet high)

Brief: "You own `<R>/build/report.md`, `<R>/assets/*` and `<R>/<Title>.pdf`. Read all `parts/*.md` and `facts.md`. (a) Resolve contradictions against facts.md and list each fix. (b) Remove duplication across parts; edit parts only for these fixes. (c) Write `## Yönetici özeti` (one page: scope, 5 headline numbers, overall score, top 3 risks, next step) as the first section. (d) Draw the diagrams from the specs in parts as inline SVG (no external tools; fixed `viewBox`, `width:100%`, wrapped in `<figure>` with `<figcaption>`, fonts DejaVu Sans, text ≥8pt). (e) Assemble `build/report.md` in section order. (f) Build: `cd <R>/build && uv run --with weasyprint --with markdown python build_pdf.py report.md ../<Title>.pdf --css ../assets/report.css --title '<Title>' --subtitle '<sub>' --meta '<date, author>'`. Report a change log in ≤150 words."

## 5. Layout QA (sonnet medium, separate agent)

Brief: "Own only `<R>/assets/report.css`, minimal table splits in `<R>/build/report.md`, and rebuilding the PDF with the editor's command. Loop (max 3 passes): run `python <R>/build/check_layout.py <pdf>`; render flagged pages plus first and last with `<R>/build/render_pages.sh <pdf> <R>/build/out/png <pages>` (≤6 images total); check text/tables/code beyond the right margin, cut table cells, heading orphaned at page bottom, diagram split across pages, broken Turkish characters, page number and header present. Fix via CSS, rebuild, re-run. Done when check_layout exits 0 and the images show none of the listed defects, or 3 passes are used. Report remaining issues in ≤150 words."

## 6. Conductor review (main session)

Check, without rewriting:
- Spot check ≥5 numbers in the PDF text (`pdftotext`) against facts.md.
- Executive summary agrees with sections 05-07 (score, test count, risks).
- Page count plausible (typically 25-45); QA report clean.
- `grep -nE '/home/|C:\\\\|api[_-]?key|secret|token' ` over `build/report.md` finds no personal paths or secrets.
- No "doğrulanmadı" claim hidden as fact.

Accept, or send targeted fixes to the editor or QA agent (fresh brief naming the exact defect). Commit/push only if the user asks.

## Files

- `references/style-guide.md` writing rules and facts discipline
- `references/section-briefs.md` per-section briefs and required tables
- `scripts/` build_pdf.py, check_layout.py, render_pages.sh; `assets/report.css`
