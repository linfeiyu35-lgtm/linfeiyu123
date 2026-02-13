<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />
  <title>我们和好吧</title>
  <style>
    :root{
      --bg1:#ffe6ef;
      --bg2:#e6f2ff;
      --card:#ffffffcc;
      --text:#1f2937;
      --accent:#ff4d6d;
      --accent2:#4f46e5;
    }
    *{box-sizing:border-box;font-family:system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Arial,"PingFang SC","Hiragino Sans GB","Microsoft YaHei",sans-serif;}
    body{
      margin:0; min-height:100vh; color:var(--text);
      background: radial-gradient(1200px 800px at 20% 10%, var(--bg1), transparent 60%),
                  radial-gradient(1200px 800px at 80% 90%, var(--bg2), transparent 60%),
                  #fff;
      overflow:hidden;
    }
    .wrap{
      min-height:100vh; display:flex; align-items:center; justify-content:center; padding:24px;
    }
    .card{
      width:min(520px, 92vw);
      background:var(--card);
      border:1px solid #ffffff80;
      border-radius:24px;
      box-shadow: 0 16px 40px rgba(0,0,0,.10);
      padding:22px 18px;
      backdrop-filter: blur(10px);
    }
    h1{
      margin:8px 0 6px; font-size:22px; letter-spacing:.5px;
      text-align:center;
    }
    p{
      margin:8px 0 14px; line-height:1.6; font-size:15px; text-align:center;
      opacity:.92;
    }
    .btnRow{
      display:flex; gap:12px; justify-content:center; align-items:center; flex-wrap:wrap;
      margin-top:10px;
    }
    button{
      border:0; outline:0; cursor:pointer;
      padding:14px 18px; border-radius:16px;
      font-size:16px; font-weight:700;
      box-shadow: 0 10px 22px rgba(0,0,0,.12);
      transition: transform .18s ease, filter .18s ease;
      user-select:none;
      -webkit-tap-highlight-color: transparent;
    }
    button:active{transform: scale(.98);}
    .yes{
      background: linear-gradient(135deg, var(--accent), #ff8fab);
      color:white;
      transform: scale(1);
    }
    .no{
      background: linear-gradient(135deg, #111827, #374151);
      color:white;
    }
    .sub{
      font-size:12px; opacity:.75; text-align:center; margin-top:10px;
    }

    /* 挽留遮罩 */
    .overlay{
      position:fixed; inset:0; display:none;
      background: rgba(0,0,0,.45);
      align-items:center; justify-content:center;
      padding:20px;
      z-index:50;
    }
    .overlay.show{display:flex;}
    .modal{
      width:min(460px, 92vw);
      background:#fff;
      border-radius:22px;
      padding:18px 16px;
      box-shadow: 0 18px 50px rgba(0,0,0,.25);
      text-align:center;
      animation: pop .22s ease;
    }
    @keyframes pop{
      from{transform: translateY(8px) scale(.98); opacity:.6;}
      to{transform: translateY(0) scale(1); opacity:1;}
    }
    .modal h2{margin:6px 0 8px; font-size:18px;}
    .modal p{margin:6px 0 12px; font-size:14px;}
    .tiny{
      display:block; margin-top:6px; font-size:12px; opacity:.6;
    }
    .shake{
      animation: shake .28s ease;
    }
    @keyframes shake{
      0%{transform: translateX(0);}
      25%{transform: translateX(-6px);}
      50%{transform: translateX(6px);}
      75%{transform: translateX(-4px);}
      100%{transform: translateX(0);}
    }

    /* 转盘页 */
    .wheelWrap{
      display:none;
      min-height:100vh;
      align-items:center;
      justify-content:center;
      padding:24px;
    }
    .wheelWrap.show{display:flex;}
    .wheelCard{
      width:min(560px, 94vw);
      background:var(--card);
      border:1px solid #ffffff80;
      border-radius:24px;
      box-shadow: 0 16px 40px rgba(0,0,0,.10);
      padding:18px 14px 16px;
      backdrop-filter: blur(10px);
      text-align:center;
    }
    canvas{
      width:min(360px, 78vw);
      height:auto;
      display:block;
      margin:14px auto 8px;
      background: transparent;
    }
    .pointer{
      width:0; height:0;
      border-left:14px solid transparent;
      border-right:14px solid transparent;
      border-bottom:26px solid #111827;
      margin: 0 auto -6px;
      filter: drop-shadow(0 6px 8px rgba(0,0,0,.25));
    }
    .spinBtn{
      background: linear-gradient(135deg, var(--accent2), #8b5cf6);
      color:#fff;
      margin-top:10px;
    }
    .note{
      font-size:12px; opacity:.75; margin-top:8px;
    }
    .result{
      margin-top:10px;
      font-weight:800;
      font-size:16px;
    }
  </style>
</head>
<body>

  <!-- 第1屏：选择和好 -->
  <div class="wrap" id="screen1">
    <div class="card">
      <h1>给你一个小小的请求 🥺</h1>
      <p>我想认真跟你和好。<br/>你愿意给我一次机会吗？</p>

      <div class="btnRow">
        <button class="yes" id="btnYes">和好</button>
        <button class="no" id="btnNo">不和好</button>
      </div>

      <div class="sub"></div>
    </div>
  </div>

  <!-- 挽留弹窗 -->
  <div class="overlay" id="overlay">
    <div class="modal" id="modal">
      <h2>再想想嘛…</h2>
      <p>你点“不和好”的时候，我心里咯噔一下🥲<br/>要不我们先抱抱，听我说完？</p>
      <div class="btnRow">
        <button class="yes" id="btnOverlayYes">好吧，和好</button>
        <button class="no" id="btnOverlayClose">我再考虑</button>
      </div>
      <span class="tiny">提示：每点一次“不和好”，「和好」都会长大一点点。</span>
    </div>
  </div>

  <!-- 第2屏：转盘 -->
  <div class="wheelWrap" id="screen2">
    <div class="wheelCard">
      <h1>和好成功 ✅</h1>
      <p>那我们来转个小转盘，决定你想要的“赔罪礼包”🎁</p>

      <div class="pointer"></div>
      <canvas id="wheel" width="600" height="600" aria-label="转盘"></canvas>

      <button class="spinBtn" id="btnSpin">开始旋转</button>
      <div class="note">（我承认：我在转盘里偷偷加了“彩蛋”😶‍🌫️）</div>
      <div class="result" id="result"></div>
    </div>
  </div>

<script>
(() => {
  const btnYes = document.getElementById('btnYes');
  const btnNo  = document.getElementById('btnNo');
  const overlay = document.getElementById('overlay');
  const modal = document.getElementById('modal');
  const btnOverlayYes = document.getElementById('btnOverlayYes');
  const btnOverlayClose = document.getElementById('btnOverlayClose');
  const screen1 = document.getElementById('screen1');
  const screen2 = document.getElementById('screen2');

  // “和好”按钮放大逻辑
  let yesScale = 1;
  function growYes(){
    yesScale = Math.min(yesScale + 0.12, 2.2);
    btnYes.style.transform = `scale(${yesScale})`;
    btnYes.style.filter = `brightness(${1 + (yesScale-1)*0.1})`;
  }

  // “不和好”点击：展示挽留弹窗 + 让“和好”变大
  btnNo.addEventListener('click', () => {
    growYes();
    overlay.classList.add('show');

    // 轻微震动（有的浏览器/微信可能不支持）
    if (navigator.vibrate) navigator.vibrate([20, 30, 20]);

    // 给“不和好”来个抖动
    btnNo.classList.remove('shake');
    void btnNo.offsetWidth;
    btnNo.classList.add('shake');
  });

  btnOverlayClose.addEventListener('click', () => {
    overlay.classList.remove('show');
  });

  btnOverlayYes.addEventListener('click', () => gotoWheel());
  btnYes.addEventListener('click', () => gotoWheel());

  function gotoWheel(){
    overlay.classList.remove('show');
    screen1.style.display = 'none';
    screen2.classList.add('show');
  }

  // 尝试拦截离开（只能“提示”，不能真正阻止退出）
  window.addEventListener('beforeunload', (e) => {
    // 只在第一页做挽留提示，避免转盘结束后还烦
    if (screen1.style.display !== 'none') {
      e.preventDefault();
      e.returnValue = '';
    }
  });

  /** 转盘实现 **/
  const canvas = document.getElementById('wheel');
  const ctx = canvas.getContext('2d');
  const resultEl = document.getElementById('result');
  const btnSpin = document.getElementById('btnSpin');

  const labels = ['看扑克牌魔术','打屁屁','100元现金红包','全都要']; // 从“正上方”开始顺时针
  const segCount = labels.length;
  const segAngle = (Math.PI * 2) / segCount;
  const startAngle = -Math.PI / 2; // 从正上方开始画
  const R = canvas.width/2;
  const center = {x:R, y:R};

  let rotation = 0;      // 当前旋转角（弧度）
  let spinning = false;

  function drawWheel(rot){
    ctx.clearRect(0,0,canvas.width,canvas.height);

    // 外圈阴影
    ctx.save();
    ctx.translate(center.x, center.y);
    ctx.beginPath();
    ctx.arc(0,0,R-8,0,Math.PI*2);
    ctx.shadowColor = 'rgba(0,0,0,.18)';
    ctx.shadowBlur = 18;
    ctx.fillStyle = 'rgba(255,255,255,.6)';
    ctx.fill();
    ctx.restore();

    // 扇区
    for(let i=0;i<segCount;i++){
      const a0 = startAngle + rot + i*segAngle;
      const a1 = a0 + segAngle;

      // 交替柔和色（不指定具体“品牌色”，但这里是固定配色；你要更随机也行）
      const colors = ['#ffd6e7','#dbeafe','#ffe4c7','#dcfce7'];
      ctx.beginPath();
      ctx.moveTo(center.x, center.y);
      ctx.arc(center.x, center.y, R-22, a0, a1);
      ctx.closePath();
      ctx.fillStyle = colors[i % colors.length];
      ctx.fill();

      // 分割线
      ctx.strokeStyle = 'rgba(17,24,39,.15)';
      ctx.lineWidth = 3;
      ctx.stroke();

      // 文本
      const mid = (a0 + a1)/2;
      ctx.save();
      ctx.translate(center.x, center.y);
      ctx.rotate(mid);
      ctx.textAlign = 'right';
      ctx.fillStyle = '#111827';
      ctx.font = 'bold 26px system-ui, -apple-system, "PingFang SC", "Microsoft YaHei"';
      ctx.fillText(labels[i], R-70, 10);
      ctx.restore();
    }

    // 中心圆
    ctx.beginPath();
    ctx.arc(center.x, center.y, 76, 0, Math.PI*2);
    ctx.fillStyle = 'rgba(255,255,255,.92)';
    ctx.fill();
    ctx.strokeStyle = 'rgba(17,24,39,.12)';
    ctx.lineWidth = 4;
    ctx.stroke();

    ctx.fillStyle = '#111827';
    ctx.font = '900 30px system-ui, -apple-system, "PingFang SC", "Microsoft YaHei"';
    ctx.textAlign = 'center';
    ctx.fillText('转！', center.x, center.y + 10);
  }

  drawWheel(rotation);

  function easeOutCubic(t){ return 1 - Math.pow(1-t, 3); }

  function spinToAllYouWant(){
    if (spinning) return;
    spinning = true;
    resultEl.textContent = '';

    // 固定落到“全都要”
    const targetIndex = labels.indexOf('全都要');

    // 让“指针在正上方”，所以希望目标扇区中心最终处于正上方（-90°）
    // 我们画扇区从 startAngle 开始，rot 会影响整个轮盘。
    // 目标：目标扇区中心角 = startAngle + rot + (i+0.5)*segAngle  == -PI/2
    // => rot = -PI/2 - startAngle - (i+0.5)*segAngle
    const desiredRot = (-Math.PI/2) - startAngle - (targetIndex + 0.5)*segAngle;

    // 多转几圈更爽
    const extraTurns = 6; // 圈数
    const from = rotation;
    // 归一化：从当前角度开始，转到 (extraTurns*2PI + desiredRot) 附近
    // 为了避免突然倒转，确保目标比当前大
    let to = extraTurns * Math.PI*2 + desiredRot;

    // 把 to 调到 >= from
    while (to < from) to += Math.PI*2;

    const duration = 4200; // ms
    const t0 = performance.now();

    function tick(now){
      const t = Math.min(1, (now - t0)/duration);
      const k = easeOutCubic(t);
      rotation = from + (to - from)*k;
      drawWheel(rotation);

      if (t < 1){
        requestAnimationFrame(tick);
      } else {
        spinning = false;
        // 最终把 rotation 稍微归一化一下
        rotation = rotation % (Math.PI*2);
        drawWheel(rotation);

        resultEl.textContent = '🎉 结果：全都要（我认真的）';
        if (navigator.vibrate) navigator.vibrate([40, 40, 80]);
      }
    }
    requestAnimationFrame(tick);
  }

  btnSpin.addEventListener('click', spinToAllYouWant);
})();
</script>
</body>
</html>
