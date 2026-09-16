# Feliz-cumple
Feliz cumple a mi amiga &lt;3

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>🎉 Feliz Cumple Coni 🎂</title>
  <style>
    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      text-align: center;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      color: #333;
    }
    .card {
      margin-top: 20px;
      padding: 20px;
      background: #fff;
      border-radius: 20px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.3);
      display: inline-block;
    }
    img {
      width: 250px;
      border-radius: 15px;
      margin-bottom: 20px;
    }
    #snakeCanvas {
      border: 3px solid #ff6f61;
      background: #fafafa;
      margin-top: 20px;
      display: none;
    }
    #mensaje {
      font-size: 2em;
      font-weight: bold;
      color: #ff0066;
      margin-top: 15px;
      text-shadow: 2px 2px #fff;
    }
    #juegoMensaje {
      font-size: 1.2em;
      margin-top: 10px;
      color: #333;
    }
    #score {
      font-size: 1.3em;
      color: #0066ff;
      margin-top: 10px;
    }
    #retryBtn {
      display: none;
      margin-top: 10px;
      padding: 10px 20px;
      background: #ff6f61;
      color: #fff;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>🎉 ¡Feliz Cumpleaños! 🎂</h1>
  <div class="card">
    <img src="Coni_foto.jpg" alt="Foto de Coni">
    <p>Inserta tu apodo:</p>
    <input type="text" id="apodo">
    <button onclick="verificar()">Enviar</button>
    <p id="mensaje"></p>
  </div>

  <canvas id="snakeCanvas" width="300" height="300"></canvas>
  <p id="score"></p>
  <p id="juegoMensaje"></p>
  <button id="retryBtn" onclick="reiniciarJuego()">🔄 Reintentar</button>

  <div id="tutorial" style="display:none; margin-top:20px;">
    <h3>📖 Cómo jugar:</h3>
    <p>Usa las flechas del teclado ⬅️ ⬆️ ➡️ ⬇️ para mover la serpiente.</p>
    <p>Come la comida verde 🍏 para ganar puntos.</p>
    <p>Si chocas contra los bordes o contigo misma 💀 → Game Over.</p>
    <p>Al llegar a 5 puntos 🎉 → ¡Sorpresa especial!</p>
  </div>

  <script>
    function verificar() {
      let apodo = document.getElementById("apodo").value.toLowerCase();
      if(apodo === "coni") {
        document.getElementById("mensaje").innerHTML = 
          "✨ FELIZ CUMPLE AMIGA 💖<br>TE QUIERO MUCHO 🎂🎶";
        document.getElementById("snakeCanvas").style.display = "block";
        document.getElementById("tutorial").style.display = "block";
        iniciarJuego();
      } else {
        document.getElementById("mensaje").innerHTML = 
          "❌ Ese no es el apodo correcto...";
      }
    }

    let canvas, ctx, box, snake, direction, food, score, game;

    function iniciarJuego() {
      canvas = document.getElementById("snakeCanvas");
      ctx = canvas.getContext("2d");
      box = 15;
      snake = [{x: 9*box, y: 9*box}];
      direction = "RIGHT";
      food = {
        x: Math.floor(Math.random()*20)*box,
        y: Math.floor(Math.random()*20)*box
      };
      score = 0;
      document.getElementById("score").innerHTML = "⭐ Puntos: " + score;
      document.getElementById("juegoMensaje").innerHTML = "";
      document.getElementById("retryBtn").style.display = "none";
      if(game) clearInterval(game);
      game = setInterval(draw, 200); // más lento y jugable
    }

    function reiniciarJuego() {
      iniciarJuego();
    }

    function draw() {
      ctx.fillStyle = "#fafafa";
      ctx.fillRect(0,0,300,300);

      for(let i=0; i<snake.length; i++) {
        ctx.fillStyle = (i===0) ? "#ff0066" : "#333";
        ctx.fillRect(snake[i].x, snake[i].y, box, box);
        ctx.strokeStyle = "#fff";
        ctx.strokeRect(snake[i].x, snake[i].y, box, box);
      }

      ctx.fillStyle = "#00cc00";
      ctx.fillRect(food.x, food.y, box, box);

      let snakeX = snake[0].x;
      let snakeY = snake[0].y;

      if(direction === "LEFT") snakeX -= box;
      if(direction === "UP") snakeY -= box;
      if(direction === "RIGHT") snakeX += box;
      if(direction === "DOWN") snakeY += box;

      if(snakeX === food.x && snakeY === food.y) {
        score++;
        document.getElementById("score").innerHTML = "⭐ Puntos: " + score;
        food = {
          x: Math.floor(Math.random()*20)*box,
          y: Math.floor(Math.random()*20)*box
        };
      } else {
        snake.pop();
      }

      let newHead = {x: snakeX, y: snakeY};
      snake.unshift(newHead);

      if(snakeX < 0 || snakeY < 0 || snakeX >= 300 || snakeY >= 300 ||
         snake.slice(1).some(seg => seg.x === snakeX && seg.y === snakeY)) {
        clearInterval(game);
        document.getElementById("juegoMensaje").innerHTML = "💀 Game Over";
        document.getElementById("retryBtn").style.display = "inline-block";
      }

      if(score === 5) {
        document.getElementById("juegoMensaje").innerHTML = 
          "🎉 FELICITACIONES. Te ganaste algo hecho por Fiore <3 🎁";
        clearInterval(game);
        document.getElementById("retryBtn").style.display = "inline-block";
      }
    }
  </script>
</body>
</html>

