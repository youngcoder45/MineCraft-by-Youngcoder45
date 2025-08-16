# 🧱 Minecraft in Python (Pyglet)

A simple, playable **Minecraft-like 3D block world** built with **Python** and **pyglet**.
This project recreates the core feel of block building and exploration: place and remove blocks, walk/fly around, and enjoy a small procedurally-generated world. It’s a great learning project for 3D graphics, game loops, and input handling.

---

## 🔎 What this is

* A compact Python implementation of a block-based world (in the spirit of Minecraft).
* Uses **pyglet** for windowing, OpenGL bindings, and rendering.
* World is generated with layers, outer walls, and random hills.
* Player can move, jump, fly, place blocks, and remove blocks.

This code is ideal as a learning/demo project — study it to learn how rendering, collision detection, sectors, and input work in a simple 3D game.

---

## ✅ Features

* First-person 3D movement (walk & fly).
* Physics: gravity, jumping, terminal velocity.
* Block placement and removal (hit test + add/remove).
* Simple textured blocks (grass, sand, brick, stone).
* Sector-based rendering for performance (only nearby blocks are rendered).
* Crosshair, FPS + position label.
* Procedural hills for variety.

---

## ⚙️ Requirements

* **Python 3.8+** (recommend latest Python 3)
* **pyglet** — used for windowing, input, assets and OpenGL bindings.

Install pyglet with pip:

```bash
pip install pyglet
```

You must also have working GPU drivers and OpenGL support (OpenGL 2.0+ recommended). On Linux you may need system packages like `libgl1-mesa-glx` or similar depending on distribution.

---

## 📁 Project structure

(Adapt names if you renamed the file.)

```
minecraft-in-py/
├── main.py                 # main game file (the code you shared)
├── texture.png             # block texture atlas (required)
├── README.md
```

> **Important:** `texture.png` must be present in the same directory as the script, since the code loads `TEXTURE_PATH = 'texture.png'`.

---

## ▶️ How to run

1. Clone or download the repo.
2. Ensure `texture.png` is present.
3. Install pyglet: `pip install pyglet`
4. Run the game:

```bash
python main.py
```

(If your file has a different name, replace `main.py` accordingly.)

---

## 🎮 Controls

* `W` / `A` / `S` / `D` — Move forward / left / back / right
* `SPACE` — Jump
* `TAB` — Toggle flying mode
* `Mouse` — Look around (move the mouse)
* `Left click` — Remove block (when pointing at one)
* `Right click` — Place block (places the selected block at the aimed spot)
* `1` / `2` / `3` / ... — Cycle block types (numbers choose from inventory array)
* `ESC` — Release mouse / show cursor (press again to capture)

---

## 🧩 How the code is organized (brief)

* `Model` class — world data, block add/remove, shown blocks, sectors, and batch rendering.
* `Window` class — player state, input handlers, movement, collisions, and on-draw logic.
* Utility functions: `cube_vertices`, `tex_coords`, `normalize`, `sectorize`.
* The world is split into sectors (defined by `SECTOR_SIZE`) for efficient rendering. Showing/hiding sectors is done when the player moves.

---

## 🛠 Customization & Hacks

You can easily tweak and experiment:

* **Change world size**
  Modify the `n` variable in `Model._initialize()` to increase/decrease world half-width.

* **Add new block textures**
  Edit `texture.png` and update `GRASS`, `SAND`, `BRICK`, `STONE` texture coordinates with `tex_coords()`.

* **Change walking/flying speed**
  Adjust `WALKING_SPEED` and `FLYING_SPEED` constants.

* **Adjust gravity / jump**
  Tweak `GRAVITY`, `MAX_JUMP_HEIGHT`, and `JUMP_SPEED`.

* **Reduce rendering load**
  Decrease `SECTOR_SIZE` or reduce `n` to render fewer blocks at a time.

* **Change fog / draw distance**
  Modify `setup_fog()` fog start/end (`glFogf(GL_FOG_START, ...)`) to visually limit distance.

Example: to add a new texture constant:

```py
NEW_BLOCK = tex_coords((3,0), (3,1), (3,0))
# and add to inventory: self.inventory.append(NEW_BLOCK)
```

---

## 🧪 Troubleshooting

* **ImportError: No module named pyglet** — run `pip install pyglet`.
* **Black/Blank window or crash on startup** — likely OpenGL/driver issue. Update GPU drivers. On Linux, make sure system OpenGL libs are installed.
* **texture.png not found** — ensure file exists in same folder or update `TEXTURE_PATH`.
* **Low FPS / slow** — reduce world size (`n`), reduce sector pad, or lower `TICKS_PER_SEC`. Also close other GPU-heavy apps.
* **Mouse not captured or movement not working** — ensure the window has focus and call `window.set_exclusive_mouse(True)` by clicking into the window. ESC releases the mouse.

---

## ⚠️ Known limitations

* No networking / multiplayer — single player only.
* No persistence — world is generated fresh each run.
* Basic collision handling — good for demo but not a complete physics system.
* No sophisticated lighting — just basic fog and textures.
* Tiles/texture atlas layout is assumed to match the constants; if your texture atlas differs, you must change `tex_coords` calls.

---

## 🔧 Useful development tips

* Use an editor with Python linting to navigate functions.
* Use small world sizes while testing (reduce `n`) for faster iteration.
* For debugging, print player position and sector info from `draw_label()` or add logging statements.
* To export a screenshot, call `pyglet.image.get_buffer_manager().get_color_buffer().save('screenshot.png')` from a hotkey handler.

---

## 🤝 Contributing

Contributions are welcome:

* Bug fixes and performance improvements
* New block types and textures
* Save/load world feature
* GUI or menus to toggle settings

Please fork, create a feature branch, and open a pull request describing the change.

---

## 📜 License

This project is released under the **MIT License** — free to use and modify.

---

## ❤️ Credits

* Inspired by the classic sandbox gameplay of Minecraft.
* Built using **pyglet** — [http://pyglet.org](http://pyglet.org)
* Made by Aditya - @youngcoder45
