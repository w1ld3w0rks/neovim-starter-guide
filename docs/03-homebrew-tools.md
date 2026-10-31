# Homebrew tools

Install the current build's packages:

```bash
brew install neovim node tmux eza bat ripgrep fd fzf zoxide btop dust git-delta jq tree-sitter tree-sitter-cli
```

| Tool | Purpose | Example |
|---|---|---|
| `eza` | Modern directory listings | `ll`, `lt` |
| `bat` | Colored file viewing | `cat file` |
| `rg` | Fast recursive search | `rg pattern` |
| `fd` | Fast file finding | `fd config` |
| `fzf` | Fuzzy selection | shell history/file search |
| `zoxide` | Frecency directory jumping | `z project` |
| `btop` | Resource monitor | `top` alias |
| `dust` | Disk usage | `du` alias |
| `delta` | Git diff pager | Git integration |
| `jq` | JSON processing | `jq . file.json` |
| `tree-sitter-cli` | Parser compilation | required by current Treesitter |

Verify with `command -v nvim tmux eza bat rg fd fzf zoxide tree-sitter`.
