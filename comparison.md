# Comparisons in Erlang

Are messed up!

```erlang
1 < false.
true
```

This is because `false` is an *atom*. In general,

```
number < atom < reference < fun < port < pid < tuple < list < bit string
```



