<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>For Sata ❤️</title>
<style>
body {
  margin: 0;
  background: radial-gradient(circle, #000 0%, #111 100%);
  font-family: 'Arial', sans-serif;
  overflow: hidden;
  text-align: center;
}

/* Countdown */
#countdown {
  font-size: 80px;
  margin-top: 100px;
}

/* Cake */
.cake {
  font-size: 120px;
  cursor: pointer;
  display: none;
  transition: transform 0.3s;
}
.cake:hover { transform: scale(1.2); }

/* Message */
#message {
  margin-top: 20px;
  font-size: 26px;
  width: 80%;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.5;
  white-space: pre-line;
  color: white;
}

/* Fireworks */
.fire {
  position: absolute;
  font-size: 25px;
  animation: firework 1.5s forwards;
}
@keyframes firework {
  from {opacity:1; transform: translate(0,0);}
  to {opacity:0; transform: translate(var(--x), var(--y));}
}

/* Orbiting Heart Text */
.orbit-container {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 400px;
  height: 400px;
  transform: translate(-50%, -50%);
  pointer-events: none;
}
.orbit-container span {
  position: absolute;
  font-size: 22px;
  color: #ff66cc;
  font-weight: bold;
  text-shadow:
    1px 1px 0 #e60073,
    2px 2px 0 #e60073;
  user-select: none;
}
</style>
</head>
<body>

<div id="countdown">3</div>
<div class="cake" onclick="startMagic()">🎂</div>

<div id="message"></div>

<div class="orbit-container" id="orbitContainer"></div>

<audio id="music" loop>
  <source src="https://www.mfiles.co.uk/mp3-downloads/Happy-Birthday-Song.mp3" type="audio/mpeg">
</audio>

<script>
// Countdown
let c = 3;
let counter = setInterval(() => {
  c--;
  document.getElementById("countdown").innerHTML = c > 0 ? c : '';
  if(c == 0){
    clearInterval(counter);
    document.getElementById("countdown").style.display = "none";
    document.querySelector(".cake").style.display = "block";
  }
}, 1000);

// Typing text slowly
let text = "Happy Birthday Sata ❤️\nYou are one of the most beautiful parts of my life.\nMay your days always shine with happiness and love ✨🎂";
let i = 0;
function typeText(){
  if(i < text.length){
    document.getElementById("message").innerHTML += text.charAt(i);
    i++;
    setTimeout(typeText, 100);
  }
}

// Fireworks
function fireworks(){
  for(let i=0;i<60;i++){
    let f=document.createElement("div");
    f.className="fire";
    f.innerHTML="✨";

    f.style.left=window.innerWidth/2+"px";
    f.style.top=window.innerHeight/2+"px";

    f.style.setProperty('--x',(Math.random()*800-400)+"px");
    f.style.setProperty('--y',(Math.random()*800-400)+"px");

    document.body.appendChild(f);
    setTimeout(()=>f.remove(),1500);
  }
}

// Orbiting Heart Text
function startOrbitText() {
  const container = document.getElementById("orbitContainer");
  const text = "I LOVE YOU ".repeat(15);
  const letters = text.split("");
  
  letters.forEach(letter => {
    const span = document.createElement("span");
    span.innerText = letter;
    container.appendChild(span);
  });

  let angle = 0;
  setInterval(() => {
    const spans = container.children;
    const R = 150; // size of heart
    for(let i=0;i<spans.length;i++){
      const t = (i*10 + angle) * Math.PI/180;
      // Heart parametric equation
      const x = R * 16 * Math.pow(Math.sin(t),3) / 16;
      const y = -R * (13*Math.cos(t) - 5*Math.cos(2*t) - 2*Math.cos(3*t) - Math.cos(4*t)) / 16;
      spans[i].style.left = 200 + x + "px";
      spans[i].style.top = 200 + y + "px";
    }
    angle += 2;
  }, 50);
}

// Start magic
function startMagic(){
  document.getElementById("music").play();
  document.querySelector(".cake").style.display="none";

  fireworks();
  typeText();
  startOrbitText();
}
</script>

</body>
</html>

