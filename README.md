# azkar<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أذكاري - موسوعة الأذكار</title>
<link href="https://fonts.googleapis.com/css2?family=Amiri:wght@400;700&family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: 'Cairo', sans-serif;
    background: linear-gradient(135deg, #0f3d2e 0%, #1a5c47 50%, #0a2a20 100%);
    min-height: 100vh;
    color: #fff;
    padding: 15px;
  }
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: radial-gradient(circle at 20% 30%, rgba(212, 175, 55, 0.1) 0%, transparent 50%),
                      radial-gradient(circle at 80% 70%, rgba(212, 175, 55, 0.08) 0%, transparent 50%);
    pointer-events: none;
    z-index: 0;
  }
  .container { max-width: 900px; margin: 0 auto; position: relative; z-index: 1; }
  header {
    text-align: center;
    padding: 25px 0;
    border-bottom: 2px solid rgba(212, 175, 55, 0.3);
    margin-bottom: 20px;
  }
  header h1 {
    font-family: 'Amiri', serif;
    font-size: 2.8rem;
    color: #d4af37;
    text-shadow: 0 2px 10px rgba(212, 175, 55, 0.3);
    margin-bottom: 8px;
  }
  header p { color: #c9d6cf; font-size: 1.05rem; }
  .stats {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 15px;
    flex-wrap: wrap;
  }
  .stat-box {
    background: rgba(212, 175, 55, 0.15);
    padding: 8px 18px;
    border-radius: 20px;
    border: 1px solid rgba(212, 175, 55, 0.3);
    font-size: 0.9rem;
  }
  .stat-box span { color: #d4af37; font-weight: 700; }

  .tabs {
    display: flex;
    gap: 8px;
    margin-bottom: 20px;
    flex-wrap: wrap;
    justify-content: center;
  }
  .tab {
    padding: 10px 16px;
    background: rgba(255,255,255,0.08);
    border: 1px solid rgba(212, 175, 55, 0.3);
    border-radius: 25px;
    color: #fff;
    cursor: pointer;
    font-family: 'Cairo', sans-serif;
    font-size: 0.9rem;
    font-weight: 600;
    transition: all 0.3s;
  }
  .tab:hover { background: rgba(212, 175, 55, 0.2); }
  .tab.active {
    background: linear-gradient(135deg, #d4af37, #b8941f);
    color: #0f3d2e;
    border-color: #d4af37;
  }

  .section { display: none; animation: fadeIn 0.5s; }
  .section.active { display: block; }
  @keyframes fadeIn { from {opacity:0; transform:translateY(10px);} to {opacity:1; transform:translateY(0);} }

  .counter-box, .salawat-box {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(212, 175, 55, 0.3);
    border-radius: 20px;
    padding: 25px;
    text-align: center;
    backdrop-filter: blur(10px);
  }
  .salawat-box { background: rgba(212, 175, 55, 0.08); border: 2px solid rgba(212, 175, 55, 0.4); padding: 30px 20px; }
  .current-dhikr {
    font-family: 'Amiri', serif;
    font-size: 2rem;
    color: #d4af37;
    margin-bottom: 10px;
    min-height: 70px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .dhikr-target { color: #c9d6cf; margin-bottom: 20px; }
  .counter-display {
    font-size: 5rem;
    font-weight: 700;
    color: #fff;
    margin: 15px 0;
    text-shadow: 0 0 30px rgba(212, 175, 55, 0.5);
  }
  .counter-btn {
    width: 160px;
    height: 160px;
    border-radius: 50%;
    background: radial-gradient(circle, #d4af37 0%, #8b6914 100%);
    border: 5px solid #f4d76e;
    color: #0f3d2e;
    font-size: 1.3rem;
    font-weight: 700;
    cursor: pointer;
    font-family: 'Cairo', sans-serif;
    box-shadow: 0 10px 40px rgba(212, 175, 55, 0.4), inset 0 -5px 15px rgba(0,0,0,0.2);
    transition: transform 0.1s;
    margin: 15px auto;
    display: block;
  }
  .counter-btn:active { transform: scale(0.95); }
  .counter-controls { display: flex; gap: 10px; justify-content: center; margin-top: 15px; flex-wrap: wrap; }
  .ctrl-btn {
    padding: 8px 16px;
    background: rgba(255,255,255,0.1);
    border: 1px solid rgba(212, 175, 55, 0.4);
    border-radius: 10px;
    color: #fff;
    cursor: pointer;
    font-family: 'Cairo', sans-serif;
    font-size: 0.9rem;
    transition: all 0.3s;
  }
  .ctrl-btn:hover { background: rgba(212, 175, 55, 0.3); }

  .dhikr-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 8px;
    margin-top: 20px;
  }
  .dhikr-item {
    padding: 10px;
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(212, 175, 55, 0.2);
    border-radius: 10px;
    cursor: pointer;
    text-align: center;
    font-size: 0.85rem;
    transition: all 0.3s;
  }
  .dhikr-item:hover { background: rgba(212, 175, 55, 0.15); }
  .dhikr-item.selected { background: rgba(212, 175, 55, 0.3); border-color: #d4af37; }

  .azkar-card {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(212, 175, 55, 0.3);
    border-radius: 15px;
    padding: 20px;
    margin-bottom: 12px;
    backdrop-filter: blur(10px);
    transition: all 0.3s;
  }
  .azkar-card:hover { border-color: #d4af37; }
  .azkar-text {
    font-family: 'Amiri', serif;
    font-size: 1.25rem;
    line-height: 2.1;
    color: #fff;
    margin-bottom: 12px;
    text-align: center;
  }
  .azkar-meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 8px;
    padding-top: 12px;
    border-top: 1px solid rgba(212, 175, 55, 0.2);
  }
  .azkar-count {
    background: rgba(212, 175, 55, 0.2);
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.85rem;
    color: #d4af37;
  }
  .azkar-ref { color: #a8b5ad; font-size: 0.8rem; font-style: italic; }
  .azkar-btn {
    padding: 6px 14px;
    background: linear-gradient(135deg, #d4af37, #b8941f);
    border: none;
    border-radius: 20px;
    color: #0f3d2e;
    font-weight: 700;
    cursor: pointer;
    font-family: 'Cairo', sans-serif;
    font-size: 0.85rem;
    transition: transform 0.2s;
  }
  .azkar-btn:hover { transform: scale(1.05); }
  .azkar-btn.done { background: #4a7c59; color: #fff; }

  .salawat-title { font-family: 'Amiri', serif; font-size: 1.8rem; color: #d4af37; margin-bottom: 15px; }
  .salawat-text { font-family: 'Amiri', serif; font-size: 1.6rem; line-height: 2.3; color: #fff; margin-bottom: 20px; }
  .salawat-counter { font-size: 3.5rem; font-weight: 700; color: #d4af37; margin: 15px 0; }

  footer {
    text-align: center;
    padding: 25px 0;
    margin-top: 30px;
    color: #a8b5ad;
    border-top: 1px solid rgba(212, 175, 55, 0.2);
  }
  footer p { margin: 5px 0; }

  @media (max-width: 600px) {
    header h1 { font-size: 2rem; }
    .counter-display { font-size: 4rem; }
    .counter-btn { width: 140px; height: 140px; font-size: 1.1rem; }
    .current-dhikr { font-size: 1.4rem; }
    .salawat-text { font-size: 1.2rem; }
    .tab { padding: 8px 12px; font-size: 0.8rem; }
    .azkar-text { font-size: 1.1rem; }
  }
</style>
</head>
<body>
<div class="container">
  <header>
    <h1>﷽</h1>
    <h1>أذكـاري</h1>
    <p>﴿ أَلَا بِذِكْرِ اللَّهِ تَطْمَئِنُّ الْقُلُوبُ ﴾</p>
    <div class="stats">
      <div class="stat-box">إجمالي الأذكار: <span id="totalCount">0</span></div>
      <div class="stat-box">المنجزة اليوم: <span id="doneCount">0</span></div>
    </div>
  </header>

  <div class="tabs">
    <button class="tab active" data-tab="counter">📿 المسبحة</button>
    <button class="tab" data-tab="morning">🌅 الصباح</button>
    <button class="tab" data-tab="evening">🌙 المساء</button>
    <button class="tab" data-tab="sleep">😴 النوم</button>
    <button class="tab" data-tab="wake">☀️ الاستيقاظ</button>
    <button class="tab" data-tab="prayer">🕌 بعد الصلاة</button>
    <button class="tab" data-tab="food">🍽️ الطعام</button>
    <button class="tab" data-tab="mosque">🕋 المسجد</button>
    <button class="tab" data-tab="home">🏠 المنزل</button>
    <button class="tab" data-tab="travel">✈️ السفر</button>
    <button class="tab" data-tab="clothes">👕 اللباس</button>
    <button class="tab" data-tab="misc">📖 متفرقات</button>
    <button class="tab" data-tab="salawat">ﷺ الصلاة على النبي</button>
  </div>

  <!-- Counter Section -->
  <section class="section active" id="counter">
    <div class="counter-box">
      <div class="current-dhikr" id="currentDhikr">سُبْحَانَ اللَّهِ</div>
      <div class="dhikr-target" id="dhikrTarget">العدد المطلوب: 33</div>
      <div class="counter-display" id="counterDisplay">0</div>
      <button class="counter-btn" id="countBtn">اضغط للتسبيح</button>
      <div class="progress-bar" style="width:100%;height:6px;background:rgba(255,255,255,0.1);border-radius:3px;margin-top:15px;overflow:hidden;">
        <div id="progressFill" style="height:100%;background:linear-gradient(90deg,#d4af37,#f4d76e);transition:width 0.3s;border-radius:3px;width:0%"></div>
      </div>
      <div class="counter-controls">
        <button class="ctrl-btn" onclick="resetCounter()">🔄 إعادة</button>
        <button class="ctrl-btn" onclick="prevDhikr()">⬅️ السابق</button>
        <button class="ctrl-btn" onclick="nextDhikr()">التالي ➡️</button>
      </div>
      <h3 style="margin-top:25px; color:#d4af37;">اختر الذكر:</h3>
      <div class="dhikr-list" id="dhikrList"></div>
    </div>
  </section>

  <section class="section" id="morning"><div id="morningList"></div></section>
  <section class="section" id="evening"><div id="eveningList"></div></section>
  <section class="section" id="sleep"><div id="sleepList"></div></section>
  <section class="section" id="wake"><div id="wakeList"></div></section>
  <section class="section" id="prayer"><div id="prayerList"></div></section>
  <section class="section" id="food"><div id="foodList"></div></section>
  <section class="section" id="mosque"><div id="mosqueList"></div></section>
  <section class="section" id="home"><div id="homeList"></div></section>
  <section class="section" id="travel"><div id="travelList"></div></section>
  <section class="section" id="clothes"><div id="clothesList"></div></section>
  <section class="section" id="misc"><div id="miscList"></div></section>

  <!-- Salawat Section -->
  <section class="section" id="salawat">
    <div class="salawat-box">
      <div class="salawat-title">الصلاة على النبي ﷺ</div>
      <div class="salawat-text">
        اللَّهُمَّ صَلِّ وَسَلِّمْ وَبَارِكْ<br>
        عَلَى سَيِّدِنَا مُحَمَّد<br>
        وَعَلَى آلِهِ وَصَحْبِهِ أَجْمَعِينَ
      </div>
      <div class="salawat-counter" id="salawatCount">0</div>
      <button class="counter-btn" id="salawatBtn" style="width:150px; height:150px;">صلِّ على النبي ﷺ</button>
      <div class="counter-controls">
        <button class="ctrl-btn" onclick="resetSalawat()">🔄 إعادة</button>
      </div>
      <p style="margin-top:20px; color:#c9d6cf; font-style:italic;">
        «مَنْ صَلَّى عَلَيَّ صَلَاةً صَلَّى اللَّهُ عَلَيْهِ بِهَا عَشْرًا»<br>
        <small style="color:#a8b5ad;">— رواه مسلم</small>
      </p>
    </div>
  </section>

  <footer>
    <p>🤲 اللهم تقبل منا ومنكم صالح الأعمال</p>
    <p style="font-size:0.85rem;">© أذكاري — موسوعة الأذكار والأدعية</p>
  </footer>
</div>

<script>
  // ========== المسبحة (موسعة) ==========
  const adhkar = [
    { text: "سُبْحَانَ اللَّهِ", target: 33 },
    { text: "الْحَمْدُ لِلَّهِ", target: 33 },
    { text: "اللَّهُ أَكْبَرُ", target: 34 },
    { text: "لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ", target: 10 },
    { text: "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ، سُبْحَانَ اللَّهِ الْعَظِيمِ", target: 100 },
    { text: "لَا حَوْلَ وَلَا قُوَّةَ إِلَّا بِاللَّهِ", target: 100 },
    { text: "أَسْتَغْفِرُ اللَّهَ الْعَظِيمَ وَأَتُوبُ إِلَيْهِ", target: 100 },
    { text: "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ، عَدَدَ خَلْقِهِ وَرِضَا نَفْسِهِ وَزِنَةَ عَرْشِهِ وَمِدَادَ كَلِمَاتِهِ", target: 3 },
    { text: "اللَّهُمَّ صَلِّ عَلَى مُحَمَّدٍ وَعَلَى آلِ مُحَمَّدٍ", target: 100 },
    { text: "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ، عَدَدَ مَا خَلَقَ فِي السَّمَاءِ وَعَدَدَ مَا خَلَقَ فِي الْأَرْضِ", target: 10 },
    { text: "اللَّهُمَّ اغْفِرْ لِي وَارْحَمْنِي وَاهْدِنِي وَعَافِنِي وَارْزُقْنِي", target: 10 },
    { text: "رَبِّ اغْفِرْ لِي وَتُبْ عَلَيَّ إِنَّكَ أَنْتَ التَّوَّابُ الرَّحِيمُ", target: 100 },
    { text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنَ الْهَمِّ وَالْحَزَنِ", target: 10 },
    { text: "حَسْبِيَ اللَّهُ لَا إِلَهَ إِلَّا هُوَ عَلَيْهِ تَوَكَّلْتُ", target: 7 },
    { text: "يَا حَيُّ يَا قَيُّومُ بِرَحْمَتِكَ أَسْتَغِيثُ", target: 10 }
  ];

  // ========== أذكار الصباح ==========
  const morningAzkar = [
    { text: "أَعُوذُ بِاللَّهِ مِنَ الشَّيْطَانِ الرَّجِيمِ. اللَّهُ لَا إِلَهَ إِلَّا هُوَ الْحَيُّ الْقَيُّومُ لَا تَأْخُذُهُ سِنَةٌ وَلَا نَوْمٌ... (آية الكرسي)", count: 1, ref: "البقرة: 255" },
    { text: "بِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيمِ. قُلْ هُوَ اللَّهُ أَحَدٌ، اللَّهُ الصَّمَدُ، لَمْ يَلِدْ وَلَمْ يُولَدْ، وَلَمْ يَكُن لَّهُ كُفُوًا أَحَدٌ", count: 3, ref: "الإخلاص" },
    { text: "بِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيمِ. قُلْ أَعُوذُ بِرَبِّ الْفَلَقِ...", count: 3, ref: "الفلق" },
    { text: "بِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيمِ. قُلْ أَعُوذُ بِرَبِّ النَّاسِ...", count: 3, ref: "الناس" },
    { text: "أَصْبَحْنَا وَأَصْبَحَ الْمُلْكُ لِلَّهِ، وَالْحَمْدُ لِلَّهِ، لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ، وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ", count: 1, ref: "مسلم" },
    { text: "اللَّهُمَّ بِكَ أَصْبَحْنَا، وَبِكَ أَمْسَيْنَا، وَبِكَ نَحْيَا، وَبِكَ نَمُوتُ، وَإِلَيْكَ النُّشُورُ", count: 1, ref: "الترمذي" },
    { text: "اللَّهُمَّ أَنْتَ رَبِّي لَا إِلَهَ إِلَّا أَنْتَ، خَلَقْتَنِي وَأَنَا عَبْدُكَ، وَأَنَا عَلَى عَهْدِكَ وَوَعْدِكَ مَا اسْتَطَعْتُ، أَعُوذُ بِكَ مِنْ شَرِّ مَا صَنَعْتُ، أَبُوءُ لَكَ بِنِعْمَتِكَ عَلَيَّ، وَأَبُوءُ لَكَ بِذَنْبِي فَاغْفِرْ لِي فَإِنَّهُ لَا يَغْفِرُ الذُّنُوبَ إِلَّا أَنْتَ (سيد الاستغفار)", count: 1, ref: "البخاري" },
    { text: "اللَّهُمَّ إِنِّي أَصْبَحْتُ أُشْهِدُكَ، وَأُشْهِدُ حَمَلَةَ عَرْشِكَ، وَمَلَائِكَتَكَ، وَجَمِيعَ خَلْقِكَ، أَنَّكَ أَنْتَ اللَّهُ لَا إِلَهَ إِلَّا أَنْتَ وَحْدَكَ لَا شَرِيكَ لَكَ، وَأَنَّ مُحَمَّدًا عَبْدُكَ وَرَسُولُكَ", count: 4, ref: "أبو داود" },
    { text: "اللَّهُمَّ مَا أَصْبَحَ بِي مِنْ نِعْمَةٍ أَوْ بِأَحَدٍ مِنْ خَلْقِكَ فَمِنْكَ وَحْدَكَ لَا شَرِيكَ لَكَ، فَلَكَ الْحَمْدُ وَلَكَ الشُّكْرُ", count: 1, ref: "أبو داود" },
    { text: "اللَّهُمَّ عَافِنِي فِي بَدَنِي، اللَّهُمَّ عَافِنِي فِي سَمْعِي، اللَّهُمَّ عَافِنِي فِي بَصَرِي، لَا إِلَهَ إِلَّا أَنْتَ", count: 3, ref: "أبو داود" },
    { text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنَ الْكُفْرِ، وَالْفَقْرِ، وَأَعُوذُ بِكَ مِنْ عَذَابِ الْقَبْرِ، لَا إِلَهَ إِلَّا أَنْتَ", count: 3, ref: "أبو داود" },
    { text: "حَسْبِيَ اللَّهُ لَا إِلَهَ إِلَّا هُوَ عَلَيْهِ تَوَكَّلْتُ وَهُوَ رَبُّ الْعَرْشِ الْعَظِيمِ", count: 7, ref: "أبو داود" },
    { text: "بِسْمِ اللَّهِ الَّذِي لَا يَضُرُّ مَعَ اسْمِهِ شَيْءٌ فِي الْأَرْضِ وَلَا فِي السَّمَاءِ وَهُوَ السَّمِيعُ الْعَلِيمُ", count: 3, ref: "الترمذي" },
    { text: "رَضِيتُ بِاللَّهِ رَبًّا، وَبِالْإِسْلَامِ دِينًا، وَبِمُحَمَّدٍ ﷺ نَبِيًّا", count: 3, ref: "أحمد" },
    { text: "يَا حَيُّ يَا قَيُّومُ بِرَحْمَتِكَ أَسْتَغِيثُ، أَصْلِحْ لِي شَأْنِي كُلَّهُ، وَلَا تَكِلْنِي إِلَى نَفْسِي طَرْفَةَ عَيْنٍ", count: 3, ref: "الحاكم" },
    { text: "أَصْبَحْنَا عَلَى فِطْرَةِ الْإِسْلَامِ، وَعَلَى كَلِمَةِ الْإِخْلَاصِ، وَعَلَى دِينِ نَبِيِّنَا مُحَمَّدٍ ﷺ، وَعَلَى مِلَّةِ أَبِينَا إِبْرَاهِيمَ حَنِيفًا مُسْلِمًا وَمَا كَانَ مِنَ الْمُشْرِكِينَ", count: 1, ref: "أحمد" },
    { text: "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ", count: 100, ref: "مسلم" },
    { text: "لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ، وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ", count: 10, ref: "البخاري" },
    { text: "لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ، وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ (عشر مرات)", count: 10, ref: "النسائي" },
    { text: "أَسْتَغْفِرُ اللَّهَ وَأَتُوبُ إِلَيْهِ", count: 100, ref: "متفق عليه" },
    { text: "اللَّهُمَّ صَلِّ وَسَلِّمْ عَلَى نَبِيِّنَا مُحَمَّدٍ", count: 10, ref: "الطبراني" }
  ];

  // ========== أذكار المساء ==========
  const eveningAzkar = morningAzkar.map(z => {
    let t = z.text
      .replace(/أَصْبَحْنَا/g, "أَمْسَيْنَا")
      .replace(/أَصْبَحْتُ/g, "أَمْسَيْتُ")
      .replace(/أَصْبَحَ/g, "أَمْسَى");
    return { ...z, text: t };
  });

  // ========== أذكار النوم ==========
  const sleepAzkar = [
    { text: "بِاسْمِكَ اللَّهُمَّ أَمُوتُ وَأَحْيَا", count: 1, ref: "البخاري" },
    { text: "اللَّهُمَّ قِنِي عَذَابَكَ يَوْمَ تَبْعَثُ عِبَادَكَ", count: 3, ref: "أبو داود" },
    { text: "سُبْحَانَ اللَّهِ (33) وَالْحَمْدُ لِلَّهِ (33) وَاللَّهُ أَكْبَرُ (34)", count: 1, ref: "متفق عليه" },
    { text: "اللَّهُمَّ رَبَّ السَّمَاوَاتِ السَّبْعِ وَرَبَّ الْعَرْشِ الْعَظِيمِ، رَبَّنَا وَرَبَّ كُلِّ شَيْءٍ، فَالِقَ الْحَبِّ وَالنَّوَى، وَمُنْزِلَ التَّوْرَاةِ وَالْإِنْجِيلِ وَالْفُرْقَانِ، أَعُوذُ بِكَ مِنْ شَرِّ كُلِّ شَيْءٍ أَنْتَ آخِذٌ بِنَاصِيَتِهِ، اللَّهُمَّ أَنْتَ الْأَوَّلُ فَلَيْسَ قَبْلَكَ شَيْءٌ، وَأَنْتَ الْآخِرُ فَلَيْسَ بَعْدَكَ شَيْءٌ، وَأَنْتَ الظَّاهِرُ فَلَيْسَ فَوْقَكَ شَيْءٌ، وَأَنْتَ الْبَاطِنُ فَلَيْسَ دُونَكَ شَيْءٌ، اقْضِ عَنَّا الدَّيْنَ وَأَغْنِنَا مِنَ الْفَقْرِ", count: 1, ref: "مسلم" },
    { text: "الْحَمْدُ لِلَّهِ الَّذِي أَطْعَمَنَا وَسَقَانَا، وَكَفَانَا وَآوَانَا، فَكَمْ مِمَّنْ لَا كَافِيَ لَهُ وَلَا مُؤْوِيَ", count: 1, ref: "مسلم" },
    { text: "اللَّهُمَّ أَسْلَمْتُ نَفْسِي إِلَيْكَ، وَوَجَّهْتُ وَجْهِي إِلَيْكَ، وَفَوَّضْتُ أَمْرِي إِلَيْكَ، وَأَلْجَأْتُ ظَهْرِي إِلَيْكَ، رَغْبَةً وَرَهْبَةً إِلَيْكَ، لَا مَلْجَأَ وَلَا مَنْجَا مِنْكَ إِلَّا إِلَيْكَ، آمَنْتُ بِكِتَابِكَ الَّذِي أَنْزَلْتَ، وَبِنَبِيِّكَ الَّذِي أَرْسَلْتَ", count: 1, ref: "متفق عليه" },
    { text: "قراءة آية الكرسي", count: 1, ref: "البخاري" },
    { text: "قراءة سورتَي الإخلاص والمعوذتين ثم مسح الجسد", count: 3, ref: "البخاري" },
    { text: "قراءة سورة البقرة (آخر آيتين)", count: 1, ref: "متفق عليه" },
    { text: "قراءة سورة السجدة", count: 1, ref: "الترمذي" },
    { text: "قراءة سورة الملك", count: 1, ref: "الترمذي" },
    { text: "قراءة سورة الكافرون", count: 1, ref: "أبو داود" },
    { text: "التكبير (34) والتحميد (33) والتسبيح (33)", count: 1, ref: "متفق عليه" }
  ];

  // ========== أذكار الاستيقاظ ==========
  const wakeAzkar = [
    { text: "الْحَمْدُ لِلَّهِ الَّذِي أَحْيَانَا بَعْدَ مَا أَمَاتَنَا وَإِلَيْهِ النُّشُورُ", count: 1, ref: "البخاري" },
    { text: "لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ، وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ، سُبْحَانَ اللَّهِ، وَالْحَمْدُ لِلَّهِ، وَلَا إِلَهَ إِلَّا اللَّهُ، وَاللَّهُ أَكْبَرُ، وَلَا حَوْلَ وَلَا قُوَّةَ إِلَّا بِاللَّهِ الْعَلِيِّ الْعَظِيمِ", count: 1, ref: "البخاري" },
    { text: "الْحَمْدُ لِلَّهِ الَّذِي عَافَانِي فِي جَسَدِي، وَرَدَّ عَلَيَّ رُوحِي، وَأَذِنَ لِي بِذِكْرِهِ", count: 1, ref: "الترمذي" },
    { text: "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ، عَدَدَ خَلْقِهِ، وَرِضَا نَفْسِهِ، وَزِنَةَ عَرْشِهِ، وَمِدَادَ كَلِمَاتِهِ", count: 3, ref: "مسلم" },
    { text: "اللَّهُمَّ إِنِّي أَسْأَلُكَ عِلْمًا نَافِعًا، وَرِزْقًا طَيِّبًا، وَعَمَلًا مُتَقَبَّلًا", count: 1, ref: "ابن ماجه" },
    { text: "مسح النوم عن الوجه وقراءة آخر عشر آيات من سورة آل عمران", count: 1, ref: "البخاري" }
  ];

  // ========== أذكار بعد الصلاة ==========
  const prayerAzkar = [
    { text: "أَسْتَغْفِرُ اللَّهَ، أَسْتَغْفِرُ اللَّهَ، أَسْتَغْفِرُ اللَّهَ. اللَّهُمَّ أَنْتَ السَّلَامُ وَمِنْكَ السَّلَامُ، تَبَارَكْتَ يَا ذَا الْجَلَالِ وَالْإِكْرَامِ", count: 1, ref: "مسلم" },
    { text: "لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ، اللَّهُمَّ لَا مَانِعَ لِمَا أَعْطَيْتَ، وَلَا مُعْطِيَ لِمَا مَنَعْتَ، وَلَا يَنْفَعُ ذَا الْجَدِّ مِنْكَ الْجَدُّ", count: 1, ref: "متفق عليه" },
    { text: "لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ، لَا حَوْلَ وَلَا قُوَّةَ إِلَّا بِاللَّهِ، لَا إِلَهَ إِلَّا اللَّهُ، وَلَا نَعْبُدُ إِلَّا إِيَّاهُ، لَهُ النِّعْمَةُ وَلَهُ الْفَضْلُ، وَلَهُ الثَّنَاءُ الْحَسَنُ، لَا إِلَهَ إِلَّا اللَّهُ مُخْلِصِينَ لَهُ الدِّينَ وَلَوْ كَرِهَ الْكَافِرُونَ", count: 1, ref: "مسلم" },
    { text: "سُبْحَانَ اللَّهِ", count: 33, ref: "مسلم" },
    { text: "الْحَمْدُ لِلَّهِ", count: 33, ref: "مسلم" },
    { text: "اللَّهُ أَكْبَرُ", count: 33, ref: "مسلم" },
    { text: "لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ (تمام المائة)", count: 1, ref: "مسلم" },
    { text: "قراءة آية الكرسي بعد كل صلاة", count: 1, ref: "النسائي" },
    { text: "قُلْ هُوَ اللَّهُ أَحَدٌ + المعوذتين", count: 1, ref: "أبو داود" },
    { text: "اللَّهُمَّ أَعِنِّي عَلَى ذِكْرِكَ، وَشُكْرِكَ، وَحُسْنِ عِبَادَتِكَ", count: 1, ref: "أبو داود" },
    { text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنَ الْبُخْلِ، وَأَعُوذُ بِكَ مِنَ الْجُبْنِ، وَأَعُوذُ بِكَ أَنْ أُرَدَّ إِلَى أَرْذَلِ الْعُمُرِ، وَأَعُوذُ بِكَ مِنْ فِتْنَةِ الدُّنْيَا، وَأَعُوذُ بِكَ مِنْ عَذَابِ الْقَبْرِ", count: 1, ref: "أبو داود" }
  ];

  // ========== أذكار الطعام ==========
  const foodAzkar = [
    { text: "بِسْمِ اللَّهِ (في أوله)", count: 1, ref: "أبو داود" },
    { text: "بِسْمِ اللَّهِ فِي أَوَّلِهِ وَآخِرِهِ (إذا نسي في البداية)", count: 1, ref: "أبو داود" },
    { text: "الْأَكْلُ بِاليَمِينِ وَالشُّرْبُ بِاليَمِينِ", count: 1, ref: "مسلم" },
    { text: "الْأَكْلُ مِمَّا يَلِيكَ", count: 1, ref: "متفق عليه" },
    { text: "الْحَمْدُ لِلَّهِ الَّذِي أَطْعَمَنِي هَذَا، وَرَزَقَنِيهِ مِنْ غَيْرِ حَوْلٍ مِنِّي وَلَا قُوَّةٍ", count: 1, ref: "الترمذي" },
    { text: "الْحَمْدُ لِلَّهِ حَمْدًا كَثِيرًا طَيِّبًا مُبَارَكًا فِيهِ، غَيْرَ مَكْفِيٍّ وَلَا مُوَدَّعٍ، وَلَا مُسْتَغْنًى عَنْهُ رَبَّنَا", count: 1, ref: "البخاري" },
    { text: "اللَّهُمَّ بَارِكْ لَنَا فِيهِ وَأَطْعِمْنَا خَيْرًا مِنْهُ (عند شرب اللبن)", count: 1, ref: "الترمذي" },
    { text: "اللَّهُمَّ بَارِكْ لَنَا فِيهِ وَزِدْنَا مِنْهُ (عند شرب اللبن)", count: 1, ref: "الترمذي" }
  ];

  // ========== أذكار المسجد ==========
  const mosqueAzkar = [
    { text: "اللَّهُمَّ افْتَحْ لِي أَبْوَابَ رَحْمَتِكَ (عند الدخول)", count: 1, ref: "مسلم" },
    { text: "بِسْمِ اللَّهِ، وَالصَّلَاةُ وَالسَّلَامُ عَلَى رَسُولِ اللَّهِ، اللَّهُمَّ اغْفِرْ لِي ذُنُوبِي وَافْتَحْ لِي أَبْوَابَ رَحْمَتِكَ", count: 1, ref: "الترمذي" },
    { text: "الدخول بالرجل اليمنى", count: 1, ref: "البخاري" },
    { text: "الخروج بالرجل اليسرى", count: 1, ref: "مسلم" },
    { text: "اللَّهُمَّ إِنِّي أَسْأَلُكَ مِنْ فَضْلِكَ (عند الخروج)", count: 1, ref: "مسلم" },
    { text: "بِسْمِ اللَّهِ، وَالصَّلَاةُ وَالسَّلَامُ عَلَى رَسُولِ اللَّهِ، اللَّهُمَّ اغْفِرْ لِي ذُنُوبِي وَافْتَحْ لِي أَبْوَابَ فَضْلِكَ (عند الخروج)", count: 1, ref: "مسلم" },
    { text: "ركعتان تحية المسجد قبل الجلوس", count: 1, ref: "متفق عليه" },
    { text: "قراءة آية الكرسي بعد الوضوء في المسجد", count: 1, ref: "الطبراني" }
  ];

  // ========== أذكار المنزل ==========
  const homeAzkar = [
    { text: "بِسْمِ اللَّهِ وَلَجْنَا، وَبِسْمِ اللَّهِ خَرَجْنَا، وَعَلَى اللَّهِ رَبِّنَا تَوَكَّلْنَا (عند الدخول)", count: 1, ref: "أبو داود" },
    { text: "السلام عليكم (عند الدخول)", count: 1, ref: "النور: 61" },
    { text: "اللَّهُمَّ إِنِّي أَسْأَلُكَ خَيْرَ الْمَوْلِجِ وَخَيْرَ الْمَخْرَجِ، بِسْمِ اللَّهِ وَلَجْنَا، وَبِسْمِ اللَّهِ خَرَجْنَا، وَعَلَى اللَّهِ رَبِّنَا تَوَكَّلْنَا (عند الخروج)", count: 1, ref: "أبو داود" },
    { text: "إطفاء النار والمصابيح بالليل قبل النوم", count: 1, ref: "متفق عليه" },
    { text: "تغطية الآنية وإغلاق الأبواب مع ذكر اسم الله", count: 1, ref: "متفق عليه" }
  ];

  // ========== أذكار السفر ==========
  const travelAzkar = [
    { text: "اللَّهُ أَكْبَرُ، اللَّهُ أَكْبَرُ، اللَّهُ أَكْبَرُ، سُبْحَانَ الَّذِي سَخَّرَ لَنَا هَذَا وَمَا كُنَّا لَهُ مُقْرِنِينَ، وَإِنَّا إِلَى رَبِّنَا لَمُنْقَلِبُونَ، اللَّهُمَّ إِنَّا نَسْأَلُكَ فِي سَفَرِنَا هَذَا الْبِرَّ وَالتَّقْوَى، وَمِنَ الْعَمَلِ مَا تَرْضَى، اللَّهُمَّ هَوِّنْ عَلَيْنَا سَفَرَنَا هَذَا وَاطْوِ عَنَّا بُعْدَهُ، اللَّهُمَّ أَنْتَ الصَّاحِبُ فِي السَّفَرِ، وَالْخَلِيفَةُ فِي الْأَهْلِ، اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنْ وَعْثَاءِ السَّفَرِ، وَكَآبَةِ الْمَنْظَرِ، وَسُوءِ الْمُنْقَلَبِ فِي الْمَالِ وَالْأَهْلِ", count: 1, ref: "مسلم" },
    { text: "آيِبُونَ تَائِبُونَ عَابِدُونَ لِرَبِّنَا حَامِدُونَ (عند الرجوع)", count: 1, ref: "مسلم" },
    { text: "دعاء دخول القرية أو البلد: اللَّهُمَّ رَبَّ السَّمَاوَاتِ السَّبْعِ وَمَا أَظْلَلْنَ، وَرَبَّ الْأَرَضِينَ السَّبْعِ وَمَا أَقْلَلْنَ، وَرَبَّ الشَّيَاطِينِ وَمَا أَضْلَلْنَ، وَرَبَّ الرِّيَاحِ وَمَا ذَرَيْنَ، أَسْأَلُكَ خَيْرَ هَذِهِ الْقَرْيَةِ وَخَيْرَ أَهْلِهَا وَخَيْرَ مَا فِيهَا، وَأَعُوذُ بِكَ مِنْ شَرِّهَا وَشَرِّ أَهْلِهَا وَشَرِّ مَا فِيهَا", count: 1, ref: "الحاكم" },
    { text: "التكبير عند الصعود والتسبيح عند النزول", count: 1, ref: "البخاري" }
  ];

  // ========== أذكار اللباس ==========
  const clothesAzkar = [
    { text: "الْحَمْدُ لِلَّهِ الَّذِي كَسَانِي هَذَا الثَّوْبَ وَرَزَقَنِيهِ مِنْ غَيْرِ حَوْلٍ مِنِّي وَلَا قُوَّةٍ", count: 1, ref: "الترمذي" },
    { text: "اللَّهُمَّ لَكَ الْحَمْدُ أَنْتَ كَسَوْتَنِيهِ، أَسْأَلُكَ مِنْ خَيْرِهِ وَخَيْرِ مَا صُنِعَ لَهُ، وَأَعُوذُ بِكَ مِنْ شَرِّهِ وَشَرِّ مَا صُنِعَ لَهُ (عند لبس الجديد)", count: 1, ref: "أبو داود" },
    { text: "تُسْمِي اللَّهَ إِذَا وَضَعْتَ ثَوْبَكَ (عند الخلع)", count: 1, ref: "الترمذي" },
    { text: "بِدَاءَةُ الْمِيْمَنَةِ فِي اللُّبْسِ", count: 1, ref: "متفق عليه" }
  ];

  // ========== أذكار متفرقة ==========
  const miscAzkar = [
    { text: "بِسْمِ اللَّهِ (عند دخول الخلاء)", count: 1, ref: "الترمذي" },
    { text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنَ الْخُبُثِ وَالْخَبَائِثِ (عند دخول الخلاء)", count: 1, ref: "متفق عليه" },
    { text: "غُفْرَانَكَ (عند الخروج من الخلاء)", count: 1, ref: "الترمذي" },
    { text: "الدخول بالرجل اليسرى للخلاء، واليمنى للخروج", count: 1, ref: "متفق عليه" },
    { text: "بِسْمِ اللَّهِ، تَوَكَّلْتُ عَلَى اللَّهِ، وَلَا حَوْلَ وَلَا قُوَّةَ إِلَّا بِاللَّهِ (عند الخروج من البيت)", count: 1, ref: "الترمذي" },
    { text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ أَنْ أَضِلَّ أَوْ أُضَلَّ، أَوْ أَزِلَّ أَوْ أُزَلَّ، أَوْ أَظْلِمَ أَوْ أُظْلَمَ، أَوْ أَجْهَلَ أَوْ يُجْهَلَ عَلَيَّ (عند الخروج من البيت)", count: 1, ref: "الترمذي" },
    { text: "اللَّهُمَّ اجْعَلْ فِي قَلْبِي نُورًا، وَفِي لِسَانِي نُورًا، وَفِي سَمْعِي نُورًا، وَفِي بَصَرِي نُورًا، وَمِنْ فَوْقِي نُورًا، وَمِنْ تَحْتِي نُورًا، وَعَنْ يَمِينِي نُورًا، وَعَنْ شِمَالِي نُورًا، وَمِنْ أَمَامِي نُورًا، وَمِنْ خَلْفِي نُورًا، وَاجْعَلْ لِي نُورًا", count: 1, ref: "متفق عليه" },
    { text: "اللَّهُمَّ إِنِّي أَسْأَلُكَ الْهُدَى وَالتُّقَى وَالْعَفَافَ وَالْغِنَى", count: 1, ref: "مسلم" },
    { text: "لَا إِلَهَ إِلَّا أَنْتَ سُبْحَانَكَ إِنِّي كُنْتُ مِنَ الظَّالِمِينَ (دعاء ذي النون)", count: 1, ref: "الأنبياء: 87" },
    { text: "رَبَّنَا آتِنَا فِي الدُّنْيَا حَسَنَةً وَفِي الْآخِرَةِ حَسَنَةً وَقِنَا عَذَابَ النَّارِ", count: 1, ref: "البقرة: 201" },
    { text: "اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنْ زَوَالِ نِعْمَتِكَ، وَتَحَوُّلِ عَافِيَتِكَ، وَفُجَاءَةِ نِقْمَتِكَ، وَجَمِيعِ سَخَطِكَ", count: 1, ref: "مسلم" },
    { text: "اللَّهُمَّ اغْفِرْ لِي ذَنْبِي كُلَّهُ، دِقَّهُ وَجِلَّهُ، وَأَوَّلَهُ وَآخِرَهُ، وَعَلَانِيَتَهُ وَسِرَّهُ", count: 1, ref: "مسلم" },
    { text: "اللَّهُمَّ إِنِّي أَسْأَلُكَ الْجَنَّةَ وَأَعُوذُ بِكَ مِنَ النَّارِ", count: 1, ref: "أبو داود" },
    { text: "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ، سُبْحَانَ اللَّهِ الْعَظِيمِ (كلمتان خفيفتان على اللسان، ثقيلتان في الميزان)", count: 1, ref: "متفق عليه" }
  ];

  // ========== المتغيرات ==========
  let currentDhikrIndex = 0;
  let count = 0;
  let salawatCount = 0;

  // ========== التخزين ==========
  function loadData() {
    const saved = localStorage.getItem('adhkari_data_v2');
    if (saved) {
      const data = JSON.parse(saved);
      count = data.count || 0;
      currentDhikrIndex = data.currentDhikrIndex || 0;
      salawatCount = data.salawatCount || 0;
      updateCounterDisplay();
      document.getElementById('salawatCount').textContent = salawatCount;
    }
  }

  function saveData() {
    localStorage.setItem('adhkari_data_v2', JSON.stringify({
      count, currentDhikrIndex, salawatCount
    }));
  }

  // ========== المسبحة ==========
  function renderDhikrList() {
    const list = document.getElementById('dhikrList');
    list.innerHTML = '';
    adhkar.forEach((d, i) => {
      const item = document.createElement('div');
      item.className = 'dhikr-item' + (i === currentDhikrIndex ? ' selected' : '');
      item.textContent = d.text.length > 28 ? d.text.substring(0, 28) + '...' : d.text;
      item.onclick = () => selectDhikr(i);
      list.appendChild(item);
    });
  }

  function selectDhikr(i) {
    currentDhikrIndex = i;
    count = 0;
    updateCounterDisplay();
    renderDhikrList();
    saveData();
  }

  function updateCounterDisplay() {
    const d = adhkar[currentDhikrIndex];
    document.getElementById('currentDhikr').textContent = d.text;
    document.getElementById('dhikrTarget').textContent = `العدد المطلوب: ${d.target}`;
    document.getElementById('counterDisplay').textContent = count;
    const progress = Math.min((count / d.target) * 100, 100);
    document.getElementById('progressFill').style.width = progress + '%';
  }

  function nextDhikr() {
    currentDhikrIndex = (currentDhikrIndex + 1) % adhkar.length;
    count = 0;
    updateCounterDisplay();
    renderDhikrList();
    saveData();
  }

  function prevDhikr() {
    currentDhikrIndex = (currentDhikrIndex - 1 + adhkar.length) % adhkar.length;
    count = 0;
    updateCounterDisplay();
    renderDhikrList();
    saveData();
  }

  function resetCounter() {
    count = 0;
    updateCounterDisplay();
    saveData();
  }

  document.getElementById('countBtn').addEventListener('click', () => {
    count++;
    const d = adhkar[currentDhikrIndex];
    if (count > d.target) {
      if (confirm(`أكملت ${d.target} مرة! هل تريد الانتقال للذكر التالي؟`)) {
        nextDhikr();
        return;
      }
    }
    updateCounterDisplay();
    saveData();
    if (navigator.vibrate) navigator.vibrate(30);
  });

  // ========== الصلاة على النبي ==========
  document.getElementById('salawatBtn').addEventListener('click', () => {
    salawatCount++;
    document.getElementById('salawatCount').textContent = salawatCount;
    if (navigator.vibrate) navigator.vibrate(30);
    saveData();
  });

  function resetSalawat() {
    if (confirm('هل تريد إعادة عداد الصلاة على النبي؟')) {
      salawatCount = 0;
      document.getElementById('salawatCount').textContent = 0;
      saveData();
    }
  }

  // ========== التبويبات ==========
  document.querySelectorAll('.tab').forEach(tab => {
    tab.addEventListener('click', () => {
      document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
      document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
      tab.classList.add('active');
      document.getElementById(tab.dataset.tab).classList.add('active');
    });
  });

  // ========== عرض الأذكار ==========
  function renderAzkar(list, containerId) {
    const container = document.getElementById(containerId);
    const key = 'adhkari_done_' + containerId;
    const done = JSON.parse(localStorage.getItem(key) || '[]');
    container.innerHTML = '';
    list.forEach((z, i) => {
      const isDone = done.includes(i);
      const card = document.createElement('div');
      card.className = 'azkar-card';
      card.innerHTML = `
        <div class="azkar-text">${z.text}</div>
        <div class="azkar-meta">
          <span class="azkar-count">العدد: ${z.count}</span>
          <span class="azkar-ref">${z.ref}</span>
          <button class="azkar-btn ${isDone ? 'done' : ''}" data-idx="${i}">
            ${isDone ? '✓ تم' : 'تم ✓'}
          </button>
        </div>
      `;
      container.appendChild(card);
    });
    container.querySelectorAll('.azkar-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        const idx = parseInt(btn.dataset.idx);
        const done = JSON.parse(localStorage.getItem(key) || '[]');
        if (done.includes(idx)) {
          done.splice(done.indexOf(idx), 1);
        } else {
          done.push(idx);
        }
        localStorage.setItem(key, JSON.stringify(done));
        renderAzkar(list, containerId);
        updateStats();
      });
    });
  }

  // ========== الإحصائيات ==========
  function updateStats() {
    const allLists = [
      { id: 'morningList', list: morningAzkar },
      { id: 'eveningList', list: eveningAzkar },
      { id: 'sleepList', list: sleepAzkar },
      { id: 'wakeList', list: wakeAzkar },
      { id: 'prayerList', list: prayerAzkar },
      { id: 'foodList', list: foodAzkar },
      { id: 'mosqueList', list: mosqueAzkar },
      { id: 'homeList', list: homeAzkar },
      { id: 'travelList', list: travelAzkar },
      { id: 'clothesList', list: clothesAzkar },
      { id: 'miscList', list: miscAzkar }
    ];
    let total = 0, done = 0;
    allLists.forEach(({ id, list }) => {
      total += list.length;
      const d = JSON.parse(localStorage.getItem('adhkari_done_' + id) || '[]');
      done += d.length;
    });
    document.getElementById('totalCount').textContent = total;
    document.getElementById('doneCount').textContent = done;
  }

  // ========== التشغيل ==========
  loadData();
  renderDhikrList();
  updateCounterDisplay();
  renderAzkar(morningAzkar, 'morningList');
  renderAzkar(eveningAzkar, 'eveningList');
  renderAzkar(sleepAzkar, 'sleepList');
  renderAzkar(wakeAzkar, 'wakeList');
  renderAzkar(prayerAzkar, 'prayerList');
  renderAzkar(foodAzkar, 'foodList');
  renderAzkar(mosqueAzkar, 'mosqueList');
  renderAzkar(homeAzkar, 'homeList');
  renderAzkar(travelAzkar, 'travelList');
  renderAzkar(clothesAzkar, 'clothesList');
  renderAzkar(miscAzkar, 'miscList');
  updateStats();
</script>
</body>
</html>
