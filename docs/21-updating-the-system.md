# Updating

Update layers separately and verify after each one:

```bash
brew update && brew upgrade
```

Inside Neovim:

```text
:Lazy update
:MasonUpdate
:TSUpdate
:checkhealth
```

Update TPM plugins with `Ctrl-a`, then uppercase `U`. Review changes before committing. If a new update breaks startup, use the lockfile or restore the timestamped backup.
