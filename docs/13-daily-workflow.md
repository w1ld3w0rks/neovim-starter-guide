# Daily workflow

```bash
cd ~/Projects/my-project
tmux
nvim .
```

Use `:Telescope find_files` to open a file, `i` to edit, `Esc`, `:w` to save, `gd` for definitions, `K` for documentation, and `:q` to close. Use `:NvimTreeToggle` for a file tree, `:Mason` for tools, and `:LspInfo` to inspect the current language server.

For a new project, start with the project root as Neovim's working directory so Telescope, ripgrep, LSP, and Git integrations share the same scope.
