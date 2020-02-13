# Commands

## Attack Modifiers

### Sneak Attack

Usage: `!a [aname] sneak`

```
!servsnippet sneakattack {{ l = get("RogueLevel") }} {{ '-title "[name] makes a sneak attack with [aname]!" -d "' + str(ceil(l / 2)) + 'd6[Sneak Attack]" -f "Sneak Attack|Rogue Level ' + str(l) + '"' if l else '-f "Sneak Attack|You\'re not a rogue!"' }}
```

## Feats

### Sharpshooter

Usage: `!a [aname] sharpshooter`

```
!servsnippet sharpshooter -b "-5[Sharpshooter]" -d "10[Sharpshooter]" -f "Feat Used|Sharpshooter"
```
