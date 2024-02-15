---
layout: base
title: MOOD
permalink: /mood/
--- 

<html lang="en">
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
<head>
    <meta charset="UTF-8">
    <title>Mood</title>
</head>
<body>
<div id="selectedAscii"></div>
<script src="https://vidhaganji.github.io/frontend/assets/js/Mood.js" defer></script>
<div class="purple-form">
        <div id="binaryDurationBadge" class="binary-badge"></div>
        <form id="MoodForm">
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" placeholder="Enter your name" required>
            <label for="MoodType">Mood Type:</label>
            <input type="text" id="MoodType" name="MoodType" placeholder="Enter Mood type" required>
            <label for="duration">Duration (in minutes):</label>
            <input type="number" id="duration" name="duration" placeholder="Enter duration" required>
            <label for="MoodDate">Date of Mood:</label>
            <input type="date" id="MoodDate" name="MoodDate" required>
            <input type="submit" value="Submit">
        </form>
    </div>
    <script>
        const userIDFromLocalStorage = localStorage.getItem('loggedInUserId');
        console.log(userIDFromLocalStorage);
        document.getElementById('MoodForm').addEventListener('submit', function (event) {
            event.preventDefault();
            const name = document.getElementById('name').value;
            const MoodType = document.getElementById('MoodType').value;
            const duration = document.getElementById('duration').value;
            const MoodDate = document.getElementById('MoodDate').value;
            fetch(`http://127.0.0.1:8240/api/users/${userIDFromLocalStorage}`)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Network response was not ok');
                    }
                    return response.json();
                })
                .then(data => {
                    const originalMoodData = Array.isArray(data.Mood) ? data.Mood : [];
                    const originalSleepData = Array.isArray(data.tracking) ? data.tracking : [];
                    const Mood = {
                        "name": name,
                        "MoodType": MoodType,
                        "duration": duration,
                        "MoodDate": MoodDate
                    }
                    const updatedMoodData = [...originalMoodData, Mood];
                    const data2 = {
                        "id": userIDFromLocalStorage,
                        "name": name,
                        "uid": "life",
                        "dob": "10/12/13",
                        "age": "16",
                        "Mood": updatedMoodData,
                        "tracking": originalSleepData
                    };
                    var jsonData = JSON.stringify(data2);
                    fetch(`http://127.0.0.1:8240/api/users/${userIDFromLocalStorage}`, {
                        method: 'PUT',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: jsonData
                    })
                        .then(response => response.json())
                        .then(data => {
                            console.log('Server response:', data);
                        })
                        .catch(error => {
                            console.error('Error:', error);
                        });
                    const binaryDuration = decimalToBinary(duration);
                    displayBinaryBadge(binaryDuration);
                })
                .catch(error => {
                    console.error('Error:', error);
                });
        });
        function decimalToBinary(number) {
            return (number >>> 0).toString(2);
        }
        function displayBinaryBadge(binaryString) {
            const binaryBadgeElement = document.getElementById('binaryDurationBadge');
            binaryBadgeElement.innerHTML = '';
            const overThirtyMinutes = isOverThirtyMinutes(binaryString);
            const overTenMinutes = isOverTenMinutes(binaryString);
            const didPractice = checkPracticeToday(); // Assuming you have a function to check if they practiced today
            const badgeEarned = performOR(overThirtyMinutes, performAND(overTenMinutes, didPractice));
            createBadge(badgeEarned);
        }
        function isOverThirtyMinutes(binaryString) {
            return parseInt(binaryString, 2) >= 30; // Assuming 30 minutes equals binary 11110
        }
        function isOverTenMinutes(binaryString) {
            return parseInt(binaryString, 2) >= 10; // Assuming 10 minutes equals binary 1010
        }
        function checkPracticeToday(MoodDate) {
          const today = new Date(); // Get current date
          const Mood = new Date(MoodDate); // Convert Mood date string to Date object
           // Compare the year, month, and day of both dates
          return (
            today.getFullYear() === Mood.getFullYear() &&
            today.getMonth() === Mood.getMonth() &&
            today.getDate() === Mood.getDate()
            );
        }
        function performOR(flag1, flag2) {
            return (flag1 || flag2) ? 1 : 0;
        }
        function performAND(flag1, flag2) {
            return (flag1 && flag2) ? 1 : 0;
        }
        function createBinaryBadge(duration, isToday) {
            const binaryBadgeElement = document.getElementById('binaryDurationBadge');
            binaryBadgeElement.innerHTML = '';
            if (isToday) {
                const asciiBadge = document.createElement('pre');
                asciiBadge.style.fontSize = '24px';
                asciiBadge.style.lineHeight = '1';
                asciiBadge.style.color = 'green';
                asciiBadge.textContent = 'Today';
                binaryBadgeElement.appendChild(asciiBadge);
            } else if (duration >= 30) {
                const binaryString = (duration >>> 0).toString(2); // Convert duration to binary string
                for (let i = 0; i < binaryString.length; i++) {
                    const span = document.createElement('span');
                    span.textContent = binaryString[i];
                    span.classList.add('binary-digit');
                    binaryBadgeElement.appendChild(span);
                }
            } else {
                for (let i = 0; i < 6; i++) {
                    const span = document.createElement('span');
                    span.textContent = '0';
                    span.classList.add('binary-digit');
                    binaryBadgeElement.appendChild(span);
                }
            }
        }
    function displayBinaryBadge(duration, MoodDate) {
        const binaryBadgeElement = document.getElementById('binaryDurationBadge');
        binaryBadgeElement.innerHTML = '';
        const today = new Date();
        const Mood = new Date(MoodDate);
        const isToday = (
            today.getFullYear() === Mood.getFullYear() &&
            today.getMonth() === Mood.getMonth() &&
            today.getDate() === Mood.getDate()
        );
        createBinaryBadge(duration, isToday);
    }
    </script>
</body>

</html>







