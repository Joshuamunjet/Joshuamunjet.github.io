# Joshuamunjet.github.io<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Joshua Munjet — Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --card: #16161f;
    --accent: #f0c040;
    --accent2: #40e0ff;
    --accent3: #ff5f7e;
    --text: #e8e8f0;
    --muted: #7070a0;
    --border: rgba(255,255,255,0.07);
    --mono: 'Space Mono', monospace;
    --sans: 'Syne', sans-serif;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    overflow-x: hidden;
    cursor: none;
  }

  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    mix-blend-mode: difference;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: all 0.12s ease;
    opacity: 0.6;
  }

  #bg-canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    opacity: 0.4;
  }

  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 20px 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: linear-gradient(to bottom, rgba(10,10,15,0.95), transparent);
    backdrop-filter: blur(10px);
  }

  .nav-logo {
    font-family: var(--mono);
    font-size: 14px;
    color: var(--accent);
    letter-spacing: 0.1em;
  }

  .nav-links {
    display: flex;
    gap: 36px;
    list-style: none;
  }

  .nav-links a {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    transition: color 0.2s;
    position: relative;
  }

  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--accent);
    transition: width 0.3s;
  }

  .nav-links a:hover { color: var(--accent); }
  .nav-links a:hover::after { width: 100%; }

  section {
    position: relative;
    z-index: 10;
    min-height: 100vh;
    padding: 120px 60px 80px;
    max-width: 1100px;
    margin: 0 auto;
  }

  #hero {
    display: flex;
    flex-direction: column;
    justify-content: center;
    min-height: 100vh;
    padding-top: 140px;
  }

  .hero-tag {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--accent);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.8s 0.2s ease both;
  }

  .hero-tag span {
    display: inline-block;
    width: 40px; height: 1px;
    background: var(--accent);
    vertical-align: middle;
    margin-right: 12px;
  }

  .hero-name {
    font-size: clamp(60px, 8vw, 110px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.03em;
    opacity: 0;
    animation: fadeUp 0.8s 0.4s ease both;
    position: relative;
  }

  .hero-name .first { color: var(--text); display: block; }
  .hero-name .last {
    color: transparent;
    -webkit-text-stroke: 2px var(--accent);
    display: block;
  }

  .hero-role {
    margin-top: 32px;
    font-family: var(--mono);
    font-size: 16px;
    color: var(--accent2);
    opacity: 0;
    animation: fadeUp 0.8s 0.6s ease both;
  }

  .hero-desc {
    margin-top: 20px;
    font-size: 18px;
    color: var(--muted);
    max-width: 520px;
    line-height: 1.6;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s ease both;
  }

  .hero-cta {
    margin-top: 48px;
    display: flex;
    gap: 20px;
    opacity: 0;
    animation: fadeUp 0.8s 1s ease both;
  }

  .btn-primary {
    padding: 14px 32px;
    background: var(--accent);
    color: #000;
    font-family: var(--mono);
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-decoration: none;
    border: none;
    cursor: none;
    transition: transform 0.2s, box-shadow 0.2s;
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
    display: inline-block;
  }

  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 30px rgba(240,192,64,0.4);
  }

  .btn-outline {
    padding: 14px 32px;
    background: transparent;
    color: var(--text);
    font-family: var(--mono);
    font-size: 13px;
    letter-spacing: 0.08em;
    text-decoration: none;
    border: 1px solid var(--border);
    cursor: none;
    transition: border-color 0.2s, color 0.2s;
    display: inline-block;
  }

  .btn-outline:hover {
    border-color: var(--accent2);
    color: var(--accent2);
  }

  .hero-scroll {
    position: absolute;
    bottom: 40px;
    left: 60px;
    display: flex;
    align-items: center;
    gap: 12px;
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
    opacity: 0;
    animation: fadeUp 0.8s 1.4s ease both;
  }

  .scroll-line {
    width: 40px; height: 1px;
    background: var(--muted);
    animation: scrollPulse 2s infinite;
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 60px;
  }

  .section-num {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--accent);
    letter-spacing: 0.1em;
  }

  .section-title {
    font-size: clamp(36px, 4vw, 52px);
    font-weight: 800;
    letter-spacing: -0.02em;
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .stack-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }

  .stack-card {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 28px 32px;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s;
  }

  .stack-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: var(--accent);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }

  .stack-card:hover { transform: translateY(-4px); border-color: rgba(240,192,64,0.2); }
  .stack-card:hover::before { transform: scaleX(1); }

  .stack-label {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  .stack-value {
    font-size: 20px;
    font-weight: 600;
    color: var(--text);
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
  }

  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 36px;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s;
    cursor: none;
  }

  .project-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(240,192,64,0.04), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .project-card:hover { transform: translateY(-6px); border-color: rgba(240,192,64,0.3); }
  .project-card:hover::after { opacity: 1; }

  .project-num {
    font-family: var(--mono);
    font-size: 48px;
    font-weight: 700;
    color: rgba(240,192,64,0.08);
    line-height: 1;
    margin-bottom: 20px;
  }

  .project-title {
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 16px;
    color: var(--text);
  }

  .project-desc {
    font-size: 14px;
    color: var(--muted);
    line-height: 1.7;
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 24px;
  }

  .tag {
    font-family: var(--mono);
    font-size: 10px;
    padding: 5px 10px;
    border: 1px solid var(--border);
    color: var(--muted);
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .edu-list {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .edu-item {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 32px 40px;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 20px;
    align-items: center;
    transition: border-color 0.3s, transform 0.3s;
    position: relative;
    overflow: hidden;
  }

  .edu-item::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 3px;
    background: var(--accent2);
    transform: scaleY(0);
    transform-origin: bottom;
    transition: transform 0.4s;
  }

  .edu-item:hover { border-color: rgba(64,224,255,0.2); transform: translateX(4px); }
  .edu-item:hover::before { transform: scaleY(1); }

  .edu-degree {
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 6px;
  }

  .edu-uni {
    font-family: var(--mono);
    font-size: 13px;
    color: var(--muted);
  }

  .edu-year {
    font-family: var(--mono);
    font-size: 13px;
    color: var(--accent2);
    text-align: right;
    white-space: nowrap;
  }

  .strengths-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
  }

  .strength-pill {
    padding: 14px 28px;
    border: 1px solid var(--border);
    font-size: 15px;
    font-weight: 600;
    color: var(--text);
    position: relative;
    overflow: hidden;
    transition: color 0.3s, border-color 0.3s;
    cursor: none;
  }

  .strength-pill::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--accent);
    transform: translateX(-105%);
    transition: transform 0.35s ease;
    z-index: -1;
  }

  .strength-pill:hover { color: #000; border-color: var(--accent); }
  .strength-pill:hover::before { transform: translateX(0); }

  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
  }

  .contact-item {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 28px 32px;
    text-decoration: none;
    transition: border-color 0.3s, transform 0.3s;
    display: block;
    cursor: none;
  }

  .contact-item:hover { border-color: rgba(255,95,126,0.4); transform: translateY(-3px); }

  .contact-label {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--accent3);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .contact-value {
    font-size: 16px;
    color: var(--text);
    word-break: break-all;
  }

  .cert-badge {
    display: inline-flex;
    align-items: center;
    gap: 14px;
    background: var(--card);
    border: 1px solid rgba(240,192,64,0.3);
    padding: 20px 28px;
    margin-top: 20px;
  }

  .cert-icon { font-size: 28px; }
  .cert-name { font-size: 16px; font-weight: 600; }
  .cert-source { font-family: var(--mono); font-size: 11px; color: var(--muted); margin-top: 3px; }

  footer {
    position: relative;
    z-index: 10;
    text-align: center;
    padding: 40px;
    border-top: 1px solid var(--border);
    font-family: var(--mono);
    font-size: 12px;
    color: var(--muted);
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes scrollPulse {
    0%, 100% { width: 40px; opacity: 0.5; }
    50% { width: 60px; opacity: 1; }
  }

  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }

  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }
  .reveal-delay-5 { transition-delay: 0.5s; }

  .glitch { position: relative; }

  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    font-size: inherit;
    font-weight: inherit;
    letter-spacing: inherit;
    line-height: inherit;
  }

  .glitch::before {
    color: var(--accent2);
    animation: glitch1 4s infinite;
    clip-path: polygon(0 30%, 100% 30%, 100% 50%, 0 50%);
  }

  .glitch::after {
    color: var(--accent3);
    animation: glitch2 4s infinite;
    clip-path: polygon(0 65%, 100% 65%, 100% 80%, 0 80%);
  }

  @keyframes glitch1 {
    0%, 88%, 100% { transform: translate(0); opacity: 0; }
    90% { transform: translate(-3px, 1px); opacity: 1; }
    92% { transform: translate(3px, -1px); opacity: 1; }
    94% { transform: translate(0); opacity: 0; }
  }

  @keyframes glitch2 {
    0%, 88%, 100% { transform: translate(0); opacity: 0; }
    91% { transform: translate(3px, 1px); opacity: 1; }
    93% { transform: translate(-3px, -1px); opacity: 1; }
    95% { transform: translate(0); opacity: 0; }
  }
</style>
</head>
<body>

<canvas id="bg-canvas"></canvas>
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<nav>
  <div class="nav-logo">JM<span style="color:var(--muted);">_dev</span></div>
  <ul class="nav-links">
    <li><a href="#about">Stack</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<section id="hero">
  <div class="hero-tag"><span></span>Available for opportunities</div>
  <h1 class="hero-name glitch" data-text="MUNJET">
    <span class="first">JOSHUA</span>
    <span class="last">MUNJET</span>
  </h1>
  <div class="hero-role">&gt; <span id="typewriter"></span><span style="color:var(--accent);animation:blink 0.8s step-end infinite;display:inline-block;" id="tw-cursor">|</span></div>
  <p class="hero-desc">Entry-level developer skilled in Java, Python and machine learning. Passionate about building software systems and learning new technologies.</p>
  <div class="hero-cta">
    <a href="#projects" class="btn-primary">View Projects</a>
    <a href="#contact" class="btn-outline">Get In Touch</a>
  </div>
  <div class="hero-scroll">
    <div class="scroll-line"></div>
    SCROLL DOWN
  </div>
</section>

<section id="about" style="min-height:auto;">
  <div class="section-header reveal">
    <span class="section-num">01</span>
    <h2 class="section-title">Tech Stack</h2>
    <div class="section-line"></div>
  </div>
  <div class="stack-grid">
    <div class="stack-card reveal reveal-delay-1">
      <div class="stack-label">Languages</div>
      <div class="stack-value">Java &middot; Python &middot; C</div>
    </div>
    <div class="stack-card reveal reveal-delay-2">
      <div class="stack-label">Web</div>
      <div class="stack-value">HTML &middot; CSS</div>
    </div>
    <div class="stack-card reveal reveal-delay-3">
      <div class="stack-label">Database</div>
      <div class="stack-value">SQL</div>
    </div>
    <div class="stack-card reveal reveal-delay-4">
      <div class="stack-label">AI / ML</div>
      <div class="stack-value">Machine Learning</div>
    </div>
  </div>
</section>

<section id="projects">
  <div class="section-header reveal">
    <span class="section-num">02</span>
    <h2 class="section-title">Projects</h2>
    <div class="section-line"></div>
  </div>
  <div class="projects-grid">
    <div class="project-card reveal reveal-delay-1">
      <div class="project-num">01</div>
      <h3 class="project-title">Movie Recommendation App</h3>
      <p class="project-desc">Designed and implemented a movie recommendation application that enables users to discover films based on 50+ data points using ML algorithms.</p>
      <div class="project-tags">
        <span class="tag">Python</span>
        <span class="tag">ML</span>
        <span class="tag">Data</span>
      </div>
    </div>
    <div class="project-card reveal reveal-delay-2">
      <div class="project-num">02</div>
      <h3 class="project-title">Real Estate Price Predictor</h3>
      <p class="project-desc">Python-based mini-project that predicts house prices using a predictive model with area, bedrooms, and location as key parameters.</p>
      <div class="project-tags">
        <span class="tag">Python</span>
        <span class="tag">Regression</span>
        <span class="tag">ML</span>
      </div>
    </div>
  </div>
</section>

<section id="education" style="min-height:auto;">
  <div class="section-header reveal">
    <span class="section-num">03</span>
    <h2 class="section-title">Education</h2>
    <div class="section-line"></div>
  </div>
  <div class="edu-list">
    <div class="edu-item reveal reveal-delay-1">
      <div>
        <div class="edu-degree">Master of Computer Applications (MCA)</div>
        <div class="edu-uni">Biju Patnaik University of Technology</div>
      </div>
      <div class="edu-year">Pursuing<br>Exp. 2026</div>
    </div>
    <div class="edu-item reveal reveal-delay-2">
      <div>
        <div class="edu-degree">Bachelor of Computer Applications (BCA)</div>
        <div class="edu-uni">Utkal University</div>
      </div>
      <div class="edu-year">2024</div>
    </div>
  </div>

  <div style="margin-top:60px;">
    <div class="section-header reveal">
      <span class="section-num">04</span>
      <h2 class="section-title" style="font-size:clamp(28px,3vw,38px);">Certifications</h2>
      <div class="section-line"></div>
    </div>
    <div class="cert-badge reveal">
      <div class="cert-icon">&#127; </div>
      <div>
        <div class="cert-name">Artificial Intelligence &amp; Machine Learning</div>
        <div class="cert-source">Udemy</div>
      </div>
    </div>
  </div>
</section>

<section style="min-height:auto;">
  <div class="section-header reveal">
    <span class="section-num">05</span>
    <h2 class="section-title">Strengths</h2>
    <div class="section-line"></div>
  </div>
  <div class="strengths-grid">
    <div class="strength-pill reveal reveal-delay-1">Problem Solving</div>
    <div class="strength-pill reveal reveal-delay-2">Innovation</div>
    <div class="strength-pill reveal reveal-delay-3">Analytical Thinking</div>
    <div class="strength-pill reveal reveal-delay-4">Team Collaboration</div>
    <div class="strength-pill reveal reveal-delay-5">Quick Learner</div>
    <div class="strength-pill reveal">Communication</div>
  </div>
</section>

<section id="contact" style="min-height:auto;">
  <div class="section-header reveal">
    <span class="section-num">06</span>
    <h2 class="section-title">Contact</h2>
    <div class="section-line"></div>
  </div>
  <div class="contact-grid">
    <a href="mailto:munjetjoshua@gmail.com" class="contact-item reveal reveal-delay-1">
      <div class="contact-label">Email</div>
      <div class="contact-value">munjetjoshua@gmail.com</div>
    </a>
    <a href="tel:+919777511751" class="contact-item reveal reveal-delay-2">
      <div class="contact-label">Phone</div>
      <div class="contact-value">+91-9777511751</div>
    </a>
    <a href="https://linkedin.com/in/joshua-munjet-0853b333b" target="_blank" class="contact-item reveal reveal-delay-3" style="grid-column:span 2;">
      <div class="contact-label">LinkedIn</div>
      <div class="contact-value">linkedin.com/in/joshua-munjet-0853b333b</div>
    </a>
  </div>
</section>

<footer>
  <p>Joshua Munjet &mdash; Bhubaneswar, Odisha &mdash; 2026</p>
</footer>

<style>
@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
</style>

<script>
  // Cursor
  const cursor = document.getElementById('cursor');
  const cursorRing = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  (function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    cursorRing.style.left = rx + 'px';
    cursorRing.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  })();

  // Particle canvas
  const canvas = document.getElementById('bg-canvas');
  const ctx = canvas.getContext('2d');
  let W = canvas.width = window.innerWidth;
  let H = canvas.height = window.innerHeight;

  window.addEventListener('resize', () => {
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
  });

  const particles = Array.from({length: 70}, () => ({
    x: Math.random() * W, y: Math.random() * H,
    vx: (Math.random() - 0.5) * 0.3,
    vy: (Math.random() - 0.5) * 0.3,
    size: Math.random() * 1.5 + 0.5,
    alpha: Math.random() * 0.5 + 0.1
  }));

  (function drawParticles() {
    ctx.clearRect(0, 0, W, H);
    particles.forEach((p, i) => {
      p.x = (p.x + p.vx + W) % W;
      p.y = (p.y + p.vy + H) % H;
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(240,192,64,${p.alpha})`;
      ctx.fill();
      for (let j = i + 1; j < particles.length; j++) {
        const q = particles[j];
        const dx = p.x - q.x, dy = p.y - q.y;
        const d = Math.sqrt(dx * dx + dy * dy);
        if (d < 120) {
          ctx.beginPath();
          ctx.moveTo(p.x, p.y);
          ctx.lineTo(q.x, q.y);
          ctx.strokeStyle = `rgba(240,192,64,${0.05 * (1 - d / 120)})`;
          ctx.lineWidth = 0.5;
          ctx.stroke();
        }
      }
    });
    requestAnimationFrame(drawParticles);
  })();

  // Typewriter
  const roles = ['Entry-Level Developer', 'Java & Python Engineer', 'ML Enthusiast', 'Problem Solver'];
  let ri = 0, ci = 0, deleting = false;
  const tw = document.getElementById('typewriter');

  function type() {
    const word = roles[ri];
    if (!deleting) {
      tw.textContent = word.slice(0, ++ci);
      if (ci >= word.length) { deleting = true; setTimeout(type, 1800); return; }
    } else {
      tw.textContent = word.slice(0, --ci);
      if (ci <= 0) { deleting = false; ri = (ri + 1) % roles.length; }
    }
    setTimeout(type, deleting ? 50 : 90);
  }
  setTimeout(type, 1200);

  // Scroll reveal
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(r => observer.observe(r));
</script>
</body>
</html>
