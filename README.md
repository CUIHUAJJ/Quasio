<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <title>Pake · 轻量级网页转桌面应用</title>
  <!-- Google Font & Prism.js 样式 -->
  <link rel="preconnect" href="https://fonts.gstatic.com"/>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet"/>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-tomorrow.min.css" rel="stylesheet"/>

  <style>
    /* —— RESET —— */
    *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }
    html { font-size:16px; scroll-behavior:smooth; }
    body { font-family:'Inter',sans-serif; background:var(--bg); color:var(--text); line-height:1.6; }
    img, svg { display:block; max-width:100%; }
    a { color:inherit; text-decoration:none; }
    ul { list-style:none; }

    /* —— 变量 —— */
    :root {
      --primary: #5568f1;
      --primary-light: #e4e8ff;
      --secondary: #6e728e;
      --bg: #f7f9fc;
      --surface: #ffffff;
      --text: #333333;
      --radius: 8px;
      --transition: .3s ease;
    }
    [data-theme="dark"] {
      --primary: #839ffe;
      --primary-light: #2c2d34;
      --secondary: #a0a3b5;
      --bg: #1f2025;
      --surface: #2c2d34;
      --text: #e4e6eb;
    }

    /* —— 全局组件 —— */
    .container { width:100%; max-width:1024px; margin:0 auto; padding:0 1rem; }
    .btn {
      display:inline-block; font-weight:600; border-radius:var(--radius);
      transition: background var(--transition), transform var(--transition);
      cursor:pointer; text-align:center; user-select:none;
    }
    .btn:active { transform:scale(.98); }
    .btn--primary {
      padding:.6rem 1.2rem; background:var(--primary); color:#fff;
    }
    .btn--primary:hover { background:#3b4fd4; }

    /* —— HEADER —— */
    .header {
      position:sticky; top:0; z-index:100;
      background:var(--surface); box-shadow:0 2px 6px rgba(0,0,0,0.05);
    }
    .header__inner {
      display:flex; align-items:center; justify-content:space-between;
      padding:1rem 0;
    }
    .header__logo { font-size:1.5rem; font-weight:700; color:var(--primary); }
    .header__nav {
      display:flex; gap:1.5rem; font-size:.95rem;
    }
    .header__nav a:hover { color:var(--primary); }
    .header__toggle, .header__theme {
      background:none; border:none; font-size:1.25rem; cursor:pointer;
    }
    /* mobile */
    @media (max-width:768px) {
      .header__toggle { display:block; }
      .header__nav {
        position:fixed; top:0; left:-100%; height:100vh; width:70%;
        flex-direction:column; padding:4rem 1rem; background:var(--surface);
        gap:1.25rem; transition:left var(--transition);
      }
      .header__nav.active { left:0; }
    }
    @media (min-width:769px) {
      .header__toggle { display:none; }
    }

    /* —— HERO —— */
    .hero {
      background:var(--primary-light); border-radius:var(--radius);
      padding:3rem 1rem; text-align:center; margin:2rem 0;
      animation:fadeInUp .8s ease both;
    }
    .hero__title {
      font-size:2.25rem; font-weight:700; color:var(--primary);
      margin-bottom:.5rem;
    }
    .hero__desc {
      font-size:1rem; color:var(--secondary); margin-bottom:1.5rem; max-width:600px;
    }
    .hero__cta { animation:fadeInUp 1.2s ease both; }

    /* fadeInUp */
    @keyframes fadeInUp {
      from { opacity:0; transform:translateY(20px); }
      to   { opacity:1; transform:none; }
    }

    /* —— FEATURES —— */
    .features {
      display:grid; grid-template-columns:repeat(auto-fit,minmax(240px,1fr));
      gap:1.5rem; margin-bottom:2rem;
    }
    .feature {
      background:var(--surface); border-radius:var(--radius);
      padding:1.5rem; box-shadow:0 2px 6px rgba(0,0,0,0.03);
      text-align:center; transition:transform var(--transition);
    }
    .feature:hover { transform:translateY(-5px); }
    .feature__icon { font-size:2rem; color:var(--primary); margin-bottom:.75rem; }
    .feature__title { font-size:1.1rem; font-weight:600; margin-bottom:.5rem; }
    .feature__desc { font-size:.95rem; color:var(--secondary); }

    /* —— QUICKSTART —— */
    .quickstart {
      background:var(--surface); border-radius:var(--radius);
      padding:1.5rem; box-shadow:0 2px 6px rgba(0,0,0,0.03);
      margin-bottom:2rem; animation:fadeInUp 1s ease both;
    }
    .quickstart__title { font-size:1.2rem; font-weight:600; color:var(--primary); margin-bottom:.75rem; }
    pre[class*="language-"] {
      background:var(--bg); padding:1rem; border-radius:var(--radius);
      overflow-x:auto; font-size:.9rem; box-shadow:0 1px 3px rgba(0,0,0,0.1);
    }

    /* —— FOOTER —— */
    .footer {
      text-align:center; font-size:.9rem; color:var(--secondary);
      padding:2rem 0 1rem;
    }
    .footer a:hover { text-decoration:underline; }
  </style>
</head>
<body data-theme="light">

  <!-- HEADER -->
  <header class="header">
    <div class="container header__inner">
      <div class="header__logo">Pake</div>
      <button class="header__toggle" aria-label="打开菜单">☰</button>
      <nav class="header__nav">
        <a href="#features">特性</a>
        <a href="#quickstart">快速开始</a>
        <a href="https://github.com/yourname/pake" target="_blank" rel="noopener">GitHub</a>
      </nav>
      <button class="header__theme" aria-label="切换主题">🌙</button>
    </div>
  </header>

  <!-- HERO -->
  <section class="container hero">
    <h1 class="hero__title">Pake · Rust 驱动的网页转桌面</h1>
    <p class="hero__desc">
      一条命令，把任意网页打包成 Windows、macOS、Linux 应用，体积小、启动快、安全稳定。
    </p>
    <a href="#quickstart" class="btn btn--primary hero__cta">立即上手</a>
  </section>

  <!-- FEATURES -->
  <section id="features" class="container features">
    <div class="feature">
      <div class="feature__icon">⚡️</div>
      <h3 class="feature__title">极速启动</h3>
      <p class="feature__desc">秒级冷启动，基于 Tauri 内核，体验丝滑。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🧰</div>
      <h3 class="feature__title">跨平台</h3>
      <p class="feature__desc">原生支持 macOS、Windows、Linux，多端一致。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">💾</div>
      <h3 class="feature__title">超小体积</h3>
      <p class="feature__desc">二进制 ~5MB，比 Electron 小 95%。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🔧</div>
      <h3 class="feature__title">易于上手</h3>
      <p class="feature__desc">一行命令打包，告别繁琐配置。</p>
    </div>
  </section>

  <!-- QUICKSTART -->
  <section id="quickstart" class="container quickstart">
    <h2 class="quickstart__title">快速开始</h2>
    <pre><code class="language-bash">
git clone https://github.com/yourname/pake.git
cd pake
cargo install --path .
pake init https://example.com
pake build
    </code></pre>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    © 2025 Pake • <a href="https://github.com/yourname/pake" target="_blank" rel="noopener">GitHub 项目</a> • MIT License
  </footer>

  <!-- Prism.js & 交互脚本 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js"></script>
  <script>
    // 主题切换
    const btnTheme = document.querySelector('.header__theme');
    const root = document.documentElement;
    btnTheme.onclick = () => {
      const next = root.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
      root.setAttribute('data-theme', next);
      btnTheme.textContent = next === 'light' ? '🌙' : '☀️';
      localStorage.setItem('theme', next);
    };
    // 载入本地主题
    const saved = localStorage.getItem('theme');
    if (saved) {
      root.setAttribute('data-theme', saved);
      btnTheme.textContent = saved === 'light' ? '🌙' : '☀️';
    }
    // 移动端导航
    const btnToggle = document.querySelector('.header__toggle');
    const nav = document.querySelector('.header__nav');
    btnToggle.onclick = () => nav.classList.toggle('active');
  </script>
</body>
</html>
