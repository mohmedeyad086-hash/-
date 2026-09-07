<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>سيرة كريستيانو رونالدو الأسطورية</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #0b0f19;
            color: #f1f5f9;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 700px;
            background: #1e293b;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            overflow: hidden;
            border: 1px solid #334155;
        }

        /* رأس الصفحة */
        .header {
            background: linear-gradient(135deg, #1e3a8a, #0f172a);
            padding: 30px;
            text-align: center;
            border-bottom: 3px solid #eab308;
        }

        .header h1 {
            color: #eab308;
            font-size: 2rem;
            margin-bottom: 8px;
        }

        .header p {
            color: #94a3b8;
            font-size: 1rem;
        }

        /* أزرار التنقل الإعلانية */
        .tabs {
            display: flex;
            background-color: #0f172a;
            border-bottom: 1px solid #334155;
            overflow-x: auto;
        }

        .tab-btn {
            flex: 1;
            padding: 15px 10px;
            background: none;
            border: none;
            color: #94a3b8;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            white-space: nowrap;
        }

        .tab-btn:hover {
            color: #f1f5f9;
            background-color: #1e293b;
        }

        .tab-btn.active {
            color: #eab308;
            background-color: #1e293b;
            border-bottom: 3px solid #eab308;
        }

        /* محتوى الأقسام */
        .content-section {
            padding: 35px;
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .content-section.active {
            display: block;
        }

        h2 {
            color: #eab308;
            margin-bottom: 20px;
            font-size: 1.5rem;
            border-right: 4px solid #eab308;
            padding-right: 10px;
        }

        p {
            font-size: 1.05rem;
            line-height: 1.8;
            margin-bottom: 15px;
            text-align: justify;
            color: #cbd5e1;
        }

        ul {
            list-style-type: none;
            margin-top: 15px;
        }

        li {
            position: relative;
            padding-right: 25px;
            margin-bottom: 12px;
            font-size: 1.05rem;
            color: #e2e8f0;
        }

        li::before {
            content: "✦";
            position: absolute;
            right: 0;
            color: #eab308;
            font-weight: bold;
        }

        /* ذيل الصفحة أزرار التالي والسابق */
        .footer-nav {
            display: flex;
            justify-content: space-between;
            padding: 20px 35px;
            background-color: #0f172a;
            border-top: 1px solid #334155;
        }

        .nav-btn {
            padding: 10px 20px;
            background-color: #1e293b;
            color: #f1f5f9;
            border: 1px solid #475569;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }

        .nav-btn:hover:not(:disabled) {
            background-color: #eab308;
            color: #0f172a;
            border-color: #eab308;
        }

        .nav-btn:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- الرأس -->
        <div class="header">
            <h1>CRISTIANO RONALDO</h1>
            <p>الموسوعة الكاملة لمسيرة وسيرة الدون الاحترافية</p>
        </div>

        <!-- أشرطة التنقل -->
        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab(0)">النشأة</button>
            <button class="tab-btn" onclick="switchTab(1)">الأندية الأوروبية</button>
            <button class="tab-btn" onclick="switchTab(2)">العالمية والنصر</button>
            <button class="tab-btn" onclick="switchTab(3)">الأرقام القياسية</button>
        </div>

        <!-- الأقسام -->
        <!-- القسم 1 -->
        <div class="content-section active">
            <h2>المولد والطفولة القاسية</h2>
            <p>ولد كريستيانو رونالدو دوس سانتوس أفيرو في 5 فبراير 1985 في جزيرة ماديرا البرتغالية، ونشأ في عائلة فقيرة جداً كأصغر ابن بين إخوته.</p>
            <p>اكتشف شغفه بكرة القدم منذ طفولته المبكرة وكان يلعب في شوارع الجزيرة. انضم لاحقاً لأكاديمية سبورتينغ لشبونة، حيث واجه صعوبات بالغة بسبب بعده عن عائلته، وتخطى أزمة صحية في قلبه بسن الـ15 عبر جراحة دقيقة كادت تنهي مسيرته قبل أن تبدأ.</p>
        </div>

        <!-- القسم 2 -->
        <div class="content-section">
            <h2>الحقبة الأوروبية التاريخية</h2>
            <p>انطلق للعالمية عام 2003 بعد انضمامه إلى مانشستر يونايتد الإنجليزي تحت قيادة السير أليكس فيرغسون، وحقق معهم أول دوري أبطال أوروبا والكرة الذهبية الأولى له.</p>
            <p>في عام 2009، انتقل إلى ريال مدريد الإسباني بصفقة تاريخية، ليصبح الهداف التاريخي للنادي بـ 450 هدفاً متوجاً بأربعة ألقاب دوري أبطال أوروبا. خاض بعدها تجربة ملهمة مع يوفنتوس الإيطالي محققاً كافة الألقاب المحلية هناك.</p>
        </div>

        <!-- القسم 3 -->
        <div class="content-section">
            <h2>التجربة الدولية والنصر السعودي</h2>
            <p>قاد منتخب البرتغال للتتويج التاريخي بكأس أمم أوروبا (يورو 2016) ودوري الأمم الأوروبية 2019، وأصبح الهداف التاريخي لكرة القدم الدولية على مستوى المنتخبات.</p>
            <p>في أواخر عام 2022، دشن خطوة استثنائية بانتقاله إلى نادي النصر السعودي، مما أحدث ثورة شاملة وجذب كبار نجوم كرة القدم العالمية إلى دوري روشن السعودي.</p>
        </div>

        <!-- القسم 4 -->
        <div class="content-section">
            <h2>أبرز الإنجازات والأرقام القياسية</h2>
            <p>تضم الخزينة الأسطورية لـ CR7 إحصائيات لم تسبق في تاريخ كرة القدم:</p>
            <ul>
                <li>الفوز بـ 5 كرات ذهبية (Ballon d'Or).</li>
                <li>الهداف التاريخي الرسمي لكرة القدم متجاوزاً حاجز الـ 900 هدف.</li>
                <li>الهداف التاريخي لدوري أبطال أوروبا والبطولات الأوروبية للمنتخبات.</li>
                <li>الحذاء الذهبي الأوروبي 4 مرات.</li>
            </ul>
        </div>

        <!-- أزرار الأسفل -->
        <div class="footer-nav">
            <button class="nav-btn" id="prevBtn" onclick="changeSection(-1)" disabled>السابق</button>
            <button class="nav-btn" id="nextBtn" onclick="changeSection(1)">التالي</button>
        </div>
    </div>

    <script>
        let currentIdx = 0;
        const sections = document.querySelectorAll('.content-section');
        const tabs = document.querySelectorAll('.tab-btn');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');

        function updateUI() {
            sections.forEach((sec, idx) => {
                if(idx === currentIdx) {
                    sec.classList.add('active');
                    tabs[idx].classList.add('active');
                } else {
                    sec.classList.remove('active');
                    tabs[idx].classList.remove('active');
                }
            });

            // تحديث حالة الأزرار
            prevBtn.disabled = (currentIdx === 0);
            nextBtn.disabled = (currentIdx === sections.length - 1);
        }

        function switchTab(index) {
            currentIdx = index;
            updateUI();
        }

        function changeSection(direction) {
            currentIdx += direction;
            if(currentIdx < 0) currentIdx = 0;
            if(currentIdx >= sections.length) currentIdx = sections.length - 1;
            updateUI();
        }
    </script>
</body>
</html>
