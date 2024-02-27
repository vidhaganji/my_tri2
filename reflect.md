Reflect:
---
layout: base
title: reflect
permalink: /reflect/
--- 

<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Reflect</title>
   <style>
   body {
       font-family: Arial, sans-serif;
       margin: 0;
       padding: 20px;
   }

   h1 {
       text-align: center;
   }

   .entry {
       margin-bottom: 10px;
   }
   </style>
</head>
<body>
   <h1>Reflections</h1>
   <table>
       <thead>
           <tr>
               <th>Timestamp</th>
               <th>Message</th>
           </tr>
       </thead>
       <tbody id="entries"></tbody>
   </table>

   <script>
   // Retrieve saved entries from localStorage
   const entries = JSON.parse(localStorage.getItem('journalEntries'));

   // Display entries in the table
   const entriesContainer = document.getElementById('entries');
   if (entries && entries.length > 0) {
       // Reverse the entries array to display the latest entries first
       entries.reverse().forEach(entry => {
           // Check if entry and timestamp property exist and timestamp is a valid date
           if (entry && entry.timestamp && !isNaN(new Date(entry.timestamp))) {
               const entryRow = document.createElement('tr');
               const timestampCell = document.createElement('td');
               const messageCell = document.createElement('td');

               // Format the timestamp to DD-MM-YYYY
               const timestamp = new Date(entry.timestamp);
               const formattedDate = `${timestamp.getDate().toString().padStart(2, '0')}-${(timestamp.getMonth() + 1).toString().padStart(2, '0')}-${timestamp.getFullYear()}`;

               timestampCell.textContent = formattedDate;
               messageCell.textContent = entry.message;

               entryRow.appendChild(timestampCell);
               entryRow.appendChild(messageCell);

               entriesContainer.appendChild(entryRow);
           }
       });
   } else {
       const noEntriesMsg = document.createElement('p');
       noEntriesMsg.textContent = 'No entries to display.';
       entriesContainer.appendChild(noEntriesMsg);
   }
   </script>
</body>
</html>