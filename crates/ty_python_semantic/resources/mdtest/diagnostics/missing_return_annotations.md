# Missing return annotations

```toml
[rules]
missing-return-type = "error"
```

## Functions

```py
def increment(value: int):  # snapshot: missing-return-type
    return value + 1

def annotated() -> str:  # ok
    return "ready"
```

```snapshot
error[missing-return-type]: Missing return type annotation for function `increment`
 --> src/mdtest_snippet.py:1:5
  |
1 | def increment(value: int):  # snapshot: missing-return-type
  |     ^^^^^^^^^
```

## Methods

```py
class Counter:
    def __init__(self):  # error: [missing-return-type]
        self.value = 0

    @classmethod
    def _unit(cls): ...  # error: [missing-return-type]
```

## Overloads

Only the overload signatures require an annotation.

```py
from typing import overload

@overload
def parse(value: int): ...  # error: [missing-return-type]
@overload
def parse(value: str) -> str: ...  # ok
def parse(value):  # ok
    return value
```

## Return type inference

The rule requires an explicit annotation whether ty infers a precise return type or falls back to
`Unknown`.

```toml
[analysis]
return-type-inference = "always"

[rules]
missing-return-type = "error"
```

```py
def inferred():  # error: [missing-return-type]
    return 1

def echo(value):  # error: [missing-return-type]
    return value

reveal_type(inferred())  # revealed: Literal[1]
reveal_type(echo(1))  # revealed: Unknown
```
