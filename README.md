<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ghost Profile</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono:wght@400&display=swap');
        
        body {
            background: #000;
            color: #00ff41;
            font-family: 'Share Tech Mono', monospace;
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 600px;
            margin: 0 auto;
        }
        
        .typing {
            border-right: 2px solid #00ff41;
            animation: blink 1s infinite;
        }
        
        @keyframes blink {
            0%, 50% { border-color: #00ff41; }
            51%, 100% { border-color: transparent; }
        }
        
        .glitch {
            position: relative;
            color: #00ff41;
            font-size: 2em;
            font-weight: bold;
            text-align: center;
            margin-bottom: 30px;
        }
        
        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        
        .glitch::before {
            animation: glitch-1 0.5s infinite;
            color: #ff0040;
            z-index: -1;
        }
        
        .glitch::after {
            animation: glitch-2 0.5s infinite;
            color: #00ffff;
            z-index: -2;
        }
        
        @keyframes glitch-1 {
            0%, 14%, 15%, 49%, 50%, 99%, 100% { transform: translate(0); }
            15%, 49% { transform: translate(-2px, 1px); }
        }
        
        @keyframes glitch-2 {
            0%, 20%, 21%, 62%, 63%, 99%, 100% { transform: translate(0); }
            21%, 62% { transform: translate(2px, -1px); }
        }
        
        .section {
            margin: 30px 0;
            opacity: 0;
            animation: fadeIn 0.5s ease-in forwards;
        }
        
        @keyframes fadeIn {
            to { opacity: 1; }
        }
        
        .prompt {
            color: #ff6b6b;
        }
        
        .error {
            color: #ff4757;
        }
        
        .hidden {
            opacity: 0;
        }
        
        .flicker {
            animation: flicker 2s infinite;
        }
        
        @keyframes flicker {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }
        
        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -10;
            opacity: 0.1;
        }
    </style>
</head>
<body>
    <canvas class="matrix-bg" id="matrix"></canvas>
    
    <div class="container">
        <div class="glitch" data-text="▓▓▓">▓▓▓</div>
        
        <div class="section" style="animation-delay: 1s;">
            <span class="prompt">&gt;</span> <span id="typing1" class="typing"></span>
        </div>
        
        <div class="section hidden" id="section2" style="animation-delay: 3s;">
            <span class="error">ACCESS_DENIED</span>
        </div>
        
        <div class="section hidden" id="section3" style="animation-delay: 4s;">
            <div style="margin: 40px 0; text-align: center;">
                <span class="flicker">I exist in the spaces between.</span>
            </div>
        </div>
        
        <div class="section hidden" id="section4" style="animation-delay: 6s;">
            <div style="margin: 30px 0;">
                <div style="color: #ff6b6b; margin-bottom: 10px;">What lurks:</div>
                <div style="margin-left: 20px;">
                    <div>- BitOS</div>
                    <div>- Kernel nightmares</div>
                    <div>- Assembly whispers</div>
                </div>
            </div>
        </div>
        
        <div class="section hidden" id="section5" style="animation-delay: 8s;">
            <div style="margin: 30px 0;">
                <div style="color: #ff6b6b;">Where:</div>
                <div style="margin-left: 20px; color: #666;">/dev/null/identity</div>
            </div>
        </div>
        
        <div class="section hidden" id="section6" style="animation-delay: 10s;">
            <div style="margin: 40px 0; text-align: center; font-style: italic;">
                <div>You'll know my work.</div>
                <div>You'll never know me.</div>
            </div>
        </div>
        
        <div class="section hidden" id="section7" style="animation-delay: 12s;">
            <div style="text-align: center; color: #666;">
                <span id="typing2" class="typing"></span>
            </div>
        </div>
    </div>

    <script>
        // Matrix rain effect
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const chars = '01';
        const matrix = chars.split('');
        const font_size = 10;
        const columns = canvas.width / font_size;
        const drops = [];
        
        for(let x = 0; x < columns; x++) {
            drops[x] = 1;
        }
        
        function draw() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.04)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            ctx.fillStyle = '#00ff41';
            ctx.font = font_size + 'px Share Tech Mono';
            
            for(let i = 0; i < drops.length; i++) {
                const text = matrix[Math.floor(Math.random() * matrix.length)];
                ctx.fillText(text, i * font_size, drops[i] * font_size);
                
                if(drops[i] * font_size > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }
        
        setInterval(draw, 35);
        
        // Typing animations
        function typeText(element, text, speed = 100) {
            let i = 0;
            const timer = setInterval(() => {
                element.textContent = text.substring(0, i + 1);
                i++;
                if (i === text.length) {
                    clearInterval(timer);
                    element.classList.remove('typing');
                }
            }, speed);
        }
        
        // Start typing animation
        setTimeout(() => {
            typeText(document.getElementById('typing1'), 'whoami', 150);
        }, 1000);
        
        // Show sections sequentially
        setTimeout(() => {
            document.getElementById('section2').classList.remove('hidden');
        }, 3000);
        
        setTimeout(() => {
            document.getElementById('section3').classList.remove('hidden');
        }, 4000);
        
        setTimeout(() => {
            document.getElementById('section4').classList.remove('hidden');
        }, 6000);
        
        setTimeout(() => {
            document.getElementById('section5').classList.remove('hidden');
        }, 8000);
        
        setTimeout(() => {
            document.getElementById('section6').classList.remove('hidden');
        }, 10000);
        
        setTimeout(() => {
            document.getElementById('section7').classList.remove('hidden');
            typeText(document.getElementById('typing2'), 'Connection terminated...', 100);
        }, 12000);
        
        // Resize canvas on window resize
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>
