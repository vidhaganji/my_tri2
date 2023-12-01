---
toc: true
comments: true
layout: post
title: Binary Color Picker 
description: Use binary's help to pick different colors!
type: hacks
courses: { compsci: {week: 13} }
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binary Color Picker</title>
    <style>
        #container {
            display: flex;
            align-items: center;
            flex-direction: column;
        }
        #explanation {
            margin-bottom: 20px;
            text-align: center;
        }
        #sliders {
            margin-bottom: 20px;
        }
        #colorDisplayContainer {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        #colorDisplay {
            width: 200px;
            height: 200px;
            border: 1px solid #000;
            border-radius: 50%;
            margin-bottom: 10px;
        }
        #binaryRepresentationContainer {
            position: relative;
            display: inline-block;
            margin-top: 10px;
        }
        #binaryRepresentation {
            font-size: 18px;
        }
        #binaryRepresentationBox {
            position: absolute;
            background-color: #fff;
            border: 2px solid #000;
            border-radius: 10px;
            padding: 10px;
            display: none;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }
        #binaryRepresentationContainer:hover #binaryRepresentationBox {
            display: block;
        }
        #searchContainer {
            margin-top: 20px;
            display: flex;
            align-items: center;
        }
        #searchInput {
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <h1>Binary Color Picker</h1>
    <div id="container">
        <div id="explanation">
            <p>The Binary Color Picker allows you to explore colors using both binary and RGB representations. RGB (Red, Green, Blue) is a common color model in which colors are represented as combinations of red, green, and blue components. Each component can have values ranging from 0 to 255, defining the intensity of each color.</p>
            <p>In contrast, binary representation uses a base-2 numeral system with only two digits, 0 and 1. In this color picker, the RGB values are converted to their binary equivalents, showcasing the binary representation of each color component. The resulting binary string represents the color in a concise sequence of 0s and 1s.</p>
        </div>
        <h1>Slide to pick a color!</h1>
        <div id="sliders">
            <form>
                <label for="red">Red:</label>
                <input type="range" id="red" name="red" min="0" max="255" value="0">
                <br>
                <label for="green">Green:</label>
                <input type="range" id="green" name="green" min="0" max="255" value="0">
                <br>
                <label for="blue">Blue:</label>
                <input type="range" id="blue" name="blue" min="0" max="255" value="0">
                <br>
                <button type="button" onclick="pickColor()">Pick Color</button>
            </form>
        </div>
        <div id="colorDisplayContainer">
            <div id="colorDisplay"></div>
            <div id="binaryRepresentationContainer">
                <div id="binaryRepresentation"></div>
                <div id="binaryRepresentationBox">
                    <p>Color Hex Code: <span id="hexCode"></span></p>
                </div>
            </div>
        </div>
        <div id="searchContainer">
            <input type="text" id="searchInput" placeholder="Enter Binary Code">
            <button type="button" onclick="searchColorByBinary()">Search Color</button>
        </div>
    </div>
    <script>
        function pickColor() {
            var red = document.getElementById("red").value;
            var green = document.getElementById("green").value;
            var blue = document.getElementById("blue").value;
            var binaryRed = decimalToBinary(red, 8);
            var binaryGreen = decimalToBinary(green, 8);
            var binaryBlue = decimalToBinary(blue, 8);
            var binaryColor = binaryRed + binaryGreen + binaryBlue;
            var color = "rgb(" + red + "," + green + "," + blue + ")";
            document.getElementById("colorDisplay").style.backgroundColor = color;
            document.getElementById("binaryRepresentation").innerText = "Binary Color: " + binaryColor;
            document.getElementById("hexCode").innerText = rgbToHex(red, green, blue);
        }
        function searchColorByBinary() {
            var searchInput = document.getElementById("searchInput").value;
            // Assume searchInput is a valid binary string (you might want to add validation)
            var redBinary = searchInput.substring(0, 8);
            var greenBinary = searchInput.substring(8, 16);
            var blueBinary = searchInput.substring(16, 24);
            // Convert binary to decimal
            var red = parseInt(redBinary, 2);
            var green = parseInt(greenBinary, 2);
            var blue = parseInt(blueBinary, 2);
            // Update sliders and display color
            document.getElementById("red").value = red;
            document.getElementById("green").value = green;
            document.getElementById("blue").value = blue;
            pickColor();
        }
        function decimalToBinary(decimalValue, length) {
            return padWithZeros(Number(decimalValue).toString(2), length);
        }
        function padWithZeros(binaryString, length) {
            while (binaryString.length < length) {
                binaryString = '0' + binaryString;
            }
            return binaryString;
        }
        function rgbToHex(r, g, b) {
            return "#" + componentToHex(r) + componentToHex(g) + componentToHex(b);
        }
        function componentToHex(c) {
            var hex = c.toString(16);
            return hex.length == 1 ? "0" + hex : hex;
        }
    </script>
</body>
</html>