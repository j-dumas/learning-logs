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

## Logs
---
### 2025-08-02
- Created the site, but the project is older than that
- What is done already:
	- MVC architecture for Tkinter with classes
	- Graphviz image generation from a hardcoded tree
	- Rescaling of the image so that it fits on first open
- Wanted to add possibility of opening new files and a button to solve, but out of scope.
  It was easier to simply use the GUI as a tool used for each of the tree instead of the trees being included in one GUI