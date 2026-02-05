<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Geonation Store</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;font-family:Inter,sans-serif;margin:0;padding:0}
body {
  margin:0;
  color:#fff;
  background: linear-gradient(270deg,#000,#0f0,#000);
  background-size: 600% 600%;
  animation: gradientMove 20s ease infinite;
}
@keyframes gradientMove {
  0%{background-position:0% 50%;}
  50%{background-position:100% 50%;}
  100%{background-position:0% 50%;}
}

header{
  display:flex;justify-content:space-between;align-items:center;padding:20px 40px;
}

.logo{font-size:22px;font-weight:800}

.copy-ip{
  background:#fff;color:#000;border:none;padding:10px 18px;border-radius:14px;font-weight:700;cursor:pointer;
  box-shadow: 0 0 10px #fff;
  transition:0.3s;
}
.copy-ip:hover{box-shadow:0 0 20px #0f0;}

.menu{
  display:flex;gap:14px;justify-content:center;margin:20px 0;
}
.menu button{
  background:#1a1a1a;border:none;padding:10px 18px;border-radius:14px;color:#fff;cursor:pointer;
  font-weight:700;
  box-shadow:0 0 5px #0f0;
  transition:0.3s;
}
.menu button:hover{box-shadow:0 0 15px #0f0; transform: translateY(-2px);}

.section{display:none}
.section.active{display:grid}

.store{padding:40px;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:25px}

.card{
  background:linear-gradient(160deg,#151515,#0c0c0c);
  border-radius:22px;
  padding:22px;
  position:relative;
  transition:0.3s;
}
.card:hover{transform:translateY(-6px); box-shadow:0 0 20px #0f0;}

.price{position:absolute;top:18px;right:18px;font-weight:700}

.card h2{margin-top:40px}
.card ul{list-style:none;padding:0}
.card ul li{opacity:.85;margin-bottom:8px}

.buy{width:100%;padding:12px;border-radius:14px;border:none;font-weight:700;cursor:pointer;transition:0.3s;}
.buy.white{background:#fff;color:#000;box-shadow:0 0 10px #fff;}
.buy.white:hover{box-shadow:0 0 20px #0f0;}
.buy.orange{background:#ffae00;color:#000;box-shadow:0 0 10px #ff0;}
.buy.orange:hover{box-shadow:0 0 20px #ff0;}

.vip{border-top:4px solid #8a2be2}
.plus{border-top:4px solid #ff4040}
.key{border-top:4px solid #00ffaa}

/* STATUS */
.status-card{
  background:linear-gradient(160deg,#111,#222);
  border-radius:22px;
  padding:22px;
  display:flex; flex-direction:column; gap:12px;
  max-width:300px;
  box-shadow:0 0 15px #0f0;
}
.status-line{display:flex;justify-content:space-between;align-items:center;}
.status-dot{
  width:14px; height:14px; border-radius:50%; background:red;
  box-shadow:0 0 10px #f00;
  transition:0.3s;
}

/* PREVIEW MODAL */
#previewModal{
  display:none;position:fixed;inset:0;background:rgba(0,0,0,.85);z-index:999;
}
#previewBox{
  width:90%;height:90%;margin:5%;background:#000;border-radius:20px;overflow:auto;
}
#closePreview{
  position:absolute;top:20px;right:20px;padding:10px 16px;border-radius:12px;border:none;font-weight:700;cursor:pointer;
}
</style>
</head>
<body>

<header>
  <div class="logo">Geonation</div>
  <button class="copy-ip" onclick="copyIP()">Copy IP</button>
</header>

<div class="menu">
  <button onclick="show('vip')">VIP Ranks</button>
  <button onclick="show('keys')">Buy Keys</button>
  <button onclick="show('status')">Main Menu</button>
  <button onclick="openPreview()">Preview</button>
</div>

<!-- VIP -->
<section id="vip" class="store section active">
  <div class="card vip">
    <div class="price">5 GEL / Monthly</div>
    <h2>VIP</h2>
    <ul><li>✔ Unique Kit</li><li>✔ /fly</li></ul>
    <button class="buy white">ყიდვა</button>
  </div>
  <div class="card plus">
    <div class="price">10 GEL / Monthly</div>
    <h2>+VIP</h2>
    <ul><li>✔ All VIP perks</li></ul>
    <button class="buy white">ყიდვა</button>
  </div>
</section>

<!-- KEYS -->
<section id="keys" class="store section">
  <div class="card key"><div class="price">2 GEL</div><h2>Amethyst Key</h2><button class="buy orange">Buy</button></div>
  <div class="card key"><div class="price">1 GEL</div><h2>Legendary Key</h2><button class="buy orange">Buy</button></div>
  <div class="card key"><div class="price">0.50 GEL</div><h2>Light Key</h2><button class="buy orange">Buy</button></div>
</section>

<!-- STATUS / MAIN MENU -->
<section id="status" class="store section">
  <div class="status-card">
    <div class="status-line">
      <div>Server Status:</div>
      <div><span id="statusDot" class="status-dot"></span> <span id="statusText">Checking...</span></div>
    </div>
    <div class="status-line">
      <div>Players:</div>
      <div id="playersCount">0</div>
    </div>
    <div class="status-line">
      <div>IP:</div>
      <div>
        <span id="serverIP">91.197.6.16:22976</span>
        <button class="copy-ip" onclick="copyIP()">Copy</button>
      </div>
    </div>
  </div>
</section>

<!-- PREVIEW -->
<div id="previewModal">
  <button id="closePreview" onclick="closePreview()">Close</button>
  <div id="previewBox">
    <iframe src="" style="width:100%;height:100%;border:none"></iframe>
  </div>
</div>

<script>
function copyIP(){
  navigator.clipboard.writeText("91.197.6.16:22976");
  alert("IP copied!");
}

function show(id){
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

function openPreview(){
  document.querySelector('#previewModal iframe').src = location.href;
  document.getElementById('previewModal').style.display='block';
}
function closePreview(){
  document.getElementById('previewModal').style.display='none';
}

// Fake server check (you can replace with real API)
function checkServer(){
  const online = Math.random()>0.5; // simulate
  const players = Math.floor(Math.random()*100);
  document.getElementById('statusDot').style.background = online?'#0f0':'#f00';
  document.getElementById('statusDot').style.boxShadow = online?'0 0 10px #0f0':'0 0 10px #f00';
  document.getElementById('statusText').innerText = online?'Online':'Offline';
  document.getElementById('playersCount').innerText = players;
}

setInterval(checkServer, 3000);
checkServer();
</script>

</body>
</html>
