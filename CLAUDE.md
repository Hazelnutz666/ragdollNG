# Ragdoll Sandbox

## Project

This workspace contains the development specification in `description.md`.

The deliverable is a complete, single-file browser game in `index.html`.

## Stack

- HTML5, CSS3, and vanilla JavaScript
- Matter.js loaded from a CDN
- HTML5 Canvas rendering
- No build system or framework

## Architecture

Keep implementation logic in `index.html` and organize it into logical classes:

- `PhysicsManager`
- `Ragdoll`
- `CharacterController`
- `ObjectManager`
- `InteractionManager`
- `ToolManager`
- `PresetManager`
- `UIManager`

## Required Product Areas

- Stable Matter.js physics with gravity, boundaries, collision, friction, restitution, and time scaling
- Articulated, physically constrained ragdolls
- Spawnable walls, crates, metal blocks, bridges, platforms, ramps, and balls
- Mouse grabbing, dragging, throwing, deletion, and explosion impulses
- Real-time physics and object-inspector controls
- Character movement presets that use forces or motors
- Responsive dark-themed UI with the simulation viewport as the main focus

## Implementation Guidance

- Prioritize a working, stable physics sandbox over decorative features.
- Do not substitute CSS animations or direct position teleportation for character physics.
- Keep object creation definitions reusable for easy extension.
- Use the full Matter.js simulation loop; pause, reset, and resize must affect the real state.
- Preserve one-file delivery unless a build requirement makes it necessary.

## Validation

- Run directly in a modern desktop browser.
- Check for JavaScript console errors.
- Verify spawning, grabbing, throwing, deletion, reset, physics presets, explosions, and object property edits.
