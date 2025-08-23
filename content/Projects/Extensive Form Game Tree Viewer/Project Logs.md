# Project Logs
### [2025-08-18]
- Scraped the old Python version to start a new C++ version from scratch.
- Will need to setup a container for running a clean Linux machine with Distrobox and later possibly interface with Windows too. At this time I would probably separate OSs concerns so the rest of the project shares the same code
- Will also need to implement a simple tree structure to work with that supports outcome and, later, information sets

#### 💡Ideas
- It would be interesting to also have a tool to create trees based on simple rules instead of hardcoding them

#### ✅ Done
- Started this log

---
### [2025-08-22]
After fighting with EndeavourOS, my Hyprland setup's startup timing for `xdg-desktop-portal` and `waybar` and the new Nvidia drivers switching card numbers crashing my config, I have finally managed to start the project.
For reference, I will be using Distrobox to run a clean Arch Linux container into which I will develop the C++ Tree Viewer.

#### ✅ Done
- Created a script that creates a container with specified packages, a name and a project path with Distrobox
  Since it is not in the repository, but in my dotfiles, I will include it here when done

#### 📌 Learned 
- How to use Distrobox to create an Arch Linux container
- How to install additional packages on container creation
- How to enter, stop and delete a container