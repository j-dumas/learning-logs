# Extensive Form Game Tree Viewer
> Repo is private for now, might publish later
## Overview
---
Small game tree viewer made in Python with Gambit as a game theory library, Graphviz as the visualizer and Tkinter as the simple GUI to show the image of the game tree and display solution and equilibrium informations.

## Goal
---
The goal of this project is to help me visualize game trees to better understand complex games like Stackelberg or stochastic games.
By seeing the shape of the tree, I believe it will also help me better understand equilibria possible actions by players.

Another goal is to start using tools like Gambit to find solutions to games and understand possible resolution techniques and implement ones that are not in the available libraries from articles I've read while researching the topic.

> Side goal: develop my Python and software architecture experience

## Logs
---
### [2025-08-02]
- Created the site, but the project is older than that

#### ✅ Done
- MVC architecture for Tkinter with classes
- Graphviz image generation from a hardcoded tree
- Rescaling of the image so that it fits on first open

#### 📌 Learned
- Wanted to add possibility of opening new files and a button to solve, but out of scope.
  It was easier to simply use the GUI as a tool used for each of the tree instead of the trees being included in one GUI

### [2025-08-12]
- Strongly considering ditching the project and using Gambit's own GUI.
  Might finish the translation between Gambit and Graphviz, implement a simple backward induction and then work with Gambit's GUI until games become too big for it and I come back here
  
> Edit: The UI is weird to use and does not include every solvers available, like enumpure.
> Will continue implementing Gambit and Graphviz for now to develop my experience

- I will study Nashpy to see their algorithms and implementations too, they will be simpler than trying to understand the convoluted and undocumented code of Gambit

#### ✅ Done
- Added entirety of choices made by Minimax, hardcoded, to see what the complete SPNEs would be like.
  This was removed further in the day in favor or using Gambit
- Started reading Gambit's C++ source code to see how outcomes were implemented as to understand what their roles was versus payoffs
- Added opening of an Extended Form Game (`.efg`) with Gambit and displaying of the root node with player and label

#### 📌 Learned
- Possible strategies are the cross-products of the actions, so NEs (Nash Equilibria) and SPNEs (Subgame Perfect Nash Equilibria) are multiplied by actions never reached.
  This means that if an equilibrium never reaches a state that has two actions, there will be two equilibria, one for each action since they are included in the optimal strategies
- Outcomes are objects with stored payoffs that also include a label, making them reusable.
  For example, Nim has two outcomes, -1 and +1, that are reused at each terminal nodes
- Added two scripts from Gambit's source code that build Nim games as trees and  *started* converting it to Python3

#### 🎯Challenges
- Accessing the payoffs means indexing the Outcome object by the Player.
  No way to get the array directly, meaning I need to iterate on each player.
  It seems to be excessively slow, maybe because of Cython bindings
- **Don't forget to refactor and document...**