# Zsh and Oh My Zsh

Files:

```text
~/.zshrc
~/.p10k.zsh
~/.oh-my-zsh/
~/.oh-my-zsh/custom/plugins/
```

The active theme is `powerlevel10k/powerlevel10k`. Plugins are `git`, `zsh-autosuggestions`, `zsh-syntax-highlighting`, and `web-search`. Install the external plugins from their official repositories:

- [Oh My Zsh](https://ohmyz.sh/)
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

The custom shell section initializes fzf and zoxide, sets Catppuccin-inspired Powerlevel10k colors, and defines aliases for eza, bat, ripgrep, dust, btop, Git, LazyGit, reload, and Homebrew updates. `mkcd` creates and enters a directory.

Validate safely with `zsh -n ~/.zshrc`, then reload with `source ~/.zshrc`.
