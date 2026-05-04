# DZNLinux Zsh

Default Zsh configuration for DZN Linux, deployed to new user home directories via `/etc/skel`. Provides Oh My Zsh integration, syntax highlighting, and a comprehensive set of Arch Linux shell aliases out of the box.

## Features

- Oh My Zsh with randomized theme on each shell start
- `zsh-syntax-highlighting` enabled globally
- `GLOB_DOTS` enabled — dotfiles included in glob patterns by default
- Persistent, de-duplicated command history
- `~/.bin` and `~/.local/bin` added to `PATH` automatically
- Pacman and yay aliases for common package management tasks
- Reflector aliases for fast mirror updates
- yt-dlp aliases for audio and video downloads
- Shell-switch aliases (`tobash`, `tozsh`)
- Archive extractor function `ex()` supporting tar, zip, 7z, rar, and more
- `~/.zshrc-personal` hook — personal aliases loaded automatically without overwriting skel
- Compatible with KDE Plasma 6.6, Hyprland, and any Arch Linux desktop

## Compatibility

- **Desktop Environments**: KDE Plasma 6.6 (primary), Hyprland, Xfce, and others
- **Display Server**: X11 and Wayland
- **Distribution**: Arch Linux and Arch-based distributions
- **Shell**: Zsh

## Installation

### From DZN Linux Repository (Recommended)

First, add the DZN Linux repository to your system:

```bash
# Add the PGP key
sudo pacman-key --recv-key BB31837564255477
sudo pacman-key --lsign-key BB31837564255477
```

Add the following to `/etc/pacman.conf`:

```ini
[dznlinux_repo]
SigLevel = Required DatabaseOptional
Server = https://repo.dozzen.me/archlinux/$repo/$arch

[dznlinux_repo_3party]
SigLevel = Required DatabaseOptional
Server = https://repo.dozzen.me/archlinux/$repo/$arch
```

Then install the package:

```bash
sudo pacman -Sy
sudo pacman -S dznlinux-zsh-git
```

### Manual Installation

```bash
# Clone this repository
git clone https://github.com/DZN-Linux/dznlinux-zsh.git

# Copy configuration to your home directory
cp dznlinux-zsh/etc/skel/.zshrc ~/
```

## Configuration

### Personal Aliases

Add personal aliases and settings to `~/.zshrc-personal`. This file is sourced automatically and will not be overwritten when the package is updated or when using the `skel` alias.

```bash
# Example ~/.zshrc-personal
alias myalias="some command"
export MY_VAR="value"
```

### Oh My Zsh Theme

The default theme is `random`, which picks a different Oh My Zsh theme on each shell start. To pin a specific theme, edit `~/.zshrc`:

```bash
ZSH_THEME="robbyrussell"   # replace with any theme name
```

Browse available themes at [github.com/ohmyzsh/ohmyzsh/wiki/Themes](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes).

### Restoring Defaults

To reset your Zsh config to the package defaults:

```bash
cz   # alias included in .zshrc — copies /etc/skel/.zshrc to ~/
```

Or manually:

```bash
sudo cp /etc/skel/.zshrc ~/.zshrc && source ~/.zshrc
```

## File Structure

```
etc/skel/
└── .zshrc    # Zsh configuration deployed to new user home directories
```

## License

Licensed under the GNU General Public License v3.0 or later (GPL-3.0-or-later).

See [LICENSE](LICENSE) file for details.

## Credits

- Oh My Zsh: Robby Russell and contributors — https://ohmyzsh.org
- DZN Linux adaptation: Seth Dawson

## Links

- GitHub: https://github.com/DZN-Linux/dznlinux-zsh
- DZN Linux: https://github.com/DZN-Linux

## Troubleshooting

### Oh My Zsh not found on shell start

Ensure `oh-my-zsh` is installed. The `.zshrc` sources from `/usr/share/oh-my-zsh/`, which is the path used by the `oh-my-zsh` AUR package:

```bash
yay -S oh-my-zsh-git
```

If you installed Oh My Zsh via the upstream script instead, update the `ZSH` variable in `~/.zshrc`:

```bash
export ZSH="$HOME/.oh-my-zsh"
```

### Syntax highlighting not working

Ensure `zsh-syntax-highlighting` is installed:

```bash
sudo pacman -S zsh-syntax-highlighting
```

### yt-dlp aliases not found

Install `yt-dlp`:

```bash
sudo pacman -S yt-dlp
```

### Switching back to Bash

```bash
tobash   # alias included in .zshrc
```

Then log out and back in for the change to take effect.
