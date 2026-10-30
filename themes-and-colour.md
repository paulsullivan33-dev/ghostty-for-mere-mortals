# Themes and Colour

Outcome: you can pick a theme from the
463 Ghostty ships with, apply it, and
prove from the command line which
colours you actually got. The check:

```bash
ghostty +list-themes | wc -l
```

```text
463
```

(transcript `t02-themes-and-colors.txt`.)

## Choosing from the shelf

`ghostty +list-themes` prints every
available theme, each tagged
`(resources)` when it ships with
Ghostty. The shelf is deep — the
Catppuccin family alone on the lab's
build:

```text
Catppuccin Frappe (resources)
Catppuccin Latte (resources)
Catppuccin Macchiato (resources)
Catppuccin Mocha (resources)
```

Most famous editor colour schemes of
the last twenty years are here, along
with hundreds of community ones.
Names are matched **exactly**,
including case on case-sensitive
filesystems — `Catppuccin Mocha`
works, a near-miss does not, and
chapter 14 covers the silence that
follows a wrong name.

Applying one is a single config line:

```text
theme = "Catppuccin Mocha"
```

Values with spaces take quotes. That
is the whole procedure — the interest
is in what the line *does*.

## A theme is a config file

Look at the theme itself — themes live
in the resources folder as plain
files, and the head of Catppuccin
Mocha is nothing but palette lines:

```text
palette = 0=#45475a
palette = 1=#f38ba8
palette = 2=#a6e3a1
…
palette = 15=#bac2de
```

A theme is a Ghostty config file that
sets colours — background, foreground,
cursor, selection, and the 256-entry
**palette** your programs draw with.
That is why `+show-config` in chapter 5
exploded after one theme line: the
effective configuration honestly
reports all 256 changed entries, plus
results like:

```text
background = #1e1e2e
foreground = #cdd6f4
```

Two consequences follow, one useful
and one a warning:

- **Useful:** anything a theme sets,
  you can override after it. Your own
  `background = …` line, later in the
  loading order, wins over the theme's
  — themes are a starting point, not a
  cage.
- **Warning:** a theme can set *any*
  configuration option, not just
  colours. The built-in themes are
  audited to stay safe, but a theme
  file downloaded from a forum is a
  config file from a stranger. Read it
  before you use it; it is short, and
  it is plain text. That is the ethics
  rule of this guide, stated where it
  belongs: **do not run configuration
  you have not read.**

## Your own themes

A name that is not found in the
resources is looked up in a `themes`
folder inside your config directory
(`~/.config/ghostty/themes`) — drop a
file there and its filename becomes a
theme name you can select, or point
`theme` at an absolute path to a theme
file anywhere. A custom theme is the
same format as the lab's excerpt
above: mostly `palette = N=#rrggbb`
lines, plus whichever of background,
foreground, cursor-color and
selection colours you care to set.

When you need a colour's hex value,
Ghostty knows 617 named colours:

```bash
ghostty +list-colors | head -5
```

```text
alice blue = #f0f8ff
AliceBlue = #f0f8ff
antique white = #faebd7
```

## Light and dark

One line can carry both of your
system's moods. The theme option's own
documentation (transcript
`t08-documented-defaults.txt`) gives
the syntax:

```text
theme = "light:Rose Pine Dawn,dark:Rose Pine"
```

Ghostty then follows the desktop's
light/dark preference, switching the
pair as your system switches. The
order of the two halves does not
matter; whitespace is trimmed. If you
only ever use one mode, the single
name from the start of this chapter is
all you need — and now you know
precisely what it changed, and how to
prove it.
