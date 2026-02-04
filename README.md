
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Favorite Person</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&family=Playfair+Display:ital,wght@0,700;1,700&family=Dancing+Script:wght@600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary: #ff4d6d;
            --bg: #0a0a0c;
        }

        body {
            background-color: var(--bg);
            color: #ffffff;
            font-family: 'Inter', sans-serif;
            overflow-x: hidden;
            margin: 0;
        }

        .glass {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 24px;
        }

        .gradient-text {
            background: linear-gradient(45deg, #ff4d6d, #ff8fa3);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .handwritten {
            font-family: 'Dancing Script', cursive;
        }

        .floating {
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }

        .heart-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
            opacity: 0.2;
        }

        #no-button {
            transition: all 0.15s ease;
        }

        .letter-scroll::-webkit-scrollbar {
            width: 4px;
        }
        .letter-scroll::-webkit-scrollbar-thumb {
            background: rgba(255, 77, 109, 0.3);
            border-radius: 10px;
        }
    </style>
</head>
<body class="flex flex-col items-center justify-center min-h-screen p-4">

    <canvas id="heartCanvas" class="heart-bg"></canvas>

    <div id="step-1" class="max-w-md w-full glass p-8 text-center space-y-6 reveal active">
        <h2 class="text-sm uppercase tracking-[0.3em] text-gray-400">February 14, 2026</h2>
        <h1 class="text-4xl font-bold font-serif italic">Hey, Api. 👋</h1>
        <p class="text-gray-300 leading-relaxed">
            I have a very important question for you... 🤫
        </p>
        <button onclick="nextStep(2)" class="px-8 py-3 bg-white text-black rounded-full font-semibold hover:scale-105 transition-all">
            Unlock Message 🔓
        </button>
    </div>

    <div id="step-2" class="max-w-lg w-full glass p-10 text-center space-y-8 hidden">
        <div class="floating text-6xl">💝</div>
        <h1 class="text-4xl md:text-5xl font-bold leading-tight">
            Will you be my <span class="gradient-text">Valentine?</span>
        </h1>
        <p class="text-gray-400 italic">No is not an option (I've made sure of it) 🎀</p>
        
        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center mt-8">
            <button onclick="celebrate()" class="px-10 py-4 bg-white text-black rounded-full font-bold text-lg hover:shadow-[0_0_30px_rgba(255,255,255,0.4)] transition-all">
                YES! 💍
            </button>
            <button id="no-button" onmouseover="moveNoButton()" class="px-10 py-4 border border-white/20 rounded-full font-semibold">
                No 🏃‍♀️💨
            </button>
        </div>
    </div>

    <div id="step-3" class="max-w-2xl w-full glass p-8 md:p-12 text-center space-y-6 hidden">
        <div class="inline-block px-4 py-1 rounded-full border border-pink-500/30 text-pink-400 text-xs font-bold tracking-widest uppercase mb-4">
            Official Valentine Status: Active ✅
        </div>
        
        <h1 class="text-4xl font-serif italic font-bold gradient-text">Thank you, KABAB! 💖</h1>
        
        <div class="letter-scroll max-h-[450px] overflow-y-auto pr-2 text-left space-y-6 mt-6">
            <p class="text-gray-200 leading-relaxed handwritten text-3xl">
                My RUBAB, 🌸
            </p>
            <p class="text-gray-300 leading-relaxed text-lg">
                I just wanted to take a second to tell you how much you mean to me. 🧸 I know I call you "crusty" sometimes, but honestly? You’re the most amazing part of my day. ✨
            </p>
            <p class="text-gray-300 leading-relaxed text-lg font-semibold border-l-2 border-pink-500 pl-4 italic">
                They always say that <span class="text-pink-400">"R" letter people are the absolute BEST</span> and it’s totally true. 👸 You have this way of staying forever in someone's heart once you're there. ♾️💖 
            </p>
            <p class="text-gray-300 leading-relaxed text-lg">
                Thank you for being my person, for the endless laughs 😂, and for staying by my side through everything. Life is just better with you in it. 🌈☁️
            </p>
            <p class="text-gray-300 leading-relaxed text-lg">
                Let's make some more chaotic memories together! 🥂🔥
            </p>
            <p class="text-pink-400 font-bold handwritten text-4xl pt-4">
                Love you forever, 💋 <br>
                [RUBAB] 🏹
            </p>
        </div>

        <div class="pt-8 border-t border-white/10 mt-6">
            <p class="text-gray-500 text-xs tracking-tighter uppercase">Created with ❤️ just for you</p>
        </div>
    </div>

    <script>
        function nextStep(step) {
            const current = document.querySelector('.active') || document.getElementById('step-2');
            current.style.opacity = '0';
            current.style.transform = 'translateY(-20px)';
            
            setTimeout(() => {
                current.classList.add('hidden');
                current.classList.remove('active');
                const next = document.getElementById(`step-${step}`);
                next.classList.remove('hidden');
                setTimeout(() => {
                    next.classList.add('active');
                    next.style.opacity = '1';
                    next.style.transform = 'translateY(0)';
                }, 50);
            }, 600);
        }

        function moveNoButton() {
            const btn = document.getElementById('no-button');
            const x = Math.random() * (window.innerWidth - btn.offsetWidth - 50);
            const y = Math.random() * (window.innerHeight - btn.offsetHeight - 50);
            btn.style.position = 'fixed';
            btn.style.left = x + 'px';
            btn.style.top = y + 'px';
            btn.style.zIndex = '1000';
        }

        function celebrate() {
            const count = 200;
            const defaults = { origin: { y: 0.7 }, zIndex: 9999 };
            function fire(particleRatio, opts) {
                confetti(Object.assign({}, defaults, opts, {
                    particleCount: Math.floor(count * particleRatio)
                }));
            }
            fire(0.25, { spread: 26, startVelocity: 55 });
            fire(0.2, { spread: 60 });
            fire(0.35, { spread: 100, decay: 0.91, scalar: 0.8 });
            fire(0.1, { spread: 120, startVelocity: 25, decay: 0.92, scalar: 1.2 });
            fire(0.1, { spread: 120, startVelocity: 45 });
            nextStep(3);
        }

        const canvas = document.getElementById('heartCanvas');
        const ctx = canvas.getContext('2d');
        let hearts = [];
        function resize() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
        class Heart {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * canvas.width;
                this.y = canvas.height + 20;
                this.size = Math.random() * 10 + 2;
                this.speed = Math.random() * 1.5 + 0.5;
                this.opacity = Math.random() * 0.4;
            }
            update() { this.y -= this.speed; if (this.y < -20) this.reset(); }
            draw() {
                ctx.fillStyle = `rgba(255, 77, 109, ${this.opacity})`;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }
        function init() {
            resize();
            for (let i = 0; i < 50; i++) hearts.push(new Heart());
            animate();
        }
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            hearts.forEach(h => { h.update(); h.draw(); });
            requestAnimationFrame(animate);
        }
        window.addEventListener('resize', resize);
        init();
    </script>
</body>
</html>
