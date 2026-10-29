# Encoding of the CAG TEI files

*DRAFT (2026-10-21). To be finalised with the release; numbers will be recomputed for the released version.*

This document describes how the printed pages of the *Commentaria in Aristotelem Graeca* (CAG, Berlin: Reimer 1882–1909)
are represented in the TEI P5 files of this dataset. Each file's own `teiHeader` (`editorialDecl`, `revisionDesc`)
records the details of its production; what is said here holds for all 59 files.

## 1. One file per work, CTS identifiers

- One TEI file per commentary (59 files: 57 Greek, 2 Latin translations from the Hebrew in CAG V.4–5).
  Works printed in two volumes (Simplicius and Philoponus *in Physica*, CAG IX–X and XVI–XVII) are one file each.
- The edition is `<div type="edition" n="urn:cts:greekLit:tlg0732.tlg005.humanitext-grc1" xml:lang="grc">`.
  Text group and work follow the TLG numbering where it exists (as in First1KGreek); the edition part is
  `humanitext-grc1` (`humanitext-lat1` for the Latin files).
- `metadata/works.tsv` lists every file with its CAG volume, editor, year, page range, scan and counts.

## 2. Pages and lines

```xml
<pb n="17" facs="https://archive.org/download/p1commentariainari02bero/page/n42.jpg"/>
<p>
  <lb n="1" xml:id="p17-0"/>λόγου τὴν οἰκείαν καὶ ἴδιον οὐσίαν …
  <lb n="2" xml:id="p17-1"/>γένει ἔδειξε, διὰ μὲν τοῦ τεθέντων …
```

- `pb/@n` is the CAG page. `pb/@facs` points to the image of that page in the Internet Archive item named in the
  `sourceDesc` (for the few pages supplied from another copy, to that copy).
- One `lb` per printed line. `lb/@n` is the CAG line number of the page (headings included, as the edition counts them),
  checked against the numbers printed every five lines in the left margin. Lines the edition does not count
  (e.g. some titles) have an `lb` without `@n`.
- `lb/@xml:id` = `p{page}-{k}`, where k is the index of the line on the page (0-based). It is an internal anchor for
  the apparatus (§5); use `@n` for citation.
- **Citation by page and line** (the usual way of citing the CAG, e.g. 105.17) is declared in
  `refsDecl n="page-line"`: the `lb` with `@n` = line after the `pb` with `@n` = page.
- Words hyphenated across a line end are joined; the `lb` is placed at the next word boundary, so the second half of the
  word stands on the line where the word began.
- Running heads, page numbers, the printers' signatures at the foot of the page and the CAG's own marginal line numbers
  are not transcribed.

## 3. Structure (CTS citation units)

```xml
<div type="textpart" subtype="chapter" n="1">
  <head>…</head>
  <div type="textpart" subtype="lemma" n="1">
    <milestone unit="bekker" n="24a10"/>
    <quote type="lemma">
      <lb n="3" xml:id="p9-2"/>Πρῶτον εἰπεῖν περὶ τί καὶ τίνος ἐστὶν ἡ σκέψις, ὅτι
    </quote>
    <p> … commentary … </p>
  </div>
```

- Two or three levels: `chapter` (books, major parts, titled sections of the edition) and, inside it, `lemma`
  (a lemma of Aristotle's text and the commentary on it) or `section` (numbered or titled sections, paragraphs of the
  paraphrases); some works have a middle level (`section` between chapter and lemma, e.g. lectures).
  Text before the first lemma of a chapter is a leaf with `n="0"`.
- The CTS citation scheme is declared in `refsDecl n="CTS"` (e.g. `chapter.lemma`).
- `quote type="lemma"`: the lemma as printed (spaced type in the edition). `milestone unit="bekker"`: the Bekker
  reference printed before the lemma (normalised, e.g. `24a10`).
- Headings inside a div (sub-headings, closing formulas, labels of tables) are `ab type="head"`.
- The divisions of 15 works (the "pilot" set) were made by hand; those of the other 44 automatically and reviewed
  (see each header).

## 4. Text

- Transcribed from the page images by OCR (Gemini models, line by line, with coordinates) and corrected: collated with
  First1KGreek where available (used as a collation witness only; no text was copied), re-read, and checked on the
  page images. Spelling, accents, breathings, punctuation and brackets follow the printed page.
- Signs: supplements of the editor `〈 〉`, deletions `[ ]`, cruces `†`, lacunae `* * *` are kept as printed characters.
  Numeral signs are written with ʹ (U+0374, stored in its NFC form U+02B9). Elision is marked with ’ (U+2019).
  Quotation marks: single ‘ ’ (U+2018, U+2019) and double “ ” (U+201C, U+201D), single and double as printed.
  The edition prints opening marks in the reversed form (‛ ‟, resembling a rough breathing); they are encoded with the
  ordinary ‘ “ as a matter of glyph, not of reading.
- Evident misprints of the edition are kept and given with the correct form:
  `<choice><sic>δεικνυμένον</sic><corr>δεικνύμενον</corr></choice>`. Mere variants of spelling or accentuation are left as printed.
- Diagrams and tables are not body text. Each is given once as `figure` after the last body line printed before it:
  labels and trees as `list`, tables as `table`, pure geometry described in `figDesc`.
  Where the edition counts the rows of a diagram as lines, those numbers are not used by any `lb`.
- A scholion printed below the text (Syrianus, *in Metaph.* p. 142) is `note type="scholium"`.

## 5. Critical apparatus

```xml
… συντιθεὶς ταύτας τῷ<note type="apparatus" n="1" target="#p17-0">οὐσίαν post συντιθεὶς …</note>
```

- Each entry of the printed apparatus is a `note type="apparatus"` at the end of the line it cites; `@n` is the line
  reference as printed (`1`, `13-14`, `1 et 5`) and `@target` points to the `lb` of every line cited.
- The attachment is **line-level**: the lemma words of an entry are not linked to words of the text.
- Entries that could not be attached to a line remain at the page end as `note type="footnote"`.

## 6. References to older editions

```xml
… ἢ ἐν τῇ<milestone type="alt-edition" unit="line" ed="Aldina 1520" n="45"/>
… τῶν <milestone type="alt-edition" unit="folio" ed="Aldina 1520" n="7r"/> λαμβανομένων
```

- The CAG prints in the right margin the pages, folios or columns of an older edition (with a vertical bar `|` in the
  text where the new page begins) and its line numbers. These are `milestone type="alt-edition"` with
  `@unit` (`page`, `folio`, `column`, `line`), `@ed` (the edition, identified from the preface of the volume, e.g.
  `Aldina 1520`, `Bonitz 1847`, `Karsten 1865`) and `@n`.
- Page/folio/column milestones stand where the bar is printed; line milestones at the end of the line beside which the
  number is printed.
- The repetition of the current old-edition page or folio beside the first line of each CAG page is not encoded,
  nor is the exact line count sometimes printed beside it.
- Misprinted numbers are given with the corrected value where the sequence determines it.
- A few positions that could not be fixed exactly carry `cert="low"`.

## 7. Header

- `titleStmt/respStmt`: who is responsible for the edition and for the structure; `sourceDesc`: the printed edition
  (volume, editor, year, pages) and the scans; `editorialDecl`: the procedure and conventions of that file;
  `revisionDesc`: the history of the file, with dates.
- Licence: CC BY 4.0 for the transcription and encoding (the printed edition is in the public domain).
