## What it does

Checks for functions and methods with only one `@overload` declaration.

## Why is this bad?

An overload describes one of several ways to call a function. If one signature describes all valid
calls, annotate the implementation directly and remove the overload declaration. In a stub file,
keep the declaration and remove the `@overload` decorator.

## Example

```py
from typing import overload


@overload
def foo(x: int) -> int: ...  # error
def foo(x: int) -> int:
    return x
```

## Migrating from `invalid-overload`

In 0.0.97, four rules replace `invalid-overload`. To keep a custom level for all the checks it
covered, replace the old setting with the same level for `single-overload`,
`inconsistent-overload-decorator`, `missing-overload-implementation`, and
`inconsistent-overload-implementation`. In a `ty: ignore` comment, list only the diagnostics you
want to suppress on that line. For example, to allow a lone overload without a required
implementation, use `# ty: ignore[single-overload, missing-overload-implementation]`.

## References

- [Python documentation: `@overload`](https://docs.python.org/3/library/typing.html#typing.overload)
