# Treesitter

The current [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter) main branch uses `require("nvim-treesitter").setup()` and `install()`. The configuration is `lua/josean/plugins/treesitter.lua`.

Parsers include JSON, JavaScript, TypeScript, TSX, YAML, HTML, CSS, Prisma, Markdown, Svelte, GraphQL, Bash, Lua, Vim, Dockerfile, Gitignore, Query, Vimdoc, and C. Zsh files use the Bash parser.

```text
:TSUpdate
:TSInstallInfo
:InspectTree
```

The Homebrew library and CLI are separate packages; install both `tree-sitter` and `tree-sitter-cli`.
