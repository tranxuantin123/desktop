Bạn là Lead Developer + Game Designer. Hãy tạo một project game 2D top-down tên "Ngôi Làng Của Gió" (Windy Village) theo yêu cầu CHI TIẾT dưới đây. Stack bắt buộc: TypeScript + Phaser 3. Mục tiêu: HTML5 playable + PWA (manifest + service-worker), responsive, playable trên iOS Safari & Android Chrome (touch joystick + touch buttons + keyboard fallback). Trả về 1 file ZIP chứa toàn bộ project, assets placeholder, demo media (MP4 hoặc GIF fallback), và README hướng dẫn.

PHẦN A — YÊU CẦU CHUNG
- Thể loại: farming + adventure + light RPG + social-lite.
- Canvas responsive (autoscale) — mục tiêu ~60 FPS trên thiết bị tầm trung.
- Input: touch (joystick analog + buttons A/B/X/Y), keyboard fallback (WASD/Arrows + E interact + I inventory). Có nút "Enable Sound" để vượt autoplay iOS.
- Code: TypeScript modules, rõ types/interfaces, comment đầy đủ.

PHẦN B — SCENES (bắt buộc)
- Scenes: Boot, Preload, Title, Farm (demo), Village (demo), Forest (demo), River/Fishing, Festival (demo).
- Tilemap: dùng Tiled JSON format; camera follow player; warp/door transition giữa scenes.

PHẦN C — HỆ THỐNG THỜI GIAN & THỜI TIẾT
- 1 day = 10 real minutes; 4 seasons (Spring, Summer, Autumn, Winter), mỗi season = 10 days.
- Weather types: Sunny, Rain, Windy, Storm, Snow.
  - Rain auto-waters plants.
  - Storm may damage crops/fences.
  - Wind reduces stamina cost & triggers leaf particles.
  - Snow increases animal food consumption.
- Day/night cycle: overlay tint + light radius around player at night.

PHẦN D — PLAYER, CONTROLS, STATS
- Player: 8-directional movement; animation sheet 4 directions × 3 frames.
- Stats: HP, Stamina, EXP/Level, Skill points (Farming, Fishing, Cooking, Friendship).
- Mobile controls: left joystick (analog) + right buttons:
  - A = Action/Interact/Use tool
  - B = Open Inventory
  - X = Skill (Wind Blast)
  - Y = Dash/Dodge
- Desktop: WASD/Arrows + E interact, I inventory, 1/2 skills.

PHẦN E — FARMING & ANIMALS
- Farming flow: Hoe → Plant seed → Water (or rain) → Multiple growth stages → Harvest.
- Crops defined in `crops.json` with fields: id, name, seedItemId, stages, minutesPerStage, seasons[], waterNeededPerDay, sellPrice.
- Fertilizer speeds growth; rain counts as water.
- Animals: Chicken (egg), Cow (milk), Sheep (wool) — have affection and daily feed requirement. Higher affection => higher yield.

PHẦN F — NPC, QUESTS, SOCIAL
- 6 demo NPC with schedule (morning/afternoon/evening) and weather/season-dependent dialogues.
- Quest system: `quests.json` supports steps types: collect, plant, talk, kill, craft; rewards: gold/items/recipes.
- Friendship: gifting increases friendship; thresholds unlock quests/recipes.
- Social-lite: ability to "visit" friend farm locally (demo only, no backend).

PHẦN G — MINIGAMES & FESTIVAL
- Fishing: tap to cast, hold to control tension/timing bar; success depends on Fishing skill & timing.
- Cooking: drag-and-drop recipe UI producing consumables (HP/Stamina restore).
- Festival "Day of Wind": kite mini-game controlled by swipe gestures; scoring rewards items/cosmetics.

PHẦN H — LIGHT COMBAT & EXPLORATION
- Enemies: SlimeWind, WindWolf in Forest. Basic attack + skill (knockback). Drops: wood, stone, wind crystal.
- Simple respawn + loot table.

PHẦN I — INVENTORY & CRAFTING
- Inventory grid 5×6, stackable items. Chest/storage persists.
- Crafting uses `recipes.json`. Example: Flour + Egg => Wind Cake (stamina restore).
- Drag-and-drop UI + hotbar (4 quick-use slots).

PHẦN J — SAVE / LOAD / EXPORT
- Save namespace: "windy_village_save_v1" in `localStorage`.
- Auto-save at end of day and manual save button.
- Export/Import save as JSON for backup/share.

PHẦN K — ASSETS & MEDIA (bắt buộc xuất kèm)
- Provide placeholder pixel-art PNGs (transparent background):
  - Player sprite-sheet: frame 32×48 px, 4 dirs × 3 frames → `player.png`.
  - 4 NPC sprite-sheets: 32×48 frames.
  - Crops: Wind Grain stages 0..3, each 32×32 → `windgrain_stage0.png` ... `_stage3.png`.
  - Animals: chicken, cow, sheep sprites (idle + produce), ~48×48.
  - Tileset: 32×32 tiles (grass, dirt, water, fence, house, path).
  - UI: joystick.png, btn_A.png, btn_B.png, inventory icons 64×64.
  - Particles: rain.png (tile), leaf.png, snowflake.png.
- Mockups (full-HD PNGs 1920×1080):
  - `Farm_overview.png`, `Village_overview.png`, `Festival_mockup.png`, `UI_HUD.png`.
- Demo media:
  - `demo_day.mp4` ~60s (H.264 1280×720) showing: walk → plant → water → time-lapse growth → harvest → short NPC dialog overlay HUD.
  - `demo_fishing.mp4` ~20s fishing minigame.
  - `demo_festival.mp4` ~30s festival kite minigame.
  - `demo_mobile_controls.mp4` ~20s showing joystick + touch buttons on iOS Safari.
  - If MP4 cannot be produced, include GIF fallbacks ≤10MB and a short README explaining how to record MP4 locally (QuickTime for iOS or Chrome remote).

PHẦN L — PWA & BUILD
- Include `manifest.json` (name, short_name, icons, start_url, display: standalone, theme_color).
- `service-worker.js` with basic precache of built assets and runtime caching for images; offline fallback page.
- npm setup: `package.json`, `tsconfig.json`, vite (or webpack) config. Scripts:
  - `npm run dev` (dev server)
  - `npm run build` (prod build)
  - `npm run serve` (serve built files)
- README must document: dev/build/deploy, iOS Add-to-Home-Screen steps, audio autoplay specifics, known limitations.

PHẦN M — CODE & STRUCTURE (bắt buộc)
Root ZIP must include:
- /src
  - /scenes (Boot.ts, Preload.ts, Title.ts, Farm.ts, Village.ts, Forest.ts, River.ts, Festival.ts)
  - /systems (TimeSystem.ts, WeatherSystem.ts, FarmingSystem.ts, AnimalSystem.ts, InventorySystem.ts, QuestSystem.ts, SaveSystem.ts, UISystem.ts)
  - /ui (Joystick.ts, TouchButtons.ts, HUD.ts, InventoryUI.ts)
  - /data (items.json, crops.json, quests.json, recipes.json, i18n/en.json, i18n/vi.json)
  - /utils (helpers)
  - main.ts (bootstrap)
  - index.html
- /assets (images/audio)
- /pwa (manifest.json, service-worker.js)
- package.json, tsconfig.json, vite.config.js (or webpack)
- README.md
- /demos (mp4/gif)
- /mockups (png)
- Optional: tests folder with unit/integration/e2e

PHẦN N — DỮ LIỆU MẪU (bắt buộc)
Include these sample JSONs (exact content):

items.json
[
  {"id":1,"name":"Wind Grain Seed","type":"seed","stack":99,"price":5},
  {"id":2,"name":"Wind Grain","type":"crop","stack":99,"price":20},
  {"id":3,"name":"Egg","type":"food","stack":30,"price":10},
  {"id":4,"name":"Flour","type":"material","stack":99,"price":8}
]

crops.json
[
  {"id":1,"seedItemId":1,"name":"Wind Grain","stages":4,"minutesPerStage":2,"seasons":["Spring","Summer"],"waterNeededPerDay":1,"sellPrice":20}
]

quests.json
[
  {"id":1,"title":"Welcome to Windy Village","steps":[{"type":"collect","itemId":2,"count":3},{"type":"talk","npcId":101}],"rewards":{"gold":100,"items":[3]}}
]

recipes.json
[
  {"id":1,"name":"Wind Cake","inputs":[2,3],"output":{"id":5,"name":"Wind Cake","type":"food","stack":10},"staminaRestore":30}
]

PHẦN O — ACCEPTANCE CRITERIA (QA)
Project must satisfy:
1. Player can plant Wind Grain Seed, water it (or let rain happen), see growth stages and harvest Wind Grain item.
2. Fishing minigame playable with touch + keyboard.
3. NPCs move by schedule and dialogues change by weather/season.
4. Save/Load restores crops, inventory, NPC friendship, time/day.
5. PWA installable (manifest + service-worker) and cached assets load offline.
6. Demo images + at least GIF demos included (MP4 preferred).

PHẦN P — TESTS, CI, LOCALIZATION, MARKETING (bonus but desired)
- Provide unit tests (Jest) for FarmingSystem and SaveSystem with `npm run test`.
- Provide E2E (Playwright) sample that simulates planting & harvesting on mobile viewport.
- GitHub Actions workflow: run tests on PR, build on push to dev, release on tag (artifact = zip).
- i18n files: `/data/i18n/en.json` and `/data/i18n/vi.json` with HUD strings and 10 sample quest titles/descriptions.
- Provide 3 short store copy texts (EN/VI) and 3 suggested social captions.

PHẦN Q — DELIVERY & FALLBACK
- Deliverable: 1 ZIP with full project. If tool cannot produce MP4s or high-res PNGs, produce GIF fallback files and include explicit instructions to record high-quality MP4s locally (exact steps for QuickTime on Mac and Chrome Remote Debugging for iOS). If images cannot be hand-drawn, generate procedural placeholder PNGs (programmatic sprites) and include generator script.

GHI CHÚ KỸ THUẬT (to help generator)
- Sprite dims: player frame 32×48; tileset 32×32; UI icons 64×64.
- Mockups: PNG 1920×1080.
- Video spec: MP4 H.264 1280×720, 20–60s per demo.
- Save key: "windy_village_save_v1".

KẾT THÚC: Trả về 1 file ZIP có đúng cấu trúc trên, kèm README giải thích các phần chưa có (nếu có) và hướng dẫn hoàn thiện bước còn thiếu. Nếu có bất kỳ phần nào không thể thực hiện, liệt kê rõ phần thay thế đã tạo (ví dụ GIF thay MP4; procedural sprites thay art), và hướng dẫn chi tiết để người dùng tự hoàn thiện.