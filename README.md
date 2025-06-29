<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>上传界面</title>
  <style>
    /* 通用重置和字体 */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #f0f2f5;
      color: #333;
      line-height: 1.6;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
    }

    /* 容器 */
    .upload-wrapper {
      background: #fff;
      width: 100%;
      max-width: 480px;
      border-radius: 8px;
      box-shadow: 0 4px 14px rgba(0, 0, 0, 0.1);
      overflow: hidden;
    }
    .upload-header {
      background: linear-gradient(90deg, #4e54c8, #8f94fb);
      padding: 20px;
      text-align: center;
      color: #fff;
    }
    .upload-header h1 {
      font-size: 24px;
      font-weight: 600;
    }

    /* 主体 */
    .upload-body {
      padding: 20px 24px;
    }
    .upload-description {
      margin-bottom: 16px;
      font-size: 14px;
      color: #666;
    }

    /* 上传区 */
    .upload-area {
      border: 2px dashed #ccc;
      border-radius: 6px;
      padding: 40px 20px;
      text-align: center;
      transition: border-color 0.3s, background-color 0.3s;
      cursor: pointer;
      position: relative;
    }
    .upload-area:hover {
      border-color: #4e54c8;
      background-color: rgba(78, 84, 200, 0.05);
    }
    .upload-area input[type="file"] {
      position: absolute;
      opacity: 0;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      cursor: pointer;
    }
    .upload-area .icon {
      font-size: 48px;
      color: #4e54c8;
      margin-bottom: 12px;
    }
    .upload-area p {
      font-size: 16px;
      color: #555;
    }
    .upload-area small {
      display: block;
      margin-top: 8px;
      font-size: 12px;
      color: #999;
    }

    /* 进度条 */
    .progress-bar {
      margin-top: 20px;
      height: 6px;
      background: #e0e0e0;
      border-radius: 3px;
      overflow: hidden;
      display: none;
    }
    .progress-bar-inner {
      width: 0;
      height: 100%;
      background: #4e54c8;
      transition: width 0.4s ease;
    }

    /* 按钮 */
    .upload-footer {
      padding: 16px 24px;
      text-align: right;
      background: #fafafa;
    }
    .btn {
      padding: 10px 20px;
      border: none;
      border-radius: 4px;
      font-size: 14px;
      font-weight: 500;
      cursor: pointer;
      transition: background 0.3s;
    }
    .btn-primary {
      background: #4e54c8;
      color: #fff;
    }
    .btn-primary:hover {
      background: #3b43a4;
    }
    .btn-secondary {
      background: #e0e0e0;
      color: #666;
      margin-right: 8px;
    }
    .btn-secondary:hover {
      background: #cfcfcf;
    }
  </style>
</head>
<body>
  <div class="upload-wrapper">
    <header class="upload-header">
      <h1>上传文件</h1>
    </header>
    <section class="upload-body">
      <p class="upload-description">支持拖拽或点击上传，单次最多可上传 5 个文件，支持 PNG/JPG/PDF。</p>
      <div class="upload-area" id="uploadArea">
        <div class="icon">📁</div>
        <p>将文件拖到此处，或点击选择</p>
        <small>最大 10MB/个 文件</small>
        <input type="file" id="fileInput" multiple />
      </div>
      <div class="progress-bar" id="progressBar">
        <div class="progress-bar-inner" id="progressBarInner"></div>
      </div>
    </section>
    <footer class="upload-footer">
      <button class="btn btn-secondary" id="resetBtn">重置</button>
      <button class="btn btn-primary" id="uploadBtn">开始上传</button>
    </footer>
  </div>

  <script>
    const fileInput = document.getElementById('fileInput');
    const uploadArea = document.getElementById('uploadArea');
    const uploadBtn = document.getElementById('uploadBtn');
    const resetBtn = document.getElementById('resetBtn');
    const progressBar = document.getElementById('progressBar');
    const progressBarInner = document.getElementById('progressBarInner');
    let files = [];

    uploadArea.addEventListener('dragover', e => {
      e.preventDefault();
      uploadArea.classList.add('hover');
    });
    uploadArea.addEventListener('dragleave', () => {
      uploadArea.classList.remove('hover');
    });
    uploadArea.addEventListener('drop', e => {
      e.preventDefault();
      files = Array.from(e.dataTransfer.files);
      console.log(files);
    });
    fileInput.addEventListener('change', e => {
      files = Array.from(e.target.files);
      console.log(files);
    });

    uploadBtn.addEventListener('click', () => {
      if (files.length === 0) {
        alert('请选择文件！');
        return;
      }
      progressBar.style.display = 'block';
      // 模拟上传进度
      let loaded = 0;
      const total = files.reduce((sum, f) => sum + f.size, 0);
      const interval = setInterval(() => {
        loaded += total / 50;
        if (loaded >= total) {
          loaded = total;
          clearInterval(interval);
          alert('上传完成！');
        }
        const percent = Math.round((loaded / total) * 100);
        progressBarInner.style.width = percent + '%';
      }, 100);
    });

    resetBtn.addEventListener('click', () => {
      files = [];
      fileInput.value = '';
      progressBar.style.display = 'none';
      progressBarInner.style.width = '0';
    });
  </script>
</body>
</html>
