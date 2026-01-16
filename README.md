# da-mines

A Paper Minecraft server running on Fly.io with scale-to-zero to minimize costs.

## Server Info

| | |
|---|---|
| **Server IP** | `109.105.222.39:25565` |
| **Minecraft Version** | 1.21.11 (Java Edition) |
| **Server Type** | Paper |
| **Region** | Los Angeles (lax) |

## How It Works

- Server auto-stops after 2 minutes with no players connected
- Server auto-starts when a player tries to connect (may take ~30 seconds to boot)
- World data persists on a 1GB volume

## Commands

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

## Deployment

Push to `main` branch to trigger automatic deployment via GitHub Actions.

### Required GitHub Secrets

- `APP_NAME` - Fly.io app name (`da-mines`)
- `FLY_API_TOKEN` - Fly.io deploy token

## Cost

- ~$2/month for IPv4 address
- VM costs only while server is running (~$0.02/hour for 4GB shared CPU)

## License

MIT
