# Troubleshooting

Work from the cheap end: Ghostty can
inspect itself, so most faults are
named before they are hunted. Each
entry here was either reproduced in
the lab or follows directly from a
transcript that was.

## The config errors, one by one

The lab's deliberately broken file
(transcript `t04-broken-config.txt`,
kept as `ghostty-lab/config.broken.example`)
produced four errors — the four ways
a config line can be wrong:

```text
…/ghostty/config:2:font-size: invalid value "banana"
…/ghostty/config:3:window-width: invalid value "-5"
…/ghostty/config:4:keybind: unknown error error.InvalidAction
…/ghostty/config:5:this-key-does-not-exist: unknown field
```

- **`invalid value`** — the key is
  real, the value is not: a word where
  a number belongs, a negative window
  size. The fix is in the line named.
- **`unknown error error.InvalidAction`**
  — a keybind pointing at an action
  that does not exist. The message is
  the least friendly of the four; the
  remedy is `ghostty +list-actions`,
  the 85 real verbs, spelled exactly.
- **`unknown field`** — the key itself
  is not a Ghostty option (a typo, or
  an option from a newer release than
  yours — chapter 3's gate again).
  `+show-config --default` lists your
  version's real keys.

Run `ghostty +validate-config` after
every edit and all four stay
hypothetical. Exit 0 and silence mean
the file is sound; the errors print
to stderr and the exit code is 1.

## Both config files exist

Startup warns:

```text
warning(config): both config files `…/config` and `…/config.ghostty` exist.
warning(config): loading them both in that order
```

(transcript `t07-no-display.txt`.) A
setting you changed "has no effect"
when the *other* file sets it later.
Keep one file. An untouched, empty
`config.ghostty` also draws an
`error.FileIsEmpty` warning in the
same log — harmless, and a sign the
file can simply be deleted.

## The theme name that does not match

A `theme` value is matched exactly,
case-sensitively on Linux: a name
that is almost right applies nothing.
Compare yours against
`ghostty +list-themes` character for
character, quotes included for names
with spaces — then confirm the
result with recipe 2's audition
command, which shows the background
and foreground you actually got.

## The wrong font draws a character

Not a rendering bug, usually: a
**fallback** (chapter 7). Ask
`ghostty +show-face --cp=…` or
`--string=…` which face will be used.
Remember the equals form — the space
form of `--string` fails with `config
error: cli:2:string: value required`,
an error about the *command line*, not
your config. If a whole family is
missing from `+list-fonts`, the font
is not installed where fontconfig
looks; fix the installation, then
restart Ghostty.

## A keybind does nothing

In order: `ghostty +show-config |
grep keybind` — is your line in the
*effective* set, or did a later line
take the same trigger? Then the
sequence trap: if the trigger begins
a `>` sequence, Ghostty is still
waiting for the rest of it, forever,
by design. Then the focus trap: a
plain bind does nothing in another
app's window — that is what the
`global:` prefix is for (chapter 8).
Then the desktop trap: your window
manager may consume the combination
before any application sees it; try
the same action on a different
trigger to find out.

## Prompt jumping does nothing

`jump_to_prompt` needs marks to jump
between, and marks come from **shell
integration** (chapter 10). If the
binds are right but the leaps are
not, check the integration is active
for the shell you are actually
running — `detect` can miss shells
reached through `sudo` or other
indirections, and forcing the shell's
name in the `shell-integration`
option is the fix.

## It will not start, or starts old

No display at all ends startup with
`Gtk: Failed to open display` and
exit 1 (`t07`) — on a desktop that
message means a broken graphics
session, not a broken Ghostty. And if
`+version` reports an older release
than you installed, read its GTK
lines: a build held back by the
version gate (chapter 3) is a system
fact, and no reinstall of Ghostty
will move it.
