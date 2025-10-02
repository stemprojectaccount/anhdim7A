<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gallery Ảnh Dìm - Quản lý ảnh bạn bè</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4361ee;
            --primary-dark: #3a56d4;
            --secondary: #7209b7;
            --accent: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --success: #4cc9f0;
            --card-bg: #ffffff;
            --shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            --radius: 16px;
            --transition: all 0.3s ease;
            --sparkle: #fffacd;
        }

        .dark-mode {
            --primary: #4895ef;
            --primary-dark: #3a7bc8;
            --secondary: #b5179e;
            --accent: #f72585;
            --light: #121212;
            --dark: #f8f9fa;
            --gray: #a0a0a0;
            --card-bg: #1e1e1e;
            --shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            --sparkle: #ffd700;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: var(--dark);
            min-height: 100vh;
            padding: 20px;
            transition: var(--transition);
            overflow-x: hidden;
        }

        .dark-mode body {
            background: linear-gradient(135deg, #2c3e50 0%, #3498db 100%);
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Hiệu ứng lấp lánh nền */
        .sparkle-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .sparkle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: var(--sparkle);
            border-radius: 50%;
            box-shadow: 0 0 10px 2px var(--sparkle);
            animation: sparkle 5s infinite;
        }

        @keyframes sparkle {
            0%, 100% { opacity: 0; }
            50% { opacity: 1; }
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding: 20px;
            background: var(--card-bg);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
        }

        header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1), transparent);
            transform: rotate(45deg);
            animation: shine 3s infinite;
        }

        @keyframes shine {
            0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo i {
            font-size: 2.5rem;
            color: var(--primary);
            filter: drop-shadow(0 0 5px rgba(67, 97, 238, 0.5));
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .logo h1 {
            font-size: 1.8rem;
            background: linear-gradient(to right, var(--primary), var(--accent));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            font-weight: 700;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .controls {
            display: flex;
            gap: 15px;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: var(--transition);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: var(--transition);
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background: var(--primary-dark);
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(67, 97, 238, 0.4);
        }

        .btn-secondary {
            background: var(--secondary);
            color: white;
        }

        .btn-secondary:hover {
            background: #5a08a0;
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(114, 9, 183, 0.4);
        }

        .btn-accent {
            background: var(--accent);
            color: white;
        }

        .btn-accent:hover {
            background: #e11574;
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(247, 37, 133, 0.4);
        }

        .btn-outline {
            background: transparent;
            color: var(--dark);
            border: 2px solid var(--dark);
        }

        .btn-outline:hover {
            background: var(--dark);
            color: var(--light);
        }

        .btn i {
            filter: drop-shadow(0 0 3px rgba(0, 0, 0, 0.2));
        }

        .main-content {
            display: grid;
            grid-template-columns: 300px 1fr;
            gap: 25px;
        }

        .sidebar {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 25px;
            box-shadow: var(--shadow);
            height: fit-content;
            position: relative;
            overflow: hidden;
        }

        .sidebar::after {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 100px;
            height: 100px;
            background: radial-gradient(circle, var(--primary) 0%, transparent 70%);
            opacity: 0.1;
            border-radius: 50%;
        }

        .section-title {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 20px;
            color: var(--primary);
            font-size: 1.2rem;
        }

        .section-title i {
            font-size: 1.5rem;
            filter: drop-shadow(0 0 5px rgba(67, 97, 238, 0.3));
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }

        .form-control {
            width: 100%;
            padding: 14px;
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            font-size: 16px;
            transition: var(--transition);
            background: var(--light);
            color: var(--dark);
        }

        .form-control:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }

        .file-upload {
            position: relative;
            display: inline-block;
            width: 100%;
        }

        .file-upload-label {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            padding: 14px;
            background: var(--light);
            border: 2px dashed #b0b0b0;
            border-radius: 12px;
            cursor: pointer;
            transition: var(--transition);
            color: var(--gray);
        }

        .file-upload-label:hover {
            border-color: var(--primary);
            color: var(--primary);
        }

        .file-upload input {
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0;
            width: 100%;
            height: 100%;
            cursor: pointer;
        }

        .content {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 25px;
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
        }

        .content::before {
            content: '';
            position: absolute;
            bottom: -50px;
            right: -50px;
            width: 150px;
            height: 150px;
            background: radial-gradient(circle, var(--accent) 0%, transparent 70%);
            opacity: 0.1;
            border-radius: 50%;
        }

        .search-container {
            display: flex;
            margin-bottom: 25px;
            gap: 15px;
        }

        .search-box {
            flex: 1;
            position: relative;
        }

        .search-box i {
            position: absolute;
            left: 18px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--gray);
            z-index: 2;
        }

        .search-box input {
            width: 100%;
            padding: 16px 16px 16px 50px;
            border: 2px solid #e0e0e0;
            border-radius: 50px;
            font-size: 16px;
            transition: var(--transition);
            background: var(--light);
            color: var(--dark);
            position: relative;
            z-index: 1;
        }

        .search-box input:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }

        .tabs {
            display: flex;
            margin-bottom: 25px;
            border-bottom: 2px solid #e0e0e0;
        }

        .tab {
            padding: 12px 24px;
            cursor: pointer;
            font-weight: 600;
            transition: var(--transition);
            border-bottom: 3px solid transparent;
            color: var(--gray);
            position: relative;
        }

        .tab.active {
            color: var(--primary);
            border-bottom: 3px solid var(--primary);
        }

        .tab i {
            margin-right: 8px;
            filter: drop-shadow(0 0 3px rgba(0, 0, 0, 0.1));
        }

        .friend-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .friend-card {
            background: var(--light);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            transition: var(--transition);
            cursor: pointer;
            text-align: center;
            position: relative;
        }

        .friend-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(67,97,238,0.1) 0%, rgba(247,37,133,0.1) 100%);
            opacity: 0;
            transition: var(--transition);
        }

        .friend-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
        }

        .friend-card:hover::before {
            opacity: 1;
        }

        .friend-avatar {
            width: 100%;
            height: 140px;
            object-fit: cover;
            border-bottom: 3px solid var(--primary);
            position: relative;
            z-index: 1;
        }

        .friend-info {
            padding: 15px;
            position: relative;
            z-index: 1;
        }

        .friend-name {
            font-weight: 700;
            margin-bottom: 5px;
            color: var(--dark);
        }

        .friend-count {
            font-size: 0.9rem;
            color: var(--gray);
        }

        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .gallery-item {
            position: relative;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: var(--transition);
            cursor: pointer;
            aspect-ratio: 1;
        }

        .gallery-item:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }

        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }

        .gallery-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.7), transparent);
            padding: 15px;
            color: white;
            transform: translateY(100%);
            transition: var(--transition);
        }

        .gallery-item:hover .gallery-overlay {
            transform: translateY(0);
        }

        .gallery-actions {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
        }

        .action-btn {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: var(--transition);
            backdrop-filter: blur(10px);
        }

        .action-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.1);
        }

        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: var(--gray);
            grid-column: 1 / -1;
        }

        .empty-state i {
            font-size: 4rem;
            margin-bottom: 20px;
            color: #e0e0e0;
            filter: drop-shadow(0 0 5px rgba(0, 0, 0, 0.1));
        }

        .empty-state h3 {
            font-size: 1.5rem;
            margin-bottom: 10px;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom: 25px;
        }

        .stat-card {
            background: var(--light);
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }

        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(to right, var(--primary), var(--accent));
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 5px;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
        }

        .modal-content {
            max-width: 90%;
            max-height: 90%;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            position: relative;
            animation: zoomIn 0.3s ease;
        }

        @keyframes zoomIn {
            from { transform: scale(0.8); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        .modal img {
            width: 100%;
            height: auto;
            display: block;
        }

        .modal-close {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.5);
            border: none;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 1.2rem;
            transition: var(--transition);
            backdrop-filter: blur(10px);
            z-index: 10;
        }

        .modal-close:hover {
            background: rgba(0, 0, 0, 0.7);
            transform: scale(1.1);
        }

        .toast {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: var(--success);
            color: white;
            padding: 16px 24px;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            display: flex;
            align-items: center;
            gap: 10px;
            transform: translateY(100px);
            opacity: 0;
            transition: var(--transition);
            z-index: 1100;
        }

        .toast.show {
            transform: translateY(0);
            opacity: 1;
        }

        .toast i {
            filter: drop-shadow(0 0 3px rgba(0, 0, 0, 0.2));
        }

        @media (max-width: 1100px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .sidebar {
                order: 2;
            }
            
            .content {
                order: 1;
            }
        }

        @media (max-width: 768px) {
            .friend-list, .gallery {
                grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
            
            header {
                flex-direction: column;
                gap: 20px;
            }
            
            .search-container {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <!-- Hiệu ứng lấp lánh nền -->
    <div class="sparkle-bg" id="sparkleBg"></div>

    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-camera-retro"></i>
                <h1>Gallery Ảnh Dìm</h1>
            </div>
            <div class="controls">
                <button class="btn btn-outline" id="themeToggle">
                    <i class="fas fa-moon"></i> Chế độ tối
                </button>
                <button class="btn btn-primary" id="exportBtn">
                    <i class="fas fa-download"></i> Xuất dữ liệu
                </button>
            </div>
        </header>

        <div class="main-content">
            <div class="sidebar">
                <div class="section-title">
                    <i class="fas fa-user-plus"></i>
                    <h2>Thêm bạn mới</h2>
                </div>
                
                <div class="form-group">
                    <label for="friendName">Tên bạn</label>
                    <input type="text" id="friendName" class="form-control" placeholder="Nhập tên bạn...">
                </div>
                
                <div class="form-group">
                    <label for="friendImages">Chọn ảnh dìm</label>
                    <div class="file-upload">
                        <label for="friendImages" class="file-upload-label">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <span>Kéo thả ảnh hoặc nhấn để chọn</span>
                        </label>
                        <input type="file" id="friendImages" multiple accept="image/*">
                    </div>
                </div>
                
                <button class="btn btn-primary" id="addFriendBtn" style="width: 100%;">
                    <i class="fas fa-plus-circle"></i> Thêm bạn
                </button>
                
                <div class="stats">
                    <div class="stat-card">
                        <div class="stat-value" id="totalFriends">47</div>
                        <div class="stat-label">Bạn bè</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="totalImages">128</div>
                        <div class="stat-label">Ảnh dìm</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="storageUsed">24%</div>
                        <div class="stat-label">Bộ nhớ</div>
                    </div>
                </div>
            </div>

            <div class="content">
                <div class="search-container">
                    <div class="search-box">
                        <i class="fas fa-search"></i>
                        <input type="text" id="searchInput" placeholder="Tìm kiếm bạn bè...">
                    </div>
                    <button class="btn btn-accent" id="searchBtn">
                        <i class="fas fa-search"></i> Tìm kiếm
                    </button>
                </div>
                
                <div class="tabs">
                    <div class="tab active" data-tab="friends">
                        <i class="fas fa-users"></i> Danh sách bạn bè
                    </div>
                    <div class="tab" data-tab="gallery">
                        <i class="fas fa-images"></i> Thư viện ảnh
                    </div>
                </div>
                
                <div id="friendsTab" class="tab-content">
                    <div class="friend-list" id="friendList">
                        <!-- Friend cards will be generated here -->
                    </div>
                </div>
                
                <div id="galleryTab" class="tab-content" style="display: none;">
                    <div class="gallery" id="imageGallery">
                        <!-- Gallery images will be generated here -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Image Modal -->
    <div class="modal" id="imageModal">
        <button class="modal-close" id="closeModal">
            <i class="fas fa-times"></i>
        </button>
        <div class="modal-content">
            <img id="modalImage" src="" alt="Ảnh lớn">
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast" id="toast">
        <i class="fas fa-check-circle"></i>
        <span id="toastMessage">Thao tác thành công!</span>
    </div>

    <script>
        // Tạo hiệu ứng lấp lánh
        function createSparkles() {
            const sparkleBg = document.getElementById('sparkleBg');
            const sparkleCount = 50;
            
            for (let i = 0; i < sparkleCount; i++) {
                const sparkle = document.createElement('div');
                sparkle.className = 'sparkle';
                
                // Vị trí ngẫu nhiên
                sparkle.style.left = `${Math.random() * 100}%`;
                sparkle.style.top = `${Math.random() * 100}%`;
                
                // Kích thước ngẫu nhiên
                const size = Math.random() * 3 + 2;
                sparkle.style.width = `${size}px`;
                sparkle.style.height = `${size}px`;
                
                // Thời gian animation ngẫu nhiên
                sparkle.style.animationDelay = `${Math.random() * 5}s`;
                sparkle.style.animationDuration = `${Math.random() * 3 + 3}s`;
                
                sparkleBg.appendChild(sparkle);
            }
        }

        // Lưu trữ dữ liệu bạn bè và ảnh
        let friendsData = JSON.parse(localStorage.getItem('friendsData')) || {};
        
        // DOM Elements
        const themeToggle = document.getElementById('themeToggle');
        const friendNameInput = document.getElementById('friendName');
        const friendImagesInput = document.getElementById('friendImages');
        const addFriendBtn = document.getElementById('addFriendBtn');
        const friendList = document.getElementById('friendList');
        const searchInput = document.getElementById('searchInput');
        const searchBtn = document.getElementById('searchBtn');
        const imageGallery = document.getElementById('imageGallery');
        const imageModal = document.getElementById('imageModal');
        const modalImage = document.getElementById('modalImage');
        const closeModal = document.getElementById('closeModal');
        const toast = document.getElementById('toast');
        const toastMessage = document.getElementById('toastMessage');
        const tabs = document.querySelectorAll('.tab');
        const tabContents = document.querySelectorAll('.tab-content');
        const totalFriendsEl = document.getElementById('totalFriends');
        const totalImagesEl = document.getElementById('totalImages');
        const storageUsedEl = document.getElementById('storageUsed');
        
        // Khởi tạo
        document.addEventListener('DOMContentLoaded', function() {
            createSparkles();
            displayFriends();
            updateStats();
            
            // Kiểm tra chế độ tối
            if (localStorage.getItem('darkMode') === 'enabled') {
                document.body.classList.add('dark-mode');
                themeToggle.innerHTML = '<i class="fas fa-sun"></i> Chế độ sáng';
            }
        });
        
        // Chuyển đổi chế độ tối/sáng
        themeToggle.addEventListener('click', function() {
            document.body.classList.toggle('dark-mode');
            
            if (document.body.classList.contains('dark-mode')) {
                localStorage.setItem('darkMode', 'enabled');
                themeToggle.innerHTML = '<i class="fas fa-sun"></i> Chế độ sáng';
            } else {
                localStorage.setItem('darkMode', 'disabled');
                themeToggle.innerHTML = '<i class="fas fa-moon"></i> Chế độ tối';
            }
        });
        
        // Chuyển đổi tab
        tabs.forEach(tab => {
            tab.addEventListener('click', function() {
                const targetTab = this.getAttribute('data-tab');
                
                // Cập nhật tab active
                tabs.forEach(t => t.classList.remove('active'));
                this.classList.add('active');
                
                // Hiển thị nội dung tab tương ứng
                tabContents.forEach(content => {
                    content.style.display = 'none';
                });
                
                document.getElementById(`${targetTab}Tab`).style.display = 'block';
            });
        });
        
        // Hiển thị danh sách bạn bè
        function displayFriends() {
            friendList.innerHTML = '';
            
            if (Object.keys(friendsData).length === 0) {
                friendList.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-users"></i>
                        <h3>Chưa có bạn bè nào</h3>
                        <p>Thêm bạn bè và ảnh dìm để bắt đầu</p>
                    </div>
                `;
                return;
            }
            
            Object.keys(friendsData).forEach(friendName => {
                const friendCard = document.createElement('div');
                friendCard.className = 'friend-card';
                
                const avatar = document.createElement('img');
                avatar.className = 'friend-avatar';
                
                // Sử dụng ảnh đầu tiên làm avatar
                if (friendsData[friendName].images.length > 0) {
                    avatar.src = friendsData[friendName].images[0];
                } else {
                    avatar.src = 'data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgdmlld0JveD0iMCAwIDIwMCAyMDAiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxyZWN0IHdpZHRoPSIyMDAiIGhlaWdodD0iMjAwIiBmaWxsPSIjZWVlIi8+CjxjaXJjbGUgY3g9IjEwMCIgY3k9IjcwIiByPSIzMCIgZmlsbD0iI2NjYyIvPgo8cmVjdCB4PSI2MCIgeT0iMTEwIiB3aWR0aD0iODAiIGhlaWdodD0iODAiIGZpbGw9IiNjY2MiLz4KPHRleHQgeD0iMTAwIiB5PSIxODAiIGZvbnQtZmFtaWx5PSJBcmlhbCIgZm9udC1zaXplPSIxNCIgZmlsbD0iIzk5OSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZHk9Ii4zZW0iPk5vIEltYWdlPC90ZXh0Pgo8L3N2Zz4=';
                }
                
                const friendInfo = document.createElement('div');
                friendInfo.className = 'friend-info';
                
                const name = document.createElement('div');
                name.className = 'friend-name';
                name.textContent = friendName;
                
                const count = document.createElement('div');
                count.className = 'friend-count';
                count.textContent = `${friendsData[friendName].images.length} ảnh`;
                
                friendInfo.appendChild(name);
                friendInfo.appendChild(count);
                
                friendCard.appendChild(avatar);
                friendCard.appendChild(friendInfo);
                
                // Thêm sự kiện click để hiển thị ảnh của bạn đó
                friendCard.addEventListener('click', () => {
                    searchInput.value = friendName;
                    displayFriendImages(friendName);
                    
                    // Chuyển sang tab gallery
                    tabs.forEach(t => t.classList.remove('active'));
                    document.querySelector('[data-tab="gallery"]').classList.add('active');
                    
                    tabContents.forEach(content => {
                        content.style.display = 'none';
                    });
                    document.getElementById('galleryTab').style.display = 'block';
                });
                
                friendList.appendChild(friendCard);
            });
        }
        
        // Hiển thị ảnh của một người bạn cụ thể
        function displayFriendImages(friendName) {
            imageGallery.innerHTML = '';
            
            if (friendsData[friendName] && friendsData[friendName].images.length > 0) {
                friendsData[friendName].images.forEach((imageSrc, index) => {
                    const galleryItem = document.createElement('div');
                    galleryItem.className = 'gallery-item';
                    
                    const img = document.createElement('img');
                    img.src = imageSrc;
                    img.alt = `Ảnh dìm của ${friendName}`;
                    img.loading = 'lazy';
                    
                    const overlay = document.createElement('div');
                    overlay.className = 'gallery-overlay';
                    
                    const fileName = document.createElement('div');
                    fileName.textContent = `${friendName}_${index + 1}.jpg`;
                    fileName.style.fontWeight = '600';
                    fileName.style.marginBottom = '5px';
                    
                    const actions = document.createElement('div');
                    actions.className = 'gallery-actions';
                    
                    const downloadBtn = document.createElement('button');
                    downloadBtn.className = 'action-btn';
                    downloadBtn.innerHTML = '<i class="fas fa-download"></i>';
                    downloadBtn.title = 'Tải ảnh về';
                    downloadBtn.addEventListener('click', (e) => {
                        e.stopPropagation();
                        downloadImage(imageSrc, `${friendName}_${index + 1}.jpg`);
                    });
                    
                    const viewBtn = document.createElement('button');
                    viewBtn.className = 'action-btn';
                    viewBtn.innerHTML = '<i class="fas fa-expand"></i>';
                    viewBtn.title = 'Xem ảnh lớn';
                    viewBtn.addEventListener('click', (e) => {
                        e.stopPropagation();
                        modalImage.src = imageSrc;
                        imageModal.style.display = 'flex';
                    });
                    
                    actions.appendChild(downloadBtn);
                    actions.appendChild(viewBtn);
                    
                    overlay.appendChild(fileName);
                    overlay.appendChild(actions);
                    
                    galleryItem.appendChild(img);
                    galleryItem.appendChild(overlay);
                    
                    // Thêm sự kiện click để mở ảnh lớn
                    galleryItem.addEventListener('click', () => {
                        modalImage.src = imageSrc;
                        imageModal.style.display = 'flex';
                    });
                    
                    imageGallery.appendChild(galleryItem);
                });
            } else {
                imageGallery.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-images"></i>
                        <h3>Không có ảnh nào</h3>
                        <p>${friendName} chưa có ảnh dìm nào</p>
                    </div>
                `;
            }
        }
        
        // Tải ảnh về
        function downloadImage(imageSrc, filename) {
            const link = document.createElement('a');
            link.href = imageSrc;
            link.download = filename;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            showToast(`Đã tải xuống ${filename}`);
        }
        
        // Cập nhật thống kê
        function updateStats() {
            const totalFriends = Object.keys(friendsData).length;
            const totalImages = Object.values(friendsData).reduce((total, friend) => total + friend.images.length, 0);
            
            totalFriendsEl.textContent = totalFriends;
            totalImagesEl.textContent = totalImages;
            
            // Tính % bộ nhớ sử dụng (giả lập)
            const storageUsed = Math.min(100, Math.round(totalImages / 5));
            storageUsedEl.textContent = `${storageUsed}%`;
        }
        
        // Hiển thị thông báo
        function showToast(message) {
            toastMessage.textContent = message;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }
        
        // Sự kiện thêm bạn
        addFriendBtn.addEventListener('click', () => {
            const friendName = friendNameInput.value.trim();
            const files = friendImagesInput.files;
            
            if (!friendName) {
                showToast('Vui lòng nhập tên bạn!');
                return;
            }
            
            if (files.length === 0) {
                showToast('Vui lòng chọn ít nhất một ảnh!');
                return;
            }
            
            // Khởi tạo mảng ảnh cho bạn mới nếu chưa tồn tại
            if (!friendsData[friendName]) {
                friendsData[friendName] = { images: [] };
            }
            
            // Đọc và lưu ảnh
            let processed = 0;
            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    friendsData[friendName].images.push(e.target.result);
                    processed++;
                    
                    // Lưu vào localStorage sau khi đọc xong tất cả ảnh
                    if (processed === files.length) {
                        localStorage.setItem('friendsData', JSON.stringify(friendsData));
                        displayFriends();
                        updateStats();
                        friendNameInput.value = '';
                        friendImagesInput.value = '';
                        showToast(`Đã thêm ${files.length} ảnh cho ${friendName}`);
                    }
                };
                
                reader.readAsDataURL(file);
            }
        });
        
        // Sự kiện tìm kiếm
        searchBtn.addEventListener('click', () => {
            const searchName = searchInput.value.trim();
            if (searchName) {
                if (friendsData[searchName]) {
                    displayFriendImages(searchName);
                    
                    // Chuyển sang tab gallery
                    tabs.forEach(t => t.classList.remove('active'));
                    document.querySelector('[data-tab="gallery"]').classList.add('active');
                    
                    tabContents.forEach(content => {
                        content.style.display = 'none';
                    });
                    document.getElementById('galleryTab').style.display = 'block';
                } else {
                    showToast(`Không tìm thấy bạn tên "${searchName}"`);
                }
            } else {
                showToast('Vui lòng nhập tên để tìm kiếm!');
            }
        });
        
        // Đóng modal
        closeModal.addEventListener('click', () => {
            imageModal.style.display = 'none';
        });
        
        // Đóng modal khi click bên ngoài
        imageModal.addEventListener('click', (e) => {
            if (e.target === imageModal) {
                imageModal.style.display = 'none';
            }
        });
        
        // Tạo dữ liệu mẫu nếu chưa có
        if (Object.keys(friendsData).length === 0) {
            // Tạo dữ liệu mẫu cho 47 người bạn
            for (let i = 1; i <= 47; i++) {
                const friendName = `Bạn ${i}`;
                friendsData[friendName] = {
                    images: [
                        'data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgdmlld0JveD0iMCAwIDIwMCAyMDAiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxyZWN0IHdpZHRoPSIyMDAiIGhlaWdodD0iMjAwIiBmaWxsPSIjZWVlIi8+CjxjaXJjbGUgY3g9IjEwMCIgY3k9IjcwIiByPSIzMCIgZmlsbD0iI2NjYyIvPgo8cmVjdCB4PSI2MCIgeT0iMTEwIiB3aWR0aD0iODAiIGhlaWdodD0iODAiIGZpbGw9IiNjY2MiLz4KPHRleHQgeD0iMTAwIiB5PSIxODAiIGZvbnQtZmFtaWx5PSJBcmlhbCIgZm9udC1zaXplPSIxNCIgZmlsbD0iIzk5OSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZHk9Ii4zZW0iPkFuaCBt4bq/dSB7IGkgfTwvdGV4dD4KPC9zdmc+'
                    ]
                };
            }
            localStorage.setItem('friendsData', JSON.stringify(friendsData));
            displayFriends();
            updateStats();
        }
    </script>
</body>
</html>
