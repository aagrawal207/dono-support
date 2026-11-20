# Data licences

Every source used to build `Data/lexicon/` and `Data/emoji/`, with what was read to confirm its licence. All licences were read on the source's own page on 20 November 2026. URLs are pinned in `tools/lexicon/common.py` and checksums in `tools/lexicon/checksums.txt`.

## Licence of the built files

| File | Licence | Why |
|---|---|---|
| `words-en.tsv` | CC BY-SA 4.0 | Counts come partly from FrequencyWords (CC BY-SA 4.0); word forms from AOSP (Apache 2.0); counts also from Tatoeba (CC BY 2.0 FR) and Common Voice (CC0). |
| `bigrams-en.tsv` | CC BY 2.0 FR | Counted from Tatoeba (CC BY 2.0 FR) and Common Voice (CC0), filtered to words of `words-en.tsv`. Treat as CC BY-SA 4.0 if in doubt. |
| `words-hi.tsv`, `bigrams-hi.tsv` | CC BY-SA 4.0 | Spellings and their weights come from Dakshina (CC BY-SA 4.0); Hindi counts partly from FrequencyWords (CC BY-SA 4.0). |
| `blocklist-en.txt` | Apache 2.0 | AOSP "possibly offensive" flags plus Dono's own lists. |
| `blocklist-hi.txt`, `domains.txt`, `manual-en.tsv`, `manual-hi.tsv` | Dono's own | Written by hand for Dono. |
| `emoji.tsv`, `skin-tones.tsv` | Unicode License v3 | From emoji-test.txt and CLDR, plus Dono's own Hinglish keywords. |
| `default-frequent.txt` | Dono's own | Order taken from Unicode's published frequency ranking, which is a list of facts. |

**Share-alike.** The CC BY-SA 4.0 files stay CC BY-SA 4.0, and so does the binary dictionary built from them. The app must show the credits below, and the derived lists must be offered under CC BY-SA 4.0. The simplest way is to publish `Data/lexicon/` on the support site with this file. CC BY-SA covers the data only, not the app's code.

## Sources used

| Source | URL and version | Licence, and where it was read | What was taken | How it was changed |
|---|---|---|---|---|
| AOSP LatinIME dictionaries | `android.googlesource.com/platform/packages/inputmethods/LatinIME`, commit `127336e9`, files `dictionaries/en_wordlist.combined.gz`, `en_US_…`, `en_GB_…` (dictionary version 54) | Apache 2.0. Read the repository's `NOTICE` file ("Copyright (c) 2008, The Android Open Source Project, Licensed under the Apache License, Version 2.0"). | Word forms with capitals, frequency classes, `possibly_offensive` flags | Union of the three lists; `not_a_word` entries dropped; used as the English validity list; flags turned into the blocklist. |
| FrequencyWords (Hermit Dave) | `github.com/hermitdave/FrequencyWords`, commit `525f9b56`, `content/2018/en/en_full.txt` and `hi/hi_full.txt` (OpenSubtitles 2018) | README section "License": "MIT License for code. CC-by-sa-4.0 for content." | Word counts from film subtitles, English and Hindi | Kept only words in the AOSP list (English) or valid Devanagari words (Hindi); blended with other counts. |
| Tatoeba | `downloads.tatoeba.org/exports/per_language/{eng,hin}/…_sentences.tsv.bz2`, weekly export of 14 November 2026 | Downloads page: "These files are released under CC BY 2.0 FR." | English and Hindi sentences | Word and pair counts only; no sentence is shipped. |
| Mozilla Common Voice | `github.com/common-voice/common-voice`, commit `9f55dafb`, `server/data/{en,hi}/sentence-collector.txt` | README "Licensing and content source": sentence text "released under a CC0 public domain" licence; `server/data/en/LICENSE` is CC0 1.0. | English and Hindi sentences | Word and pair counts only. |
| IndicCorp v2 (AI4Bharat) | `huggingface.co/datasets/ai4bharat/IndicCorpV2`, revision `2d7285e6`, four 90 MB slices of `data/hi-1.txt`, `hi-2.txt`, `hi-3.txt` | `github.com/AI4Bharat/IndicBERT` README "LICENSE": "All the datasets created as part of this work will be released under a CC-0 license." The Hugging Face card has no licence field. | Hindi news text, streamed, never stored | Word and pair counts only. |
| Dakshina (Google Research) | `storage.googleapis.com/gresearch/dakshina/dakshina_dataset_v1.0.tar` (v1.0, 27 May 2020); only `hi/lexicons/*` and two `hi/romanized/*` files, fetched by byte range | README "License": "The dataset is licensed under CC BY-SA 4.0." | Human romanisations of Hindi words with attestation counts; 10,000 romanised sentences | Spellings lowercased and weighted; misaligned tokens dropped; sentence capitals used to spot names. |
| Aksharantar (AI4Bharat) | `huggingface.co/datasets/ai4bharat/Aksharantar`, revision `e418c1fc`, `hin.zip` | Dataset card "Licensing Information": manually collected data CC BY; mined data (Samanantar, IndicCorp) CC0; existing sources CC0. | Rows with source `IndicCorp` (mined, CC0, score ≥ −0.35) and `AK-Freq` (manual, CC BY 4.0) as spelling evidence; `Wikidata` and `Samanantar` rows only as a signal that a word is a name | Rows from `Existing` were not used, because the card does not say which third-party sets they come from. `Dakshina` rows were not used again. |
| Hinglish-TOP (Google Research) | `github.com/google-research-datasets/Hinglish-TOP-Dataset`, commit `fdd3998a`, `Dataset/Human Annotated Data/*.tsv` | `LICENSE.md` is the Apache License 2.0; the GitHub repository licence is Apache 2.0. | Human-written code-mixed queries | Romanised token and pair counts; the synthetic part was not used. |
| Unicode emoji-test.txt | `www.unicode.org/Public/18.0.0/emoji/emoji-test.txt` (Emoji 18.0, 30 April 2026) | Unicode License v3, read at `www.unicode.org/license.txt`. | Fully-qualified emoji, groups, subgroups, names, E versions | Toned forms moved to `skin-tones.tsv`. |
| Unicode CLDR annotations | `github.com/unicode-org/cldr`, tag `release-49`, `common/annotations` and `common/annotationsDerived` for `en`, `en_001`, `en_IN`, `hi_Latn` | File headers: "SPDX-License-Identifier: Unicode-3.0"; Unicode License v3 as above. | English and Hinglish keywords | `↑↑↑` resolved through hi_Latn → en_IN → en_001 → en; flag names added as keywords; Dono's own Hinglish keywords added. |
| Unicode Emoji Frequency | `home.unicode.org/emoji/emoji-frequency/` (2019 ranking) | Unicode terms of use; only the order of the first 30 emoji was used, which is a fact, not copied text. | Ranking | Used to order `default-frequent.txt`. |

## Sources looked at and not used

| Source | Why not |
|---|---|
| Leipzig Corpora Collection | Its download and licence pages sit behind a bot wall (Anubis), so the licence could not be read on its own page. |
| L3Cube-HingCorpus | CC BY-NC-SA 4.0: non-commercial. |
| CMU Hinglish DoG (festvox on Hugging Face) | The card's metadata says CC BY-SA 3.0 and GFDL, but its "Licensing Information" says "More Information Needed" and the original repository has no licence: unclear. |
| Hinglish-TOP synthetic data | Machine-generated, so it does not show how people spell. |
| LLM-generated Hinglish sets on Hugging Face | Synthetic, and most have no licence or a licence that does not cover the model output. |
| OpenSubtitles raw text (OPUS) | No licence for the subtitle text; only FrequencyWords' licensed counts were used. |
| Aksharantar `Existing` rows | Third-party provenance not stated. |
| SCOWL | Not needed: the AOSP union already holds both American and British spellings. |

## Credit lines for the app

Show these on the app's acknowledgements screen:

- Word lists from the Android Open Source Project, © 2008 The Android Open Source Project, Apache License 2.0.
- Word frequencies from FrequencyWords by Hermit Dave, built from OpenSubtitles 2018, CC BY-SA 4.0.
- Sentences from Tatoeba (tatoeba.org), CC BY 2.0 FR.
- Sentences from Mozilla Common Voice, CC0.
- IndicCorp v2 and Aksharantar by AI4Bharat, CC0 and CC BY 4.0.
- Dakshina dataset by Google Research, CC BY-SA 4.0.
- Hinglish-TOP dataset by Google Research, Apache License 2.0.
- Emoji data from the Unicode Consortium (emoji-test.txt and CLDR), © 1991–2026 Unicode, Inc., Unicode License v3.
- Dono's English and Hinglish dictionaries are derived from these sources and are shared under CC BY-SA 4.0.

The Apache 2.0 sources need the licence text and the AOSP `NOTICE` text in the app's acknowledgements. The Unicode data needs the Unicode copyright and permission notice (the text at `www.unicode.org/license.txt`) in the acknowledgements.
