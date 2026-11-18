# CAG-TEI: the *Commentaria in Aristotelem Graeca* in TEI

*Version 1.0.2 (2026-11-18). DOI of the latest version: [10.5281/zenodo.24301130](https://doi.org/10.5281/zenodo.24301130).*

A TEI P5 edition of the 59 commentaries of the *Commentaria in Aristotelem Graeca* (CAG I–XXIII, Berlin: Reimer
1882–1909; 57 Greek, 2 Latin), transcribed from page images and encoded with:

- the text of each printed line, citable by **CAG page and line** (e.g. 105.17);
- the division into **lemmata** with their **Bekker references**, and into chapters and sections, as CTS citation units;
- the **critical apparatus**, each entry attached to the line(s) it cites;
- the references to **older editions** printed in the margin (Aldine and other early editions, Bonitz, Karsten, …),
  each with its edition, unit (page, folio, column, line) and number;
- a link from every page to its **page image** (Internet Archive).

All files validate against the TEI `tei_all` schema (P5 version 4.12.0).

| | |
|---|---|
| Files | 59 (one per commentary) |
| Printed pages | 14,392 |
| Lines | 474,843 (474,786 with the printed line number) |
| Apparatus entries | 217,043 |
| Lemmata with Bekker reference | 12,249 |
| Older-edition references | 71,483 |
| Licence | CC BY 4.0 (transcription and encoding); the printed edition is in the public domain |

## Contents

```
tei/              59 TEI files, <textgroup>/<work>/<urn>.xml (e.g. tei/tlg0732/tlg005/tlg0732.tlg005.humanitext-grc1.xml)
metadata/works.tsv   one row per file: CAG volume, title, editor, year, pages, URN, scans, counts
docs/encoding.md     how the printed page is encoded
CITATION.cff
CHANGELOG.md
```

## How the text was made

OCR of the page images with vision-language models (Gemini): the 15 pilot works line by line with coordinates, the
other 44 as text aligned to the physical lines of the page image; collation with
First1KGreek where a file of the same edition exists (as a collation witness only: no text was copied, every
disagreement was decided on the page image); re-reading of doubtful lines; checks of line numbers, structure,
apparatus and older-edition references on the page images by the editors, student assistants and AI-assisted checking
under the editors' supervision. The `teiHeader` of each file records its procedure (`editorialDecl`) and history
(`revisionDesc`). Accuracy, measured on a stratified sample against the page images, is reported in the accompanying data paper
(Nakayama & Iwata, in preparation).

## Citing

Please cite this dataset by the DOI of its Zenodo record (and the data paper, once published); see `CITATION.cff`.
To cite a passage, use the CAG page and line (e.g. *in APr.* 17.4), which the files resolve through
`refsDecl n="page-line"`, or the CTS URN of the lemma.

## Reporting errors

Errors in the text or the encoding can be reported through the Issues of this repository (work, CAG page and line,
the reading of the file and the reading of the printed page). Corrections are published as new versions; see
`CHANGELOG.md`.

## Related resources

- First1KGreek (Open Greek and Latin, Leipzig) has TEI files for many CAG volumes; this dataset is an independent
  transcription and adds the apparatus, the older-edition references, line-exact page/line citation and page images.
- The scans are those of the Internet Archive (mostly University of Toronto copies); each file names its scan.

## Credits

Naoya Iwata (responsible for the edition); Tomomi Nakayama (structure of the texts and its review). Student assistants
Xiaoyun SHI, Xingyu ZHOU and Itsuki AOU checked the OCR and the line numbers; Xiaoyun SHI and Itsuki AOU also
carried out the accuracy evaluation.

## Licence

The printed edition (1882–1909) is in the public domain. The transcription and encoding in this repository are
licensed under the Creative Commons Attribution 4.0 International licence (CC BY 4.0); see `LICENSE`.

## Funding

This work was supported by JST BOOST (Japan Science and Technology Agency, Next-Generation AI Researcher Development Programme), "Research on AI-Driven Text Analysis and Database Expansion Technologies for Classical Studies" (PI: Naoya Iwata, 2025–2030), Grant Number JPMJBY24B0.
