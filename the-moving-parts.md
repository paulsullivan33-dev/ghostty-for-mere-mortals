# The Moving Parts

Outcome: you can name the five parts of
Ghostty and say which one is
responsible when something looks,
feels, or behaves unexpectedly. The
check is the version report — every
part signs its name there.

```bash
ghostty +version
```

The lab's copy is in transcript
`t01-version.txt`. Reading it top to
bottom is a tour of the machine.

## The terminal core

At the centre sits the part that speaks
**terminal**: it reads the stream of
characters and escape codes your
programs print, and maintains the grid
— lines of cells, each holding a
character, a colour, and styles like
bold or underline — plus the scrollback
behind it. This core is platform-blind.
It is also the part being packaged as
**libghostty**, a library other
programs can embed; the guide does not
cover embedding, but it explains why
the core is so carefully separated from
everything around it.

## The renderer

The core decides *what* the screen
says; the **renderer** draws it. The
version report names it:

```text
  - renderer      : renderer.generic.Renderer(renderer.OpenGL)
```

On the lab's Linux build that is
OpenGL; macOS builds use Metal,
Apple's graphics system. Either way the
drawing is done by the GPU, in
per-character glyph textures cached
ahead of time — that is where the
speed in chapter 1 comes from, and why
a fast-scrolling log does not stutter.
The renderer is the one part a headless
lab cannot exercise at all: with no
display there is nothing to draw on.
Transcript `t07-no-display.txt` shows
how far startup gets without one.

## The app runtime

Around core and renderer sits the
**app**: windows, tabs, menus, dialogs,
the clipboard, drag and drop — every-
thing your operating system provides
and your hand touches.

```text
  - app runtime   : .gtk
  - GTK version   :
    build         : 4.14.5
    runtime       : 4.14.5
  - libadwaita    : enabled
```

On Linux the app is **GTK 4** with
**libadwaita**, the library behind
GNOME's look and feel; on macOS it is
Swift and AppKit instead. This split is
Ghostty's defining bet — two native
apps sharing one core — and it has a
practical consequence chapter 3 leans
on: the Linux app can only be as new
as your system's GTK. The version
report prints build *and* runtime GTK
versions precisely because they can
differ, and the difference matters.

## The font engine

```text
  - font engine   : .fontconfig_freetype
```

On Linux, **fontconfig** finds fonts
(the same system the rest of your
desktop uses) and **FreeType** renders
them; macOS uses Core Text. The font
engine owns a question you will ask in
chapter 7: when your chosen font has no
glyph for a character, *which* font
supplies it? That decision — **font
fallback** — is made here, and Ghostty
will show you its answer in advance.

## Configuration and shell integration

The fifth part is not code that runs
the terminal but the material that
shapes it: the **config file**
(chapter 5), the **themes** that are
themselves small config files
(chapter 6), and the **shell
integration** scripts that ship inside
Ghostty's resources folder and teach
your shell to report its prompt and
working directory (chapter 10). The
lab could list those scripts even with
no window to run them in:

```text
$ ls root/usr/share/ghostty/shell-integration/
bash
elvish
fish
nushell
zsh
```

(from transcript `t02-themes-and-colors.txt`;
on an installed system that folder
lives under `/usr/share/ghostty`.)

When something misbehaves, place it
before you fix it. Wrong colours: the
theme, or the core's palette. A key
that does the wrong thing: the app's
keybinds. A character drawn in a
strange font: the font engine's
fallback. A feature your friend's newer
Ghostty has and yours lacks: the
runtime's GTK, holding your build to an
older line. The next chapter is about
exactly that.
