# Limits

What Ghostty cannot do, stated
plainly. Most of these the lab met
directly; the rest are the project's
own documented positions.

**No persistence.** Ghostty has no
server, no session store, no
resurrection. Tabs and splits
(chapter 9) are arrangements of one
living window; when it closes, every
shell inside it ends. Survival across
disconnects, reboots, and SSH hops is
a multiplexer's job — tmux or Zellij,
both in this series — and no Ghostty
release changes that, because it is a
design boundary, not a missing
feature.

**No Windows.** Ghostty runs on macOS
and Linux. The project's position, as
of this writing, is that a Windows
GUI is not on its roadmap — the
underlying library is being made
portable for others to build on, but
a Ghostty app for Windows is not
promised. If Windows is one of your
platforms, chapter 12's WezTerm is
the honest recommendation.

**Your GTK is your ceiling.** On
Linux the app is only as new as the
GTK and libadwaita it runs against:
Ghostty 1.4 asks for GTK 4.18 and
libadwaita 1.7, so Ubuntu 24.04 —
GTK 4.14, libadwaita 1.5 — stops at
1.3.1 (chapter 3). Features land on
the far side of that gate on their
own schedule, not yours. The version
report's build-versus-runtime lines
exist to tell you which side you are
on.

**The config file is data, not a
language.** No variables, no
conditionals, no "use this theme on
this machine only" logic inside the
file itself. The workarounds are
honest ones — the `config-file`
include directive (chapter 5), a
dotfiles manager generating the file,
one config per machine — but the file
will never compute. WezTerm's Lua is
the neighbourly opposite, and the
choice between them is a real one,
not a ladder.

**A young project's ground moves.**
Ghostty 1.0 shipped in December 2024.
Options are added, defaults adjusted,
and machinery appears between minor
releases — key tables arrived in
1.3.0 (chapter 8). Pin your reference
to your version (recipe 5) and expect
a guide — including this one — to lag
the newest release somewhere.

**The inspection tools inspect; they
do not drive.** The `+` actions list,
show, and validate. They will not
rearrange a running window, replay a
session, or script the GUI; that kind
of remote control is kitty's territory
(chapter 12), not Ghostty's.

**Nothing here fixes your shell.**
Ghostty draws what programs print. A
slow prompt, a broken completion, a
wrong character from a program whose
locale is unset — these arrive
*through* the terminal, not *from*
it, and chapter 14's first discipline
is telling the two apart.
