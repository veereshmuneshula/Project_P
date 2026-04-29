<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>ChatPro Plus - Advanced Real-time Messenger</title>
    
    <!-- Google Fonts - Poppins -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-database-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-storage-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-auth-compat.js"></script>
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
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
            font-weight: 600;
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
            font-family: 'Poppins', sans-serif;
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
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            font-family: 'Poppins', sans-serif;
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
            width: 320px;
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
            font-weight: 600;
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
            font-family: 'Poppins', sans-serif;
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
            font-weight: 500;
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
            font-weight: 400;
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
            font-weight: 600;
            font-size: 18px;
        }

        .chat-actions {
            display: flex;
            gap: 12px;
        }

        .chat-action-btn {
            background: none;
            border: none;
            color: #8696A0;
            font-size: 20px;
            cursor: pointer;
            padding: 6px;
            border-radius: 50%;
            transition: all 0.2s;
        }

        .chat-action-btn:hover {
            background: #2A3942;
            color: #25D366;
        }

        .member-count {
            color: #8696A0;
            font-size: 12px;
            margin-top: 4px;
        }

        /* Messages Area */
        .messages-area {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        /* Message Selection Mode */
        .selection-mode .message {
            cursor: pointer;
            transition: opacity 0.2s;
        }

        .selection-mode .message.selected {
            opacity: 0.6;
            border: 2px solid #25D366;
        }

        .selection-bar {
            background: #25D366;
            padding: 12px 20px;
            display: none;
            justify-content: space-between;
            align-items: center;
            color: white;
        }

        .selection-bar.active {
            display: flex;
        }

        .selection-bar button {
            background: white;
            border: none;
            padding: 6px 12px;
            border-radius: 8px;
            cursor: pointer;
            font-family: 'Poppins', sans-serif;
            font-weight: 500;
        }

        /* Message Bubbles */
        .message {
            max-width: 70%;
            padding: 10px 14px;
            border-radius: 16px;
            position: relative;
            animation: fadeIn 0.3s ease;
            transition: all 0.2s;
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

        .message.view-once {
            opacity: 0.8;
            filter: blur(2px);
            transition: all 0.3s;
        }

        .message.view-once.viewed {
            display: none;
        }

        .message-sender {
            font-size: 11px;
            color: #25D366;
            margin-bottom: 4px;
            font-weight: 600;
        }

        .message-text {
            font-size: 14px;
            word-wrap: break-word;
            font-weight: 400;
        }

        .message-edited {
            font-size: 9px;
            color: rgba(255,255,255,0.5);
            margin-left: 5px;
        }

        .message-media {
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
            display: flex;
            justify-content: flex-end;
            gap: 8px;
            align-items: center;
        }

        .message-actions {
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
            display: none;
            gap: 4px;
            background: #202C33;
            padding: 4px;
            border-radius: 20px;
        }

        .message:hover .message-actions {
            display: flex;
        }

        .msg-action-btn {
            background: none;
            border: none;
            font-size: 14px;
            cursor: pointer;
            padding: 4px 6px;
            border-radius: 50%;
            transition: background 0.2s;
        }

        .msg-action-btn:hover {
            background: #2A3942;
        }

        .read-status {
            font-size: 10px;
        }

        /* Message Reactions */
        .message-reactions {
            display: flex;
            gap: 4px;
            margin-top: 6px;
            flex-wrap: wrap;
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
            font-family: 'Poppins', sans-serif;
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
            font-weight: 600;
            cursor: pointer;
            font-family: 'Poppins', sans-serif;
        }

        /* File Upload Modal */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: #111B21;
            border-radius: 20px;
            padding: 24px;
            width: 90%;
            max-width: 400px;
        }

        .modal-content h3 {
            color: white;
            margin-bottom: 20px;
            font-weight: 600;
        }

        .file-option {
            background: #202C33;
            padding: 15px;
            margin: 10px 0;
            border-radius: 12px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 12px;
            transition: background 0.2s;
        }

        .file-option:hover {
            background: #2A3942;
        }

        .view-once-toggle {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 15px 0;
            color: white;
        }

        .toggle-switch {
            width: 50px;
            height: 24px;
            background: #2A3942;
            border-radius: 12px;
            cursor: pointer;
            position: relative;
            transition: background 0.2s;
        }

        .toggle-switch.active {
            background: #25D366;
        }

        .toggle-switch::after {
            content: '';
            width: 20px;
            height: 20px;
            background: white;
            border-radius: 50%;
            position: absolute;
            top: 2px;
            left: 3px;
            transition: left 0.2s;
        }

        .toggle-switch.active::after {
            left: 27px;
        }

        /* Edit Message Modal */
        .edit-input {
            width: 100%;
            padding: 12px;
            background: #2A3942;
            border: none;
            border-radius: 12px;
            color: white;
            margin: 15px 0;
            font-family: 'Poppins', sans-serif;
        }

        .modal-buttons {
            display: flex;
            gap: 12px;
            justify-content: flex-end;
        }

        .modal-buttons button {
            padding: 10px 20px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-family: 'Poppins', sans-serif;
            font-weight: 500;
        }

        .btn-primary {
            background: #25D366;
            color: white;
        }

        .btn-secondary {
            background: #2A3942;
            color: white;
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
            z-index: 2000;
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
                left: -320px;
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

        /* Loading Spinner */
        .spinner {
            display: inline-block;
            width: 16px;
            height: 16px;
            border: 2px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 0.6s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <!-- Login Screen -->
    <div id="loginScreen" class="login-container">
        <div class="login-card">
            <div class="logo">💬</div>
            <h1>Project P </h1>
            <p>Advanced Real-time Messenger</p>
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
                <div class="chat-actions">
                    <button class="chat-action-btn" onclick="app.toggleSelectionMode()" title="Select Messages">☑️</button>
                    <button class="chat-action-btn" onclick="app.clearAllMessages()" title="Clear All Messages">🗑️</button>
                </div>
            </div>

            <!-- Selection Bar -->
            <div id="selectionBar" class="selection-bar">
                <span id="selectedCount">0 selected</span>
                <div>
                    <button onclick="app.deleteSelectedMessages()">Delete Selected</button>
                    <button onclick="app.cancelSelection()">Cancel</button>
                </div>
            </div>

            <div class="messages-area" id="messagesArea"></div>

            <div class="typing-indicator hidden" id="typingIndicator">
                <span>Someone is typing</span>
                <span class="typing-dots"></span>
            </div>

            <div class="input-area">
                <button class="input-btn" onclick="app.openEmojiPicker()">😊</button>
                <button class="input-btn" onclick="app.openFileUploadModal()">📎</button>
                <textarea id="messageInput" class="message-input" placeholder="Type a message..." rows="1" onkeypress="app.handleKeyPress(event)"></textarea>
                <button class="send-btn" onclick="app.sendMessage()">Send</button>
            </div>
        </div>
    </div>

    <!-- File Upload Modal -->
    <div id="fileUploadModal" class="modal">
        <div class="modal-content">
            <h3>Upload File</h3>
            <div class="file-option" onclick="app.uploadImage()">
                📷 Upload Image
            </div>
            <div class="file-option" onclick="app.uploadVideo()">
                🎥 Upload Video
            </div>
            <div class="file-option" onclick="app.uploadDocument()">
                📄 Upload Document
            </div>
            <div class="view-once-toggle">
                <span>View Once Mode</span>
                <div id="viewOnceToggle" class="toggle-switch" onclick="app.toggleViewOnce()"></div>
            </div>
            <button class="btn-secondary" onclick="app.closeFileUploadModal()" style="width:100%; margin-top:10px;">Cancel</button>
        </div>
    </div>

    <!-- Edit Message Modal -->
    <div id="editModal" class="modal">
        <div class="modal-content">
            <h3>Edit Message</h3>
            <input type="text" id="editInput" class="edit-input" placeholder="Edit your message...">
            <div class="modal-buttons">
                <button class="btn-secondary" onclick="app.closeEditModal()">Cancel</button>
                <button class="btn-primary" onclick="app.saveEditedMessage()">Save</button>
            </div>
        </div>
    </div>

    <!-- Delete Options Modal -->
    <div id="deleteModal" class="modal">
        <div class="modal-content">
            <h3>Delete Message</h3>
            <div class="file-option" onclick="app.deleteMessageForMe()">
                🔒 Delete for me
            </div>
            <div class="file-option" onclick="app.deleteMessageForEveryone()">
                🌐 Delete for everyone
            </div>
            <button class="btn-secondary" onclick="app.closeDeleteModal()" style="width:100%; margin-top:10px;">Cancel</button>
        </div>
    </div>

    <!-- Emoji Picker -->
    <div id="emojiPicker" class="emoji-picker hidden"></div>

    <!-- Image Modal -->
    <div id="imageModal" class="image-modal" onclick="this.classList.remove('active')">
        <img id="modalImage" src="">
    </div>

    <script>
        // ============ FIREBASE CONFIGURATION ============
        // REPLACE WITH YOUR FIREBASE CONFIG FROM FIREBASE CONSOLE!
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
        const storage = firebase.storage();
        const auth = firebase.auth();

        // ============ MAIN APPLICATION ============
        const app = {
            // User Data
            currentUser: null,
            currentUserId: null,
            currentAvatar: '😀',
            currentGroup: 'general',
            
            // UI State
            typingTimeout: null,
            isTyping: false,
            selectionMode: false,
            selectedMessages: new Set(),
            viewOnceMode: false,
            currentEditMessageId: null,
            currentDeleteMessageId: null,
            
            // File Upload
            pendingFile: null,
            pendingFileType: null,

            // ============ AUTHENTICATION ============
            async login() {
                const userName = document.getElementById('userName').value.trim();
                if (!userName) {
                    alert('Please enter your name');
                    return;
                }

                const selected = document.querySelector('.avatar-option.selected');
                if (selected) this.currentAvatar = selected.dataset.avatar;

                try {
                    const userCredential = await auth.signInAnonymously();
                    this.currentUserId = userCredential.user.uid;
                    this.currentUser = userName;

                    await database.ref('users/' + this.currentUserId).set({
                        name: this.currentUser,
                        avatar: this.currentAvatar,
                        online: true,
                        lastSeen: firebase.database.ServerValue.TIMESTAMP
                    });

                    document.getElementById('loginScreen').style.display = 'none';
                    document.getElementById('chatContainer').classList.add('active');
                    document.getElementById('userAvatar').innerText = this.currentAvatar;
                    document.getElementById('userDisplayName').innerText = this.currentUser;

                    this.loadGroups();
                    this.loadOnlineUsers();
                    this.loadMessages();
                    this.setupTypingIndicator();
                    
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

            // ============ GROUP FUNCTIONS ============
            async createGroup() {
                const groupName = prompt('Enter group name:');
                if (!groupName) return;

                const groupId = 'group_' + Date.now();
                await database.ref('groups/' + groupId).set({
                    name: groupName,
                    createdBy: this.currentUserId,
                    createdAt: firebase.database.ServerValue.TIMESTAMP,
                    members: { [this.currentUserId]: true }
                });
            },

            loadGroups() {
                database.ref('groups').on('value', (snapshot) => {
                    const groups = snapshot.val() || {};
                    const groupsList = document.getElementById('groupsList');
                    groupsList.innerHTML = '';

                    const generalDiv = document.createElement('div');
                    generalDiv.className = `group-item ${this.currentGroup === 'general' ? 'active' : ''}`;
                    generalDiv.innerHTML = '💬 General Chat';
                    generalDiv.onclick = () => this.switchGroup('general');
                    groupsList.appendChild(generalDiv);

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
                this.cancelSelection();
                
                document.querySelectorAll('.group-item').forEach(item => {
                    item.classList.remove('active');
                });
            },

            // ============ ONLINE USERS ============
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
                const items = document.querySelectorAll('.user-item');
                items.forEach(item => {
                    const text = item.innerText.toLowerCase();
                    item.style.display = text.includes(query.toLowerCase()) ? 'flex' : 'none';
                });
            },

            // ============ MESSAGE FUNCTIONS ============
            async sendMessage() {
                const input = document.getElementById('messageInput');
                const text = input.value.trim();
                
                if (!text && !this.pendingFile) return;

                this.clearTyping();

                const message = {
                    userId: this.currentUserId,
                    userName: this.currentUser,
                    userAvatar: this.currentAvatar,
                    groupId: this.currentGroup,
                    timestamp: firebase.database.ServerValue.TIMESTAMP,
                    readBy: { [this.currentUserId]: true },
                    delivered: true
                };

                if (text) {
                    message.text = text;
                    input.value = '';
                }

                if (this.pendingFile) {
                    message.fileUrl = this.pendingFile.url;
                    message.fileType = this.pendingFile.type;
                    message.fileName = this.pendingFile.name;
                    if (this.viewOnceMode) {
                        message.viewOnce = true;
                        message.viewedBy = [];
                    }
                    this.pendingFile = null;
                    this.viewOnceMode = false;
                    document.getElementById('viewOnceToggle').classList.remove('active');
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

                // Listen for message updates (edits, deletes)
                messagesRef.on('child_changed', (snapshot) => {
                    const message = snapshot.val();
                    this.updateMessageDisplay(snapshot.key, message);
                });

                messagesRef.on('child_removed', (snapshot) => {
                    this.removeMessageDisplay(snapshot.key);
                });
            },

            displayMessage(message, messageId) {
                const container = document.getElementById('messagesArea');
                const isSent = message.userId === this.currentUserId;
                const isViewOnce = message.viewOnce === true;
                const isViewed = isViewOnce && message.viewedBy && message.viewedBy.includes(this.currentUserId);
                
                if (isViewOnce && isViewed) return;
                
                const messageDiv = document.createElement('div');
                messageDiv.className = `message ${isSent ? 'sent' : 'received'}`;
                if (isViewOnce && !isViewed) messageDiv.classList.add('view-once');
                messageDiv.id = `msg-${messageId}`;
                messageDiv.dataset.messageId = messageId;
                
                let content = `<div class="message-sender">${message.userName}</div>`;
                
                if (message.text) {
                    content += `<div class="message-text">${this.escapeHtml(message.text)}`;
                    if (message.edited) content += `<span class="message-edited">(edited)</span>`;
                    content += `</div>`;
                }
                
                if (message.fileUrl) {
                    if (message.fileType === 'image') {
                        content += `<img src="${message.fileUrl}" class="message-media" onclick="app.showImage('${message.fileUrl}', '${messageId}')">`;
                    } else if (message.fileType === 'video') {
                        content += `<video src="${message.fileUrl}" controls class="message-media"></video>`;
                    } else {
                        content += `<a href="${message.fileUrl}" download class="message-media" style="display:block; padding:10px; background:#2A3942; border-radius:8px; text-decoration:none; color:#25D366;">📄 ${message.fileName}</a>`;
                    }
                }
                
                const time = new Date(message.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                let readStatus = '';
                
                if (isSent) {
                    if (message.seen) readStatus = '✓✓ Seen';
                    else if (message.delivered) readStatus = '✓✓ Delivered';
                    else readStatus = '✓ Sent';
                }
                
                content += `
                    <div class="message-time">
                        ${time}
                        <span class="read-status">${readStatus}</span>
                    </div>
                    <div class="message-reactions" id="reactions-${messageId}"></div>
                `;
                
                // Add action buttons for sent messages
                if (isSent) {
                    content += `
                        <div class="message-actions">
                            <button class="msg-action-btn" onclick="app.openEditMessage('${messageId}', '${this.escapeHtml(message.text || '')}')">✏️</button>
                            <button class="msg-action-btn" onclick="app.openDeleteOptions('${messageId}')">🗑️</button>
                        </div>
                    `;
                }
                
                messageDiv.innerHTML = content;
                container.appendChild(messageDiv);
                
                // Mark as read if not sent by current user
                if (!isSent && !message.seen) {
                    this.markAsRead(messageId);
                }
                
                // Load reactions
                this.loadReactions(messageId);
                
                // Handle view-once auto-delete
                if (isViewOnce && !isViewed && !isSent) {
                    setTimeout(() => {
                        this.markViewOnceAsViewed(messageId);
                    }, 3000); // Auto-mark as viewed after 3 seconds
                }
                
                this.scrollToBottom();
            },

            updateMessageDisplay(messageId, message) {
                const messageDiv = document.getElementById(`msg-${messageId}`);
                if (!messageDiv) return;
                
                if (message.text) {
                    const textDiv = messageDiv.querySelector('.message-text');
                    if (textDiv) {
                        textDiv.innerHTML = `${this.escapeHtml(message.text)}${message.edited ? '<span class="message-edited">(edited)</span>' : ''}`;
                    }
                }
            },

            removeMessageDisplay(messageId) {
                const messageDiv = document.getElementById(`msg-${messageId}`);
                if (messageDiv) messageDiv.remove();
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

            async markViewOnceAsViewed(messageId) {
                const messageRef = database.ref(`messages/${messageId}`);
                const message = (await messageRef.once('value')).val();
                
                if (message.viewOnce && (!message.viewedBy || !message.viewedBy.includes(this.currentUserId))) {
                    const viewedBy = message.viewedBy || [];
                    viewedBy.push(this.currentUserId);
                    await messageRef.update({ viewedBy: viewedBy });
                    
                    // Remove from UI
                    const messageDiv = document.getElementById(`msg-${messageId}`);
                    if (messageDiv) messageDiv.remove();
                }
            },

            // ============ FILE UPLOAD ============
            openFileUploadModal() {
                document.getElementById('fileUploadModal').classList.add('active');
            },

            closeFileUploadModal() {
                document.getElementById('fileUploadModal').classList.remove('active');
            },

            toggleViewOnce() {
                this.viewOnceMode = !this.viewOnceMode;
                const toggle = document.getElementById('viewOnceToggle');
                if (this.viewOnceMode) {
                    toggle.classList.add('active');
                } else {
                    toggle.classList.remove('active');
                }
            },

            async uploadImage() {
                const input = document.createElement('input');
                input.type = 'file';
                input.accept = 'image/*';
                input.onchange = async (e) => {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    this.showUploadingIndicator();
                    
                    try {
                        const storageRef = storage.ref(`uploads/${Date.now()}_${file.name}`);
                        await storageRef.put(file);
                        const url = await storageRef.getDownloadURL();
                        
                        this.pendingFile = {
                            url: url,
                            type: 'image',
                            name: file.name
                        };
                        
                        this.closeFileUploadModal();
                        this.sendMessage();
                    } catch (error) {
                        console.error('Upload error:', error);
                        alert('Upload failed: ' + error.message);
                    } finally {
                        this.hideUploadingIndicator();
                    }
                };
                input.click();
            },

            async uploadVideo() {
                const input = document.createElement('input');
                input.type = 'file';
                input.accept = 'video/*';
                input.onchange = async (e) => {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    this.showUploadingIndicator();
                    
                    try {
                        const storageRef = storage.ref(`uploads/${Date.now()}_${file.name}`);
                        await storageRef.put(file);
                        const url = await storageRef.getDownloadURL();
                        
                        this.pendingFile = {
                            url: url,
                            type: 'video',
                            name: file.name
                        };
                        
                        this.closeFileUploadModal();
                        this.sendMessage();
                    } catch (error) {
                        console.error('Upload error:', error);
                        alert('Upload failed: ' + error.message);
                    } finally {
                        this.hideUploadingIndicator();
                    }
                };
                input.click();
            },

            async uploadDocument() {
                const input = document.createElement('input');
                input.type = 'file';
                input.accept = '.pdf,.doc,.docx,.txt,.xls,.xlsx';
                input.onchange = async (e) => {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    this.showUploadingIndicator();
                    
                    try {
                        const storageRef = storage.ref(`uploads/${Date.now()}_${file.name}`);
                        await storageRef.put(file);
                        const url = await storageRef.getDownloadURL();
                        
                        this.pendingFile = {
                            url: url,
                            type: 'document',
                            name: file.name
                        };
                        
                        this.closeFileUploadModal();
                        this.sendMessage();
                    } catch (error) {
                        console.error('Upload error:', error);
                        alert('Upload failed: ' + error.message);
                    } finally {
                        this.hideUploadingIndicator();
                    }
                };
                input.click();
            },

            showUploadingIndicator() {
                const sendBtn = document.querySelector('.send-btn');
                sendBtn.innerHTML = '<span class="spinner"></span> Uploading...';
                sendBtn.disabled = true;
            },

            hideUploadingIndicator() {
                const sendBtn = document.querySelector('.send-btn');
                sendBtn.innerHTML = 'Send';
                sendBtn.disabled = false;
            },

            // ============ EDIT & DELETE MESSAGES ============
            openEditMessage(messageId, currentText) {
                this.currentEditMessageId = messageId;
                document.getElementById('editInput').value = currentText;
                document.getElementById('editModal').classList.add('active');
            },

            closeEditModal() {
                document.getElementById('editModal').classList.remove('active');
                this.currentEditMessageId = null;
            },

            async saveEditedMessage() {
                const newText = document.getElementById('editInput').value.trim();
                if (!newText || !this.currentEditMessageId) return;
                
                await database.ref(`messages/${this.currentEditMessageId}`).update({
                    text: newText,
                    edited: true,
                    editedAt: firebase.database.ServerValue.TIMESTAMP
                });
                
                this.closeEditModal();
            },

            openDeleteOptions(messageId) {
                this.currentDeleteMessageId = messageId;
                document.getElementById('deleteModal').classList.add('active');
            },

            closeDeleteModal() {
                document.getElementById('deleteModal').classList.remove('active');
                this.currentDeleteMessageId = null;
            },

            async deleteMessageForMe() {
                if (!this.currentDeleteMessageId) return;
                
                // Hide message from UI only (soft delete for user)
                const messageDiv = document.getElementById(`msg-${this.currentDeleteMessageId}`);
                if (messageDiv) messageDiv.remove();
                
                this.closeDeleteModal();
            },

            async deleteMessageForEveryone() {
                if (!this.currentDeleteMessageId) return;
                
                await database.ref(`messages/${this.currentDeleteMessageId}`).remove();
                this.closeDeleteModal();
            },

            // ============ SELECT & DELETE CHAT HISTORY ============
            toggleSelectionMode() {
                this.selectionMode = !this.selectionMode;
                const container = document.getElementById('messagesArea');
                const selectionBar = document.getElementById('selectionBar');
                
                if (this.selectionMode) {
                    container.classList.add('selection-mode');
                    selectionBar.classList.add('active');
                } else {
                    container.classList.remove('selection-mode');
                    selectionBar.classList.remove('active');
                    this.selectedMessages.clear();
                }
            },

            toggleMessageSelection(messageId) {
                if (!this.selectionMode) return;
                
                const messageDiv = document.getElementById(`msg-${messageId}`);
                if (this.selectedMessages.has(messageId)) {
                    this.selectedMessages.delete(messageId);
                    messageDiv.classList.remove('selected');
                } else {
                    this.selectedMessages.add(messageId);
                    messageDiv.classList.add('selected');
                }
                
                document.getElementById('selectedCount').innerText = `${this.selectedMessages.size} selected`;
            },

            async deleteSelectedMessages() {
                if (this.selectedMessages.size === 0) return;
                
                if (confirm(`Delete ${this.selectedMessages.size} messages?`)) {
                    const deletePromises = [];
                    this.selectedMessages.forEach(messageId => {
                        deletePromises.push(database.ref(`messages/${messageId}`).remove());
                    });
                    
                    await Promise.all(deletePromises);
                    this.cancelSelection();
                }
            },

            async clearAllMessages() {
                if (confirm('Delete ALL messages in this chat? This cannot be undone!')) {
                    const messagesRef = database.ref('messages');
                    const snapshot = await messagesRef.orderByChild('groupId').equalTo(this.currentGroup).once('value');
                    const messages = snapshot.val();
                    
                    if (messages) {
                        const deletePromises = [];
                        Object.keys(messages).forEach(messageId => {
                            deletePromises.push(database.ref(`messages/${messageId}`).remove());
                        });
                        await Promise.all(deletePromises);
                    }
                }
            },

            cancelSelection() {
                this.selectionMode = false;
                this.selectedMessages.clear();
                document.getElementById('messagesArea').classList.remove('selection-mode');
                document.getElementById('selectionBar').classList.remove('active');
            },

            // ============ REACTIONS ============
            async addReaction(messageId, reaction) {
                const reactionRef = database.ref(`reactions/${messageId}/${reaction}`);
                const users = (await reactionRef.once('value')).val() || [];
                
                if (!users.includes(this.currentUserId)) {
                    users.push(this.currentUserId);
                    await reactionRef.set(users);
                }
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
                            reactionSpan.onclick = () => this.addReaction(messageId, emoji);
                            container.appendChild(reactionSpan);
                        });
                    }
                    
                    // Add reaction button
                    const addBtn = document.createElement('span');
                    addBtn.className = 'reaction';
                    addBtn.innerHTML = '+';
                    addBtn.onclick = () => this.showQuickReactions(messageId);
                    container.appendChild(addBtn);
                });
            },

            showQuickReactions(messageId) {
                const reactions = ['👍', '❤️', '😂', '😮', '😢', '😡'];
                const picker = document.getElementById('reactionPicker');
                if (!picker) {
                    const div = document.createElement('div');
                    div.id = 'reactionPicker';
                    div.className = 'reaction-picker hidden';
                    document.body.appendChild(div);
                }
                
                const pickerDiv = document.getElementById('reactionPicker');
                pickerDiv.innerHTML = '';
                reactions.forEach(reaction => {
                    const span = document.createElement('span');
                    span.className = 'reaction-option';
                    span.innerText = reaction;
                    span.onclick = () => {
                        this.addReaction(messageId, reaction);
                        pickerDiv.classList.add('hidden');
                    };
                    pickerDiv.appendChild(span);
                });
                
                pickerDiv.classList.remove('hidden');
                setTimeout(() => {
                    document.addEventListener('click', () => {
                        pickerDiv.classList.add('hidden');
                    }, { once: true });
                }, 100);
            },

            // ============ TYPING INDICATOR ============
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

            // ============ EMOJI PICKER ============
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

            // ============ UTILITY FUNCTIONS ============
            handleKeyPress(event) {
                if (event.key === 'Enter' && !event.shiftKey) {
                    event.preventDefault();
                    this.sendMessage();
                }
            },

            showImage(url, messageId) {
                const modal = document.getElementById('imageModal');
                document.getElementById('modalImage').src = url;
                modal.classList.add('active');
                
                // For view-once images, mark as viewed
                if (messageId) {
                    this.markViewOnceAsViewed(messageId);
                }
            },

            scrollToBottom() {
                const container = document.getElementById('messagesArea');
                setTimeout(() => container.scrollTop = container.scrollHeight, 100);
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
        document.querySelectorAll('.avatar-option').forEach(avatar => {
            avatar.onclick = () => {
                document.querySelectorAll('.avatar-option').forEach(a => a.classList.remove('selected'));
                avatar.classList.add('selected');
            };
        });
        document.querySelector('.avatar-option').classList.add('selected');

        // Close modals on outside click
        document.getElementById('fileUploadModal').onclick = (e) => {
            if (e.target === document.getElementById('fileUploadModal')) {
                app.closeFileUploadModal();
            }
        };
        
        document.getElementById('editModal').onclick = (e) => {
            if (e.target === document.getElementById('editModal')) {
                app.closeEditModal();
            }
        };
        
        document.getElementById('deleteModal').onclick = (e) => {
            if (e.target === document.getElementById('deleteModal')) {
                app.closeDeleteModal();
            }
        };

        // Make message selection work
        document.getElementById('messagesArea').addEventListener('click', (e) => {
            if (app.selectionMode) {
                const messageDiv = e.target.closest('.message');
                if (messageDiv && messageDiv.dataset.messageId) {
                    app.toggleMessageSelection(messageDiv.dataset.messageId);
                }
            }
        });
    </script>
</body>
</html>
