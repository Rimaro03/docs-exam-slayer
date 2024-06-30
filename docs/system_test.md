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
    Given that there are no enemies alive in the current room <br>
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
| View the inventory     | During the game, the player can see a <br> window with the items he collected | A game is in progress | The inventory is visible | <span style="color:green">PASSED</span> |
| Move between rooms     | The player can move between rooms <br> using doors |  No enemies alive in current room <br> (doors are opened) | The room displayed changes when player goes through a door | <span style="color:green">PASSED</span> |
| Collecting items       | The player may collect items by <br> walking over them | There are items in the current room | After collecting the item, <br>  it will be visible in the inventory | <span style="color:green">PASSED</span> |
| Interact with entities | The player can interact with the entities he meets | There are entities in the current room | Only after beating all the enemies in a room, the player can change room  | <span style="color:green">PASSED</span> |
| Beat bosses            | The player can fight and beat all the bosses to complete the game | There are still bosses alive | Once all the bosses have been defeated, the game is completed | <span style="color:green">PASSED</span> |
| Saving and loading     | In the main menu, the player may choose wether to load or save a game | There are saved games | All the progress previously made are saved and loaded correctly | <span style="color:green">PASSED</span> |