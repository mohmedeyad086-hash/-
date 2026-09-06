<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🐐 CR7 Matches | مباريات الدون</title>
  <style>
    :root {
      --primary-color: #f1c40f; /* اللون الذهبي */
      --bg-color: #111111; /* الخلفية السوداء الفخمة */
      --card-bg: #1e1e1e;
      --text-color: #ffffff;
    }
    
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 20px;
      display: flex;
      justify-content: center;
    }

    .app-container {
      width: 100%;
      max-width: 480px;
      background: var(--card-bg);
      border-radius: 20px;
      padding: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.5);
      border: 1px solid #333;
    }

    .header {
      text-align: center;
      margin-bottom: 25px;
    }

    .header h1 {
      font-size: 28px;
      margin: 5px 0;
      color: var(--primary-color);
    }

    .header p {
      color: #aaa;
      font-size: 14px;
    }

    .nav-buttons {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-bottom: 25px;
    }

    button {
      background: #2a2a2a;
      color: white;
      border: 2px solid transparent;
      padding: 12px;
      border-radius: 12px;
      font-size: 15px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    button:hover, button.active {
      border-color: var(--primary-color);
      background: #333;
      color: var(--primary-color);
    }

    .content-area {
      background: #151515;
      border-radius: 15px;
      padding: 15px;
      min-height: 200px;
      border: 1px solid #222;
    }

    .match-card {
      background: #222;
      padding: 12px;
      border-radius: 10px;
      margin-bottom: 10px;
      border-right: 4px solid var(--primary-color);
    }

    .match-card h4 {
      margin: 0 0 5px 0;
      color: #fff;
    }

    .match-card p {
      margin: 0;
      font-size: 13px;
      color: #999;
    }

    ul { padding-right: 20px; margin: 0; }
    li { margin-bottom: 10px; color: #ccc; font-size: 14px; }
  </style>
</head>
<body>

<div class="app-container">
  <div class="header">
    <h1>🐐 CR7 Matches</h1>
    <p>تطبيق مباريات وأخبار الأسطورة كريستيانو رونالدو ⚽</p>
  </div>

  <!-- الأزرار للتنقل -->
  <div class="nav-buttons">
    <button onclick="showSection('matches', this)" class="active">⚽ المباريات</button>
    <button onclick="showSection('news', this)">📰 الأخبار</button>
    <button onclick="showSection('stats', this)">📊 الإحصائيات</button>
    <button onclick="showSection('trophies', this)">🏆 البطولات</button>
  </div>

  <!-- مساحة عرض المحتوى المربوط -->
  <div id="content" class="content-area">
    <!-- المحتوى الافتراضي المباشر عند فتح الموقع -->
    <h3>📅 مباريات قريبة لـ رونالدو:</h3>
    <div class="match-card">
      <h4>النصر 🆚 الهلال</h4>
      <p>🏆 الدوري السعودي للمحترفين</p>
    </div>
    <div class="match-card">
      <h4>البرتغال 🆚 كرواتيا</h4>
      <p>🏆 دوري الأمم الأوروبية</p>
    </div>
  </div>
</div>

<script>
  // البيانات التي سيتم عرضها عند الضغط على الأزرار
  const sections = {
    matches: `
      <h3>📅 مباريات قريبة لـ رونالدو:</h3>
      <div class="match-card">
        <h4>النصر 🆚 الهلال</h4>
        <p>🏆 الدوري السعودي للمحترفين</p>
      </div>
      <div class="match-card">
        <h4>البرتغال 🆚 كرواتيا</h4>
        <p>🏆 دوري الأمم الأوروبية</p>
      </div>
    `,
    news: `
      <h3>📰 أحدث الأخبار الحالية:</h3>
      <ul>
        <li>🔥 رونالدو يقترب من كسر أرقام قياسية جديدة في عالم المستديرة لعام 2026.</li>
        <li>الحساب الرسمي للدون على يوتيوب يستمر في تحطيم الأرقام القياسية عالمياً.</li>
      </ul>
    `,
    stats: `
      <h3>📊 إحصائيات الأسطورة الكروية:</h3>
      <ul>
        <li>تخطى حاجز الـ 900 هدف رسمي في مسيرته الاحترافية ⚽</li>
        <li>الهداف التاريخي لمنتخب البرتغال وبطولة دوري أبطال أوروبا 🇵🇹</li>
      </ul>
    `,
    trophies: `
      <h3>🏆 أبرز البطولات والإنجازات:</h3>
      <ul>
        <li>الكرة الذهبية (Ballon d'Or): 5 مرات 🏅</li>
        <li>دوري أبطال أوروبا (UCL): 5 ألقاب تاريخية 🇪🇺</li>
        <li>كأس أمم أوروبا (اليورو): لقبان مع البرتغال 🇵🇹</li>
      </ul>
    `
  };

  // دالة التحكم بالعرض وتغيير حالة الأزرار
  function showSection(sectionId, element) {
    // تحديث المحتوى
    document.getElementById('content').innerHTML = sections[sectionId];
    
    // إزالة التصميم النشط من كل الأزرار
    const buttons = document.querySelectorAll('.nav-buttons button');
    buttons.forEach(btn => btn.classList.remove('active'));
    
    // إضافة التصميم النشط للزر الحالي
    element.classList.add('active');
  }
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🐐 CR7 Matches | مباريات وفيديوهات الدون</title>
  <style>
    :root {
      --primary-color: #f1c40f; 
      --bg-color: #111111; 
      --card-bg: #1e1e1e;
      --text-color: #ffffff;
    }
    
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 20px;
      display: flex;
      justify-content: center;
    }

    .app-container {
      width: 100%;
      max-width: 480px;
      background: var(--card-bg);
      border-radius: 20px;
      padding: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.5);
      border: 1px solid #333;
    }

    .header {
      text-align: center;
      margin-bottom: 25px;
    }

    .header h1 {
      font-size: 28px;
      margin: 5px 0;
      color: var(--primary-color);
    }

    .header p {
      color: #aaa;
      font-size: 14px;
    }

    .nav-buttons {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
      margin-bottom: 25px;
    }

    button {
      background: #2a2a2a;
      color: white;
      border: 2px solid transparent;
      padding: 12px;
      border-radius: 12px;
      font-size: 14px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 5px;
    }

    button:hover, button.active {
      border-color: var(--primary-color);
      background: #333;
      color: var(--primary-color);
    }

    .content-area {
      background: #151515;
      border-radius: 15px;
      padding: 15px;
      min-height: 200px;
      border: 1px solid #222;
    }

    .match-card {
      background: #222;
      padding: 12px;
      border-radius: 10px;
      margin-bottom: 10px;
      border-right: 4px solid var(--primary-color);
    }

    .match-card h4 { margin: 0 0 5px 0; color: #fff; }
    .match-card p { margin: 0; font-size: 13px; color: #999; }

    ul { padding-right: 20px; margin: 0; }
    li { margin-bottom: 10px; color: #ccc; font-size: 14px; }

    /* تنسيق مشغل الفيديو ليناسب الهواتف */
    .video-container {
      position: relative;
      padding-bottom: 56.25%;
      height: 0;
      overflow: hidden;
      max-width: 100%;
      background: #000;
      border-radius: 10px;
      margin-bottom: 15px;
    }
    .video-container iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: 0;
    }
  </style>
</head>
<body>

<div class="app-container">
  <div class="header">
    <h1>🐐 CR7 Matches</h1>
    <p>تطبيق مباريات وأخبار الأسطورة كريستيانو رونالدو ⚽</p>
  </div>

  <!-- الأزرار للتنقل -->
  <div class="nav-buttons">
    <button onclick="showSection('matches', this)" class="active">⚽ المباريات</button>
    <button onclick="showSection('videos', this)">📺 الفيديوهات</button>
    <button onclick="showSection('news', this)">📰 الأخبار</button>
    <button onclick="showSection('stats', this)">📊 الإحصائيات</button>
  </div>

  <!-- مساحة عرض المحتوى المربوط -->
  <div id="content" class="content-area">
    <h3>📅 مباريات قريبة لـ رونالدو:</h3>
    <div class="match-card">
      <h4>النصر 🆚 الهلال</h4>
      <p>🏆 الدوري السعودي للمحترفين</p>
    </div>
    <div class="match-card">
      <h4>البرتغال 🆚 كرواتيا</h4>
      <p>🏆 دوري الأمم الأوروبية</p>
    </div>
  </div>
</div>

<script>
  // البيانات المربوطة بالأزرار
  const sections = {
    matches: `
      <h3>📅 مباريات قريبة لـ رونالدو:</h3>
      <div class="match-card">
        <h4>النصر 🆚 الهلال</h4>
        <p>🏆 الدوري السعودي للمحترفين</p>
      </div>
      <div class="match-card">
        <h4>البرتغال 🆚 كرواتيا</h4>
        <p>🏆 دوري الأمم الأوروبية</p>
      </div>
    `,
    videos: `
      <h3>📺 أهداف ومهارات الدون:</h3>
      <p style="font-size:13px; color:#aaa;">أجمل مهارات وأهداف رونالدو التاريخية:</p>
      
      <!-- فيديو يوتيوب 1 -->
      <div class="video-container">
        <iframe src="https://youtube.com" allowfullscreen></iframe>
      </div>

      <!-- فيديو يوتيوب 2 -->
      <div class="video-container">
        <iframe src="https://youtube.com" allowfullscreen></iframe>
      </div>
    `,
    news: `
      <h3>📰 أحدث الأخبار الحالية:</h3>
      <ul>
        <li>🔥 رونالدو يقترب من كسر أرقام قياسية جديدة في عالم المستديرة لعام 2026.</li>
        <li>الحساب الرسمي للدون على يوتيوب يستمر في تحطيم الأرقام القياسية عالمياً.</li>
      </ul>
    `,
    stats: `
      <h3>📊 إحصائيات الأسطورة الكروية:</h3>
      <ul>
        <li>تخطى حاجز الـ 900 هدف رسمي في مسيرته الاحترافية ⚽</li>
        <li>الهداف التاريخي لمنتخب البرتغال وبطولة دوري أبطال أوروبا 🇵🇹</li>
      </ul>
    `
  };

  function showSection(sectionId, element) {
    document.getElementById('content').innerHTML = sections[sectionId];
    const buttons = document.querySelectorAll('.nav-buttons button');
    buttons.forEach(btn => btn.classList.remove('active'));
    element.classList.add('active');
  }
</script>

</body>
</html>
