# Overview
> Repo is private for now, might publish later

## Summary
---
Small game tree viewer made in Python with Gambit as a game theory library, Graphviz as the visualizer and Tkinter as the simple GUI to show the image of the game tree and display solution and equilibrium informations.

## Goal
---
The goal of this project is to help me visualize game trees to better understand complex games like Stackelberg or stochastic games.
By seeing the shape of the tree, I believe it will also help me better understand equilibria possible actions by players.

Another goal is to start using tools like Gambit to find solutions to games and understand possible resolution techniques and implement ones that are not in the available libraries from articles I've read while researching the topic.

> Side goal: develop my Python and software architecture experience

## Overall
---
> [[Project Logs|Details of the progress]]
### 📌 Learned 
- Possible strategies are the cross-products of the actions, so NEs (Nash Equilibria) and SPNEs (Subgame Perfect Nash Equilibria) are multiplied by actions never reached

### 🎯Challenges
- Accessing the payoffs means indexing the Outcome object by the Player.
  No way to get the array directly, meaning I need to iterate on each player

