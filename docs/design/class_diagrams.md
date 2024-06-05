# Class diagrams

## Saving system class diagram
```mermaid
classDiagram
  SavingIO --* Vec2Int: contains many
  SavingIO --> ListReader: uses

  Savable ..|> ListReader
```

## Items class diagram
```mermaid
classDiagram
  Item ..|> Heart
  Item ..|> Sword
```

[//]: # (TODO split generation class diagram diagram (separate level and room))

## Generation class diagram
```mermaid
classDiagram
  LevelGenerator --> GenerationSettings: uses
  LevelGenerator --* Room: has many
  LevelGenerator --* IllegalArgumentException: throws
  LevelGenerator --* SuperRoom: has many
  LevelGenerator --> Algorithm: uses

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
  Renderable --* Comparator: contains (nested?)
  Renderable <|-- RenderableCircle
  Renderable <|-- RenderableImage
  Renderable <|-- RenderableRectangle
  Renderable <|-- RenderableText


  Application <-- Renderer
  Renderable *-- Renderer
  Comparator *-- Renderer
  RenderableCircle *-- Renderer
  RenderableImage *-- Renderer
  RenderableRectangle *-- Renderer
  RenderableText *-- Renderer

  RenderableRectangle --> Renderer: uses

  RenderableCircle --> Renderer: uses

  RenderableImage --> Renderer: uses

  RenderableText --> Renderer: uses
```
[//]: # (TODO split component class diagram diagram)

## Component class diagram
```mermaid
classDiagram
  GameObject --* Component: contains many

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
  GameObjectFactory --> Collider: uses
  GameObjectFactory --> WeaponData: uses

  Component --* GameObject: contains

  ItemController --|> Component: extends
  ItemController --> GameObject: uses
  ItemController --* Item: contains

  PlayerController --|> Component: extends
  PlayerController --> Time: uses
  PlayerController --> Input: uses
  PlayerController --> GameObject: uses
  PlayerController --* PlayerStats: contains
  PlayerController --* AnimatedSpriteRenderer: contains

  Projectile --|> Component: extends
  Projectile --> Time: uses
  Projectile --> GameObject: uses

  AnimatedSpriteRenderer --|> Component
  AnimatedSpriteRenderer --> Renderer: uses
  AnimatedSpriteRenderer --> GameObject: uses

```
### Component Colliders class diagram
```mermaid
classDiagram
  Collider --> GameObject: uses

  AbstractBoxCollider --|> Collider: extends
  AbstractBoxCollider --> GameObject: uses
  AbstractBoxCollider --> Collider: uses
  AbstractBoxCollider --* AbstractCircleCollider: contains
  AbstractBoxCollider --> CircleCollider: uses

  AbstractCircleCollider --|> Collider: extends
  AbstractCircleCollider --> GameObject: uses
  AbstractCircleCollider --> Collider: uses

  BoxCollider --|> AbstractBoxCollider: extends
  BoxCollider --> GameObject: uses
  BoxCollider --> Collider: uses
  BoxCollider --* CircleCollider: contains

  CircleCollider --|> AbstractCircleCollider: extends
  CircleCollider --> GameObject: uses
  CircleCollider --> AbstractBoxCollider: uses
  CircleCollider --* BoxCollider: contains

  DoorCollider --|> AbstractBoxCollider: extends
  DoorCollider --> GameObject: uses
  DoorCollider --> Collider: uses

  ItemCollider --|> BoxCollider: extends
  ItemCollider --> GameObject: uses
  ItemCollider --> AnimatedSpriteRenderer: uses
  ItemCollider --> Collider: uses
  ItemCollider --* PlayerStats: contains
  ItemCollider --* Item: contains

  ProjectileCollider --|> AbstractBoxCollider: extends
  ProjectileCollider --* GameObject: contains
  ProjectileCollider --* Projectile: contains
  ProjectileCollider --* Stats: contains
```
### Component Stats class diagram
```mermaid
classDiagram
  Stats --|> Component: extends
  Stats --> Game: uses
  Stats --> GameObject: uses

  PlayerStats --|> Stats: extends
  PlayerStats --> Renderer: uses
  PlayerStats --> GameObject: uses
  PlayerStats --> Heart: uses
  PlayerStats --* Item: contains many

  Stats <|-- EntityStats: extends
  EntityStats --> GameObject: uses
```
### Component Weapons class diagram
```mermaid
classDiagram
  PlayerShootingController --|> Component: extends
  PlayerShootingController --> Time: uses
  PlayerShootingController --> Input: uses
  PlayerShootingController --> Game: uses
  PlayerShootingController --> GameObjectFactory: uses
  PlayerShootingController --> WeaponData: uses
  PlayerShootingController --* GameObject: contains

  WeaponData --> WeaponType: uses
```

## Utils class diagram
```mermaid
classDiagram
  Vec2Int ..|> Savable: implements
```