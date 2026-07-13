# Dead Signal

**Dead Signal** is a real-time online zombie survival and social-deduction game for 2–10 players. One crew member is secretly the carrier. The survivors must restore the city's relay stations, recover four cure samples, and reach evacuation while the carrier sabotages the grid and waits for the right moment to mutate.

The art, map, interface, names, and code are original. The project uses no copyrighted game assets.

## Play locally

```bash
npm install
npm start
```

Open `http://localhost:3000`. To test multiplayer on one computer, open a second private/incognito window, enter the room code, and join with a different name.

## Controls

| Action | Desktop | Phone/tablet |
|---|---|---|
| Move | WASD or arrow keys | Left joystick |
| Aim / fire | Mouse / left click | Fire button |
| Interact / report | E | Use button |
| Reload | R | Automatic UI (desktop key supported) |
| Transform / hide (carrier) | Q | Ability button |
| Bite while transformed | Space or left click | Fire button |
| Blackout sabotage (carrier) | X | — |
| Emergency meeting | Radio console button | Radio console button |

## Game loop

1. A host creates a five-letter room and shares the code.
2. Players join and ready up; the host deploys the crew.
3. A secret carrier is assigned when two or more players are present.
4. Survivors complete seven objectives while fighting server-controlled zombies.
5. Bodies can be reported and the safehouse radio can call a 30-second vote.
6. Survivors win by escaping with the cure or identifying the carrier. The carrier wins by reaching parity with the remaining survivors.

Solo rooms are supported as a zombie-survival practice mode without a secret carrier.

## Architecture

- Node.js + Express serves the browser client.
- Socket.IO provides rooms and low-latency state synchronization.
- The server owns movement validation, collision, enemy AI, projectiles, health, roles, voting, objectives, and win conditions.
- The client uses a responsive Canvas renderer with no external art dependencies.
- `/health` provides a deployment health check.

## Deploy

This is a persistent WebSocket server, so deploy it to a Node-compatible service such as Render, Railway, Fly.io, or a VPS. Static-only GitHub Pages cannot run the multiplayer server.

Build command:

```bash
npm install
```

Start command:

```bash
npm start
```

The server respects the platform-provided `PORT` environment variable.

## Tests

```bash
npm test
```

The test suite verifies sanitization, collision detection, room creation, multiplayer joining, role assignment, and match startup.
