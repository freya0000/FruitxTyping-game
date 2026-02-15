# 🍎 Fruit Catcher: A Retro Typing Game

Fast-paced typing game built with the **Pyxel** retro game engine. This project combines classic "catcher" mechanics with typing challenges to improve keyboard speed and accuracy.

## 🎮 Gameplay
The objective is to catch as much fruit as possible. However, you should**type its name first**!

<img width="355.5" height="374.5" alt="game" src="https://github.com/user-attachments/assets/63fb4ece-8aa7-4951-8c4f-797d10f93340" />

<img src="https://github.com/user-attachments/assets/54f865c6-2a1c-437e-95f3-a35ed3975a0a" height = "374.5">

* **Targeting:** The most bottom fruit "glow" and is your active target. But you can click another fruit to move the target
* **Typing:** Type the fruit's name (e.g., "apple", "banana") and press **Enter** to turn it into a star.
* **Catching:** Move your catcher with the **Arrow Keys** to collect the falling stars.
* **Power-ups:** Every 10 successful catches, a heart falls. Catch it to regain a life.
* **Avoid Bombs:** Do not type when a bomb is glowing, or you will lose a life!
* **Dynamic Difficulty:** The game speeds up every 5 points, 

## Technical Features
* **Object-Oriented Programming (OOP):** Modular classes for `Fruit`, `Catcher`, and `Star`.
* **State Logic:** Managed game states for Start Screen, Active Gameplay, and Game Over.
* **Dynamic Difficulty Scaling:** Speed and spawn intervals adjust based on your score.
* **Asset Integration:** Custom `.pyxres` file for pixel art and audio.

## Setup & Installation

### Prerequisites
* Python 3.x
* Pyxel library

### Installation
1. **Install Pyxel:**
   https://github.com/kitao/pyxel
   
2. **Run the game:**
   ```bash
   python FruitTyping_Game_Code.py
