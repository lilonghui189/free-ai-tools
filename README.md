<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LOOM42 AI｜家纺全能创作平台</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;font-family:system-ui,-apple-system,sans-serif;}
        body{display:flex;height:100vh;background:#0b101d;color:#e6edf3;overflow:hidden;}
        .sidebar{width:240px;background:#121829;border-right:1px solid #222b3f;padding:24px 0;display:flex;flex-direction:column;}
        .logo{font-size:24px;font-weight:700;color:#38bdf8;text-align:center;margin-bottom:40px;letter-spacing:1px;}
        .nav-item{padding:14px 28px;margin:4px 8px;border-radius:8px;cursor:pointer;transition:0.2s;display:flex;align-items:center;gap:12px;color:#a0aec0;}
        .nav-item.active,.nav-item:hover{background:#1e293b;color:#fff;}
        .main{flex:1;padding:32px;overflow-y:auto;}
        .page{display:none;}
        .page.active{display:block;}
        h2{font-size:22px;margin-bottom:24px;color:#f1f5f9;}
        .config-card{background:#121829;border:1px solid #222b3f;border-radius:12px;padding:20px;margin-bottom:24px;}
        .row{display:flex;gap:16px;margin-bottom:12px;flex-wrap:wrap;}
        .col2{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
        input,textarea,select{flex:1;min-width:260px;background:#0b101d;border:1px solid #222b3f;border-radius:8px;padding:12px 14px;color:#e6edf3;outline:none;}
        textarea{min-height:120px;resize:vertical;}
        button{background:#2563eb;color:#fff;border:0;border-radius:8px;padding:12px 24px;font-weight:600;cursor:pointer;transition:0.2s;}
        button:hover{background:#1d4ed8;}
        .result{margin-top:20px;background:#121829;border:1px solid #222b3f;border-radius:12px;padding:20px;white-space:pre-wrap;}
        .tip{color:#718096;font-size:13px;margin-top:6px;}
        .img-box{margin:12px 0;}
        .img-preview{max-width:100%;border-radius:8px;}
        .canvas-wrap{position:relative;margin:12px 0;}
        #maskCanvas{border-radius:8px;max-width:100%;}
    </style>
</head>
<body>
    <div class="sidebar">
        <div class="logo">LOOM42 AI</div>
        <div class="nav-item active" data-page="chat">💬 文案创作</div>
        <div class="nav-item" data-page="txt2img">🎨 文生图</div>
        <div class="nav-item" data-page="img2img">🖼️ 图生图/重绘</div>
        <div class="nav-item" data-page="tools">🧰 实用工具</div>
    </div>

    <div class="main">
        <!-- 文案 -->
        <div class="page active" id="chat">
            <h2>电商AI文案｜通义千问 / 豆包</h2>
            <div class="config-card">
                <div class="row"><select id="model"><option value="qwen">通义千问</option><option value="doubao">豆包大模型</option></select></div>
                <div class="row">
                    <input id="qwenKey" placeholder="通义千问 sk-xxx">
                    <input id="doubaoKey" placeholder="豆包 ark-xxx">
                </div>
                <div class="row"><input id="doubaoEp" placeholder="豆包 EndpointID ep-xxx"></div>
            </div>
            <textarea id="userPrompt" placeholder="家纺产品需求：四件套、毛毯、床垫，写标题/详情/小红书文案"></textarea>
            <div style="margin:16px 0;"><button onclick="runAI()">立即生成</button></div>
            <div class="result" id="resBox"></div>
        </div>

        <!-- 文生图 -->
        <div class="page" id="txt2img">
            <h2>Flux 文生图</h2>
            <div class="config-card">
                <div class="row"><input id="fluxKey" placeholder="SiliconFlow Flux Key"></div>
                <div class="col2">
                    <input id="wVal" value="1024" placeholder="宽度">
                    <input id="hVal" value="1024" placeholder="高度">
                </div>
            </div>
            <textarea id="t2iPrompt" placeholder="正向提示词\n反向提示词"></textarea>
            <div style="margin:16px 0;"><button onclick="txt2img()">开始生成</button></div>
            <div class="result" id="t2iRes"></div>
        </div>

        <!-- 图生图 + 局部重绘 -->
        <div class="page" id="img2img">
            <h2>图生图 / 局部重绘（LOOM42同款）</h2>
            <div class="config-card">
                <div class="row"><input id="fluxKey2" placeholder="Flux API Key"></div>
                <div class="col2">
                    <input id="imgStrength" value="0.7" placeholder="重绘强度 0.3~0.9">
                    <input type="file" id="imgUpload" accept="image/*">
                </div>
                <div class="tip">上传图片 → 涂抹蒙版 → 仅重绘涂抹区域</div>
            </div>

            <div class="canvas-wrap">
                <canvas id="maskCanvas"></canvas>
            </div>

            <textarea id="i2iPrompt" placeholder="修改需求：换花色、换面料、改风格、换背景"></textarea>
            <div style="margin:16px 0;display:flex;gap:10px;">
                <button onclick="img2imgRun()">整张图重绘</button>
                <button onclick="inpaintRun()">涂抹区域局部重绘</button>
                <button onclick="clearMask()">清除蒙版</button>
            </div>
            <div class="result" id="i2iRes"></div>
        </div>

        <!-- 工具 -->
        <div class="page" id="tools">
            <h2>高效工具</h2>
            <div class="config-card" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:12px;">
                <a href="https://www.remove.bg" target="_blank" style="color:#fff;padding:16px;background:#1e293b;border-radius:8px;text-decoration:none;text-align:center;">一键抠图</a>
                <a href="https://smallpdf.com" target="_blank" style="color:#fff;padding:16px;background:#1e293b;border-radius:8px;text-decoration:none;text-align:center;">PDF处理</a>
            </div>
        </div>
    </div>

    <script>
        // 【替换成你的 Cloudflare Workers 代理】
        const PROXY = "https://xxx.xxx.workers.dev/?url=";
        let originImg = null, maskCanvas, ctx;
        let isDrawing = false;

        // 侧边栏切换
        document.querySelectorAll('.nav-item').forEach(item=>{
            item.onclick = ()=>{
                document.querySelectorAll('.nav-item').forEach(i=>i.classList.remove('active'));
                document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
                item.classList.add('active');
                document.getElementById(item.dataset.page).classList.add('active');
            }
        });

        // ---------- 大模型文案 ----------
        async function qwen(key,msg){
            let api = "https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions";
            let res = await fetch(PROXY+encodeURIComponent(api),{
                method:"POST",
                headers:{"Content-Type":"application/json","Authorization":"Bearer "+key},
                body:JSON.stringify({
                    model:"qwen-turbo",
                    messages:[
                        {role:"system",content:"家纺电商资深文案，写标题、详情、小红书、短视频文案"},
                        {role:"user",content:msg}
                    ]
                })
            });
            let d = await res.json();
            return d.choices[0].message.content;
        }
        async function doubao(key,ep,msg){
            let api = "https://ark.cn-beijing.volces.com/api/v3/chat/completions";
            let res = await fetch(PROXY+encodeURIComponent(api),{
                method:"POST",
                headers:{"Content-Type":"application/json","Authorization":"Bearer "+key},
                body:JSON.stringify({
                    model:ep,
                    messages:[{role:"system",content:"家纺带货文案专家"},{role:"user",content:msg}]
                })
            });
            let d = await res.json();
            return d.choices[0].message.content;
        }
        async function runAI(){
            let m = document.getElementById('model').value;
            let p = document.getElementById('userPrompt').value.trim();
            let box = document.getElementById('resBox');
            box.innerText = "生成中...";
            try{
                let t;
                if(m==="qwen"){
                    let k = document.getElementById('qwenKey').value.trim();
                    t = await qwen(k,p);
                }else{
                    let k = document.getElementById('doubaoKey').value.trim();
                    let ep = document.getElementById('doubaoEp').value.trim();
                    t = await doubao(k,ep,p);
                }
                box.innerText = t;
            }catch(e){box.innerText = "错误："+e;}
        }

        // ---------- 文生图 ----------
        async function txt2img(){
            let key = document.getElementById('fluxKey').value.trim();
            let p = document.getElementById('t2iPrompt').value.trim();
            let w = document.getElementById('wVal').value;
            let h = document.getElementById('hVal').value;
            let box = document.getElementById('t2iRes');
            if(!key||!p){box.innerText="请填Key+提示词";return;}
            box.innerText="绘图中...";
            try{
                let api = "https://api.siliconflow.cn/v1/images/generations";
                let res = await fetch(PROXY+encodeURIComponent(api),{
                    method:"POST",
                    headers:{"Content-Type":"application/json","Authorization":"Bearer "+key},
                    body:JSON.stringify({model:"flux-schnell",prompt:p,image_size:`${w}x${h}`,num_images:1})
                });
                let j = await res.json();
                box.innerHTML = `<img class="img-preview" src="${j.images[0].url}">`;
            }catch(e){box.innerText="失败："+e;}
        }

        // ---------- 图生图 + 局部重绘 画布初始化 ----------
        window.onload = function(){
            maskCanvas = document.getElementById("maskCanvas");
            ctx = maskCanvas.getContext("2d");
            // 上传图片
            document.getElementById("imgUpload").addEventListener("change",function(e){
                let file = e.target.files[0];
                if(!file)return;
                let img = new Image();
                img.onload = function(){
                    originImg = img;
                    maskCanvas.width = Math.min(720,img.width);
                    maskCanvas.height = maskCanvas.width * img.height / img.width;
                    ctx.drawImage(img,0,0,maskCanvas.width,maskCanvas.height);
                }
                img.src = URL.createObjectURL(file);
            });
            // 画笔涂抹
            maskCanvas.addEventListener("mousedown",()=>isDrawing=true);
            maskCanvas.addEventListener("mouseup",()=>isDrawing=false);
            maskCanvas.addEventListener("mousemove",drawMask);
        }
        function drawMask(e){
            if(!isDrawing)return;
            let rect = maskCanvas.getBoundingClientRect();
            let x = e.clientX - rect.left;
            let y = e.clientY - rect.top;
            ctx.fillStyle = "rgba(0,0,0,0.85)";
            ctx.beginPath();
            ctx.arc(x,y,12,0,Math.PI*2);
            ctx.fill();
        }
        function clearMask(){
            if(!originImg)return;
            ctx.clearRect(0,0,maskCanvas.width,maskCanvas.height);
            ctx.drawImage(originImg,0,0,maskCanvas.width,maskCanvas.height);
        }

        // 整张图重绘
        async function img2imgRun(){
            alert("已集成图生图接口，我下一段直接给你补齐【图生图+局部重绘完整后端请求代码】，无缝对接SiliconFlow Flux");
        }
        // 局部重绘
        async function inpaintRun(){
            alert("蒙版画布已做好，下一段补齐重绘提交逻辑，直接涂抹就能局部改床品花色/背景");
        }
    </script>
</body>
</html>
