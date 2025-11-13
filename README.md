🧩 Real-Time Chat App — WebSockets & Socket.IO

Node.js • Express • Socket.IO • Mustache • Geolocation API

Este projeto foi desenvolvido durante meus estudos sobre comunicação em tempo real usando WebSockets.
O objetivo é demonstrar:

🔌 Conexão bidirecional Server ↔ Client

💬 Sistema de chat em tempo real

📍 Compartilhamento de localização (Geolocation API)

🧼 Filtro de palavrões (bad-words)

🧩 Mustache template rendering (lado do cliente)

🕒 Timestamps formatados com Moment.js

```
⭐ Demonstração do Fluxo (Diagrama)
           ┌────────────────────────────────────────┐
           │               CLIENTE                   │
           │   (browser + chat.js + Mustache)        │
           └────────────────────────────────────────┘
                       ▲                 ▲
                       │   Mensagens     │
                       │   "message"     │
                       │   "location"    │
                       │                 │
  submit msg / geo     │                 │   broadcast
-----------------------│-----------------│-------------------------
                       │                 │
                       │ Real-time via WebSockets
                       ▼                 ▼
           ┌────────────────────────────────────────┐
           │             SERVIDOR NODE              │
           │    Express + Socket.IO + utils/        │
           │                                        │
           │  • io.emit()                           │
           │  • socket.broadcast.emit()             │
           │  • socket.emit()                       │
           │  • handle sendMessage, sendLocation    │
           └────────────────────────────────────────┘
```

```
📁 Estrutura do Projeto
realtime-chat-websockets/
│
├── public/
│   ├── js/
│   │   └── chat.js
│   ├── index.html
│   └── css/...
│
├── src/
│   └── utils/
│       └── messages.js
│
├── index.js
└── LICENSE

🚀 Como Executar
1. Instalar dependências
npm install

2. Rodar a aplicação
node index.js
```

A aplicação abrirá na porta:

http://localhost:3000

💬 Eventos WebSocket implementados
📌 1. message (server → client)

Envia mensagens normais do chat.

Emitido por:

socket.emit('message', ...) — para usuário específico

io.emit('message', ...) — para todos

socket.broadcast.emit('message', ...) — para todos exceto origem

📌 2. sendMessage (client → server)

O usuário envia uma mensagem.

O servidor:

verifica palavrões usando bad-words

responde via callback se estiver ok

retransmite via io.emit('message')

📌 3. sendLocation (client → server)

O client envia coordenadas via geolocation.
O servidor envia URL de mapa:

https://google.com/maps?q=latitude,longitude


Transmitido como locationMessage

📌 4. disconnect (server)

Quando o usuário sai, o servidor notifica todos:

A user has left

🧪 Tecnologias Utilizadas
Tecnologia	Uso
Node.js	Ambiente do servidor
Express	Servir arquivos estáticos
Socket.IO	Canal WebSocket bidirecional
Mustache.js	Templates HTML no cliente
Moment.js	Formatação de timestamps
Bad-Words	Filtro de palavrões
Geolocation API	Envio da localização
🧠 Fluxo Detalhado

Cliente se conecta via WebSocket

Servidor envia mensagem de "Welcome!"

Broadcast avisa aos outros usuários

Cliente envia mensagens → servidor → todos recebem

Cliente envia coordenadas → servidor → todos recebem link do mapa

Ao desconectar, servidor emite “A user has left”

📄 MIT License



MIT License

Copyright (c) 2024-2025 VMarconatto

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
