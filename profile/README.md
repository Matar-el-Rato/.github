# Matar el Rato

[IMAGES - game screenshot]

A multiplayer 3D Parchís-style board game for 2–4 players. Players roll dice, move their four pieces around the board, and compete to be the first to get all four pieces to their goal. Each match is overseen by **Ophanim**, a supernatural dealer who presides over the initiative sequence, the golden square roulette, and the Sword of Damocles — a turn timer enforced by a falling blade.

Source code: [github.com/Matar-el-Rato](https://github.com/Matar-el-Rato)  
Latest video: [youtu.be/it1Uf9Nida0](https://youtu.be/it1Uf9Nida0)

---

## Physical Layer

![Game Architecture Diagram](https://github.com/user-attachments/assets/a666bfa4-b674-4dde-9bd9-41f91118ff19)

---

## Environment & UI

- **View:** Isometric view (Isoview)
- **POV:** In-game point of view

---

## Core Mechanics

### Turn Flow

At the start of each turn the current player rolls two dice and moves one piece by the combined total. If no legal moves exist, the turn is skipped automatically. After the first piece moves anywhere in the match, a **60-second turn timer** begins. Warnings are broadcast at 30, 10, and 5 seconds remaining. If the timer expires, the Sword of Damocles falls.

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

Landing on a square occupied by an opponent's piece sends it back home. The attacker receives **20 bonus movement points**. Safe squares block captures.

### Goals

Getting a piece to its goal square earns **10 bonus movement points**. The first player to place all four pieces at the goal wins.

### Barriers

Two pieces of the same color on the same square form a barrier. Enemy pieces cannot land on or pass through a barrier. The barrier dissolves when one of its pieces moves away. A **Fire Axe** can destroy an enemy barrier directly.

### Doubles

Rolling doubles grants a second roll. Three consecutive doubles triggers a penalty: the active piece is sent home and the player loses one life.

### Lives

Each player starts with **3 lives**. Reaching zero lives eliminates that player from the match.

### Golden Squares

Each color quadrant has one golden square. Landing on it triggers a roulette spin presided over by Ophanim. The outcome is either an item grant or nothing ("click"). The Damocles sword is dismissed during this sequence and respawns on the next turn.

### Sword of Damocles

At the start of each turn, Ophanim hangs a sword above the board on a thin rope. The sword swings with spring physics throughout the turn as a visible countdown. If the 60-second timer expires, the rope is cut and the sword falls and impales the board. Once the next dice roll lands, the sword is dismissed. The timer only arms after the first piece move of the entire match, so it never runs during the opening Ophanim sequence.

---

## Items & Abilities

[IMAGES - items]

| Item | Protocol name | Effect | Image | 
|------|--------------|--------|--------|
| Handcuffs | `handcuffs` | Skip an opponent's next turn | <img width="256" height="256" alt="esposas" src="https://github.com/user-attachments/assets/af9cc6ae-30ac-44fe-8a3c-28752c83a3ac" /> |
| Fire Axe | `fire_axe` | Destroy one enemy barrier | <img width="256" height="256" alt="hacha" src="https://github.com/user-attachments/assets/0e58c345-30f4-48a7-800a-aeeaddaf692f" /> |
| Magnifying Glass | `magnifying_glass` | Peek at the dice result before rolling | <img width="256" height="256" alt="lupa" src="https://github.com/user-attachments/assets/686ccfb0-691f-46b3-951b-e556cdb84ca0" /> |
| Cigarette | `cigarette` | Reroll the current dice | <img width="256" height="256" alt="cigs" src="https://github.com/user-attachments/assets/4cf76e80-085b-4033-817d-c3547a70837d" /> |
| Makarov | `gun` | Shoot a target — ignores safe squares (Russian roulette) | <img width="256" height="256" alt="makarov" src="https://github.com/user-attachments/assets/58121435-910f-4634-9cd7-c0c432f1e1e5" /> |

Items are acquired through the golden square roulette. A player can hold multiple items.

---

## Characters

[IMAGES - characters]

| Skin ID | Character |
|---------|-----------|
| 101 | Main Character (default) |
| 102 | Killer |
| 103 | Goth |
| 104 | Clown |
| 105 | Black Dude |
| 106 | Female Police Officer |

---

## Protocol

Server: `bolty.website:8888` (TCP)

### Request Types (Client → Server)

| Code | Name | Status |
|------|------|--------|
| 1 | REQ_REGISTER | Done |
| 2 | REQ_LOGIN | Done |
| 3 | REQ_CHANGE_SKIN | Done |
| 4 | REQ_LOGOUT | Done |
| 5 | REQ_JOIN_ROOM | Done |
| 6 | REQ_SEND_CHAT | Done |
| 7 | REQ_GAME_ACTION | Done |
| 8 | REQ_LEAVE_ROOM | Done |
| 9 | REQ_CONNECT_LIVE | Done |

### Push Message Types (Server → Client)

| Code | Name |
|------|------|
| 10 | MSG_USER_LIST |
| 11 | MSG_CHAT |
| 12 | MSG_ROOM_STATE |
| 13 | MSG_COUNTDOWN |
| 14 | MSG_GAME_START |
| 17 | MSG_GAME_ACTION |

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

### Game Action Flow

```
[game_start] → server starts Ophanim sequence / chair selection


-- Chair selection --

Client  → choose_chair    { action, color }
Server  → chair_taken     { action, color, user_id, username }
Server  → chairs_locked   { action }


-- Initiative sequence --

Server  → initiative_sequence { action, turn_order:[user_id,...],
                                item_grants:[{user_id, items:[...]},...],
                                golden_squares:[sq,sq,sq,sq] }


-- Normal turn --

Server  → turn_start      { action, user_id }
Client  → roll_dice       { action, die1, die2 }
Server  → dice_result     { action, user_id, die1, die2, total,
                            moveable_pieces:[0-3,...],
                            can_exit_house:bool,
                            is_doubles:bool,
                            consecutive_doubles:N }
                           (empty moveable_pieces: server auto-skips)

Client  → move_piece      { action, piece_id }
Server  → piece_moved     { action, user_id, piece_id, from, to,
                            is_exit:bool, on_safe_square:bool }


-- Follow-up events (after piece_moved) --

Server  → capture              { action, attacker_user_id, victim_user_id,
                                 piece_id, square, bonus_moves:20 }
Server  → goal_scored          { action, user_id, piece_id,
                                 pieces_in_goal:N, bonus_moves:10 }
Server  → golden_square_event  { action, user_id, square,
                                 result:"item"|"click", item:name|null }
Server  → barrier_formed       { action, user_id, square }
Server  → barrier_broken       { action, user_id, square }


-- Extra turn --

Server  → extra_turn      { action, user_id, reason:"doubles"|
                            "capture_bonus"|"goal_bonus", pending_moves:N }
           doubles   → continues with new turn_start (same user_id)
           bonus     → player moves pending_moves extra points


-- Triple doubles penalty --

Server  → triple_double_penalty { action, user_id, piece_id }
Server  → life_lost             { action, user_id, lives_remaining }
Server  → turn_end              { action, user_id, next_user_id }
Server  → turn_start            { action, user_id }   ← next player


-- Normal turn end --

Server  → turn_end        { action, user_id, next_user_id }
Server  → turn_start      { action, user_id }


-- Handcuff skip (in place of turn_start) --

Server  → handcuff_skip   { action, user_id }


-- Turn timer --

Server  → turn_timer_warning  { action, seconds_remaining }
Server  → turn_timer_expired  { action, user_id }


-- Item use --                                         [TOBEDONE - client UI]

Client  → use_gun              { action }
Server  → gun_available        { action }              (private)
Server  → gun_result           { action, ... }

Client  → use_cigarette        { action }
Server  → cigarette_result     { action, die1, die2 }

Client  → use_magnifying_glass { action }
Server  → magnifying_glass_used { action }
Server  → peek_result          { action, die1, die2 }  (private)

Client  → use_handcuffs        { action, target_user_id }
Server  → handcuffs_applied    { action, target_user_id }

Client  → use_fire_axe         { action, target_square }
Server  → fire_axe_available   { action }              (private)
Server  → barrier_destroyed    { action, square }


-- Player elimination --

Server  → player_eliminated { action, user_id }


-- Game over --

Server  → game_over       { action, reason:"race", winner_user_id }
```

---

## Credits

- **[sodaraptor](https://sodaraptor.itch.io/)**
- **[elbolilloduro](https://elbolilloduro.itch.io/)**
- **[binbun3d](https://binbun3d.itch.io/)**
- **[ggbot](https://ggbot.itch.io/)**
- **[arlez80](https://godotengine.org/asset-library/asset?user=arlez80)**
- **[doctor-sci3nce](https://doctor-sci3nce.itch.io/)**
- **[youpzdev](https://sketchfab.com/youpzdev)**
- **[pepperonijabroni](https://pepperonijabroni.itch.io/)**

---

## Authors

- **David Garcia**
- **Eric Menaya**
- **Xavi Guillamon**
