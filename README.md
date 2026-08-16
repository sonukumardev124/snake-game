# 🐍 Snake Game

> A classic Snake Game built from scratch using **HTML, CSS & Vanilla JavaScript** — no frameworks, no libraries, just pure JavaScript logic.

<div align="center">

**Eat 🍎 · Grow 🐍 · Score 🏆 · Survive ⚡**

</div>

---

## 🎮 About The Project

This project is a browser-based implementation of the classic **Snake Game**.

The main purpose of this project was to understand how a real-time interactive game can be built using **Vanilla JavaScript** and core browser APIs.

Instead of using a game engine or external library, the entire game logic is handled manually using:

* DOM manipulation
* JavaScript arrays & objects
* Coordinate-based movement
* Timers
* Keyboard events
* Collision detection
* Browser `localStorage`

---

## ✨ Features

| Feature           | Description                                   |
| ----------------- | --------------------------------------------- |
| 🐍 Snake Movement | Control the snake using keyboard arrows       |
| 🍎 Food System    | Food appears at random positions              |
| 📈 Score System   | Earn points by eating food                    |
| 🏆 High Score     | High score is stored using `localStorage`     |
| ⏱️ Timer          | Tracks how long the player survives           |
| 💥 Wall Collision | Game ends when the snake hits the boundary    |
| 🔄 Restart        | Restart the game after Game Over              |
| 🪟 Game Modals    | Start and Game Over screens                   |
| ⚡ Game Loop       | Continuous game updates using `setInterval()` |

---

## 🕹️ Controls

| Keyboard | Movement   |
| :------: | ---------- |
|    ⬆️    | Move Up    |
|    ⬇️    | Move Down  |
|    ⬅️    | Move Left  |
|    ➡️    | Move Right |

### 🎯 Objective

Eat as much food as possible and achieve the highest score.

Each food gives:

```text
+5 Points
```

---

## 📸 Screenshots

> Add your project screenshots here.

### Start Screen

```text
[ Add Screenshot Here ]
```

### Gameplay

```text
[ Add Screenshot Here ]
```

### Game Over

```text
[ Add Screenshot Here ]
```

You can later replace these placeholders with:

```md
![Start Screen](./screenshots/start.png)

![Gameplay](./screenshots/gameplay.png)

![Game Over](./screenshots/game-over.png)
```

---

# 🧠 How The Game Works

The game is based on a simple **grid coordinate system**.

The board is divided into blocks.

```text
┌────┬────┬────┬────┬────┐
│    │    │    │    │    │
├────┼────┼────┼────┼────┤
│    │ 🐍 │ 🐍 │    │    │
├────┼────┼────┼────┼────┤
│    │    │ 🍎 │    │    │
├────┼────┼────┼────┼────┤
│    │    │    │    │    │
└────┴────┴────┴────┴────┘
```

Every position is represented using:

```js
{
    x: row,
    y: column
}
```

For example:

```js
const snake = [
    { x: 3, y: 4 }
];
```

Here:

* `x` represents the row.
* `y` represents the column.

---

# 🔄 Game Loop

The game continuously executes the `render()` function.

```text
                ┌──────────────┐
                │   Game Start │
                └──────┬───────┘
                       ↓
                ┌──────────────┐
                │ Read Input   │
                └──────┬───────┘
                       ↓
                ┌──────────────┐
                │ Move Snake   │
                └──────┬───────┘
                       ↓
              ┌──────────────────┐
              │ Collision Check  │
              └────────┬─────────┘
                       ↓
               ┌───────┴────────┐
               │                │
             Collision        Safe
               │                │
               ↓                ↓
          Game Over        Check Food
                                │
                         ┌──────┴──────┐
                         │             │
                       Eaten         Not Eaten
                         │             │
                         ↓             ↓
                   Increase Score   Continue
                         │             │
                         └──────┬──────┘
                                ↓
                           Next Frame
```

The game loop currently runs approximately every **400ms**:

```js
intervalId = setInterval(() => {
    render();
}, 400);
```

---

# 🐍 Snake Movement

The snake's head is calculated based on its current direction.

### Moving Right

```js
head = {
    x: snake[0].x,
    y: snake[0].y + 1
};
```

### Moving Left

```js
head = {
    x: snake[0].x,
    y: snake[0].y - 1
};
```

### Moving Down

```js
head = {
    x: snake[0].x + 1,
    y: snake[0].y
};
```

### Moving Up

```js
head = {
    x: snake[0].x - 1,
    y: snake[0].y
};
```

---

# 🍎 Food System

Food is generated randomly using the board dimensions.

```js
food = {
    x: Math.floor(Math.random() * rows),
    y: Math.floor(Math.random() * cols)
};
```

When the snake reaches the food:

```text
Snake Head
    ↓
Same Position as Food?
    ↓
   YES
    ↓
Remove Food
    ↓
Generate New Food
    ↓
Grow Snake
    ↓
+5 Score
```

---

# 💥 Collision Detection

The game checks whether the snake's head has moved outside the board.

```js
if (
    head.x < 0 ||
    head.x >= rows ||
    head.y < 0 ||
    head.y >= cols
) {
    // Game Over
}
```

This prevents the snake from moving outside the game board.

---

# 🏆 High Score System

The high score is stored in the browser using:

```js
localStorage
```

This means the score can persist even after refreshing the page.

The basic flow is:

```text
Current Score
      ↓
Is Score > High Score?
      ↓
     YES
      ↓
Update High Score
      ↓
Save to localStorage
```

---

# ⏱️ Timer

The game contains a separate timer interval.

The timer follows:

```text
MM:SS
```

Example:

```text
00:01
00:02
00:03
...
```

Every second:

1. Seconds increase.
2. When seconds reach `60`, minutes increase.
3. The timer is rendered back to the UI.

---

# 🧩 DOM Architecture

The game board is dynamically generated using JavaScript.

```js
for (let row = 0; row < rows; row++) {
    for (let col = 0; col < cols; col++) {

        const block = document.createElement("div");

        block.classList.add("block");

        board.appendChild(block);

        blocks[`${row}-${col}`] = block;
    }
}
```

This allows the board to be represented using coordinates such as:

```text
0-0
0-1
0-2
1-0
1-1
1-2
```

The coordinate can then directly access the corresponding DOM block.

---

# 🗂️ Project Structure

```text
snake-game/
│
├── index.html
│
├── style.css
│
├── script.js
│
├── screenshots/
│   ├── start.png
│   ├── gameplay.png
│   └── game-over.png
│
└── README.md
```

---

# 🛠️ Tech Stack

### Frontend

* **HTML5**
* **CSS3**
* **JavaScript (ES6+)**

### Browser APIs

* DOM API
* Keyboard Events
* `localStorage`
* `setInterval()`
* `clearInterval()`

### No Dependencies

This project does **not** use:

* React
* Vue
* Angular
* jQuery
* Game Engines
* External JavaScript libraries

Everything is implemented using **Vanilla JavaScript**.

---

# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone https://github.com/your-username/snake-game.git
```

## 2. Open the Project

```bash
cd snake-game
```

## 3. Run The Game

Open `index.html` in your browser.

For development, you can also use **VS Code Live Server**.

---

# 📚 What I Learned

Building this project helped me understand several important JavaScript concepts.

### JavaScript

* Variables & scope
* Arrays
* Objects
* Functions
* Conditional logic
* Loops
* Template literals
* Array methods

### DOM

* `querySelector()`
* `createElement()`
* `appendChild()`
* `classList`
* `innerText`
* Event listeners

### Browser APIs

* Keyboard events
* `localStorage`
* Timers

### Game Development Concepts

* Game state
* Game loop
* Grid-based movement
* Coordinates
* Collision detection
* Rendering
* User input
* State updates

---

# 🔮 Future Roadmap

The current version focuses on the core Snake mechanics.

Planned improvements:

### Gameplay

* [ ] Snake self-collision
* [ ] Prevent reverse movement
* [ ] Dynamic difficulty
* [ ] Increasing snake speed
* [ ] Pause / Resume
* [ ] Multiple food types
* [ ] Obstacles
* [ ] Bonus points

### UI / UX

* [ ] Responsive game board
* [ ] Mobile controls
* [ ] Touch support
* [ ] Better animations
* [ ] Sound effects
* [ ] Background music
* [ ] Dark / Light themes

### Advanced Features

* [ ] Global leaderboard
* [ ] Player profiles
* [ ] Multiple game modes
* [ ] Difficulty selection
* [ ] Online multiplayer
* [ ] Backend leaderboard API

---

# 🐛 Known Limitations

The current version is intentionally simple and has some areas that can be improved:

* The snake currently does not have self-collision detection.
* Food can potentially spawn on the snake.
* Direction changes can be improved to prevent instant reversal.
* The game board can be made more responsive.
* Mobile/touch controls are not implemented yet.
* Game state management can be further improved.

---

# 🎯 Why This Project?

This project was built to strengthen my understanding of **JavaScript fundamentals through a practical project**.

Rather than only learning JavaScript syntax, I wanted to understand how different concepts work together in a real application:

```text
User Input
     ↓
Game State
     ↓
Logic
     ↓
State Update
     ↓
DOM Rendering
     ↓
User Sees Result
     ↓
Next Game Loop
```

This project is one step toward building more complex interactive applications.

---

# 🤝 Contributing

Contributions are welcome!

If you have an idea that can improve the project:

1. Fork the repository.
2. Create a new branch.

```bash
git checkout -b feature/new-feature
```

3. Make your changes.
4. Commit your changes.

```bash
git commit -m "Add new feature"
```

5. Push your branch.

```bash
git push origin feature/new-feature
```

6. Open a Pull Request.

---

# ⭐ Support

If you found this project useful or interesting, consider giving it a ⭐ on GitHub.

It helps support the project and motivates further development.

---

# 👨‍💻 Author

### Mandeep

Frontend / Full-Stack Developer in progress 🚀

Currently exploring:

```text
JavaScript
    ↓
Frontend
    ↓
Backend
    ↓
Full Stack
    ↓
System Design
    ↓
DevOps
```

---

<div align="center">

### 🐍 Eat the food. Grow the snake. Beat the high score.

**Built with ❤️ and Vanilla JavaScript**

⭐ If you like the project, don't forget to star the repository!

</div>
