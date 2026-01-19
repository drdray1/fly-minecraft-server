# Player Data Commands

This guide explains how to query player data from the da-mines Minecraft server using rcon commands.

## Prerequisites

- Fly.io CLI (`flyctl`) installed and authenticated
- Server must be running

## Basic Command Format

```bash
flyctl ssh console --app da-mines -C "rcon-cli '<command>'"
```

## Getting Player Inventory

### Full Inventory (truncated)
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> Inventory'"
```

### Specific Hotbar Slot (0-8)
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> Inventory[0]'"
```

### Main Inventory Slots (9-35)
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> Inventory[9]'"
```

### Loop Through All Hotbar Slots
```bash
for i in 0 1 2 3 4 5 6 7 8; do
  flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> Inventory[$i]'" 2>&1 | grep "minecraft:"
done
```

## Getting Equipment (Armor & Hands)

### Offhand (Left Hand)
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> equipment.offhand'"
```

### Head Armor
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> equipment.head'"
```

### Chest Armor
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> equipment.chest'"
```

### Leg Armor
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> equipment.legs'"
```

### Feet Armor
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> equipment.feet'"
```

### All Equipment at Once
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> equipment'"
```

## Other Useful Player Data

### Player Position
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> Pos'"
```

### Player Health
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> Health'"
```

### Player Food Level
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> foodLevel'"
```

### Player XP Level
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> XpLevel'"
```

### Player Game Mode
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER> playerGameType'"
```
- 0 = Survival
- 1 = Creative
- 2 = Adventure
- 3 = Spectator

### All Player Data (very long output)
```bash
flyctl ssh console --app da-mines -C "rcon-cli 'data get entity <PLAYER>'"
```

## Inventory Slot Reference

| Slot Numbers | Location |
|--------------|----------|
| 0-8 | Hotbar (left to right) |
| 9-35 | Main inventory (top-left to bottom-right) |

## Equipment Paths

| Path | Location |
|------|----------|
| `equipment.mainhand` | Right hand (selected hotbar slot) |
| `equipment.offhand` | Left hand |
| `equipment.head` | Helmet slot |
| `equipment.chest` | Chestplate slot |
| `equipment.legs` | Leggings slot |
| `equipment.feet` | Boots slot |

## Example: Full Inventory Check Script

```bash
#!/bin/bash
PLAYER="DrDray_1"
APP="da-mines"

echo "=== $PLAYER's Equipment ==="
for slot in offhand head chest legs feet; do
  result=$(flyctl ssh console --app $APP -C "rcon-cli 'data get entity $PLAYER equipment.$slot'" 2>&1 | grep "minecraft:")
  if [ -n "$result" ]; then
    item=$(echo "$result" | sed 's/.*id: "minecraft:\([^"]*\)".*/\1/')
    echo "$slot: $item"
  fi
done

echo ""
echo "=== $PLAYER's Hotbar ==="
for i in 0 1 2 3 4 5 6 7 8; do
  result=$(flyctl ssh console --app $APP -C "rcon-cli 'data get entity $PLAYER Inventory[$i]'" 2>&1 | grep "minecraft:")
  if [ -n "$result" ]; then
    item=$(echo "$result" | sed 's/.*id: "minecraft:\([^"]*\)", count: \([0-9]*\).*/\1 x\2/')
    echo "Slot $i: $item"
  fi
done
```

## Notes

- Player must be online for these commands to work
- Output may be truncated for long data - query specific fields for full data
- Replace `<PLAYER>` with the actual player username (case-sensitive)
- The `2>&1 | grep "minecraft:"` filters out connection messages and errors
