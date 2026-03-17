## Ideal Philosophy

The workflow should follow **four simple stages**:
`Assets -> Rules -> Generation Graph -> Output`

That's it!

Users should never need to understand the internal algorithms unless they want to (look at the repo).

## Step 0 - Choose Seed

The developer first defines a seed.
`seed: 8931`

This ensures:
- deterministic worlds
- reproducibility
- debugging
- multiplayer synchronization

If the user does not specify a seed, Genesis generates a random one.
## Step 1 - Import Assets

The developer provides the building blocks:
```
assets/
  trees/
    oak.png
    pine.png
  rocks/
    rock1.png
  houses/
    house1.png
    house2.png
  roads/
    dirt_road.png
```

Our system should automatically categorize assets like:
```
vegetation
structures
terrain
decorations
```

If automatic categorization fails, users can manually define asset metadata.
```
assets.yaml

oak:
  type: vegetation
  biome: forest

rock1:
  type: decoration

house1:
  type: structure
```

Genesis will prioritize **explicit metadata over automatic classification**.
## Step 2 - Define World Rules

This is the **core innovation**.

Instead of writing code, users define rules.

Example rule file:
```
biomes:
  forest:
    vegetation: [oak, pine]
    density: high

  plains:
    vegetation: [grass]
    density: medium
```

Placement rules:
```
village:
  houses: 20-40
  near: water
  connect_with: road

trees:
  avoid: roads
  cluster_size: 5-20
```

## Step 3 - Generation Pipeline

Users select generators like modules.

Generators run sequentially. Later generators depend on previous results.
Example pipeline:
```
Terrain -> Rivers -> Biomes -> Vegetation -> Settlements -> Roads
```

Each generator receives the **current world state** and modify it.

Internally this could use:
- noise
- graphs
- constraint solving

But the user doesn't care.

## Step 4 - Tuning

Now the users tweaks parameter. There should be some presets but the user's will have control to tweak manually.

Example:
```
terrain:
  roughness: 0.6
  mountain_density: 0.2

rivers:
  count: 4

villages:
  density: low
```

## Step 5 - Output

Genesis exports to any target engine.

Possible Output:
```
Godot scene
Unity scene
Unreal map
JSON world file
tilemap
heightmap
```

We have to support:
- Godot (main priority)
- Unity
- Unreal Engine
- As data

## Optional Advanced Workflow (Power Users)

Advanced users can build **generation graphs**.

Example:
```
Noise → Heightmap → Biomes
Biome → Vegetation
Heightmap → Rivers
Villages → Roads
```

This becomes a **node system** similar to tools like *Houdini* but simpler.

# Example End-To-End Workflow

Imagine a developer wants a **fantasy forest world**.
#### Step 1
Import assets:
```
tree.png
pine.png
rock.png
house.png
road.png
```
#### Step 2:
Define rules:
```
forest:
  trees: [oak, pine]
  density: high

village:
  houses: 10-20
  near: river
```
#### Step 3:
Choose modules:
```
terrain
rivers
biomes
vegetation
settlements
roads
```
#### Step 4:
Press generate.

Our tool produces:
```
terrain
river network
forests
village
road connections
```