<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Goodbye 2025, Hello 2026 </title>
<style>
  body {
    margin: 0;
    font-family: 'Georgia', serif;
    background: linear-gradient(180deg, #f6efe9, #fdfaf7);
    color: #3b2f2f;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    overflow: hidden;
  }

  .page { display: none; max-width: 720px; padding: 2.5rem; text-align: center; animation: fadeIn 0.9s ease; }
  .page.active { display: block; }
  h1 { font-size: 2.2rem; margin-bottom: 1rem; }
  p { font-size: 1.1rem; line-height: 1.6; margin-bottom: 1.8rem; }
  textarea { width: 100%; height: 120px; padding: 1rem; border-radius: 14px; border: 1px solid #d8cfc8; font-family: inherit; font-size: 1rem; background: #fffaf6; resize: none; }
  button { margin-top: 1.6rem; padding: 0.8rem 2.2rem; font-size: 1rem; border: none; border-radius: 30px; background: #c7a17a; color: white; cursor: pointer; transition: all 0.3s ease; }
  button:hover { background: #b08968; transform: translateY(-2px); }
  .emoji { font-size: 2.2rem; margin-bottom: 0.8rem; }

  .letter { background: #fffaf6; padding: 1.6rem; border-radius: 14px; border: 1px solid #e3d9d2; margin-bottom: 1.8rem; position: relative; cursor: pointer; transition: all 2s ease; }
  .flames { position: absolute; bottom: -10px; left: 50%; transform: translateX(-50%); font-size: 2.8rem; opacity: 0; animation: erupt 0.5s infinite alternate; }
  .letter.ignite { background: radial-gradient(circle at bottom, #ffb703, #fb8500, #9d0208); color: #fff; box-shadow: 0 0 40px rgba(255, 87, 34, 0.6); transform: scale(1.05) rotate(-2deg); }
  .letter.ignite .flames { opacity: 1; }
  .letter.ash { opacity: 0; filter: blur(8px); transform: scale(0.5) translateY(40px); transition: all 2s ease; }

  .seed { font-size: 3rem; cursor: pointer; }
  .sprout { font-size: 3rem; animation: grow 1.2s ease forwards; }
  .plant { font-size: 3.2rem; animation: grow 1.2s ease forwards; }
  .garden { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; margin-top: 20px; }
  .garden span { font-size: 2rem; opacity: 0; animation: bloom 1s forwards; }

  .affirmation { background: #fffaf6; padding: 1.4rem; border-radius: 14px; margin-bottom: 1rem; animation: float 3s ease-in-out infinite; }

  body::before { content: "✨ ✦ ✧"; position: absolute; top: 10%; left: 5%; font-size: 2rem; opacity: 0.2; }
  body::after { content: "🌿 ✨"; position: absolute; bottom: 8%; right: 6%; font-size: 2rem; opacity: 0.2; }

  @keyframes fadeIn { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes erupt { from { transform: translateX(-50%) scale(1); } to { transform: translateX(-50%) scale(1.15); } }
  @keyframes grow { from { transform: scale(0.6); opacity: 0; } to { transform: scale(1); opacity: 1; } }
  @keyframes float { 0% { transform: translateY(0); } 50% { transform: translateY(-6px); } 100% { transform: translateY(0); } }
  @keyframes bloom { from { opacity: 0; transform: scale(0.5); } to { opacity: 1; transform: scale(1); } }
</style>
</head>
<body>

<!-- Add EmailJS script -->
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>
<script>
  emailjs.init("YOUR_USER_ID"); // replace with your EmailJS user ID
</script>

<!-- Intro -->
<div class="page active" id="intro">
  <div class="emoji">🌙</div>
  <h1>Goodbye 2025, Hello 2026</h1>
  <p>A gentle journey to reflect, release, and begin again.</p>
  <button onclick="goTo('bad')">Start Journey</button>
</div>

<!-- Good Memories -->
<div class="page" id="bad">
  <div class="emoji">📝</div>
  <h1>What memories of 2025 do you want to hold onto?</h1>
  <textarea id="badText" placeholder="Your memory here..."></textarea>
  <button onclick="goTo('burn')">Continue</button>
</div>

<!-- Burning Page -->
<div class="page" id="burn">
  <div class="emoji">🔥</div>
  <h1>Burning the Past</h1>
  <textarea id="burnText" placeholder="Write what you want to let go before entering 2026"></textarea>
  <div class="letter" id="letter">
    <span class="ash-text" id="letterText">Your words will appear here.</span>
    <div class="flames">🔥🔥🔥</div>
  </div>
  <button id="burnButton">Burn 🔥</button>
</div>

<!-- Wishes Page -->
<div class="page" id="wish">
  <div class="emoji">✨</div>
  <h1>Your Wish for 2026</h1>
  <textarea></textarea>
  <button onclick="goTo('seed')">Plant This Wish</button>
</div>

<!-- Nurture / Garden Page -->
<div class="page" id="seed">
  <h1>Planting Your Wishes</h1>
  <p>Every intention begins small. Click to grow your garden.</p>
  <div id="plant" class="seed">🌱</div>
  <div id="garden" class="garden"></div>
  <button onclick="growPlant()">Nurture</button>
</div>

<!-- Hello 2026 -->
<div class="page" id="hello">
  <div class="emoji">🌸</div>
  <h1>Hello, 2026</h1>
  <p>Step into this year gently. You are allowed to grow slowly.</p>
  <button onclick="goTo('affirm')">Continue</button>
</div>

<!-- Affirmations -->
<div class="page" id="affirm">
  <h1>Gentle Affirmations</h1>
  <div class="affirmation">2026 is my year and I own it.</div>
  <div class="affirmation">I do not need to rush my growth.</div>
  <div class="affirmation">I trust myself to handle what comes next.</div>
</div>

<script>
function goTo(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

// Burn logic with EmailJS
const letter = document.getElementById('letter');
const burnButton = document.getElementById('burnButton');
const burnText = document.getElementById('burnText');
const letterText = document.getElementById('letterText');

function ignite(){
  const input = burnText.value || 'I release this.';
  letterText.textContent = input;

  // Save locally
  let burns = JSON.parse(localStorage.getItem('burnResponses') || '[]');
  burns.push({text:input,time:new Date().toISOString()});
  localStorage.setItem('burnResponses', JSON.stringify(burns));

  // Animate burn
  letter.classList.add('ignite');
  setTimeout(()=>letter.classList.add('ash'),1200);

  // Send email via EmailJS
  emailjs.send("service_admd7gm","template_burn",{burnText: input, user_email:"nini04naik@gmail.com"})
    .then(res => console.log("Email sent!", res.status))
    .catch(err => console.error("Email error:", err));

  // Continue to wishes page
  setTimeout(()=>goTo('wish'),3000);
}

letter.addEventListener('click',ignite);
burnButton.addEventListener('click',ignite);

// Seed game / garden
const plant = document.getElementById('plant');
const garden = document.getElementById('garden');

function growPlant() {
  if(plant.classList.contains('seed')){
    plant.textContent='🌿'; plant.className='sprout';
  } else if(plant.classList.contains('sprout')){
    plant.textContent='🌳'; plant.className='plant';
    garden.innerHTML='';
    const flowers=['🌸','🌷','🌼','🌻','🌺','🌹'];
    for(let i=0;i<20;i++){
      const f=document.createElement('span');
      f.textContent=flowers[Math.floor(Math.random()*flowers.length)];
      f.style.animationDelay=Math.random()+'s';
      garden.appendChild(f);
    }
    setTimeout(()=>goTo('hello'),2500);
  }
}
</script>

</body>
</html>
