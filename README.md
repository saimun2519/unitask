<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>UniTask – Earn by Watching Ads</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <style>
        /* All styles from previous version, with ad iframe */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Inter', 'Hind Siliguri', sans-serif;
            background: #f0f4f8;
            color: #1e293b;
            max-width: 640px;
            margin: 0 auto;
            min-height: 100vh;
            position: relative;
        }
        
        .loading-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255,255,255,0.9);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 9999;
        }
        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid #e0e0e0;
            border-top: 5px solid #2e7d32;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        
        .auth-container {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            background: linear-gradient(135deg, #f0f4f8, #e0eae0);
        }
        .auth-card {
            background: white;
            border-radius: 40px;
            padding: 40px 30px;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 20px 40px rgba(0,40,0,0.1);
        }
        .auth-logo {
            font-size: 32px;
            font-weight: 700;
            color: #2e7d32;
            text-align: center;
            margin-bottom: 30px;
        }
        .auth-input {
            width: 100%;
            padding: 16px 20px;
            border: 2px solid #e0eae0;
            border-radius: 40px;
            font-size: 15px;
            margin-bottom: 15px;
            transition: 0.2s;
        }
        .auth-input:focus {
            border-color: #2e7d32;
            outline: none;
        }
        .auth-btn {
            width: 100%;
            padding: 16px;
            background: #2e7d32;
            color: white;
            border: none;
            border-radius: 40px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            margin: 10px 0;
            transition: 0.2s;
        }
        .auth-btn:hover {
            background: #1b5e20;
            transform: translateY(-2px);
        }
        .auth-link {
            text-align: center;
            margin-top: 20px;
            color: #64748b;
            cursor: pointer;
        }
        .auth-link span {
            color: #2e7d32;
            font-weight: 600;
        }
        .auth-error {
            color: #dc3545;
            text-align: center;
            margin: 10px 0;
            font-size: 14px;
            background: #ffe6e6;
            padding: 8px;
            border-radius: 20px;
        }
        .auth-success {
            color: #2e7d32;
            text-align: center;
            margin: 10px 0;
            font-size: 14px;
            background: #e6ffe6;
            padding: 8px;
            border-radius: 20px;
        }
        
        #mainApp {
            display: none;
        }
        
        .mini-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 16px;
            background: transparent;
        }
        .logo-small {
            font-size: 20px;
            font-weight: 700;
            color: #2e7d32;
        }
        .header-right {
            display: flex;
            gap: 16px;
            align-items: center;
            position: relative;
        }
        .header-right i {
            font-size: 20px;
            color: #5e6f88;
            cursor: pointer;
        }
        .language-selector {
            background: #e8f5e9;
            border: none;
            padding: 6px 12px;
            border-radius: 30px;
            font-size: 14px;
            font-weight: 600;
            color: #2e7d32;
            cursor: pointer;
        }
        .notification-badge {
            position: absolute;
            top: -5px;
            right: 60px;
            background: #dc3545;
            color: white;
            border-radius: 50%;
            width: 18px;
            height: 18px;
            font-size: 11px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
        
        .page {
            display: none;
            padding: 0 16px 80px;
        }
        .page.active { display: block; }
        
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            max-width: 640px;
            margin: 0 auto;
            background: white;
            display: flex;
            justify-content: space-around;
            padding: 8px 8px 18px;
            border-radius: 30px 30px 0 0;
            box-shadow: 0 -4px 15px rgba(0,20,0,0.05);
            border-top: 1px solid #e0eae0;
        }
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: #8a9cb0;
            font-size: 11px;
            font-weight: 500;
            cursor: pointer;
        }
        .nav-item i {
            font-size: 22px;
            margin-bottom: 2px;
        }
        .nav-item.active {
            color: #2e7d32;
        }
        
        .section-title {
            font-size: 18px;
            font-weight: 600;
            color: #1b4a2c;
            margin: 18px 0 14px;
            padding-left: 8px;
            border-left: 4px solid #f39c12;
        }
        
        .ad-card {
            background: white;
            border-radius: 20px;
            padding: 14px 18px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 8px rgba(0,20,0,0.03);
            border: 1px solid rgba(70,140,70,0.15);
            cursor: pointer;
            transition: 0.2s;
            position: relative;
        }
        .ad-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,20,0,0.08);
        }
        .ad-info h4 {
            font-size: 16px;
            font-weight: 600;
            color: #1b4a2c;
            margin-bottom: 4px;
        }
        .ad-info p {
            color: #64748b;
            font-size: 12px;
            display: flex;
            align-items: center;
            gap: 4px;
        }
        .ad-reward {
            background: #2e7d32;
            color: white;
            font-size: 16px;
            font-weight: 600;
            padding: 8px 16px;
            border-radius: 40px;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .ad-reward i { color: #ffd966; }
        .ad-progress {
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 4px;
            background: #e0eae0;
            border-radius: 0 0 20px 20px;
            overflow: hidden;
        }
        .ad-progress-fill {
            height: 100%;
            background: #2e7d32;
            width: 0%;
            transition: width 0.3s;
        }
        .ad-limit-text {
            font-size: 11px;
            color: #2e7d32;
            margin-left: 8px;
        }
        
        .social-strip {
            display: flex;
            justify-content: space-between;
            background: white;
            border-radius: 50px;
            padding: 12px 24px;
            margin: 15px 0 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.02);
        }
        .social-icon {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: white;
            cursor: pointer;
            transition: 0.2s;
        }
        .social-icon:hover { transform: scale(1.1); }
        .telegram { background: #0088cc; }
        .youtube { background: #ff0000; }
        .facebook { background: #1877f2; }
        .tiktok { background: #010101; }
        .instagram { background: linear-gradient(45deg, #f09433, #d62976, #962fbf); }
        .support-btn {
            background: #2e7d32;
            color: white;
            padding: 12px 20px;
            border-radius: 40px;
            display: inline-block;
            text-align: center;
            font-weight: 600;
            cursor: pointer;
            margin: 15px 0;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            width: 100%;
        }
        
        .ref-card {
            background: white;
            border-radius: 26px;
            padding: 24px 18px;
            text-align: center;
            margin-bottom: 18px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.02);
        }
        .ref-link-box, .ref-username-box {
            background: #e8f5e9;
            border: 1px dashed #2e7d32;
            border-radius: 40px;
            padding: 12px 15px;
            font-size: 13px;
            margin: 16px 0;
            word-break: break-all;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .ref-username-box {
            margin-top: 8px;
        }
        .copy-icon {
            color: #2e7d32;
            cursor: pointer;
            font-size: 18px;
            margin-left: 10px;
            padding: 5px;
        }
        .copy-btn {
            background: #2e7d32;
            color: white;
            border: none;
            padding: 10px 28px;
            border-radius: 40px;
            font-size: 14px;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            transition: 0.2s;
        }
        .copy-btn:hover {
            background: #1b5e20;
            transform: translateY(-2px);
        }
        .stats-row {
            display: flex;
            gap: 12px;
        }
        .stat-item {
            background: white;
            flex: 1;
            padding: 16px;
            border-radius: 22px;
            text-align: center;
            border: 1px solid #e0f0e0;
        }
        .stat-value {
            font-size: 26px;
            font-weight: 700;
            color: #2e7d32;
        }
        .stat-label {
            font-size: 13px;
            color: #64748b;
        }
        .ranking-table {
            background: white;
            border-radius: 26px;
            padding: 20px;
            margin-top: 20px;
        }
        .ranking-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #e0eae0;
        }
        .ranking-item:last-child {
            border-bottom: none;
        }
        .rank-number {
            font-weight: 700;
            color: #2e7d32;
            width: 30px;
        }
        .rank-name {
            flex: 1;
            font-weight: 500;
        }
        .rank-value {
            font-weight: 600;
            color: #1b4a2c;
        }
        
        .profile-card {
            background: white;
            border-radius: 26px;
            padding: 18px;
            display: flex;
            gap: 16px;
            align-items: center;
            margin-bottom: 16px;
            border: 1px solid #e0f0e0;
            position: relative;
        }
        .profile-pic {
            width: 56px;
            height: 56px;
            border-radius: 50%;
            background: #c8e6c9;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            color: #2e7d32;
            border: 2px solid #2e7d32;
            overflow: hidden;
            cursor: pointer;
        }
        .profile-pic img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .profile-info h3 {
            font-size: 18px;
            font-weight: 600;
            color: #1b3b2a;
        }
        .profile-info p {
            font-size: 13px;
            color: #5e768d;
        }
        .balance-box {
            background: #e8f5e9;
            border-radius: 40px;
            padding: 16px 20px;
            display: flex;
            justify-content: space-between;
            font-size: 18px;
            font-weight: 600;
            color: #1b5e20;
            margin: 16px 0;
            border: 1px solid #a5d6a7;
        }
        .withdraw-btn {
            background: #d32f2f;
            color: white;
            border: none;
            padding: 15px;
            border-radius: 40px;
            font-size: 16px;
            font-weight: 600;
            width: 100%;
            cursor: pointer;
            margin-bottom: 16px;
            transition: 0.2s;
        }
        .withdraw-btn:hover {
            background: #b71c1c;
            transform: translateY(-2px);
        }
        
        .edit-profile-modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 2000;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .edit-profile-content {
            background: white;
            border-radius: 30px;
            padding: 25px;
            width: 100%;
            max-width: 400px;
        }
        .edit-profile-content h3 {
            margin-bottom: 20px;
            color: #1b4a2c;
        }
        .edit-profile-content input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #d0e0d0;
            border-radius: 30px;
            margin-bottom: 15px;
        }
        .edit-profile-content button {
            width: 100%;
            padding: 12px;
            background: #2e7d32;
            color: white;
            border: none;
            border-radius: 30px;
            font-weight: 600;
            cursor: pointer;
        }
        
        .contact-info {
            background: white;
            border-radius: 20px;
            padding: 20px;
            margin: 20px 0;
            border: 1px solid #e0f0e0;
        }
        .contact-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #e0eae0;
        }
        .contact-item:last-child {
            border-bottom: none;
        }
        .contact-item span {
            font-size: 16px;
            color: #1e293b;
        }
        .contact-item i {
            color: #2e7d32;
            font-size: 18px;
            cursor: pointer;
            margin-left: 15px;
        }
        
        .notice-board {
            background: white;
            border-radius: 20px;
            padding: 20px;
            margin-top: 25px;
            border: 1px solid #ff9800;
            box-shadow: 0 4px 12px rgba(255,152,0,0.1);
        }
        .notice-board h3 {
            font-size: 18px;
            font-weight: 600;
            color: #b85c00;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .notice-board p {
            font-size: 15px;
            color: #5e5e5e;
            line-height: 1.5;
        }
        
        .withdraw-form {
            background: white;
            border-radius: 26px;
            padding: 20px;
            margin: 12px 0;
            border: 1px solid #e0f0e0;
        }
        .method-selector {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }
        .method-btn {
            flex: 1;
            padding: 12px;
            border: 2px solid #e0eae0;
            border-radius: 40px;
            background: white;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            transition: 0.2s;
        }
        .method-btn.active {
            border-color: #2e7d32;
            background: #e8f5e9;
            color: #2e7d32;
        }
        .input-field {
            width: 100%;
            padding: 14px 18px;
            border: 1px solid #d0e0d0;
            border-radius: 40px;
            font-size: 14px;
            margin-bottom: 12px;
            font-family: 'Inter', sans-serif;
        }
        .submit-btn {
            background: #2e7d32;
            color: white;
            border: none;
            padding: 14px;
            border-radius: 40px;
            font-size: 16px;
            font-weight: 600;
            width: 100%;
            cursor: pointer;
            transition: 0.2s;
        }
        
        .dropdown-menu {
            position: absolute;
            top: 55px;
            right: 16px;
            background: white;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            display: none;
            z-index: 100;
            min-width: 200px;
            border: 1px solid #e0f0e0;
        }
        .dropdown-menu div {
            padding: 14px 18px;
            cursor: pointer;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 12px;
            border-bottom: 1px solid #f0f7f0;
            transition: 0.2s;
        }
        .dropdown-menu div:hover {
            background: #f5f5f5;
        }
        .dropdown-menu div i { width: 20px; color: #2e7d32; }
        
        .fullscreen-modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: #111;
            z-index: 3000;
            flex-direction: column;
        }
        .ad-corner-buttons {
            position: absolute;
            top: 16px;
            right: 16px;
            display: flex;
            gap: 10px;
            z-index: 10;
        }
        .corner-btn {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: rgba(30,30,30,0.9);
            backdrop-filter: blur(4px);
            color: white;
            font-size: 22px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border: 1px solid #444;
            transition: 0.2s;
            display: none;
        }
        .ad-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .ad-iframe {
            width: 100%;
            height: 70vh;
            min-height: 400px;
            border: 2px solid #2e7d32;
            border-radius: 30px;
            background: white;
            margin-bottom: 20px;
        }
        .timer-large {
            font-size: 60px;
            font-weight: 800;
            color: #2e7d32;
            text-shadow: 0 0 15px rgba(46,125,50,0.5);
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #2e7d32;
            color: white;
            padding: 12px 24px;
            border-radius: 40px;
            z-index: 9999;
            animation: slideIn 0.3s;
        }
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
    </style>
</head>
<body>
    <div class="loading-overlay" id="loadingOverlay">
        <div class="spinner"></div>
    </div>

    <div id="authPages">
        <div class="auth-container">
            <div class="auth-card">
                <div class="auth-logo">UniTask</div>
                <div id="loginForm">
                    <input type="email" id="loginEmail" class="auth-input" placeholder="Email Address" autocomplete="email">
                    <input type="password" id="loginPassword" class="auth-input" placeholder="Password" autocomplete="current-password">
                    <div id="loginError" class="auth-error"></div>
                    <button class="auth-btn" onclick="handleLogin()">Login</button>
                    <div class="auth-link" onclick="showRegister()">New user? <span>Create Account</span></div>
                </div>
                <div id="registerForm" style="display: none;">
                    <input type="email" id="regEmail" class="auth-input" placeholder="Email Address" autocomplete="email">
                    <input type="text" id="regUsername" class="auth-input" placeholder="Username">
                    <input type="password" id="regPassword" class="auth-input" placeholder="Password" autocomplete="new-password">
                    <input type="password" id="regConfirmPassword" class="auth-input" placeholder="Confirm Password" autocomplete="new-password">
                    <input type="text" id="regReferral" class="auth-input" placeholder="Referral ID (optional)">
                    <div id="registerError" class="auth-error"></div>
                    <div id="registerSuccess" class="auth-success"></div>
                    <button class="auth-btn" onclick="handleRegister()">Register</button>
                    <div class="auth-link" onclick="showLogin()">Already have account? <span>Login</span></div>
                </div>
            </div>
        </div>
    </div>

    <div id="mainApp">
        <div class="mini-header">
            <div class="logo-small">UniTask</div>
            <div class="header-right">
                <select class="language-selector" id="languageSelect" onchange="changeLanguage(this.value)">
                    <option value="en">English</option>
                    <option value="bn">বাংলা</option>
                </select>
                <i class="fas fa-bell" id="notificationBell"></i>
                <span class="notification-badge" id="notificationBadge" style="display: none;">0</span>
                <i class="fas fa-sliders-h" id="settingsIcon"></i>
            </div>
        </div>

        <div id="homePage" class="page active"></div>
        <div id="sharePage" class="page"></div>
        <div id="profilePage" class="page"></div>

        <div class="bottom-nav">
            <div class="nav-item active" data-page="home"><i class="fas fa-home"></i><span>HOME</span></div>
            <div class="nav-item" data-page="share"><i class="fas fa-share-alt"></i><span>SHARE</span></div>
            <div class="nav-item" data-page="profile"><i class="fas fa-user"></i><span>PROFILE</span></div>
        </div>

        <div class="fullscreen-modal" id="adModal">
            <div class="ad-corner-buttons">
                <div class="corner-btn" id="skipAdCorner">⏭</div>
                <div class="corner-btn" id="closeAdCorner" style="display:none;">✕</div>
            </div>
            <div class="ad-content">
                <iframe class="ad-iframe" id="adIframe" sandbox="allow-scripts allow-same-origin allow-popups allow-forms" src="about:blank"></iframe>
                <div class="timer-large" id="adTimerFull">00:00</div>
            </div>
        </div>

        <div class="dropdown-menu" id="profileMenu">
            <div onclick="editProfile()"><i class="fas fa-user-edit"></i> Edit Profile</div>
            <div onclick="contactSupport()"><i class="fas fa-headset"></i> Contact</div>
            <div onclick="aboutApp()"><i class="fas fa-info-circle"></i> About</div>
            <div onclick="logout()"><i class="fas fa-sign-out-alt"></i> Log Out</div>
        </div>

        <div class="edit-profile-modal" id="editProfileModal">
            <div class="edit-profile-content">
                <h3>Edit Profile</h3>
                <input type="text" id="editName" placeholder="Full Name">
                <input type="text" id="editUsername" placeholder="Username">
                <input type="password" id="editPassword" placeholder="New Password (optional)">
                <button onclick="saveProfileChanges()">Save Changes</button>
                <button onclick="closeEditProfile()" style="background:#6c757d; margin-top:10px;">Cancel</button>
            </div>
        </div>
    </div>

    <!-- Firebase SDK (using your config) -->
    <script type="module">
        const firebaseConfig = {
            apiKey: "AIzaSyDp5ptxuQaZ8xMSDu4ZlRJ0P3UV5TQD3fE",
            authDomain: "uni-da9b5.firebaseapp.com",
            projectId: "uni-da9b5",
            storageBucket: "uni-da9b5.firebasestorage.app",
            messagingSenderId: "828115344512",
            appId: "1:828115344512:web:aa1cdb6e6b52567a8b9a65",
            measurementId: "G-Q8CJEZ1EZZ"
        };

        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged, signOut, updatePassword, updateProfile } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getFirestore, collection, query, where, getDocs, addDoc, updateDoc, doc, getDoc, onSnapshot, orderBy, limit } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";
        import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-storage.js";
        import { getAnalytics } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-analytics.js";

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        const storage = getStorage(app);
        const analytics = getAnalytics(app);

        let currentUser = null;
        let currentUserDoc = null;
        let currentAd = null;
        let adStep = 1;
        let timerInterval = null;
        let timeLeft = 0;
        let selectedMethod = 'bkash';
        let adBoxes = [];
        let networks = [];
        let socialLinks = {};
        let settings = {
            minWithdraw: 2000,
            coinRate: 200,
            referralBonus: 200,
            announcement: "New tasks available! Double coins weekend is coming!",
            aboutUs: "UniTask is a platform where you can earn coins by watching ads."
        };
        let currentLanguage = 'en';
        let notificationCount = 0;
        let notifications = [];
        let adWatchCounts = {};
        let supportGroupLink = 'https://t.me/+i7ubfptv0wBiZDc9';

        function showLoading() { document.getElementById('loadingOverlay').style.display = 'flex'; }
        function hideLoading() { document.getElementById('loadingOverlay').style.display = 'none'; }

        async function loadAdWatchCounts() {
            if (!currentUserDoc) return;
            try {
                const userRef = doc(db, "users", currentUserDoc.id);
                const userSnap = await getDoc(userRef);
                if (userSnap.exists()) {
                    adWatchCounts = userSnap.data().adWatchCounts || {};
                }
            } catch (error) { console.error(error); }
        }

        onAuthStateChanged(auth, async (user) => {
            if (user) {
                showLoading();
                try {
                    const usersRef = collection(db, "users");
                    const q = query(usersRef, where("uid", "==", user.uid));
                    const snapshot = await getDocs(q);
                    if (!snapshot.empty) {
                        currentUserDoc = { id: snapshot.docs[0].id, ...snapshot.docs[0].data() };
                        currentUser = user;
                        await loadSettings();
                        await loadNetworks();
                        await loadAdBoxes();
                        await loadSocialLinks();
                        await loadNotifications();
                        await loadAdWatchCounts();
                        document.getElementById('authPages').style.display = 'none';
                        document.getElementById('mainApp').style.display = 'block';
                        renderHome();
                        renderShare();
                        renderProfile();
                        updateNotificationBadge();
                        listenForNotifications();
                    } else {
                        await signOut(auth);
                    }
                } catch (error) { console.error(error); } finally { hideLoading(); }
            } else {
                document.getElementById('authPages').style.display = 'block';
                document.getElementById('mainApp').style.display = 'none';
                showLogin();
                hideLoading();
            }
        });

        async function loadSettings() {
            try {
                const gen = await getDoc(doc(db, "settings", "general"));
                if (gen.exists()) settings = { ...settings, ...gen.data() };
                const notice = await getDoc(doc(db, "settings", "notice"));
                if (notice.exists()) settings.announcement = notice.data().message || settings.announcement;
                const about = await getDoc(doc(db, "settings", "about"));
                if (about.exists()) settings.aboutUs = about.data().message || settings.aboutUs;
                const social = await getDoc(doc(db, "settings", "social"));
                if (social.exists() && social.data().supportGroup) supportGroupLink = social.data().supportGroup;
            } catch (error) { console.error(error); }
        }

        async function loadNetworks() {
            try {
                const snap = await getDocs(collection(db, "networks"));
                networks = snap.docs.map(d => ({ id: d.id, ...d.data() }));
            } catch (error) { console.error(error); }
        }

        async function loadAdBoxes() {
            try {
                const q = query(collection(db, "adboxes"), where("status", "==", "active"));
                const snap = await getDocs(q);
                adBoxes = snap.docs.map(d => ({ id: d.id, ...d.data() }));
            } catch (error) { console.error(error); }
        }

        async function loadSocialLinks() {
            try {
                const social = await getDoc(doc(db, "settings", "social"));
                if (social.exists()) socialLinks = social.data();
            } catch (error) { console.error(error); }
        }

        async function loadNotifications() {
            if (!currentUserDoc) return;
            try {
                const q = query(collection(db, "notifications"), where("userId", "==", currentUserDoc.id), orderBy("createdAt", "desc"));
                const snap = await getDocs(q);
                notifications = [];
                notificationCount = 0;
                snap.forEach(d => {
                    const n = { id: d.id, ...d.data() };
                    notifications.push(n);
                    if (!n.read) notificationCount++;
                });
                updateNotificationBadge();
            } catch (error) { console.error(error); }
        }

        function updateNotificationBadge() {
            const badge = document.getElementById('notificationBadge');
            if (notificationCount > 0) {
                badge.style.display = 'flex';
                badge.textContent = notificationCount > 9 ? '9+' : notificationCount;
            } else badge.style.display = 'none';
        }

        function listenForNotifications() {
            if (!currentUserDoc) return;
            const q = query(collection(db, "notifications"), where("userId", "==", currentUserDoc.id), orderBy("createdAt", "desc"));
            onSnapshot(q, (snap) => {
                snap.docChanges().forEach(c => {
                    if (c.type === 'added') {
                        const n = { id: c.doc.id, ...c.doc.data() };
                        notifications.unshift(n);
                        if (!n.read) notificationCount++;
                        updateNotificationBadge();
                        showNotification(n.title + ': ' + n.message);
                    }
                });
            });
        }

        window.showLogin = () => {
            document.getElementById('loginForm').style.display = 'block';
            document.getElementById('registerForm').style.display = 'none';
            document.getElementById('loginError').innerHTML = '';
        };
        window.showRegister = () => {
            document.getElementById('loginForm').style.display = 'none';
            document.getElementById('registerForm').style.display = 'block';
            document.getElementById('registerError').innerHTML = '';
            document.getElementById('registerSuccess').innerHTML = '';
        };

        window.handleLogin = async () => {
            const email = document.getElementById('loginEmail').value.trim();
            const pw = document.getElementById('loginPassword').value;
            if (!email || !pw) { document.getElementById('loginError').innerHTML = 'Please enter email and password'; return; }
            showLoading();
            try {
                await signInWithEmailAndPassword(auth, email, pw);
            } catch (error) {
                hideLoading();
                let msg = '';
                if (error.code === 'auth/user-not-found') msg = 'User not found. Please register first.';
                else if (error.code === 'auth/wrong-password') msg = 'Wrong password. Please try again.';
                else if (error.code === 'auth/invalid-email') msg = 'Invalid email address.';
                else if (error.code === 'auth/too-many-requests') msg = 'Too many failed attempts. Try again later.';
                else msg = 'Login failed: ' + error.message;
                document.getElementById('loginError').innerHTML = msg;
            }
        };

        window.handleRegister = async () => {
            const email = document.getElementById('regEmail').value.trim();
            const username = document.getElementById('regUsername').value.trim();
            const pw = document.getElementById('regPassword').value;
            const cpw = document.getElementById('regConfirmPassword').value;
            const ref = document.getElementById('regReferral').value.trim();
            if (!email || !username || !pw || !cpw) { document.getElementById('registerError').innerHTML = 'Please fill all fields'; return; }
            if (pw !== cpw) { document.getElementById('registerError').innerHTML = 'Passwords do not match'; return; }
            if (pw.length < 6) { document.getElementById('registerError').innerHTML = 'Password must be at least 6 characters'; return; }
            showLoading();
            try {
                const usersRef = collection(db, "users");
                const unameQuery = query(usersRef, where("username", "==", username));
                const unameSnap = await getDocs(unameQuery);
                if (!unameSnap.empty) {
                    document.getElementById('registerError').innerHTML = 'Username already taken';
                    hideLoading(); return;
                }
                const cred = await createUserWithEmailAndPassword(auth, email, pw);
                let referrerId = null;
                if (ref) {
                    const refQuery = query(usersRef, where("username", "==", ref));
                    const refSnap = await getDocs(refQuery);
                    if (!refSnap.empty) referrerId = refSnap.docs[0].id;
                }
                const newUser = {
                    uid: cred.user.uid,
                    email, name: username, username,
                    referredBy: referrerId,
                    coins: 0, referrals: 0, referralEarnings: 0,
                    createdAt: new Date().toISOString(),
                    profilePic: '', adWatchCounts: {}
                };
                await addDoc(collection(db, "users"), newUser);
                if (referrerId) {
                    const refDoc = await getDoc(doc(db, "users", referrerId));
                    if (refDoc.exists()) {
                        const rd = refDoc.data();
                        await updateDoc(doc(db, "users", referrerId), {
                            referrals: (rd.referrals || 0) + 1,
                            referralEarnings: (rd.referralEarnings || 0) + (settings.referralBonus || 200)
                        });
                    }
                }
                document.getElementById('registerSuccess').innerHTML = 'Registration successful! You can now login.';
                setTimeout(() => showLogin(), 2000);
            } catch (error) {
                hideLoading();
                let msg = error.code === 'auth/email-already-in-use' ? 'Email already in use.' : 'Registration failed: ' + error.message;
                document.getElementById('registerError').innerHTML = msg;
            }
        };

        window.logout = async () => { try { await signOut(auth); document.getElementById('profileMenu').style.display = 'none'; } catch (error) { console.error(error); } };

        window.changeLanguage = (lang) => {
            currentLanguage = lang;
            if (document.getElementById('homePage').classList.contains('active')) renderHome();
            if (document.getElementById('sharePage').classList.contains('active')) renderShare();
            if (document.getElementById('profilePage').classList.contains('active')) renderProfile();
        };

        function renderHome() {
            const home = document.getElementById('homePage');
            let html = `<div class="section-title">${currentLanguage === 'en' ? "Today's Offers" : "আজকের অফার"}</div>`;
            if (adBoxes.length === 0) {
                html += `<div style="text-align:center;padding:40px;color:#64748b;">${currentLanguage === 'en' ? "No ads available" : "কোনো এড নেই"}</div>`;
            } else {
                adBoxes.forEach(ad => {
                    const limit = ad.dailyLimit || 10;
                    const watched = adWatchCounts[ad.id] || 0;
                    const remaining = limit - watched;
                    const progress = (watched / limit) * 100;
                    html += `<div class="ad-card" onclick="openAdModal('${ad.id}')">
                        <div class="ad-info"><h4>${ad.title || (currentLanguage === 'en' ? 'Special Offer' : 'স্পেশাল অফার')}</h4>
                        <p><i class="fas fa-clock"></i> ${ad.time || 20} ${currentLanguage === 'en' ? 'sec' : 'সেকেন্ড'}</p></div>
                        <div class="ad-reward"><i class="fas fa-coins"></i> ${ad.coins || 0}</div>
                        <div class="ad-progress"><div class="ad-progress-fill" style="width:${progress}%;"></div></div>
                        <span class="ad-limit-text">${remaining}/${limit}</span>
                    </div>`;
                });
            }
            html += `<div class="section-title">${currentLanguage === 'en' ? "Official Channels" : "আমাদের চ্যানেল"}</div>`;
            html += `<div class="social-strip">`;
            const chans = [
                { name: 'telegram', icon: 'telegram', link: socialLinks.telegram || '#' },
                { name: 'youtube', icon: 'youtube', link: socialLinks.youtube || '#' },
                { name: 'facebook', icon: 'facebook', link: socialLinks.facebook || '#' },
                { name: 'tiktok', icon: 'tiktok', link: socialLinks.tiktok || '#' },
                { name: 'instagram', icon: 'instagram', link: socialLinks.instagram || '#' }
            ];
            chans.forEach(ch => html += `<div class="social-icon ${ch.icon}" onclick="window.open('${ch.link}', '_system')"><i class="fab fa-${ch.name}"></i></div>`);
            html += `</div><div class="support-btn" onclick="window.open('${supportGroupLink}', '_system')"><i class="fab fa-telegram"></i> Join Support Group</div>`;
            home.innerHTML = html;
        }

        window.openAdModal = function(adId) {
            const ad = adBoxes.find(a => a.id === adId);
            if (!ad) return;
            const limit = ad.dailyLimit || 10;
            const watched = adWatchCounts[ad.id] || 0;
            if (watched >= limit) {
                showNotification(currentLanguage === 'en' ? 'Daily limit reached for this ad' : 'এই এডের আজকের লিমিট শেষ');
                return;
            }
            currentAd = ad;
            adStep = 1;
            loadNetworkLinks(ad.networkIndex);
            document.getElementById('adTimerFull').innerText = formatTime(ad.time || 20);
            document.getElementById('skipAdCorner').style.display = 'none';
            document.getElementById('closeAdCorner').style.display = 'none';
            document.getElementById('adModal').style.display = 'flex';
            timeLeft = ad.time || 20;
            startFullTimer();
        };

        async function loadNetworkLinks(idx) {
            try {
                if (networks && networks[idx]) {
                    const link = networks[idx].link1;
                    document.getElementById('adIframe').src = link && link !== '#' ? link : 'about:blank';
                } else {
                    document.getElementById('adIframe').src = 'about:blank';
                }
            } catch (error) { console.error(error); }
        }

        function startFullTimer() {
            if (timerInterval) clearInterval(timerInterval);
            timerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById('adTimerFull').innerText = formatTime(timeLeft);
                if (adStep === 1 && timeLeft <= Math.floor((currentAd.time || 20)/2)) {
                    document.getElementById('skipAdCorner').style.display = 'flex';
                }
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    if (adStep === 1) {
                        adStep = 2;
                        timeLeft = Math.ceil((currentAd.time || 20)/2);
                        document.getElementById('adTimerFull').innerText = formatTime(timeLeft);
                        document.getElementById('skipAdCorner').style.display = 'none';
                        // Load second ad link if exists
                        if (networks && networks[currentAd.networkIndex]) {
                            const link2 = networks[currentAd.networkIndex].link2;
                            document.getElementById('adIframe').src = link2 && link2 !== '#' ? link2 : 'about:blank';
                        } else {
                            document.getElementById('adIframe').src = 'about:blank';
                        }
                        startFullTimer();
                    } else {
                        document.getElementById('skipAdCorner').style.display = 'none';
                        document.getElementById('closeAdCorner').style.display = 'flex';
                    }
                }
            }, 1000);
        }

        function formatTime(s) {
            if (s < 0) s = 0;
            const m = Math.floor(s/60).toString().padStart(2,'0');
            const sec = Math.floor(s%60).toString().padStart(2,'0');
            return `${m}:${sec}`;
        }

        document.getElementById('skipAdCorner').addEventListener('click', function() {
            if (adStep === 1 && currentAd) {
                adStep = 2;
                timeLeft = Math.ceil((currentAd.time || 20)/2);
                document.getElementById('adTimerFull').innerText = formatTime(timeLeft);
                document.getElementById('skipAdCorner').style.display = 'none';
                if (networks && networks[currentAd.networkIndex]) {
                    const link2 = networks[currentAd.networkIndex].link2;
                    document.getElementById('adIframe').src = link2 && link2 !== '#' ? link2 : 'about:blank';
                }
                startFullTimer();
            }
        });

        document.getElementById('closeAdCorner').addEventListener('click', async function() {
            if (currentAd && currentUserDoc) {
                const reward = currentAd.coins || 0;
                const userRef = doc(db, "users", currentUserDoc.id);
                const adId = currentAd.id;
                const newCount = (adWatchCounts[adId] || 0) + 1;
                adWatchCounts[adId] = newCount;
                await updateDoc(userRef, { coins: (currentUserDoc.coins || 0) + reward, adWatchCounts: adWatchCounts });
                currentUserDoc.coins += reward;
                showNotification(currentLanguage === 'en' ? `You earned ${reward} coins!` : `আপনি ${reward} কয়েন পেয়েছেন!`);
                renderProfile();
                renderHome();
            }
            document.getElementById('adModal').style.display = 'none';
            if (timerInterval) clearInterval(timerInterval);
            document.getElementById('skipAdCorner').style.display = 'none';
            document.getElementById('closeAdCorner').style.display = 'none';
            document.getElementById('adIframe').src = 'about:blank';
        });

        async function renderShare() {
            const share = document.getElementById('sharePage');
            let rankHTML = '';
            try {
                const q = query(collection(db, "users"), orderBy("referrals", "desc"), limit(12));
                const snap = await getDocs(q);
                let r = 1;
                rankHTML = '<div class="ranking-table"><h3>Top 12 Referrers</h3>';
                snap.forEach(d => {
                    const u = d.data();
                    rankHTML += `<div class="ranking-item"><span class="rank-number">#${r}</span><span class="rank-name">${u.name || u.username}</span><span class="rank-value">${u.referrals || 0}</span></div>`;
                    r++;
                });
                rankHTML += '</div>';
            } catch { rankHTML = '<p>Unable to load ranking</p>'; }
            share.innerHTML = `
                <div class="ref-card">
                    <h3>${currentLanguage === 'en' ? "Invite Friends" : "বন্ধুদের আমন্ত্রণ"}</h3>
                    <p>${settings.referralBonus} ${currentLanguage === 'en' ? 'coins per referral' : 'কয়েন প্রতি রেফারেল'}</p>
                    <div class="ref-link-box"><span id="refLink">https://t.me/unitask?ref=${currentUserDoc?.username || 'user'}</span><i class="fas fa-copy copy-icon" onclick="copyText('refLink')"></i></div>
                    <div class="ref-username-box"><span id="refUsername">${currentUserDoc?.username || 'username'}</span><i class="fas fa-copy copy-icon" onclick="copyText('refUsername')"></i></div>
                    <button class="copy-btn" onclick="copyText('refLink')"><i class="fas fa-copy"></i> ${currentLanguage === 'en' ? "Copy Link" : "লিংক কপি"}</button>
                </div>
                <div class="stats-row"><div class="stat-item"><div class="stat-value">${currentUserDoc?.referrals || 0}</div><div class="stat-label">${currentLanguage === 'en' ? "Referrals" : "রেফারেল"}</div></div><div class="stat-item"><div class="stat-value">${currentUserDoc?.referralEarnings || 0}</div><div class="stat-label">${currentLanguage === 'en' ? "Earned" : "আয়"}</div></div></div>
                ${rankHTML}
            `;
        }

        window.copyText = (id) => {
            const text = document.getElementById(id).innerText;
            if (navigator.clipboard && navigator.clipboard.writeText) {
                navigator.clipboard.writeText(text).then(() => showNotification(currentLanguage === 'en' ? 'Copied!' : 'কপি হয়েছে!'));
            } else {
                const ta = document.createElement('textarea');
                ta.value = text;
                document.body.appendChild(ta);
                ta.select();
                document.execCommand('copy');
                document.body.removeChild(ta);
                showNotification(currentLanguage === 'en' ? 'Copied!' : 'কপি হয়েছে!');
            }
        };

        function renderProfile() {
            const profile = document.getElementById('profilePage');
            const pic = currentUserDoc?.profilePic || '';
            profile.innerHTML = `
                <div class="profile-card"><div class="profile-pic" onclick="uploadProfilePic()">${pic ? `<img src="${pic}">` : '<i class="fas fa-user"></i>'}</div><div class="profile-info"><h3>${currentUserDoc?.name || currentUserDoc?.username || 'User'}</h3><p>@${currentUserDoc?.username || 'username'} • ID: ${currentUserDoc?.id?.substring(0,8) || '123'}</p></div></div>
                <div class="balance-box"><span><i class="fas fa-coins" style="color:#f39c12;"></i> ${currentLanguage === 'en' ? 'Coin Balance' : 'কয়েন ব্যালেন্স'}</span><span>${currentUserDoc?.coins || 0}</span></div>
                <button class="withdraw-btn" onclick="showWithdrawForm()"><i class="fas fa-arrow-up"></i> ${currentLanguage === 'en' ? 'Withdraw' : 'উইথড্র'}</button>
                <div id="withdrawForm" class="withdraw-form" style="display:none;"><div class="method-selector"><button class="method-btn ${selectedMethod === 'bkash' ? 'active' : ''}" onclick="selectMethod('bkash', event)">Bkash</button><button class="method-btn ${selectedMethod === 'nagad' ? 'active' : ''}" onclick="selectMethod('nagad', event)">Nagad</button><button class="method-btn ${selectedMethod === 'binance' ? 'active' : ''}" onclick="selectMethod('binance', event)">Binance</button></div><input type="text" class="input-field" id="withdrawAccount" placeholder="${currentLanguage === 'en' ? 'Account Number' : 'একাউন্ট নম্বর'}"><input type="number" class="input-field" id="withdrawAmount" placeholder="${currentLanguage === 'en' ? 'Amount (coins)' : 'পরিমাণ (কয়েন)'}"><button class="submit-btn" onclick="submitWithdraw()">${currentLanguage === 'en' ? 'Submit Request' : 'রিকোয়েস্ট জমা দিন'}</button></div>
                <div class="notice-board"><h3><i class="fas fa-bullhorn" style="color:#ff9800;"></i> ${currentLanguage === 'en' ? 'NOTICE' : 'নোটিশ'}</h3><p>${settings.announcement}</p></div>
            `;
        }

        window.uploadProfilePic = async () => {
            const input = document.createElement('input');
            input.type = 'file';
            input.accept = 'image/*';
            input.onchange = async (e) => {
                const file = e.target.files[0];
                if (!file) return;
                showLoading();
                try {
                    const ref = ref(storage, `profilePics/${currentUserDoc.id}`);
                    await uploadBytes(ref, file);
                    const url = await getDownloadURL(ref);
                    await updateDoc(doc(db, "users", currentUserDoc.id), { profilePic: url });
                    currentUserDoc.profilePic = url;
                    renderProfile();
                    showNotification('Profile picture updated');
                } catch (error) { showNotification('Upload failed', 'error'); } finally { hideLoading(); }
            };
            input.click();
        };

        window.editProfile = () => {
            document.getElementById('editName').value = currentUserDoc?.name || '';
            document.getElementById('editUsername').value = currentUserDoc?.username || '';
            document.getElementById('editPassword').value = '';
            document.getElementById('editProfileModal').style.display = 'flex';
        };
        window.closeEditProfile = () => document.getElementById('editProfileModal').style.display = 'none';
        window.saveProfileChanges = async () => {
            const name = document.getElementById('editName').value.trim();
            const uname = document.getElementById('editUsername').value.trim();
            const pw = document.getElementById('editPassword').value;
            if (!name || !uname) { showNotification('Name and username cannot be empty', 'error'); return; }
            showLoading();
            try {
                await updateDoc(doc(db, "users", currentUserDoc.id), { name, username: uname });
                currentUserDoc.name = name; currentUserDoc.username = uname;
                if (pw.length >= 6) { await updatePassword(auth.currentUser, pw); showNotification('Password updated'); }
                if (auth.currentUser) await updateProfile(auth.currentUser, { displayName: name });
                showNotification('Profile updated');
                renderProfile(); renderShare(); closeEditProfile();
            } catch (error) { showNotification('Update failed: ' + error.message, 'error'); } finally { hideLoading(); }
        };

        window.contactSupport = () => alert(`Email: saimunahmad67@gmail.com\nPhone: 01798792581\n\nTap and hold to copy.`);

        document.getElementById('notificationBell').addEventListener('click', () => {
            let msg = '';
            notifications.forEach(n => msg += `${n.title}: ${n.message}\n`);
            alert(msg || 'No notifications');
            notificationCount = 0;
            updateNotificationBadge();
        });

        document.querySelectorAll('.nav-item').forEach(item => {
            item.addEventListener('click', function() {
                document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                this.classList.add('active');
                const page = this.dataset.page;
                document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
                document.getElementById(page + 'Page').classList.add('active');
                if (page === 'home') renderHome();
                if (page === 'share') renderShare();
                if (page === 'profile') renderProfile();
            });
        });

        document.getElementById('settingsIcon')?.addEventListener('click', (e) => {
            e.stopPropagation();
            const m = document.getElementById('profileMenu');
            m.style.display = m.style.display === 'block' ? 'none' : 'block';
        });
        document.addEventListener('click', (e) => {
            const m = document.getElementById('profileMenu');
            const s = document.getElementById('settingsIcon');
            if (!s?.contains(e.target) && !m?.contains(e.target)) m.style.display = 'none';
        });

        window.selectMethod = (method, e) => {
            selectedMethod = method;
            document.querySelectorAll('.method-btn').forEach(b => b.classList.remove('active'));
            e.target.classList.add('active');
        };

        window.showWithdrawForm = () => {
            const f = document.getElementById('withdrawForm');
            f.style.display = f.style.display === 'none' ? 'block' : 'none';
        };

        window.submitWithdraw = async () => {
            const acc = document.getElementById('withdrawAccount').value;
            const amt = parseInt(document.getElementById('withdrawAmount').value);
            if (!acc || !amt) { showNotification('Please fill all fields'); return; }
            if (amt > currentUserDoc.coins) { showNotification('Insufficient coins'); return; }
            if (amt < settings.minWithdraw) { showNotification(`Minimum withdraw is ${settings.minWithdraw} coins`); return; }
            try {
                await addDoc(collection(db, "withdrawals"), {
                    userId: currentUserDoc.id, userName: currentUserDoc.name, userEmail: currentUserDoc.email,
                    method: selectedMethod, account: acc, amount: amt, status: 'pending',
                    requestedAt: new Date().toISOString()
                });
                await addDoc(collection(db, "notifications"), {
                    userId: currentUserDoc.id, title: 'Withdrawal Request',
                    message: `Your withdrawal request of ${amt} coins is pending.`,
                    type: 'withdrawal', read: false, createdAt: new Date().toISOString()
                });
                showNotification('Withdrawal request submitted!');
                document.getElementById('withdrawForm').style.display = 'none';
                document.getElementById('withdrawAccount').value = '';
                document.getElementById('withdrawAmount').value = '';
            } catch (error) { showNotification('Error submitting request', 'error'); }
        };

        window.aboutApp = () => alert(settings.aboutUs);

        function showNotification(msg, type = 'success') {
            const n = document.createElement('div');
            n.className = 'notification';
            if (type === 'error') n.style.background = '#dc3545';
            n.innerHTML = `<i class="fas fa-check-circle"></i> ${msg}`;
            document.body.appendChild(n);
            setTimeout(() => n.remove(), 3000);
        }

        onSnapshot(collection(db, "adboxes"), () => { loadAdBoxes(); if (document.getElementById('homePage').classList.contains('active')) renderHome(); });
        onSnapshot(doc(db, "settings", "social"), () => { loadSocialLinks(); if (document.getElementById('homePage').classList.contains('active')) renderHome(); });
        onSnapshot(doc(db, "settings", "notice"), (d) => { if (d.exists()) { settings.announcement = d.data().message || settings.announcement; if (document.getElementById('profilePage').classList.contains('active')) renderProfile(); } });
    </script>
</body>
</html>
