<html>
<head>
    <style>
        body {
            background-color:#e8d8cf;
        }
        .rectangle2 {
            background-color: #f3eef4;
            height: 56px;
            width: fill;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .button {
            color: #000000;
            font-size: 30px;
            font-family: Kaisei Tokumin;
            line-height: auto;
            border-style: hidden;
            outline: none;
            background: none;
            border: none;
            cursor: pointer;
        }
        .button:hover {
            text-decoration: underline;
        }
        .mentaltherapy {
            font-size: 36px;
            width: auto;
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
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
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
            font-size: 40px; /* Change the font size */
            color: #333; /* Change the text color */
            text-align: center; /* Change the alignment */
            margin-top: 20px; /* Change the top margin */
        }
        .image-container {
        display: flex;
        justify-content: space-around;
        align-items: center;
        margin: 20px 0;
        }
        .image-container img {
            max-width: 600px;
            max-height: 600px;
            margin: 10px;
        }
    </style>
</head>
<body>
    <div class="dropdown">
        <button class='button signins' onclick="location.href='//https://isabellehp.github.io/tri2/';">Sign In Options</button>
        <div class="dropdown-content">
            <a href="">Sign Up </a>
            <a href="https://isabellehp.github.io/tri2/login/">Log In</a>
            <!-- Add more artist links as needed -->
        </div>
    </div>
    <div class="dropdown">
        <button class='button metaltherapy' onclick="location.href='//https://isabellehp.github.io/tri2/homepage';">Mental Therapy</button>
    </div>
    <div class="dropdown">
        <button class='button more' onclick="location.href='//https://isabellehp.github.io/tri2/';">More Help</button>
        <div class="dropdown-content">
            <a href="https://isabellehp.github.io/tri2/2024/02/09/daily_agenda.">Daily Agenda </a>
            <a href="">Moodtracker</a>
            <!-- Add more artist links as needed -->
        </div>
    </div>
</div>

    
    

<!-- Add other sections and content for your homepage here -->
</body>
</html>
