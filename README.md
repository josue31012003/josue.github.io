<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Chatbot de Seguridad</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f6f8;
        }
        #chat {
            width: 400px;
            margin: 50px auto;
            background: white;
            padding: 15px;
            border-radius: 8px;
        }
        #messages {
            height: 300px;
            overflow-y: auto;
            border: 1px solid #ddd;
            padding: 10px;
        }
        input {
            width: 100%;
            padding: 8px;
        }
        button {
            width: 100%;
            margin-top: 5px;
            padding: 8px;
        }
    </style>
</head>
<body>

<div id="chat">
    <h3>🦺 Chatbot de Seguridad</h3>
    <div id="messages"></div>
    <input id="input" placeholder="Escribe tu consulta..." />
    <button onclick="sendMessage()">Enviar</button>
</div>

<script>
async function sendMessage() {
    const input = document.getElementById("input");
    const messages = document.getElementById("messages");

    const userMessage = input.value;
    messages.innerHTML += `<p><b>Tú:</b> ${userMessage}</p>`;
    input.value = "";

    const response = await fetch("http://127.0.0.1:8000/chat", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ message: userMessage })
    });

    const data = await response.json();
    messages.innerHTML += `<p><b>Bot:</b> ${data.response}</p>`;
    messages.scrollTop = messages.scrollHeight;
}
</script>

</body>
</html>
