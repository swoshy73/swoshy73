<!DOCTYPE html>
<html>
<head>
    <title>Interactive Profile Animation</title>
    <style>
        canvas { display: block; margin: auto; }
        #pieChart { width: 200px; height: 200px; }
    </style>
</head>
<body>

<h2>Interactive Snake Animation</h2>
<canvas id="snakeCanvas" width="400" height="400"></canvas>

<h2>Pie Chart Representation</h2>
<canvas id="pieChart" width="200" height="200"></canvas>

<script>
    // Snake Animation
    const canvas = document.getElementById('snakeCanvas');
    const ctx = canvas.getContext('2d');
    let snake = [{x: 50, y: 50}];
    let dx = 5;
    let loop = setInterval(drawSnake, 100);

    function drawSnake() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (let segment of snake) {
            ctx.fillStyle = 'green';
            ctx.fillRect(segment.x, segment.y, 10, 10);
            segment.x += dx;
            if (segment.x > canvas.width) segment.x = 0; // Loop
        }
    }

    // Pie Chart Animation
    const pieCtx = document.getElementById('pieChart').getContext('2d');
    const data = [99, 1]; // 99% Python, 1% HTML
    let currentAngle = 0;
    const animatePieChart = setInterval(() => {
        pieCtx.clearRect(0, 0, 200, 200);
        currentAngle = (currentAngle + 1) % 360;
        let startAngle = ((2 * Math.PI) / 360) * currentAngle;

        pieCtx.beginPath();
        pieCtx.moveTo(100, 100);
        pieCtx.arc(100, 100, 100, 0, (Math.PI * 2) * (data[0] / 100));
        pieCtx.closePath();
        pieCtx.fillStyle = 'blue';
        pieCtx.fill();

        pieCtx.beginPath();
        pieCtx.moveTo(100, 100);
        pieCtx.arc(100, 100, 100, (Math.PI * 2) * (data[0] / 100), (Math.PI * 2));
        pieCtx.closePath();
        pieCtx.fillStyle = 'orange';
        pieCtx.fill();
    }, 100);
</script>

</body>
</html>
