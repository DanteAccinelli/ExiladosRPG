# Exilados RPG Roadmap

---

## Phase 1 - Core Systems

### Project Setup
  Create repository  
  Configure Git  
  Define folder structure  
  Organize namespaces (Core, Characters, Combat, Dungeon, Items, Systems, UI)

### Game Loop
  Create GameManager  
  Implement main game loop  
  Handle player input  
  Handle game state transitions  
  Implement start and exit conditions  

### Game State Management
  Create GameState enum  
  Implement StateManager  
  Define states (MainMenu, Playing, Combat, Inventory, Dialogue, GameOver)  
  Implement state transitions  

### Input System
  Create InputHandler class  
  Map player commands  
  Validate player input  
  Handle invalid commands  

### Character Classes
  Create base Character class  
  Implement Player class  
  Implement Enemy class  
  Define base attributes (HP, Attack, Defense, Level)  
  Implement core methods (Attack, TakeDamage, Heal, IsAlive)

### Basic Combat
  Create CombatSystem  
  Implement turn-based combat  
  Implement damage calculation  
  Implement player attack  
  Implement enemy attack  
  Implement victory and defeat conditions  

### Status Effects
  Create StatusEffect class  
  Implement poison effect  
  Implement burn effect  
  Implement stun effect  
  Implement buff and debuff durations  

### Simple Dungeon Navigation
  Create Dungeon class  
  Create Room class  
  Implement player movement between rooms  
  Implement room descriptions  
  Implement navigation commands (north, south, east, west)

### Enemy Encounters
  Spawn enemies inside rooms  
  Trigger combat when entering enemy rooms  
  Handle enemy defeat  
  Implement basic loot drops  

### Debug System
  Create Logger system  
  Print system messages  
  Log combat calculations  
  Log dungeon generation  

---

## Phase 2 - RPG Systems

### Inventory
  Create Inventory class  
  Implement add item  
  Implement remove item  
  Implement view inventory  
  Implement item usage  

### Items and Equipment
  Create Item base class  
  Create Weapon class  
  Create Armor class  
  Create Potion class  
  Create Relic class  
  Implement item attributes (name, description, value)

### Equipment System
  Create EquipmentManager  
  Implement equipment slots (weapon, armor, accessory)  
  Implement equip and unequip actions  
  Apply equipment stat bonuses  

### Leveling System
  Implement experience points  
  Implement level progression  
  Implement stat growth  
  Implement LevelUp method  
  Implement GainExperience method  

### Abilities
  Create Ability class  
  Implement ability unlocking  
  Store abilities on player  
  Implement ability activation  
  Implement ability effects  

### Loot System
  Create LootTable system  
  Implement drop chances  
  Generate random items  
  Implement rarity tiers (Common, Uncommon, Rare, Epic, Legendary)

### Economy System
  Implement gold currency  
  Implement item buying  
  Implement item selling  
  Generate shop inventory  

### Save / Load System
  Implement save game files  
  Save player stats  
  Save inventory data  
  Save dungeon progress  
  Implement load game  
  Implement autosave system  

### Data Management
  Store enemies in JSON files  
  Store items in JSON files  
  Load data at runtime  
  Separate game data from code  

---

## Phase 3 - World Systems

### Procedural Dungeon Generator
  Create DungeonGenerator class  
  Generate dungeon layout  
  Connect rooms  
  Generate dungeon floors  
  Implement difficulty scaling by floor  

### Room Types
  Create EnemyRoom  
  Create TreasureRoom  
  Create EventRoom  
  Create ShopRoom  
  Create BossRoom  
  Implement room-specific behaviors  

### Random Events
  Create EventSystem  
  Implement random event selection  
  Implement event triggers  
  Implement event outcomes  
  Implement player decision options  

### Boss System
  Create Boss base class  
  Implement boss abilities  
  Implement boss phases  
  Implement boss loot rewards  

### Run System
  Implement start new run  
  Reset dungeon on run start  
  Generate new dungeon layout  
  Track run progress  

---

## Phase 4 - Advanced Features

### Relic System
  Implement relic discovery  
  Implement passive modifiers  
  Implement relic stacking  
  Implement relic effects during gameplay  

### Faction Reputation
  Define world factions  
  Implement reputation values  
  Implement reputation changes from decisions  
  Implement faction-based events  

### Branching Story Events
  Implement dialogue system  
  Track player decisions  
  Implement branching outcomes  
  Implement story flags and consequences  

### Difficulty Scaling
  Scale enemy stats by dungeon depth  
  Implement elite enemies  
  Implement boss mechanics  

---

## Phase 5 - Game Systems Polish

### Balancing
  Adjust enemy stats  
  Adjust XP progression curves  
  Adjust item scaling and rarity balance  

### Performance
  Optimize dungeon generation  
  Optimize combat calculations  
  Reduce unnecessary memory usage  

### Code Refactoring
  Improve class architecture  
  Remove duplicated code  
  Improve maintainability  

### Debugging
  Expand debug logs  
  Test edge cases  
  Fix gameplay bugs  

---

## Phase 6 - Unity Migration

### Convert Console Systems to Unity
  Port core systems (characters, combat, dungeon)  
  Adapt systems to Unity architecture  
  Separate game logic from UI  

### Implement Graphics and Animation
  Create player sprites  
  Create enemy sprites  
  Create dungeon tiles  
  Implement character animations  

### Replace Text UI with Gameplay Scenes
  Implement player movement  
  Implement camera system  
  Implement scene management  
  Implement graphical UI (health, inventory, abilities)

---
