# Fonts

Outcome: you can set a terminal font,
and — the skill this chapter really
teaches — ask Ghostty in advance which
font will draw any character, so a
surprise on screen becomes a fact you
already knew. The check:

```bash
ghostty +show-face --cp=0x2192
```

```text
U+2192 « → » found in face “DejaVu Sans Mono”.
```

(transcript `t06-fonts.txt`.)

## Where fonts come from

Ghostty does not bundle a font. On
Linux, **fontconfig** — the same
discovery system the rest of your
desktop uses — finds the fonts
installed on your machine; on macOS,
Core Text does the equivalent. Ask
what yours offers:

```bash
ghostty +list-fonts | wc -l
```

The lab's machine answered **2,573**
lines — families and their styles.
Your number will differ; the command
is the point. Each family lists its
faces beneath it:

```text
DejaVu Sans Mono
  DejaVu Sans Mono
  DejaVu Sans Mono Bold
  DejaVu Sans Mono Bold Oblique
  DejaVu Sans Mono Oblique
```

If a font you installed does not
appear here, Ghostty cannot use it —
the argument is with fontconfig (a
font in an unwatched folder, a cache
that needs rebuilding), not with the
terminal. `+list-fonts` is how you
know which side of that line you are
on.

## Setting the font

```text
font-family = DejaVu Sans Mono
font-size = 13
```

Chapter 5 showed the fan-out:
`font-family` alone also fills
`font-family-bold`, `-italic`, and
`-bold-italic` with derived faces.
Set those separately only when a
family's real bold or italic lives
under a different name. Font *features*
— ligatures and their kin — are the
`font-feature` option; the binary's
own documentation (chapter 5's dump)
notes that programming ligatures are
typically the `calt` feature, so
`font-feature = -calt` turns them off
for readers who find joined glyphs
harder to read than separate ones.

## Fallback: the chapter's real subject

No monospace font contains every
character. Arrows, box-drawing, braille,
emoji — somewhere past your font's
edge, Ghostty must borrow a glyph from
another font. That borrowing is **font
fallback**, and it is invisible until
a character arrives drawn in a
different weight, style, or width than
its neighbours.

`+show-face` removes the invisibility.
Give it a codepoint — decimal, hex
(`0x…`), octal, or binary — and it
names the face Ghostty will use, under
your current config:

```text
$ ghostty +show-face --cp=0x41
U+41 « A » found in face “DejaVu Sans Mono”.
$ ghostty +show-face --cp=0x1F600 --presentation=emoji
U+1F600 « 😀 » found in face “Noto Color Emoji”.
```

The letter A comes from the lab's
configured family, as expected. The
emoji does not — it falls back to
**Noto Color Emoji**, a different font
entirely, which is exactly what a real
window would do. Whole strings work
too, one face per character:

```bash
ghostty +show-face '--string=a→b'
```

Note the `--string=value` form with
the equals sign — it is not a stylistic
choice. The space form,
`--string 'a→b'`, fails on the lab's
build with a real error worth meeting
here rather than in chapter 14:

```text
config error: cli:2:string: value required
```

The equals form is the reliable one
for action options that take text.
When a symbol in your prompt, your
status line, or your code renders
oddly, this chapter's two commands —
list the fonts, ask for the face —
are the whole investigation.
