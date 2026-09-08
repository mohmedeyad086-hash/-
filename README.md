<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Eiad Football ⚽</title>

<style>
*{box-sizing:border-box}

body{
  margin:0;
  background:#101010;
  color:white;
  font-family:Arial,sans-serif;
  text-align:center;
}

h1{margin:8px}

#top{
  display:flex;
  justify-content:center;
  align-items:center;
  gap:25px;
  font-size:24px;
  font-weight:bold;
  margin:8px;
}

#timer{
  background:#222;
  padding:6px 14px;
  border-radius:10px;
}

#game{
  position:relative;
  width:95vw;
  height:70vh;
  max-width:1000px;
  margin:auto;
  background:#168a38;
  border:5px solid white;
  overflow:hidden;
}

.line{
  position:absolute;
  left:50%;
  top:0;
  width:4px;
  height:100%;
  background:white;
}

.circle{
  position:absolute;
  width:130px;
  height:130px;
  border:4px solid white;
  border-radius:50%;
  left:calc(50% - 65px);
  top:calc(50% - 65px);
}

.goal{
  position:absolute;
  top:30%;
  width:55px;
  height:40%;
  border:5px solid white;
  background:rgba(255,255,255,.12);
}

.left-goal{left:-8px}
.right-goal{right:-8px}

.player{
  position:absolute;
  width:44px;
  height:44px;
  border-radius:50%;
  border:3px solid white;
  z-index:3;
  box-shadow:0 3px 7px #000;
}

#p1{background:#1976ff}
#p2{background:#ff3030}

.player::after{
  content:"";
  position:absolute;
  width:12px;
  height:12px;
  background:#ffd2a1;
  border-radius:50%;
  left:50%;
  top:-9px;
  transform:translateX(-50%);
  border:2px solid white;
}

.keeper{
  position:absolute;
  width:40px;
  height:40px;
  border-radius:50%;
  border:3px solid white;
  z-index:3;
}

#k1{background:#00c853}
#k2{background:#ffea00}

#ball{
  position:absolute;
  width:24px;
  height:24px;
  background:white;
  border:3px solid #222;
  border-radius:50%;
  z-index:4;
  box-shadow:0 2px 5px #000;
}

#message{
  position:absolute;
  inset:0;
  display:none;
  justify-content:center;
  align-items:center;
  flex-direction:column;
  background:rgba(0,0,0,.78);
  z-index:10;
  font-size:36px;
  font-weight:bold;
}

button{
  margin:7px;
  padding:10px 18px;
  font-size:17px;
  border:0;
  border-radius:10px;
  cursor:pointer;
}

#restart{
  background:white;
}

.controls{
  font-size:15px;
}
</style>
</head>

<body>

<h1>⚽ Eiad Football</h1>

<div id="top">
  <span>🔵 <b id="s1">0</b></span>
  <span id="timer">02:00</span>
  <span><b id="s2">0</b> 🔴</span>
</div>

<div id="game">

  <div class="line"></div>
  <div class="circle"></div>

  <div class="goal left-goal"></div>
  <div class="goal right-goal"></div>

  <div id="p1" class="player"></div>
  <div id="p2" class="player"></div>

  <div id="k1" class="keeper"></div>
  <div id="k2" class="keeper"></div>

  <div id="ball"></div>

  <div id="message"></div>

</div>

<button id="restart">🔄 مباراة جديدة</button>

<div class="controls">
  🔵 W A S D للحركة | Space تسديدة | Shift Sprint
  <br>
  🔴 الأسهم للحركة | Enter تسديدة | Shift + الأسهم Sprint
</div>

<script>

const game=document.getElementById("game");

const p1=document.getElementById("p1");
const p2=document.getElementById("p2");

const k1=document.getElementById("k1");
const k2=document.getElementById("k2");

const ball=document.getElementById("ball");

const s1=document.getElementById("s1");
const s2=document.getElementById("s2");

const timer=document.getElementById("timer");
const message=document.getElementById("message");
const restart=document.getElementById("restart");

const keys={};

let score1=0;
let score2=0;

let timeLeft=120;
let gameOver=false;

let player1={
  x:150,
  y:250
};

let player2={
  x:750,
  y:250
};

let keeper1={
  x:30,
  y:200
};

let keeper2={
  x:750,
  y:200
};

let ballData={
  x:488,
  y:250,
  vx:0,
  vy:0
};

document.addEventListener("keydown",e=>{
  keys[e.key.toLowerCase()]=true;

  if(e.code==="Space"){
    keys["space"]=true;
  }
});

document.addEventListener("keyup",e=>{
  keys[e.key.toLowerCase()]=false;

  if(e.code==="Space"){
    keys["space"]=false;
  }
});

function distance(a,b){
  return Math.hypot(
    a.x-b.x,
    a.y-b.y
  );
}

/* ركلة عادية */
function kick(player){

  if(distance(player,ballData)<65){

    let dx=ballData.x-player.x;
    let dy=ballData.y-player.y;

    let len=Math.hypot(dx,dy)||1;

    ballData.vx=(dx/len)*10;
    ballData.vy=(dy/len)*10;
  }
}

/* تسديدة قوية */
function powerKick(player){

  if(distance(player,ballData)<70){

    let dx=ballData.x-player.x;
    let dy=ballData.y-player.y;

    let len=Math.hypot(dx,dy)||1;

    ballData.vx=(dx/len)*18;
    ballData.vy=(dy/len)*18;
  }
}

/* حركة اللاعب الأول */
function movePlayer1(){

  let speed=keys["shift"]?8:5;

  if(keys["w"])player1.y-=speed;
  if(keys["s"])player1.y+=speed;
  if(keys["a"])player1.x-=speed;
  if(keys["d"])player1.x+=speed;

  if(keys["space"]){
    powerKick(player1);
  }
}

/* حركة اللاعب الثاني */
function movePlayer2(){

  let speed=keys["shift"]?8:5;

  if(keys["arrowup"])player2.y-=speed;
  if(keys["arrowdown"])player2.y+=speed;
  if(keys["arrowleft"])player2.x-=speed;
  if(keys["arrowright"])player2.x+=speed;

  if(keys["enter"]){
    powerKick(player2);
  }
}

function limitPlayer(p){

  p.x=Math.max(
    0,
    Math.min(game.clientWidth-44,p.x)
  );

  p.y=Math.max(
    0,
    Math.min(game.clientHeight-44,p.y)
  );
}

/* الحراس يتحركون ناحية الكرة */
function moveKeepers(){

  let targetY=ballData.y-20;

  keeper1.y +=
    (targetY-keeper1.y)*0.04;

  keeper2.y +=
    (targetY-keeper2.y)*0.04;

  keeper1.y=Math.max(
    game.clientHeight*.30,
    Math.min(game.clientHeight*.70-40,keeper1.y)
  );

  keeper2.y=Math.max(
    game.clientHeight*.30,
    Math.min(game.clientHeight*.70-40,keeper2.y)
  );
}

/* اصطدام الحارس */
function keeperCollision(k){

  if(distance(k,ballData)<43){

    ballData.vx*=-1.2;

    ballData.vy*=0.9;

    if(Math.abs(ballData.vx)<5){
      ballData.vx=
        ballData.vx<0?-7:7;
    }
  }
}

function moveBall(){

  ballData.x+=ballData.vx;
  ballData.y+=ballData.vy;

  ballData.vx*=0.985;
  ballData.vy*=0.985;

  if(
    ballData.y<=0 ||
    ballData.y>=game.clientHeight-24
  ){
    ballData.vy*=-0.85;
  }

  keeperCollision(keeper1);
  keeperCollision(keeper2);

  /* الهدف الأيسر */
  if(ballData.x<=0){

    if(
      ballData.y>game.clientHeight*.30 &&
      ballData.y<game.clientHeight*.70
    ){

      score2++;
      resetBall();

    }else{

      ballData.x=0;
      ballData.vx=Math.abs(ballData.vx);
    }
  }

  /* الهدف الأيمن */
  if(ballData.x>=game.clientWidth-24){

    if(
      ballData.y>game.clientHeight*.30 &&
      ballData.y<game.clientHeight*.70
    ){

      score1++;
      resetBall();

    }else{

      ballData.x=game.clientWidth-24;
      ballData.vx=-Math.abs(ballData.vx);
    }
  }
}

function resetBall(){

  ballData.x=
    game.clientWidth/2-12;

  ballData.y=
    game.clientHeight/2-12;

  ballData.vx=0;
  ballData.vy=0;

  player1.x=150;
  player1.y=250;

  player2.x=750;
  player2.y=250;
}

function updateScore(){

  s1.textContent=score1;
  s2.textContent=score2;
}

function updateTimer(){

  let min=Math.floor(timeLeft/60);
  let sec=timeLeft%60;

  timer.textContent=
    String(min).padStart(2,"0")
    +":"+
    String(sec).padStart(2,"0");
}

setInterval(()=>{

  if(gameOver)return;

  timeLeft--;

  updateTimer();

  if(timeLeft<=0){

    gameOver=true;

    if(score1>score2){
      message.textContent="🏆 الأزرق فاز!";
    }
    else if(score2>score1){
      message.textContent="🏆 الأحمر فاز!";
    }
    else{
      message.textContent="🤝 تعادل!";
    }

    message.style.display="flex";
  }

},1000);

function draw(){

  p1.style.left=player1.x+"px";
  p1.style.top=player1.y+"px";

  p2.style.left=player2.x+"px";
  p2.style.top=player2.y+"px";

  k1.style.left=keeper1.x+"px";
  k1.style.top=keeper1.y+"px";

  k2.style.left=keeper2.x+"px";
  k2.style.top=keeper2.y+"px";

  ball.style.left=ballData.x+"px";
  ball.style.top=ballData.y+"px";

  updateScore();
}

function gameLoop(){

  if(!gameOver){

    movePlayer1();
    movePlayer2();

    limitPlayer(player1);
    limitPlayer(player2);

    moveKeepers();
    moveBall();
    draw();
  }

  requestAnimationFrame(gameLoop);
}

restart.onclick=()=>{

  score1=0;
  score2=0;

  timeLeft=120;
  gameOver=false;

  message.style.display="none";

  resetBall();
  updateScore();
  updateTimer();
};

updateTimer();
gameLoop();

</script>

</body>
</html>
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">

<title>Eiad Football Online ⚽</title>

<style>

*{
  box-sizing:border-box;
}

body{
  margin:0;
  background:#101010;
  color:white;
  font-family:Arial,sans-serif;
  text-align:center;
}

.container{
  width:90%;
  max-width:500px;
  margin:80px auto;
  background:#1d1d1d;
  padding:30px;
  border-radius:20px;
  box-shadow:0 0 25px rgba(0,0,0,.6);
}

h1{
  font-size:35px;
}

input{
  width:90%;
  padding:15px;
  margin:10px;
  border-radius:10px;
  border:0;
  font-size:18px;
  text-align:center;
}

button{
  width:90%;
  padding:15px;
  margin:10px;
  border:0;
  border-radius:12px;
  font-size:19px;
  font-weight:bold;
  cursor:pointer;
}

#create{
  background:#1976ff;
  color:white;
}

#join{
  background:#00c853;
  color:white;
}

#status{
  margin-top:20px;
  font-size:18px;
  min-height:25px;
}

#room{
  display:none;
}

.code{
  font-size:35px;
  letter-spacing:8px;
  margin:20px;
  color:#00e5ff;
}

</style>
</head>

<body>

<div class="container">

  <h1>⚽ Eiad Football</h1>

  <div id="menu">

    <input
      id="playerName"
      placeholder="اكتب اسمك"
      maxlength="15"
    >

    <button id="create">
      🎮 إنشاء غرفة
    </button>

    <button id="join">
      👥 دخول غرفة
    </button>

    <input
      id="roomCode"
      placeholder="كود الغرفة"
      maxlength="6"
      style="display:none"
    >

    <div id="status"></div>

  </div>

  <div id="room">

    <h2>🎮 الغرفة جاهزة!</h2>

    <p>ابعت الكود للاعب الثاني:</p>

    <div class="code" id="roomNumber"></div>

    <p id="players">
      👤 أنت فقط داخل الغرفة
    </p>

  </div>

</div>

<script>

const createButton=
document.getElementById("create");

const joinButton=
document.getElementById("join");

const nameInput=
document.getElementById("playerName");

const roomInput=
document.getElementById("roomCode");

const status=
document.getElementById("status");

const menu=
document.getElementById("menu");

const room=
document.getElementById("room");

const roomNumber=
document.getElementById("roomNumber");

function createRoomCode(){

  const chars=
  "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";

  let code="";

  for(let i=0;i<6;i++){

    code+=chars[
      Math.floor(
        Math.random()*chars.length
      )
    ];

  }

  return code;
}

createButton.onclick=()=>{

  const name=
    nameInput.value.trim();

  if(!name){

    status.textContent=
      "⚠️ اكتب اسمك الأول";

    return;
  }

  const code=
    createRoomCode();

  roomNumber.textContent=code;

  menu.style.display="none";
  room.style.display="block";

};

joinButton.onclick=()=>{

  if(
    roomInput.style.display==="none"
  ){

    roomInput.style.display="block";

    status.textContent=
      "اكتب كود الغرفة ثم اضغط دخول مرة أخرى";

    return;
  }

  const code=
    roomInput.value
      .trim()
      .toUpperCase();

  if(code.length!==6){

    status.textContent=
      "⚠️ كود الغرفة لازم يكون 6 أحرف";

    return;
  }

  status.textContent=
    "🔄 جاري الاتصال بالغرفة...";

};

</script>

</body>
</html>
<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Eiad Football Online ⚽</title>
</head>

<body>

  <h1>🔥 Eiad Football Online ⚽</h1>

  <p>المرحلة 6: الاتصال بين جهازين 🌐</p>

  <button id="connectBtn">اتصال باللعبة</button>

  <p id="status">غير متصل ❌</p>

  <script>
    document.getElementById("connectBtn").onclick = function () {
      document.getElementById("status").textContent =
        "جاهز للاتصال 🌐⚽";
    };
  </script>

</body>
</html>
