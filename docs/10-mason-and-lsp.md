# Mason, LSP, formatting, and linting

[Mason.nvim](https://github.com/williamboman/mason.nvim) installs language servers and tools. Open it with `:Mason`.

```text
:MasonInstall lua-language-server
:MasonInstall typescript-language-server
:MasonInstall prettierd
:MasonInstall eslint-lsp
:MasonUpdate
:LspInfo
```

LSP server overrides are in `~/.config/nvim/after/lsp/`. Formatting and linting specs are in `lua/josean/plugins/formatting.lua` and `linting.lua`. Common actions are `gd` for definition, `K` for documentation, and `gr` for references.
