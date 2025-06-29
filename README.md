<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>专业文件上传</title>
  <!-- Materialize CSS & Icons -->
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  <link href="https://cdn.jsdelivr.net/npm/materialize-css@1.0.0/dist/css/materialize.min.css" rel="stylesheet"/>
  <style>
    #drop-area {
      position: relative;
      border: 2px dashed #90caf9;
      border-radius: 8px;
      padding: 40px 20px;
      transition: background .2s, border-color .2s;
      cursor: pointer;
    }
    #drop-area.hover {
      background: #e3f2fd;
      border-color: #42a5f5;
    }
    #drop-area input {
      position: absolute;
      top:0; left:0; width:100%; height:100%;
      opacity:0; cursor: pointer;
    }
    #file-list .collection-item .secondary-content {
      cursor: pointer;
      color: #e53935;
    }
    #file-list .collection-item .secondary-content:hover {
      color: #b71c1c;
    }
  </style>
</head>
<body class="grey lighten-4">

  <div class="container" style="max-width:600px; margin-top: 4rem;">
    <div class="card">
      <div class="card-content">
        <span class="card-title center-align">📁 上传文件</span>
        <p class="center-align grey-text text-darken-1">支持拖拽或点击，最多 5 个文件，PNG/JPG/PDF，单文件 ≤ 10MB。</p>

        <div id="drop-area" class="center-align" tabindex="0">
          <i class="material-icons large blue-text text-darken-2">cloud_upload</i>
          <p class="blue-text text-darken-2">点此或拖拽文件到此处</p>
          <input type="file" id="fileElem" accept=".png,.jpg,.jpeg,.pdf" multiple>
        </div>

        <ul id="file-list" class="collection" style="margin-top:1rem;"></ul>

        <div id="progress-wrapper" class="progress blue lighten-4" style="height:6px; display:none;">
          <div class="determinate blue darken-2" style="width:0%"></div>
        </div>
      </div>

      <div class="card-action right-align">
        <a id="resetBtn" class="btn-flat grey-text text-darken-2">重置</a>
        <a id="uploadBtn" class="btn blue darken-2 white-text">开始上传</a>
      </div>
    </div>
  </div>

  <!-- Materialize & 脚本 -->
  <script src="https://cdn.jsdelivr.net/npm/materialize-css@1.0.0/dist/js/materialize.min.js"></script>
  <script>
    const dropArea = document.getElementById('drop-area');
    const fileElem = document.getElementById('fileElem');
    const fileList = document.getElementById('file-list');
    const uploadBtn = document.getElementById('uploadBtn');
    const resetBtn = document.getElementById('resetBtn');
    const progressWrapper = document.getElementById('progress-wrapper');
    const progressBar = progressWrapper.querySelector('.determinate');

    let files = [];

    // 高亮拖拽区
    ['dragenter','dragover'].forEach(ev => {
      dropArea.addEventListener(ev, e => {
        e.preventDefault(); dropArea.classList.add('hover');
      });
    });
    ['dragleave','drop'].forEach(ev => {
      dropArea.addEventListener(ev, e => {
        e.preventDefault(); dropArea.classList.remove('hover');
      });
    });

    // 获取文件
    dropArea.addEventListener('drop', e => {
      files = Array.from(e.dataTransfer.files);
      renderFileList();
    });
    fileElem.addEventListener('change', e => {
      files = Array.from(e.target.files);
      renderFileList();
    });

    // 渲染列表
    function renderFileList() {
      fileList.innerHTML = '';
      files.slice(0,5).forEach((file, idx) => {
        const li = document.createElement('li');
        li.className = 'collection-item';
        li.innerHTML = `
          <span>${file.name}</span>
          <i class="material-icons secondary-content" data-idx="${idx}">cancel</i>
        `;
        fileList.append(li);
      });
      // 绑定删除
      fileList.querySelectorAll('.secondary-content').forEach(icon => {
        icon.addEventListener('click', e => {
          files.splice(+e.target.dataset.idx,1);
          renderFileList();
        });
      });
    }

    // 重置
    resetBtn.addEventListener('click', () => {
      files = [];
      fileElem.value = '';
      renderFileList();
      progressWrapper.style.display = 'none';
      progressBar.style.width = '0%';
    });

    // 模拟上传
    uploadBtn.addEventListener('click', () => {
      if (!files.length) return M.toast({html: '请先选择文件！'});
      progressWrapper.style.display = 'block';
      const total = files.reduce((sum, f) => sum + f.size, 0);
      let loaded = 0;
      const step = total / 50;
      const timer = setInterval(() => {
        loaded = Math.min(loaded + step, total);
        const pct = Math.round(loaded / total * 100);
        progressBar.style.width = pct + '%';
        if (loaded >= total) {
          clearInterval(timer);
          M.toast({html: '上传完成！'});
        }
      }, 100);
    });

    // 初始化 Materialize 提示
    document.addEventListener('DOMContentLoaded', () => {
      M.AutoInit();
    });
  </script>
</body>
</html>
