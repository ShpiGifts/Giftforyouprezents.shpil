# Giftforyouprezents.shpil
Gift for you prezents shpil
git init
git remote add origin https://github.com/ТВОЄ_ІМʼЯ/telegram-easy-gift.git
git add .
git commit -m "First commit"
git branch -M main
git push -u origin main
<!DOCTYPE html>
<html>
<head>
  <title>Easy Gift</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
</head>
<body>
  <h1>🎁 Відкрий свій кейс</h1>
  <button onclick="buyCase()">Купити кейс за 1 зірку</button>
  <p id="result"></p>
</body>
<script>
  const tg = window.Telegram.WebApp;
  tg.expand();

  async function buyCase() {
    const res = await fetch('/buy', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ user_id: tg.initDataUnsafe.user.id })
    });
    const data = await res.json();
    document.getElementById("result").innerText = Випав подарунок: ${data.gift};
  }
</script>
</html>
