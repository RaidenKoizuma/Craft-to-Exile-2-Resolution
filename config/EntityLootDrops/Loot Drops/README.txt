Entity Loot Drops Configuration Guide
===================================

This directory contains all entity loot drop configurations.

FILE MANAGEMENT SYSTEM:
======================
ON FIRST LOAD: All example files and directories are created automatically.

AUTO-REGENERATING FILES:
- Global_Hostile_Drops.json: ALWAYS regenerates if deleted (contains your main config)

EXAMPLE FILES:
- Clean, simple examples for learning the basic format
- Safe to delete - will NOT regenerate automatically
- Can be renamed, edited, or replaced with custom files

COMPREHENSIVE REFERENCE:
- Global_Hostile_Drops.example: Complete reference with ALL possible fields
- Use as template for advanced configurations
- Safe to delete - will NOT regenerate automatically

REGENERATE EXAMPLES:
- Delete entire folders (like 'Loot Drops' or 'Mobs') to regenerate examples
- Individual example files will NOT regenerate
- Folder deletion triggers complete example recreation

Directory Structure:
-------------------
Loot Drops/
  ??? Normal Drops/           # Always active drops
  ?   ??? Global_Hostile_Drops.json        # Main config (AUTO-REGENERATES)
  ?   ??? Global_Hostile_Drops.example      # Comprehensive reference
  ?   ??? Mobs/               # Entity-specific drops
  ?       ??? Zombie_Example.json    # Basic examples (safe to delete)
  ?       ??? Skeleton_Example.json  # Basic examples (safe to delete)
  ?       ??? custom_folder/  # Nested folders supported!
  ?       ?   ??? your_drops.json
  ?       ??? organized/      # Any depth of nesting works
  ?           ??? subfolder/
  ?               ??? special_drops.json
  ??? Event Drops/            # Event-specific drops
      ??? Winter/             # Winter event drops
      ?   ??? Winter_Event_Drops_Example.json  # Basic examples
      ?   ??? Drop_Count.json # Drop counting data (auto-generated)
      ?   ??? Mobs/
      ??? Summer/             # Summer event drops
      ?   ??? Summer_Event_Drops_Example.json
      ?   ??? Drop_Count.json # Drop counting data (auto-generated)
      ?   ??? Mobs/
      ??? Easter/             # Easter event drops
      ?   ??? Easter_Event_Drops_Example.json
      ?   ??? Drop_Count.json # Drop counting data (auto-generated)
      ?   ??? Mobs/
      ??? Halloween/          # Halloween event drops
          ??? Halloween_Event_Drops_Example.json
          ??? Drop_Count.json # Drop counting data (auto-generated)
          ??? Mobs/

Configuration Format:
--------------------
All drop configurations use JSON format.

BASIC FORMAT (used in example files):
- itemId: Item to drop (e.g., "minecraft:diamond")
- dropChance: Percentage chance to drop (0-100)
- minAmount: Minimum amount to drop
- maxAmount: Maximum amount to drop
- requirePlayerKill: If true, only drops when killed by a player
- enableDropCount: If true, tracks drops for competitions/leaderboards

ADVANCED PROPERTIES (see Global_Hostile_Drops.example):
- nbtData: Custom NBT data for the item
- requiredAdvancement: Required advancement for drop
- requiredEffect: Required potion effect for drop
- requiredEquipment: Required equipment for drop
- requiredDimension: Required dimension for drop
- command: Command to execute on drop
- commandChance: Chance for command execution
- allowDefaultDrops: Allow default drops (requires "allowModIDs")
- allowModIDs: Allows drops from modids if allowDefaultDrops is false
- enableDropCount: Enable drop tracking for this item
- _comment: Documentation comment

DROP COUNTING SYSTEM:
====================
COMPETITIVE EVENT FEATURE: Track player drop statistics!

How Drop Counting Works:
- Add "enableDropCount": true to any drop configuration
- Only works for Event Drops (not Normal Drops)
- Creates Drop_Count.json in each event folder automatically
- Tracks individual player statistics per event
- Perfect for competitive events and leaderboards

Drop Count Commands:
- /lootdrops dropcount <true|false>: Enable/disable drop counting globally
- /lootdrops top [count]: Show top players across all events
- /lootdrops eventtop <event> [count]: Show top players for specific event
- /lootdrops playerstats <player>: Show detailed player statistics
- /lootdrops reset_counts: Reset all drop count data

Drop_Count.json Structure:
{
  "players": {
    "uuid": {
      "playerName": "PlayerName",
      "totalDrops": 15,
      "itemCounts": {
        "minecraft:diamond": 10,
        "minecraft:emerald": 5
      }
    }
  },
  "summary": {
    "totalItems": 15,
    "totalPlayers": 1,
    "itemBreakdown": {
      "minecraft:diamond": 10,
      "minecraft:emerald": 5
    }
  }
}

NESTED FOLDER ORGANIZATION:
==========================
FEATURE: Organize your Mobs configurations using nested folders!

Examples of valid organization:
- Mobs/vanilla_mobs/zombie_drops.json
- Mobs/modded_mobs/thermal_expansion/machines.json
- Mobs/boss_mobs/twilight_forest/bosses.json
- Mobs/by_biome/desert/desert_mobs.json
- Mobs/by_difficulty/hard/elite_drops.json

Benefits of nested folders:
- Organize drops by mod, biome, difficulty, or any system you prefer
- Keep related configurations together
- Easier to manage large numbers of entity configurations
- Works in both Normal Drops and Event Drops

Example Basic Drop Configuration:
[
  {
    "itemId": "minecraft:diamond",
    "dropChance": 5.0,
    "minAmount": 1,
    "maxAmount": 1,
    "requirePlayerKill": true,
    "enableDropCount": true
  }
]

Example Entity-Specific Drop Configuration:
[
  {
    "entityId": "minecraft:zombie",
    "itemId": "minecraft:emerald",
    "dropChance": 10.0,
    "minAmount": 1,
    "maxAmount": 2,
    "requirePlayerKill": false,
    "enableDropCount": true
  }
]

CUSTOM FILE LOADING:
===================
- ANY .json file in the correct directory will be loaded
- Rename, edit, or create new files freely
- Use /lootdrops reload to apply changes
- No server restart required!

HOW TO DISABLE DROPS:
====================
Option 1 - Empty the file: Replace all content with []
Option 2 - Set drop chances to 0: Change "dropChance": [value] to "dropChance": 0
Option 3 - Rename file extension: Change .json to .json.disabled

DON'T DELETE Global_Hostile_Drops.json - it will just regenerate!
Use the disable methods above instead.

COMPETITIVE EVENT SETUP:
=======================
Perfect for server events and competitions:

1. Create Event Configuration:
   - Set up your event drops with "enableDropCount": true
   - Use special items with NBT data for unique prizes
   - Set appropriate drop chances for competition balance

2. Enable Drop Counting:
   - Use /lootdrops dropcount true
   - Activate your event with /lootdrops event [name] on

3. Monitor Progress:
   - Check leaderboards with /lootdrops eventtop [event]
   - View individual stats with /lootdrops playerstats [player]
   - Drop_Count.json files update automatically

4. End Event:
   - Review final statistics in Drop_Count.json
   - Award prizes to top performers
   - Use /lootdrops reset_counts to clear for next event

Tips:
----
- Use Global_Hostile_Drops.json for drops that apply to all hostile mobs
- Use Mobs/ folder for entity-specific drops
- Create nested folders in Mobs/ to organize your configurations
- Create custom .json files for organized drop categories
- Event drops only activate when the event is enabled
- Drop counting only works for Event Drops, not Normal Drops
- Add "enableDropCount": true to track specific items
- Reference Global_Hostile_Drops.example for all possible configuration options
- Use /lootdrops reload to apply changes without restarting
- Delete entire folders to regenerate all example files
- Nested folders are scanned recursively - any .json file will be found
- Folder names don't affect functionality - organize however you prefer
- Drop_Count.json files are created automatically when needed
- Multiple events can have drop counting enabled simultaneously
- Each event maintains separate drop count statistics
