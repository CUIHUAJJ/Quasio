<!-- HERO -->
  <section class="container hero">
    <h1 class="hero__title">Quasio · 跨平台开发实验室</h1>
    <p class="hero__desc">
      一站式打包分发：Android/Cordova、Windows/Electron、Web 静态 Bundle，CI/CD 零配置，离线一键打包。
    </p>
    <div class="hero__badges">
      <img src="https://img.shields.io/github/v/release/yourname/quasio-lab?color=5568f1" alt="Release"/>
      <img src="https://img.shields.io/github/license/yourname/quasio-lab" alt="License"/>
      <img src="https://img.shields.io/github/stars/yourname/quasio-lab?style=social" alt="Stars"/>
      <img src="https://img.shields.io/badge/downloads-10K+-blue" alt="Downloads"/>
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
      <p class="feature__desc">瞬时生成 APK/EXE/HTML Bundle，断网也能测试。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🔐</div>
      <h3 class="feature__title">安全签名管理</h3>
      <p class="feature__desc">可视化切换多环境签名与证书，内置流水线。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">📊</div>
      <h3 class="feature__title">实时监控</h3>
      <p class="feature__desc">日志、状态、报表 Web Dashboard 一览无余。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🌐</div>
      <h3 class="feature__title">多平台覆盖</h3>
      <p class="feature__desc">Android、Web、Windows、macOS、Linux 全平台支持。</p>
    </div>
    <div class="feature">
      <div class="feature__icon">🤝</div>
      <h3 class="feature__title">开源 & 社区共建</h3>
      <p class="feature__desc">完整源码、自由扩展，社区生态持续增长。</p>
    </div>
  </section>

  <!-- GALLERY -->
  <section id="gallery" class="container gallery">
    <div class="gallery__item">
      <img src="ui-preview-1.png" alt="UI 预览 1"/>
    </div>
    <div class="gallery__item">
      <img src="ui-preview-2.png" alt="UI 预览 2"/>
    </div>
  </section>

  <!-- QUICKSTART -->
  <section id="quickstart" class="container quickstart">
    <h2 class="quickstart__title">快速开始</h2>
    <pre><code class="language-bash">git clone https://github.com/yourname/quasio-lab.git
cd quasio-lab
npm install -g pake-cli
pake build:web      # Web 静态 Bundle
pake build:android  # Cordova Android APK
pake build:desktop  # Electron Windows/macOS</code></pre>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    © 2025 Quasio Lab • <a href="https://github.com/yourname/quasio-lab" target="_blank" rel="noopener">GitHub 项目</a> • MIT License
  </footer>

  <!-- Prism.js & 主题切换 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js"></script>
  <script>
    const btnTheme = document.querySelector('.header__theme');
    const root = document.documentElement;
    // 加载上次主题
    const saved = localStorage.getItem('theme');
    if (saved) {
      root.setAttribute('data-theme', saved);
      btnTheme.textContent = saved === 'light' ? '🌙' : '☀️';
    }
    // 切换
    btnTheme.addEventListener('click', () => {
      const next = root.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
      root.setAttribute('data-theme', next);
      btnTheme.textContent = next === 'light' ? '🌙' : '☀️';
      localStorage.setItem('theme', next);
    });
  </script>
</body>
</html>
