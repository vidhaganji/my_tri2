---
layout: base
title: apreflect
permalink: /apreflect/
---


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Journal Entries</title>
</head>
<body>
    <div id="entries"></div>

    <script>
        // Function to generate Markdown table from journal entries
        function generateMarkdownTable(entries) {
            let markdown = "# Journal Entries\n\n";
            markdown += "| Timestamp (UTC)       | Rating | Entry                                 |\n";
            markdown += "|------------------------|--------|---------------------------------------|\n";

            entries.forEach(entry => {
                markdown += `| ${entry.timestamp}  |   ${entry.rating}    | ${entry.entryText} |\n`;
            });

            return markdown;
        }

        // Retrieve journal entries from local storage
        const entries = JSON.parse(localStorage.getItem("journalEntries")) || [];

        // Generate Markdown table
        const markdownTable = generateMarkdownTable(entries);

        // Display Markdown table
        document.getElementById("entries").innerText = markdownTable;
    </script>
</body>
</html>
