---
layout: post
title:  "Nested try/except blocks and re-raised exceptions in Python 2 and 3"
categories: Python
---

In Python, you can re-raise an exception caught in an `except` block just by saying `raise`.
However, there can be unexpected behaviour when working with nested try/excepts.
Consider the following code:

```python
try:
    raise ValueError()
except ValueError as e1:
    try:
        raise TypeError()
    except TypeError as e2:
        pass
    raise 
```

You'd expect that this code would re-raise `ValueError`, and it does - on Python 3.
On Python 2, it re-raises `TypeError` instead, despite it having been caught in the
nested try/except block.

In this scenario, to get the expected behaviour on both Python 2 and Python 3,
an unqualified `raise` can't be used. Instead, the original exception needs to be
re-raised explicitly, e.g. `raise e1` in the example above.
