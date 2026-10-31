# Neovim Starter Guide

A complete, personal macOS terminal and Neovim build. This repository documents how I built my setup, what each layer does, where every configuration file lives, which software is installed, and how to reproduce the system.

This is my independent build and documentation. It was adapted from [Josean Martinez's `dev-environment-files`](https://github.com/josean-dev/dev-environment-files), which was the foundation and reference for the Neovim portion. It is not an official Josean repository or release.

## What this build includes

- macOS Zsh with [Oh My Zsh](https://ohmyz.sh/) and [Powerlevel10k](https://github.com/romkatv/powerlevel10k).
- Catppuccin Mocha-inspired colors for the shell, prompt, tmux, and Neovim.
- Zsh autosuggestions, syntax highlighting, web search, fuzzy finding, directory jumping, and modern CLI aliases.
- Homebrew utilities: `eza`, `bat`, `ripgrep`, `fd`, `fzf`, `zoxide`, `btop`, `dust`, `git-delta`, `jq`, `tmux`, `tree-sitter`, and `tree-sitter-cli`.
- tmux with true color, mouse support, Vim-style navigation and copy mode, Ctrl-A prefix, current-directory panes, TPM, Catppuccin, resurrect, continuum, and Neovim pane navigation.
- Neovim 0.12 with a Lazy.nvim-based configuration.
- Completion, snippets, LSP, Mason, formatting, linting, Treesitter, file navigation, Git signs, statusline, tabs, sessions, diagnostics, and editing helpers.
- A dedicated backup of the previous Neovim configuration before the modern setup was installed.

## Architecture: how the pieces fit together

```text
macOS
└── Zsh
    ├── Oh My Zsh
    │   ├── Powerlevel10k prompt
    │   ├── zsh-autosuggestions
    │   ├── zsh-syntax-highlighting
    │   └── web-search
    ├── Homebrew CLI tools
    │   ├── fzf / fd / ripgrep / zoxide
    │   ├── eza / bat / dust / btop
    │   └── git-delta / jq
    ├── tmux
    │   └── TPM-managed tmux plugins
    └── Neovim
        ├── init.lua
        ├── Lua core settings and keymaps
        ├── Lazy.nvim plugin manager
        ├── Mason-managed language tools
        └── Treesitter parsers
```

Zsh launches terminal programs. tmux manages terminal panes. Neovim is the editor. Lua configures Neovim and its plugins. Lazy.nvim installs Neovim plugins. Mason installs language servers and developer tools. Treesitter parses source code for highlighting and structure.

## Prerequisites

This build targets Apple Silicon macOS and assumes:

- macOS with the standard `/bin/zsh` shell.
- Git and a working internet connection.
- A Nerd Font for prompt and icon glyphs. [Nerd Fonts](https://www.nerdfonts.com/) provides installable fonts; MesloLGS NF works well with Powerlevel10k.
- [Homebrew](https://brew.sh/).
- A terminal that supports true color, such as iTerm2 or the macOS Terminal.

Check the important versions on the current system:

```bash
zsh --version
nvim --version | head -1
tmux -V
brew --version
```

## 1. Install Homebrew software

Install Homebrew from [brew.sh](https://brew.sh/) if it is not already installed. Then install the CLI tools used by this build:

```bash
brew install \
  eza \
  bat \
  ripgrep \
  fd \
  fzf \
  zoxide \
  btop \
  dust \
  git-delta \
  jq \
  tmux \
  tree-sitter \
  tree-sitter-cli
```

Install Neovim and Node tooling if they are not already present:

```bash
brew install neovim node
```

`tree-sitter` supplies the parsing library. `tree-sitter-cli` supplies the command-line compiler required by current Treesitter parser installation.

Verify the tools:

```bash
for command in nvim tmux eza bat rg fd fzf zoxide btop dust delta jq tree-sitter; do
  command -v "$command" || echo "missing: $command"
done
```

## 2. Install Oh My Zsh and Powerlevel10k

Install Oh My Zsh using the official instructions at [ohmyz.sh](https://ohmyz.sh/). Install Powerlevel10k using its [official repository](https://github.com/romkatv/powerlevel10k):

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
```

Install the Oh My Zsh plugins used by this build:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions \
  "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-autosuggestions"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting"
```

The `web-search` plugin is included with Oh My Zsh. `zsh-completions` may also be installed for expanded completion:

```bash
git clone https://github.com/zsh-users/zsh-completions \
  "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-completions"
```

Set the theme and plugins in `~/.zshrc`:

```zsh
ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(git zsh-autosuggestions zsh-syntax-highlighting web-search)
```

Powerlevel10k stores its prompt configuration in:

```text
~/.p10k.zsh
```

Run `p10k configure` to generate or redesign the prompt.

## 3. Zsh configuration

The active shell configuration is:

```text
~/.zshrc
```

The custom section in this build adds:

- Catppuccin Mocha-inspired Powerlevel10k colors.
- fzf shell integration.
- zoxide initialization.
- `eza` aliases for `ls`, long listings, and directory trees.
- `bat` as a friendlier `cat`.
- `rg` as the default `grep` alias.
- `dust` as a friendlier `du`.
- `btop` as a friendlier `top`.
- Git shortcuts: `g`, `gs`, and `lg`.
- `reload` to reload `~/.zshrc`.
- `brewup` to update, upgrade, and clean Homebrew.
- `mkcd` to create a directory and enter it.

Important commands:

```bash
source ~/.zshrc
zsh -n ~/.zshrc
```

`zsh -n` checks syntax without executing the configuration. If a startup error appears, inspect the reported line before opening a new terminal.

The setup currently contains duplicate NVM initialization lines inherited from the original shell configuration. They are harmless but can be consolidated later.

## 4. tmux and TPM

The active tmux configuration is:

```text
~/.tmux.conf
```

Install the [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm):

```bash
git clone https://github.com/tmux-plugins/tpm \
  ~/.tmux/plugins/tpm
```

Start tmux and install the plugins from inside tmux:

```bash
tmux
```

Press `Ctrl-a`, then uppercase `I` to install TPM plugins.

The configured plugins are:

- [Catppuccin tmux](https://github.com/catppuccin/tmux) with the `mocha` flavor.
- [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator).
- [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect).
- [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum).

The tmux prefix is `Ctrl-a` instead of the default `Ctrl-b`.

### tmux keybindings

```text
Ctrl-a |       Split vertically
Ctrl-a -       Split horizontally
Ctrl-a c       New window in the current directory
Ctrl-a r       Reload ~/.tmux.conf
Ctrl-a h/j/k/l Move between panes
```

In copy mode, tmux uses Vim keys:

```text
Ctrl-a [       Enter copy mode
v              Begin selection
y              Copy and exit
q              Exit copy mode
```

Mouse support is enabled. New panes and windows open in the current working directory. True-color overrides are enabled for Catppuccin and Neovim themes.

## 5. Neovim installation

Install Neovim with Homebrew:

```bash
brew install neovim
```

The Neovim configuration lives at:

```text
~/.config/nvim
```

The current build uses the `josean` Lua namespace because it was adapted from Josean's configuration. The namespace does not mean the configuration is an official copy; this repository documents my independent build.

The entrypoint is:

```lua
-- ~/.config/nvim/init.lua
require("josean.core")
require("josean.lazy")
require("josean.lsp")
```

Start Neovim with:

```bash
nvim
```

Open a project:

```bash
cd ~/Projects/my-project
nvim .
```

## 6. Exact Neovim folder layout

```text
~/.config/nvim/
├── .stylua.toml
├── init.lua
├── lazy-lock.json
├── after/
│   ├── lsp/
│   │   ├── emmet_ls.lua
│   │   ├── eslint.lua
│   │   ├── graphql.lua
│   │   └── svelte.lua
│   └── queries/
│       └── ecma/
│           └── textobjects.scm
└── lua/
    └── josean/
        ├── core/
        │   ├── init.lua
        │   ├── keymaps.lua
        │   └── options.lua
        ├── lazy.lua
        ├── lsp.lua
        └── plugins/
            ├── ai.lua
            ├── alpha.lua
            ├── auto-session.lua
            ├── autopairs.lua
            ├── bufferline.lua
            ├── colorscheme.lua
            ├── dressing.lua
            ├── flash.lua
            ├── formatting.lua
            ├── gitsigns.lua
            ├── indent-blankline.lua
            ├── init.lua
            ├── lazygit.lua
            ├── linting.lua
            ├── lualine.lua
            ├── nvim-cmp.lua
            ├── nvim-tree.lua
            ├── nvim-treesitter-text-objects.lua
            ├── nvim-ts-autotag.lua
            ├── substitute.lua
            ├── surround.lua
            ├── telescope.lua
            ├── todo-comments.lua
            ├── treesitter.lua
            ├── trouble.lua
            ├── vim-maximizer.lua
            └── which-key.lua
```

### What the important folders do

| Path | Purpose |
|---|---|
| `init.lua` | Entry point loaded when Neovim starts. |
| `lua/josean/core/` | Global options and keymaps. |
| `lua/josean/lazy.lua` | Bootstraps and configures Lazy.nvim. |
| `lua/josean/lsp.lua` | Loads the LSP layer. |
| `lua/josean/plugins/` | One plugin specification per feature. |
| `after/lsp/` | Per-server LSP adjustments loaded after defaults. |
| `after/queries/` | Custom Treesitter queries. |
| `lazy-lock.json` | Pins plugin revisions for repeatable installs. |
| `.stylua.toml` | Lua formatter configuration. |

## 7. Lazy.nvim plugin system

Lazy.nvim is bootstrapped by:

```text
~/.config/nvim/lua/josean/lazy.lua
```

It installs itself to:

```text
~/.local/share/nvim/lazy/lazy.nvim
```

The build imports plugin specifications from:

```text
~/.config/nvim/lua/josean/plugins/
~/.config/nvim/lua/josean/plugins/lsp/
```

The current plugin categories include:

- **Interface:** Alpha, Bufferline, Lualine, Dressing, Which-key, Indent Blankline, Catppuccin/Tokyonight colors.
- **Navigation:** Telescope, Telescope fzf-native, NvimTree, Flash, Trouble, LazyGit.
- **Editing:** nvim-cmp, LuaSnip, nvim-autopairs, nvim-ts-autotag, nvim-surround, substitute.nvim.
- **Code understanding:** nvim-treesitter, Treesitter text objects, LSP, Mason, formatting, linting, todo-comments.
- **Git and workflow:** Gitsigns, vim-tmux-navigator, auto-session, vim-maximizer.
- **Optional productivity/AI:** the AI plugin specification included in `ai.lua`.

Inside Neovim:

```text
:Lazy
:Lazy sync
:Lazy update
:Lazy clean
:Lazy check
```

When adding or removing a plugin, edit or create a file under `lua/josean/plugins/`, restart Neovim, then run `:Lazy sync`.

## 8. Mason, LSP, formatting, and linting

[Mason.nvim](https://github.com/williamboman/mason.nvim) installs external developer tools inside Neovim's data directory. Open it with:

```text
:Mason
```

Useful installs:

```text
:MasonInstall lua-language-server
:MasonInstall typescript-language-server
:MasonInstall prettierd
:MasonInstall eslint-lsp
:MasonUpdate
```

Inspect the current file's language server:

```text
:LspInfo
```

Common LSP actions:

```text
gd    Go to definition
K     Show documentation
gr    Find references
```

LSP server-specific overrides live in:

```text
~/.config/nvim/after/lsp/
```

Formatting and linting specifications live in:

```text
~/.config/nvim/lua/josean/plugins/formatting.lua
~/.config/nvim/lua/josean/plugins/linting.lua
```

## 9. Treesitter

The current configuration uses the main branch of [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter), whose current API is based on `require("nvim-treesitter").setup()` and `install()`.

The configuration installs parsers for:

```text
json javascript typescript tsx yaml html css prisma
markdown markdown_inline svelte graphql bash lua vim
 dockerfile gitignore query vimdoc c
```

The parser installation command is:

```text
:TSUpdate
```

To inspect installed parsers and the current syntax tree:

```text
:TSInstallInfo
:InspectTree
```

Zsh files are registered to use the Bash parser. The custom Treesitter configuration is:

```text
~/.config/nvim/lua/josean/plugins/treesitter.lua
```

## 10. Neovim modes and keymaps

| Mode | Purpose | Enter with |
|---|---|---|
| Normal | Navigate and run commands | `Esc` |
| Insert | Type text | `i` |
| Command | Run editor commands | `:` |
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

The configured leader key is Space. `<leader>` means press the Space bar.

```text
Space + sv    Vertical split
Space + sh    Horizontal split
Space + se    Equalize splits
Space + sx    Close split
Space + to    New tab
Space + tx    Close tab
Space + tn    Next tab
Space + tp    Previous tab
Space + tf    Current file in a new tab
Space + nh    Clear search highlighting
Space +       Increment number
Space -       Decrement number
jk            Leave Insert mode
```

With tmux navigation enabled:

```text
Ctrl-h    Move left
Ctrl-j    Move down
Ctrl-k    Move up
Ctrl-l    Move right
```

## 11. Daily workflow

```bash
cd ~/Projects/my-project
tmux
nvim .
```

Inside Neovim:

```text
:NvimTreeToggle
:Telescope find_files
:Telescope live_grep
:Mason
:LspInfo
:checkhealth
```

Inside NvimTree, `Enter` opens a file, `a` creates, `d` deletes, `r` renames, `R` refreshes, and `q` closes.

## 12. Running Lua

Lua normally runs automatically through `init.lua`. To execute Lua manually from Neovim's command line:

```text
:lua print("Hello from Lua")
:lua print(vim.o.number)
:lua vim.opt.number = true
```

Reload the configuration:

```text
:source ~/.config/nvim/init.lua
```

Restarting Neovim is generally safer after changing plugin or autocommand files:

```text
:qa
nvim
```

Avoid repeatedly requiring configuration modules if you are unsure what they do, because some modules create keymaps or autocommands.

## 13. Reproduce this build from scratch

The following is the high-level order used to build the system:

```bash
# 1. Install Homebrew, then tools.
brew install neovim node tmux eza bat ripgrep fd fzf zoxide btop dust git-delta jq tree-sitter tree-sitter-cli

# 2. Install Oh My Zsh, Powerlevel10k, and Zsh plugins.
# Follow the official links in the sections above.

# 3. Install or copy ~/.zshrc and ~/.p10k.zsh.
# Validate the shell before opening a new terminal.
zsh -n ~/.zshrc

# 4. Install TPM and copy ~/.tmux.conf.
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
tmux
# Press Ctrl-a, then I.

# 5. Install the Neovim configuration.
mkdir -p ~/.config
# Copy this build's nvim/ directory into ~/.config/nvim.

# 6. Start Neovim and let Lazy.nvim install plugins.
nvim
:Lazy sync

# 7. Install or update Treesitter parsers.
:TSUpdate

# 8. Install language servers and tools.
:Mason

# 9. Run diagnostics.
:checkhealth
```

For this repository, the guide itself lives at:

```text
~/Projects/neovim-starter-guide/README.md
```

This repository documents the build, while the live configuration remains in your home directory under `~/.config/nvim`, `~/.zshrc`, `~/.p10k.zsh`, and `~/.tmux.conf`.

## 14. Backups and recovery

Before the modern Lazy.nvim setup was installed, the previous Neovim configuration was moved to a timestamped backup:

```text
~/.config/nvim.before-josean.20261031005256
```

To restore it manually:

```bash
mv ~/.config/nvim ~/.config/nvim.current
mv ~/.config/nvim.before-josean.20261031005256 ~/.config/nvim
```

Only do this after closing Neovim. Keep the current directory as `nvim.current` until the restored setup has been tested.

## 15. Useful links

### Foundation and project references

- [My Neovim Starter Guide](https://github.com/w1ld3w0rks/neovim-starter-guide)
- [Josean Martinez's dev-environment-files](https://github.com/josean-dev/dev-environment-files)
- [Neovim documentation](https://neovim.io/doc/)

### Shell and terminal

- [Homebrew](https://brew.sh/)
- [Oh My Zsh](https://ohmyz.sh/)
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
- [fzf](https://github.com/junegunn/fzf)
- [zoxide](https://github.com/ajeetdsouza/zoxide)
- [eza](https://github.com/eza-community/eza)
- [bat](https://github.com/sharkdp/bat)
- [ripgrep](https://github.com/BurntSushi/ripgrep)
- [fd](https://github.com/sharkdp/fd)
- [btop](https://github.com/aristocratos/btop)
- [dust](https://github.com/bootandy/dust)
- [delta](https://github.com/dandavison/delta)

### tmux

- [tmux](https://github.com/tmux/tmux)
- [TPM](https://github.com/tmux-plugins/tpm)
- [Catppuccin tmux](https://github.com/catppuccin/tmux)
- [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator)
- [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect)
- [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum)

### Neovim plugins and tools

- [Lazy.nvim](https://github.com/folke/lazy.nvim)
- [Mason.nvim](https://github.com/williamboman/mason.nvim)
- [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)
- [nvim-cmp](https://github.com/hrsh7th/nvim-cmp)
- [LuaSnip](https://github.com/L3MON4D3/LuaSnip)
- [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter)
- [Telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)
- [NvimTree](https://github.com/nvim-tree/nvim-tree.lua)
- [Gitsigns](https://github.com/lewis6991/gitsigns.nvim)
- [Lualine](https://github.com/nvim-lualine/lualine.nvim)
- [Trouble.nvim](https://github.com/folke/trouble.nvim)
- [LazyGit](https://github.com/kdheepak/lazygit.nvim)

## Troubleshooting checklist

```text
:messages
:checkhealth
:Lazy
:Mason
:LspInfo
:TSInstallInfo
```

From the shell:

```bash
zsh -n ~/.zshrc
tmux -f ~/.tmux.conf -L neovim-guide-test start-server
nvim --headless '+qa'
```

If a plugin fails to load, first check `:Lazy`. If an LSP fails, check `:Mason` and `:LspInfo`. If parsing fails, verify both `tree-sitter` and `tree-sitter-cli` are installed and run `:TSUpdate`.
