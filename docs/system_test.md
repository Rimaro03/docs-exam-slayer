---
Title: Sistem Test Document
Description:
---
## Acceptance criteria

### View the inventory
*As a player I want to view my inventory anytime so that I can view which items I'm carrying*

- **Scenario**: Show inventory if a game is in progres <br>
    Given that the game is not started yet <br>
    When I start/load a new game <br>
    Then I can see my inventory on the screen <br>
  
### Move between rooms
*As a player, I want to be able to move between the rooms so that I can explore the game map*

- **Scenario**: Change room when the player goes through a door <br>
    Given that there are no boss alive in the current room <br>
    When I go throw a door <br>
    Then I can change the room I'm in <br>

### Collecting items
*As a player, I want to collect and use the items I find while exploring the game map to be able to use them*

- **Scenario**: Add items to the player inventory when he walks over one <br>
    Given that there are items in the current room <br>
    When I walk over an item <br>
    Then I collect it<br>
    And see it in my intentory<br>

### Interact with entities
*As a player, I want to interact with other entities so that I can defeat enemies, for example*

- **Scenario**: When the player encounters entities, let him interact with them <br>
    Given that there are entities alive<br>
    When I enter a room with entities <br>
    Then I can interact with them<br>

### Beat bosses
*As a player, I want to beat the bosses so that I can complete the game*

- **Scenario**: When the player encounters bosses, let him fight with them <br>
    Given that there are bosses alive<br>
    When I enter a boss room <br>
    Then I can use my items to fight and kill him<br>
    And be able to complete the game<br>


### Saving and loading
*As a player, I wan to save and load the game so that I can play the game when I want without losing savings*

- **Scenario**: Let the player loads saved games, if there are any <br>
    Given that there are sagings available<br>
    When I start the game I wat to be able to load a game <br>
    Then I can resume playing without losing all the progress<br>

## System Test Report

| Acceptance Criteria    | Summary                                                                   | Pre-Condition | Post Condition | Status                                  |
| :--------------------- | :------------------------------------------------------------------------ | :------------ | :------------- | :-------------------------------------- |
| View the inventory     | During the game, the player can see a <br> window with the items he collected | A game is in progress |  | <span style="color:green">PASSED</span> |
| Move between rooms     |                                                                           |               |                | <span style="color:green">PASSED</span> |
| Collecting items       |                                                                           |               |                | <span style="color:green">PASSED</span> |
| Interact with entities |                                                                           |               |                | <span style="color:green">PASSED</span> |
| Beat bosses            |                                                                           |               |                | <span style="color:green">PASSED</span> |
| Saving and loading     |                                                                           |               |                | <span style="color:green">PASSED</span> |