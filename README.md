# Playing with Erlang

Reading through [the book](http://learnyousomeerlang.com/starting-out-for-real).

**Tuple unpacking**

```erlang
Point = {4, 5}.
{X, Y} = Point.
X.
% 4
{Z, _} = Point. % Second tuple element will be unbound.
```
