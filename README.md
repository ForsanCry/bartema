# bartema

Switch your [Noctalia](https://docs.noctalia.dev) v5 bar between a transparent floating style and the flat default with a single command.

## Requirements

- Noctalia v5 (the native C++ shell started with `noctalia`). It does not apply to the Quickshell-based v4 line.
- bash

## Install

    git clone https://github.com/ForsanCry/bartema.git
    cd bartema
    install -Dm755 bartema ~/.local/bin/bartema

Make sure `~/.local/bin` is in your `PATH`.

## Usage

    bartema transparent      # transparent bar, 4 px gap from the screen edge
    bartema transparent 2    # same, with a 2 px gap
    bartema transparent 0    # transparent, attached to the edge
    bartema flat             # back to your normal bar

## Options

Set these environment variables to change the defaults:

| Variable           | Default   | Meaning                         |
|--------------------|-----------|---------------------------------|
| `BARTEMA_BAR`      | `default` | Name of the bar (`[bar.<name>]`) |
| `BARTEMA_OPACITY`  | `0.3`     | Bar background opacity (0 to 1) |
| `BARTEMA_RADIUS`   | `18`      | Corner radius of all four corners |

Example: `BARTEMA_OPACITY=0.5 bartema transparent 2`

## How it works

Noctalia reads every `*.toml` file in `~/.config/noctalia/` in alphabetical order and merges them. `bartema transparent` writes a small override file, `zz-bartema.toml`, which is read last. `bartema flat` deletes that file. Your own config files are never modified.

After writing the file, the script runs `noctalia config validate`. If the result is invalid, the change is reverted. Noctalia is then restarted, so any open panels will close.

## Notes

- Changes made through Noctalia's Settings are stored in `~/.local/state/noctalia/settings.toml`, which is loaded after your config files and can override the values written by this script.
- If your bar is not called `default`, set `BARTEMA_BAR`.
- Tested only on CachyOS with Hyprland and Noctalia 5.3.0.
