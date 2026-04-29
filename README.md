# Project_P
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Project P - Real-time Chat</title>
    <!-- Emoji Picker Library -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/emoji-mart@5.5.2/css/emoji-mart.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: #0B141A;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }

        ::-webkit-scrollbar-track {
            background: #1E2A32;
        }

        ::-webkit-scrollbar-thumb {
            background: #3E4A52;
            border-radius: 3px;
        }

        .chat-container {
            width: 100%;
            max-width: 500px;
            height: 95vh;
            background: #111B21;
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            overflow: hidden;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            position: relative;
        }

        /* Header */
        .header {
            background: #202C33;
            padding: 16px 20px;
            color: white;
            display: flex;
            align-items: center;
            gap: 12px;
            border-bottom: 1px solid #2A3942;
        }

        .avatar {
            width: 40px;
            height: 40px;
            background: #25D366;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 18px;
        }

        .header-info {
            flex: 1;
        }

        .header-info h2 {
            font-size: 16px;
            margin-bottom: 2px;
        }

        .online-status {
            font-size: 12px;
            color: #8696A0;
        }

        .online-status.online {
            color: #25D366;
        }

        .header-actions {
            display: flex;
            gap: 16px;
        }

        .icon-btn {
            background: none;
            border: none;
            color: white;
            font-size: 20px;
            cursor: pointer;
            padding: 4px;
            transition: opacity 0.2s;
        }

        .icon-btn:hover {
            opacity: 0.7;
        }

        /* Login Screen */
        .login-screen {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 20px;
            padding: 20px;
            background: linear-gradient(135deg, #111B21 0%, #1a2a33 100%);
        }

        .login-screen h2 {
            color: #E9EDEF;
            font-size: 24px;
        }

        .login-card {
            background: #202C33;
            padding: 30px;
            border-radius: 16px;
            width: 100%;
            max-width: 320px;
        }

        .login-input {
            width: 100%;
            padding: 14px;
            font-size: 16px;
            border: 2px solid #2A3942;
            border-radius: 12px;
            background: #2A3942;
            color: white;
            margin-bottom: 12px;
        }

        .login-input:focus {
            outline: none;
            border-color: #25D366;
        }

        .login-btn {
            width: 100%;
            padding: 14px;
            font-size: 16px;
            background: #25D366;
            color: white;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s;
        }

        .login-btn:hover {
            background: #1da15a;
            transform: translateY(-2px);
        }

        /* Messages Area */
        .messages-area {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 8px;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><circle cx="50" cy="50" r="1" fill="%232A3942" opacity="0.3"/></svg>');
        }

        .message {
            max-width: 75%;
            padding: 8px 12px;
            border-radius: 12px;
            position: relative;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .message.sent {
            background: #005C4B;
            color: white;
            align-self: flex-end;
            border-bottom-right-radius: 4px;
        }

        .message.received {
            background: #202C33;
            color: #E9EDEF;
            align-self: flex-start;
            border-bottom-left-radius: 4px;
        }

        .message-user {
            font-size: 12px;
            font-weight: bold;
            color: #25D366;
            margin-bottom: 4px;
        }

        .message-text {
            font-size: 14px;
            word-wrap: break-word;
        }

        .message-image {
            max-width: 100%;
            border-radius: 8px;
            margin-top: 4px;
            cursor: pointer;
        }

        .message-time {
            font-size: 10px;
            color: rgba(255,255,255,0.6);
            text-align: right;
            margin-top: 4px;
        }

        /* Typing Indicator */
        .typing-indicator {
            padding: 8px 20px;
            background: #202C33;
            color: #8696A0;
            font-size: 12px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .typing-dots {
            display: flex;
            gap: 3px;
        }

        .typing-dots span {
            width: 4px;
            height: 4px;
            background: #8696A0;
            border-radius: 50%;
            animation: typing 1.4s infinite;
        }

        .typing-dots span:nth-child(2) {
            animation-delay: 0.2s;
        }

        .typing-dots span:nth-child(3) {
            animation-delay: 0.4s;
        }

        @keyframes typing {
            0%, 60%, 100% {
                transform: translateY(0);
            }
            30% {
                transform: translateY(-6px);
            }
        }

        /* Input Area */
        .input-area {
            padding: 12px 16px;
            background: #202C33;
            display: flex;
            gap: 10px;
            align-items: center;
            border-top: 1px solid #2A3942;
        }

        .attach-btn {
            background: none;
            border: none;
            color: #8696A0;
            font-size: 24px;
            cursor: pointer;
            padding: 8px;
            transition: color 0.2s;
        }

        .attach-btn:hover {
            color: #25D366;
        }

        .emoji-btn {
            background: none;
            border: none;
            color: #8696A0;
            font-size: 24px;
            cursor: pointer;
            padding: 8px;
            transition: color 0.2s;
        }

        .emoji-btn:hover {
            color: #FFD93D;
        }

        .message-input {
            flex: 1;
            padding: 10px 16px;
            border: none;
            border-radius: 24px;
            background: #2A3942;
            color: white;
            font-size: 14px;
            resize: none;
            font-family: inherit;
            max-height: 100px;
        }

        .message-input:focus {
            outline: none;
        }

        .send-btn {
            padding: 10px 20px;
            background: #25D366;
            color: white;
            border: none;
            border-radius: 24px;
            cursor: pointer;
            font-weight: bold;
            transition: transform 0.2s;
        }

        .send-btn:hover {
            transform: scale(1.05);
        }

        /* Emoji Picker Modal */
        .emoji-picker-modal {
            position: absolute;
            bottom: 80px;
            right: 16px;
            z-index: 1000;
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.3);
            display: none;
        }

        .emoji-picker-modal.active {
            display: block;
        }

        /* Image Preview Modal */
        .image-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.9);
            z-index: 2000;
            display: none;
            justify-content: center;
            align-items: center;
            cursor: pointer;
        }

        .image-modal.active {
            display: flex;
        }

        .image-modal img {
            max-width: 90%;
            max-height: 90%;
            border-radius: 8px;
        }

        /* File Input Hidden */
        #imageUpload {
            display: none;
        }

        /* Responsive */
        @media (max-width: 600px) {
            .chat-container {
                height: 100vh;
                max-width: 100%;
                border-radius: 0;
            }
            
            .message {
                max-width: 85%;
            }
        }
    </style>
</head>
<body>
    <div class="chat-container">
        <div class="header" id="header" style="display: none;">
            <div class="avatar" id="userAvatar">👤</div>
            <div class="header-info">
                <h2>WhatsApp Clone</h2>
                <div class="online-status" id="onlineStatus">Connecting...</div>
            </div>
            <div class="header-actions">
                <button class="icon-btn" onclick="logout()" title="Logout">🚪</button>
            </div>
        </div>
        
        <!-- Login Screen -->
        <div id="loginSection" class="login-screen">
            <h2>💬 Project P</h2>
            <div class="login-card">
                <input type="text" id="usernameInput" class="login-input" placeholder="Enter your name" maxlength="25" autocomplete="off">
                <button onclick="login()" class="login-btn">Start Chatting →</button>
                <div style="color:#8696A0; font-size:12px; margin-top:16px; text-align:center;">
                    ✨ Real-time • Images • Emojis • Typing indicators
                </div>
            </div>
        </div>
        
        <!-- Chat Interface -->
        <div id="chatSection" style="display: none; flex-direction: column; flex: 1;">
            <div id="messagesArea" class="messages-area"></div>
            <div id="typingIndicator" class="typing-indicator" style="display: none;">
                <span>Someone is typing</span>
                <div class="typing-dots">
                    <span>●</span><span>●</span><span>●</span>
                </div>
            </div>
            <div class="input-area">
                <input type="file" id="imageUpload" accept="image/*">
                <button class="attach-btn" onclick="document.getElementById('imageUpload').click()">📎</button>
                <button class="emoji-btn" onclick="toggleEmojiPicker()">😊</button>
                <textarea id="messageInput" class="message-input" placeholder="Type a message..." rows="1" onkeypress="handleKeyPress(event)"></textarea>
                <button class="send-btn" onclick="sendMessage()">Send</button>
            </div>
        </div>
    </div>
    
    <div id="emojiPickerModal" class="emoji-picker-modal"></div>
    <div id="imageModal" class="image-modal" onclick="closeImageModal()">
        <img id="modalImage" src="">
    </div>

    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getDatabase, ref, push, onChildAdded, set, update, onValue, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
        import { getStorage, ref as storageRef, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-storage.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
        
        // REPLACE THIS WITH YOUR FIREBASE CONFIG FROM FIREBASE CONSOLE!
        const firebaseConfig = {
            apiKey: "AIzaSyBU-ic-SGb-Qlxr4JAK2JXXTdetLhhQetI",
            authDomain: "project-p-5c219.firebaseapp.com",
            databaseURL: "https://project-p-5c219-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "project-p-5c219",
            storageBucket: "project-p-5c219.firebasestorage.app",
            messagingSenderId: "564190205574",
            appId: "1:564190205574:web:fba28383fd60b733dee307"
        };
        
        // Initialize Firebase
        const app = initializeApp(firebaseConfig);
        const database = getDatabase(app);
        const storage = getStorage(app);
        const auth = getAuth(app);
        
        // Global variables
        let currentUser = null;
        let currentUserId = null;
        let typingTimeout = null;
        let isTyping = false;
        
        // Login function
        window.login = async function() {
            const username = document.getElementById('usernameInput').value.trim();
            if (!username) {
                alert("Please enter your name");
                return;
            }
            
            try {
                // Sign in anonymously with Firebase
                const userCredential = await signInAnonymously(auth);
                currentUserId = userCredential.user.uid;
                currentUser = username;
                
                // Save user info to database
                await set(ref(database, 'users/' + currentUserId), {
                    name: currentUser,
                    online: true,
                    lastSeen: serverTimestamp()
                });
                
                // Show chat interface
                document.getElementById('loginSection').style.display = 'none';
                document.getElementById('chatSection').style.display = 'flex';
                document.getElementById('header').style.display = 'flex';
                document.getElementById('userAvatar').textContent = currentUser.charAt(0).toUpperCase();
                document.getElementById('onlineStatus').innerHTML = '✅ Online';
                document.getElementById('onlineStatus').classList.add('online');
                
                // Load messages
                loadMessages();
                
                // Set up typing listeners
                setupTypingListener();
                
                // Update online status when tab closes
                window.addEventListener('beforeunload', () => {
                    update(ref(database, 'users/' + currentUserId), {
                        online: false,
                        lastSeen: serverTimestamp()
                    });
                });
                
            } catch (error) {
                console.error("Login error:", error);
                alert("Error logging in. Make sure you've set up Firebase correctly!");
            }
        };
        
        // Load and display messages
        function loadMessages() {
            const messagesRef = ref(database, 'messages');
            onChildAdded(messagesRef, (snapshot) => {
                const message = snapshot.val();
                displayMessage(message);
            });
        }
        
        // Display a single message
        function displayMessage(message) {
            const container = document.getElementById('messagesArea');
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${message.userId === currentUserId ? 'sent' : 'received'}`;
            
            let content = `<div class="message-user">${message.userName}</div>`;
            
            if (message.text) {
                content += `<div class="message-text">${escapeHtml(message.text)}</div>`;
            }
            
            if (message.imageUrl) {
                content += `<img src="${message.imageUrl}" class="message-image" onclick="event.stopPropagation(); showImageModal('${message.imageUrl}')" loading="lazy">`;
            }
            
            const time = new Date(message.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            content += `<div class="message-time">${time}</div>`;
            
            messageDiv.innerHTML = content;
            container.appendChild(messageDiv);
            container.scrollTop = container.scrollHeight;
        }
        
        // Send message (text or image)
        window.sendMessage = async function() {
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            
            if (!text && !pendingImage) {
                return;
            }
            
            // Clear typing indicator
            clearTypingTimeout();
            
            const messageData = {
                userId: currentUserId,
                userName: currentUser,
                timestamp: serverTimestamp()
            };
            
            if (text) {
                messageData.text = text;
                input.value = '';
                input.style.height = 'auto';
            }
            
            if (pendingImage) {
                messageData.imageUrl = pendingImage;
                pendingImage = null;
            }
            
            // Send to Firebase
            const messagesRef = ref(database, 'messages');
            await push(messagesRef, messageData);
        };
        
        // Image upload handling
        let pendingImage = null;
        document.getElementById('imageUpload').addEventListener('change', async (e) => {
            const file = e.target.files[0];
            if (!file) return;
            
            // Show loading indicator
            const sendBtn = document.querySelector('.send-btn');
            const originalText = sendBtn.textContent;
            sendBtn.textContent = '📤 Uploading...';
            sendBtn.disabled = true;
            
            try {
                // Upload to Firebase Storage
                const imageRef = storageRef(storage, `images/${Date.now()}_${file.name}`);
                await uploadBytes(imageRef, file);
                const imageUrl = await getDownloadURL(imageRef);
                
                pendingImage = imageUrl;
                sendBtn.textContent = 'Send Image →';
                sendBtn.disabled = false;
                
                // Auto-send after upload
                setTimeout(() => {
                    if (pendingImage) {
                        sendMessage();
                        sendBtn.textContent = originalText;
                    }
                }, 500);
                
            } catch (error) {
                console.error("Upload error:", error);
                alert("Failed to upload image. Check Firebase Storage rules!");
                sendBtn.textContent = originalText;
                sendBtn.disabled = false;
            }
            
            e.target.value = '';
        });
        
        // Typing indicators
        function setupTypingListener() {
            const typingRef = ref(database, 'typing');
            onValue(typingRef, (snapshot) => {
                const typingData = snapshot.val();
                if (typingData && typingData.userId !== currentUserId && typingData.isTyping) {
                    const indicator = document.getElementById('typingIndicator');
                    indicator.style.display = 'flex';
                    indicator.querySelector('span').innerHTML = `${typingData.userName} is typing`;
                    
                    setTimeout(() => {
                        indicator.style.display = 'none';
                    }, 1000);
                } else {
                    document.getElementById('typingIndicator').style.display = 'none';
                }
            });
        }
        
        // Handle typing in input
        document.getElementById('messageInput').addEventListener('input', () => {
            if (!currentUserId) return;
            
            if (!isTyping) {
                isTyping = true;
                update(ref(database, 'typing'), {
                    userId: currentUserId,
                    userName: currentUser,
                    isTyping: true,
                    timestamp: serverTimestamp()
                });
            }
            
            clearTimeout(typingTimeout);
            typingTimeout = setTimeout(() => {
                isTyping = false;
                update(ref(database, 'typing'), {
                    isTyping: false
                });
            }, 1000);
        });
        
        function clearTypingTimeout() {
            if (typingTimeout) clearTimeout(typingTimeout);
            if (isTyping) {
                update(ref(database, 'typing'), { isTyping: false });
                isTyping = false;
            }
        }
        
        // Auto-resize textarea
        document.getElementById('messageInput').addEventListener('input', function() {
            this.style.height = 'auto';
            this.style.height = Math.min(this.scrollHeight, 100) + 'px';
        });
        
        window.handleKeyPress = function(event) {
            if (event.key === 'Enter' && !event.shiftKey) {
                event.preventDefault();
                sendMessage();
            }
        };
        
        // Emoji picker
        window.toggleEmojiPicker = async function() {
            const modal = document.getElementById('emojiPickerModal');
            
            if (modal.classList.contains('active')) {
                modal.classList.remove('active');
                return;
            }
            
            // Dynamically load emoji picker
            if (!window.EmojiMart) {
                await import('https://cdn.jsdelivr.net/npm/emoji-mart@5.5.2/dist/index.js');
                const Picker = window.emojiMart.Picker;
                const picker = new Picker({
                    onEmojiSelect: (emoji) => {
                        const input = document.getElementById('messageInput');
                        input.value += emoji.native;
                        input.focus();
                        modal.classList.remove('active');
                    }
                });
                modal.innerHTML = '';
                modal.appendChild(picker);
            }
            
            modal.classList.toggle('active');
        };
        
        window.showImageModal = function(url) {
            const modal = document.getElementById('imageModal');
            document.getElementById('modalImage').src = url;
            modal.classList.add('active');
        };
        
        window.closeImageModal = function() {
            document.getElementById('imageModal').classList.remove('active');
        };
        
        window.logout = function() {
            if (currentUserId) {
                update(ref(database, 'users/' + currentUserId), {
                    online: false,
                    lastSeen: serverTimestamp()
                });
            }
            location.reload();
        };
        
        // Helper function to escape HTML
        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }
        
        // Close emoji picker when clicking outside
        document.addEventListener('click', (e) => {
            const modal = document.getElementById('emojiPickerModal');
            if (modal && !modal.contains(e.target) && !e.target.classList.contains('emoji-btn')) {
                modal.classList.remove('active');
            }
        });
    </script>
</body>
</html>
