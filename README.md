# Valentines-specials
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>NNI ❤️ BEEBO</title>

<style>
body {
    margin: 0;
    font-family: "Segoe UI", Arial, sans-serif;
    background: linear-gradient(135deg, #ff758c, #ff7eb3);
    color: white;
    height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
}

/* Soft glow background */
body::before {
    content: "";
    position: absolute;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle, rgba(255,255,255,0.15), transparent 40%);
    animation: glowMove 10s linear infinite;
}

@keyframes glowMove {
    from { transform: translate(-20%, -20%); }
    to { transform: translate(-30%, -30%); }
}

.card {
    background: rgba(0,0,0,0.25);
    padding: 30px;
    border-radius: 30px;
    width: 90%;
    max-width: 420px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.35);
    backdrop-filter: blur(10px);
    position: relative;
    z-index: 2;
}

h1 { margin: 0; font-size: 32px; }

.typing {
    margin-top: 10px;
    font-size: 18px;
    min-height: 60px;
}

/* Teddy images */
.hug-img {
    width: 140px;
    margin: 10px auto;
    display: block;
    filter: drop-shadow(0 10px 20px rgba(0,0,0,0.35));
    animation: float 3s ease-in-out infinite;
}

@keyframes float {
    0% { transform: translateY(0); }
    50% { transform: translateY(-6px); }
    100% { transform: translateY(0); }
}

button {
    padding: 12px 24px;
    border: none;
    border-radius: 30px;
    background: white;
    color: #ff4f81;
    font-size: 16px;
    cursor: pointer;
    margin-top: 12px;
    transition: 0.3s;
}

button:hover { transform: scale(1.05); }

.hidden { display: none; }

.game-area {
    position: relative;
    height: 120px;
}

#yesBtn { position: absolute; left: 10%; top: 40px; }
#noBtn { position: absolute; right: 10%; top: 40px; }

.quiz-option {
    display: block;
    margin: 8px auto;
    width: 85%;
}

/* Countdown */
.countdown {
    margin-top: 10px;
    font-size: 16px;
    background: rgba(255,255,255,0.15);
    padding: 10px;
    border-radius: 15px;
}

/* Floating hearts */
.heart, .sparkle {
    position: absolute;
    bottom: -10px;
    pointer-events: none;
}

.heart {
    animation: floatUp 6s linear infinite;
}

.sparkle {
    animation: sparkleFloat 4s linear infinite;
    text-shadow: 0 0 10px rgba(255,255,255,0.8);
}

@keyframes floatUp {
    from { transform: translateY(0); opacity: 0.8; }
    to { transform: translateY(-110vh); opacity: 0; }
}

@keyframes sparkleFloat {
    from { transform: translateY(0) scale(0.8); opacity: 0; }
    50% { opacity: 1; }
    to { transform: translateY(-80vh) scale(1.2); opacity: 0; }
}
</style>
</head>

<body>

<div class="card">
    <h1>NNI ❤️</h1>

    <div class="typing" id="typing"></div>

    <img class="hug-img" src="https://i.imgur.com/3ZQ3Z4O.png">

    <div class="countdown">
        ⏳ Counting every heartbeat till 25 Feb 💕<br>
        <span id="timer"></span>
    </div>

    <button onclick="startProposal()">Continue 💌</button>

    <!-- Proposal -->
    <div id="proposal" class="hidden">
        <p>Will you be BEEBO’s Valentine? 🥺💖</p>
        <div class="game-area">
            <button id="yesBtn" onclick="startQuiz()">Yes 💕</button>
            <button id="noBtn" onmouseover="runAway()">No 🙈</button>
        </div>
    </div>

    <!-- Quiz -->
    <div id="quiz" class="hidden">
        <p>Mini Love Quiz 😌💞<br>Who loves you the most?</p>
        <button class="quiz-option" onclick="wrong()">Someone Else 😜</button>
        <button class="quiz-option" onclick="wrong()">Secret Admirer 🤭</button>
        <button class="quiz-option" onclick="finalWin()">BEEBO Obviously 💖</button>
    </div>

    <!-- Final -->
    <div id="final" class="hidden">
        <p style="font-size:20px;">
            YAYYY NNI !!! ❤️✨<br><br>
            Sending You Infinite Hugs 🤗💞<br>
            NNI + BEEBO = Forever 🥰<br><br>
            See You On 25 Feb 😘
        </p>
        <img class="hug-img" src="https://i.imgur.com/JqEuJ6t.png">
    </div>
</div>

<script>
// Typewriter
const message = "Happy Valentine’s Day My Love 💕 You are my happiness, my heart, my everything.";
let i = 0;

function typeText() {
    if (i < message.length) {
        document.getElementById("typing").innerHTML += message.charAt(i);
        i++;
        setTimeout(typeText, 55);
    }
}
typeText();

// Countdown
const targetDate = new Date("Feb 25, 2026 00:00:00").getTime();

function updateTimer() {
    const now = new Date().getTime();
    const diff = targetDate - now;

    if (diff <= 0) {
        document.getElementById("timer").innerHTML = "Finally together ❤️";
        return;
    }

    const d = Math.floor(diff / (1000*60*60*24));
    const h = Math.floor((diff / (1000*60*60)) % 24);
    const m = Math.floor((diff / (1000*60)) % 60);
    const s = Math.floor((diff / 1000) % 60);

    document.getElementById("timer").innerHTML =
        d + " Days 💖 " + h + " Hrs ✨ " + m + " Min 💕 " + s + " Sec";
}
setInterval(updateTimer, 1000);
updateTimer();

// Flow logic
function startProposal() {
    document.getElementById("proposal").style.display = "block";
}

function runAway() {
    const btn = document.getElementById("noBtn");
    btn.style.left = Math.random() * 250 + "px";
    btn.style.top = Math.random() * 80 + "px";
}

function startQuiz() {
    document.getElementById("proposal").style.display = "none";
    document.getElementById("quiz").style.display = "block";
}

function wrong() {
    alert("Wrong answer NNI 😌 Try again 💕");
}

function finalWin() {
    document.getElementById("quiz").style.display = "none";
    document.getElementById("final").style.display = "block";
}

// Hearts
function createHeart() {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "❤️";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = (Math.random()*20 + 16) + "px";
    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 6000);
}
setInterval(createHeart, 350);

// Sparkles
function createSparkle() {
    const sp = document.createElement("div");
    sp.className = "sparkle";
    sp.innerHTML = "✨";
    sp.style.left = Math.random() * 100 + "vw";
    sp.style.fontSize = (Math.random()*10 + 14) + "px";
    document.body.appendChild(sp);
    setTimeout(() => sp.remove(), 4000);
}
setInterval(createSparkle, 200);
</script>

</body>
</html>
