<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Pixel Gift Heart</title>

<style>
body {
  margin: 0;
  overflow: hidden;
  background: #fff;
  font-family: monospace;
}

/* ===== UI ===== */
#dontOpen {
  position: absolute;
  top: 20px;
  width: 100%;
  text-align: center;
  font-size: 18px;
  z-index: 10;
  transition: 0.5s;
}

#openBtn {
  position: absolute;
  top: 60px;
  left: 50%;
  transform: translateX(-50%);
  padding: 10px 20px;
  cursor: pointer;
  z-index: 10;
}

/* ===== GIFT ===== */
#gift {
  width: 120px;
  height: 120px;
  background: #fff;
  border: 3px solid #000;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  transition: 1s;
  image-rendering: pixelated;
}

#gift::before,
#gift::after {
  content: "";
  position: absolute;
  background: #000;
}

#gift::before {
  width: 18px;
  height: 100%;
  left: 50%;
  transform: translateX(-50%);
}

#gift::after {
  height: 18px;
  width: 100%;
  top: 50%;
  transform: translateY(-50%);
}

/* ===== PHOTOS ===== */
.photo {
  width: 60px;
  height: 60px;
  position: absolute;
  background-size: cover;
  border: 2px solid #000;
  image-rendering: pixelated;
  transition: 1.2s cubic-bezier(.2,.8,.2,1);
}

/* ===== CANVAS BLOBS ===== */
#glitter {
  position: absolute;
  width: 100%;
  height: 100%;
  pointer-events: none;
}
</style>
</head>

<body>

<div id="dontOpen">DON'T OPEN</div>
<button id="openBtn">OPEN</button>

<div id="gift"></div>
<canvas id="glitter"></canvas>

<script>

const images = ["1.jpg","2.jpg","3.jpg","4.jpg","5.jpg","6.jpg"];

/* ❤️ сердце */
const heartPoints = [
  [-90,-40],[-70,-60],[-50,-70],[-30,-60],[-10,-40],[10,-40],[30,-60],[50,-70],[70,-60],[90,-40],
  [-100,-20],[-80,-40],[-60,-50],[-40,-40],[40,-40],[60,-50],[80,-40],[100,-20],
  [-100,0],[-80,-10],[-60,0],[-40,10],[40,10],[60,0],[80,-10],[100,0],
  [-80,20],[-60,30],[-40,40],[-20,50],[0,60],[20,50],[40,40],[60,30],[80,20],
  [-40,60],[-20,70],[0,80],[20,70],[40,60]
];

const gift = document.getElementById("gift");
const btn = document.getElementById("openBtn");
const dontOpen = document.getElementById("dontOpen");

const canvas = document.getElementById("glitter");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particles = [];
let photos = [];
let opened = false;

/* ===== PHOTOS ===== */
images.forEach((src, i) => {
  const el = document.createElement("div");
  el.className = "photo";
  el.style.backgroundImage = `url(${src})`;

  // старт — центр подарка
  el.style.left = (window.innerWidth/2 - 30) + "px";
  el.style.top = (window.innerHeight/2 - 30) + "px";

  document.body.appendChild(el);
  photos.push(el);
});

/* ===== GLITTER ===== */
function spawnGlitter(x,y) {
  for (let i=0;i<25;i++) {
    particles.push({
      x, y,
      vx: (Math.random()-0.5)*6,
      vy: (Math.random()-0.5)*6,
      life: 60
    });
  }
}

function animate() {
  ctx.clearRect(0,0,canvas.width,canvas.height);

  particles.forEach(p => {
    p.x += p.vx;
    p.y += p.vy;
    p.vy += 0.05;
    p.life--;

    ctx.fillStyle = "#000";
    ctx.fillRect(p.x, p.y, 2, 2);
  });

  particles = particles.filter(p => p.life > 0);
  requestAnimationFrame(animate);
}
animate();

/* ===== OPEN ===== */
btn.onclick = () => {
  if (opened) return;
  opened = true;

  dontOpen.style.opacity = 0;

  // подарок исчезает
  gift.style.transform = "translate(-50%, -50%) scale(0) rotate(180deg)";
  gift.style.opacity = 0;

  // блёстки в центре
  spawnGlitter(window.innerWidth/2, window.innerHeight/2);

  // фотки в сердце
  photos.forEach((p, i) => {
    const pt = heartPoints[i % heartPoints.length];

    setTimeout(() => {
      p.style.left = (window.innerWidth/2 + pt[0]) + "px";
      p.style.top = (window.innerHeight/2 + pt[1]) + "px";

      spawnGlitter(window.innerWidth/2 + pt[0], window.innerHeight/2 + pt[1]);
    }, i * 120);
  });
};

/* resize */
window.addEventListener("resize", () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});

</script>

</body>
</html>
