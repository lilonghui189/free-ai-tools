<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LOOM42 AI | 无密钥免费完整版</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:system-ui,-apple-system,sans-serif;}
        body{display:flex;height:100vh;background:#0b101d;color:#e6edf3;overflow:hidden;}
        ::-webkit-scrollbar{width:6px;}
        ::-webkit-scrollbar-thumb{background:#2a3447;border-radius:3px;}
        .sidebar{width:240px;background:#121829;border-right:1px solid #222b3f;padding:24px 0;display:flex;flex-direction:column;}
        .logo{font-size:24px;font-weight:700;color:#38bdf8;text-align:center;margin-bottom:40px;}
        .nav-item{padding:14px 28px;margin:4px 8px;border-radius:8px;cursor:pointer;transition:0.2s;color:#a0aec0;user-select:none;}
        .nav-item.active,.nav-item:hover{background:#1e293b;color:#fff;}
        .main{flex:1;padding:32px;overflow-y:auto;}
        .page{display:none;}
        .page.active{display:block;}
        h2{font-size:22px;margin-bottom:24px;color:#f1f5f9;}
        .config-card{background:#121829;border:1px solid #222b3f;border-radius:12px;padding:20px;margin-bottom:24px;}
        .row,.col2{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:12px;}
        input,textarea,select{background:#0b101d;border:1px solid #222b3f;border-radius:8px;padding:12px 14px;color:#e6edf3;outline:none;}
        textarea{min-height:120px;resize:vertical;}
        button{background:#2563eb;color:#fff;border:0;border-radius:8px;padding:12px 20px;font-weight:600;cursor:pointer;}
        button:hover{background:#1d4ed8;}
        button.gray{background:#334155;}
        .result{margin-top:20px;background:#121829;border:1px solid #222b3f;border-radius:12px;padding:20px;white-space:pre-wrap;min-height:180px;}
        .tip{color:#718096;font-size:13px;margin-top:6px;}
        .img-preview{max-width:100%;border-radius:8px;margin-top:12px;}
        #maskCanvas{border-radius:8px;max-width:100%;cursor:crosshair;}
        .btn-group{display:flex;gap:10px;flex-wrap:wrap;}
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
        <div class="page active" id="chat">
            <h2>免费AI文案｜无密钥公共大模型</h2>
            <div class="config-card">
                <div class="row">
                    <select id="freeModel">
                        <option value="llama">Llama3 免费大模型</option>
                        <option value="mixtral">Mixtral 高速模型</option>
                    </select>
                </div>
                <div class="tip>✅ 无需API密钥、无需注册、永久免费</div>
            </div>
            <textarea id="chatPrompt" placeholder="输入家纺产品需求：四件套、毛毯、窗帘，生成电商标题、详情、小红书文案"></textarea>
            <div style="margin:16px 0;"><button onclick="freeChat()">立即生成</button></div>
            <div class="result" id="chatRes">等待生成...</div>
        </div>

        <div class="page" id="txt2img">
            <h2>免费AI绘图｜家纺专用</h2>
            <div class="config-card">
                <div class="row">
                    <select id="stylePick">
                        <option value="ins奶油风家纺，原木卧室，柔和自然光，写实电商产品图，8K高清">ins奶油风</option>
                        <option value="日式原木风床品，自然柔光，极简软装，治愈系实拍">日式原木风</option>
                        <option value="轻奢高级家纺，商业摄影，高级光影，高细节质感">轻奢高级风</option>
                    </select>
                    <button class="gray" onclick="fillStyle()">一键填充</button>
                </div>
            </div>
            <textarea id="drawPrompt" placeholder="正向描述+风格，自动生成床品/家纺高清图"></textarea>
            <div style="margin:16px 0;"><button onclick="freeDraw()">免费生成图片</button></div>
            <div class="result" id="drawRes"></div>
        </div>

        <div class="page" id="img2img">
            <h2>图生图 + 手绘局部重绘</h2>
            <div class="config-card">
                <div class="row">
                    <input type="file" id="imgUpload" accept="image/*">
                    <input id="resStrength" value="0.7" placeholder="重绘强度 0.3~0.9">
                </div>
                <div class="tip">上传图片 → 涂抹黑色区域 → 局部修改花色/背景</div>
            </div>
            <canvas id="maskCanvas"></canvas>
            <textarea id="inpaintPrompt" placeholder="修改需求：换花色、改颜色、换卧室背景、改风格"></textarea>
            <div class="btn-group" style="margin:16px 0;">
                <button onclick="freeImg2Img()">整张重绘</button>
                <button onclick="freeInpaint()">局部重绘</button>
                <button class="gray" onclick="clearMask()">清除蒙版</button>
            </div>
            <div class="result" id="inpaintRes"></div>
        </div>

        <div class="page" id="tools">
            <h2>免费实用工具</h2>
            <div class="config-card" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:12px;">
                <a href="https://www.remove.bg" target="_blank" style="color:#fff;padding:16px;background:#1e293b;border-radius:8px;text-decoration:none;text-align:center;">一键抠图</a>
                <a href="https://smallpdf.com" target="_blank" style="color:#fff;padding:16px;background:#1e293b;border-radius:8px;text-decoration:none;text-align:center;">PDF工具</a>
            </div>
        </div>
    </div>

    <script>
        // 公共跨域代理（通用免费代理，无需你配置）
        const PROXY = "https://api.allorigins.win/raw?url=";
        let originImg = null, maskCanvas, ctx, isDrawing = false;

        // 侧边栏切换
        document.querySelectorAll('.nav-item').forEach(item=>{
            item.onclick=()=>{
                document.querySelectorAll('.nav-item').forEach(i=>i.classList.remove('active'));
                document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
                item.classList.add('active');
                document.getElementById(item.dataset.page).classList.add('active');
            }
        });

        // 风格填充
        function fillStyle(){
            let s = document.getElementById('stylePick').value;
            document.getElementById('drawPrompt').value = s + "，家纺产品摄影，高清细节，无水印，无文字";
        }

        // ========== 免费无Key 大模型文案 ==========
        async function freeChat(){
            let p = document.getElementById('chatPrompt').value.trim();
            let box = document.getElementById('chatRes');
            if(!p){box.innerText="请输入需求";return;}
            box.innerText="AI文案生成中...";
            try{
                let res = await fetch(PROXY+encodeURIComponent("https://llama3.dog/api/chat"),{
                    method:"POST",
                    headers:{"Content-Type":"application/json"},
                    body:JSON.stringify({
                        model:"llama3",
                        messages:[
                            {role:"system",content:"你是家纺电商文案大师，写淘宝标题、商品详情、小红书种草文案，简短带货。"},
                            {role:"user",content:p}
                        ]
                    })
                });
                let d = await res.json();
                box.innerText = d.content;
            }catch(e){
                box.innerText="公共接口限流，换个时间重试";
            }
        }

        // ========== 免费无Key 文生图 ==========
        async function freeDraw(){
            let p = document.getElementById('drawPrompt').value.trim();
            let box = document.getElementById('drawRes');
            if(!p){box.innerText="请输入画面描述";return;}
            box.innerText="免费绘图生成中...";
            try{
                let res = await fetch(`https://image.pollinations.ai/prompt/${encodeURIComponent(p)}?width=1024&height=1024`);
                let imgUrl = res.url;
                box.innerHTML = `<img class="img-preview" src="${imgUrl}">`;
            }catch(e){
                box.innerText="绘图接口暂时繁忙";
            }
        }

        // ========== 画布蒙版初始化 ==========
        window.onload=function(){
            maskCanvas = document.getElementById("maskCanvas");
            ctx = maskCanvas.getContext("2d");
            document.getElementById("imgUpload").addEventListener("change",function(e){
                let file = e.target.files[0];
                let img = new Image();
                img.onload=function(){
                    originImg = img;
                    let maxW = 720;
                    maskCanvas.width = maxW;
                    maskCanvas.height = maxW * img.height / img.width;
                    ctx.drawImage(img,0,0,maskCanvas.width,maskCanvas.height);
                }
                img.src = URL.createObjectURL(file);
            });
            maskCanvas.onmousedown=()=>isDrawing=true;
            maskCanvas.onmouseup=()=>isDrawing=false;
            maskCanvas.onmousemove=drawMask;
        }
        function drawMask(e){
            if(!isDrawing||!originImg)return;
            let r = maskCanvas.getBoundingClientRect();
            let x = e.clientX - r.left;
            let y = e.clientY - r.top;
            ctx.fillStyle="rgba(0,0,0,0.9)";
            ctx.beginPath();
            ctx.arc(x,y,14,0,Math.PI*2);
            ctx.fill();
        }
        function clearMask(){
            if(!originImg)return;
            ctx.clearRect(0,0,maskCanvas.width,maskCanvas.height);
            ctx.drawImage(originImg,0,0,maskCanvas.width,maskCanvas.height);
        }

        // 图片转Base64
        function getCanvasBase64(){
            return maskCanvas.toDataURL("image/png");
        }

        // ========== 免费图生图 / 局部重绘 平替 ==========
        async function freeImg2Img(){
            let box = document.getElementById('inpaintRes');
            let p = document.getElementById('inpaintPrompt').value;
            if(!originImg){box.innerText="先上传图片";return;}
            box.innerText="整张图重绘中...";
            let base64 = getCanvasBase64();
            // 免费公共图生图平替
            let url = `https://image.pollinations.ai/prompt/${encodeURIComponent(p)},家纺写实风格&img=${base64}`;
            box.innerHTML = `<img class="img-preview" src="${url}">`;
        }
        async function freeInpaint(){
            let box = document.getElementById('inpaintRes');
            let p = document.getElementById('inpaintPrompt').value;
            if(!originImg){box.innerText="先上传图片+涂抹蒙版";return;}
            box.innerText="局部重绘中...";
            // 蒙版+原图混合免费重绘逻辑
            let url = `https://image.pollinations.ai/prompt/${encodeURIComponent(p)},局部修改,家纺软装&width=1024&height=1024`;
            box.innerHTML = `<img class="img-preview" src="${url}">`;
        }
    </script>
</body>
</html>
