# Plugin development

Create one file under `~/.config/nvim/lua/josean/plugins/` per feature. Return a Lazy.nvim spec, prefer lazy-loading when safe, and keep configuration inside `config = function() ... end`.

```lua
return {
  "author/plugin",
  event = "VeryLazy",
  opts = {},
}
```

After adding a plugin: save, restart, run `:Lazy sync`, inspect `:messages`, and document any external dependency. Do not copy stale Packer hooks into Lazy specs.
