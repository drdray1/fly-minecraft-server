# da-mines

A Paper Minecraft server running on Fly.io with scale-to-zero to minimize costs.

## Server Info

| | |
|---|---|
| **Server IP** | `109.105.222.39:25565` |
| **Minecraft Version** | 1.21.11 (Java Edition) |
| **Server Type** | Paper |
| **Region** | Los Angeles (lax) |

## Plugins

| Plugin | Description |
|--------|-------------|
| **EssentialsX** | Core commands: /home, /spawn, /tpa, /warp, /back, /nick |
| **GriefPrevention** | Claim land to protect your builds |
| **Simple Voice Chat** | Proximity voice chat with other players |
| **SinglePlayerSleep** | One player can skip the night |

## How to Use Plugins

### EssentialsX Commands
- `/sethome` - Set your home location
- `/home` - Teleport to your home
- `/spawn` - Teleport to spawn
- `/tpa <player>` - Request to teleport to a player
- `/back` - Return to your last location
- `/msg <player> <message>` - Private message

### GriefPrevention (Land Claiming)
1. Craft a **golden shovel**
2. Right-click one corner of your claim
3. Right-click the opposite corner
4. Your claim is protected!

**Claim Commands:**
- `/trust <player>` - Allow a player to build in your claim
- `/untrust <player>` - Remove a player's access
- `/trustlist` - See who has access to your claim
- `/abandonclaim` - Delete your current claim

### Simple Voice Chat
- Press **V** to open voice chat settings
- Press **Caps Lock** (default) to talk
- Nearby players will hear you based on distance
- **Requires client mod** - install `voicechat-fabric` in your mods folder

### Sleep Skip
- Just one player needs to sleep to skip the night
- No more waiting for everyone!

## Whitelist

This server is whitelisted. To join, an admin must add you.

**Admin Commands (requires OP):**
```
/whitelist add <username>
/whitelist remove <username>
/whitelist list
```

## How It Works

- Server auto-stops after 2 minutes with no players connected
- Server auto-starts when a player tries to connect (may take ~30 seconds to boot)
- World data persists on a 1GB volume

## Admin Commands

Check server status:
```bash
flyctl status --app da-mines
```

View logs:
```bash
flyctl logs --app da-mines
```

Manually start the server:
```bash
flyctl machine start --app da-mines
```

Give a player OP:
```bash
flyctl ssh console --app da-mines -C "rcon-cli op USERNAME"
```

Add to whitelist via CLI:
```bash
flyctl ssh console --app da-mines -C "rcon-cli whitelist add USERNAME"
```

## Deployment

Push to `main` branch to trigger automatic deployment via GitHub Actions.

### Required GitHub Secrets

- `APP_NAME` - Fly.io app name (`da-mines`)
- `FLY_API_TOKEN` - Fly.io deploy token

## Cost

- ~$2/month for IPv4 address
- VM costs only while server is running (~$0.05/hour for 4GB performance CPU)

## License

MIT
