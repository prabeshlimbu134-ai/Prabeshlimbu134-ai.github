<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Happy Birthday, My Love ❤️</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Montserrat:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,500;0,700;1,400&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            --primary: #e8889c;
            --primary-dark: #b84964;
            --accent: #fcd34d;
            --bg-dark: #120914;
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background: linear-gradient(135deg, #18091a 0%, #2a0826 50%, #120914 100%);
            color: #fce7f3;
            overflow-x: hidden;
            touch-action: manipulation;
        }

        .font-serif-custom {
            font-family: 'Playfair Display', serif;
        }

        .font-cursive {
            font-family: 'Dancing Script', cursive;
        }

        /* Floating Hearts & Lilies Canvas */
        #bgCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        /* Glassmorphism styling */
        .glass-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 182, 193, 0.18);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        /* Lilies Cake Styling & Animations */
        .cake-container {
            position: relative;
            width: 260px;
            height: 220px;
            margin: 0 auto;
            cursor: pointer;
        }

        .cake-tier {
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 16px 16px 8px 8px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.4);
            overflow: hidden;
        }

        .cake-bottom {
            bottom: 0;
            width: 230px;
            height: 80px;
            background: linear-gradient(135deg, #fbcfe8 0%, #f472b6 60%, #e11d48 100%);
            border-bottom: 8px solid #9f1239;
        }

        .cake-top {
            bottom: 80px;
            width: 170px;
            height: 70px;
            background: linear-gradient(135deg, #ffffff 0%, #fce7f3 60%, #f472b6 100%);
            border-bottom: 6px solid #be185d;
        }

        /* Lily Icing & Vines */
        .icing {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 20px;
            background: #fff;
            border-radius: 0 0 12px 12px;
            box-shadow: 0 2px 6px rgba(0,0,0,0.15);
        }

        .vine-decor {
            position: absolute;
            bottom: 12px;
            left: 0;
            width: 100%;
            height: 12px;
            background: radial-gradient(circle at 10px 6px, #4ade80 4px, transparent 5px) repeat-x;
            background-size: 20px 12px;
            opacity: 0.8;
        }

        /* Lily Petal Overlays on Cake */
        .cake-lily-decor {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 45px;
            height: 45px;
            pointer-events: none;
            z-index: 5;
        }

        .candle {
            position: absolute;
            bottom: 150px;
            width: 12px;
            height: 45px;
            background: linear-gradient(to right, #fef08a, #f59e0b);
            border-radius: 6px 6px 2px 2px;
            box-shadow: 0 0 8px rgba(251, 191, 36, 0.6);
            z-index: 10;
        }

        .candle-1 { left: 33%; }
        .candle-2 { left: 50%; transform: translateX(-50%); }
        .candle-3 { left: 67%; }

        .flame {
            position: absolute;
            top: -20px;
            left: 50%;
            transform: translateX(-50%);
            width: 16px;
            height: 22px;
            background: radial-gradient(ellipse at bottom, #fef08a 0%, #f97316 60%, transparent 100%);
            border-radius: 50% 50% 20% 20%;
            box-shadow: 0 0 14px #f97316, 0 0 28px #fef08a;
            animation: flicker 1.2s infinite alternate ease-in-out;
            transform-origin: center bottom;
        }

        @keyframes flicker {
            0% { transform: translateX(-50%) scale(1) rotate(-2deg); opacity: 0.9; }
            50% { transform: translateX(-50%) scale(1.15) rotate(2deg); opacity: 1; }
            100% { transform: translateX(-50%) scale(0.95) rotate(-1deg); opacity: 0.85; }
        }

        .flame.extinguished {
            display: none !important;
        }

        .smoke {
            position: absolute;
            top: -25px;
            left: 50%;
            transform: translateX(-50%);
            width: 6px;
            height: 6px;
            background: rgba(220, 220, 220, 0.7);
            border-radius: 50%;
            animation: rise 2s forwards ease-out;
            opacity: 0;
        }

        @keyframes rise {
            0% { opacity: 0.8; transform: translateX(-50%) translateY(0) scale(1); }
            100% { opacity: 0; transform: translateX(-50%) translateY(-45px) scale(3.5); }
        }

        /* Card Flip Effect */
        .flip-card {
            perspective: 1000px;
            height: 180px;
        }

        .flip-card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.6s cubic-bezier(0.4, 0.2, 0.2, 1);
            transform-style: preserve-3d;
        }

        .flip-card.flipped .flip-card-inner {
            transform: rotateY(180deg);
        }

        .flip-card-front, .flip-card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            border-radius: 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1.25rem;
        }

        .flip-card-back {
            transform: rotateY(180deg);
        }

        /* Letter Envelope Animation */
        .letter-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.8s cubic-bezier(0, 1, 0, 1);
        }

        .letter-content.open {
            max-height: 2000px;
            transition: max-height 1.2s cubic-bezier(0.85, 0, 0.15, 1);
        }

        .glow-pulse {
            animation: glowPulse 2s infinite alternate;
        }

        @keyframes glowPulse {
            0% { box-shadow: 0 0 15px rgba(244, 114, 182, 0.4); }
            100% { box-shadow: 0 0 30px rgba(244, 114, 182, 0.8), 0 0 15px rgba(254, 240, 138, 0.6); }
        }

        /* Floating Animation */
        .animate-float {
            animation: float 3s ease-in-out infinite;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .animate-sway {
            animation: sway 4s ease-in-out infinite;
        }
        @keyframes sway {
            0%, 100% { transform: rotate(-3deg); }
            50% { transform: rotate(3deg); }
        }
    </style>
</head>
<body class="relative min-h-screen pb-20 select-none">

    <!-- Background Animated Canvas (Hearts & Blooming Lilies) -->
    <canvas id="bgCanvas"></canvas>

    <!-- Navigation Header -->
    <div class="fixed top-4 right-4 z-50 flex items-center gap-2 flex-wrap justify-end">
        <button id="musicCustomizerBtn" onclick="toggleMusicModal()" class="glass-card px-3.5 py-2 rounded-full flex items-center gap-2 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
            <i class="fa-solid fa-sliders text-cyan-300"></i>
            <span>Custom Music</span>
        </button>

        <button id="quizManagerBtn" onclick="toggleQuizModal()" class="glass-card px-3.5 py-2 rounded-full flex items-center gap-2 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
            <i class="fa-solid fa-clipboard-question text-pink-300"></i>
            <span>Edit Quiz</span>
        </button>

        <button id="photoManagerBtn" onclick="togglePhotoModal()" class="glass-card px-3.5 py-2 rounded-full flex items-center gap-2 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
            <i class="fa-solid fa-images text-amber-300"></i>
            <span>Photos</span>
        </button>

        <button id="musicToggle" class="glass-card px-3.5 py-2 rounded-full flex items-center gap-2 text-xs font-medium border border-rose-300/30 text-rose-200 hover:bg-rose-900/40 transition active:scale-95 shadow-lg">
            <i id="musicIcon" class="fa-solid fa-music text-rose-400"></i>
            <span id="musicText">Music</span>
        </button>
    </div>

    <!-- MAIN CONTAINER -->
    <div class="relative z-10 max-w-4xl mx-auto px-4 pt-10 sm:pt-16 space-y-20">

        <!-- HERO SECTION -->
        <section class="text-center space-y-6 pt-6">
            <div class="inline-block px-4 py-1.5 rounded-full glass-card text-rose-300 text-xs sm:text-sm font-medium tracking-widest uppercase mb-2 animate-bounce">
                ✨ Today Is All About You ✨
            </div>
            
            <h1 class="text-4xl sm:text-6xl md:text-7xl font-bold font-serif-custom leading-tight tracking-wide text-transparent bg-clip-text bg-gradient-to-r from-rose-200 via-pink-300 to-amber-200 drop-shadow-sm">
                Happy Birthday, <br class="sm:hidden"/>
                <span id="girlfriendName" class="font-cursive text-5xl sm:text-7xl md:text-8xl text-rose-400 block mt-2 animate-float">My Favorite person Ning Ning❤️</span>
            </h1>

            <p class="max-w-xl mx-auto text-rose-100/80 text-sm sm:text-base font-light px-4 leading-relaxed">
                I created this little space wrapped in your favorite blooming lilies, just to remind you how deeply loved, valued, and cherished you are every single day.
            </p>

            <div class="pt-4">
                <a href="#cake-section" class="glow-pulse inline-flex items-center gap-3 bg-gradient-to-r from-rose-500 to-pink-600 hover:from-rose-600 hover:to-pink-700 text-white font-semibold px-8 py-4 rounded-full shadow-xl transform transition hover:-translate-y-1 active:scale-95">
                    <span>Blow Out Candles</span>
                    <i class="fa-solid fa-cake-candles text-rose-200"></i>
                </a>
            </div>
        </section>

        <!-- INTERACTIVE LILIES CAKE SECTION WITH MIC BLOWOUT -->
        <section id="cake-section" class="scroll-mt-10">
            <div class="glass-card rounded-3xl p-6 sm:p-10 text-center relative overflow-hidden">
                <div class="absolute -top-24 -left-24 w-48 h-48 bg-rose-500/20 rounded-full blur-3xl pointer-events-none"></div>
                
                <h2 class="text-2xl sm:text-3xl font-serif-custom font-bold text-rose-200 mb-2">Make A Wish</h2>
                <p id="cakeInstructions" class="text-xs sm:text-sm text-rose-200/70 mb-4">
                    Blow into your microphone ("fuuu") or tap the blooming lily cake below! 🌸
                </p>

                <!-- Mic Control Button -->
                <div class="mb-6">
                    <button id="micBtn" onclick="initMicBlowout()" class="glass-card px-4 py-2 rounded-full text-xs font-semibold text-rose-200 hover:bg-rose-900/50 border border-rose-400/30 transition flex items-center gap-2 mx-auto">
                        <i class="fa-solid fa-microphone text-rose-400"></i>
                        <span id="micBtnText">Enable Mic Blow Detection</span>
                    </button>
                    <p id="micStatus" class="text-[11px] text-pink-300/70 mt-1 hidden"></p>
                </div>

                <!-- Custom 3D Lilies Birthday Cake -->
                <div class="py-8">
                    <div id="cake" class="cake-container">
                        <!-- Candles -->
                        <div class="candle candle-1">
                            <div class="flame"></div>
                        </div>
                        <div class="candle candle-2">
                            <div class="flame"></div>
                        </div>
                        <div class="candle candle-3">
                            <div class="flame"></div>
                        </div>

                        <!-- Top Tier: Cream White & Lily Blossoms -->
                        <div class="cake-tier cake-top">
                            <div class="icing"></div>
                            <div class="vine-decor"></div>
                            <!-- SVG Lily Blossom Emblem -->
                            <div class="cake-lily-decor">
                                <svg viewBox="0 0 100 100" class="w-full h-full drop-shadow">
                                    <g transform="translate(50,50) scale(0.45)">
                                        <path d="M0 -40 Q 20 -20 0 0 Q -20 -20 0 -40" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                                        <path d="M0 40 Q 20 20 0 0 Q -20 20 0 40" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                                        <path d="M-40 0 Q -20 20 0 0 Q -20 -20 -40 0" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                                        <path d="M40 0 Q 20 20 0 0 Q 20 -20 40 0" fill="#ffffff" stroke="#f472b6" stroke-width="2"/>
                                        <circle cx="0" cy="0" r="6" fill="#fde047"/>
                                    </g>
                                </svg>
                            </div>
                        </div>

                        <!-- Bottom Tier: Pink Gradient with Floral Vines -->
                        <div class="cake-tier cake-bottom">
                            <div class="icing"></div>
                            <div class="vine-decor"></div>
                            <!-- Decorative Side Lilies -->
                            <div class="absolute bottom-2 left-4 w-8 h-8 opacity-90">
                                <svg viewBox="0 0 100 100"><circle cx="50" cy="50" r="35" fill="#fbcfe8"/><circle cx="50" cy="50" r="15" fill="#ffffff"/></svg>
                            </div>
                            <div class="absolute bottom-2 right-4 w-8 h-8 opacity-90">
                                <svg viewBox="0 0 100 100"><circle cx="50" cy="50" r="35" fill="#fbcfe8"/><circle cx="50" cy="50" r="15" fill="#ffffff"/></svg>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Wish Revealed Message -->
                <div id="wishMessage" class="hidden mt-6 p-6 rounded-2xl bg-rose-950/50 border border-rose-500/30 transition-all duration-700 transform translate-y-4">
                    <i class="fa-solid fa-wand-magic-sparkles text-3xl text-amber-300 mb-3 block animate-bounce"></i>
                    <p class="text-lg sm:text-2xl font-serif-custom italic text-rose-200 mb-2">
                        "Make a wish, my love... mine already came true because I have you."
                    </p>
                    <p class="text-xs sm:text-sm text-pink-300/80">
                        May every single dream you hold in your heart bloom as gracefully as a garden of lilies! ❤️
                    </p>
                </div>
            </div>
        </section>

        <!-- CUSTOMIZABLE QUIZ SECTION -->
        <section class="space-y-6">
            <div class="text-center space-y-2">
                <h2 class="text-3xl sm:text-4xl font-serif-custom font-bold text-rose-200">How Well Do You Know Us?</h2>
                <p class="text-xs sm:text-sm text-rose-200/60">A quick fun quiz just for you!</p>
            </div>

            <div class="glass-card max-w-xl mx-auto rounded-3xl p-6 sm:p-8 border border-rose-300/30 text-center relative">
                <div id="quizContainer">
                    <div class="flex items-center justify-between text-xs text-rose-300/70 mb-4 pb-2 border-b border-rose-200/10">
                        <span id="quizProgress">Question 1 of 3</span>
                        <span id="quizScore">Score: 0</span>
                    </div>

                    <h3 id="quizQuestion" class="text-lg sm:text-xl font-serif-custom text-rose-100 font-semibold mb-6">
                        Loading question...
                    </h3>

                    <div id="quizOptions" class="grid grid-cols-1 gap-3">
                        <!-- Populated dynamically -->
                    </div>

                    <div id="quizFeedback" class="mt-4 p-3 rounded-xl text-xs font-medium hidden"></div>
                </div>

                <div id="quizResult" class="hidden space-y-4 py-4">
                    <i class="fa-solid fa-trophy text-4xl text-amber-300 animate-bounce block"></i>
                    <h3 class="text-2xl font-serif-custom text-rose-200 font-bold">Quiz Complete!</h3>
                    <p id="quizResultMessage" class="text-sm text-rose-100/90"></p>
                    <button onclick="restartQuiz()" class="bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold text-xs px-6 py-2.5 rounded-full shadow-lg hover:from-rose-600 hover:to-pink-700 transition">
                        Try Again
                    </button>
                </div>
            </div>
        </section>

        <!-- PHOTO GALLERY SECTION -->
        <section class="space-y-8">
            <div class="text-center space-y-2">
                <h2 class="text-3xl sm:text-4xl font-serif-custom font-bold text-rose-200"> Happiest birthday to you once again</h2>
                <p class="text-xs sm:text-sm text-rose-200/60">Tap "Photos" at top right to upload your own pictures!</p>
            </div>

            <div id="photoGrid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6 pt-4">
                <!-- Initialized dynamically -->
            </div>
        </section>

        <!-- REASONS WHY YOU ARE SPECIAL SECTION -->
        <section class="space-y-8">
            <div class="text-center space-y-2">
                <h2 class="text-3xl sm:text-4xl font-serif-custom font-bold text-rose-200">Why You Are So Special</h2>
                <p class="text-xs sm:text-sm text-rose-200/60">Tap any card to flip and reveal a secret reason</p>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6">
                <!-- Card 1 -->
                <div class="flip-card cursor-pointer" onclick="flipCard(this)">
                    <div class="flip-card-inner">
                        <div class="flip-card-front glass-card border-rose-400/20 text-rose-200">
                            <div class="space-y-2">
                                <i class="fa-solid fa-heart text-2xl text-rose-400 animate-pulse"></i>
                                <h3 class="font-semibold text-base">Reason #1</h3>
                                <p class="text-xs text-rose-300/60">Tap to flip ✨</p>
                            </div>
                        </div>
                        <div class="flip-card-back bg-gradient-to-br from-rose-900/90 to-purple-900/90 border border-rose-400/40 text-rose-100">
                            <p class="text-xs sm:text-sm font-medium leading-relaxed">
                                "You are my instant peace. No matter how crazy the world gets, seeing your face settles everything."
                            </p>
                        </div>
                    </div>
                </div>

                <!-- Card 2 -->
                <div class="flip-card cursor-pointer" onclick="flipCard(this)">
                    <div class="flip-card-inner">
                        <div class="flip-card-front glass-card border-rose-400/20 text-rose-200">
                            <div class="space-y-2">
                                <i class="fa-solid fa-face-smile-beam text-2xl text-amber-300"></i>
                                <h3 class="font-semibold text-base">Reason #2</h3>
                                <p class="text-xs text-rose-300/60">Tap to flip ✨</p>
                            </div>
                        </div>
                        <div class="flip-card-back bg-gradient-to-br from-rose-900/90 to-purple-900/90 border border-rose-400/40 text-rose-100">
                            <p class="text-xs sm:text-sm font-medium leading-relaxed">
                                "Your laugh is my absolute favorite sound in the whole world. It brightens my worst days instantly."
                            </p>
                        </div>
                    </div>
                </div>

                <!-- Card 3 -->
                <div class="flip-card cursor-pointer" onclick="flipCard(this)">
                    <div class="flip-card-inner">
                        <div class="flip-card-front glass-card border-rose-400/20 text-rose-200">
                            <div class="space-y-2">
                                <i class="fa-solid fa-house-chimney-heart text-2xl text-pink-400"></i>
                                <h3 class="font-semibold text-base">Reason #3</h3>
                                <p class="text-xs text-rose-300/60">Tap to flip ✨</p>
                            </div>
                        </div>
                        <div class="flip-card-back bg-gradient-to-br from-rose-900/90 to-purple-900/90 border border-rose-400/40 text-rose-100">
                            <p class="text-xs sm:text-sm font-medium leading-relaxed">
                                "Home used to be a physical place for me—until I met you. Now, home is wherever you are."
                            </p>
                        </div>
                    </div>
                </div>

                <!-- Card 4 -->
                <div class="flip-card cursor-pointer" onclick="flipCard(this)">
                    <div class="flip-card-inner">
                        <div class="flip-card-front glass-card border-rose-400/20 text-rose-200">
                            <div class="space-y-2">
                                <i class="fa-solid fa-sparkles text-2xl text-amber-200"></i>
                                <h3 class="font-semibold text-base">Reason #4</h3>
                                <p class="text-xs text-rose-300/60">Tap to flip ✨</p>
                            </div>
                        </div>
                        <div class="flip-card-back bg-gradient-to-br from-rose-900/90 to-purple-900/90 border border-rose-400/40 text-rose-100">
                            <p class="text-xs sm:text-sm font-medium leading-relaxed">
                                "You notice the little things that everyone else misses. Your kindness and warmth are unmatched."
                            </p>
                        </div>
                    </div>
                </div>

                <!-- Card 5 -->
                <div class="flip-card cursor-pointer" onclick="flipCard(this)">
                    <div class="flip-card-inner">
                        <div class="flip-card-front glass-card border-rose-400/20 text-rose-200">
                            <div class="space-y-2">
                                <i class="fa-solid fa-gem text-2xl text-cyan-300"></i>
                                <h3 class="font-semibold text-base">Reason #5</h3>
                                <p class="text-xs text-rose-300/60">Tap to flip ✨</p>
                            </div>
                        </div>
                        <div class="flip-card-back bg-gradient-to-br from-rose-900/90 to-purple-900/90 border border-rose-400/40 text-rose-100">
                            <p class="text-xs sm:text-sm font-medium leading-relaxed">
                                "You make me want to be a better person every day just by being around your incredible light."
                            </p>
                        </div>
                    </div>
                </div>

                <!-- Card 6 -->
                <div class="flip-card cursor-pointer" onclick="flipCard(this)">
                    <div class="flip-card-inner">
                        <div class="flip-card-front glass-card border-rose-400/20 text-rose-200">
                            <div class="space-y-2">
                                <i class="fa-solid fa-infinity text-2xl text-rose-300"></i>
                                <h3 class="font-semibold text-base">Reason #6</h3>
                                <p class="text-xs text-rose-300/60">Tap to flip ✨</p>
                            </div>
                        </div>
                        <div class="flip-card-back bg-gradient-to-br from-rose-900/90 to-purple-900/90 border border-rose-400/40 text-rose-100">
                            <p class="text-xs sm:text-sm font-medium leading-relaxed">
                                "Simply because you are YOU. Out of everyone on this planet, my heart picked you, and it always will."
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECRET LETTER WITH BOUQUET OF LILIES SECTION -->
        <section class="space-y-6">
            <div class="text-center space-y-2">
                <h2 class="text-3xl sm:text-4xl font-serif-custom font-bold text-rose-200">A Secret Letter For You</h2>
                <p class="text-xs sm:text-sm text-rose-200/60">Tap the bouquet of lilies on the letter to unseal</p>
            </div>

            <div class="max-w-2xl mx-auto">
                <div id="envelope" class="envelope-wrapper glass-card p-6 sm:p-10 rounded-3xl border border-rose-300/40 text-center relative overflow-hidden cursor-pointer hover:border-rose-200/80 transition duration-500 shadow-2xl" onclick="toggleLetter()">
                    
                    <!-- Sealed Envelope State with Detailed SVG Lily Bouquet -->
                    <div id="envelopeClosed" class="space-y-5 py-6">
                        <!-- Bouquet Container -->
                        <div class="relative w-32 h-32 mx-auto flex items-center justify-center transform transition duration-500 hover:scale-110 animate-sway">
                            <!-- Soft Radial Glow Background -->
                            <div class="absolute inset-0 bg-gradient-to-tr from-pink-500/30 to-amber-200/30 rounded-full blur-xl"></div>
                            
                            <!-- Detailed SVG Lily Bouquet -->
                            <svg class="w-full h-full drop-shadow-lg" viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <!-- Ribbon / Stem Wrap -->
                                <path d="M90 145 C 80 165, 75 180, 70 190 M100 145 C 100 168, 102 182, 105 192 M110 145 C 120 165, 125 180, 130 190" stroke="#4a7c59" stroke-width="4" stroke-linecap="round"/>
                                <path d="M82 150 Q100 160 118 150 Q100 142 82 150" fill="#f43f5e"/>
                                <path d="M85 152 Q100 170 115 152" fill="#be185d"/>
                                
                                <!-- Stems & Leaves -->
                                <path d="M85 110 Q 60 125 45 120" stroke="#5c946e" stroke-width="3.5" stroke-linecap="round"/>
                                <path d="M115 110 Q 140 125 155 120" stroke="#5c946e" stroke-width="3.5" stroke-linecap="round"/>
                                
                                <!-- LILY 1: LEFT -->
                                <g transform="translate(50, 70) scale(0.65)">
                                    <path d="M50 80 Q 20 40 10 10 Q 40 30 50 80" fill="url(#lilyGrad)" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <path d="M50 80 Q 80 40 90 10 Q 60 30 50 80" fill="url(#lilyGrad)" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <path d="M50 80 Q 50 20 50 0 Q 50 30 50 80" fill="#fff" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <!-- Stamens -->
                                    <path d="M50 60 Q 40 35 35 25 M50 60 Q 50 30 50 20 M50 60 Q 60 35 65 25" stroke="#fde047" stroke-width="2"/>
                                    <circle cx="35" cy="25" r="3" fill="#f59e0b"/>
                                    <circle cx="50" cy="20" r="3" fill="#f59e0b"/>
                                    <circle cx="65" cy="25" r="3" fill="#f59e0b"/>
                                </g>

                                <!-- LILY 2: RIGHT -->
                                <g transform="translate(85, 70) scale(0.65)">
                                    <path d="M50 80 Q 20 40 10 10 Q 40 30 50 80" fill="url(#lilyGrad)" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <path d="M50 80 Q 80 40 90 10 Q 60 30 50 80" fill="url(#lilyGrad)" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <path d="M50 80 Q 50 20 50 0 Q 50 30 50 80" fill="#fff" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <!-- Stamens -->
                                    <path d="M50 60 Q 40 35 35 25 M50 60 Q 50 30 50 20 M50 60 Q 60 35 65 25" stroke="#fde047" stroke-width="2"/>
                                    <circle cx="35" cy="25" r="3" fill="#f59e0b"/>
                                    <circle cx="50" cy="20" r="3" fill="#f59e0b"/>
                                    <circle cx="65" cy="25" r="3" fill="#f59e0b"/>
                                </g>

                                <!-- LILY 3: CENTER TOP (MAIN BLOOM) -->
                                <g transform="translate(50, 25) scale(0.9)">
                                    <!-- Back Petals -->
                                    <path d="M50 90 Q 15 50 0 10 Q 35 35 50 90" fill="url(#lilyGrad)" stroke="#f472b6" stroke-width="1.5"/>
                                    <path d="M50 90 Q 85 50 100 10 Q 65 35 50 90" fill="url(#lilyGrad)" stroke="#f472b6" stroke-width="1.5"/>
                                    <path d="M50 90 Q 50 30 50 -10 Q 50 30 50 90" fill="url(#lilyGrad)" stroke="#f472b6" stroke-width="1.5"/>
                                    <!-- Front Petals -->
                                    <path d="M50 90 Q 25 70 10 40 Q 40 55 50 90" fill="#ffffff" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <path d="M50 90 Q 75 70 90 40 Q 60 55 50 90" fill="#ffffff" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <path d="M50 90 Q 50 65 50 30 Q 50 65 50 90" fill="#fff" stroke="#fbcfe8" stroke-width="1.5"/>
                                    <!-- Stamens & Anthers -->
                                    <path d="M50 75 Q 35 45 28 30 M50 75 Q 45 40 42 22 M50 75 Q 55 40 58 22 M50 75 Q 65 45 72 30" stroke="#fde047" stroke-width="2.5" stroke-linecap="round"/>
                                    <circle cx="28" cy="30" r="3.5" fill="#d97706"/>
                                    <circle cx="42" cy="22" r="3.5" fill="#d97706"/>
                                    <circle cx="58" cy="22" r="3.5" fill="#d97706"/>
                                    <circle cx="72" cy="30" r="3.5" fill="#d97706"/>
                                </g>

                                <!-- Gradients Definition -->
                                <defs>
                                    <linearGradient id="lilyGrad" x1="0%" y1="100%" x2="0%" y2="0%">
                                        <stop offset="0%" stop-color="#f472b6" />
                                        <stop offset="50%" stop-color="#fbcfe8" />
                                        <stop offset="100%" stop-color="#ffffff" />
                                    </linearGradient>
                                </defs>
                            </svg>
                        </div>

                        <p class="font-cursive text-2xl text-rose-200">"A bouquet of lilies for my favorite person..."</p>
                        <span class="inline-block text-xs text-pink-300/80 bg-rose-950/70 px-4 py-1.5 rounded-full border border-rose-400/30 shadow-md">
                            Tap to unseal letter
                        </span>
                    </div>

                    <!-- Unfolded Letter Content -->
                    <div id="letterContent" class="letter-content text-left space-y-4">
                        <!-- Top Decorative Floral Header -->
                        <div class="border-b border-rose-300/20 pb-4 text-center relative">
                            <div class="text-xs text-amber-200/70 tracking-widest uppercase font-light mb-1">❀ Wrapped in Lilies & Love ❀</div>
                            <span class="font-cursive text-3xl sm:text-4xl text-rose-300">My Dearest Ning Ning,</span>
                        </div>

                        <p class="text-sm sm:text-base leading-relaxed text-rose-100/90 font-light">
                            I want you to know why this day matters so much to me—not just because it’s your birthday, but because today is the reason my world is so much brighter. Like a bouquet of white lilies bringing light, purity, and beauty into a room, your presence gently transformed my entire life the moment you walked into it.
                        </p>

                        <p class="text-sm sm:text-base leading-relaxed text-rose-100/90 font-light">
                            Before you came along, ordinary days were just dates on a calendar. But today marks the day the universe gave me the person who became my peace, my favorite smile, and my absolute favorite part of every single day.
                        </p>

                        <p class="text-sm sm:text-base leading-relaxed text-rose-100/90 font-light">
                            Celebrating today isn't just about the gifts or the candles; it’s about honoring everything you are and every beautiful memory we've bloomed together. Every laugh we’ve shared, every quiet moment where just holding your hand was enough, and every little habit of yours that makes me fall for you a little more—it all started today.
                        </p>

                        <p class="text-sm sm:text-base leading-relaxed text-rose-100/90 font-light">
                            Today gave me <em>you</em>, and for that, it will forever be the most special day of my year.
                        </p>

                        <!-- Bottom Signature with Lily Emblem -->
                        <div class="pt-6 text-right border-t border-rose-300/20 flex items-center justify-between">
                            <div class="text-rose-300/40 text-lg">🌸 🪷 🌸</div>
                            <div>
                                <p class="font-cursive text-2xl text-amber-200">Forever & Always,</p>
                                <p class="text-xs text-rose-300/70 mt-1">Yours Truly ❤️</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- FOOTER -->
        <footer class="text-center pt-10 pb-6 border-t border-rose-900/30 text-rose-300/60 text-xs sm:text-sm space-y-2">
            <p class="font-cursive text-xl text-rose-300">Made with all my heart, surrounded by lilies just for you ✨</p>
            <p>© Happy Birthday, My Love!</p>
        </footer>
    </div>

    <!-- MUSIC CUSTOMIZER MODAL -->
    <div id="musicModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-6">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-sliders text-cyan-300"></i>
                    <span>Customize Background Music</span>
                </h3>
                <button onclick="toggleMusicModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-2">Preset Melodies</label>
                    <select id="musicPresetSelect" onchange="loadPresetMusic()" class="w-full bg-rose-950/70 border border-rose-300/30 rounded-xl px-4 py-2.5 text-xs text-rose-100 focus:outline-none focus:border-rose-400">
                        <option value="romantic">Soft Romance (Default)</option>
                        <option value="birthday">Happy Birthday Melody</option>
                        <option value="lullaby">Sweet Dream Lullaby</option>
                        <option value="custom">Custom Frequencies</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Custom Note Frequencies (Hz)</label>
                    <p class="text-[10px] text-rose-200/60 mb-2">Comma separated values (e.g. 261.63, 293.66, 329.63, 349.23, 392.00)</p>
                    <input type="text" id="customNotesInput" placeholder="261.63, 329.63, 392.00, 523.25" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-4 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400">
                </div>

                <div class="grid grid-cols-2 gap-4 pt-2">
                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Tempo (Speed)</label>
                        <input type="range" id="musicSpeed" min="400" max="2000" step="100" value="1200" onchange="updateMusicSettings()" class="w-full accent-pink-500 cursor-pointer">
                        <span id="speedValue" class="text-[10px] text-pink-300 block text-right mt-1">1.2s per note</span>
                    </div>

                    <div>
                        <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300 mb-1">Volume</label>
                        <input type="range" id="musicVolume" min="0.01" max="0.25" step="0.01" value="0.08" onchange="updateMusicSettings()" class="w-full accent-pink-500 cursor-pointer">
                        <span id="volumeValue" class="text-[10px] text-pink-300 block text-right mt-1">Medium</span>
                    </div>
                </div>

                <button onclick="saveMusicCustomization()" class="w-full bg-gradient-to-r from-pink-500 to-rose-600 text-white font-semibold py-2.5 rounded-xl text-xs hover:from-pink-600 hover:to-rose-700 transition shadow-lg mt-2">
                    Save & Play Music
                </button>
            </div>

            <button onclick="toggleMusicModal()" class="w-full bg-rose-950/80 border border-rose-400/30 text-rose-200 font-medium py-2.5 rounded-xl text-xs hover:bg-rose-900/60 transition">
                Close
            </button>
        </div>
    </div>

    <!-- PHOTO MANAGEMENT MODAL -->
    <div id="photoModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-6">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-images text-rose-400"></i>
                    <span>Customize Photos</span>
                </h3>
                <button onclick="togglePhotoModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-4">
                <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300">Add New Photo</label>
                
                <div class="flex flex-col gap-3">
                    <input type="file" id="imageInput" accept="image/*" class="block w-full text-xs text-rose-300 file:mr-4 file:py-2.5 file:px-4 file:rounded-full file:border-0 file:text-xs file:font-semibold file:bg-rose-500 file:text-white hover:file:bg-rose-600 transition cursor-pointer">
                    
                    <input type="text" id="captionInput" placeholder="Enter romantic caption (e.g., Our First Trip)" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-4 py-2.5 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400">
                    
                    <button onclick="addPhotoFromUpload()" class="w-full bg-gradient-to-r from-rose-500 to-pink-600 text-white font-semibold py-2.5 rounded-xl text-xs hover:from-rose-600 hover:to-pink-700 transition">
                        Upload & Add Photo
                    </button>
                </div>
            </div>

            <div class="space-y-3 pt-2">
                <div class="flex items-center justify-between">
                    <label class="text-xs font-semibold uppercase tracking-wider text-rose-300">Manage Current Photos</label>
                    <button onclick="resetDefaultPhotos()" class="text-[10px] text-amber-300 hover:underline">Reset Defaults</button>
                </div>
                
                <div id="modalPhotoList" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                    <!-- Populated via JavaScript -->
                </div>
            </div>

            <button onclick="togglePhotoModal()" class="w-full bg-rose-950/80 border border-rose-400/30 text-rose-200 font-medium py-2.5 rounded-xl text-xs hover:bg-rose-900/60 transition">
                Close & Save Changes
            </button>
        </div>
    </div>

    <!-- QUIZ EDITING MODAL -->
    <div id="quizModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden">
        <div class="glass-card w-full max-w-lg p-6 rounded-3xl border border-rose-300/30 max-h-[90vh] overflow-y-auto text-rose-100 space-y-6">
            <div class="flex items-center justify-between border-b border-rose-200/20 pb-4">
                <h3 class="text-xl font-serif-custom font-bold text-rose-200 flex items-center gap-2">
                    <i class="fa-solid fa-pen-to-square text-pink-300"></i>
                    <span>Customize Quiz</span>
                </h3>
                <button onclick="toggleQuizModal()" class="text-rose-300 hover:text-white text-xl">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-3">
                <label class="block text-xs font-semibold uppercase tracking-wider text-rose-300">Add New Question</label>
                
                <input type="text" id="newQuestionText" placeholder="Enter Question (e.g., Where was our 1st date?)" class="w-full bg-rose-950/50 border border-rose-300/30 rounded-xl px-4 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none focus:border-rose-400">
                
                <div class="grid grid-cols-2 gap-2">
                    <input type="text" id="opt0" placeholder="Option A (Correct Answer)" class="bg-rose-950/50 border border-emerald-400/50 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    <input type="text" id="opt1" placeholder="Option B" class="bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    <input type="text" id="opt2" placeholder="Option C" class="bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                    <input type="text" id="opt3" placeholder="Option D" class="bg-rose-950/50 border border-rose-300/30 rounded-xl px-3 py-2 text-xs text-rose-100 placeholder-rose-300/40 focus:outline-none">
                </div>

                <button onclick="addNewQuizQuestion()" class="w-full bg-gradient-to-r from-pink-500 to-rose-600 text-white font-semibold py-2 rounded-xl text-xs hover:from-pink-600 hover:to-rose-700 transition">
                    Add Question
                </button>
            </div>

            <div class="space-y-3 pt-2">
                <div class="flex items-center justify-between">
                    <label class="text-xs font-semibold uppercase tracking-wider text-rose-300">Existing Questions</label>
                    <button onclick="resetDefaultQuiz()" class="text-[10px] text-amber-300 hover:underline">Reset Defaults</button>
                </div>
                
                <div id="modalQuizList" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                    <!-- Populated via JavaScript -->
                </div>
            </div>

            <button onclick="toggleQuizModal()" class="w-full bg-rose-950/80 border border-rose-400/30 text-rose-200 font-medium py-2.5 rounded-xl text-xs hover:bg-rose-900/60 transition">
                Done & Save Quiz
            </button>
        </div>
    </div>

    <script>
        /* ----------------------------------------------------
           1. PHOTO STORAGE & MANAGEMENT (LocalStorage)
        ---------------------------------------------------- */
        const DEFAULT_PHOTOS = [
            {
                url: 'https://images.unsplash.com/photo-1518199266791-5375a83190b7?auto=format&fit=crop&w=600&q=80',
                caption: 'Our Favorite Memories'
            },
            {
                url: 'https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&fit=crop&w=600&q=80',
                caption: 'Quiet Sunset Moments'
            },
            {
                url: 'https://images.unsplash.com/photo-1516589178581-6cd7833ae3b2?auto=format&fit=crop&w=600&q=80',
                caption: 'To Infinite Adventures'
            }
        ];

        function getStoredPhotos() {
            try {
                const saved = localStorage.getItem('birthday_photos');
                return saved ? JSON.parse(saved) : DEFAULT_PHOTOS;
            } catch (e) {
                return DEFAULT_PHOTOS;
            }
        }

        function savePhotos(photos) {
            try {
                localStorage.setItem('birthday_photos', JSON.stringify(photos));
            } catch (e) {
                console.warn('Storage quota exceeded');
            }
            renderPhotoGallery();
            renderModalPhotoList();
        }

        function renderPhotoGallery() {
            const photos = getStoredPhotos();
            const grid = document.getElementById('photoGrid');
            grid.innerHTML = '';

            photos.forEach((photo, idx) => {
                const rotations = ['-rotate-2', 'rotate-2', '-rotate-1', 'rotate-3', '-rotate-3'];
                const rotClass = rotations[idx % rotations.length];

                const card = document.createElement('div');
                card.className = `bg-amber-50/10 p-4 rounded-xl glass-card border border-rose-200/20 transform ${rotClass} hover:rotate-0 transition duration-300 hover:scale-105 shadow-xl flex flex-col justify-between`;
                
                card.innerHTML = `
                    <div class="aspect-square rounded-lg overflow-hidden border border-rose-300/20 relative group bg-rose-950/40">
                        <img src="${photo.url}" alt="${photo.caption}" class="w-full h-full object-cover group-hover:scale-110 transition duration-500" onerror="this.src='https://placehold.co/400x400/2a0826/fce7f3?text=Memory+Photo'">
                    </div>
                    <div class="pt-3 text-center">
                        <p class="font-cursive text-xl text-rose-200 truncate px-1">${photo.caption}</p>
                        <p class="text-[10px] text-rose-300/50 uppercase tracking-widest mt-1">Memory #${idx + 1}</p>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function renderModalPhotoList() {
            const photos = getStoredPhotos();
            const list = document.getElementById('modalPhotoList');
            list.innerHTML = '';

            photos.forEach((photo, idx) => {
                const item = document.createElement('div');
                item.className = 'flex items-center justify-between bg-rose-950/40 p-2 rounded-xl border border-rose-300/20';
                item.innerHTML = `
                    <div class="flex items-center gap-3 overflow-hidden pr-2">
                        <img src="${photo.url}" class="w-10 h-10 object-cover rounded-lg flex-shrink-0" onerror="this.src='https://placehold.co/100x100/2a0826/fce7f3?text=Photo'">
                        <span class="text-xs text-rose-200 truncate">${photo.caption}</span>
                    </div>
                    <button onclick="deletePhoto(${idx})" class="text-rose-400 hover:text-rose-200 text-sm px-2 flex-shrink-0">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                `;
                list.appendChild(item);
            });
        }

        function addPhotoFromUpload() {
            const fileInput = document.getElementById('imageInput');
            const captionInput = document.getElementById('captionInput');
            const file = fileInput.files[0];
            const caption = captionInput.value.trim() || 'Beautiful Memory';

            if (!file) {
                alert('Please select an image file first!');
                return;
            }

            const reader = new FileReader();
            reader.onload = function(e) {
                const photos = getStoredPhotos();
                photos.push({
                    url: e.target.result,
                    caption: caption
                });
                savePhotos(photos);
                
                fileInput.value = '';
                captionInput.value = '';
            };
            reader.readAsDataURL(file);
        }

        function deletePhoto(index) {
            const photos = getStoredPhotos();
            photos.splice(index, 1);
            savePhotos(photos);
        }

        function resetDefaultPhotos() {
            savePhotos(DEFAULT_PHOTOS);
        }

        function togglePhotoModal() {
            const modal = document.getElementById('photoModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                renderModalPhotoList();
            }
        }

        /* ----------------------------------------------------
           2. CUSTOMIZABLE QUIZ SYSTEM & STORAGE
        ---------------------------------------------------- */
        const DEFAULT_QUIZ = [
            {
                question: "What is my absolute favorite thing about you?",
                options: ["Your beautiful smile", "Your kind heart", "Your spirit🐦‍🔥", "All of the above! ❤️"],
                correctIndex: 3
            },
            {
                question: "Where is my favorite place in the world?",
                options: ["Paris", "The Beach", "Right next to you", "In a cozy café"],
                correctIndex: 2
            },
            {
                question: "Who loves you more than anything in this universe?",
                options: ["Me!", "Definitely me!", "100% me!", "All options are correct ❤️"],
                correctIndex: 3
            }
        ];

        let currentQuizIndex = 0;
        let quizScore = 0;

        function getStoredQuiz() {
            try {
                const saved = localStorage.getItem('birthday_quiz');
                return saved ? JSON.parse(saved) : DEFAULT_QUIZ;
            } catch (e) {
                return DEFAULT_QUIZ;
            }
        }

        function saveQuiz(questions) {
            try {
                localStorage.setItem('birthday_quiz', JSON.stringify(questions));
            } catch (e) {
                console.warn('Storage error for quiz');
            }
            restartQuiz();
            renderModalQuizList();
        }

        function renderCurrentQuestion() {
            const questions = getStoredQuiz();
            const qContainer = document.getElementById('quizContainer');
            const rContainer = document.getElementById('quizResult');

            if (questions.length === 0) {
                document.getElementById('quizQuestion').textContent = "No questions added yet!";
                document.getElementById('quizOptions').innerHTML = '';
                return;
            }

            if (currentQuizIndex >= questions.length) {
                qContainer.classList.add('hidden');
                rContainer.classList.remove('hidden');
                document.getElementById('quizResultMessage').textContent = 
                    `You scored ${quizScore} out of ${questions.length}! You're absolute perfection! ❤️`;
                
                if (typeof confetti === 'function') {
                    confetti({ particleCount: 80, spread: 70, origin: { y: 0.6 } });
                }
                return;
            }

            qContainer.classList.remove('hidden');
            rContainer.classList.add('hidden');

            const current = questions[currentQuizIndex];
            document.getElementById('quizProgress').textContent = `Question ${currentQuizIndex + 1} of ${questions.length}`;
            document.getElementById('quizScore').textContent = `Score: ${quizScore}`;
            document.getElementById('quizQuestion').textContent = current.question;

            const optionsBox = document.getElementById('quizOptions');
            optionsBox.innerHTML = '';

            const feedback = document.getElementById('quizFeedback');
            feedback.classList.add('hidden');

            current.options.forEach((opt, idx) => {
                const btn = document.createElement('button');
                btn.className = 'w-full bg-rose-950/40 hover:bg-rose-900/60 border border-rose-300/20 text-rose-100 text-xs sm:text-sm py-3 px-4 rounded-xl transition text-left font-medium flex items-center justify-between group';
                btn.innerHTML = `
                    <span>${opt}</span>
                    <i class="fa-solid fa-heart text-rose-400/0 group-hover:text-rose-400 transition-all"></i>
                `;
                btn.onclick = () => handleAnswer(idx, current.correctIndex);
                optionsBox.appendChild(btn);
            });
        }

        function handleAnswer(selectedIndex, correctIndex) {
            const feedback = document.getElementById('quizFeedback');
            feedback.classList.remove('hidden');

            if (selectedIndex === correctIndex) {
                quizScore++;
                feedback.className = "mt-4 p-3 rounded-xl text-xs font-semibold bg-emerald-950/60 border border-emerald-500/40 text-emerald-200";
                feedback.innerHTML = '<i class="fa-solid fa-circle-check mr-1"></i> Correct! You know me so well ❤️';
                playCelebrationSound();
            } else {
                feedback.className = "mt-4 p-3 rounded-xl text-xs font-semibold bg-rose-950/60 border border-rose-500/40 text-rose-200";
                feedback.innerHTML = '<i class="fa-solid fa-circle-xmark mr-1"></i> Aww, close! But I love you anyway 💕';
            }

            const btns = document.querySelectorAll('#quizOptions button');
            btns.forEach(b => b.disabled = true);

            setTimeout(() => {
                currentQuizIndex++;
                renderCurrentQuestion();
            }, 1200);
        }

        function restartQuiz() {
            currentQuizIndex = 0;
            quizScore = 0;
            renderCurrentQuestion();
        }

        function toggleQuizModal() {
            const modal = document.getElementById('quizModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                renderModalQuizList();
            }
        }

        function renderModalQuizList() {
            const questions = getStoredQuiz();
            const list = document.getElementById('modalQuizList');
            list.innerHTML = '';

            questions.forEach((q, idx) => {
                const item = document.createElement('div');
                item.className = 'flex items-center justify-between bg-rose-950/40 p-2.5 rounded-xl border border-rose-300/20';
                item.innerHTML = `
                    <div class="overflow-hidden pr-2">
                        <p class="text-xs text-rose-200 font-medium truncate">${idx + 1}. ${q.question}</p>
                        <p class="text-[10px] text-pink-300/60 truncate">Ans: ${q.options[q.correctIndex]}</p>
                    </div>
                    <button onclick="deleteQuizQuestion(${idx})" class="text-rose-400 hover:text-rose-200 text-sm px-2 flex-shrink-0">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                `;
                list.appendChild(item);
            });
        }

        function addNewQuizQuestion() {
            const qText = document.getElementById('newQuestionText').value.trim();
            const o0 = document.getElementById('opt0').value.trim();
            const o1 = document.getElementById('opt1').value.trim();
            const o2 = document.getElementById('opt2').value.trim();
            const o3 = document.getElementById('opt3').value.trim();

            if (!qText || !o0 || !o1) {
                alert('Please provide a question and at least 2 option choices!');
                return;
            }

            const options = [o0, o1];
            if (o2) options.push(o2);
            if (o3) options.push(o3);

            const questions = getStoredQuiz();
            questions.push({
                question: qText,
                options: options,
                correctIndex: 0
            });

            saveQuiz(questions);

            document.getElementById('newQuestionText').value = '';
            document.getElementById('opt0').value = '';
            document.getElementById('opt1').value = '';
            document.getElementById('opt2').value = '';
            document.getElementById('opt3').value = '';
        }

        function deleteQuizQuestion(index) {
            const questions = getStoredQuiz();
            questions.splice(index, 1);
            saveQuiz(questions);
        }

        function resetDefaultQuiz() {
            saveQuiz(DEFAULT_QUIZ);
        }

        /* ----------------------------------------------------
           3. CANVAS FLOATING HEARTS & BLOOMING LILIES
        ---------------------------------------------------- */
        const canvas = document.getElementById('bgCanvas');
        const ctx = canvas.getContext('2d');
        let width = canvas.width = window.innerWidth;
        let height = canvas.height = window.innerHeight;

        window.addEventListener('resize', () => {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        });

        // Floating Hearts
        class HeartParticle {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * width;
                this.y = height + Math.random() * 100;
                this.size = Math.random() * 10 + 5;
                this.speedY = Math.random() * 1.2 + 0.4;
                this.speedX = Math.sin(Math.random() * Math.PI) * 0.6;
                this.opacity = Math.random() * 0.5 + 0.2;
                this.color = `hsla(${Math.random() * 30 + 330}, 80%, 75%, ${this.opacity})`;
            }
            update() {
                this.y -= this.speedY;
                this.x += this.speedX;
                if (this.y < -20) this.reset();
            }
            draw() {
                ctx.save();
                ctx.translate(this.x, this.y);
                ctx.fillStyle = this.color;
                ctx.beginPath();
                const topCurve = this.size * 0.3;
                ctx.moveTo(0, topCurve);
                ctx.bezierCurveTo(0, 0, -this.size / 2, 0, -this.size / 2, topCurve);
                ctx.bezierCurveTo(-this.size / 2, (this.size + topCurve) / 2, 0, this.size, 0, this.size);
                ctx.bezierCurveTo(0, this.size, this.size / 2, (this.size + topCurve) / 2, this.size / 2, topCurve);
                ctx.bezierCurveTo(this.size / 2, 0, 0, 0, 0, topCurve);
                ctx.closePath();
                ctx.fill();
                ctx.restore();
            }
        }

        // Floating Lily Petal / Blossom Particles
        class LilyParticle {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * width;
                this.y = height + Math.random() * 150;
                this.size = Math.random() * 14 + 10;
                this.speedY = Math.random() * 1.0 + 0.3;
                this.rotation = Math.random() * Math.PI * 2;
                this.rotSpeed = (Math.random() - 0.5) * 0.02;
                this.opacity = Math.random() * 0.4 + 0.2;
            }
            update() {
                this.y -= this.speedY;
                this.x += Math.sin(this.y * 0.01) * 0.8;
                this.rotation += this.rotSpeed;
                if (this.y < -30) this.reset();
            }
            draw() {
                ctx.save();
                ctx.translate(this.x, this.y);
                ctx.rotate(this.rotation);
                ctx.globalAlpha = this.opacity;

                // Draw a stylized 6-petal white/pink lily blossom
                for (let i = 0; i < 6; i++) {
                    ctx.rotate(Math.PI / 3);
                    const grad = ctx.createLinearGradient(0, 0, 0, -this.size);
                    grad.addColorStop(0, '#f472b6');
                    grad.addColorStop(0.4, '#fbcfe8');
                    grad.addColorStop(1, '#ffffff');

                    ctx.beginPath();
                    ctx.moveTo(0, 0);
                    ctx.quadraticCurveTo(-this.size * 0.3, -this.size * 0.6, 0, -this.size);
                    ctx.quadraticCurveTo(this.size * 0.3, -this.size * 0.6, 0, 0);
                    ctx.fillStyle = grad;
                    ctx.fill();
                }

                // Center yellow stamen ring
                ctx.beginPath();
                ctx.arc(0, 0, this.size * 0.15, 0, Math.PI * 2);
                ctx.fillStyle = '#fde047';
                ctx.fill();

                ctx.restore();
            }
        }

        const heartParticles = Array.from({ length: 25 }, () => new HeartParticle());
        const lilyParticles = Array.from({ length: 15 }, () => new LilyParticle());

        function animateParticles() {
            ctx.clearRect(0, 0, width, height);
            heartParticles.forEach(p => { p.update(); p.draw(); });
            lilyParticles.forEach(p => { p.update(); p.draw(); });
            requestAnimationFrame(animateParticles);
        }
        animateParticles();

        /* ----------------------------------------------------
           4. INTERACTIVE CAKE & MIC BLOWOUT LOGIC
        ---------------------------------------------------- */
        let candlesBlown = false;
        let micStream = null;

        document.getElementById('cake').addEventListener('click', blowCandles);

        function blowCandles() {
            if (candlesBlown) return;
            candlesBlown = true;

            const flames = document.querySelectorAll('.flame');
            flames.forEach(flame => {
                flame.classList.add('extinguished');
                const smoke = document.createElement('div');
                smoke.className = 'smoke';
                flame.parentElement.appendChild(smoke);
            });

            if (typeof confetti === 'function') {
                confetti({
                    particleCount: 120,
                    spread: 80,
                    origin: { y: 0.6 },
                    colors: ['#f43f5e', '#fb7185', '#fde047', '#a855f7', '#ffffff']
                });
            }

            document.getElementById('cakeInstructions').textContent = '✨ Your wish has been sent to the stars! ✨';
            const wishMsg = document.getElementById('wishMessage');
            wishMsg.classList.remove('hidden');
            
            playCelebrationSound();

            if (micStream) {
                micStream.getTracks().forEach(track => track.stop());
            }
        }

        async function initMicBlowout() {
            const status = document.getElementById('micStatus');
            const btnText = document.getElementById('micBtnText');

            try {
                micStream = await navigator.mediaDevices.getUserMedia({ audio: true, video: false });
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const analyser = audioContext.createAnalyser();
                const microphone = audioContext.createMediaStreamSource(micStream);
                
                analyser.fftSize = 256;
                microphone.connect(analyser);

                const bufferLength = analyser.frequencyBinCount;
                const dataArray = new Uint8Array(bufferLength);

                status.classList.remove('hidden');
                status.textContent = '🎙️ Mic Active! Blow hard into your microphone ("fuuu")...';
                btnText.textContent = 'Listening for blow...';

                function checkVolume() {
                    if (candlesBlown) return;

                    analyser.getByteFrequencyData(dataArray);
                    let sum = 0;
                    for (let i = 0; i < bufferLength; i++) {
                        sum += dataArray[i];
                    }
                    let average = sum / bufferLength;

                    if (average > 45) {
                        blowCandles();
                        status.textContent = '✨ Blow detected! Happy Birthday!';
                    } else {
                        requestAnimationFrame(checkVolume);
                    }
                }

                checkVolume();
            } catch (err) {
                status.classList.remove('hidden');
                status.textContent = '⚠️ Could not access mic. You can tap the cake directly!';
                console.warn('Microphone access denied or unsupported:', err);
            }
        }

        /* ----------------------------------------------------
           5. CARD FLIP INTERACTION
        ---------------------------------------------------- */
        function flipCard(cardElement) {
            cardElement.classList.toggle('flipped');
            if (typeof confetti === 'function' && cardElement.classList.contains('flipped')) {
                const rect = cardElement.getBoundingClientRect();
                confetti({
                    particleCount: 20,
                    spread: 50,
                    origin: {
                        x: (rect.left + rect.width / 2) / window.innerWidth,
                        y: (rect.top + rect.height / 2) / window.innerHeight
                    },
                    colors: ['#f472b6', '#fcd34d']
                });
            }
        }

        /* ----------------------------------------------------
           6. SECRET LETTER TOGGLE
        ---------------------------------------------------- */
        function toggleLetter() {
            const letter = document.getElementById('letterContent');
            const envelopeClosed = document.getElementById('envelopeClosed');
            
            letter.classList.toggle('open');
            
            if (letter.classList.contains('open')) {
                envelopeClosed.style.display = 'none';
                if (typeof confetti === 'function') {
                    confetti({
                        particleCount: 60,
                        spread: 70,
                        origin: { y: 0.7 },
                        colors: ['#ffffff', '#fbcfe8', '#f472b6', '#fde047']
                    });
                }
            }
        }

        /* ----------------------------------------------------
           7. WEB AUDIO SYNTHESIZER & CUSTOM MUSIC LOGIC
        ---------------------------------------------------- */
        let audioCtx = null;
        let isPlaying = false;
        let melodyInterval = null;

        const PRESET_MELODIES = {
            romantic: [261.63, 329.63, 392.00, 493.88, 523.25, 659.25],
            birthday: [261.63, 261.63, 293.66, 261.63, 349.23, 329.63, 261.63, 261.63, 293.66, 261.63, 392.00, 349.23],
            lullaby: [329.63, 329.63, 392.00, 329.63, 261.63, 293.66, 329.63, 293.66]
        };

        let currentMusicConfig = {
            notes: PRESET_MELODIES.romantic,
            speed: 1200,
            volume: 0.08
        };

        function getStoredMusicConfig() {
            try {
                const saved = localStorage.getItem('birthday_music');
                return saved ? JSON.parse(saved) : currentMusicConfig;
            } catch (e) {
                return currentMusicConfig;
            }
        }

        document.getElementById('musicToggle').addEventListener('click', toggleMusic);

        function initAudio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
        }

        function toggleMusic() {
            initAudio();

            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }

            const musicIcon = document.getElementById('musicIcon');
            const musicText = document.getElementById('musicText');

            if (!isPlaying) {
                isPlaying = true;
                musicText.textContent = 'Pause';
                musicIcon.classList.add('fa-spin');
                startCustomMelody();
            } else {
                isPlaying = false;
                musicText.textContent = 'Music';
                musicIcon.classList.remove('fa-spin');
                clearInterval(melodyInterval);
            }
        }

        function startCustomMelody() {
            clearInterval(melodyInterval);
            currentMusicConfig = getStoredMusicConfig();
            const notes = currentMusicConfig.notes.length ? currentMusicConfig.notes : PRESET_MELODIES.romantic;
            let noteIdx = 0;

            melodyInterval = setInterval(() => {
                if (!isPlaying) return;
                
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                
                osc.type = 'sine';
                osc.frequency.value = notes[noteIdx % notes.length];
                
                gain.gain.setValueAtTime(0, audioCtx.currentTime);
                gain.gain.linearRampToValueAtTime(currentMusicConfig.volume, audioCtx.currentTime + 0.8);
                gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + (currentMusicConfig.speed / 1000) * 1.5);

                osc.connect(gain);
                gain.connect(audioCtx.destination);

                osc.start();
                osc.stop(audioCtx.currentTime + (currentMusicConfig.speed / 1000) * 1.6);

                noteIdx = (noteIdx + 1) % notes.length;
            }, currentMusicConfig.speed);
        }

        function toggleMusicModal() {
            const modal = document.getElementById('musicModal');
            modal.classList.toggle('hidden');
            if (!modal.classList.contains('hidden')) {
                const config = getStoredMusicConfig();
                document.getElementById('musicSpeed').value = config.speed;
                document.getElementById('musicVolume').value = config.volume;
                document.getElementById('customNotesInput').value = config.notes.join(', ');
                updateMusicSettingsDisplay();
            }
        }

        function loadPresetMusic() {
            const select = document.getElementById('musicPresetSelect').value;
            const input = document.getElementById('customNotesInput');
            if (PRESET_MELODIES[select]) {
                input.value = PRESET_MELODIES[select].join(', ');
            }
        }

        function updateMusicSettingsDisplay() {
            const speed = document.getElementById('musicSpeed').value;
            const vol = document.getElementById('musicVolume').value;
            document.getElementById('speedValue').textContent = (speed / 1000).toFixed(1) + 's per note';
            document.getElementById('volumeValue').textContent = Math.round(vol * 1000) + '%';
        }

        function updateMusicSettings() {
            updateMusicSettingsDisplay();
        }

        function saveMusicCustomization() {
            const notesStr = document.getElementById('customNotesInput').value;
            const notesArr = notesStr.split(',').map(n => parseFloat(n.trim())).filter(n => !isNaN(n) && n > 0);
            
            const speed = parseInt(document.getElementById('musicSpeed').value);
            const volume = parseFloat(document.getElementById('musicVolume').value);

            const newConfig = {
                notes: notesArr.length > 0 ? notesArr : PRESET_MELODIES.romantic,
                speed: speed,
                volume: volume
            };

            try {
                localStorage.setItem('birthday_music', JSON.stringify(newConfig));
            } catch (e) {
                console.warn('Could not save music config');
            }

            toggleMusicModal();

            if (isPlaying) {
                startCustomMelody();
            } else {
                toggleMusic();
            }
        }

        function playCelebrationSound() {
            initAudio();
            if (audioCtx.state === 'suspended') audioCtx.resume();

            const freqs = [523.25, 659.25, 783.99, 1046.50];
            freqs.forEach((f, index) => {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();

                osc.type = 'triangle';
                osc.frequency.value = f;

                const startTime = audioCtx.currentTime + (index * 0.12);
                gain.gain.setValueAtTime(0.15, startTime);
                gain.gain.exponentialRampToValueAtTime(0.001, startTime + 0.6);

                osc.connect(gain);
                gain.connect(audioCtx.destination);

                osc.start(startTime);
                osc.stop(startTime + 0.6);
            });
        }

        window.addEventListener('DOMContentLoaded', () => {
            renderPhotoGallery();
            renderCurrentQuestion();
        });
    </script>
</body>
</html>
