# Ghostty for Mere Mortals

Every program you run in a terminal —
the shell, the editor, the log tail —
is drawn on screen by a **terminal
emulator**: a program whose whole job
is to be the glass the text appears
behind. Most people use whichever one
came with their operating system and
never think about it again. **Ghostty**
is the one people switch to on purpose.
It is a terminal emulator built for
speed — it draws with your computer's
**GPU**, the graphics processor, instead
of leaving the work to the main CPU —
and it aims to feel native on each
platform it runs on: a proper Mac app
on macOS, a proper GTK app on Linux.
It is free, open source (MIT), and
written by Mitchell Hashimoto, the
co-founder of HashiCorp.

Its other defining choice is how you
configure it. There is no settings
window with tabs of checkboxes. There
is a **plain-text config file** — one
`key = value` per line — and a set of
command-line tools that let the
terminal inspect itself: list its 463
built-in themes, print its effective
configuration, validate a config file
and name every error in it, and report
which font will draw a given character.
Those tools are this guide's best
friend, for a reason the next paragraph
explains.

The lab that wrote this guide ran the
real thing — **Ghostty 1.3.1**, the
community package built for Ubuntu
24.04, its checksum verified against
the publisher's — on a machine with
**no display at all**. It could not
open a single window. So every claim
that can be checked without one was
checked for real: the version report,
the theme and colour lists, a config
file written, validated, and read back
as Ghostty itself understood it, a
second config broken in four deliberate
ways to capture the error messages word
for word, the keybind and action
lists, and the font machinery asked
which face draws an arrow and which
draws an emoji. What needs a screen —
the window itself, splits and tabs in
use, GPU rendering in action — is
taught from the documentation and
labelled as such wherever it appears.
`criteria.md` keeps the full ledger of
what was run and what was only read.

## What this guide covers

- [**What Ghostty is**](what-ghostty-is.md) —
  the mental model: a program that draws
  text fast, natively, and answers
  questions about itself from the
  command line
- [**The moving parts**](the-moving-parts.md) —
  the terminal core, the GPU renderer,
  the platform app around it, the font
  engine, and where configuration lives
- [**Installing Ghostty**](installing-ghostty.md) —
  the official Mac download, Linux
  distro packages, the community package
  for Ubuntu and Debian, and the version
  gate that decides which release your
  system can run
- [**Your first window**](your-first-window.md) —
  what happens when Ghostty starts, and
  the one part of this guide the lab
  could only document, not run
- [**The config file**](the-config-file.md) —
  where the file lives, how its lines
  work, and the three commands that
  validate it, print it as understood,
  and dump every option with its
  documentation
- [**Themes and colour**](themes-and-colour.md) —
  463 built-in themes, what a theme
  really is (another config file), and
  light/dark pairs
- [**Fonts**](fonts.md) — how Ghostty
  finds fonts, and how to ask which face
  will draw a character before it
  surprises you on screen
- [**Keybinds and actions**](keybinds-and-actions.md) —
  the 85 things Ghostty can be told to
  do, the triggers that invoke them,
  sequences, and key tables
- [**Splits, tabs and windows**](splits-tabs-and-windows.md) —
  dividing one window into many
  terminals, from the keybind list that
  proves the shape of it
- [**Shell integration**](shell-integration.md) —
  the quiet features — prompt jumping,
  inherited directories, no nagging when
  you close a shell at rest — and how
  the shell learns them
- [**Recipes**](recipes.md) — a starter
  config, auditioning themes without
  touching yours, checking a config in a
  script, and making your own reference
  manual from the binary
- [**The neighbours**](the-neighbours.md) —
  WezTerm, Alacritty, kitty, and the
  terminals your system came with: what
  each does that Ghostty doesn't, and
  vice versa
- [**Limits**](limits.md) — no session
  persistence, no Windows version, a
  config file that is not a programming
  language, and a young project's moving
  ground
- [**Troubleshooting**](troubleshooting.md) —
  the four config errors, the two-config
  warning, the theme name that doesn't
  match, and the font that wasn't used
- [**Glossary**](glossary.md) — the
  terms, collected in one place

## What it doesn't cover

Scripting or embedding: Ghostty's
engine exists as a library
(libghostty), and other programs are
beginning to build on it, but embedding
it is a developer project with its own
documentation, not a user topic.
Building Ghostty from source — a Zig
build needing current GTK libraries —
is described as a route in chapter 3
but was not the lab's route, and its
steps are the project's to maintain.
Windows: there is no Ghostty for
Windows, and chapter 13 says plainly
where that stands.

## How to use this guide

Read chapter 1 for the model and
chapter 2 before installing anything —
knowing which part does what turns
later surprises into named problems.
Chapters 3 and 5 get you an installed
terminal and a config file you have
verified with Ghostty's own tools;
those two chapters are the spine.
Chapters 6 to 10 each take one part of
the config file and go deep. The lab's
transcripts live in
`ghostty-lab/transcripts/`; its starter
config is `ghostty-lab/config.example`
and its deliberately broken one is
`ghostty-lab/config.broken.example`.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [WezTerm for Mere Mortals](https://paulsullivan33-dev.github.io/wezterm-for-mere-mortals/)
- [Zellij for Mere Mortals](https://paulsullivan33-dev.github.io/zellij-for-mere-mortals/)
- [tmux for Mere Mortals](https://paulsullivan33-dev.github.io/tmux-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/ghostty-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/ghostty-for-mere-mortals/blob/main/LICENSE-CODE).
