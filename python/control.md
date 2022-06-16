# Control structures

- [Python SpeedSheet](https://speedsheet.io/s/python?select=45aB)

## if

```python
if condition_1:
    ...
elif condition_2:
    ...
else:
    ...
```

## for

```python
for item in sequence_1:
    ...
```

For-else:

```python
for i in range(range_options):
    ...
else:
    ...
```

## while

```python
while condition:
    ...
    break          # Exit for loop.
    ...
    continue       # Jump to next iteration.
    ...
else:
    ...            # When condition = False.
```

## Loop control

Exit Loop: `break`

Continue on Next Iteration: `continue`

## match

Python Version: 3.10+

```python
match variable_1:
    case value_1:
        ...
    case _:        # Unmatched
        ...
```
