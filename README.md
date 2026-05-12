# Politecnico di Milano — Beamer theme

A LaTeX/Beamer port of the official Politecnico di Milano (Ateneo) 2025
PowerPoint template. Colours, fonts, slide dimensions and the geometry of
every layout are taken directly from the source `.pptx` so the LaTeX slides
match the corporate look without leaving LaTeX.

Remember to install Manrope in the fonts folder (download at https://github.com/davelab6/manrope/tree/master/ttf%20format%20(legacy)) and compile using xelatex (otherwise Manrope is not used).

## Repository layout

```
polimi-latex/
├── beamerthemepolimi.sty   ← the theme
├── example.tex             ← minimal demo deck (13 slides)
├── complete_example.tex    ← full reference — every macro, with usage notes
├── nex_example.tex         ← showcase of the extended/newer slide macros
├── fonts/                  ← Manrope TTFs (add as described in the following the correct files)
├── logos/                  ← PoliMi logo variants (dark, white, logotype)
└── figures/                ← sample assets (wallpaper, QR code, profile pic)
```
To have Manrope, download https://github.com/davelab6/manrope/tree/master/ttf%20format%20(legacy) and copy it inside the fonts/ directory.

## Theme options

| Option       | Default | What it does                                |
| ------------ | ------- | ------------------------------------------- |
| `lang=it/en` | `en`    | Language for TOC title and closing-slide text |
| `showlogo`   | `true`  | Logo in the header bar and on dark slides   |

## Preamble commands

| Command                       | Effect                                             |
| ----------------------------- | -------------------------------------------------- |
| `\polimisubtitle{...}`        | Optional subtitle on the title page                |
| `\polimiheadertext{...}`      | Centre text in the header bar (pass `{}` for none) |
| `\polimilogodark{path}`       | Override the dark-logo path                        |
| `\polimilogowhite{path}`      | Override the white-logo path                       |

## Slide reference

### Structural slides

| Slide                               | How                                                           |
| ----------------------------------- | ------------------------------------------------------------- |
| Title page                          | `\titlepage` inside `\begin{frame}[plain, noframenumbering]`  |
| Table of contents                   | `\tocslide` or `\tocslide[currentsection]`                    |
| Section divider (big number, navy)  | `\frame{\sectionpage}` / `\AtBeginSection[]{\frame{\sectionpage}}` |
| Subsection divider (light grey)     | `\frame{\subsectionpage}` / `\AtBeginSubsection[]{...}`       |
| Closing slide                       | `\closingframe` or `\closingframe[Custom text]`               |
| Dark pull-quote slide               | `\darkframe{Headline text}`                                   |

### Asymmetric layouts

These output a complete `frame`, so call them **outside** any `frame` environment.

```latex
% 23/74 split — narrow white left column, wide grey right column
\asymtextslide{Title}{narrow content}{wide content}

% Title + text on left, image on right
\imagerightslide{Title}{text}{image-path}        % '' → placeholder

% Image on left, title + text on right
\imageleftslide{Title}{text}{image-path}

% Title + text on left, captioned image on right
\imagecaptionslide{Title}{text}{image-path}{Caption}

% Title + text on left, two stacked captioned images on right
\twoimagecaptionslide{Title}{text}{img1}{cap1}{img2}{cap2}
```

Pass an empty string `{}` for any image path to render a dashed placeholder box.

> **Note on macro arguments:** content lives in TikZ nodes. Plain text and
> `itemize`/`enumerate` lists work well. `verbatim` and `listings` content
> must be placed inside a regular `\begin{frame}` with the node body adapted
> by hand.

### Content layouts

```latex
% Three equal columns separated by ruled lines
\threecolslide{Title}{left}{centre}{right}

% Full-bleed image (stretched to 16:9); optional navy title strip at the bottom
\fullbleedslide{image-path}
\fullbleedslide[Title overlay]{image-path}   % '' path → placeholder

% Pull-quote — large centred text on a light background
\quoteslide{Quote text}{Attribution}         % attribution may be empty
\quoteslide[image=fig.png, desaturate=0.4, navyshade=0.2, textcolor=white]
           {Quote text}{Attribution}

% Three statistics callout (large number + caption per column)
\bignumberslide{Title}{num1}{cap1}{num2}{cap2}{num3}{cap3}
```

### Academic / math slides

```latex
% Single theorem/definition block + optional extra content below
\theoremslide{Frame title}{Block type}{Theorem name}{body}{extra}

% Two theorem/definition blocks stacked
\twotheoremslide{Frame title}{Type1}{Name1}{body1}{Type2}{Name2}{body2}

% Explanation + pseudocode (monospace right panel)
\algoslide{Frame title}{explanation}{pseudocode}
```

### Practical / structural slides

```latex
% Horizontal timeline with four labelled milestones
\timelineslide{Title}{label1}{desc1}{label2}{desc2}{label3}{desc3}{label4}{desc4}

% Appendix section divider (light palette; noframenumbering)
\appendixdivider[Appendix label]{subtitle}

% Backup-slides marker (dark navy; noframenumbering)
\backupmarker[Custom label]

% Contact / author info card (name, email, institution, photo, QR)
\contactslide{Name}{email@polimi.it}{Department}{photo-path}{qr-path}
```

### Bibliography slides

```latex
% References on a warm off-white background
\bibslide{title text}{bibliography content}

% References with an image or QR code on the right
\bibslideimg{bibliography content}{image-path}{caption}
```

## Colour palette

| Macro                      | Hex      | Where it appears                    |
| -------------------------- | -------- | ----------------------------------- |
| `polimiNavy`               | `102C53` | Brand primary, title backgrounds    |
| `polimiSlate`              | `596C87` | Mid-tone accents, captions          |
| `polimiSteel`              | `8795A8` | Section-divider dome, circles       |
| `polimiMist`               | `B7BFCA` | Header underline, column dividers   |
| `polimiFog`                | `D0D5DD` | Image placeholder fill              |
| `polimiCloud`              | `F3F3F6` | Light slide background              |
| `polimiPanel`              | `DDE2E8` | Subsection-divider background       |

All colours are registered with `xcolor`, so you can use them freely in
`\textcolor`, `\fcolorbox`, TikZ paths, pgfplots, etc.

## Notes / caveats

- **Italics**: Manrope has no true italic variant. The theme aliases italic to
  regular to prevent font-family fallbacks in footer text. If you need genuine
  italics, substitute a companion font with `\setsansfontfamily`.
- **Aspect ratio**: Every coordinate is calibrated for 16:9 (`aspectratio=169`,
  16 × 9 cm Beamer paper). Other ratios require adjusting the TikZ `x`/`y`
  values inside `beamerthemepolimi.sty`.
- **Logo licence**: The PDF logos were extracted from the official Brand Identity Kit.
  Internal academic use is fine; for external publication verify Politecnico di
  Milano's brand-asset terms.
- **Unofficial**: This is an unofficial reproduction. It is not endorsed by
  Politecnico di Milano.
