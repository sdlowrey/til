# Vim

## Replacing strings

You can use `sed` substitutions in command mode by preceding the expression with `%`.

To substitute `this` with `that` in the entire file:
```
:%s/this/that/g
```

To do the same but only over lines 1-2:
```
:6,10s/this/that/g
```

You can use `:&&` to repeat the last substitution on another set of lines.
```
:6,10s/this/that/g | 9,10&&
``` 
