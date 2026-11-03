## What it does

Checks that an overloaded function has at least two `@overload` definitions and that its definitions
agree on `@classmethod` and `@staticmethod`. If you use `@final` or `@override`, put it on the
implementation, or on the first overload if there is no implementation.

## Why is this bad?

An overload describes one of several ways to call a function. With only one signature, the function
can be annotated directly. Decorators that describe how a method is bound or how it participates in
inheritance apply to the whole method.

## Example

```py
from typing import overload


@overload
def foo(x: int) -> int: ...  # error
def foo(x: int) -> int:
    return x
```

## Configuration

Before 0.0.97, `invalid-overload` also reported missing implementations and implementations
inconsistent with their overloads. To keep a custom rule level for all three checks, set the same
level for `missing-overload-implementation` and `inconsistent-overload-implementation` as for
`invalid-overload`. If a `# ty: ignore[invalid-overload]` comment suppressed an implementation
diagnostic, replace the rule name with the corresponding implementation rule. Keep
`invalid-overload` alongside it if you also want to suppress a declaration error on that line.

## References

- [Python documentation: `@overload`](https://docs.python.org/3/library/typing.html#typing.overload)
