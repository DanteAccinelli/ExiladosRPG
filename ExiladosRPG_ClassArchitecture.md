\---



# **# Exilados RPG Class Architecture**



\---



### **1. Core**

*(Game loop, input logging, commands, global state)*



##### 1.1 Game Loop / State



\### GameManager

&#x20; - StateManager StateManager, InputHandler InputHandler, bool IsRunning

&#x20; - StartGame(), Update(), ExitGame(), InitializeSystem(), GameLoop()



\### StateManager

&#x20; - GameState CurrentState

&#x20; - ChangeState(GameState new State), GetCurrentState(), UpdateState()



\### GameState

&#x20; - GameState(enum) -> MainMenu, Playing, Combat, Inventory, Dialogue, GameOver



\### RandomService

&#x20; - RandomService(), int Next(), float NextFloat(), RollChance(), Pick<Random>()



##### 1.2 Commands \& Input



\### ICommand

&#x20; - string Name, string Description

&#x20; - Execute()



\### CommandParser

&#x20; - Parse(string input), ExecuteCommand(string input), RegisterCommand(string key, ICommand command)



\### CommandHelpSystem : ICommand

&#x20; - string Name, string Description, CommandParser parser

&#x20; - Execute(), ShowAllCommands()



\### IInput

&#x20; - ReadLine(), ReadInt()



\### ConsoleInput : IInput

&#x20; - ReadLine(), ReadInt()



//More Input types



\### InputHandler

&#x20; - IInput Input, CommandParser parser, StateManager StateManager

&#x20; - HandleInput() 



##### 1.3 Logging



\### ILogger

&#x20; - LogInfo(string message), LogWarning(string message), LogError(string message)



\### Logger : ILogger

&#x20; - bool DebugMode

&#x20; - LogInfo(string message), LogWarning(string message), LogError(string message)



\---



### **2. Characters**

*(Stats, effects, player, enemies, AI)*



##### 2.1 Base Interfaces



\### IDamageable

&#x20; - TakeDamage(int amount), IsAlive()



\### IAttacker

&#x20; - Attack(IDamageable target)



\### IHealable

&#x20; - Heal(int amount)



##### 2.2 Stats \& Effects



\### Stats

&#x20; - int MaxHP, int HP, int Attack, int Defense, int Speed, int CritChance, int CritDamage



\### StatusEffectContainer

&#x20; - List<IStatusEffect> ActiveEffects

&#x20; - Add(IStatusEffect effect), Remove(IStatusEffect effect), UpdateTurnStart(Character c), UpdateTurnEnd(Character c)



\### IStatusEffect

&#x20; - String Name {get;} int Duration {get;} bool IsExpired{get;}

&#x20; - OnApply(Character target), OnTurnStart(Character target), OnTurnEnd(Character target), OnExpire(Character target)



\### PoisonEffect : IStatusEffect

&#x20; - string Name, int Duration, bool IsExpired, int DamagePerTurn

&#x20; - PoisonEffect(int damage, int duration)



//More Effect types



##### 2.3 Character Hierarchy



\### Character: IDamageable, IAttacker, IHealable

&#x20; - string Name, Stats BaseStats, Stats CurrentStats, StatusEffectContainer EffectManager, int Level

&#x20; - TakeDamage(int amount), Attack(IDamageable target), Heal(int amount), IsAlive()



\### Player : Character

&#x20; - Inventory Inventory, EquipmentManager EquipmentManager, List<IAbility> Abilities, SkillTree SkillTree, int Gold, int Experience

&#x20; - GainExperience(int amount), LevelUp(), UnlockAbility(IAbility ability), EquipItem(Item item), UnequipItem(Item item)



\### Enemy : Character

&#x20; - LootTable LootTable, IAIBehavior AI

&#x20; - ICombatAction DecideAction(GameContext context), DropLoot(), InitializeStats()



\### MeleeEnemy : Enemy



//More Enemy types



##### 2.4 AI Behaviors



\### IAIBehavior

&#x20; - DecideAction(Enemy enemy, GameContext context)



\### AgressiveBehavior : IAIBehavior

&#x20; - DecideAction(Enemy enemy, GameContext context)



//More Behavior types



\---



### **3. Combat System**

*(Actions, turn order, formulas, processors)*



##### 3.1 Core Combat



\### CombatSystem

&#x20; - Player player, List<Enemy> Enemies, bool IsCombatActive

&#x20; - StartCombat(Player player, List<Enemy> enemies), TurnOrderManager TurnOrder, ExecuteAction(ICombatAction action), EndCombat(), CheckVictory()



\### TurnOrderManager

&#x20; - List<Character> TurnOrder

&#x20; - Initialize(List<Character> actions), Character GetNextCharacter(), RefreshTurnOrder()



##### 3.2 Combat Actions



\### ICombatAction

&#x20; - Execute(GameContext context)



\### AttackAction : ICombatAction

&#x20; - Character Attacker, Character Defender

&#x20; - Execute(GameContext context)



\### UseItemAction : ICombatAction

&#x20; - Player User, Item Item

&#x20; - Execute(GameContext context)



\### AbilityAction : ICombatAction

&#x20; - Character User, IAbility Ability

&#x20; - Execute(GameContext context)



//More Action types



##### 3.3 Combat Calculations



\### DamageFormula

&#x20; - CalculateDamage(Character attacker, Character defender), bool RollCritical(Character attacker)



\### StatusEffectProcessor

&#x20; - ApplyDamageModifiers(int damage, Character attacker, Character defender), ApplyOnHitEffects(Character attacker, Character defender)



\---



### **4. Dungeons \& Rooms**

*(Graph structure, navigation, traps, room contents)*



##### 4.1 Dungeon Structure



\### Dungeon

&#x20; - RoomGraph Graph, RoomNode CurrentNode

&#x20; - Generate(), EnterRoom(RoomNode room)



\### RoomGraph

&#x20; - List<RoomNode> Nodes



\### RoomNode

&#x20; - IRoom Room, Dictionary<string, RoomNode> Connections



\### RoomNavigation

&#x20; - RoomNode GetAdjacent(RoomNode current, string direction), MoveTo(RoomNode next)



\### DungeonGenerator

&#x20; - int NumberOfRooms

&#x20; - GenerateRooms(), ConnectRooms(), AssignRoomTypes()



##### 4.2 Room Base



\### IRoom

&#x20; - int RoomID, List<IRoomContent> Contents, bool Visited



\### TreasureRoom : IRoom



//More Room types



##### 4.3 Room Contents



\### IRoomContent

&#x20; - OnEnter(GameContext context), OnExit(GameContext context)



\### EnemyGroup : IRoomContent

&#x20; - List<Enemy> Enemies

&#x20; - OnEnter(GameContext context)



\### LootContainer : IRoomContent

&#x20; - List<Item> Items

&#x20; - OnEnter(GameContext context)



\### TrapComponent : IRoomContent

&#x20; - ITrap Trap

&#x20; - OnEnter(GameContext context)



\### RoomEvent : IRoomContent

&#x20; - IGameEvent Event

&#x20; - OnEnter(GameContext context)



//More Room Content types



##### 4.4 Traps



\### ITrap

&#x20; - string Name, bool IsHidden

&#x20; - Trigger(GameContext context), Detect(GameContext context)



\### SpikeTrap : ITrap

&#x20; - string Name, bool IsHidden, int Damage

&#x20; - SpikeTrap(bool isHidden, int damage), void Trigger(GameContext context), void Detect(GameContext context)



//More Trap types



##### 4.5 Map



\### MapSystem

&#x20; - List<IRoom> VisitedRooms

&#x20; - RevealRoom(IRoom room), ShowMap()



\---



### **5. Items \& Equipment**

*(Items, effects, generation, loot)*



##### 5.1 Item Interfaces



\### IUsable

&#x20; - Use(Player player)



\### IEquipable

&#x20; - Equip(Player player), Unequip(Player player)





\### IItemEffect

&#x20; - OnEquip(Player player), OnUnequip(Player player), OnUse(Player player)



##### 5.2 Item Core



\### Item

&#x20; - string Name, string Description, int Value, enum Rarity (Common, Uncommon, Rare, Epic, Legendary), ItemEffectContainer Effects



\### Weapon : Item, IEquipable

&#x20; - int DamageBonus, float AttackSpeed

&#x20; - Equip(Player player), Unequip(Player player)



\### Armor : Item, IEquipable

&#x20; - int DefenseBonus

&#x20; - Equip(Player player), Unequip(Player player)



\### Potion : Item, IUsable

&#x20; - int HealAmount, ItemEffectContainer Effects

&#x20; - Use(Player player)



\### Relic : Item

&#x20; - ItemEffectContainer Effects



##### 5.3 Item Effects



\### ItemEffectContainer

&#x20; - List<IItemEffect> Effects

&#x20; - AddEffect(IItemEffect effect), ApplyEquip(Player player), ApplyUnequip(Player player), ApplyUse(Player player)



##### 5.4 Loot \& Generation



\### LootTable

&#x20; - List<Item> PossibleLoot

&#x20; - RollLoot()



\### ItemGenerator

&#x20; - GenerateItem(), ApplyGenerationModifiers(Item item)



\### IItemGenerationModifier

&#x20; - ApplyTo(Item item)



\---



### **6. Character Systems**

*(Inventory, abilities, skill tree, equipment)*



##### 6.1 Inventory



\### Inventory

&#x20; - List<Item> Items

&#x20; - AddItem(Item item), RemoveItem(Item item), GetItems()



\### InventoryController

&#x20; - Inventory Inventory

&#x20; - UseItem(Item item, Player player), ListItems(), CanUse(Item item, Player player)



##### 6.2 Equipment



\### EquipmentManager

&#x20; - Item Weapon, Item Armor, Item Acessory

&#x20; - EquipItem(Item item), UnequipItem(Item item), GetEquippedStats()



##### 6.3 Abilities



\### IAbility

&#x20; - string Name

&#x20; - Activate(Player player)



\### Ability : IAbility

&#x20; - string Name, int Cooldown, IRequirement UseRequirement

&#x20; - Activate(Player player), ApplyEffect()



//More Ability types



##### 6.4 Skills



\### SkillTree

&#x20; - List<SkillNode> Nodes

&#x20; - UnlockSkill(SkillNode node), GetAvailableSkills()



\### SkillNode

&#x20; - string Name, bool IsUnlocked, IRequirement UnlockRequirement



\---



### **7. Economy \& Shops**

*(Gold, transactions, price calculation)*



##### 7.1 Economy



\### EconomySystem

&#x20; - AddGold(int amount), SpendGold(int amount), CalculateBuyPrice(Item item), CalculateSellPrice(Item item)



\### EconomyController

&#x20; - EconomySystem Economy, bool CanBuy(Player player, Item item), bool CanSell(Player player, Item item), Buy(Player player, Item item, Shop shop), Sell(Player player, Item item, Shop shop), int GetFinalBuyPrice(Item item), GetFinalSellPrice(Item item)



### 7.2 Shop



\### Shop

&#x20; - List<Item> Inventory, EconomyController Economy



\---



### **8. Requirements System**

*(Conditions for abilities, items, skills)*



##### 8.1 Base



\### IRequirement

&#x20; - bool IsSatisfied(GameContext context), string FailureMessage



\### RequirementGroup

&#x20; - List<IRequirement> Requirements, bool RequireAll, bool IsSatisfied(GameContext context)



##### 8.2 Specific Requirements



\### LevelRequirement : IRequirement



\### GoldRequirement : IRequirement



\### SkillRequirement : IRequirement



\### FactionRequirement: IRequirement



//More Requirement types



\---



### **9. Save \& Profile**

*(Data serialization, profiles, loaders)*



##### 9.1 Saving



\### ISaveable

&#x20; - Serialize(), Deserialize(string data)



\### SaveSystem

&#x20; - SaveGame(), LoadGame(), AutoSave()



##### 9.2 Profile Management



\### ProfileManager

&#x20; - List<string> Profiles

&#x20; - CreateProfile(string name), LoadProfile(string name), DeleteProfile(string name)



##### 9.3 Data Loading



\### IDataLoader

&#x20; - Load()



\### DataManager : IDataLoader

&#x20; - LoadItems(), LoadEnemies(), LoadEvents(), Load()



\---



### **10. Events \& Meta Systems**

*(Game events, dialogue, faction, achievements)*



##### 10.1 Event Framework



\### IGameEvent

&#x20; - Execute(GameContext context)



\### TreasureEvent : IGameEvent

&#x20; - Execute(GameContext context)



//More Event types



\### EventSystem

&#x20; - RoomEntry(GameContext context, IRoom room), RunEvent(IGameEvent event), RunTrap(ITrap trap, GameContext context)



##### 10.2 Dialogue



\### DialogueSystem

&#x20; - StartDialogue(string text), PresentChoices(List<string> choices), ResolveChoice(int choice)



##### 10.3 Meta Systems



\### GameContext

&#x20; - Player Player, Dungeon Dungeon, EventSystem EventSystem, DialogueSystem Dialogue, CombatSystem Combat



\### FactionSystem

&#x20; - Dictionary<string, int> Reputation

&#x20; - ModifyReputation(string faction, int value), GetFactionStanding(string faction)



\### AchievementSystem

&#x20; - List<string> UnlockedAchievements

&#x20; - UnlockAchievement(string achievement), CheckConditions()



\### MetaProgressionSystem

&#x20; - List<Relic> UnlockedRelics

&#x20; - UnlockRelic(Relic relic), UnlockAbility(Ability ability)



\### MetricsSystem

&#x20; - int Deaths, int Kills, float RunTime

&#x20; - RecordDeath(), RecordKill(), RecordRunTime(float time)



\---



### **11. UI (Console Version)**

*(Renderer, menus, inventory, combat, dialogue)*



##### 11.1 Core UI



\### UIController

&#x20; - IRenderer Renderer, IMenuUI MenuUI, IInventoryUI InventoryUI, ICombatUI CombatUI, IDialogueUI DialogueUI

&#x20; - ShowMainMenu(), ShowInventory(Inventory inventory), ShowCombatState(Player player, Enemy enemy), ShowDialogue(String text, List<string> choices)



\### IRenderer

&#x20; - Print(string text), Clear()



\### ConsoleRenderer : IRenderer

&#x20; - Clear(), Print(string text)



##### 11.2 Menu UI



\### UIMenuModel

&#x20; - string Title, List<string> Options



\### IMenuUI

&#x20; - ShowMenu(UIMenuModel model), GetSelection()



##### 11.3 Inventory UI



\### UIInventoryModel

&#x20; - string Title, List<UIItemEntry> Items



\### UIItemEntry

&#x20; - string Name, string Description, string Rarity, int Value



\### UIItemDetailsModel

&#x20; - string Name, string Description, string Rarity, int Value, List<string> Effects



\### IInventoryUI

&#x20; - ShowInventory(UIInventoryModel model), SelectItem(), ShowItemDetails(UIItemDetailsModel model)



##### 11.4 Combat UI



\### UICombatStateModel

&#x20; - String PlayerName, int PlayerHP, int PlayerMaxHP, string EnemyName, int EnemyHP, int EnemyMaxHP, List<string> LogLines



\### ICombatUI

&#x20; - ShowCombatState(UICombatStateModel model), ShowCombatOptions(), ShowLog(string message)



##### 11.5 Dialogue UI



\### UIDialogueModel

&#x20; - string Text, List<string> Choices



\### IDialogueUI

&#x20; - ShowDialogue(UIDialogueModel model), GetPlayerChoice()



\---



