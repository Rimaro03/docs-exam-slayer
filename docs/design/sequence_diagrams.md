# Sequence diagram

## System Sequence diagram
``` mermaid
sequenceDiagram
  Actor Player
  Game ->> Player: asks new game or load one?
  alt new game
    Game ->> Game: start new game
  else load one
    Game ->> Game: load existing saving
  end
  loop  
    Game->>Game: refresh the map
    Player ->> Game: moves in the map
    Game ->> Player: update player position
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
  Controller ->> Input: keyPressed(keyCode)
  activate Input
  Input ->> Controller: true if key pressed
  deactivate Input
  Controller ->> Controller: updates position vector
  Controller ->> AnimatedSpriteRenderer: setSheetState(x,y)
  Controller ->> Component: setPosition(position)
  loop
    Window ->> Player: repaint
  end
```