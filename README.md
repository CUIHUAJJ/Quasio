<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Quasio 跨平台开发实验室</title>
  <!-- 字体 & 代码高亮 -->
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <link href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-tomorrow.min.css" rel="stylesheet" />

  <style>
    /* ========= RESET ========= */
    *, *::before, *::after { margin:0; padding:0; box-sizing:border-box }
    html { font-size:16px; scroll-behavior:smooth }
    body { font-family:'Inter',sans-serif; background:var(--bg); color:var(--text); line-height:1.6 }
    img, svg { display:block; max-width:100% }
    a { color:inherit; text-decoration:none }
    ul { list-style:none }

    /* ====== VARIABLES ====== */
    :root {
      --primary: #5568f1;
      --primary-light: #e4e8ff;
      --secondary: #6e728e;
      --bg: #f7f9fc;
      --surface: #ffffff;
      --text: #333333;
      --radius: 8px;
      --shadow: rgba(0,0,0,0.1);
      --transition: .3s ease;
    }
    [data-theme="dark"] {
      --primary: #839ffe;
      --primary-light: #2c2d34;
      --secondary: #a0a3b5;
      --bg: #1e1f24;
      --surface: #2c2d34;
      --text: #e4e6eb;
    }

    /* ===== GLOBAL ===== */
    .container { width:100%; max-width:1024px; margin:0 auto; padding:0 1rem }
    .btn { 
      display:inline-block; font-weight:600; border-radius:var(--radius);
      cursor:pointer; transition:background var(--transition), transform var(--transition);
      user-select:none; text-align:center; padding:.6rem 1.2rem;
    }
    .btn:active { transform:scale(.98) }
    .btn--primary { background:var(--primary); color:#fff }
    .btn--primary:hover { background:#3b4fd4 }

    /* ===== HEADER ===== */
    .header {
      position:sticky; top:0; background:var(--surface);
      box-shadow:0 2px 6px var(--shadow); z-index:100;
    }
    .header__inner {
      display:flex; align-items:center; justify-content:space-between;
      padding:1rem 0;
    }
    .header__logo { font-size:1.5rem; font-weight:700; color:var(--primary) }
    .header__nav { display:flex; gap:1.5rem; font-size:.95rem }
    .header__nav a:hover { color:var(--primary) }
    .header__theme {
      background:none; border:none; font-size:1.2rem; cursor:pointer;
    }

    /* ===== HERO ===== */
    .hero {
      background:var(--primary-light); border-radius:var(--radius);
      text-align:center; padding:3rem 1rem; margin:2rem 0;
    }
    .hero__title { font-size:2.25rem; font-weight:700; color:var(--primary); margin-bottom:.5rem }
    .hero__desc { font-size:1rem; color:var(--secondary); margin-bottom:1.5rem; max-width:600px; margin-inline:auto }
    .hero__badges { margin-bottom:1.5rem }
    .hero__badges img { margin:0 .3rem; vertical-align:middle; }
    .hero__cta { display:inline-block }

    /* ===== FEATURES ===== */
    .features {
      display:grid; grid-template-columns:repeat(auto-fit,minmax(240px,1fr));
      gap:1.5rem; margin-bottom:2rem;
    }
    .feature {
      background:var(--surface); border-radius:var(--radius);
      padding:1.5rem; box-shadow:0 2px 6px var(--shadow);
      text-align:center; transition:transform var(--transition);
    }
    .feature:hover { transform:translateY(-5px) }
    .feature__icon { font-size:2rem; color:var(--primary); margin-bottom:.75rem }
    .feature__title { font-size:1.1rem; font-weight:600; margin-bottom:.5rem }
    .feature__desc { font-size:.95rem; color:var(--secondary) }

    /* ===== GALLERY ===== */
    .gallery {
      display:grid; grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
      gap:1rem; margin-bottom:2rem;
    }
    .gallery__item {
      overflow:hidden; border-radius:var(--radius);
      box-shadow:0 2px 6px var(--shadow);
    }
    .gallery__item img {
      display:block; width:100%; height:auto; transition:transform var(--transition);
    }
    .gallery__item:hover img { transform:scale(1.05) }

    /* ===== QUICKSTART ===== */
    .quickstart {
      background:var(--surface); border-radius:var(--radius);
      padding:1.5rem; box-shadow:0 2px 6px var(--shadow);
      margin-bottom:3rem;
    }
    .quickstart__title { font-size:1.2rem; font-weight:600; color:var(--primary); margin-bottom:.75rem }
    .quickstart pre {
      background:var(--bg); padding:1rem; border-radius:var(--radius);
      overflow-x:auto; font-size:.9rem; box-shadow:0 1px 3px var(--shadow);
    }

    /* ===== FOOTER ===== */
    .footer {
      text-align:center; font-size:.9rem; color:var(--secondary);
      padding:2rem 0 1rem;
    }
    .footer a:hover { text-decoration:underline }
  </style>
</head>
<body data-theme="light">

  <!-- HEADER -->
  <header class="header">
    <div class="container header__inner">
      <div class="header__logo">Quasio Lab</div>
      <nav class="header__nav">
        <a href="#features">核心特性</a>
        <a href="#gallery">UI 预览</a>
        <a href="#quickstart">快速开始</a>
        <a href="https://github.com/yourname/quasio-lab" target="_blank" rel="noopener">GitHub</a>
      </nav>
      <button class="header__theme" aria-label="切换主题">🌙</button>
    </div>
  </header>

  <!-- HERO -->
  <section class="container hero">
    <h1 class="hero__title">Quasio · 跨平台开发实验室</h1>
    <p class="hero__desc">
      一站式打包分发：Android/Cordova、Windows/Electron、Web 静态 Bundle，CI/CD 零配置，离线一键打包。
    </p>
    <div class="hero__badges">
      <img src="https://img.shields.io/github/v/release/yourname/quasio-lab?color=5568f1" alt="Release">
      <img src="https://img.shields.io/github/license/yourname/quasio-lab" alt="License">
      <img src="https://img.shields.io/github/stars/yourname/quasio-lab?style=social" alt="Stars">
      <img src="https://img.shields.io/badge/downloads-10K+-blue" alt="Downloads">
    </div>
    <a href="#quickstart" class="btn btn--primary hero__cta">立即上手</a>
  </section>

  <!-- FEATURES -->
  <section id="features" class="container features">
    <div class="feature">
      <div class="feature__icon">🛠️</div>
      <h3 class="feature__title">端到端自动化</h3>
      <p class="feature__desc">集成 Pake、HBuilder X、Cordova、Electron，CI/CD 零配置。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">📦</div>
      <h3 class="feature__title">离线一键打包</h3>
      <p class="feature__desc">瞬时生成 APK/EXE/HTML Bundle，网络断开下也可测试。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🔐</div>
      <h3 class="feature__title">安全签名管理</h3>
      <p class="feature__desc">可视化切换多环境签名与证书，自动化流水线内嵌。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">📊</div>
      <h3 class="feature__title">实时监控</h3>
      <p class="feature__desc">日志、状态、报表一览无余，支持 Web Dashboard。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🌐</div>
      <h3 class="feature__title">多平台覆盖</h3>
      <p class="feature__desc">Android、Web、Windows、macOS、Linux 全平台支持。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🤝</div>
      <h3 class="feature__title">开源 & 社区共建</h3>
      <p class="feature__desc">完整源码、自由扩展，社区插件生态持续增长。</p>
    </div>
  </section>

  <!-- GALLERY -->
  <section id="gallery" class="container gallery">
    <div class="gallery__item"><img src="ui-preview-1.png" alt="UI 预览 1"></div>
    <div class="gallery__item"><img src="ui-preview-2.png" alt="UI 预览 2"></div>
  </section>

  <!-- QUICKSTART -->
  <section id="quickstart" class="container quickstart">
    <h2 class="quickstart__title">快速开始</h2>
    <pre><code class="language-bash">
git clone https://github.com/yourname/quasio-lab.git
cd quasio-lab
npm install -g pake-cli
pake build:web      # Web 静态 Bundle
pake build:android  # Cordova Android APK
pake build:desktop  # Electron Windows/macOS
    </code></pre>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    © 2025 Quasio Lab • <a href="https://github.com/yourname/quasio-lab" target="_blank">GitHub 项目</a> • MIT License
  </footer>

  <!-- Prism.js & 主题切换 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js"></script>
  <script>
    // 主题切换
    const btnTheme = document.querySelector('.header__theme');
    const root = document.documentElement;
    btnTheme.onclick = () => {
      const next = root.getAttribute('data-theme')==='light'?'dark':'light';
      root.setAttribute('data-theme', next);
      btnTheme.textContent = next==='light'?'🌙':'☀️';
      localStorage.setItem('theme', next);
    };
    // 加载上次主题
    const saved = localStorage.getItem('theme');
    if(saved) {
      root.setAttribute('data-theme', saved);
      document.querySelector('.header__theme').textContent = saved==='light'?'🌙':'☀️';
    }
  </script>
</body>
</html>
