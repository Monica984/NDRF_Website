<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Disaster Ready Challenge (AI Edition)</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      text-align: center;
      padding: 0;
      margin: 0;
      overflow: hidden;
      transition: background 0.8s ease;
      color: #01579b;
    }

    /* Start Screen */
    #start-screen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background: linear-gradient(135deg, #0288d1, #ff7043);
      color: white;
      animation: fadeIn 1s ease;
      z-index: 10;
    }

    #start-screen h1 {
      font-size: 2.8em;
      margin: 10px 0;
    }

    #start-screen p {
      font-size: 1.2em;
      margin-bottom: 30px;
    }

    #start-button {
      padding: 15px 40px;
      font-size: 18px;
      border: none;
      border-radius: 50px;
      background: white;
      color: #ff7043;
      cursor: pointer;
      font-weight: bold;
      box-shadow: 0 0 15px rgba(255,255,255,0.6);
      transition: transform 0.3s, box-shadow 0.3s;
    }

    #start-button:hover {
      transform: scale(1.1);
      box-shadow: 0 0 25px rgba(255,255,255,0.9);
    }

    @keyframes fadeOut {
      from { opacity: 1; }
      to { opacity: 0; visibility: hidden; }
    }

    /* Game Box */
    .game-box {
      background: white;
      border-radius: 20px;
      padding: 30px;
      max-width: 600px;
      margin: 60px auto;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
      display: none;
      animation: fadeIn 0.5s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }

    button.choice-btn {
      display: block;
      margin: 15px auto;
      padding: 12px 20px;
      border: none;
      border-radius: 10px;
      background-color: #0288d1;
      color: white;
      font-size: 16px;
      cursor: pointer;
      transition: background 0.3s;
    }

    button.choice-btn:hover {
      background-color: #0277bd;
    }

    #result {
      font-size: 18px;
      margin-top: 20px;
      color: #004d40;
    }

    #icon {
      font-size: 50px;
      margin-bottom: 10px;
      display: block;
    }
  </style>
</head>
<body>
  <!-- Start Screen -->
  <div id="start-screen">
    <div style="font-size:60px;">🦺</div>
    <h1>Disaster Ready Challenge</h1>
    <p>Test your disaster readiness skills!</p>
    <button id="start-button">Start Game</button>
  </div>

  <!-- Game Box -->
  <div class="game-box" id="game-box">
    <span id="icon">🌎</span>
    <h1>Disaster Ready Challenge (AI Edition)</h1>
    <p id="scenario">Loading a unique scenario...</p>
    <div id="choices"></div>
    <p id="result"></p>
  </div>

  <script>
    const questionPool = [
      {
        type: 'earthquake', icon: '🌋', color: 'linear-gradient(135deg, #ffe082, #ffb300)',
        text: "An earthquake just struck! What’s your first move?",
        options: [
          { text: "Run outside immediately.", correct: false, feedback: "❌ It’s safer to drop, cover, and hold on indoors." },
          { text: "Take cover under a sturdy table.", correct: true, feedback: "✅ Correct! Protect yourself from falling objects." },
          { text: "Stand near glass windows to look outside.", correct: false, feedback: "❌ Dangerous! Stay away from glass and heavy items." }
        ]
      },
      {
        type: 'flood', icon: '🌊', color: 'linear-gradient(135deg, #b3e5fc, #0288d1)',
        text: "Heavy rain continues for hours and your area is flooding. What should you do?",
        options: [
          { text: "Move to higher ground immediately.", correct: true, feedback: "✅ Perfect! Flood safety 101: go higher." },
          { text: "Stay in your car on the road.", correct: false, feedback: "❌ Never stay in a car in floodwaters." },
          { text: "Walk through floodwater to your house.", correct: false, feedback: "❌ Floodwaters may hide electrical wires or debris." }
        ]
      },
      {
        type: 'fire', icon: '🔥', color: 'linear-gradient(135deg, #ff8a65, #d84315)',
        text: "A fire breaks out in the building. What’s the safest action?",
        options: [
          { text: "Use the elevator to exit quickly.", correct: false, feedback: "❌ Elevators can fail in a fire — use stairs!" },
          { text: "Cover your nose with cloth and crawl low.", correct: true, feedback: "✅ Smart! Smoke rises, so crawl under it." },
          { text: "Hide inside a room and wait.", correct: false, feedback: "❌ You must find a safe exit quickly." }
        ]
      },
      {
        type: 'heatwave', icon: '☀️', color: 'linear-gradient(135deg, #ffecb3, #ffca28)',
        text: "During a heatwave, what’s the best thing to do?",
        options: [
          { text: "Stay hydrated and indoors.", correct: true, feedback: "✅ Excellent! Keep cool and drink plenty of water." },
          { text: "Go jogging outside.", correct: false, feedback: "❌ Avoid physical exertion during high heat." },
          { text: "Wear thick clothing.", correct: false, feedback: "❌ Light, loose clothing is safer." }
        ]
      },
      {
        type: 'thunderstorm', icon: '🌩️', color: 'linear-gradient(135deg, #c5cae9, #283593)',
        text: "You’re caught in a thunderstorm while outdoors. What do you do?",
        options: [
          { text: "Stand under a tall tree.", correct: false, feedback: "❌ Lightning often strikes tall trees!" },
          { text: "Find shelter in a building or car.", correct: true, feedback: "✅ Correct! Get to shelter immediately." },
          { text: "Lie flat on the ground.", correct: false, feedback: "❌ Unsafe — crouch low if no shelter is near." }
        ]
      }
    ];

    let current = 0;
    let score = 0;
    let scenarios = [];

    function generateRandomScenarios() {
      const shuffled = questionPool.sort(() => 0.5 - Math.random());
      return shuffled.slice(0, 3);
    }

    function updateBackground(type, icon, color) {
      document.body.style.background = color;
      document.getElementById('icon').textContent = icon;
    }

    function showScenario() {
      const s = scenarios[current];
      document.getElementById('scenario').textContent = s.text;
      const choicesDiv = document.getElementById('choices');
      choicesDiv.innerHTML = '';
      updateBackground(s.type, s.icon, s.color);
      s.options.forEach(opt => {
        const btn = document.createElement('button');
        btn.textContent = opt.text;
        btn.classList.add('choice-btn');
        btn.onclick = () => handleChoice(opt);
        choicesDiv.appendChild(btn);
      });
    }

    function handleChoice(option) {
      document.getElementById('result').textContent = option.feedback;
      if (option.correct) score++;
      setTimeout(() => {
        current++;
        document.getElementById('result').textContent = '';
        if (current < scenarios.length) showScenario();
        else showResult();
      }, 1500);
    }

    function showResult() {
      document.getElementById('scenario').textContent = `Game Over! You scored ${score}/${scenarios.length}.`;
      document.getElementById('icon').textContent = '🏆';
      document.body.style.background = 'linear-gradient(135deg, #c8e6c9, #81c784)';
      document.getElementById('choices').innerHTML = '<button class="choice-btn" onclick="restartGame()">Play Again</button>';
    }

    function restartGame() {
      current = 0;
      score = 0;
      scenarios = generateRandomScenarios();
      document.getElementById('result').textContent = '';
      showScenario();
    }

    // Start Screen Logic
    document.getElementById('start-button').addEventListener('click', () => {
      const startScreen = document.getElementById('start-screen');
      startScreen.style.animation = 'fadeOut 1s ease forwards';
      setTimeout(() => {
        startScreen.style.display = 'none';
        document.getElementById('game-box').style.display = 'block';
        scenarios = generateRandomScenarios();
        showScenario();
      }, 900);
    });
  </script>
</body>
</html>
