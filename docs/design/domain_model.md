# Domain model

``` mermaid
classDiagram
    player --> room: moves between
    player --> item: collects
    player --> enemies: interact with
    player --> bosses: interact with
    player --> save_load: use
    player --> win: views
    player --> item: uses
    save_load --> game: save/loads
    game --> win: notifies
    game --> level: has
    level --> room: has
    room --> enemies: contains
    room --> bosses: contains
    room --> item: contains

    class player {
        stats
        inventory
    }
```