<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>ChatPro - Advanced Real-time Messenger with Cloudinary</title>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-database-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-auth-compat.js"></script>
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
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
            font-family: 'Inter', sans-serif;
        }

        .login-input:focus {
            outline: none;
            background: #2F3E48;
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
            font-family: 'Inter', sans-serif;
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
            align-items: center;
            gap: 12px;
            position: relative;
        }

        .profile-photo {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: #25D366;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        .profile-photo img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .profile-photo input {
            position: absolute;
            opacity: 0;
            cursor: pointer;
            width: 100%;
            height: 100%;
        }

        .user-info {
            flex: 1;
        }

        .user-name {
            color: white;
            font-weight: 600;
            font-size: 16px;
        }

        .user-status {
            color: #8696A0;
            font-size: 12px;
        }

        .logout-btn {
            background: none;
            border: none;
            font-size: 20px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: background 0.2s;
            color: #8696A0;
        }

        .logout-btn:hover {
            background: #2A3942;
            color: #e74c3c;
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
            font-family: 'Inter', sans-serif;
        }

        .chats-list {
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

        .chat-item {
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

        .chat-item:hover {
            background: #202C33;
        }

        .chat-item.active {
            background: #2A3942;
        }

        .chat-avatar {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: #2A3942;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            position: relative;
        }

        .chat-avatar img {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
        }

        .online-indicator {
            position: absolute;
            bottom: 2px;
            right: 2px;
            width: 12px;
            height: 12px;
            background: #25D366;
            border-radius: 50%;
            border: 2px solid #111B21;
        }

        .chat-info {
            flex: 1;
            min-width: 0;
        }

        .chat-name {
            font-weight: 500;
            font-size: 15px;
        }

        .chat-last-message {
            font-size: 12px;
            color: #8696A0;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
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
            align-items: center;
            gap: 15px;
        }

        .chat-header-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #2A3942;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
        }

        .chat-header-avatar img {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
        }

        .chat-header-info {
            flex: 1;
        }

        .chat-header-name {
            color: white;
            font-weight: 600;
            font-size: 16px;
        }

        .chat-header-status {
            color: #8696A0;
            font-size: 12px;
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

        .chat-action-btn.delete-mode {
            background: #e74c3c;
            color: white;
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

        /* Message Bubbles */
        .message {
            max-width: 70%;
            padding: 8px 12px;
            border-radius: 16px;
            position: relative;
            animation: fadeIn 0.3s ease;
            transition: all 0.2s;
        }

        .message.selection-mode {
            cursor: pointer;
        }

        .message.selection-mode.selected {
            opacity: 0.6;
            border: 2px solid #25D366;
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
            font-weight: 600;
        }

        .message-text {
            font-size: 14px;
            word-wrap: break-word;
            line-height: 1.4;
        }

        .message-media {
            max-width: 200px;
            max-height: 200px;
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

        /* Selection Bar */
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
            font-family: 'Inter', sans-serif;
            font-weight: 500;
            margin-left: 8px;
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
            border-top: 1px solid #2A3942;
        }

        .input-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: all 0.2s;
            color: #8696A0;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
        }

        .input-btn:hover {
            background: #2A3942;
            color: #25D366;
        }

        .message-input {
            flex: 1;
            padding: 12px 16px;
            background: #2A3942;
            border: none;
            border-radius: 24px;
            color: white;
            font-size: 14px;
            resize: none;
            font-family: 'Inter', sans-serif;
            max-height: 100px;
        }

        .message-input:focus {
            outline: none;
        }

        .send-btn {
            padding: 10px 24px;
            background: #25D366;
            border: none;
            border-radius: 24px;
            color: white;
            font-weight: 600;
            cursor: pointer;
            font-family: 'Inter', sans-serif;
            transition: all 0.2s;
            min-width: 80px;
        }

        .send-btn:hover {
            background: #1da15a;
            transform: scale(1.02);
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
            transition: background 0.2s;
            color: white;
            text-align: center;
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

        /* Delete Options Modal */
        .delete-modal {
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

        .delete-modal.active {
            display: flex;
        }

        .delete-modal-content {
            background: #111B21;
            border-radius: 20px;
            padding: 24px;
            width: 90%;
            max-width: 350px;
        }

        .delete-modal-content h3 {
            color: white;
            margin-bottom: 20px;
            font-weight: 600;
        }

        .delete-option {
            background: #202C33;
            padding: 15px;
            margin: 10px 0;
            border-radius: 12px;
            cursor: pointer;
            transition: background 0.2s;
            color: white;
            text-align: center;
        }

        .delete-option:hover {
            background: #2A3942;
        }

        .delete-option.danger {
            color: #e74c3c;
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

        /* Toast Notification */
        .toast {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%);
            background: #e74c3c;
            color: white;
            padding: 12px 24px;
            border-radius: 8px;
            font-size: 14px;
            z-index: 1100;
            animation: slideUp 0.3s ease;
        }

        .toast.success {
            background: #25D366;
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

        /* Upload Progress */
        .upload-progress {
            position: fixed;
            bottom: 100px;
            right: 20px;
            background: #202C33;
            padding: 12px 20px;
            border-radius: 24px;
            display: flex;
            align-items: center;
            gap: 12px;
            color: white;
            font-size: 14px;
            z-index: 100;
            box-shadow: 0 2px 10px rgba(0,0,0,0.3);
        }

        .upload-progress.hidden {
            display: none;
        }

        .progress-bar {
            width: 150px;
            height: 6px;
            background: #2A3942;
            border-radius: 3px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: #25D366;
            width: 0%;
            transition: width 0.3s;
            border-radius: 3px;
        }

        /* Profile Photo Upload Overlay */
        .profile-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.6);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            opacity: 0;
            transition: opacity 0.2s;
            cursor: pointer;
        }

        .profile-photo:hover .profile-overlay {
            opacity: 1;
        }

        .profile-overlay span {
            color: white;
            font-size: 20px;
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

        /* Tablet Responsive */
        @media (min-width: 769px) and (max-width: 1024px) {
            .sidebar {
                width: 280px;
            }
            
            .message {
                max-width: 75%;
            }
        }

        /* Desktop */
        @media (min-width: 1025px) {
            .sidebar {
                width: 350px;
            }
        }

        .menu-toggle {
            display: none;
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            margin-right: 15px;
            color: white;
        }

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
            <h1>ChatPro</h1>
            <p>Advanced Real-time Messenger with Cloudinary</p>
            <input type="text" id="userName" class="login-input" placeholder="Enter your name" maxlength="25">
            <button class="login-btn" onclick="app.login()">Start Chatting →</button>
        </div>
    </div>

    <!-- Main Chat Interface -->
    <div id="chatContainer" class="chat-container">
        <div class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <div class="profile-photo" id="profilePhoto">
                    <div class="profile-avatar" style="font-size: 32px;">😀</div>
                    <input type="file" id="profilePhotoInput" accept="image/*" style="display:none">
                    <div class="profile-overlay" onclick="app.uploadProfilePhoto()">
                        <span>📷</span>
                    </div>
                </div>
                <div class="user-info">
                    <div class="user-name" id="userDisplayName">User</div>
                    <div class="user-status" id="userStatus">Online</div>
                </div>
                <button class="logout-btn" onclick="app.logout()" title="Logout">🚪</button>
            </div>
            <div class="search-box">
                <input type="text" id="searchUsers" placeholder="Search users..." oninput="app.searchUsers(this.value)">
            </div>
            <div class="chats-list">
                <div class="section-title">CHATS</div>
                <div id="chatsList"></div>
            </div>
        </div>

        <div class="chat-area">
            <div class="chat-header">
                <button class="menu-toggle" onclick="app.toggleSidebar()">☰</button>
                <div class="chat-header-avatar" id="chatHeaderAvatar">💬</div>
                <div class="chat-header-info">
                    <div class="chat-header-name" id="chatHeaderName">Select a chat</div>
                    <div class="chat-header-status" id="chatHeaderStatus"></div>
                </div>
                <div class="chat-actions">
                    <button class="chat-action-btn" id="deleteModeBtn" onclick="app.toggleDeleteMode()" title="Select Messages">☑️</button>
                    <button class="chat-action-btn" onclick="app.openFileUploadModal()" title="Upload File">📎</button>
                </div>
            </div>

            <!-- Selection Bar -->
            <div id="selectionBar" class="selection-bar">
                <span id="selectedCount">0 selected</span>
                <div>
                    <button onclick="app.deleteSelectedMessages()">Delete Selected</button>
                    <button onclick="app.cancelDeleteMode()">Cancel</button>
                </div>
            </div>

            <div class="messages-area" id="messagesArea"></div>

            <div class="typing-indicator hidden" id="typingIndicator">
                <span>Someone is typing</span>
                <span class="typing-dots"></span>
            </div>

            <div class="input-area">
                <button class="input-btn" onclick="app.openEmojiPicker()">😊</button>
                <textarea id="messageInput" class="message-input" placeholder="Type a message..." rows="1" onkeypress="app.handleKeyPress(event)"></textarea>
                <button class="send-btn" onclick="app.sendMessage()" id="sendButton">Send →</button>
            </div>
        </div>
    </div>

    <!-- File Upload Modal -->
    <div id="fileUploadModal" class="modal">
        <div class="modal-content">
            <h3>Upload to Cloudinary</h3>
            <div class="file-option" onclick="app.uploadImage()">
                📷 Upload Image
            </div>
            <div class="file-option" onclick="app.uploadVideo()">
                🎥 Upload Video
            </div>
            <div class="file-option" onclick="app.uploadFile()">
                📄 Upload Document
            </div>
            <div class="view-once-toggle">
                <span>View Once Mode</span>
                <div id="viewOnceToggle" class="toggle-switch" onclick="app.toggleViewOnce()"></div>
            </div>
            <button class="file-option" onclick="app.closeFileUploadModal()" style="background:#2A3942;">Cancel</button>
        </div>
    </div>

    <!-- Delete Options Modal -->
    <div id="deleteModal" class="delete-modal">
        <div class="delete-modal-content">
            <h3>Delete Message</h3>
            <div class="delete-option" onclick="app.deleteForMe()">
                🔒 Delete for me
            </div>
            <div class="delete-option danger" onclick="app.deleteForEveryone()">
                🌐 Delete for everyone
            </div>
            <div class="delete-option" onclick="app.closeDeleteModal()">
                Cancel
            </div>
        </div>
    </div>

    <!-- Emoji Picker -->
    <div id="emojiPicker" class="emoji-picker hidden"></div>

    <!-- Image Modal -->
    <div id="imageModal" class="image-modal" onclick="this.classList.remove('active')">
        <img id="modalImage" src="">
    </div>

    <!-- Upload Progress -->
    <div id="uploadProgress" class="upload-progress hidden">
        <span>📤 Uploading to Cloudinary...</span>
        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
        </div>
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

        // ============ CLOUDINARY CONFIGURATION ============
        // REPLACE WITH YOUR CLOUDINARY DETAILS!
        const CLOUDINARY_CONFIG = {
            cloudName: "duebhhrk9",  // Get from Cloudinary Dashboard
            uploadPreset: "chat_uploads",   // Create in Cloudinary Settings → Upload
            maxFileSize: {
                image: 10 * 1024 * 1024,    // 10MB
                video: 100 * 1024 * 1024,   // 100MB
                document: 20 * 1024 * 1024  // 20MB
            }
        };

        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);
        const database = firebase.database();
        const auth = firebase.auth();

        // ============ MAIN APPLICATION ============
        const app = {
            // User Data
            currentUser: null,
            currentUserId: null,
            currentChat: null,
            currentChatType: 'group',
            
            // UI State
            typingTimeout: null,
            isTyping: false,
            deleteMode: false,
            selectedMessages: new Set(),
            currentDeleteMessageId: null,
            viewOnceMode: false,
            
            // File Upload
            pendingFile: null,

            // ============ AUTHENTICATION ============
            async login() {
                const userName = document.getElementById('userName').value.trim();
                if (!userName) {
                    app.showToast('Please enter your name');
                    return;
                }

                try {
                    const userCredential = await auth.signInAnonymously();
                    this.currentUserId = userCredential.user.uid;
                    this.currentUser = userName;

                    await database.ref('users/' + this.currentUserId).set({
                        name: this.currentUser,
                        avatar: this.getRandomAvatar(),
                        online: true,
                        lastSeen: firebase.database.ServerValue.TIMESTAMP
                    });

                    document.getElementById('loginScreen').style.display = 'none';
                    document.getElementById('chatContainer').classList.add('active');
                    document.getElementById('userDisplayName').innerText = this.currentUser;

                    this.loadChats();
                    this.loadOnlineStatus();
                    this.setupTypingIndicator();
                    
                    this.currentChat = 'general';
                    this.currentChatType = 'group';
                    document.getElementById('chatHeaderName').innerText = 'General Chat';
                    document.getElementById('chatHeaderAvatar').innerHTML = '💬';
                    this.loadMessages();
                    
                    window.addEventListener('beforeunload', () => {
                        database.ref('users/' + this.currentUserId).update({
                            online: false,
                            lastSeen: firebase.database.ServerValue.TIMESTAMP
                        });
                    });

                } catch (error) {
                    console.error('Login error:', error);
                    app.showToast('Login failed: ' + error.message);
                }
            },

            getRandomAvatar() {
                const avatars = ['😀', '😎', '🥰', '🤓', '👨‍💻', '👩‍💻', '🐱', '⭐'];
                return avatars[Math.floor(Math.random() * avatars.length)];
            },

            // ============ PROFILE PHOTO (Cloudinary) ============
            async uploadProfilePhoto() {
                const input = document.getElementById('profilePhotoInput');
                input.click();
                input.onchange = async (e) => {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    if (!file.type.startsWith('image/')) {
                        app.showToast('Please select an image file');
                        return;
                    }
                    
                    app.showUploadProgress();
                    
                    try {
                        const result = await this.uploadToCloudinary(file, 'image', 'profile_photos');
                        
                        await database.ref('users/' + this.currentUserId).update({
                            photoUrl: result.url
                        });
                        
                        this.updateProfilePhotoDisplay(result.url);
                        app.hideUploadProgress();
                        app.showToast('Profile photo updated!', 'success');
                    } catch (error) {
                        app.hideUploadProgress();
                        app.showToast('Upload failed: ' + error.message);
                    }
                };
            },

            updateProfilePhotoDisplay(photoUrl) {
                const profileDiv = document.getElementById('profilePhoto');
                profileDiv.innerHTML = `
                    <img src="${photoUrl}" style="width:100%; height:100%; border-radius:50%; object-fit:cover;">
                    <input type="file" id="profilePhotoInput" accept="image/*" style="display:none">
                    <div class="profile-overlay" onclick="app.uploadProfilePhoto()">
                        <span>📷</span>
                    </div>
                `;
            },

            // ============ CLOUDINARY UPLOAD FUNCTION ============
            async uploadToCloudinary(file, type, folder = 'chat_media') {
                const formData = new FormData();
                formData.append('file', file);
                formData.append('upload_preset', CLOUDINARY_CONFIG.uploadPreset);
                
                let uploadUrl = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CONFIG.cloudName}/auto/upload`;
                
                if (type === 'video') {
                    uploadUrl = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CONFIG.cloudName}/video/upload`;
                } else if (type === 'raw' || type === 'document') {
                    uploadUrl = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CONFIG.cloudName}/raw/upload`;
                }
                
                // Add folder parameter
                formData.append('folder', folder);
                
                return new Promise((resolve, reject) => {
                    const xhr = new XMLHttpRequest();
                    
                    xhr.upload.addEventListener('progress', (e) => {
                        if (e.lengthComputable) {
                            const progress = (e.loaded / e.total) * 100;
                            app.updateUploadProgress(progress);
                        }
                    });
                    
                    xhr.onload = () => {
                        if (xhr.status === 200) {
                            const response = JSON.parse(xhr.responseText);
                            resolve({
                                url: response.secure_url,
                                publicId: response.public_id,
                                type: type,
                                name: file.name
                            });
                        } else {
                            reject(new Error('Upload failed with status: ' + xhr.status));
                        }
                    };
                    
                    xhr.onerror = () => reject(new Error('Network error during upload'));
                    
                    xhr.open('POST', uploadUrl);
                    xhr.send(formData);
                });
            },

            // ============ FILE UPLOAD METHODS ============
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
                    
                    if (file.size > CLOUDINARY_CONFIG.maxFileSize.image) {
                        app.showToast('Image too large! Max 10MB');
                        return;
                    }
                    
                    app.showUploadProgress();
                    app.updateUploadProgress(0);
                    
                    try {
                        const result = await this.uploadToCloudinary(file, 'image');
                        this.pendingFile = result;
                        app.hideUploadProgress();
                        this.closeFileUploadModal();
                        await this.sendMessage();
                    } catch (error) {
                        app.hideUploadProgress();
                        app.showToast('Upload failed: ' + error.message);
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
                    
                    if (file.size > CLOUDINARY_CONFIG.maxFileSize.video) {
                        app.showToast('Video too large! Max 100MB');
                        return;
                    }
                    
                    app.showUploadProgress();
                    app.updateUploadProgress(0);
                    
                    try {
                        const result = await this.uploadToCloudinary(file, 'video');
                        this.pendingFile = result;
                        app.hideUploadProgress();
                        this.closeFileUploadModal();
                        await this.sendMessage();
                    } catch (error) {
                        app.hideUploadProgress();
                        app.showToast('Upload failed: ' + error.message);
                    }
                };
                input.click();
            },

            async uploadFile() {
                const input = document.createElement('input');
                input.type = 'file';
                input.accept = '.pdf,.doc,.docx,.txt,.xls,.xlsx,.ppt,.pptx,.zip,.rar';
                input.onchange = async (e) => {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    if (file.size > CLOUDINARY_CONFIG.maxFileSize.document) {
                        app.showToast('File too large! Max 20MB');
                        return;
                    }
                    
                    app.showUploadProgress();
                    app.updateUploadProgress(0);
                    
                    try {
                        const result = await this.uploadToCloudinary(file, 'document');
                        this.pendingFile = result;
                        app.hideUploadProgress();
                        this.closeFileUploadModal();
                        await this.sendMessage();
                    } catch (error) {
                        app.hideUploadProgress();
                        app.showToast('Upload failed: ' + error.message);
                    }
                };
                input.click();
            },

            showUploadProgress() {
                const progressDiv = document.getElementById('uploadProgress');
                progressDiv.classList.remove('hidden');
            },

            updateUploadProgress(progress) {
                const fill = document.getElementById('progressFill');
                fill.style.width = `${progress}%`;
            },

            hideUploadProgress() {
                const progressDiv = document.getElementById('uploadProgress');
                progressDiv.classList.add('hidden');
                const fill = document.getElementById('progressFill');
                fill.style.width = '0%';
            },

            // ============ CHATS LIST ============
            async loadChats() {
                database.ref('users').on('value', (snapshot) => {
                    const users = snapshot.val();
                    const chatsList = document.getElementById('chatsList');
                    chatsList.innerHTML = '';
                    
                    const generalChat = document.createElement('div');
                    generalChat.className = `chat-item ${this.currentChat === 'general' && this.currentChatType === 'group' ? 'active' : ''}`;
                    generalChat.innerHTML = `
                        <div class="chat-avatar">💬</div>
                        <div class="chat-info">
                            <div class="chat-name">General Chat</div>
                            <div class="chat-last-message">Group conversation</div>
                        </div>
                    `;
                    generalChat.onclick = () => this.openGroupChat();
                    chatsList.appendChild(generalChat);
                    
                    Object.entries(users).forEach(([id, user]) => {
                        if (id !== this.currentUserId) {
                            const chatDiv = document.createElement('div');
                            chatDiv.className = `chat-item ${this.currentChat === id && this.currentChatType === 'private' ? 'active' : ''}`;
                            chatDiv.innerHTML = `
                                <div class="chat-avatar">
                                    ${user.photoUrl ? `<img src="${user.photoUrl}">` : `<span>${user.avatar || '😀'}</span>`}
                                    ${user.online ? '<div class="online-indicator"></div>' : ''}
                                </div>
                                <div class="chat-info">
                                    <div class="chat-name">${this.escapeHtml(user.name)}</div>
                                    <div class="chat-last-message">${user.online ? 'Online' : 'Offline'}</div>
                                </div>
                            `;
                            chatDiv.onclick = () => this.openPrivateChat(id, user);
                            chatsList.appendChild(chatDiv);
                        }
                    });
                });
            },

            openGroupChat() {
                this.currentChat = 'general';
                this.currentChatType = 'group';
                document.getElementById('chatHeaderName').innerText = 'General Chat';
                document.getElementById('chatHeaderAvatar').innerHTML = '💬';
                document.getElementById('chatHeaderStatus').innerText = '';
                document.getElementById('messagesArea').innerHTML = '';
                this.cancelDeleteMode();
                this.loadMessages();
                
                document.querySelectorAll('.chat-item').forEach(item => {
                    item.classList.remove('active');
                });
            },

            openPrivateChat(userId, user) {
                this.currentChat = userId;
                this.currentChatType = 'private';
                document.getElementById('chatHeaderName').innerText = user.name;
                document.getElementById('chatHeaderAvatar').innerHTML = user.photoUrl ? 
                    `<img src="${user.photoUrl}" style="width:100%; height:100%; border-radius:50%; object-fit:cover;">` : 
                    (user.avatar || '😀');
                document.getElementById('chatHeaderStatus').innerText = user.online ? 'Online' : 'Offline';
                document.getElementById('messagesArea').innerHTML = '';
                this.cancelDeleteMode();
                this.loadMessages();
                
                document.querySelectorAll('.chat-item').forEach(item => {
                    item.classList.remove('active');
                });
            },

            loadOnlineStatus() {
                database.ref('users').on('value', (snapshot) => {
                    const users = snapshot.val();
                    if (this.currentChatType === 'private' && users[this.currentChat]) {
                        const user = users[this.currentChat];
                        document.getElementById('chatHeaderStatus').innerText = user?.online ? 'Online' : 'Offline';
                    }
                });
            },

            // ============ MESSAGE FUNCTIONS ============
            async sendMessage() {
                const input = document.getElementById('messageInput');
                const text = input.value.trim();
                
                if (!text && !this.pendingFile) return;

                const sendBtn = document.getElementById('sendButton');
                sendBtn.disabled = true;

                this.clearTyping();

                const message = {
                    userId: this.currentUserId,
                    userName: this.currentUser,
                    chatType: this.currentChatType,
                    chatId: this.currentChat,
                    timestamp: firebase.database.ServerValue.TIMESTAMP,
                    readBy: { [this.currentUserId]: true },
                    delivered: true
                };

                if (text) {
                    message.text = text;
                    input.value = '';
                    input.style.height = 'auto';
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

                try {
                    const messageRef = database.ref('messages').push();
                    await messageRef.set(message);
                    this.scrollToBottom();
                } catch (error) {
                    console.error('Send error:', error);
                    app.showToast('Failed to send message');
                } finally {
                    sendBtn.disabled = false;
                }
            },

            loadMessages() {
                const messagesRef = database.ref('messages');
                let query;
                
                if (this.currentChatType === 'group') {
                    query = messagesRef.orderByChild('chatId').equalTo('general');
                } else {
                    query = messagesRef.orderByChild('chatId').equalTo(this.currentChat);
                }
                
                query.on('child_added', (snapshot) => {
                    const message = snapshot.val();
                    if ((this.currentChatType === 'group' && message.chatId === 'general') ||
                        (this.currentChatType === 'private' && message.chatId === this.currentChat)) {
                        this.displayMessage(message, snapshot.key);
                    }
                });
            },

            displayMessage(message, messageId) {
                const container = document.getElementById('messagesArea');
                const isSent = message.userId === this.currentUserId;
                const isViewOnce = message.viewOnce === true;
                const isViewed = isViewOnce && message.viewedBy && message.viewedBy.includes(this.currentUserId);
                
                if (isViewOnce && isViewed && !isSent) return;
                
                const messageDiv = document.createElement('div');
                messageDiv.className = `message ${isSent ? 'sent' : 'received'}`;
                messageDiv.id = `msg-${messageId}`;
                messageDiv.dataset.messageId = messageId;
                
                if (this.deleteMode) {
                    messageDiv.classList.add('selection-mode');
                }
                
                let content = '';
                
                if (!isSent && this.currentChatType === 'group') {
                    content += `<div class="message-sender">${this.escapeHtml(message.userName)}</div>`;
                }
                
                if (message.text) {
                    content += `<div class="message-text">${this.escapeHtml(message.text)}</div>`;
                }
                
                if (message.fileUrl) {
                    if (message.fileType === 'image') {
                        content += `<img src="${message.fileUrl}" class="message-media" onclick="app.showImage('${message.fileUrl}')" loading="lazy">`;
                    } else if (message.fileType === 'video') {
                        content += `<video src="${message.fileUrl}" controls class="message-media" preload="metadata"></video>`;
                    } else {
                        content += `<a href="${message.fileUrl}" download class="message-media" style="display:block; padding:10px; background:#2A3942; border-radius:8px; text-decoration:none; color:#25D366;">📄 ${this.escapeHtml(message.fileName)}</a>`;
                    }
                }
                
                const time = new Date(message.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                
                content += `
                    <div class="message-time">
                        ${time}
                        ${isSent ? `<span class="read-status">${message.seen ? '✓✓' : (message.delivered ? '✓✓' : '✓')}</span>` : ''}
                    </div>
                `;
                
                // Add delete button for sent messages
                if (isSent) {
                    content += `<div style="position:absolute; right:-30px; top:0;" onclick="app.openDeleteOptions('${messageId}')">🗑️</div>`;
                }
                
                messageDiv.innerHTML = content;
                
                if (this.deleteMode) {
                    messageDiv.onclick = (e) => {
                        e.stopPropagation();
                        this.toggleMessageSelection(messageId);
                    };
                }
                
                container.appendChild(messageDiv);
                
                if (!isSent && !message.seen) {
                    this.markAsRead(messageId);
                }
                
                // Auto-mark view-once messages as viewed
                if (isViewOnce && !isViewed && !isSent) {
                    setTimeout(() => {
                        this.markViewOnceAsViewed(messageId);
                    }, 5000);
                }
                
                this.scrollToBottom();
            },

            async markAsRead(messageId) {
                try {
                    const messageRef = database.ref(`messages/${messageId}`);
                    const message = (await messageRef.once('value')).val();
                    
                    if (!message.seen && message.userId !== this.currentUserId) {
                        await messageRef.update({
                            seen: true,
                            seenAt: firebase.database.ServerValue.TIMESTAMP
                        });
                    }
                } catch (error) {
                    console.error('Mark as read error:', error);
                }
            },

            async markViewOnceAsViewed(messageId) {
                try {
                    const messageRef = database.ref(`messages/${messageId}`);
                    const message = (await messageRef.once('value')).val();
                    
                    if (message.viewOnce && (!message.viewedBy || !message.viewedBy.includes(this.currentUserId))) {
                        const viewedBy = message.viewedBy || [];
                        viewedBy.push(this.currentUserId);
                        await messageRef.update({ viewedBy: viewedBy });
                        
                        const messageDiv = document.getElementById(`msg-${messageId}`);
                        if (messageDiv && !messageDiv.classList.contains('sent')) {
                            messageDiv.remove();
                        }
                    }
                } catch (error) {
                    console.error('Mark view-once error:', error);
                }
            },

            // ============ DELETE MESSAGES ============
            toggleDeleteMode() {
                this.deleteMode = !this.deleteMode;
                const selectionBar = document.getElementById('selectionBar');
                const deleteBtn = document.getElementById('deleteModeBtn');
                
                if (this.deleteMode) {
                    selectionBar.classList.add('active');
                    deleteBtn.classList.add('delete-mode');
                    document.querySelectorAll('.message').forEach(msg => {
                        msg.classList.add('selection-mode');
                    });
                } else {
                    selectionBar.classList.remove('active');
                    deleteBtn.classList.remove('delete-mode');
                    document.querySelectorAll('.message').forEach(msg => {
                        msg.classList.remove('selection-mode', 'selected');
                    });
                    this.selectedMessages.clear();
                }
            },

            toggleMessageSelection(messageId) {
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
                
                if (confirm(`Delete ${this.selectedMessages.size} message(s)?`)) {
                    const deletePromises = [];
                    this.selectedMessages.forEach(messageId => {
                        deletePromises.push(database.ref(`messages/${messageId}`).remove());
                    });
                    
                    await Promise.all(deletePromises);
                    app.showToast(`${this.selectedMessages.size} message(s) deleted!`, 'success');
                    this.cancelDeleteMode();
                }
            },

            openDeleteOptions(messageId) {
                this.currentDeleteMessageId = messageId;
                document.getElementById('deleteModal').classList.add('active');
            },

            closeDeleteModal() {
                document.getElementById('deleteModal').classList.remove('active');
                this.currentDeleteMessageId = null;
            },

            async deleteForMe() {
                if (!this.currentDeleteMessageId) return;
                
                const messageDiv = document.getElementById(`msg-${this.currentDeleteMessageId}`);
                if (messageDiv) messageDiv.remove();
                
                this.closeDeleteModal();
                app.showToast('Message deleted for you', 'success');
            },

            async deleteForEveryone() {
                if (!this.currentDeleteMessageId) return;
                
                await database.ref(`messages/${this.currentDeleteMessageId}`).remove();
                this.closeDeleteModal();
                app.showToast('Message deleted for everyone', 'success');
            },

            cancelDeleteMode() {
                this.deleteMode = false;
                this.selectedMessages.clear();
                document.getElementById('selectionBar').classList.remove('active');
                document.getElementById('deleteModeBtn').classList.remove('delete-mode');
                document.querySelectorAll('.message').forEach(msg => {
                    msg.classList.remove('selection-mode', 'selected');
                });
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
                            chatId: this.currentChat,
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
                    
                    if (data && data.isTyping && data.userId !== this.currentUserId && data.chatId === this.currentChat) {
                        indicator.classList.remove('hidden');
                        indicator.querySelector('span').innerHTML = `${this.escapeHtml(data.userName)} is typing`;
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

            // ============ SEARCH USERS ============
            searchUsers(query) {
                const items = document.querySelectorAll('.chat-item');
                items.forEach(item => {
                    const text = item.innerText.toLowerCase();
                    item.style.display = text.includes(query.toLowerCase()) ? 'flex' : 'none';
                });
            },

            // ============ UTILITY FUNCTIONS ============
            autoResizeTextarea() {
                const textarea = document.getElementById('messageInput');
                textarea.style.height = 'auto';
                textarea.style.height = Math.min(textarea.scrollHeight, 100) + 'px';
            },

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
                if (!text) return '';
                const div = document.createElement('div');
                div.textContent = text;
                return div.innerHTML;
            },

            toggleSidebar() {
                document.getElementById('sidebar').classList.toggle('open');
            },

            showToast(message, type = 'error') {
                const toast = document.createElement('div');
                toast.className = `toast ${type}`;
                toast.innerText = message;
                document.body.appendChild(toast);
                setTimeout(() => toast.remove(), 3000);
            },

            logout() {
                database.ref('users/' + this.currentUserId).update({
                    online: false,
                    lastSeen: firebase.database.ServerValue.TIMESTAMP
                });
                location.reload();
            }
        };

        // Auto-resize textarea
        document.getElementById('messageInput').addEventListener('input', () => app.autoResizeTextarea());

        // Close modals
        document.getElementById('fileUploadModal').onclick = (e) => {
            if (e.target === document.getElementById('fileUploadModal')) {
                app.closeFileUploadModal();
            }
        };
        
        document.getElementById('deleteModal').onclick = (e) => {
            if (e.target === document.getElementById('deleteModal')) {
                app.closeDeleteModal();
            }
        };
        
        document.getElementById('imageModal').onclick = (e) => {
            if (e.target === document.getElementById('imageModal')) {
                document.getElementById('imageModal').classList.remove('active');
            }
        };

        // Close emoji picker
        document.addEventListener('click', (e) => {
            const emojiPicker = document.getElementById('emojiPicker');
            if (emojiPicker && !emojiPicker.contains(e.target) && !e.target.classList.contains('input-btn')) {
                emojiPicker.classList.add('hidden');
            }
        });
    </script>
</body>
</html>
