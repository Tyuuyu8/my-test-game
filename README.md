<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اربح بدون ايداع - ماكنة الحظ</title>
    <style>
        body {
            background-color: #121212;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .game-container {
            text-align: center;
            background-color: #1e1e1e;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
            width: 90%;
            max-width: 350px;
        }

        h1 { color: #ff9800; margin-bottom: 5px; font-size: 1.8em; }

        .status-panel { background: #2a2a2a; padding: 10px; border-radius: 8px; margin-bottom: 20px; }
        #balance { font-weight: bold; color: #4caf50; font-size: 1.3em; }
        .cost-text { color: #aaa; font-size: 0.9em; margin: 5px 0 0 0; }

        .slot-machine {
            display: flex;
            justify-content: space-between;
            background-color: #000;
            padding: 15px;
            border-radius: 10px;
            border: 4px solid #333;
            margin-bottom: 20px;
            overflow: hidden;
        }

        .reel {
            width: 75px;
            height: 100px; 
            background-color: white;
            border-radius: 5px;
            overflow: hidden; 
            position: relative;
        }

        .symbols-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            transition: transform 3s cubic-bezier(.2,.8,.4,.9); 
        }

        .symbol {
            height: 100px; 
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 3.5em; 
        }

        #spin-button {
            background-color: #ff9800;
            color: #121212;
            border: none;
            padding: 15px 30px;
            font-size: 1.2em;
            font-weight: bold;
            border-radius: 30px;
            cursor: pointer;
            width: 100%;
            transition: background-color 0.3s;
        }

        #spin-button:hover { background-color: #e68a00; }
        #spin-button:disabled { background-color: #555; cursor: not-allowed; }

        #message { margin-top: 15px; font-weight: bold; min-height: 1.2em; }
        .win { color: #4caf50; }
        .loss { color: #f44336; }
    </style>
</head>
<body>

    <div class="game-container">
        <h1>اربح بدون ايداع</h1>
        
        <div class="status-panel">
            <p style="margin:0;">رصيدك الحالي: <span id="balance">100</span> نقطة</p>
            <p class="cost-text">تكلفة اللفة: 10 نقاط</p>
        </div>

        <div class="slot-machine">
            <div class="reel" id="reel1"><div class="symbols-container"></div></div>
            <div class="reel" id="reel2"><div class="symbols-container"></div></div>
            <div class="reel" id="reel3"><div class="symbols-container"></div></div>
        </div>

        <button id="spin-button" onclick="spin()">إضغط لتجربة حظك</button>
        <p id="message"></p>
    </div>

    <script>
        const SYMBOLS = ['🍒', '🍋', '🍊', '🍇', '⭐', '💰'];
        const SPIN_COST = 10; 
        const SYMBOL_HEIGHT = 100; 
        const NUM_SYMBOLS_PER_REEL = 10; 

        let balance = 100; 
        let isSpinning = false; 

        const balanceEl = document.getElementById('balance');
        const messageEl = document.getElementById('message');
        const spinButton = document.getElementById('spin-button');

        function initReels() {
            const reels = document.querySelectorAll('.symbols-container');
            reels.forEach(reel => {
                let html = '';
                for (let i = 0; i < NUM_SYMBOLS_PER_REEL; i++) {
                    const randomSymbol = SYMBOLS[Math.floor(Math.random() * SYMBOLS.length)];
                    html += `<div class="symbol">${randomSymbol}</div>`;
                }
                reel.innerHTML = html;
                reel.style.transform = 'translateY(0px)';
            });
        }

        function spin() {
            if (isSpinning) return; 

            if (balance < SPIN_COST) {
                messageEl.textContent = "عفواً، ليس لديك نقاط كافية!";
                messageEl.className = 'loss';
                return;
            }

            isSpinning = true;
            balance -= SPIN_COST;
            updateUI();
            spinButton.disabled = true;
            messageEl.textContent = "جاري تدوير البكرات...";
            messageEl.className = '';

            const results = []; 

            for (let i = 1; i <= 3; i++) {
                const reelContainer = document.querySelector(`#reel${i} .symbols-container`);
                reelContainer.style.transition = 'none';
                reelContainer.style.transform = 'translateY(0px)';
                
                const finalSymbolIndex = Math.floor(Math.random() * SYMBOLS.length);
                const finalSymbol = SYMBOLS[finalSymbolIndex]; // تم تعديلها هنا بشكل صحيح مية بالمية
                results.push(finalSymbol);

                let animationHtml = '';
                for (let j = 0; j < NUM_SYMBOLS_PER_REEL - 1; j++) {
                    const randomSymbol = SYMBOLS[Math.floor(Math.random() * SYMBOLS.length)];
                    animationHtml += `<div class="symbol">${randomSymbol}</div>`;
                }
                animationHtml += `<div class="symbol">${finalSymbol}</div>`;
                reelContainer.innerHTML = animationHtml;

                setTimeout(() => {
                    reelContainer.style.transition = 'transform 3s cubic-bezier(.2,.8,.4,.9)';
                    const translateY = -(NUM_SYMBOLS_PER_REEL - 1) * SYMBOL_HEIGHT;
                    reelContainer.style.transform = `translateY(${translateY}px)`;
                }, 50);
            }

            setTimeout(() => {
                isSpinning = false;
                spinButton.disabled = false;
                calculateWin(results);
            }, 3050);
        }

        function calculateWin(results) {
            const [s1, s2, s3] = results;
            let winAmount = 0;

            if (s1 === '💰' && s2 === '💰' && s3 === '💰') {
                winAmount = 100;
            } else if (s1 === '⭐' && s2 === '⭐' && s3 === '⭐') {
                winAmount = 50;
            } else if (s1 === s2 && s2 === s3) {
                winAmount = 25;
            } else if (s1 === '🍒' && s2 === '🍒') {
                winAmount = 5;
            }

            if (winAmount > 0) {
                balance += winAmount;
                messageEl.textContent = `مبروك! فزت بـ ${winAmount} نقطة! 🎉`;
                messageEl.className = 'win';
            } else {
                messageEl.textContent = "حظاً أوفق في المرة القادمة.";
                messageEl.className = 'loss';
            }
            updateUI();
        }

        function updateUI() {
            balanceEl.textContent = balance;
        }

        initReels();
        updateUI();
    </script>
</body>
</html>
