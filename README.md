# <!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Rea 🎂💖</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif;}
body{
    height:100vh;
    overflow:hidden;
    display:flex;
    justify-content:center;
    align-items:center;
    background:linear-gradient(-45deg,#ff9ecf,#ff6fb5,#ffc0e6,#d89bff,#ffd6a5);
    background-size:400% 400%;
    animation:gradientMove 12s ease infinite;
    transition:0.8s ease;
}
@keyframes gradientMove{
    0%{background-position:0% 50%}
    50%{background-position:100% 50%}
    100%{background-position:0% 50%}
}
.container{
    width:90%;
    max-width:900px;
    background:rgba(255,255,255,0.2);
    backdrop-filter:blur(15px);
    padding:40px;
    border-radius:25px;
    text-align:center;
    color:white;
    box-shadow:0 20px 50px rgba(0,0,0,0.2);
    position:relative;
}
h1{font-size:36px;margin-bottom:20px;}
button{
    padding:12px 25px;
    border:none;
    border-radius:25px;
    margin:10px;
    cursor:pointer;
    font-size:16px;
    background:white;
    color:#ff4fa3;
}
button:hover{ transform:scale(1.1); }
.hidden{ display:none; }
.blur{ filter:blur(10px); }
#noBtn{ position:relative; }

/* confetti */
.confetti{
    position:absolute;
    animation:fall 4s linear infinite;
}
@keyframes fall{
    0%{transform:translateY(-10vh);opacity:1}
    100%{transform:translateY(100vh);opacity:0}
}

/* FOTO SECTION 10 FOTO */
.photo-grid{
    margin-top:20px;
    display:grid;
    grid-template-columns:repeat(5,1fr);
    gap:10px;
}
.photo-grid img{
    width:100%;
    border-radius:15px;
    height:120px;
    object-fit:cover;
    border:3px solid white;
}

/* LILIN */
.candle{
    width:10px;
    height:50px;
    background:#ffe066;
    margin:10px auto;
    position:relative;
    border-radius:3px;
}
.flame{
    width:12px;
    height:20px;
    background:orange;
    position:absolute;
    top:-18px;
    left:-1px;
    border-radius:50%;
    filter:blur(1px);
    animation:flameAnim 0.4s ease-in-out infinite alternate;
}
@keyframes flameAnim{
    0%{transform:scaleY(1) translateY(0)}
    100%{transform:scaleY(1.3) translateY(-3px)}
}

/* TYPING TEXT */
#romanticText{
    font-size:20px;
    margin-top:20px;
    min-height:50px;
}
</style>
</head>

<body>

<div class="container" id="slide1">
    <h1>Happy Birthday Rea 🎂💖.....</h1>
    <p> semoga kamu suka ya by...</p>
    <button onclick="showChoice()">Liat 💗</button>
</div>

<div class="container hidden" id="slide2">
    <h1>Mau lanjut nggak ni? </h1>
    <button onclick="showPassword()">Mauuu</button>
    <button id="noBtn">No thanks</button>
</div>

<div class="container hidden" id="slide3">
    <h1>Password dulu yaa </h1>
    <input type="password" id="pw" placeholder="Masukin password...">
    <br><br>
    <button onclick="checkPw()">Masuk</button>
    <p id="wrong"></p>
</div>

<div class="container hidden" id="slide4">
    <h1>🎉 HAPPY BIRTHDAY 🎉</h1>
    <p>Semoga semua impian kamu tercapai ✨</p>
    <br>
    <button onclick="showFinal()">Liat Kenangan 📸</button>
</div>

<div class="container hidden" id="slide5">
    <h1>Kenangan Kita 💕</h1>
    <!-- LILIN + FLAME + IKON -->
    <div class="candle"><div class="flame"></div></div>
    <div id="romanticText"></div>

    <!-- FOTO 10 SLOT -->
    <div class="danendra-my">
        <img src="perpus.jpeg">
        <img src="foto2.jpg">
        <img src="foto3.jpg">
        <img src="foto4.jpg">
        <img src="foto5.jpg">
        <img src="foto6.jpg">
        <img src="foto7.jpg">
        <img src="foto8.jpg">
        <img src="foto9.jpg">
        <img src="foto10.jpg">
    </div>
</div>

<script>
let noBtn=document.getElementById("noBtn");
noBtn.addEventListener("mouseover",function(){
    let x=Math.random()*300-150;
    let y=Math.random()*300-150;
    noBtn.style.transform=`translate(${x}px,${y}px)`;
});

function blurTransition(next){
    document.body.classList.add("blur");
    setTimeout(()=>{
        document.querySelectorAll(".container").forEach(el=>el.classList.add("hidden"));
        document.getElementById(next).classList.remove("hidden");
        document.body.classList.remove("blur");
    },700);
}

function showChoice(){ blurTransition("slide2"); }
function showPassword(){ blurTransition("slide3"); }

function checkPw(){
    let input=document.getElementById("pw").value;
    if(input==="sacin ui"){
        playHappyBirthdayLoop();
        blurTransition("slide4");
        startConfetti();
    }else{
        document.getElementById("wrong").innerText="Salahhh by 😭 coba lagi";
    }
}

function showFinal(){ 
    blurTransition("slide5");
    startTyping();
    startConfetti();
}

/* 🎵 HAPPY BIRTHDAY LOOP */
let ctx;
function playHappyBirthdayLoop(){
    if(ctx) return;
    ctx = new (window.AudioContext || window.webkitAudioContext)();

    const notes = [
        264,264,297,264,352,330,
        264,264,297,264,396,352,
        264,264,528,440,352,330,297,
        466,466,440,352,396,352
    ];
    const durations = [
        0.45,0.45,0.45,0.45,0.7,0.7,
        0.45,0.45,0.45,0.45,0.7,0.7,
        0.45,0.45,0.45,0.7,0.45,0.45,0.45,
        0.45,0.45,0.7,0.45,0.7,0.7
    ];

    let i = 0;
    function playNext(){
        if(i>=notes.length) i=0;
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type="sine";
        osc.frequency.value = notes[i];
        osc.connect(gain);
        gain.connect(ctx.destination);
        gain.gain.setValueAtTime(0.25, ctx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + durations[i]);
        osc.start(ctx.currentTime);
        osc.stop(ctx.currentTime + durations[i]);
        setTimeout(playNext, durations[i]*1000);
        i++;
    }
    playNext();
}

/* TYPING EFFECT */
const text="Rea, kamu itu selalu bikin hari-hariku lebih berwarna 🎉🎂💖🌸";
function startTyping(){
    let i=0;
    let el=document.getElementById("romanticText");
    el.innerHTML="";
    function typeChar(){
        if(i<text.length){
            el.innerHTML += text[i];
            i++;
            setTimeout(typeChar,50);
        }
    }
    typeChar();
}

/* confetti */
function startConfetti(){
    setInterval(()=>{
        let c=document.createElement("div");
        c.classList.add("confetti");
        const icons=["🎉","🎂","💖","🌸"];
        c.innerHTML = icons[Math.floor(Math.random()*icons.length)];
        c.style.left=Math.random()*100+"vw";
        c.style.fontSize=(Math.random()*25+15)+"px";
        document.body.appendChild(c);
        setTimeout(()=>{c.remove()},4000);
    },200);
}
</script>
</body>
</html>
