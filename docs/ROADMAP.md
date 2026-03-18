## Stage 1 – The First Step: A Usable 2D World Generator for Godot

**Goal:** Deliver a polished, useful tool for Godot developers that generates 2D tile-based worlds from simple rules. This stage proves the core value proposition and builds an initial user base.

### Phase 0 – Foundation & Community Kickoff *(Month 1)*

- [x] Set up public GitHub repository with MIT license.
- [x] Create basic README, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`.
- [x] Establish Discord server for early users/contributors.
- [x] Draft initial design docs (already done – refine based on feedback).
- [x] Choose tech stack and document decision.

**Deliverable:** Project is public with a welcoming space for community.

### Phase 1 – Core Engine Prototype *(Months 2–3)*

- [ ] Project scaffolding (CLI binary, core library separation).
- [ ] Define `WorldState` data structure (2D grid for height, biomes; lists for rivers, settlements, roads).
- [ ] Implement seed system (deterministic RNG).
- [ ] Create `Generator` trait/interface with `generate()` method.
- [ ] Build simple pipeline that runs generators sequentially.
- [ ] Configuration loader (YAML for rules and asset metadata).
- [ ] Basic logging and error reporting.

**Deliverable:** CLI that can read a config file, run an empty pipeline, and output a JSON dump of world state.

### Phase 2 – Basic World Generation *(Months 4–5)*

- [ ] Integrate a noise library (e.g., `fastnoise-lite`).
- [ ] **Terrain generator:** Produce heightmap (2D grid of floats) using Perlin noise.
- [ ] **River generator:** Simple erosion or pathfinding (place rivers from high to low).
- [ ] **Biome generator:** Map height + moisture (or just height) to biome IDs.
- [ ] Add simple visualization output: export heightmap as PNG, biome map as colored PNG.
- [ ] Unit tests for deterministic output.

**Deliverable:** CLI generates terrain with rivers and biomes; can visualize as images.

### Phase 3 – First Usable Tool *(Months 6–8)*

#### Phase 3A - Playable World

- [ ] **Asset system:** Scan asset folder, load metadata (YAML) mapping sprites to types/biomes.
- [ ] **Vegetation generator:** Place trees/rocks based on biome density, with avoidance rules (water, steep slopes).
- [ ] **Settlement generator:** Place villages near water (using rules like `near: river`, `count: 3`).
- [ ] **Road generator:** Connect villages with simple paths (A* on grid or Bezier curves).
#### Phase 3B - Godot Integration + Polish

- [ ] **Export JSON world**: Generate a `.json` with the data for the map
- [ ] **Small Godot plugin**: It reads the exported `.json` file and builds a scene.
- [ ] **Godot export:** Generate a `.tscn` file with:
  - TileMap layer for terrain (using tileset from assets).
  - Instanced scenes for trees, houses, roads.
- [ ] **CLI workflow:** `genesis generate --rules world.yaml --assets path/ --output world.tscn`
- [ ] Basic documentation: Getting Started guide, example project.

**Deliverable:** A Godot developer can drop in their sprites, write a simple rule file, and get a playable scene with terrain, forests, villages, and roads.

### Parallel Community Building *(Ongoing)*

- [ ] Complete Discord Setup!
- [ ] Post devlogs on Reddit (r/godot, r/proceduralgeneration), Twitter, and Discord.
- [ ] After Phase 2 post a visual proof on r/godot and r/proceduralgeneration.
- [ ] Create a simple landing page with screenshots and signup form.
- [ ] Release early alpha to gather feedback.
- [ ] Tag "good first issues" on GitHub to attract contributors.
- [ ] Engage with Godot YouTubers for potential coverage.
- [ ] Prepare a Godot Asset Library release for v1 launch.

---

## Stage 2 – Generator Ecosystem

**Goal:** Make Genesis extensible and algorithm-rich.

- [ ] Plugin architecture: load external generators (e.g., via WebAssembly or scripting).
- [ ] Add more PCG techniques:
  - Wave Function Collapse for dungeons/towns.
  - L-systems for road networks.
  - Cellular automata for caves.
- [ ] Rule system enhancements: conditional rules, constraints, priorities.
- [ ] Reusable rule packs (e.g., "fantasy biome pack").

**Deliverable:** Genesis becomes a flexible PCG toolkit; developers can write their own generators.

---

## Stage 3 – Visual Tooling

**Goal:** Make Genesis usable by non-programmers.

- [ ] Visual rule editor (biome configuration, placement rules).
- [ ] Pipeline graph editor (drag & connect generators).
- [ ] Live world preview (2D map with zoom/pan).
- [ ] In-browser preview via WebAssembly.
- [ ] Asset management UI (tag sprites, set metadata).

**Deliverable:** A standalone or web-based GUI for designing worlds without writing YAML.

---

## Stage 4 – Plugin & Ecosystem Platform

**Goal:** Turn Genesis into a platform for community-driven content.

- [ ] Official plugin registry.
- [ ] Generator packs (e.g., "modern city pack", "dungeon pack").
- [ ] World templates (shareable `.genesis` files).
- [ ] Asset pack integration (Itch.io, OpenGameArt).
- [ ] Monetization options for premium plugins (optional).

**Deliverable:** A thriving marketplace where users share and sell generators, rulesets, and assets.

---

## Stage 5 – Advanced Generation Systems

**Goal:** Generate complex, structured worlds with history and logic.

- [ ] City generation (zoning, buildings, roads).
- [ ] Faction territories and political boundaries.
- [ ] Procedural storytelling (quests, lore, NPCs).
- [ ] Ecosystem simulation (animal populations, resource distribution).
- [ ] Dungeon generation with puzzles and enemies.

**Deliverable:** Genesis generates entire game worlds with narrative and simulation depth.