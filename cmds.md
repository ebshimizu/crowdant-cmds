# Commands

### Report Result

Usage: `!report [value] [reason]`

```
!serveralias report embed
-title "Reporting real roll for {{ name }}"
-f "Result|**%1%** total for &2&"
-thumb {{ image }}
```

### Health Potion

```
!serveralias hpot embed
{{ mods = {"reg" : 2, "greater" : 4, "superior" : 8, "supreme" : 20 } }}
{{ die = {"reg" : 2, "greater" : 4, "superior" : 8, "supreme" : 10 } }}
{{ render = {"reg" : "", "greater" : "Greater ", "superior" : "Superior ", "supreme" : "Supreme " } }}
{{ args = &ARGS& }}
{{ level = args[0] if len(args) else "reg" }}
{{ r = vroll(f"{die[level]}d4+{mods[level]}") }}
-title "{{f"{name} uses a {render[level]}Potion of Healing"}}"
-f "{{f"HP Recovered|{str(r)}"}}"
-color #00FF00
-thumb {{ image }}
```

## Attack Modifiers

### Shadow Blade

Usage: Character adds a custom attack. Have them copy + paste the following.

```!a add "Shadow Blade" -d 2d8[psychic] -b "{{ dexterityMod + proficiencyBonus }}"```

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
!serveralias smite embed {{ isPld = get("PaladinLevel") }}
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

### Flame Arrows

```
!snippet fa -d "1d6[fire]" -f "Bonus Damage|Flame Arrows"
```

### Hunter's Mark

```
!snippet hm -d "1d6" -f "Bonus Damage|Hunter's Mark"
```

## Feats

### Sharpshooter

Usage: `!a [aname] ss`

```
!servsnippet ss -b "-5[Sharpshooter]" -d "10[Sharpshooter]" -f "Feat Used|Sharpshooter"
```

### Sacred Weapon

```
!snippet sw -b "3[Sacred Weapon]" -d "3[Sacred Weapon]" -f "Feat Used|Sacred Weapon"
```

## Spells

### Thorn Whip

Usage: `!thwhip`

```
!serveralias thwhip embed {{ r = vroll(f"1d20 + {spell + proficiencyBonus}") }}
{{ lv = level }}
{{ ct = 4 if lv >= 17 else (3 if lv >= 11 else (2 if lv >= 5 else 1)) }}
{{ crit = r.result.crit == 1 }}
{{ ct = ct * 2 if crit else ct }}
{{ dmg = vroll(f"{ct}d6[piercing]") }}
-title "{{f"{name} casts Thorn Whip!"}}"
-f "Attack|{{f"**To Hit**: {str(r)}{', critical hit!' if crit else ''}\n**Damage**: {str(dmg)}"}}"
-thumb {{ image }}
-color #0a6b12
-desc "You create a long, vine-like whip covered in thorns that lashes out at your command toward a creature in range. If the attack hits, the creature takes damage, and if the creature is Large or smaller, you pull the creature up to 10 feet closer to you."
```
