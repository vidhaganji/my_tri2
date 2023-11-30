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
<div>To perform a binary shift, add 0s to the opposite end of the direction asked (if left, add 0 on the right end and vice versa). Then, shift all the numbers down in the direction (left/right) and discard the numbers shifted out of the ends. See image below for an example.</div>
<img src="{{site.baseurl}}/images/shift.png" width="640" length="480">

<h2>How to Convert Binary Numbers Using Power of 2 Rule</h2>
<div>Binary numbers are made up of 0s and 1s, each corresponding to a power of two based on its position. Starting from 1 on the right end, multiply by two each bit to the left. To find the binary number, add the powers of 2 that the 1s coordinate with. A left shift is used to multiply the binary number by 2, and a right shift is used to divide the binary number by 2.</div>
<div>In the example below, the binary number has 8 bits meaning the highest power of 2 reaches 128, and the binary number is 16 + 4 + 1 = 21. When shifted to the left, the binary number becomes 42 since it is multiplied by 2. Check: 32 + 8 + 2 = 42. When shifted to the right, the binary number becomes 10 since it is divided by 2. Check: 8 + 2 = 10.</div>
<img src="{{site.baseurl}}/images/binaryshift.png" width="640" length="480">

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
  <div>In this game, you select which direction of shift you want to perform on a randomly generated binary number using the buttons below. Then, you will be asked to shift the binary number in the direction you chose by 1 position. Input your answer and submit to see if you got it right! After submitting the first question, you will be asked to convert the binary number to decimal.</div>
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
  const positions = 1; // may code random position in the future
  const input = prompt(`Enter the result of ${direction === 'left' ? 'left' : 'right'} shifting the binary number: ${binaryNumber} by ${positions} positions`);
  const answer = direction === 'left'
    ? binaryNumber.slice(positions) + '0'.repeat(positions)
    : '0'.repeat(positions) + binaryNumber.slice(0, -positions);
  // input feedback
  if (input === answer) {
    alert('Correct! :)');
  } else {
    alert(`Incorrect >:( The correct answer is ${answer}. Please review binary shift explanation above.`);
  }
  powerOf2();
}

// binary to decimal using power of 2 rule
function powerOf2(){
  const binaryNumber = generateBinaryNumber(8);
  const decimalValue = binaryToDecimal(binaryNumber);
  const input = prompt(`Enter the decimal value of the binary number: ${binaryNumber}`);
  if (parseInt(input, 10) === decimalValue) {
    alert('Correct! :)');
  } else {
    alert(`Incorrect >:( The correct answer is ${decimalValue}. Please review binary to decimal conversion.`);
  }
}

function binaryToDecimal(binary) {
  return parseInt(binary, 2);
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