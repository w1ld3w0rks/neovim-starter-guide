# Neovim installation

Install Neovim and Node through Homebrew:

```bash
brew install neovim node
```

Neovim reads `~/.config/nvim/init.lua` at startup. Start it with `nvim`, open a project with `nvim .`, and use `:checkhealth` for diagnostics. The current build uses Lazy.nvim rather than Packer.

The previous setup was preserved at `~/.config/nvim.before-josean.20261031005256`.
