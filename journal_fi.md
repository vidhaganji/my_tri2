---
layout: base
title: journal
permalink: /journal/
--- 
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Daily Journal</title>
   <style>
   body {
   background-color: #fae5de;
   font-family: Arial, sans-serif;
   margin: 0;
   padding: 0;
}


.container {
   max-width: 600px;
   margin: 50px auto;
   padding: 20px;
   background-color: #fff;
   border-radius: 8px;
   box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}


h1 {
   text-align: center;
}


#word-of-the-day {
   margin-bottom: 20px;
   font-size: 24px;
   text-align: center;
   color: #333;
}


textarea {
   width: 100%;
   height: 200px;
   padding: 10px;
   margin-bottom: 20px;
   border: 1px solid #ccc;
   border-radius: 5px;
   resize: none;
}


button {
   display: block;
   width: 100%;
   padding: 10px;
   background-color: #007bff;
   color: #fff;
   border: none;
   border-radius: 5px;
   cursor: pointer;
}


button:hover {
   background-color: #0056b3;
}
   </style>
</head>
<body>
   <div class="container" id="animation">
       <h1>Daily Journal</h1>
       <div id="word-of-the-day"></div>
       <textarea id="journal-entry" placeholder="Write about today's word..."></textarea>
       <button class="button" id="save-entry">Save Entry</button>
   </div>

   <script>
   // Sample words to be used, you can replace this with a more comprehensive list
const words = ['serendipity', 'ephemeral', 'quixotic', 'resilience', 'effervescent'];


function getRandomWord() {
   return words[Math.floor(Math.random() * words.length)];
}


function displayWordOfTheDay() {
   const wordElement = document.getElementById('word-of-the-day');
   const randomWord = getRandomWord();
   wordElement.textContent = `Word of the Day: ${randomWord}`;
}


function saveEntry() {
   const entry = document.getElementById('journal-entry').value;
   if (entry.trim() !== '') {
       // You can add code here to save the journal entry to a database or localStorage
       alert('Entry saved successfully!');
       document.getElementById('journal-entry').value = ''; // Clear the textarea after saving
       // Create a redirect button
       const redirectButton = document.createElement('button');
       redirectButton.textContent = 'Reflect';
       redirectButton.style.display = 'block';
       redirectButton.style.width = '100%';
       redirectButton.style.padding = '10px';
       redirectButton.style.backgroundColor = '#007bff';
       redirectButton.style.color = '#fff';
       redirectButton.style.border = 'none';
       redirectButton.style.borderRadius = '5px';
       redirectButton.style.cursor = 'pointer';
       redirectButton.addEventListener('click', function() {
           window.location.href = /reflect/; // Redirect to the reflect page
       });
       document.querySelector('.container').appendChild(redirectButton);
   } else {
       alert('Please write something before saving!');
   }
}


// Display a new word of the day when the page loads
window.onload = displayWordOfTheDay;


// Event listener for the save button
document.getElementById('save-entry').addEventListener('click', saveEntry);


  
   </script>
</body>
</html>
