<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bot AI</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        button {
            padding: 8px 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin: 5px;
        }
        button:hover {
            background-color: #45a049;
        }
        .hosting-plans {
            display: flex;
            gap: 20px;
            margin-top: 15px;
        }
        .chat-container {
            margin-top: 20px;
            border: 1px solid #ddd;
            border-radius: 5px;
            height: 400px;
            overflow-y: auto;
        }
        .chat-log {
            padding: 15px;
            height: calc(100% - 60px);
        }
        .chat-input {
            display: flex;
            padding: 10px;
            border-top: 1px solid #ddd;
        }
        #user-input {
            flex-grow: 1;
            padding: 8px;
            border-radius: 4px;
            border: 1px solid #ddd;
        }
        .subtitle {
            color: #666;
            margin-top: -10px;
        }
        #output, #ajaxResult {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: #f9f9f9;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>AI Chat Bot</h1>
        <p class="subtitle">Intelligent conversational assistant powered by AI</p>
        
        <!-- Contoh Interaksi Dasar -->
        <h2>1. Interaksi Dasar</h2>
        <button id="greetBtn">Sapa Pengguna</button>
        <button id="calculateBtn">Hitung Faktorial</button>
        <div id="output"></div>

        <!-- Chat Interface -->
        <div class="chat-container">
            <div id="chat-log" class="chat-log"></div>
            <div class="chat-input">
                <input type="text" id="user-input" placeholder="Type your message here...">
                <button id="send-btn">Send</button>
            </div>
        </div>

        <!-- Contoh Event Handling -->
        <h2>3. Penanganan Event</h2>
        <button id="eventBtn">Klik Saya</button>
        <p id="eventStatus">Status: Belum diklik</p>

        <!-- Contoh AJAX/Fetch API -->
        <h2>4. Fetch API (AJAX)</h2>
        <button id="fetchBtn">Ambil Data dari API</button>
        <div id="ajaxResult">Data akan muncul di sini...</div>

        <!-- Contoh Web Storage -->
        <h2>5. Penyimpanan Lokal</h2>
        <input type="text" id="storageInput" placeholder="Masukkan teks untuk disimpan">
        <button id="saveBtn">Simpan ke LocalStorage</button>
        <button id="loadBtn">Muat dari LocalStorage</button>
        <p id="storageOutput"></p>
    </div>

    <script>
        // ===== 1. AI Bot Functionality =====
        const chatLog = document.getElementById('chat-log');
        const userInput = document.getElementById('user-input');
        
        // Simple responses
        const botResponses = {
            "hello": "Hello there! How can I assist you today?",
            "how are you": "I'm just a bot, but thanks for asking!",
            "goodbye": "Goodbye! Have a nice day!",
            "help": "I can answer simple questions. Try asking me anything."
        };

        function addMessage(message, isUser = false) {
            const msgDiv = document.createElement('div');
            msgDiv.classList.add(isUser ? 'user-message' : 'bot-message');
            msgDiv.textContent = message;
            chatLog.appendChild(msgDiv);
            chatLog.scrollTop = chatLog.scrollHeight;
        }

        function calculateFactorial() {
            const number = 5; // Ganti dengan input jika diperlukan
            let result = 1;
            for(let i = 1; i <= number; i++) {
                result *= i;
            }
            document.getElementById('output').textContent = `Faktorial dari ${number} adalah ${result}`;
        }

        // Event Listeners untuk bagian 1
        document.getElementById('greetBtn').addEventListener('click', greetUser);
        document.getElementById('calculateBtn').addEventListener('click', calculateFactorial);

        // ===== 2. Manipulasi DOM =====
        function addElement() {
            const newElement = document.createElement('p');
            newElement.textContent = 'Elemen baru ditambahkan!';
            document.getElementById('domDemo').appendChild(newElement);
        }

        function changeStyle() {
            const demoArea = document.getElementById('domDemo');
            demoArea.style.backgroundColor = '#f0f8ff';
            demoArea.style.padding = '15px';
            demoArea.style.border = '1px dashed #4682b4';
        }

        document.getElementById('addElementBtn').addEventListener('click', addElement);
        document.getElementById('changeStyleBtn').addEventListener('click', changeStyle);

        // ===== 3. Penanganan Event =====
        document.getElementById('eventBtn').addEventListener('click', function() {
            clickCount++;
            const statusElement = document.getElementById('eventStatus');
            statusElement.textContent = `Status: Diklik ${clickCount} kali`;
            statusElement.style.color = clickCount % 2 === 0 ? 'green' : 'red';
        });

        // ===== 4. Fetch API (AJAX) =====
        document.getElementById('fetchBtn').addEventListener('click', async function() {
            try {
                const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
                if (!response.ok) {
                    throw new Error('Gagal mengambil data');
                }
                const data = await response.json();
                document.getElementById('ajaxResult').innerHTML = `
                    <h3>${data.title}</h3>
                    <p>${data.body}</p>
                `;
            } catch (error) {
                document.getElementById('ajaxResult').textContent = 'Error: ' + error.message;
            }
        });

        // ===== 5. Web Storage =====
        document.getElementById('saveBtn').addEventListener('click', function() {
            const inputText = document.getElementById('storageInput').value;
            if (inputText) {
                localStorage.setItem('userText', inputText);
                alert('Teks berhasil disimpan!');
            }
        });

        document.getElementById('loadBtn').addEventListener('click', function() {
            const savedText = localStorage.getItem('userText');
            if (savedText) {
                document.getElementById('storageOutput').textContent = `Teks tersimpan: ${savedText}`;
            } else {
                document.getElementById('storageOutput').textContent = 'Tidak ada teks yang tersimpan';
            }
        });

        // ===== 6. Fitur Modern (ES6+) =====
        // Contoh: Arrow Function, Template Literals, dll...
    </script>
</body>
</html>
