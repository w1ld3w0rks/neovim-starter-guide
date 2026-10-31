# Neovim folder structure

```text
~/.config/nvim/
├── init.lua
├── lazy-lock.json
├── .stylua.toml
├── after/lsp/
├── after/queries/ecma/
└── lua/josean/
    ├── core/{init,keymaps,options}.lua
    ├── lazy.lua
    ├── lsp.lua
    └── plugins/
```

`init.lua` is the entrypoint. `core/` holds global options and keymaps. `lazy.lua` bootstraps Lazy.nvim. `plugins/` contains feature-specific plugin specs. `after/lsp/` contains server overrides. `after/queries/` contains custom Treesitter queries. `lazy-lock.json` pins plugin revisions.

See [paths.md](../reference/paths.md) for the complete path reference.
