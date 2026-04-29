<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Project P - Advanced WhatsApp Clone</title>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
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
            cursor: pointer;
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

        .member-count {
            color: #8696A0;
            font-size: 12px;
            margin-top: 4px;
        }

        .chat-actions {
            display: flex;
            gap: 12px;
        }

        .chat-action-btn {
            background: none;
            border: none;
            font-size: 20px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: background 0.2s;
            color: #8696A0;
        }

        .chat-action-btn:hover {
            background: #2A3942;
            color: #25D366;
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

        /* Reply Preview */
        .reply-preview {
            background: #202C33;
            padding: 8px 12px;
            margin: 5px 0;
            border-radius: 8px;
            border-left: 3px solid #25D366;
            font-size: 12px;
            color: #8696A0;
        }

        .reply-preview strong {
            color: #25D366;
        }

        .reply-preview .reply-text {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
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

        .message:hover {
            transform: scale(1.01);
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
            max-width: 250px;
            max-height: 250px;
            border-radius: 8px;
            margin-top: 4px;
            cursor: pointer;
        }

        .audio-message {
            width: 200px;
            height: 36px;
            margin-top: 4px;
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

        .read-status {
            font-size: 10px;
            cursor: pointer;
        }

        /* Message Actions */
        .message-actions {
            position: absolute;
            right: -40px;
            top: 50%;
            transform: translateY(-50%);
            display: none;
            gap: 4px;
            background: #202C33;
            padding: 4px;
            border-radius: 20px;
            z-index: 10;
        }

        .message:hover .message-actions {
            display: flex;
        }

        .msg-action-btn {
            background: none;
            border: none;
            font-size: 16px;
            cursor: pointer;
            padding: 4px 8px;
            border-radius: 50%;
            transition: background 0.2s;
            color: #8696A0;
        }

        .msg-action-btn:hover {
            background: #2A3942;
            color: #25D366;
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

        /* Reply Indicator Bar */
        .reply-bar {
            background: #202C33;
            padding: 8px 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-left: 3px solid #25D366;
            margin: 0 20px;
            border-radius: 8px;
        }

        .reply-bar.hidden {
            display: none;
        }

        .reply-info {
            flex: 1;
            font-size: 12px;
            color: #8696A0;
        }

        .reply-info strong {
            color: #25D366;
        }

        .cancel-reply {
            background: none;
            border: none;
            color: #8696A0;
            cursor: pointer;
            font-size: 18px;
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

        .input-btn.recording {
            color: #ff4444;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
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
            font-family: 'Poppins', sans-serif;
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
            font-family: 'Poppins', sans-serif;
            transition: all 0.2s;
            min-width: 80px;
        }

        .send-btn:hover {
            background: #1da15a;
            transform: scale(1.02);
        }

        .send-btn:disabled {
            background: #2A3942;
            cursor: not-allowed;
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

        /* Voice Recording */
        .voice-recording {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%);
            background: #202C33;
            padding: 15px 25px;
            border-radius: 50px;
            display: flex;
            align-items: center;
            gap: 15px;
            z-index: 100;
            box-shadow: 0 4px 20px rgba(0,0,0,0.3);
        }

        .voice-recording.hidden {
            display: none;
        }

        .recording-timer {
            color: #ff4444;
            font-weight: 600;
        }

        .recording-wave {
            display: flex;
            gap: 3px;
            align-items: center;
        }

        .recording-wave span {
            width: 3px;
            height: 20px;
            background: #25D366;
            animation: wave 0.5s infinite;
        }

        @keyframes wave {
            0%, 100% { height: 10px; }
            50% { height: 25px; }
        }

        /* Read Receipts Modal */
        .read-receipts-modal {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: #111B21;
            border-radius: 20px 20px 0 0;
            padding: 20px;
            max-height: 70vh;
            overflow-y: auto;
            z-index: 1000;
            transform: translateY(100%);
            transition: transform 0.3s;
        }

        .read-receipts-modal.active {
            transform: translateY(0);
        }

        .read-receipts-modal h3 {
            color: white;
            margin-bottom: 15px;
        }

        .read-user {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 10px;
            border-bottom: 1px solid #2A3942;
        }

        /* Search Modal */
        .search-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            background: #111B21;
            padding: 20px;
            z-index: 1000;
            transform: translateY(-100%);
            transition: transform 0.3s;
        }

        .search-modal.active {
            transform: translateY(0);
        }

        .search-modal input {
            width: 100%;
            padding: 12px;
            background: #2A3942;
            border: none;
            border-radius: 24px;
            color: white;
            font-family: 'Poppins', sans-serif;
        }

        .search-result {
            padding: 10px;
            margin: 10px 0;
            background: #202C33;
            border-radius: 12px;
            cursor: pointer;
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
            color: white;
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
            
            .message-actions {
                right: -35px;
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
            <h1>Project P</h1>
            <p>Advanced WhatsApp Clone</p>
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
                <div class="user-profile" onclick="app.showUserProfile()">
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
                    <button class="chat-action-btn" onclick="app.openSearchModal()" title="Search Messages">🔍</button>
                    <button class="chat-action-btn" onclick="app.clearAllMessages()" title="Clear All Messages">🗑️</button>
                </div>
            </div>

            <div class="messages-area" id="messagesArea"></div>

            <div class="typing-indicator hidden" id="typingIndicator">
                <span>Someone is typing</span>
                <span class="typing-dots"></span>
            </div>

            <!-- Reply Preview Bar -->
            <div id="replyBar" class="reply-bar hidden">
                <div class="reply-info">
                    Replying to <strong id="replyToName"></strong>: 
                    <span id="replyPreviewText"></span>
                </div>
                <button class="cancel-reply" onclick="app.cancelReply()">✕</button>
            </div>

            <div class="input-area">
                <button class="input-btn" onclick="app.openEmojiPicker()">😊</button>
                <button class="input-btn" onclick="app.openFileUploadModal()">📎</button>
                <button class="input-btn" id="voiceBtn" onclick="app.toggleVoiceRecording()">🎤</button>
                <textarea id="messageInput" class="message-input" placeholder="Type a message..." rows="1" onkeypress="app.handleKeyPress(event)"></textarea>
                <button class="send-btn" onclick="app.sendMessage()" id="sendButton">Send →</button>
            </div>
        </div>
    </div>

    <!-- Voice Recording UI -->
    <div id="voiceRecordingUI" class="voice-recording hidden">
        <div class="recording-wave">
            <span></span><span></span><span></span><span></span><span></span>
        </div>
        <div class="recording-timer" id="recordingTimer">0:00</div>
        <button onclick="app.stopVoiceRecording()" style="background:#ff4444; border:none; padding:8px 16px; border-radius:20px; color:white; cursor:pointer;">Stop</button>
        <button onclick="app.cancelVoiceRecording()" style="background:#2A3942; border:none; padding:8px 16px; border-radius:20px; color:white; cursor:pointer;">Cancel</button>
    </div>

    <!-- Upload Progress -->
    <div id="uploadProgress" class="upload-progress hidden">
        <span>📤 Uploading to Cloudinary...</span>
        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
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
            <div class="file-option" onclick="app.uploadDocument()">
                📄 Upload Document
            </div>
            <div class="view-once-toggle">
                <span>View Once Mode</span>
                <div id="viewOnceToggle" class="toggle-switch" onclick="app.toggleViewOnce()"></div>
            </div>
            <button class="file-option" onclick="app.closeFileUploadModal()" style="background:#2A3942; justify-content:center;">Cancel</button>
        </div>
    </div>

    <!-- Search Modal -->
    <div id="searchModal" class="search-modal">
        <input type="text" id="searchInput" placeholder="Search messages..." oninput="app.searchMessages(this.value)">
        <div id="searchResults"></div>
        <button onclick="app.closeSearchModal()" style="margin-top:10px; padding:8px; background:#2A3942; border:none; border-radius:8px; color:white; cursor:pointer;">Close</button>
    </div>

    <!-- Read Receipts Modal -->
    <div id="readReceiptsModal" class="read-receipts-modal">
        <h3>Message Info</h3>
        <div id="readReceiptsList"></div>
        <button onclick="app.closeReadReceipts()" style="margin-top:15px; padding:10px; background:#2A3942; border:none; border-radius:8px; color:white; cursor:pointer; width:100%;">Close</button>
    </div>

    <!-- Emoji Picker -->
    <div id="emojiPicker" class="emoji-picker hidden"></div>

    <!-- Image Modal -->
    <div id="imageModal" class="image-modal" onclick="this.classList.remove('active')">
        <img id="modalImage" src="">
    </div>

    <script>
        // ============ FIREBASE CONFIGURATION ============
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
        const CLOUDINARY_CONFIG = {
            cloudName: "duebhhrk9",
            uploadPreset: "chat_uploads",
            maxFileSize: {
                image: 10 * 1024 * 1024,
                video: 100 * 1024 * 1024,
                document: 20 * 1024 * 1024
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
            currentAvatar: '😀',
            currentGroup: 'general',
            
            // UI State
            typingTimeout: null,
            isTyping: false,
            viewOnceMode: false,
            
            // File Upload
            pendingFile: null,
            
            // Voice Recording
            mediaRecorder: null,
            audioChunks: [],
            recordingTimer: null,
            recordingSeconds: 0,
            
            // Reply Feature
            replyingTo: null,
            
            // Notification Permission
            notificationPermission: false,

            // ============ AUTHENTICATION ============
            async login() {
                const userName = document.getElementById('userName').value.trim();
                if (!userName) {
                    app.showToast('Please enter your name');
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
                    this.requestNotificationPermission();
                    
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

            // ============ NOTIFICATIONS ============
            requestNotificationPermission() {
                if ('Notification' in window) {
                    Notification.requestPermission().then(permission => {
                        this.notificationPermission = permission === 'granted';
                    });
                }
            },

            showNotification(title, body) {
                if (this.notificationPermission && document.hidden) {
                    new Notification(title, { body: body, icon: 'https://emojicdn.elk.sh/💬' });
                }
            },

            // ============ GROUP FUNCTIONS ============
            async createGroup() {
                const groupName = prompt('Enter group name:');
                if (!groupName) return;

                const groupId = 'group_' + Date.now();
                try {
                    await database.ref('groups/' + groupId).set({
                        name: groupName,
                        createdBy: this.currentUserId,
                        createdAt: firebase.database.ServerValue.TIMESTAMP,
                        members: { [this.currentUserId]: true }
                    });
                    app.showToast(`Group "${groupName}" created!`);
                } catch (error) {
                    app.showToast('Failed to create group');
                }
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
                            groupDiv.innerHTML = `👥 ${this.escapeHtml(group.name)}`;
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
                this.cancelReply();
                
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
                                    <div>${this.escapeHtml(user.name)}</div>
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

                const sendBtn = document.getElementById('sendButton');
                sendBtn.disabled = true;

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

                // Add reply data if replying to a message
                if (this.replyingTo) {
                    message.replyTo = {
                        messageId: this.replyingTo.id,
                        text: this.replyingTo.text,
                        userName: this.replyingTo.userName
                    };
                    this.cancelReply();
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
                messagesRef.orderByChild('groupId').equalTo(this.currentGroup).on('child_added', (snapshot) => {
                    const message = snapshot.val();
                    this.displayMessage(message, snapshot.key);
                    
                    // Show notification for new message
                    if (message.userId !== this.currentUserId && document.hidden) {
                        this.showNotification(message.userName, message.text || 'Sent a message');
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
                
                let content = '';
                
                // Show reply preview if this is a reply
                if (message.replyTo) {
                    content += `<div class="reply-preview">
                        <strong>↩️ ${this.escapeHtml(message.replyTo.userName)}</strong>
                        <div class="reply-text">${this.escapeHtml(message.replyTo.text.substring(0, 50))}${message.replyTo.text.length > 50 ? '...' : ''}</div>
                    </div>`;
                }
                
                content += `<div class="message-sender">${this.escapeHtml(message.userName)}</div>`;
                
                if (message.text) {
                    content += `<div class="message-text">${this.escapeHtml(message.text)}</div>`;
                }
                
                if (message.fileUrl) {
                    if (message.fileType === 'image') {
                        content += `<img src="${message.fileUrl}" class="message-media" onclick="app.showImage('${message.fileUrl}', '${messageId}')" loading="lazy">`;
                    } else if (message.fileType === 'video') {
                        content += `<video src="${message.fileUrl}" controls class="message-media" preload="metadata"></video>`;
                    } else if (message.fileType === 'audio') {
                        content += `<audio src="${message.fileUrl}" controls class="audio-message"></audio>`;
                    } else {
                        content += `<a href="${message.fileUrl}" download class="message-media" style="display:block; padding:10px; background:#2A3942; border-radius:8px; text-decoration:none; color:#25D366;">📄 ${this.escapeHtml(message.fileName)}</a>`;
                    }
                }
                
                const time = new Date(message.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                
                content += `
                    <div class="message-time">
                        ${time}
                        ${isSent ? `<span class="read-status" onclick="app.showReadReceipts('${messageId}')">${message.seen ? '✓✓' : (message.delivered ? '✓✓' : '✓')}</span>` : ''}
                    </div>
                    <div class="message-reactions" id="reactions-${messageId}"></div>
                `;
                
                // Add action buttons for all messages
                content += `
                    <div class="message-actions">
                        <button class="msg-action-btn" onclick="app.replyToMessage('${messageId}', '${this.escapeHtml(message.text || 'Media')}', '${this.escapeHtml(message.userName)}')">↩️</button>
                        <button class="msg-action-btn" onclick="app.addReactionToMessage('${messageId}')">😊</button>
                        ${isSent ? `<button class="msg-action-btn" onclick="app.deleteMessage('${messageId}')">🗑️</button>` : ''}
                    </div>
                `;
                
                messageDiv.innerHTML = content;
                container.appendChild(messageDiv);
                
                if (!isSent && !message.seen) {
                    this.markAsRead(messageId);
                }
                
                this.loadReactions(messageId);
                
                // Auto-mark view-once messages as viewed after 5 seconds
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

            async deleteMessage(messageId) {
                if (confirm('Delete this message?')) {
                    await database.ref(`messages/${messageId}`).remove();
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
                        app.showToast('Chat cleared!', 'success');
                    }
                }
            },

            // ============ REPLY FEATURE ============
            replyToMessage(messageId, text, userName) {
                this.replyingTo = {
                    id: messageId,
                    text: text,
                    userName: userName
                };
                
                const replyBar = document.getElementById('replyBar');
                document.getElementById('replyToName').innerText = userName;
                document.getElementById('replyPreviewText').innerText = text.length > 50 ? text.substring(0, 50) + '...' : text;
                replyBar.classList.remove('hidden');
                document.getElementById('messageInput').focus();
            },

            cancelReply() {
                this.replyingTo = null;
                document.getElementById('replyBar').classList.add('hidden');
            },

            // ============ READ RECEIPTS ============
            async showReadReceipts(messageId) {
                const messageRef = database.ref(`messages/${messageId}`);
                const message = (await messageRef.once('value')).val();
                
                if (!message) return;
                
                const readBy = message.readBy || {};
                const modal = document.getElementById('readReceiptsModal');
                const list = document.getElementById('readReceiptsList');
                
                list.innerHTML = '<div style="color:#8696A0;">Loading...</div>';
                modal.classList.add('active');
                
                // Get user names for each readBy entry
                const readUsers = [];
                for (const [userId] of Object.entries(readBy)) {
                    const userRef = await database.ref(`users/${userId}`).once('value');
                    const user = userRef.val();
                    if (user) {
                        readUsers.push(user);
                    }
                }
                
                if (readUsers.length === 0) {
                    list.innerHTML = '<div style="color:#8696A0;">No one has read this message yet</div>';
                } else {
                    list.innerHTML = readUsers.map(user => `
                        <div class="read-user">
                            <div style="font-size: 32px">${user.avatar || '😀'}</div>
                            <div>
                                <div style="color:white; font-weight:500;">${this.escapeHtml(user.name)}</div>
                                <small style="color:#25D366">✓✓ Read</small>
                            </div>
                        </div>
                    `).join('');
                }
            },

            closeReadReceipts() {
                document.getElementById('readReceiptsModal').classList.remove('active');
            },

            // ============ SEARCH MESSAGES ============
            openSearchModal() {
                document.getElementById('searchModal').classList.add('active');
                document.getElementById('searchInput').value = '';
                document.getElementById('searchResults').innerHTML = '';
                document.getElementById('searchInput').focus();
            },

            closeSearchModal() {
                document.getElementById('searchModal').classList.remove('active');
            },

            async searchMessages(query) {
                if (!query.trim()) {
                    document.getElementById('searchResults').innerHTML = '';
                    return;
                }
                
                const messagesRef = database.ref('messages');
                const snapshot = await messagesRef.orderByChild('groupId').equalTo(this.currentGroup).once('value');
                const messages = snapshot.val();
                const results = [];
                
                if (messages) {
                    Object.entries(messages).forEach(([id, message]) => {
                        if (message.text && message.text.toLowerCase().includes(query.toLowerCase())) {
                            results.push({ id, ...message });
                        }
                    });
                }
                
                const resultsDiv = document.getElementById('searchResults');
                if (results.length === 0) {
                    resultsDiv.innerHTML = '<div style="color:#8696A0; padding:10px; text-align:center;">No messages found</div>';
                } else {
                    resultsDiv.innerHTML = results.map(msg => `
                        <div class="search-result" onclick="app.scrollToMessage('${msg.id}')">
                            <div style="color:#25D366; font-size:12px;">${this.escapeHtml(msg.userName)}</div>
                            <div style="color:white; font-size:13px;">${this.escapeHtml(msg.text.substring(0, 100))}${msg.text.length > 100 ? '...' : ''}</div>
                            <div style="color:#8696A0; font-size:10px;">${new Date(msg.timestamp).toLocaleString()}</div>
                        </div>
                    `).join('');
                }
            },

            scrollToMessage(messageId) {
                const messageDiv = document.getElementById(`msg-${messageId}`);
                if (messageDiv) {
                    messageDiv.scrollIntoView({ behavior: 'smooth', block: 'center' });
                    messageDiv.style.backgroundColor = '#2A3942';
                    setTimeout(() => {
                        messageDiv.style.backgroundColor = '';
                    }, 2000);
                    this.closeSearchModal();
                }
            },

            // ============ VOICE RECORDING ============
            async toggleVoiceRecording() {
                if (this.mediaRecorder && this.mediaRecorder.state === 'recording') {
                    this.stopVoiceRecording();
                } else {
                    this.startVoiceRecording();
                }
            },

            async startVoiceRecording() {
                try {
                    const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
                    this.mediaRecorder = new MediaRecorder(stream);
                    this.audioChunks = [];
                    
                    this.mediaRecorder.ondataavailable = (event) => {
                        this.audioChunks.push(event.data);
                    };
                    
                    this.mediaRecorder.onstop = async () => {
                        const audioBlob = new Blob(this.audioChunks, { type: 'audio/webm' });
                        await this.uploadAudio(audioBlob);
                        stream.getTracks().forEach(track => track.stop());
                    };
                    
                    this.mediaRecorder.start();
                    
                    // Start timer
                    this.recordingSeconds = 0;
                    this.recordingTimer = setInterval(() => {
                        this.recordingSeconds++;
                        const minutes = Math.floor(this.recordingSeconds / 60);
                        const seconds = this.recordingSeconds % 60;
                        document.getElementById('recordingTimer').innerText = `${minutes}:${seconds.toString().padStart(2, '0')}`;
                    }, 1000);
                    
                    document.getElementById('voiceRecordingUI').classList.remove('hidden');
                    document.getElementById('voiceBtn').classList.add('recording');
                    
                } catch (error) {
                    console.error('Microphone error:', error);
                    app.showToast('Microphone access denied');
                }
            },

            stopVoiceRecording() {
                if (this.mediaRecorder && this.mediaRecorder.state === 'recording') {
                    this.mediaRecorder.stop();
                    clearInterval(this.recordingTimer);
                    document.getElementById('voiceRecordingUI').classList.add('hidden');
                    document.getElementById('voiceBtn').classList.remove('recording');
                }
            },

            cancelVoiceRecording() {
                if (this.mediaRecorder && this.mediaRecorder.state === 'recording') {
                    this.mediaRecorder.onstop = null;
                    this.mediaRecorder.stop();
                    clearInterval(this.recordingTimer);
                    document.getElementById('voiceRecordingUI').classList.add('hidden');
                    document.getElementById('voiceBtn').classList.remove('recording');
                }
            },

            async uploadAudio(audioBlob) {
                this.showUploadProgress();
                this.updateUploadProgress(0);
                
                const formData = new FormData();
                formData.append('file', audioBlob, `voice_${Date.now()}.webm`);
                formData.append('upload_preset', CLOUDINARY_CONFIG.uploadPreset);
                formData.append('resource_type', 'raw');
                
                const xhr = new XMLHttpRequest();
                const uploadUrl = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CONFIG.cloudName}/raw/upload`;
                
                xhr.upload.addEventListener('progress', (e) => {
                    if (e.lengthComputable) {
                        const progress = (e.loaded / e.total) * 100;
                        app.updateUploadProgress(progress);
                    }
                });
                
                xhr.onload = () => {
                    if (xhr.status === 200) {
                        const response = JSON.parse(xhr.responseText);
                        this.pendingFile = {
                            url: response.secure_url,
                            type: 'audio',
                            name: 'Voice Message'
                        };
                        this.hideUploadProgress();
                        this.sendMessage();
                    } else {
                        this.hideUploadProgress();
                        app.showToast('Voice upload failed');
                    }
                };
                
                xhr.onerror = () => {
                    this.hideUploadProgress();
                    app.showToast('Upload failed');
                };
                
                xhr.open('POST', uploadUrl);
                xhr.send(formData);
            },

            // ============ REACTIONS ============
            async addReaction(messageId, reaction) {
                try {
                    const reactionRef = database.ref(`reactions/${messageId}/${reaction}`);
                    const users = (await reactionRef.once('value')).val() || [];
                    
                    if (!users.includes(this.currentUserId)) {
                        users.push(this.currentUserId);
                        await reactionRef.set(users);
                    }
                } catch (error) {
                    console.error('Reaction error:', error);
                }
            },

            addReactionToMessage(messageId) {
                const reactions = ['👍', '❤️', '😂', '😮', '😢', '😡'];
                const pickerDiv = document.createElement('div');
                pickerDiv.className = 'reaction-picker';
                pickerDiv.style.position = 'absolute';
                pickerDiv.style.background = '#202C33';
                pickerDiv.style.borderRadius = '20px';
                pickerDiv.style.padding = '8px';
                pickerDiv.style.display = 'flex';
                pickerDiv.style.gap = '8px';
                pickerDiv.style.zIndex = '100';
                
                reactions.forEach(reaction => {
                    const span = document.createElement('span');
                    span.style.fontSize = '20px';
                    span.style.cursor = 'pointer';
                    span.innerText = reaction;
                    span.onclick = () => {
                        this.addReaction(messageId, reaction);
                        pickerDiv.remove();
                    };
                    pickerDiv.appendChild(span);
                });
                
                const messageDiv = document.getElementById(`msg-${messageId}`);
                const rect = messageDiv.getBoundingClientRect();
                document.body.appendChild(pickerDiv);
                pickerDiv.style.top = rect.top - 50 + 'px';
                pickerDiv.style.left = rect.left + 'px';
                
                setTimeout(() => {
                    document.addEventListener('click', () => pickerDiv.remove(), { once: true });
                }, 100);
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
                    
                    const addBtn = document.createElement('span');
                    addBtn.className = 'reaction';
                    addBtn.innerHTML = '+';
                    addBtn.onclick = () => this.addReactionToMessage(messageId);
                    container.appendChild(addBtn);
                });
            },

            // ============ CLOUDINARY UPLOAD FUNCTIONS ============
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

            async uploadToCloudinary(file, type) {
                const formData = new FormData();
                formData.append('file', file);
                formData.append('upload_preset', CLOUDINARY_CONFIG.uploadPreset);
                
                let uploadUrl = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CONFIG.cloudName}/auto/upload`;
                
                if (type === 'video') {
                    uploadUrl = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CONFIG.cloudName}/video/upload`;
                }
                
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
                    
                    this.showUploadProgress();
                    this.updateUploadProgress(0);
                    
                    try {
                        const result = await this.uploadToCloudinary(file, 'image');
                        this.pendingFile = result;
                        this.hideUploadProgress();
                        this.closeFileUploadModal();
                        await this.sendMessage();
                    } catch (error) {
                        this.hideUploadProgress();
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
                    
                    this.showUploadProgress();
                    this.updateUploadProgress(0);
                    
                    try {
                        const result = await this.uploadToCloudinary(file, 'video');
                        this.pendingFile = result;
                        this.hideUploadProgress();
                        this.closeFileUploadModal();
                        await this.sendMessage();
                    } catch (error) {
                        this.hideUploadProgress();
                        app.showToast('Upload failed: ' + error.message);
                    }
                };
                input.click();
            },

            async uploadDocument() {
                const input = document.createElement('input');
                input.type = 'file';
                input.accept = '.pdf,.doc,.docx,.txt,.xls,.xlsx,.ppt,.pptx';
                input.onchange = async (e) => {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    if (file.size > CLOUDINARY_CONFIG.maxFileSize.document) {
                        app.showToast('Document too large! Max 20MB');
                        return;
                    }
                    
                    this.showUploadProgress();
                    this.updateUploadProgress(0);
                    
                    try {
                        const formData = new FormData();
                        formData.append('file', file);
                        formData.append('upload_preset', CLOUDINARY_CONFIG.uploadPreset);
                        formData.append('resource_type', 'raw');
                        
                        const xhr = new XMLHttpRequest();
                        const uploadUrl = `https://api.cloudinary.com/v1_1/${CLOUDINARY_CONFIG.cloudName}/raw/upload`;
                        
                        xhr.upload.addEventListener('progress', (e) => {
                            if (e.lengthComputable) {
                                const progress = (e.loaded / e.total) * 100;
                                this.updateUploadProgress(progress);
                            }
                        });
                        
                        xhr.onload = () => {
                            if (xhr.status === 200) {
                                const response = JSON.parse(xhr.responseText);
                                this.pendingFile = {
                                    url: response.secure_url,
                                    type: 'document',
                                    name: file.name,
                                    publicId: response.public_id
                                };
                                this.hideUploadProgress();
                                this.closeFileUploadModal();
                                this.sendMessage();
                            } else {
                                throw new Error('Upload failed');
                            }
                        };
                        
                        xhr.onerror = () => {
                            throw new Error('Network error');
                        };
                        
                        xhr.open('POST', uploadUrl);
                        xhr.send(formData);
                    } catch (error) {
                        this.hideUploadProgress();
                        app.showToast('Upload failed: ' + error.message);
                    }
                };
                input.click();
            },

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

            showImage(url, messageId) {
                const modal = document.getElementById('imageModal');
                document.getElementById('modalImage').src = url;
                modal.classList.add('active');
                
                if (messageId) {
                    this.markViewOnceAsViewed(messageId);
                }
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

            showUserProfile() {
                app.showToast(`Logged in as ${this.currentUser}`, 'success');
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

        // Initialize avatar selection
        document.querySelectorAll('.avatar-option').forEach(avatar => {
            avatar.onclick = () => {
                document.querySelectorAll('.avatar-option').forEach(a => a.classList.remove('selected'));
                avatar.classList.add('selected');
            };
        });
        document.querySelector('.avatar-option').classList.add('selected');

        // Close modals
        document.getElementById('fileUploadModal').onclick = (e) => {
            if (e.target === document.getElementById('fileUploadModal')) {
                app.closeFileUploadModal();
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
