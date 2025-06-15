<!DOCTYPE html>
<html lang="lo">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ເກມທາຍຕົວເລກລາວ - ສະບັບປັບປຸງ</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Lao:wght@400;700&display=swap');
        
        :root {
            --primary: #8b5cf6;
            --secondary: #ec4899;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
        }
        
        body {
            font-family: 'Noto Sans Lao', sans-serif;
            background: linear-gradient(135deg, #4f46e5, #7c3aed, #c026d3);
            min-height: 100vh;
            overflow-x: hidden;
            display: flex; /* ເພີ່ມ display flex ເພື່ອຈັດກึ่งກາງເນື້ອຫາ */
            flex-direction: column; /* ຈັດລຽງແນວຕັ້ງ */
            align-items: center; /* ຈັດກึ่งກາງແນວນອນ */
            justify-content: center; /* ຈັດກึ่งກາງແນວຕັ້ງ */
            padding: 1rem; /* ເພີ່ມ padding */
        }
        
        .glass-card {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        
        .glowing-border {
            box-shadow: 0 0 15px rgba(139, 92, 246, 0.5);
        }
        
        .difficulty-btn {
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .difficulty-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }
        
        .floating {
            animation: float 4s ease-in-out infinite;
        }
        
        .progress-bar {
            height: 8px;
            border-radius: 4px;
            background: #e5e7eb;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #8b5cf6, #ec4899);
            transition: width 0.3s ease;
        }
        
        .guess-history {
            max-height: 200px;
            overflow-y: auto;
        }
        
        .guess-item {
            padding: 8px 12px;
            border-radius: 10px;
            margin: 4px 0;
            font-weight: 500;
        }
        
        .too-low {
            background: rgba(59, 130, 246, 0.2);
            border-left: 4px solid #3b82f6;
        }
        
        .too-high {
            background: rgba(239, 68, 68, 0.2);
            border-left: 4px solid #ef4444;
        }
        
        .correct {
            background: rgba(16, 185, 129, 0.2);
            border-left: 4px solid #10b981;
        }
        
        .confetti {
            position: absolute;
            width: 12px;
            height: 12px;
            top: 0;
            opacity: 0;
        }
        
        @keyframes confetti-fall {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
        
        .trophy {
            text-shadow: 0 0 10px rgba(245, 158, 11, 0.7);
        }
        
        .stats-card {
            background: rgba(255, 255, 255, 0.7);
            border-radius: 12px;
            padding: 15px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }
        
        .leaderboard-item {
            padding: 10px;
            border-radius: 10px;
            margin: 5px 0;
            background: rgba(255, 255, 255, 0.5);
        }
        
        .highlight {
            background: linear-gradient(90deg, #fde68a, #fcd34d);
        }

        /* ສຳລັບເອັບເຟັກ Pop */
        @keyframes pop {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        .text-pop-animation {
            animation: pop 0.3s ease-out;
        }

        /* ສຳລັບເອັບເຟັກ Shake ເມື່ອທາຍຜິດ/ໃສ່ຂໍ້ມູນບໍ່ຖືກຕ້ອງ */
        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }
        .shake-animation {
            animation: shake 0.3s ease-in-out;
        }

        /* ສຳລັບເອັບເຟັກ Background Pulse ເມື່ອທາຍຖືກ */
        @keyframes bg-pulse {
            0% { box-shadow: 0 0 0px 0px rgba(255, 255, 0, 0.7), 0 10px 30px rgba(0, 0, 0, 0.15); }
            50% { box-shadow: 0 0 40px 20px rgba(255, 255, 0, 0.7), 0 10px 30px rgba(0, 0, 0, 0.15); }
            100% { box-shadow: 0 0 0px 0px rgba(255, 255, 0, 0), 0 10px 30px rgba(0, 0, 0, 0.15); }
        }
        .bg-success-pulse {
            animation: bg-pulse 1s ease-out;
        }

        /* Modal Styles */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.6);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease, visibility 0.3s ease;
        }
        .modal-overlay.show {
            opacity: 1;
            visibility: visible;
        }
        .modal-content {
            background: white;
            padding: 2.5rem;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            text-align: center;
            width: 90%;
            max-width: 400px;
            transform: translateY(-20px);
            transition: transform 0.3s ease;
        }
        .modal-overlay.show .modal-content {
            transform: translateY(0);
        }
    </style>
</head>
<body class="flex flex-col items-center justify-center min-h-screen p-4">
    <!-- Decorative Elements -->
    <div class="absolute top-10 left-10 w-24 h-24 rounded-full bg-purple-500 opacity-20 blur-xl"></div>
    <div class="absolute bottom-20 right-20 w-32 h-32 rounded-full bg-pink-500 opacity-20 blur-xl"></div>
    <div class="absolute top-1/3 right-1/4 w-16 h-16 rounded-full bg-blue-500 opacity-20 blur-xl"></div>
    
    <!-- Floating Elements -->
    <div class="absolute top-20 right-20 text-4xl text-yellow-400 floating">
        <i class="fas fa-star"></i>
    </div>
    <div class="absolute bottom-20 left-20 text-4xl text-blue-400 floating" style="animation-delay: 1s;">
        <i class="fas fa-moon"></i>
    </div>
    
    <!-- Main Game Container -->
    <div id="gameContainer" class="glass-card w-full max-w-2xl p-6 md:p-8 relative overflow-hidden glowing-border">
        <!-- Confetti Container -->
        <div id="confettiContainer" class="absolute inset-0 pointer-events-none overflow-hidden z-confetti"></div>
        
        <!-- Header -->
        <div class="text-center mb-8">
            <h1 class="text-3xl md:text-4xl font-bold text-gray-800 mb-2">
                <i class="fas fa-brain mr-2 text-purple-600"></i>ເກມທາຍຕົວເລກລາວ
            </h1>
            <p class="text-gray-600" id="game-instruction">ທາຍເລກລະຫວ່າງ 1-100 ເພື່ອຊະນະຄະແນນສູງສຸດ!</p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <!-- Left Column - Game Area -->
            <div class="space-y-6">
                <!-- Game Stats -->
                <div class="flex justify-between items-center">
                    <div class="stats-card">
                        <div class="text-xs text-gray-500">ຄະແນນລວມ</div>
                        <div id="total-score" class="text-xl font-bold text-purple-600">0</div>
                    </div>
                    <div class="stats-card">
                        <div class="text-xs text-gray-500">ເກມທີ່ຊະນະ</div>
                        <div id="games-won" class="text-xl font-bold text-green-600">0</div>
                    </div>
                    <div class="stats-card">
                        <div class="text-xs text-gray-500">ລາຍການ</div>
                        <div id="total-games" class="text-xl font-bold text-blue-600">0</div>
                    </div>
                </div>
                
                <!-- Difficulty Selection -->
                <div class="bg-white bg-opacity-80 rounded-xl p-4">
                    <h2 class="text-lg font-semibold text-gray-700 mb-3 flex items-center">
                        <i class="fas fa-chart-line mr-2 text-purple-500"></i>ເລືອກລະດັບຄວາມຍາກ:
                    </h2>
                    <div class="space-y-3">
                        <button id="easy-btn" class="difficulty-btn w-full bg-gradient-to-r from-green-500 to-emerald-600 text-white font-bold py-3 px-4 rounded-xl text-lg flex items-center justify-center">
                            <i class="fas fa-seedling mr-2"></i>ງ່າຍ (1-50)
                        </button>
                        <button id="medium-btn" class="difficulty-btn w-full bg-gradient-to-r from-yellow-500 to-amber-600 text-white font-bold py-3 px-4 rounded-xl text-lg flex items-center justify-center">
                            <i class="fas fa-balance-scale mr-2"></i>ປານກາງ (1-100)
                        </button>
                        <button id="hard-btn" class="difficulty-btn w-full bg-gradient-to-r from-red-500 to-rose-700 text-white font-bold py-3 px-4 rounded-xl text-lg flex items-center justify-center">
                            <i class="fas fa-fire mr-2"></i>ຍາກ (1-1000)
                        </button>
                        <button id="very-hard-btn" class="difficulty-btn w-full bg-gradient-to-r from-gray-800 to-black text-white font-bold py-3 px-4 rounded-xl text-lg flex items-center justify-center">
                            <i class="fas fa-skull-crossbones mr-2"></i>ຍາກທີ່ສຸດ (1-1,000,000)
                        </button>
                    </div>
                </div>
                
                <!-- Game Progress -->
                <div class="bg-white bg-opacity-80 rounded-xl p-4">
                    <div class="flex justify-between text-sm text-gray-600 mb-2">
                        <span>ຄວາມຄືບໜ້າ:</span>
                        <span id="progress-percentage">0%</span>
                    </div>
                    <div class="progress-bar">
                        <div id="progress-fill" class="progress-fill" style="width: 0%"></div>
                    </div>
                </div>
            </div>
            
            <!-- Right Column - Game Play -->
            <div class="space-y-6">
                <!-- Game Play Area -->
                <div class="bg-white bg-opacity-80 rounded-xl p-4">
                    <div class="flex items-center justify-between mb-4">
                        <div>
                            <div class="text-sm text-gray-600">ເວລາ:</div>
                            <div id="game-time" class="text-xl font-bold text-blue-600">00:00</div>
                        </div>
                        <div>
                            <div class="text-sm text-gray-600">ຄັ້ງທີ່ທາຍ:</div>
                            <div id="attempts-display" class="text-xl font-bold text-gray-800">0</div>
                        </div>
                        <div>
                            <div class="text-sm text-gray-600">ຄະແນນ:</div>
                            <div id="current-score" class="text-xl font-bold text-purple-600">0</div>
                        </div>
                    </div>
                    
                    <div class="mb-4">
                        <div id="game-message" class="text-center text-lg font-medium text-gray-700 bg-blue-50 py-2 rounded-lg">
                            ທ່ານຄິດວ່າເລກທີ່ຂ້ອຍຄິດຢູ່ແມ່ນຫຍັງ?
                        </div>
                    </div>
                    
                    <div class="flex flex-col space-y-2 mb-4">
                        <input 
                            type="number" 
                            id="guess-input"
                            placeholder="ໃສ່ຕົວເລກທີ່ນີ້..."
                            class="w-full p-4 border-2 border-purple-300 rounded-xl text-lg focus:outline-none focus:ring-4 focus:ring-purple-300"
                            min="1"
                        >
                        <button id="submit-guess-btn" class="w-full bg-gradient-to-r from-purple-600 to-indigo-700 text-white font-bold py-4 px-6 rounded-xl text-lg">
                            <i class="fas fa-paper-plane mr-2"></i>ສົ່ງເລກທາຍ
                        </button>
                    </div>
                    
                    <!-- Hint button removed as per user request -->
                    <!-- <button id="hint-btn" class="w-full bg-gradient-to-r from-cyan-500 to-blue-600 text-white font-bold py-3 px-4 rounded-xl text-lg mt-2">
                        <i class="fas fa-lightbulb mr-2"></i>ຂໍຄຳແນະນຳ
                    </button> -->
                </div>
                
                <!-- Guess History -->
                <div class="bg-white bg-opacity-80 rounded-xl p-4">
                    <h3 class="text-md font-semibold text-gray-700 mb-3 flex items-center">
                        <i class="fas fa-history mr-2 text-purple-500"></i>ປະຫວັດການທາຍ:
                    </h3>
                    <div id="guess-history-list" class="guess-history">
                        <!-- Guess items will be appended here by JS -->
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Leaderboard -->
        <div class="mt-8 bg-white bg-opacity-80 rounded-xl p-4">
            <h3 class="text-lg font-semibold text-gray-700 mb-3 flex items-center">
                <i class="fas fa-trophy mr-2 text-yellow-500 trophy"></i>ກະດານຜູ້ໄດ້ຄະແນນສູງສຸດ:
            </h3>
            <div id="leaderboard-list" class="space-y-2">
                <!-- Leaderboard items will be appended here by JS -->
                <p class="text-center text-gray-500 py-4">ຫຼິ້ນເກມເພື່ອບັນທຶກຄະແນນຂອງທ່ານແລະເບິ່ງກະດານຜູ້ນໍາ!</p>
            </div>
            <p id="player-id-display" class="text-xs text-gray-500 mt-4 text-center">
                ລະຫັດຜູ້ໃຊ້: <span>ກຳລັງໂຫຼດ...</span>
            </p>
        </div>
        
        <!-- Game Controls -->
        <div class="flex justify-center space-x-4 mt-6">
            <button id="start-game-btn" class="bg-gradient-to-r from-green-500 to-emerald-600 text-white font-bold py-3 px-6 rounded-xl flex items-center">
                <i class="fas fa-play mr-2"></i>ເລີ່ມຫຼິ້ນ
            </button>
            <button id="reset-game-btn" class="bg-gradient-to-r from-gray-500 to-gray-700 text-white font-bold py-3 px-6 rounded-xl flex items-center hidden">
                <i class="fas fa-redo mr-2"></i>ເລີ່ມໃໝ່
            </button>
            <button id="toggle-sound-btn" class="bg-gradient-to-r from-blue-500 to-cyan-600 text-white font-bold py-3 px-6 rounded-xl flex items-center">
                <i class="fas fa-music mr-2"></i>ສຽງ
            </button>
        </div>
    </div>
    
    <!-- Footer -->
    <div class="text-center text-white mt-8 text-sm opacity-80">
        ພັດທະນາໂດຍ ໂປຣແກຣມເມີລາວ | ສະບັບ 2.0 | 2026
    </div>

    <!-- Player Name Modal -->
    <div id="playerNameModal" class="modal-overlay">
        <div class="modal-content">
            <h2 class="text-2xl font-bold text-gray-800 mb-4">ຍິນດີດ້ວຍ! ເຈົ້າຊະນະແລ້ວ!</h2>
            <p class="text-gray-700 mb-6">ກະລຸນາໃສ່ຊື່ຂອງທ່ານເພື່ອບັນທຶກຄະແນນ:</p>
            <input
                type="text"
                id="playerNameInput"
                placeholder="ຊື່ຂອງເຈົ້າ"
                class="w-full p-3 mb-4 border-2 border-gray-300 rounded-lg text-lg focus:outline-none focus:ring-2 focus:ring-purple-500"
                maxlength="20"
            >
            <button
                id="saveScoreBtn"
                class="w-full bg-gradient-to-r from-purple-600 to-indigo-700 text-white font-bold py-3 px-4 rounded-xl text-lg transition duration-300 ease-in-out transform hover:scale-105"
            >
                ບັນທຶກຄະແນນ
            </button>
        </div>
    </div>

    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, query, orderBy, onSnapshot, limit } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // ===============================================
        //  ການປະກາດຕົວແປ ແລະ Element HTML
        // ===============================================
        const gameContainer = document.getElementById('gameContainer');
        const confettiContainer = document.getElementById('confettiContainer');
        const gameInstruction = document.getElementById('game-instruction');
        const totalScoreDisplay = document.getElementById('total-score');
        const gamesWonDisplay = document.getElementById('games-won');
        const totalGamesDisplay = document.getElementById('total-games');
        const progressPercentageDisplay = document.getElementById('progress-percentage');
        const progressFill = document.getElementById('progress-fill');
        const gameTimeDisplay = document.getElementById('game-time');
        const attemptsDisplay = document.getElementById('attempts-display');
        const currentScoreDisplay = document.getElementById('current-score');
        const gameMessage = document.getElementById('game-message');
        const guessInput = document.getElementById('guess-input');
        const submitGuessBtn = document.getElementById('submit-guess-btn');
        const guessHistoryList = document.getElementById('guess-history-list');
        const leaderboardList = document.getElementById('leaderboard-list');
        const startGameBtn = document.getElementById('start-game-btn');
        const resetGameBtn = document.getElementById('reset-game-btn');
        const toggleSoundBtn = document.getElementById('toggle-sound-btn');
        const playerIdDisplay = document.getElementById('player-id-display').querySelector('span');

        // ປຸ່ມເລືອກຄວາມຍາກ
        const easyBtn = document.getElementById('easy-btn');
        const mediumBtn = document.getElementById('medium-btn');
        const hardBtn = document.getElementById('hard-btn');
        const veryHardBtn = document.getElementById('very-hard-btn'); // New very hard button
        const difficultyButtons = document.querySelectorAll('.difficulty-btn');
        
        // ໄອຄອນຖ້ວຍລາງວັນ (Leaderboard Trophy)
        const trophyIcon = document.querySelector('.trophy');

        // Player Name Modal Elements
        const playerNameModal = document.getElementById('playerNameModal');
        const playerNameInput = document.getElementById('playerNameInput');
        const saveScoreBtn = document.getElementById('saveScoreBtn');

        // ===============================================
        //  ຕົວແປສະຖານະເກມ
        // ===============================================
        let secretNumber = 0;
        let minNumber = 1;
        let maxNumber = 100;
        let attempts = 0;
        let maxAttempts = 10; // ຈຳນວນຄັ້ງສູງສຸດທີ່ທາຍໄດ້
        let timer = 0;
        let timerInterval;
        let currentScore = 0;
        let gameStarted = false;
        let gameWon = false;
        let isSoundOn = true; // ສະຖານະສຽງ

        // ສະຖິຕິລວມຂອງຜູ້ຫຼິ້ນ (ໃນຄວາມຈຳ)
        let totalGamesPlayed = 0;
        let totalGamesWon = 0;
        let overallScore = 0;

        // Firebase Instances
        let app;
        let auth;
        let db;
        let userId = 'loading...'; // ຕັ້ງຄ່າເລີ່ມຕົ້ນ

        // ===============================================
        //  ຟັງຊັນ Firebase ແລະ Authentication
        // ===============================================

        /**
         * @function initializeFirebase
         * @description ເລີ່ມຕົ້ນ Firebase App ແລະ Auth
         */
        async function initializeFirebase() {
            try {
                // ດຶງຄ່າຈາກ global variables
                const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
                const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
                const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

                app = initializeApp(firebaseConfig);
                auth = getAuth(app);
                db = getFirestore(app);

                onAuthStateChanged(auth, async (user) => {
                    if (user) {
                        userId = user.uid;
                        playerIdDisplay.textContent = userId;
                        console.log('Firebase user authenticated:', userId);
                        // ເລີ່ມຟັງຊັນທີ່ຕ້ອງໃຊ້ Firebase ຫຼັງຈາກ Auth ພ້ອມ
                        renderLeaderboard(); // ໂຫຼດ leaderboard ເມື່ອຜູ້ໃຊ້ authenticated
                    } else {
                        // ຖ້າບໍ່ມີຜູ້ໃຊ້, ພະຍາຍາມລົງຊື່ອັດຕະໂນມັດ
                        if (initialAuthToken) {
                            try {
                                await signInWithCustomToken(auth, initialAuthToken);
                                console.log('Signed in with custom token.');
                            } catch (error) {
                                console.error('Error signing in with custom token:', error);
                                await signInAnonymously(auth); // ຖ້າ custom token ບໍ່ສຳເລັດ, ໃຫ້ sign in ແບບ anonymous
                                console.log('Signed in anonymously after custom token failure.');
                            }
                        } else {
                            await signInAnonymously(auth);
                            console.log('Signed in anonymously.');
                        }
                    }
                });
            } catch (error) {
                console.error("Firebase initialization error:", error);
                gameMessage.textContent = "ເກີດຂໍ້ຜິດພາດໃນການເຊື່ອມຕໍ່ກັບເຊີບເວີ.";
            }
        }

        // ===============================================
        //  ຟັງຊັນຊ່ວຍເຫຼືອ
        // ===============================================

        /**
         * @function updateUIStats
         * @description ອັບເດດສະຖິຕິເກມເທິງ UI
         */
        function updateUIStats() {
            totalScoreDisplay.textContent = overallScore.toLocaleString();
            gamesWonDisplay.textContent = totalGamesWon;
            totalGamesDisplay.textContent = totalGamesPlayed;
            attemptsDisplay.textContent = attempts;
            currentScoreDisplay.textContent = currentScore;
        }

        /**
         * @function updateTimerDisplay
         * @description ອັບເດດການສະແດງຜົນເວລາ
         */
        function updateTimerDisplay() {
            const minutes = Math.floor(timer / 60);
            const seconds = timer % 60;
            gameTimeDisplay.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        /**
         * @function updateProgressBar
         * @description ອັບເດດແຖບຄວາມຄືບໜ້າ
         */
        function updateProgressBar() {
            if (maxAttempts === 0) {
                progressFill.style.width = '100%';
                progressPercentageDisplay.textContent = '100%';
                return;
            }
            const percentage = (attempts / maxAttempts) * 100;
            progressFill.style.width = `${percentage}%`;
            progressPercentageDisplay.textContent = `${Math.floor(percentage)}%`;
        }

        /**
         * @function addGuessToHistory
         * @description ເພີ່ມລາຍການທາຍເຂົ້າໃນປະຫວັດ
         * @param {number} guess - ຕົວເລກທີ່ຜູ້ຫຼິ້ນທາຍ
         * @param {string} resultClass - class CSS ສຳລັບຜົນລัพທ໌ (too-low, too-high, correct)
         * @param {string} message - ຂໍ້ຄວາມສະແດງຜົນ
         */
        function addGuessToHistory(guess, resultClass, message) {
            const guessItem = document.createElement('div');
            guessItem.className = `guess-item ${resultClass}`;
            guessItem.textContent = `${guess} → ${message}`;
            guessHistoryList.prepend(guessItem);

            if (guessHistoryList.children.length > 5) {
                guessHistoryList.removeChild(guessHistoryList.lastChild);
            }
        }

        /**
         * @function calculateScore
         * @description ຄິດໄລ່ຄະແນນ
         * @returns {number} ຄະແນນທີ່ຄິດໄລ່ໄດ້
         */
        function calculateScore() {
            let baseScore = 0;
            if (maxNumber === 50) baseScore = 500;
            else if (maxNumber === 100) baseScore = 1000;
            else if (maxNumber === 1000) baseScore = 2000;
            else if (maxNumber === 1000000) baseScore = 10000; // Base score for very hard

            const attemptsPenalty = attempts * 50;
            const timePenalty = Math.floor(timer / 5) * 20;

            let finalScore = baseScore - attemptsPenalty - timePenalty;
            return Math.max(0, finalScore);
        }

        /**
         * @function updateLeaderboardFirestore
         * @description ອັບເດດ Leaderboard ດ້ວຍຄະແນນໃໝ່
         * @param {string} playerName - ຊື່ຜູ້ຫຼິ້ນ
         * @param {number} score - ຄະແນນທີ່ໄດ້
         */
        async function updateLeaderboardFirestore(playerName, score) {
            if (!db || !userId) {
                console.error("Firestore not initialized or user not authenticated.");
                gameMessage.textContent = "ບໍ່ສາມາດບັນທຶກຄະແນນໄດ້. ກະລຸນາລອງໃໝ່ພາຍຫຼັງ.";
                return;
            }

            try {
                const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
                const leaderboardCollectionRef = collection(db, `artifacts/${appId}/public/data/leaderboard`);
                
                await addDoc(leaderboardCollectionRef, {
                    name: playerName,
                    score: score,
                    timestamp: Date.now(), // ເວລາທີ່ບັນທຶກ
                    userId: userId // ບັນທຶກ userId ໄວ້
                });
                console.log("Score successfully written to Firestore!");
            } catch (e) {
                console.error("Error adding document: ", e);
                gameMessage.textContent = "ເກີດຂໍ້ຜິດພາດໃນການບັນທຶກຄະແນນ.";
            }
        }

        /**
         * @function renderLeaderboard
         * @description ສະແດງ Leaderboard ເທິງ UI ຈາກ Firestore real-time updates
         */
        function renderLeaderboard() {
            if (!db) {
                console.warn("Firestore not initialized for leaderboard rendering.");
                return;
            }
            const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
            const leaderboardCollectionRef = collection(db, `artifacts/${appId}/public/data/leaderboard`);
            const q = query(leaderboardCollectionRef, orderBy('score', 'desc'), limit(5));

            onSnapshot(q, (snapshot) => {
                leaderboardList.innerHTML = ''; // Clear previous items
                if (snapshot.empty) {
                    // Display message if no scores exist
                    leaderboardList.innerHTML = '<p class="text-center text-gray-500 py-4">ຫຼິ້ນເກມເພື່ອບັນທຶກຄະແນນຂອງທ່ານແລະເບິ່ງກະດານຜູ້ນໍາ!</p>';
                } else {
                    snapshot.forEach((doc, index) => {
                        const item = doc.data();
                        const leaderboardItem = document.createElement('div');
                        leaderboardItem.className = `leaderboard-item flex items-center ${index === 0 ? 'highlight' : ''}`;
                        leaderboardItem.innerHTML = `
                            <span class="w-6 h-6 rounded-full ${index === 0 ? 'bg-yellow-400' : 'bg-gray-300'} flex items-center justify-center text-white mr-3">
                                ${index + 1}
                            </span>
                            <div class="flex-1">${item.name}</div>
                            <div class="font-bold text-purple-600">${item.score.toLocaleString()}</div>
                        `;
                        leaderboardList.appendChild(leaderboardItem);
                    });
                }
            }, (error) => {
                console.error("Error fetching leaderboard: ", error);
                leaderboardList.innerHTML = '<p class="text-center text-red-500 py-4">ບໍ່ສາມາດໂຫຼດກະດານຄະແນນໄດ້.</p>';
            });
        }
        
        /**
         * @function createConfetti
         * @description ສ້າງເອັບເຟັກ confetti (ພລັງງານ)
         */
        function createConfetti() {
            const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff'];
            confettiContainer.innerHTML = ''; // ລຶບ confetti ເກົ່າອອກ
            
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.left = Math.random() * 100 + '%';
                confetti.style.animation = `confetti-fall ${Math.random() * 3 + 2}s linear forwards`;
                confetti.style.animationDelay = `${Math.random() * 0.5}s`;
                confettiContainer.appendChild(confetti);
                
                setTimeout(() => {
                    confetti.remove();
                }, 5000);
            }
        }

        /**
         * @function triggerShakeAnimation
         * @description ເພີ່ມເອັບເຟັກສັ່ນໃສ່ກ່ອງເກມ
         */
        function triggerShakeAnimation() {
            gameContainer.classList.add('shake-animation');
            setTimeout(() => {
                gameContainer.classList.remove('shake-animation');
            }, 300);
        }

        /**
         * @function triggerSuccessAnimation
         * @description ເພີ່ມເອັບເຟັກສຳລັບການທາຍຖືກ
         */
        function triggerSuccessAnimation() {
            gameMessage.classList.add('text-pop-animation');
            gameContainer.classList.add('bg-success-pulse');

            setTimeout(() => {
                gameMessage.classList.remove('text-pop-animation');
                gameContainer.classList.remove('bg-success-pulse');
            }, 1000);
            createConfetti();
        }

        /**
         * @function showPlayerNameModal
         * @description ສະແດງ Player Name Modal
         */
        function showPlayerNameModal() {
            playerNameModal.classList.add('show');
            playerNameInput.value = ''; // Clear previous input
            playerNameInput.focus();
        }

        /**
         * @function hidePlayerNameModal
         * @description ເຊື່ອງ Player Name Modal
         */
        function hidePlayerNameModal() {
            playerNameModal.classList.remove('show');
        }


        // ===============================================
        //  ຟັງຊັນຫຼັກຂອງເກມ
        // ===============================================

        /**
         * @function startGame
         * @description ເລີ່ມຕົ້ນເກມໃໝ່ ຫຼື ຫຼິ້ນຕໍ່
         */
        function startGame() {
            if (gameStarted) return;
            
            gameStarted = true;
            gameWon = false;
            attempts = 0;
            timer = 0;
            guessHistoryList.innerHTML = '';
            guessInput.value = '';
            guessInput.disabled = false;
            submitGuessBtn.disabled = false;
            gameMessage.textContent = `ຂ້ອຍກຳລັງຄິດເລກລະຫວ່າງ ${minNumber} ຫາ ${maxNumber.toLocaleString('lo-LA')} ຢູ່... ເຈົ້າທາຍໄດ້ບໍວ່າມັນແມ່ນເລກຫຍັງ?`;
            
            secretNumber = Math.floor(Math.random() * (maxNumber - minNumber + 1)) + minNumber;
            console.log('Secret Number (for debugging):', secretNumber);

            updateUIStats();
            updateProgressBar();
            updateTimerDisplay();

            timerInterval = setInterval(() => {
                timer++;
                updateTimerDisplay();
            }, 1000);

            startGameBtn.classList.add('hidden');
            resetGameBtn.classList.remove('hidden');
        }

        /**
         * @function resetGame
         * @description ຣີເຊັດເກມ
         */
        function resetGame() {
            clearInterval(timerInterval);
            gameStarted = false;
            gameWon = false;
            attempts = 0;
            timer = 0;
            secretNumber = 0;
            currentScore = 0;

            guessHistoryList.innerHTML = '';
            guessInput.value = '';
            guessInput.disabled = true;
            submitGuessBtn.disabled = true;
            gameMessage.textContent = 'ກົດ "ເລີ່ມຫຼິ້ນ" ເພື່ອເລີ່ມເກມ!';

            updateUIStats();
            updateProgressBar();
            updateTimerDisplay();
            
            startGameBtn.classList.remove('hidden');
            resetGameBtn.classList.add('hidden');

            gameContainer.classList.remove('shake-animation', 'bg-success-pulse');
            gameMessage.classList.remove('text-pop-animation');

            difficultyButtons.forEach(btn => {
                btn.classList.remove('pulse', 'ring-4', 'ring-green-500', 'ring-yellow-500', 'ring-red-500', 'ring-gray-800'); // Add ring-gray-800 for very hard
            });
        }

        /**
         * @function checkGuess
         * @description ກວດສອບຕົວເລກທີ່ຜູ້ຫຼິ້ນທາຍ
         */
        function checkGuess() {
            if (!gameStarted || gameWon) return;

            const userGuess = parseInt(guessInput.value);

            if (isNaN(userGuess) || userGuess < minNumber || userGuess > maxNumber) {
                gameMessage.textContent = `ກະລຸນາໃສ່ຕົວເລກລະຫວ່າງ ${minNumber} ຫາ ${maxNumber.toLocaleString('lo-LA')} ເທົ່ານັ້ນເດີ້!`;
                triggerShakeAnimation();
                guessInput.value = '';
                return;
            }

            attempts++;
            updateProgressBar();
            
            if (userGuess === secretNumber) {
                gameWon = true;
                clearInterval(timerInterval);
                currentScore = calculateScore();
                overallScore += currentScore;
                totalGamesPlayed++;
                totalGamesWon++;
                
                gameMessage.textContent = `ຮ່າໆໆໆ! ເຈົ້າທາຍຖືກແລ້ວ! ແມ່ນເລກ ${secretNumber} 😝 ເຈົ້າທາຍໄປ ${attempts} ຄັ້ງ, ໃຊ້ເວລາ ${timer} ວິນາທີ! ເກັ່ງເກີນໄປແລ້ວ!`;
                
                addGuessToHistory(userGuess, 'correct', 'ຖືກຕ້ອງ! 🎉');
                updateUIStats();
                triggerSuccessAnimation();

                guessInput.disabled = true;
                submitGuessBtn.disabled = true;
                
                showPlayerNameModal();

            } else if (userGuess < secretNumber) {
                gameMessage.textContent = 'ໜ້ອຍໂພດ! ລອງທາຍອີກຄັ້ງ';
                addGuessToHistory(userGuess, 'too-low', 'ໜ້ອຍໂພດ!');
                triggerShakeAnimation();
            } else {
                gameMessage.textContent = 'ຫຼາຍໂພດ! ລອງທາຍອີກຄັ້ງ';
                addGuessToHistory(userGuess, 'too-high', 'ຫຼາຍໂພດ!');
                triggerShakeAnimation();
            }
            guessInput.value = '';
        }

        /**
         * @function selectDifficulty
         * @description ກຳນົດຄວາມຍາກຂອງເກມ
         * @param {number} min - ຄ່າຕໍ່າສຸດຂອງຕົວເລກ
         * @param {number} max - ຄ່າສູງສຸດຂອງຕົວເລກ
         * @param {HTMLElement} activeBtn - ປຸ່ມຄວາມຍາກທີ່ກົດ
         */
        function selectDifficulty(min, max, activeBtn) {
            minNumber = min;
            maxNumber = max;
            maxAttempts = Math.ceil(Math.log2(max - min + 1)) + 3;
            gameInstruction.textContent = `ທາຍເລກລະຫວ່າງ ${minNumber}-${maxNumber.toLocaleString('lo-LA')} ເພື່ອຊະນະຄະແນນສູງສຸດ!`;
            
            resetGame(); // ຣີເຊັດເກມເມື່ອປ່ຽນຄວາມຍາກ
            
            difficultyButtons.forEach(btn => {
                btn.classList.remove('pulse', 'ring-4', 'ring-green-500', 'ring-yellow-500', 'ring-red-500', 'ring-gray-800');
            });
            if (activeBtn) {
                activeBtn.classList.add('pulse', 'ring-4');
                if (activeBtn.id === 'easy-btn') activeBtn.classList.add('ring-green-500');
                else if (activeBtn.id === 'medium-btn') activeBtn.classList.add('ring-yellow-500');
                else if (activeBtn.id === 'hard-btn') activeBtn.classList.add('ring-red-500');
                else if (activeBtn.id === 'very-hard-btn') activeBtn.classList.add('ring-gray-800');
            }
        }

        /**
         * @function toggleSound
         * @description ເປີດ/ປິດສຽງ (ຕົວຢ່າງ: ປ່ຽນໄອຄອນ)
         */
        function toggleSound() {
            isSoundOn = !isSoundOn;
            const soundIcon = toggleSoundBtn.querySelector('i');
            if (isSoundOn) {
                soundIcon.classList.remove('fa-volume-mute');
                soundIcon.classList.add('fa-music');
                gameMessage.textContent = 'ສຽງເປີດແລ້ວ! 🎶';
            } else {
                soundIcon.classList.remove('fa-music');
                soundIcon.classList.add('fa-volume-mute');
                gameMessage.textContent = 'ສຽງປິດແລ້ວ! �';
            }
            setTimeout(() => {
                if (!gameStarted || gameWon) {
                     gameMessage.textContent = 'ກົດ "ເລີ່ມຫຼິ້ນ" ເພື່ອເລີ່ມເກມ!';
                } else {
                     gameMessage.textContent = `ຂ້ອຍກຳລັງຄິດເລກລະຫວ່າງ ${minNumber} ຫາ ${maxNumber.toLocaleString('lo-LA')} ຢູ່...`;
                }
            }, 2000);
        }


        // ===============================================
        //  Event Listeners
        // ===============================================

        startGameBtn.addEventListener('click', startGame);
        resetGameBtn.addEventListener('click', resetGame);
        submitGuessBtn.addEventListener('click', checkGuess);
        guessInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                checkGuess();
            }
        });
        toggleSoundBtn.addEventListener('click', toggleSound);
        easyBtn.addEventListener('click', () => selectDifficulty(1, 50, easyBtn));
        mediumBtn.addEventListener('click', () => selectDifficulty(1, 100, mediumBtn));
        hardBtn.addEventListener('click', () => selectDifficulty(1, 1000, hardBtn));
        veryHardBtn.addEventListener('click', () => selectDifficulty(1, 1000000, veryHardBtn)); // New event listener

        saveScoreBtn.addEventListener('click', () => {
            const playerName = playerNameInput.value.trim();
            if (playerName) {
                updateLeaderboardFirestore(playerName, currentScore);
                hidePlayerNameModal();
                resetGame(); // Reset game after saving score and hiding modal
            } else {
                playerNameInput.placeholder = 'ກະລຸນາໃສ່ຊື່ກ່ອນ!';
                playerNameInput.classList.add('border-red-500');
                triggerShakeAnimation(); // Shake the input field
            }
        });
        playerNameInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                saveScoreBtn.click(); // Simulate click on save button
            }
        });

        setInterval(() => {
            if (trophyIcon) {
                trophyIcon.classList.toggle('text-yellow-400');
                trophyIcon.classList.toggle('text-yellow-300');
            }
        }, 1000);

        // ===============================================
        //  ການເລີ່ມຕົ້ນເກມເມື່ອໂຫຼດໜ້າ
        // ===============================================
        window.onload = async () => {
            await initializeFirebase(); // Initialize Firebase first
            // ເລືອກຄວາມຍາກປານກາງເປັນຄ່າເລີ່ມຕົ້ນ
            selectDifficulty(1, 100, mediumBtn); 
        };
    </script>
</body>
</html>
�
