---
Title: Sistem Test Document
Description:
---

# System Test Report
Each user stories has some acceptance criteria with their system test results.

## View the inventory
*As a player I want to view my inventory anytime so that I can view which items I'm carrying*

| Acceptance Criteria | Result |
| :------------------ | :----- |
| Display a window in the game for the inventory | <span style="color:green">PASSED</span> | 
| Store the items the player collects | <span style="color:green">PASSED</span> |
| When the player collect a new item, add it to the inventory | <span style="color:green">PASSED</span> |

## Move between rooms
*As a player, I want to be able to move between the rooms so that I can explore the game map*

| Acceptance Criteria | Result |
| :------------------ | :----- |
| Generate the game map | <span style="color:green">PASSED</span> | 
| Divide the game map into rooms | <span style="color:green">PASSED</span> |
| Add doors to move between the rooms, not all rooms should be directly connected | <span style="color:green">PASSED</span> |
| Implement player movement | <span style="color:green">PASSED</span> |

## Collecting items
*As a player, I want to collect and use the items I find while exploring the game map to be able to use them*

| Acceptance Criteria | Result |
| :------------------ | :----- |
| Add various types of items inside each room | <span style="color:green">PASSED</span> | 
| Let the player collect the collectable items | <span style="color:green">PASSED</span> |
| Implement a way to use these items, such as shooting | <span style="color:green">PASSED</span> |

## Interact with entities
*As a player, I want to interact with other entities so that I can defeat enemies, for example*

| Acceptance Criteria | Result |
| :------------------ | :----- |
| Generate other entities in the game map | <span style="color:green">PASSED</span> | 
| Entities must have limited life | <span style="color:green">PASSED</span> |
| Bosses should have more life than simple enemies | <span style="color:green">PASSED</span> |
| Let the player interact with entities, like shooting | <span style="color:green">PASSED</span> |

## Beat bosses
*As a player, I want to beat the bosses so that I can complete the game*

| Acceptance Criteria | Result |
| :------------------ | :----- |
| Spawn bosses in some parts of the map | <span style="color:green">PASSED</span> | 
| Bosses should be more difficult to defeat | <span style="color:green">PASSED</span> |
| When each boss is defeated, the player has completed the game | <span style="color:green">PASSED</span> |

## Saving and loading
*As a player, I wan to save and load the game so that I can play the game when I want without losing savings*

| Acceptance Criteria | Result |
| :------------------ | :----- |
| Implement cloud game save | <span style="color:green">PASSED</span> | 
| Implement loading game from cloud savings | <span style="color:green">PASSED</span> |
| Delete a saving if the player dies | <span style="color:green">PASSED</span> |
| Create new saving if the player starts a new game | <span style="color:green">PASSED</span> |

