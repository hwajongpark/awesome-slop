# Awesome Slop [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Tools, research, and word-lists for catching and fixing **AI slop**: the tells that mark writing as machine-generated, in every language you publish in.

Most "AI detector" products are black boxes built and evaluated mainly on English, and they misfire even there: they flag non-native English writing as AI-generated far more often than native writing (Liang et al., 2023, listed under The research below). And AI slop is not only English. In Korean it surfaces as 번역투, in Russian as канцелярит, in Chinese as 公文腔, in Vietnamese as Hán-Việt overuse. This list is organized **by language** and grounded in the research on how AI text actually reads, so you can find the tells, the tools, and the fixes for the languages you work in.

Disclosure: the maintainer of this list also maintains slop-gate, which appears in several sections below.

## Contents

- [What is AI slop](#what-is-ai-slop)
- [The research](#the-research)
- [Catch it: linters](#catch-it-linters)
- [Detect it: classifiers](#detect-it-classifiers)
- [Fix it: humanizers](#fix-it-humanizers)
- [By language](#by-language)
  - [English](#english)
  - [Korean (번역투)](#korean-번역투)
  - [Russian (канцелярит)](#russian-канцелярит)
  - [Chinese (公文腔)](#chinese-公文腔)
  - [Vietnamese (Hán-Việt overuse)](#vietnamese-hán-việt-overuse)
  - [Filipino](#filipino)
- [Word and phrase lists](#word-and-phrase-lists)

## What is AI slop

"Slop" is text that reads as machine-generated: a handful of over-used words, one punctuation mark, and stiff calques that show up far more often in LLM output than in anything a person writes unprompted. Readers have learned to spot it, and the moment they do, trust drops even when the substance is fine.

## The research

What the tells actually are, measured at scale.

- [Quantifying LLM usage in scientific papers](https://www.nature.com/articles/s41562-025-02273-8) - Liang et al., *Nature Human Behaviour* (2025). Over a million papers; "realm," "intricate," "showcasing," and "pivotal" were flat for a decade, then surged from 2023.
- [Delving into LLM-assisted writing through excess vocabulary](https://pmc.ncbi.nlm.nih.gov/articles/PMC12219543/) - Kobak et al., *Science Advances* (2025). 15 million biomedical abstracts; "delve" rose about 1,500% between 2022 and 2024.
- [Monitoring AI-Modified Content at Scale](https://arxiv.org/abs/2403.07183) - Liang et al., ICML 2024. Estimates from word-frequency shifts that 6.5% to 16.9% of peer-review text at major AI conferences in 2023 and 2024 was substantially modified by LLMs.
- [Why Does ChatGPT "Delve" So Much?](https://arxiv.org/abs/2412.11385) - Juzek and Ward, COLING 2025. Identifies 21 words over-represented in scientific abstracts and finds the evidence points to human-feedback fine-tuning rather than training data or architecture.
- [Measuring AI "Slop" in Text](https://arxiv.org/abs/2509.19163) - Shaib et al. (2025). Builds a taxonomy of slop from expert interviews and span-level annotation, and finds that slop judgments track dimensions like coherence and relevance.
- [GPT detectors are biased against non-native English writers](https://arxiv.org/abs/2304.02819) - Liang et al., *Patterns* (2023). Popular detectors misclassify non-native English essays as AI-generated far more often than native ones.
- [EQ-Bench Slop Score](https://eqbench.com/slop-score.html) - Public leaderboard scoring language models on slop words, "not x, but y" constructions, and over-represented trigrams.

## Catch it: linters

Tools that flag specific tells in *your own* prose, locally or in CI.

- [slop-gate](https://github.com/hwajongpark/slop-gate) - Zero-dependency CLI: the em-dash and ~40 English tells, plus opt-in translationese packs for Korean, Russian, Vietnamese, Chinese, and Filipino.
- [Vale](https://github.com/vale-cli/vale) - Customizable prose linter with style rules; the standard for docs teams.
- [alex](https://github.com/get-alex/alex) - Catches insensitive, inconsiderate phrasing.
- [proselint](https://github.com/amperser/proselint) - Lints prose against a body of style-guide best practices.
- [write-good](https://github.com/btford/write-good) - Flags weak, passive, and wordy phrasing.
- [LanguageTool](https://languagetool.org) - Open-source grammar and style checker across many languages.

## Detect it: classifiers

Tools that try to classify whether text is AI-generated. **Treat the verdicts with caution:** detectors produce frequent false positives, are easily bypassed, and should not drive high-stakes decisions about a person.

- [GPTZero](https://gptzero.me) - AI-text detector aimed at education.
- [Originality.ai](https://originality.ai) - AI-detection and plagiarism checking for publishers.
- [Pangram](https://www.pangram.com) - Commercial AI-text classifier with a published technical report and independent academic evaluations of its error rates.
- [Binoculars](https://github.com/ahans30/Binoculars) - Open-source, zero-shot detector that contrasts how two related language models score the same text (ICML 2024).
- [Fast-DetectGPT](https://github.com/baoguangsheng/fast-detect-gpt) - Open-source, zero-shot detector based on conditional probability curvature, much faster than DetectGPT (ICLR 2024).
- [DetectGPT](https://github.com/eric-mitchell/detect-gpt) - Reference implementation of the zero-shot method that checks whether text sits near a local peak of a model's log-probability.
- [Ghostbuster](https://github.com/vivek3141/ghostbuster) - Detector that trains a classifier on features from weaker language models, without needing the target model's token probabilities (NAACL 2024).
- [GLTR](https://github.com/HendrikStrobelt/detecting-fake-text) - Early visual tool that colors each token by how predictable a language model finds it.
- [M4](https://github.com/mbzuai-nlp/M4) - Multilingual, multi-domain, multi-generator benchmark for machine-generated text detection (EACL 2024).
- [RAID](https://github.com/liamdugan/raid) - Benchmark of over 10 million documents across 11 models, 11 domains, and adversarial attacks for testing whether detectors generalize (ACL 2024).
- [Can AI-Generated Text be Reliably Detected?](https://arxiv.org/abs/2303.11156) - Sadasivan et al. (2023). Shows that recursive paraphrasing defeats many detectors and argues there are theoretical limits on reliable detection.

## Fix it: humanizers

Tools that remove tells, by rewriting the text or by stopping the tells at generation time. Use with judgment: the goal is clear human prose, not evading a detector.

- [im-not-ai / Humanize KR](https://github.com/epoko77-ai/im-not-ai) - Claude Code skill that rewrites AI-drafted Korean to strip 번역투 without changing the meaning.
- [antislop-sampler](https://github.com/sam-paech/antislop-sampler) - Sampler that backtracks during generation to suppress thousands of known slop phrases; part of the [Antislop framework](https://arxiv.org/abs/2510.15061) (ICLR 2026).
- [Zero Slop](https://github.com/manavmishra/ZeroSlop) - Agent Skill that scores a draft 0-100 against 290 weighted patterns, then rewrites it under a local fact gate that rejects any version changing a name, number, quotation or link. Offline, standard-library Python, no account; `--batch --gate` also fails a build in CI.

## By language

The fingerprint of AI text differs by language. Each section names the phenomenon and lists the tools for it.

### English

The over-used LLM vocabulary (delve, leverage, robust, tapestry) plus the em-dash.

- [slop-gate vocabulary pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/vocabulary.json) - English LLM overuse words and phrases.
- [slop-gate punctuation pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/punctuation.json) - Punctuation tells, including the em-dash.
- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) - Field guide to the vocabulary, punctuation, and formatting tells of chatbot text, built from real examples in flagged Wikipedia articles.
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup) - The Wikipedia editor project that reviews suspected AI-generated content and maintains the signs guide.

### Korean (번역투)

Translationese: English calques (의 경우, 따라서) and stiff written-register forms. The naturalness lever in Korean editorial writing is stripping 번역투 and restoring native discourse particles.

- [slop-gate Korean pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/korean.json) - Korean translationese patterns and suggested rewrites.
- [영한 번역에 나타난 번역투 문장](https://www.korean.go.kr/nkview/nklife/2012_1/22_0105.pdf) - Article in the National Institute of Korean Language's *새국어생활* (2012) that sorts English-to-Korean translationese by sentence structure, inflection, and prepositional phrases, with natural rewrites.

### Russian (канцелярит)

Bureaucratic register: the copula `является`, split-predicate verbs like `осуществить`. Kornei Chukovsky named it the central disease of the language; Maxim Ilyakhov's *Пиши, сокращай* is the canonical guide against it.

- [slop-gate Russian pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/russian.json) - Russian bureaucratic-register tells.
- [Нора Галь, «Слово живое и мёртвое»](https://fantlab.ru/work397792) - Catalog page for the 1972 translator's and editor's handbook whose chapters on канцелярит made it the standard reference against it.

### Chinese (公文腔)

Officialese: `进行`+noun padding, `予以`, and stock openers like `众所周知`.

- [slop-gate Chinese pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/chinese.json) - Chinese officialese and padding patterns.
- [地道中文怎么写？英中翻译要避免哪些坑？](https://sspai.com/post/59943) - 少数派 article with before-and-after examples of 翻译腔 and 欧化 sentence patterns, such as stray passives and English-style openers.

### Vietnamese (Hán-Việt overuse)

Sino-Vietnamese vocabulary and calque openers (`thực hiện`, `trong trường hợp`) where plain Vietnamese is simpler.

- [slop-gate Vietnamese pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/vietnamese.json) - Vietnamese calque and over-formality patterns.

### Filipino

Over-formal literary Tagalog and calque openers (`upang`, `sa pamamagitan ng`) where editorial Filipino is conversational Taglish.

- [slop-gate Filipino pack](https://github.com/hwajongpark/slop-gate/blob/main/rules/filipino.json) - Filipino over-formality and calque patterns.

## Word and phrase lists

The raw lists of tells, editable and worth reading.

- [slop-gate rule packs](https://github.com/hwajongpark/slop-gate/tree/main/rules) - JSON lists of tells per language, each with a suggested fix.
- [Your AI Slop Word Blacklist Is a Request. Build a Gate.](https://blog.atharvashah.com/p/the-ultimate-ai-slop-word-blacklist) - Short starter list (six words, four phrases) plus an argument for enforcing it with a script that scores each draft rather than a prompt instruction.

## Contributing

Contributions are welcome. Read the [contribution guidelines](contributing.md) first.

Licensed under [CC0 1.0](LICENSE): to the extent possible under law, the contributors have waived all copyright and related rights to this list.
