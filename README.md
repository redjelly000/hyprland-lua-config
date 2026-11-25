# Hyprland Lua Configuration

A personal Hyprland configuration for a keyboard-driven tiling desktop. It includes workspaces 1–10, a scratchpad, laptop media keys, and three-finger workspace switching. Appearance settings cover gaps, rounded corners, window opacity, blur, and spring animations.

[`hyprland.lua`](hyprland.lua) loads nine modules so you can change your shortcuts, display, or theme independently.

## Requirements

Use a Linux system running Hyprland with Lua configuration support, introduced in Hyprland 0.55. Check your installed version with `hyprctl version`. [Hyprland Lua configuration guide](https://wiki.hypr.land/0.55.0/configuring/start/)

Install the tools for the features you want, or change their commands in [`modules/binds.lua`](modules/binds.lua).

| Feature | Commands or tools |
| --- | --- |
| Terminal | `wezterm` |
| File manager | `kitty -e yazi` |
| App launcher | `rofi -show drun` |
| Browser | `helium-browser` |
| Volume and microphone keys | `wpctl` from WirePlumber |
| Brightness keys | `brightnessctl` |
| Media playback keys | `playerctl` |
| Session exit | `hyprshutdown` if installed, with a Hyprland exit fallback |
| Qt appearance | `qt6ct`, selected in [`modules/env.lua`](modules/env.lua) |

## Setup

1. Clone the repository on the Linux machine running Hyprland.

   ```bash
   git clone https://github.com/senitheknath/hyprland-lua-configuration.git
   cd hyprland-lua-configuration
   ```

2. Check the settings in your local copy before installing.

   - In [`modules/layout.lua`](modules/layout.lua), change `layout = "dwingle"` to `layout = "dwindle"`. [Dwindle layout documentation](https://wiki.hypr.land/configuring/layouts/dwindle-layout/)
   - In [`modules/monitors.lua`](modules/monitors.lua), replace `output = "1920x1200"` with your connector name, such as `eDP-1`. Run `hyprctl monitors all` from an active Hyprland session to find it. For a fallback rule that picks each display’s preferred mode, use `output = ""`, `mode = "preferred"`, `position = "auto"`, and `scale = 1`. [Monitor configuration](https://wiki.hypr.land/configuring/core/monitors/)
   - In [`modules/binds.lua`](modules/binds.lua), set the terminal command to one you have installed so you can open it with `Super + Q`.

3. Back up your existing configuration and copy both the entry point and its modules. Run these commands from the repository root.

   ```bash
   config_dir="${XDG_CONFIG_HOME:-$HOME/.config}/hypr"
   backup_dir="$config_dir.backup-$(date +%Y%m%d-%H%M%S)"

   if [ -d "$config_dir" ]; then
     cp -a -- "$config_dir/" "$backup_dir"
   fi

   mkdir -p -- "$config_dir"
   cp -R -- modules "$config_dir/"
   cp -- hyprland.lua "$config_dir/"
   ```

## Keybindings

`Super` is usually the Windows key.

| Shortcut | Action |
| --- | --- |
| `Super + Q` | Open WezTerm |
| `Super + E` | Open Yazi in Kitty |
| `Super + R` | Open the Rofi launcher |
| `Super + B` | Open Helium Browser |
| `Super + C` | Close the focused window |
| `Super + V` | Toggle floating |
| `Super + P` | Toggle pseudotiling |
| `Super + J` | Toggle the Dwindle split direction |
| `Super + Arrow keys` | Focus a window by direction |
| `Super + 1–0` | Switch to workspaces 1–10 |
| `Super + Shift + 1–0` | Move the focused window to workspaces 1–10 |
| `Super + Scroll` | Cycle through existing workspaces |
| `Super + S` | Toggle the `magic` scratchpad |
| `Super + Shift + S` | Move the focused window to the scratchpad |
| `Super + Left drag` / `Super + Right drag` | Move / resize a window |
| `Super + M` | Exit the Hyprland session |

The touchpad uses natural scrolling and a three-finger horizontal swipe to switch workspaces. Dedicated media keys control volume, microphone mute, backlight brightness, and media playback.

## Configuration files

| File | Settings |
| --- | --- |
| [`modules/monitors.lua`](modules/monitors.lua) | Display output, mode, position, and scaling |
| [`modules/binds.lua`](modules/binds.lua) | Application commands, keyboard and mouse shortcuts, and media keys |
| [`modules/autostart.lua`](modules/autostart.lua) | Session startup hook with commented-out Waybar and `awww-daemon` examples |
| [`modules/env.lua`](modules/env.lua) | Cursor sizes, Wayland toolkit settings, and Qt appearance |
| [`modules/decoration.lua`](modules/decoration.lua) | Gaps, borders, opacity, shadows, blur, and animations |
| [`modules/layout.lua`](modules/layout.lua) | Tiling layout and options for Dwindle, Master, and Scrolling |
| [`modules/misc.lua`](modules/misc.lua) | Built-in wallpaper and Hyprland logo settings |
| [`modules/input.lua`](modules/input.lua) | US keyboard layout, pointer focus, and touchpad behavior |
| [`modules/windowrules.lua`](modules/windowrules.lua) | Maximize request suppression and an XWayland drag workaround |

## License

[MIT](LICENSE) © 2026 Senith Eknath.
