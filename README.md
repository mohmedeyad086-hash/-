<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لعبة كرة قدم واقعية</title>
    <style>
        body {
            margin: 0;
            background-color: #222;
            color: white;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            overflow: hidden;
        }
        #scoreboard {
            font-size: 24px;
            margin-bottom: 10px;
            font-weight: bold;
        }
        canvas {
            background-color: #387344;
            border: 5px solid white;
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
        }
        .controls {
            margin-top: 15px;
            font-size: 14px;
            color: #aaa;
        }
    </style>
</head>
<body>

    <div id="scoreboard">اللاعب 1: <span id="p1Score">0</span> | اللاعب 2: <span id="p2Score">0</span></div>
    <canvas id="gameCanvas" width="800" height="400"></canvas>
    
    <div class="controls">
        **التحكم:** اللاعب 1 (الأزرق): W, A, S, D | اللاعب 2 (الأحمر): الأسهم الإتجاهية
    </div>

    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // النتيجة
        let score1 = 0;
        let score2 = 0;

        // إعدادات اللاعبين
        const player1 = { x: 100, y: 200, radius: 20, color: "#007bff", speed: 4 };
        const player2 = { x: 700, y: 200, radius: 20, color: "#dc3545", speed: 4 };

        // إعدادات الكرة
        const ball = { x: 400, y: 200, radius: 12, color: "white", vx: 0, vy: 0, friction: 0.98 };

        // المرمى
        const goalWidth = 10;
        const goalHeight = 100;
        const goalY = (canvas.height - goalHeight) / 2;

        // أزرار التحكم
        const keys = {};

        window.addEventListener("keydown", (e) => keys[e.code] = true);
        window.addEventListener("keyup", (e) => keys[e.code] = false);

        function reset() {
            ball.x = canvas.width / 2;
            ball.y = canvas.height / 2;
            ball.vx = 0;
            ball.vy = 0;
            player1.x = 100; player1.y = 200;
            player2.x = 700; player2.y = 200;
        }

        function checkCollision(p, b) {
            let dx = b.x - p.x;
            let dy = b.y - p.y;
            let distance = Math.sqrt(dx * dx + dy * dy);

            if (distance < p.radius + b.radius) {
                let angle = Math.atan2(dy, dx);
                let speed = 6; // قوة التسديد عند اللمس
                b.vx = Math.cos(angle) * speed;
                b.vy = Math.sin(angle) * speed;
            }
        }

        function update() {
            // حركة اللاعب 1 (W, A, S, D)
            if (keys["KeyW"] && player1.y > player1.radius) player1.y -= player1.speed;
            if (keys["KeyS"] && player1.y < canvas.height - player1.radius) player1.y += player1.speed;
            if (keys["KeyA"] && player1.x > player1.radius) player1.x -= player1.speed;
            if (keys["KeyD"] && player1.x < canvas.width - player1.radius) player1.x += player1.speed;

            // حركة اللاعب 2 (الأسهم)
            if (keys["ArrowUp"] && player2.y > player2.radius) player2.y -= player2.speed;
            if (keys["ArrowDown"] && player2.y < canvas.height - player2.radius) player2.y += player2.speed;
            if (keys["ArrowLeft"] && player2.x > player2.radius) player2.x -= player2.speed;
            if (keys["ArrowRight"] && player2.x < canvas.width - player2.radius) player2.x += player2.speed;

            // حركة الكرة والفيزياء
            ball.x += ball.vx;
            ball.y += ball.vy;
            ball.vx *= ball.friction;
            ball.vy *= ball.friction;

            // اصطدام الكرة بالجدران
            if (ball.y - ball.radius < 0 || ball.y + ball.radius > canvas.height) {
                ball.vy = -ball.vy;
            }

            // اصطدام الكرة باللاعبين
            checkCollision(player1, ball);
            checkCollision(player2, ball);

            // التحقق من الأهداف
            if (ball.x < 0) {
                if (ball.y > goalY && ball.y < goalY + goalHeight) {
                    score2++;
                    document.getElementById("p2Score").innerText = score2;
                    reset();
                } else {
                    ball.vx = -ball.vx;
                }
            }
            if (ball.x > canvas.width) {
                if (ball.y > goalY && ball.y < goalY + goalHeight) {
                    score1++;
                    document.getElementById("p1Score").innerText = score1;
                    reset();
                } else {
                    ball.vx = -ball.vx;
                }
            }
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // خطوط الملعب
            ctx.strokeStyle = "rgba(255,255,255,0.3)";
            ctx.lineWidth = 4;
            ctx.beginPath();
            ctx.moveTo(canvas.width / 2, 0);
            ctx.lineTo(canvas.width / 2, canvas.height);
            ctx.stroke();

            ctx.beginPath();
            ctx.arc(canvas.width / 2, canvas.height / 2, 50, 0, Math.PI * 2);
            ctx.stroke();

            // المرمى الأيسر والأيمن
            ctx.fillStyle = "white";
            ctx.fillRect(0, goalY, goalWidth, goalHeight);
            ctx.fillRect(canvas.width - goalWidth, goalY, goalWidth, goalHeight);

            // رسم اللاعب 1
            ctx.fillStyle = player1.color;
            ctx.beginPath();
            ctx.arc(player1.x, player1.y, player1.radius, 0, Math.PI * 2);
            ctx.fill();

            // رسم اللاعب 2
            ctx.fillStyle = player2.color;
            ctx.beginPath();
            ctx.arc(player2.x, player2.y, player2.radius, 0, Math.PI * 2);
            ctx.fill();

            // رسم الكرة
            ctx.fillStyle = ball.color;
            ctx.beginPath();
            ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
            ctx.fill();
        }

        function gameLoop() {
            update();
            draw();
            requestAnimationFrame(gameLoop);
        }

        gameLoop();
    </script>
</body>
</html>
