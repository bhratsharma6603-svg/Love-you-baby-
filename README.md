<!doctype html>
<html lang="hi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>💖 Proposal — Will you be mine again?</title>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@500;700&family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
  <style>
    :root{--accent:#ff6b81;--bg:#05060a}
    *{box-sizing:border-box}
    body{margin:0;background:var(--bg);color:#fff;font-family:'Poppins',system-ui,Arial;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:20px}
    .stage{width:100%;max-width:900px;border-radius:18px;padding:24px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));box-shadow:0 12px 40px rgba(0,0,0,0.6);position:relative;overflow:hidden}
    .hearts-bg{position:absolute;inset:0;pointer-events:none;z-index:0}
    .heart{position:absolute;color:#ff4d6d;font-size:26px;opacity:.14;animation:floatUp 8s linear infinite}
    @keyframes floatUp{0%{transform:translateY(40vh) scale(.6);opacity:0}10%{opacity:.6}50%{opacity:.95}100%{transform:translateY(-30vh) scale(1.2);opacity:0}}
    .header{position:relative;z-index:2;display:flex;flex-direction:column;align-items:center;gap:12px}
    .sticker{width:220px;height:220px;border-radius:50%;background:radial-gradient(circle at 30% 20%, #fff, #ffeef5 60%);display:flex;align-items:center;justify-content:center;box-shadow:0 10px 30px rgba(0,0,0,0.6);transform-origin:center;animation:float 4s ease-in-out infinite}
    @keyframes float{0%{transform:translateY(0)}50%{transform:translateY(-12px)}100%{transform:translateY(0)}}
    .speech{font-family:'Dancing Script',cursive;font-size:36px;color:var(--bg);transform:rotate(-6deg);background:linear-gradient(90deg,#fff,#ffeef5);padding:8px 12px;border-radius:10px;box-shadow:0 6px 16px rgba(0,0,0,0.25)}
    .controls{display:flex;gap:12px;align-items:center;flex-direction:column;margin-top:6px}
    .btn{padding:12px 22px;border-radius:999px;border:none;background:var(--accent);color:#fff;font-weight:700;cursor:pointer;box-shadow:0 8px 18px rgba(0,0,0,0.35);font-size:18px}
    .message-wrap{margin-top:18px;display:none;flex-direction:column;gap:12px;align-items:center;z-index:2}
    .message-card{width:100%;background:rgba(0,0,0,0.45);border-radius:14px;padding:20px;text-align:left;position:relative}
    .message-text{font-family:'Dancing Script',cursive;font-size:26px;color:#ffeef3;line-height:1.35;white-space:pre-wrap;opacity:0;transform:translateY(6px);transition:all 700ms ease}
    .message-text.show{opacity:1;transform:translateY(0)}
    .stickers{display:flex;gap:10px;flex-wrap:wrap;margin-top:6px}
    .sticker-mini{width:56px;height:56px;border-radius:12px;background:linear-gradient(180deg,#fff2,#fff1);display:flex;align-items:center;justify-content:center;font-size:26px;color:#ff6b81;box-shadow:0 8px 20px rgba(0,0,0,0.35)}
    .hint{font-size:13px;opacity:.9;color:#f3c7d0;margin-top:6px}
    @media (max-width:520px){.sticker{width:160px;height:160px}.speech{font-size:28px}.message-text{font-size:20px}}
    /* small loader text for starting */
    .starting{font-size:14px;color:#fff;opacity:.9}
  </style>
</head>
<body>
  <div class="stage" role="application" aria-label="Proposal card">
    <div class="hearts-bg" aria-hidden="true"></div>

    <div class="header">
      <div class="sticker" id="panda">
        <!-- panda svg -->
        <svg viewBox="0 0 200 200" width="160" height="160" xmlns="http://www.w3.org/2000/svg">
          <defs><linearGradient id="g" x1="0" x2="0" y1="0" y2="1"><stop offset="0" stop-color="#fff"/><stop offset="1" stop-color="#ffeef0"/></linearGradient></defs>
          <rect width="100%" height="100%" rx="80" fill="url(#g)"/>
          <g transform="translate(100,100)">
            <circle cx="0" cy="0" r="42" fill="#fff" stroke="#000" stroke-opacity="0.06"/>
            <circle cx="-18" cy="-8" r="10" fill="#000"/>
            <circle cx="18" cy="-8" r="10" fill="#000"/>
            <ellipse cx="0" cy="12" rx="12" ry="8" fill="#000"/>
            <circle cx="-46" cy="-40" r="18" fill="#000"/>
            <circle cx="46" cy="-40" r="18" fill="#000"/>
            <g id="heart" transform="translate(36,38) scale(.8)">
              <path d="M0 0 C 0 -6 6 -10 12 -10 C 18 -10 24 -6 24 0 C 24 10 12 18 12 18 C 12 18 0 10 0 0 Z" fill="#ff6b81" opacity="0.95">
                <animate attributeName="transform" values="scale(.9);scale(1.08);scale(.9)" dur="1.6s" repeatCount="indefinite"/>
              </path>
            </g>
          </g>
        </svg>
      </div>

      <div class="speech">I ♥ YOU</div>

      <div class="controls">
        <button id="nextBtn" class="btn" aria-label="Next">Next</button>
        <div id="status" class="hint">Tap "Next" — music will start and your letter will appear</div>
      </div>
    </div>

    <div id="messageWrap" class="message-wrap" aria-hidden="true">
      <div class="message-card">
        <div id="messageText" class="message-text" aria-live="polite"></div>
      </div>
      <div class="stickers" id="stickersRow">
        <div class="sticker-mini">💖</div>
        <div class="sticker-mini">💍</div>
        <div class="sticker-mini">❤️</div>
        <div class="sticker-mini">🤍</div>
      </div>
    </div>

    <!-- audio (Google Drive direct download link) -->
    <audio id="song" preload="auto"></audio>
  </div>

  <script>
    // CONFIG: put your Google Drive FILE_ID here (from the link)
    const FILE_ID = '18XTBOmqQjJOIUYU7Us_5uZjsuQQgPBql';
    const DRIVE_DL = `https://docs.google.com/uc?export=download&id=${FILE_ID}`;

    // hearts background
    const heartsBg = document.querySelector('.hearts-bg');
    for(let i=0;i<18;i++){
      const s = document.createElement('div');
      s.className = 'heart';
      s.style.left = Math.random()*100 + '%';
      s.style.top = (40 + Math.random()*50) + '%';
      s.style.fontSize = (18 + Math.random()*36) + 'px';
      s.style.animationDuration = (6 + Math.random()*8) + 's';
      s.style.opacity = 0.04 + Math.random()*0.25;
      s.textContent = '❤';
      heartsBg.appendChild(s);
    }

    // love letter
    const fullText = `💖 My Love Letter to You 💖\n\nDear Anushka,\n\nKabhi socha nahi tha ki main tujhe dobara propose karunga…\nLekin dil ke kuch jazbaat aise hote hain jo baar-baar kehne ka mann karta hai. Shayad har din ke sath tera liye mera pyaar aur gehra hota ja raha hai… aur shayad issi liye main fir se tujhe “I Love You” kehne se khud ko rok nahi pa raha. 💞\n\nSabse pehle — Sorry.\nSorry agar kabhi meri kisi baat ne tujhe hurt kiya ho, agar main kabhi tujhe samajh nahi paaya, ya kabhi tere emotions ko ignore kar diya ho.\nMujhe pata hai main perfect nahi hoon, lekin har din main yahi seekh raha hoon ki tujhe khush kaise rakhun.\nDil se keh raha hoon Anushka — mera dil sirf tujhse hi juda hai. ❤️\n\nTere bina sab kuch adhoora lagta hai.\nTere bina hasi bhi aadhi lagti hai, aur har din be-rang sa lagta hai.\nTu meri zindagi ka woh hissa hai jise main chhod nahi sakta — chahe jitni bhi doori ho, chahe kitni bhi baatein galat samajh li gayi ho.\n\nAaj main fir se ek chhoti si baat, bada dil lekar kehna chahta hoon…\n\n💍 Will you be mine again, Anushka? 💍\n\nMain chahta hoon ki hum apne purane lamhon se seekh kar ek nayi shuruaat karein —\njahan sirf trust, pyaar aur ek dusre ka saath ho. Mujhe fir se woh mauka de ki main tujhe har din woh feel kara sakun jo ek perfect love story mein hota hai.\n\nTere bina main apni duniya imagine bhi nahi kar sakta. Tu meri har dua ka sabse khoobsurat hissa hai.\nAur main wada karta hoon, ab se har pal tera khayal rakhunga —\ntere aansuon se pehle muskura dunga,\naur tere gusse se pehle tujhe gale laga lunga. 🤍\n\nBas ek baar keh de…\n“Haan, main fir se teri hoon.”\nAur fir main duniya ka sabse khush-naseeb insaan ban jaunga.\n\nI love you, Anushka — not just today, but every day, in every way, for the rest of my life. 💌\n\nAlways yours,\nBhrat Sharma 💖`;

    const nextBtn = document.getElementById('nextBtn');
    const songEl = document.getElementById('song');
    const status = document.getElementById('status');
    const messageWrap = document.getElementById('messageWrap');
    const messageText = document.getElementById('messageText');

    // set an initial src to try direct (many times works)
    songEl.src = DRIVE_DL;

    function typeText(text, element, cb){
      element.innerHTML = '';
      let i = 0;
      function step(){
        if(i >= text.length){ if(cb) cb(); return; }
        const ch = text[i++];
        if(ch === '\n'){
          element.innerHTML += '<br/>';
          setTimeout(step, 200);
        } else {
          element.innerHTML += ch;
          setTimeout(step, 26);
        }
      }
      step();
    }

    // Robust play function: try normal play; if fails, fetch blob and play
    async function robustPlay(){
      try{
        await songEl.play();
        return true;
      }catch(err){
        // try to fetch and create blob URL (user gesture present)
        status.innerText = 'Starting music (preparing)...';
        try{
          const resp = await fetch(DRIVE_DL, {mode:'cors'});
          if(!resp.ok) throw new Error('fetch-failed');
          const blob = await resp.blob();
          const blobUrl = URL.createObjectURL(blob);
          songEl.src = blobUrl;
          await songEl.play();
          return true;
        }catch(e){
          console.warn('Fallback fetch failed:', e);
          return false;
        }
      }
    }

    nextBtn.addEventListener('click', async ()=>{
      nextBtn.disabled = true;
      nextBtn.innerText = 'Starting...';
      status.innerText = 'Starting music...';

      const ok = await robustPlay();
      if(!ok){
        // final fallback: show manual play button
        status.innerHTML = 'Audio could not start automatically. <button id="manualPlay" class="btn">Play Song</button>';
        const btn = document.getElementById('manualPlay');
        btn.addEventListener('click', async ()=>{
          try{ await songEl.play(); btn.remove(); status.innerText = ''; startLetter(); }
          catch(e){ alert('Audio playback failed — try in a different browser/device.'); }
        });
        nextBtn.style.display = 'none';
        return;
      }

      // music started -> show letter
      startLetter();
    });

    function startLetter(){
      // show message area and type
      messageWrap.style.display = 'flex';
      messageWrap.setAttribute('aria-hidden','false');
      messageText.classList.add('show');
      typeText(fullText, messageText, ()=>{
        // finished typing
        status.innerText = '';
        nextBtn.style.display = 'none';
      });
    }

    // accessibility: allow Enter to trigger
    nextBtn.addEventListener('keyup', (e)=>{ if(e.key === 'Enter') nextBtn.click(); });

    // small note: if user navigates away or audio blocked, instructions will show
    window.addEventListener('error', (e)=> console.error(e));
  </script>
</body>
</html>
