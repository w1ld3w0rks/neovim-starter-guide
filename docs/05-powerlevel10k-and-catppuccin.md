# Powerlevel10k and Catppuccin

Powerlevel10k reads `~/.p10k.zsh`. Run `p10k configure` to generate a prompt. Install a [Nerd Font](https://www.nerdfonts.com/) and select it in the terminal for icons.

This build uses Catppuccin Mocha-inspired colors across Zsh, tmux, and Neovim. The shell colors are set with `POWERLEVEL9K_*` variables in `~/.zshrc`; tmux uses `@catppuccin_flavor 'mocha'`; Neovim's theme is configured by the colorscheme plugin.

If symbols are broken, select a Nerd Font, restart the terminal, and check true-color support before changing prompt code.
