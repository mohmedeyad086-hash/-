<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>كريستيانو رونالدو | CR7 Legend</title>
    <style>
        :root {
            --primary-color: #7a1212; /* لون النصر والبرتغال */
            --accent-color: #e6b800; /* اللون الذهبي للجوائز */
            --bg-dark: #111111;
            --bg-light: #1e1e1e;
            --text-color: #ffffff;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-color);
            line-height: 1.6;
        }

        header {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('https://unsplash.com') no-repeat center center/cover;
            height: 60vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            border-bottom: 4px solid var(--accent-color);
        }

        header h1 {
            font-size: 3.5rem;
            color: var(--text-color);
            text-shadow: 2px 2px 10px rgba(0,0,0,0.5);
            margin-bottom: 10px;
        }

        header p {
            font-size: 1.5rem;
            color: var(--accent-color);
            font-weight: bold;
        }

        nav {
            background-color: var(--bg-light);
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 5px rgba(0,0,0,0.5);
            display: flex;
            justify-content: center;
            padding: 15px;
        }

        nav a {
            color: var(--text-color);
            text-decoration: none;
            margin: 0 20px;
            font-size: 1.1rem;
            font-weight: bold;
            transition: color 0.3s;
        }

        nav a:hover {
            color: var(--accent-color);
        }

        .container {
            max-width: 1200px;
            margin: 40px auto;
            padding: 0 20px;
        }

        section {
            margin-bottom: 60px;
            scroll-margin-top: 80px;
        }

        h2 {
            font-size: 2.2rem;
            border-right: 5px solid var(--primary-color);
            padding-right: 15px;
            margin-bottom: 30px;
            color: var(--accent-color);
        }

        /* قسم الإحصائيات */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
        }

        .stat-card {
            background-color: var(--bg-light);
            padding: 30px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid #333;
            transition: transform 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-5px);
            border-color: var(--accent-color);
        }

        .stat-card h3 {
            font-size: 2.5rem;
            color: var(--accent-color);
            margin-bottom: 10px;
        }

        /* قسم الأهداف والفيديوهات */
        .video-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
        }

        .video-card {
            background-color: var(--bg-light);
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        .video-wrapper {
            position: relative;
            padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
            height: 0;
        }

        .video-wrapper iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: 0;
        }

        .video-info {
            padding: 15px;
        }

        .video-info h4 {
            font-size: 1.2rem;
            margin-bottom: 5px;
            color: var(--text-color);
        }

        /* السيرة الذاتية */
        .info-box {
            background-color: var(--bg-light);
            padding: 30px;
            border-radius: 10px;
            border-left: 4px solid var(--primary-color);
        }

        .info-box ul {
            list-style: none;
            margin-top: 15px;
        }

        .info-box li {
            margin-bottom: 12px;
            font-size: 1.1rem;
        }

        .info-box strong {
            color: var(--accent-color);
        }

        footer {
            text-align: center;
            padding: 30px;
            background-color: var(--bg-light);
            color: #888;
            border-top: 1px solid #333;
        }
    </style>
</head>
<body>

    <header>
        <h1>كريستيانو رونالدو</h1>
        <p>CR7 - الهداف التاريخي لكرة القدم</p>
    </header>

    <nav>
        <a href="#about">السيرة الذاتية</a>
        <a href="#stats">إحصائيات التاريخية</a>
        <a href="#goals">فيديوهات الأهداف</a>
    </nav>

    <div class="container">

        <!-- قسم السيرة الذاتية -->
        <section id="about">
            <h2>من هو الدون؟</h2>
            <div class="info-box">
                <p>كريستيانو رونالدو دوس سانتوس أفيرو، يعتبره الكثيرون أفضل لاعب في تاريخ كرة القدم. تميز عبر مسيرته الطويلة بالسرعة، القوة البدنية، والقدرة التهديفية الخارقة مع مختلف الأندية العالمية والمنتخب البرتغالي.</p>
                <ul>
                    <li><strong>تاريخ الميلاد:</strong> 5 فبراير 1985 (العمر حالياً 41 عاماً)</li>
                    <li><strong>النادي الحالي:</strong> نادي النصر السعودي</li>
                    <li><strong>المركز:</strong> مهاجم / جناح</li>
                    <li><strong>رقم القميص:</strong> 7</li>
                </ul>
            </div>
        </section>

        <!-- قسم الإحصائيات المحدثة لعام 2026 -->
        <section id="stats">
            <h2>إحصائيات المسيرة التهديفية (تحديث 2026)</h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <h3 id="total-goals">978</h3>
                    <p>إجمالي الأهداف الرسمية</p>
                </div>
                <div class="stat-card">
                    <h3>5</h3>
                    <p>كرات ذهبية (Ballon d'Or)</p>
                </div>
                <div class="stat-card">
                    <h3>146</h3>
                    <p>هدف دولي مع البرتغال</p>
                </div>
                <div class="stat-card">
                    <h3>140</h3>
                    <p>هدف في دوري أبطال أوروبا</p>
                </div>
            </div>
        </section>

        <!-- قسم الفيديوهات (الأجوان) -->
        <section id="goals">
            <h2>فيديوهات أجمل الأهداف والمهارات</h2>
            <div class="video-grid">
                
                <!-- فيديو 1 -->
                <div class="video-card">
                    <div class="video-wrapper">
                        <!-- تم استخدام روابط يوتيوب آمنة للمشاركة كمثال للأهداف التاريخية -->
                        <iframe src="https://youtube.com" allowfullscreen></iframe>
                    </div>
                    <div class="video-info">
                        <h4>أجمل 40 هدفاً مجنوناً في مسيرة رونالدو</h4>
                        <p>تجميع لأفضل التسديدات، الركلات الحرة، والأهداف الأكروباتية.</p>
                    </div>
                </div>

                <!-- فيديو 2 -->
                <div class="video-card">
                    <div class="video-wrapper">
                        <iframe src="https://youtube.com" allowfullscreen></iframe>
                    </div>
                    <div class="video-info">
                        <h4>الهدف التاريخي "المقصية" ضد يوفنتوس</h4>
                        <p>هدفه الأسطوري بالضربة الخلفية المزدوجة الذي صفق له جمهور الخصم.</p>
                    </div>
                </div>

                <!-- فيديو 3 -->
                <div class="video-card">
                    <div class="video-wrapper">
                        <iframe src="https://youtube.com" allowfullscreen></iframe>
                    </div>
                    <div class="video-info">
                        <h4>أهداف رونالدو الحاسمة مع نادي النصر</h4>
                        <p>جانب من مهاراته وأهدافه المذهلة في الدوري السعودي للمحترفين.</p>
                    </div>
                </div>

            </div>
        </section>

    </div>

    <footer>
        <p>صفحة معجبي CR7 | تم إنشاؤها لتعمل على GitHub Pages © 2026</p>
    </footer>

</body>
</html>
