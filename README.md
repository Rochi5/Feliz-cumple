# Feliz-cumple
Feliz cumple a mi amiga &lt;3

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>🎉 Feliz Cumple Coni 🎂</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      color: #333;
    }
    .card {
      margin-top: 20px;
      padding: 20px;
      background: #fff;
      border-radius: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      display: inline-block;
    }
    img {
      width: 250px;
      border-radius: 15px;
      margin-bottom: 20px;
    }
    #snakeCanvas {
      border: 2px solid #333;
      background: #fafafa;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <h1>🎉 ¡Feliz Cumpleaños! 🎂</h1>
  <div class="card">
    <img src="tu_foto.jpg" alt="Foto de Coni">
    <p>Inserta tu apodo:</p>
    <input type="text" id="apodo">
    <button onclick="verificar()">Enviar</button>
    <p id="mensaje"></p>
  </div>

  <canvas id="snakeCanvas" width="300" height="300"></canvas>
  <p id="juegoMensaje"></p>

  <script>
    function verificar() {
      let apodo = document.getElementById("apodo").value.toLowerCase();
      if(apodo === "coni") {
        document.getElementById("mensaje").innerHTML = 
          "🎉 FELIZ CUMPLE AMIGA <3 🎶 Te quiero mucho 💖 Felices 21 🎂 🪇💖";
      } else {
        document.getElementById("mensaje").innerHTML = 
          "❌ Ese no es el apodo correcto...";
      }
    }

    // --- Snake Game ---
    const canvas = document.getElementById("snakeCanvas");
    const ctx = canvas.getContext("2d");

    let box = 15;
    let snake = [{x: 9*box, y: 9*box}];
    let direction = "RIGHT";
    let food = {
      x: Math.floor(Math.random()*20)*box,
      y: Math.floor(Math.random()*20)*box
    };
    let score = 0;

    document.addEventListener("keydown", event => {
      if(event.key === "ArrowLeft" && direction !== "RIGHT") direction = "LEFT";
      if(event.key === "ArrowUp" && direction !== "DOWN") direction = "UP";
      if(event.key === "ArrowRight" && direction !== "LEFT") direction = "RIGHT";
      if(event.key === "ArrowDown" && direction !== "UP") direction = "DOWN";
    });

    function draw() {
      ctx.fillStyle = "#fafafa";
      ctx.fillRect(0,0,300,300);

      for(let i=0; i<snake.length; i++) {
        ctx.fillStyle = (i===0) ? "#ff6f61" : "#333";
        ctx.fillRect(snake[i].x, snake[i].y, box, box);
      }

      ctx.fillStyle = "#00ff00";
      ctx.fillRect(food.x, food.y, box, box);

      let snakeX = snake[0].x;
      let snakeY = snake[0].y;

      if(direction === "LEFT") snakeX -= box;
      if(direction === "UP") snakeY -= box;
      if(direction === "RIGHT") snakeX += box;
      if(direction === "DOWN") snakeY += box;

      if(snakeX === food.x && snakeY === food.y) {
        score++;
        food = {
          x: Math.floor(Math.random()*20)*box,
          y: Math.floor(Math.random()*20)*box
        };
      } else {
        snake.pop();
      }

      let newHead = {x: snakeX, y: snakeY};
      snake.unshift(newHead);

      if(score === 5) {
        document.getElementById("juegoMensaje").innerHTML = 
          "🎉 FELICITACIONES. Te ganaste algo hecho por Fiore <3 🎁";
        clearInterval(game);
      }
    }

    let game = setInterval(draw, 100);
  </script>
</body>
</html>
