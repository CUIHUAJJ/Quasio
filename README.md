<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>文件上传</title>
  <!-- 引入 Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="min-h-screen bg-gray-100 flex items-center justify-center p-4">
  <div class="w-full max-w-md bg-white rounded-xl shadow-lg overflow-hidden">
    <!-- 标题 -->
    <header class="bg-gradient-to-r from-indigo-600 to-purple-600 p-6 text-white">
      <h1 class="text-2xl font-semibold">上传文件</h1>
    </header>

    <!-- 说明 & 上传区 -->
    <section class="p-6">
      <p class="text-gray-600 mb-4">支持拖拽或点击选择，最多 5 个文件，PNG/JPG/PDF。</p>
      
      <div id="dropZone"
           class="border-2 border-dashed border-gray-300 rounded-md p-8 text-center cursor-pointer hover:border-indigo-500 hover:bg-indigo-50 transition">
        <div class="text-indigo-500 text-4xl mb-2">📂</div>
        <p class="text-gray-700">将文件拖到此处，或点击选择</p>
        <small class="text-gray-500">单文件 ≤ 10MB</small>
        <input type="file" id="fileInput" multiple class="absolute inset-0 w-full h-full opacity-0 cursor-pointer"/>
      </div>

      <!-- 文件预览列表 -->
      <ul id="fileList" class="mt-4 space-y-2"></ul>

      <!-- 进度条 -->
      <div id="progressWrapper" class="mt-6 hidden">
        <div class="text-right text-sm text-gray-600 mb-1"><span id="percent">0%</span></div>
        <div class="w-full bg-gray-200 rounded-full overflow-hidden">
          <div id="progressBar" class="h-2 bg-indigo-600 w-0 transition-all"></div>
        </div>
      </div>
    </section>

    <!-- 按钮组 -->
    <footer class="bg-gray-50 p-6 flex justify-end space-x-3">
      <button id="resetBtn" class="px-4 py-2 bg-gray-200 rounded hover:bg-gray-300 text-gray-700">
        重置
      </button>
      <button id="uploadBtn" class="px-4 py-2 bg-indigo-600 rounded hover:bg-indigo-700 text-white">
        开始上传
      </button>
    </footer>
  </div>

  <script>
    const dropZone = document.getElementById('dropZone');
    const fileInput = document.getElementById('fileInput');
    const fileList  = document.getElementById('fileList');
    const uploadBtn = document.getElementById('uploadBtn');
    const resetBtn  = document.getElementById('resetBtn');
    const progWrap  = document.getElementById('progressWrapper');
    const progBar   = document.getElementById('progressBar');
    const percentEl = document.getElementById('percent');

    let files = [];

    // 拖拽样式
    ['dragenter','dragover'].forEach(ev => {
      dropZone.addEventListener(ev, e => {
        e.preventDefault();
        dropZone.classList.add('border-indigo-500','bg-indigo-50');
      });
    });
    ['dragleave','drop'].forEach(ev => {
      dropZone.addEventListener(ev, e => {
        e.preventDefault();
        dropZone.classList.remove('border-indigo-500','bg-indigo-50');
      });
    });

    // 拖拽/选择文件回调
    dropZone.addEventListener('drop', e => {
      files = Array.from(e.dataTransfer.files);
      renderList();
    });
    fileInput.addEventListener('change', e => {
      files = Array.from(e.target.files);
      renderList();
    });

    // 渲染文件列表
    function renderList() {
      fileList.innerHTML = '';
      files.slice(0, 5).forEach((f, i) => {
        const li = document.createElement('li');
        li.className = 'flex items-center justify-between bg-gray-50 p-2 rounded';
        li.innerHTML = `
          <span class="text-gray-800 text-sm truncate">${f.name}</span>
          <button data-index="${i}" class="text-red-500 hover:text-red-700 text-sm">移除</button>
        `;
        fileList.append(li);
      });

      // 绑定移除
      fileList.querySelectorAll('button').forEach(btn => {
        btn.addEventListener('click', e => {
          files.splice(+e.target.dataset.index, 1);
          renderList();
        });
      });
    }

    // 重置
    resetBtn.addEventListener('click', () => {
      files = [];
      fileInput.value = '';
      renderList();
      progWrap.classList.add('hidden');
      progBar.style.width = '0';
      percentEl.textContent = '0%';
    });

    // 模拟上传
    uploadBtn.addEventListener('click', () => {
      if (!files.length) return alert('请先选择文件');
      progWrap.classList.remove('hidden');
      let uploaded = 0, total = files.reduce((s,f)=>s+f.size,0);
      const interval = setInterval(() => {
        uploaded += total/60;
        if (uploaded >= total) {
          clearInterval(interval);
          uploaded = total;
          alert('上传完成！');
        }
        const p = Math.min(100, Math.floor(uploaded/total*100));
        progBar.style.width = p+'%';
        percentEl.textContent = p+'%';
      }, 100);
    });
  </script>
</body>
</html>
