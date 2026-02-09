<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مسابقة توقعات المباريات</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin: 20px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }
        
        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
        }
        
        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }
        
        .form-control {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        .form-control:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 10px rgba(102, 126, 234, 0.1);
        }
        
        .btn {
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            margin: 5px;
        }
        
        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }
        
        .btn-success {
            background: #28a745;
            color: white;
        }
        
        .btn-success:hover {
            background: #218838;
            transform: translateY(-2px);
        }
        
        .btn-warning {
            background: #ffc107;
            color: #000;
        }
        
        .btn-warning:hover {
            background: #e0a800;
        }
        
        .match-prediction {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 15px;
            margin: 10px 0;
            background: #f8f9fa;
            border-radius: 10px;
            border: 2px solid transparent;
            transition: all 0.3s;
        }
        
        .match-prediction:hover {
            border-color: #667eea;
            background: #fff;
        }
        
        .match-prediction.double-match {
            border-color: #ffc107;
            background: #fff8e1;
        }
        
        .team-input {
            width: 60px;
            text-align: center;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-weight: bold;
            font-size: 18px;
        }
        
        .vs {
            font-weight: bold;
            font-size: 18px;
            color: #666;
            margin: 0 15px;
        }
        
        .double-btn {
            background: #ffc107;
            color: #000;
            border: none;
            padding: 8px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        .double-btn:hover {
            background: #e0a800;
            transform: scale(1.05);
        }
        
        .double-btn.active {
            background: #ff8c00;
            color: white;
        }
        
        .leaderboard-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 15px;
            margin: 8px 0;
            background: #f8f9fa;
            border-radius: 8px;
            border-right: 4px solid #667eea;
        }
        
        .rank {
            font-size: 24px;
            font-weight: bold;
            color: #667eea;
            margin-left: 15px;
            min-width: 40px;
        }
        
        .rank.first { color: #ffd700; }
        .rank.second { color: #c0c0c0; }
        .rank.third { color: #cd7f32; }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .user-name {
            font-weight: bold;
            font-size: 18px;
        }
        
        .points {
            background: #667eea;
            color: white;
            padding: 8px 12px;
            border-radius: 20px;
            font-weight: bold;
        }
        
        .navigation {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        
        .nav-btn {
            background: rgba(255,255,255,0.2);
            color: white;
            border: 2px solid white;
            padding: 10px 20px;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .nav-btn:hover, .nav-btn.active {
            background: white;
            color: #667eea;
        }
        
        .hidden {
            display: none;
        }
        
        .user-header {
            background: linear-gradient(45deg, #28a745, #20c997);
            color: white;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            margin-bottom: 20px;
        }
        
        .loading {
            text-align: center;
            padding: 20px;
            color: #666;
        }
        
        .alert {
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            font-weight: bold;
        }
        
        .alert-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .alert-error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .alert-info {
            background: #d1ecf1;
            color: #0c5460;
            border: 1px solid #bee5eb;
        }
        
        .admin-section {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            border-radius: 8px;
            padding: 20px;
            margin: 20px 0;
        }
        
        .admin-title {
            color: #856404;
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 1.2em;
        }
        
        @media (max-width: 768px) {
            .match-prediction {
                flex-direction: column;
                gap: 10px;
            }
            
            .team-input {
                width: 80px;
            }
            
            .header h1 {
                font-size: 1.8em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏆 مسابقة توقعات المباريات</h1>
            <p>توقع النتائج واحصل على النقاط!</p>
        </div>

        <!-- صفحة تسجيل الدخول -->
        <div id="loginPage" class="card">
            <h2 style="text-align: center; color: #667eea; margin-bottom: 20px;">تسجيل الدخول</h2>
            <div class="alert alert-info">
                💡 إذا كنت مستخدم جديد، فقط أدخل اسمك وكلمة مرور جديدة وسيتم إنشاء حساب لك تلقائياً
            </div>
            <form id="loginForm">
                <div class="form-group">
                    <label for="username">اسم المستخدم:</label>
                    <input type="text" id="username" class="form-control" required placeholder="أدخل اسم المستخدم">
                </div>
                <div class="form-group">
                    <label for="password">كلمة المرور:</label>
                    <input type="password" id="password" class="form-control" required placeholder="أدخل كلمة المرور">
                </div>
                <button type="submit" class="btn btn-primary" style="width: 100%;">دخول</button>
            </form>
            <div id="loginAlert"></div>
        </div>

        <!-- الصفحة الرئيسية -->
        <div id="mainPage" class="hidden">
            <div id="userHeader" class="user-header"></div>
            
            <div class="navigation">
                <button class="nav-btn active" onclick="showSection('predictions')">التوقعات</button>
                <button class="nav-btn" onclick="showSection('leaderboard')">الترتيب</button>
                <div id="adminNav"></div>
            </div>

            <!-- قسم التوقعات -->
            <div id="predictionsSection" class="card">
                <h3 style="color: #667eea; margin-bottom: 20px;">🎯 توقعاتك للجولة الحالية</h3>
                <div id="roundInfo" class="alert alert-info" style="margin-bottom: 20px;"></div>
                <div id="predictionsForm">
                    <div class="loading">جاري تحميل المباريات...</div>
                </div>
            </div>

            <!-- قسم الترتيب -->
            <div id="leaderboardSection" class="card hidden">
                <h3 style="color: #667eea; margin-bottom: 20px;">🏆 الترتيب العام</h3>
                <div id="leaderboardList">
                    <div class="loading">جاري تحميل الترتيب...</div>
                </div>
            </div>

            <!-- قسم الإدارة -->
            <div id="adminSection" class="card hidden">
                <div class="admin-section">
                    <div class="admin-title">⚙️ لوحة الإدارة</div>
                    
                    <div style="margin-bottom: 30px;">
                        <h4>إضافة جولة جديدة:</h4>
                        <div class="form-group">
                            <label>رقم الجولة:</label>
                            <input type="text" id="roundNumber" class="form-control" placeholder="مثال: الجولة 1">
                        </div>
                        <button onclick="addNewRound()" class="btn btn-primary">إضافة جولة</button>
                    </div>
                    
                    <div style="margin-bottom: 30px;">
                        <h4>إدخال النتائج الفعلية:</h4>
                        <div id="resultsForm">
                            <div class="loading">جاري تحميل النموذج...</div>
                        </div>
                    </div>
                    
                    <div>
                        <h4>إدارة الجولة:</h4>
                        <button onclick="lockCurrentRound()" class="btn btn-warning">قفل الجولة الحالية</button>
                        <p style="margin-top: 10px; font-size: 14px; color: #666;">
                            ⚠️ قفل الجولة يمنع المستخدمين من تعديل توقعاتهم
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // المتغيرات العامة
        let currentUser = null;
        let currentRound = null;
        let doubleMatchChoice = 0;
        let savedPredictions = null;
        
        // استخدام رابط نفس الصفحة (سيعمل تلقائياً من Apps Script)
        const SCRIPT_URL = window.location.href.split('?')[0];

        // تسجيل الدخول
        document.getElementById('loginForm').addEventListener('submit', async function(e) {
            e.preventDefault();
            
            const name = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value;
            
            if (!name || !password) {
                showAlert('يرجى إدخال اسم المستخدم وكلمة المرور', 'error', 'loginAlert');
                return;
            }
            
            try {
                const response = await fetch(SCRIPT_URL, {
                    method: 'POST',
                    body: JSON.stringify({
                        action: 'login',
                        name: name,
                        password: password
                    })
                });
                
                const result = await response.json();
                
                if (result.success) {
                    currentUser = result.user;
                    showMainPage();
                    if (result.isNewUser) {
                        showAlert('مرحباً! تم إنشاء حساب جديد بنجاح!', 'success');
                    }
                } else {
                    showAlert(result.error || 'خطأ في تسجيل الدخول', 'error', 'loginAlert');
                }
            } catch (error) {
                console.error('Error:', error);
                showAlert('خطأ في الاتصال: ' + error.message, 'error', 'loginAlert');
            }
        });

        // باقي الكود كما هو...
        // (نسخ جميع الدوال من الكود السابق)
    </script>
</body>
</html>
