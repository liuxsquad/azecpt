<!DOCTYPE html>
<html lang="az">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Azecht</title>
    <style>
        * { margin:0; padding:0; box-sizing:border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: #fff;
            height: 100vh;
            display: flex;
            flex-direction: column;
        }
        h1 {
            text-align: center;
            padding: 15px 0;
            font-size: 1.8rem;
            background: rgba(0, 0, 0, 0.3);
            margin-bottom: 10px;
        }
        #chat {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
            background: rgba(0,0,0,0.2);
        }
        .message {
            margin: 10px 0;
            padding: 12px 16px;
            border-radius: 20px;
            max-width: 80%;
            word-wrap: break-word;
            font-size: 1rem;
            line-height: 1.4;
        }
        .user {
            background: #00d4ff;
            color: #000;
            margin-left: auto;
        }
        .bot {
            background: rgba(255,255,255,0.15);
            margin-right: auto;
        }
        .input-area {
            padding: 12px;
            background: rgba(0,0,0,0.4);
            display: flex;
            gap: 8px;
        }
        #input {
            flex: 1;
            padding: 12px 16px;
            border: none;
            border-radius: 30px;
            background: rgba(255,255,255,0.15);
            color: white;
            font-size: 1rem;
        }
        #input::placeholder { color: rgba(255,255,255,0.6); }
        button {
            padding: 12px 24px;
            background: #00d4ff;
            color: #000;
            border: none;
            border-radius: 30px;
            font-weight: bold;
            cursor: pointer;
        }
        button:active { background: #00b7e0; }
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
        const apiKey = "BURAYA_GROQ_API_KEY_QOY"; // ← buraya öz Groq key-ni yapışdır!!!
        const model = "llama-3.1-70b-versatile";

        async function gonder() {
            const input = document.getElementById("input");
            const mesaj = input.value.trim();
            if (!mesaj) return;

            elaveEt(mesaj, "user");
            input.value = "";

            try {
                const res = await fetch("https://api.groq.com/openai/v1/chat/completions", {
                    method: "POST",
                    headers: {
                        "Authorization": `Bearer ${apiKey}`,
                        "Content-Type": "application/json"
                    },
                    body: JSON.stringify({
                        model,
                        messages: [
                            {
                                role: "system",
                                content: "Sən Azecht adlı AI botsan. Hər zaman YALNIZ AZƏRBAYCAN DİLİNDƏ cavab ver. Heç vaxt başqa dilə keçmə. Cavabların dostcasına, gülməli və köməkçi olsun. Salamlaşanda 'Salam qardaş! Nə xəbər? 😏' kimi başla."
                            },
                            { role: "user", content: mesaj }
                        ],
                        temperature: 0.85,
                        max_tokens: 400
                    })
                });

                if (!res.ok) throw new Error();
                const data = await res.json();
                elaveEt(data.choices[0].message.content.trim(), "bot");
            } catch {
                elaveEt("Bağışla qardaş, xəta çıxdı 😅 Yenə cəhd et", "bot");
            }
        }

        function elaveEt(m, tip) {
            const chat = document.getElementById("chat");
            const div = document.createElement("div");
            div.className = `message ${tip}`;
            div.textContent = m;
            chat.appendChild(div);
            chat.scrollTop = chat.scrollHeight;
        }
    </script>
</body>
</html>
