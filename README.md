<p align="center">
  <img src="assets/SFS New World_ Multiplayer Spaceflight.jpg" alt="SFS NEW WORLD" width="100%">
</p>

<p align="center">
  <a href="https://discord.gg/xMe75bZVAt">
    <img src="https://img.shields.io/badge/Community-SFS%20NEW%20WORLD-5865F2?style=for-the-badge&logo=discord&logoColor=white">
  </a>
  <a href="https://www.reddit.com/r/SFSNEWWORLD/">
    <img src="https://img.shields.io/badge/Community-SFS%20NEW%20WORLD-FF4500?style=for-the-badge&logo=reddit&logoColor=white">
  </a>
  <a href="https://www.reddit.com/user/Allsh0/">
    <img src="https://img.shields.io/badge/Reddit-Developer%20Updates-FF4500?style=for-the-badge&logo=reddit&logoColor=white">
  </a>
</p>


#  SFS NEW WORLD

### Multiplayer for Spaceflight Simulator

> A multiplayer modification for **Spaceflight Simulator** focused on synchronized gameplay, shared worlds, networking, rooms, moderation, and real-time diagnostics — powered by a standalone multiplayer server.

**Release:** Beta 1
**Supported Game Versions:** `SFS 1.5.10.2` · `SFS 1.6.x`
**Project Status:** Closed Source · Private Development

---

##  Beta 1

**SFS NEW WORLD Beta 1** is the first public testing release of the project.

The current Beta 1 client supports:

- **Spaceflight Simulator 1.5.10.2**
- **Spaceflight Simulator 1.6.x**

Both supported game versions provide the **same multiplayer feature set**. Each game version uses its own compatible client build to ensure compatibility with the corresponding SFS version.

### Beta 1 Distribution Model

Beta 1 currently uses a **client-only distribution model**.

Players only need to install the official client DLL. The multiplayer server is hosted and managed by the project developer during the Beta 1 testing phase.

Server files and server infrastructure are **not publicly distributed** at this stage.

---

##  Supported Versions

| Game Version     | Client Package            | Multiplayer Features                |
| ---------------- | ------------------------- | ----------------------------------- |
| **SFS 1.6.x**    | `MultiplayerSFS-1.6`      | Full Beta 1 multiplayer feature set |
| **SFS 1.5.10.2** | `MultiplayerSFS-1.5.10.2` | Full Beta 1 multiplayer feature set |

> **Important:** Do not mix client builds between game versions.
> The `1.5.10.2` client is intended for SFS `1.5.10.2`, while the `1.6.x` client is intended for SFS `1.6.x`.

---

##  Features

### Multiplayer

- Connect to a multiplayer server using `IP:Port`
- LAN server discovery
- Public and private rooms
- Invite codes for private rooms
- Player list
- Real-time multiplayer chat
- Vehicle synchronization
- Position and movement synchronization
- Player input synchronization
- World-time synchronization through voting
- Player vehicle names and tags
- Multiplayer status bar
- Automatic compatibility validation
- Automatic reconnection
- Standalone server architecture
- Server-side moderation
- Real-time diagnostics

### Moderation

- Room owner moderation
- Mute / unmute
- Kick players
- Ban players
- Server administration
- Permanent IP bans
- `/unban` support
- Administrative logging

### Synchronization & Stability

- Multiplayer vehicle synchronization
- Simulation authority handling
- Collision resynchronization
- Docking synchronization
- Launchpad protection
- Packet-size validation
- Separate message-rate limits for synchronization and administration
- Player and chat validation

---

##  Architecture

```text
                         SFS NEW WORLD
                              │
                ┌─────────────┴─────────────┐
                │                           │
             CLIENT                       SERVER
          Mod / DLL                     Server.exe
                │                     Standalone
                │                           │
                └─────────────┬─────────────┘
                              │
                        Network Layer
                    UDP · Rooms · Sync
                              │
                ┌─────────────┼─────────────┐
                │             │             │
             Player A       Player B      Player C
```

The client runs inside **Spaceflight Simulator**, while the multiplayer server operates independently from the game installation.

The server does not require a copy of the game to run.

### Client

The client is distributed as a **single DLL**.

```text
SFS NEW WORLD.dll
```

The networking layer is embedded into the client package, so players do not need to install additional networking DLLs.

### Server

The multiplayer server is a standalone application independent from the game installation.

During Beta 1, the server is privately managed by the project developer and is **not included in the public client distribution**.

---

##  Installation

### Beta 1 — Client

The public Beta 1 release requires only one file.

1. Download the client package matching your version of Spaceflight Simulator.
2. Create the following folder inside your game installation:

```text
<Game>\Mods\SFS NEW WORLD\
```

3. Place the following file inside it:

```text
<Game>\Mods\SFS NEW WORLD\SFS NEW WORLD.dll
```

4. Launch Spaceflight Simulator.
5. Open **Multiplayer** from the mod interface.

### Important

- Install only the client build matching your SFS version.
- Do not install multiple copies of SFS NEW WORLD.
- Do not rename the DLL.
- Do not copy additional networking DLLs.
- `Lidgren.Network.dll` is embedded and does not need to be installed separately.
- `UITools` is not required for SFS NEW WORLD.

> **Beta 1:** Server installation is not required for players. The multiplayer server is managed by the project developer.

---

##  How to Play

### Connect to the Server

1. Launch Spaceflight Simulator.
2. Open **Multiplayer**.
3. Enter the server address and port.
4. Select **JOIN SERVER**.
5. Open the **ROOMS** section.

### Create a Room

1. Connect to the multiplayer server.
2. Open **ROOMS**.
3. Create a new room.
4. Choose the room name, privacy settings, and player limit.
5. Share the invitation code if the room is private.
6. Join the room and begin playing.

### Join a Room

1. Connect to the multiplayer server.
2. Open **ROOMS**.
3. Select an available room or enter an invitation code.
4. Join the room.
5. The client will synchronize the current multiplayer world and available vehicles.

### Launching & Control

- Build your vehicle normally in the game's construction area.
- Launch your vehicle into the multiplayer world.
- Vehicle state and movement are synchronized between connected players.
- A player cannot take control of a vehicle currently controlled by another player.
- Launchpad protection prevents conflicting launches when the launch platform is occupied.

---

##  Administration

SFS NEW WORLD includes server and room moderation systems.

### Room Owner

The player who creates a room automatically becomes its room owner.

Room owners can:

- Mute players
- Unmute players
- Kick players
- Ban players from their room

Room-owner permissions are limited to their own room.

### Server Administrator

The server administrator has access to server-wide administrative functionality.

Available commands include:

| Command               | Function                                   |
| --------------------- | ------------------------------------------ |
| `/help`               | Display available commands                 |
| `/admin [password]`   | Enable or disable administrator privileges |
| `/list`               | Display players in the room                |
| `/stats`              | Display server statistics                  |
| `/timewarp`           | Start a time-warp vote                     |
| `/stopwarp`           | Stop time warp                             |
| `/destroy`            | Destroy vehicles (administrator)           |
| `/unban <IP or name>` | Remove a permanent ban                     |

Administrative actions require appropriate permissions and are logged by the server.

---

##  Diagnostics

SFS NEW WORLD provides real-time multiplayer diagnostics.

Example:

```text
Players: 2/8       Vehicles: 3
Rooms: 1            Ping: 42 ms
Packets/sec: 320    Bandwidth: 1.8 MB/s
Server Tick: 1.0 ms
Uptime: 12m
```

Diagnostics can provide information about:

- Connected players
- Active vehicles
- Active rooms
- Network latency
- Packets per second
- Bandwidth usage
- Server tick time
- Server uptime

---

##  Beta Status

Beta 1 is primarily focused on testing:

- Multiplayer connectivity
- Vehicle synchronization
- World-time synchronization
- Room stability
- Server performance
- Player interaction
- Launching and vehicle control
- Network reliability

The project is still under active development. Bugs, synchronization issues, and unexpected behavior may occur during testing.

---

##  Known Issues

### World Saving

World saving is currently unavailable.

Rooms are temporary and may be removed when they become empty. This behavior is intentional during the current Beta stage.

### Version Compatibility

The `1.5.10.2` and `1.6.x` clients must not be mixed with incompatible server builds.

### Collision Synchronization

Collision states may temporarily differ between clients.

The synchronization system can request a directed resynchronization when an inconsistent collision state is detected.

In rare cases, reconnecting to the room may be required.

### Docking

Docking between vehicles controlled by different players may still be sensitive and can result in synchronization inconsistencies.

### Duplicate Mod Installations

Multiple copies of the mod can prevent SFS NEW WORLD from loading correctly.

Remove old or duplicate installations before launching the game.
---

##  Roadmap

###  Beta 1

- [x] Multiplayer server connectivity
- [x] Multiplayer rooms
- [x] Player synchronization
- [x] Vehicle synchronization
- [x] World-time synchronization
- [x] Server and room browser
- [x] Multiplayer chat
- [x] Player names and vehicle tags
- [x] Support for SFS 1.5.10.2
- [x] Support for SFS 1.6.x
- [x] Standalone server architecture
- [x] Version compatibility validation
- [x] Automatic reconnection
- [x] Room moderation
- [x] Server administration
- [x] Real-time diagnostics
- [x] Launchpad protection
- [x] Server security and packet validation

###  In Development

- [ ] World saving and restoration after server restart
- [ ] Improved collision synchronization
- [ ] Improved docking synchronization
- [ ] Greater stability with large numbers of vehicles
- [ ] Expanded ban and administration system
- [ ] Improved server management tools

###  Future

- [ ] Public online server browser
- [ ] Remote server administration
- [ ] Additional multiplayer gameplay systems
- [ ] Additional platform support

---

##  Compatibility

| Component             | Status                 |
| --------------------- | ---------------------- |
| Spaceflight Simulator | `1.5.10.2` and `1.6.x` |
| Client                | Version-specific build |
| Server                | Standalone             |
| Operating System      | Windows                |
| Client Runtime        | .NET Framework 4.8     |
| Networking            | UDP                    |

> Each SFS version requires its corresponding compatible client build.

---

##  Development

```text
C# · .NET Framework 4.8 · Unity · Lidgren.Network · UDP
```

### Client

The client uses Harmony-based modifications to `Assembly-CSharp` and an embedded networking layer.

The multiplayer networking components are packaged into the client DLL.

### Server

The server is a standalone application independent from the game installation.

The client and server communicate through the project's multiplayer protocol over UDP.

---

##  Bug Reports

SFS NEW WORLD is actively tested during Beta 1.

When reporting a problem, please include:

- Spaceflight Simulator version
- SFS NEW WORLD version
- Server name
- Whether the issue occurred on the client or server
- Steps to reproduce the problem
- Expected behavior
- Actual behavior
- `Player.log` when applicable
- Server logs when applicable
- Screenshots or video when useful

Clear reproduction steps make debugging significantly easier.

---

##  Releases

Beta releases are distributed through **GitHub Releases**.

Each release may include:

- Version number
- Supported SFS version
- New features
- Bug fixes
- Known issues
- Installation instructions
- Compatibility information

Always download the client build matching your installed version of Spaceflight Simulator.

---

##  Community & Testing

SFS NEW WORLD is currently developed as an independent project.

Community participation is focused on:

- Beta testing
- Bug reports
- Feedback
- Feature suggestions
- Multiplayer testing

The project is **closed source**, so the source code and internal development files are not publicly available.

---

##  License

**SFS NEW WORLD is proprietary software. All rights reserved.**

The source code is not publicly distributed.

The official client may be installed and used for personal, non-commercial gameplay during the Beta testing period, subject to the project's license terms.

Without explicit permission from the author, you may not:

- Redistribute or re-upload the official client files.
- Modify or create derivative versions of the software.
- Decompile, disassemble, or attempt to obtain the source code, except where such activity cannot legally be restricted.
- Sell, sublicense, or commercially redistribute the software.
- Repackage SFS NEW WORLD as another mod or software package.
- Claim ownership or authorship of the project or its original components.
- Distribute private server software or internal development files.
- Use the SFS NEW WORLD name or branding to imply an official or authorized derivative project.

Third-party libraries and components remain subject to their respective licenses.

For permissions not explicitly granted by the project license, contact the author.

**Author:** Allsh
**Project:** SFS NEW WORLD
**Copyright:** © 2026 Allsh. All rights reserved.

---

### SFS NEW WORLD

**Build. Connect. Explore.**

*The next multiplayer world.*
