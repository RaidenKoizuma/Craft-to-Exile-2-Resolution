Event Drops Configuration
========================

This directory contains drops that are only active during specific events.

FILES CREATED ON FIRST LOAD:
============================
Each event folder contains:
- [Event]_Event_Drops_Example.json: Clean basic example (safe to delete)
- Mobs/ folder: For entity-specific event drops
- Drop_Count.json: Auto-generated drop counting data (when enabled)

Built-in Events:
- Winter/: Winter season drops
- Summer/: Summer season drops
- Easter/: Easter holiday drops
- Halloween/: Halloween holiday drops

Custom Events:
You can create your own event folders with any name.
Each event folder can contain:
- Custom .json files: Your event-specific drop configurations
- Mobs/: Entity-specific drops during this event
  * Supports nested folders for organization!
  * Example: Mobs/event_bosses/special_halloween_boss.json
- Drop_Count.json: Automatically created when drop counting is used

DROP COUNTING SYSTEM:
====================
EXCLUSIVE FEATURE: Drop counting only works in Event Drops!

Setting Up Drop Counting:
1. Add "enableDropCount": true to any drop configuration
3. Activate your event: /lootdrops event [name] on
4. Drop_Count.json will be created automatically

Drop Counting Features:
- Tracks individual player statistics per event
- Supports multiple simultaneous events with separate tracking
- Perfect for competitive events and leaderboards
- Auto-generates comprehensive statistics
- Real-time updates as players collect items

Example Drop Count Configuration:
[
  {
    "itemId": "minecraft:diamond",
    "dropChance": 10.0,
    "minAmount": 1,
    "maxAmount": 3,
    "requirePlayerKill": true,
    "enableDropCount": true,
    "_comment": "Special competition diamonds"
  }
]

Drop Count Commands:
- /lootdrops top: Show top players across all events
- /lootdrops eventtop [event]: Show top players for specific event
- /lootdrops playerstats [player]: Show detailed player statistics
- /lootdrops reset_counts: Reset all drop count data

REGENERATE EVENT EXAMPLES:
=========================
To regenerate examples for a specific event:
1. Delete the entire event folder (e.g., 'Winter/')
2. Use /lootdrops reload or restart the server
3. The event folder and examples will be recreated

WARNING: Deleting an event folder will also delete Drop_Count.json!
Back up your drop count data before regenerating examples.

Event Management:
Events are controlled through Active_Events.json in the main config directory.
Use the /lootdrops event [name] [on/off] command to toggle events.

Event drops are checked IN ADDITION to normal drops when active.

COMPETITIVE EVENT WORKFLOW:
==========================
1. PREPARATION:
   - Design your event drops with balanced chances
   - Add "enableDropCount": true to tracked items
   - Test configurations in creative mode

2. EVENT START:
   - Enable drop counting: /lootdrops dropcount true
   - Activate event: /lootdrops event [name] on
   - Announce event to players

3. DURING EVENT:
   - Monitor progress: /lootdrops alltop
   - Check individual stats: /lootdrops playerstats [player]
   - Drop_Count.json updates automatically

4. EVENT END:
   - Deactivate event: /lootdrops event [name] off
   - Review final Drop_Count.json for winners
   - Award prizes based on statistics
   - Optional: Reset counts for next event

MULTI-EVENT COMPETITIONS:
========================
Run multiple events simultaneously:
- Each event maintains separate drop counts
- Players can participate in multiple events
- /lootdrops top shows combined statistics
- /lootdrops eventtop [event] shows event-specific stats

ADVANCED CONFIGURATION:
======================
For advanced event drop configurations, reference:
- Normal Drops/Global_Hostile_Drops.example for all possible properties
- Event drops use the same JSON format as normal drops
- All advanced features (NBT, commands, conditions) work in events
- Combine drop counting with custom NBT for unique competition items
- Use commands with drops to create special effects or announcements
