# Developer Commands

LinuxGSM provides commands to help developers gather information about the game server they are developing.

| Command Name | Command | Short |
| :--- | :--- | :--- |
| [Developer](developer-commands.md#developer) | `./gameserver developer` | `./gameserver dev` |
| Detect Dependencies | `./gameserver detect-deps` | `./gameserver dd` |
| Detect Glibc | `./gameserver detect-glibc` | `./gameserver dg` |
| Detect ldd | `./gameserver detect-ldd` | `./gameserver dl` |
| Query Raw | `./gameserver query-raw` | `./gameserver qr` |
| Clear Functions | `./gameserver clear-functions` | `./gameserver cf` |

### Developer

The `developer` command enable development mode allowing access to all hidden developer commands. plus generates a debug log `dev-debug.log`of everything LinuxGSM does when a command is run.

```bash
./gameserver developer
./gameserver dev
```

### Detect Dependencies

Detects dependencies the server requires by checking the contents of serverfiles. The output suggests the install command required.

```bash
./gameserver detect-deps
./gameserver dd
```

### Detect Glibc

Automatically detects which version of GLIBC a game server requires

```bash
./gameserver detect-glibc
./gameserver dg
```

### Detect ldd

Automatically detects required dependencies using the ldd command.

```bash
./gameserver detect-ldd
./gameserver dl
```

### Query Raw

Queries the game server using,`gamedig` , `query_gsquery.py`, `tcp` and `upd`, giving a raw output. This can diagnose if the game server query is working and configured correctly.

```bash
./gameserver query-raw
./gameserver qr
```

### Clear Functions

Use this command when pushing commits to a specific branch. It deletes all functions from `lgsm/functions` and removes default LinxuGSM configs. Allowing a commit to be applied to the testing enviroment without  `gameserver.sh` being overwritten and reseting the github branch settings.

```bash
./gameserver clear-fuctions
./gameserver cf
```

