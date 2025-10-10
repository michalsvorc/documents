# Godot neovim support

Guides:
- [Topy721 | reddit](https://www.reddit.com/r/neovim/comments/1c2bhcs/godotgdscript_in_neovim_with_lsp_and_debugging_in/)

## Setup

### Enable external editor in Godot (v4.3)

Editor > Editor Settings >
| - Text Editor > External

Use External Editor: On
Exec Path: <nvim binary path> (/usr/bin/nvim)
Exec Flags: --server /tmp/godot.pipe --remote-send "<esc>:n {file}<CR>:call cursor({line},{col})<CR>"

| - Network > Language Server

Native Symbols in Editor: On
Check the language server port, by default it's `6005`.

| - Network > Debug Adapter

Synchronize Breakpoints: On
Check the port, by default it's `6006`.

### Godot project

Create new Godot project and initialize git in project root for better Neovim project root integration.

```.gitignore
# Godot 4+ specific ignores
.godot/
/android/
```

### Neovim LSP

Configure `nvim-lspconfig` with Godot Network > Language Server default port:

```lua
require("lspconfig")["gdscript"].setup({
  name = "godot",
  cmd = vim.lsp.rpc.connect("127.0.0.1", 6005),
})
```

### Starting Neovim

Ensure that Godot is running the project.

cd to project root and execute in terminal:

```shell
nvim --listen /tmp/godot.pipe
```

### Optional: syntax highlighting

Install tree-sitter `gdscript`.

### Optional: linter and formatter

Install [gdtoolkit](https://github.com/Scony/godot-gdscript-toolkit).

## QA

### Do I need netcat system package?

Windows only, Neovim on Windows doesn't support nvim.lsp.rpc.connect so you're gonna have to use ncat.
https://www.reddit.com/r/neovim/comments/1c2bhcs/godotgdscript_in_neovim_with_lsp_and_debugging_in/

