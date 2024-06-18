---
title: Project manual
summary: Project manual containing the game description, tenchnologies used, how to compile, how to win
---

# __Exam Slayer - Final course exam project__

Full documentation of the project. Check out the source code [here](https://github.com/UNI-projects-team/exam-slayer)

## Brief description

Exam Slayer is a 2D graphical adventure game, set in various UniPD classrooms. The goal of the game is to __graduate__: as in real life,
to achieve such goal you need to pass some exams, represented in the game as boss to defeat.

## How to play
The game consists of __three levels__, which represent three academical years. To complete the game, you need to pass each level by collecting enough CFUs, dropped by each boss you defeat.

Finally, during the gameplay, you can collect and use the items you find, for example spending money on the vending machiens to buy upgrades.


## Installation and execution
To download the game in `.jar` format, get the last release from [here](https://www.github.com).

If you want to compile the game yourself, make sure you have `git` installed, the follow these instructions:
```bash
git clone https://github.com/UNI-projects-team/exam-slayer
cd exam-slayer
mvn clean compile assembly:single
java -jar target/Progetto-edids-1.0.0-jar-with-dependencies.jar
```
The compilation process is automated with Maven, which create the `.jar` file in the `target/` directory inside the project root.

## Technologies used

| Name       | Version | Description                                                   |
| :--------- | :------ | :------------------------------------------------------------ |
| Lombok     | 1.18.32 | Java library that writes code like getters automatically      |
| Junit      | 4.13.2  | Java framework used for developer-side testing on the JVM     |
| Maven      | 3.9.6   | Software that manages the project's build and its dependecies |
| Java Swing | 1.4.2   | Graphic framework for Java, used to develop the GUI           |

## Project structure


## World generation
Each time a new game is created, a random map is generated; the map generation is handled with the `wave function collapse algorithm`. <br/> <u>Breaf explanation</u> of how it works: lets consider a grid that has to be filled following some rules. At first, the algorithm considers that every grid cells is potentially in every state permitted by the rules. In every loop, the algorithm sets the state for a specific cell, restricting the states the nearby cells could be by removing the invalid ones. The result is a grid filled following the rules.
For a more detailed explenation, refer to [this video](https://www.youtube.com/watch?v=2SuvO4Gi7uY&t=31s&pp=ygUXd2F2ZSBjb2xsYXBzZSBhbGdvcml0aG0%3D).

## Colliders

## Controllers

## Final notes
- __Class Diagram__<br/> The class diagram has been divided into three parts (main, level, items) so that its easier to read it. Keeping it united would have resulted in a too small diagram.
<!--TODO: Setup bucket>