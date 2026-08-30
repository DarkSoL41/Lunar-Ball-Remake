# Lunar Ball (NES) — Remake + Level Editor

A fan-made remake of the classic NES billiards game **Lunar Ball (J)**, written in
C++20 + SDL2, together with a **level editor** for it. The game logic is ported
1:1 from the original ROM (verified against a tracing-emulator oracle), the
graphics use the real NES tiles and palette, and the audio is an accurate
emulation of the NES 2A03 sound chip.

## Contents of this folder

| File                 | Description                                  |
|----------------------|----------------------------------------------|
| `lunarball-remake.exe` | The game                                    |
| `editor.exe`           | The level editor                            |
| `README.md`            | This file                                   |
| `levels.dat`           | Data for all 60 levels (v2, per-cell palette) |
| `SDL2.dll`             | Runtime library (both programs)             |
| `SDL2_ttf.dll`         | Runtime library (editor)                    |

---

## The Game

### Controls

| Key         | Action                                      | Notes |
|-------------|---------------------------------------------|-------|
| **X**       | Button A                                    | Hit / shoot |
| **Z**       | Button B                                    |       |
| **Shift**   | Button Select                               | Cycle mode |
| **Enter**   | Button Start                                | Confirm |
| **Up / Down** | D-pad Up / Down                          | Cue length |
| **Left / Right** | D-pad Left / Right                   | Cue rotation |
| **Esc**     | Quit                                        |       |

### How to play

1. On the title screen press **Enter** (Start).
2. In the menu: **Up / Down** selects the level, **Left / Right** adjusts
   friction, **Shift** (Select) cycles the mode (1P / 2P / CPU). Press **Enter**
   to start.
3. Aim with the arrow keys, then press **X** (A) to shoot and sink the colour
   balls.
4. You lose a ball of life on a miss, or when the cue ball is pocketed.

### Features

- Palette is stored **per cell** (one palette per 8×8 tile), unlike the NES
  (which shares a palette per 2×2 block) — so pieces are placed exactly 1×1,
  as drawn, and never bleed into neighbours.
- The audio is quieter (~80% below the original level) for comfortable play.

---

## The Level Editor

Edit the `levels.dat` levels, view only the table with the game's real graphics
(no game HUD), and save your changes.

### Controls

| Action                      | Keys / Mouse                                                    |
|-----------------------------|-----------------------------------------------------------------|
| **Ball** tool (place/select/move balls) | **1** or the **Ball** button                     |
| **Tile** tool (stamp a tile-set piece) | **2**, or click a tile in the right panel         |
| Stamp a tile (drag = pencil) | **LMB** + drag                                                |
| Erase a cell (felt) / remove a ball | **RMB**                                             |
| Scroll the tile-set          | Mouse wheel over the panel                                    |
| Toggle tile grid             | **G** or the **Grid** button                                  |
| Toggle physics (collision) overlay | **M** or the **Physics** button                          |
| Toggle pixel-perfect scale   | **P** or the **Pixel scale** button (on by default)           |
| Previous / next level        | **PgUp** / **PgDn**, or the **‹** / **›** buttons              |
| Drag a ball                  | **LMB** on a ball + drag                                      |
| Add a new ball               | Double-click on the felt, or **B**, or the **Add ball** button |
| Nudge the selected ball 1 px | Arrow keys                                                     |
| Remove a ball                | **RMB** on the ball (in Ball tool), or **Delete** / **Backspace** |
| Undo (up to 64 steps)        | **Ctrl+Z** or the **Undo** button                             |
| Save `levels.dat`            | **Ctrl+S** or the **Save** button                             |
| Quit                         | **Esc**                                                       |

### Tips

- The **TILE SET** panel on the right holds every real cell type that appears in
  the game, drawn with the actual game graphics (CHR tile + palette). Each entry
  is the smallest unit — a single 8×8 tile. For example, a full pocket is built
  from four such tiles.
- An unsaved-changes dialog appears before closing if there are pending edits.
- On launch the editor automatically finds `levels.dat` next to itself (in the
  same `release\` folder); you can also pass the file path as the first argument.

---

## Author

**Remake and level editor:** DarkSoL
**Discord:** darksol41
If you’d like to support me financially, BTC address: bc1qp476rmcaapl6n6xjvg2la50cfw3kwvxe8sj0m5
