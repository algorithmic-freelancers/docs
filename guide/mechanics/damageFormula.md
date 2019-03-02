---
id: damageFormula
title: Anthem's Damage Formula
sidebar_label: Damage Formula
---

[Original study by Cebarik](/docs/blog/2019/02/26/damageFormula)

## The Formula

Anthem's damage formula is as follows:

```DAMAGE = (Base * (1+A)*B*(1+C)*D*E)+1```


### Parameters used

**A:** Damage Modifiers. If you’re looking at a weapon with 75% weapon damage and no other modifiers, this number is 0.75. However, this should be the sum of every applicable damage modifier. Consult the [Damage Types](mechanics/damageTypes.md) guide for more information about how to calculate this.

**B:** Crit Multiplier. For anything that cannot crit, this value is 1. For anything that can crit, this value depends on what it is. Every weapon and ability that can crit has a crit multiplier specific to the item. For Blastback, this value is 1.8. For Plasma Star, this value is 0.75. Please note that shielded enemies cannot be critically hit for damage purposes.

**C:** Critical Damage Modifiers.  If your item cannot crit, this value is 0. If your item can crit, this value is the total of all applicable crit damage modifiers. If you have 10% on your primary gun (gear icon) and 50% on your secondary gun (gear icon), these values are 0.1 and 0.5, respectively. However, some slots other than weapons can roll javelin-wide (javelin icon) critical inscriptions. These inscriptions should be included.

**D:** Damage type multiplier. This represents the damage bonus (or penalty) applied based on the damage type of your attack and the health type of the enemy. All attacks fall into one of 5 categories: Impact, Acid, Electric, Ice, or Fire. A table showing what the value of D should be is shown in the table below

**E:** Debuff multiplier. If the enemy is neither afflicted by Acid nor Target Beacon, this value is 1. This value increased by 0.25 if the enemy is afflicted by Acid, and increases by 0.33 if the enemy is marked with Target Beacon. If both are applied, this value is 1.58.


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
![alt-text](/docs/assets/damageFormulaWeapon.png)

**Other Relevant Gear:**
![alt-text](/docs/assets/damageFormulaGear.png)

**Target:** Ursix

**Critical:** Yes


Our values for the formula are as follows:

**Base:** 50 (from weapon card)

**A:** 0.68 (50% from weapon, 18% from the Viper’s Bite equipped in Case 1)

**B:** 0.5

**C:** 0 (I do not have additional critical modifiers on)

**D:** 0.75 (Impact attacking armor)

**E:** 1.33 (Target Beacon applied)

Plugging it in:
```
DAMAGE = 238 * (1.68) * (0.5 + 1) * 0.75 * 1.33 + 1
DAMAGE = 599
```

The weapon will deal 599 damage per shot to the target Ursix.

## Oddities and Exceptions
Sometimes, the damage numbers seen will not match this document. Every ability is buffed by an array of modifiers, and perhaps not the ones you might expect. For example, acid damage is physical and not elemental.

Here are a list of possible reasons your damage is not what you expected:
* Range - there is range falloff. If you are outside of the effective range, your damage may be reduced.
* Explosive Weapons/Gear - Devastator and all three grenade launchers, as well as many abilities, do damage in an area. Enemies may be hit for partial damage based on their proximity to the blast.
* Strange Enemies - Some enemies (such as many of the Scar and the Outlaw Shotgunners) take more or less to some or all parts of their body. Ash Titans are another example.
* Confusing Inscriptions - What inscriptions actually do is not always clear. For example, damage inscriptions on a Truth of Tarsis will apply only to the ‘Damage’ stat, but a weapon damage inscription elsewhere will apply to both
* Effects of other gear - Be sure you don’t have anything on that you forgot about. This may include in-combat buffs.
* Bugs - Unfortunately, many inscriptions don’t work exactly as you might expect. The Ranger’s Chaos Core and Crossed Arms components are great examples of this.
* Rounding - The game rounds numbers it displays. An item may read 100 damage but that could be anywhere from 499.5 to 500.49 (note: I am not sure how many decimals it rounds to). This will not cause a difference of more than a few points of damage, however.
