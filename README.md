# Neovim Starter Guide

A beginner guide for the Neovim setup installed from [josean-dev/dev-environment-files](https://github.com/josean-dev/dev-environment-files).

## Start Neovim

From your terminal:

```bash
nvim
nvim ~/.zshrc
nvim ~/Projects/my-project/src/index.js
nvim .
```

## Modes and basics

| Mode | Purpose | Enter with |
|---|---|---|
| Normal | Navigate and run commands | `Esc` |
| Insert | Type text | `i` |
| Command | Run commands | `:` |
| Visual | Select text | `v` |

```text
i       Start typing
Esc     Return to normal mode
:w      Save
:q      Quit
:wq     Save and quit
:q!     Quit without saving
u       Undo
Ctrl-r  Redo
```

The leader key is **Space**. `<leader>` means press Space.

## Keybindings

```text
Space + sv    Vertical split
Space + sh    Horizontal split
Space + se    Equalize splits
Space + sx    Close split
Space + to    New tab
Space + tx    Close tab
Space + tn    Next tab
Space + tp    Previous tab
Space + tf    Current file in new tab
Space + nh    Clear search highlighting
Space +       Increment number
Space -       Decrement number
jk            Leave Insert mode
```

Tmux and Neovim pane navigation:

```text
Ctrl-h    Left
Ctrl-j    Down
Ctrl-k    Up
Ctrl-l    Right
```
## File tree and search

Open NvimTree:

```text
:NvimTreeToggle
```

Inside it: `Enter` opens, `a` creates, `d` deletes, `r` renames, `R` refreshes, and `q` closes.

Telescope fuzzy search:

```text
:Telescope find_files
:Telescope live_grep
:Telescope buffers
:Telescope help_tags
```

Use `live_grep` to search text across the current project.

## Lazy.nvim plugins

This setup uses Lazy.nvim:

```text
:Lazy
:Lazy sync       Install and update plugins
:Lazy update     Update plugins
:Lazy clean      Remove unused plugins
:Lazy check      Check for updates
```

Plugin configuration:

```text
~/.config/nvim/lua/josean/plugins/
~/.config/nvim/init.lua
~/.config/nvim/lua/josean/lazy.lua
~/.config/nvim/lua/josean/core/options.lua
~/.config/nvim/lua/josean/core/keymaps.lua
```

## Mason and LSP

Open Mason:

```text
:Mason
```

Install tools:

```text
:MasonInstall lua-language-server
:MasonInstall typescript-language-server
:MasonInstall prettierd
:MasonInstall eslint-lsp
:MasonUpdate
```

Inspect the current language server:

```text
:LspInfo
```

Common LSP actions:

```text
gd    Go to definition
K     Show documentation
gr    Find references
```
## Treesitter and Lua

Treesitter provides parsing, highlighting, folding, and code structure. Useful commands:

```text
:TSInstallInfo
:TSUpdate
:InspectTree
```

Parsers are installed for JavaScript, TypeScript, Lua, Bash, JSON, HTML, CSS, Markdown, YAML, C, and more. Zsh files use the Bash parser automatically.

Lua normally runs automatically through `init.lua`, but you can execute it directly:

```text
:lua print("Hello from Lua")
:lua print(vim.o.number)
:lua vim.opt.number = true
```

Reload the configuration:

```text
:source ~/.config/nvim/init.lua
```

Restarting Neovim is usually safer:

```text
:qa
nvim
```

## Editing configuration

```bash
nvim ~/.config/nvim/init.lua
nvim ~/.config/nvim/lua/josean/core/keymaps.lua
nvim ~/.config/nvim/lua/josean/plugins/
```

After changing plugins: save, restart Neovim, run `:Lazy sync` if needed, and use `:checkhealth` if something fails.

## Daily workflow

```bash
cd ~/Projects/my-project
nvim .
```

Then use `:Telescope find_files`, `i` to edit, `Esc`, `:w` to save, `gd` for definition, `K` for documentation, and `:q` to close.

## Troubleshooting

```text
:messages
:checkhealth
:Lazy
:Mason
:LspInfo
```

## What each part does

- **Zsh** runs terminal commands such as `nvim`, `tmux`, and `git`.
- **Neovim** runs editor commands beginning with `:`.
- **Lua** configures Neovim and its plugins.
- **Lazy.nvim** manages Neovim plugins.
- **Mason** manages language servers, formatters, and linters.
- **Treesitter** provides code parsing and syntax features.
- **tmux** manages terminal panes around Neovim.

## Attribution and project scope

This is my personal Neovim build and starter guide. I built and adapted it for my own workflow, using [Josean Martinez's `dev-environment-files`](https://github.com/josean-dev/dev-environment-files) as the foundation and reference.

The project is an independent build, not an official Josean repository or release. Josean's work is credited here because the setup, ideas, and configuration patterns were the starting point for this version.
