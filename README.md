# Margo-Riba-Moya
Gift project
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Happy Birthday</title>

<style>
body {
  margin: 0;
  height: 100vh;
  background: #ffd6e8;
  overflow: hidden;
  font-family: Arial;
}

/* сцена */
.scene {
  width: 100%;
  height: 100%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

/* КОНВЕРТ (белый пиксельный) */
.envelope {
  width: 260px;
  height: 170px;
  background: #fff;
  border: 3px solid #f3a6c6;
  box-shadow: 0 10px 0 #f3a6c6;
  position: relative;
  cursor: pointer;
  transition: all 0.8s ease;
  overflow: hidden;
}

/* сердечко */
.envelope::before {
  content: "💗";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 42px;
  transition: 0.5s;
}

/* анимация открытия */
.envelope.open {
  transform: scale(1.05) rotateX(20deg);
  opacity: 0;
}

/* кнопки */
.buttons {
  margin-top: 20px;
  z-index: 10;
}

button {
  padding: 10px 18px;
  margin: 5px;
  border: none;
  border-radius: 12px;
  font-size: 16px;
  cursor: pointer;
}

#openBtn {
  background: #ff4d88;
  color: white;
}

#fakeBtn {
  background: #ffc1d6;
  position: absolute;
}

/* фото */
.photos {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}

.photos img {
  width: 80px;
  position: absolute;
  opacity: 0;
  transition: 1s ease;
}

/* сердце финальное */
.heartZone {
  position: absolute;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

/* видео */
.video {
  position: absolute;
  opacity: 0;
  transition: 1s;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.video.show {
  opacity: 1;
}

/* подпись */
.footer {
  position: absolute;
  bottom: 20px;
  width: 100%;
  text-align: center;
  font-size: 22px;
  color: #b30059;
  opacity: 0;
  transition: 1s;
}

.footer.show {
  opacity: 1;
}
</style>
</head>

<body>

<div class="scene">

  <div class="envelope" id="envelope"></div>

  <div class="buttons">
    <button id="openBtn">Open</button>
    <button id="fakeBtn">Don’t open</button>
  </div>

  <!-- ФОТО -->
  <div class="photos" id="photos">
    <img src="photo1.jpg">
    <img src="photo2.jpg">
    <img src="photo3.jpg">
    <img src="photo4.jpg">
    <img src="photo5.jpg">
    <img src="photo6.jpg">
    <img src="photo7.jpg">
    <img src="photo8.jpg">
    <img src="photo9.jpg">
    <img src="photo10.jpg">
  </div>

  <!-- ВИДЕО -->
  <div class="video" id="video">
    <video width="300" controls>
      <source src="video.mp4" type="video/mp4">
    </video>
  </div>

</div>

<div class="footer" id="footer">
Happy birthday, Margot
</div>

<script>
const envelope = document.getElementById("envelope");
const openBtn = document.getElementById("openBtn");
const fakeBtn = document.getElementById("fakeBtn");
const photos = document.querySelectorAll(".photos img");
const video = document.getElementById("video");
const footer = document.getElementById("footer");

let fakeMoves = 0;

/* убегающая кнопка */
function moveButton() {
  fakeBtn.style.left = Math.random() * (window.innerWidth - 100) + "px";
  fakeBtn.style.top = Math.random() * (window.innerHeight - 50) + "px";
}

fakeBtn.addEventListener("mouseenter", moveButton);
fakeBtn.addEventListener("click", moveButton);

/* открыть */
openBtn.onclick = function () {

  envelope.classList.add("open");

  setTimeout(() => {

    /* фотки появляются */
    photos.forEach((img) => {
      img.style.opacity = 1;

      const x = Math.random() * window.innerWidth * 0.8;
      const y = Math.random() * window.innerHeight * 0.8;

      img.style.left = x + "px";
      img.style.top = y + "px";
    });

    /* через 2 сек — собираются в сердце */
    setTimeout(() => {

      photos.forEach((img, i) => {

        const angle = i * (Math.PI * 2 / photos.length);
        const radius = 120;

        const x = window.innerWidth / 2 + Math.cos(angle) * radius;
        const y = window.innerHeight / 2 + Math.sin(angle) * radius;

        img.style.left = x + "px";
        img.style.top = y + "px";
      });

    }, 2000);

    /* видео */
    setTimeout(() => {
      video.classList.add("show");
      footer.classList.add("show");
    }, 3500);

  }, 800);
};
</script>

</body>
</html>
