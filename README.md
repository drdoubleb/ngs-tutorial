# Base by Base — an interactive NGS tutorial

A hands-on, drag-and-drop walkthrough of an Illumina next-generation sequencing
workflow, from a living cell to demultiplexed FASTQ reads. Built as a single
self-contained HTML file — no build step, no dependencies, no server required.

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

State (which barcode each patient got, the read you sequenced) carries through
the scenes, so the run tells one continuous story. Progress is saved in
`localStorage`.

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
