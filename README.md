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

**Set manipulation**

```erlang
40> [1,2,3] ++ [4,5].
[1,2,3,4,5]
41> [1,2,3] -- [4,5].
[1,2,3]
```


**Lists and stuff**

```erlang
hd([1,2,3,4]). % 1        % car
tl([1,2,3,4]). % [2,3,4]  % cdr
List = [2,3,4].
NewList = [1|List].
[Head|Tail] = NewList.
Head.
Tail.
```

**List comprehension**

```erlang
[ 2 * N || N <- [1, 2, 3, 4] ]. % [2,4,6,8]
[X || X <- [1,2,3,4,5,6,7,8,9,10], X rem 2 =:= 0].
RestaurantMenu = [{steak, 5.99}, {beer, 3.99}, {poutine, 3.50}, {kitten, 20.99}, {water, 0.00}].
[{Item, Price*1.07} || {Item, Price} <- RestaurantMenu, Price >= 3, Price =< 10].
% [{steak,6.409300000000001},{beer,4.2693},{poutine,3.745}]
% Possible to have multiple generator expressions and multiple conditions.
% Also possible to use generators to pattern match and extract.
Weather = [{toronto, rain}, {montreal, storms}, {london, fog},
 {paris, sun}, {boston, fog}, {vancouver, snow}].
FoggyPlaces = [X || {X, fog} <- Weather]. % [london, boston]
```





