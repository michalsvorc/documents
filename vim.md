# Vim

Cheat sheets:

- [Vim Cheat Sheet](https://vim.rtorr.com/)
- [vim / vimdiff cheatsheet - essential commands · GitHub](https://gist.github.com/azadkuh/5d223d46a8c269dadfe4)
- [tabs and window splits](https://gist.github.com/Starefossen/5957088)

Graphical cheat sheets:

- [Vim Cheat Sheet](https://i.imgur.com/YLInLlY.png)
- [Keyboard cheat sheet](https://helloacm.com/wp-content/uploads/2015/09/vi-vim-cheat-sheet.jpg)

Blog posts:

- [Advanced Vim topics, tips and tricks](https://www.integralist.co.uk/posts/vim/)

## Working directory

Maintains different types of working directories:

- global
- local: `:lcd` sets the current directory for the current window.
- window: `:tcd` sets the directory for the current tab. The current window will also use this directory.

## Navigation

- `g;` jump to last edited position
- `gh` open file path
- `gx` open link in default browser

## Misc

- `z=` spelling suggestions

## History

- `q/` history of searches
- `q:` history of commands

## Search

Search in current file:

- Forward: `/`
- Backward: `?`
- Case-sensitive: `/<pattern>\C`
- Case-insensitive: `/<pattern>\c`

Search the word under the cursor:

- Forward: `*` or `g*`
- Backward: `#` or `g#`

## Search and replace

- [sed regular expressions](https://www.gnu.org/software/sed/manual/sed.html#sed-regular-expressions).
- [Vim Search and Replace With Examples](https://thevaluable.dev/vim-search-find-replace/)

### Grep search

Grep search populates the quickfix list.

```vim
:grep <pattern> <path>
:copen
```

Where path can be:

- filename
- glob pattern
- `*` working directory
- `%` current file

### Search in current file with list

Quickfix list:

```vim
:grep <pattern> %
:copen
```

### Quick name refactor in single buffer

Prefer LSP refactoring.

- Place the cursor at name to refactor and type `gd` or `gD` if you're refactoring a global variable.
- `cgn` to replace the name and escape insert mode.
- Cycle trough find results, use `.` to repeat replacement on occurrences or `:%norm .` to refactor all occurrences in the buffer at once.

### Substitute in the current file

`:s` current line
`:%s` current file

- `:%s/search/replace/g`
- `:%s//replace/g` replaces last search result

### Substitute in multiple files

Populate the quickfix list with search results.

Additionally filter quickfix list with [:Cfilter](https://neovim.io/doc/user/quickfix.html#%3ACfilter)

Execute search and replace command with `:cdo` in each valid entry in the quickfix list:

```vim
:cdo s/foo/bar/gc
```

- g: This flag means to replace all occurrences on each line.
- c: This flag means to confirm each substitution.

Save all modified buffers:

```vim
:cfdo | up
```

## Quickfix list

- [Quickfix](https://neovim.io/doc/user/quickfix.html)

### Filter results

- [Cfilter plugin](https://neovim.io/doc/user/quickfix.html#cfilter-plugin)

```vim
:packadd cfilter
:Cfilter /pattern/
```

Extract a quickfix sub-list:

```vim
:call setqflist(getqflist()[1:2])
```

### Open all items

```
:silent tabedit %
```

## Diff

`:diffthis` execute in every buffer you want to compare

## Help

`<C-]>` jump to tag under the cursor
`<C-o>` jump back

- `:1,10normal! I#` would insert a `# ` at the beginning of lines 1 to 10.!
- `'<,'>normal! @q` execute macro recorded for mark q over visual selection
