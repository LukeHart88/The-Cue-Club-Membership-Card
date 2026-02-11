<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cue Club Membership Card</title>
  <style>
    body { font-family: Arial, sans-serif; display: flex; flex-direction: column; align-items: center; background: #f0f0f0; margin: 0; padding: 20px; min-height: 100vh; }
    #card { width: 100%; max-width: 350px; height: auto; position: relative; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.2); }
    #overlay { position: absolute; top: 60%; left: 10%; color: black; font-weight: bold; font-size: 18px; text-align: center; background: rgba(255,255,255,0.9); padding: 5px; border-radius: 5px; }
    input { margin: 10px; padding: 10px; width: 80%; max-width: 300px; border: 1px solid #ccc; border-radius: 5px; }
    button { background: #4CAF50; color: white; padding: 15px; border: none; border-radius: 5px; font-size: 16px; cursor: pointer; width: 90%; }
    #ready { display: none; text-align: center; }
    @media (max-width: 400px) { #overlay { font-size: 16px; top: 55%; } }
  </style>
</head>
<body>
  <h1>Cue Club Membership</h1>
  <img id="card" src="card.jpg" alt="Membership Card" onerror="this.src='https://via.placeholder.com/350x220?text=Cue+Club+Card'">
  <div id="overlay" style="display:none;">
    <div id="name"></div>
    <div id="number"></div>
  </div>
  <input type="text" id="memberName" placeholder="Enter name (e.g. Luke Hart)">
  <input type="text" id="memberNum" placeholder="Membership number (e.g. 147)">
  <button onclick="generateCard()">Generate Card</button>
  <div id="ready">
    <h2>Ready!</h2>
    <p>Enable NFC, hold phone to door reader. Works on Android HCE. Test with NFC Tools first.</p>
    <button onclick="simulateNFC()">Tap Door (Sim)</button>
  </div>
  <script>
    function generateCard() {
      const name = document.getElementById('memberName').value || 'Luke Hart';
      const num = document.getElementById('memberNum').value || '147';
      document.getElementById('name').textContent = name;
      document.getElementById('number').textContent = num;
      document.getElementById('overlay').style.display = 'block';
      if (name && num) document.getElementById('ready').style.display = 'block';
    }
    function simulateNFC() {
      alert('NFC Tap Simulated! Door would open if membership valid.');
    }
    // Auto-save inputs
    document.getElementById('memberName').addEventListener('input', () => localStorage.setItem('name', document.getElementById('memberName').value));
    document.getElementById('memberNum').addEventListener('input', () => localStorage.setItem('num', document.getElementById('memberNum').value));
    // Load saved
    window.onload = () => {
      document.getElementById('memberName').value = localStorage.getItem('name') || '';
      document.getElementById('memberNum').value = localStorage.getItem('num') || '';
      generateCard();
    };
  </script>
</body>
</html>
