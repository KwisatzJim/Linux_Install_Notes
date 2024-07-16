### Fix fish not recognizing brew

```
vi ~/.config/fish/config.fish
```

```
if status --is-login
  eval (/opt/homebrew/bin/brew shellenv)
end
```

```
source ~/.config/fish/config.fish
```
