# Invasion of Meridell

Invasion of Meridell was a fun turn based game that existed in Neopets up until 2011 (?), when it was permanently removed due to it being exploited (TODO, fill in details here).

## Resources Available

First, the resources we have available to use to reverse engineer the game.

Game Guides:
* http://www.jellyneo.net/?go=invasion_of_meridell
* http://www.thedailyneopets.com/neopets-games/invasion-of-meridell/
* https://www.neofriends.net/threads/guide-invasion-of-meridell-in-depth.26528/
* http://www.neocodex.us/forum/topic/109241-invasion-of-meridell-guide/
* http://neopointsdeals.com/neopets-invasion-of-meridell-guide/
* http://home.neopets.com/templates/homepage.phtml?pet_name=happylark
* http://www.neopets.com/~Demeanours
* http://www.angelfire.com/pop2/krillin373/invasionm.html
* https://www.pinkpt.com/neodex/index.php?title=Invasion_of_Meridell

Youtube Videos:
* https://www.youtube.com/watch?v=QJCtRCyfVww (levels 1, 2, 3)
* https://www.youtube.com/watch?v=644qdG2yd1w

[2015] Java Clone of game (author = darkflagrance):
- [Announcement](http://www.bay12forums.com/smf/index.php?topic=154262.0)
- [Source](https://drive.google.com/open?id=0B2Y0VMXUm08mRkNremE5ZVV0bnc)
- [Compiled Game](https://drive.google.com/file/d/0B2Y0VMXUm08maEFyTE5meG9hOFk/view?usp=sharing)

## Reverse Engineering Strategy

The 2015 Java Clone is a complete clone of the game - albeit imperfect (his goal seemed to be to recreate the experience and adjust the values as he saw fit, not necessarily to perfectly match the original game).

Our reverse engineering strategy is to start with the values in the 2015 Java Clone, then attempt to correct them based off our other resources (guides/videos).

In terms of trust...

* [Highest Trust] Images of the game from guides/youtube videos, as they are screencaps of the actual game being played (and there was no value in faking them at the time)
* [Medium Trust] Text from guides / youtube video description, as they were written while the actual game was live.
* [Low Trust] The 2015 Java clone falls in this category, as it was written 4 years after the game disappeared

With that in mind, we will cycle through each section of the game, review the Java values, and correct them.

### Treasures

All treasures were correct in the 2015 Java clone, verified by numerous screenshots online. No changes necessary.

### Potions

* Mission 1 = Health_Potion, verified in screenshots
* Mission 2 = Potion_of_Fortitude, verified in screenshots
* Mission 3 = Mega_Potion, verified in screenshots
* Mission 4 = Potion_of_Well-Being, verified in screenshots
* Mission 5 = Potion_of_Fortitude, verified in screenshots
* Mission 6 = Potion_of_Well-Being, verified in screenshots. (Java clone incorrectly puts Mega_Potion here)
* Mission 7 = Potion_of_Fortitude, verified in screenshots. (Java clone incorrectly puts Potion_of_Well-Being here)
* Mission 8 = Mega_Potion, verified in screenshots. (Java clone incorrectly puts Potion_of_Fortitude here)
* Mission 9 = ??? (Java clone puts Mega_Potion here)
* Mission 10 = ??? (Java clone puts Potion_of_Well-Being here)

There are no records in guides/videos from what potions are in Missions 9 and 10.

We've already established that the Java clone was incorrect in its values for Missions 6, 7, and 8 - so it is likely incorrect for 9 and 10 as well.

Pattern-wise in the 8 missions we were able to verify, there isn't a lot to go on.

Missions 3-8 go Mega / Well-Being / Fortitude and then Well-Being / Fortitude / Mega, which could indicate a recurring pattern which would next become Fortitude / Mega / Well-Being (popping the left-most element and putting it on the right).

There are only 4 potions, but 10 missions - so two potions (at least) would need to be used 3 times. We already see Fortitude being used 3 times, Mega and Well Being both twice, and Health just once... but then again, the Health potion seems basic, and may just be intended to be on the introductory level.

As all potions heal pets to full health and thus have no affect on gameplay other than asthetics, I've decided to just let this go and just go with the below values:

* Mission 9 = Potion_of_Well-Being. (Java clone puts Mega_Potion here)
* Mission 10 = Health_Potion. (Java clone puts Potion_of_Well-Being here)

### Attack Items

Every mission will spawn four items - two Attack items, and two Defense items.

There is some randomness in which weapon combinations will spawn. For example, in Mission 4 both the Magic_Force_Spell and the Bow are in the spawn pool - the possible spawns are two Bows, two Magic_Force_Spells, or one of each. Because of this, just because an item does not appear in a screenshot does not mean we can 100% rule it out.

* Mission 1 = ["Mace", "Broadsword"]. Verified in screenshots

* Mission 2 = ["Bow", "Hammer"]. Two screenshots have double bows. One screenshot shows a broadsword, which was likely picked up in Mission 1 and then dropped here when a new weapon was picked up. The Java clone includes Hammer, which we are unable to verify, but we include it here because it's the same base stat-line as bow and if we don't put it here it wouldn't fit anywhere.

* Mission 3 = ["Magic_Force_Spell", "Magic_Force_Spell"]. We have three unique game screenshots, all three of which have double Magic_Force_Spell spawned. The Java clone includes Berserker_Battleaxe as a possible spawn here - but I believe that is incorrect. None of our three unique screenshots support that. Also there is an advanced guide at http://www.neopets.com/~Demeanours which shows the items his team holds after beating Mission 3 and Mission 4, and in neither of them does any soldier have a Berserker_Battleaxe, even though it would be far better than the Magic_Force_Spell they are holding. So with that, I'm removing Berserker_Battleaxe from this spawn, and doing double Magic_Force_Spell, which fits all our screenshots and the guide.

* Mission  4 = ["Magic_Force_Spell", "Bow"]. Both Magic_Force_Spell and Bow are verified in screenshots showing the start of a Mission 4 level, giving us a high degree of certainty. The only variable is that the text in the description/guide on this video (https://www.youtube.com/watch?v=644qdG2yd1w) suggests a Berserker_Battleaxe should spawn in this level. We're going to assume that textual guide was in error, and trust the screenshots.

* Mission 5 = ["Berserker_Battleaxe", "Berserker_Battleaxe"]. The Java clone includes Magic_Force_Spell as a possible spawn here. I believe that is incorrect - all three unique game screenshots we have include double Berserker_Battleaxe. In Mission 3 we concluded that the Java Clone removed one Magic_Force_Spell spawn and replaced it with a Berserker_Battleaxe spawn, so it's not far-fetched to believe it did the opposite here - and our screenshots support the theory.

* Mission 6 = ["Sword_of_Deflection", "Sword_of_Deflection"]. Our one start of match screenshot has double Sword_of_Deflection. On a mid-game screenshot, a Berserker_Battleaxe is seen. However, it is within the path of the Techo, who likely dropped it to pickup a Sword_of_Deflection - so I believe the Berserker_Battleaxe was not spawned in this Mission, but just carried over from the previous mission and then dropped.

* Mission 7 = ["Double_Sword", "Halberd"]. We have two Mission 7 screenshots, and both are double Halberds. The guide at http://home.neopets.com/templates/homepage.phtml?pet_name=happylark notes that it's unnecessary to pick up Halberds here, as their attack bonuses (+4) aren't any better than what you already have. The Java clone includes "Double_Sword" here, which is identical in stats to the Sword of Deflection from the last level but without the ability to disenchant. I elected to keep this spawn chance here, even though not supported by screenshots, because the java game has it, and it fits in with the guide's note that the weapons here aren't worth picking up because they aren't better than what you already have (so gameplay is unchanged if I'm wrong and its Halberd). Also if Double_Sword does not go here... then it doesn't have a mission it spawns in.

* Mission 8 = ["Magic_Lightening_Spell", "Magic_Lightening_Spell"]. Single screenshot we have shows double Magic_Lightening_Spell. Text on video https://www.youtube.com/watch?v=644qdG2yd1w notes that you need to pickup a Magic_Lightening_Spell here for your Grundo. Java clone includes double "Magic_Lightening_Spell", so we'll roll with it.

* Mission 9 = ["Double_Axe", "Double_Axe"]. We have no screenshots or guides for this, so we'll just accept the Java clone's value.

* Mission 10 = ["Double_Axe", "Magic_Lightening_Spell"]. We have no screenshots or guides for this, so we'll just accept the Java clone's value.




### Defense Items

* Mission 1 = ["Magic_Staff_of_Thunder", "Magic_Staff_of_Thunder"]. All screenshots and guides show double Magic_Staff_of_Thunder, as does the Java clone.

* Mission 2 = ["Amulet_of_Teleportation", "Amulet_of_Teleportation"]. All start of game screenshots show double Amulet_of_Teleportation. Some mid game screenshots show Magic_Staff_of_Thunder, which we assume was dropped to pick up an Amulet_of_Teleportation.

* Mission 3 = ["Helmet", "Shield"]. We have 3 unique screenshots, all of which show double Helmet. However the guide at http://www.neopets.com/~Demeanours shows his team with Shields after beating Mission 3. Therefore, we accept the Java clone value of Helmet and Shield.

* Mission 4 = ["Plate_Armor", "Magic_Cloak_of_Invisibility"]. We have three unique screenshots of this Mission, all of which show double Plate_Armor here. The Java clone does not include Plate_Armor as a spawn option, including instead Amulet_of_Teleportation and Magic_Cloak_of_Invisibility. The guide at http://www.neopets.com/~Demeanours shows his team with a Magic_Cloak_of_Invisibility after beating this mission. Therefore, we take the Java clone value, but swap Amulet_of_Teleportation for Plate_Armor.

* Mission 5 = ["Counter_Enchantment_Helmet", "Counter_Enchantment_Helmet"]. We have three screenshots here, all of which show only Counter_Enchantment_Helmet. The Java clone uses (normal) Helmet and Shield as spawn options. We know "Helmet" is wrong and should be "Counter_Enchantment_Helmet". The only evidence for "Shield" is that the Java clone includes it, but since we already know the Java clone is wrong, we'll just go double "Counter_Enchantment_Helmet" here (which matches all screenshots). This makes up for the next mission, where the Java clone spawns too many Counter_Enchantment_Helmet so we need to reduce them.

* Mission 6 = ["Plate_Armor", "Plate_Armor"]. All screenshots solely support Plate_Armor spawning here. The Java clone has a double Counter_Enchantment_Helmet here. We'll roll with double Plate_Armor to support the screenshots.

* Mission 7 = ["Chainmail", "Chainmail"]. We have only 2 screenshots, which both have double Chainmail. The guide at http://home.neopets.com/templates/homepage.phtml?pet_name=happylark notes that it's unnecessary to pick up Chainmails here, as their defense bonuses (+4) aren't any better than what you already have. The Java clone includes Leather_Armor here alongside Chainmail. Leather_Armor is supposed to be in Mission 8 according to screenshots, but the Java clone is missing it - so assume the Java clone is wrong here and misplaced Leather_Armor, but it's really supposed to be double Chainmail.

* Mission 8 = ["Leather_Armor", "Leather_Armor"]. Our sole screenshot has double Leather_Armor. The Java clone has Plate_Armor and Chainmail as the spawn options, so it's wrong for leaving out Leather_Armor. We cannot know whether double Leather_Armor or Leather_Armor + X is correct here. I elect to go with double Leather_Armor to match the screenshots. The core concept seems to be that this armor (at +3) is worse than what you already have, but better than nothing. Including Plate_Armor (+5) or Chainmail (+4) would go against that concept.

* Mission 9 = ["Amulet_of_Teleportation", "Chainmail"]. We have no screenshots or guides for this, so we'll just accept the Java clone's value.

* Mission 10 = ["Plate_Armor", "Chainmail"]. We have no screenshots or guides for this, so we'll just accept the Java clone's value.

### Foes

All foes spawns were correct in the Java clone for Missions 1-8 that we were able to verify with screenshots. Therefore, we just trust the Java clone to be correct for Missions 9 and 10.

### Map - Mountains

Reviewing all game board screenshots, we see there are all four sets of two mountains, and they are connected symmetrically by row. Each set of two mountains may spawn on the far right and left, or one block in from the right and left, or in the middle two squares. The only exception is the top-most row, which if it spawns in the middle, then the left mountain remains an empty space (because in later levels an enemy troop will spawn in that square).

### Map - Villages

The villages always spawn in rows 2-4 (counting from the bottom up). There are two villages per row, and each row has one in the first 5 squares and one in the second 5 squares.

### Map - Items

Potions always spawn in the same two slots.

Attack/Defense items always spawn in rows 2-6 (counting from the bottom up). Note that they only spawn in empty spaces, calculated AFTER everything else has spawned. This means villages, mountains, and potions spawn before them.

I believe that it is a purely random chance, but my screenshots make it seem like rows 4-6 have a greater chance of getting items. I believe this is just due to the fact that villages spawn in the lower rows, reducing the number of empty squares and thus reducing the likelihood for items to spawn there.

### Pet Stats

[Enemies stats reviewed here](foe_pet_stats.md)

[Allies stats reviewed here](friendly_pet_stats.md), and [also here](pet_stats.md)

### Misc

[Spells reviewed here](spells.md)

[Shields reviewed here](shields.md)

### List of Unknowns

* We do not know which potions spawn in Mission 9 and 10. (Does not change gameplay)

* We assume item spawn chances do not change between battles in a mission. Is it possible they do? (If so, does change gameplay)

* We have no proof that "Hammer" should spawn as an attack item in Mission 2.

* We have no proof that "Double_Sword" should spawn as an attack item in Mission 7.

* We have no knowledge of what ATTACK or DEFENSE items spawn in Missions 9 and 10 - but at that point, a players items should be maxed out, so this shouldn't affect gameplay unless one of their soldiers gets converted.
