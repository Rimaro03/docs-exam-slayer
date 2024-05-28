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