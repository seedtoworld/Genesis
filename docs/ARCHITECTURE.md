This document describes the internal architecture of **Genesis**, a procedural pipeline system.

The goal of this document is to help understand:
- the core systems of **Genesis**
- how generators interact
- how world data flows through the pipeline
- how new generators can be added

Genesis is designed as a **modular procedural pipeline system** where generation occurs through a sequence of generators operating on a shared world state.

## High-Level Architecture

> Generators must only communicate through the World State

```
					   CLI
						|
						▼
					Config/Asset Loader
						|
						▼
					Generation Pipeline
						|
						▼
					World State
						|
						▼
					Export System
```

### 1. CLI Layer

- Entry point of Genesis
- Parses commands like:
	`genesis generate --rules world.yaml --assets ./assets --output world.json`
- Responsible only for:
	- argument parsing
	- triggering pipeline

### 2. Config/Asset System

- Loads the assets
- Loads YAML rules
- Defines:
	- world parameters
	- generator settings
	- asset metadata

### 3. Generator Pipeline

- Core execution system
- Runs generators in sequence
Example: 
	`Terrain -> Rivers -> Biomes -> Vegetation -> Settlements -> Roads`

Each generator:
- reads from `WorldState`
- write to `WorldState`

### 4. WorldState (Core Data Model)

- Central shared data structure
- Represents the entire world

Example contents:
- heightmap (2D grid)
- biome map (2D grid)
- rivers (list of paths)
- object (trees, houses, etc..)

### 5. Export System

- Converts `WorldState` into:
	- JSON (initial)
	- PNG (visual debug)
	- Godot Scene

## Tech Stack (Stage 1)

**Language**: C++ (might change to Rust later)
**Libraries**:
- CLI Parsing -> `CLI11` or `cxxopts`
- YAML parsing -> `yamp-cpp`
- JSON export -> `nlohmann/json`
- Noise -> `FastNoiseLite`
- PNG export -> `stb_image_write`
**Build System**: `Cmake`

**Project Structure**:
```
genesis/
├── src/
│   ├── core/          # WorldState, base systems
│   ├── generators/    # terrain, rivers, etc.
│   ├── pipeline/      # execution logic
│   ├── config/        # YAML parsing
│   ├── export/        # JSON, PNG
│   └── cli/           # entry point
│
├── include/
├── assets/            # test assets
├── examples/          # sample configs
├── tests/
└── docs/
```

## Low - Level Architecture (Stage 1)

### WorldState (core)

```c++
struct WorldState {
	int width;
	int height;
	
	std::vector<float> heightmap;  // 2D grid
	std::vector<int> biome_map;    // 2D grid
	
	std::vector<River> rivers;     // path or graph
	// added as needed
};
```

Helper access:
```c++
float &height(int x, int y);
float &width(int x, int y);
```

### Generator Interface

```c++
class Generator {
public:
	virtual void generate(WorldState& world) = 0;
	virtual ~Generator() = default;
};
```

### Pipeline System

```c++
class Pipeline {
public:
	void add(std::unique_ptr<Generator> gen);
	void run(WorldState& world);

private:
	std::vector<std::unique_ptr<Generator>> generators;
};
```

### Config System

YAML -> structs

YAML example:
```yaml
world:
	width: 512
	height: 512

terrain:
	scale: 0.01

biomes:
	- type: grass
	  min_height: 0.2
```

Parsed into:
```c++
struct Config {
	WorldConfig world;
	TerrainConfig terrain;
	BiomeConfig biome;
};
```

### Generators

```c++
class ExampleGenerator : public Generator {
public:
	void generate(WorldState &world) override;
};
```

### Biome

```c++
class BiomeGenerator : public Generator {
public:
	void generate(WorldState &world) override;
};
```

### Exporters

```c++
class Exporter {
public:
	virtual void export_world(const WorldState &world) = 0;
};
```