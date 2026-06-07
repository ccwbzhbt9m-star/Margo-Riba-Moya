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
  background: #ffd6e8; /* нежно-розовый */
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial;
  overflow: hidden;
}

/* контейнер */
.scene {
  text-align: center;
}

/* пиксельный конверт */
.envelope {
  width: 220px;
  height: 160px;
  background: #ff4d88;
  position: relative;
  margin: auto;
  cursor: pointer;
  image-rendering: pixelated;
  box-shadow: 0 10px 0 #c2185b;
}

/* сердечко */
.heart {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  font-size: 40px;
}

/* кнопки */
.buttons {
  margin-top: 25px;
}

button {
  padding: 10px 18px;
  margin: 5px;
  border: none;
  font-size: 16px;
  cursor: pointer;
  border-radius: 10px;
}

/* Open */
#openBtn {
  background: #ff4d88;
  color: white;
}

/* Fake button */
#fakeBtn {
  background: #ffc1d6;
  position: relative;
}

/* кнопка “не открыть” убегает */
#fakeBtn:hover {
  position: relative;
  left: 40px;
  top: -10px;
}

/* скрытые элементы пока */
.hidden {
  display: none;
}

/* подпись */
.footer {
  position: absolute;
  bottom: 20px;
  width: 100%;
  text-align: center;
  font-size: 22px;
  color: #b30059;
}
</style>
</head>

<body>

<div class="scene">

  <div class="envelope">
    <div class="heart">💗</div>
  </div>

  <div class="buttons">
    <button id="openBtn">Open</button>
    <button id="fakeBtn">Don’t open</button>
  </div>

</div>

<div class="footer">Happy birthday, Margot</div>

<script>
document.getElementById("openBtn").onclick = function() {
  alert("Дальше добавим анимацию открытия 💌");
};
</script>

</body>
</html>