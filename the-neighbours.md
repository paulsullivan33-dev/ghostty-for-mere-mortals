# The Neighbours

What the other terminals do — and what
Ghostty does that they don't. Nothing
here was run or benchmarked for this
guide; these are characterisations
from each project's own documentation,
to help you place Ghostty rather than
to crown it.

## WezTerm — the programmable one

WezTerm (this series has a full guide)
is Ghostty's closest rival in spirit:
GPU-accelerated, cross-platform, with
tabs, splits, and a built-in
multiplexer that can even keep
sessions on a remote machine. Its
defining difference is configuration:
a **Lua program**, not a data file —
it can compute, branch, and react.
That buys power Ghostty deliberately
declines, and costs the simplicity
Ghostty deliberately keeps. WezTerm
also runs on **Windows**, where
Ghostty does not run at all. If your
life spans all three platforms or your
config needs logic, WezTerm is the
neighbour to visit first.

## Alacritty — the minimalist

Alacritty staked out GPU-accelerated
minimalism years before Ghostty: very
fast, very plain, configured in a
TOML file, with **no tabs and no
splits at all** — its position is that
windows are the window manager's job
and persistence is tmux's. If
Ghostty's surface area feels large,
Alacritty is the same philosophy with
the dial turned further. If you would
miss the tabs, it is a step too far.

## kitty — the maximalist

kitty goes the other way: GPU drawing
plus an empire of features — its own
graphics protocol for images in the
terminal, remote control of windows
from scripts, extensions ("kittens")
written in Python, layouts, and
sessions. Where Ghostty's self-
inspection stops at listing and
validating, kitty aims to be
scriptable end to end. The price is a
program with strong opinions and a
configuration to match.

## The ones that came with your system

GNOME Terminal and KDE's Konsole on
Linux, Terminal.app and iTerm2 on
macOS: the defaults are not bad
terminals. They are integrated,
maintained, and already installed.
iTerm2 in particular is a deep,
mature Mac application. Ghostty's
case against them is not contempt —
it is chapter 1's pair of claims: the
GPU rendering keeps up when they
choke on a firehose of output, and
the config file is one text document
instead of a settings maze. If
neither claim bites on your workload,
the default you already have is a
legitimate answer.

## The multiplexers are not neighbours — they are housemates

tmux and Zellij do a different job —
sessions that survive — and chapter 9
explained the division of labour.
They appear in this chapter only to
say: "Ghostty or tmux?" is the wrong
question, asked often. The right one
is what each layer is for in *your*
setup. The series' guides to both
multiplexers work through it from
their side.
