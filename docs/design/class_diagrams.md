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

[//]: # (TODO split generation class diagram diagram (separate level and room))

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
  Room --> Collider: uses
  Room --> BoxCollider: uses
  
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

## Component class diagram
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
  GameObjectFactory --> Collider: uses
  GameObjectFactory --> WeaponData: uses

  Component --* GameObject: contains
  Component --> Vec2: uses

  ItemController --|> Component: extends
  ItemController --> GameObject: uses
  ItemController --* Item: contains

  PlayerController --|> Component: extends
  PlayerController --> Time: uses
  PlayerController --> Input: uses
  PlayerController --> GameObject: uses
  PlayerController --* PlayerStats: contains
  PlayerController --* AnimatedSpriteRenderer: contains
  PlayerController --* Vec2: contains

  Projectile --|> Component: extends
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
  Collider --|> Component: extends
  Collider --> GameObject: uses

  AbstractBoxCollider --|> Collider: extends
  AbstractBoxCollider --> GameObject: uses
  AbstractBoxCollider --* Vec2: contains
  AbstractBoxCollider --> Collider: uses
  AbstractBoxCollider --* AbstractCircleCollider: contains
  AbstractBoxCollider --> CircleCollider: uses

  AbstractCircleCollider --|> Collider: extends
  AbstractCircleCollider --> GameObject: uses
  AbstractCircleCollider --* Vec2: contains
  AbstractCircleCollider --> Collider: uses

  BoxCollider --|> AbstractBoxCollider: extends
  BoxCollider --> Game: uses
  BoxCollider --> Debug: uses
  BoxCollider --> Renderer: uses
  BoxCollider --* Vec2: contains
  BoxCollider --> GameObject: uses
  BoxCollider --> Collider: uses
  BoxCollider --* CircleCollider: contains

  CircleCollider --|> AbstractCircleCollider: extends
  CircleCollider --> Game: uses
  CircleCollider --> Debug: uses
  CircleCollider --> Renderer: uses
  CircleCollider --> GameObject: uses
  CircleCollider --> AbstractBoxCollider: uses
  CircleCollider --* BoxCollider: contains

  DoorCollider --|> AbstractBoxCollider: extends
  DoorCollider --> Game: uses
  DoorCollider --> Debug: uses
  DoorCollider --> GameObject: uses
  DoorCollider --> Renderer: uses
  DoorCollider --> Direction: uses
  DoorCollider --> Room: uses
  DoorCollider --> Collider: uses
  DoorCollider --* Vec2: contains

  ItemCollider --|> BoxCollider: extends
  ItemCollider --> GameObject: uses
  ItemCollider --> AnimatedSpriteRenderer: uses
  ItemCollider --> Collider: uses
  ItemCollider --* PlayerStats: contains
  ItemCollider --* Item: contains
  ItemCollider --* Vec2: contains

  ProjectileCollider --|> AbstractBoxCollider: extends
  ProjectileCollider --> Game: uses
  ProjectileCollider --> Contains: uses
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
  PlayerStats --* Vec2: contains

  EntityStats --|> Stats: extends
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
  PlayerShootingController --* Vec2: contains

  WeaponData --> WeaponType: uses
```

## Utils class diagram
```mermaid
classDiagram
  class Vec2

  Vec2Int ..|> Savable: implements
```