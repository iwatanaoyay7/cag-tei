# Changelog

Corrections are made in the source data, checked on the page images, and published here as new versions.
Each file's `revisionDesc` records the changes to that file. Version numbers: the third digit for corrections of
readings and numbers, the second for additions to the encoding or larger revisions of the divisions, the first for
changes that affect how passages are cited.

## 1.0.2 (2026-11-18)

- Bekker references of 13 lemmata, misread by the OCR, corrected on the page images
  (`milestone[@unit='bekker']/@n`; the text is unchanged):
  Alexander, *In Metaphysica* (`tlg0732.tlg004`) p. 284 `1007a8`, p. 547 `1042b9`, p. 683 `1071a11`;
  Philoponus, *In Categorias* (`tlg4015.tlg001`) p. 17 `1a1`, p. 68 `3a29`;
  Philoponus, *In Analytica priora* (`tlg4015.tlg002`) p. 379 `52a24`;
  Ammonius, *In De interpretatione* (`tlg4016.tlg003`) p. 29 `16a19`, p. 266 `23b32`;
  Syrianus, *In Metaphysica* (`tlg4017.tlg001`) p. 146 `1084a2`, p. 148 `1084a18`;
  Eustratius et al., *In Ethica Nicomachea* (`tlg4031.tlg002`) p. 38 `1096a5`, p. 296 `1139b33`, p. 516 `1170a25`.
  Recorded in each file's `revisionDesc`.
- Not changed: references that are misprinted in the CAG volumes themselves are kept as printed
  (e.g. Ps.-Alexander, *In Sophisticos elenchos* p. 141 "p. 117a20" for 177a20).

## 1.0.1 (2026-11-17)

- Michael of Ephesus, *In libros de animalium motione commentarium* (CAG XXII.2, `tlg4034.tlg004`): the last page,
  p. 131, was missing from the transcription. Its five lines (131.1–5) and two apparatus entries are restored from the
  page image and collated with the First1KGreek text; the two disagreements were decided on the image. Recorded in the
  file's `revisionDesc`.
- `metadata/works.tsv` and the counts in the README follow (lines 474,843; apparatus entries 217,043).

## 1.0.0 (2026-11-17)

First public release: 59 TEI files (CAG I–XXIII), `metadata/works.tsv`, `docs/encoding.md`.
All files validate against TEI `tei_all` (P5 version 4.12.0).
