<html>
<head>
    <style>
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
<script src="{{site.baseurl}}/assets/js/three.r134.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.clouds.min.js"></script>

<script>
  

VANTA.CLOUDS ({
  el: "#animation",
  mouseControls: true,
  touchControls: true,
  gyroControls: false,
  skyColor: 0xf9d1d1,
  cloudColor: 0xbba2a8,
  cloudShadowColor: 0x905167,
  sunColor: 0x845d66,
  sunGlareColor: 0x5e2610,
  speed: 0.80
})
<body>
    <div id='rectangle2' class='rectangle2'>
        <div class="dropdown">
            <button class='button signins' onclick="location.href='//https://isabellehp.github.io/tri2/';';">Sign In Options</button>
            <div class="dropdown-content">
                <a href="">Sign Up </a>
                <a href="https://isabellehp.github.io/tri2/login/">Log In</a>
                <!-- Add more artist links as needed -->
            </div>
        </div>
        <div class="dropdown">
            <button class='button metaltherapy' onclick="location.href='//https://isabellehp.github.io/tri2/homepage';">Mental Therapy</button>

    <!-- Add other sections and content for your homepage here -->
</body>
</html>
