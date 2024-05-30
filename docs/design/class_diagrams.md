# Class diagrams

## Saving system class diagram
```mermaid
classDiagram
  SavingIO --* Vec2Int: contains many
  SavingIO --* ListReader: contains
  Savable ..|> ListReader
```

## Items class diagram
```mermaid
classDiagram
  Item ..|> Heart
  Item ..|> Sword
```

[//]: # (TODO split generation class diagram diagram)

## Generation class diagram
```mermaid
classDiagram
  LevelGenerator --> GenerationSettings: uses
  LevelGenerator --* Room: has many
  LevelGenerator --* IllegalArgumentException: throws
  LevelGenerator --* SuperRoom: has many
  LevelGenerator --> Algorithm: uses
  LevelGenerator --> Debug: uses

  SuperRoom --* RoomState: has many
  SuperRoom --> GenerationFailedException: throws
  SuperRoom --> IllegalArgumentException: throws
  SuperRoom --> IllegalStateException: throws
  
  WaveFunctionCollapse --* SuperRoom: contains many
  WaveFunctionCollapse --* Room: contains many
  WaveFunctionCollapse --> GenerationFailedException: throws
  WaveFunctionCollapse --> Direction: uses
  
  Algorithm --* RoomDistancePair: contains many
  Algorithm --* Room: contains many

  Room --> Direction: uses
  Room --> InvalidDirectionException: throws
  Room --> Game: uses
  Room --* GameObject: contains
  Room --> GameObjectFactory: uses
  
  Level --> Algorithm: uses
  Level --* Room: contains many
  Level --* Physics: contains and initializes
  Level --> Game: uses
  Level --> GameObject: uses
```

## Core class diagram
```mermaid
classDiagram
  Main --> Application: launches

  Application --* Window: contains
  Application --* Game: contains, initializes
  Application --> Time: uses

  Game --* Level: contains
  Game --* SavingIO: contains
  Game --* Item: contains many
  Game --> LevelGenerator: uses
  Game --> GenerationSettings: uses

  Window --> Renderer: uses
  Window --> Application: uses

  Physics --* Colliders: contains many

  Input --> Application: uses
  Input --* KeyInput: contains (nested?)
  Input --* MouseInput: contains (nested?)

  Renderer --> Application: uses
```
### Core Rendering class diagram
```mermaid
classDiagram
  Renderable --* Vec2: contains
  Renderable --* Comparator: contains (nested?)
  Renderable <|-- RenderableCircle
  Renderable <|-- RenderableImage
  Renderable <|-- RenderableRectangle
  Renderable <|-- RenderableText

  Renderer --> Application: uses
  Renderer --> Vec2: uses
  Renderer --* Renderable: has many
  Renderer --* Comparator: contain (?)
  Renderer --* RenderableCircle: has many
  Renderer --* RenderableImage: has many
  Renderer --* RenderableRectangle: has many
  Renderer --* RenderableText: has many

  RenderableRectangle --> Renderer: uses
  RenderableRectangle --> Vec2: uses

  RenderableCircle --> Renderer: uses
  RenderableCircle --> Vec2: uses

  RenderableImage --> Renderer: uses
  RenderableImage --> Vec2: uses

  RenderableText --> Renderer: uses
  RenderableText --> Vec2: uses
```
[//]: # (TODO split component class diagram diagram)

## Component system class diagram
```mermaid
classDiagram
  GameObject --* Component: contains many
  GameObject --* Vec2: contains

  GameObjectFactory --* GameObject: contains many
  GameObjectFactory --* PlayerStats: contains
  GameObjectFactory --* EntityStats: contains
  GameObjectFactory --* AnimatedSpriteRenderer: contains
  GameObjectFactory --* PlayerController: contains
  GameObjectFactory --* PlayerShootingController: contains
  GameObjectFactory --* BoxCollider: contains
  GameObjectFactory --* DoorCollider: contains
  GameObjectFactory --* ProjectileCollider: contains
  GameObjectFactory --* Projectile: contains
  GameObjectFactory --* ItemController: contains
  GameObjectFactory --* ItemCollider: contains

  Component --* GameObject: contains
  Component --> Vec2: uses

  ItemController --|> Component: inherits
  ItemController --> GameObject: uses
  ItemController --* Item: contains

  PlayerController --|> Component: inherits
  PlayerController --> Time: uses
  PlayerController --> Input: uses
  PlayerController --> GameObject: uses
  PlayerController --* PlayerStats: contains
  PlayerController --* AnimatedSpriteRenderer: contains
  PlayerController --* Vec2: contains

  Projectile --|> Component: inherits
  Projectile --> Time: uses
  Projectile --> GameObject: uses
  Projectile --* Vec2: contains

  AnimatedSpriteRenderer --|> Component
  AnimatedSpriteRenderer --> Renderer: uses
  AnimatedSpriteRenderer --> GameObject: uses

```
### Component Colliders class diagram
```mermaid
classDiagram
  AbstractBoxCollider --> GameObject: uses

  Collider --> GameObject: uses

  BoxCollider --> Game: uses
  BoxCollider --> Debug: uses
  BoxCollider --> Renderer: uses

  CircleCollider --> Game: uses
  CircleCollider --> Debug: uses
  CircleCollider --> Renderer: uses
  CircleCollider --> GameObject: uses

  DoorCollider --> Game: uses
  DoorCollider --> Debug: uses
  DoorCollider --> GameObject: uses

  ProjectileCollider --> Game: uses
  ProjectileCollider --* GameObject: contains
```
### Component Stats class diagram
```mermaid
classDiagram
  Stats --> Game: uses

  PlayerStats --|> Stats: inherits
  PlayerStats --> Renderer: uses

  EntityStats --|> Stats: inherits
  EntityStats --> GameObject: uses
```
### Component Weapons class diagram
```mermaid
classDiagram
  PlayerShootingController --> Time: uses
  PlayerShootingController --> Input: uses
  PlayerShootingController --> Game: uses
  PlayerShootingController --> GameObjectFactory: uses
  PlayerShootingController --* GameObject: contains
```