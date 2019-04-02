---
id: damageFormula
title: Anthem's Damage Formula
sidebar_label: Damage Formula
---

[Original study by Cebarik](/docs/blog/2019/02/26/damageFormula)

## The Formula

It helps to break up the damage formula as follows

```DamageDealt = NormalDamage * (1 + CriticalBonus) + 1```  

where

```NormalDamage = TooltipDamage *(1 +  SumDamageModifiers) * TypeModifier * (1 + DebuffModifiers)```

and

```CriticalBonus = ItemCritBonus * WeakPointResistanceMultiplier * (1 + CritModifiers)```



### Parameters used

**Base:** Card damage on the Weapon/Ability. For secondary damage sources this value is hidden.

**SumDamageModifiers:** If you’re looking at a weapon with +75% weapon damage and no other modifiers, this number is 0.75. However, this should be the sum of every applicable damage modifier. Consult the [Damage Types](mechanics/damageTypes.md) guide for more information about how to calculate this.

**TypeModifier:** This represents the damage bonus (or penalty) applied based on the damage type of your attack and the health type of the enemy. For example, if using lightning against a shielded enemy this value is 1.5. You can find a full table of TypeModifier values below. 

**SumDebuffModifiers:** Sum of all debuffs applied to an enemy that cause them to take additional damage. Currently Acid, Interceptor's Target Beacon, and Colossus' Taunt. Beacon and Taunt do not stack with each other. Thus, the maximum value is Acid (0.25) plus either Beacon or Taunt (0.33) for a total of 0.58

**ItemCritBonus:** For anything that can crit, this value depends on the damage source. Every weapon and ability that can crit has a crit multiplier specific to the item. Blastback is 2.4, Plasma Star is 1.5. a full list of datamined values can be found on [AnthemArchive](http:AnthemArchive.com) Please note that shielded enemies cannot be critically hit for damage purposes.

**WeakPointResistanceMultiplier:**  Each weakpoint on an enemy has it's own crit multiplier. This value is typically <1. For most enemies, this value is 0.75. Some enemies such as scars, outlaw shotgunners, and Ash Titan's have higher or lower values.

**CritModifiers:**  This value is the total of all applicable crit damage modifiers. If you have 10% on your primary gun (gear icon) and 50% on your secondary gun (gear icon), these values are 0.1 and 0.5, respectively. However, some slots other than weapons can roll javelin-wide (javelin icon) critical inscriptions. These inscriptions should be included.

### Damage Type Multipliers

| Attack Type | Against Health (Red) | Against Armor (Yellow) | Against Shields (Blue) |
| ------------ | ---- | ---- | ---- |
| **Impact**   | 1    | 0.5  | 0.75 |
| **Acid**     | 1    | 1.5  | 0.5  |
| **Electric** | 1    | 0.5  | 1.5  |
| **Ice**      | 1    | 0.75 | 1.25 |
| **Fire**     | 1    | 1.25 | 0.75 |


## Example

**Weapon:**
Level 38 Epic Anvil

**Other Relevant Gear:**
Viper's Bite with +18% Weapon Damage

**Target:** Ursix Head

**Critical:** Yes


Our values for the formula are as follows:

**Base:** 687 (from weapon card)

**SumDamageModifiers:** 0.68 (50% from weapon, 18% from the Viper’s Bite equipped in Case 1)

**TypeModifier:** 0.75 (Impact attacking armor)

**SumDebuffModifiers:** 0.33 (Target Beacon applied)

**ItemCritBonus:** 1.75

**WeakPointMultiplier:** 0.5

**CritModifiers:** 0.2 (I do not have additional critical modifiers on)



Plugging it in:
```
NormalDamage = 687 * (1 + 0.68)  * 0.75 * (1 + 0.33) = 1151
CritBonus =  1.75 * 0.5 * (1 + 0.2) = 1.05
DamageDealt = 1151 * (1 + 1.05) = 2360
```

The weapon will deal 2360 damage per shot to the target Ursix.

## Oddities and Exceptions
Sometimes, the damage numbers seen will not match this document. Every ability is buffed by an array of modifiers, and perhaps not the ones you might expect. For example, acid damage is physical and not elemental.

Here are a list of possible reasons your damage is not what you expected:
* Range - there is range falloff. If you are outside of the effective range, your damage may be reduced.
* Explosive Weapons/Gear - Devastator and all three grenade launchers, as well as many abilities, do damage in an area. Enemies may be hit for partial damage based on their proximity to the blast.
* Confusing Inscriptions - What inscriptions actually do is not always clear. For example, damage inscriptions on a Truth of Tarsis will apply only to the ‘Damage’ stat, but a weapon damage inscription elsewhere will apply to both
* Effects of other gear - Be sure you don’t have anything on that you forgot about. This may include in-combat buffs.
* Bugs - Unfortunately, many inscriptions don’t work exactly as you might expect. The Ranger’s Chaos Core and Crossed Arms components are great examples of this.
* Rounding - The game rounds numbers it displays. An item may read 100 damage but that could be anywhere from 499.5 to 500.49 (note: I am not sure how many decimals it rounds to). This will not cause a difference of more than a few points of damage, however.
