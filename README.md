<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <title>تجربة ماكنة حظ</title>
    <style>
        body { text-align: center; font-family: sans-serif; background: #121212; color: white; padding-top: 50px; }
        #balance { font-size: 24px; color: #4CAF50; }
        button { padding: 15px 30px; font-size: 18px; cursor: pointer; background: #ff9800; border: none; border-radius: 5px; }
    </style>
</head>
<body>
    <h1>ماكنة الحظ التجريبية</h1>
    <p>رصيدك الوهمي: <span id="balance">100</span> نقطة</p>
    <button onclick="play()">إضغط لتجربة حظك (تكلفة 10 نقاط)</button>
    <p id="result"></p>

    <script>
        let credits = 100;
        function play() {
            if (credits < 10) { alert("رصيدك خلص!"); return; }
            credits -= 10;
            let win = Math.random() < 0.2; // نسبة الفوز 20%
            if (win) {
                credits += 50;
                document.getElementById("result").innerText = "مبروك! فزت بـ 50 نقطة 🎉";
            } else {
                document.getElementById("result").innerText = "للأسف، خسرت.. حاول مرة ثانية 💔";
            }
            document.getElementById("balance").innerText = credits;
        }
    </script>
</body>
</html>
