---
toc: true
comments: true
layout: post
title: Binary Color by Number
description: Use binary's help to pick different colors!
type: hacks
courses: { compsci: {week: 13} }
---


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Color by Number</title>
    <style>
        canvas {
            border: 1px solid #000;
        }
    </style>
</head>
<body>

<h1>Color by Number</h1>
<p>This is a fun color by number game that can help you with learning binary where you can type in the binary representation for each number to fill in the boxes. If you fill in all the boxes, congrats! Have fun learning binary.</p>

<h2> Instructions on How to Play </h2>
<p>Enter the binary representation for each number to color the corresponding spot:</p>

<h3> Color with me! </h3>

<canvas id="coloringCanvas" width="300" height="300"></canvas>
<br>
<label for="binaryInput">Enter binary:</label>
<input type="text" id="binaryInput" placeholder="Enter binary">
<button onclick="colorByBinary()">Color</button>

<script>
    // Updated coloring data for a smiley face
    const coloringData = [
        [1, 2, 3, 4, 5],
        [6, 7, 8, 9, 10],
        [11, 12, 13, 14, 15],
        [16, 17, 18, 19, 20],
        [21, 22, 23, 24, 25],
    ];

    const canvas = document.getElementById('coloringCanvas');
    const ctx = canvas.getContext('2d');

    // Draw initial coloring
    drawColoring(coloringData);

    function drawColoring(data) {
        const cellSize = canvas.width / data.length;

        // Clear canvas
        ctx.fillStyle = '#fff';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        for (let i = 0; i < data.length; i++) {
            for (let j = 0; j < data[i].length; j++) {
                const x = j * cellSize;
                const y = i * cellSize;

                // Draw number
                ctx.fillStyle = '#000';
                ctx.font = '20px Arial';
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';
                ctx.fillText(data[i][j], x + cellSize / 2, y + cellSize / 2);
            }
        }
    }

    function getColorByBinary(number) {
        const binaryString = Number(number).toString(2);
        const binaryColor = '#' + binaryString.padStart(6, '0'); // Use first 6 characters as hex color
        return binaryColor;
    }

    function colorByBinary() {
        const binaryInput = document.getElementById('binaryInput').value;
        const binaryNumber = parseInt(binaryInput, 2);

        // Find and color the corresponding number
        for (let i = 0; i < coloringData.length; i++) {
            for (let j = 0; j < coloringData[i].length; j++) {
                if (coloringData[i][j] === binaryNumber) {
                    const color = getColorByBinary(binaryNumber);
                    ctx.fillStyle = color;
                    ctx.fillRect(j * (canvas.width / coloringData.length), i * (canvas.height / coloringData.length), canvas.width / coloringData.length, canvas.height / coloringData.length);
                    return;
                }
            }
        }

        alert('Number not found in the coloring!');
    }
</script>

</body>
</html>
