# What Ghostty Is

You type into a window and read what
comes back. The program in that window —
the thing that draws the letters, keeps
the scrollback, resizes when you drag a
corner — is a **terminal emulator**. It
pretends to be a piece of 1970s hardware
(a glass terminal) well enough that
your shell, your editor, and forty years
of command-line tools all believe it.

**Ghostty is a terminal emulator built
to be fast and to belong.** Fast, in a
specific way: it hands the drawing to
your **GPU** — the graphics processor
that spends most of its life waiting
for games — so redrawing a screenful of
text costs the main processor almost
nothing, and scrolling through ten
thousand lines stays smooth. Belonging,
in this way: on macOS it is a native
Mac app built with Apple's own tools,
and on Linux it is a native GTK app.
It does not look like the same program
pasted onto both systems. It looks like
it grew there.

It is free and open source under the
MIT licence, and it is written in **Zig**
by Mitchell Hashimoto — a name you may
know from HashiCorp, the company behind
Vagrant and Terraform, whose guides sit
elsewhere in this series. The first
stable release, 1.0, arrived in
December 2024 after several years of
development in the open. The lab
verified the current stable line:
**Ghostty 1.3.1**.

## A first taste

Ghostty's unusual feature — the one
this guide leans on from here to the
glossary — is that the program will
answer questions about itself from the
command line, without opening a window.
These helper commands are called
**actions**, and each starts with a
`+`:

```bash
ghostty +version
```

```text
Ghostty 1.3.1

Version
  - version: 1.3.1
  - channel: stable
Build Config
  - Zig version   : 0.15.2
  - build mode    : .ReleaseFast
  - app runtime   : .gtk
  - font engine   : .fontconfig_freetype
  - renderer      : renderer.generic.Renderer(renderer.OpenGL)
```

That is the real output, from
transcript `t01-version.txt`. It already
tells you the shape of the program: the
runtime here is GTK (this is Linux), the
font engine is fontconfig with FreeType,
and the renderer is OpenGL. Chapter 2
takes those lines apart one by one.

There are fifteen actions in 1.3.1 —
listing fonts, keybinds, themes,
colours and actions themselves;
showing and validating configuration;
asking which font face draws a given
character. A terminal that can be
interrogated like this can be
configured with confidence: you do not
guess what your settings did, you ask.
Chapters 5 to 8 are built on that.

## What it is not

Ghostty is not a **shell**. It does not
interpret your commands; bash, zsh or
fish does that, running *inside*
Ghostty the way a play runs inside a
theatre.

It is not a **multiplexer**. It has
tabs and splits — chapter 9 — but it
does not keep your programs alive when
the window closes, the way tmux and
Zellij do. Those are neighbours and
partners, not rivals: many people run
tmux inside Ghostty and get both
strengths. The series has guides to
each, and chapter 12 compares them.

It is not configured by **scripting**.
Some terminals are programmed in a real
language (WezTerm uses Lua). Ghostty's
config file is deliberately just data —
`key = value`, one setting per line —
which makes it easy to read, easy to
diff, and impossible to loop. Chapter
13 counts that as both a feature and a
limit.

And it is not on **Windows**. macOS and
Linux are the supported platforms;
chapter 13 states the Windows position
plainly.

## Who it is for

The person who lives in a terminal and
feels every millisecond of lag. The Mac
user who wants a terminal that behaves
like a Mac app — real tabs, real
settings sync with the system theme —
without giving up speed. The Linux user
who wants the same, in GTK. And the
person who has been burned by a
graphical settings maze and would
rather keep their terminal's whole
personality in one text file they can
back up, version, and carry to the next
machine. That file is chapter 5.
