# 🍎 Fruit Catcher: A Retro Typing Game

A fast-paced, arcade-style typing game built with the **Pyxel** retro game engine. This project combines classic "catcher" mechanics with typing challenges to improve keyboard speed and accuracy.

## 🎮 Gameplay
The objective is to catch as much fruit as possible. However, the fruit is out of reach of your catcher until you **type its name**!

* **Targeting:** Click a fruit to make it "glow" and become your active target.
* **Typing:** Type the fruit's name (e.g., "apple", "banana") and press **Enter** to turn it into a star.
* **Catching:** Move your catcher with the **Arrow Keys** to collect the falling stars.
* **Avoid Bombs:** Do not type when a bomb is glowing, or you will lose a life!
* **Dynamic Difficulty:** The game speeds up every 5 points, testing your reflexes.

## 🛠️ Technical Features
* **Object-Oriented Programming (OOP):** Modular classes for `Fruit`, `Catcher`, and `Star`.
* **Dynamic Difficulty Scaling:** Speed and spawn intervals adjust based on your score.
* **Asset Integration:** Custom `.pyxres` file for pixel art and audio.

## 🚀 Setup & Installation

### Prerequisites
* Python 3.x
* Pyxel library

### Installation
1. **Install Pyxel:**
   ```bash
   pip install pyxel
   
2. **Run the game:**
   ```bash
   python your_filename.py
