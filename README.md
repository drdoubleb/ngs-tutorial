# Base by Base — an interactive NGS tutorial

A hands-on, drag-and-drop walkthrough of an Illumina next-generation sequencing
workflow in two modules: the wet lab (from a living cell to demultiplexed FASTQ
reads) and the bioinformatics (from FASTQ to an annotated variant). Built as a
single self-contained HTML file — no build step, no dependencies, no server
required.

## Run it

Open `index.html` in any modern browser. That's it.

To host it publicly, enable **GitHub Pages** for this repo (Settings → Pages →
deploy from the main branch, root folder) and it will be served at
`https://<user>.github.io/ngs-tutorial/`.

## What you do in it

Every step is interactive — you drag reagents onto the bench (or click a
reagent, then click its destination), and wrong moves get an explanation of
*why* they don't work:

| # | Step | Interaction |
|---|------|-------------|
| 1 | Cell lysis | Drag lysis buffer (not PBS, not ethanol) onto the sample |
| 2 | DNA cleanup | SPRI beads → magnet → ethanol wash → elution, in order |
| 3 | Fragmentation | Load the sonicator, pulse into the 300–500 bp window — over-shear and you start over |
| 4 | End repair & A-tailing | Enzymes in the right order; ligase is rejected as "too early" |
| 5 | Adapter ligation | Give two patients *different* index barcodes, ligate, pool |
| 6 | Hybrid capture | Match biotinylated probes to their target genes, then beads → magnet → wash |
| 7 | Flow cell | Denature with NaOH, seed the lawn, run bridge-amplification cycles |
| 8 | Sequencing by synthesis | You are the polymerase: drag the complementary fluorescent nucleotide each cycle |
| 9 | Basecalling & demux | Call bases from the camera strip, then sort pooled reads back to their patients |

**Module 2 — Bioinformatics** (rendered as dark "terminal" screens):

| # | Step | Interaction |
|---|------|-------------|
| B1 | Read QC & trimming | Cut the low-quality tail where Phred drops below Q20; scan for and clip adapter read-through |
| B2 | Alignment | Slide the read you sequenced along the reference, watch the ±1 score, beat the decoy near-match |
| B3 | Indels & CIGAR | Drag a 2-base gap into the right junction; watch the CIGAR go 8M → 4M2D4M |
| B4 | Sort & dedup | `samtools sort` the pile, then flag the PCR duplicates (keeping the best-quality copy) |
| B5 | Variant calling | Flag the true heterozygous SNV column, reject the low-quality error column, call the genotype |
| B6 | Annotation | Apply the alt allele to a BRCA1 codon, derive Arg→His, classify it as missense |

State (which barcode each patient got, the read you sequenced) carries through
the scenes and across the modules, so the run tells one continuous story — the
read you build in sequencing-by-synthesis is the read you later align. Progress
is saved in `localStorage`. Genomic coordinates in module 2 are illustrative,
not clinical assertions.

## Tech notes

- Vanilla HTML/CSS/JS in one file (`index.html`), ~1,700 lines.
- Custom pointer-event drag engine with a click-to-pick fallback (works on
  touch screens and with keyboards; chips and drop zones are focusable).
- Respects `prefers-reduced-motion`.
- Fonts from Google Fonts (Bricolage Grotesque / IBM Plex), with system
  fallbacks if offline.

## Ideas for later

Paired-end reads, patterned flow cells and index hopping, UMIs, a quiz mode,
per-step "deeper dive" panels, long-read (ONT/PacBio) comparison track.
