<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>💖 Proposal — Final Version</title>
<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
<style>
:root{
    --bg1: #fff1f6;
    --bg2: #f0feff;
    --accent:#ff3b7d;
    --muted:#6b6b6b;
}
*{box-sizing:border-box;}
body{
    margin:0;
    min-height:100vh;
    font-family:"Poppins",sans-serif;
    background: linear-gradient(135deg,var(--bg1) 0%, var(--bg2) 100%);
    display:flex;
    align-items:center;
    justify-content:center;
    padding:20px;
    color:#222;
    overflow:hidden;
}
.stage{
    width:100%;
    max-width:820px;
    background: rgba(255,255,255,0.6);
    border-radius:20px;
    padding:26px;
    box-shadow: 0 18px 40px rgba(12,18,35,0.12);
    position:relative;
    overflow:visible;
    text-align:center;
}
.hearts{
    pointer-events:none;
    position:absolute;
    left:0;top:0;right:0;bottom:0;
    z-index:1;
    overflow:visible;
}
#kittyWrap{position:relative;z-index:2}
#kitty{
    width:180px;height:180px;display:block;margin:12px auto;
    filter: drop-shadow(0 10px 30px rgba(0,0,0,0.18));
    animation: kittyFloat 3.4s ease-in-out infinite;
}
@keyframes kittyFloat{
    0%,100%{ transform:translateY(0) }
    50%{ transform:translateY(-12px) }
}
h1{
    font-family:'Great Vibes', cursive;
    font-size:34px;
    margin:6px 0 4px 0;
    color:var(--accent);
    z-index:2;
    position:relative;
}
p.lead{color:var(--muted); margin:0 0 14px 0; z-index:2; position:relative}
#letterWrap{
    display:none;
    margin-top:22px;
    z-index:2;
    position:relative;
}
#letter{
    background:rgba(255,255,255,0.92);
    border-radius:12px;
    padding:20px;
    max-height:58vh;
    overflow:auto;
    text-align:left;
    font-family:'Great Vibes', cursive;
    font-size:18px;
    color:#2b2b2b;
    line-height:1.6;
    box-shadow:0 12px 30px rgba(12,18,35,0.06);
}
.fade-in{ animation: fadeIn 1.6s ease forwards; opacity:0 }
@keyframes fadeIn{ to { opacity:1 } }
.heart {
    position:absolute;
    width:18px;
    height:18px;
    transform:translate(-50%,-50%) rotate(-20deg);
    pointer-events:none;
    opacity:0.95;
    will-change: transform, opacity;
    filter: drop-shadow(0 6px 18px rgba(0,0,0,0.12));
}
@media (max-width:440px){
    #kitty{width:140px;height:140px}
    h1{font-size:28px}
    #letter{font-size:16px}
}
.dim::before{
    content:'';
    position:absolute;left:0;right:0;top:0;bottom:0;
    background:rgba(255,255,255,0.3);
    backdrop-filter: blur(6px);
    z-index:1;
    border-radius:20px;
}
.btn{
    display:inline-block;
    border:0;
    padding:10px 18px;  
    border-radius:999px;
    font-weight:600;
    cursor:pointer;
    font-family:'Great Vibes', cursive;
    font-size:16px;  
    transition: all 0.3s ease;
}
.btn.start{
    background: linear-gradient(45deg,#ff3b7d,#ff7aa3);
    color:white;
    box-shadow:0 8px 20px rgba(255,59,125,0.4);
}
.btn.start:hover{
    transform:scale(1.05);
    box-shadow:0 10px 25px rgba(255,59,125,0.5);
}
.btn.next{
    background:#ffd1e6;
    color:#ff3b7d;
    border:2px solid #ff3b7d;
}
.btn.next:hover{
    background:#ff3b7d;
    color:white;
}
.controls#controls {
    margin-top:14px;
    display:flex;
    justify-content:center;
    align-items:center;
}
.controls#letterButtons {
    display:none;
    justify-content:space-between;
    margin-top:12px;
}
</style>
</head>
<body>
<div class="stage" id="stage">
    <div class="hearts" id="hearts"></div>
    <div id="kittyWrap">
      <!-- Updated with your GIF -->
      <img id="kitty" src="https://www.dropbox.com/scl/fi/odhoi925s552dm3tzdaur/d4e920e6b0da6b5fb8e947e458e876cc.gif?rlkey=v0vepe0ckgh76hwoa9lxjcpim&st=svyu9crh&dl=1" alt="Love Sticker">
      <h1>💖 My Love Letter to You 💖</h1>
      <p class="lead">A small surprise for Anushka — made with all my heart</p>
    </div>
    <div class="controls" id="controls">
      <button class="btn start" id="startBtn">Play Song & Start</button>
    </div>
    <div id="letterWrap">
        <div id="letter" aria-live="polite"></div>
        <div class="controls" id="letterButtons">
            <button class="btn next" id="replayBtn">Replay 🔄</button>
            <button class="btn next" id="nextBtn">Next Part 💌</button>
        </div>
    </div>
</div>

<audio id="bgAudio" preload="auto">
  <source src="https://www.dropbox.com/scl/fi/uzrtw8vbtbfwxdbfz4a61/I-Wanna-Be-Yours-22.mp3?rlkey=lc0ueze8sl4pgchb1rp9cafi4&st=s3kedg19&dl=1" type="audio/mpeg">
</audio>

<script>
const HEART_FREQ = 700;
const HEART_COLORS = ['#ff9ccf','#ff6ea8','#ff3b7d','#ffd1e6','#ffb3c6'];
const startBtn = document.getElementById('startBtn');
const nextBtn = document.getElementById('nextBtn');
const replayBtn = document.getElementById('replayBtn');
const letterWrap = document.getElementById('letterWrap');
const letterEl = document.getElementById('letter');
const letterButtons = document.getElementById('letterButtons');
const bgAudio = document.getElementById('bgAudio');
const heartsContainer = document.getElementById('hearts');
const stage = document.getElementById('stage');

const parts = [
`💖 My Love Letter to You 💖<br><br>
Dear Anushka,<br><br>
Kabhi socha nahi tha ki main tujhe dobara propose karunga…<br>
Lekin dil ke kuch jazbaat aise hote hain jo baar-baar kehne ka mann karta hai…`,

`Sabse pehle — Sorry.<br>
Sorry agar kabhi meri kisi baat ne tujhe hurt kiya ho…<br>
Mujhe pata hai main perfect nahi hoon, lekin har din main yahi seekh raha hoon ki tujhe khush kaise rakhun.<br>
Dil se keh raha hoon Anushka — mera dil sirf tujhse hi juda hai. ❤️`,

`Tere bina sab kuch adhoora lagta hai.<br>
Tu meri zindagi ka woh hissa hai jise main chhod nahi sakta…<br>
💍 Will you be mine again, Anushka? 💍<br>
I love you, Anushka — not just today, but every day, in every way, for the rest of my life. 💌<br>
Always yours,<br>Bhrat Sharma 💖`
];

let currentPart = 0;

function typeText(text, cb){
    letterEl.innerHTML='';
    let i=0;
    function step(){
        if(i>=text.length){ cb && cb(); return;}
        if(text[i]==='<'){
            const closeIndex = text.indexOf('>',i);
            letterEl.innerHTML += text.slice(i,closeIndex+1);
            i = closeIndex+1;
        } else {
            letterEl.innerHTML += text[i];
            i++;
        }
        setTimeout(step,14);
    }
    step();
}

let heartInterval=null;
function spawnHeart(){
    const h=document.createElement('div');
    h.className='heart';
    const size=Math.random()*18+12;
    h.style.width=size+'px';
    h.style.height=size+'px';
    const color=HEART_COLORS[Math.floor(Math.random()*HEART_COLORS.length)];
    h.innerHTML=`<svg viewBox="0 0 512 512" width="${size}" height="${size}"><path fill="${color}" d="M471.701 73.604c-54.65-46.259-136.96-38.39-188.904 13.904L256 114.277l-26.797-26.769C178.955 35.214 96.646 27.345 41.995 73.604-9.018 118.004-10.688 196.2 27.55 242.9l194.63 209.369c6.965 7.486 18.091 7.486 25.056 0L484.45 242.9c38.238-46.7 36.568-124.896-12.749-169.296z"/></svg>`;
    const left=Math.random()*100;
    h.style.left=left+'%';
    h.style.bottom='-10%';
    heartsContainer.appendChild(h);
    const duration=Math.random()*6000+9000;
    const drift=(Math.random()*80-40);
    const start=performance.now();
    function animate(now){
        const t=(now-start)/duration;
        if(t>=1){ h.remove(); return;}
        const y=t*140;
        const x=drift*Math.sin(t*Math.PI*2);
        const scale=0.7+0.6*Math.sin(t*Math.PI);
        h.style.transform=`translate(${x}px, ${-y}%) scale(${scale}) rotate(${t*40}deg)`;
        h.style.opacity=1-t*0.92;
        requestAnimationFrame(animate);
    }
    requestAnimationFrame(animate);
}
function startHearts(){ if(!heartInterval) heartInterval=setInterval(spawnHeart,HEART_FREQ);}
function stopHearts(){ if(heartInterval){ clearInterval(heartInterval); heartInterval=null; }}

startBtn.addEventListener('click',()=>{
    startBtn.style.display='none';
    letterWrap.style.display='block';
    letterButtons.style.display='flex';
    stage.classList.add('dim');
    startHearts();
    bgAudio.play().catch(()=>{});
    typeText(parts[currentPart]);
});

nextBtn.addEventListener('click',()=>{
    currentPart++;
    if(currentPart<parts.length){
        typeText(parts[currentPart]);
    }
    if(currentPart===parts.length-1){
        nextBtn.style.display='none';
    }
});

replayBtn.addEventListener('click',()=>{
    currentPart = 0;
    typeText(parts[currentPart],()=>{ nextBtn.style.display='inline-block'; });
    bgAudio.currentTime=0;
    bgAudio.play();
});
</script>
</body>
</html>
