# Margo-Riba-Moya
Gift project
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Happy Birthday</title>

<style>
  .envelope {
  width: 240px;
  height: 160px;
  background: #fff;
  position: relative;
  margin: auto;
  cursor: pointer;
  box-shadow: 0 10px 0 #f3a6c6;
  border: 3px solid #f3a6c6;
  overflow: hidden;
}
  .envelope::before {
  content: "💗";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 40px;
}
body {
  margin: 0;
  height: 100vh;
  background: #ffd6e8;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial;
  overflow: hidden;
}

/* сцена */
.scene {
  text-align: center;
}

/* конверт */
.envelope {
  width: 220px;
  height: 160px;
  background: #ff4d88;
  position: relative;
  margin: auto;
  cursor: pointer;
  box-shadow: 0 10px 0 #c2185b;
  transition: 0.6s ease;
}

.heart {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  font-size: 40px;
}

/* открытие */
.envelope.open {
  transform: scale(1.05);
  background: #ff2f75;
}

.envelope.open .heart {
  opacity: 0;
}

/* кнопки */
.buttons {
  margin-top: 20px;
}

button {
  padding: 10px 16px;
  margin: 5px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-size: 16px;
}

#openBtn {
  background: #ff4d88;
  color: white;
}

#fakeBtn {
  background: #ffc1d6;
  position: relative;
}

#fakeBtn:hover {
  left: 40px;
  top: -10px;
  position: relative;
}

/* фото */
.photos {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  pointer-events: none;
}

.photos img {
  width: 80px;
  position: absolute;
  opacity: 0;
  transition: 1s ease;
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

/* видео блок */
.video {
  display: none;
  margin-top: 20px;
}

.video video {
  width: 300px;
  border-radius: 10px;
}
</style>
</head>

<body>

<div class="scene">

  <div class="envelope" id="envelope">
    <div class="heart">💗</div>
  </div>

  <div class="buttons">
    <button id="openBtn">Open</button>
    <button id="fakeBtn">Don’t open</button>
  </div>

  <!-- ФОТО -->
  <div class="photos" id="photos">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
    <img src="https://via.placeholder.com/100">
  </div>

  <!-- ВИДЕО -->
  <div class="video" id="video">
    <video controls>
      <source src="" type="video/mp4">
    </video>
  </div>

</div>

<!-- ПОДПИСЬ -->
<div class="footer" id="footer">
Happy birthday, Margot
</div>

<script>
const envelope = document.getElementById("envelope");
const openBtn = document.getElementById("openBtn");
const fakeBtn = document.getElementById("fakeBtn");
const photos = document.querySelectorAll(".photos img");
const footer = document.getElementById("footer");

openBtn.onclick = function () {
  envelope.classList.add("open");

  setTimeout(() => {
    photos.forEach(img => {
      img.style.opacity = 1;
      img.style.top = Math.random() * 70 + "%";
      img.style.left = Math.random() * 70 + "%";
    });

    footer.classList.add("show");
  }, 700);
};

fakeBtn.onclick = function () {
  alert("🙈");
};
</script>

</body>
</html>
