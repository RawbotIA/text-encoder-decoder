// A simple JavaScript game for a Hide and Seek maze
// This game will use a canvas element to draw the maze and player

// Set up the canvas and context
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

// Player properties
const player = {
  x: 50,
  y: 50,
  width: 20,
  height: 20,
  color: 'blue',
  speed: 5
};

// Obstacles representing the maze
const obstacles = [
  { x: 100, y: 0, width: 20, height: 300 },
  { x: 200, y: 150, width: 300, height: 20 },
  { x: 400, y: 0, width: 20, height: 300 },
  { x: 300, y: 300, width: 20, height: 200 }
];

// Goal to reach
const goal = {
  x: 750,
  y: 550,
  width: 30,
  height: 30,
  color: 'green'
};

// Handle player movement
let keys = {};
window.addEventListener('keydown', (e) => {
  keys[e.key] = true;
});
window.addEventListener('keyup', (e) => {
  keys[e.key] = false;
});

function updatePlayerPosition() {
  if (keys['ArrowUp']) player.y -= player.speed;
  if (keys['ArrowDown']) player.y += player.speed;
  if (keys['ArrowLeft']) player.x -= player.speed;
  if (keys['ArrowRight']) player.x += player.speed;

  // Prevent player from moving out of bounds
  player.x = Math.max(0, Math.min(canvas.width - player.width, player.x));
  player.y = Math.max(0, Math.min(canvas.height - player.height, player.y));
}

function checkCollisions() {
  // Check for collisions with obstacles
  for (let obstacle of obstacles) {
    if (
      player.x < obstacle.x + obstacle.width &&
      player.x + player.width > obstacle.x &&
      player.y < obstacle.y + obstacle.height &&
      player.y + player.height > obstacle.y
    ) {
      // Simple collision response: stop player movement
      if (keys['ArrowUp']) player.y += player.speed;
      if (keys['ArrowDown']) player.y -= player.speed;
      if (keys['ArrowLeft']) player.x += player.speed;
      if (keys['ArrowRight']) player.x -= player.speed;
    }
  }
}

function checkGoalReached() {
  if (
    player.x < goal.x + goal.width &&
    player.x + player.width > goal.x &&
    player.y < goal.y + goal.height &&
    player.y + player.height > goal.y
  ) {
    alert('You reached the goal!');
    // Reset player position
    player.x = 50;
    player.y = 50;
  }
}

function draw() {
  // Clear the canvas
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Draw player
  ctx.fillStyle = player.color;
  ctx.fillRect(player.x, player.y, player.width, player.height);

  // Draw obstacles
  ctx.fillStyle = 'red';
  for (let obstacle of obstacles) {
    ctx.fillRect(obstacle.x, obstacle.y, obstacle.width, obstacle.height);
  }

  // Draw goal
  ctx.fillStyle = goal.color;
  ctx.fillRect(goal.x, goal.y, goal.width, goal.height);
}

function gameLoop() {
  updatePlayerPosition();
  checkCollisions();
  checkGoalReached();
  draw();
  requestAnimationFrame(gameLoop);
}

// Start the game loop
gameLoop();