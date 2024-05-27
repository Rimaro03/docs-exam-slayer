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

## Sequence diagrams
### System sequence diagram
``` mermaid
sequenceDiagram
  Actor Player
  Game ->> Player: asks new game or load one?
  alt new game
    Game ->> Game: start new game
  else load one
    Game --> Game: load existing saving
  end
  par  
    loop
      Game->>Game: refresh the map
    end
    Player ->> Game: moves in the map
    alt went through a door?
      Game->>Player: change room displayed
    end
    Player ->> Game: shoots
    alt hits entity & entity life = 0?
      Game ->> Player: entity died
    else
      Game ->> Game: decrease entity life
    end
    Player ->> Game: collects item
    alt collected heart?
      Game ->> Player: increase life points
    else
      Game ->> Player: increas atk points
    end
  end
```

## Class diagrams
### Main class diagram
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
  class Window {
    -int width, height
    +Window(int width, int height)
    +update()
    -paintComponent(Graphics g)
    -setup()
    +componentResized(ComponentEvent e)
    +componentMoved(ComponentEvent e)
    +componentShown(ComponentEvent e)
    +componentHidden(ComponentEvent e)
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

  Main-->Application: launches
  Application *-- Game: instantiates and contains
  Application --* Window: contains
  Game *-- Item: contains many
  Game *-- Level: instanciates and contains

```

### Levels class diagram
``` mermaid
classDiagram
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

  Level *-- Room: contains many
  Level *-- Physics: contains
  Room *-- GameObject: contains many
  Physics *-- Collider: contains many
  GameObject *-- Component: contains many
  GameObject *-- Vec2: contains
  Component *-- Vec2: contains
```

### Items class diagram
``` mermaid
classDiagram
    class Item {
    <<Abstract>>
    -String name
    -int weight
    -String physicalPath
    -String inventoryPath
    -BufferedImage inventoryImage
    +Item(String name, int weight, String physicalPath, \nString inventoryPath)
    +abstract  use()
    +abstract  update()
  }
  class Heart{
    -final int health
    +Heart(String name, int weight, String physicalPath, \nString invetoryPath, int health)
    + use()
    + update()
  }
  class Sword {
    -final int damage
    +Sword(String name, int weight, String physicalPath, \nString inventoryPath, int damage)
    + use()
    + update()
  }

  Heart --|> Item: is a
  Sword --|> Item: is a
```