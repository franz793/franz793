<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Birthday Surprise</title>
    <style>
        body {
            text-align: center;
            background-color: #ffebcd;
            font-family: Arial, sans-serif;
        }
        #message {
            display: none;
            font-size: 2em;
            color: #ff1493;
            margin-top: 20px;
        }
        .btn {
            margin-top: 50px;
            padding: 10px 20px;
            font-size: 1.5em;
            cursor: pointer;
            background-color: #ff1493;
            color: white;
            border: none;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <h1>Click the button for a surprise!</h1>
    <button class="btn" onclick="showMessage()">Surprise Me!</button>
    <div id="thank you for existing">🎉 Happy Birthday! 🎂🎁</div><script>
    function showMessage() {
        document.getElementById('message').style.display = 'block';
        confetti();
    }

    function confetti() {
        let end = Date.now() + (5 * 1000);
        (function frame() {
            if (Date.now() > end) return;
            for (let i = 0; i < 10; i++) {
                let confetti = document.createElement('div');
                confetti.innerText = '🎉';
                confetti.style.position = 'absolute';
                confetti.style.left = Math.random() * window.innerWidth + 'px';
                confetti.style.top = Math.random() * window.innerHeight + 'px';
                confetti.style.fontSize = Math.random() * 20 + 20 + 'px';
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 2000);
            }
            requestAnimationFrame(frame);
        })();
    }
</script>

</body>
</html>
