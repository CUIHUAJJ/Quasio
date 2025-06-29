<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <title>Quasio · 跨平台开发实验室</title>

  <!-- Google Font & Prism.js Theme -->
  <link rel="preconnect" href="https://fonts.gstatic.com"/>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet"/>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-tomorrow.min.css" rel="stylesheet"/>

  <style>
    /* —— reset & variables —— */
    *,*::before,*::after{margin:0;padding:0;box-sizing:border-box;}
    html{font-size:16px;scroll-behavior:smooth;}
    body{font-family:'Inter',sans-serif;background:var(--bg);color:var(--text);line-height:1.6;}
    img,svg{max-width:100%;display:block;}
    a{text-decoration:none;color:inherit;}
    ul{list-style:none;}
    :root{
      --primary: #5568f1;
      --primary-light: #e4e8ff;
      --secondary: #6e728e;
      --accent: #f67e7e;
      --bg: #f7f9fc;
      --surface: #fff;
      --text: #333;
      --radius: 8px;
      --shadow: rgba(0,0,0,0.1);
      --transition: .3s ease;
    }
    [data-theme="dark"]{
      --primary: #839ffe; --primary-light: #2c2d34;
      --secondary: #a0a3b5; --bg: #1f2025;
      --surface: #2c2d34; --text: #e4e6eb;
    }

    /* —— utilities —— */
    .container{max-width:1024px;margin:0 auto;padding:0 1rem;}
    .btn{display:inline-block;padding:.6rem 1.4rem;font-weight:600;border-radius:var(--radius);
         transition:background var(--transition),transform var(--transition);cursor:pointer;}
    .btn:active{transform:scale(.97);}
    .btn--primary{background:var(--primary);color:#fff;}
    .btn--primary:hover{background:#3b4fd4;}
    .btn--outline{background:transparent;border:2px solid var(--primary);color:var(--primary);}
    .btn--outline:hover{background:var(--primary);color:#fff;}

    h2,h3{color:var(--primary);}
    /* —— Header —— */
    .header{position:sticky;top:0;z-index:100;background:var(--surface);box-shadow:0 2px 6px var(--shadow);}
    .header__inner{display:flex;align-items:center;justify-content:space-between;padding:1rem 0;}
    .header__logo{font-size:1.5rem;font-weight:700;color:var(--primary);}
    .header__nav{display:flex;gap:1.5rem;font-size:.95rem;}
    .header__nav a:hover{color:var(--primary);}
    .header__toggle,
    .header__theme{display:none;background:none;border:none;font-size:1.3rem;cursor:pointer;}
    @media(max-width:768px){
      .header__toggle{display:block;}
      .header__nav{
        position:fixed;top:0;left:-100%;height:100vh;width:70%;
        flex-direction:column;padding:4rem 1rem;background:var(--surface);
        gap:1.2rem;transition:left var(--transition);
      }
      .header__nav.active{left:0;}
      .header__theme{display:block;}
    }

    /* —— Hero —— */
    .hero{position:relative;overflow:hidden;margin:2rem 0;
      background:linear-gradient(135deg,var(--primary),var(--primary-light));border-radius:var(--radius);
      padding:4rem 1rem;text-align:center;color:#fff;}
    .hero::after{content:"";position:absolute;top:0;left:0;width:100%;height:100%;
      background:url('data:image/svg+xml;utf8,\
        <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">\
          <defs><pattern id="p" width="40" height="40" patternUnits="userSpaceOnUse">\
            <circle cx="2" cy="2" r="2" fill="rgba(255,255,255,0.15)"/></pattern></defs>\
          <rect width="100%" height="100%" fill="url(%23p)"/></svg>')
      center/cover no-repeat;pointer-events:none;mix-blend-mode:overlay;}
    .hero__title{font-size:2.5rem;font-weight:700;margin-bottom:.5rem;}
    .hero__desc{font-size:1.1rem;max-width:640px;margin:0 auto 1.5rem;color:rgba(255,255,255,0.9);}
    .hero__actions{display:flex;justify-content:center;gap:1rem;}
    .hero__actions .btn{font-size:1rem;}

    /* —— Features —— */
    .features{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:1.5rem;margin-bottom:2rem;}
    .feature{background:var(--surface);border-radius:var(--radius);padding:1.5rem;
      box-shadow:0 2px 6px var(--shadow);text-align:center;transition:transform var(--transition),box-shadow var(--transition);}
    .feature:hover{transform:translateY(-6px);box-shadow:0 8px 16px var(--shadow);}
    .feature__icon{font-size:2.2rem;margin-bottom:.75rem;color:var(--primary);}
    .feature__title{font-size:1.15rem;margin-bottom:.5rem;}
    .feature__desc{font-size:.95rem;color:var(--secondary);}

    /* —— Comparison —— */
    .comparison{overflow-x:auto;margin-bottom:2rem;}
    .comparison table{width:100%;border-collapse:separate;border-spacing:0 12px;}
    .comparison th{background:var(--primary);color:#fff;padding:.75rem;text-align:left;}
    .comparison td{background:var(--surface);padding:.75rem;color:var(--text);}
    .comparison th:first-child, .comparison td:first-child{border-radius:var(--radius) 0 0 var(--radius);}
    .comparison th:last-child, .comparison td:last-child{border-radius:0 var(--radius) var(--radius) 0;}

    /* —— Testimonials —— */
    .testimonials{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:1.5rem;margin-bottom:2rem;}
    .testimonial{background:var(--surface);border-radius:var(--radius);padding:1.5rem;
      box-shadow:0 2px 6px var(--shadow);transition:transform var(--transition);}
    .testimonial:hover{transform:translateY(-4px);}
    .testimonial__avatar{width:50px;height:50px;border-radius:50%;margin-bottom:.75rem;}
    .testimonial__name{font-weight:600;margin-bottom:.25rem;}
    .testimonial__role{font-size:.85rem;color:var(--secondary);margin-bottom:.75rem;}
    .testimonial__text{font-size:.9rem;color:var(--text);}

    /* —— Gallery —— */
    .gallery-section{margin-bottom:2rem;text-align:center;}
    .gallery-section h2{margin-bottom:1rem;}
    .gallery{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:1rem;}
    .gallery__item{overflow:hidden;border-radius:var(--radius);box-shadow:0 2px 6px var(--shadow);}
    .gallery__item img{width:100%;height:auto;transition:transform var(--transition);}
    .gallery__item:hover img{transform:scale(1.05);}

    /* —— Quickstart —— */
    .quickstart{background:var(--surface);border-radius:var(--radius);padding:1.5rem;
      box-shadow:0 2px 6px var(--shadow);margin-bottom:3rem;}
    .tabs{display:flex;gap:1rem;border-bottom:2px solid var(--shadow);margin-bottom:1rem;}
    .tab{padding:.5rem 1rem;cursor:pointer;color:var(--secondary);transition:color var(--transition);}
    .tab.active{color:var(--primary);border-bottom:3px solid var(--primary);}
    pre{background:var(--bg);padding:1rem;border-radius:var(--radius);overflow-x:auto;
      font-size:.9rem;box-shadow:0 1px 3px var(--shadow);}

    /* —— Footer —— */
    .footer{text-align:center;color:var(--secondary);font-size:.9rem;padding:2rem 0 1rem;}
    .footer a{margin:0 .5rem;color:var(--primary);transition:color var(--transition);}
    .footer a:hover{color:var(--accent);}
  </style>
</head>

<body data-theme="light">
  <!-- HEADER -->
  <header class="header">
    <div class="container header__inner">
      <div class="header__logo">Quasio Lab</div>
      <button class="header__toggle" aria-label="菜单">☰</button>
      <nav class="header__nav">
        <a href="#features">特性</a>
        <a href="#comparison">对比</a>
        <a href="#testimonials">评价</a>
        <a href="#gallery">预览</a>
        <a href="#quickstart">快速开始</a>
        <a href="https://github.com/yourname/quasio-lab" target="_blank">GitHub</a>
      </nav>
      <button class="header__theme" aria-label="切换主题">🌙</button>
    </div>
  </header>

  <!-- HERO -->
  <section class="hero">
    <div class="container">
      <h1 class="hero__title">Quasio · 跨平台开发实验室</h1>
      <p class="hero__desc">
        一站式端到端自动化打包：Android/Cordova、Windows/Electron、Web 静态 Bundle，CI/CD 零配置，离线一键完成。
      </p>
      <div class="hero__actions">
        <a href="#quickstart" class="btn btn--primary">立即上手</a>
        <a href="#features" class="btn btn--outline">查看文档</a>
      </div>
    </div>
  </section>

  <!-- FEATURES -->
  <section id="features" class="container features">
    <div class="feature">
      <div class="feature__icon">⚡</div>
      <h3 class="feature__title">极速启动</h3>
      <p class="feature__desc">基于 Tauri 内核，秒级冷启动，体验丝滑顺畅。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">📦</div>
      <h3 class="feature__title">超小体积</h3>
      <p class="feature__desc">二进制 ~5MB，远小于 Electron 的几十倍。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🔒</div>
      <h3 class="feature__title">安全签名</h3>
      <p class="feature__desc">可视化管理多环境签名证书，自动化嵌入流水线。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🌐</div>
      <h3 class="feature__title">全平台覆盖</h3>
      <p class="feature__desc">支持 macOS、Windows、Linux、Android、Web 多端统一体验。</p>
    </div>
  </section>

  <!-- COMPARISON -->
  <section id="comparison" class="container comparison">
    <table>
      <tr>
        <th>对比项</th><th>Quasio</th><th>Electron</th><th>Cordova</th>
      </tr>
      <tr>
        <td>启动速度</td><td>≤100ms</td><td>≥1000ms</td><td>300–500ms</td>
      </tr>
      <tr>
        <td>包体体积</td><td>≈5MB</td><td>≥50MB</td><td>≈40MB</td>
      </tr>
      <tr>
        <td>底层技术</td><td>Rust / Tauri</td><td>Chromium + Node</td><td>WebView</td>
      </tr>
      <tr>
        <td>自动化</td><td>一条命令</td><td>需手动配置</td><td>需脚本化</td>
      </tr>
      <tr>
        <td>离线打包</td><td>原生支持</td><td>需插件</td><td>需网络</td>
      </tr>
    </table>
  </section>

  <!-- TESTIMONIALS -->
  <section id="testimonials" class="container testimonials">
    <div class="testimonial">
      <img class="testimonial__avatar" src="avatar1.jpg" alt="用户 A"/>
      <div class="testimonial__name">用户 A</div>
      <div class="testimonial__role">前端工程师</div>
      <p class="testimonial__text">
        “Quasio 让我在 5MB 以内打包应用简直神了，性能和体验都超出预期！”
      </p>
    </div>
    <div class="testimonial">
      <img class="testimonial__avatar" src="avatar2.jpg" alt="团队 B"/>
      <div class="testimonial__name">团队 B</div>
      <div class="testimonial__role">产品经理</div>
      <p class="testimonial__text">
        “一条命令搞定多端发布，离线测试也毫无压力，CI/CD 超便利。”
      </p>
    </div>
  </section>

  <!-- GALLERY -->
  <section id="gallery" class="gallery-section container">
    <h2>UI 预览</h2>
    <div class="gallery">
      <div class="gallery__item"><img src="ui-preview-1.png" alt="预览1"/></div>
      <div class="gallery__item"><img src="ui-preview-2.png" alt="预览2"/></div>
      <div class="gallery__item"><img src="ui-preview-3.png" alt="预览3"/></div>
    </div>
  </section>

  <!-- QUICKSTART -->
  <section id="quickstart" class="container quickstart">
    <h2 class="quickstart__title">快速开始</h2>
    <div class="tabs">
      <div class="tab active" data-target="cmd-web">Web</div>
      <div class="tab" data-target="cmd-android">Android</div>
      <div class="tab" data-target="cmd-desktop">Desktop</div>
    </div>
    <pre id="cmd-web"><code class="language-bash">
git clone https://github.com/yourname/quasio-lab.git
cd quasio-lab
npm install -g pake-cli
pake build:web      # 生成 Web 静态 Bundle
    </code></pre>
    <pre id="cmd-android" style="display:none"><code class="language-bash">
pake build:android  # 打包 Cordova Android APK
    </code></pre>
    <pre id="cmd-desktop" style="display:none"><code class="language-bash">
pake build:desktop  # 打包 Electron Windows/macOS 应用
    </code></pre>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="container">
      © 2025 Quasio Lab • 
      <a href="https://github.com/yourname/quasio-lab" target="_blank">GitHub</a> • 
      <a href="#features">文档</a> • 
      MIT License
    </div>
  </footer>

  <!-- Prism.js & 交互脚本 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js"></script>
  <script>
    // 移动端菜单
    const btnToggle = document.querySelector('.header__toggle');
    const nav = document.querySelector('.header__nav');
    btnToggle.onclick = ()=> nav.classList.toggle('active');

    // 主题切换
    const btnTheme = document.querySelector('.header__theme');
    const root = document.documentElement;
    let theme = localStorage.getItem('theme')||'light';
    root.setAttribute('data-theme', theme);
    btnTheme.textContent = theme==='light'?'🌙':'☀️';
    btnTheme.onclick = ()=>{
      theme = theme==='light'?'dark':'light';
      root.setAttribute('data-theme', theme);
      btnTheme.textContent = theme==='light'?'🌙':'☀️';
      localStorage.setItem('theme', theme);
    };

    // Quickstart Tabs
    document.querySelectorAll('.tab').forEach(tab=>{
      tab.onclick = ()=>{
        document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
        tab.classList.add('active');
        document.querySelectorAll('[id^="cmd-"]').forEach(pre=>pre.style.display='none');
        document.getElementById(tab.dataset.target).style.display='block';
      };
    });
  </script>
</body>
</html>
