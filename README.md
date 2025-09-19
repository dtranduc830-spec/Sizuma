<!doctype html>
<html lang="vi">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>MENU CHÍNH — Bộ cài đặt (Mô phỏng)</title>
<style>
  :root{
    --bg1: #071025; --bg2:#0b1726; --card:#0f1b2a;
    --accent: linear-gradient(90deg,#6b8cff,#7fe0ff);
    --accent-solid: #6b8cff;
    --glass: rgba(255,255,255,0.03);
    --muted: #9fb0d0;
    --success: #4ade80;
  }
  *{box-sizing:border-box}
  body{
    margin:0; font-family:Inter,system-ui,Segoe UI,Arial,sans-serif;
    background: radial-gradient(1200px 600px at 10% 10%, rgba(107,140,255,0.06), transparent),
                linear-gradient(180deg,var(--bg1), var(--bg2));
    color:#eaf3ff; min-height:100vh; display:flex; align-items:center; justify-content:center;
    padding:28px;
  }
  .wrap{width:1100px; max-width:100%; display:grid; grid-template-columns: 1fr 420px; gap:18px; align-items:start}
  .card{background:linear-gradient(180deg,var(--card), #071627); border-radius:14px; padding:18px; border:1px solid rgba(255,255,255,0.03); box-shadow: 0 12px 40px rgba(3,6,20,0.6)}
  .header{display:flex; justify-content:space-between; align-items:center; gap:12px}
  .title{font-size:20px; font-weight:700; display:flex; align-items:center; gap:10px}
  .logo{width:44px;height:44px;border-radius:10px;display:inline-grid;place-items:center;background:linear-gradient(180deg,#2e5cff,#5fb9ff); box-shadow:0 6px 18px rgba(107,140,255,0.12); font-weight:700;color:#02102a}
  .subtitle{color:var(--muted); font-size:13px}
  .section{margin-top:14px}
  .grid{display:grid; grid-template-columns: repeat(2,1fr); gap:12px}
  .control{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); padding:12px; border-radius:10px; border:1px solid rgba(255,255,255,0.02)}
  .control h4{margin:0 0 6px 0; font-size:14px}
  .muted{color:var(--muted); font-size:13px}
  /* toggle */
  .toggle{width:56px; height:32px; background:rgba(255,255,255,0.04); border-radius:999px; position:relative; cursor:pointer; border:1px solid rgba(255,255,255,0.03)}
  .toggle .knob{position:absolute; top:4px; left:4px; width:24px; height:24px; background:#fff; border-radius:50%; transition:all .16s ease; box-shadow:0 3px 10px rgba(2,6,23,0.4)}
  .toggle.on{background:linear-gradient(90deg,#6b8cff,#7fe0ff); box-shadow:0 6px 20px rgba(107,140,255,0.12)}
  .toggle.on .knob{transform:translateX(24px)}
  .row{display:flex; align-items:center; justify-content:space-between; gap:8px; margin:10px 0}
  input[type="range"]{width:100%}
  .val{font-weight:700; color:#dff4ff; min-width:44px; text-align:right}
  /* right panel */
  .panel-right .card{position:sticky; top:26px}
  .buttons{display:flex; gap:8px; margin-top:12px; flex-wrap:wrap}
  .btn{background:linear-gradient(180deg,#0f2538,#071827); color:#dbefff; padding:10px 12px; border-radius:10px; border:1px solid rgba(255,255,255,0.03); cursor:pointer}
  .btn.primary{background:linear-gradient(90deg,#6b8cff,#7fe0ff); color:#022; font-weight:700}
  pre{background:#061428; padding:10px; border-radius:8px; color:#9fd6ff; max-height:220px; overflow:auto}
  .footer{font-size:13px; color:var(--muted); margin-top:10px}
  .chip{display:inline-flex; gap:8px; align-items:center; background:rgba(255,255,255,0.02); padding:8px 10px; border-radius:999px; border:1px solid rgba(255,255,255,0.02)}
  .status{display:flex; gap:8px; align-items:center; margin-top:12px}
  .dot{width:10px;height:10px;border-radius:50%}
  .dot.ok{background:var(--success)} .dot.off{background:#6b7b91}
  @media(max-width:1150px){ .wrap{grid-template-columns:1fr} .grid{grid-template-columns:1fr} }
</style>
</head>
<body>
<div class="wrap">
  <div class="card" role="main" aria-label="Menu chính cấu hình">
    <div class="header">
      <div>
        <div class="title"><span class="logo">M</span> MENU CHÍNH — Bản demo</div>
        <div class="subtitle">Giao diện hoàn chỉnh — chỉ mô phỏng, không can thiệp vào phần mềm</div>
      </div>
      <div style="text-align:right">
        <div class="muted">Phiên bản: <strong>1.0.0</strong></div>
        <div class="muted">Cập nhật: <strong id="updated">—</strong></div>
      </div>
    </div>
    <!-- Các control (fix rung, fix lố, tăng nhạy, giảm delay, smoothing) -->
    <div class="section grid" role="group" aria-label="Các thiết lập chính">
      <div class="control" aria-labelledby="stability">
        <h4 id="stability">Fix rung</h4>
        <div class="muted">Giảm rung mô phỏng: điều chỉnh mức ổn định hiển thị</div>
        <div class="row" style="margin-top:12px;">
          <div style="flex:1; margin-right:12px;">
            <input id="stabilityRange" type="range" min="0" max="100" value="40" aria-label="Mức ổn định">
            <div class="muted" style="margin-top:6px">Mức: <span id="stabilityVal" class="val">40</span></div>
          </div>
          <div>
            <div id="stabilityToggle" class="toggle" role="switch" aria-checked="false" tabindex="0"><div class="knob"></div></div>
          </div>
        </div>
      </div>

      <div class="control" aria-labelledby="overcorrection">
        <h4 id="overcorrection">Fix lố</h4>
        <div class="muted">Giảm phản hồi quá mức — điều chỉnh ngưỡng</div>
        <div class="row" style="margin-top:12px;">
          <div style="flex:1; margin-right:12px;">
            <input id="overRange" type="range" min="0" max="100" value="30" aria-label="Ngưỡng">
            <div class="muted" style="margin-top:6px">Ngưỡng: <span id="overVal" class="val">30</span></div>
          </div>
          <div>
            <div id="overToggle" class="toggle" role="switch" aria-checked="false" tabindex="0"><div class="knob"></div></div>
          </div>
        </div>
      </div>

      <div class="control" aria-labelledby="sensitivity">
        <h4 id="sensitivity">Độ nhạy</h4>
        <div class="muted">Tinh chỉnh độ nhạy (mô phỏng)</div>
        <div class="row" style="margin-top:12px;">
          <div style="flex:1; margin-right:12px;">
            <input id="sensiRange" type="range" min="1" max="200" value="70" aria-label="Độ nhạy">
            <div class="muted" style="margin-top:6px">Mức: <span id="sensiVal" class="val">70</span></div>
          </div>
          <div>
            <div id="sensiToggle" class="toggle" role="switch" aria-checked="true" tabindex="0"><div class="knob"></div></div>
          </div>
        </div>
      </div>

      <div class="control" aria-labelledby="delay">
        <h4 id="delay">Giảm delay</h4>
        <div class="muted">Tăng tần suất mô phỏng làm mới (không can thiệp)</div>
        <div class="row" style="margin-top:12px;">
          <div style="flex:1; margin-right:12px;">
            <input id="delayRange" type="range" min="0" max="500" value="120" aria-label="Delay (ms)">
            <div class="muted" style="margin-top:6px">Delay (ms): <span id="delayVal" class="val">120</span></div>
          </div>
          <div>
            <div id="delayToggle" class="toggle" role="switch" aria-checked="false" tabindex="0"><div class="knob"></div></div>
          </div>
        </div>
      </div>
    </div>

    <div class="section">
      <h4>Chế độ smoothing (mô phỏng)</h4>
      <div class="muted">Làm mượt độ chuyển tiếp giữa các bước mô phỏng</div>
      <div style="margin-top:10px" class="control">
        <div class="row">
          <div style="flex:1">
            <input id="smoothRange" type="range" min="0" max="20" value="6">
            <div class="muted" style="margin-top:6px">Smoothing: <span id="smoothVal" class="val">6</span></div>
          </div>
          <div style="width:110px; text-align:right">
            <div class="chip">Mode: <strong id="modeText" style="margin-left:8px">Standard</strong></div>
          </div>
        </div>
      </div>
    </div>

    <div class="section" style="display:flex; gap:10px; align-items:center; justify-content:space-between">
      <div class="muted">Trạng thái mô phỏng</div>
      <div class="status">
        <div class="dot ok" id="dotSim"></div><div class="muted" id="simText">Inactive</div>
      </div>
    </div>
  </div>