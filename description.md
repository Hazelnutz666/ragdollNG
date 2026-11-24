# Ragdoll Sandbox — Development Prompt

You are an expert browser game developer. Build a fully playable, 2D browser-based physics sandbox inspired by games like People Playground.

## 1. Core Concept

Create an interactive sandbox where players can:
- Spawn and control ragdoll characters.
- Experiment with gravity and physics.
- Move, throw, and manipulate objects using the mouse.
- Build structures using walls, bridges, platforms, ramps, and crates.
- Create funny physics interactions, collisions, explosions, and chain reactions.

Physics must ALWAYS apply. Characters should naturally fall, collide, stumble, and react to forces, even when using movement presets.

## 2. Physics Engine

Use **Matter.js** or another suitable 2D physics engine.

Implement:
- Gravity and gravity direction.
- Mass and weight.
- Collision detection.
- Friction and restitution.
- Velocity and acceleration.
- Angular velocity.
- Joint constraints and stiffness.
- Damping and air resistance.
- Time scale.

### Physics Control Panel

Provide real-time sliders and controls for physics parameters.

Include presets:
- Realistic (default).
- Moon Gravity.
- Zero Gravity.
- Heavy Gravity.
- Super Bouncy.
- Low Friction.
- Chaos Mode.

A Reset to Realistic Physics button must restore sensible real-world-inspired defaults.

## 3. Ragdoll Characters

Build articulated ragdolls using connected physical body parts:
- Head and torso.
- Upper/lower arms.
- Upper/lower legs.

Use actual physics constraints and joints.

Characters must react naturally to collisions, gravity, forces, and other characters.

### Individual Character Presets

Each character should independently support:
- Idle.
- Walking.
- Running.
- Jumping.
- Falling.
- Flailing.
- Sitting.

Movement must use physical forces or joint motors, NOT CSS animations or manually setting character positions. Characters must remain vulnerable to collisions and loss of balance while moving.

## 4. Objects and Environment

Provide a ground plane and boundaries.

Initial objects:
- Static and movable walls.
- Wooden crates.
- Metal blocks.
- Bridges.
- Platforms.
- Ramps.
- Bouncy platforms.
- Heavy balls.

Objects should have configurable physical properties.

### Mouse Interaction
- Click and drag objects.
- Pick up and move ragdolls.
- Throw objects.
- Build structures.
- Interact with objects physically, not through teleportation.

Design objects using reusable definitions so new object types can easily be added.

## 5. Sandbox Tools

Include:
- Spawn ragdoll.
- Spawn objects.
- Grab and drag.
- Delete objects.
- Reset environment.
- Wind force.
- **Explosion tool:** Apply adjustable physical impulses to nearby characters and objects. Allow the player to configure explosion radius and strength.
  
## 6. Object Inspector

Allow players to select any object and edit its properties in real time.

Include:
- Mass.
- Width and height / size.
- Material type (wood, metal, rubber, etc.).
- Friction.
- Bounciness.
- Static/dynamic behavior.

Changes must immediately affect the physics simulation.

## 7. User Interface

Create a modern, dark-themed sandbox interface.

Suggested layout:

**Top toolbar:** Play/Pause, Reset, Spawn, Tools, Physics presets.

**Left sidebar:** Object spawning, character management, environment tools.

**Right sidebar:** Physics controls, selected object inspector, character presets.

**Main area:** Large interactive simulation viewport.

Keep the interface clean, intuitive, and responsive. The simulation should be the main focus.

## 8. Technical Requirements

Preferred stack:
- HTML5.
- CSS3.
- JavaScript.
- Matter.js for physics.
- WebGL for hardware-accelerated rendering where appropriate.
- HTML5 Canvas as a fallback or simpler rendering solution.

Choose a rendering approach that works reliably in modern browsers. Do not sacrifice physics stability for graphical effects.

### Single-File Architecture

Keep the entire project in ONE `index.html` file if reasonably possible:
- HTML.
- CSS.
- JavaScript.
- Game logic.
- UI.
- Rendering.

CDN libraries are acceptable. Avoid build systems and unnecessary frameworks.

Organize the code into logical components/classes:
- PhysicsManager.
- Ragdoll.
- CharacterController.
- ObjectManager.
- InteractionManager.
- ToolManager.
- PresetManager.
- UIManager.

Make the architecture easy to extend with new objects, characters, tools, and physics presets.

## 9. Performance and Quality

- Smooth animation and stable physics.
- Efficient simulation loop.
- Proper browser resizing.
- Support multiple ragdolls and objects.
- Prevent unstable joints and disappearing objects.
- Work in modern desktop browsers.

## 10. Deliverable

Build a COMPLETE, PLAYABLE game.

Do not produce a mockup, static demo, pseudocode, or non-functional buttons.

All major controls must work and interact with the actual simulation.

Prioritize a working physics sandbox over decorative features.

Deliver a complete `index.html` that can run directly in a browser without a build process.

Test for JavaScript errors and verify the main interactions.

If the full feature set is too ambitious, implement a smaller but fully functional version rather than leaving features unfinished.

**Ultimate goal:** A fun, expandable physics playground where players can spawn ragdolls, manipulate objects, experiment with physics, trigger explosions, and create ridiculous physical interactions.