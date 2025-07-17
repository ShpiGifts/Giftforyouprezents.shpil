# Giftforyouprezents.shpil
<!DOCTYPE html>
<html>
<head>
  <title>Easy Gift</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
</head>
<body>
  <h1>🎁 Открой свой кейс</h1>
  <button onclick="buyCase()">Купити кейс за 1 звезду</button>
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
const express = require('express');
const bodyParser = require('body-parser');
const axios = require('axios');
const app = express();
app.use(bodyParser.json());

const gifts = [
  { name: "Парфум", chance: 0.1 },
  { name: "Плюшевий ведмедик", chance: 0.3 },
  { name: "Казковий змій", chance: 0.2 },
  { name: "Капсула-сюрприз", chance: 0.4 }
];

function pickGift() {
  const rand = Math.random();
  let acc = 0;
  for (const gift of gifts) {
    acc += gift.chance;
    if (rand <= acc) return gift.name;
  }
  return gifts[gifts.length - 1].name;
}

app.post('/buy', async (req, res) => {
  const userId = req.body.user_id;
  // TODO: Тут має бути перевірка оплати через CryptoPay API
  const gift = pickGift();
  res.json({ gift });
});

app.listen(3000, () => console.log('Server running on http://localhost:3000'));
