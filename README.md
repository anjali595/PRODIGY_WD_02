# PRODIGY_WD_02
This project is an interactive Stopwatch Web Application built using HTML, CSS and JS. It allows users to start, pause, reset and track lap times in a user-friendly and visually appealing way. The application features an elegant design with smooth transitions, hover effects, and a responsive layout that adapts seamlessly to different screen sizes.

CODE:
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stopwatch Web Application</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #6a11cb, #2575fc); 
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .stopwatch-container {
      text-align: center;
      background-color: rgba(255, 255, 255, 0.9); 
      padding: 40px;
      border-radius: 12px;
      box-shadow: 0 15px 40px rgba(0, 0, 0, 0.1);
      width: 350px;
      transition: transform 0.3s ease;
    }

    .stopwatch-container:hover {
      transform: translateY(-10px); 
    }

    #display {
      font-size: 60px;
      margin: 30px 0;
      color: #333;
      font-weight: bold;
      letter-spacing: 2px;
      transition: color 0.5s ease;
    }

    .button-container {
      display: flex;
      justify-content: space-between;
      margin-top: 20px;
      gap: 20px;
    }

    button {
      padding: 12px 25px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      background-color: #007bff;
      color: white;
      transition: background-color 0.3s ease, transform 0.2s ease;
      width: 100px;
    }

    button:hover {
      background-color: #0056b3;
      transform: scale(1.1);
    }

    button:active {
      background-color: #004085;
      transform: scale(1);
    }

    button:focus {
      outline: none;
    }

    #lap-list {
      margin-top: 30px;
      padding: 0;
      list-style-type: none;
      text-align: left;
      max-height: 200px;
      overflow-y: auto;
    }
    #lap-list li {
      background-color: #f0f0f0;
      padding: 10px;
      margin: 8px 0;
      border-radius: 8px;
      font-size: 16px;
      color: #555;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    #lap-list::-webkit-scrollbar {
      width: 6px;
    }
    #lap-list::-webkit-scrollbar-thumb {
      background-color: #007bff;
      border-radius: 10px;
    }
    @media (max-width: 768px) {
      .stopwatch-container {
        width: 90%;
      }

      #display {
        font-size: 48px;
      }

      button {
        width: 80px;
        font-size: 16px;
      }
    }
  </style>
</head>
<body>
  <div class="stopwatch-container">
    <div id="display">00:00:00</div>
    <div class="button-container">
      <button id="start-stop">Start</button>
      <button id="reset">Reset</button>
      <button id="lap">Lap</button>
    </div>
    <ul id="lap-list"></ul>
  </div>

  <script>
    let timer;
    let isRunning = false;
    let seconds = 0;
    let minutes = 0;
    let hours = 0;

    const display = document.getElementById('display');
    const startStopButton = document.getElementById('start-stop');
    const resetButton = document.getElementById('reset');
    const lapButton = document.getElementById('lap');
    const lapList = document.getElementById('lap-list');

    function startStopwatch() {
      if (isRunning) {
        clearInterval(timer);
        startStopButton.textContent = 'Start';
      } else {
        timer = setInterval(updateTime, 1000);
        startStopButton.textContent = 'Pause';
      }
      isRunning = !isRunning;
    }
    function updateTime() {
      seconds++;
      if (seconds === 60) {
        seconds = 0;
        minutes++;
      }
      if (minutes === 60) {
        minutes = 0;
        hours++;
      }
      display.textContent = formatTime(hours, minutes, seconds);
    }
    function formatTime(h, m, s) {
      return `${padZero(h)}:${padZero(m)}:${padZero(s)}`;
    }
    function padZero(num) {
      return num < 10 ? `0${num}` : num;
    }
    function resetStopwatch() {
      clearInterval(timer);
      isRunning = false;
      seconds = 0;
      minutes = 0;
      hours = 0;
      display.textContent = '00:00:00';
      startStopButton.textContent = 'Start';
      lapList.innerHTML = '';
    }
    function recordLap() {
      if (isRunning) {
        const lapTime = formatTime(hours, minutes, seconds);
        const lapItem = document.createElement('li');
        lapItem.textContent = `Lap: ${lapTime}`;
        lapList.appendChild(lapItem);
      }
    }
    startStopButton.addEventListener('click', startStopwatch);
    resetButton.addEventListener('click', resetStopwatch);
    lapButton.addEventListener('click', recordLap);
  </script>

</body>
</html>
