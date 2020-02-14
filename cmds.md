# Commands

## Attack Modifiers

### Sneak Attack

Usage: `!a [aname] sa`

```
!servsnippet sa {{ l = get("RogueLevel") }} {{ '-title "[name] makes a sneak attack with [aname]!" -d "' + str(ceil(l / 2)) + 'd6[Sneak Attack]" -f "Sneak Attack|Rogue Level ' + str(l) + '"' if l else '-f "Sneak Attack|You\'re not a rogue!"' }}
```

### Divine Smite

Usage: `!smite [slot level] [optional args]`
Optional args:
- `crit` indicates a critical hit. Dice will be doubled.
- `undead` indicates a strike against an undead or fiend. 1d8 added automatically.

```
!serveralias smite2 embed {{ isPld = get("PaladinLevel") }}
{{ crit = any([x == 'crit' for x in &ARGS&]) }}
{{ dead = any([x == 'undead' for x in &ARGS&]) }}
{{ l = %1% if not dead else %1% + 1 }}
{{ limit = 6 if dead else 5 }}
{{ dice = min(l + 1, limit) }}
{{ dice = dice * 2 if crit else dice }}
{{ roll = vroll(f"{dice}d8[radiant]") }}
-title "{{f"{name} {'uses' if isPld else 'attempts to use'} Divine Smite{' against an undead' if dead else ''}!"}}"
-f "{{f"Damage|{str(roll)}" if isPld else 'Result|You are not a paladin.'}}"
-f "{{f"Slot Level|{%1%}{', critical!' if crit else ''}"}}"
-thumb {{ image }}
-color #FFD700
```

## Feats

### Sharpshooter

Usage: `!a [aname] ss`

```
!servsnippet ss -b "-5[Sharpshooter]" -d "10[Sharpshooter]" -f "Feat Used|Sharpshooter"
```
