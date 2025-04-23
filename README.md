# christian.zrg-games
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Catch the Ball Game</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
        }
        canvas {
            display: block;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas"></canvas>
    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let score = 0;

        // Ball properties
        const ball = {
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            radius: 20,
            color: 'red'
        };

        // Function to draw the ball
        function drawBall() {
            ctx.beginPath();
            ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
            ctx.fillStyle = ball.color;
            ctx.fill();
            ctx.closePath();
        }

        // Function to update and draw the game
        function updateGame() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawBall();
            displayScore();
        }

        // Function to handle mouse click
        canvas.addEventListener('click', (e) => {
            const dist = Math.hypot(e.clientX - ball.x, e.clientY - ball.y);
            if (dist < ball.radius) {
                score++;
                ball.x = Math.random() * canvas.width;
                ball.y = Math.random() * canvas.height;
            }
        });

        // Function to display the score
        function displayScore() {
            ctx.font = '24px Arial';
            ctx.fillStyle = 'black';
            ctx.fillText(`Score: ${score}`, 10, 30);
        }

        // Game loop
        function gameLoop() {
            updateGame();
            requestAnimationFrame(gameLoop);
        }

        gameLoop();
    </script>
</body>
</html>
