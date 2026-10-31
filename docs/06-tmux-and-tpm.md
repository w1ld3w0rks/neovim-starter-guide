# tmux and TPM

Configuration: `~/.tmux.conf`. Plugin manager: [TPM](https://github.com/tmux-plugins/tpm), installed at `~/.tmux/plugins/tpm`.

Plugins:

- [Catppuccin tmux](https://github.com/catppuccin/tmux)
- [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator)
- [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect)
- [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum)

Prefix is `Ctrl-a`. Use `Ctrl-a |` for a vertical split, `Ctrl-a -` for a horizontal split, `Ctrl-a c` for a current-directory window, and `Ctrl-a r` to reload. `Ctrl-a h/j/k/l` navigates panes. Copy mode uses Vim keys: `Ctrl-a [`, `v`, `y`, `q`. Mouse and true color are enabled.

Install TPM, start tmux, and press `Ctrl-a`, then uppercase `I`.
