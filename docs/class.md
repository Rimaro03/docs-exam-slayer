# Class diagrams

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
    -Level currentLevel
    -SavingIO savingIO
    +static final ArrayList<Item> allitems
    -game()
    +static Game loadNewGame() Game
    +static Level getCurrentLevel() Level
    +static getSavingIO(): SavingIO
    +static getCurrentLevel(): Level
    +start()
    +update()
  }
  class SavingIO {
    -final String path
    -final StringBuilder text
    +SavingIO(String path)
    +flush()
    +setInt(String name, int value)
    +setFloat(String name, float value)
    +setLong(String name, long value)
    +setVec2Int(String name, Vec2Int value)
    +setVec2IntList(String name, List<Vec2Int> list)
    +getInt(String name): Integer
    +getFloat(String name): Float
    +getLong(String name): Long
    +getVec2Int(String name): Vec2Int
    +getVec2IntList(String name): List<Vec2Int>
    -set(String name, String savingString)
    -get(String name): String
    -listToSaveString(List<? extends Savable<?>> list): String
    -elementsCount(String text):int
    -getText(): StringBuilder
    -startIndex(String name): int
    -endIndex(int startIndex): int
  }
  class Level {
    -Room currentRoom
    -final List<Room> bossRooms
    -final Physics physicsEngine
    -final long seed
    -Room previousRoom
    +Level(Room startRoom, List<Room> bossRooms)
    +updateToSavedData()
    +save()
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

  Main-->Application: launches
  Application *-- Game: instantiates and contains
  Application --* Window: contains
  Game *-- Item: contains many
  Game *-- Level: instanciates and contains
  Game *-- SavingIO: instaciates and contains
  Level *-- Room: contains many
  Level *-- Physics: contains
  Room *-- GameObject: contains many
  Physics *-- Collider: contains many
  GameObject *-- Component: contains many
  GameObject *-- Vec2: contains
  Component *-- Vec2: contains
  Heart --|> Item: is a
  Sword --|> Item: is a

  Room *-- GameObject: contains many
  Room --|> GameObjectFactory: uses
  Room --|> BoxCollider: uses
  Room --|> Collider: uses
  Room --|> Direction: uses
  Room *-- InvalidDirectionException: throws
  Room *-- Vec2: contains

  Level --|> Algorithm: uses  
  Level *-- SavingIO: contains
  Level *-- Vec2Int: contains
  Level *-- GameObject: contains
  Level --|> WaveFunctionCollapse: uses

  LevelGenerator --|> GenerationSettings: uses
  LevelGenerator *-- Room: has many
  LevelGenerator *-- IllegalArgumentException: throws
  LevelGenerator *-- SuperRoom: has many
  LevelGenerator --|> Algorithm: uses
  LevelGenerator --|> GenerationFailedException: catches
  LevelGenerator --|> RoomState: uses
  LevelGenerator --|> WaveFunctionCollapse: uses

  RoomState --|> Direction: uses

  SuperRoom *-- RoomState: has many
  SuperRoom --|> GenerationFailedException: throws
  SuperRoom --|> IllegalArgumentException: throws
  SuperRoom --|> IllegalStateException: throws
  SuperRoom --|> GenerationSettings: uses
  
  WaveFunctionCollapse *-- SuperRoom: contains many
  WaveFunctionCollapse *-- Room: contains many
  WaveFunctionCollapse --|> GenerationFailedException: throws
  WaveFunctionCollapse *-- RoomState: contains and uses
  
  Algorithm *-- RoomDistancePair: contains many
  Algorithm *-- Room: contains many
```