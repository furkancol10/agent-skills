# agent-skills

Claude Code skills built while working on AI/RAG projects. Each skill lives in `skills/<name>/` with a `SKILL.md` and its bundled references, assets and scripts.

| Skill | What it does |
|---|---|
| [`proje-teslim-raporu`](skills/proje-teslim-raporu/SKILL.md) | Produces a detailed project handover report as a PDF with a team of agents: a fact-sheet agent, parallel section writers, an editor that merges them, and a separate layout-QA agent that checks the PDF pages for overflow and broken breaks. The main session only plans and reviews. Reports default to Turkish. |

## Install

Copy or symlink a skill folder into your Claude Code skills directory:

```bash
git clone https://github.com/furkancol10/agent-skills.git
ln -s "$PWD/agent-skills/skills/proje-teslim-raporu" ~/.claude/skills/proje-teslim-raporu
```

## Requirements (proje-teslim-raporu)

- [uv](https://docs.astral.sh/uv/) — the PDF build runs `uv run --with weasyprint --with markdown`, nothing to install globally
- `poppler-utils` (`pdftotext`, `pdftoppm`) for the layout checker and page renders
- A font with Turkish glyphs (DejaVu Sans or Noto Sans)

## Türkçe

Yapay zeka / RAG projelerinde geliştirdiğim Claude Code skill'leri. `proje-teslim-raporu`, bir projeyi ajan ekibiyle inceleyip iş teslimi düzeyinde detaylı bir PDF rapor üretir: olgu toplayıcı, paralel bölüm yazarları, birleştiren editör ve sayfa taşmalarını denetleyen ayrı bir düzen kontrol ajanı. Ana oturum yalnızca planlar ve son incelemeyi yapar.

## License

MIT
