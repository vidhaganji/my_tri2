---
layout: base
title: ap
permalink: /ap/
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Daily Journal</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vanta@0.5.23/dist/vanta.waves.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* Global styles */
        body {
            font-family: 'Playfair Display', serif;
            margin: 0;
            padding: 0;
            background-color: #000;
            color: #fff;
            overflow-y: scroll; /* Allow vertical scrolling */
        }

        #your-element-selector {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }

        /* Journal container styles */
        #journal-container {
            position: relative;
            z-index: 1;
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #000; /* Solid black */
            border-radius: 10px;
            border: 2px solid #aaa; /* Silver border */
            text-align: center; /* Center align journal content */
        }

        h1 {
            font-family: 'Playfair Display', serif; /* Playfair Display font */
            font-weight: 700;
            font-size: 3em; /* Larger font size */
            text-transform: uppercase; /* All caps */
            margin-bottom: 20px; /* Add some space below the heading */
        }

        #prompt-container {
            font-size: 1.5em; /* Larger font size */
            margin-bottom: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-family: 'Playfair Display', serif;
        }

        #prompt {
            margin-right: 10px;
        }

        .btn {
            padding: 20px 40px; /* Larger padding */
            font-size: 1.5em; /* Larger font size */
            background-color: #fff;
            color: #000;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-family: 'Playfair Display', serif;
            transition: background-color 0.3s;
            margin-bottom: 20px;
            display: inline-block; /* Make buttons inline-block */
        }

        .btn:hover {
            background-color: #673ab7; /* Purple */
            color: #fff; /* White */
            background-image: linear-gradient(to right, #673ab7, #512da8); /* Purple water effect */
        }

        .btn:active {
            background-color: transparent;
            background-image: none;
        }

        #entry {
            width: 100%;
            height: 200px; /* Larger height */
            resize: none;
            padding: 10px;
            margin-bottom: 20px;
            box-sizing: border-box;
            background-color: #000;
            border: 2px solid #ccc;
            border-radius: 5px;
            font-family: 'Playfair Display', serif;
            font-size: 16px;
            color: #ccc;
        }

        #rating {
            margin-bottom: 20px;
        }

        .rating-label {
            font-size: 2em; /* Larger emoji size */
            margin: 0 5px; /* Space between emojis */
            cursor: pointer;
        }

        #show-entries-btn {
            padding: 20px 40px; /* Larger padding */
            font-size: 1.5em; /* Larger font size */
            background-color: #fff;
            color: #000;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-family: 'Playfair Display', serif;
            transition: background-color 0.3s;
        }

        #show-entries-btn:hover {
            background-color: #673ab7; /* Purple */
            color: #fff; /* White */
            background-image: linear-gradient(to right, #673ab7, #512da8); /* Purple water effect */
        }

        #show-entries-btn:active {
            background-color: transparent;
            background-image: none;
        }

        #entries-container {
            display: none;
            margin-top: 20px;
            padding: 10px;
            background-color: #111;
            border: 2px solid #ccc;
            border-radius: 5px;
            max-height: 300px;
            overflow-y: auto; /* Allow vertical scrolling */
        }

        .entry {
            margin-bottom: 10px;
            border-bottom: 1px solid #666;
            padding-bottom: 10px;
            font-family: 'Playfair Display', serif;
            font-size: 16px;
            color: #ccc;
        }

        .entry .rating {
            font-size: 1.2em;
        }
    </style>
</head>
<body>
    <div id="your-element-selector"></div>
    <div id="journal-container">
        <h1>DAILY JOURNAL</h1>
        <div id="prompt-container">
            <span id="prompt">Today's Prompt: <span id="daily-prompt"></span></span>
            <button class="btn" id="change-prompt-btn">Change Prompt</button>
        </div>
        <textarea id="entry" placeholder="Enter your journal entry here"></textarea>
        <div id="rating">
            <label class="rating-label" id="rating1" for="rating-1">😡</label>
            <input type="radio" id="rating-1" name="rating" value="1">
            <label class="rating-label" id="rating2" for="rating-2">😞</label>
            <input type="radio" id="rating-2" name="rating" value="2">
            <label class="rating-label" id="rating3" for="rating-3">😐</label>
            <input type="radio" id="rating-3" name="rating" value="3">
            <label class="rating-label" id="rating4" for="rating-4">🙂</label>
            <input type="radio" id="rating-4" name="rating" value="4">
            <label class="rating-label" id="rating5" for="rating-5">😄</label>
            <input type="radio" id="rating-5" name="rating" value="5">
        </div>
        <button class="btn" id="submit-btn">Submit</button>
        <button class="btn" id="show-entries-btn">Show Entries</button>
        <div id="entries-container"></div>
    </div>

    <script>
        VANTA.WAVES({
            el: "#your-element-selector",
            mouseControls: true,
            touchControls: true,
            gyroControls: false,
            minHeight: 200.00,
            minWidth: 200.00,
            scale: 1.00,
            scaleMobile: 1.00,
            color: 0xc5749e,
            shininess: 88.00,
            waveHeight: 40.00,
            waveSpeed: 2.00,
            zoom: 0.65
        });

        // Function to generate timestamp
        function getCurrentTimestamp() {
            const date = new Date();
            return date.toLocaleString(); // Get date and time in local format
        }

        // Function to get a random prompt
        function getRandomPrompt() {
            const prompts = [
                "What made you smile today?",
                "What was the highlight of your day?",
                "What are you grateful for today?",
                "What did you learn today?",
                "What is something you accomplished today?",
                "What's your favorite memory from this week?",
                "Describe a recent act of kindness you experienced or witnessed.",
                "What is a challenge you faced today, and how did you overcome it?",
                "Write about something that inspires you.",
                "What is something new you learned recently?",
                "Describe a moment when you felt proud of yourself.",
                "What is something you're looking forward to?",
                "What's something that made you laugh recently?",
                "Write about a small victory you had today.",
                "Describe something you did today that made you feel good about yourself."
            ];
            return prompts[Math.floor(Math.random() * prompts.length)];
        }

        // Function to set the daily prompt
        function setDailyPrompt() {
            document.getElementById("daily-prompt").textContent = getRandomPrompt();
        }

        // Initialize daily prompt
        setDailyPrompt();

        // Event listener for change prompt button
        document.getElementById("change-prompt-btn").addEventListener("click", function() {
            setDailyPrompt();
        });

        // Event listener for submit button
        document.getElementById("submit-btn").addEventListener("click", function() {
            const entryText = document.getElementById("entry").value.trim();
            const rating = document.querySelector('input[name="rating"]:checked');

            // Save the entry and timestamp to local storage
            if (entryText && rating) {
                const entry = {
                    timestamp: getCurrentTimestamp(),
                    entryText: entryText,
                    rating: rating.value
                };

                let entries = JSON.parse(localStorage.getItem("journalEntries")) || [];
                entries.push(entry);
                localStorage.setItem("journalEntries", JSON.stringify(entries));

                // Reset form
                document.getElementById("entry").value = "";
                document.querySelector('input[name="rating"]:checked').checked = false;
            } else {
                alert("Please enter your journal entry and rate your day.");
            }
        });

        // Event listener for show entries button
        document.getElementById("show-entries-btn").addEventListener("click", function() {
            const entries = JSON.parse(localStorage.getItem("journalEntries")) || [];
            const entriesContainer = document.getElementById("entries-container");
            entriesContainer.innerHTML = ""; // Clear previous entries

            if (entries.length > 0) {
                entries.forEach(entry => {
                    const entryDiv = document.createElement("div");
                    entryDiv.classList.add("entry");

                    const entryText = document.createElement("p");
                    entryText.textContent = entry.entryText;

                    const entryDate = document.createElement("p");
                    entryDate.textContent = "Date: " + entry.timestamp; // Display entry date

                    const rating = document.createElement("p");
                    rating.classList.add("rating");
                    rating.textContent = "Rating: ";
                    for (let i = 0; i < entry.rating; i++) {
                        rating.textContent += "😄"; // Display selected emoji for rating
                    }

                    entryDiv.appendChild(entryDate); // Append date
                    entryDiv.appendChild(entryText);
                    entryDiv.appendChild(rating);
                    entriesContainer.appendChild(entryDiv);
                });

                entriesContainer.style.display = "block";
            } else {
                alert("No entries found!");
            }
        });
    </script>
</body>
</html>





