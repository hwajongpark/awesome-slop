# awesome-slop [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Tools, research, and word-lists for catching and fixing **AI slop**: the tells that mark writing as machine-generated, in every language you publish in.

Most "AI detector" products are English-only black boxes. But AI slop is not only English. In Korean it surfaces as 번역투, in Russian as канцелярит, in Chinese as 公文腔, in Vietnamese as Hán-Việt overuse. This list is organized **by language** and grounded in the research on how AI text actually reads, so you can find the tells, the tools, and the fixes for the languages you work in.

## Contents

- [What is AI slop?](#what-is-ai-slop)
- [The research](#the-research)
- [Catch it: linters](#catch-it-linters)
- [Detect it: classifiers](#detect-it-classifiers)
- [Fix it: humanizers](#fix-it-humanizers)
- [By language](#by-language)
- [Word and phrase lists](#word-and-phrase-lists)
- [Contributing](#contributing)

## What is AI slop?

"Slop" is text that reads as machine-generated: a handful of over-used words, one punctuation mark, and stiff calques that show up far more often in LLM output than in anything a person writes unprompted. Readers have learned to spot it, and the moment they do, trust drops even when the substance is fine.

## The research

What the tells actually are, measured at scale.

- [Quantifying LLM usage in scientific papers](https://www.nature.com/articles/s41562-025-02273-8) - Liang et al., *Nature Human Behaviour* (2025). Over a million papers; "realm," "intricate," "showcasing," and "pivotal" were flat for a decade, then surged from 2023.
- [Delving into LLM-assisted writing through excess vocabulary](https://pmc.ncbi.nlm.nih.gov/articles/PMC12219543/) - *Science Advances* (2025). 15 million biomedical abstracts; "delve" rose about 1,500% between 2022 and 2024.

## Catch it: linters

Tools that flag specific tells in *your own* prose, locally or in CI.

- [slop-gate](https://github.com/hwajongpark/slop-gate) - Zero-dependency CLI: the em-dash and ~40 English tells, plus opt-in translationese packs for Korean, Russian, Vietnamese, Chinese, and Filipino.
- [Vale](https://github.com/errata-ai/vale) - Customizable prose linter with style rules; the standard for docs teams.
- [alex](https://github.com/get-alex/alex) - Catches insensitive, inconsiderate phrasing.
- [proselint](https://github.com/amperser/proselint) - Lints prose against a body of style-guide best practices.
- [write-good](https://github.com/btford/write-good) - Flags weak, passive, and wordy phrasing.
- [LanguageTool](https://languagetool.org) - Open-source grammar and style checker across many languages.

## Detect it: classifiers

Tools that try to classify whether text is AI-generated. **Treat the verdicts with caution:** detectors produce frequent false positives, are easily bypassed, and should not drive high-stakes decisions about a person.

- [GPTZero](https://gptzero.me) - AI-text detector aimed at education.
- [Originality.ai](https://originality.ai) - AI-detection and plagiarism checking for publishers.

## Fix it: humanizers

Tools that rewrite text to remove tells. Use with judgment: the goal is clear human prose, not evading a detector.

- [im-not-ai / Humanize KR](https://github.com/epoko77-ai/im-not-ai) - Claude Code skill that rewrites AI-drafted Korean to strip 번역투 without changing the meaning.
- [QuillBot](https://quillbot.com) - Paraphrasing and rewriting (English-focused).
- [Undetectable AI](https://undetectable.ai) - Rewrites AI text (English-focused).

## By language

The fingerprint of AI text differs by language. Each section names the phenomenon and lists the tools for it.

### English

The over-used LLM vocabulary (delve, leverage, robust, tapestry) plus the em-dash.

- [slop-gate](https://github.com/hwajongpark/slop-gate), [Vale](https://github.com/errata-ai/vale), [alex](https://github.com/get-alex/alex), [proselint](https://github.com/amperser/proselint).

### Korean — 번역투

Translationese: English calques (의 경우, 따라서) and stiff written-register forms. The naturalness lever in Korean editorial writing is stripping 번역투 and restoring native discourse particles.

- [slop-gate korean pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/korean.json), [im-not-ai](https://github.com/epoko77-ai/im-not-ai).

### Russian — канцелярит

Bureaucratic register: the copula `является`, split-predicate verbs like `осуществить`. Kornei Chukovsky named it the central disease of the language; Maxim Ilyakhov's *Пиши, сокращай* is the canonical guide against it.

- [slop-gate russian pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/russian.json).

### Chinese — 公文腔

Officialese: `进行`+noun padding, `予以`, and stock openers like `众所周知`.

- [slop-gate chinese pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/chinese.json).

### Vietnamese — Hán-Việt overuse

Sino-Vietnamese vocabulary and calque openers (`thực hiện`, `trong trường hợp`) where plain Vietnamese is simpler.

- [slop-gate vietnamese pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/vietnamese.json).

### Filipino

Over-formal literary Tagalog and calque openers (`upang`, `sa pamamagitan ng`) where editorial Filipino is conversational Taglish.

- [slop-gate filipino pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/filipino.json).

## Word and phrase lists

The raw lists of tells, editable and worth reading.

- [slop-gate rule packs](https://github.com/hwajongpark/slop-gate/tree/main/rules) - JSON lists of tells per language, each with a suggested fix.

## Contributing

Contributions are welcome: a tool, a research link, or a language section. Every entry must be a real, working resource with a one-line description, and the per-language sections especially need help from native speakers. Detectors are listed with a caution by design; humanizers are listed without endorsing detector-evasion.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the maintainers have waived all copyright and related rights to this work.
