# Roadmap

Veloren's development process is naturally open-ended and guided by its community: new features get added as and when
there is consensus within the community. Veloren's development is a constant process of re-evaluation and incremental
improvement, with contributors working on the features that most interest them. For this reason, the project doesn't
have a precise roadmap! The goal of this roadmap is to provide a rough idea of where Veloren is headed, while also trying to explain why things are the way they are, and why some features are still unclear. Another thing to note is that we want all those features to work alongside each other to create synergies and deeper gameplay. Therefore, you will see similar subjects addressed in different parts of the roadmap. Finally, we are not able to provide a specific date for those features, as we are not a game studio: the game is based on the work of volunteers, whose time and motivation vary, so it’s impossible for us to give concrete estimates without creating potential disappointment for the players awaiting those features.

**Existing Features’ Expansion/Rework:**



* **Durability**

How it works

Every piece of equipment, consisting of armor and weapons, starts off with 12/12 charges of durability with each death reducing said charge by 1. Durability has no effect on the stats of the equipment for a vast majority of charge, with the player only seeing a reduction in stats once the armor reaches 4/12 durability and steeply continues to decline the closer it gets to 0/12. Once a piece of equipment reaches 0/12 durability the item will still be usable, however, due to the steep decline in stats it becomes unviable for combat. A player can repair their damaged items at repair benches found in towns, costing Velorite and the primary material at lower levels.

Why do we want this?

Durability is an important death penalty as it hinders players from continuously zerg-rushing entities that exceed their abilities in order to obtain high-ranking items. 

Future plans

Durability is a relatively new mechanic within the world of Veloren and thereby lacks polish. With the current implementation of the mechanic being unclear and frustrating for a lot of players, we are looking at a few tweaks that would make it more accessible and understandable for the players. The planned changes consist of:
- Reducing the maximum durability to 8.
- Making all repairs free.
- Adding an option to *reinforce* durability, temporarily raising the maximum durability by eg. 6 on every reinforcement
  - Each reinforcement would cost extra materials (velorite + primary materials).
  - Reinforced durability cannot be repaired.
- UI Changes:
  - Make the durability section of the death screen more explanatory (and flash!).
  - Add a durability bar below damaged items.

Additionally, we would like to incorporate more Points of Interest in the open world of Veloren such as Inns or other resting locations which allow you to repair your items outside of towns.

For more information, feel free to contact us on the Veloren Discord. 



* **Pets and Mounts**

Pets and Mounts have both been introduced in the game for a while now. However, they are far from being a complete system. We plan to rework them sometime in the future, but most of the mechanics wanted for pets and mounts have to be discussed to know where we are headed. It is quite a complex topic, as there have been many variants of pets in games we take inspiration from. There is no set plan for how they will work, and it will probably take time for them to get a proper rework. Those are some of the questions and debates we have surrounding the system:



1. Should pets and mounts die permanently? If yes, how do we make them more resistant and less superficial? 
2. How should we implement the orders that we give? Should it be a skill tree? Should it be only related to combat? Etc. 
3. How do we distinguish battle pets from regular pets?

For more information, feel free to contact us on the Veloren Discord. 



* **Vehicles (Airships, Ships, Trains, Carriages, etc.)**

When asked about fast travel, we answer that there will be no teleportation. Instead, we have decided that we want to add faster means of travel, aka vehicles. The 100% confirmed means of travel are Airships and Ships. Carriages and trains are still on the discussion table, or at least we aren’t 100% sure how they will operate aesthetically or technically. The decision to not have instant travel is to protect the economy and incentivize players to explore. Flights/Rides will take less time but will not be instant. Because of that, we also want to make sure those travels aren’t chores, so we want to have enough potential activities to do on them notably by having crafting stations and other players/NPCs to talk/trade with. As for ownership, there is no set decision yet on how it will be implemented for technical and gameplay reasons. Some questions we ask ourselves are for example: “How accessible should such a vehicle be?” “Won’t it be weird if everyone has their own ship/airship?” “What do we do about a vehicle when its owner logs out?” etc. For more information, feel free to contact us on the Veloren Discord. 



* **Food**

Currently, food serves as a healing mechanic, but we plan to change it to a “long-time buff”. 



* **Economy**

We plan to have a complete economy that touches upon every single aspect of the game. That’s to say all mechanics will be directly or indirectly impacted by the economy. The ideal goal is to reach a point where players and NPCs can impact the economy without breaking it, while also ensuring no artificial resources are spawned. This means that we want all resources and coins to be actually traded and not appear out of nowhere. This will allow the game to have coherent/developed shortages, supply and demand pricing, price competition, market control, market regulations, regions of influence, trade routes, externalities, etc. While this is extremely promising, it is also extremely complex and hard to pull off, therefore, it will take a lot of time and tweaking to reach a stable and believable stage. For more information, feel free to contact us on the Veloren Discord. 



* **World Sim**

In Veloren’s description, Dwarf Fortress is listed as one of the inspirations, and world sim is where most of that inspiration will go. Currently, we have rtsim, which is a system that keeps track of things that change over time in the world. This ranges from NPCs to how many resources are left in a chunk, so understandably this will have a big effect on the whole game. One quite important goal with rtsim is that we don’t want there to be too much of a difference, for simulated things, whether a chunk is loaded or not. This also means we don’t want different kinds of resources to be created from nothing when a chunk is reloaded, this also has the effect of making grinding not viable. There are more things we want to keep track of here though. We want to keep track of wildlife populations, of NPCs inventories while unloaded (maybe at a lower resolution). We also want to make NPCs actually work, some examples might include hunters affecting the wildlife population, or herbalists affecting resource counts in chunks when they pick things up. For more information, feel free to contact us on the Veloren Discord. 



* **Dungeons:**

Dungeons are currently under rework, with the Gnarling Fortress and the Adlet Caves being the first two dungeons to be reworked. The future dungeons rework/addition include Sahagin Dungeon, Haniwa Tombs, Myrmidons Dungeon, Cultist Dungeon, Dwarven Mine, Vampire Dungeon, etc.

The objective is to make the dungeons more unique in how they look, how they play, and how the player interacts with them. We want dungeons to feel more tied to the world of Veloren, where there is interaction between the dungeon inhabitants and the world. For that, we aim at answering the following questions: Why is this dungeon here, what is its importance in the region, what are their motivations, and what will happen if they are defeated? (etc.) Therefore, we want those dungeons to feel “organic”, that’s to say they are an actual part of the world, and they interact with it. For that, the dungeons will not have instances, as this is incompatible with the “organic” part of it. The organic element of it also means that when a dungeon is cleared, we want to have the possibility that another group can settle in that particular dungeon. The tricky part is to find a balance between the availability of said dungeon and avoiding having grindy dungeons.

Additionally, in regards to content and balancing around dungeons we would like dungeons to be a more niche aspect of combat which requires a group of individuals to complete. This, of course, means that there will be both content designed for solo players and grouped players so as to not trivialize the completion of said content. For those playing single-player or those that find it difficult to form groups with other individuals, we offer the opportunity to team up with NPCs either by gaining favor or purchasing them for wares (See NPC Companions part of the roadmap).

For more information, feel free to refer to the following chapters of the roadmap: Horizontal Progression, Quests, NPCs Companions, and Instances. You can also contact us on the Veloren Discord. 



* **Skill Trees**

For now, Sword and Axe have received a Skill Tree rework (Note that it is not definitive, there will be modifications later to balance all weapons). Hammer, Bow, Staff, Sceptre, and General skill trees will also receive a rework. However, the discussions for those have either not begun, or are still in the very early stages. Therefore it is currently not possible to give more information about those without creating unstable expectations. For more information, feel free to contact us on the Veloren Discord. 



* **Respawn**

Respawns will receive a rework, to propose a more interesting and meaningful part of gameplay. However, there are no concrete plans yet, only a few areas around the mechanic that are being discussed on Discord. First, we might replace campfires with shrines/magic stones to give another use to campfires (cooking for example). Then, with the dungeon reworks (See Dungeon part of the Roadmap), respawn points might also be removed from dungeon entrances. Finally, we want to make the respawn points interactive, meaning that you would have to purposely select it as your spawn point (by pressing E). For more information, feel free to contact us on the Veloren Discord. 



* **Combat animations**

One feedback we receive a lot is about the animations in Veloren, more precisely the combat animations. They will most likely be reworked one day, but as things stand, the persons working on animations are not 3D animators per se. Therefore, most animations can be considered as placeholder for now, until someone gets to rework them. One important thing to note is that we do animations through code (**Sam/Slipped explains**). The downside is that many animators are only used to working with 3D rigging. For more information, feel free to contact us on the Veloren Discord. 

**Planned Features:**



* **Quests**

Quests are one of the main features we want that is still missing from the game. The reason for that is that we don’t want traditional quests that reset and have no direct ties to the events of the world. As you may have seen in the world sim section, we want quests to be generated with that system (RT Sim2), where quests are generated based on an actual need in the world. For that, we need to procedurally generate the quest objective based on a set of variables. As an example, let’s say a region has been attacked by wolves and the sheep and farm have been damaged. The local population would want someone to deal with that, but they would also need enough money to pay the hunter. This simple example can be developed for all kinds of quests, from a microenvironment to a macroenvironment, thus leading to complex quest lines and many opportunities to complete those quests. As you may suspect, this takes a lot of time, as other systems need to be developed beforehand. There will be a first iteration for quests, where we set up the structure and develop an MVP. For more information, feel free to contact us on the Veloren Discord. 



* **Tutorial**

Rest assured, a better tutorial is planned. However, there are many reasons why the current tutorial is lacking. First, it was developed a while ago, when the game loop was different from the current one, meaning that it may be wrong in some aspects. It does give valuable information, but could vastly be improved. That being said, it would be a lot of work for very little to rework the tutorial now. Indeed, as we are in the pre-alpha stages, the game is evolving very fast, and from one week to another, a completely new feature can be introduced. Therefore, it is better for us to wait until we have developed the core of the gameplay to our liking before building a new tutorial. For more information, feel free to contact us on the Veloren Discord. 



* **Horizontal Progression**

We plan on moving away from vertical progression and focusing more on its horizontal counterpart when designing player-based progression. The charm of a horizontal system is that it allows for every encounter to carry some weight of danger even when returning to, what would be described as, earlier areas of content. That is not to say that the player will never get stronger as it is important to have some degree of verticality to help work the players through earlier stages of the game whilst learning game mechanics and other fundamental systems that will set up for a large portion of the game that is horizontal. To expand on this, Veloren will see three tiers of verticality and two tiers of horizontalness when viewing gear. These tiers are described as T1, T2, T3A, and T3B, with the latter two being horizontal variants of one another in which the B variant acts as a more niche version of the A while still being just as strong and viable to use.

Although there is a degree of verticality, as mentioned before, a large portion of the game focuses on aspects in which verticality is trivial. Instead, we encourage and would like to see a player’s ability to deal with difficult situations by having a large amount of game understanding and experience in dealing with said challenge under their belt. Additionally, we would like to encourage group plays for more treacherous entities found in the overworld, with only the most experienced being able to solo group-oriented content with a great deal of content and resources (See NPC Companions part of the roadmap).

For more information, feel free to contact us on the Veloren Discord. 



* **New Weapons**

Shields, Daggers, Spears/Polearms, Crossbows, and more magical weapons (grimoires, elemental gauntlets, etc.) are all planned. They will be worked on when the current weapons have all received their rework. Guns are up for discussion (Think pirate guns rather than modern guns). Some other questions include the addition of throwing weapons, and having ammunition for ranged weapons. For more information, feel free to contact us on the Veloren Discord. 



* **Recipes**

We plan to have recipes in the game to expand crafting gameplay. As of right now, all crafts are unlocked at the start, which lessens the sense of exploration and progression. Having recipes will add a deeper layer to the crafting system by tying it to other mechanics, such as quests for example. The development of this feature is in its early stages, so a lot of details and implementation plans still need to be discussed. For more information, feel free to contact us on the Veloren Discord. 



* **Jobs / Professions**

Veloren will have jobs and professions with a wide variety. So far, we have only planned the mechanic, but we have no concrete plan of execution for it. Some of the jobs would include Alchemy, Cooking, Smithing, Hunting, Mining, Wood Cutting, Trading, etc. For more information, feel free to contact us on the Veloren Discord. 



* **NPC Companions**

One of the fundamental premises of Veloren is that players are no different from the inhabitants of the world. This means that humanoid NPCs should be continuously interacting with the world in a similar fashion to players in an attempt to breathe life into the game. As players are capable of teaming up with one another we wish to see adventuring NPCs form parties with one another and players. This can be done by either gaining the favor of an adventurer NPC or hiring them for wares.  

Why is this wanted?

Aside from the aforementioned pros it provides for the world it also is an incredibly important premise for the sake of combat-related balance. A large portion of entities will be created under the assumption that it will take a group of humanoids to slay the beast. This allows individuals playing on single-player to experience the same kind of content as those in multiplayer, in addition to individuals playing on multiplayer that find it difficult to form a party with others and/or prefer playing by themselves.

For more information, feel free to contact us on the Veloren Discord. 



* **Storage / Banking**

Banking is a desired feature within the future of the game. We would like to see major banks have some sort of bank that allows them to store non-perishable items in them for a cost. These items can be removed at other banks in other cities as long as they have the corresponding resources to do so. An example of this would be If the player were to submit X-troll hide in town A’s bank and were to then travel to town B, they may not be able to withdraw troll hide if the town has a lack of trolls in their vicinity, and subsequently lack the material in their bank stock.

Such a system is desired as it provides content, coherence in the world of Veloren, and roleplaying opportunities. In Veloren we would like to provide a variety of choices for how one interacts with the world. This can range from roleplaying as a noble adventurer to partying with a band of crooked thugs intent on robbing the town’s local bank.

For more information, feel free to contact us on the Veloren Discord. 



* **Housing**

We definitely want a way for players to have a more settled presence in the world of Veloren. Therefore, housing is planned to be a mechanic, but there is currently no concrete plan of execution because it relies on core systems that are not complete yet. Some of the questions we currently have are:



1. How can we make it persist with map changes? 
2. How to tie it to our rtsim2 system?
3. How do we set up the real estate market?

For more information, feel free to contact us on the Veloren Discord. 



* **Server Federation**

Eventually, we’d like to have a ‘federation’ system for Veloren servers, which would allow trusted servers to enable character transfer (and perhaps other aspects of economy sharing & communication) between one another. Note that, in general, there is no good way to authenticate the world or player data generated by third-party servers, so all servers in a federation must trust one another to act in a legitimate manner. Note that this is a long-term feature with no specific implementation plan or timeline, so is unlikely to happen soon. For more information, feel free to contact us on the Veloren Discord. 



* **Reputation system (RTSim)**

Our goal is to have a reputation system using RTSim in which the actions of the players are remembered by NPCs and can affect the world around them. This system is currently in its early stages, where NPCs will remember and attack you if you have killed an NPC in the past hour and have been sighted. We plan to extend the system to create more scenarios that reinforce the coherence of the world. For example, reputation could allow a player access to a faction restricted areas, or give them the possibility to interact in a particular quest because of their past actions. This would greatly reinforce the roleplay elements in the game as every action would have potential consequences. For more information, feel free to contact us on the Veloren Discord. 



* **World Map**

We definitely plan to have a bigger map, with bigger biomes, and more biome types. However, there are two main reasons why we are currently not doing it. First, some of the worldgen tools and systems are not developed or optimized, which would currently damage the quality of the landscape and the performance. Such improvements take a lot of time and research. Secondly, gameplay-wise, Veloren is not ready to be much bigger in scale map-wise: we need to have more connections between regions, more activities in the overworld, better means of travel, and overall more reasons to travel.

We plan to expand the map to 262x262 km^2 and to have oceans and continents rather than only one big landmass. Some of the additional biomes include oceans, badlands, plains, swamps, more types of forests such as bamboo, more magical/fantasy biomes, etc.

For more information, feel free to contact us on the Veloren Discord. 



* **Factions / Kingdoms / Wars **

Thanks to rtsim2, we want to have organic factions/kingdoms that will be able to take part in power struggles between each other and within themselves. Therefore, the diplomatic map will evolve with time because of the actions of the actors of Veloren. Note that this is a very long-term planned mechanic and that core mechanics will need to be developed and expanded before such a feature makes its appearance in the game. For more information, feel free to contact us on the Veloren Discord. 



* **Mods & Plugins**

We definitely want mods and plugins in the game. Some of the decisions we make may not be to the liking of everyone, that’s why we think it’s important that everyone can freely and easily modify the game on their side. The open-source aspect of the projects will enhance the modding potential of the game. The #learning channel in our discord is also open for anyone who has questions regarding coding or any aspect of the game or programs we can help with. 

Some ideas for plugins are that they enable (in ascending complexity): 



1. adding new models (armor), graphics, ron based stats to the game 
2. adding new animations, weapon skills, NPCs, structures (ships) 
3. logic behavior for sprite interaction (far future) I would like plugins to get downloaded from the server on the connection (but locally cached to cut down initial bandwidth). 

Our devs working on plugins would also like to use wasm component model technology (WASI preview2) to enable plugins in Rust, C/++, python, javascript, and perhaps more languages. This will enable servers to differentiate even more with different game content.

For more information, feel free to contact us on the Veloren Discord. 

**Discussed Features:**



* **Inventory rework**

The current inventory system is heavily affected by the introduction of new items, as it is slots based. It favors having stacks of items while limiting the diversity of materials. There are talks of switching to a weight-based system, which would remove the item introduction constraint, and allow for a deeper/more meaningful inventory management. However, no set conclusion has been reached yet so a lot of the details are still to be discussed. For more information, feel free to contact us on the Veloren Discord. 



* **Building**

The majority of core developers, if not all, do want some kind of building system. Therefore, it is safe to assume that a building system could see the light of day. However, there are a lot of questions surrounding such a mechanic, as it is first and foremost an RPG. First, free building will not be a thing (See Free Building part of the roadmap). However, this is the only thing that is certain for the official version of the game regarding the building. Some of the questions we have regarding building include terrain persistence between maps, accessibility of the mechanic, ties to the world, level of freedom, and more. Note that this is a long-term feature. For more information, feel free to contact us on the Veloren Discord. 



* **Fog of War / Better Map gameplay**

Currently, the map shows every dungeon and region on the map. We don’t intend to keep it that way as it damages exploration and discovery quite heavily. Fog of War is more than likely planned, but the details regarding its implementation have not been discussed yet. Some of the questions we have concern the gameplay loop around map discovery, that’s to say we need to discuss the various ways the player will be able to discover the map and mark the different sites. For more information, feel free to contact us on the Veloren Discord. 

**Non-Planned Features:**



* **Instances**

Instances are not compatible with a lot of core systems we have planned. Because we want to have organic dungeons (see the dungeon part of the roadmap), we can’t have instances on top of that, as it would affect the world coherence and the synergies of the core systems. Moreover, we believe that different actors should be able to impact the evolution and development of a dungeon. To conclude, instances can work in a traditional raid dungeon system, but this is not what we have planned for dungeons. For more information, feel free to contact us on the Veloren Discord. 



* **Teleportation**

Fast travel is a mechanic we do not want to see in Veloren as it trivializes a lot of planned systems such as the world’s economics. Teleportation implies the ability to instantaneously bring certain rare materials from one end of the world to another. For an economic system that relies on the notion of scarcity of supply depending on the environment, and thereby the subsequent increase in cost, this mechanic would oppose it in its entirety. Although fast travel is not desired, we would like to see fast_er_ travel such as airships, trains, sea-fairing ships, and a variety of mounts to still allow for both world coherence and to encourage the exploration of the wonderful world of Veloren which will be peppered in a large array of points of interests. For more information, feel free to contact us on the Veloren Discord. 



* **Free building**

Free building in a way similar to Minecraft isn’t something that is compatible with the style of game Veloren aims to be. First, we have a finite map, so the map would quickly be filled with a huge population. Then, we want to keep the coherence of the world, both aesthetically and gameplay-wise, that’s to say we want to conserve the art direction and quality, while also preventing profanity through free building. Then, we need to tie those buildings to civilization and our rtsim2 feature, which is most likely incompatible with such a mechanic as free building. It’s worth mentioning that the game is first and foremost a RPG, not a survival/sandbox building game like Minecraft is. For the world to be coherent and the RPG elements to stay at the core, we can’t really allow free building in the main game mode. (By main game mode we mean that people are free to create other game modes where free building could work. Think of creative/god mods in other games as potential game modes. For more information, feel free to contact us on the Veloren Discord. 



* **Singleplayer characters in Multiplayer**

Because everyone is an admin in single-player, we can not allow single-player characters to transfer to the official MP server, as it could quickly destroy the economy and the balance of the game. There are plans to have a server hierarchy, where you can go to a server “below” the one you are currently on in terms of “server trust”, but cannot go up. This would allow players to keep their characters in single-player no matter the fate of a server. However, such a feature takes a lot of time and isn’t planned for the short term. You can also check the Server Federation explanation for more details. For more information, feel free to contact us on the Veloren Discord. 



* **Vanity Slots / Transmog:**

We do not want a vanity system as we would like the player/NPC to be able to tell how strong an entity is based on visible equipment. We also don't want it simply for roleplaying purposes. If a player wants to look a certain way for roleplay, they should also bear the consequences of that decision. On another note, if players really want to change their look, they can do so on their side by replacing the .vox files of the item in question. That way, it will only be visible to them and it won’t impact the experience of other players. For more information, feel free to contact us on the Veloren Discord. 

