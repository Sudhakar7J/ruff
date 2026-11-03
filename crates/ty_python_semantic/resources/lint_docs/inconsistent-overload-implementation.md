## What it does

Checks that an overload implementation is callable after decorators are applied. When the overloads
and implementation all have non-generic signatures, it also checks that the implementation accepts
every call allowed by each overload and that each overload's return type is assignable to the
implementation's return type.

## Why is this bad?

Callers rely on the overloads to know which arguments they can pass and what type to expect in
return. A call that matches an overload can fail if the implementation requires another argument.

## Example

```py
from typing import overload


@overload
def read() -> str: ...  # error
@overload
def read(size: int) -> str: ...
def read(size: int) -> str:
    return "x" * size
```

Adding a default value for `size` lets the implementation handle `read()` as well as `read(3)`.

## References

- [Typing specification: Implementation consistency](https://typing.python.org/en/latest/spec/overload.html#implementation-consistency)
