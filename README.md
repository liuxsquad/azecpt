<!DOCTYPE html>
<html lang="az">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Azecht – Sənin AI Dostun</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: #fff;
            margin: 0;
            padding: 20px;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        h1 {
            margin: 20px 0;
            font-size: 2.5em;
            text-shadow: 0 0 10px #00d4ff;
        }
        #chat {
            width: 100%;
            max-width: 700px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 15px;
            height: 60vh;
            overflow-y: auto;
            margin-bottom: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .message {
            margin: 12px 0;
            padding: 12px 18px;
            border-radius: 18px;
            max-width: 80%;
            word-wrap: break-word;
        }
        .user {
            background: #00d4ff;
            align-self: flex-end;
            margin-left: auto;
            color: #000;
        }
        .bot {
            background: rgba(255, 255, 255, 0.2);
            align-self: flex-start;
        }
        .input-area {
            width: 100%;
            max-width: 700px;
            display: flex;
            gap: 10px;
        }
        #input {
            flex: 1;
            padding: 14px;
            border: none;
            border-radius: 30px;
            font-size: 1.1em;
            background: rgba(255, 255, 255, 0.15);
            color: white;
            outline: none;
        }
        #input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }
        button {
            padding: 14px 28px;
            background: #00d4ff;
            color: black;
            border: none;
            border-radius: 30px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }
        button:hover {
            background: #00b7e0;
            transform: scale(1.05);
        }
    </style>
</head>
<body>
    <h1>Azecht</h1>
    <div id="chat"></div>

    <div class="input-area">
        <input id="input" placeholder="Mesaj yaz..." autocomplete="off">
        <button onclick="gonder()">Göndər</button>
    </div>

    <script>
        const apiKey = "BURAYA_GROQ_API_KEY_QOY"; // ← Groq-dan aldığın key-i bura yapışdır
        const model = "llama-3.1-70b-versatile";

        async function gonder() {
            const input = document.getElementById("input");
            const mesaj = input.value.trim();
            if (!mesaj) return;

            elaveEt(mesaj, "user");
            input.value = "";

            try {
                const response = await fetch("https://api.groq.com/openai/v1/chat/completions", {
                    method: "POST",
                    headers: {
                        "Authorization": `Bearer ${apiKey}`,
                        "Content-Type": "application/json"
                    },
                    body: JSON.stringify({
                        model: model,
                        messages: [
                            {
                                role: "system",
                                content: "Sən Azecht adlı AI botsan. Hər zaman YALNIZ AZƏRBAYCAN DİLİNDƏ cavab ver. Heç vaxt başqa dilə keçmə. Cavabların dostcasına, gülməli və köməkçi olsun. Salamlaşanda 'Salam qardaş! Nə xəbər? 😏' kimi başla."
                            },
                            { role: "user", content: mesaj }
                        ],
                        temperature: 0.85,
                        max_tokens: 500
                    })
                });

                if (!response.ok) throw new Error("API xətası");
                const data = await response.json();
                const cavab = data.choices[0].message.content.trim();
                elaveEt(cavab, "bot");
            } catch (err) {
                elaveEt("Bağışla qardaş, xəta çıxdı 😅 Yenə cəhd et", "bot");
            }
        }

        function elaveEt(mesaj, tip) {
            const chat = document.getElementById("chat");
            const div = document.createElement("div");
            div.className = `message ${tip}`;
            div.textContent = mesaj;
            chat.appendChild(div);
            chat.scrollTop = chat.scrollHeight;
        }
    </script>
</body>
</html>
