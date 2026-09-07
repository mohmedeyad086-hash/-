<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لعبة كرة قدم أونلاين</title>
    <style>
        body {
            margin: 0;
            background-color: #222;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: white;
            font-family: Arial, sans-serif;
            overflow: hidden;
        }
        canvas {
            border: 4px solid white;
            background-color: #2e7d32; /* لون الملعب الأخضر */
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
        }
    </style>
</head>
<body>

    <canvas id="gameCanvas" width="800" height="400"></canvas>

    <!-- استدعاء مكتبات الـ Firebase الرسمية لتشغيل الأونلاين -->
    <script src="https://gstatic.com"></script>
    <script src="https://gstatic.com"></script>

    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // --- 1. إعدادات كائنات ومكونات اللعبة ---
        let player1 = { x: 100, y: 200, radius: 20, color: "red", score: 0 };
        let player2 = { x: 700, y: 200, radius: 20, color: "blue", score: 0 };
        let ball = { x: 400, y: 200, radius: 12, color: "white", vx: 0, vy: 0 };

        let keys = {};

        // مراقبة ضغط الأزرار في لوحة المفاتيح
        window.addEventListener("keydown", (e) => keys[e.key] = true);
        window.addEventListener("keyup", (e) => keys[e.key] = false);

        // دوال فصل الحركة: تحريك اللاعب الأول (الأحمر)
        function movePlayer1Only() {
            if (keys["w"] || keys["W"]) player1.y -= 4;
            if (keys["s"] || keys["S"]) player1.y += 4;
            if (keys["a"] || keys["A"]) player1.x -= 4;
            if (keys["d"] || keys["D"]) player1.x += 4;
            keepInBounds(player1);
        }

        // دوال فصل الحركة: تحريك اللاعب الثاني (الأزرق)
        function movePlayer2Only() {
            if (keys["ArrowUp"] || keys["w"] || keys["W"]) player2.y -= 4;
            if (keys["ArrowDown"] || keys["s"] || keys["S"]) player2.y += 4;
            if (keys["ArrowLeft"] || keys["a"] || keys["A"]) player2.x -= 4;
            if (keys["ArrowRight"] || keys["d"] || keys["D"]) player2.x += 4;
            keepInBounds(player2);
        }

        // منع الكرات واللاعبين من الخروج عن حدود شاشة اللعبة
        function keepInBounds(player) {
            if (player.x - player.radius < 0) player.x = player.radius;
            if (player.x + player.radius > canvas.width) player.x = canvas.width - player.radius;
            if (player.y - player.radius < 0) player.y = player.radius;
            if (player.y + player.radius > canvas.height) player.y = canvas.height - player.radius;
        }

        // --- 2. فيزياء الكرة والاصطدام والأهداف ---
        function updateBall() {
            ball.x += ball.vx;
            ball.y += ball.vy;

            // احتكاك لتقليل سرعة الكرة تدريجياً لتبدو واقعية
            ball.vx *= 0.98;
            ball.vy *= 0.98;

            // ارتداد الكرة من الحوائط العلوية والسفلية
            if (ball.y - ball.radius < 0 || ball.y + ball.radius > canvas.height) {
                ball.vy = -ball.vy;
            }

            // فحص تسجيل الأهداف داخل الشباك (المرمى بين الإحداثي Y 150 و 250)
            if (ball.x < 0) {
                if (ball.y > 150 && ball.y < 250) { player2.score++; resetBall(); } 
                else { ball.vx = -ball.vx; ball.x = ball.radius; }
            }
            if (ball.x > canvas.width) {
                if (ball.y > 150 && ball.y < 250) { player1.score++; resetBall(); } 
                else { ball.vx = -ball.vx; ball.x = canvas.width - ball.radius; }
            }

            // فحص اصطدام اللاعبين بالكرة لركلها
            checkCollision(player1);
            checkCollision(player2);
        }

        function checkCollision(player) {
            let dx = ball.x - player.x;
            let dy = ball.y - player.y;
            let distance = Math.sqrt(dx * dx + dy * dy);

            if (distance < player.radius + ball.radius) {
                let angle = Math.atan2(dy, dx);
                ball.vx = Math.cos(angle) * 7;
                ball.vy = Math.sin(angle) * 7;
            }
        }

        function resetBall() {
            ball.x = canvas.width / 2;
            ball.y = canvas.height / 2;
            ball.vx = 0;
            ball.vy = 0;
        }

        // --- 3. رسم غرافيك اللعبة على الشاشة ---
        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // رسم خطوط الملعب
            ctx.strokeStyle = "rgba(255,255,255,0.6)";
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(canvas.width / 2, 0);
            ctx.lineTo(canvas.width / 2, canvas.height);
            ctx.stroke();
            ctx.beginPath();
            ctx.arc(canvas.width / 2, canvas.height / 2, 60, 0, Math.PI * 2);
            ctx.stroke();

            // رسم المرمى يمين ويسار
            ctx.fillStyle = "white";
            ctx.fillRect(0, 150, 8, 100);
            ctx.fillRect(canvas.width - 8, 150, 8, 100);

            // رسم اللاعب 1 (الأحمر)
            ctx.fillStyle = player1.color;
            ctx.beginPath();
            ctx.arc(player1.x, player1.y, player1.radius, 0, Math.PI * 2);
            ctx.fill();

            // رسم اللاعب 2 (الأزرق)
            ctx.fillStyle = player2.color;
            ctx.beginPath();
            ctx.arc(player2.x, player2.y, player2.radius, 0, Math.PI * 2);
            ctx.fill();

            // رسم الكرة
            ctx.fillStyle = ball.color;
            ctx.beginPath();
            ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
            ctx.fill();

            // طباعة النتيجة في الأعلى
            ctx.font = "bold 32px Arial";
            ctx.fillStyle = "white";
            ctx.fillText(player1.score, canvas.width / 2 - 60, 45);
            ctx.fillText(player2.score, canvas.width / 2 + 35, 45);
        }

        // --- 4. إعدادات الأونلاين عبر Firebase ---
        
        // ⚠️ قم بتعديل البيانات بالأسفل ببيانات مشروعك التي حصلت عليها من موقع Firebase لتشغيل الأونلاين
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_AUTH_DOMAIN",
            databaseURL: "YOUR_DATABASE_URL",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_STORAGE_BUCKET",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };

        // تشغيل مكتبة Firebase
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        // حجز غرفة رقم 1 داخل السيرفر
        const gameRoom = db.ref("rooms/room1");
        let playerRole = null; 

        // نظام التحقق وتعيين الأدوار (من يدخل أولاً يكون الأحمر ومن يدخل ثانياً يكون الأزرق)
        gameRoom.once("value", (snapshot) => {
            const data = snapshot.val();
            if (!data || !data.p1_online) {
                playerRole = "player1";
                gameRoom.update({ p1_online: true });
                console.log("تم دخولك كاللاعب الأول");
            } else if (!data.p2_online) {
                playerRole = "player2";
                gameRoom.update({ p2_online: true });
                console.log("تم دخولك كاللاعب الثاني");
            } else {
                alert("الغرفة ممتلئة! يمكنك الانتظار أو المشاهدة.");
            }
        });

        // عند الخروج أو إغلاق الصفحة يتم تحرير مكان اللاعب بالسيرفر تلقائياً
        window.addEventListener("beforeunload", () => {
            if (playerRole === "player1") gameRoom.update({ p1_online: false });
            if (playerRole === "player2") gameRoom.update({ p2_online: false });
        });

        // الاستماع المستمر لتغيرات حركة الخصم من السيرفر وتحديث شاشتك
        gameRoom.on("value", (snapshot) => {
            const data = snapshot.val();
            if (data) {
                // إذا كنت اللاعب الثاني، قم بأخذ مواقع الكرة واللاعب الأول والنتيجة من السيرفر
                if (playerRole === "player2") {
                    if (data.p1_x) player1.x = data.p1_x;
                    if (data.p1_y) player1.y = data.p1_y;
                    if (data.ball_x) ball.x = data.ball_x;
                    if (data.ball_y) ball.y = data.ball_y;
                    if (data.p1_score !== undefined) player1.score = data.p1_score;
                    if (data.p2_score !== undefined) player2.score = data.p2_score;
                }
                // إذا كنت اللاعب الأول، قم بأخذ موقع اللاعب الثاني فقط
                if (playerRole === "player1") {
                    if (data.p2_x) player2.x = data.p2_x;
                    if (data.p2_y) player2.y = data.p2_y;
                }
            }
        });

        // --- 5. حلقة اللعبة الرئيسية (Game Loop) ---
        function gameLoop() {
            if (playerRole === "player1") {
                movePlayer1Only();
                updateBall(); // اللاعب الأول يدير فيزياء الكرة ويرفعها للسيرفر
                gameRoom.update({
                    p1_x: player1.x,
                    p1_y: player1.y,
                    ball_x: ball.x,
                    ball_y: ball.y,
                    p1_score: player1.score,
                    p2_score: player2.score
                });
            } else if (playerRole === "player2") {
                movePlayer2Only();
                gameRoom.update({
                    p2_x: player2.x,
                    p2_y: player2.y
                });
            }

            draw();
            requestAnimationFrame(gameLoop);
        }

        // بدء تشغيل اللعبة فوراً
        gameLoop();
    </script>
</body>
</html>
