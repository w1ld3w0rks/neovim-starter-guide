# Backups and recovery

Before replacing a configuration, rename it with a timestamp. The prior Neovim setup is preserved at `~/.config/nvim.before-josean.20261031005256`.

To restore it after closing Neovim:

```bash
mv ~/.config/nvim ~/.config/nvim.current
mv ~/.config/nvim.before-josean.20261031005256 ~/.config/nvim
```

Keep the current directory until the restored configuration is tested. Never use destructive reset commands on a configuration you have not backed up.
