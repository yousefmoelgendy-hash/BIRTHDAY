# BIRTHDAY
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>كل سنه وانت طيبه يقمر ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&family=Amiri:ital,wght@0,700;1,700&display=swap" rel="stylesheet">
    <style>
        :root {
            --matrix-pink: #ff2a75;
            --soft-pink: #ff758c;
            --correct-green: #2ed573;
            --wrong-red: #ff4757;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Tajawal', sans-serif;
            background: linear-gradient(135deg, #0f0c20 0%, #2b102f 50%, #0f0c20 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow-x: hidden;
            padding: 15px;
            color: #ffffff;
        }

        #matrixCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 0;
        }

        .music-btn {
            position: fixed;
            top: 15px;
            right: 15px;
            z-index: 100;
            background: rgba(255, 42, 117, 0.3);
            border: 1px solid var(--matrix-pink);
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            backdrop-filter: blur(5px);
            font-family: 'Tajawal', sans-serif;
            font-size: 0.9rem;
        }

        .container {
            width: 100%;
            max-width: 420px;
            height: 580px;
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(15px);
            border-radius: 25px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5), 0 0 15px rgba(255, 42, 117, 0.2);
            padding: 20px;
            text-align: center;
            position: relative;
            z-index: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            border: 1px solid rgba(255, 42, 117, 0.4);
            overflow: hidden;
        }

        .screen { 
            display: none; 
            opacity: 0;
            transform: translateY(10px);
            transition: all 0.5s ease-in-out;
            height: 100%;
            width: 100%;
            overflow-y: auto;
            padding-right: 5px;
        }
        
        .screen.active { 
            display: flex; 
            flex-direction: column;
            justify-content: flex-start;
            align-items: center;
            opacity: 1;
            transform: translateY(0);
        }

        .screen::-webkit-scrollbar {
            width: 5px;
        }
        .screen::-webkit-scrollbar-thumb {
            background: var(--matrix-pink);
            border-radius: 10px;
        }

        .countdown-text {
            font-size: 2.2rem;
            font-weight: bold;
            color: var(--matrix-pink);
            text-shadow: 0 0 20px var(--matrix-pink);
            font-family: 'Amiri', serif;
            text-align: center;
            width: 100%;
            word-break: break-word;
            line-height: 1.4;
            margin: auto 0;
        }

        h2 { 
            font-family: 'Amiri', serif; 
            color: var(--matrix-pink); 
            margin-bottom: 12px;
            font-size: 1.5rem;
        }
        
        p, .msg-box { 
            line-height: 1.8; 
            color: #f0f0f0; 
            font-size: 0.98rem; 
            margin-bottom: 15px;
            word-wrap: break-word;
            overflow-wrap: break-word;
            white-space: pre-wrap;
            text-align: right;
            width: 100%;
        }

        .btn {
            background: linear-gradient(45deg, #ff2a75, #ff758c); 
            color: white; 
            border: none;
            padding: 10px 25px; 
            border-radius: 25px; 
            cursor: pointer;
            font-size: 1rem; 
            transition: 0.3s; 
            margin-top: 10px;
            font-family: 'Tajawal', sans-serif;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(255, 42, 117, 0.4);
            flex-shrink: 0;
            text-decoration: none;
            display: inline-block;
        }
        
        .btn:hover { 
            transform: scale(1.05); 
        }

        .cake-container {
            position: relative;
            display: inline-block;
            margin: 15px 0;
            cursor: pointer;
        }
        .cake { font-size: 4.5rem; }
        .flame {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 1.6rem;
            animation: burn 0.5s infinite alternate;
        }
        .flame.off { display: none; }
        @keyframes burn {
            0% { transform: translateX(-50%) scale(1); opacity: 1; }
            100% { transform: translateX(-50%) scale(1.2); opacity: 0.8; }
        }

        .quiz-opt {
            background: rgba(255,255,255,0.1);
            border: 1px solid var(--matrix-pink);
            padding: 12px 15px;
            border-radius: 12px;
            margin: 8px 0;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            font-weight: bold;
        }
        .quiz-opt:hover {
            background: var(--matrix-pink);
        }
        .quiz-opt.correct {
            background: var(--correct-green) !important;
            border-color: var(--correct-green) !important;
            color: #fff;
        }
        .quiz-opt.wrong {
            background: var(--wrong-red) !important;
            border-color: var(--wrong-red) !important;
            color: #fff;
        }
        .quiz-feedback {
            font-size: 0.95rem;
            margin-top: 10px;
            min-height: 25px;
            font-weight: bold;
        }

        .heart-gallery {
            display: flex;
            justify-content: center;
            gap: 10px;
            flex-wrap: wrap;
            margin: 15px 0;
        }
        .heart-frame {
            width: 80px;
            height: 80px;
            clip-path: path('M 40,12 A 20,20 0 0,0 0,40 C 0,60 40,80 40,80 C 40,80 80,60 80,40 A 20,20 0 0,0 40,12 Z');
            background: var(--matrix-pink);
            padding: 2px;
            cursor: pointer;
            transition: transform 0.3s;
        }
        .heart-frame:hover { transform: scale(1.1); }
        .heart-frame img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            clip-path: path('M 40,12 A 20,20 0 0,0 0,40 C 0,60 40,80 40,80 C 40,80 80,60 80,40 A 20,20 0 0,0 40,12 Z');
        }

        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.85);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        .modal img { max-width: 85%; max-height: 75%; border-radius: 15px; border: 2px solid var(--matrix-pink); }

        .timer-box { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin: 15px 0; width: 100%; }
        .time-unit { background: rgba(0, 0, 0, 0.4); padding: 10px; border-radius: 12px; border: 1px solid rgba(255, 42, 117, 0.3); }
        .time-unit span { display: block; font-weight: bold; font-size: 1.2rem; color: var(--matrix-pink); }
        
        .timeline { text-align: right; margin: 15px 0; border-right: 2px solid var(--matrix-pink); padding-right: 12px; width: 100%; }
        .event { margin-bottom: 15px; position: relative; }
        .event::after { content: '✨'; position: absolute; right: -20px; top: 0; }
        .event-date { font-weight: bold; color: var(--matrix-pink); font-size: 0.9rem; }

        .links-grid {
            display: flex;
            flex-direction: column;
            gap: 10px;
            width: 100%;
            margin: 15px 0;
        }
        .site-card {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 42, 117, 0.4);
            padding: 12px;
            border-radius: 15px;
            text-align: right;
            text-decoration: none;
            color: #fff;
            transition: 0.3s;
        }
        .site-card:hover {
            background: rgba(255, 42, 117, 0.2);
            transform: translateY(-2px);
        }
        .site-card h4 { color: var(--matrix-pink); margin-bottom: 3px; font-size: 1rem; }
        .site-card p { font-size: 0.8rem; color: #ccc; margin-bottom: 0; }
    </style>
</head>
<body>

<button class="music-btn" id="musicBtn" onclick="toggleAudio()">🎵 تشغيل الصوت</button>
<audio id="bgMusic" loop src="hBD.mp3" preload="auto"></audio>

<canvas id="matrixCanvas"></canvas>

<div class="container">
    
    <!-- Screen 1: Matrix -->
    <div class="screen active" id="screen1">
        <div class="countdown-text" id="cdText">3</div>
    </div>

    <!-- Screen 2: Candle Blowing -->
    <div class="screen" id="screen2">
        <h2>اتمني امنيه ودوسي علي الشمعه ونطفيها 🎂</h2>
        <div class="cake-container" onclick="blowOutCandle()">
            <div class="flame" id="flame">🔥</div>
            <div class="cake">🎂</div>
        </div>
        <p id="candleInstruction" style="text-align: center;">اتمني امنيه ي ميور وادعيلي.. ✨</p>
    </div>

    <!-- Screen 3: Typewriter Msg Part 1 -->
    <div class="screen" id="screen3">
        <h2>مسج عيد ميلادك ❤️</h2>
        <div class="msg-box" id="typeText1"></div>
        <button class="btn" id="btnNext1" style="display:none;" onclick="nextScreen(3.5)">التالي... ✨</button>
    </div>

    <!-- Screen 3.5: Typewriter Msg Part 2 -->
    <div class="screen" id="screen3_5">
        <h2>مسج عيد ميلادك ❤️</h2>
        <div class="msg-box" id="typeText2"></div>
        <button class="btn" id="btnNext2" style="display:none;" onclick="nextScreen(4)">نلعب لعبة صغيرة؟ 🎮</button>
    </div>

    <!-- Screen 4: Quiz -->
    <div class="screen" id="screen4">
        <h2>يلا جاوبي يبت 😂</h2>
        <div id="quizContainer" style="width: 100%;">
            <p id="quizQuestion" style="font-weight: bold; color: var(--soft-pink); text-align: center; margin-bottom: 15px; font-size: 1.1rem;"></p>
            <div id="quizOptions"></div>
            <div id="quizFeedback" class="quiz-feedback"></div>
        </div>
    </div>

    <!-- Screen 5: Heart Gallery (9 Photos) -->
    <div class="screen" id="screen5">
        <h2>شويه صور كد بينا ✨</h2>
        <p style="text-align: center;">دوسي على أي صورة عشان تكبريها ❤️</p>
        <div class="heart-gallery">
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/wjK4cn6V/photo-2026-09-08-00-56-18.jpg')">
                <img src="https://i.postimg.cc/wjK4cn6V/photo-2026-09-08-00-56-18.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/vBm0Zsvt/photo-2026-09-08-00-56-21.jpg')">
                <img src="https://i.postimg.cc/vBm0Zsvt/photo-2026-09-08-00-56-21.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/zvbpTF6H/photo-2026-09-08-00-56-23.jpg')">
                <img src="https://i.postimg.cc/zvbpTF6H/photo-2026-09-08-00-56-23.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/W45QnSWy/photo-2026-09-08-00-56-25.jpg')">
                <img src="https://i.postimg.cc/W45QnSWy/photo-2026-09-08-00-56-25.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/J43YxPG8/photo-2026-09-08-00-56-27.jpg')">
                <img src="https://i.postimg.cc/J43YxPG8/photo-2026-09-08-00-56-27.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/MZV9Zd0K/photo-2026-09-08-00-56-29.jpg')">
                <img src="https://i.postimg.cc/MZV9Zd0K/photo-2026-09-08-00-56-29.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/3rXZQW7r/photo-2026-09-08-00-56-32.jpg')">
                <img src="https://i.postimg.cc/3rXZQW7r/photo-2026-09-08-00-56-32.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/3NYmxC7T/photo-2026-09-08-00-56-34.jpg')">
                <img src="https://i.postimg.cc/3NYmxC7T/photo-2026-09-08-00-56-34.jpg">
            </div>
            <div class="heart-frame" onclick="openModal('https://i.postimg.cc/3xdpNwMR/photo-2026-09-08-00-56-36.jpg')">
                <img src="https://i.postimg.cc/3xdpNwMR/photo-2026-09-08-00-56-36.jpg">
            </div>
        </div>
        <button class="btn" onclick="nextScreen(6)">إحنا مع بعض من قد إيه؟</button>
    </div>

    <!-- Screen 6: Love Timer -->
    <div class="screen" id="screen6">
        <h2>من اول ما اتقابلنا ❤️</h2>
        <div class="timer-box">
            <div class="time-unit"><span id="days">0</span> يوم</div>
            <div class="time-unit"><span id="hours">0</span> ساعة</div>
            <div class="time-unit"><span id="minutes">0</span> دقيقة</div>
            <div class="time-unit"><span id="seconds">0</span> ثانية</div>
        </div>
        <button class="btn" onclick="nextScreen(7)">قصتنا 📖</button>
    </div>

    <!-- Screen 7: Timeline FULL -->
    <div class="screen" id="screen7">
        <h2>Our Story 📖</h2>
        <div class="timeline">
            <div class="event"><div class="event-date">١٣ / ١٠ / ٢٠٢٢</div><div>الصدفه واول يوم لينا مع بعض🫶🏻🫵🏻</div></div>
            <div class="event"><div class="event-date">١ / ١ / ٢٠٢٣</div><div>يوم ما بطلنا استعباط واعلنا ارتباطنا😍😉</div></div>
            <div class="event"><div class="event-date">٣٠ / ١١ / ٢٠٢٣</div><div>يوم ما وثقتي فيا ثقه عمياء وجيتي معايا عند البطاط واغلي يوم عندي بعد يوم ما عرفنا بعض❤️🫡</div></div>
            <div class="event"><div class="event-date">٢ / ٦ / ٢٠٢٤</div><div>First touch😍 اول ماسكه ايد لبعض</div></div>
            <div class="event"><div class="event-date">٥ / ١ / ٢٠٢٥</div><div>اول بوسه انتي عطيهالي😂🫶🏻</div></div>
            <div class="event"><div class="event-date">٢٥ / ١ / ٢٠٢٥</div><div>يوم كامل من اوله لاخره عيشناه مع بعض من الصبح لاخر اليوم بليل❤️😉</div></div>
            <div class="event"><div class="event-date">٨ / ١ / ٢٠٢٥ 🔚 ٣٠ / ١ / ٢٠٢٥</div><div>Retry... 🔄</div></div>
            <div class="event"><div class="event-date">٣١ / ١ / ٢٠٢٥</div><div>Last kiss.......😘</div></div>
            <div class="event"><div class="event-date">٣ / ٢ / ٢٠٢٥ 🔚 ٢٥ / ٢ / ٢٠٢٥</div><div>Lost in my life....... 💔</div></div>
            <div class="event"><div class="event-date">١٢ / ٣ / ٢٠٢٥</div><div>عوده علاقات🫀🫂...</div></div>
            <div class="event"><div class="event-date">٢٢ / ٣ / ٢٠٢٥</div><div>بعاد تاني🙂.....</div></div>
            <div class="event"><div class="event-date">١ / ٤ / ٢٠٢٥</div><div>عوده علاقات😂🫀....</div></div>
            <div class="event"><div class="event-date">٧ / ٤ / ٢٠٢٥</div><div>بعاد تالت🥰..</div></div>
            <div class="event"><div class="event-date">١٠ / ٤ / ٢٠٢٥</div><div>الصلح❤️.</div></div>
            <div class="event"><div class="event-date">١٢ / ٥ / ٢٠٢٥</div><div>بعاد رابع.....</div></div>
            <div class="event"><div class="event-date">٣١ / ٥ / ٢٠٢٥</div><div>عوده علاقات😂😍..</div></div>
            <div class="event"><div class="event-date">١١ / ٧ / ٢٠٢٥</div><div>بعاد خامس واسوء بعاد.....</div></div>
            <div class="event"><div class="event-date">٢٢ / ٧ / ٢٠٢٥</div><div>العوده والصلح بقي😍🫂🫀...</div></div>
            <div class="event"><div class="event-date">٢٨ / ٨ / ٢٠٢٥</div><div>بعاد......</div></div>
            <div class="event"><div class="event-date">٢٩ / ٨ / ٢٠٢٥</div><div>استعباط😂😆....</div></div>
            <div class="event"><div class="event-date">٣٠ / ٨ / ٢٠٢٥</div><div>الرجعه😍🫂....</div></div>
            <div class="event"><div class="event-date">١٥ / ١١ / ٢٠٢٥</div><div>بعاد المفروض لابد.</div></div>
            <div class="event"><div class="event-date">٢٩ / ١٢ / ٢٠٢٥</div><div>حاولت ومفيش فايده...</div></div>
            <div class="event"><div class="event-date">٢٣ / ١ / ٢٠٢٦</div><div>اتكلمنا تاني❤️..</div></div>
            <div class="event"><div class="event-date">١٨ / ٢ / ٢٠٢٦</div><div>قطعنا..</div></div>
            <div class="event"><div class="event-date">١٠ / ٣ / ٢٠٢٦</div><div>بتوحشيني</div></div>
            <div class="event"><div class="event-date">١٧ / ٣ / ٢٠٢٦</div><div>العوده زي زمان ان شاء الله 🫶</div></div>
            <div class="event"><div class="event-date">٤ / ٤ / ٢٠٢٦</div><div>نفس النهايه😂😂...</div></div>
            <div class="event"><div class="event-date">٢٨ / ٤ / ٢٠٢٦</div><div>رجعنا نتكلم...</div></div>
            <div class="event"><div class="event-date">١٢ / ٥ / ٢٠٢٦</div><div>قطعنا كلام...</div></div>
            <div class="event"><div class="event-date">٢٤ / ٥ / ٢٠٢٦</div><div>نهايتنا....</div></div>
            <div class="event"><div class="event-date">١٩ / ٨ / ٢٠٢٦</div><div>رجعنا اتكلمنا عادي</div></div>
        </div>
        <button class="btn" onclick="nextScreen(8)">الويب سايت اللي عاملتهالك 🌐</button>
    </div>

    <!-- Screen 8: Old Websites Archive -->
    <div class="screen" id="screen8">
        <h2>مواقعنا القديمة 🌐✨</h2>
        <p style="text-align: center; margin-bottom: 10px;">جمعتلك كل حاجة عملتها ليكي هنا عشان تفضل ذكري جميلة بينا ❤️</p>
        
        <div class="links-grid">
            <a href="https://yousefmoelgendy-hash.github.io/el-eidd/" target="_blank" class="site-card">
                <h4>🌙 ويب سايت العيد</h4>
                <p>اضغطي هنا عشان تفتحي ويب سايت العيد..</p>
            </a>
            
            <a href="https://yousefmoelgendy-hash.github.io/valentine/" target="_blank" class="site-card">
                <h4>❤️ ويب سايت الفلانتين</h4>
                <p>اضغطي هنا عشان تفتحي ويب سايت الفلانتين..</p>
            </a>

            <a href="https://yousefmoelgendy-hash.github.io/cristmass/" target="_blank" class="site-card">
                <h4>🎄 ويب سايت الكريسماس</h4>
                <p>اضغطي هنا عشان تفتحي ويب سايت الكريسماس..</p>
            </a>
        </div>

        <button class="btn" onclick="nextScreen(9)">اخر حاجه.. ❤️</button>
    </div>

    <!-- Screen 9: Final -->
    <div class="screen" id="screen9">
        <h2>المهم يست الكل. ❤️</h2>
        <p style="text-align: center; font-size: 1.05rem;">
            اتمني ي ميور تكون المسج عجبتك واكون قدرت جمعت كل حاجه فيها واكون عرفت ابسطك واكون اخر مره اتقابلنا اخليكي تكوني حسيتي من نحيتي بعدم الخوف والامان شويه واكون راضيتك واتمنالك الخير في حياتك وكل حاجه يميوره ي جلبي ❤️
        </p>
        <div style="font-size: 2.8rem; margin-top: 15px;">🫂❤️✨</div>
    </div>

</div>

<div class="modal" id="imgModal" onclick="closeModal()">
    <img id="modalImg" src="">
</div>

<script>
    // Matrix Background
    const canvas = document.getElementById('matrixCanvas');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth; 
    canvas.height = window.innerHeight;
    const chars = '❤️✨🎂';
    const drops = Array(Math.floor(canvas.width / 16)).fill(1);

    function drawMatrix() {
        ctx.fillStyle = 'rgba(15, 12, 32, 0.1)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = '#ff2a75';
        ctx.font = '16px monospace';
        drops.forEach((y, i) => {
            const text = chars[Math.floor(Math.random() * chars.length)];
            ctx.fillText(text, i * 16, y * 16);
            if (y * 16 > canvas.height && Math.random() > 0.975) drops[i] = 0;
            drops[i]++;
        });
    }
    setInterval(drawMatrix, 33);

    // Audio Control
    const audio = document.getElementById('bgMusic');
    const musicBtn = document.getElementById('musicBtn');

    function playAudio() {
        audio.play().then(() => {
            musicBtn.innerText = '🔊 إيقاف الصوت';
        }).catch(err => {
            console.log("Audio playback waiting for interaction");
        });
    }

    function toggleAudio() {
        if (audio.paused) { 
            playAudio();
        } else { 
            audio.pause(); 
            musicBtn.innerText = '🎵 تشغيل الصوت'; 
        }
        initMic();
    }

    // Countdown
    const sequence = ['3', '2', '1', 'HAPPY BIRTHDAY Mayar ❤️'];
    let seqIdx = 0;
    function runCountdown() {
        if (seqIdx < sequence.length) {
            const cdElem = document.getElementById('cdText');
            cdElem.innerText = sequence[seqIdx++];
            if(sequence[seqIdx - 1].includes('HAPPY BIRTHDAY')) {
                cdElem.style.fontSize = '2.2rem';
            } else {
                cdElem.style.fontSize = '3.5rem';
            }
            setTimeout(runCountdown, 1000);
        } else { 
            nextScreen(2); 
        }
    }
    runCountdown();

    // Candle Blowing Logic
    function blowOutCandle() {
        document.getElementById('flame').classList.add('off');
        document.getElementById('candleInstruction').innerText = 'أمنيتك هتتحقق إن شاء الله! ❤️✨';
        
        // Play song automatically
        playAudio();

        setTimeout(() => nextScreen(3), 2000);
    }

    let micInitialized = false;
    function initMic() {
        if (micInitialized) return;
        if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
            navigator.mediaDevices.getUserMedia({ audio: true }).then(stream => {
                micInitialized = true;
                const ctx = new AudioContext();
                const mic = ctx.createMediaStreamSource(stream);
                const analyzer = ctx.createAnalyser();
                mic.connect(analyzer);
                const data = new Uint8Array(analyzer.frequencyBinCount);
                function checkBlowing() {
                    analyzer.getByteFrequencyData(data);
                    let sum = data.reduce((a, b) => a + b, 0);
                    if (sum / data.length > 40) { blowOutCandle(); }
                    else if (!document.getElementById('flame').classList.contains('off')) { requestAnimationFrame(checkBlowing); }
                }
                checkBlowing();
            }).catch(() => {});
        }
    }

    // Message Split into 2 Parts
    const msg1_part1 = "كل سنه وانت طيبه ي ميور وتكون سنه سعيده عليكي وتحققي كل حاجه بتتمنياها وكل حاجه كانت وحشه في حياتك اذا كان انا او اي حاجه تانيه تتعوضي عنها كل خير ي ميور انا عامل الويب سايت دي الله اعلم هتكون اخر ويب سايت او لسه في كمان هنعمهالك ومهما كان اي بينا بس تكون ذكري كويسه بينا وانا المسج دي مش هقعد اتكلم في حاجه وحشه او اي حاجه دا ويب سايت عيد ميلادك ياعني كلها هتكون حاجه كويسه مش عايز فيها اي حاجه تكون فيها زعل.";
    const msg1_part2 = "انا عايزك كد ي ميور تكوني افضل واحده في الدنيا عايز البنت الي انا ربيتها اربع سنين تعمل بتربيتها مهما كنا اي قدام عايزك كد دايما في افضل حال مش عايز جواهرك النضيف يتوسخ مهما كان حواليكي اي او مهما كان المشاكل الي عديتي بيها خليكي دايما نضيفه وابعدي عن اي حاجه تكون واحد في الميه توسخ جواهرك النضيف وان شاء الله تكون سنه سعيده وكل سنينك الجايه تكون سعيده وتكوني في اسعد حال واشوفك احلى عروسه في الدنيا ومش هقولك مستحيل ان تكوني انتي عروستي لان ربنا لو عايز حاجه تحصل هتحصل انا ايوه الموضوع انا وانتي شايفنه صعب بس انا مبقتش افكر ان المواضيع صعبه او غيرها زي ما قولتلك بسيب كل حاجه ربنا الي يختارها ليا وانا عايزك اهم حاجه ي ميور تكوني قريبه من ربنا وترجعي تصلي واخر حاجه هختم بيها كلامي ان شاء الله هجمعلك كل حاجه كانت بينا او بينا (كويسه) هنا في الويب سايت عايزه تخليها ذكري او لا براحتك بس دي هتكون يعتبر ذكري كويسه بينا في يوم عشان زي ما انتي بتقولي مش عايزه يكون بينا حاجه وحشه وبرضه مش هستكتر الكلمه عليكي في عيد ميلادك وهقولهالك (بحبك ي ميار واتمني اشوفك اسعد واحده في الدنيا وتحققي كل حاجه بتحلمي بيها اعرفها او معرفهاش)❤️.";

    function typeWriter(text, elementId, btnId) {
        let i = 0;
        const elem = document.getElementById(elementId);
        elem.innerText = "";
        function type() {
            if (i < text.length) {
                elem.innerText += text.charAt(i);
                i++;
                setTimeout(type, 25);
            } else {
                document.getElementById(btnId).style.display = 'inline-block';
            }
        }
        type();
    }

    function nextScreen(id) {
        document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
        
        let targetId = 'screen' + id;
        if (id === 3.5) targetId = 'screen3_5';
        
        const next = document.getElementById(targetId);
        next.classList.add('active');
        next.scrollTop = 0;
        
        if(id === 2) initMic();
        if(id === 3) typeWriter(msg1_part1, 'typeText1', 'btnNext1');
        if(id === 3.5) typeWriter(msg1_part2, 'typeText2', 'btnNext2');
        if(id === 4) loadQuiz();
        if(id === 6) startTimer();
    }

    // Quiz Logic
    const questions = [
        { q: "مين كان بيتقمص بسرعه؟ ", opts: ["يوسف", "ميار"], correct: "ميار" },
        { q: "مين كان اكتر حد حنين؟ ", opts: ["يوسف", "ميار"], correct: "يوسف" },
        { q: " مين اكتر حد مستفز؟محدش غيرك مستفز😂❤️ ", opts: ["ميار", "ميار"], correct: "ميار" }
    ];
    let qIdx = 0;
    let score = 0;
    let canAnswer = true;

    function loadQuiz() {
        canAnswer = true;
        const feedback = document.getElementById('quizFeedback');
        feedback.innerText = '';
        
        if(qIdx < questions.length) {
            const current = questions[qIdx];
            document.getElementById('quizQuestion').innerText = current.q;
            const container = document.getElementById('quizOptions');
            container.innerHTML = '';
            
            current.opts.forEach(opt => {
                const div = document.createElement('div');
                div.className = 'quiz-opt';
                div.innerText = opt;
                div.onclick = () => checkAnswer(div, opt, current.correct);
                container.appendChild(div);
            });
        } else {
            const container = document.getElementById('quizContainer');
            container.innerHTML = `
                <h3 style="color: var(--matrix-pink); margin-bottom: 10px;">نتيجة الكويز 🏆</h3>
                <p style="text-align: center; font-size: 1.1rem; font-weight: bold;">جبتي ${score} من ${questions.length}! ${score === 3 ? 'شطورة يا ميور فخور بيكي يبت 😍' : 'ماشية بركة بس بحبك برضه ❤️'}</p>
                <button class="btn" onclick="nextScreen(5)">نشوف ذكرياتنا؟ ✨</button>
            `;
        }
    }

    function checkAnswer(selectedDiv, selectedOpt, correctOpt) {
        if (!canAnswer) return;
        canAnswer = false;

        const feedback = document.getElementById('quizFeedback');
        const allOpts = document.querySelectorAll('.quiz-opt');

        if (selectedOpt === correctOpt) {
            selectedDiv.classList.add('correct');
            feedback.style.color = 'var(--correct-green)';
            feedback.innerText = 'صح شاطرة! 🎉✨';
            score++;
        } else {
            selectedDiv.classList.add('wrong');
            feedback.style.color = 'var(--wrong-red)';
            feedback.innerText = `غلط! الإجابة الصح هي: ${correctOpt}`;
            
            allOpts.forEach(div => {
                if (div.innerText === correctOpt) div.classList.add('correct');
            });
        }

        setTimeout(() => {
            qIdx++;
            loadQuiz();
        }, 1500);
    }

    // Timer
    function startTimer() {
        const startDate = new Date("2022-10-13T00:00:00").getTime();
        setInterval(() => {
            const diff = new Date().getTime() - startDate;
            document.getElementById("days").innerText = Math.floor(diff / (1000 * 60 * 60 * 24));
            document.getElementById("hours").innerText = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            document.getElementById("minutes").innerText = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            document.getElementById("seconds").innerText = Math.floor((diff % (1000 * 60)) / 1000);
        }, 1000);
    }

    function openModal(src) { 
        document.getElementById('modalImg').src = src; 
        document.getElementById('imgModal').style.display = 'flex'; 
    }
    
    function closeModal() { 
        document.getElementById('imgModal').style.display = 'none'; 
    }
</script>

</body>
</html>
