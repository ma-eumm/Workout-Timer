# Workout-Timer
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <style>
    #time-display { font-size: 48px; margin-bottom: 10px; }
    button { font-size: 16px; margin: 5px; padding: 10px 20px; }
  </style>
</head>
<body>
  <div id="time-display">00:00</div>
  <button id="add-minute">+1 min</button>
  <button id="subtract-minute">–1 min</button><br/>
  <button id="start-timer">Start</button>
  <button id="pause-timer" disabled>Pause</button>
  <button id="reset-timer">Reset</button>
  <script>
    let minutes = 0, seconds = 0, interval = null;
    const display = document.getElementById('time-display'),
          addMin = document.getElementById('add-minute'),
          subMin = document.getElementById('subtract-minute'),
          startBtn = document.getElementById('start-timer'),
          pauseBtn = document.getElementById('pause-timer'),
          resetBtn = document.getElementById('reset-timer');

    function updateDisplay(){
      display.textContent = String(minutes).padStart(2,'0') + ':' + String(seconds).padStart(2,'0');
    }

    addMin.onclick = () => { minutes++; updateDisplay(); };
    subMin.onclick = () => { if(minutes>0) minutes--; else seconds=0; updateDisplay(); };
    startBtn.onclick = () => {
      if(interval) return;
      startBtn.disabled = true;
      pauseBtn.disabled = false;
      interval = setInterval(() => {
        if(seconds === 0){
          if(minutes === 0){
            clearInterval(interval);
            interval = null;
            startBtn.disabled = false;
            pauseBtn.disabled = true;
            alert('Time’s up!');
          } else {
            minutes--; seconds = 59;
          }
        } else seconds--;
        updateDisplay();
      }, 1000);
    };
    pauseBtn.onclick = () => {
      if(interval){ clearInterval(interval); interval = null; startBtn.disabled = false; }
    };
    resetBtn.onclick = () => {
      clearInterval(interval);
      interval = null;
      minutes = 0; seconds = 0;
      startBtn.disabled = false;
      pauseBtn.disabled = true;
      updateDisplay();
    };

    updateDisplay();
  </script>
</body>
</html>
