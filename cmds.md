# Commands

## Attack Modifiers

### Sneak Attack

Usage: `!a [aname] sa`

```
!servsnippet sa {{ l = get("RogueLevel") }} {{ '-title "[name] makes a sneak attack with [aname]!" -d "' + str(ceil(l / 2)) + 'd6[Sneak Attack]" -f "Sneak Attack|Rogue Level ' + str(l) + '"' if l else '-f "Sneak Attack|You\'re not a rogue!"' }}
```

### Divine Smite

Usage: `!smite [slot level]`

```
!serveralias smite embed {{ isPld = get("PaladinLevel") }}
{{ l = %1% }}
{{ roll = vroll(f"{min(l + 1, 5)}d8[radiant]") }}
-title "{{f"{name} {'uses' if isPld else 'attempts to use'} Divine Smite!"}}"
-f "{{f"Damage|{str(roll)}" if isPld else 'Result|You are not a paladin.'}}"
-f "{{f"Slot Level|{l}"}}"
-thumb {{ image }}
-color #FFD700
```

## Feats

### Sharpshooter

Usage: `!a [aname] ss`

```
!servsnippet ss -b "-5[Sharpshooter]" -d "10[Sharpshooter]" -f "Feat Used|Sharpshooter"
```
