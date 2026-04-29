<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>ChatPro - Free Messenger</title>
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
            overflow: hidden;
        }

        /* Login Screen */
        .login-container {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(135deg, #0B141A 0%, #1a2a33 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .login-card {
            background: #111B21;
            border-radius: 28px;
            padding: 40px 30px;
            width: 90%;
            max-width: 400px;
            text-align: center;
            box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5);
            animation: slideUp 0.5s ease;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .logo {
            font-size: 64px;
            margin-bottom: 20px;
        }

        .login-card h1 {
            color: #E9EDEF;
            font-size: 28px;
            margin-bottom: 8px;
        }

        .login-card p {
            color: #8696A0;
            font-size: 14px;
            margin-bottom: 30px;
        }

        .login-input {
            width: 100%;
            padding: 14px 18px;
            background: #2A3942;
            border: none;
            border-radius: 16px;
            color: white;
            font-size: 16px;
            margin-bottom: 15px;
        }

        .login-input:focus {
            outline: none;
            background: #2F3E48;
        }

        .avatar-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
            margin: 20px 0;
        }

        .avatar-option {
            background: #2A3942;
            border-radius: 50%;
            padding: 12px;
            font-size: 28px;
            cursor: pointer;
            transition: all 0.2s;
            text-align: center;
        }

        .avatar-option:hover {
            transform: scale(1.1);
            background: #25D366;
        }

        .avatar-option.selected {
            background: #25D366;
            transform: scale(1.05);
        }

        .login-btn {
            width: 100%;
            padding: 14px;
            background: #25D366;
            border: none;
            border-radius: 16px;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
        }

        .login-btn:hover {
            background: #1da15a;
            transform: translateY(-2px);
        }

        /* Main Chat Interface */
        .chat-container {
            display: none;
            width: 100%;
            height: 100vh;
        }

        .chat-container.active {
            display: flex;
        }

        /* Sidebar */
        .sidebar {
            width: 300px;
            background: #111B21;
            border-right: 1px solid #2A3942;
            display: flex;
            flex-direction: column;
        }

        .sidebar-header {
            padding: 20px;
            background: #202C33;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .user-avatar {
            width: 48px;
            height: 48px;
            background: #25D366;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
        }

        .user-name {
            color: white;
            font-weight: bold;
        }

        .logout-icon {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: background 0.2s;
        }

        .logout-icon:hover {
            background: #2A3942;
        }

        .search-box {
            padding: 15px;
            background: #111B21;
        }

        .search-box input {
            width: 100%;
            padding: 10px 15px;
            background: #202C33;
            border: none;
            border-radius: 20px;
            color: white;
        }

        .groups-list, .users-list {
            flex: 1;
            overflow-y: auto;
            padding: 10px;
        }

        .section-title {
            color: #8696A0;
            font-size: 12px;
            padding: 10px;
            letter-spacing: 1px;
        }

        .group-item, .user-item {
            padding: 12px;
            margin: 4px 0;
            border-radius: 12px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 12px;
            transition: background 0.2s;
            color: #E9EDEF;
        }

        .group-item:hover, .user-item:hover {
            background: #202C33;
        }

        .group-item.active {
            background: #2A3942;
        }

        .create-group-btn {
            background: #25D366;
            border: none;
            width: 28px;
            height: 28px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 18px;
            margin-left: 10px;
        }

        /* Chat Area */
        .chat-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            background: #0B141A;
        }

        .chat-header {
            background: #202C33;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .chat-title {
            color: white;
            font-weight: bold;
            font-size: 18px;
        }

        .member-count {
            color: #8696A0;
            font-size: 12px;
            margin-top: 4px;
        }

        .messages-area {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        /* Message Bubbles */
        .message {
            max-width: 70%;
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

        .message-sender {
            font-size: 11px;
            color: #25D366;
            margin-bottom: 4px;
            font-weight: bold;
        }

        .message-text {
            font-size: 14px;
            word-wrap: break-word;
        }

        .message-image {
            max-width: 250px;
            max-height: 250px;
            border-radius: 8px;
            margin-top: 4px;
            cursor: pointer;
        }

        .message-time {
            font-size: 10px;
            color: rgba(255,255,255,0.6);
            margin-top: 4px;
            text-align: right;
        }

        .read-status {
            font-size: 10px;
            margin-left: 8px;
        }

        /* Message Reactions */
        .message-reactions {
            display: flex;
            gap: 4px;
            margin-top: 6px;
        }

        .reaction {
            background: rgba(0,0,0,0.3);
            padding: 2px 6px;
            border-radius: 12px;
            font-size: 11px;
            cursor: pointer;
        }

        /* Typing Indicator */
        .typing-indicator {
            padding: 8px 20px;
            color: #8696A0;
            font-size: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .typing-indicator.hidden {
            display: none;
        }

        .typing-dots::after {
            content: '...';
            animation: typing 1.5s infinite;
        }

        @keyframes typing {
            0%, 20% { content: '.'; }
            40%, 60% { content: '..'; }
            80%, 100% { content: '...'; }
        }

        /* Input Area */
        .input-area {
            padding: 15px 20px;
            background: #202C33;
            display: flex;
            gap: 12px;
            align-items: center;
        }

        .input-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: background 0.2s;
            color: #8696A0;
        }

        .input-btn:hover {
            background: #2A3942;
            color: #25D366;
        }

        .message-input {
            flex: 1;
            padding: 10px 16px;
            background: #2A3942;
            border: none;
            border-radius: 24px;
            color: white;
            font-size: 14px;
            resize: none;
        }

        .message-input:focus {
            outline: none;
        }

        .send-btn {
            padding: 8px 20px;
            background: #25D366;
            border: none;
            border-radius: 24px;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }

        /* Emoji Picker */
        .emoji-picker {
            position: absolute;
            bottom: 80px;
            right: 20px;
            background: #202C33;
            border-radius: 16px;
            padding: 12px;
            max-width: 280px;
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 8px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.3);
            z-index: 100;
        }

        .emoji-picker.hidden {
            display: none;
        }

        .emoji-item {
            font-size: 24px;
            cursor: pointer;
            text-align: center;
            padding: 4px;
            transition: transform 0.1s;
        }

        .emoji-item:hover {
            transform: scale(1.2);
        }

        /* Reaction Picker */
        .reaction-picker {
            position: absolute;
            background: #202C33;
            border-radius: 24px;
            padding: 8px;
            display: flex;
            gap: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
            z-index: 100;
        }

        .reaction-picker.hidden {
            display: none;
        }

        .reaction-option {
            font-size: 20px;
            cursor: pointer;
            padding: 4px 8px;
            transition: transform 0.1s;
        }

        .reaction-option:hover {
            transform: scale(1.2);
        }

        /* Image Modal */
        .image-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.95);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .image-modal.active {
            display: flex;
        }

        .image-modal img {
            max-width: 90%;
            max-height: 90%;
            border-radius: 8px;
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .sidebar {
                position: fixed;
                left: -300px;
                top: 0;
                bottom: 0;
                z-index: 200;
                transition: left 0.3s;
            }
            
            .sidebar.open {
                left: 0;
            }
            
            .message {
                max-width: 85%;
            }
            
            .menu-toggle {
                display: block;
            }
        }

        .menu-toggle {
            display: none;
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            margin-right: 15px;
        }

        /* Scrollbar */
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
    </style>
</head>
<body>
    <!-- Login Screen -->
    <div id="loginScreen" class="login-container">
        <div class="login-card">
            <div class="logo">💬</div>
            <h1>ChatPro</h1>
            <p>Free Real-time Messenger</p>
            <input type="text" id="userName" class="login-input" placeholder="Enter your name" maxlength="25">
            <div class="avatar-grid" id="avatarGrid">
                <div class="avatar-option" data-avatar="😀">😀</div>
                <div class="avatar-option" data-avatar="😎">😎</div>
                <div class="avatar-option" data-avatar="🥰">🥰</div>
                <div class="avatar-option" data-avatar="🤓">🤓</div>
                <div class="avatar-option" data-avatar="👨‍💻">👨‍💻</div>
                <div class="avatar-option" data-avatar="👩‍💻">👩‍💻</div>
                <div class="avatar-option" data-avatar="🐱">🐱</div>
                <div class="avatar-option" data-avatar="⭐">⭐</div>
            </div>
            <button class="login-btn" onclick="app.login()">Start Chatting →</button>
        </div>
    </div>

    <!-- Main Chat Interface -->
    <div id="chatContainer" class="chat-container">
        <div class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <div class="user-profile">
                    <div class="user-avatar" id="userAvatar">😀</div>
                    <div class="user-name" id="userDisplayName">User</div>
                </div>
                <button class="logout-icon" onclick="app.logout()">🚪</button>
            </div>
            <div class="search-box">
                <input type="text" id="searchUsers" placeholder="Search users..." oninput="app.searchUsers(this.value)">
            </div>
            <div class="groups-list">
                <div class="section-title">
                    GROUPS 
                    <button class="create-group-btn" onclick="app.createGroup()">+</button>
                </div>
                <div id="groupsList"></div>
            </div>
            <div class="users-list">
                <div class="section-title">ONLINE USERS</div>
                <div id="onlineUsersList"></div>
            </div>
        </div>

        <div class="chat-area">
            <div class="chat-header">
                <button class="menu-toggle" onclick="app.toggleSidebar()">☰</button>
                <div>
                    <div class="chat-title" id="chatTitle">General</div>
                    <div class="member-count" id="memberCount"></div>
                </div>
            </div>

            <div class="messages-area" id="messagesArea"></div>

            <div class="typing-indicator hidden" id="typingIndicator">
                <span>Someone is typing</span>
                <span class="typing-dots"></span>
            </div>

            <div class="input-area">
                <button class="input-btn" onclick="app.openEmojiPicker()">😊</button>
                <input type="file" id="imageUpload" accept="image/*" style="display:none">
                <button class="input-btn" onclick="document.getElementById('imageUpload').click()">📎</button>
                <textarea id="messageInput" class="message-input" placeholder="Type a message..." rows="1" onkeypress="app.handleKeyPress(event)"></textarea>
                <button class="send-btn" onclick="app.sendMessage()">Send</button>
            </div>
        </div>
    </div>

    <div id="emojiPicker" class="emoji-picker hidden"></div>
    <div id="reactionPicker" class="reaction-picker hidden"></div>
    <div id="imageModal" class="image-modal" onclick="this.classList.remove('active')">
        <img id="modalImage" src="">
    </div>

    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-database-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-auth-compat.js"></script>

    <script>
        // ============ FIREBASE CONFIGURATION ============
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
        firebase.initializeApp(firebaseConfig);
        const database = firebase.database();
        const auth = firebase.auth();

        // ============ MAIN APP ============
        const app = {
            currentUser: null,
            currentUserId: null,
            currentAvatar: '😀',
            currentGroup: 'general',
            typingTimeout: null,
            isTyping: false,
            selectedAvatar: '😀',
            pendingImage: null,

            // Login
            async login() {
                const userName = document.getElementById('userName').value.trim();
                if (!userName) {
                    alert('Please enter your name');
                    return;
                }

                // Get selected avatar
                const selected = document.querySelector('.avatar-option.selected');
                if (selected) this.currentAvatar = selected.dataset.avatar;

                try {
                    // Anonymous sign in
                    const userCredential = await auth.signInAnonymously();
                    this.currentUserId = userCredential.user.uid;
                    this.currentUser = userName;

                    // Save user to database
                    await database.ref('users/' + this.currentUserId).set({
                        name: this.currentUser,
                        avatar: this.currentAvatar,
                        online: true,
                        lastSeen: firebase.database.ServerValue.TIMESTAMP
                    });

                    // Update UI
                    document.getElementById('loginScreen').style.display = 'none';
                    document.getElementById('chatContainer').classList.add('active');
                    document.getElementById('userAvatar').innerText = this.currentAvatar;
                    document.getElementById('userDisplayName').innerText = this.currentUser;

                    // Load data
                    this.loadGroups();
                    this.loadOnlineUsers();
                    this.loadMessages();
                    this.setupTypingIndicator();
                    
                    // Set online status on disconnect
                    window.addEventListener('beforeunload', () => {
                        database.ref('users/' + this.currentUserId).update({
                            online: false,
                            lastSeen: firebase.database.ServerValue.TIMESTAMP
                        });
                    });

                } catch (error) {
                    console.error('Login error:', error);
                    alert('Login failed. Check Firebase configuration!');
                }
            },

            // Avatar selection
            initAvatarSelection() {
                document.querySelectorAll('.avatar-option').forEach(avatar => {
                    avatar.onclick = () => {
                        document.querySelectorAll('.avatar-option').forEach(a => a.classList.remove('selected'));
                        avatar.classList.add('selected');
                        this.selectedAvatar = avatar.dataset.avatar;
                    };
                });
                // Select first avatar by default
                document.querySelector('.avatar-option').classList.add('selected');
            },

            // Group Functions
            async createGroup() {
                const groupName = prompt('Enter group name:');
                if (!groupName) return;

                const groupId = 'group_' + Date.now();
                await database.ref('groups/' + groupId).set({
                    name: groupName,
                    createdBy: this.currentUserId,
                    createdAt: firebase.database.ServerValue.TIMESTAMP,
                    members: {
                        [this.currentUserId]: true
                    }
                });
            },

            async addToGroup(groupId) {
                const userId = prompt('Enter user ID to add:');
                if (userId) {
                    await database.ref(`groups/${groupId}/members/${userId}`).set(true);
                }
            },

            loadGroups() {
                database.ref('groups').on('value', (snapshot) => {
                    const groups = snapshot.val() || {};
                    const groupsList = document.getElementById('groupsList');
                    groupsList.innerHTML = '';

                    // Add General group
                    const generalDiv = document.createElement('div');
                    generalDiv.className = `group-item ${this.currentGroup === 'general' ? 'active' : ''}`;
                    generalDiv.innerHTML = '💬 General Chat';
                    generalDiv.onclick = () => this.switchGroup('general');
                    groupsList.appendChild(generalDiv);

                    // Add user's groups
                    Object.entries(groups).forEach(([id, group]) => {
                        if (group.members && group.members[this.currentUserId]) {
                            const groupDiv = document.createElement('div');
                            groupDiv.className = `group-item ${this.currentGroup === id ? 'active' : ''}`;
                            groupDiv.innerHTML = `👥 ${group.name}`;
                            groupDiv.onclick = () => this.switchGroup(id);
                            groupsList.appendChild(groupDiv);
                        }
                    });
                });
            },

            switchGroup(groupId) {
                this.currentGroup = groupId;
                document.getElementById('chatTitle').innerText = groupId === 'general' ? 'General Chat' : 'Group Chat';
                document.getElementById('messagesArea').innerHTML = '';
                this.loadMessages();
                
                // Update active state in groups list
                document.querySelectorAll('.group-item').forEach(item => {
                    item.classList.remove('active');
                });
            },

            // Online Users
            loadOnlineUsers() {
                database.ref('users').on('value', (snapshot) => {
                    const users = snapshot.val();
                    const usersList = document.getElementById('onlineUsersList');
                    usersList.innerHTML = '';

                    Object.entries(users).forEach(([id, user]) => {
                        if (id !== this.currentUserId && user.online) {
                            const userDiv = document.createElement('div');
                            userDiv.className = 'user-item';
                            userDiv.innerHTML = `
                                <div style="font-size: 28px">${user.avatar || '😀'}</div>
                                <div>
                                    <div>${user.name}</div>
                                    <small style="color:#25D366">● Online</small>
                                </div>
                            `;
                            usersList.appendChild(userDiv);
                        }
                    });
                });
            },

            searchUsers(query) {
                // Simple client-side search
                const items = document.querySelectorAll('.user-item');
                items.forEach(item => {
                    const text = item.innerText.toLowerCase();
                    if (text.includes(query.toLowerCase())) {
                        item.style.display = 'flex';
                    } else {
                        item.style.display = 'none';
                    }
                });
            },

            // Messages
            async sendMessage() {
                const input = document.getElementById('messageInput');
                const text = input.value.trim();
                
                if (!text && !this.pendingImage) return;

                this.clearTyping();

                const message = {
                    userId: this.currentUserId,
                    userName: this.currentUser,
                    userAvatar: this.currentAvatar,
                    groupId: this.currentGroup,
                    timestamp: firebase.database.ServerValue.TIMESTAMP,
                    readBy: { [this.currentUserId]: true }
                };

                if (text) {
                    message.text = text;
                    input.value = '';
                }

                if (this.pendingImage) {
                    message.imageUrl = this.pendingImage;
                    this.pendingImage = null;
                }

                const messageRef = database.ref('messages').push();
                await messageRef.set(message);
                
                this.scrollToBottom();
            },

            loadMessages() {
                const messagesRef = database.ref('messages');
                messagesRef.orderByChild('groupId').equalTo(this.currentGroup).on('child_added', (snapshot) => {
                    const message = snapshot.val();
                    this.displayMessage(message, snapshot.key);
                });
            },

            displayMessage(message, messageId) {
                const container = document.getElementById('messagesArea');
                const isSent = message.userId === this.currentUserId;
                
                const messageDiv = document.createElement('div');
                messageDiv.className = `message ${isSent ? 'sent' : 'received'}`;
                
                let content = `<div class="message-sender">${message.userName}</div>`;
                
                if (message.text) {
                    content += `<div class="message-text">${this.escapeHtml(message.text)}</div>`;
                }
                
                if (message.imageUrl) {
                    content += `<img src="${message.imageUrl}" class="message-image" onclick="app.showImage('${message.imageUrl}')">`;
                }
                
                const time = new Date(message.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                content += `<div class="message-time">${time}</div>`;
                content += `<div class="message-reactions" id="reactions-${messageId}"></div>`;
                
                messageDiv.innerHTML = content;
                container.appendChild(messageDiv);
                
                // Mark as read if not sent by current user
                if (!isSent) {
                    this.markAsRead(messageId);
                }
                
                // Load reactions for this message
                this.loadReactions(messageId);
                
                this.scrollToBottom();
            },

            async markAsRead(messageId) {
                const messageRef = database.ref(`messages/${messageId}`);
                const message = (await messageRef.once('value')).val();
                
                if (!message.seen && message.userId !== this.currentUserId) {
                    await messageRef.update({
                        seen: true,
                        seenAt: firebase.database.ServerValue.TIMESTAMP
                    });
                }
            },

            // Image Upload using Base64 (no external service needed)
            uploadImage() {
                const input = document.getElementById('imageUpload');
                input.click();
                input.onchange = (e) => {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    if (!file.type.startsWith('image/')) {
                        alert('Please select an image file');
                        return;
                    }
                    
                    // Compress and convert to base64
                    const reader = new FileReader();
                    reader.onload = (event) => {
                        this.pendingImage = event.target.result;
                        this.sendMessage();
                    };
                    reader.readAsDataURL(file);
                };
            },

            // Emoji Picker
            openEmojiPicker() {
                const picker = document.getElementById('emojiPicker');
                if (picker.classList.contains('hidden')) {
                    const emojis = ['😀','😃','😄','😁','😆','😅','😂','🤣','😊','😇','🙂','🙃','😉','😌','😍','🥰','😘','😗','😙','😚','😋','😛','😝','😜','🤪','🤨','🧐','🤓','😎','🤩','🥳','😏','😒','😞','😔','😟','😕','🙁','☹️','😣','😖','😫','😩','🥺','😢','😭','😤','😠','😡','🤬','🤯','😳','🥵','🥶','😱','😨','😰','😥','😓','🤗','🤔','🤭','🤫','🤥','😶','😐','😑','😬','🙄','😯','😦','😧','😮','😲','🥱','😴','🤤','😪','😵'];
                    
                    picker.innerHTML = '';
                    emojis.forEach(emoji => {
                        const span = document.createElement('span');
                        span.className = 'emoji-item';
                        span.innerText = emoji;
                        span.onclick = () => {
                            const input = document.getElementById('messageInput');
                            input.value += emoji;
                            input.focus();
                            picker.classList.add('hidden');
                        };
                        picker.appendChild(span);
                    });
                    picker.classList.remove('hidden');
                } else {
                    picker.classList.add('hidden');
                }
            },

            // Reactions
            showReactionPicker(event, messageId) {
                event.stopPropagation();
                const picker = document.getElementById('reactionPicker');
                const reactions = ['👍', '❤️', '😂', '😮', '😢', '😡'];
                
                picker.innerHTML = '';
                reactions.forEach(reaction => {
                    const span = document.createElement('span');
                    span.className = 'reaction-option';
                    span.innerText = reaction;
                    span.onclick = () => this.addReaction(messageId, reaction);
                    picker.appendChild(span);
                });
                
                const rect = event.target.getBoundingClientRect();
                picker.style.top = rect.top - 50 + 'px';
                picker.style.left = rect.left + 'px';
                picker.classList.remove('hidden');
                
                setTimeout(() => {
                    document.addEventListener('click', () => {
                        picker.classList.add('hidden');
                    }, { once: true });
                }, 100);
            },

            async addReaction(messageId, reaction) {
                const reactionRef = database.ref(`reactions/${messageId}/${reaction}`);
                const users = (await reactionRef.once('value')).val() || [];
                
                if (!users.includes(this.currentUserId)) {
                    users.push(this.currentUserId);
                    await reactionRef.set(users);
                }
                
                document.getElementById('reactionPicker').classList.add('hidden');
            },

            loadReactions(messageId) {
                database.ref(`reactions/${messageId}`).on('value', (snapshot) => {
                    const reactions = snapshot.val();
                    const container = document.getElementById(`reactions-${messageId}`);
                    if (!container) return;
                    
                    container.innerHTML = '';
                    if (reactions) {
                        Object.entries(reactions).forEach(([emoji, users]) => {
                            const reactionSpan = document.createElement('span');
                            reactionSpan.className = 'reaction';
                            reactionSpan.innerHTML = `${emoji} ${users.length}`;
                            container.appendChild(reactionSpan);
                        });
                    }
                });
            },

            // Typing Indicator
            setupTypingIndicator() {
                const typingRef = database.ref('typing');
                const input = document.getElementById('messageInput');
                
                input.addEventListener('input', () => {
                    if (!this.isTyping) {
                        this.isTyping = true;
                        typingRef.set({
                            userId: this.currentUserId,
                            userName: this.currentUser,
                            groupId: this.currentGroup,
                            isTyping: true
                        });
                    }
                    
                    clearTimeout(this.typingTimeout);
                    this.typingTimeout = setTimeout(() => {
                        this.isTyping = false;
                        typingRef.set({ isTyping: false });
                    }, 1000);
                });
                
                typingRef.on('value', (snapshot) => {
                    const data = snapshot.val();
                    const indicator = document.getElementById('typingIndicator');
                    
                    if (data && data.isTyping && data.userId !== this.currentUserId && data.groupId === this.currentGroup) {
                        indicator.classList.remove('hidden');
                        indicator.querySelector('span').innerHTML = `${data.userName} is typing`;
                    } else {
                        indicator.classList.add('hidden');
                    }
                });
            },

            clearTyping() {
                if (this.isTyping) {
                    database.ref('typing').set({ isTyping: false });
                    this.isTyping = false;
                }
            },

            // Utility Functions
            handleKeyPress(event) {
                if (event.key === 'Enter' && !event.shiftKey) {
                    event.preventDefault();
                    this.sendMessage();
                }
            },

            showImage(url) {
                const modal = document.getElementById('imageModal');
                document.getElementById('modalImage').src = url;
                modal.classList.add('active');
            },

            scrollToBottom() {
                const container = document.getElementById('messagesArea');
                setTimeout(() => {
                    container.scrollTop = container.scrollHeight;
                }, 100);
            },

            escapeHtml(text) {
                const div = document.createElement('div');
                div.textContent = text;
                return div.innerHTML;
            },

            toggleSidebar() {
                document.getElementById('sidebar').classList.toggle('open');
            },

            logout() {
                database.ref('users/' + this.currentUserId).update({
                    online: false,
                    lastSeen: firebase.database.ServerValue.TIMESTAMP
                });
                location.reload();
            }
        };

        // Initialize avatar selection
        app.initAvatarSelection();

        // Close emoji picker on outside click
        document.addEventListener('click', (e) => {
            const emojiPicker = document.getElementById('emojiPicker');
            if (!emojiPicker.contains(e.target) && !e.target.classList.contains('input-btn')) {
                emojiPicker.classList.add('hidden');
            }
        });
    </script>
</body>
</html>
