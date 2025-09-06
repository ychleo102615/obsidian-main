[參考](https://unix.stackexchange.com/questions/2161/rsync-filter-copying-one-pattern-only)
[man](https://linux.die.net/man/1/rsync)

```
rsync -zar --prune-empty-dirs --include "*/" --include="*.mp4" --include="*/4.screenshot/*/*.png"  --exclude="*"  littleGameCliTool testing
```