# Recipes

Outcome: a handful of small, finished
jobs — each built only from commands
and files the earlier chapters
verified. Where a recipe depends on a
window, it says so; the rest run
anywhere, including a machine with no
display at all.

## 1. A starter config worth keeping

Copy the lab's config —
`ghostty-lab/config.example` — to
`~/.config/ghostty/config`, edit the
theme and font to taste, and prove it:

```bash
ghostty +validate-config
```

Nine lines: a theme, a font and size,
a window size, a bar cursor, hidden
mouse-while-typing, and two keybinds.
It is small on purpose. Every further
line you add later will be one you
chose, and `+show-config` (chapter 5)
will always be able to tell you what
the whole pile means.

## 2. Audition a theme without touching your config

Themes are easiest to judge by their
key colours, and you can read those
off without disturbing your setup.
Point `XDG_CONFIG_HOME` at a scratch
folder holding a one-line config:

```bash
mkdir -p /tmp/audition/ghostty
printf 'theme = "Gruvbox Dark"\n' \
  > /tmp/audition/ghostty/config
XDG_CONFIG_HOME=/tmp/audition \
  ghostty +show-config \
  | grep -E '^(theme|background|foreground) ='
```

```text
theme = Gruvbox Dark
background = #282828
foreground = #ebdbb2
```

Swap the theme name and rerun to
compare candidates side by side; add
`cursor-color` and `selection-background`
to the grep when the shortlist gets
serious. When one wins, its name goes
into your real config — the only step
of this recipe that changes anything.

## 3. Check a config in a script

`+validate-config` speaks in exit
codes — 0 for valid, 1 with every
error printed as `file:line:key:
message` (chapter 5's broken file,
transcript `t04-broken-config.txt`).
That makes it scriptable anywhere you
keep the file:

```bash
if ghostty +validate-config; then
  echo "config OK"
fi
```

Run it from your dotfiles install
script, or before committing a change,
and a typo'd key stops being a
surprise at the next startup.

## 4. Find which font draws a symbol

A prompt glyph, an icon in a status
line, a box-drawing character that
renders in the wrong weight — chapter
7's question, as a one-liner:

```bash
ghostty +show-face '--string=→'
```

It names the face. If the face is not
your configured family, you have found
a fallback, and you know whether to
fix the font choice or accept the
borrow.

## 5. Make your own reference manual

```bash
ghostty +show-config --default --docs \
  > ~/ghostty-reference.txt
```

Four thousand lines sounds like a lot
until the first time an unfamiliar
option is misbehaving and the answer
is a text search away — in the
documentation for *your* version, not
a website's newer one. Regenerate it
whenever you upgrade Ghostty; chapter
3's version gate means your neighbour's
manual may describe a terminal you
cannot have yet.

## 6. The two binds that pay for the file

In any window (this one needs the
GUI): **Ctrl+comma** opens your config
in your editor; **Ctrl+Shift+comma**
reloads it after you save. Together
they collapse the edit-check loop of
chapters 5 and 6 into seconds, and
they were in the default keybind list
(transcript `t05-keybinds-and-actions.txt`)
before you configured anything. Learn
those two first; the other 70-odd
will arrive as you need them.
