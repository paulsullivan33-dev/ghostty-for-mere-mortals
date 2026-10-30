# Your First Window

Outcome: you know exactly what happens
when Ghostty starts, what the window
gives you in its first minute, and how
to prove the startup half of it from
the command line. One honest label
before anything else: **this chapter is
documented-only.** The lab had no
display, so no window was ever opened
in the making of this guide. What the
lab *could* do is run Ghostty's startup
right up to the edge of the window —
and that transcript is quoted below,
because startup is most of what a
first window is.

## What startup does, in order

Ghostty's startup log, captured in
transcript `t07-no-display.txt`, shows
the sequence plainly:

```text
info: ghostty version=1.3.1
info: runtime=.gtk
info: renderer=renderer.generic.Renderer(renderer.OpenGL)
info: reading configuration file path=…/ghostty/config
info(config): default shell src=passwd value=/bin/bash
info(config): default working directory src=passwd value=/root
```

In words:

1. **It reads your configuration** —
   the file of chapter 5 — before any
   window exists. A broken config is
   therefore a startup problem, which
   is why chapter 5's validation tools
   matter before you ever see a
   prompt.
2. **It chooses a shell.** With no
   `command` setting, the shell is
   taken from your account's entry in
   the system password file (`src=passwd`
   in the log) — the same login shell
   every other terminal would start —
   in your home directory, likewise
   inherited. Ghostty does not pick a
   shell for you; it respects the one
   your account already declares.
3. **It opens the window** — and here
   the lab's run ends:

```text
warning(glib): WARNING: Gtk: Failed to open display
exit=1
```

No display, no window, exit code 1.
On your machine, with a display, this
is the step where the window appears:
one terminal surface, your shell's
prompt, the theme and font of your
config already applied — because they
were loaded in step 1.

## The first minute in the window

What you can do immediately, per the
documentation and the default keybinds
the lab *could* list (transcript
`t05-keybinds-and-actions.txt`):

- **Type.** It is a terminal; your
  shell is waiting. Nothing about the
  shell itself is different here —
  that is the point of an emulator.
- **Split the window** with
  Ctrl+Shift+O (right) or Ctrl+Shift+E
  (down), and move between splits with
  Ctrl+Alt+arrow keys. Chapter 9.
- **Open a tab** with Ctrl+Shift+T.
- **Open your config** with Ctrl+comma
  — the default bind for the
  `open_config` action — and **reload
  it** after edits with
  Ctrl+Shift+comma. Chapter 5.
- **Summon the quick terminal** — a
  drop-down terminal that slides in
  over your other windows on a global
  keybind you choose. It is unbound by
  default; the `toggle_quick_terminal`
  action in chapter 8's list is what
  you bind it to.

## Checking a first run without a window

Even on a machine with a screen, the
command-line half of a first run is
worth doing, because it separates
"Ghostty works" from "my config
works":

```bash
ghostty +validate-config   # silence and exit 0 mean valid
ghostty +version           # the build you actually got
```

If both are clean and the window still
misbehaves, the fault is in the GUI
layer — your desktop, your graphics
drivers — not in Ghostty's setup.
Chapter 14 works through the failures
in that order.
