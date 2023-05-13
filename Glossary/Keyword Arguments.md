- Keyword arguments are arguments that can be called using their key in the function definition as key-value pairs.
- The example function below calculates a certain percentage of a certain number:

```python
def percentage(number, percent):
    return (number * percent) / 100

percentage(number=50, percent=75)	# 75% of 50
percentage(percent=75, number=50)	# 75% of 50
```

> [!CAUTION]
> In [[Python]], no space is allowed around the '=' sign in a keyword argument.

> [!NOTE]
> Unlike [[positional arguments]], **order of appearance** for arguments doesn't matter.
