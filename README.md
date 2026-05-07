<!DOCTYPE html><html lang="en"><head>    <meta charset="UTF-8">    <meta name="viewport" content="width=device-width, initial-scale=1.0">    <title>Car Game</title>    <style>        body {            display: flex;            justify-content: center;            align-items: center;            height: 100vh;            margin: 0;            background-color: #f0f0f0;        }        canvas {            border: 2px solid #000;            background-color: #333;        }        #score {            position: absolute;            top: 10px;            left: 10px;            color: white;            font-size: 20px;        }    </style></head><body>    <div id="score">Score: 0</div>    <canvas id="gameCanvas" width="400" height="600"></canvas>    <script>        const canvas = document.getElementById('gameCanvas');        const ctx = canvas.getContext('2d');        const scoreDisplay = document.getElementById('score');        let car = { x: 175, y: 500, width: 50, height: 80 };        let obstacles = [];        let score = 0;        let gameRunning = true;        // Draw car        function drawCar() {            // Car body            ctx.fillStyle = 'orange';            ctx.fillRect(car.x + 5, car.y + 10, 40, 60);            // Car roof            ctx.fillStyle = 'orange';            ctx.fillRect(car.x + 10, car.y + 5, 30, 20);            // Wheels            ctx.fillStyle = 'black';            ctx.beginPath();            ctx.arc(car.x + 15, car.y + 70, 8, 0, Math.PI * 2);            ctx.fill();            ctx.beginPath();            ctx.arc(car.x + 35, car.y + 70, 8, 0, Math.PI * 2);            ctx.fill();            // Spoiler            ctx.fillStyle = 'black';            ctx.fillRect(car.x + 20, car.y, 10, 5);        }        // Draw obstacles        function drawObstacles() {            ctx.fillStyle = 'blue';            obstacles.forEach(obstacle => {                // Obstacle car body                ctx.fillRect(obstacle.x + 5, obstacle.y + 10, 40, 60);                // Obstacle car roof                ctx.fillRect(obstacle.x + 10, obstacle.y + 5, 30, 20);                // Wheels                ctx.fillStyle = 'black';                ctx.beginPath();                ctx.arc(obstacle.x + 15, obstacle.y + 70, 8, 0, Math.PI * 2);                ctx.fill();                ctx.beginPath();                ctx.arc(obstacle.x + 35, obstacle.y + 70, 8, 0, Math.PI * 2);                ctx.fill();                // Reset color                ctx.fillStyle = 'blue';            });        }        // Update game        function update() {            if (!gameRunning) return;            // Move obstacles down            obstacles.forEach(obstacle => {                obstacle.y += 5;            });            // Remove off-screen obstacles            obstacles = obstacles.filter(obstacle => obstacle.y < canvas.height);            // Add new obstacles            if (Math.random() < 0.02) {
                obstacles.push({
                    x: Math.random() * (canvas.width - 50),
                    y: -50,
                    width: 50,
                    height: 50
                });
            }

            // Check collisions
            obstacles.forEach(obstacle => {
                if (car.x < obstacle.x + obstacle.width &&
                    car.x + car.width > obstacle.x &&
                    car.y < obstacle.y + obstacle.height &&
                    car.y + car.height > obstacle.y) {
                    gameRunning = false;
                    alert('Game Over! Score: ' + score);
                }
            });

            // Increase score
            score++;
            scoreDisplay.textContent = 'Score: ' + score;
        }

        // Draw everything
        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawCar();
            drawObstacles();
        }

        // Game loop
        function gameLoop() {
            update();
            draw();
            requestAnimationFrame(gameLoop);
        }

        // Handle keyboard input
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft' && car.x > 0) {
                car.x -= 10;
            } else if (e.key === 'ArrowRight' && car.x < canvas.width - lamborgini
        
        .width) {
                car.x += 10;
            }
        });

        // Start game
        gameLoop();
    </script>
</body>
</html>
