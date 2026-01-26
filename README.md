# 👋 Welcome to my GitHub Profile!

Click the button below to see my **Snake Animation** and **Skills Chart**:

<button onclick="toggleDisplay()" style="padding: 10px 20px; font-size: 16px; background-color: #238636; color: white; border: none; border-radius: 6px; cursor: pointer;">
  🐍 Show Animation & Skills 🐍
</button>

<div id="animationContainer" style="display: none; margin-top: 30px;">

### Snake Animation
<canvas id="snakeCanvas" width="400" height="400" style="border: 2px solid #238636; background-color: #0d1117; display: block; margin: 20px auto;"></canvas>

### My Skills Distribution
<canvas id="chartCanvas" width="400" height="400" style="border: 2px solid #238636; background-color: #0d1117; display: block; margin: 20px auto;"></canvas>

</div>

<script>
function toggleDisplay() {
  const container = document.getElementById('animationContainer');
  if (container.style.display === 'none') {
    container.style.display = 'block';
    startSnakeAnimation();
    drawSkillsChart();
  } else {
    container.style.display = 'none';
  }
}

// Snake Animation
function startSnakeAnimation() {
  const canvas = document.getElementById('snakeCanvas');
  const ctx = canvas.getContext('2d');
  
  const gridSize = 20;
  let snake = [{x: 10, y: 10}];
  let direction = {x: 1, y: 0};
  let nextDirection = {x: 1, y: 0};
  
  function drawSnake() {
    ctx.fillStyle = '#00ff00';
    snake.forEach((segment, index) => {
      ctx.fillRect(segment.x * gridSize, segment.y * gridSize, gridSize - 2, gridSize - 2);
      if (index === 0) {
        ctx.fillStyle = '#00dd00';
      }
    });
  }
  
  function update() {
    direction = nextDirection;
    const head = {x: snake[0].x + direction.x, y: snake[0].y + direction.y};
    
    // Wrap around edges
    head.x = (head.x + canvas.width / gridSize) % (canvas.width / gridSize);
    head.y = (head.y + canvas.height / gridSize) % (canvas.height / gridSize);
    
    snake.unshift(head);
    snake.pop();
  }
  
  function draw() {
    ctx.fillStyle = '#0d1117';
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.strokeStyle = '#30363d';
    
    for (let i = 0; i <= canvas.width; i += gridSize) {
      ctx.beginPath();
      ctx.moveTo(i, 0);
      ctx.lineTo(i, canvas.width);
      ctx.stroke();
    }
    
    for (let i = 0; i <= canvas.height; i += gridSize) {
      ctx.beginPath();
      ctx.moveTo(0, i);
      ctx.lineTo(canvas.width, i);
      ctx.stroke();
    }
    
    drawSnake();
  }
  
  // Auto-turn the snake
  const directions = [{x: 1, y: 0}, {x: 0, y: 1}, {x: -1, y: 0}, {x: 0, y: -1}];
  let directionIndex = 0;
  
  setInterval(() => {
    nextDirection = directions[directionIndex];
    directionIndex = (directionIndex + 1) % directions.length;
  }, 2000);
  
  setInterval(() => {
    update();
    draw();
  }, 100);
  
  draw();
}

// Pie Chart for Skills
function drawSkillsChart() {
  const canvas = document.getElementById('chartCanvas');
  const ctx = canvas.getContext('2d');
  
  const centerX = canvas.width / 2;
  const centerY = canvas.height / 2;
  const radius = 100;
  
  // Background
  ctx.fillStyle = '#0d1117';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  // Python (99%)
  ctx.fillStyle = '#3776ab';
  ctx.beginPath();
  ctx.arc(centerX, centerY, radius, 0, (99 / 100) * 2 * Math.PI);
  ctx.lineTo(centerX, centerY);
  ctx.fill();
  
  // HTML (1%)
  ctx.fillStyle = '#e34c26';
  ctx.beginPath();
  ctx.arc(centerX, centerY, radius, (99 / 100) * 2 * Math.PI, 2 * Math.PI);
  ctx.lineTo(centerX, centerY);
  ctx.fill();
  
  // Draw labels
  ctx.fillStyle = '#ffffff';
  ctx.font = 'bold 16px Arial';
  ctx.textAlign = 'center';
  ctx.fillText('Python: 99%', centerX - 60, centerY - 40);
  
  ctx.fillStyle = '#ffffff';
  ctx.font = 'bold 14px Arial';
  ctx.fillText('HTML: 1%', centerX + 70, centerY + 30);
}
</script>

---

### About Me
- 🐍 Python Enthusiast
- 💻 Building projects with modern tech
- 🎮 Love creating interactive experiences

**Feel free to explore my repositories!**
