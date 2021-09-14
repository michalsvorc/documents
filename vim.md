# Vim

Cheat sheets:

* [Vim Cheat Sheet](https://vim.rtorr.com/)
* [vim / vimdiff cheatsheet - essential commands · GitHub](https://gist.github.com/azadkuh/5d223d46a8c269dadfe4)
* [tabs and window splits](https://gist.github.com/Starefossen/5957088)

Graphical cheat sheets:

* [Vim Cheat Sheet](https://i.imgur.com/YLInLlY.png)
* [Keyboard cheat sheet](https://helloacm.com/wp-content/uploads/2015/09/vi-vim-cheat-sheet.jpg)

## Navigation

Jump to last edit:

```
<leader>. to your last change

<leader>` to where the cursor was before you made your last jump
```

Screen:

```
H | M | L

C + u | C + d | C + f | C + b
```

## Quick name refactor in one buffer

Place cursor at name to refactor and type gd (or `gD` if you're refactoring a global variable).

Then cgn new_name `<Esc>` and . one or more times to refactor next occurrence(s), or `:%norm .` to refactor all
occurrences in the buffer at once.

## Spelling

`z=` on a hovered word shows spell suggestions.

