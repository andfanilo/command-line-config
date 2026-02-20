Here is the complete **"Ghostty-on-Windows" Setup Guide**. You can copy this entire block directly into a GitHub Gist or a README.md file.

---

# 👻 Ghostty-Style Terminal Setup for Windows

**WezTerm + Git Bash + Starship**

This setup provides a GPU-accelerated, minimalist, Unix-like environment on Windows with a modern Lua-based configuration.

## 📦 Phase 1: Binaries & Assets

1. **WezTerm**: Download the `wezterm-gui-*.zip` (Portable), unzip to `C:/executables`.
2. **Starship**: Download `starship-x86_64-pc-windows-msvc.zip`, move `starship.exe` to `C:/executables`.
3. **Git for Windows**: Install to default directory (`C:/Program Files/Git`).
4. **Font**: Install [Cascadia Code NF](https://github.com/microsoft/cascadia-code/releases) or [JetBrains Mono Nerd Font](https://www.nerdfonts.com/font-downloads). *(Critical for icons).*

---

## ⚙️ Phase 2: WezTerm Configuration

Create/Edit: `C:/Users/<User>/.wezterm.lua`

```lua
local wezterm = require 'wezterm'
local config = wezterm.config_builder()

-- Default Workspace
config.default_cwd = "C:/workspace"

-- Shell: Git Bash
config.default_prog = { 'C:\\Program Files\\Git\\bin\\bash.exe', '--login', '-i' }

-- Visuals (Ghostty Aesthetic)
config.color_scheme = 'Tokyo Night'
config.font = wezterm.font('Cascadia Code NF') -- Change to your preferred Nerd Font
config.font_size = 11.0
config.line_height = 1.1

-- Window Polish
config.window_background_opacity = 0.90
config.win32_system_backdrop = 'Acrylic'
config.window_decorations = "RESIZE"
config.window_padding = { left = 15, right = 15, top = 15, bottom = 15 }

-- Behavior
config.adjust_window_size_when_changing_font_size = false

-- Mouse Bindings (Scroll Zoom)
config.mouse_bindings = {
  {
    event = { Down = { streak = 1, button = { WheelUp = 1 } } },
    mods = 'CTRL',
    action = wezterm.action.IncreaseFontSize,
  },
  {
    event = { Down = { streak = 1, button = { WheelDown = 1 } } },
    mods = 'CTRL',
    action = wezterm.action.DecreaseFontSize,
  },
}

-- Keys
config.keys = {
  { key = '0', mods = 'CTRL', action = wezterm.action.ResetFontSize },
}

return config

```

---

## 🐚 Phase 3: Shell Configuration (Bash)

Create/Edit: `C:/Users/<User>/.bashrc`

```bash
# Add custom executables to PATH
export PATH="$PATH:/c/executables"

# Initialize Starship Prompt
eval "$(starship init bash)"

```

Create/Edit: `C:/Users/<User>/.bash_profile`
*(Ensures .bashrc loads in login shells)*

```bash
[[ -f ~/.bashrc ]] && . ~/.bashrc

```

---

## 🚀 Phase 4: Starship Customization

Create/Edit: `C:/Users/<User>/.config/starship.toml`

```toml
add_newline = false

[character]
success_symbol = "[❯](bold magenta)"
error_symbol = "[❯](bold red)"

[directory]
style = "bold cyan"
truncation_length = 3
truncation_symbol = "…/"

[git_branch]
symbol = " "
style = "bold purple"

[package]
disabled = true

```

---

## 📌 Phase 5: Taskbar Integration

1. Go to `C:/executables`.
2. Right-click `wezterm-gui.exe` > **Create Shortcut**.
3. Right-click **Shortcut** > **Properties**.
4. Set **Start in:** to `C:\workspace`.
5. Click **Change Icon** if you wish to use a custom Ghostty `.ico`.
6. Right-click Shortcut > **Pin to Taskbar**.

---

**Is there anything else you'd like to tweak in this protocol before you save it?**
