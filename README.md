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
│   └── structures/         ← the logos of the departments, schools and poles
│                             (<code>-<it|en>-<white|blue>.pdf, from the brand kit)
└── figures/                ← sample assets (wallpaper, QR code, profile pic)
```
To have Manrope, download https://github.com/davelab6/manrope/tree/master/ttf%20format%20(legacy) and copy it inside the fonts/ directory.

## Theme options

| Option       | Default | What it does                                |
| ------------ | ------- | ------------------------------------------- |
| `lang=it/en` | `en`    | Language for TOC title and closing-slide text (and the language of a structure's logo) |
| `showlogo`   | `true`  | Logo in the header bar and on dark slides   |
| `structure=` | `ateneo` | The Politecnico style of a department, school or pole (below) |

### Department, school and pole styles (`structure=`)

The brand kit of the Politecnico gives every structure its own variant of the identity: a colour (Brand guidelines 5.0,
pp. 53-55, and the official 2024 PowerPoint templates of the kit) and a logo (the flag + the name of the structure).
`\usetheme[structure=deib]{polimi}` (or `\usepackage[structure=deib]{beamerthemepolimi}`) follows those templates:

| Kind | Codes | What changes |
| ---- | ----- | ------------ |
| Ateneo (default) | `ateneo` | nothing: the navy pages and the white flag |
| Department | `dabc` `daer` `dastu` `dcmc` `ddes` `deib` `deng` `dfis` `dica` `dig` `dmat` `dmec` | title, section and closing pages and the contact strip in the department's colour, navy text, the department's blue logo; subsection and appendix pages in a light tint of the colour |
| School | `auic` `design` `ingcat` `ingindinf` | navy title and section pages with the circles and the dome in the school's colour (Matte Red, Acid Green, Alpha Blue, Beta Blue); subsection and appendix pages in that colour; the school's white logo |
| Territorial pole | `cremona` `lecco` `mantova` `piacenza` | the Ateneo's colours with the campus logo |

| Department | Code | Colour |
| ---------- | ---- | ------ |
| Architecture, Built Environment and Construction Engineering | `dabc` | Metropolitan Purple `909FDE` |
| Aerospace Science and Technology | `daer` | Space Blue `6698FF` |
| Architecture and Urban Studies | `dastu` | Urban Lavender `96AEEF` |
| Chemistry, Materials and Chemical Engineering "Giulio Natta" | `dcmc` | Reactive Lilac `A8BEF2` |
| Design | `ddes` | Smart Mint `7BAEBC` |
| Electronics, Information and Bioengineering | `deib` | Silicon Green `8DB9CD` |
| Energy | `deng` | Sustainable Sage `67B2C6` |
| Physics | `dfis` | Photonic Azure `73A1F7` |
| Civil and Environmental Engineering | `dica` | Subsoil Amethyst `8292CB` |
| Management, Economics and Industrial Engineering | `dig` | Management Teal `6C98BE` |
| Mathematics | `dmat` | Binary Cyan `73A2D1` |
| Mechanical Engineering | `dmec` | Steel Indigo `5C9BE0` |

The logo follows `lang` (`lang=it`: the Italian logo); the Design, Energy and Physics departments and the School of
Design have an Italian logo only. With a structure the default header text is the structure's name
(`\polimistructurename`, in the deck's language), and the colours `polimiAccent` (the structure's colour),
`polimiAccentDark`, `polimiCover` and `polimiOnCover` (the ground of the title / section / closing pages and the text on
it) are there for your own slides. An unknown code gives a warning and the Ateneo style.

## Preamble commands

| Command                       | Effect                                             |
| ----------------------------- | -------------------------------------------------- |
| `\polimisubtitle{...}`        | Optional subtitle on the title page                |
| `\polimiheadertext{...}`      | Centre text in the header bar (pass `{}` for none) |
| `\polimititlelogo[height]{what}` | The logo of the **title page** and of the strip of `\contactslide`: `default`, `none` or the path of a picture |
| `\polimibarlogo[height]{what}`   | The same for the **upper-left corner**: the logotype of the header bar and the flag of the bibliography slides |
| `\poliminologo`               | No logo anywhere (the same as `showlogo=false`)    |
| `\renewcommand{\polimilogowhite}{path}` | The default logo on dark grounds (white flag; a structure's white logo) |
| `\renewcommand{\polimilogodark}{path}`  | The default logo on light grounds (blue flag: bibliography slides, a department's title page) |
| `\renewcommand{\polimilogotipo}{path}`  | The logotype of the header bar                     |
| `\polimimathmanrope`          | Maths letters in Manrope (needs `mathastext`)      |

The logo commands go in the preamble, after `\usetheme`; the last one wins, and with `showlogo=false` (or
`\poliminologo`) nothing brings a logo back. *height* is that of the logo the picture replaces unless given: title
1.5 cm (0.9 cm for a structure's logo), header bar 0.3 cm, bibliography 1.5 / 0.9 cm; a height given to
`\polimibarlogo` is used on both of its pages. `default` with a height scales the theme's own logo
(`\polimititlelogo[1.2cm]{default}`). Example: the lab's logo on the title page, nothing in the corner:

```latex
\usetheme[structure=deib, lang=it]{polimi}
\polimititlelogo[1.2cm]{figures/lab-logo.pdf}
\polimibarlogo{none}
```

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
| `polimiPanel`              | `DDE2E8` | Subsection-divider background (a structure's tint with `structure=`) |
| `polimiAccent`             | `102C53` | The structure's colour (navy for the Ateneo and the poles) |
| `polimiCover`, `polimiOnCover` | `102C53`, `FFFFFF` | Ground of the title / section / closing pages and the text on it |

All colours are registered with `xcolor`, so you can use them freely in
`\textcolor`, `\fcolorbox`, TikZ paths, pgfplots, etc.

## Notes / caveats

- **Italics**: Manrope has no true italic variant. The theme aliases italic to
  regular to prevent font-family fallbacks in footer text. If you need genuine
  italics, substitute a companion font with `\setsansfontfamily`.
- **Aspect ratio**: Every coordinate is calibrated for 16:9 (`aspectratio=169`,
  16 × 9 cm Beamer paper). Other ratios require adjusting the TikZ `x`/`y`
  values inside `beamerthemepolimi.sty`.
- **Logo licence**: The PDF logos were extracted from the official Brand Identity Kit (the logos of the
  structures: the kit's horizontal logos, cropped to their drawing; the boxed DFIS / DENG / DIG / DMEC files
  redrawn without the box).
  Internal academic use is fine; for external publication verify Politecnico di
  Milano's brand-asset terms.
- **Unofficial**: This is an unofficial reproduction. It is not endorsed by
  Politecnico di Milano.
