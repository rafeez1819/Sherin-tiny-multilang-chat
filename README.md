tiny-multilang-chat/
├── src/
|
│   ├── chat.js       # core logic
|   |
│   ├── lang.js      # language detection
|   |
│   └── reply.js     # response engine
|
├── index.html
|
├── style.css
|
├── README.md
|
└── .gitignore

# Sherin-tiny-multilang-chat


<p align="center">
  <a href="https://raw.githubusercontent.com/rafeez1819/Sherin-tiny-multilang-chat/main/sherin.html" download>
    <img src="https://img.shields.io/badge/⬇️%20Download-Sherin.html-blue?style=for-the-badge">
  </a>
</p>





🌍 Language Auto-Detection (Ultra-Light)
Strategy

Uses Unicode ranges + keyword hints

No ML, no external APIs

~300 bytes logic

Example (chat.js)
function detectLang(text) {
  if (/[\u0600-\u06FF]/.test(text)) return "ar"; // Arabic
  if (/[\u0400-\u04FF]/.test(text)) return "ru"; // Russian
  if (/[\u4E00-\u9FFF]/.test(text)) return "zh"; // Chinese
  if (/[\u0D00-\u0D7F]/.test(text)) return "ml"; // Malayalam
  return "en";
}

function reply(text) {
  const lang = detectLang(text);
  const replies = {
    en: "Hello 👋 How can I help?",
    ar: "مرحباً 👋 كيف أساعدك؟",
    ru: "Привет 👋 Чем могу помочь?",
    zh: "你好 👋 我能帮你什么？",
    ml: "ഹലോ 👋 എങ്ങനെ സഹായിക്കാം?"
  };
  return replies[lang] || replies.en;
}


✅ No dependencies
✅ Fast
✅ Offline

🚀 12 KB Optimization Tips

✅ Vanilla JS only

❌ No React / Vue

❌ No language libraries

✅ Inline CSS

✅ Minify JS (terser)

✅ Gzip enabled

Target sizes:

index.html   ~3 KB
chat.js      ~2 KB
server.js    ~4 KB
TOTAL        ~9–11 KB

🤖 Telegram Bot Ready
Telegram Flow
User → Telegram → Webhook → server.js → reply()

Minimal Telegram Handler
app.post('/telegram', (req, res) => {
  const msg = req.body.message.text;
  const chatId = req.body.message.chat.id;
  sendMessage(chatId, reply(msg));
  res.sendStatus(200);
});


Works with:

node-telegram-bot-api

or raw HTTPS

🌐 API Usage
POST /chat
{
  "message": "مرحبا"
}

Response
{
  "reply": "مرحباً 👋 كيف أساعدك؟",
  "lang": "ar"
}

🐳 Docker Ready
Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install --omit=dev
CMD ["node", "server.js"]

Run
docker build -t tiny-chat .
docker run -p 3000:3000 tiny-chat

🔐 Security Notes

Validate input length

Rate-limit API

Use Telegram secret token

Disable public logs in production

📜 License

MIT — use it freely, modify it, ship it 🚀

🧠 Next Up (Optional)

🔊 Text-to-Speech

🧠 AI / LLM backend

🌐 WebSocket streaming

💾 Memory / context

📱 Mobile UI
