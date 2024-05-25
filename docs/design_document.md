---
title: Design document
summary: Composed by Domain model, system sequence diagram
weight: -8
---

# Design document

## Domain model
``` mermaid
classDiagram
    player --> room: moves between
    player --> item: interact with
    player --> fixed_item: interact with
    player --> entity: interact with
    player --> save_load: use
    player --> win: views
    save_load --> game: save/loads
    game --> win: notifies
    game --> map: has
    map --> room: contains
    map --> entity: contains
    map --> item: contains
    map --> fixed_item: contains

    class player {
        stats
        inventory
    }
```

## Sequence diagram
### System sequence diagram
``` mermaid
sequenceDiagram
  Actor Player
  Player->>Game: moves(direction)   
  loop
    Game->>Game: refresh(map)
  end
  alt went through a door?
   Game->>Player: change_current_room()
  end
```

## Class diagram
``` mermaid
classDiagram
  class Main {
    +static  main(String[])
  }
  class Application {
    -static Application instance
    -Window window
    -Application()
    +static getWindow() Window
    +static  init()
    +static  run()
    - initInternal()
    - runInternal()
    - setup()
    -windowCenteredX() int
    -windowCenteredY() int
  }
  class Game {
    -static Game currentGame
    -static Level currentLevel
    +static final ArrayList<Item> allitems
    -game()
    +static Game loadNewGame() Game
    +static Level getCurrentLevel() Level
    + start()
    + update()
  }
  class Item {
    <<Abstract>>
    -String name
    -int weight
    -String physicalPath
    -String inventoryPath
    -BufferedImage inventoryImage
    +Item(String name, int weight, String physicalPath, String inventoryPath)
    +abstract  use()
    +abstract  update()
  }
  class Heart{
    -final int health
    +Heart(String name, int weight, String physicalPath, String invetoryPath, int health)
    + use()
    + update()
  }
  class Sword {
    -final int damage
    +Sword(String name, int weight, String physicalPath, String inventoryPath, int damage)
    + use()
    + update()
  }
  class Level {
    -Room currentRoom
    -final List<Room> bossRooms
    -final Physics physicsEngine
    +Level(Room startRoom, List<Room> bossRooms)
    + changeRoom(int direction)
    + instantiateGameObject(GameObject gameObject, Vec2 position)
    + destroyGameObject(GameObject gameObject)
    + init()
    + update()
  }
  class Room{
    +static final float SIZE
    -final ArrayList<GameObject> gameObjects
    -final Room[] adjacentRooms
    -boolean initialized
    -InitType initType
    -final int x, y
    +Room(int x, int y)
    +setAdjacentRoom(int direction, Room room)
    +getAdjacentRoom(int direction) Room
    +getGameObject(String name) GameObject
    +addGameObject(GameObject gameObject)
    +removeGameObject(GameObject gameObject)
    +setEnabled(boolean enabled)
    +init()
    +updateGameObjects()
    +toString() String
  }
  class Physics {
    -final ArrayList<Collider> colliders
    +Physics()
    +addCollider(Collider collider)
    +removeCollider(Collider collider)
    +update()
  }
  class GameObject {
    -String name
    -ArrayList<Component> components
    -Vec2 position
    -boolean enabled
    +GameObject(String name)
    +GameObject(String name, Vec2 position)
    +setEnabled(boolean enabled)
    +addComponent(Component component)
    +removeComponent(Component component)
    +getComponent(Class<? extends Component> clazz) Component
    +start()
    +update()
    +destroy()
    +toString() String
  }
  class Collider {
    -boolean movable
    -ArrayList<Collider> ignoreColliders
    +Collider(GameObject gameObject, boolean enabled, boolean movable)
    +Collider(GameObject gameObject, boolean movable)
    +abstract collidesWith(Collider other) boolean
    +abstract onCollide(Collider other)
  }
  class Component {
    -String name
    -ArrayList<Component> components
    -Vec2 position
    -boolean enabled
    +GameObject(String name)
    +GameObject(String name, Vec2 position)
    +setEnabled(boolean enabled)
    +addComponent(Component component)
    +removeComponent(Component component)
    +getComponent(Class<? extends Component> clazz) Component
    +start()
    +update()
    +destroy()
    +toString() String
  }
  class Vec2 {
    -float x
    -float y
    +Vec2(float x, float y)
    +add(Vec2 other) Vec2
    +subtract(Vec2 other) Vec2
    +multiply(float scalar) Vec2
    +divide(float scalar) Vec2
    +dot(Vec2 other) float
    +magnitude() float
    +normalized() Vec2
    +distance(Vec2 other) float
    +copy() Vec2
    +equals(Object o) boolean
    +clamp(Vec2 value, Vec2 min, Vec2 max) Vec2
    +toString() String
  }

  Main-->Application: launches
  Application --|> JFrame: is a
  Application *-- Game: instantiates and contains
  Game *-- Item: contains many
  Heart --|> Item: is a
  Sword --|> Item: is a
  Game *-- Level: instanciates and contains
  Level *-- Room: contains many
  Level *-- Physics: contains
  Room *-- GameObject: contains many
  Physics *-- Collider: contains many
  GameObject *-- Component: contains many
  GameObject *-- Vec2: contains
  Component *-- Vec2: contains
```