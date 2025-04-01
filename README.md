<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy 19th Birthday</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: black;
            color: white;
            text-align: center;
            font-family: Arial, sans-serif;
        }
        #message {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 3em;
            font-weight: bold;
            z-index: 10;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
</head>
<body>
    <div id="message">Happy 19th Birthday!</div>
    <canvas id="fireworks"></canvas>
    <script>
        const canvas = document.getElementById("fireworks");
        const ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;class Firework {
        constructor(x, y, color) {
            this.x = x;
            this.y = y;
            this.color = color;
            this.particles = [];
            for (let i = 0; i < 50; i++) {
                this.particles.push({
                    x: this.x,
                    y: this.y,
                    angle: Math.random() * 2 * Math.PI,
                    speed: Math.random() * 4 + 1,
                    alpha: 1
                });
            }
        }
        update() {
            this.particles.forEach(p => {
                p.x += Math.cos(p.angle) * p.speed;
                p.y += Math.sin(p.angle) * p.speed;
                p.alpha -= 0.02;
            });
            this.particles = this.particles.filter(p => p.alpha > 0);
        }
        draw() {
            this.particles.forEach(p => {
                ctx.globalAlpha = p.alpha;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(p.x, p.y, 3, 0, Math.PI * 2);
                ctx.fill();
            });
        }
    }
    
    let fireworks = [];
    function animate() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        if (Math.random() < 0.05) {
            fireworks.push(new Firework(
                Math.random() * canvas.width,
                Math.random() * canvas.height * 0.5,
                `hsl(${Math.random() * 360}, 100%, 50%)`
            ));
        }
        fireworks.forEach(firework => {
            firework.update();
            firework.draw();
        });
        fireworks = fireworks.filter(f => f.particles.length > 0);
        requestAnimationFrame(animate);
    }
    animate();
</script>

</body>
</html>
