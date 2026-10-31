# Performance

Measure before changing configuration. Use `nvim --startuptime /tmp/nvim-startup.log`, inspect `:Lazy`, and keep shell plugins limited to those you use. Lazy-load UI and editing plugins when startup time becomes noticeable.

Avoid putting expensive commands in `~/.zshrc`; keep them behind command checks or lazy integrations. Large repositories benefit from ripgrep, fd, and disabled unnecessary indexing.
