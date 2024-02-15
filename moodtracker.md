---
layout: base
title: tracker
permalink: /tracker/
--- 
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Whiteboard and Prompt Generator</title>
  <style>
    body {
      background-color: #fae5de;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 50px;
      position: relative;
    }
    .whiteboard {
      position: relative;
      padding: 20px;
      border: 2px solid #ccc;
      border-radius: 10px;
    }
    .canvas-container {
      position: absolute;
      top: 0;
      left: 0;
    }
    canvas {
      cursor: crosshair;
    }
    .palette {
      display: none;
      margin-top: 20px;
    }
    button {
      margin-right: 10px;
      padding: 10px 20px;
      cursor: pointer;
      border: none;
      background-color: #007bff;
      color: #fff;
      border-radius: 5px;
    }
    button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="prompt-generator">
      <h2>Prompt Generator</h2>
      <button class="button" id="generatePromptBtn">Generate Drawing Prompt</button>
      <p id="prompt"></p>
    </div>
    <div class="palette">
      <input type="color" id="colorPicker" value="#000000">
    </div>
    <div class="whiteboard">
      <h2>Whiteboard</h2>
      <canvas id="whiteboardCanvas" width="600" height="400"></canvas>
    </div>
    <button class="button" id="openPaletteBtn">Open Color Picker</button>
    <button class="button" id="markerBtn">Marker</button>
    <button class="button" id="eraserBtn">Eraser</button>
    <button class="button" id="increaseEraserSizeBtn">Increase Eraser Size</button>
    <button class="button" id="submitBtn">Submit</button>
  </div>
  
  <canvas id="confetti"></canvas>

  <script>
    document.getElementById('generatePromptBtn').addEventListener('click', generateDrawingPrompt);
    document.getElementById('submitBtn').addEventListener('click', showConfetti);
    document.getElementById('openPaletteBtn').addEventListener('click', togglePalette);

    const whiteboardCanvas = document.getElementById('whiteboardCanvas');
    const ctx = whiteboardCanvas.getContext('2d');
    const markerBtn = document.getElementById('markerBtn');
    const eraserBtn = document.getElementById('eraserBtn');
    const increaseEraserSizeBtn = document.getElementById('increaseEraserSizeBtn');
    const colorPicker = document.getElementById('colorPicker');
    const palette = document.querySelector('.palette');
    let isDrawing = false;
    let isErasing = false;
    let eraserSize = 10;

    function generateDrawingPrompt() {
      const prompts = [
        "Draw a landscape with mountains and a river.",
        "Sketch a portrait of someone you admire.",
        "Create a still life drawing of objects on your desk.",
        "Illustrate your favorite fictional character.",
        "Design a futuristic cityscape.",
        "Draw your dream vacation destination."
      ];
      const randomIndex = Math.floor(Math.random() * prompts.length);
      document.getElementById('prompt').innerText = prompts[randomIndex];
    }

    function showConfetti() {
      const canvas = document.getElementById('confetti');
      const ctx = canvas.getContext('2d');
      
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      const pieces = [];

      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        pieces.forEach(function (piece) {
          ctx.beginPath();
          ctx.arc(piece.x, piece.y, piece.size, 0, 2 * Math.PI);
          ctx.fillStyle = piece.color;
          ctx.fill();
        });
      }

      function random(min, max) {
        return Math.random() * (max - min) + min;
      }

      function createPiece() {
        return {
          x: canvas.width / 2,
          y: canvas.height / 2,
          size: random(10, 20),
          angle: random(0, 2 * Math.PI),
          rotation: random(-0.1, 0.1),
          speed: random(1, 5),
          color: 'hsl(' + random(0, 360) + ', 100%, 50%)',
        };
      }

      function update() {
        pieces.forEach(function (piece) {
          piece.x += Math.cos(piece.angle) * piece.speed;
          piece.y += Math.sin(piece.angle) * piece.speed;
          piece.rotation += piece.rotation;
          piece.speed -= 0.1;

          if (piece.y < 0) piece.y = canvas.height;
          if (piece.y > canvas.height) piece.y = 0;
          if (piece.x < 0) piece.x = canvas.width;
          if (piece.x > canvas.width) piece.x = 0;
        });

        pieces.forEach(function (piece, index) {
          if (piece.speed < 0) pieces.splice(index, 1);
        });

        if (pieces.length < 100) pieces.push(createPiece());
      }

      function loop() {
        draw();
        update();
        requestAnimationFrame(loop);
      }

      loop();
    }

    whiteboardCanvas.addEventListener('mousedown', startDrawing);
    whiteboardCanvas.addEventListener('mouseup', stopDrawing);
    whiteboardCanvas.addEventListener('mousemove', draw);

    markerBtn.addEventListener('click', function() {
      isErasing = false;
      markerBtn.classList.add('active');
      eraserBtn.classList.remove('active');
    });

    eraserBtn.addEventListener('click', function() {
      isErasing = true;
      eraserBtn.classList.add('active');
      markerBtn.classList.remove('active');
    });

    increaseEraserSizeBtn.addEventListener('click', function() {
      eraserSize += 5;
    });

    colorPicker.addEventListener('change', function() {
      ctx.strokeStyle = colorPicker.value;
    });

    function togglePalette() {
      palette.style.display = palette.style.display === 'none' ? 'block' : 'none';
    }

    function startDrawing(e) {
      isDrawing = true;
      draw(e);
    }

    function stopDrawing() {
      isDrawing = false;
    }

    function draw(e) {
      if (!isDrawing) return;

      const x = e.clientX - whiteboardCanvas.getBoundingClientRect().left;
      const y = e.clientY - whiteboardCanvas.getBoundingClientRect().top;

      ctx.lineWidth = isErasing ? eraserSize : 2;
      ctx.lineCap = 'round';

      if (isErasing) {
        ctx.globalCompositeOperation = 'destination-out';
      } else {
        ctx.globalCompositeOperation = 'source-over';
      }

      ctx.lineTo(x, y);
      ctx.stroke();
      ctx.beginPath();
      ctx.moveTo(x, y);
    }
  </script>
</body>
</html>
