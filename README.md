# Birthday-girl
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Pratiksha ❤️</title>
<style>
body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(to right, #ff9a9e, #fad0c4);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  overflow: hidden;
}
.card {
  background-color: #fff3f3;
  border-radius: 20px;
  padding: 5vw;
  text-align: center;
  box-shadow: 0 8px 20px rgba(0,0,0,0.2);
  max-width: 90vw;
  z-index: 10;
  position: relative;
}
.card h1 {
  color: #ff4b5c;
  font-size: 6vw;
  margin-bottom: 4vw;
}
.card p {
  font-size: 4vw;
  margin-bottom: 4vw;
  color: #333;
  min-height: 10vw;
}
#final-message {
  font-size: 5vw;
  font-weight: bold;
  color: #ff1f3c;
  opacity: 0;
  margin-top: 2vw;
}
.card button {
  padding: 3vw 6vw;
  font-size: 4vw;
  color: #fff;
  background-color: #ff4b5c;
  border: none;
  border-radius: 10vw;
  cursor: pointer;
  margin: 2vw;
  transition: 0.3s;
}
.card button:hover {
  background-color: #ff1f3c;
}
canvas {
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
}
#hearts-container, #balloons-container, #fireworks-container {
  position: fixed;
  width: 100%;
  height: 100%;
  pointer-events: none;
  overflow: hidden;
  top: 0;
  left: 0;
}
.heart {
  position: absolute;
  font-size: 5vw;
  color: #ff4b5c;
  animation: float 5s linear infinite;
  opacity: 0.8;
}
@keyframes float {
  0% { transform: translateY(0) rotate(0deg); }
  100% { transform: translateY(-100vh) rotate(360deg); }
}
.balloon {
  position: absolute;
  bottom: -15vw;
  font-size: 10vw;
  animation: floatBalloon linear infinite;
}
@keyframes floatBalloon {
  0% { transform: translateY(0) rotate(0deg); }
  100% { transform: translateY(-120vh) rotate(360deg); }
}
.firework {
  position: absolute;
  width: 2vw;
  height: 2vw;
  border-radius: 50%;
  background-color: #ffd700;
  opacity: 0.8;
  animation: explode 0.8s ease-out forwards;
}
@keyframes explode {
  0% { transform: scale(0); opacity: 1; }
  100% { transform: scale(2) translateY(-50px); opacity: 0; }
}
</style>
</head>
<body>
<div class="card">
  <h1>Happy Birthday, Pratiksha! ❤️</h1>
  <p id="typed-text"></p>
  <p id="final-message"></p>
  <button onclick="showConfetti()">Celebrate 🎉</button>
</div>

<canvas id="confetti"></canvas>
<div id="hearts-container"></div>
<div id="balloons-container"></div>
<div id="fireworks-container"></div>

<audio id="bg-music" autoplay loop>
  <source src="https://www.bensound.com/bensound-music/bensound-romantic.mp3" type="audio/mpeg">
</audio>

<script>
// Typing Effect
const message = "Braj wishes you the happiest birthday, Pratiksha! You are my heart and soul ❤️";
let i = 0;
const speed = 70;
function typeWriter() {
  if (i < message.length) {
    document.getElementById("typed-text").innerHTML += message.charAt(i);
    i++;
    setTimeout(typeWriter, speed);
  } else {
    showFinalMessage();
  }
}
typeWriter();

// Show Final Message + Fireworks
function showFinalMessage() {
  const final = document.getElementById("final-message");
  final.innerText = "I Love You Pratiksha ❤️ – Braj";
  final.style.opacity = 1;
  createFireworks();
  showConfetti();
}

// Confetti
function showConfetti() {
  const canvas = document.getElementById('confetti');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const confetti = [];
  const colors = ['#ff4b5c','#ffb347','#ff9a9e','#fad0c4','#fbc2eb'];
  for(let j=0;j<80;j++){ // fewer for mobile
    confetti.push({x:Math.random()*canvas.width,y:Math.random()*canvas.height-canvas.height,r:Math.random()*6+4,d:Math.random()*150+50,color:colors[Math.floor(Math.random()*colors.length)],tilt:Math.random()*10-10,tiltAngleIncrement:Math.random()*0.07+0.05});
  }

  function draw(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    confetti.forEach(c=>{
      ctx.beginPath();
      ctx.lineWidth=c.r;
      ctx.strokeStyle=c.color;
      ctx.moveTo(c.x+c.tilt+c.r/2,c.y);
      ctx.lineTo(c.x+c.tilt,c.y+c.tilt+c.r/2);
      ctx.stroke();
    });
    update();
  }

  function update(){
    confetti.forEach(c=>{
      c.y+=2;
      c.tiltAngleIncrement+=0.05;
      c.tilt=Math.sin(c.tiltAngleIncrement)*15;
      if(c.y>canvas.height){c.y=-10;c.x=Math.random()*canvas.width;}
    });
  }
  setInterval(draw,20);
}

// Hearts
function createHearts(){
  const container = document.getElementById('hearts-container');
  setInterval(()=>{
    const heart = document.createElement('div');
    heart.classList.add('heart');
    heart.style.left = Math.random()*window.innerWidth+'px';
    heart.style.fontSize = Math.random()*5+3+'vw';
    heart.textContent='❤️';
    container.appendChild(heart);
    setTimeout(()=>heart.remove(),5000);
  },400);
}
createHearts();

// Balloons
function createBalloons(){
  const container = document.getElementById('balloons-container');
  const colors=['🎈','🎉','💖','❤️','🧡','💛'];
  setInterval(()=>{
    const balloon=document.createElement('div');
    balloon.classList.add('balloon');
    balloon.style.left=Math.random()*window.innerWidth+'px';
    balloon.style.fontSize=Math.random()*10+5+'vw';
    balloon.textContent=colors[Math.floor(Math.random()*colors.length)];
    balloon.style.animationDuration=(5+Math.random()*5)+'s';
    container.appendChild(balloon);
    setTimeout(()=>balloon.remove(),10000);
  },600);
}
createBalloons();

// Fireworks
function createFireworks(){
  const container=document.getElementById('fireworks-container');
  for(let i=0;i<20;i++){
    const firework=document.createElement('div');
    firework.classList.add('firework');
    firework.style.left=Math.random()*window.innerWidth+'px';
    firework.style.top=Math.random()*window.innerHeight/2+'px';
    container.appendChild(firework);
    setTimeout(()=>firework.remove(),800);
  }
}
</script>
</body>
</html>


