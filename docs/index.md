---
title: Project manual
summary: Project manual containing the game description, tenchnologies used, how to compile, how to win
weight: -9
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

