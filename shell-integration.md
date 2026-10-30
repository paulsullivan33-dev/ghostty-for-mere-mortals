# Shell Integration

Outcome: you understand what your
shell quietly tells Ghostty, what
Ghostty gives back for it, and how to
check the machinery is in place. The
check needs no window:

```bash
ls /usr/share/ghostty/shell-integration/
```

Five shells' worth of integration
scripts ship inside Ghostty's
resources — the lab listed them in
transcript `t02-themes-and-colors.txt`:

```text
bash
elvish
fish
nushell
zsh
```

## What the shell reports

**Shell integration** is a small
script your shell sources at startup
(the **injection** — Ghostty arranges
it automatically for shells it
recognises) that makes the shell
report three things it normally keeps
to itself:

- **Where the prompt is.** Before and
  after each command, the shell marks
  the prompt's start and end in the
  output stream.
- **What the working directory is,**
  whenever it changes.
- **Whether a command is running,**
  or the shell is sitting idle at its
  prompt.

None of this is visible. All of it is
load-bearing.

## What you get back

The `shell-integration` option's own
documentation — read from the lab's
`+show-config --default --docs` dump —
lists the returns plainly:

- **Inherited directories.** A new
  tab, split, or window opens in the
  directory the previous terminal was
  in, because Ghostty was told what it
  was. Without integration, every new
  surface starts at home.
- **Prompt jumping.** The marks make
  `jump_to_prompt` real: Ctrl+Shift+
  Page Up / Page Down (the defaults,
  in transcript `t03-config.txt`) leap
  between the prompts in your
  scrollback — the fastest way to
  re-read the *beginning* of a long
  command's output.
- **No nagging.** Closing a surface
  whose shell sits at its prompt asks
  no confirmation; closing one with a
  command still running does. The
  terminal knows the difference only
  because the shell said so.
- **Cleaner resizes.** A complex
  prompt repaints properly when the
  window changes size, because its
  exact extent is known.

## Controlling it

The option itself:

```text
shell-integration = detect
```

`detect`, the default, identifies the
shell from the command being run and
injects the matching script. Naming a
shell (`bash`, `zsh`, `fish`,
`elvish`, `nushell`) forces that
scheme; `none` turns injection off —
after which you can still source the
script by hand from your shell's own
startup file, pointing at the copy in
the resources folder shown above. The
manual route is the one to know when
`detect` guesses wrong: shells run
under other names, through `sudo`, or
inside environments Ghostty did not
start are where detection thins out,
and chapter 14 treats a missing
prompt-jump as an integration problem
before it treats it as a keybind one.

A boundary worth naming: the
integration tells Ghostty about the
*shell's* state. Run another program
that takes over the screen — an
editor, a pager, tmux — and the marks
pause until you return to the prompt.
Inside tmux the integration story
belongs to tmux; Ghostty's scripts
serve the outermost shell. That is
not a failure of either tool; it is
the seam between them, and now you
know where it is.
