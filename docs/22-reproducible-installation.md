# Reproducible installation

A clean rebuild needs Homebrew, the packages in [homebrew-tools.md](03-homebrew-tools.md), Oh My Zsh and its plugins, TPM, and this Neovim configuration.

```bash
brew install neovim node tmux eza bat ripgrep fd fzf zoxide btop dust git-delta jq tree-sitter tree-sitter-cli
mkdir -p ~/.config
# Copy the desired nvim directory to ~/.config/nvim.
# Install TPM at ~/.tmux/plugins/tpm and copy ~/.tmux.conf.
nvim
```

Then run `:Lazy sync`, `:TSUpdate`, configure tools with `:Mason`, and run `:checkhealth`. Do not copy generated plugin data; let the managers install it.
