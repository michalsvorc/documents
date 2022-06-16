# Errors

## Error handling

- [Python SpeedSheet](https://speedsheet.io/s/python?select=Gtxq)

```python
try:
	...

except Exception1:
	# Catches Exception1
  # No exception variable assignd so exceptions can not be referenced in this block.
	...

except Exception2 as exception_2
	# Catches Exception2, Reference with exception_2
	...

except Exception as exception_3
	# Catches Any Exception
	...

else:
	# Called if no exception thrown.
	...

finally:
	# Always executes even if an exception is thrown.
	...
```
