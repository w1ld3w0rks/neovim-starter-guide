# Troubleshooting

Start with:

```text
:messages
:checkhealth
:Lazy
:Mason
:LspInfo
:TSInstallInfo
```

Known resolved problems:

- **Unmatched Zsh quote:** the zoxide line must be `eval "$(zoxide init zsh)"`; validate with `zsh -n ~/.zshrc`.
- **Missing lspconfig:** the old Packer declarations did not install all LSP dependencies; the active Lazy setup declares them.
- **Stale Packer runtime:** `packer_compiled.lua` and `:PackerSync` belonged to the old setup; use `:Lazy sync`.
- **Headless TSUpdate error:** an old Packer `run = ":TSUpdate"` hook was incompatible with bootstrap; the current setup uses the modern Treesitter flow.
- **Old Treesitter API:** use `require("nvim-treesitter").setup()` rather than `nvim-treesitter.configs`.
- **Missing compiler:** install both `tree-sitter` and `tree-sitter-cli`.

Shell checks:

```bash
zsh -n ~/.zshrc
tmux -f ~/.tmux.conf -L neovim-guide-test start-server
nvim --headless '+qa'
```
