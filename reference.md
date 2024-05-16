<script>
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
    function getCurrentTimestamp() {
        const date = new Date();
        return date.toLocaleString(); 
    }

    
    function saveEntryToLocalStorage(entryText) {
        if (entryText) {
            const entry = {
                timestamp: getCurrentTimestamp(),
                entryText: entryText
            };

            let entries = JSON.parse(localStorage.getItem("journalEntries")) || [];
            entries.push(entry);
            localStorage.setItem("journalEntries", JSON.stringify(entries));

            document.getElementById("entry").value = "";
        } else {
            alert("Please enter your journal entry.");
        }
    }

    function showEntries(entries) {
        const entriesContainer = document.getElementById("entries-container");
        entriesContainer.innerHTML = ""; 
        if (entries.length > 0) {
            entries.forEach(entry => {
                const entryDiv = document.createElement("div");
                entryDiv.classList.add("entry");

                const entryText = document.createElement("p");
                entryText.textContent = entry.entryText;

                const entryDate = document.createElement("p");
                entryDate.textContent = "Date: " + entry.timestamp; 

                entryDiv.appendChild(entryDate); 
                entryDiv.appendChild(entryText);
                entriesContainer.appendChild(entryDiv);
            });

            entriesContainer.style.display = "block";
        } else {
            alert("No entries found!");
        }
    }

    initWaveEffect();

    setDailyPrompt();

    document.getElementById("change-prompt-btn").addEventListener("click", setDailyPrompt);

    document.getElementById("show-entries-btn").addEventListener("click", function() {
        const entries = JSON.parse(localStorage.getItem("journalEntries")) || [];
        showEntries(entries);
    });

    document.getElementById("submit-btn").addEventListener("click", function() {
        const entryText = document.getElementById("entry").value.trim();
        saveEntryToLocalStorage(entryText);
    });
</script>

I would like to thank Mr. Lopez, my AP CSP teacher, as well as my group members who were there to support me and for me to augment my knoweldge and code with any further concepts.

Nighthawk Pages (base for webpage): https://github.com/nighthawkcoders/Nighthawk-Pages
