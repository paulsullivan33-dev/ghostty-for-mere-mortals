# Keybinds and Actions

Outcome: you can read any keybind line
and say what it does, write your own,
and enumerate everything Ghostty can
be told to do. The check:

```bash
ghostty +list-actions | wc -l
```

```text
85
```

(transcript `t05-keybinds-and-actions.txt`.)

## Actions: the verbs

An **action** is a named thing Ghostty
can do: `new_window`, `new_tab`,
`new_split`, `copy_to_clipboard`,
`toggle_fullscreen`, `reload_config`,
85 of them in 1.3.1, and `+list-actions`
prints the whole vocabulary — worth
reading end to end once, because it is
the honest table of contents of
Ghostty's abilities. If a capability
is not in that list, no keybind will
conjure it. The list includes the
quietly powerful ones: `write_screen_file`
(save the screen's text to a file),
`jump_to_prompt` (leap between shell
prompts — chapter 10 explains what
makes it possible), `toggle_quick_terminal`,
`toggle_command_palette`, and the key
table actions of the last section of
this chapter.

## Keybinds: the triggers

A **keybind** ties a **trigger** — a
key, with modifiers — to an action:

```text
keybind = ctrl+shift+n=new_window
keybind = f11=toggle_fullscreen
```

`+list-keybinds` prints the effective
set. On a machine with no config it
prints **72** defaults; the lab's
config — nine lines, two of them
keybinds — brought it to **73**: the
`ctrl+shift+n` line replaced a default
of the same trigger, and `f11` was
new. Setting a trigger that already
exists replaces it; that is the whole
rule, and `+show-config` shows the
survivors, so a bind that seems to be
ignored is a bind that lost to a later
line (chapter 14).

Modifiers are `shift`, `ctrl`, `alt`,
`super` (aliases include `control`,
`opt`, `cmd`). A trigger can also name
a physical key by its W3C code —
`KeyA` matches the key in the A
position whatever your layout prints
on it — while a plain letter matches
by the character it produces, which
keeps bindings honest across layouts
in the other direction. The option's
own documentation covers the corner
cases; `catch_all` exists for binding
whatever is left over.

## Sequences and prefixes

A trigger can be a **sequence**: keys
pressed in turn, joined with `>`:

```text
keybind = ctrl+a>n=new_window
```

Press Ctrl+A, release, press N. (In
other tools this is a leader key or a
chord.) Sequences wait indefinitely
for their next key — there is no
timeout to configure — and chapter 14
names the confusion that causes when a
sequence's first key is one you also
use alone.

Prefixes refine when a bind applies:

- **`global:`** — the bind works even
  when Ghostty is not the focused app.
  This is how you summon the quick
  terminal from inside another
  program; it is also a power to hand
  out sparingly.
- **`unconsumed:`** — the keypress is
  also passed on to the program
  running in the terminal, instead of
  being swallowed by the action.
- **`performable:`** — the bind fires
  only if the action can actually be
  performed right now; otherwise the
  key falls through as if unbound.

## Key tables

New in 1.3.0, and present in the lab's
1.3.1 action list (`activate_key_table`,
`deactivate_key_table`, and kin): a
**key table** is a named set of
keybinds you switch on and off as a
group — a mode, in editor language.
One table for window management, say,
entered with a sequence and left with
Escape, keeps the everyday trigger
space uncluttered. The tables
themselves are defined in the config
with the same `keybind` machinery
scoped by table name; the option
documentation in chapter 5's dump is
the reference. The lab verified the
actions exist and the defaults load;
building a table you live in is
documented-only here, and honestly a
second-month topic — the defaults,
plus two binds of your own, are a
first month well spent.

To remove binds: `keybind = clear`
clears everything set so far in the
file (the documentation's own warning
is blunt about its reach), and the
`unbind` action releases a single
trigger. Start from the defaults,
change little, and let
`+list-keybinds` tell you the truth
about what you have.
