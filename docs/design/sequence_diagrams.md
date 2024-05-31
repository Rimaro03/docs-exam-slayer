# Sequence diagram

## System Sequence diagram
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

## Internal sequence diagrams
### Movement
```mermaid
sequenceDiagram
  Actor Player
  Player ->> Controller: moves
  alt keyPressed == A
    Controller ->> Controller: delta.add(new Vec2(-1, 0))
  else keyPressed == D
    Controller ->> Controller: delta.add(new Vec2(1, 0))
  else keyPressed == W
    Controller ->> Controller: delta.add(new Vec2(0, 1))
  else keyPressed == S
    Controller ->> Controller: delta.add(new Vec2(0, -1))
  end
  Controller ->> AnimatedSpriteRenderer: setSheetState(x,y)
  Controller ->> Component: setPosition(position)
```