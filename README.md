<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>هدية لبابا الغالي</title>
    <style>
        @import url('https://googleapis.com');
        
        body {
            font-family: 'Cairo', sans-serif;
            background-color: #f4f7f6;
            color: #333;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            width: 90%;
            max-width: 500px;
            background: #ffffff;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            overflow: hidden;
            text-align: center;
            padding: 30px 20px;
            border-top: 8px solid #2c3e50;
        }

        .envelope-btn {
            background-color: #2c3e50;
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 30px;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(44, 62, 80, 0.3);
            transition: transform 0.2s, background-color 0.2s;
        }

        .envelope-btn:hover {
            transform: scale(1.05);
            background-color: #34495e;
        }

        .gift-content {
            display: none;
            animation: fadeIn 1.5s ease-in-out forwards;
        }

        .heart {
            color: #e74c3c;
            font-size: 50px;
            animation: pulse 1.5s infinite;
            margin-bottom: 10px;
        }

        h1 {
            color: #2c3e50;
            font-size: 26px;
            margin-bottom: 20px;
        }

        .message {
            font-size: 18px;
            line-height: 1.8;
            color: #555;
            text-align: right;
            background: #f9fbfb;
            padding: 20px;
            border-right: 4px solid #3498db;
            border-radius: 8px;
            margin-bottom: 25px;
        }

        .photo-placeholder {
            width: 100%;
            height: 250px;
            background-color: #eaeded;
            border-radius: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #7f8c8d;
            font-size: 16px;
            margin-bottom: 20px;
            border: 2px dashed #bdc3c7;
            background-image: url('dad.jpg'); /* استبدل dad.jpg باسم صورتك لاحقاً */
            background-size: cover;
            background-position: center;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- واجهة المفاجأة الأولى -->
        <div id="welcome-screen">
            <div class="heart">🎁</div>
            <h1>إلى بابا الغالي.. أحلى وأعظم أب في الدنيا</h1>
            <p style="color: #7f8c8d; margin-bottom: 30px;">اضغط على الزر أدناه لرؤية مفاجأتك</p>
            <button class="envelope-btn" onclick="openGift()">افتح الهدية 🤍</button>
        </div>

        <!-- محتوى الهدية الذي سيظهر بعد الضغط -->
        <div id="gift-screen" class="gift-content">
            <div class="heart">❤️</div>
            <h1>كل عام وأنت سندنا وفخرنا</h1>
            
            <!-- مكان الصورة العائلية -->
            <div class="photo-placeholder">
                <!-- إذا لم تضف صورة سيظهر هذا النص، وإذا أضفت صورة سيغطي عليها -->
                <span>مكان صورتك مع بابا 📸</span>
            </div>

            <!-- الرسالة المؤثرة -->
            <div class="message">
                بابا الحبيب، <br>
                أردت أن أقدم لك هذه الهدية البسيطة لأعبر لك عن مدى حبي وامتناني لكل ما تفعله من أجلنا. <br>
                شكراً لأنك السند الدافئ، وشكراً لكل تضحية قدمتها لتجعلنا سعداء. <br>
                أدعو الله أن يحفظك لنا، ويمدك بالصحة والعافية، ويحفظ ضحكتك التي تنير حياتنا. <br><br>
                من ابنك/ابنتك المحبة دائماً..
            </div>
            
            <p style="color: #2c3e50; font-weight: bold;">أحبك يا بابا! 🥰</p>
        </div>
    </div>

    <script>
        function openGift() {
            document.getElementById('welcome-screen').style.display = 'none';
            document.getElementById('gift-screen').style.display = 'block';
        }
    </script>
</body>
</html>
