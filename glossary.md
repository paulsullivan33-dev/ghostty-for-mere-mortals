# Glossary

**Action** — a named thing Ghostty can
do: `new_tab`, `reload_config`,
`toggle_fullscreen`. There are 85 in
1.3.1, listed by `ghostty +list-actions`.
The `+`-prefixed command-line tools —
`+version`, `+show-config` — are also
called actions.

**Config file** — the plain-text file
of `key = value` lines that shapes
Ghostty, at `~/.config/ghostty/config`
on Linux. Its sibling `config.ghostty`,
if present, is loaded after it.

**Effective configuration** — what your
config *means* once defaults, themes,
and includes are applied. Printed by
`ghostty +show-config`.

**Font fallback** — when a character
is missing from your font, another
font supplies its glyph. `+show-face`
names the supplier in advance.

**fontconfig** — the Linux system that
discovers installed fonts and answers
"which font has this?" Ghostty's font
engine on Linux is fontconfig with
FreeType.

**GPU rendering** — drawing the
terminal with the graphics processor
instead of the CPU. Ghostty's renderer
is OpenGL on Linux, Metal on macOS.

**GTK / libadwaita** — the toolkit and
companion library Ghostty's Linux app
is built with (GNOME's stack). Their
versions gate which Ghostty releases
your system can run.

**Key table** — a named, switchable
set of keybinds: a mode. Arrived in
Ghostty 1.3.0.

**Keybind** — a line tying a trigger
to an action: `keybind =
ctrl+shift+n=new_window`.

**Palette** — the numbered table of
colours (0–255) terminal programs draw
with. A theme's main content is a
palette plus background and
foreground.

**Quick terminal** — a drop-down
terminal summoned over other windows
by a global keybind, via the
`toggle_quick_terminal` action.

**Sequence** — a keybind trigger of
several keys pressed in turn, joined
with `>`: `ctrl+a>n`. Also called a
leader key or chord elsewhere.

**Shell integration** — scripts,
shipped with Ghostty and sourced by
your shell, that report prompt
positions, the working directory, and
whether a command is running.

**Split** — a division of a tab into
two terminal surfaces, side by side
or stacked. A view, not a session.

**Surface** — one terminal area: what
a tab or a split displays. Several
actions and messages use the word.

**Theme** — a named config file that
sets colours, selected with the
`theme` option. Ghostty 1.3.1 ships
463.

**Trigger** — the key half of a
keybind: modifiers plus a key, a
physical key code, or a sequence.

**XDG config home** — the directory
under which Linux apps keep settings,
`~/.config` unless `XDG_CONFIG_HOME`
says otherwise. Ghostty's config lives
in its `ghostty` subfolder.
