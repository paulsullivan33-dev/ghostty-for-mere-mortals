# The Config File

Outcome: you have a config file at the
address Ghostty reads, you can prove
Ghostty understood it the way you
meant it, and you can get every
mistake named before it costs you a
startup. The check is:

```bash
ghostty +validate-config
```

Silence, and an exit code of 0, means
valid. Everything in this chapter was
run for real; the transcripts are
`t03-config.txt` and `t04-broken-config.txt`.

## Where it lives

```text
~/.config/ghostty/config
```

More precisely, `$XDG_CONFIG_HOME/ghostty/config`
— the XDG config home is `~/.config`
unless you have moved it. Ghostty
also recognises a sibling named
`config.ghostty` in the same folder.
If **both** exist, both are loaded,
`config` first, and startup logs say
so — the lab captured that warning
verbatim in `t07-no-display.txt`:

```text
warning(config): both config files `…/ghostty/config` and `…/ghostty/config.ghostty` exist.
warning(config): loading them both in that order
```

Two files quietly merging is a fine
feature and a fine way to confuse
yourself; chapter 14 lists it as a
troubleshooting suspect. Pick one —
this guide uses `config` — and keep
everything there. On macOS the same
file lives at
`~/Library/Application Support/com.mitchellh.ghostty/config`.

## How its lines work

One setting per line, `key = value`,
`#` starts a comment:

```text
# A small, ordinary starter config (written for this lab)
theme = "Catppuccin Mocha"
font-family = DejaVu Sans Mono
font-size = 13
window-width = 100
window-height = 32
cursor-style = bar
mouse-hide-while-typing = true
keybind = ctrl+shift+n=new_window
keybind = f11=toggle_fullscreen
```

That is the lab's actual config, kept
in the guide as
`ghostty-lab/config.example`. Three
rules cover most of the format:

- **Some keys repeat.** `keybind` and
  `palette` take one line per entry;
  later lines add to earlier ones
  rather than replacing them. Most
  other keys simply take the last
  value given.
- **Every key is also a command-line
  option** in the same spelling —
  `--font-size=13` — per the `+help`
  text. Useful for trying a value
  once without editing the file.
- **A config can include other files**
  with the `config-file` directive,
  paths relative to the file doing the
  including — how a shared base config
  and a per-machine one combine.

## Proving Ghostty understood it

`+validate-config` checks the file.
`+show-config` answers the deeper
question — not "is it valid?" but
"what did it *mean*?" It prints the
**effective configuration**: everything
that differs from the defaults once
your file, and anything it pulls in,
has been applied. With the lab's
nine-line config, the interesting
lines are:

```text
font-family = DejaVu Sans Mono
font-size = 13
theme = Catppuccin Mocha
background = #1e1e2e
cursor-style = bar
window-height = 32
window-width = 100
```

Two lessons hide in the full output
(transcript `t03-config.txt` runs to
hundreds of lines). First, your font
choice **fans out**: `font-family`
alone sets `font-family-bold`,
`-italic`, and `-bold-italic` to the
same family, because Ghostty derived
them — set them separately only when
a font's bold really lives elsewhere.
Second, a theme **restates the whole
palette**: all 256 palette entries
appear, because applying Catppuccin
Mocha changed every one of them from
the defaults. `+show-config` is not
being verbose; it is showing you that
a theme is a bigger lever than it
looks. Chapter 6 picks it up.

## The built-in manual

There are hundreds of options, and no
guide chapter should pretend to be the
reference for them. Ghostty carries
its own:

```bash
ghostty +show-config --default --docs
```

On the lab's build that is **4,070
lines** — every option at its default,
each preceded by its documentation as
comments (transcript
`t08-documented-defaults.txt`).
`+show-config --default` without
`--docs` prints the 613 lines of bare
defaults. Chapter 11 turns this into
a personal reference file; the
glossary and the option docs together
are how you learn what a setting you
have never heard of does — from the
binary itself, in the version you
actually run.

## Changing it live

Two default keybinds serve the file
itself: **Ctrl+comma** opens it in
your editor (`open_config`), and
**Ctrl+Shift+comma** reloads it
(`reload_config`) — both visible in
transcript `t05-keybinds-and-actions.txt`.
Most settings apply on reload; a few
(the documentation for each option
says) need a restart. And a courtesy
the format earns you: because it is
plain text, the file belongs in your
usual dotfiles backup, diffable and
versioned like any other. The starter
in `config.example` is deliberately
small — nine lines is enough to make
the terminal yours, and every line in
it is one this chapter has verified.
