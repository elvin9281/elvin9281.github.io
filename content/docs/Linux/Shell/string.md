# Strings 

##  [Remove first and last quote (") from a variable](https://stackoverflow.com/questions/9733338/shell-script-remove-first-and-last-quote-from-a-variable)

- `'s/^"//'`replaces a leading " with nothing
- `'s/"$//'`replaces a trailing " with nothing 
- `<<<` : here-string Operator，string as `stdin`

(In the same invocation ,there isn't any need to pipe and start another sed. 
Using -e you can have multiple text processing).
```tpl
opt="\"html test\""

sed -e 's/^"//' -e 's/"$//' <<<"$opt"
```
---