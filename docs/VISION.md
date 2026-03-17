Procedural generation knowledge exists, but it's **fragmented**, **academic** or **engine-specific**
People jump between:
- noise tutorials
- random github repos
- research papers
- engine plugins

There's no **unified system** where a dev can say:
> "I want a medieval city with forests and rivers around it."

... and get a starting result.

That's what **Genesis** intends to solve. 
A dev can come in, 
- drop their assets in
- define some rules
- **Genesis** does it's thing
And they have their imagined build ready to tweak. This is powerful.

> **Genesis** is not just a procedural generator -- it is a **procedural pipeline system**.

But the **key to succeeding here is narrowing the first version**.

## THE DESCRIPTION

Pipeline Concept:
```
Assets
 ↓
Rules
 ↓
Generation Graph
 ↓
World
```

### Example Workflow:

Developer imports:
```
tree.png
rock.png
house.png
road.png
river.png
```

Then defines:
```
forest:
  density: high
  trees: [oak, pine]

village:
  houses: 20-50
  near: water
  connected_by: roads
```

Then **Genesis** will take over generating:
- terrain
- biome layout
- rivers
- forests
- villages
- roads

# Core Principles

Genesis is built on the following ideas:
1. Declarative generation
	+ Developers describe *what they want, not how to generate it*.
2. Modular generators
	+ Every generator is a pluggable module.
3. Deterministic worlds
	+ Worlds are reproducible using seeds.
4. Engine Independent
	+ Genesis generate worlds that can be exported anywhere.
5. Composable pipelines
	+ Generators combine into pipelines.

# Architecture (High Level)

[TODO: Fill this up after finishing architectutre]

# Why This Idea Might be Good

Three big industry trends support it.

### Indie Explosion

Engines like:
- Unity
- Godot
- Unreal Engine
made game creation easier.

But **content creation is still the bottleneck**.

Procedural tools solve that.

### Infinite games are becoming popular

Example:
- Minecraft
- No man's sky
- Dwarf Fortress
- Factorio

### Small teams need automation

Indie teams often have:
```
1 programmer
1 artist
0 world designers
```

PCG tools act like **extra designers**.

# What Make Genesis Special

Not algorithms. They are everywhere.

Our advantage should be:
### 1. Simplicity

Most PCG tools are **painful to use**.
Even powerful ones like *Houdini* are extremely complex.

Genesis should feel like:
```
import assets
define rules
hit generate
```

### 2. Composibility

Everything should plug together.

Example:
`terrain -> biome -> vegetation -> settlements`

### 3. Cross-engine compatibility

Support multiple engines.
Especially:
- Godot (growing fast)
- Unity
- Gamemaker
# Monetization & Sustainability

**TODO**
1. Asset Stores via plugin for respective engines
2. Open-source core with paid modules

# Long-Term Vision

Genesis may expand to include:
+ procedural cities
+ procedural dungeons
+ ecosystem simulation
+ procedural storytelling
+ procedural animations
+ intergrating AI into engines

Eventually Genesis could become a **complete procedural world platform**.