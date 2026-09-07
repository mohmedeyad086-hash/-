<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لعبة كرة قدم - شخصين</title>
    <style>
        body { margin: 0; background-color: #222; display: flex; justify-content: center; align-items: center; height: 100vh; color: white; font-family: Arial, sans-serif; overflow: hidden; }
        canvas { border: 4px solid white; background-color: #2e7d32; box-shadow: 0 10px 20px rgba(0,0,0,0.5); }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="800" height="400"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        let player1 = { x: 100, y: 200, radius: 20, color: "red", score: 0 };
        let player2 = { x: 700, y: 200, radius: 20, color: "blue", score: 0 };
        let ball = { x: 400, y: 200, radius: 12, color: "white", vx: 0, vy: 0 };
        let keys = {};

        window.addEventListener("keydown", (e) => keys[e.key] = true);
        window.addEventListener("keyup", (e) => keys[e.key] = false);

        function movePlayers() {
            if (keys["w"] || keys["W"]) player1.y -= 5;
            if (keys["s"] || keys["S"]) player1.y += 5;
            if (keys["a"] || keys["A"]) player1.x -= 5;
            if (keys["d"] || keys["D"]) player1.x += 5;

            if (keys["ArrowUp"]) player2.y -= 5;
            if (keys["ArrowDown"]) player2.y += 5;
            if (keys["ArrowLeft"]) player2.x -= 5;
            if (keys["ArrowRight"]) player2.x += 5;

            keepInBounds(player1);
            keepInBounds(player2);
        }

        function keepInBounds(player) {
            if (player.x - player.radius < 0) player.x = player.radius;
            if (player.x + player.radius > canvas.width) player.x = canvas.width - player.radius;
            if (player.y - player.radius < 0) player.y = player.radius;
            if (player.y + player.radius > canvas.height) player.y = canvas.height - player.radius;
        }

        function updateBall() {
            ball.x += ball.vx; ball.y += ball.vy;
            ball.vx *= 0.98; ball.vy *= 0.98;

            if (ball.y - ball.radius < 0 || ball.y + ball.radius > canvas.height) ball.vy = -ball.vy;

            if (ball.x < 0) {
                if (ball.y > 150 && ball.y < 250) { player2.score++; resetBall(); } 
                else { ball.vx = -ball.vx; ball.x = ball.radius; }
            }
            if (ball.x > canvas.width) {
                if (ball.y > 150 && ball.y < 250) { player1.score++; resetBall(); } 
                else { ball.vx = -ball.vx; ball.x = canvas.width - ball.radius; }
            }
            checkCollision(player1); checkCollision(player2);
        }

        function checkCollision(player) {
            let dx = ball.x - player.x, dy = ball.y - player.y;
            let distance = Math.sqrt(dx * dx + dy * dy);
            if (distance < player.radius + ball.radius) {
                let angle = Math.atan2(dy, dx);
                ball.vx = Math.cos(angle) * 7; ball.vy = Math.sin(angle) * 7;
            }
        }

        function resetBall() { ball.x = canvas.width / 2; ball.y = canvas.height / 2; ball.vx = 0; ball.vy = 0; }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.strokeStyle = "rgba(255,255,255,0.6)"; ctx.lineWidth = 2;
            ctx.beginPath(); ctx.moveTo(canvas.width / 2, 0); ctx.lineTo(canvas.width / 2, canvas.height); ctx.stroke();
            ctx.beginPath(); ctx.arc(canvas.width / 2, canvas.height / 2, 60, 0, Math.PI * 2); ctx.stroke();
            ctx.fillStyle = "white"; ctx.fillRect(0, 150, 8, 100); ctx.fillRect(canvas.width - 8, 150, 8, 100);

            ctx.fillStyle = player1.color; ctx.beginPath(); ctx.arc(player1.x, player1.y, player1.radius, 0, Math.PI * 2); ctx.fill();
            ctx.fillStyle = player2.color; ctx.beginPath(); ctx.arc(player2.x, player2.y, player2.radius, 0, Math.PI * 2); ctx.fill();
            ctx.fillStyle = ball.color; ctx.beginPath(); ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2); ctx.fill();

            ctx.font = "bold 32px Arial"; ctx.fillStyle = "white";
            ctx.fillText(player1.score, canvas.width / 2 - 60, 45); ctx.fillText(player2.score, canvas.width / 2 + 35, 45);
        }

        function gameLoop() { movePlayers(); updateBall(); draw(); requestAnimationFrame(gameLoop); }
        gameLoop();
    </script>
</body>
</html>
