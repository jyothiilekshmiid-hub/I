<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">

<!-- Mobile-only viewport -->
<meta name="viewport" content="width=device-width, height=device-height, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<!-- App-like behavior -->
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#ff69b4">

<title>Be My Valentine 💘</title>

<style>
html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    touch-action: manipulation;
    overscroll-behavior: none;
    font-family: 'Comic Sans MS', 'Arial Rounded MT Bold', cursive;
}

body {
    background: linear-gradient(135deg, #ffb6c1, #ffc0cb);
    display: flex;
    align-items: center;
    justify-content: center;
}

.screen {
    display: none;
    width: 100%;
    height: 100%;
    padding: 20px;
    text-align: center;
}

.active {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.question {
    font-size: 1.6rem;
    color: #c71585;
    max-width: 90%;
    line-height: 1.4;
}

.yes-word {
    color: #ff1493;
    font-weight: bold;
    text-decoration: underline;
    padding: 8px 12px;
}

.no-button {
    position: absolute;
    min-width: 140px;
    min-height: 60px;
    font-size: 1.5rem;
    border: none;
    border-radius: 40px;
    background-color: #ff69b4;
    color: white;
    box-shadow: 0 6px 12px rgba(0,0,0,0.25);
}

.wrong-box {
    background: #ff69b4;
    padding: 40px 25px;
    border-radius: 25px;
    color: white;
}

.wrong-box h1 {
    font-size: 2.8rem;
    margin-bottom: 20px;
}

.try-btn {
    font-size: 1.3rem;
    padding: 14px 30px;
    border: none;
    border-radius: 30px;
    background: white;
    color: #ff1493;
}

.yay {
    background: linear-gradient(135deg, #ffd1dc, #ff9ecf);
    padding: 50px 30px;
    border-radius: 30px;
}

.yay h1 {
    font-size: 3.2rem;
    color: #ff1493;
}

.bow {
    position: absolute;
    font-size: 2.2rem;
    animation: float 6s infinite ease-in-out;
}

@keyframes float {
    0% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
    100% { transform: translateY(0); }
}
</style>
</head>

<body>

<!-- QUESTION SCREEN -->
<div class="screen active" id="questionScreen">
    <div class="question">
        Will you be my valentine, Dev?  
        I’ll give you kisses if you say
        <span class="yes-word" onclick="showYay()">yes</span> 💋
    </div>

    <button class="no-button" id="no1" ontouchstart="moveNo(this)">No</button>
    <button class="no-button" id="no2" ontouchstart="moveNo(this)">No</button>
</div>

<!-- WRONG SCREEN -->
<div class="screen" id="wrongScreen">
    <div class="wrong-box">
        <h1>❌ WRONG ANSWER ❌</h1>
        <button class="try-btn" ontouchstart="goBack()">Try Again</button>
    </div>
</div>

<!-- YAY SCREEN -->
<div class="screen" id="yayScreen">
    <div class="yay">
        <h1>🎀 YAYYYYYYY 🎀</h1>
    </div>

    <div class="bow" style="top:10%; left:10%;">🎀</div>
    <div class="bow" style="top:20%; right:15%;">🎀</div>
    <div class="bow" style="bottom:15%; left:20%;">🎀</div>
    <div class="bow" style="bottom:10%; right:10%;">🎀</div>
</div>

<script>
// Lock portrait if possible
if (screen.orientation && screen.orientation.lock) {
    screen.orientation.lock("portrait").catch(() => {});
}

const noButtons = document.querySelectorAll(".no-button");

function randomPosition(btn) {
    const padding = 80;
    const maxX = window.innerWidth - padding;
    const maxY = window.innerHeight - padding;

    const x = Math.random() * maxX;
    const y = Math.random() * maxY;

    btn.style.left = x + "px";
    btn.style.top = y + "px";
}

function moveNo(btn) {
    randomPosition(btn);
    navigator.vibrate?.(50);
}

function showWrong() {
    questionScreen.classList.remove("active");
    wrongScreen.classList.add("active");
}

function showYay() {
    questionScreen.classList.remove("active");
    yayScreen.classList.add("active");
}

function goBack() {
    wrongScreen.classList.remove("active");
    questionScreen.classList.add("active");
    noButtons.forEach(btn => randomPosition(btn));
}

// Initial placement
noButtons.forEach(btn => randomPosition(btn));
</script>

</body>
</html>
