# Python Tips & Tricks

## Selectively ignore specific exceptions

From Dan Bader:
You can use contextlib.suppress() to selectively ignore specific exceptions using a context manager and the "with" statement:

```
import contextlib

with contextlib.suppress(FileNotFoundError):
    os.remove('somefile.tmp')
```

This is equivalent to the following try/except clause:

```
try:
    os.remove('somefile.tmp')
except FileNotFoundError:
    pass
```