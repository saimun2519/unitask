<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>UniTask – Earn Money Online</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background: #f8fafc; color: #1e293b; font-size: 13px; min-height: 100vh; }
        
        .auth-container { min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 20px; background: linear-gradient(135deg, #2e7d32 0%, #1b5e20 100%); }
        .auth-card { background: white; border-radius: 32px; padding: 32px 24px; width: 100%; max-width: 400px; box-shadow: 0 25px 50px rgba(0,0,0,0.2); }
        .auth-card h2 { font-size: 28px; font-weight: 800; background: linear-gradient(135deg, #2e7d32, #4caf50); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-align: center; margin-bottom: 8px; }
        .auth-card .subtitle { text-align: center; color: #64748b; margin-bottom: 24px; font-size: 13px; }
        .input-group { margin-bottom: 16px; }
        .input-group label { display: block; font-size: 12px; font-weight: 600; margin-bottom: 6px; color: #1e293b; }
        .input-group input { width: 100%; padding: 12px 14px; border: 1.5px solid #e2e8f0; border-radius: 14px; font-size: 14px; font-family: inherit; transition: 0.2s; }
        .input-group input:focus { outline: none; border-color: #2e7d32; box-shadow: 0 0 0 3px rgba(46,125,50,0.1); }
        .auth-btn { width: 100%; padding: 14px; background: #2e7d32; color: white; border: none; border-radius: 14px; font-size: 16px; font-weight: 700; cursor: pointer; font-family: inherit; transition: 0.2s; }
        .auth-btn:hover { background: #1b5e20; transform: translateY(-1px); }
        .auth-link { text-align: center; margin-top: 20px; font-size: 13px; color: #64748b; }
        .auth-link a { color: #2e7d32; text-decoration: none; font-weight: 600; cursor: pointer; }
        .error-msg { background: #fef2f2; color: #dc2626; padding: 10px; border-radius: 12px; font-size: 12px; margin-bottom: 16px; text-align: center; display: none; }
        .success-msg { background: #f0fdf4; color: #2e7d32; padding: 10px; border-radius: 12px; font-size: 12px; margin-bottom: 16px; text-align: center; display: none; }
        
        .user-view { max-width: 640px; margin: 0 auto; min-height: 100vh; position: relative; display: none; background: #f8fafc; }
        .mini-header { display: flex; justify-content: space-between; align-items: center; padding: 12px 16px; background: white; margin: 10px 12px; border-radius: 24px; box-shadow: 0 2px 10px rgba(0,0,0,0.04); position: relative; }
        .logo-small { font-size: 18px; font-weight: 800; background: linear-gradient(135deg, #2e7d32, #4caf50); -webkit-background-clip: text; -webkit-text-fill-color: transparent; cursor: pointer; }
        .header-right { display: flex; gap: 12px; align-items: center; position: relative; }
        .language-selector { background: #f0fdf4; border: none; padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: 600; color: #2e7d32; cursor: pointer; font-family: inherit; }
        .notification-wrapper { position: relative; cursor: pointer; }
        .notification-icon { font-size: 20px; color: #64748b; }
        .notification-badge { position: absolute; top: -8px; right: -10px; background: #ef4444; color: white; border-radius: 50%; min-width: 18px; height: 18px; font-size: 10px; display: flex; align-items: center; justify-content: center; font-weight: bold; padding: 0 4px; }
        .logout-btn { background: #ef4444; color: white; border: none; padding: 6px 14px; border-radius: 20px; font-size: 11px; font-weight: 600; cursor: pointer; font-family: inherit; transition: 0.2s; }
        .logout-btn:hover { background: #dc2626; }
        .settings-icon { background: none; border: none; color: #64748b; font-size: 20px; cursor: pointer; padding: 4px; }
        
        .page { display: none; padding: 0 12px 80px; }
        .page.active { display: block; }
        
        .bottom-nav { position: fixed; bottom: 0; left: 0; right: 0; max-width: 640px; margin: 0 auto; background: white; display: flex; justify-content: space-around; padding: 8px 16px 20px; border-radius: 28px 28px 0 0; border-top: 1px solid #e2e8f0; z-index: 100; box-shadow: 0 -4px 12px rgba(0,0,0,0.05); }
        .nav-item { display: flex; flex-direction: column; align-items: center; color: #94a3b8; font-size: 10px; font-weight: 500; cursor: pointer; transition: 0.2s; user-select: none; }
        .nav-item i { font-size: 22px; margin-bottom: 4px; }
        .nav-item.active { color: #2e7d32; }
        .nav-item:hover { color: #4caf50; }
        
        .balance-header { display: flex; gap: 12px; margin: 12px 0; }
        .balance-card { flex: 1; background: white; border-radius: 24px; padding: 16px; text-align: center; box-shadow: 0 2px 8px rgba(0,0,0,0.04); transition: all 0.2s; }
        .balance-card:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(0,0,0,0.08); }
        .balance-card .label { font-size: 12px; color: #64748b; margin-bottom: 6px; font-weight: 500; }
        .balance-card .amount { font-size: 24px; font-weight: 800; color: #2e7d32; }
        .balance-card.income .amount { color: #f59e0b; }
        
        .section-title { font-size: 16px; font-weight: 700; color: #1e293b; margin: 20px 0 12px; padding-left: 12px; border-left: 4px solid #2e7d32; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 8px; }
        
        .jobs-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 20px; }
        .job-card { background: white; border-radius: 20px; padding: 14px 10px; box-shadow: 0 2px 8px rgba(0,0,0,0.04); cursor: pointer; text-align: center; transition: all 0.2s; border: 1px solid #e2e8f0; }
        .job-card:hover { transform: translateY(-3px); box-shadow: 0 8px 20px rgba(46,125,50,0.12); border-color: #2e7d32; }
        .job-reward { background: linear-gradient(135deg, #2e7d32, #4caf50); color: white; font-size: 14px; font-weight: 700; padding: 6px 14px; border-radius: 30px; display: inline-block; margin-bottom: 10px; }
        .job-title { font-size: 13px; font-weight: 600; color: #1e293b; padding: 8px 4px; margin: 6px 0; word-break: break-word; background: #f8fafc; border-radius: 12px; }
        .submit-badge { background: #f59e0b; color: white; font-size: 10px; padding: 5px 12px; border-radius: 20px; display: inline-block; margin-top: 8px; font-weight: 600; }
        .unlimited-badge { background: #8b5cf6; color: white; font-size: 10px; padding: 4px 12px; border-radius: 20px; }
        
        .progress-container { margin: 8px 0; background: #e2e8f0; border-radius: 10px; height: 5px; overflow: hidden; width: 100%; }
        .progress-bar { background: #2e7d32; height: 100%; width: 0%; border-radius: 10px; transition: width 0.3s ease; }
        .progress-stats { font-size: 10px; color: #64748b; margin-top: 4px; display: flex; justify-content: space-between; }
        
        .tasks-grid { display: flex; flex-direction: column; gap: 10px; }
        .task-card { background: white; border-radius: 16px; padding: 12px 14px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); border: 1px solid #e2e8f0; margin-bottom: 0; cursor: pointer; transition: all 0.2s; }
        .task-card:hover { transform: translateX(3px); border-left: 3px solid #2e7d32; background: #fefce8; }
        .task-header-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px; flex-wrap: wrap; gap: 8px; }
        .task-reward-box { background: linear-gradient(135deg, #2e7d32, #4caf50); color: white; font-size: 13px; font-weight: 700; padding: 5px 12px; border-radius: 20px; display: inline-block; }
        .task-title-text { font-size: 14px; font-weight: 700; color: #1e293b; margin-bottom: 6px; }
        .task-stats-row { font-size: 11px; color: #64748b; margin-bottom: 8px; display: flex; gap: 12px; flex-wrap: wrap; }
        .action-buttons-row { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 8px; padding-top: 8px; border-top: 1px solid #e2e8f0; }
        .action-btn { padding: 6px 14px; border-radius: 30px; font-size: 11px; font-weight: 600; cursor: pointer; border: none; font-family: inherit; transition: 0.2s; }
        .action-btn.running { background: #2e7d32; color: white; }
        .action-btn.pause { background: #f59e0b; color: white; }
        .action-btn.submitted { background: #3b82f6; color: white; }
        .action-btn.increase { background: #8b5cf6; color: white; }
        .action-btn.delete { background: #ef4444; color: white; }
        .action-btn.approve { background: #10b981; color: white; }
        .action-btn.reject { background: #ef4444; color: white; }
        .action-btn:hover { opacity: 0.85; transform: translateY(-1px); }
        
        .submissions-table { width: 100%; border-collapse: collapse; font-size: 11px; }
        .submissions-table th, .submissions-table td { padding: 8px 6px; text-align: left; border-bottom: 1px solid #e2e8f0; }
        .submissions-table th { background: #f1f5f9; font-weight: 600; color: #475569; }
        .proof-link { color: #3b82f6; text-decoration: none; font-size: 10px; cursor: pointer; }
        .badge-pending { background: #fef3c7; color: #d97706; padding: 2px 8px; border-radius: 20px; font-size: 10px; }
        .badge-approved { background: #d1fae5; color: #059669; padding: 2px 8px; border-radius: 20px; font-size: 10px; }
        .badge-rejected { background: #fee2e2; color: #dc2626; padding: 2px 8px; border-radius: 20px; font-size: 10px; }
        .badge-completed { background: #d1fae5; color: #059669; padding: 2px 8px; border-radius: 20px; font-size: 10px; }
        
        .notification-panel { position: fixed; top: 60px; right: 10px; left: 10px; max-width: 380px; margin: 0 auto; background: white; border-radius: 24px; box-shadow: 0 10px 40px rgba(0,0,0,0.15); z-index: 1000; display: none; max-height: 70vh; overflow-y: auto; border: 1px solid #e2e8f0; }
        .notification-panel.show { display: block; }
        .notification-header { padding: 14px 16px; border-bottom: 1px solid #e2e8f0; display: flex; justify-content: space-between; align-items: center; background: #f8fafc; border-radius: 24px 24px 0 0; }
        .notification-header h4 { font-size: 14px; font-weight: 700; color: #1e293b; }
        .mark-all-btn { background: none; border: none; color: #3b82f6; font-size: 11px; font-weight: 600; cursor: pointer; }
        .notification-list { padding: 8px 0; }
        .notification-item { padding: 12px 16px; border-bottom: 1px solid #f1f5f9; cursor: pointer; transition: 0.2s; }
        .notification-item:hover { background: #f8fafc; }
        .notification-item.unread { background: #f0fdf4; border-left: 3px solid #2e7d32; }
        .notification-title { font-size: 13px; font-weight: 600; color: #1e293b; margin-bottom: 4px; }
        .notification-message { font-size: 11px; color: #64748b; margin-bottom: 4px; }
        .notification-time { font-size: 9px; color: #94a3b8; }
        .empty-notifications { text-align: center; padding: 40px 20px; color: #64748b; }
        
        .proof-detail-modal .modal-content { max-width: 500px; }
        .proof-text-box { background: #f8fafc; padding: 16px; border-radius: 16px; font-size: 13px; line-height: 1.5; color: #1e293b; margin-bottom: 16px; word-break: break-word; }
        .proof-image-box { text-align: center; margin-bottom: 16px; }
        .proof-image-box img { max-width: 100%; max-height: 300px; border-radius: 16px; border: 1px solid #e2e8f0; cursor: pointer; }
        .copy-btn { background: #e2e8f0; border: none; padding: 8px 12px; border-radius: 12px; font-size: 11px; font-weight: 600; cursor: pointer; color: #1e293b; margin-top: 8px; transition: 0.2s; }
        .copy-btn:hover { background: #cbd5e1; }
        
        .btn-primary { width: 100%; padding: 14px; background: #2e7d32; color: white; border: none; border-radius: 14px; font-weight: 700; cursor: pointer; margin: 8px 0; font-family: inherit; font-size: 14px; transition: 0.2s; }
        .btn-primary:hover { background: #1b5e20; }
        .btn-cancel { background: #64748b; }
        .btn-cancel:hover { background: #475569; }
        .btn-danger { background: #ef4444; }
        .btn-danger:hover { background: #dc2626; }
        
        .modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 5000; justify-content: center; align-items: center; padding: 16px; }
        .modal-content { background: white; border-radius: 28px; padding: 24px; width: 100%; max-width: 500px; max-height: 85vh; overflow-y: auto; }
        .modal-content h3 { font-size: 18px; color: #1b5e20; margin-bottom: 16px; font-weight: 800; }
        .input-field { width: 100%; padding: 12px 14px; border: 1.5px solid #e2e8f0; border-radius: 14px; margin-bottom: 12px; font-size: 14px; font-family: inherit; color: #1e293b; background: white; }
        .input-field:focus { outline: none; border-color: #2e7d32; }
        textarea.input-field { resize: vertical; font-family: inherit; }
        
        .image-upload-label { display: block; background: #f0fdf4; border: 2px dashed #2e7d32; border-radius: 16px; padding: 16px; text-align: center; cursor: pointer; margin: 10px 0; font-size: 13px; font-weight: 600; color: #2e7d32; }
        .image-upload-label:hover { background: #dcfce7; }
        .file-input { display: none; }
        .image-preview { text-align: center; margin: 10px 0; }
        .screenshot-preview { max-width: 100%; max-height: 150px; border-radius: 12px; border: 2px solid #2e7d32; }
        
        .notification-toast { position: fixed; top: 16px; right: 16px; padding: 12px 20px; border-radius: 30px; z-index: 9999; color: white; font-weight: 600; font-size: 13px; animation: slideIn 0.3s; }
        .notification-toast.success { background: #2e7d32; }
        .notification-toast.error { background: #ef4444; }
        @keyframes slideIn { from { transform: translateX(100%); opacity: 0; } to { transform: translateX(0); opacity: 1; } }
        
        .empty-state { text-align: center; padding: 50px 20px; color: #64748b; background: white; border-radius: 24px; margin: 10px 0; }
        .empty-state i { font-size: 48px; margin-bottom: 12px; opacity: 0.5; }
        
        .profile-card { background: white; border-radius: 24px; padding: 18px; display: flex; gap: 14px; margin: 12px 0; align-items: center; }
        .profile-pic { width: 60px; height: 60px; border-radius: 50%; background: linear-gradient(135deg, #2e7d32, #4caf50); display: flex; align-items: center; justify-content: center; font-size: 28px; color: white; }
        .stats-row { display: flex; gap: 10px; margin-top: 15px; flex-wrap: wrap; }
        .stat-item { flex: 1; text-align: center; background: white; border-radius: 18px; padding: 14px; }
        .stat-value { font-size: 22px; font-weight: 800; color: #2e7d32; }
        .stat-label { font-size: 10px; color: #64748b; }
        
        .social-strip { display: flex; justify-content: space-around; background: white; border-radius: 40px; padding: 12px 16px; margin: 12px 0; }
        .social-icon { width: 45px; height: 45px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 22px; color: white; cursor: pointer; transition: 0.2s; }
        .social-icon:hover { transform: scale(1.1); }
        .telegram { background: #0088cc; }
        .youtube { background: #ff0000; }
        .facebook { background: #1877f2; }
        .instagram { background: linear-gradient(45deg, #f09433, #d62976, #962fbf); }
        .support-btn { background: #2e7d32; color: white; padding: 14px; border-radius: 40px; width: 100%; border: none; margin: 8px 0; cursor: pointer; font-weight: 700; transition: 0.2s; }
        .support-btn:hover { background: #1b5e20; }
        
        .ref-card { background: white; border-radius: 24px; padding: 24px; text-align: center; margin: 10px 0; }
        .ref-link-box { background: #f0fdf4; border: 1.5px dashed #2e7d32; border-radius: 16px; padding: 12px 14px; margin: 15px 0; display: flex; justify-content: space-between; align-items: center; }
        .copy-icon { cursor: pointer; color: #2e7d32; padding: 6px 14px; background: white; border-radius: 30px; transition: 0.2s; }
        .copy-icon:hover { background: #dcfce7; }
        
        .tab-bar { display: flex; gap: 8px; margin-bottom: 16px; background: white; padding: 6px; border-radius: 50px; }
        .tab-btn { flex: 1; padding: 12px 8px; border: none; border-radius: 40px; font-size: 12px; font-weight: 600; cursor: pointer; background: transparent; color: #64748b; }
        .tab-btn.active { background: #2e7d32; color: white; }
        
        .fee-info { background: #fef3c7; padding: 12px; border-radius: 14px; margin: 10px 0; font-size: 12px; color: #d97706; }
        .total-display { background: #f0fdf4; padding: 14px; border-radius: 14px; margin: 10px 0; text-align: center; font-weight: 800; }
        .review-notice { background: #fef3c7; border: 1px solid #f59e0b; border-radius: 14px; padding: 12px; margin: 10px 0; font-size: 11px; color: #d97706; text-align: center; }
        .dropdown-menu { position: absolute; top: 50px; right: 12px; background: white; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.15); display: none; z-index: 200; min-width: 180px; overflow: hidden; }
        .dropdown-menu div { padding: 12px 18px; cursor: pointer; display: flex; align-items: center; gap: 10px; }
        .dropdown-menu div:hover { background: #f0fdf4; }
        .admin-badge { background: #8b5cf6; color: white; font-size: 9px; padding: 3px 10px; border-radius: 30px; margin-left: 8px; }
        .method-selector { display: flex; gap: 12px; margin-bottom: 16px; }
        .method-btn { flex: 1; padding: 12px; border: 2px solid #e2e8f0; border-radius: 16px; cursor: pointer; font-weight: 700; background: white; }
        .method-btn.active { border-color: #2e7d32; background: #f0fdf4; color: #2e7d32; }
        
        /* Limit info text */
        .limit-info { font-size: 10px; color: #64748b; margin-top: 4px; display: block; text-align: center; }
        .limit-note { font-size: 10px; color: #64748b; margin-top: 2px; }
        
        @media (max-width: 480px) {
            .action-btn { padding: 5px 10px; font-size: 10px; }
            .task-title-text { font-size: 13px; }
            .notification-panel { left: 10px; right: 10px; max-width: none; }
        }
    </style>
</head>
<body>
    <div id="loginPage" class="auth-container">
        <div class="auth-card">
            <h2>🚀 UniTask</h2>
            <div class="subtitle">Login to your account</div>
            <div id="loginError" class="error-msg"></div>
            <div class="input-group"><label>Email</label><input type="email" id="loginEmail" placeholder="Enter your email"></div>
            <div class="input-group"><label>Password</label><input type="password" id="loginPassword" placeholder="Enter your password"></div>
            <button class="auth-btn" onclick="window.handleLogin()">Login</button>
            <div class="auth-link">Don't have an account? <a onclick="window.showRegister()">Register</a><br><a onclick="window.showForgotPassword()">Forgot Password?</a></div>
        </div>
    </div>
    
    <div id="registerPage" class="auth-container" style="display:none;">
        <div class="auth-card">
            <h2>🚀 UniTask</h2>
            <div class="subtitle">Create a new account</div>
            <div id="registerError" class="error-msg"></div>
            <div id="registerSuccess" class="success-msg"></div>
            <div class="input-group"><label>Full Name</label><input type="text" id="registerName" placeholder="Your full name"></div>
            <div class="input-group"><label>Email</label><input type="email" id="registerEmail" placeholder="Enter your email"></div>
            <div class="input-group"><label>Username</label><input type="text" id="registerUsername" placeholder="Choose a username"></div>
            <div class="input-group"><label>Password</label><input type="password" id="registerPassword" placeholder="Create a password (min 6 chars)"></div>
            <div class="input-group"><label>Referral Code (Optional)</label><input type="text" id="referralCode" placeholder="Enter referral code"></div>
            <button class="auth-btn" onclick="window.handleRegister()">Register</button>
            <div class="auth-link">Already have an account? <a onclick="window.showLogin()">Login</a></div>
        </div>
    </div>
    
    <div id="forgotPage" class="auth-container" style="display:none;">
        <div class="auth-card">
            <h2>🚀 UniTask</h2>
            <div class="subtitle">Reset your password</div>
            <div id="forgotError" class="error-msg"></div>
            <div id="forgotSuccess" class="success-msg"></div>
            <div class="input-group"><label>Email</label><input type="email" id="resetEmail" placeholder="Enter your email"></div>
            <button class="auth-btn" onclick="window.handleForgotPassword()">Send Reset Link</button>
            <div class="auth-link"><a onclick="window.showLogin()">Back to Login</a></div>
        </div>
    </div>
    
    <div id="mainApp" class="user-view">
        <div class="mini-header">
            <div class="logo-small">🚀 UniTask</div>
            <div class="header-right">
                <select class="language-selector" id="languageSelect" onchange="window.changeLanguage(this.value)">
                    <option value="en">EN</option>
                    <option value="bn">বাংলা</option>
                </select>
                <div class="notification-wrapper" id="notificationBell">
                    <i class="fas fa-bell notification-icon"></i>
                    <span class="notification-badge" id="notificationBadge" style="display:none;">0</span>
                </div>
                <i class="fas fa-bars settings-icon" id="settingsIcon" style="cursor:pointer;"></i>
                <button class="logout-btn" onclick="window.handleLogout()"><i class="fas fa-sign-out-alt"></i></button>
            </div>
        </div>
        <div id="homePage" class="page active"></div>
        <div id="tasksPage" class="page"></div>
        <div id="sharePage" class="page"></div>
        <div id="profilePage" class="page"></div>
        <div class="bottom-nav">
            <div class="nav-item active" data-page="home"><i class="fas fa-home"></i><span id="navHome">Home</span></div>
            <div class="nav-item" data-page="tasks"><i class="fas fa-tasks"></i><span id="navTask">Tasks</span></div>
            <div class="nav-item" data-page="share"><i class="fas fa-share-alt"></i><span id="navShare">Refer</span></div>
            <div class="nav-item" data-page="profile"><i class="fas fa-user"></i><span id="navProfile">Profile</span></div>
        </div>
    </div>
    
    <div class="notification-panel" id="notificationPanel">
        <div class="notification-header">
            <h4><i class="fas fa-bell"></i> Notifications</h4>
            <button class="mark-all-btn" onclick="window.markAllNotificationsRead()">Mark all read</button>
        </div>
        <div class="notification-list" id="notificationList">
            <div class="empty-notifications">No notifications</div>
        </div>
    </div>
    
    <div class="modal-overlay" id="submitProofModal">
        <div class="modal-content">
            <h3 id="modalTaskTitle">📤 Submit Work</h3>
            <div id="modalTaskDesc" style="background:#f8fafc; padding:12px; border-radius:14px; margin-bottom:16px; font-size:12px; color:#475569;"></div>
            <div class="proof-section">
                <label class="proof-label" style="font-weight:600; font-size:13px; display:block; margin-bottom:6px;"><i class="fas fa-pencil-alt"></i> Description / Proof Link</label>
                <textarea id="proofText" class="input-field" rows="3" placeholder="Write your proof description, provide a link, or explain your work..."></textarea>
            </div>
            <div class="proof-section">
                <label class="proof-label" style="font-weight:600; font-size:13px; display:block; margin-bottom:6px;"><i class="fas fa-camera"></i> Upload Screenshot</label>
                <label class="image-upload-label" id="screenshotLabel" for="screenshotInput"><i class="fas fa-image"></i> Click to Select Image</label>
                <input type="file" id="screenshotInput" class="file-input" accept="image/*" onchange="window.previewScreenshot(this)">
                <div id="screenshotPreview" class="image-preview"></div>
            </div>
            <button class="btn-primary" id="submitWorkBtn" onclick="window.submitWorkFromModal()">✅ Submit Work</button>
            <button class="btn-primary btn-cancel" onclick="window.closeModal('submitProofModal')">Cancel</button>
        </div>
    </div>
    
    <div class="modal-overlay" id="submissionsModal">
        <div class="modal-content" style="max-width: 600px;">
            <h3 id="submissionsModalTitle">📋 Submissions</h3>
            <div id="submissionsListContainer" style="overflow-x: auto;"></div>
            <button class="btn-primary btn-cancel" onclick="window.closeModal('submissionsModal')">Close</button>
        </div>
    </div>
    
    <div class="modal-overlay proof-detail-modal" id="proofDetailModal">
        <div class="modal-content">
            <h3 id="proofDetailTitle">📄 Proof Details</h3>
            <div id="proofDetailContent"></div>
            <button class="btn-primary btn-cancel" onclick="window.closeModal('proofDetailModal')">Close</button>
        </div>
    </div>
    
    <div class="modal-overlay" id="increaseJobModal">
        <div class="modal-content">
            <h3>➕ Increase Job Workers</h3>
            <p style="margin-bottom:12px;">Add more worker slots to this task</p>
            <input type="number" id="increaseWorkersCount" class="input-field" placeholder="Additional workers needed" min="1">
            <button class="btn-primary" onclick="window.confirmIncreaseWorkers()">Increase Workers</button>
            <button class="btn-primary btn-cancel" onclick="window.closeModal('increaseJobModal')">Cancel</button>
        </div>
    </div>
    
    <div class="modal-overlay" id="deleteTaskModal">
        <div class="modal-content">
            <h3>⚠️ Delete Task</h3>
            <p id="deleteTaskInfo" style="margin-bottom:16px;"></p>
            <p style="background:#fef3c7; padding:12px; border-radius:12px; font-size:12px; margin-bottom:16px;">
                <i class="fas fa-info-circle"></i> Platform fee will be kept. Remaining balance will be refunded to your deposit.
            </p>
            <button class="btn-primary btn-danger" onclick="window.confirmDeleteTask()">Confirm Delete</button>
            <button class="btn-primary btn-cancel" onclick="window.closeModal('deleteTaskModal')">Cancel</button>
        </div>
    </div>
    
    <!-- Deposit Modal with Limit Info -->
    <div class="modal-overlay" id="depositModal">
        <div class="modal-content">
            <h3>💰 Add Deposit</h3>
            <div class="method-selector">
                <button class="method-btn active" id="methodBkash" onclick="window.selectDepositMethod('bkash')">📱 bKash</button>
                <button class="method-btn" id="methodNagad" onclick="window.selectDepositMethod('nagad')">📱 Nagad</button>
            </div>
            <div style="background:#f0fdf4; padding:14px; border-radius:14px; margin:10px 0; text-align:center;">Send to: <strong id="depositNumber">01798792581</strong></div>
            <input type="text" id="depositTrxId" class="input-field" placeholder="Transaction ID">
            <input type="text" id="depositFromAccount" class="input-field" placeholder="Your Account Number">
            <input type="number" id="depositAmount" class="input-field" placeholder="Amount (BDT)" min="1">
            <span id="depositMinMsg" class="limit-info" style="color:#dc2626; display:none;"></span>
            <span id="depositLimitInfo" class="limit-info">💰 Minimum deposit: ৳<span id="minDepositValue">50</span></span>
            <button class="btn-primary" onclick="window.addDeposit()">Submit Deposit Request</button>
            <button class="btn-primary btn-cancel" onclick="window.closeModal('depositModal')">Cancel</button>
        </div>
    </div>
    
    <!-- Withdraw Modal with Limit Info -->
    <div class="modal-overlay" id="withdrawModal">
        <div class="modal-content">
            <h3>💸 Withdraw Income</h3>
            <div class="method-selector">
                <button class="method-btn active" id="wMethodBkash" onclick="window.selectWithdrawMethod('bkash')">📱 bKash</button>
                <button class="method-btn" id="wMethodNagad" onclick="window.selectWithdrawMethod('nagad')">📱 Nagad</button>
            </div>
            <input type="text" id="withdrawAccount" class="input-field" placeholder="Account Number">
            <input type="number" id="withdrawAmount" class="input-field" placeholder="Amount (BDT)" min="1">
            <span id="withdrawMinMsg" class="limit-info" style="color:#dc2626; display:none;"></span>
            <span id="withdrawLimitInfo" class="limit-info">💸 Minimum withdrawal: ৳<span id="minWithdrawValue">200</span></span>
            <p style="font-size:11px; color:#64748b; text-align:center; margin-top:5px;">Available: ৳<span id="withdrawAvail">0</span></p>
            <button class="btn-primary" onclick="window.submitWithdraw()">Submit Request</button>
            <button class="btn-primary btn-cancel" onclick="window.closeModal('withdrawModal')">Cancel</button>
        </div>
    </div>
    
    <div class="modal-overlay" id="editProfileModal"><div class="modal-content"><h3>✏️ Edit Profile</h3><input type="text" id="editName" class="input-field" placeholder="Full Name"><input type="text" id="editUsername" class="input-field" placeholder="Username"><input type="password" id="editPassword" class="input-field" placeholder="New Password (optional)"><button class="btn-primary" onclick="window.saveProfile()">Save Changes</button><button class="btn-primary btn-cancel" onclick="window.closeModal('editProfileModal')">Cancel</button></div></div>
    <div class="dropdown-menu" id="profileMenu"><div onclick="window.openEditProfile()"><i class="fas fa-user-edit"></i> Edit Profile</div><div onclick="window.openDepositModal()"><i class="fas fa-plus-circle"></i> Add Deposit</div><div onclick="window.openWithdrawModal()"><i class="fas fa-arrow-up"></i> Withdraw</div><div onclick="window.showAbout()"><i class="fas fa-info-circle"></i> About</div></div>
    
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged, sendPasswordResetEmail } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";
        import { getFirestore, collection, doc, getDocs, addDoc, updateDoc, deleteDoc, query, where, getDoc, setDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";
        import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-storage.js";
        
        const firebaseConfig = {
            apiKey: "AIzaSyDp5ptxuQaZ8xMSDu4ZlRJ0P3UV5TQD3fE",
            authDomain: "uni-da9b5.firebaseapp.com",
            projectId: "uni-da9b5",
            storageBucket: "uni-da9b5.firebasestorage.app",
            messagingSenderId: "828115344512",
            appId: "1:828115344512:web:aa1cdb6e6b52567a8b9a65"
        };
        
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        const storage = getStorage(app);
        
        let currentUser = null;
        let tasks = [];
        let homeJobs = [];
        let submissions = [];
        let notifications = [];
        let withdrawals = [];
        let currentLanguage = 'en';
        let activeTaskTab = 'browse';
        let depositMethod = 'bkash';
        let withdrawMethod = 'bkash';
        let isPosting = false;
        let realtimeUnsubs = [];
        
        let currentTaskId = null;
        let currentIncreaseTaskId = null;
        let currentDeleteTaskId = null;
        let currentIsHomeJob = false;
        let selectedImageFile = null;
        
        // Network links
        let networkLinks = {
            youtube: 'https://youtube.com/@unitask',
            facebook: 'https://facebook.com/unitask',
            telegram: 'https://t.me/unitask2026',
            instagram: 'https://instagram.com/unitask',
            support: 'https://t.me/unitaskSupport'
        };
        
        let appSettings = {
            minWithdraw: 200,
            minDeposit: 50,
            minWorkers: 10,
            minBudgetPerPerson: 2,
            platformFee: 8,
            referralBonus: 2,
            referralCommissionPercent: 3,
            bkashNumber: '01798792581',
            nagadNumber: '01806213100'
        };
        
        const SITE_URL = "https://saimun2519.github.io/unitask/";
        
        const translations = {
            en: { navHome: 'Home', navTask: 'Tasks', navShare: 'Refer', navProfile: 'Profile', deposit: 'Deposit', income: 'Income', browse: 'Browse Tasks', myTasks: 'My Tasks', post: 'Post Task' },
            bn: { navHome: 'হোম', navTask: 'টাস্ক', navShare: 'রেফার', navProfile: 'প্রোফাইল', deposit: 'ডিপোজিট', income: 'ইনকাম', browse: 'ব্রাউজ টাস্ক', myTasks: 'আমার টাস্ক', post: 'টাস্ক পোস্ট' }
        };
        
        function t(key) { return translations[currentLanguage]?.[key] || translations.en[key] || key; }
        function formatBDT(amt) { return Number(amt || 0).toFixed(2); }
        function escapeHtml(str) { if (!str) return ''; return String(str).replace(/[&<>]/g, m => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;' }[m] || m)); }
        
        function showNotification(msg, type) {
            const existing = document.querySelector('.notification-toast');
            if (existing) existing.remove();
            const n = document.createElement('div');
            n.className = 'notification-toast ' + type;
            n.innerHTML = msg;
            document.body.appendChild(n);
            setTimeout(() => { if (n.parentNode) n.remove(); }, 3500);
        }
        
        window.copyToClipboard = async function(text, buttonElement) {
            try {
                await navigator.clipboard.writeText(text);
                const originalHtml = buttonElement.innerHTML;
                buttonElement.innerHTML = '<i class="fas fa-check"></i> Copied!';
                setTimeout(() => { buttonElement.innerHTML = originalHtml; }, 1500);
                showNotification('✅ Copied to clipboard!', 'success');
            } catch (err) {
                const textarea = document.createElement('textarea');
                textarea.value = text;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                const originalHtml = buttonElement.innerHTML;
                buttonElement.innerHTML = '<i class="fas fa-check"></i> Copied!';
                setTimeout(() => { buttonElement.innerHTML = originalHtml; }, 1500);
                showNotification('✅ Copied to clipboard!', 'success');
            }
        };
        
        window.closeModal = function(id) { 
            const modal = document.getElementById(id); 
            if (modal) modal.style.display = 'none';
            if (id === 'submitProofModal') {
                selectedImageFile = null;
                document.getElementById('screenshotPreview').innerHTML = '';
                document.getElementById('proofText').value = '';
                document.getElementById('screenshotInput').value = '';
            }
        };
        
        window.previewScreenshot = function(input) {
            const file = input.files[0];
            if (file) {
                selectedImageFile = file;
                const reader = new FileReader();
                reader.onload = function(e) {
                    const preview = document.getElementById('screenshotPreview');
                    if (preview) {
                        preview.innerHTML = `<img src="${e.target.result}" class="screenshot-preview" style="max-width:100%; max-height:150px; border-radius:12px;">`;
                    }
                };
                reader.readAsDataURL(file);
            }
        };
        
        window.selectDepositMethod = function(method) { 
            depositMethod = method; 
            document.getElementById('depositNumber').innerText = method === 'bkash' ? appSettings.bkashNumber : appSettings.nagadNumber;
            document.getElementById('methodBkash').classList.toggle('active', method === 'bkash'); 
            document.getElementById('methodNagad').classList.toggle('active', method === 'nagad'); 
        };
        
        window.selectWithdrawMethod = function(method) { 
            withdrawMethod = method; 
            document.getElementById('wMethodBkash').classList.toggle('active', method === 'bkash'); 
            document.getElementById('wMethodNagad').classList.toggle('active', method === 'nagad'); 
        };
        
        window.switchTaskTab = function(tab) { activeTaskTab = tab; renderTasks(); };
        window.showLogin = function() { document.getElementById('loginPage').style.display = 'flex'; document.getElementById('registerPage').style.display = 'none'; document.getElementById('forgotPage').style.display = 'none'; };
        window.showRegister = function() { document.getElementById('loginPage').style.display = 'none'; document.getElementById('registerPage').style.display = 'flex'; document.getElementById('forgotPage').style.display = 'none'; };
        window.showForgotPassword = function() { document.getElementById('loginPage').style.display = 'none'; document.getElementById('registerPage').style.display = 'none'; document.getElementById('forgotPage').style.display = 'flex'; };
        window.changeLanguage = function(lang) { currentLanguage = lang; document.getElementById('navHome').innerText = t('navHome'); document.getElementById('navTask').innerText = t('navTask'); document.getElementById('navShare').innerText = t('navShare'); document.getElementById('navProfile').innerText = t('navProfile'); refreshAllPages(); };
        window.showAbout = function() { alert('🚀 UniTask - Earn Money Online'); document.getElementById('profileMenu').style.display = 'none'; };
        
        window.toggleNotificationPanel = function() {
            const panel = document.getElementById('notificationPanel');
            panel.classList.toggle('show');
            if (panel.classList.contains('show')) { renderNotificationPanel(); }
        };
        
        function renderNotificationPanel() {
            const container = document.getElementById('notificationList');
            if (!notifications.length) {
                container.innerHTML = '<div class="empty-notifications"><i class="fas fa-bell-slash"></i><p>No notifications yet</p></div>';
                return;
            }
            let html = '';
            notifications.sort((a,b) => new Date(b.createdAt) - new Date(a.createdAt)).forEach(notif => {
                const unreadClass = !notif.read ? 'unread' : '';
                const date = notif.createdAt ? new Date(notif.createdAt).toLocaleString() : '';
                html += `<div class="notification-item ${unreadClass}" onclick="window.markNotificationRead('${notif.id}')"><div class="notification-title">${escapeHtml(notif.title || 'New Notification')}</div><div class="notification-message">${escapeHtml(notif.message || '')}</div><div class="notification-time">${date}</div></div>`;
            });
            container.innerHTML = html;
        }
        
        window.markNotificationRead = async function(notifId) {
            await updateDoc(doc(db, 'notifications', notifId), { read: true });
            await loadAllData();
        };
        
        window.markAllNotificationsRead = async function() {
            for (const notif of notifications.filter(n => !n.read)) {
                await updateDoc(doc(db, 'notifications', notif.id), { read: true });
            }
            await loadAllData();
            showNotification('All notifications marked as read', 'success');
        };
        
        window.viewFullProof = function(proofText, imageUrl, workerName, submittedAt) {
            let content = '';
            if (proofText) {
                content += `<div class="proof-text-box"><strong>📝 Proof Description:</strong><br>${escapeHtml(proofText)}</div><button class="copy-btn" onclick="copyToClipboard('${escapeHtml(proofText).replace(/'/g, "\\'")}', this)"><i class="fas fa-copy"></i> Copy Proof Text</button>`;
            }
            if (imageUrl) {
                content += `<div class="proof-image-box"><strong>🖼️ Screenshot:</strong><br><img src="${imageUrl}" alt="Proof Screenshot" onclick="window.open('${imageUrl}','_blank')"></div>`;
            }
            if (!proofText && !imageUrl) { content = '<div class="proof-text-box">No proof provided</div>'; }
            content += `<div style="margin-top:12px; font-size:11px; color:#64748b;">👤 Submitted by: ${escapeHtml(workerName)} | 📅 ${new Date(submittedAt).toLocaleString()}</div>`;
            document.getElementById('proofDetailTitle').innerHTML = '📄 Proof Details';
            document.getElementById('proofDetailContent').innerHTML = content;
            document.getElementById('proofDetailModal').style.display = 'flex';
        };
        
        window.copyReferLink = function(link, buttonElement) { copyToClipboard(link, buttonElement); };
        
        function hasUserSubmittedToUserTask(taskId) {
            const isOfficial = homeJobs.some(j => j.id === taskId);
            if (isOfficial) return false;
            return submissions.some(s => s.taskId === taskId && s.workerId === currentUser?.id);
        }
        
        function isTaskCompleted(task) {
            return (task.completedCount || 0) >= (task.totalWorkers || 1);
        }
        
        async function loadSettings() {
            try {
                const settingsDoc = await getDoc(doc(db, 'settings', 'appSettings'));
                if (settingsDoc.exists()) {
                    const s = settingsDoc.data();
                    appSettings = {
                        minWithdraw: s.minWithdraw || 200,
                        minDeposit: s.minDeposit || 50,
                        minWorkers: s.minWorkers || 10,
                        minBudgetPerPerson: s.minBudgetPerPerson || 2,
                        platformFee: s.platformFee || 8,
                        referralBonus: s.referralBonus || 2,
                        referralCommissionPercent: s.referralCommissionPercent || 3,
                        bkashNumber: s.bkashNumber || '01798792581',
                        nagadNumber: s.nagadNumber || '01806213100'
                    };
                }
                document.getElementById('minDepositValue').innerText = appSettings.minDeposit;
                document.getElementById('minWithdrawValue').innerText = appSettings.minWithdraw;
                document.getElementById('depositNumber').innerText = depositMethod === 'bkash' ? appSettings.bkashNumber : appSettings.nagadNumber;
            } catch(e) { console.log("Settings load error:", e); }
        }
        
        async function loadNetworks() {
            try {
                const networksDoc = await getDoc(doc(db, 'settings', 'networks'));
                if (networksDoc.exists()) {
                    const n = networksDoc.data();
                    networkLinks = {
                        youtube: n.youtube || 'https://youtube.com/@unitask',
                        facebook: n.facebook || 'https://facebook.com/unitask',
                        telegram: n.telegram || 'https://t.me/unitask2026',
                        instagram: n.instagram || 'https://instagram.com/unitask',
                        support: n.support || 'https://t.me/unitaskSupport'
                    };
                }
            } catch(e) { console.log("Networks load error:", e); }
        }
        
        window.handleLogin = async function() {
            const email = document.getElementById('loginEmail').value.trim();
            const password = document.getElementById('loginPassword').value;
            const errorDiv = document.getElementById('loginError');
            if (!email || !password) { errorDiv.style.display = 'block'; errorDiv.innerHTML = '⚠️ Please fill all fields'; return; }
            errorDiv.style.display = 'none';
            try {
                const userCredential = await signInWithEmailAndPassword(auth, email, password);
                const user = userCredential.user;
                const userDoc = await getDoc(doc(db, 'users', user.uid));
                if (userDoc.exists()) { currentUser = { id: user.uid, ...userDoc.data() }; }
                else { 
                    currentUser = { id: user.uid, email: user.email, name: user.email.split('@')[0], username: user.email.split('@')[0], depositBalance: 0, incomeBalance: 0, referrals: 0, referralEarnings: 0, totalReferralCommission: 0, referredBy: null, referralCode: user.uid.substring(0, 8) }; 
                    await setDoc(doc(db, 'users', user.uid), currentUser); 
                }
                document.getElementById('loginPage').style.display = 'none';
                document.getElementById('mainApp').style.display = 'block';
                await loadSettings();
                await loadNetworks();
                await loadAllData(); 
                startRealtimeListeners(); 
                refreshAllPages();
                showNotification('✅ Welcome, ' + currentUser.name + '!', 'success');
            } catch (error) { errorDiv.style.display = 'block'; errorDiv.innerHTML = '❌ ' + error.message; }
        };
        
        window.handleRegister = async function() {
            const name = document.getElementById('registerName').value.trim();
            const email = document.getElementById('registerEmail').value.trim();
            const username = document.getElementById('registerUsername').value.trim();
            const password = document.getElementById('registerPassword').value;
            const referralCode = document.getElementById('referralCode').value.trim();
            const errorDiv = document.getElementById('registerError');
            const successDiv = document.getElementById('registerSuccess');
            
            if (!name || !email || !username || !password) { errorDiv.style.display = 'block'; errorDiv.innerHTML = '⚠️ Please fill all fields'; return; }
            if (password.length < 6) { errorDiv.style.display = 'block'; errorDiv.innerHTML = '⚠️ Password must be at least 6 characters'; return; }
            errorDiv.style.display = 'none';
            
            try {
                const userCredential = await createUserWithEmailAndPassword(auth, email, password);
                const user = userCredential.user;
                const newReferralCode = user.uid.substring(0, 8);
                
                const userData = { id: user.uid, name, email, username, depositBalance: 0, incomeBalance: 0, referrals: 0, referralEarnings: 0, totalReferralCommission: 0, referralCode: newReferralCode, referredBy: null, createdAt: new Date().toISOString() };
                
                if (referralCode) {
                    const usersSnapshot = await getDocs(query(collection(db, 'users'), where('referralCode', '==', referralCode)));
                    if (!usersSnapshot.empty) {
                        const referrer = usersSnapshot.docs[0];
                        const referrerData = referrer.data();
                        const currentRefs = referrerData.referrals || 0;
                        const currentBonus = referrerData.referralEarnings || 0;
                        const currentDeposit = referrerData.depositBalance || 0;
                        await updateDoc(doc(db, 'users', referrer.id), { referrals: currentRefs + 1, referralEarnings: currentBonus + appSettings.referralBonus, depositBalance: currentDeposit + appSettings.referralBonus });
                        userData.referredBy = referrer.id;
                        await addDoc(collection(db, 'notifications'), { userId: referrer.id, title: '🎉 New Referral!', message: `${name} joined using your referral code! You earned ৳${appSettings.referralBonus} bonus!`, read: false, createdAt: new Date().toISOString() });
                    }
                }
                await setDoc(doc(db, 'users', user.uid), userData);
                successDiv.style.display = 'block'; successDiv.innerHTML = '✅ Account created! Redirecting to login...';
                setTimeout(() => { successDiv.style.display = 'none'; window.showLogin(); }, 2000);
            } catch (error) { errorDiv.style.display = 'block'; errorDiv.innerHTML = '❌ ' + error.message; }
        };
        
        window.handleForgotPassword = async function() {
            const email = document.getElementById('resetEmail').value.trim();
            const errorDiv = document.getElementById('forgotError'); const successDiv = document.getElementById('forgotSuccess');
            if (!email) { errorDiv.style.display = 'block'; errorDiv.innerHTML = '⚠️ Please enter your email'; return; }
            errorDiv.style.display = 'none';
            try { await sendPasswordResetEmail(auth, email); successDiv.style.display = 'block'; successDiv.innerHTML = '✅ Password reset link sent!'; }
            catch (error) { errorDiv.style.display = 'block'; errorDiv.innerHTML = '❌ ' + error.message; }
        };
        
        window.handleLogout = async function() {
            realtimeUnsubs.forEach(unsub => { try { unsub(); } catch(e) {} });
            realtimeUnsubs = [];
            await signOut(auth);
            document.getElementById('mainApp').style.display = 'none';
            document.getElementById('loginPage').style.display = 'flex';
            currentUser = null; showNotification('Logged out', 'success');
        };
        
        async function loadAllData() {
            if (!currentUser) return;
            try {
                const [tasksSnap, homeJobsSnap, subsSnap, notifSnap, userDoc, withSnap] = await Promise.all([
                    getDocs(collection(db, 'tasks')), getDocs(collection(db, 'homeJobs')), getDocs(collection(db, 'submissions')),
                    getDocs(query(collection(db, 'notifications'), where('userId', '==', currentUser.id))), getDoc(doc(db, 'users', currentUser.id)),
                    getDocs(query(collection(db, 'withdrawals'), where('userId', '==', currentUser.id)))
                ]);
                tasks = []; tasksSnap.forEach(d => tasks.push({ id: d.id, ...d.data() }));
                homeJobs = []; homeJobsSnap.forEach(d => homeJobs.push({ id: d.id, ...d.data() }));
                submissions = []; subsSnap.forEach(d => submissions.push({ id: d.id, ...d.data() }));
                notifications = []; notifSnap.forEach(d => notifications.push({ id: d.id, ...d.data() }));
                withdrawals = []; withSnap.forEach(d => withdrawals.push({ id: d.id, ...d.data() }));
                if (userDoc.exists()) currentUser = { id: currentUser.id, ...userDoc.data() };
                refreshAllPages();
            } catch(e) { console.error("Load error:", e); }
        }
        
        function startRealtimeListeners() {
            if (!currentUser) return;
            realtimeUnsubs.forEach(unsub => { try { unsub(); } catch(e) {} });
            realtimeUnsubs = [];
            let debounceTimer = null;
            const debouncedLoad = () => { clearTimeout(debounceTimer); debounceTimer = setTimeout(() => loadAllData(), 500); };
            realtimeUnsubs.push(onSnapshot(collection(db, 'tasks'), debouncedLoad));
            realtimeUnsubs.push(onSnapshot(collection(db, 'homeJobs'), debouncedLoad));
            realtimeUnsubs.push(onSnapshot(collection(db, 'submissions'), debouncedLoad));
            realtimeUnsubs.push(onSnapshot(doc(db, 'users', currentUser.id), debouncedLoad));
            realtimeUnsubs.push(onSnapshot(query(collection(db, 'notifications'), where('userId', '==', currentUser.id)), debouncedLoad));
            realtimeUnsubs.push(onSnapshot(query(collection(db, 'withdrawals'), where('userId', '==', currentUser.id)), debouncedLoad));
            realtimeUnsubs.push(onSnapshot(doc(db, 'settings', 'appSettings'), () => loadSettings()));
            realtimeUnsubs.push(onSnapshot(doc(db, 'settings', 'networks'), () => loadNetworks()));
        }
        
        function refreshAllPages() { renderHome(); renderTasks(); renderShare(); renderProfile(); updateBadge(); renderNotificationPanel(); }
        
        function updateBadge() { 
            const b = document.getElementById('notificationBadge'); 
            const n = notifications.filter(x => !x.read).length; 
            if (b) { 
                if (n > 0) { b.style.display = 'flex'; b.innerText = n > 99 ? '99+' : n; } 
                else { b.style.display = 'none'; } 
            } 
        }
        
        function hasPendingSubmission(taskId) { return submissions.some(s => s.taskId === taskId && s.workerId === currentUser?.id && s.status === 'pending'); }
        function hasCompletedTask(taskId) { return submissions.some(s => s.taskId === taskId && s.workerId === currentUser?.id && s.status === 'approved'); }
        
        window.openSubmitModal = function(taskId, isHomeJob = false) {
            const task = isHomeJob ? homeJobs.find(t => t.id === taskId) : tasks.find(t => t.id === taskId);
            if (!task) { showNotification('❌ Task not found!', 'error'); return; }
            if (!isHomeJob && hasUserSubmittedToUserTask(taskId)) { showNotification('⚠️ You have already submitted work for this task!', 'error'); return; }
            if (isTaskCompleted(task)) { showNotification('⚠️ This task is already completed!', 'error'); return; }
            currentTaskId = taskId;
            currentIsHomeJob = isHomeJob;
            document.getElementById('modalTaskTitle').innerHTML = `📤 Submit Work - ${escapeHtml(task.title)}`;
            document.getElementById('modalTaskDesc').innerHTML = `<strong>💰 Reward:</strong> ৳${formatBDT(task.budget)}<br><strong>📋 Description:</strong><br>${escapeHtml(task.description || 'No description')}`;
            document.getElementById('proofText').value = '';
            document.getElementById('screenshotPreview').innerHTML = '';
            selectedImageFile = null;
            document.getElementById('screenshotInput').value = '';
            document.getElementById('submitProofModal').style.display = 'flex';
        };
        
        window.submitWorkFromModal = async function() {
            const proof = document.getElementById('proofText').value.trim();
            if (!proof && !selectedImageFile) { showNotification('⚠️ Please provide a screenshot or description', 'error'); return; }
            const btn = document.getElementById('submitWorkBtn');
            if (btn) { btn.disabled = true; btn.innerHTML = '⏳ Submitting...'; }
            const task = currentIsHomeJob ? homeJobs.find(t => t.id === currentTaskId) : tasks.find(t => t.id === currentTaskId);
            if (!task) { showNotification('❌ Task not found!', 'error'); if (btn) { btn.disabled = false; btn.innerHTML = '✅ Submit Work'; } window.closeModal('submitProofModal'); return; }
            if (!currentIsHomeJob && hasUserSubmittedToUserTask(currentTaskId)) { showNotification('⚠️ You already submitted!', 'error'); if (btn) { btn.disabled = false; btn.innerHTML = '✅ Submit Work'; } window.closeModal('submitProofModal'); return; }
            let imageUrl = '';
            if (selectedImageFile) {
                try {
                    const storageRef = ref(storage, `submissions/${Date.now()}_${selectedImageFile.name}`);
                    await uploadBytes(storageRef, selectedImageFile);
                    imageUrl = await getDownloadURL(storageRef);
                } catch(e) { showNotification('Image upload failed', 'error'); if (btn) { btn.disabled = false; btn.innerHTML = '✅ Submit Work'; } return; }
            }
            try {
                const newCompletedCount = (task.completedCount || 0) + 1;
                const isComplete = newCompletedCount >= (task.totalWorkers || 1);
                if (currentIsHomeJob) {
                    await updateDoc(doc(db, 'homeJobs', currentTaskId), { completedCount: newCompletedCount, status: isComplete ? 'completed' : 'open' });
                } else {
                    await updateDoc(doc(db, 'tasks', currentTaskId), { completedCount: newCompletedCount, status: isComplete ? 'completed' : 'open' });
                }
                await addDoc(collection(db, 'submissions'), {
                    taskId: task.id, taskTitle: task.title, workerId: currentUser.id, workerName: currentUser.name,
                    textProof: proof, imageUrl: imageUrl, budget: task.budget, isHomeJob: currentIsHomeJob,
                    status: 'pending', submittedAt: new Date().toISOString()
                });
                if (!currentIsHomeJob && task.postedBy && task.postedBy !== currentUser.id) {
                    await addDoc(collection(db, 'notifications'), { userId: task.postedBy, title: 'New Submission', message: `${currentUser.name} submitted work for "${task.title}"`, read: false, createdAt: new Date().toISOString() });
                }
                showNotification('✅ Work submitted! Waiting for admin approval.', 'success');
                window.closeModal('submitProofModal');
                await loadAllData();
            } catch(e) { showNotification('Error: ' + e.message, 'error'); } finally { if (btn) { btn.disabled = false; btn.innerHTML = '✅ Submit Work'; } }
        };
        
        window.viewSubmissions = async function(taskId) {
            const taskSubmissions = submissions.filter(s => s.taskId === taskId);
            const task = tasks.find(t => t.id === taskId);
            if (!taskSubmissions.length) {
                document.getElementById('submissionsModalTitle').innerHTML = `📋 Submissions for "${task?.title || 'Task'}"`;
                document.getElementById('submissionsListContainer').innerHTML = '<div class="empty-state">No submissions yet</div>';
                document.getElementById('submissionsModal').style.display = 'flex';
                return;
            }
            let tableHtml = `<table class="submissions-table"><thead><tr><th>ID</th><th>Worker</th><th>Proof</th><th>Submitted</th><th>Status</th><th>Action</th></table></thead><tbody>`;
            taskSubmissions.forEach(sub => {
                const proofHtml = sub.textProof ? `<div>📝 <span class="proof-link" onclick="window.viewFullProof('${escapeHtml(sub.textProof).replace(/'/g, "\\'")}', '${sub.imageUrl || ''}', '${escapeHtml(sub.workerName)}', '${sub.submittedAt}')">Click to view</span></div>` : '';
                const imageHtml = sub.imageUrl ? `<div>🖼️ <span class="proof-link" onclick="window.viewFullProof('${escapeHtml(sub.textProof || '').replace(/'/g, "\\'")}', '${sub.imageUrl}', '${escapeHtml(sub.workerName)}', '${sub.submittedAt}')">View Image</span></div>` : '';
                const date = sub.submittedAt ? new Date(sub.submittedAt).toLocaleDateString() : '-';
                let statusBadge = '';
                if (sub.status === 'pending') statusBadge = '<span class="badge-pending">Pending</span>';
                else if (sub.status === 'approved') statusBadge = '<span class="badge-approved">Approved</span>';
                else if (sub.status === 'rejected') statusBadge = '<span class="badge-rejected">Rejected</span>';
                tableHtml += `<tr><td>${sub.id.slice(-6)}</td><td>${escapeHtml(sub.workerName || '-')}</td><td>${proofHtml} ${imageHtml}</td><td>${date}</td><td>${statusBadge}</td><td>${sub.status === 'pending' ? `<button class="action-btn approve" onclick="window.approveSubmission('${sub.id}', ${sub.budget}, '${sub.workerId}')" style="padding:4px 8px; font-size:10px;">✅</button><button class="action-btn reject" onclick="window.rejectSubmission('${sub.id}')" style="padding:4px 8px; font-size:10px;">❌</button>` : '-'}</td></tr>`;
            });
            tableHtml += `</tbody></table>`;
            document.getElementById('submissionsModalTitle').innerHTML = `📋 Submissions for "${task?.title || 'Task'}"`;
            document.getElementById('submissionsListContainer').innerHTML = tableHtml;
            document.getElementById('submissionsModal').style.display = 'flex';
        };
        
        window.approveSubmission = async function(subId, budget, workerId) {
            try {
                await updateDoc(doc(db, 'submissions', subId), { status: 'approved' });
                if (workerId && budget > 0) {
                    const userRef = doc(db, 'users', workerId);
                    const userDoc = await getDoc(userRef);
                    if (userDoc.exists()) {
                        const currentIncome = userDoc.data().incomeBalance || 0;
                        await updateDoc(userRef, { incomeBalance: currentIncome + budget });
                        const referredBy = userDoc.data().referredBy;
                        if (referredBy) {
                            const referrerRef = doc(db, 'users', referredBy);
                            const referrerDoc = await getDoc(referrerRef);
                            if (referrerDoc.exists()) {
                                const commission = budget * (appSettings.referralCommissionPercent / 100);
                                const currentCommission = referrerDoc.data().totalReferralCommission || 0;
                                const currentDeposit = referrerDoc.data().depositBalance || 0;
                                const currentEarnings = referrerDoc.data().referralEarnings || 0;
                                await updateDoc(referrerRef, { totalReferralCommission: currentCommission + commission, depositBalance: currentDeposit + commission, referralEarnings: currentEarnings + commission });
                                await addDoc(collection(db, 'notifications'), { userId: referredBy, title: '💰 Referral Commission!', message: `You earned ৳${formatBDT(commission)} (${appSettings.referralCommissionPercent}%) from your referral's work!`, read: false, createdAt: new Date().toISOString() });
                            }
                        }
                    }
                }
                showNotification('✅ Submission approved! Payment + referral commission sent.', 'success');
                await loadAllData();
            } catch(e) { showNotification('Error: ' + e.message, 'error'); }
        };
        
        window.rejectSubmission = async function(subId) {
            try {
                const subDoc = await getDoc(doc(db, 'submissions', subId));
                const sub = subDoc.data();
                await updateDoc(doc(db, 'submissions', subId), { status: 'rejected' });
                if (sub && sub.workerId) {
                    await addDoc(collection(db, 'notifications'), { userId: sub.workerId, title: 'Submission Rejected', message: `Your submission for "${sub.taskTitle}" was rejected.`, read: false, createdAt: new Date().toISOString() });
                }
                showNotification('❌ Submission rejected', 'success');
                await loadAllData();
            } catch(e) { showNotification('Error: ' + e.message, 'error'); }
        };
        
        window.openIncreaseModal = function(taskId) {
            const task = tasks.find(t => t.id === taskId);
            if (!task) { showNotification('❌ Task not found!', 'error'); return; }
            currentIncreaseTaskId = taskId;
            document.getElementById('increaseWorkersCount').value = '';
            document.getElementById('increaseJobModal').style.display = 'flex';
        };
        
        window.confirmIncreaseWorkers = async function() {
            const additional = parseInt(document.getElementById('increaseWorkersCount').value);
            if (!additional || additional < 1) { showNotification('Enter valid number', 'error'); return; }
            const task = tasks.find(t => t.id === currentIncreaseTaskId);
            if (!task) { showNotification('Task not found!', 'error'); window.closeModal('increaseJobModal'); return; }
            try {
                await updateDoc(doc(db, 'tasks', currentIncreaseTaskId), { totalWorkers: (task.totalWorkers || 0) + additional });
                showNotification(`✅ Added ${additional} more worker slots!`, 'success');
                window.closeModal('increaseJobModal');
                await loadAllData();
            } catch(e) { showNotification('Error: ' + e.message, 'error'); }
        };
        
        window.openDeleteTaskModal = function(taskId) {
            const task = tasks.find(t => t.id === taskId);
            if (!task) return;
            currentDeleteTaskId = taskId;
            const totalPaid = (task.budget || 0) * (task.completedCount || 0);
            const platformFeeKept = totalPaid * (appSettings.platformFee / 100);
            const totalCost = (task.budget || 0) * (task.totalWorkers || 1);
            const totalWithFee = totalCost * (1 + (appSettings.platformFee / 100));
            const refundAmount = totalWithFee - totalPaid;
            document.getElementById('deleteTaskInfo').innerHTML = `<strong>${escapeHtml(task.title)}</strong><br>📊 Total Workers: ${task.totalWorkers || 1}<br>✅ Completed: ${task.completedCount || 0}<br>💰 Paid to workers: ৳${formatBDT(totalPaid)}<br>📈 Platform fee kept: ৳${formatBDT(platformFeeKept)}<br>🔄 Refund amount: ৳${formatBDT(refundAmount)}`;
            document.getElementById('deleteTaskModal').style.display = 'flex';
        };
        
        window.confirmDeleteTask = async function() {
            const task = tasks.find(t => t.id === currentDeleteTaskId);
            if (!task) { showNotification('Task not found', 'error'); window.closeModal('deleteTaskModal'); return; }
            try {
                const totalPaid = (task.budget || 0) * (task.completedCount || 0);
                const totalCost = (task.budget || 0) * (task.totalWorkers || 1);
                const totalWithFee = totalCost * (1 + (appSettings.platformFee / 100));
                const refundAmount = totalWithFee - totalPaid;
                if (refundAmount > 0) {
                    const currentBalance = currentUser.depositBalance || 0;
                    await updateDoc(doc(db, 'users', currentUser.id), { depositBalance: currentBalance + refundAmount });
                }
                await deleteDoc(doc(db, 'tasks', currentDeleteTaskId));
                showNotification(`✅ Task deleted! Refunded ৳${formatBDT(refundAmount)} to your deposit.`, 'success');
                window.closeModal('deleteTaskModal');
                await loadAllData();
                renderTasks();
            } catch(e) { showNotification('Error: ' + e.message, 'error'); }
        };
        
        window.pauseJob = async function(taskId) { try { await updateDoc(doc(db, 'tasks', taskId), { status: 'paused' }); showNotification('Job paused', 'success'); await loadAllData(); } catch(e) { showNotification('Error: ' + e.message, 'error'); } };
        window.resumeJob = async function(taskId) { try { await updateDoc(doc(db, 'tasks', taskId), { status: 'open' }); showNotification('Job resumed', 'success'); await loadAllData(); } catch(e) { showNotification('Error: ' + e.message, 'error'); } };
        
        window.submitWithdraw = async function() {
            const account = document.getElementById('withdrawAccount')?.value?.trim() || '';
            const amount = parseFloat(document.getElementById('withdrawAmount')?.value) || 0;
            const msgSpan = document.getElementById('withdrawMinMsg');
            if (!account || !amount) { showNotification('⚠️ Fill all fields', 'error'); return; }
            if (amount < appSettings.minWithdraw) { msgSpan.style.display = 'block'; msgSpan.innerText = `⚠️ Minimum withdrawal is ৳${appSettings.minWithdraw}`; setTimeout(() => msgSpan.style.display = 'none', 3000); return; }
            if (amount > (currentUser.incomeBalance || 0)) { showNotification('⚠️ Insufficient balance', 'error'); return; }
            await addDoc(collection(db, 'withdrawals'), { userId: currentUser.id, userName: currentUser.name, amount, account, method: withdrawMethod, status: 'pending', requestedAt: new Date().toISOString() });
            showNotification('✅ Withdraw request submitted! Admin will review.', 'success');
            window.closeModal('withdrawModal');
        };
        
        window.addDeposit = async function() {
            const trx = document.getElementById('depositTrxId')?.value?.trim() || '';
            const from = document.getElementById('depositFromAccount')?.value?.trim() || '';
            const amount = parseFloat(document.getElementById('depositAmount')?.value) || 0;
            const msgSpan = document.getElementById('depositMinMsg');
            if (!trx || !from || !amount) { showNotification('⚠️ Fill all fields', 'error'); return; }
            if (amount < appSettings.minDeposit) { msgSpan.style.display = 'block'; msgSpan.innerText = `⚠️ Minimum deposit is ৳${appSettings.minDeposit}`; setTimeout(() => msgSpan.style.display = 'none', 3000); return; }
            await addDoc(collection(db, 'deposits'), { userId: currentUser.id, userName: currentUser.name, amount, transactionId: trx, fromAccount: from, method: depositMethod, status: 'pending', createdAt: new Date().toISOString() });
            showNotification('✅ Deposit request submitted!', 'success');
            window.closeModal('depositModal');
        };
        
        function renderHome() {
            const container = document.getElementById('homePage'); if (!currentUser) return;
            let html = `<div class="balance-header"><div class="balance-card"><div class="label">💰 ${t('deposit')}</div><div class="amount">৳${formatBDT(currentUser.depositBalance)}</div></div><div class="balance-card income"><div class="label">💵 ${t('income')}</div><div class="amount">৳${formatBDT(currentUser.incomeBalance)}</div></div></div><div class="section-title"><span>🏢 Official Tasks</span><span class="unlimited-badge"><i class="fas fa-infinity"></i> Unlimited (Can do multiple times)</span></div>`;
            const openJobs = homeJobs.filter(j => j.status === 'open');
            if (openJobs.length > 0) { html += `<div class="jobs-grid">`; openJobs.forEach(job => { const completed = job.completedCount || 0; const total = job.totalWorkers || 1; const pct = Math.min((completed / total) * 100, 100); html += `<div class="job-card" onclick="window.openSubmitModal('${job.id}', true)"><div class="job-reward">৳${formatBDT(job.budget)}</div><div class="job-title">${escapeHtml(job.title)}</div><div class="progress-container"><div class="progress-bar" style="width: ${pct}%;"></div></div><div class="progress-stats"><span>✅ ${completed} done</span><span>👥 ${completed}/${total}</span></div><div class="submit-badge">📤 Submit Work</div></div>`; }); html += `</div>`; }
            else { html += `<div class="empty-state"><i class="fas fa-folder-open"></i><p>No official tasks available</p></div>`; }
            html += `<div class="section-title">📱 Official Channels</div><div class="social-strip"><div class="social-icon telegram" onclick="window.open('${networkLinks.telegram}','_blank')"><i class="fab fa-telegram"></i></div><div class="social-icon youtube" onclick="window.open('${networkLinks.youtube}','_blank')"><i class="fab fa-youtube"></i></div><div class="social-icon facebook" onclick="window.open('${networkLinks.facebook}','_blank')"><i class="fab fa-facebook"></i></div><div class="social-icon instagram" onclick="window.open('${networkLinks.instagram}','_blank')"><i class="fab fa-instagram"></i></div></div><button class="support-btn" onclick="window.open('${networkLinks.support}','_blank')"><i class="fab fa-telegram"></i> Join Support Group</button>`;
            container.innerHTML = html;
        }
        
        function renderTasks() {
            const container = document.getElementById('tasksPage'); if (!currentUser) return;
            let html = `<div class="balance-header"><div class="balance-card"><div class="label">💰 ${t('deposit')}</div><div class="amount">৳${formatBDT(currentUser.depositBalance)}</div></div><div class="balance-card income"><div class="label">💵 ${t('income')}</div><div class="amount">৳${formatBDT(currentUser.incomeBalance)}</div></div></div><div class="tab-bar"><button class="tab-btn ${activeTaskTab === 'browse' ? 'active' : ''}" onclick="window.switchTaskTab('browse')"><i class="fas fa-globe"></i> ${t('browse')}</button><button class="tab-btn ${activeTaskTab === 'my' ? 'active' : ''}" onclick="window.switchTaskTab('my')"><i class="fas fa-list"></i> ${t('myTasks')}</button><button class="tab-btn ${activeTaskTab === 'post' ? 'active' : ''}" onclick="window.switchTaskTab('post')"><i class="fas fa-plus-circle"></i> ${t('post')}</button></div>`;
            
            if (activeTaskTab === 'browse') {
                const available = tasks.filter(task => task.approved === true && task.status === 'open' && !isTaskCompleted(task) && !hasUserSubmittedToUserTask(task.id));
                html += `<div class="section-title">📋 Available Tasks (One time only)</div><div class="tasks-grid">`;
                if (available.length > 0) { 
                    available.forEach(task => { 
                        const completed = task.completedCount || 0; 
                        const total = task.totalWorkers || 1; 
                        html += `<div class="task-card" style="cursor:pointer;" onclick="window.openSubmitModal('${task.id}', false)"><div class="task-header-row"><span class="task-reward-box">৳${formatBDT(task.budget)}</span></div><div class="task-title-text">${escapeHtml(task.title)}</div><div class="task-stats-row"><span><i class="fas fa-users"></i> Progress: ${completed}/${total}</span></div><div class="progress-container"><div class="progress-bar" style="width: ${(completed/total)*100}%;"></div></div></div>`;
                    }); 
                } else { html += `<div class="empty-state"><i class="fas fa-clipboard-list"></i><p>No tasks available right now</p></div>`; }
                html += `</div>`;
            } else if (activeTaskTab === 'my') {
                const myTasks = tasks.filter(task => task.postedBy === currentUser.id);
                html += `<div class="section-title">📋 My Posted Tasks</div><div class="tasks-grid">`;
                if (myTasks.length > 0) { 
                    myTasks.forEach(task => { 
                        const completed = task.completedCount || 0; 
                        const total = task.totalWorkers || 1; 
                        const statusText = task.approved === true ? (isTaskCompleted(task) ? 'Completed' : 'Active') : (task.approved === false ? 'Under Review' : 'Pending');
                        const statusColor = isTaskCompleted(task) ? 'completed' : (task.approved === true ? 'approved' : 'pending');
                        html += `<div class="task-card"><div class="task-header-row"><span class="task-reward-box">৳${formatBDT(task.budget)}</span><span class="badge-${statusColor}" style="background:${statusColor === 'completed' ? '#d1fae5' : (statusColor === 'approved' ? '#d1fae5' : '#fef3c7')}; color:${statusColor === 'completed' ? '#059669' : (statusColor === 'approved' ? '#059669' : '#d97706')}; padding:4px 12px; border-radius:20px; font-size:11px;">${statusText}</span></div><div class="task-title-text">${escapeHtml(task.title)}</div><div class="task-stats-row"><span><i class="fas fa-users"></i> ${completed}/${total} completed</span><span><i class="fas fa-calendar"></i> ${task.createdAt ? new Date(task.createdAt).toLocaleDateString() : '-'}</span></div><div class="progress-container"><div class="progress-bar" style="width: ${(completed/total)*100}%;"></div></div><div class="action-buttons-row"><button class="action-btn submitted" onclick="window.viewSubmissions('${task.id}')"><i class="fas fa-list"></i> Submitted Task</button>${!isTaskCompleted(task) && task.approved === true ? `<button class="action-btn increase" onclick="window.openIncreaseModal('${task.id}')"><i class="fas fa-plus"></i> Increase Job</button>` : ''}${task.status === 'open' && !isTaskCompleted(task) && task.approved === true ? `<button class="action-btn pause" onclick="window.pauseJob('${task.id}')"><i class="fas fa-pause"></i> Pause</button>` : ''}${task.status === 'paused' && task.approved === true ? `<button class="action-btn running" onclick="window.resumeJob('${task.id}')"><i class="fas fa-play"></i> Running</button>` : ''}<button class="action-btn delete" onclick="window.openDeleteTaskModal('${task.id}')"><i class="fas fa-trash"></i> Delete Task</button></div></div>`;
                    }); 
                } else { html += `<div class="empty-state"><i class="fas fa-clipboard-list"></i><p>You haven't posted any tasks yet</p></div>`; }
                html += `</div>`;
            } else if (activeTaskTab === 'post') {
                html += `<div class="section-title">📝 Post New Task</div><div class="review-notice">⏳ All posted tasks require Admin review before going live. Your deposit will be deducted immediately.</div><div style="background:white; border-radius:24px; padding:20px; margin-top:10px;"><input type="text" id="newTaskTitle" class="input-field" placeholder="Task Title (e.g., YouTube Like)"><textarea id="newTaskDesc" class="input-field" placeholder="Describe what workers need to do..." rows="3"></textarea><input type="number" id="newTaskBudget" class="input-field" placeholder="Budget per person (BDT) - Min 2" min="2"><input type="number" id="newTaskWorkers" class="input-field" placeholder="Workers needed - Min 10" min="10" value="10"><div class="fee-info">📊 Platform Fee: <strong>${appSettings.platformFee}%</strong></div><div class="total-display" id="totalDisplay">Total: ৳0.00</div><button class="btn-primary" id="postTaskBtn" onclick="window.createTask()">📤 Post Task</button></div>`;
                setTimeout(() => { const budgetInput = document.getElementById('newTaskBudget'); const workersInput = document.getElementById('newTaskWorkers'); if (budgetInput && workersInput) { const updateTotal = () => { const budget = parseFloat(budgetInput.value) || 0; const workers = parseInt(workersInput.value) || 0; const sub = budget * workers; const fee = sub * (appSettings.platformFee / 100); const totalDiv = document.getElementById('totalDisplay'); if (totalDiv) totalDiv.innerHTML = `Subtotal: ৳${formatBDT(sub)} + Fee (${appSettings.platformFee}%): ৳${formatBDT(fee)} = <strong>৳${formatBDT(sub + fee)}</strong>`; }; budgetInput.addEventListener('input', updateTotal); workersInput.addEventListener('input', updateTotal); updateTotal(); } }, 100);
            }
            container.innerHTML = html;
        }
        
        function renderShare() {
            const container = document.getElementById('sharePage'); if (!currentUser) return;
            const refCode = currentUser.referralCode || currentUser.id?.substring(0, 8) || '';
            const referLink = `${SITE_URL}?ref=${refCode}`;
            container.innerHTML = `<div class="ref-card"><h3>👥 Refer & Earn</h3><p style="color:#64748b; margin-bottom:4px;">🎁 Get ${appSettings.referralBonus} BDT per referral + ${appSettings.referralCommissionPercent}% commission from their earnings!</p><div class="ref-link-box"><span style="font-size:10px; word-break:break-all;">${referLink}</span><i class="fas fa-copy copy-icon" onclick="copyReferLink('${referLink}', this)" title="Copy Link"></i></div><div class="stats-row"><div class="stat-item"><div class="stat-value">${currentUser.referrals || 0}</div><div class="stat-label">Referrals</div></div><div class="stat-item"><div class="stat-value">৳${formatBDT(currentUser.referralEarnings || 0)}</div><div class="stat-label">Total Earned</div></div><div class="stat-item"><div class="stat-value">৳${formatBDT(currentUser.totalReferralCommission || 0)}</div><div class="stat-label">${appSettings.referralCommissionPercent}% Commission</div></div></div><div style="margin-top:12px; background:#f0fdf4; padding:10px; border-radius:12px;"><p style="font-size:11px; color:#2e7d32;"><i class="fas fa-info-circle"></i> Your Referral Code: <strong>${refCode}</strong></p></div></div>`;
        }
        
        function renderProfile() {
            const container = document.getElementById('profilePage'); if (!currentUser) return;
            const postedCount = tasks.filter(task => task.postedBy === currentUser.id).length;
            const approvedCount = submissions.filter(s => s.workerId === currentUser.id && s.status === 'approved').length;
            const pendingCount = submissions.filter(s => s.workerId === currentUser.id && s.status === 'pending').length;
            const pendingWithdrawals = withdrawals.filter(w => w.status === 'pending').length;
            const adminBadge = currentUser.isAdmin ? '<span class="admin-badge">Admin</span>' : '';
            container.innerHTML = `<div class="profile-card"><div class="profile-pic">👤</div><div class="profile-info"><h3>${escapeHtml(currentUser.name)} ${adminBadge}</h3><p>@${escapeHtml(currentUser.username)}</p><p>${escapeHtml(currentUser.email)}</p></div></div><div class="balance-header"><div class="balance-card"><div class="label">💰 ${t('deposit')}</div><div class="amount">৳${formatBDT(currentUser.depositBalance)}</div></div><div class="balance-card income"><div class="label">💵 ${t('income')}</div><div class="amount">৳${formatBDT(currentUser.incomeBalance)}</div></div></div><button class="btn-primary" onclick="window.openDepositModal()" style="background:#10b981;">💸 Add Deposit</button><button class="btn-primary" onclick="window.openWithdrawModal()" style="background:#f59e0b;">💰 Withdraw</button><div class="stats-row"><div class="stat-item"><div class="stat-value">${postedCount}</div><div class="stat-label">Posted</div></div><div class="stat-item"><div class="stat-value">${approvedCount}</div><div class="stat-label">Approved</div></div><div class="stat-item"><div class="stat-value">${pendingCount}</div><div class="stat-label">Pending Subs</div></div><div class="stat-item"><div class="stat-value">${pendingWithdrawals}</div><div class="stat-label">Withdraw Req</div></div></div><div style="margin-top:12px; background:#f0fdf4; padding:12px; border-radius:14px;"><p style="font-size:11px;"><i class="fas fa-gift"></i> <strong>Referral Stats:</strong> ${currentUser.referrals || 0} referrals | ৳${formatBDT(currentUser.referralEarnings || 0)} earned</p></div>`;
        }
        
        window.createTask = async function() {
            if (isPosting) { showNotification('⏳ Please wait...', 'info'); return; }
            const titleEl = document.getElementById('newTaskTitle');
            const descEl = document.getElementById('newTaskDesc');
            const budgetEl = document.getElementById('newTaskBudget');
            const workersEl = document.getElementById('newTaskWorkers');
            const btn = document.getElementById('postTaskBtn');
            const title = titleEl?.value?.trim() || '';
            const desc = descEl?.value?.trim() || '';
            const budget = parseFloat(budgetEl?.value) || 0;
            const workers = parseInt(workersEl?.value) || 0;
            if (!title) { showNotification('⚠️ Please enter a task title', 'error'); return; }
            if (!desc) { showNotification('⚠️ Please enter a description', 'error'); return; }
            if (budget < appSettings.minBudgetPerPerson) { showNotification(`⚠️ Minimum budget ৳${appSettings.minBudgetPerPerson} per person`, 'error'); return; }
            if (workers < appSettings.minWorkers) { showNotification(`⚠️ Minimum ${appSettings.minWorkers} workers required`, 'error'); return; }
            const total = (budget * workers) * (1 + (appSettings.platformFee / 100));
            if ((currentUser.depositBalance || 0) < total) { showNotification(`⚠️ Insufficient balance. Need ৳${formatBDT(total)}`, 'error'); return; }
            isPosting = true;
            if (btn) { btn.disabled = true; btn.innerText = '⏳ Posting...'; }
            try {
                await updateDoc(doc(db, 'users', currentUser.id), { depositBalance: (currentUser.depositBalance || 0) - total });
                await addDoc(collection(db, 'tasks'), { title, description: desc, budget, totalWorkers: workers, assignedWorkers: [], completedCount: 0, status: 'open', approved: false, postedBy: currentUser.id, postedByName: currentUser.name, createdAt: new Date().toISOString() });
                showNotification(`✅ Task posted! Waiting for admin approval. -৳${formatBDT(total)}`, 'success');
                if (titleEl) titleEl.value = '';
                if (descEl) descEl.value = '';
                if (budgetEl) budgetEl.value = '';
                if (workersEl) workersEl.value = '10';
                const totalDiv = document.getElementById('totalDisplay');
                if (totalDiv) totalDiv.innerHTML = 'Total: ৳0.00';
                await loadAllData();
                activeTaskTab = 'my';
                renderTasks();
            } catch(e) { console.error("Post task error:", e); showNotification('❌ Error posting task: ' + e.message, 'error'); }
            setTimeout(() => { isPosting = false; if (btn) { btn.disabled = false; btn.innerText = '📤 Post Task'; } }, 3000);
        };
        
        window.openDepositModal = function() { 
            document.getElementById('minDepositValue').innerText = appSettings.minDeposit;
            document.getElementById('depositModal').style.display = 'flex'; 
            window.selectDepositMethod('bkash'); 
            document.getElementById('profileMenu').style.display = 'none'; 
        };
        
        window.openWithdrawModal = function() { 
            document.getElementById('minWithdrawValue').innerText = appSettings.minWithdraw;
            document.getElementById('withdrawAvail').innerText = formatBDT(currentUser.incomeBalance || 0); 
            document.getElementById('withdrawModal').style.display = 'flex'; 
            window.selectWithdrawMethod('bkash'); 
            document.getElementById('profileMenu').style.display = 'none'; 
        };
        
        window.openEditProfile = function() { document.getElementById('editName').value = currentUser.name || ''; document.getElementById('editUsername').value = currentUser.username || ''; document.getElementById('editPassword').value = ''; document.getElementById('editProfileModal').style.display = 'flex'; document.getElementById('profileMenu').style.display = 'none'; };
        window.saveProfile = async function() { const name = document.getElementById('editName').value.trim(); const username = document.getElementById('editUsername').value.trim(); if (!name || !username) { showNotification('⚠️ Fill required fields', 'error'); return; } await updateDoc(doc(db, 'users', currentUser.id), { name, username }); currentUser.name = name; currentUser.username = username; showNotification('✅ Profile updated!', 'success'); window.closeModal('editProfileModal'); refreshAllPages(); };
        
        document.getElementById('notificationBell')?.addEventListener('click', (e) => { e.stopPropagation(); window.toggleNotificationPanel(); });
        document.addEventListener('click', function(e) { 
            const panel = document.getElementById('notificationPanel');
            const bell = document.getElementById('notificationBell');
            if (panel && bell && !bell.contains(e.target) && !panel.contains(e.target)) { panel.classList.remove('show'); }
            document.getElementById('profileMenu').style.display = 'none';
        });
        document.getElementById('settingsIcon')?.addEventListener('click', function(e) { e.stopPropagation(); const menu = document.getElementById('profileMenu'); menu.style.display = menu.style.display === 'block' ? 'none' : 'block'; });
        document.querySelectorAll('.nav-item').forEach(item => { item.addEventListener('click', function() { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); this.classList.add('active'); document.querySelectorAll('.page').forEach(p => p.classList.remove('active')); const pageId = this.dataset.page + 'Page'; document.getElementById(pageId).classList.add('active'); refreshAllPages(); }); });
        document.querySelectorAll('.modal-overlay').forEach(modal => { modal.addEventListener('click', function(e) { if (e.target === this) this.style.display = 'none'; }); });
        document.getElementById('screenshotLabel')?.addEventListener('click', function(e) { e.preventDefault(); document.getElementById('screenshotInput').click(); });
        
        onAuthStateChanged(auth, async (user) => {
            if (user) { 
                await loadSettings();
                await loadNetworks();
                const userDoc = await getDoc(doc(db, 'users', user.uid)); 
                if (userDoc.exists()) { currentUser = { id: user.uid, ...userDoc.data() }; } 
                document.getElementById('loginPage').style.display = 'none'; 
                document.getElementById('mainApp').style.display = 'block'; 
                await loadAllData(); 
                startRealtimeListeners(); 
                refreshAllPages(); 
            }
            else { document.getElementById('mainApp').style.display = 'none'; document.getElementById('loginPage').style.display = 'flex'; }
        });
        
        console.log("🚀 UniTask - Settings and Networks fully loaded from Admin Panel!");
    </script>
</body>
</html>
