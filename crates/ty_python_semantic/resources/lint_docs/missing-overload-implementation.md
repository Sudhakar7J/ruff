## What it does

Checks for overloaded functions and methods that require an implementation but have none. An
implementation can be omitted in a stub file, when all overloads are in `if TYPE_CHECKING` blocks,
on a protocol method, or when every overload of a method on an abstract base class is decorated with
`@abstractmethod`.

## Why is this bad?

The `@overload` definitions describe the calls a type checker should accept. A separate
implementation handles those calls at runtime. Calling a function defined only with `@overload`
raises an exception.

## Example

```py
from typing import overload


@overload
def foo() -> None: ...  # error
@overload
def foo(x: int) -> int: ...
```

## References

- [Python documentation: `@overload`](https://docs.python.org/3/library/typing.html#typing.overload)
