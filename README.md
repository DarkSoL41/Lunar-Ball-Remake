# Lunar Ball (NES) — Remake + Level Editor

A fan-made remake of the classic NES billiards game **Lunar Ball (J)**, written in
C++20 + SDL2, together with a **level editor** for it. The game logic is ported
1:1 from the original ROM (verified against a tracing-emulator oracle), the
graphics use the real NES tiles and palette, and the audio is an accurate
emulation of the NES 2A03 sound chip.

## Contents of this folder

| File                 | Description                                  |
|----------------------|----------------------------------------------|
| `launcher.exe`         | **Start here** — settings and the PLAY button |
| `lunarball-remake.exe` | The game                                    |
| `editor.exe`           | The level editor                            |
| `README.md`            | This file                                   |
| `levels.dat`           | Data for all 60 levels (v2, per-cell palette) |
| `lunarball.ini`        | Your settings (created by the launcher)     |
| `editor.ini`           | The editor's window and tool state (created by the editor) |
| `levels_original.dat`  | The 60 original tables, never changed       |
| `SDL2.dll`             | Runtime library (all three programs)        |

---

## The Launcher

Run `launcher.exe`, change what you like and press **PLAY**. Settings are saved
automatically to `lunarball.ini` next to the game; delete that file to get the
defaults back. The game also runs fine on its own without the launcher.

| Page         | What you can set |
|--------------|------------------|
| **Controls** | Keyboard keys (two per action) and gamepad buttons for Player 1 and Player 2, left stick + dead zone, hotkeys, with a live input test |
| **Audio**    | Master volume, mute, NES channel mixer (pulse 1/2, triangle, noise), soft filter, latency — plus a sound test that plays every tune and effect of the game |
| **Video**    | Window / fullscreen, window size, pixel shape (square, NES TV 8:7, stretch), sharp or smooth scaling, whole-number scaling, overscan, scanlines, v-sync — with a preview |
| **Colours**  | NES palette: Classic, NTSC TV, black & white, or any emulator `.pal` file from the `palettes` folder; brightness / contrast / saturation / hue / gamma; repaint any of the 64 colours — with a live preview of the title, menu and every table |
| **Game**     | Interface size, light / dark theme (or follow the system), pause when the window is inactive, shortcut to the level editor |

In a 2-player game Player 2 plays with the Player 2 bindings on their turn (and,
if you leave the option on, with Player 1's as well — handy on one keyboard).

## The Game

### Controls

These are the defaults; everything can be rebound in the launcher.

| Key         | Action                                      | Notes |
|-------------|---------------------------------------------|-------|
| **X**       | Button A                                    | Hit / shoot |
| **Z**       | Button B                                    |       |
| **Shift**   | Button Select                               | Cycle mode |
| **Enter**   | Button Start                                | Confirm |
| **Up / Down** | D-pad Up / Down                          | Cue length |
| **Left / Right** | D-pad Left / Right                   | Cue rotation |
| **Esc**     | Quit                                        |       |
| **P**       | Pause                                       |       |
| **Tab** (hold) | Fast-forward                             | Speed is set in the launcher |
| **F11** / **Alt+Enter** | Fullscreen on / off             |       |
| **F12**     | Screenshot                                  | Saved to `screenshots\` |
| **M**       | Mute                                        |       |

Player 2 defaults: **W A S D** (D-pad), **G** (A), **F** (B), **R** (Start), **Q** (Select).
Gamepads work out of the box: D-pad / left stick, A or B to shoot, Start, Back.

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
- The audio is quieter than the original by default (30% master volume) for
  comfortable play; change it on the launcher's Audio page.

---

## The Level Editor

Run `editor.exe` (or press **Open the level editor** in the launcher). It opens
`levels.dat` next to it — the 60 tables the game plays.

You do not paint tiles. You draw the table the way the original game describes
it — **rail cells** (full or diagonal halves), **felt**, **pockets** and
**balls** — and the editor builds the rail graphics and the bounce map with a
port of the original game's own table builder. An edited table therefore looks
and plays like an original one. **Test play (F5)** runs the real game on your
level inside the editor, in 1P, 2P or vs CPU.

### Tools

| Key | Tool | What it does (right mouse button = the opposite) |
|-----|------|--------------------------------------------------|
| **V** | Select | Drag balls and pockets; drag on the table to select cells, then copy / cut / paste / delete |
| **W** | Wall | Paint rail cells (brush 1–3) |
| **D** | Diagonal | Half cells for 45° rails; the solid half follows the cursor or is chosen by hand |
| **L** | Line | Drag a straight or 45° rail, 1 or 2 cells thick, built like the original diagonal rails |
| **R** | Rectangle | Drag a complete table (rail frame + felt), a rail frame, a solid block or a patch of felt |
| **F** | Felt | Paint felt / open space |
| **G** | Fill | Flood-fill an enclosed area with felt |
| **P** | Pocket | Add pockets (up to 16); they cut through rails by themselves |
| **B** | Ball | Place the cue ball and balls 1–7 (**0**–**7** pick one), drag to move, arrow keys nudge |
| **E** | Erase | Remove rails, pockets and balls under the brush |

**Mirror** (left-right, up-down, both) repeats everything you draw on the other
side — handy for symmetrical tables.

### Everything else

| Action | Keys |
|--------|------|
| Zoom / move the view / fit | mouse wheel, **+** **-** / middle button or **Space**+drag / **Home** |
| Undo / redo | **Ctrl+Z** / **Ctrl+Y** |
| Copy, cut, paste cells | **Ctrl+C**, **Ctrl+X**, **Ctrl+V** — while pasting **H** / **V** flip, **R** rotates |
| Previous / next level, all levels | **Page Up** / **Page Down**, **Ctrl+L** |
| Grid, physics map | **F2**, **F3** |
| Test play | **F5** (Esc returns, **P** pauses, **F6** restarts) |
| Save, save as, open, new | **Ctrl+S**, **Ctrl+Shift+S**, **Ctrl+O**, **Ctrl+N** |
| All shortcuts | **F1** |

- The panel on the right names the level, copies / pastes / flips / shifts whole
  tables, brings back the original table, lists the balls and runs a **Check**:
  balls inside rails or on pockets, unreachable balls, hidden pockets, felt with
  no rail next to open space. Click a line to see the spot.
- The **physics map** (F3) shows what the ball really bounces off: red = solid
  rail, gold = cushion face, blue = pocket / drop.
- **Theme:** Dark by default; Auto / Dark / Light at the bottom of the window. Auto follows the
  Windows app mode; the choice is shared with the launcher.
- Test play uses the keys, gamepads, volume and palette you set in the launcher.
- The editor remembers its window size and position, zoom, tool options and the
  last file and level in `editor.ini`; delete that file to start fresh.
- Saving keeps a `levels.dat.bak` of the previous file. `levels_original.dat`
  always holds the untouched 60 tables; **New** in the editor also restores them.
- The file stays readable by older builds: the editor's own data (rail shapes,
  level names, the pocket list the CPU player aims at) is appended as an extra
  block that older readers ignore.

---

## Author

**Remake and level editor:** DarkSoL  
**Discord:** darksol41

---

## Legal

This is an unofficial, free, non-commercial fan project. It is not affiliated with or
endorsed by Compile, Pony Canyon or any other rights holder of *Lunar Ball* /
*Lunar Pool*.

*Lunar Ball* © 1985 Pony Inc., game designed by Compile. The game's name, graphics,
level layouts, texts and music belong to their respective owners.

**What is in this package.** The program code of the remake and the editor is my own.
To look and play like the original, the remake contains graphics (tiles and palettes),
level layouts (`levels.dat`) and on-screen texts taken from the original game. They
are included for preservation and study only.

**Third-party libraries.** `SDL2.dll` is distributed under the zlib
license (https://www.libsdl.org). The launcher and the editor embed the Inter typeface (SIL Open Font
License 1.1, https://rsms.me/inter/) and use stb_truetype (public domain). `libstdc++-6.dll`, `libgcc_s_seh-1.dll` and
`libwinpthread-1.dll` are the MinGW-w64 runtime libraries.

No warranty of any kind. If you are a rights holder and want something changed or removed, contact me on Discord (`darksol41`) and I will do it.
