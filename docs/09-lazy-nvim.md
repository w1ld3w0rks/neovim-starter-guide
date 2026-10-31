# Lazy.nvim

[Lazy.nvim](https://github.com/folke/lazy.nvim) bootstraps from `lua/josean/lazy.lua` and installs to `~/.local/share/nvim/lazy/lazy.nvim`. Plugin declarations live in `lua/josean/plugins/` and its LSP subdirectory.

Useful commands:

```text
:Lazy
:Lazy sync
:Lazy update
:Lazy clean
:Lazy check
```

Add a plugin by creating a Lua file that returns a spec, restart Neovim, and run `:Lazy sync`. Keep `lazy-lock.json` committed so installations remain reproducible.
