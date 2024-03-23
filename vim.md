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

## Navigation

`g;` jump to last edited position

## Misc

`z=` spelling suggestions

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

Telescope plugin:

- [Github issue](https://github.com/nvim-telescope/telescope.nvim/issues/762)

```vim
Telescope current_buffer_fuzzy_find fuzzy=false case_mode=ignore_case
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

Using Telescope plugin:

1. Search with `:Telescope live_grep`.
2. Optionally filter Telescope results with `<Tab>`.
3. Send results to quickfix list: `<M>q` selected, `<C>q` all results.

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

Telescope plugin:

```vim
:Telescope quickfix
```

Extract a quickfix sub-list:

```vim
:call setqflist(getqflist()[1:2])
```
