---
toc: true
comments: true
layout: post
title: Binary Shift
description: Learn binary shift and test your knowledge!
type: hacks
courses: { compsci: {week: 13} }
---

<html lang="en">
<h2>How to do Binary Shift</h2>
<div>To perform a binary shift, add as many zeroes as the number of positions to the opposite end of the direction asked (if left, add zero on the right side and vice versa). Then, shift all the numbers down in the direction (left/right) and discard the numbers shifted out of the ends. See image below for an example.</div>

<img src="{{site.baseurl}}/images/shift.png" width="640" length="480">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <h2>Binary Shift Demo</h2>
</head>
<body>

  <p>Binary Number: <span id="binaryNumber">01011101</span></p>

  <button class="button" onclick="shiftLeft()">Shift Left</button>
  <button class="button" onclick="shiftRight()">Shift Right</button>
</body>

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <h2>Binary Shift Game</h2>
</head>
<body>
  <div>In this game, you select which direction of shift you want to perform on a randomly generated binary number using the buttons below. Then, you will be asked to shift the binary number in the direction you chose by 1 position. Input your answer and submit to see if you got it right!</div>
  <div class="container">
    <div class="output" id="output"></div>
    <div class="button" id="left-shift" onclick="shift('left')">Shift Left</div>
    <div class="button" id="right-shift" onclick="shift('right')">Shift Right</div>
  </div>
  <script src="script.js"></script>
</body>
</html>

<script>
// demo code
let binaryNumber = parseInt("01011101", 2); // Initial binary number (in decimal form)

function updateBinaryDisplay() {
  document.getElementById("binaryNumber").textContent = binaryNumber.toString(2).padStart(8, '0');
}

function shiftLeft() {
  binaryNumber <<= 1; // Shift the binary number to the left
  updateBinaryDisplay();
}

function shiftRight() {
  binaryNumber >>= 1; // Shift the binary number to the right
  updateBinaryDisplay();
}
// end of demo code

// game code
// generate a random binary number with certain number of bits
function generateBinaryNumber(bits) {
  return Math.floor(Math.random() * Math.pow(2, bits)).toString(2).padStart(bits, '0');
}
// direction of shift
function shift(direction) {
  const output = document.getElementById('output');
  const binaryNumber = generateBinaryNumber(8); // here you can change the number of bits, right now there are 8
  output.textContent = binaryNumber; // updates the output div with the shifted binary number
  const positions = 1; // may code random position in the future
  const playerAnswer = prompt(`Enter the result of ${direction === 'left' ? 'left' : 'right'} shifting the binary number: ${binaryNumber} by ${positions} positions`);
  const correctAnswer = direction === 'left'
    ? binaryNumber.slice(positions) + '0'.repeat(positions)
    : '0'.repeat(positions) + binaryNumber.slice(0, -positions);
  // input feedback
  if (playerAnswer === correctAnswer) {
    alert('Correct! :)');
  } else {
    alert(`Incorrect >:( The correct answer is ${correctAnswer}. Please review binary shift explanation above.`);
  }
}

</script>
<script src="{{site.baseurl}}/assets/js/three.r134.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.clouds.min.js"></script>

<script>

VANTA.CLOUDS ({
  el: "#animation",
  mouseControls: true,
  touchControls: true,
  gyroControls: false,
  minHeight: 200.00,
  minWidth: 200.00,
  skyColor: 0xf9d1d1,
  cloudColor: 0xbba2a8,
  cloudShadowColor: 0x905167,
  sunColor: 0x845d66,
  sunGlareColor: 0x5e2610,
  speed: 0.80
})
</script>