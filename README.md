<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Love From Eyu</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(to bottom right, #1e3c72, #2a5298); /* beautiful blue gradient */
      color: white;
      font-family: 'Arial', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      text-align: center;
      overflow: hidden;
    }
    #loveIcon {
      font-size: 80px;
      cursor: pointer;
      animation: pulse 1s infinite;
      color: #ff69b4;
      text-shadow: 0 0 20px rgba(255, 255, 255, 0.6);
    }
    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.2); }
      100% { transform: scale(1); }
    }
    .hidden { display: none; }
    .heart {
      font-size: 50px;
      margin: 10px;
      cursor: pointer;
      color: #ff69b4;
      transition: transform 0.2s;
    }
    .heart:hover {
      transform: scale(1.3);
    }
    img {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      margin-bottom: 20px;
      border: 3px solid white;
      box-shadow: 0 0 15px rgba(255,255,255,0.5);
    }
    button {
      background-color: #1e90ff;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      margin-top: 10px;
      font-size: 16px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.2);
    }
    input {
      padding: 8px;
      border-radius: 5px;
      border: none;
      margin-bottom: 10px;
      font-size: 16px;
    }
    #story span {
      display: block;
      font-size: 24px;
      margin-top: 10px;
      font-weight: bold;
    }
    .floating-heart {
      position: absolute;
      font-size: 24px;
      color: pink;
      animation: floatUp 4s linear infinite;
      user-select: none;
    }
    @keyframes floatUp {
      0% { transform: translateY(100vh) scale(1); opacity: 1; }
      100% { transform: translateY(-20vh) scale(1.5); opacity: 0; }
    }
  </style>
</head>
<body>
  <audio id="bgmusic" loop>
    <source src="eyu.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <img src="eyu.jpg" alt="Eyu">
  <p id="tapStart" style="color:pink; font-size: 20px;">Tap the love icon to begin 💖</p>
  <div id="loveIcon">❤️</div>
  <div id="namePrompt" class="hidden">
    <p style="color:pink">What's your name?</p>
    <input type="text" id="username"><br>
    <button onclick="continueToGreeting()">Continue 💌</button>
  </div>
  <div id="greeting" class="hidden"></div>
  <div id="hearts" class="hidden">
    <p id="tapText" style="color:pink">Tap the 4 love icons 💕</p>
    <div id="heartContainer">
      <span class="heart" onclick="clickHeart(this)">❤️</span>
      <span class="heart" onclick="clickHeart(this)">❤️</span>
      <span class="heart" onclick="clickHeart(this)">❤️</span>
      <span class="heart" onclick="clickHeart(this)">❤️</span>
    </div>
  </div>
  <div id="story" class="hidden"></div>

  <script>
    const loveIcon = document.getElementById('loveIcon');
    const tapStart = document.getElementById('tapStart');
    const namePrompt = document.getElementById('namePrompt');
    const greeting = document.getElementById('greeting');
    const hearts = document.getElementById('hearts');
    const story = document.getElementById('story');
    const bgmusic = document.getElementById('bgmusic');
    let username = '';
    let heartCount = 0;

    loveIcon.onclick = () => {
      bgmusic.play();
      loveIcon.classList.add('hidden');
      tapStart.classList.add('hidden');
      namePrompt.classList.remove('hidden');
    };

    function continueToGreeting() {
      username = document.getElementById('username').value;
      namePrompt.classList.add('hidden');
      greeting.innerHTML = `<span style='color:skyblue'>Hi, I am Eyu 👋</span><br><span style='color:pink'>Hi ${username} 💖</span>`;
      greeting.classList.remove('hidden');
      setTimeout(() => {
        greeting.classList.add('hidden');
        hearts.classList.remove('hidden');
      }, 4000);
    }

    function clickHeart(element) {
      element.remove();
      heartCount++;
      if (heartCount === 1) {
        document.getElementById('tapText').textContent = '3 more to go... 💗';
      } else if (heartCount === 2) {
        document.getElementById('tapText').textContent = '2 more left... 💓';
      } else if (heartCount === 3) {
        document.getElementById('tapText').textContent = 'Last one! 💞';
      } else if (heartCount === 4) {
        hearts.classList.add('hidden');
        startStory();
      }
    }

    function startStory() {
      story.classList.remove('hidden');
      story.innerHTML = '<span style="color:violet">Do you know there are 3 ways to be beautiful? 💫</span>';
      setTimeout(() => { story.innerHTML = '<span style="color:lightblue">3...</span>'; }, 4000);
      setTimeout(() => { story.innerHTML = '<span style="color:lightgreen">2...</span>'; }, 7000);
      setTimeout(() => { story.innerHTML = '<span style="color:orange">1...</span>'; }, 10000);
      setTimeout(() => { story.innerHTML = '<span style="color:yellow">Why are you waiting? 😄</span>'; }, 13000);
      setTimeout(() => { story.innerHTML = '<span style="color:deeppink">You are already beautiful 😍</span>'; }, 16000);
      setTimeout(() => { story.innerHTML = '<span style="color:hotpink">Very beautiful in fact… I love you so much ❤️❤️❤️</span>'; }, 19000);
    }

    function createFloatingHeart() {
      const heart = document.createElement('div');
      heart.className = 'floating-heart';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.top = '100vh';
      heart.textContent = '💖';
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 4000);
    }
    setInterval(createFloatingHeart, 500);
  </script>
</body>
</html>

