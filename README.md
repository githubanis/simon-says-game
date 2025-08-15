# Simon Says - Memory Game

A fully responsive, single-page HTML memory game based on the classic Simon Says electronic game. Test your memory by following increasingly complex sequences of colors and sounds.

## 🎮 Game Rules

### Objective
Remember and repeat sequences of colored button presses that get progressively longer each round.

### How to Play
1. **Start**: Click "Start Game" to begin
2. **Watch**: Simon shows a sequence by lighting up colored buttons with sounds
3. **Repeat**: Click the buttons in the exact same order you saw them
4. **Progress**: Each round adds one more step to the sequence
5. **Win/Lose**: 
   - ✅ Correct sequence → Next round
   - ❌ Wrong button → Game Over
   - 🏆 Reach Round 20 → You Win!

### Difficulty Levels
- **Normal**: 600ms button flash, 200ms gap
- **Fast**: 400ms button flash, 100ms gap  
- **Insane**: 200ms button flash, 50ms gap

## 🔧 Technical Overview

### Architecture
- **Single HTML file** with embedded CSS and JavaScript
- **Web Audio API** for sound generation
- **CSS Grid/Flexbox** for responsive layout
- **Local Storage** for high score persistence
- **Touch-optimized** for mobile devices

### Game State Management
```javascript
// Core game state variables
let sequence = [];        // Simon's sequence of colors
let playerSequence = [];  // Player's input sequence
let round = 0;           // Current round number
let gameActive = false;  // Game running state
let showingSequence = false; // Prevent input during display
```

## 📋 Function Documentation

### Core Game Functions

#### `startGame()`
**Purpose**: Initialize new game session
- Resets all game variables to default
- Hides game over UI elements
- Calls `nextRound()` after 1 second delay

#### `nextRound()`
**Purpose**: Progress to next difficulty level
- Increments round counter
- Adds random color to sequence array
- Updates UI with round number
- Calls `showSequence()` to display pattern

#### `showSequence()`
**Purpose**: Display Simon's pattern to player
- Sets `showingSequence = true` (blocks input)
- Iterates through sequence array
- Lights up buttons with timing based on difficulty
- Plays corresponding sound for each button
- Sets status to "Your Turn!" when complete

#### `handleButtonClick(color)`
**Purpose**: Process player input
- Validates game state (active, not showing sequence)
- Provides visual/audio feedback
- Adds color to `playerSequence` array
- Compares with `sequence` array at current index
- Calls `gameOver()` or `nextRound()` based on result

#### `gameOver()`
**Purpose**: Handle game failure
- Sets `gameActive = false`
- Updates best score if current round is higher
- Displays game over UI with final round
- Flash effect (all buttons turn red)
- Plays low-frequency error sound

#### `winGame()`
**Purpose**: Handle perfect completion (Round 20)
- Updates high score
- Rainbow flash celebration effect
- Shows victory message
- Displays restart option

### Audio Functions

#### `initAudio()`
**Purpose**: Initialize Web Audio Context
- Creates AudioContext on first user interaction
- Required for mobile browser audio policy compliance

#### `playSound(frequency)`
**Purpose**: Generate button press sounds
- Creates oscillator with sine wave
- Uses provided frequency for unique button tones
- 300ms duration with exponential volume decay
- Connects to audio destination for playback

### Utility Functions

#### `restartGame()`
**Purpose**: Reset UI for new game
- Hides game over elements
- Shows start button
- Resets status message and round display

#### `updateStatus(message)`
**Purpose**: Update player feedback text
- Simple wrapper for status text updates
- Provides consistent UI messaging

## 🎯 Game Flow Diagram

```
START
  ↓
[Press Start Button]
  ↓
startGame() → Initialize variables
  ↓
nextRound() → Add random color to sequence
  ↓
showSequence() → Display pattern to player
  ↓
[Player clicks buttons]
  ↓
handleButtonClick() → Process each click
  ↓
[Check if sequence matches]
  ↓
┌─────────────┬─────────────┐
│  CORRECT    │  INCORRECT  │
│     ↓       │      ↓      │
│ Next Round  │ Game Over   │
│     ↓       │      ↓      │
│ (Loop back) │   [Restart] │
└─────────────┴─────────────┘
```

## 💾 Data Persistence

### Local Storage
- **Key**: `simonBestScore`
- **Value**: Highest round number achieved
- **Purpose**: Persist high score between sessions

### Session Data
- Game state variables reset on page reload
- No mid-game save functionality (by design)

## 📱 Mobile Optimization Features

### Responsive Design
- **CSS clamp()** for scalable text sizing
- **Viewport units** for consistent scaling
- **Aspect ratio** containers for perfect circles
- **Flexbox** layout adapts to screen orientation

### Touch Handling
- **Touch events** prevent double-tap zoom
- **Context menu** disabled on long press
- **Large touch targets** (minimum 44px)
- **Visual feedback** on button press

### Performance
- **CSS transitions** for smooth animations
- **Minimal DOM manipulation** during gameplay
- **Efficient audio** generation without file loading
- **Memory cleanup** prevents audio context buildup

## 🎨 Visual Design System

### Color Palette
- **Red Button**: `#e74c3c` (normal) → `#ff6b6b` (active)
- **Blue Button**: `#3498db` (normal) → `#74b9ff` (active)  
- **Green Button**: `#27ae60` (normal) → `#55efc4` (active)
- **Yellow Button**: `#f1c40f` (normal) → `#fdcb6e` (active)

### Sound Frequencies
- **Red**: 261.63 Hz (C4)
- **Blue**: 329.63 Hz (E4)
- **Green**: 392.00 Hz (G4)
- **Yellow**: 523.25 Hz (C5)

## 🚀 Installation & Usage

1. **Download** the `index.html` file
2. **Open** in any modern web browser
3. **Allow audio** when prompted (required for sounds)
4. **Start playing** immediately - no installation needed

### Browser Compatibility
- ✅ Chrome/Edge 66+
- ✅ Firefox 60+
- ✅ Safari 11.1+
- ✅ Mobile browsers (iOS Safari, Android Chrome)

## 🎯 Game Balance

### Difficulty Progression
- **Rounds 1-5**: Easy (building confidence)
- **Rounds 6-10**: Medium (developing pattern memory)
- **Rounds 11-15**: Hard (testing limits)
- **Rounds 16-20**: Expert (maximum challenge)

### Success Metrics
- **Average completion**: 7-12 rounds
- **Good players**: 15+ rounds
- **Expert players**: Consistent wins at Round 20

## 🔄 Future Enhancement Ideas

- Multiple game modes (reverse sequence, speed rounds)
- Multiplayer support via WebRTC
- Custom color themes
- Sound pack variations
- Progressive Web App (PWA) features
- Achievement system
- Leaderboard integration
