# MusiXTab - A MusiXTeX extension for guitar tablatures

MusiXTab is a small TeX file containing some useful macros for guitar tablature
typesetting. It must be used together with the MusiXTeX core package:

```tex
\input musixtex
\input musixtab
```

MusiXTab offers macros for some common notations in guitar tablatures,
including slides, half and full bends, hammer-on, pull-off and palm mute.
Below, you can find a short introduction to MusiXTab.

It is recommended that you use a 6-line system (assuming a 6-string guitar) and
increase the space between its staves, e.g.:

```tex
\setlines16
\setsize1\largevalue
```

# Table of Contents

* [Manual](#manual)
   * [Fret numbers](#fret-numbers)
   * [Clef symbol](#clef-symbol)
   * [Palm Mute](#palm-mute)
   * [Hammer On, Pull Off, (Artificial) Harmonics](#hammer-on-pull-off-artificial-harmonics)
   * [Bends](#bends)
   * [Slides](#slides)
* [MusiXTeX](#musixtex)
* [License](#license)

# Manual

## Fret numbers

Typesetting fret numbers onto the guitar strings is probably what you will do
the most when writing guitar tablatures. For this, there are two commands
defined: `\str` and `\zstr`. Both print a fret number onto a string, but only
`\str` inserts horizontal space of one `\noteskip` afterwards. `\zstr` on the
other hand typesets a *zero-spacing note*. This is similar to how e.g.
MusixTeX's `\qu` and `\zqu` behave.

Usage:
```tex
\str{<string>}{<number>}
\zstr{<string>}{<number>}
```
where `<string>` is string number between 1 and 6, and `<number>` is any number
(or other text) to put onto the string (usually a fret number between 0 and
24).

## Clef symbol

If you want to display a special **TAB** clef for your tablature staves, use
`\tabclefsymbolsmall`. It displays **TAB** vertically at the beginning of the
instrument (looks best when the overall size is set to `\smallmusicsize`).

Setting this clef for e.g. the first (lowest) instrument looks like this:

```tex
\setclefsymbol1{\tabclefsymbolsmall}
```

## Palm Mute

You can typeset a Palm Mute (P.M.) indicator starting at the current position.
This will insert **P.M.** followed by a dashed line.

Usage:
```tex
\palmmute{<pitch>}{<length>}
```
where `<pitch>` is the vertical level at which the palm mute is placed and
`<length>` is the length of the line in multiples of `\noteskip`.

The result will look similar to this:
```
P.M.-----------|
```
However, if `<length>` is sufficiently small, no line will be inserted, just
```
P.M.
```

## Hammer On, Pull Off, (Artificial) Harmonics

For Hammer On, Pull Off, Natural Harmonics, and Artificial Harmonics,
there are macros which insert the corresponding symbol at the current
position.

Usage:
```tex
\hammeron{<pitch>}{<offset>}
\pulloff{<pitch>}{<offset>}
\harmonics{<pitch>}{<offset>}
\aharmonics{<pitch>}{<offset>}
```
where `<pitch>` is the vertical level at which the symbol is placed and
`<offset>` is the horizontal offset from the current position in note head
widths.

The symbols are: **H** for Hammer On, **P** for Pull Off **Harm.** for Natural
Harmonics, and **A.H.** for Artificial Harmonics (aka. Pinch Harmonics).

## Bends

Bends in MusiXTab are indicated by a curved line going up. Both Half and Full
Bends are supported. The command should be placed right in front of the note
that should be bended.

Usage:
```tex
\bendhalf{<pitch>}{<textpitch>}{<offset>}
\bendfull{<pitch>}{<textpitch>}{<offset>}
```
where `<pitch>` is the vertical level at which the lower end of the bend curve
is placed, `<textpitch>` is the vertical level at which the text is placed and
`<offset>` is the horizontal offset from the current position in note head
widths.

`\bendhalf` uses the text **1/2**, while `\bendfull` uses **Full**.

There are additional commands like `\Bendhalf`, `\Bendfull`, and `\Bend`, which
allow full control over the curve parameters, text etc. However, they should
rarely be necessary.

## Slides

Slides are a bit more complicated than the other macros, even though they just
produce a straight line with some text. The slide macro should be placed right
in front of the note where the slide begins. There are a few variants available
which allow for fine-grained control over placement and optionally typeset the
text ***sl.*** above or below the slide line.

Usage:
```tex
\gslide{<pitch>}{<length>}{<slope>}
\gslidet{<pitch>}{<length>}{<slope>}{<textpitch>}{<textoffset>}
\gSlide{<pitch>}{<voffset>}{<length>}{<slope>}
\gSlidet{<pitch>}{<voffset>}{<length>}{<slope>}{<textpitch>}{<textoffset>}
```
where `<pitch>` is the vertical level at which the beginning of the line is
placed, `<voffset>` is additional vertical offset (for fine-tuning the line
position), `<length>` is the length of the line (values smaller than 2 may
cause weird behavior), `<slope>` is the slope of the line (should be in [-20,20]
range), `<textpitch>` is the vertical level at which the text is placed, and
`<textoffset>` is the horizontal offset of the text from the current position in
note head widths.

As you may have guessed, only the commands ending on **t** produce any text.
The others insert just a line. This allows scenarios where two notes are slided
at the same time, but you only want to insert the ***sl.*** text once.

# MusiXTeX

For more information on MusiXTeX, check out the official documentation
[here](http://icking-music-archive.org/software/musixtex/musixdoc.pdf).

# License

MusiXTab is licensed under the GNU General Public License v3. For more
information, see the [LICENSE.md](LICENSE.md) file.
