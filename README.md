<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />
  <title>我欠你一次认真的聊天</title>
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
      width:min(680px, 94vw);
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
      transition: transform .16s ease, filter .16s ease;
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
    textarea{
      width:100%;
      min-height:92px;
      resize:none;
      border-radius:16px;
      border: 1px solid rgba(17,24,39,.12);
      padding:12px 12px;
      font-size:14px;
      line-height:1.6;
      background: rgba(255,255,255,.9);
      outline:none;
    }
    textarea:focus{border-color: rgba(79,70,229,.35); box-shadow: 0 0 0 4px rgba(79,70,229,.12);}
    .page{display:none;}
    .page.show{display:block;}
    .fadeIn{animation:fade .22s ease;}
    @keyframes fade{from{opacity:.6; transform:translateY(6px);} to{opacity:1; transform:translateY(0);} }

    .copyBox{
      background: rgba(17,24,39,.04);
      border: 1px solid rgba(17,24,39,.08);
      border-radius: 16px;
      padding: 12px;
      text-align:left;
      white-space:pre-wrap;
      font-size:14px;
      line-height:1.7;
    }
    .toast{
      position:fixed; left:50%; bottom:18px; transform:translateX(-50%);
      background: rgba(17,24,39,.92);
      color:#fff;
      padding:10px 12px;
      border-radius:999px;
      font-size:13px;
      display:none;
      z-index:99;
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
    .good{color: var(--ok);}
    .smallLink{
      display:inline-block;
      margin-top:6px;
      font-size:13px;
      color: rgba(79,70,229,.95);
      text-decoration: underline;
      cursor:pointer;
    }
  </style>
</head>
<body>

<div class="wrap">
  <div class="card">

    <!-- P1：情绪选择 + 先承认 -->
    <div class="page show fadeIn" id="p1">
      <h1>我欠你一次认真的聊天</h1>
      <p class="muted">我不会逼你“马上和好”。我只想把话说清楚，也把选择权交给你。</p>

      <div class="section">
        <h2>我先把错误说清楚</h2>
        <p style="text-align:left;margin:6px 0 0;">
          视频的时候我没有认真和你聊天，一边跟你说话一边做自己的事。<br>
          这会让你觉得你不重要、我只想要结果——你生气是合理的。<br>
          <b>对不起，是我没有把注意力给到你。</b>
        </p>
      </div>

      <div class="section">
        <h2>你现在更接近哪种感受？（选一个就好）</h2>
        <div class="chipRow" id="moods">
          <div class="chip" data-key="talk">我想听你解释</div>
          <div class="chip" data-key="angry">我还在生气</div>
          <div class="chip" data-key="space">我先不想说</div>
        </div>
        <p class="muted" style="text-align:left;margin-top:10px;">
          你选哪个都可以。我只想用<b>认真</b>把这件事补回来。
        </p>
      </div>

      <div class="btnRow">
        <button class="primary" id="toP2" disabled style="filter:grayscale(1);opacity:.6;">继续</button>
        <button class="soft" id="previewMsg">先看我想发给你的话</button>
      </div>

      <p class="muted" style="margin-top:10px;">
        你随时可以退出页面。你舒服最重要。
      </p>
    </div>

    <!-- P2：根据她选的情绪生成回应 + 让她决定下一步 -->
    <div class="page" id="p2">
      <h1>我想这样跟你说</h1>
      <p class="muted">这是我最想表达的内容（你也可以直接复制发给她）。</p>

      <div class="section">
        <h2>这段话可以直接复制</h2>
        <div class="copyBox" id="msgBox"></div>
        <div class="btnRow">
          <button class="primary" id="copyBtn">复制这段话</button>
          <button class="soft" id="editBtn">我想再补一句</button>
        </div>
        <div id="editArea" style="display:none;margin-top:10px;">
          <textarea id="extraLine" placeholder="补一句你自己的话（比如她的昵称、你们的细节、你最在意她哪里难过）"></textarea>
          <div class="btnRow">
            <button class="primary" id="applyEdit">加入到上面那段</button>
            <button class="soft" id="cancelEdit">算了</button>
          </div>
        </div>
      </div>

      <div class="section">
        <h2>你愿意让我怎么补回来？（你来选节奏）</h2>
        <div class="grid">
          <button class="soft" data-comp="A">A：现在/今晚专心视频 20 分钟（我只听你说）</button>
          <button class="soft" data-comp="B">B：你讲我听 10 分钟 + 我复述确认 2 分钟</button>
          <button class="soft" data-comp="C">C：你先不想聊，我先安静，等你愿意再说</button>
          <button class="soft" data-comp="D">D：你定时间，我按你方便的来</button>
        </div>
        <p class="muted" style="text-align:left;margin-top:10px;">
          选完后我会给你一段“下一步确认话术”，让你发给她更自然。
        </p>
      </div>

      <div class="btnRow">
        <button class="secondary" id="backP1">返回</button>
        <button class="primary" id="toP3" disabled style="filter:grayscale(1);opacity:.6;">生成下一步</button>
      </div>
    </div>

    <!-- P3：补偿确认 + 可选小转盘（随机 or 她决定） -->
    <div class="page" id="p3">
      <h1>把过程补回来</h1>
      <p class="muted">不是为了“立刻和好”，而是让你感到：我在认真对待你。</p>

      <div class="section">
        <h2>你选的方式</h2>
        <div class="copyBox" id="chosenComp"></div>
        <div style="margin-top:10px;">
          <textarea id="timeNote" placeholder="（可选）你可以写：你方便的时间/我现在就可以/我会把手机放下只看你……"></textarea>
        </div>
      </div>

      <div class="section">
        <h2>你可以发给她的“下一步确认话术”</h2>
        <div class="copyBox" id="nextMsg"></div>
        <div class="btnRow">
          <button class="primary" id="copyNext">复制这段话</button>
          <button class="soft" id="updateNext">把上面的时间/补充加入</button>
        </div>
      </div>

      <div class="section">
        <h2>（可选）小小的“开心一下”</h2>
        <p class="muted" style="text-align:left;margin-top:-2px;">
          如果她愿意玩一下，就转个小转盘；如果不想玩，也完全没关系。
        </p>

        <div class="pointer"></div>
        <canvas id="wheel" width="600" height="600" aria-label="转盘"></canvas>

        <div class="btnRow">
          <button class="primary" id="spinBtn">随机转一下</button>
          <button class="soft" id="youDecideBtn">不转：全都听你的</button>
        </div>

        <div class="result" id="wheelResult"></div>
      </div>

      <div class="btnRow">
        <button class="secondary" id="backP2">返回</button>
        <button class="primary" id="restart">重新开始</button>
      </div>

      <p class="muted" style="margin-top:10px;">
        提醒：如果她还在气头上，先别急着求结果。先把“认真”做出来。
      </p>
    </div>

  </div>
</div>

<div class="toast" id="toast">已复制</div>

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

  // Copy helper
  async function copyText(text){
    try{
      await navigator.clipboard.writeText(text);
      popToast("已复制");
    }catch(e){
      // Fallback
      const ta = document.createElement("textarea");
      ta.value = text;
      document.body.appendChild(ta);
      ta.select();
      document.execCommand("copy");
      ta.remove();
      popToast("已复制");
    }
  }

  // Mood selection
  let moodKey = null;
  const moodChips = Array.from(document.querySelectorAll("#moods .chip"));
  const toP2 = $("toP2");

  moodChips.forEach(chip => {
    chip.addEventListener("click", () => {
      moodChips.forEach(c=>c.classList.remove("selected"));
      chip.classList.add("selected");
      moodKey = chip.dataset.key;

      toP2.disabled = false;
      toP2.style.filter = "none";
      toP2.style.opacity = "1";
    });
  });

  // Base apology message templates
  function buildMsg(){
    const base =
`我刚刚认真想了下，你生气是因为我在视频的时候没有认真跟你聊天：一边跟你说话一边做自己的事。
这会让你觉得你不重要、我只想快点拿到“和好结果”。这不是你的问题，是我不够尊重你的感受。对不起。

我不想用搞笑或套路跳过过程。我想把“认真陪你”的过程补回来。`;

    if(moodKey === "talk"){
      return base + `
如果你愿意，你说什么我都先听完，我不打断、不辩解。我想先把你感受弄明白。`;
    }
    if(moodKey === "angry"){
      return base + `
你现在还在生气完全合理。我先不求你马上原谅我，只想先把我该做的做到：把注意力和尊重补给你。`;
    }
    // space
    return base + `
如果你现在不想说也没关系。我不会逼你，我会等你愿意的时候再聊。`;
  }

  // Preview button on P1
  $("previewMsg").addEventListener("click", async () => {
    if(!moodKey){
      popToast("先选一个感受");
      return;
    }
    await copyText(buildMsg().trim());
  });

  // Go P2
  $("toP2").addEventListener("click", () => {
    $("msgBox").textContent = buildMsg().trim();
    show(p2);
  });

  // Edit message
  $("copyBtn").addEventListener("click", () => copyText($("msgBox").textContent));
  $("editBtn").addEventListener("click", () => {
    $("editArea").style.display = "block";
  });
  $("cancelEdit").addEventListener("click", () => {
    $("editArea").style.display = "none";
    $("extraLine").value = "";
  });
  $("applyEdit").addEventListener("click", () => {
    const extra = $("extraLine").value.trim();
    if(!extra){
      popToast("先写一句再加入");
      return;
    }
    $("msgBox").textContent = ($("msgBox").textContent.trim() + "\n\n" + extra).trim();
    $("editArea").style.display = "none";
    $("extraLine").value = "";
    popToast("已加入");
  });

  // Back to P1
  $("backP1").addEventListener("click", () => show(p1));

  // Compensation selection
  let compKey = null;
  const compButtons = Array.from(document.querySelectorAll("[data-comp]"));
  const toP3 = $("toP3");

  function compText(key){
    switch(key){
      case "A": return "A：现在/今晚专心视频 20 分钟（我把手机放一边，只听你说）";
      case "B": return "B：你讲我听 10 分钟 + 我复述确认 2 分钟（确保我真的懂你）";
      case "C": return "C：你先不想聊也没关系，我先安静，不消失，等你愿意再说";
      case "D": return "D：你定时间，你舒服最重要，我按你方便的来";
      default: return "";
    }
  }

  compButtons.forEach(btn => {
    btn.addEventListener("click", () => {
      compButtons.forEach(b => b.style.filter = "none");
      compButtons.forEach(b => b.style.border = "none");
      btn.style.filter = "brightness(1.03)";
      btn.style.border = "2px solid rgba(255,77,109,.35)";
      compKey = btn.dataset.comp;

      toP3.disabled = false;
      toP3.style.filter = "none";
      toP3.style.opacity = "1";
    });
  });

  // Generate next-step message
  function buildNextMsg(extraTime=""){
    const head = "那我们就按这个来：";
    const chosen = compText(compKey);

    const timeLine = extraTime ? `\n\n补充：${extraTime}` : "";

    const closing =
`\n\n如果你现在还是不想聊也没关系，我尊重你。你只要告诉我：你最难受的是“我分心”，还是“我让你觉得你不重要”？我会按你在意的点去改。`;

    return `${head}\n${chosen}${timeLine}${closing}`.trim();
  }

  $("toP3").addEventListener("click", () => {
    $("chosenComp").textContent = compText(compKey);
    $("nextMsg").textContent = buildNextMsg("").trim();
    show(p3);
  });

  // Back to P2
  $("backP2").addEventListener("click", () => show(p2));

  // Update next message with time note
  $("copyNext").addEventListener("click", () => copyText($("nextMsg").textContent));
  $("updateNext").addEventListener("click", () => {
    const extra = $("timeNote").value.trim();
    $("nextMsg").textContent = buildNextMsg(extra);
    popToast("已更新");
  });

  // Restart
  $("restart").addEventListener("click", () => {
    // reset
    moodKey = null;
    compKey = null;
    moodChips.forEach(c=>c.classList.remove("selected"));
    toP2.disabled = true; toP2.style.filter="grayscale(1)"; toP2.style.opacity=".6";
    toP3.disabled = true; toP3.style.filter="grayscale(1)"; toP3.style.opacity=".6";
    compButtons.forEach(b => { b.style.border="none"; b.style.filter="none"; });
    $("msgBox").textContent = "";
    $("nextMsg").textContent = "";
    $("chosenComp").textContent = "";
    $("timeNote").value = "";
    $("wheelResult").textContent = "";
    show(p1);
  });

  /** Wheel (optional, random) **/
  const canvas = $("wheel");
  const ctx = canvas.getContext("2d");

  const labels = ["看扑克牌魔术","轻轻拍两下","100元现金红包","全都听你的"];
  const segCount = labels.length;
  const segAngle = (Math.PI*2)/segCount;
  const startAngle = -Math.PI/2; // from top
  const R = canvas.width/2;
  const center = {x:R,y:R};

  let rotation = 0;
  let spinning = false;

  function drawWheel(rot){
    ctx.clearRect(0,0,canvas.width,canvas.height);

    // soft outer
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

    // center circle
    ctx.beginPath();
    ctx.arc(center.x, center.y, 76, 0, Math.PI*2);
    ctx.fillStyle = "rgba(255,255,255,.92)";
    ctx.fill();
    ctx.strokeStyle = "rgba(17,24,39,.12)";
    ctx.lineWidth = 4;
    ctx.stroke();

    ctx.fillStyle = "#111827";
    ctx.font = '900 28px system-ui, -apple-system, "PingFang SC", "Microsoft YaHei"';
    ctx.textAlign = "center";
    ctx.fillText("转一下", center.x, center.y + 10);
  }

  function easeOutCubic(t){ return 1 - Math.pow(1-t, 3); }

  function indexFromRotation(rot){
    // Pointer at top (-PI/2). Determine which segment is at top.
    // Compute angle for top direction in wheel local coords:
    const topAngle = (-Math.PI/2);
    // Convert to wheel's segment angle space:
    // segment center i at: startAngle + rot + (i+0.5)*segAngle
    // find i whose center is closest to topAngle (mod 2PI)
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

    // Make target segment center land at top
    const desiredRot = (-Math.PI/2) - startAngle - (targetIndex + 0.5)*segAngle;

    const extraTurns = 5 + Math.floor(Math.random()*3); // 5-7 turns
    const from = rotation;
    let to = extraTurns * Math.PI*2 + desiredRot;
    while(to < from) to += Math.PI*2;

    const duration = 3600;
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
        $("wheelResult").innerHTML = `🎉 抽到：<span class="good">${labels[idx]}</span>`;
        if (navigator.vibrate) navigator.vibrate([40, 30, 60]);
      }
    }
    requestAnimationFrame(tick);
  }

  $("spinBtn").addEventListener("click", spinRandom);

  $("youDecideBtn").addEventListener("click", () => {
    $("wheelResult").innerHTML = `✅ 我不转了：<span class="good">全都听你的</span>`;
  });

  // initial draw
  drawWheel(rotation);
})();
</script>

</body>
</html>
