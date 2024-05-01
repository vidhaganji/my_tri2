---
layout: base
title: ap
permalink: /ap/
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Daily Journal</title>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&display=swap" rel="stylesheet">
    
    <!-- Internal CSS -->
    <style>
        /* Global styles */
        body {
            font-family: 'Playfair Display', serif;
            margin: 0;
            padding: 0;
            overflow-y: scroll; /* Allow vertical scrolling */
            background-color: #f5f5f5; /* Light grey background */
        }

        /* Journal container styles */
        #journal-container {
            position: relative;
            z-index: 1;
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #d3d3d3; /* Pale grey, silverish */
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

        #vanta-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
    </style>
</head>
<body>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Journal App</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://www.vantajs.com/dist/vanta.waves.min.js"></script>
</head>
<body>
    <div id="vanta-background"></div>
    <h1>DAILY JOURNAL</h1>
        
        <!-- Prompt Section -->
        <div id="prompt-container">
            <span id="prompt">Today's Prompt: <span id="daily-prompt"></span></span>
            <button class="btn" id="change-prompt-btn">Change Prompt</button>
        </div>
        
        <!-- Journal Entry Section -->
        <textarea id="entry" placeholder="Enter your journal entry here"></textarea>
        
        <!-- Submit Button -->
        <button class="btn" id="submit-btn">Submit</button>
        
        <!-- Show Entries Button -->
        <button class="btn" id="show-entries-btn">Show Entries</button>
        
        <!-- Entries Container -->
        <div id="entries-container"></div>
    <script>
        // Initialize wave effect
        function initWaveEffect() {
            VANTA.WAVES({
                el: "#vanta-background",
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
        }

        // function which generates timestamp
        function getCurrentTimestamp() {
            const date = new Date();
            return date.toLocaleString(); // Get date and time in local format
        }

        // Function to save the entry to local storage
        function saveEntryToLocalStorage(entryText) {
            if (entryText) {
                const entry = {
                    timestamp: getCurrentTimestamp(),
                    entryText: entryText
                };

                let entries = JSON.parse(localStorage.getItem("journalEntries")) || [];
                entries.push(entry);
                localStorage.setItem("journalEntries", JSON.stringify(entries));

                // Reset form
                document.getElementById("entry").value = "";

                return true;
            } else {
                alert("Please enter your journal entry.");
                return false;
            }
        }

        // Function to display journal entries
        function showEntries() {
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

                    entryDiv.appendChild(entryDate); // Append date
                    entryDiv.appendChild(entryText);
                    entriesContainer.appendChild(entryDiv);
                });

                entriesContainer.style.display = "block";
            } else {
                alert("No entries found!");
            }
        }

        // Function to set the daily prompt
        function setDailyPrompt() {
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
            const randomIndex = Math.floor(Math.random() * prompts.length);
            const prompt = prompts[randomIndex];
            document.getElementById("daily-prompt").textContent = prompt;
        }

        // Initialize wave effect
        initWaveEffect();

        // Initialize daily prompt
        setDailyPrompt();

        // Event listener for change prompt button
        document.getElementById("change-prompt-btn").addEventListener("click", setDailyPrompt);

        // Event listener for show entries button
        document.getElementById("show-entries-btn").addEventListener("click", showEntries);

        // Event listener for submit button
        document.getElementById("submit-btn").addEventListener("click", function() {
            const entryText = document.getElementById("entry").value.trim();
            if (saveEntryToLocalStorage(entryText)) {
                showEntries();
            }
        });
    </script>
</body>
</html>

</body>
</html>

