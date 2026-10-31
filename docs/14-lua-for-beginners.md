# Lua for Neovim beginners

Lua files return values or execute setup code. A plugin spec commonly looks like:

```lua
return {
  "author/plugin",
  config = function()
    require("plugin").setup({})
  end,
}
```

Neovim exposes its API through `vim`:

```text
:lua print(vim.o.number)
:lua vim.opt.number = true
:lua print(vim.fn.getcwd())
```

Use `:source ~/.config/nvim/init.lua` for a reload, but restart Neovim after changing plugin loading, autocommands, or dependencies.
