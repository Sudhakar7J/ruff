## What it does

Checks that the declarations and implementation of an overloaded method agree on `@classmethod` and
`@staticmethod`. If an overloaded function or method uses `@final` or `@override`, the decorator
belongs on the implementation, or on the first overload when there is no implementation.

## Why is this bad?

Every overload describes the same function. For example, if one overload is a static method and
another is an instance method, they disagree on whether Python passes the instance as the first
argument.

## Example

```pyi
from typing import overload

class Reader:
    @staticmethod
    @overload
    def read() -> str: ...
    @overload
    def read(self, size: int) -> str: ...  # error
```

## References

- For help updating an `invalid-overload` setting or ignore comment, see `single-overload`.
- [Typing specification: Invalid overload definitions](https://typing.python.org/en/latest/spec/overload.html#invalid-overload-definitions)
