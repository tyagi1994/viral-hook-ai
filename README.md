<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Viral Hook & Caption AI</title>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
      background: #0f172a;
      color: #f8fafc;
      margin: 0;
      padding: 20px;
      display: flex;
      justify-content: center;
    }
    .card {
      background: #1e293b;
      padding: 24px;
      border-radius: 16px;
      max-width: 480px;
      width: 100%;
      box-shadow: 0 10px 25px rgba(0,0,0,0.3);
    }
    h2 {
      margin-top: 0;
      color: #38bdf8;
      text-align: center;
    }
    label {
      font-size: 14px;
      color: #94a3b8;
      display: block;
      margin-bottom: 6px;
    }
    input, textarea, button {
      width: 100%;
      padding: 12px;
      border-radius: 8px;
      border: 1px solid #334155;
      background: #0f172a;
      color: #fff;
      box-sizing: border-box;
      font-size: 15px;
      margin-bottom: 14px;
    }
    button {
      background: #2563eb;
      color: white;
      font-weight: bold;
      border: none;
      cursor: pointer;
      transition: 0.2s;
    }
    button:active {
      background: #1d4ed8;
    }
    .output {
      background: #0f172a;
      border: 1px solid #334155;
      padding: 14px;
      border-radius: 8px;
      white-space: pre-wrap;
      min-height: 80px;
      font-size: 14px;
      line-height: 1.5;
    }
  </style>
</head>
<body>

<div class="card">
  <h2>🚀 Viral AI Generator</h2>
  
  <label>Apni Gemini API Key dalein:</label>
  <input type="password" id="apiKey" placeholder="AI Studio wali Key yahan dalein">

  <label>Video ya Reel ka Topic:</label>
  <textarea id="topic" rows="3" placeholder="Jaise: GTA gameplay, Trading Tips ya trending song reel..."></textarea>

  <button id="generateBtn" onclick="generateViralContent()">Viral Content Banayein ⚡</button>

  <label>AI Response:</label>
  <div class="output" id="resultText">Yahan aapka content aayega...</div>
</div>

<script>
async function generateViralContent() {
  const apiKey = document.getElementById('apiKey').value.trim();
  const topic = document.getElementById('topic').value.trim();
  const resultBox = document.getElementById('resultText');
  const btn = document.getElementById('generateBtn');

  if (!apiKey) {
    alert("Pehle API Key dalein!");
    return;
  }
  if (!topic) {
    alert("Koi topic likhein!");
    return;
  }

  btn.innerText = "Generating...";
  btn.disabled = true;
  resultBox.innerText = "Gemini soch raha hai... ⏳";

  const prompt = `You are a viral social media expert. For this topic: "${topic}", provide:
1. 3 Catchy Viral Hooks (Hindi/Hinglish)
2. 1 Engaging Short Caption
3. 10 Trending Hashtags.`;

  try {
    const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`;
    const response = await fetch(url, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        contents: [{ parts: [{ text: prompt }] }]
      })
    });

    const data = await response.json();
    if (data.candidates && data.candidates[0].content.parts[0].text) {
      resultBox.innerText = data.candidates[0].content.parts[0].text;
    } else {
      resultBox.innerText = "Error: " + JSON.stringify(data);
    }
  } catch (err) {
    resultBox.innerText = "API error. Check key or internet connection.";
  } finally {
    btn.innerText = "Viral Content Banayein ⚡";
    btn.disabled = false;
  }
}
</script>

</body>
</html>
