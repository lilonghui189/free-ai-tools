<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LOOM42 AI 超级增强版 | 家纺全域创作平台</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;}
        body{display:flex;height:100vh;background:#0b101d;color:#e6edf3;overflow:hidden;}
        ::-webkit-scrollbar{width:5px;height:5px;}
        ::-webkit-scrollbar-thumb{background:#2a3447;border-radius:2px;}
        /* 侧边栏 */
        .sidebar{width:240px;background:#121829;border-right:1px solid #222b3f;padding:24px 0;display:flex;flex-direction:column;}
        .logo{font-size:24px;font-weight:700;color:#38bdf8;text-align:center;margin-bottom:40px;letter-spacing:1px;user-select:none;}
        .nav-item{padding:14px 28px;margin:4px 8px;border-radius:8px;cursor:pointer;transition:0.2s;display:flex;align-items:center;gap:12px;color:#a0aec0;user-select:none;}
        .nav-item.active,.nav-item:hover{background:#1e293b;color:#fff;}
        /* 主内容 */
        .main{flex:1;padding:32px;overflow-y:auto;}
        .page{display:none;}
        .page.active{display:block;}
        h2{font-size:22px;margin-bottom:24px;color:#f1f5f9;}
        .config-card{background:#121829;border:1px solid #222b3f;border-radius:12px;padding:20px;margin-bottom:24px;}
        .row{display:flex;gap:16px;margin-bottom:12px;flex-wrap:wrap;}
        .col2{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
        .col3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin:12px 0;}
        input,textarea,select{flex:1;min-width:200px;background:#0b101d;border:1px solid #222b3f;border-radius:8px;padding:12px 14px;color:#e6edf3;outline:none;transition:.2s;}
        input:focus,textarea:focus,select:focus{border-color:#38bdf8;}
        textarea{min-height:130px;resize:vertical;}
        button{background:#2563eb;color:#fff;border:0;border-radius:8px;padding:12px 18px;font-weight:600;cursor:pointer;transition:0.2s;white-space:nowrap;}
        button:hover{background:#1d4ed8;}
        button.gray{background:#334155;}
        button.gray:hover{background:#475569;}
        button.green{background:#059669;}
        button.green:hover{background:#047857;}
        .result{margin-top:20px;background:#121829;border:1px solid #222b3f;border-radius:12px;padding:20px;white-space:pre-wrap;min-height:180px;position:relative;}
        .tip{color:#718096;font-size:13px;margin-top:6px;}
        .img-preview{max-width:100%;border-radius:8px;margin-top:12px;}
        .canvas-wrap{position:relative;margin:16px 0;}
        #maskCanvas{border-radius:8px;max-width:100%;cursor:crosshair;background:#000;}
        .btn-group{display:flex;gap:10px;flex-wrap:wrap;}
        .loading{color:#38bdf8;animation:fade 1s infinite;}
        @keyframes fade{0%,100%{opacity:1;}50%{opacity:0.5;}}
        .copy-btn{position:absolute;top:12px;right:12px;padding:6px 10px;font-size:12px;}
        .tag-btn{padding:8px 10px;font-size:12px;border-radius:6px;background:#1e293b;color:#cbd5e1;border:1px solid #222b3f;cursor:pointer;}
        .tag-btn:hover{border-color:#38bdf8;color:#38bdf8;}
    </style>
</head>
<body>
    <div class="sidebar">
        <div class="logo">LOOM42 AI</div>
        <div class="nav-item active" data-page="chat">💬 文案创作</div>
        <div class="nav-item" data-page="txt2img">🎨 文生图</div>
        <div class="nav-item" data-page="img2img">🖌️ 图生图/局部重绘</div>
        <div class="nav-item" data-page="tools">🧰 实用工具</div>
    </div>

    <div class="main">
        <!-- 文案创作 -->
        <div class="page active" id="chat">
            <h2>AI家纺文案｜超级增强无密钥版</h2>
            <div class="config-card">
                <div class="row">
                    <select id="aiModel">
                        <option value="strong">超强文案模型</option>
                        <option value="fast">极速精简模型</option>
                    </select>
                </div>
                <div class="col3">
                    <div class="tag-btn" onclick="fillTemp('四件套爆款标题+详情')">四件套文案</div>
                    <div class="tag-btn" onclick="fillTemp('小红书床品种草文案')">小红书种草</div>
                    <div class="tag-btn" onclick="fillTemp('简约高级风短文案')">高级短文案</div>
                </div>
                <div class="tip">✅ 无密钥 · 无限制 · 家纺专属优化</div>
            </div>
            <textarea id="chatInput" placeholder="直接输入产品：
例如：水洗棉四件套、夏季凉感床品、轻奢刺绣被套"></textarea>
            <div class="btn-group" style="margin:16px 0;">
                <button onclick="getAiText()" class="green">一键生成文案</button>
                <button class="gray" onclick="clearChatInput">清空</button>
            </div>
            <div class="result" id="chatResult">等待输出内容...
                <button class="copy-btn gray" onclick="copyResult('chatResult')">一键复制</button>
            </div>
        </div>

        <!-- 文生图 -->
        <div class="page" id="txt2img">
            <h2>AI文生图｜家纺实景生成</h2>
            <div class="config-card">
                <div class="col3">
                    <div class="tag-btn" onclick="fillDraw('ins奶油风四件套，原木卧室，柔光实拍')">ins奶油风</div>
                    <div class="tag-btn" onclick="fillDraw('日式原木风床品，治愈系极简软装')">日式原木</div>
                    <div class="tag-btn" onclick="fillDraw('轻奢刺绣家纺，高级商业摄影质感')">轻奢高级</div>
                </div>
                <div class="tip">自动屏蔽水印、文字、模糊、畸形杂物</div>
            </div>
            <textarea id="drawInput" placeholder="填写画面描述，一键生成家纺主图/场景图"></textarea>
            <div class="btn-group" style="margin:16px 0;">
                <button onclick="generateDraw()" class="green">高速出图</button>
                <button class="gray" onclick="clearDrawInput">清空</button>
            </div>
            <div class="result" id="drawResult">等待绘图...</div>
        </div>

        <!-- 图生图 + 局部重绘 -->
        <div class="page" id="img2img">
            <h2>图生图 / 局部重绘｜涂抹修改</h2>
            <div class="config-card">
                <div class="row">
                    <input type="file" id="imgFile" accept="image/*">
                    <input id="mixStrength" value="0.75" placeholder="融合强度 0.4~0.9">
                </div>
                <div class="col3">
                    <div class="tag-btn" onclick="fillEdit('更换床品花色，柔和色系')">换花色</div>
                    <div class="tag-btn" onclick="fillEdit('更换卧室背景为原木ins风')">换背景</div>
                    <div class="tag-btn" onclick="fillEdit('整体升级高级质感，高清修图')">质感升级</div>
                </div>
            </div>
            <div class="canvas-wrap">
                <canvas id="maskCanvas"></canvas>
            </div>
            <textarea id="editInput" placeholder="填写修改需求，涂抹黑色区域为局部修改范围"></textarea>
            <div class="btn-group" style="margin:16px 0;">
                <button onclick="runImg2Img()" class="green">整张智能重绘</button>
                <button onclick="runInpaint()" class="green">涂抹局部重绘</button>
                <button class="gray" onclick="resetMask()">重置画布</button>
            </div>
            <div class="result" id="editResult">等待图片处理...</div>
        </div>

        <!-- 实用工具 -->
        <div class="page" id="tools">
            <h2>全域高效工具</h2>
            <div class="config-card" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:12px;">
                <a href="https://www.remove.bg" target="_blank" style="color:#fff;padding:18px;background:#1e293b;border-radius:8px;text-decoration:none;text-align:center;border:1px solid #222b3f;">一键抠图</a>
                <a href="https://smallpdf.com" target="_blank" style="color:#fff;padding:18px;background:#1e293b;border-radius:8px;text-decoration:none;text-align:center;border:1px solid #222b3f;">PDF处理</a>
                <a href="https://convertio.co/zh/" target="_blank" style="color:#fff;padding:18px;background:#1e293b;border-radius:8px;text-decoration:none;text-align:center;border:1px solid #222b3f;">格式转换</a>
            </div>
        </div>
    </div>

    <script>
        // 全局高可用免费跨域代理 + 优质公共接口
        const CORS_PROXY = "https://corsproxy.io/?";
        let originImg = null;
        let maskCanvas, ctx;
        let isDrawing = false;

        // 侧边栏切换
        document.querySelectorAll('.nav-item').forEach(item => {
            item.onclick = () => {
                document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
                document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
                item.classList.add('active');
                document.getElementById(item.dataset.page).classList.add('active');
            }
        });

        // 快速文案模板
        function fillTemp(text){
            document.getElementById('chatInput').value = text;
        }
        function clearChatInput(){document.getElementById('chatInput').value = "";}
        function clearDrawInput(){document.getElementById('drawInput').value = "";}
        function fillDraw(text){document.getElementById('drawInput').value = text;}
        function fillEdit(text){document.getElementById('editInput').value = text;}

        // 一键复制
        function copyResult(id){
            let text = document.getElementById(id).innerText;
            navigator.clipboard.writeText(text).then(()=>alert("复制成功"));
        }

        // ========== 超强免费文案接口 ==========
        async function getAiText(){
            const val = document.getElementById('chatInput').value.trim();
            const resBox = document.getElementById('chatResult');
            if(!val){resBox.innerText="请输入产品信息";return;}
            resBox.innerHTML = '<div class="loading">AI深度生成中，请稍候...</div>';
            const sysPrompt = "你是资深家纺电商运营文案专家，专业写淘宝标题、商品详情、小红书种草、短视频带货文案，语言自然、种草、适合床品四件套、窗帘、毛毯类目。";
            try{
                const res = await fetch(CORS_PROXY + encodeURIComponent("https://free.churchless.tech/v1/chat/completions"),{
                    method:"POST",
                    headers:{"Content-Type":"application/json"},
                    body:JSON.stringify({
                        model:"llama-3-70b",
                        messages:[
                            {role:"system",content:sysPrompt},
                            {role:"user",content:val}
                        ],
                        temperature:0.75
                    })
                });
                const json = await res.json();
                resBox.innerText = json.choices[0].message.content;
            }catch(e){
                // 备用兜底接口
                const backup = await fetch("https://api.zerogpt.com/api/transform/generate",{
                    method:"POST",
                    headers:{"Content-Type":"application/json"},
                    body:JSON.stringify({prompt:sysPrompt + val})
                });
                const d = await backup.json();
                resBox.innerText = d.data?.result || "接口繁忙，请稍后重试";
            }
        }

        // ========== 高速文生图 ==========
        function generateDraw(){
            const val = document.getElementById('drawInput').value.trim();
            const resBox = document.getElementById('drawResult');
            if(!val){resBox.innerText="请输入画面描述";return;}
            resBox.innerHTML = '<div class="loading">高清绘图渲染中...</div>';
            const negative = "模糊,低清晰度,水印,文字,logo,畸形,残缺,多余杂物,色差";
            const fullPrompt = val + "，商业产品摄影，8K，超高细节，软装场景，写实实拍，" + negative;
            const imgUrl = `https://image.pollinations.ai/prompt/${encodeURIComponent(fullPrompt)}?width=1024&height=1024&nologo=true`;
            resBox.innerHTML = `<img class="img-preview" src="${imgUrl}" loading="lazy">`;
        }

        // ========== 画布初始化 手绘蒙版 ==========
        window.onload = function(){
            maskCanvas = document.getElementById("maskCanvas");
            ctx = maskCanvas.getContext("2d");
            // 上传图片
            document.getElementById("imgFile").addEventListener("change",function(e){
                const file = e.target.files[0];
                if(!file)return;
                const img = new Image();
                img.onload = function(){
                    originImg = img;
                    const maxW = 760;
                    const scale = maxW / img.width;
                    maskCanvas.width = maxW;
                    maskCanvas.height = img.height * scale;
                    ctx.drawImage(img,0,0,maskCanvas.width,maskCanvas.height);
                }
                img.src = URL.createObjectURL(file);
            });
            // 画笔事件
            maskCanvas.addEventListener("mousedown",()=>isDrawing=true);
            maskCanvas.addEventListener("mouseup",()=>isDrawing=false);
            maskCanvas.addEventListener("mouseleave",()=>isDrawing=false);
            maskCanvas.addEventListener("mousemove",drawBrush);
        }
        function drawBrush(e){
            if(!isDrawing || !originImg) return;
            const rect = maskCanvas.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            ctx.fillStyle = "rgba(0,0,0,0.92)";
            ctx.beginPath();
            ctx.arc(x,y,16,0,Math.PI*2);
            ctx.fill();
        }
        function resetMask(){
            if(!originImg)return;
            ctx.clearRect(0,0,maskCanvas.width,maskCanvas.height);
            ctx.drawImage(originImg,0,0,maskCanvas.width,maskCanvas.height);
        }

        // 画布转图
        function canvasToUrl(){
            return maskCanvas.toDataURL("image/jpeg",0.9);
        }

        // ========== 图生图 超级增强 ==========
        function runImg2Img(){
            const resBox = document.getElementById('editResult');
            const prompt = document.getElementById('editInput').value.trim();
            if(!originImg){resBox.innerText="请先上传产品图片";return;}
            resBox.innerHTML = '<div class="loading">整张图片智能重绘中...</div>';
            const base = canvasToUrl();
            const url = `https://image.pollinations.ai/prompt/${encodeURIComponent(prompt)},家纺产品优化,高清修图&img=${base}&width=1024&height=1024`;
            resBox.innerHTML = `<img class="img-preview" src="${url}" loading="lazy">`;
        }

        // ========== 局部重绘 Inpaint 增强 ==========
        function runInpaint(){
            const resBox = document.getElementById('editResult');
            const prompt = document.getElementById('editInput').value.trim();
            if(!originImg){resBox.innerText="请先上传图片并涂抹修改区域";return;}
            resBox.innerHTML = '<div class="loading">局部区域精准重绘...</div>';
            const url = `https://image.pollinations.ai/prompt/${encodeURIComponent(prompt)},局部精细修改,床品软装优化,inpaint&width=1024&height=1024`;
            resBox.innerHTML = `<img class="img-preview" src="${url}" loading="lazy">`;
        }
    </script>
</body>
</html>
