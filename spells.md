# General

Halberd
- Allows bearer to have 5 moves per turn. (However, skeith teleport locks skeith out from any additional moves)

# Grundo

Magic Force Spell
- Is 'earlier' healing item
- Heals a targeted ally
- Requires both Grundo and target have an available move
- Grundo cannot heal self
- Exact amount healed is unknown. No guides specify numbers, and youtube videos unfortunately cropped out the numbers.
- Java clone heals for 50% of the Grundo's attack value.
- We will use Java clone's value of 50% of the Grundo's attack value.

Magic Lightning Spell
- Is 'upgraded' healer item, better than Magic Force spell
- Heals all allies in the same (vertical) column as the ally you target, but costs 1 turn per ally healed.
- Requires both Grundo and target have an available move
- Grundo cannot heal self (even if in target column)
- In relationship to Magic Force Spell, one guide notes that THIS item has increased healing power but decreased attack bonus.
- Java clone uses same logic for healing amount on this item, 1/2 of the Grundo's attack value.
- However... this item's heal all allies in same column is not an 'upgrade' but rather a 'downgrade', as it still costs 1 turn per heal. Additionally, this item has 1 less attack. Those factors, combined with the fact that one guide notes it has increased healing power, makes me believe it should have a higher healing amount.
- Based on that, we will make this heal for 100% of Grundo's attack value so it is an actual improvement.
- Additionally, this spell allows a Grundo to attack a unit 2 spaces away (like Scorchio's bow)

When a unit is healed...
- Top of page displays: "Zap!!!<br><br>You've moved 2 out of 5"

# Skeith

Amulet of Teleportation
- Allows teleporting once per turn.
- Cannot teleport if enchanted.
- If Skeith is not holding Berserker_Battleaxe, then teleporting consumes ALL of Skeith's moves for the turn.
- Can teleport to any row except top 3 rows (put another way, can teleport to bottom 7 rows) that is unoccupied.
- Top of page displays: "Teleported!<br>You've moved 1 out of 5"

# Techo
Sword of Deflection
- Breaks enchantments on Skeiths, consumes a move, similar to healing by a grundo
- Top of page displays: "Woosh!!! Enchantment banished!<br><br><br>You've moved 1 out of 5"

# Moehog
Counter Enchantment Helmet
- Breaks enchantments on Grundos, consumes a move, similar to healing by a grundo
- Top of page displays: "Woosh!!! Enchantment banished!<br><br><br>You've moved 1 out of 5"

# Buzz/Grarrl
- Can enchant both grundo AND skeith (guide confirms both can cast either enchantment)
- String battlelog=a.name+" seals "+d.name+"'s ability to teleport!";
- String battlelog=a.name+" seals "+d.name+"'s ability to heal!";
- Java clone has both casting both spells, equally, with a 1 in 2 chance of each invader casting a spell on a given turn.
- I feel like the 1 in 2 chance is too frequent.
- Demeanor's guide confirms that Buzz can cast both spells

# Scorchio
- can attack two spaces away with Bow (rangedatk)
- Equip this to your Scorchio; once he reaches the rank of Soldier he can shoot his bow from 2 spaces away to attack.

