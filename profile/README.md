<p align="center">
  <img src="https://img.shields.io/badge/Godot-4.6-478CBF?logo=godotengine&logoColor=white" alt="Godot 4.6" />
  <img src="https://img.shields.io/badge/Client-C%23%20.NET-512BD4?logo=csharp&logoColor=white" alt="Client: C# .NET" />
  <img src="https://img.shields.io/badge/Server-C-A8B9CC?logo=c&logoColor=white" alt="Server: C" />
  <img src="https://img.shields.io/badge/DB-MySQL-4479A1?logo=mysql&logoColor=white" alt="Database: MySQL" />
  <img src="https://img.shields.io/badge/Protocol-TCP-FF5B1F" alt="Protocol: TCP" />
  <img src="https://img.shields.io/badge/Game Players-2--4-brightgreen" alt="Players: 2–4" />
  <img src="https://img.shields.io/badge/Total Players-64-green" alt="Players: 2–4" />
  <img src="https://img.shields.io/badge/Platform-Windows-0078D6?logo=windows&logoColor=white" alt="Platform: Windows" />
</p>

<p align="center">
  <a href="#physical-layer">Physical Layer</a> ·
  <a href="#ui">UI</a> ·
  <a href="#core-mechanics">Core Mechanics</a> ·
  <a href="#items--abilities">Items &amp; Abilities</a> ·
  <a href="#protocol">Protocol</a> ·
  <a href="#assets-credits">Assets Credits</a> ·
  <a href="#music">Music</a> ·
  <a href="#authors">Authors</a>
</p>

<table align="center">
  <tr>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/e5333bde-170a-4fde-bdc9-5540187c97e9" width="100%" alt="Image 1" />
    </td>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/f5174d2a-4f5c-4a7d-9c84-14689ab983f5" width="100%" alt="Image 2" />
    </td>
  </tr>
  <tr>
    <td colspan="2" align="center">
      <img src="https://github.com/user-attachments/assets/f634059e-0109-4745-98bd-fa5483d32e10" width="100%" alt="logo" /> 
    </td>
  </tr>
  <tr>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/2f723882-1ca1-4878-aee8-45d460554c83" width="100%" alt="Image 3" />
    </td>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/f1f3723e-fa75-472b-9edd-b2570bff4961" width="100%" alt="Image 4" />
    </td>
  </tr>
</table>

A multiplayer 3D Parchís-style board game for 2–4 players. Players roll dice, move their four pieces around the board, and compete to be the first to get all four pieces to their goal. Each match is overseen by **Ophanim**, a supernatural dealer who presides over the initiative sequence, the golden square roulette, and the Sword of Damocles — a turn timer enforced by a falling blade.

---

## Physical Layer

![Game Architecture Diagram](https://github.com/user-attachments/assets/a666bfa4-b674-4dde-9bd9-41f91118ff19)

---

## UI

<table>
  <tr>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/1c2353c9-62fd-44dc-a78a-0b8849b1abb2" width="100%" alt="Environment" />
    </td>
    <td width="50%" align="center">
      <img src="https://github.com/user-attachments/assets/8a656567-4c17-4091-8d7b-060930fc99b5" width="100%" alt="UI" />
    </td>
  </tr>
</table>

---

## Core Mechanics

### Turn Flow

At the start of each turn the current player rolls two dice and moves one piece by the combined total. If no legal moves exist, the turn is skipped automatically. After the first piece moves anywhere in the match, a **30-second turn timer** begins. Warnings are broadcast at 30, 10, and 5 seconds remaining. If the timer expires, the Sword of Damocles falls.

### Board Layout

The board has an outer ring (squares 1–68) and four color-specific goal corridors. Pieces start at home (square 0) and must travel the full outer ring before entering their color corridor.

| Zone | Squares | Goal |
|------|---------|------|
| Outer ring | 1 – 68 | — |
| Yellow corridor | 101 – 108 | 108 |
| Blue corridor | 111 – 118 | 118 |
| Red corridor | 121 – 128 | 128 |
| Green corridor | 131 – 138 | 138 |

**Exit squares:** Yellow 5 · Blue 22 · Red 39 · Green 56  
**Universal safe squares:** 1, 12, 17, 29, 34, 46, 51, 63, 68

### Captures
<img src="https://github.com/user-attachments/assets/4d28e0e6-4c21-4526-8264-c1fa971908a8" align="right" width="120" alt="Captures">
Landing on a square occupied by an opponent's piece sends it back home. The attacker receives 20 bonus movement points. Safe squares block captures.
<br clear="all" />

---

### Goals
<img src="https://github.com/user-attachments/assets/963a9012-a0b0-4a37-a0d7-d8894944da45" align="right" width="120" alt="Goals">
Getting a piece to its goal square earns 10 bonus movement points. The first player to place all four pieces at the goal wins.
<br clear="all" />

---

### Barriers
<img src="https://github.com/user-attachments/assets/b5fb9f75-f0fd-4b20-bcef-00fce3c09156" align="right" width="120" alt="Barriers">
Two pieces of the same color on the same square form a barrier. Enemy pieces cannot land on or pass through a barrier. The barrier dissolves when one of its pieces moves away. A Fire Axe can destroy an enemy barrier directly.
<br clear="all" />

---

### Doubles
<img src="https://github.com/user-attachments/assets/933dba40-9804-4a0d-a3eb-23e396975208" align="right" width="120" alt="Doubles">
Rolling doubles grants a second roll. Three consecutive doubles triggers a penalty: the active piece is sent home and the player loses one life.
<br clear="all" />

---

### Lives
<img src="https://github.com/user-attachments/assets/d1a404d7-c33e-4267-bee2-9ea5253719b1" align="right" width="120" alt="Lives">
Each player starts with 3 lives. Reaching zero lives eliminates that player from the match.
<br clear="all" />

---

### Golden Squares
<img src="https://github.com/user-attachments/assets/bab4988e-a613-42f5-af8a-213f4ccee487" align="right" width="120" alt="Golden Squares">
Each color quadrant has one golden square. Landing on it triggers a roulette spin presided over by Ophanim. The outcome is either an item grant or nothing ("click"). The Damocles sword is dismissed during this sequence and respawns on the next turn.
<br clear="all" />

---

### Sword of Damocles
<img src="https://github.com/user-attachments/assets/b1c0426e-246c-48b5-a0a0-7744708fa63b" align="right" width="120" alt="Sword of Damocles">
At the start of each turn, Ophanim hangs a sword above the board on a thin rope. The sword swings with spring physics throughout the turn as a visible countdown. If the 30-second timer expires, the rope is cut and the sword falls and impales the board. Once the next dice roll lands, the sword is dismissed. The timer only arms after the first piece move of the entire match, so it never runs during the opening Ophanim sequence.
<br clear="all" />

---

## Items & Abilities

Items are acquired through the golden square roulette. A player can hold multiple items at once.

| Item | Protocol name | Effect | |
|------|---------------|--------|:--:|
| **Handcuffs** | `handcuffs` | Skip an opponent's next turn | <img width="96" alt="handcuffs" src="https://github.com/user-attachments/assets/af9cc6ae-30ac-44fe-8a3c-28752c83a3ac" /> |
| **Cigarette** | `cigarette` | Reroll the pending dice | <img width="96" alt="cigarette" src="https://github.com/user-attachments/assets/4cf76e80-085b-4033-817d-c3547a70837d" /> |
| **Fire Axe** | `fire_axe` | Destroy one enemy barrier | <img width="96" alt="fire axe" src="https://github.com/user-attachments/assets/0e58c345-30f4-48a7-800a-aeeaddaf692f" /> |
| **Magnifying Glass** | `magnifying_glass` | Peek at the next dice result before rolling | <img width="96" alt="magnifying glass" src="https://github.com/user-attachments/assets/686ccfb0-691f-46b3-951b-e556cdb84ca0" /> |
| **Makarov** | `gun` | Russian-roulette shot at an enemy, might bite back | <img width="96" alt="makarov" src="https://github.com/user-attachments/assets/58121435-910f-4634-9cd7-c0c432f1e1e5" /> |

---

## Protocol

Server: `bolty.website:8888` (TCP)

### Request Types (Client → Server)

| Code | Name | Purpose |
|:----:|------|---------|
| 1 | `REQ_REGISTER` | Create an account |
| 2 | `REQ_LOGIN` | Authenticate |
| 3 | `REQ_CHANGE_SKIN` | Persist the chosen character skin |
| 4 | `REQ_LOGOUT` | Graceful logout |
| 5 | `REQ_JOIN_ROOM` | Enter a room (1–3) |
| 6 | `REQ_SEND_CHAT` | Send a chat message |
| 7 | `REQ_GAME_ACTION` | Perform an in-game action |
| 8 | `REQ_LEAVE_ROOM` | Return to the lobby |
| 9 | `REQ_CONNECT_LIVE` | Open the persistent push connection |
| 13 | `REQ_READY` | Mark ready; starts the countdown when all are ready |
| 16 | `REQ_UNREADY` | Cancel ready before the countdown begins |
| 18 | `REQ_GET_HISTORY` | Fetch a player's match history |
| 19 | `REQ_GET_LEADERBOARD` | Fetch the global points leaderboard |

### Push Message Types (Server → Client)

| Code | Name | Purpose |
|:----:|------|---------|
| 10 | `MSG_USER_LIST` | Connected-players list |
| 11 | `MSG_CHAT` | Chat broadcast |
| 12 | `MSG_ROOM_STATE` | Room occupancy update |
| 14 | `MSG_COUNTDOWN` | Pre-game countdown tick |
| 15 | `MSG_GAME_START` | Match is starting |
| 17 | `MSG_GAME_ACTION` | Game action result |

### Response Codes

| Code | Meaning |
|------|---------|
| 0 | RES_SUCCESS |
| 1 | RES_ERR_USER_EXISTS |
| 2 | RES_ERR_INVALID_CREDENTIALS |
| 3 | RES_ERR_DATABASE |
| 4 | RES_ERR_INVALID_INPUT |
| 99 | RES_ERR_UNKNOWN |

### Constants

```
MAX_USERNAME     = 12 bytes
MAX_PASSWORD     = 12 bytes
MAX_CLIENTS      = 64
MAX_CHAT_MESSAGE = 100 bytes
NUM_ROOMS        = 3
MAX_ROOM_PLAYERS = 4
```

### Packet Formats

**REQ_REGISTER (1) / REQ_LOGIN (2)**
```
Client → 25 bytes:
  [type 1B][username 12B ASCII][password 12B ASCII]

Server → 129 bytes:
  [code 1B][message 128B ASCII null-padded]

On successful login, message contains:
  "Login successful. Welcome ID <user_id> SKIN <skin_id>"
```

**REQ_CHANGE_SKIN (3)**
```
Client → 9 bytes (packed, little-endian):
  [type 1B][user_id 4B][skin_id 4B]

Server → 129 bytes:
  [code 1B][message 128B ASCII null-padded]
```

**REQ_JOIN_ROOM (5)**
```
Client → 2 bytes on live connection:
  [type 1B][room_id 1B]   (room_id: 1–3)

No direct response. Server emits MSG_ROOM_STATE to all live clients.
```

**REQ_SEND_CHAT (6)**
```
Client → 101 bytes on live connection:
  [type 1B][message 100B ASCII null-terminated]

No direct response. Server emits MSG_CHAT to all live clients.
```

**REQ_LEAVE_ROOM (8)**
```
Client → 1 byte on live connection:
  [type 1B]

No direct response. Server moves client back to lobby and emits MSG_ROOM_STATE.
```

**REQ_CONNECT_LIVE (9)**
```
Client → 17 bytes:
  [type 1B][username 12B ASCII][user_id 4B big-endian]

Connection stays open. Server sends MSG_USER_LIST on connect/disconnect events.
```

**REQ_LOGOUT (4)**
```
Client → 1 byte on live connection:
  [type 1B]

No direct response. Server removes client, emits MSG_USER_LIST to remaining
clients, and closes the connection. Distinguishes a voluntary logout from an
abrupt network drop.
```

**MSG_USER_LIST (10)**
```
Server → (2 + count×12) bytes:
  [type 1B][count 1B][username 12B] × count

count = 0 is valid. Max size: 2 + 64×12 = 770 bytes.
```

**MSG_CHAT (11)**
```
Server → 113 bytes to all live clients:
  [type 1B][username 12B ASCII][message 100B ASCII]
```

**MSG_ROOM_STATE (12)**
```
Server → 51 bytes to all live clients:
  [type 1B][room_id 1B][count 1B][name 12B] × 4

Emitted whenever anyone joins or leaves a room.
```

**REQ_GAME_ACTION (7) / MSG_GAME_ACTION (17)**
```
Client → Server (live connection):
  [type 1B][match_id 4B big-endian][user_id 4B big-endian]
  [payload_len 2B big-endian][payload N bytes JSON]

Server → Client:
  [type 1B][payload_len 2B big-endian][payload N bytes JSON]

The "action" field in JSON identifies the event.
```

**REQ_GET_HISTORY (18)**
```
Client → 13 bytes:
  [type 1B][username 12B ASCII]

Server → variable:
  [code 1B][json_len 4B big-endian][json N bytes]

json is an array of the player's matches (newest first), each with room,
status, start/end times, duration, winner and the full finishing order.
```

**REQ_GET_LEADERBOARD (19)**
```
Client → 1 byte:
  [type 1B]

Server → variable:
  [code 1B][json_len 4B big-endian][json N bytes]

json is an array of the top players by points: [{ username, points }, ...].
```


### Game Action Flow

All in-game messages travel over the live connection as `REQ_GAME_ACTION` /
`MSG_GAME_ACTION` JSON payloads; the `action` field names the event. A match
plays out as the sequence of exchanges below.

#### Match start

```
game_start → server begins the Ophanim sequence and chair selection
```

#### Chair selection

```
Client → choose_chair   { action, color }
Server → chair_taken    { action, color, user_id, username }
Server → chairs_locked  { action }
```

#### Initiative sequence

```
Server → initiative_sequence {
           action,
           turn_order:     [user_id, ...],
           item_grants:    [{ user_id, items:[...] }, ...],
           golden_squares: [sq, sq, sq, sq]
         }
```

#### Normal turn

```
Server → turn_start    { action, user_id }
Client → roll_dice     { action, die1, die2 }
Server → dice_result   { action, user_id, die1, die2, total,
                         moveable_pieces:[0-3,...], can_exit_house:bool,
                         is_doubles:bool, consecutive_doubles:N }
                         (empty moveable_pieces → server auto-skips the turn)
Client → move_piece    { action, piece_id }
Server → piece_moved   { action, user_id, piece_id, from, to, steps,
                         is_exit:bool, on_safe_square:bool }
```

#### Follow-up events (after `piece_moved`)

```
Server → capture              { action, attacker_user_id, victim_user_id,
                                victim_piece_id, square, bonus_movements:20 }
Server → goal_scored          { action, user_id, piece_id,
                                pieces_in_goal:N, bonus_movements:10 }
Server → golden_square_event  { action, user_id, square,
                                spins:["gun"|"cigarette"|...|"reroll", ...],
                                final_item:"<item name>" }
Server → barrier_formed       { action, user_id, square, piece_ids:[a,b] }
Server → barrier_broken       { action, user_id, square, reason:"moved" }
```

#### Extra turns

```
Server → extra_turn  { action, user_id,
                       reason:"doubles"|"capture_bonus"|"goal_bonus",
                       pending_movements:N }
                       doubles → continues with a new turn_start (same user_id)
                       bonus   → player moves pending_movements extra points
```

> **5 + X exit + capture:** the second die (X) is consumed *before* the capture
> bonus. The server emits `dice_result(die1=X, die2=0)` first, then fires
> `extra_turn(capture_bonus, pending_movements=20)` after that move.

#### Triple doubles penalty

```
Server → triple_double_penalty { action, user_id, piece_id }
Server → life_lost             { action, user_id, lives_remaining,
                                 reason:"timeout"|"triple_double" }
Server → turn_end              { action, user_id, next_user_id }
Server → turn_start            { action, user_id }    ← next player
```

#### Turn end

```
Server → turn_end    { action, user_id, next_user_id }
Server → turn_start  { action, user_id }
```

> If the next player is handcuffed, the server emits
> `handcuff_skip { action, user_id }` in place of `turn_start`.

#### Turn timer

```
Server → turn_timer_warning  { action, user_id, seconds_remaining }
Server → turn_timer_expired  { action, user_id }
```

#### Item — Handcuffs

```
Client → use_handcuffs      { action, target_user_id }
Server → handcuffs_applied  { action, attacker_user_id, target_user_id }
```

The cuffs fly to the target's head and hover until their next turn, when the
server emits `handcuff_skip` instead of `turn_start`.

#### Item — Cigarette

```
Client → use_cigarette     { action }
Server → cigarette_result  { action, user_id, die1, die2, total,
                             moveable_pieces:[0-3,...] }
```

Replaces the pending dice. If `moveable_pieces` is empty: non-doubles auto-passes
the turn; doubles grants an `extra_turn` + new `turn_start`.

#### Item — Fire Axe

```
Client → use_fire_axe       { action, target_square }
Server → barrier_destroyed  { action, attacker_user_id, square,
                              freed_pieces:[{ user_id, piece_id }, ...] }
```

Both pieces of the targeted enemy barrier are sent home. Consumes the axe.

#### Item — Magnifying Glass

```
Client → use_magnifying_glass   { action }
Server → magnifying_glass_used  { action, user_id }       (public)
Server → peek_result            { action, die1, die2 }    (private — peeker only)
```

Pre-rolls the next dice without committing them, so the peeker can decide whether
to use a Cigarette before the real roll. Consumes the glass.

#### Item — Makarov

```
Client → use_gun     { action, target_user_id }
Server → gun_result  { action, attacker_user_id, target_user_id,
                       result:"bang"|"click", lives_remaining:N }
```

A `bang` makes the target lose a life (`life_lost` follows, possibly
`player_eliminated`); a `click` does nothing. Ignores safe squares. Consumes the gun.

#### Match conclusion

```
Server → player_eliminated  { action, user_id }
Server → game_over          { action, reason:"race"|"elimination", winner_user_id }
```


---

## Assets Credits

- **[sodaraptor](https://sodaraptor.itch.io/)**
- **[elbolilloduro](https://elbolilloduro.itch.io/)**
- **[binbun3d](https://binbun3d.itch.io/)**
- **[ggbot](https://ggbot.itch.io/)**
- **[arlez80](https://godotengine.org/asset-library/asset?user=arlez80)**
- **[doctor-sci3nce](https://doctor-sci3nce.itch.io/)**
- **[youpzdev](https://sketchfab.com/youpzdev)**
- **[pepperonijabroni](https://pepperonijabroni.itch.io/)**
- claude :D

## Music
- **[Portal Radio OST](https://www.youtube.com/watch?v=mD3v1B_aXw0&list=RDmD3v1B_aXw0&start_radio=1)**
- **[I'm not a Human OST](https://www.youtube.com/watch?v=flGJj6d1Q9M&list=RDflGJj6d1Q9M&start_radio=1)**
- **[Buckshot Roulette General OST](https://www.youtube.com/watch?v=mvkcyB_lve0&list=RDmvkcyB_lve0&start_radio=1)**

---

## Authors

- **David Garcia**
- **Eric Menaya**
- **Xavi Guillamon**
