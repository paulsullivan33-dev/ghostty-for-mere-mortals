# Installing Ghostty

Outcome: Ghostty installed, and the
version report proving it runs — with
the GTK lines read, because on Linux
they decide which Ghostty you are
allowed to have. The check is one
command:

```bash
ghostty +version
```

## On macOS, the official download

The Ghostty project distributes
prebuilt binaries for **macOS only**:
download the app from ghostty.org (or
install the same build with Homebrew's
cask), drag it to Applications, done.
This is the route the project supports
directly, and it updates itself. The
lab machine is Linux, so this route is
documented here, not run — the version
gate below is a Linux problem.

## On Linux, your distribution first

Linux builds come from distributions
and community packagers, not from the
project. Several distributions carry
Ghostty in their official repositories
— Arch Linux, Debian, NixOS, Gentoo,
openSUSE, and Ubuntu starting with
26.04 among them — and there it is one
ordinary install command (`pacman -S
ghostty`, `apt install ghostty`, and
their kin). Prefer that route when your
distribution offers a current version:
updates arrive with everything else.

## The community package for Ubuntu and Debian

Ubuntu releases before 26.04 have no
official package. For them, the
community project **ghostty-ubuntu** on
GitHub builds a `.deb` of each Ghostty
release for each supported Ubuntu and
Debian version — the same packager
whose install script the project's own
install page points to. This is the
route the lab took, and the transcript
(`t00-install.txt`) is its evidence:

- The file was
  `ghostty_1.3.1-0.ppa2_amd64_24.04.deb`
  — Ghostty **1.3.1**, built for Ubuntu
  24.04, about 18 MB.
- Its SHA-256 checksum was compared
  with the digest published by the
  release API, and **the sums matched**:
  `478d4401…b8cd47`. A community package
  earns trust exactly this way — verify
  the checksum before you install, not
  after.
- The package's declared dependencies
  are ordinary system libraries:
  libgtk-4, libadwaita, fontconfig,
  FreeType, and a handful more.

The lab did not install system-wide; it
unpacked the package into a folder and
ran the binary from there, supplying
the three libraries the bare sandbox
lacked (GTK 4.14.5 and libadwaita 1.5.0
from Ubuntu's own packages, and
gtk4-layer-shell from Debian's) on the
library path. On a real Ubuntu 24.04
desktop those libraries are a normal
`apt` transaction away and the
packager's installer handles them; the
lab's unpacked arrangement is a
sandbox workaround, not advice. What
matters for this guide is that the
binary is the genuine article,
checksum-verified, and every transcript
in `ghostty-lab/` is its real output.

## The version gate

Here is the fact that shapes Linux
installs, stated by the project and
visible in the lab's version report:
Ghostty's Linux app tracks current
**GTK and libadwaita**. Ghostty 1.4
requires GTK 4.18 and libadwaita 1.7.
Ubuntu 24.04 ships GTK 4.14 and
libadwaita 1.5 — so on 24.04, **1.3.1
is the end of the line** until the
system itself moves. The community
package simply has no 1.4 build for
24.04, because there is nothing sound
to build it against.

This is why the version report prints
build *and* runtime versions of GTK
and libadwaita separately: they are
the numbers that decide your ceiling.
When a guide or a forum post describes
a shiny new Ghostty feature, check
your `+version` output before you go
looking for it. (Key tables, chapter 8,
arrived in 1.3.0 — the lab's 1.3.1 has
them. Anything newer is past the
gate.)

## The remaining routes

A community **Flatpak** exists for
systems whose GTK is too old for their
ambitions — it bundles its own runtime
at the price of the usual Flatpak
sandboxing quirks. And Ghostty can be
**built from source** with the Zig
toolchain; the project's build
documentation is the authority there.
It is a heavy build needing current
development libraries, and the lab —
with its shared, modest machine — did
not attempt it. Both routes are
documented-only in this guide.

Whichever route you took, end here:
`ghostty +version` prints a version, a
channel, and runtime versions that
match or exceed the build versions.
The terminal is installed. Opening it
is the next chapter — the one part of
Ghostty this guide could not run.
