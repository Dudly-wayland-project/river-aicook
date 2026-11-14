<!--
SPDX-FileCopyrightText: © 2020 The River Developers
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# river (personal fork)

This is a **personal fork** of [river](https://codeberg.org/river/river), the
non-monolithic Wayland compositor, maintained for my own daily use.

It is an experimental tree: patches land here to be tried out, not to be sent
upstream. There is no support, no stability promise, and no release schedule.
You can use this as long as you can accept AI generation.

Upstream is maintained by Isaac Freund and the river contributors.

## Fork status

- Base: upstream commit `85b0088` — "LayerSurface: configure until unmap, not
  only on initial commit" (2026-10-18), version `0.6.0-dev`
- Purpose: personal experimentation, not upstream submission

## Changes in this fork

Nothing diverges from the base commit yet. Record changes here as they land:

- _(none)_

Keeping upstream as a separate remote makes rebasing easy:

```
git remote add upstream https://codeberg.org/river/river.git
git fetch upstream
git rebase upstream/main
```

## Overview

River is a non-monolithic Wayland compositor. Unlike other Wayland compositors,
river does not combine the compositor and window manager into one program.
Instead, users can choose any window manager implementing the
[river-window-management-v1] protocol.

## Features

River defers all window management policy to a separate window manager
implementing the [river-window-management-v1] protocol. This includes window
position/size, pointer/keyboard bindings, focus management, window decorations,
desktop shell graphics, and more.

River itself provides frame perfect rendering, good performance, support for
many Wayland protocol extensions, robust Xwayland support, the ability to
hot-swap window managers, and more.

The [river-window-management-v1] protocol and other river protocol extensions
are stable.

## Building

Ensure that you have the following dependencies installed. The "development"
versions are required if applicable to your distribution.

- [zig](https://ziglang.org/download/) 0.17.1
- wayland
- wayland-protocols
- [wlroots](https://gitlab.freedesktop.org/wlroots/wlroots) 0.20
- xkbcommon 1.12 or newer
- libevdev
- pixman
- pkg-config
- scdoc (optional, but required for man page generation)

Then run, for example:
```
zig build -Doptimize=ReleaseSafe --prefix ~/.local install
```
To enable Xwayland support pass the `-Dxwayland` option as well.
Run `zig build -h` to see a list of all options.

## Usage

River can either be run nested in an X11/Wayland session or directly
from a tty using KMS/DRM. Simply run the `river` command.

On startup river will run an executable file at `$XDG_CONFIG_HOME/river/init`
if such an executable exists. If `$XDG_CONFIG_HOME` is not set,
`~/.config/river/init` will be used instead.

Usually this executable is a shell script which starts the user's window manager
and any other long-running programs.

See also the `river(1)` man page.

## Hacking

See [ARCHITECTURE.md](ARCHITECTURE.md) for an overview of the code base, and
[doc/internal](doc/internal) for in-depth notes on complex corners of it.

## Licensing

This project follows the [REUSE Specification](https://reuse.software/spec-3.3/),
all files have SPDX copyright and license information.

In overview:

- River's source code is released under the GPL-3.0-only license.
- River's Wayland protocols are released under the MIT license.
- River's logo and documentation are released under the CC-BY-SA-4.0 license.

[river-window-management-v1]: https://isaacfreund.com/docs/wayland/river-window-management-v1
