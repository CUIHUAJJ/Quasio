<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <title>文件上传</title>
  <!-- Bootstrap 5 & Icons CDN -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet"/>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.5/font/bootstrap-icons.css" rel="stylesheet"/>
  <style>
    .border-dashed { border-style: dashed !important; }
    .drop-zone { transition: background .2s, border-color .2s; }
    .drop-zone.dragover { background: #f8f9fa; border-color: #0d6efd; }
  </style>
</head>
<body class="bg-light d-flex align-items-center justify-content-center vh-100 p-3">
  <div class="card shadow-sm w-100" style="max-width:480px">
    <div class="card-header bg-primary text-white d-flex align-items-center">
      <i class="bi bi-cloud-upload-fill fs-2 me-2"></i>
      <h5 class="mb-0">上传文件</h5>
    </div>
    <div class="card-body">
      <p class="text-muted">拖拽或点击选择，最多 5 个文件，PNG/JPG/PDF，单文件 ≤ 10 MB。</p>
      <div id="dropZone" class="drop-zone border border-secondary border-dashed rounded p-5 text-center position-relative">
        <i class="bi bi-file-earmark-arrow-up fs-1 text-primary mb-2"></i>
        <div class="fw-semibold">将文件拖这里，或点击选择</div>
        <input type="file" id="fileInput" multiple class="position-absolute top-0 start-0 w-100 h-100 opacity-0 cursor-pointer"/>
      </div>

      <ul id="fileList" class="list-group list-group-flush mt-3"></ul>

      <div id="progressContainer" class="mt-4 d-none">
        <div class="d-flex justify-content-between mb-1">
          <small id="percentText">0%</small>
          <small id="sizeText">0 / 0 MB</small>
        </div>
        <div class="progress">
          <div id="progressBar" class="progress-bar progress-bar-striped progress-bar-animated"
               role="progressbar" style="width: 0%"></div>
        </div>
      </div>
    </div>
    <div class="card-footer bg-white text-end">
      <button id="resetBtn" class="btn btn-secondary me-2">重置</button>
      <button id="uploadBtn" class="btn btn-primary">开始上传</button>
    </div>
  </div>

  <script>
    const dropZone = document.getElementById('dropZone');
    const fileInput = document.getElementById('fileInput');
    const fileList  = document.getElementById('fileList');
    const uploadBtn = document.getElementById('uploadBtn');
    const resetBtn  = document.getElementById('resetBtn');
    const progCont  = document.getElementById('progressContainer');
    const progBar   = document.getElementById('progressBar');
    const percentText = document.getElementById('percentText');
    const sizeText    = document.getElementById('sizeText');

    let files = [];

    // 拖拽样式切换
    ['dragenter','dragover'].forEach(e => {
      dropZone.addEventListener(e, ev => {
        ev.preventDefault();
        dropZone.classList.add('dragover');
      });
    });
    ['dragleave','drop'].forEach(e => {
      dropZone.addEventListener(e, ev => {
        ev.preventDefault();
        dropZone.classList.remove('dragover');
      });
    });

    // 文件获取 & 列表渲染
    function renderFiles() {
      fileList.innerHTML = '';
      files.slice(0,5).forEach((f,i) => {
        const li = document.createElement('li');
        li.className = 'list-group-item d-flex justify-content-between align-items-center';
        li.innerHTML = `
          <div class="text-truncate" style="max-width:70%">${f.name}</div>
          <button class="btn btn-sm btn-outline-danger" data-idx="${i}">
            <i class="bi bi-x"></i>
          </button>`;
        fileList.append(li);
      });
      fileList.querySelectorAll('button').forEach(btn=>{
        btn.onclick = () => {
          files.splice(+btn.dataset.idx,1);
          renderFiles();
        };
      });
    }

    dropZone.addEventListener('drop', e => {
      files = Array.from(e.dataTransfer.files);
      renderFiles();
    });
    fileInput.addEventListener('change', e => {
      files = Array.from(e.target.files);
      renderFiles();
    });

    // 重置
    resetBtn.onclick = () => {
      files = [];
      fileInput.value = '';
      renderFiles();
      progCont.classList.add('d-none');
      progBar.style.width = '0';
      percentText.textContent = '0%';
      sizeText.textContent = '0 / 0 MB';
    };

    // 模拟上传
    uploadBtn.onclick = () => {
      if (!files.length) return alert('请先选择文件');
      progCont.classList.remove('d-none');
      const total = files.reduce((s,f)=>s+f.size,0);
      let uploaded = 0;
      const interval = setInterval(()=>{
        uploaded += total/60;
        if (uploaded >= total) {
          clearInterval(interval);
          uploaded = total;
          alert('上传完成！');
        }
        const perc = Math.floor(uploaded/total*100);
        progBar.style.width = perc+'%';
        percentText.textContent = perc+'%';
        sizeText.textContent = `${(uploaded/1024/1024).toFixed(1)} / ${(total/1024/1024).toFixed(1)} MB`;
      },100);
    };
  </script>
</body>
</html>
