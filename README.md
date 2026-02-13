<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />
  <title>我想认真把你放在心上</title>
  <style>
    :root{
      --bgA:#fff1f5;
      --bgB:#eef2ff;
      --card:#ffffffcc;
      --text:#111827;
      --muted:#6b7280;
      --accent:#ff4d6d;
      --accent2:#4f46e5;
      --ok:#10b981;
      --shadow: 0 18px 50px rgba(0,0,0,.12);
      --radius: 22px;
    }
    *{box-sizing:border-box;font-family:system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Arial,"PingFang SC","Hiragino Sans GB","Microsoft YaHei",sans-serif;}
    body{
      margin:0; min-height:100vh; color:var(--text);
      background: radial-gradient(1200px 800px at 20% 10%, var(--bgA), transparent 60%),
                  radial-gradient(1200px 800px at 80% 90%, var(--bgB), transparent 60%),
                  #fff;
      overflow-x:hidden;
    }
    .wrap{min-height:100vh; display:flex; align-items:center; justify-content:center; padding:22px;}
    .card{
      width:min(720px, 94vw);
      background:var(--card);
      border:1px solid #ffffff80;
      border-radius:var(--radius);
      box-shadow: var(--shadow);
      padding:18px 16px;
      backdrop-filter: blur(10px);
    }
    h1{margin:10px 0 6px; font-size:22px; text-align:center; letter-spacing:.3px;}
    p{margin:8px 0 12px; line-height:1.75; font-size:15px; text-align:center; color:var(--text);}
    .muted{color:var(--muted); font-size:13px;}
    .section{
      margin-top:12px;
      background: rgba(255,255,255,.75);
      border: 1px solid rgba(17,24,39,.06);
      border-radius: 18px;
      padding: 12px 12px 10px;
    }
    .section h2{margin:4px 0 8px; font-size:15px; text-align:left;}
    .btnRow{
      display:flex; gap:10px; justify-content:center; align-items:center; flex-wrap:wrap;
      margin-top:12px;
    }
    button{
      border:0; outline:0; cursor:pointer;
      padding:12px 16px; border-radius:16px;
      font-size:15px; font-weight:800;
      box-shadow: 0 10px 22px rgba(0,0,0,.12);
      transition: transform .16s ease, filter .16s ease, opacity .16s ease;
      user-select:none;
      -webkit-tap-highlight-color: transparent;
    }
    button:active{transform: scale(.98);}
    .primary{background: linear-gradient(135deg, var(--accent), #ff8fab); color:white;}
    .secondary{background: linear-gradient(135deg, #111827, #374151); color:white;}
    .soft{
      background: linear-gradient(135deg, #ffffff, #f3f4f6);
      color:#111827;
      border: 1px solid rgba(17,24,39,.10);
      box-shadow: 0 10px 22px rgba(0,0,0,.08);
    }

    .chipRow{display:flex; flex-wrap:wrap; gap:10px; justify-content:center; margin-top:10px;}
    .chip{
      border:1px solid rgba(17,24,39,.10);
      background: rgba(255,255,255,.85);
      color: var(--text);
      padding: 10px 12px;
      border-radius: 999px;
      font-size: 14px;
      cursor:pointer;
      transition: transform .12s ease, background .12s ease, border-color .12s ease;
      user-select:none;
      -webkit-tap-highlight-color: transparent;
      font-weight:800;
    }
    .chip:active{transform:scale(.98);}
    .chip.selected{
      border-color: rgba(255,77,109,.35);
      background: rgba(255,77,109,.12);
    }

    .grid{
      display:grid;
      grid-template-columns: 1fr;
      gap:10px;
    }
    @media (min-width:560px){
      .grid{grid-template-columns: 1fr 1fr;}
    }

    .page{display:none;}
    .page.show{display:block;}
    .fadeIn{animation:fade .22s ease;}
    @keyframes fade{from{opacity:.6; transform:translateY(6px);} to{opacity:1; transform:translateY(0);} }

    .quote{
      background: rgba(17,24,39,.04);
      border: 1px solid rgba(17,24,39,.08);
      border-radius: 16px;
      padding: 12px;
      text-align:left;
      white-space:pre-wrap;
      font-size:14px;
      line-height:1.7;
    }
    .ok{color:var(--ok); font-weight:900;}

    .toast{
      position:fixed; left:50%; bottom:18px; transform:translateX(-50%);
      background: rgba(17,24,39,.92);
      color:#fff;
      padding:10px 12px;
      border-radius:999px;
      font-size:13px;
      display:none;
      z-index:999;
    }

    /* Wheel */
    .pointer{
      width:0; height:0;
      border-left:14px solid transparent;
      border-right:14px solid transparent;
      border-bottom:26px solid #111827;
      margin: 0 auto -6px;
      filter: drop-shadow(0 6px 8px rgba(0,0,0,.25));
    }
    canvas{
      width:min(360px, 78vw);
      height:auto;
      display:block;
      margin:14px auto 8px;
      background: transparent;
    }
    .result{
      margin-top:10px;
      font-weight:900;
      font-size:16px;
      text-align:center;
    }
    .confetti{
      position:fixed; inset:0; pointer-events:none; overflow:hidden; display:none;
      z-index:99;
    }
    .confetti.show{display:block;}
    .confetti i{
      position:absolute; top:-12px; width:10px; height:14px; border-radius:2px;
      opacity:.9; animation: fall 1200ms linear forwards;
    }
    @keyframes fall{
      to{ transform: translateY(110vh) rotate(320deg); opacity:1; }
    }
  </style>
</head>
<body>

<div class="confetti" id="confetti"></div>
<div class="toast" id="toast">已复制</div>

<div class="wrap">
  <div class="card">

    <!-- P1 -->
    <div class="page show fadeIn" id="p1">
      <h1>我想认真把你放在心上</h1>
      <p class="muted">你愿意点开这个页面，我已经很感谢了。</p>

      <div class="section">
        <h2>我先把我做错的说清楚</h2>
        <div class="quote">
视频的时候，我没有认真和你聊天。
我一边跟你说话，一边做自己的事。
这会让你感觉：你不重要，我只想快点要“结果”。

这些感受都很合理。
对不起，是我没有把注意力和尊重给到你。
        </div>
        <p class="muted" style="text-align:left;margin-top:10px;">
          我不想用“哄一下就算了”的方式跳过过程。
          我想把那个<strong>认真陪你</strong>的过程补回来。
        </p>
      </div>

      <div class="section">
        <h2>你现在更接近哪种感受？（选一个就好）</h2>
        <div class="chipRow" id="moods">
          <div class="chip" data-key="talk">我想听你解释</div>
          <div class="chip" data-key="angry">我还在生气</div>
          <div class="chip" data-key="space">我先不想说</div>
        </div>
      </div>

      <div class="btnRow">
        <button class="primary" id="go2" disabled style="opacity:.6;filter:grayscale(1);">继续</button>
      </div>

      <p class="muted" style="margin-top:10px;">
        你随时可以关掉页面。你舒服最重要。
      </p>
    </div>

    <!-- P2 -->
    <div class="page" id="p2">
      <h1>我会这样对待你的情绪</h1>
      <p class="muted">不辩解、不抢结论、不催你原谅。</p>

      <div class="section">
        <h2>我想对你说</h2>
        <div class="quote" id="replyBox"></div>
      </div>

      <div class="section">
        <h2>你希望我怎么补回来？（你来决定节奏）</h2>
        <div class="grid" id="compGrid">
          <button class="soft" data-comp="A">A：现在/今晚专心视频 20 分钟（我只听你说）</button>
          <button class="soft" data-comp="B">B：你讲我听 10 分钟 + 我复述确认 2 分钟</button>
          <button class="soft" data-comp="C">C：你先不想聊也没关系，我先安静，等你愿意再说</button>
          <button class="soft" data-comp="D">D：你定时间，你舒服最重要</button>
        </div>
        <p class="muted" style="text-align:left;margin-top:10px;">
          你选哪个都行。我会照做。
        </p>
      </div>

      <div class="btnRow">
        <button class="secondary" id="back1">返回</button>
        <button class="primary" id="go3" disabled style="opacity:.6;filter:grayscale(1);">下一步</button>
      </div>
    </div>

    <!-- P3 -->
    <div class="page" id="p3">
      <h1>谢谢你给我一个“过程”</h1>
      <p class="muted">你不需要立刻原谅我，但我会把认真做出来。</p>

      <div class="section">
        <h2>你选的方式</h2>
        <div class="quote" id="chosenBox"></div>
        <p class="muted" style="text-align:left;margin-top:10px;">
          如果你愿意，你可以直接回我一句：<span class="ok">“就按这个来”</span> 或者 <span class="ok">“我再想想”</span>。
        </p>
      </div>

      <!-- 新增：反馈给我 -->
      <div class="section" id="feedbackSection" style="display:none;">
        <h2>把你的选择发给我</h2>
        <p class="muted" style="text-align:left;margin-top:-2px;">
          这段不会自动上传任何信息；你点“复制/分享”再发给我就可以啦。
        </p>
        <div class="quote" id="feedbackBox"></div>
        <div class="btnRow">
          <button class="primary" id="copyFeedback">复制</button>
          <button class="soft" id="shareFeedback">分享</button>
        </div>
      </div>

      <div class="section">
        <h2>（可选）开心一下的小转盘</h2>
        <p class="muted" style="text-align:left;margin-top:-2px;">
          你想玩就玩一下；不想玩就点“你定”。
        </p>

        <div class="pointer"></div>
        <canvas id="wheel" width="600" height="600" aria-label="转盘"></canvas>

        <div class="btnRow">
          <button class="primary" id="spinBtn">随机转一下</button>
          <button class="soft" id="youDecideBtn">不转：你来定</button>
        </div>

        <div class="result" id="wheelResult"></div>
      </div>

      <div class="btnRow">
        <button class="secondary" id="back2">返回</button>
        <button class="primary" id="restart">再看一遍</button>
      </div>

      <p class="muted" style="margin-top:10px;">
        你值得被认真对待。真的。
      </p>
    </div>

  </div>
</div>

<script>
(() => {
  const $ = (id) => document.getElementById(id);

  // Pages
  const p1 = $("p1"), p2 = $("p2"), p3 = $("p3");
  function show(page){
    [p1,p2,p3].forEach(x => x.classList.remove("show","fadeIn"));
    page.classList.add("show","fadeIn");
    window.scrollTo({top:0, behavior:"smooth"});
  }

  // Toast
  const toast = $("toast");
  function popToast(text="已复制"){
    toast.textContent = text;
    toast.style.display = "block";
    clearTimeout(popToast._t);
    popToast._t = setTimeout(()=> toast.style.display="none", 1200);
  }
  async function copyText(text){
    try{
      await navigator.clipboard.writeText(text);
      popToast("已复制");
    }catch(e){
      const ta = document.createElement("textarea");
      ta.value = text;
      document.body.appendChild(ta);
      ta.select();
      document.execCommand("copy");
      ta.remove();
      popToast("已复制");
    }
  }

  // Confetti
  const confetti = $("confetti");
  function popConfetti(){
    confetti.innerHTML = "";
    confetti.classList.add("show");
    const colors = ["#ff4d6d","#4f46e5","#10b981","#f59e0b","#22c55e","#0ea5e9"];
    const n = 36;
    for(let i=0;i<n;i++){
      const el = document.createElement("i");
      el.style.left = Math.random()*100 + "vw";
      el.style.background = colors[Math.floor(Math.random()*colors.length)];
      el.style.transform = `translateY(0) rotate(${Math.random()*120}deg)`;
      el.style.animationDuration = (900 + Math.random()*600) + "ms";
      el.style.opacity = (0.7 + Math.random()*0.3).toFixed(2);
      confetti.appendChild(el);
      el.style.animationDelay = (Math.random()*120) + "ms";
    }
    setTimeout(()=> confetti.classList.remove("show"), 1400);
  }

  // ===== 记录她的选择（用于反馈）=====
  let moodKey = null;
  let compKey = null;
  let wheelChoice = ""; // 她抽到/选择的转盘结果
  function moodText(key){
    switch(key){
      case "talk": return "我想听你解释";
      case "angry": return "我还在生气";
      case "space": return "我先不想说";
      default: return "（未选择）";
    }
  }
  function compText(key){
    switch(key){
      // 你文件里这里已经改了 A 的含义，我保留它
      case "A": return "A：现在/明天视频唱一首歌，并认真反省道歉";
      case "B": return "B：你讲我听 10 分钟 + 我复述确认 2 分钟";
      case "C": return "C：你先不想聊也没关系，我先安静，等你愿意再说";
      case "D": return "D：你定时间，你舒服最重要";
      default: return "";
    }
  }
  function buildFeedback(){
    const when = new Date();
    const ts = `${when.getFullYear()}-${String(when.getMonth()+1).padStart(2,'0')}-${String(when.getDate()).padStart(2,'0')} `
             + `${String(when.getHours()).padStart(2,'0')}:${String(when.getMinutes()).padStart(2,'0')}`;
    const lines = [
      "我看完啦（来自页面的小反馈）",
      `- 我现在的感受：${moodText(moodKey)}`,
      `- 我希望你这样补回来：${compText(compKey) || "（未选择）"}`,
      `- 转盘结果：${wheelChoice || "（没转 / 还没选）"}`,
      `- 时间：${ts}`
    ];
    return lines.join("\n");
  }
  function refreshFeedbackUI(){
    if(!moodKey || !compKey) return;
    $("feedbackSection").style.display = "block";
    $("feedbackBox").textContent = buildFeedback();
  }

  // ===== P1 选择心情 =====
  const moodChips = Array.from(document.querySelectorAll("#moods .chip"));
  const go2 = $("go2");
  moodChips.forEach(chip => {
    chip.addEventListener("click", () => {
      moodChips.forEach(c=>c.classList.remove("selected"));
      chip.classList.add("selected");
      moodKey = chip.dataset.key;
      go2.disabled = false;
      go2.style.filter = "none";
      go2.style.opacity = "1";
    });
  });

  function buildReply(){
    const base =
`我听见了。
我不想解释为自己开脱。

我在视频的时候分心做别的，这就是敷衍。
你会生气、会难过，都很正常。
对不起。`;

    if(moodKey === "talk"){
      return base + `

如果你愿意说，我想先听你把话说完。
你说完之后，我会复述确认：我有没有真正听懂你。`;
    }
    if(moodKey === "angry"){
      return base + `

你现在还在生气完全合理。
我不求你马上原谅我，我只想先把“认真”做到：把你放在第一位。`;
    }
    return base + `

如果你现在不想说也没关系。
我不会逼你，我会等你愿意的时候再聊。`;
  }

  go2.addEventListener("click", () => {
    $("replyBox").textContent = buildReply().trim();
    show(p2);
  });

  // back to p1
  $("back1").addEventListener("click", () => show(p1));

  // ===== P2 选择补偿方式 =====
  const compButtons = Array.from(document.querySelectorAll("[data-comp]"));
  const go3 = $("go3");

  compButtons.forEach(btn => {
    btn.addEventListener("click", () => {
      compButtons.forEach(b => { b.style.border="none"; b.style.filter="none"; });
      btn.style.border = "2px solid rgba(255,77,109,.35)";
      btn.style.filter = "brightness(1.03)";
      compKey = btn.dataset.comp;

      go3.disabled = false;
      go3.style.filter = "none";
      go3.style.opacity = "1";
    });
  });

  go3.addEventListener("click", () => {
    $("chosenBox").textContent =
`我会照你选的来：\n${compText(compKey)}\n\n你不用急着原谅我。\n我先把“认真”还给你。`;
    popConfetti();
    show(p3);
    refreshFeedbackUI();
  });

  $("back2").addEventListener("click", () => show(p2));

  $("restart").addEventListener("click", () => {
    // reset
    moodKey = null;
    compKey = null;
    wheelChoice = "";
    moodChips.forEach(c=>c.classList.remove("selected"));
    go2.disabled = true; go2.style.filter="grayscale(1)"; go2.style.opacity=".6";
    go3.disabled = true; go3.style.filter="grayscale(1)"; go3.style.opacity=".6";
    compButtons.forEach(b => { b.style.border="none"; b.style.filter="none"; });
    $("wheelResult").textContent = "";
    $("feedbackSection").style.display = "none";
    show(p1);
  });

  // ===== 反馈：复制 & 分享 =====
  $("copyFeedback").addEventListener("click", () => copyText(buildFeedback()));
  $("shareFeedback").addEventListener("click", async () => {
    const text = buildFeedback();
    if(navigator.share){
      try{
        await navigator.share({ title:"页面反馈", text });
      }catch(e){
        // 用户取消分享也算正常
      }
    }else{
      await copyText(text);
      popToast("已复制（此设备不支持分享）");
    }
  });

  /** Wheel (optional, random) **/
  const canvas = $("wheel");
  const ctx = canvas.getContext("2d");

  // 你文件里这组转盘文案我保留（提示：有些可能会踩雷，自己确认下）
  const labels = ["30个俯卧撑","挠痒痒30分钟（位置自选）","一次全身搓澡按摩","你来定（我听你的）"];
  const segCount = labels.length;
  const segAngle = (Math.PI*2)/segCount;
  const startAngle = -Math.PI/2;
  const R = canvas.width/2;
  const center = {x:R,y:R};

  let rotation = 0;
  let spinning = false;

  function drawWheel(rot){
    ctx.clearRect(0,0,canvas.width,canvas.height);

    ctx.save();
    ctx.translate(center.x, center.y);
    ctx.beginPath();
    ctx.arc(0,0,R-8,0,Math.PI*2);
    ctx.shadowColor = "rgba(0,0,0,.18)";
    ctx.shadowBlur = 18;
    ctx.fillStyle = "rgba(255,255,255,.6)";
    ctx.fill();
    ctx.restore();

    const colors = ["#ffd6e7","#dbeafe","#ffe4c7","#dcfce7"];
    for(let i=0;i<segCount;i++){
      const a0 = startAngle + rot + i*segAngle;
      const a1 = a0 + segAngle;

      ctx.beginPath();
      ctx.moveTo(center.x, center.y);
      ctx.arc(center.x, center.y, R-22, a0, a1);
      ctx.closePath();
      ctx.fillStyle = colors[i%colors.length];
      ctx.fill();

      ctx.strokeStyle = "rgba(17,24,39,.15)";
      ctx.lineWidth = 3;
      ctx.stroke();

      const mid = (a0+a1)/2;
      ctx.save();
      ctx.translate(center.x, center.y);
      ctx.rotate(mid);
      ctx.textAlign = "right";
      ctx.fillStyle = "#111827";
      ctx.font = 'bold 26px system-ui, -apple-system, "PingFang SC", "Microsoft YaHei"';
      ctx.fillText(labels[i], R-70, 10);
      ctx.restore();
    }

    ctx.beginPath();
    ctx.arc(center.x, center.y, 76, 0, Math.PI*2);
    ctx.fillStyle = "rgba(255,255,255,.92)";
    ctx.fill();
    ctx.strokeStyle = "rgba(17,24,39,.12)";
    ctx.lineWidth = 4;
    ctx.stroke();

    ctx.fillStyle = "#111827";
    ctx.font = '900 26px system-ui, -apple-system, "PingFang SC", "Microsoft YaHei"';
    ctx.textAlign = "center";
    ctx.fillText("转一下", center.x, center.y + 10);
  }

  function easeOutCubic(t){ return 1 - Math.pow(1-t, 3); }

  function indexFromRotation(rot){
    const topAngle = (-Math.PI/2);
    let bestI = 0, bestD = Infinity;
    for(let i=0;i<segCount;i++){
      const centerAng = startAngle + rot + (i+0.5)*segAngle;
      let d = Math.atan2(Math.sin(centerAng-topAngle), Math.cos(centerAng-topAngle));
      d = Math.abs(d);
      if(d < bestD){ bestD = d; bestI = i; }
    }
    return bestI;
  }

  function spinRandom(){
    if(spinning) return;
    spinning = true;
    $("wheelResult").textContent = "";

    const targetIndex = Math.floor(Math.random()*segCount);
    const desiredRot = (-Math.PI/2) - startAngle - (targetIndex + 0.5)*segAngle;

    const extraTurns = 5 + Math.floor(Math.random()*3);
    const from = rotation;
    let to = extraTurns * Math.PI*2 + desiredRot;
    while(to < from) to += Math.PI*2;

    const duration = 3400;
    const t0 = performance.now();

    function tick(now){
      const t = Math.min(1, (now - t0)/duration);
      const k = easeOutCubic(t);
      rotation = from + (to - from)*k;
      drawWheel(rotation);

      if(t < 1){
        requestAnimationFrame(tick);
      }else{
        spinning = false;
        rotation = rotation % (Math.PI*2);
        drawWheel(rotation);

        const idx = indexFromRotation(rotation);
        wheelChoice = labels[idx];
        $("wheelResult").innerHTML = `🎉 抽到：<span class="ok">${wheelChoice}</span>`;
        popConfetti();
        if (navigator.vibrate) navigator.vibrate([30, 30, 60]);
        refreshFeedbackUI();
        $("feedbackBox").textContent = buildFeedback();
      }
    }
    requestAnimationFrame(tick);
  }

  $("spinBtn").addEventListener("click", spinRandom);

  $("youDecideBtn").addEventListener("click", () => {
    wheelChoice = "你来定（我听你的）";
    $("wheelResult").innerHTML = `✅ 好：<span class="ok">${wheelChoice}</span>`;
    popConfetti();
    refreshFeedbackUI();
    $("feedbackBox").textContent = buildFeedback();
  });

  drawWheel(rotation);
})();
</script>

</body>
</html>
