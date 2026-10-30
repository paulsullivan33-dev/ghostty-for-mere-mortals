# Writing criteria for this guide

Every "for Mere Mortals" guide is written to the same nine-point
standard, so a reader who trusts one can trust the rest. Here it
is, with the verification notes for this particular guide below.

1. **Fix it first.** Reader outcomes lead, not action items: each
   chapter opens by naming the outcome it delivers, shows a check
   the reader can run to confirm they got it, and a reasonable
   reader finishes able to state what was done, what it means,
   and what to try next.
2. **Plain language.** Short sentences, everyday vocabulary,
   technical terms defined on first use. No slang, and no
   idioms that only make sense in one country — the reader may
   be translating as they go.
3. **No dead ends.** A guide never tells the reader to do
   something it cannot show them how to verify. Every claim a
   reader relies on — an install, a command, an output — is
   something this guide demonstrates or clearly labels
   documented-only below.
4. **Live-verified where it matters.** Procedures are run for
   real in the guide's lab wherever the build machine allows it,
   and the transcripts kept in the repository are the evidence.
   What could not be run is listed honestly below, never
   presented as if it had been.
5. **General audiences.** Nothing in this guide — examples,
   fixtures, names, addresses — is modelled on any particular
   reader or author's real life, network, or organisations.
   The lab's config is a generic starter and its theme and
   fonts are famous public ones.
6. **Standalone.** A reader needs this guide, its lab, and
   nothing else. Where another guide would genuinely help, it
   is pointed to once, by name, and the chapter still completes
   without it.
7. **Honest about limits.** Chapter 13 names what the tool
   cannot do: no session persistence, no Windows version, a
   Linux feature ceiling set by the system's GTK, a config
   file that is data rather than a language, and inspection
   tools that cannot drive a running window.
8. **The ethics rule is in the text, early.** Ghostty raises no
   interception question, but it has a trust surface of its
   own: a theme file is a config file and can set almost any
   option. Chapter 6 states the rule where a reader will meet
   it — do not use a theme or config you have not read.
9. **Builds clean.** The site builds with MkDocs in strict mode
   with no warnings, and a fresh reader following the chapters
   in order reaches the stated outcome of each.

## Verification notes for this guide

The build machine is a small shared Ubuntu 24.04.5 (x86_64)
sandbox with **no display** — no `DISPLAY`, no Wayland — and
that single fact divides this guide's evidence in two. Ghostty
is a GUI program; its window never opened here, and chapters
4 and 9 say so in their first paragraphs. Everything the
program can do *without* a window — its whole `+` action
surface — was run for real, and that turned out to be most of
the configuration story.

Ghostty **1.3.1** was obtained as the community package
`ghostty_1.3.1-0.ppa2_amd64_24.04.deb` from the ghostty-ubuntu
project (the packager the official install page points to),
SHA-256 verified against the digest published with the
release: `478d4401…b8cd47`, matching. The lab unpacked the
package instead of installing it system-wide and supplied
three missing libraries the same unpacked way — GTK 4.14.5
and libadwaita 1.5.0 from Ubuntu 24.04's own packages (with
their small dependencies libappstream5, libstemmer0d,
libxmlb2), and libgtk4-layer-shell0 1.0.4 from Debian, which
Ubuntu 24.04 does not package. Version 1.3.1 is the newest
Ghostty an Ubuntu 24.04 system can run: 1.4 requires GTK
4.18 / libadwaita 1.7. The binary ran unmodified throughout;
a thin wrapper only set the library path, the resources path,
and an isolated config home. All transcripts live in
`ghostty-lab/transcripts/`; the lab's starter config is
`ghostty-lab/config.example` and its deliberately broken one
is `ghostty-lab/config.broken.example`.

Run for real, with transcripts as evidence:

- `+version` in full — version, channel, Zig 0.15.2 build,
  GTK runtime, GTK build and runtime 4.14.5, libadwaita
  1.5.0 — and the `+help` action list, all fifteen actions
  (t01).
- The install itself: package identity, checksum match,
  declared dependencies, the three libraries missing from
  the bare system, and zero missing once supplied (t00).
- `+list-themes` counted at **463** with the Catppuccin
  family shown; a theme file read directly (its head is
  palette lines, proving a theme is a config file);
  `+list-colors` counted at **617**; the shell-integration
  folder listed — bash, elvish, fish, nushell, zsh (t02).
- A nine-line config written, `+validate-config` exiting 0,
  and `+show-config` read back: the font fan-out to bold /
  italic / bold-italic, the theme's 256 palette entries,
  and the guide's key lines extracted by grep (t03).
- The same file broken four ways — bad value, negative
  size, unknown action, unknown key — with
  `+validate-config` printing all four errors verbatim as
  `file:line:key: message` and exiting 1; the good file
  restored and re-validated at exit 0 (t04).
- `+list-actions` counted at **85** and printed in full;
  `+list-keybinds` at **72** with no config and **73** with
  the lab's (one replacement, one addition); the lab's own
  two keybinds found in the effective configuration (t05).
- `+list-fonts` counted at 2,573 lines on this machine;
  `+show-face` for a letter and an arrow (both DejaVu Sans
  Mono under the lab config), for an emoji with emoji
  presentation (Noto Color Emoji — fallback, proven), and
  for a mixed string; plus the genuine failure of the
  space form of `--string` — `config error: cli:2:string:
  value required` — against the working `--string=value`
  form (t06).
- Startup without a display: the log through config load
  (default shell and working directory taken from the
  account entry) to `Gtk: Failed to open display`, exit 1;
  and, with an empty `config.ghostty` placed beside
  `config`, the verbatim warnings that both files exist
  and both are loaded, in that order (t07).
- `+show-config --default --docs` measured at 4,070 lines
  and `--default` at 613; the font-size documentation and
  the light/dark theme syntax extracted from that dump
  (t08). The keybind documentation in the same dump grounds
  chapter 8's sequences, prefixes, `catch_all`, and key
  tables; the theme documentation grounds chapter 6's
  custom-theme lookup and override rules; the
  shell-integration documentation grounds chapter 10's
  feature list.
- The theme-audition recipe (chapter 11, recipe 2) run
  against a scratch config home: `theme = "Gruvbox Dark"`
  yielding background `#282828` and foreground `#ebdbb2`
  in `+show-config`.

Documented only — described from the project's documentation,
not run, and the text does not claim otherwise:

- Opening a window and everything in it: the first-run
  experience, splits, tabs, the quick terminal, the command
  palette, GPU rendering in action, reload-by-keybind.
  Chapters 4 and 9 carry the label in their opening lines;
  their keys and actions are transcript-verified, their
  experience is not.
- The macOS side throughout: the official download, the
  AppKit app, Core Text fonts, the macOS config path.
- Building from source, the Flatpak route, and any release
  newer than 1.3.1 — including everything past the GTK
  version gate.
- Defining and living in key tables (chapter 8): the
  actions and the mechanism are verified from the binary's
  lists and documentation; no table was exercised.
- The neighbour tools of chapter 12 — characterised, not
  run or benchmarked.
- Shell integration's in-window effects (chapter 10): the
  scripts' presence and the documented feature list are
  verified; prompt jumping itself needs a window.

Fixtures are this guide's own and deliberately generic: a
nine-line starter config, a four-mistake broken config, and
public themes and fonts (Catppuccin Mocha, Gruvbox Dark,
DejaVu Sans Mono, Noto Color Emoji). No real person's
machine, accounts, or files appear anywhere.
