Thank you for your interest in contributing to **Genesis**.

Genesis aims to be a universal procedural generation pipeline for creating procedural worlds and systems. Contributions of all kinds are welcome, including bug reports, documentation improvements, new generators, and core engine development.

Before contributing, please read the project documentation:
- VISION.md
- ARCHITECTURE.md
- DESIGN_PRINCIPLES.md

## Ways to contribute

- Bug reports
- Feature requests
- Documentation improvements
- New generators
- Generator implementations
- Example worlds
- Exporter integrations
- Code improvements
- Performance improvements
## Getting Started

1. Fork the repository
2. Clone your fork
3. Create a new branch for your change
4. Make your changes
5. Submit a pull request

## Branching Strategy

```
feature/terrain-generator
fix/river-placement-bug
docs/improve-workflow
```
## Pull Request Guidelines

When submitting a pull request:
- Ensure the code follows the design principles  
- Keep pull requests focused on a single change  
- Include clear descriptions of the changes  
- Update documentation when necessary  
- Add tests if applicable  
- Update the CHANGELOG if the change affects users

## Coding Guidelines

- Prefer simple, readable code
- Avoid unnecessary dependencies
- Write modular generators
- Follow the architecture described in ARCHITECTURE.md

## Generator Development Guidelines

Generators should:
- Read from the world state
- Modify the world state
- Avoid direct dependencies on other generators
- Be deterministic given the same seed

## Reporting Bugs

When reporting a bug include:
- Description of the issue
- Steps to reproduce
- Configuration used
- Seed value
- Expected vs actual result

## Community Guidelines

Please follow the guidelines described in CODE_OF_CONDUCT.md.

