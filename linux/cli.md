# CLI

- [CLI guidelines] https://clig.dev/
- [All commands sorted by votes](https://www.commandlinefu.com/commands/browse/sort-by-votes)

## fzf

- [repository](https://github.com/junegunn/fzf)

### Options

`-q, --query=STR`
Start the finder with the given query

`-m, --multi`
Enable multi-select with tab/shift-tab. It optionally takes an integer argument which denotes the maximum number of items that can be se‐
lected

`-e, --exact`
Enable exact search mode to perform a case-sensitive exact match, same as `'` operator

`-i, --ignore-case`
Case-insensitive match (default: smart-case match)

`+i, --no-ignore-case`
Case-sensitive match

`--preview`
Execute the given command for the current line, and display the result in the preview window. The placeholder `{}` is replaced in the command by the current entry (single-quoted). Example: `--preview 'stat {}`

### Search operators

Queries are not regex patterns, only plain text queries used in a fuzzy search algorithm.
fzf’s extended search mode enabled by default allows to use a couple of metacharacters similar to most common regex engines.

- Exact Match (`'`), example: `'foo`
- Prefix Match (`^`)
- Suffix Match (`$`)
- OR Operator (`|`)
- AND Operator (`&`)
- Negation (`!`)

You can combine different operators to refine your searches even further:

- Match lines that start with "foo" and end with "bar":

```sh
^foo&bar$
```

- Match lines that contain "foo" or do not contain "bar":

```sh
foo|!bar
```
