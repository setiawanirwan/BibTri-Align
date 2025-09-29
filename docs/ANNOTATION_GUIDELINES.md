Annotation Guidelines for Alignment Confidence Flags

This document explains the alignment confidence scheme used in BibTri-Align v2, a trilingual Sundanese–Indonesian–English corpus. Each aligned unit (verse or sentence) is assigned one of three flags: High (✓), Medium (~), Low (✗). The flags are designed to give researchers practical indicators of alignment reliability.

The scheme combines automatic heuristics with manual checks on a subset of cases.

1. High (✓) — Reliable Alignment

Alignments judged to be accurate, with consistent structure and meaning across the three languages.

Indicators:

Verse numbering matches across all three versions.

Token length ratios fall within expected ranges.

Proper nouns and named entities appear consistently.

Semantic equivalence preserved.

Example:

Sundanese	Indonesian	English	Flag
"Gusti teh pangpangna asih jeung asihna langgeng."	"Tuhan itu penuh kasih setia, kasih-Nya kekal."	"The Lord is merciful, and His love endures forever."	✓
2. Medium (~) — Generally Correct, Minor Issues

Alignments that are mostly correct but include small mismatches or formatting differences.

Indicators:

Minor punctuation inconsistencies.

Slight differences in token length ratios.

Synonymous but not exact lexical choices.

Verse split differently across translations.

Example:

Sundanese	Indonesian	English	Flag
"Yesus ngadadarkeun pasemon ka maranehna."	"Yesus berbicara kepada mereka dengan perumpamaan."	"Jesus told them a parable."	~

(Indonesian has a fuller phrase; English is shorter but still semantically aligned.)

3. Low (✗) — Problematic Alignment

Alignments with more serious issues, such as omissions, partial translations, or semantic divergence.

Indicators:

Missing or truncated text in one language.

Verse numbering mismatch without clear correspondence.

Named entities missing or replaced incorrectly.

Semantic content diverges significantly.

Example:

Sundanese	Indonesian	English	Flag
"(1:5)"	"Pada waktu itu Yohanes membaptis di padang gurun."	"At that time John was baptizing in the wilderness."	✗

(The Sundanese version only contains a placeholder, not the actual verse content.)

4. Practical Use

Researchers may use these flags to:

Filter: Train only on High alignments.

Weight: Assign more weight to High, less to Medium, exclude Low.

Analyze: Study the distribution of noise and its effect on MT.

This scheme does not eliminate all uncertainty. Instead, it provides transparent metadata to help users make informed decisions when working with the corpus.
