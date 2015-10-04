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

**Dealing with bits**

Erlang is awesome at bit manipulation.

```erlang
Color = 16#F09A29.
Pixel = <<Color:24>>.
Pixels = <<213,45,132,64,76,32,76,0,0,234,32,15>>.
<<Pix1:24, Pix2:24, Pix3:24, Pix4:24>> = Pixels.
<<R:8, Rest/binary>> = Pixels.
R. % 213
```

**Type specification**

* Values: integer | float | binary | bytes | bitstring | bits | utf8 | utf16 | utf32
* Sign: signed | unsigned
* Endianness: big | little | native
* Unit: unit:Integer

```erlang
<<X1/unsigned>> =  <<-44>>. %  <<"Ô">>
<<X2/signed>> =  <<-44>>.  % <<">>
X2. % -44
<<X2/integer-signed-little>> =  <<-44>>.
X2. % -44
<<N:8/unit:1>> = <<72>>. % <<"H">>
N. % 72
<<N/integer>> = <<72>>.
<<Y:4/little-unit:8>> = <<72,0,0,0>>.  
Y. 
```

**Bit manipulation**

The standard binary operations (shifting bits to left and right, binary 'and',
'or', 'xor', or 'not') also exist in Erlang.

Just use the functions bsl (Bit Shift Left), bsr (Bit Shift Right),
band, bor, bxor, and bnot.

```erlang
2#00100 = 2#00010 bsl 1.
2#00001 = 2#00010 bsr 1.
2#10101 = 2#10001 bor 2#00101.
```

For example, now we can pattern match to TCP segments:

```erlang
<<SourcePort:16, DestinationPort:16,
AckNumber:32,
DataOffset:4, _Reserved:4, Flags:8, WindowSize:16,
CheckSum: 16, UrgentPointer:16,
Payload/binary>> = SomeBinary.
```






