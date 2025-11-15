Normal Drops Configuration
========================

Configuration Format:
-------------------
Block drops use JSON format with these properties:

Basic Properties:
- blockId: The Minecraft block ID (e.g., "minecraft:stone") - only for block-specific drops
- itemId: The item to drop (e.g., "minecraft:diamond")
- dropChance: Percentage chance to drop (0-100)
- minAmount: Minimum amount to drop
- maxAmount: Maximum amount to drop
- requirePlayerBreak: If true, only drops when broken by a player
- allowDefaultDrops: If true, keeps vanilla drops
- replaceDefaultDrops: If true, replaces vanilla drops with custom ones

Tool Requirements:
- requiredTool: Specific tool required (e.g., "minecraft:diamond_pickaxe")
- requiredEnchantment: Required enchantment (e.g., "minecraft:fortune")
- requiredEnchantLevel: Required enchantment level

Dimension Requirements:
- requiredDimension: Dimension where drops work (e.g., "minecraft:overworld", "minecraft:the_nether", "minecraft:the_end")
  Leave empty ("") for any dimension

Advanced Features:
- nbtData: Custom NBT data for the dropped item (JSON format)
- dropCommand: Command to execute when item drops
- dropCommandChance: Percentage chance to execute drop command (0-100)
- breakCommand: Command to execute when block breaks
- breakCommandChance: Percentage chance to execute break command (0-100)
- allowModIDs: List of mod IDs allowed to drop items when allowDefaultDrops is false
- comment: Optional comment for documentation

Block Regeneration:
- canRegenerate: If true, block will regenerate after breaking
- brokenBlockReplace: Block to replace when broken (e.g., "minecraft:bedrock")
- respawnTime: Time in seconds before block regenerates

UNDERSTANDING 'GLOBAL' FILES:
============================
Files with 'Global' in the name (like Global_Block_Drops.json) apply to ALL blocks
of that type, unless you have a more specific configuration.

For example:
- Global_Block_Drops.json: Affects ALL blocks when broken
- Block Types/stone.json: Only affects stone blocks specifically
- Block Types/diamond_ore.json: Only affects diamond ore blocks

If you have both a global file and a specific block file, the specific
block file takes priority for that block type.

COMPLETE EXAMPLE WITH ALL FEATURES:
=================================
Here's an example showing ALL available properties:

```json
[
  {
    "blockId": "minecraft:stone",
    "itemId": "minecraft:diamond",
    "dropChance": 10.0,
    "minAmount": 1,
    "maxAmount": 3,
    "requirePlayerBreak": true,
    "allowDefaultDrops": false,
    "replaceDefaultDrops": true,
    "requiredTool": "minecraft:diamond_pickaxe",
    "requiredEnchantment": "minecraft:fortune",
    "requiredEnchantLevel": 2,
    "requiredDimension": "minecraft:overworld",
    "nbtData": "{display:{Name:'{\"text\":\"Magical Diamond\",\"color\":\"aqua\",\"italic\":false}',Lore:['{\"text\":\"Found deep in stone\",\"color\":\"gray\",\"italic\":false}']},Enchantments:[{id:\"minecraft:unbreaking\",lvl:3}]}",
    "dropCommand": "say %player% found a magical diamond at {x} {y} {z}!",
    "dropCommandChance": 50.0,
    "breakCommand": "particle minecraft:heart ~ ~ ~ 1 1 1 0.1 20",
    "breakCommandChance": 100.0,
    "canRegenerate": true,
    "brokenBlockReplace": "minecraft:bedrock",
    "respawnTime": 60,
    "allowModIDs": ["minecraft", "forge"],
    "comment": "Rare diamond drop from stone in overworld only, requires Fortune II+ diamond pickaxe, regenerates after 60 seconds"
  }
]
```

Command Placeholders:
-------------------
You can use these placeholders in commands:
- %player% - Player's name
- {x} - Block's X coordinate
- {y} - Block's Y coordinate
- {z} - Block's Z coordinate

Common Dimension IDs:
-------------------
- minecraft:overworld - The main world
- minecraft:the_nether - The Nether
- minecraft:the_end - The End
- Leave empty ("") for any dimension

HOW TO DISABLE DROPS WITHOUT DELETING FILES:
==========================================
You can disable all drops in a file without deleting it using these methods:

Method 1 - Empty Array:
Replace the entire content with: []

Method 2 - Set Drop Chance to 0:
Set "dropChance": 0 for all drops you want to disable

Example of Disabled File:
```json
[]
```

Example of Disabled Drop (keeping file structure):
```json
[
  {
    "blockId": "minecraft:stone",
    "itemId": "minecraft:diamond",
    "dropChance": 0,
    "dropCommandChance": 0,
    "breakCommandChance": 0,
    "minAmount": 1,
    "maxAmount": 1
  }
]
```
(This disables the diamond drop AND all command executions)

