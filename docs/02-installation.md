# Installation

Target: Apple Silicon macOS with Git, internet access, a Nerd Font, and a true-color terminal.

1. Install [Homebrew](https://brew.sh/).
2. Install the packages in [homebrew-tools.md](03-homebrew-tools.md).
3. Install Oh My Zsh, Powerlevel10k, and Zsh plugins using [zsh-and-oh-my-zsh.md](04-zsh-and-oh-my-zsh.md).
4. Install Neovim and copy the configuration into `~/.config/nvim`.
5. Install TPM and copy `~/.tmux.conf`; start tmux and press `Ctrl-a`, then `I`.
6. Start `nvim`, run `:Lazy sync`, `:TSUpdate`, and configure tools in `:Mason`.
7. Run the checks in [troubleshooting.md](18-troubleshooting.md).

Never overwrite an existing configuration without making a timestamped backup first.
