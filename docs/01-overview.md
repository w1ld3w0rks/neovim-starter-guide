# System overview

This project is a personal macOS terminal and Neovim build. It combines Zsh, Oh My Zsh, Powerlevel10k, Homebrew CLI tools, tmux, TPM, Neovim, Lua, Lazy.nvim, Mason, LSP, and Treesitter.

```text
macOS -> Zsh -> tmux -> Neovim
              -> Homebrew tools
Neovim -> Lua -> Lazy.nvim -> plugins
                    -> Mason/LSP
                    -> Treesitter parsers
```

Zsh launches programs, tmux manages terminal panes, Neovim edits files, Lua configures Neovim, Lazy.nvim manages plugins, Mason manages external developer tools, and Treesitter parses source code.

The foundation is [Josean Martinez's dev-environment-files](https://github.com/josean-dev/dev-environment-files). This repository is an independent adaptation for my workflow.
