- Positional arguments are arguments that are called by their order of appearance or position in the function definition.
- Given the function below to calculate a certain percentage of a certain number:

```python
def percentage(number, percent):
  return (number * percent) / 100

percentage(50, 75)	# 75% of 50
percentage(75, 50)	# 50% of 75
```

> [!NOTE]
> Unlike [[keyword arguments]], **order of appearance** for arguments matters.
