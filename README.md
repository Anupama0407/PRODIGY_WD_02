<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background-color: antiquewhite;
            height: 100vh;
            font-family: Arial, sans-serif;
        }
        .stopwatch {
            font-size: 2rem;
            margin-bottom: 20px;
        }
        .buttons button {
            padding: 10px 20px;
            margin: 5px;
            background-color: rgb(101, 185, 234);
            font-size: 1rem;
            cursor: pointer;
        }
        .laps {
            margin-top: 20px;
            list-style: none;
            padding: 0;
        }
    </style>
</head>
<body>
    <div class="stopwatch">00:00:00</div>
    <div class="buttons">
        <button onclick="startTimer()">Start</button>
        <button onclick="pauseTimer()">Pause</button>
        <button onclick="resetTimer()">Reset</button>
        <button onclick="lapTime()">Lap</button>
    </div>
    <ul class="laps"></ul>
    
    <script>
        let timer;
        let isRunning = false;
        let seconds = 0, minutes = 0, hours = 0;
        let lapCounter = 1;
        
        function updateDisplay() {
            document.querySelector(".stopwatch").textContent = 
                `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
        }
        
        function startTimer() {
            if (!isRunning) {
                isRunning = true;
                timer = setInterval(() => {
                    seconds++;
                    if (seconds === 60) {
                        seconds = 0;
                        minutes++;
                    }
                    if (minutes === 60) {
                        minutes = 0;
                        hours++;
                    }
                    updateDisplay();
                }, 1000);
            }
        }
        
        function pauseTimer() {
            clearInterval(timer);
            isRunning = false;
        }
        
        function resetTimer() {
            clearInterval(timer);
            isRunning = false;
            seconds = 0;
            minutes = 0;
            hours = 0;
            lapCounter = 1;
            document.querySelector(".laps").innerHTML = "";
            updateDisplay();
        }
        
        function lapTime() {
            if (isRunning) {
                let lapItem = document.createElement("li");
                lapItem.textContent = `Lap ${lapCounter}: ${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
                document.querySelector(".laps").appendChild(lapItem);
                lapCounter++;
            }
        }
    </script>
</body>
</html>

