\---



# **Exilados RPG Roadmap**



\---



### **Phase 1 - Core Engine**



##### 1.1 Game Loop \& State

&#x20; - GameManager

&#x20; - StateManager

&#x20; - GameState Enum

&#x20; - GameContext

&#x20; - RandomService



##### 1.2 Commands \& Input

&#x20; - ICommand

&#x20; - CommandParser

&#x20; - CommandHelpSystem

&#x20; - IInput \& ConsoleInput 

&#x20; - //More Input types

&#x20; - InputHandler



##### 1.3 Logging

&#x20; - ILogger

&#x20; - Logger



\---



### **Phase 2 - Characters Core**



##### 2.1 Stats \& Effects Base

&#x20; - Stats

&#x20; - StatusEffectContainer

&#x20; - IStatusEffect (simple placeholder implementation)

&#x20; - PoisonEffect  

&#x20; - //More Effect types



##### 2.2 Character Hierarchy

&#x20; - IDamageable

&#x20; - IAttacker

&#x20; - IHealeable

&#x20; - Character

&#x20; - Player

&#x20; - Enemy

&#x20; - MeleeEnemy 

&#x20; - //More Enemy types



##### 2.3 AI Behaviors

&#x20; - IAIBehavior

&#x20; - AgressiveBehavior  

&#x20; - //More Behavior types



\---



### **Phase 3 - Combat System**



##### 3.1 Core Combat System

&#x20; - CombatSystem

&#x20; - TurnOrderManager



##### 3.2 Combat Actions

&#x20; - ICombatAction

&#x20; - AttackAction

&#x20; - AbilityAction

&#x20; - UseItemAction 

&#x20; - //More Action types



##### 3.3 Damage \& Effects

&#x20; - DamageFormula

&#x20; - StatusEffectProcessor



\---



### **Phase 4 - Items \& Inventory**



##### 4.1 Item Core

&#x20; - IUsable

&#x20; - IEquipable 

&#x20; - Item

&#x20; - Weapon

&#x20; - Armor

&#x20; - Potion

&#x20; - Relic



##### 4.2 Item Effects

&#x20; - ItemEffectContainer

&#x20; - IItemEffect



##### 4.3 Inventory \& Equipment

&#x20; - Inventory

&#x20; - InventoryController

&#x20; - EquipmentManager



##### 4.4 Loot \& Item Generation

&#x20; - LootTable

&#x20; - ItemGenerator

&#x20; - IItemGenerationModifier



\---



### **Phase 5 - Dungeons \& Rooms**



##### 5.1 Dungeon Structure

&#x20; - Dungeon

&#x20; - RoomGraph

&#x20; - RoomNode

&#x20; - RoomNavigation

&#x20; - DungeonGenerator



##### 5.2 Rooms \& Traps

&#x20; - IRoom

&#x20; - TreasureRoom 

&#x20; - //More Room types

&#x20; - ITrap

&#x20; - SpikeTrap 

&#x20; - //More Trap types



##### 5.3 Room Contents

&#x20; - IRoomContent

&#x20; - EnemyGroup

&#x20; - LootContainer

&#x20; - TrapComponent

&#x20; - RoomEvent 

&#x20; - //More Room Content types



##### 5.4 Map

&#x20; - MapSystem



\---



### **Phase 6 - Abilities, Skills, Requirements**



##### 6.1 Abilities

&#x20; - IAbility

&#x20; - Ability 

&#x20; - //More Ability types



##### 6.2 Skill Tree

&#x20; - SkillTree

&#x20; - SkillNode



##### 6.3 Requirements

&#x20; - IRequirement

&#x20; - RequirementGroup

&#x20; - LevelRequirement

&#x20; - GoldRequirement

&#x20; - SkillRequirement

&#x20; - FactionRequirement

&#x20; - //More Requirement Types



\---



### **Phase 7 - Economy, Shops, Meta Systems**



##### 7.1 Economy \& Shop

&#x20; - EconomySystem

&#x20; - EconomyController

&#x20; - Shop



##### 7.2 Meta Systems

&#x20; - FactionSystem

&#x20; - AchievementSystem

&#x20; - MetaProgressionSystem

&#x20; - MetricsSystem



\---



### **Phase 8 - Event FrameWork \& Dialogue**



##### 8.1 Event System

&#x20; - IGameEvent

&#x20; - TreasureEvent

&#x20; - // MoreEvents

&#x20; - EventSystem



##### 8.2 Dialogue System

&#x20; - DialogueSystem



\---



### **Phase 9 - Save, Load, Profiles**



##### 9.1 Saving

&#x20; - ISaveable

&#x20; - SaveSystem



##### 9.2 Profiles

&#x20; - ProfileManager

&#x20; - IDataLoader

&#x20; - DataManager



\---



### **Phase 10 - UI Integration**



##### 10.1 Core UI

&#x20; - UIController

&#x20; - IRenderer

&#x20; - ConsoleRenderer



##### 10.2 Menu UI

&#x20; - UIMenuModel

&#x20; - IMenuUI



##### 10.3 Inventory UI

&#x20; - UIInventoryModel

&#x20; - UIItemEntry

&#x20; - UIItemDetailsModel

&#x20; - IInventoryUI



##### 10.4 Combat UI

&#x20; - UICombatStateModel

&#x20; - ICombatUI



##### 10.5 Dialogue UI

&#x20; - UIDialogueModel

&#x20; - IDialogueUI



\---



### Phase 11 - Final Polish \& Extra Content

&#x20; - Add player classes

&#x20; - Add more abilities

&#x20; - Add more enemy types

&#x20; - Add more traps

&#x20; - Add more events

&#x20; - Add more item and status effects

&#x20; - Add factions, endings, lore

&#x20; - Add new room types

&#x20; - Add more weapon/armor categories

