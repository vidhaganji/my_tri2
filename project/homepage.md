---
layout: base
title: Homepage
permalink: /homepage/
--- 
<html lang="en">
<head>
    <style>
        body {
            background-color: #fae5de;
            margin: 0;
            padding: 0;
            font-family: 'Kaisei Tokumin', sans-serif;
        }
        #rectangle2 {
            display: flex;
            justify-content: space-around;
            align-items: center;
            height: 80px;
            background-color: #db948f;
            border: 3px solid;
            border-image: linear-gradient(to right, #6b4f4d, #d69092);
            border-image-slice: 1;
            border-radius: 8px;
            margin-top: 20px;
        }
        .button {
            color: #000000;
            font-size: 20px;
            line-height: auto;
            border-style: hidden;
            outline: none;
            background: none;
            border: none;
            cursor: pointer;
            margin: 0;
            padding: 10px;
        }
        .button:hover {
            text-decoration: underline;
        }
        .dropdown {
            position: relative;
            display: inline-block;
        }
        .dropdown-content {
            display: none;
            position: absolute;
            background-color: #f9f9f9;
            min-width: 160px;
            box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
            z-index: 1;
        }
        .dropdown-content a {
            color: black;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
        }
        .dropdown:hover .dropdown-content {
            display: block;
        }
        h1 {
            font-size: 40px;
            color: #333;
            text-align: center;
            margin-top: 20px;
        }
        .image-container {
            display: flex;
            justify-content: space-around;
            align-items: center;
            margin: 20px 0;
        }
        .image-container img {
            max-width: 400px;
            max-height: 400px;
            margin: 10px;
            border: 3px solid #d69092;
            border-radius: 8px;
        }
    </style>
</head>
<body>
    <div id='rectangle2'>
        <div class="dropdown">
            <button class='button signins' onclick="location.href='//https://isabellehp.github.io/tri2/';">Sign In Options</button>
            <div class="dropdown-content">
                <a href="https://isabellehp.github.io/tri2/Register/">Sign Up</a>
                <a href="https://isabellehp.github.io/tri2/login/">Log In</a>
            </div>
        </div>
        <div class="dropdown">
            <button class='button metaltherapy' onclick="location.href=//https://isabellehp.github.io/tri2/';">Improving Your Mental Health</button>
        </div>
        <div class="dropdown">
            <button class='button more' onclick="location.href='//https://isabellehp.github.io/tri2/';">More Help</button>
            <div class="dropdown-content">
                <a href="https://isabellehp.github.io/tri2/info">More Information</a>
                <a href="https://isabellehp.github.io/tri2/2024/02/09/daily_agenda">Daily Agenda</a>
                <a href="https://isabellehp.github.io/tri2/2024/02/08/mood-tracker">Moodtracker</a>
            </div>
        </div>
    </div>
    <h1>More on Mental Health</h1>
    <div class="image-container">
        <img src="/tri2/images/people.png" alt="Image 1 Description">
        <img src="/tri2/images/anxiety.png" alt="Image 2 Description">
        <img src="/tri2/images/therapy.png" alt="Image 3 Description">
    </div>
</body>
</html>
