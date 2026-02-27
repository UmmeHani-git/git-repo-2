<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DevOps Learning</title>

<style>
:root {
  --bg-color: #0f172a;
  --card-bg: rgba(255,255,255,0.08);
  --text-color: white;
  --accent: #00f5ff;
}

body.light {
  --bg-color: #f1f5f9;
  --card-bg: rgba(0,0,0,0.05);
  --text-color: #0f172a;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', sans-serif;
}

body {
  background: var(--bg-color);
  color: var(--text-color);
  overflow: hidden;
  transition: 0.3s ease;
}

canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
}

.container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 20px;
}

.card {
  background: var(--card-bg);
  backdrop-filter: blur(20px);
  padding: 50px;
  border-radius: 20px;
  box-shadow: 0 0 40px rgba(0,255,255,0.2);
  animation: fadeIn 1.5s ease-in-out;
  max-width: 600px;
}

h1 {
  font-size: 3rem;
  background: linear-gradient(90deg, #00f5ff, #00ff9f);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 20px;
}

p {
  font-size: 1.2rem;
  opacity: 0.8;
  margin-bottom: 30px;
}

.badges {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 30px;
}

.badge {
  padding: 8px 15px;
  border-radius: 20px;
  background: rgba(0,255,255,0.15);
  font-size: 0.9rem;
}

.btn {
  padding: 12px 30px;
  background: linear-gradient(90deg, #00f5ff, #00ff9f);
  border: none;
  border-radius: 30px;
  font-size: 1rem;
  cursor: pointer;
  color: black;
  font-weight: bold;
  transition: 0.3s ease;
  margin: 5px;
}

.btn:hover {
  transform: scale(1.1);
  box-shadow: 0 0 20px #00ff9f;
}

.toggle {
  position: absolute;
  top: 20px;
  right: 20px;
  cursor: pointer;
  font-size: 0.9rem;
  padding: 8px 15px;
  border-radius: 20px;
  background: rgba(255,255,255,0.1);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

@media(max-width: 768px){
  h1 { font-size: 2rem; }
  .card { padding: 30px; }
}
</style>
</head>
<body>

<div class="toggle" onclick="toggleMode()">🌗 Toggle Mode</div>

<canvas id="bg"></canvas>

<div class="container">
  <div class="card">
    <h1>Welcome to DevOps Learning 🚀</h1>
    <p>Master CI/CD, Containers, Cloud & Automation</p>

    <div class="badges">
      <div class="badge">Docker</div>
      <div class="badge">Kubernetes</div>
      <div class="badge">Jenkins</div>
      <div class="badge">AWS</div>
      <div class="badge">Terraform</div>
    </div>

    <button class="btn">Start Learning</button>
    <button class="btn" onclick="alert('More content coming soon!')">Explore</button>
  </div>
</div>

<script>
const canvas = document.getElementById('bg');
const ctx = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particles = [];

for (let i = 0; i < 80; i++) {
  particles.push({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    radius: 2,
    dx: (Math.random() - 0.5),
    dy: (Math.random() - 0.5)
  });
}

function drawLines(p1, p2) {
  let dist = Math.hypot(p1.x - p2.x, p1.y - p2.y);
  if (dist < 120) {
    ctx.strokeStyle = "rgba(0,255,255,0.2)";
    ctx.lineWidth = 1;
    ctx.beginPath();
    ctx.moveTo(p1.x, p1.y);
    ctx.lineTo(p2.x, p2.y);
    ctx.stroke();
  }
}

function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  particles.forEach((p, index) => {
    ctx.fillStyle = "#00f5ff";
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
    ctx.fill();

    p.x += p.dx;
    p.y += p.dy;

    if (p.x < 0 || p.x > canvas.width) p.dx *= -1;
    if (p.y < 0 || p.y > canvas.height) p.dy *= -1;

    for (let j = index + 1; j < particles.length; j++) {
      drawLines(p, particles[j]);
    }
  });

  requestAnimationFrame(animate);
}

animate();

window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
});

function toggleMode() {
  document.body.classList.toggle("light");
}
</script>

</body>
</html>
