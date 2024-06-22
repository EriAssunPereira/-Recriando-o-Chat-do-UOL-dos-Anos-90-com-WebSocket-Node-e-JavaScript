# Recriando-o-Chat-do-UOL-dos-Anos-90-com-WebSocket-Node-e-JavaScript

Recriar o chat do UOL dos anos 90 utilizando WebSocket, Node.js e JavaScript moderno é uma excelente oportunidade para explorar como tecnologias contemporâneas podem replicar experiências clássicas da web. Neste projeto, vamos focar na construção do frontend da aplicação, utilizando a biblioteca socket.io para comunicação em tempo real com o servidor Node.js que gerencia os chats. Abaixo estão os passos e exemplos de como estruturar e implementar este projeto.

### Configuração Inicial do Projeto

1. **Setup do Projeto:**
   - Configure um ambiente Node.js para desenvolvimento.
   - Instale as dependências necessárias, como `express` e `socket.io`.

2. **Estrutura do Projeto:**
   Organize o projeto para facilitar o desenvolvimento.
   ```
   /chat-uol-anos-90
   ├── /frontend
   │   ├── index.html
   │   ├── style.css
   │   ├── script.js
   ├── /backend
   │   ├── server.js
   ├── README.md
   ├── package.json
   ├── package-lock.json
   ```

### Desenvolvimento do Backend com Node.js e Socket.io

1. **Configuração do Servidor Node.js:**
   - Implemente um servidor HTTP com Express e configure o Socket.io para gerenciar conexões WebSocket.

   Exemplo de `server.js` (`backend/server.js`):
   ```javascript
   // /backend/server.js
   const express = require('express');
   const http = require('http');
   const socketIo = require('socket.io');

   const app = express();
   const server = http.createServer(app);
   const io = socketIo(server);

   app.use(express.static('frontend'));

   io.on('connection', (socket) => {
       console.log('Novo usuário conectado');

       socket.on('disconnect', () => {
           console.log('Usuário desconectado');
       });

       socket.on('chat message', (msg) => {
           console.log('Mensagem recebida: ' + msg);
           io.emit('chat message', msg);
       });
   });

   const PORT = process.env.PORT || 3000;
   server.listen(PORT, () => {
       console.log(`Servidor WebSocket escutando na porta ${PORT}`);
   });
   ```

### Desenvolvimento do Frontend com HTML, CSS e JavaScript

1. **HTML (index.html):**
   - Crie a estrutura básica da interface do chat.

   Exemplo de `index.html` (`frontend/index.html`):
   ```html
   <!-- /frontend/index.html -->
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Chat UOL dos Anos 90</title>
       <link rel="stylesheet" href="style.css">
   </head>
   <body>
       <div id="chat">
           <ul id="messages"></ul>
           <form id="form" action="">
               <input id="input" autocomplete="off">
               <button>Enviar</button>
           </form>
       </div>
       <script src="/socket.io/socket.io.js"></script>
       <script src="script.js"></script>
   </body>
   </html>
   ```

2. **CSS (style.css):**
   - Estilize a interface para refletir o estilo nostálgico dos anos 90.

   Exemplo de `style.css` (`frontend/style.css`):
   ```css
   /* /frontend/style.css */
   body {
       font-family: Arial, sans-serif;
       background-color: #f0f0f0;
       padding: 20px;
   }

   #chat {
       max-width: 600px;
       margin: 0 auto;
       background-color: #fff;
       border: 1px solid #ccc;
       border-radius: 5px;
       padding: 10px;
       box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
   }

   #messages {
       list-style-type: none;
       padding: 0;
       margin: 0;
       max-height: 300px;
       overflow-y: scroll;
   }

   #messages li {
       margin-bottom: 10px;
   }

   form {
       display: flex;
       margin-top: 10px;
   }

   form input[type="text"] {
       flex: 1;
       padding: 10px;
       font-size: 16px;
   }

   form button {
       padding: 10px 20px;
       font-size: 16px;
       cursor: pointer;
   }
   ```

3. **JavaScript (script.js):**
   - Implemente a lógica para interagir com o WebSocket e manipular a interface do chat.

   Exemplo de `script.js` (`frontend/script.js`):
   ```javascript
   // /frontend/script.js
   const socket = io();

   const form = document.getElementById('form');
   const input = document.getElementById('input');
   const messages = document.getElementById('messages');

   form.addEventListener('submit', (e) => {
       e.preventDefault();
       if (input.value) {
           socket.emit('chat message', input.value);
           input.value = '';
       }
   });

   socket.on('chat message', (msg) => {
       const item = document.createElement('li');
       item.textContent = msg;
       messages.appendChild(item);
       window.scrollTo(0, document.body.scrollHeight);
   });
   ```

### Execução e Teste

1. **Inicialização do Servidor:**
   - Inicie o servidor Node.js utilizando `node server.js`.

2. **Acesso ao Chat:**
   - Abra o navegador e acesse `http://localhost:3000`.
   - Interaja com o chat enviando mensagens e observe a comunicação em tempo real.

### Conclusão

Recriar o chat do UOL dos anos 90 utilizando WebSocket, Node.js e JavaScript moderno proporciona uma experiência prática na construção de aplicações em tempo real na web. Este projeto não apenas demonstra como integrar WebSocket com Node.js e socket.io para comunicação bidirecional, mas também ilustra como criar uma interface interativa utilizando HTML, CSS e JavaScript. Ao explorar e implementar este projeto, é possível entender melhor os conceitos fundamentais de comunicação em tempo real na web e aplicar técnicas modernas para desenvolver aplicações robustas e eficientes.
