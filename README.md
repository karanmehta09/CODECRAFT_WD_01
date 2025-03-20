# CODECRAFT_WD_01
//index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>stopwatch</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <div class="timer-display">
            00 : 00 : 00 : 000
        </div>
        <div class="buttons">
            <button id="start-timer">Start</button>
            <button id="pause-timer">Pause</button>
            <button id="reset-timer">Reset</button>
        </div>
    </div>

    <script src="script.js"></script>

</body>
</html>

//script.js

let [milliseconds, seconds, minutes, hours] = [0, 0, 0, 0];
let timeRef = document.querySelector(".timer-display");
let int = null;

document.getElementById("start-timer").addEventListener("click", () => {
    if (int !== null) {
        clearInterval(int);
    }
    int = setInterval(displayTimer, 10);
});

document.getElementById("pause-timer").addEventListener("click", () => {
    clearInterval(int);
});

document.getElementById("reset-timer").addEventListener("click", () => {
    clearInterval(int);
    [milliseconds, seconds, minutes, hours] = [0, 0, 0, 0];
    timeRef.innerHTML = "00 : 00 : 00 : 000";
    int = null;
});

function displayTimer() {
    milliseconds += 10;
    if (milliseconds == 1000) {
        milliseconds = 0;
        seconds++;
        if (seconds == 60) {
            seconds = 0;
            minutes++;
            if (minutes == 60) {
                minutes = 0;
                hours++;
            }
        }
    }

    let h = hours < 10 ? "0" + hours : hours;
    let m = minutes < 10 ? "0" + minutes : minutes;
    let s = seconds < 10 ? "0" + seconds : seconds;
    let ms = String(milliseconds).padStart(3, "0");

    timeRef.innerHTML = `${h} : ${m} : ${s} : ${ms}`;
}

//style.css

*,
*:before,
*:after {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

/* Body Background */
body {
    background: #8c52ff;
    font-family: 'Poppins', sans-serif;
}

/* Main Container */
.container {
    background-color: #fff;
    width: 40%;
    min-width: 500px;
    max-width: 700px;
    position: absolute;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    padding: 20px 0;
    padding-bottom: 50px;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.338);
}

/* Timer Display */
.timer-display {
    position: relative;
    width: 92%;
    background: #fff;
    left: 4%;
    font-family: 'Roboto Mono', monospace;
    color: #8c52ff;
    font-size: 30px;
    padding: 40px;
    display: flex;
    align-items: center;
    justify-content: space-around;
    border-radius: 5px;
    box-shadow: 0 0 20px rgba(65, 5, 145, 0.25);
}

/* Buttons Section */
.buttons {
    width: 90%;
    margin: 60px auto 0 auto;
    display: flex;
    justify-content: space-around;
}

/* Buttons Style */
.buttons button {
    width: 120px;
    height: 45px;
    background-color: #8c52ff;
    color: #fff;
    border: none;
    font-family: 'Poppins', sans-serif;
    font-size: 18px;
    border-radius: 5px;
    cursor: pointer;
    outline: none;
    transition: all 0.3s ease-in-out;
}

/* Pause Button */
.buttons button:nth-last-child(2) {
    background-color: #e35209;
}

/* Reset Button */
.buttons button:nth-last-child(1) {
    background-color: #f7df1e;
    color: #000;
}

/* Button Hover Effect */
.buttons button:hover {
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.25);
}

/* Button Click Animation */
.buttons button:active {
    transform: scale(0.95);
}

/* Media Query for Responsiveness */
@media (max-width: 600px) {
    .container {
        width: 90%;
        min-width: unset;
        padding: 15px;
    }
    .timer-display {
        font-size: 20px;
        padding: 20px;
    }
    .buttons {
        flex-direction: column;
        gap: 15px;
    }
    .buttons button {
        width: 100%;
    }
}


