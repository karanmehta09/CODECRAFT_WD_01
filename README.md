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

