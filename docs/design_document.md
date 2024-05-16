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
``` mermaid
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```

## Class diagram
``` mermaid
classDiagram
  Person <|-- Student
  Person <|-- Professor
  Person : +String name
  Person : +String phoneNumber
  Person : +String emailAddress
  Person: +purchaseParkingPass()
  Address "1" <-- "0..1" Person:lives at
  class Student{
    +int studentNumber
    +int averageMark
    +isEligibleToEnrol()
    +getSeminarsTaken()
  }
  class Professor{
    +int salary
  }
  class Address{
    +String street
    +String city
    +String state
    +int postalCode
    +String country
    -validate()
    +outputAsLabel()  
  }
```