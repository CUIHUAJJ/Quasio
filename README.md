<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Pake · 轻量级网页转桌面应用</title>
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    /* ========== CSS RESET ========== */
    *,
    *::before,
    *::after {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    html {
      font-size: 16px;
      -webkit-text-size-adjust: 100%;
    }
    body {
      font-family: 'Inter', sans-serif;
      line-height: 1.6;
      color: #333;
      background-color: #f7f9fc;
    }
    img {
      max-width: 100%;
      display: block;
    }
    a {
      color: inherit;
      text-decoration: none;
    }
    ul {
      list-style: none;
    }

    /* ========== VARIABLES & BASE ========== */
    :root {
      --color-primary: #5568f1;
      --color-primary-light: #e4e8ff;
      --color-secondary: #6e728e;
      --color-bg: #fff;
      --radius: 8px;
    }
    .container {
      max-width: 1024px;
      padding: 0 1rem;
      margin: 0 auto;
    }
    .btn {
      display: inline-block;
      font-weight: 600;
      text-align: center;
      cursor: pointer;
      border-radius: var(--radius);
      transition: background 0.2s, transform 0.2s;
    }
    .btn:active { transform: scale(.98); }
    .btn-primary {
      padding: .6em 1.2em;
      background-color: var(--color-primary);
      color: #fff;
    }
    .btn-primary:hover {
      background-color: #3b4fd4;
    }

    /* ========== HEADER ========== */
    .header {
      background-color: var(--color-bg);
      box-shadow: 0 2px 6px rgba(0,0,0,0.05);
    }
    .header__inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1rem 0;
    }
    .header__logo {
      font-size: 1.5rem;
      font-weight: 700;
      color: var(--color-primary);
    }
    .header__nav a {
      margin-left: 1.5rem;
      font-size: 0.95rem;
      color: var(--color-secondary);
    }
    .header__nav a:hover {
      color: var(--color-primary);
    }

    /* ========== HERO ========== */
    .hero {
      background: var(--color-primary-light);
      border-radius: var(--radius);
      margin: 2rem 0;
      padding: 2rem 1rem;
      text-align: center;
    }
    .hero__title {
      font-size: 2rem;
      font-weight: 700;
      color: var(--color-primary);
      margin-bottom: .5rem;
    }
    .hero__desc {
      font-size: 1rem;
      color: var(--color-secondary);
      margin-bottom: 1rem;
      max-width: 600px;
      margin-inline: auto;
    }
    .hero__badges img {
      margin: 0 .3rem;
      vertical-align: middle;
    }

    /* ========== FEATURES ========== */
    .features {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(240px,1fr));
      gap: 1.5rem;
      margin-bottom: 2rem;
    }
    .feature {
      background: var(--color-bg);
      border-radius: var(--radius);
      padding: 1.5rem;
      box-shadow: 0 2px 6px rgba(0,0,0,0.03);
      text-align: center;
    }
    .feature__icon {
      font-size: 2rem;
      color: var(--color-primary);
      margin-bottom: .75rem;
    }
    .feature__title {
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: .5rem;
    }
    .feature__desc {
      font-size: .95rem;
      color: var(--color-secondary);
      line-height: 1.4;
    }

    /* ========== QUICK START ========== */
    .quickstart {
      background: var(--color-bg);
      border-radius: var(--radius);
      padding: 1.5rem;
      box-shadow: 0 2px 6px rgba(0,0,0,0.03);
      margin-bottom: 2rem;
    }
    .quickstart__title {
      font-size: 1.2rem;
      font-weight: 600;
      margin-bottom: .75rem;
      color: var(--color-primary);
    }
    .quickstart__commands {
      background: #f1f3f7;
      padding: 1rem;
      border-radius: var(--radius);
      font-family: Consolas, Menlo, monospace;
      font-size: .9rem;
      overflow-x: auto;
    }

    /* ========== FOOTER ========== */
    .footer {
      text-align: center;
      padding: 2rem 0 1rem;
      font-size: .9rem;
      color: var(--color-secondary);
    }
    .footer a {
      color: var(--color-primary);
    }
  </style>
</head>
<body>

  <!-- HEADER -->
  <header class="header">
    <div class="container header__inner">
      <div class="header__logo">Pake</div>
      <nav class="header__nav">
        <a href="#features">特性</a>
        <a href="#quickstart">快速开始</a>
        <a href="https://github.com/yourname/pake" target="_blank">GitHub</a>
      </nav>
    </div>
  </header>

  <!-- HERO -->
  <section class="container hero">
    <h1 class="hero__title">Pake · Rust 驱动的网页转桌面</h1>
    <p class="hero__desc">
      Pake 一键将任何网页打包成 Mac、Windows、Linux 桌面应用，二进制体积小、启动迅速、安全稳定。
    </p>
    <div class="hero__badges">
      <img src="https://img.shields.io/github/v/release/yourname/pake?color=5568f1" alt="Release">
      <img src="https://img.shields.io/github/license/yourname/pake" alt="License">
      <img src="https://img.shields.io/github/stars/yourname/pake?style=social" alt="Stars">
      <img src="https://img.shields.io/dub/l/daily?color=ef5350&style=flat-square" alt="Downloads">
    </div>
    <p class="hero__desc" style="margin-top:1rem;">
      比 Electron 体积小 20 倍；基于 Rust Tauri，性能更快更轻量；简单命令行，降低学习成本。
    </p>
    <a href="#quickstart" class="btn btn-primary">立即上手</a>
  </section>

  <!-- FEATURES -->
  <section class="container" id="features">
    <div class="features">
      <div class="feature">
        <div class="feature__icon">⚡️</div>
        <div class="feature__title">极速启动</div>
        <div class="feature__desc">基于 Tauri 内核，秒级冷启动，体验丝滑。</div>
      </div>
      <div class="feature">
        <div class="feature__icon">🧰</div>
        <div class="feature__title">跨平台</div>
        <div class="feature__desc">原生支持 macOS、Windows、Linux，多端统一体验。</div>
      </div>
      <div class="feature">
        <div class="feature__icon">💾</div>
        <div class="feature__title">小体积</div>
        <div class="feature__desc">最终包体积约 5MB 左右，比 Electron 小 95%。</div>
      </div>
      <div class="feature">
        <div class="feature__icon">🔧</div>
        <div class="feature__title">简单易用</div>
        <div class="feature__desc">一条命令打包现成应用，告别繁琐配置。</div>
      </div>
    </div>
  </section>

  <!-- QUICK START -->
  <section class="container quickstart" id="quickstart">
    <h2 class="quickstart__title">快速开始</h2>
    <pre class="quickstart__commands">
git clone https://github.com/yourname/pake.git
cd pake
cargo install --path .
pake init https://example.com
pake build
    </pre>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    © 2025 Pake • <a href="https://github.com/yourname/pake" target="_blank">GitHub 项目</a> • MIT License
  </footer>

</body>
</html>
