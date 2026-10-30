# Splits, Tabs and Windows

Outcome: you know the shape of
Ghostty's window organisation and the
default keys that drive it — learned,
this once, from the keybind list
rather than from a window. The label,
again: **documented-only.** The lab
opened no windows; every key named
below was verified to exist as a
default bind in transcript
`t05-keybinds-and-actions.txt`, and
every action in transcript
`t03-config.txt`'s effective
configuration. The experience of using
them is the documentation's account,
not the lab's.

## The three levels

- A **window** is one operating-system
  window. `new_window` (Ctrl+Shift+N
  by default) makes another.
- A **tab** is a full-window terminal
  inside a window, one of several you
  switch between. `new_tab`
  (Ctrl+Shift+T), `next_tab` and
  `previous_tab` (Ctrl+Tab,
  Ctrl+Shift+Tab), `goto_tab` on
  Alt+1 through Alt+8, `last_tab` on
  Alt+9, `close_tab` (Ctrl+Shift+W).
- A **split** divides one tab's space
  into two terminals side by side or
  stacked — each a full shell, each
  independently usable. Splits are
  Ghostty's answer to the tiled layout
  a multiplexer would give you, inside
  the window.

## The split keys, from the list

```text
keybind = ctrl+shift+o=new_split:right
keybind = ctrl+shift+e=new_split:down
keybind = ctrl+alt+arrow_left=goto_split:left
keybind = ctrl+alt+arrow_right=goto_split:right
keybind = ctrl+alt+arrow_up=goto_split:up
keybind = ctrl+alt+arrow_down=goto_split:down
keybind = ctrl+shift+enter=toggle_split_zoom
```

`new_split` takes a direction;
`goto_split` moves focus by direction
(or to `previous` / `next`);
`resize_split` — on Ctrl+Super+Shift+
arrows by default — grows and shrinks
by ten cells; `equalize_splits` evens
them out; `toggle_split_zoom` blows
one split up to fill the tab and back.
Actions end with `:arguments` — you
met the pattern in chapter 8 — and the
full default set is in the transcripts
if you want the complete map before
you ever touch it.

## What splits are not

A split is a view, not a session. All
of a window's tabs and splits live and
die with the window: close it, log
out, or let the machine sleep hard
enough, and every shell in it ends.
Ghostty keeps no server process
holding your work the way tmux does.
This single fact organises most real
setups:

- **Ghostty alone** when your work is
  one machine, one sitting, and tiles
  on screen are what you want.
- **Ghostty plus tmux or Zellij**
  (both in this series) when the work
  must survive disconnects — the
  multiplexer owns persistence, the
  terminal owns speed and looks, and
  the split keys above retire in
  favour of the multiplexer's own.

There is one more window trick, the
**quick terminal**: a terminal bound
to a `global:` keybind (chapter 8)
that slides in over whatever you are
doing and away again — the natural
home of `toggle_quick_terminal`. It is
the closest Ghostty comes to being
everywhere at once, and like
everything else in this chapter, it
begins at a keybind you can list
before you can press it.
