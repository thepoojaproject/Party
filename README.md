
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Diwali Firecracker Animation</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: #0a0a2a;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            position: relative;
        }
        
        .container {
            text-align: center;
            z-index: 10;
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 15px;
            text-shadow: 0 0 10px #ff9933, 0 0 20px #ff9933, 0 0 30px #ff9933;
            color: #ffcc00;
            letter-spacing: 2px;
            animation: glow 2s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from {
                text-shadow: 0 0 10px #ff9933, 0 0 20px #ff9933, 0 0 30px #ff9933;
            }
            to {
                text-shadow: 0 0 15px #ff9933, 0 0 25px #ff9933, 0 0 35px #ff9933, 0 0 45px #ff9933;
            }
        }
        
        .subtitle {
            font-size: 1.3rem;
            margin-bottom: 30px;
            color: #ffcc00;
            font-weight: 300;
        }
        
        .festival-info {
            background: rgba(255, 204, 0, 0.1);
            border-radius: 15px;
            padding: 15px;
            margin: 20px 0;
            border: 1px solid rgba(255, 204, 0, 0.3);
            backdrop-filter: blur(5px);
        }
        
        .festival-info p {
            margin: 10px 0;
            line-height: 1.5;
        }
        
        .controls {
            margin: 25px 0;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 15px;
        }
        
        button {
            background: linear-gradient(to bottom, #ff9933, #cc6600);
            border: none;
            color: white;
            padding: 12px 25px;
            border-radius: 30px;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 0 0 15px rgba(255, 153, 51, 0.7);
            transition: all 0.3s ease;
            min-width: 150px;
            font-weight: bold;
            letter-spacing: 1px;
        }
        
        button:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px rgba(255, 153, 51, 0.9);
        }
        
        .canvas-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        
        .message {
            margin-top: 30px;
            font-size: 1.5rem;
            color: #ffcc00;
            text-shadow: 0 0 5px rgba(255, 204, 0, 0.7);
            opacity: 0;
            transition: opacity 1s;
            min-height: 40px;
            font-weight: bold;
        }
        
        .show {
            opacity: 1;
        }
        
        .diya-container {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 25px 0;
        }
        
        .diya {
            width: 80px;
            height: 80px;
            position: relative;
        }
        
        .flame {
            width: 30px;
            height: 50px;
            background: radial-gradient(ellipse at center, #ffcc00 0%, #ff6600 70%, transparent 100%);
            border-radius: 50% 50% 20% 20%;
            margin: 0 auto;
            position: relative;
            animation: flicker 0.8s infinite alternate;
            box-shadow: 0 0 20px #ff6600, 0 0 40px #ff9933;
        }
        
        @keyframes flicker {
            0% { transform: scaleY(1); opacity: 0.9; }
            100% { transform: scaleY(1.1); opacity: 1; }
        }
        
        .base {
            width: 70px;
            height: 20px;
            background: linear-gradient(to bottom, #cc6600, #663300);
            border-radius: 0 0 10px 10px;
            margin: 0 auto;
        }
        
        .footer {
            margin-top: 30px;
            font-size: 0.9rem;
            color: #aaa;
        }
        
        .counter {
            margin: 15px 0;
            font-size: 1.2rem;
            color: #ffcc00;
            font-weight: bold;
        }
        
        /* Rangoli decoration */
        .rangoli {
            position: absolute;
            bottom: 20px;
            width: 200px;
            height: 200px;
            background: radial-gradient(circle, transparent 30%, rgba(255, 204, 0, 0.2) 70%);
            border-radius: 50%;
            z-index: 2;
            animation: rotate 20s linear infinite;
        }
        
        .rangoli::before, .rangoli::after {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            border: 2px dashed rgba(255, 204, 0, 0.5);
            border-radius: 50%;
            top: 0;
            left: 0;
        }
        
        .rangoli::before {
            transform: rotate(60deg);
        }
        
        .rangoli::after {
            transform: rotate(120deg);
        }
        
        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Responsive adjustments */
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            
            .subtitle {
                font-size: 1.1rem;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
            
            button {
                width: 80%;
            }
            
            .diya-container {
                gap: 15px;
            }
            
            .rangoli {
                width: 150px;
                height: 150px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Happy Diwali!</h1>
        <p class="subtitle">Celebrate with virtual firecrackers - Safe and Eco-friendly</p>
        
        <div class="festival-info">
            <p>Diwali, the Festival of Lights, symbolizes the victory of light over darkness and good over evil.</p>
            <p>Celebrate responsibly with these virtual fireworks!</p>
        </div>
        
        <div class="diya-container">
            <div class="diya">
                <div class="flame"></div>
                <div class="base"></div>
            </div>
            <div class="diya">
                <div class="flame"></div>
                <div class="base"></div>
            </div>
            <div class="diya">
                <div class="flame"></div>
                <div class="base"></div>
            </div>
        </div>
        
        <div class="counter">
            Fireworks Burst: <span id="counter">0</span>
        </div>
        
        <div class="controls">
            <button id="burstBtn">Burst Crackers</button>
            <button id="autoBtn">Auto Mode</button>
            <button id="stopBtn">Stop</button>
            <button id="resetBtn">Reset</button>
        </div>
        
        <p class="message" id="message">Wishing you prosperity and happiness!</p>
        
        <div class="footer">
            <p>Click anywhere on the screen to create fireworks!</p>
        </div>
    </div>
    
    <div class="rangoli"></div>
    
    <div class="canvas-container">
        <canvas id="canvas"></canvas>
    </div>

    <script>
        // Canvas setup
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const message = document.getElementById('message');
        const counterElement = document.getElementById('counter');
        
        // Set canvas to full window size
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        // Particle class for firecracker effects
        class Particle {
            constructor(x, y, color, velocity, size, decay, shape = 'circle') {
                this.x = x;
                this.y = y;
                this.color = color;
                this.velocity = velocity;
                this.size = size;
                this.decay = decay;
                this.alpha = 1;
                this.gravity = 0.01;
                this.shape = shape;
                this.rotation = Math.random() * Math.PI * 2;
                this.rotationSpeed = (Math.random() - 0.5) * 0.1;
            }
            
            update() {
                this.velocity.x *= 0.99;
                this.velocity.y *= 0.99;
                this.velocity.y += this.gravity;
                
                this.x += this.velocity.x;
                this.y += this.velocity.y;
                
                this.alpha -= this.decay;
                this.size -= this.decay * 2;
                this.rotation += this.rotationSpeed;
            }
            
            draw() {
                ctx.save();
                ctx.globalAlpha = this.alpha;
                ctx.fillStyle = this.color;
                ctx.translate(this.x, this.y);
                ctx.rotate(this.rotation);
                
                if (this.shape === 'circle') {
                    ctx.beginPath();
                    ctx.arc(0, 0, this.size, 0, Math.PI * 2);
                    ctx.fill();
                } else if (this.shape === 'star') {
                    this.drawStar(0, 0, this.size, this.size * 0.5, 5);
                } else if (this.shape === 'square') {
                    ctx.fillRect(-this.size, -this.size, this.size * 2, this.size * 2);
                }
                
                ctx.restore();
            }
            
            drawStar(cx, cy, outerRadius, innerRadius, points) {
                let rot = Math.PI / 2 * 3;
                let x = cx;
                let y = cy;
                const step = Math.PI / points;
                
                ctx.beginPath();
                ctx.moveTo(cx, cy - outerRadius);
                
                for (let i = 0; i < points; i++) {
                    x = cx + Math.cos(rot) * outerRadius;
                    y = cy + Math.sin(rot) * outerRadius;
                    ctx.lineTo(x, y);
                    rot += step;
                    
                    x = cx + Math.cos(rot) * innerRadius;
                    y = cy + Math.sin(rot) * innerRadius;
                    ctx.lineTo(x, y);
                    rot += step;
                }
                
                ctx.lineTo(cx, cy - outerRadius);
                ctx.closePath();
                ctx.fill();
            }
        }
        
        // Firecracker burst effect
        class Firecracker {
            constructor(x, y, type = 'normal') {
                this.x = x;
                this.y = y;
                this.particles = [];
                this.type = type;
                this.colors = [
                    '#ff0000', '#ff9900', '#ffff00', '#00ff00', 
                    '#00ffff', '#0000ff', '#ff00ff', '#ffffff'
                ];
                this.createBurst();
            }
            
            createBurst() {
                const particleCount = this.type === 'normal' ? 150 : 200;
                const shapes = this.type === 'special' ? ['circle', 'star', 'square'] : ['circle'];
                
                for (let i = 0; i < particleCount; i++) {
                    const angle = Math.random() * Math.PI * 2;
                    const speed = Math.random() * (this.type === 'special' ? 7 : 5) + 2;
                    const velocity = {
                        x: Math.cos(angle) * speed,
                        y: Math.sin(angle) * speed
                    };
                    
                    const color = this.colors[Math.floor(Math.random() * this.colors.length)];
                    const size = Math.random() * (this.type === 'special' ? 4 : 3) + 1;
                    const decay = Math.random() * 0.02 + 0.005;
                    const shape = shapes[Math.floor(Math.random() * shapes.length)];
                    
                    this.particles.push(new Particle(
                        this.x, this.y, color, velocity, size, decay, shape
                    ));
                }
            }
            
            update() {
                this.particles.forEach((particle, index) => {
                    particle.update();
                    
                    if (particle.alpha <= 0 || particle.size <= 0) {
                        this.particles.splice(index, 1);
                    }
                });
            }
            
            draw() {
                this.particles.forEach(particle => particle.draw());
            }
            
            isFinished() {
                return this.particles.length === 0;
            }
        }
        
        // Sparkler effect
        class Sparkler {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.particles = [];
                this.timer = 0;
                this.duration = 100;
            }
            
            update() {
                this.timer++;
                
                // Create new particles
                if (this.timer < this.duration) {
                    for (let i = 0; i < 3; i++) {
                        const angle = Math.random() * Math.PI * 2;
                        const speed = Math.random() * 2;
                        const velocity = {
                            x: Math.cos(angle) * speed,
                            y: Math.sin(angle) * speed
                        };
                        
                        const color = i === 0 ? '#ff9900' : i === 1 ? '#ffff00' : '#ffffff';
                        const size = Math.random() * 2 + 1;
                        const decay = Math.random() * 0.03 + 0.01;
                        
                        this.particles.push(new Particle(
                            this.x, this.y, color, velocity, size, decay
                        ));
                    }
                }
                
                // Update existing particles
                this.particles.forEach((particle, index) => {
                    particle.update();
                    
                    if (particle.alpha <= 0 || particle.size <= 0) {
                        this.particles.splice(index, 1);
                    }
                });
            }
            
            draw() {
                this.particles.forEach(particle => particle.draw());
                
                // Draw sparkler center
                ctx.save();
                ctx.fillStyle = '#ffcc00';
                ctx.beginPath();
                ctx.arc(this.x, this.y, 3, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }
            
            isFinished() {
                return this.timer >= this.duration && this.particles.length === 0;
            }
        }
        
        // Fountain effect
        class Fountain {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.particles = [];
                this.timer = 0;
                this.duration = 120;
                this.colors = ['#ff0000', '#ff9900', '#ffff00', '#00ff00'];
            }
            
            update() {
                this.timer++;
                
                // Create new particles
                if (this.timer < this.duration) {
                    for (let i = 0; i < 5; i++) {
                        const angle = Math.random() * Math.PI * 0.4 - Math.PI * 0.2;
                        const speed = Math.random() * 4 + 3;
                        const velocity = {
                            x: Math.cos(angle) * speed,
                            y: Math.sin(angle) * speed - 8
                        };
                        
                        const color = this.colors[Math.floor(Math.random() * this.colors.length)];
                        const size = Math.random() * 2 + 1;
                        const decay = Math.random() * 0.015 + 0.005;
                        
                        this.particles.push(new Particle(
                            this.x, this.y, color, velocity, size, decay
                        ));
                    }
                }
                
                // Update existing particles
                this.particles.forEach((particle, index) => {
                    particle.update();
                    
                    if (particle.alpha <= 0 || particle.size <= 0) {
                        this.particles.splice(index, 1);
                    }
                });
            }
            
            draw() {
                this.particles.forEach(particle => particle.draw());
            }
            
            isFinished() {
                return this.timer >= this.duration && this.particles.length === 0;
            }
        }
        
        // Main animation variables
        let firecrackers = [];
        let sparklers = [];
        let fountains = [];
        let animationId;
        let autoMode = false;
        let burstCounter = 0;
        
        // Create a random firecracker burst
        function createFirecracker(type = 'normal') {
            const x = Math.random() * canvas.width;
            const y = Math.random() * canvas.height * 0.8;
            firecrackers.push(new Firecracker(x, y, type));
            
            burstCounter++;
            counterElement.textContent = burstCounter;
            
            // Show message occasionally
            if (Math.random() > 0.7) {
                showMessage();
            }
        }
        
        // Create a sparkler
        function createSparkler() {
            const x = Math.random() * canvas.width;
            const y = Math.random() * canvas.height * 0.8;
            sparklers.push(new Sparkler(x, y));
        }
        
        // Create a fountain
        function createFountain() {
            const x = Math.random() * canvas.width;
            const y = canvas.height * 0.9;
            fountains.push(new Fountain(x, y));
        }
        
        // Show festive message
        function showMessage() {
            const messages = [
                "Happy Diwali!",
                "Shubh Deepawali!",
                "Spread the light!",
                "Joy and Prosperity!",
                "Let's celebrate!",
                "Light up your life!",
                "May goodness prevail!",
                "Wishing you happiness!"
            ];
            
            message.textContent = messages[Math.floor(Math.random() * messages.length)];
            message.classList.add('show');
            
            setTimeout(() => {
                message.classList.remove('show');
            }, 2000);
        }
        
        // Animation loop
        function animate() {
            // Clear canvas with a dark blue background and slight transparency for trail effect
            ctx.fillStyle = 'rgba(10, 10, 42, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Update and draw firecrackers
            firecrackers.forEach((firecracker, index) => {
                firecracker.update();
                firecracker.draw();
                
                if (firecracker.isFinished()) {
                    firecrackers.splice(index, 1);
                }
            });
            
            // Update and draw sparklers
            sparklers.forEach((sparkler, index) => {
                sparkler.update();
                sparkler.draw();
                
                if (sparkler.isFinished()) {
                    sparklers.splice(index, 1);
                }
            });
            
            // Update and draw fountains
            fountains.forEach((fountain, index) => {
                fountain.update();
                fountain.draw();
                
                if (fountain.isFinished()) {
                    fountains.splice(index, 1);
                }
            });
            
            // Auto mode - create random effects
            if (autoMode) {
                if (Math.random() > 0.93) {
                    createFirecracker(Math.random() > 0.8 ? 'special' : 'normal');
                }
                
                if (Math.random() > 0.95) {
                    createSparkler();
                }
                
                if (Math.random() > 0.97) {
                    createFountain();
                }
            }
            
            animationId = requestAnimationFrame(animate);
        }
        
        // Start the animation
        animate();
        
        // Event listeners for buttons
        document.getElementById('burstBtn').addEventListener('click', function() {
            createFirecracker();
            if (Math.random() > 0.5) createSparkler();
            if (Math.random() > 0.7) createFountain();
        });
        
        document.getElementById('autoBtn').addEventListener('click', function() {
            autoMode = true;
            showMessage();
        });
        
        document.getElementById('stopBtn').addEventListener('click', function() {
            autoMode = false;
        });
        
        document.getElementById('resetBtn').addEventListener('click', function() {
            firecrackers = [];
            sparklers = [];
            fountains = [];
            burstCounter = 0;
            counterElement.textContent = burstCounter;
        });
        
        // Also create firecrackers on click anywhere
        canvas.addEventListener('click', function(e) {
            const rect = canvas.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            firecrackers.push(new Firecracker(x, y, Math.random() > 0.7 ? 'special' : 'normal'));
            burstCounter++;
            counterElement.textContent = burstCounter;
            
            if (Math.random() > 0.5) {
                createSparkler();
            }
        });
        
        // Create initial effects
        for (let i = 0; i < 3; i++) {
            setTimeout(() => {
                createFirecracker();
            }, i * 500);
        }
    </script>
</body>
</html>
