<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>wenchitot</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: Arial, sans-serif; }
        body { background: linear-gradient(135deg, #fff5f8, #ffeaf2); min-height: 100vh; display: flex; flex-direction: column; align-items: center; padding: 2rem 1rem; }
        .container { max-width: 500px; width: 100%; text-align: center; }
        .box { background: #ffffffee; border-radius: 20px; padding: 2.5rem 2rem; box-shadow: 0 8px 32px #ff94b844; margin-bottom: 1.5rem; }
        h1 { color: #d63384; margin-bottom: 1rem; font-size: 1.6rem; }
        p { color: #444; line-height: 1.7; margin-bottom: 1rem; font-size: 1rem; }
        input { padding: 0.75rem 1rem; border: 2px solid #f8c8dc; border-radius: 12px; font-size: 1rem; width: 180px; text-align: center; margin: 0.5rem; }
        button { padding: 0.7rem 1.5rem; background: #e8599c; color: white; border: none; border-radius: 12px; font-size: 1rem; cursor: pointer; transition: 0.2s; margin: 0.3rem; }
        button:hover { background: #d13b82; transform: scale(1.03); }
        button:disabled { background: #ccc; cursor: not-allowed; transform: none; }
        .game-area { margin: 1.5rem 0; }
        .game-btn { width: 60px; height: 60px; border-radius: 50%; font-size: 1.2rem; }
        .status { font-weight: bold; color: #c02970; margin-top: 0.8rem; }
        .wish-btn { width: 55px; height: 55px; border-radius: 50%; background: #ff7eb3; font-weight: bold; font-size: 1.1rem; }
        .wish-btn.revealed { background: #f8d7e5; color: #999; cursor: default; }
        .wish-text { margin: 1rem auto; padding: 1.2rem; background: #fff0f7; border-radius: 12px; min-height: 80px; display: flex; align-items: center; justify-content: center; color: #b02468; font-weight: 500; max-width: 400px; text-align: left; line-height: 1.6; }
        .hidden { display: none !important; }
        .final-box { background: linear-gradient(135deg, #ffd7ec, #ffb3d9); border: 2px solid #f078b0; }
    </style>
</head>
<body>
    <div class="container">
        <div id="passScreen" class="box">
            <h1>🔒 Enter Password</h1>
            <p>Type the code to open this gift 💌</p>
            <input type="password" id="passInput" placeholder="••••">
            <br>
            <button onclick="checkPass()">Open</button>
            <p id="passErr" style="color:#dc3545; font-size:0.9rem; margin-top:0.5rem;" class="hidden">Wrong password — try again</p>
        </div>
        <div id="gameScreen" class="box hidden">
            <h1>🎮 Little Game First</h1>
            <p>Click the blinking button 5 times fast to unlock your wishes! 💫</p>
            <div class="game-area">
                <button id="gameBtn" class="game-btn" onclick="tapGame()">✨</button>
                <p class="status">Taps: <span id="tapCount">0</span> / 5</p>
            </div>
        </div>
        <div id="wishScreen" class="box hidden">
            <h1>🎂 19 Wishes For You</h1>
            <p>Click each number to reveal — one by one lang 😉</p>
            <div style="display:flex; flex-wrap:wrap; gap:0.6rem; justify-content:center; margin:1.2rem 0;">
                <button class="wish-btn" data-num="1" onclick="showWish(this)">1</button>
                <button class="wish-btn" data-num="2" onclick="showWish(this)">2</button>
                <button class="wish-btn" data-num="3" onclick="showWish(this)">3</button>
                <button class="wish-btn" data-num="4" onclick="showWish(this)">4</button>
                <button class="wish-btn" data-num="5" onclick="showWish(this)">5</button>
                <button class="wish-btn" data-num="6" onclick="showWish(this)">6</button>
                <button class="wish-btn" data-num="7" onclick="showWish(this)">7</button>
                <button class="wish-btn" data-num="8" onclick="showWish(this)">8</button>
                <button class="wish-btn" data-num="9" onclick="showWish(this)">9</button>
                <button class="wish-btn" data-num="10" onclick="showWish(this)">10</button>
                <button class="wish-btn" data-num="11" onclick="showWish(this)">11</button>
                <button class="wish-btn" data-num="12" onclick="showWish(this)">12</button>
                <button class="wish-btn" data-num="13" onclick="showWish(this)">13</button>
                <button class="wish-btn" data-num="14" onclick="showWish(this)">14</button>
                <button class="wish-btn" data-num="15" onclick="showWish(this)">15</button>
                <button class="wish-btn" data-num="16" onclick="showWish(this)">16</button>
                <button class="wish-btn" data-num="17" onclick="showWish(this)">17</button>
                <button class="wish-btn" data-num="18" onclick="showWish(this)">18</button>
                <button class="wish-btn" data-num="19" onclick="showWish(this)">19</button>
            </div>
            <div id="wishDisplay" class="wish-text">👇 Pick a number above 💖</div>
            <br>
            <button id="finalBtn" class="hidden" onclick="showFinal()">✨ See Final Surprise ✨</button>
        </div>
        <div id="finalScreen" class="box final-box hidden">
            <h1>💝 Special Message</h1>
            <p style="font-size:1rem; line-height:1.8; text-align:left;">
Wenchii, that's all na 😭<br><br>
I know this is just a small thing, pero I wanted to make something for you instead of just sending a normal birthday greeting. Four years is a long time, and even though a lot has changed since then, I still wanted to wish you well on your special day.<br><br>
I don't really know what life has in store for you from here, but whatever path you choose, I genuinely hope it leads you somewhere good.<br><br>
Keep doing your best sa life, take care of yourself, and don't forget to enjoy the little things pud. And if life gets hard sometimes, I hope you remember nga kaya ra nimo na.<br><br>
Happy birthday, Wenchii. 🤍<br>
I hope you had a good day, and I hope this little gift made you smile, even just for a while.<br><br>
Take care always. And yeah... happy birthday again. 🫶
            </p>
        </div>
    </div>
<script>
const CORRECT_PASS = "0612";
function checkPass(){
    const input = document.getElementById("passInput").value.trim();
    if(input === CORRECT_PASS){
        document.getElementById("passScreen").classList.add("hidden");
        document.getElementById("gameScreen").classList.remove("hidden");
        startBlink();
    } else {
        document.getElementById("passErr").classList.remove("hidden");
    }
}
let taps = 0;
function startBlink(){
    const btn = document.getElementById("gameBtn");
    setInterval(()=> btn.style.opacity = btn.style.opacity === "1" ? "0.4" : "1", 450);
}
function tapGame(){
    taps++;
    document.getElementById("tapCount").textContent = taps;
    if(taps >=5){
        document.getElementById("gameScreen").classList.add("hidden");
        document.getElementById("wishScreen").classList.remove("hidden");
    }
}
const wishes = [
    "1. I hope you're always okay, even on the days nga medyo kapoy ka or wala kay gana.",
    "2. I hope Papa God always guides you sa mga decisions and paths nga imong pilion.",
    "3. I hope you get the happiness nga deserve jud nimo, kanang peaceful lang and genuine.",
    "4. I hope you never lose that kind side of you. Mao na isa sa things nga nice about you.",
    "5. I hope you always have people around you nga genuinely care about you.",
    "6. I hope you become closer to the person nga gusto nimo mahimong someday.",
    "7. I hope all the things you're working hard for slowly work out for you.",
    "8. I hope you get more reasons to smile this year kaysa reasons to overthink.",
    "9. I hope you learn to rest pud when you're tired. Dili kinahanglan always strong.",
    "10. I hope you keep choosing yourself and your peace when you need to.",
    "11. I hope this year gives you a lot of memories nga worth remembering.",
    "12. I hope you get to experience the things nga you've always wanted to try.",
    "13. I hope you never doubt yourself too much. You can do more than you think.",
    "14. I hope you stay soft-hearted, pero kabalo pud ka when to protect yourself.",
    "15. I hope someday you'll look back and realize nga you've grown so much already.",
    "16. I hope life becomes a little kinder to you, especially during the days nga heavy kaayo.",
    "17. I hope you always remember nga naa jud mga tao nga silently rooting for you, bisan dili always makita.",
    "18. I hope this new year of your life brings you peace, growth, good people, and a lot of genuine happiness.",
    "19. And most importantly, I hope you never forget nga you deserve to be happy. Not because you have to prove anything, but simply because you do."
];
let revealedCount = 0;
function showWish(btn){
    if(btn.classList.contains("revealed")) return;
    btn.classList.add("revealed");
    const num = parseInt(btn.dataset.num);
    document.getElementById("wishDisplay").textContent = wishes[num - 1];
    revealedCount++;
    if(revealedCount >= 19) document.getElementById("finalBtn").classList.remove("hidden");
}
function showFinal(){
    document.getElementById("wishScreen").classList.add("hidden");
    document.getElementById("finalScreen").classList.remove("hidden");
}
</script>
</body>
</html> 
