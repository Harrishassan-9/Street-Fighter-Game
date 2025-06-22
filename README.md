# 🥋 Street Fighter Bot Project

This project implements an AI bot for playing Street Fighter using a Python-based interface that communicates with the BizHawk emulator. Designed to operate as either Player 1 or Player 2, it includes extensive data logging for analysis and potential machine learning applications.

---

## Project Overview

The Street Fighter Bot provides:
- Real-time gameplay interaction with the BizHawk emulator
- Rule-based AI with strategic decision-making
- Detailed logging for gameplay analytics
- Optional neural network integration for advanced learning

---

## Architecture & Components

### 1. Game Interface Layer (`controller.py`)
- Manages socket communication with the BizHawk emulator on ports `9999` (Player 1) and `10000` (Player 2)
- Handles JSON serialization/deserialization of game state and commands
- Implements connection management with timeout handling and error recovery

### 2. Game State Representation (`game_state.py`, `player.py`)
- Represents the full game state, including both players
- Tracks player positions, health, movement status, and game mechanics like jumping and crouching

### 3. Control System (`buttons.py`, `command.py`)
- Maps to standard Street Fighter controls (directional pad and six action buttons)
- Supports complex button combinations for special moves and combos

### 4. Bot Intelligence (`bot.py`)
- Uses rule-based logic for decision making
- Adapts strategy based on player distance and state
- Supports strategies like:
  - Combo attacks
  - Jump attacks
  - Projectile attacks
  - Movement
  - Defensive blocking

---

## Bot Behavior System

### Distance-Based Strategy Selection
- **Long Range (>60 pixels)**: Uses aggressive combos, jump attacks, and projectiles
- **Mid Range**: Balanced movement and positioning
- **Close Range (<60 pixels)**: Focus on blocking and reactive movement

### Available Strategies
1. **Combo Attacks** – High-damage sequences using complex inputs
2. **Jump Attacks** – Aerial offensive maneuvers
3. **Projectile Attacks** – Long-range fire attacks
4. **Movement** – Positioning and spacing control
5. **Defensive Blocking** – Crouch blocking to reduce incoming damage

---

## Data Collection & Analytics

### Logging System (`logger.py`)
Captures:
- Timestamps of actions and game states
- Health, position, and movement status for both players
- All bot decisions and button inputs
- Game context like round, timer, and results
- Strategy metrics including distance and player actions

### Data Schema (21 Fields per Action)
- `timestamp`, `player`, `round`, `action`, `player1_health`, `player2_health`,  
  `player1_x`, `player1_y`, `player2_x`, `player2_y`, `distance`,  
  `player1_jumping`, `player2_jumping`, `player1_crouching`, `player2_crouching`,  
  `player1_in_move`, `player2_in_move`, `player1_move_id`, `player2_move_id`,  
  `timer`, `result`

### Dataset
- **Main Dataset**: `bot_moves.csv` (~18MB)
- **Session Logs**: Timestamped files per training/testing session
- **ML Model**: `bot_mlp_model.h5` (192KB) - a trained Multi-Layer Perceptron

---

## Neural Network Integration

Although `bot.py` currently uses rule-based logic, the project supports a neural network model:

1. **Data Collection** – Gameplay data used for training
2. **Model Development** – MLP trained using logged game data
3. **Future Integration** – MLP model can replace or augment rule-based AI

---

## Technical Implementation Details

### Communication Protocol
- Socket communication with BizHawk emulator
- JSON format for structured state and command exchange
- Robust error handling and reconnection logic

### Performance Features
- Tracks session stats: rounds, actions, duration
- Can act as either player
- Designed for continuous training and testing sessions

### Code Quality
- Modular, maintainable structure
- Clear separation between interface, logic, and data collection
- Exception handling and detailed error logging

---

## Key Achievements

1. Real-time integration with BizHawk emulator
2. Full-featured data logging system
3. Strategic rule-based bot implementation
4. Trained MLP neural network using gameplay data
5. Scalable and modular system for continuous development

---

## Conclusion

This project presents a complete AI pipeline from emulator integration to data logging and machine learning, serving as a robust foundation for advanced AI research in fighting games.

The combination of rule-based strategies, data-driven insights, and future neural network integration makes this bot a strong candidate for competitive development and academic exploration.

