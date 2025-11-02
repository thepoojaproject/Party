<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Diwali Crackers Burst</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: #0a0a2a;
            color: white;
            font-family: 'Arial', sans-serif;
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
        }
        
        h1 {
            font-size: 3rem;
            margin-bottom: 20px;
            text-shadow: 0 0 10px #ff9933, 0 0 20px #ff9933;
            color: #ffcc00;
        }
        
        .subtitle {
            font-size: 1.2rem;
            margin-bottom: 30px;
            color: #ffcc00;
        }
        
        .controls {
            margin: 20px 0;
        }
        
        button {
            background: linear-gradient(to bottom, #ff9933, #cc6600);
            border: none;
            color: white;
            padding: 12px 25px;
            margin: 0 10px;
            border-radius: 30px;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 0 0 15px rgba(255, 153, 51, 0.7);
            transition: all 0.3s ease;
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
        }
        
        .show {
            opacity: 1;
        }
        
        .diya {
            width: 80px;
            height: 80px;
            position: relative;
            margin: 20px auto;
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
    </style>
</head>
<body>
    <div class="container">
        <h1>Happy Diwali!</h1>
        <p class="subtitle">Celebrate with virtual firecrackers</p>
        
        <div class="diya">
            <div class="flame"></div>
            <div class="base"></div>
        </div>
        
        <div class="controls">
            <button id="burstBtn">Burst Crackers</button>
            <button id="autoBtn">Auto Mode</button>
            <button id="stopBtn">Stop</button>
        </div>
        
        <p class="message" id="message">Wishing you prosperity and happiness!</p>
    </div>
    
    <div class="canvas-container">
        <canvas id="canvas"></canvas>
    </div>

    <script>
        // Canvas setup
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const message = document.getElementById('message');
        
        // Set canvas to full window size
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);
        
        // Particle class for firecracker effects
        class Particle {
            constructor(x, y, color, velocity, size, decay) {
                this.x = x;
                this.y = y;
                this.color = color;
                this.velocity = velocity;
                this.size = size;
                this.decay = decay;
                this.alpha = 1;
                this.gravity = 0.01;
            }
            
            update() {
                this.velocity.x *= 0.99;
                this.velocity.y *= 0.99;
                this.velocity.y += this.gravity;
                
                this.x += this.velocity.x;
                this.y += this.velocity.y;
                
                this.alpha -= this.decay;
                this.size -= this.decay * 2;
            }
            
            draw() {
                ctx.save();
                ctx.globalAlpha = this.alpha;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }
        }
        
        // Firecracker burst effect
        class Firecracker {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.particles = [];
                this.colors = [
                    '#ff0000', '#ff9900', '#ffff00', '#00ff00', 
                    '#00ffff', '#0000ff', '#ff00ff', '#ffffff'
                ];
                this.createBurst();
            }
            
            createBurst() {
                const particleCount = 150;
                
                for (let i = 0; i < particleCount; i++) {
                    const angle = Math.random() * Math.PI * 2;
                    const speed = Math.random() * 5 + 2;
                    const velocity = {
                        x: Math.cos(angle) * speed,
                        y: Math.sin(angle) * speed
                    };
                    
                    const color = this.colors[Math.floor(Math.random() * this.colors.length)];
                    const size = Math.random() * 3 + 1;
                    const decay = Math.random() * 0.02 + 0.005;
                    
                    this.particles.push(new Particle(
                        this.x, this.y, color, velocity, size, decay
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
        
        // Main animation variables
        let firecrackers = [];
        let sparklers = [];
        let animationId;
        let autoMode = false;
        
        // Create a random firecracker burst
        function createFirecracker() {
            const x = Math.random() * canvas.width;
            const y = Math.random() * canvas.height * 0.8;
            firecrackers.push(new Firecracker(x, y));
            
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
        
        // Show festive message
        function showMessage() {
            const messages = [
                "Happy Diwali!",
                "Shubh Deepawali!",
                "Spread the light!",
                "Joy and Prosperity!",
                "Let's celebrate!"
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
            
            // Auto mode - create random effects
            if (autoMode) {
                if (Math.random() > 0.95) {
                    createFirecracker();
                }
                
                if (Math.random() > 0.97) {
                    createSparkler();
                }
            }
            
            animationId = requestAnimationFrame(animate);
        }
        
        // Start the animation
        animate();
        
        // Event listeners for buttons
        document.getElementById('burstBtn').addEventListener('click', function() {
            createFirecracker();
            createSparkler();
        });
        
        document.getElementById('autoBtn').addEventListener('click', function() {
            autoMode = true;
            showMessage();
        });
        
        document.getElementById('stopBtn').addEventListener('click', function() {
            autoMode = false;
        });
        
        // Also create firecrackers on click anywhere
        canvas.addEventListener('click', function(e) {
            const rect = canvas.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            firecrackers.push(new Firecracker(x, y));
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
