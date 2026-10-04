<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>百宝箱</title>
<style>
:root {
  --bg: #F5F7FA;
  --card: #FFFFFF;
  --text: #1A1D29;
  --sub: #8E95A6;
  --accent: #5B8DEF;
  --accent-2: #6366F1;
  --green: #10B981;
  --red: #EF4444;
  --orange: #F59E0B;
  --radius: 18px;
  --shadow: 0 2px 12px rgba(91,141,239,0.08);
  --shadow-lg: 0 8px 28px rgba(91,141,239,0.18);
}
* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
body {
  font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  background: var(--bg);
  color: var(--text);
  max-width: 420px;
  margin: 0 auto;
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
}
.topbar { display:flex; align-items:center; justify-content:space-between; padding:16px 20px 8px; }
.topbar .icon-btn, .back {
  width:38px; height:38px; border-radius:50%; border:none; background:var(--card);
  box-shadow:var(--shadow); display:flex; align-items:center; justify-content:center;
  cursor:pointer; transition:transform 0.15s; color:var(--text);
}
.topbar .icon-btn:active, .back:active { transform:scale(0.92); }
.topbar .title { font-size:20px; font-weight:700; }
.page { display:none; padding:0 20px 40px; animation:slideIn 0.32s cubic-bezier(0.22,1,0.36,1); }
.page.active { display:block; }
@keyframes slideIn { from{opacity:0;transform:translateX(24px)} to{opacity:1;transform:translateX(0)} }
@keyframes fadeUp { from{opacity:0;transform:translateY(12px)} to{opacity:1;transform:translateY(0)} }
.grid { display:grid; grid-template-columns:1fr 1fr; gap:14px; margin-top:8px; }
.tool-card {
  background:var(--card); border-radius:var(--radius); padding:20px 16px;
  box-shadow:var(--shadow); cursor:pointer; text-align:center;
  transition:transform 0.15s, box-shadow 0.2s; animation:fadeUp 0.4s both;
}
.tool-card:nth-child(1){animation-delay:.05s}
.tool-card:nth-child(2){animation-delay:.12s}
.tool-card:nth-child(3){animation-delay:.19s}
.tool-card:nth-child(4){animation-delay:.26s}
.tool-card:nth-child(5){animation-delay:.33s}
.tool-card:nth-child(6){animation-delay:.40s}
.tool-card:nth-child(7){animation-delay:.47s}
.tool-card:nth-child(8){animation-delay:.54s}
.tool-card:nth-child(9){animation-delay:.61s}
.tool-card:nth-child(10){animation-delay:.68s}
.tool-card:nth-child(11){animation-delay:.75s}
.tool-card:nth-child(12){animation-delay:.82s}
.tool-card:nth-child(13){animation-delay:.89s}
.tool-card:nth-child(14){animation-delay:.96s}
.tool-card:active { transform:scale(0.96); box-shadow:var(--shadow-lg); }
.tool-card .emoji-wrap {
  display:flex;
  align-items:center; justify-content:center;
  width:54px; height:54px;
  border-radius:16px;
  background:linear-gradient(135deg, var(--accent), var(--accent-2));
  margin-bottom:12px;
  box-shadow:0 4px 12px rgba(91,141,239,0.25);
}
.tool-card .ti { width:30px; height:30px; }
.tool-card .name { font-size:15px; font-weight:600; }
.tool-card .desc { font-size:11px; color:var(--sub); margin-top:4px; }
.btn {
  width:100%; padding:14px; border:none; border-radius:14px;
  background:linear-gradient(135deg, var(--accent), var(--accent-2));
  color:#fff; font-size:15px; font-weight:600; cursor:pointer;
  transition:transform 0.15s; margin-top:16px;
}
.btn:active { transform:scale(0.97); }
.btn.outline { background:var(--card); color:var(--accent); border:1.5px solid var(--accent); }
.input {
  width:100%; padding:13px 16px; border:1.5px solid #E5E9F0; border-radius:12px;
  font-size:14px; background:var(--card); outline:none; transition:border-color 0.2s;
  font-family:inherit;
}
.input:focus { border-color:var(--accent); }
.label { font-size:13px; color:var(--sub); margin:14px 0 8px; }
.row { display:flex; gap:10px; }
.row .input { flex:1; }
.back { font-size:18px; }
.quote-box {
  background:linear-gradient(135deg, var(--accent), var(--accent-2)); border-radius:22px;
  padding:40px 24px; color:#fff; margin-top:20px;
  box-shadow:0 10px 30px rgba(0,0,0,0.18); text-align:center; animation:fadeUp 0.5s both;
  transition:background 0.4s;
}
.quote-text { font-size:19px; line-height:1.6; font-weight:500; }
.quote-from { margin-top:16px; font-size:13px; opacity:0.85; }
.quote-loading { font-size:15px; opacity:0.7; padding:20px 0; }
.weather-hero {
  border-radius:24px; padding:28px 24px 24px; color:#fff; margin-top:12px;
  box-shadow:0 12px 36px rgba(0,0,0,0.18); position:relative; overflow:hidden; animation:fadeUp 0.5s both;
}
.weather-hero.sunny { background:linear-gradient(160deg, #4A90E2, #74B9FF, #87CEEB); }
.weather-hero.cloud { background:linear-gradient(160deg, #6B7A8F, #8E9EAF, #A5B2C2); }
.weather-hero.rain { background:linear-gradient(160deg, #4A5568, #606E80, #718096); }
.weather-hero.snow { background:linear-gradient(160deg, #8E9EAF, #B5C3D2, #D6E0EC); }
.weather-hero.thunder { background:linear-gradient(160deg, #2D3748, #4A5568, #6B46C1); }
.weather-hero.fog { background:linear-gradient(160deg, #7B8794, #A4B0BE, #C7CCD9); }
.wh-loc { font-size:18px; font-weight:600; display:flex; align-items:center; gap:6px; }
.wh-time { font-size:12px; opacity:0.85; margin-top:2px; }
.wh-main { display:flex; align-items:center; justify-content:space-between; margin:16px 0; }
.wh-temp { font-size:60px; font-weight:300; line-height:1; }
.wh-cond { font-size:16px; opacity:0.95; margin-top:4px; }
.wh-feel { font-size:12px; opacity:0.8; margin-top:2px; }
.wh-icon { width:110px; height:110px; display:flex; align-items:center; justify-content:center; }
.wh-stats { display:flex; justify-content:space-around; margin-top:12px; padding-top:14px; border-top:1px solid rgba(255,255,255,0.2); }
.wh-stat { text-align:center; }
.wh-stat .v { font-size:16px; font-weight:600; }
.wh-stat .l { font-size:10px; opacity:0.8; margin-top:2px; }
.section-title { font-size:14px; font-weight:600; margin:22px 4px 12px; }
.hourly { display:flex; gap:10px; overflow-x:auto; padding:4px 4px 12px; -webkit-overflow-scrolling:touch; }
.hourly::-webkit-scrollbar { display:none; }
.hour-card { background:var(--card); border-radius:14px; padding:12px 8px; min-width:58px; text-align:center; box-shadow:var(--shadow); flex-shrink:0; }
.hour-card .t { font-size:12px; color:var(--sub); }
.hour-card .ic { width:36px; height:36px; margin:6px auto; }
.hour-card .tmp { font-size:14px; font-weight:600; }
.daily { background:var(--card); border-radius:16px; box-shadow:var(--shadow); overflow:hidden; }
.daily-row { display:flex; align-items:center; padding:14px 16px; border-bottom:1px solid #F0F2F5; }
.daily-row:last-child { border-bottom:none; }
.daily-row .d { width:64px; font-size:14px; font-weight:500; }
.daily-row .ic { width:34px; height:34px; margin:0 14px 0 8px; }
.daily-row .name { flex:1; font-size:13px; color:var(--sub); }
.daily-row .range { font-size:14px; font-weight:600; }
.daily-row .range .lo { color:var(--sub); font-weight:400; margin-right:8px; }
.result-card { background:var(--card); border-radius:18px; padding:28px 20px; margin-top:18px; text-align:center; box-shadow:var(--shadow); animation:fadeUp 0.4s both; min-height:80px; }
.result-big { font-size:32px; font-weight:700; color:var(--accent); }
.result-sub { font-size:13px; color:var(--sub); margin-top:8px; }
.result-pills { display:flex; flex-wrap:wrap; gap:8px; justify-content:center; margin-top:8px; }
.pill { background:#EEF2FF; color:var(--accent); padding:6px 14px; border-radius:20px; font-size:14px; font-weight:600; }
.setting-list { margin-top:12px; background:var(--card); border-radius:16px; box-shadow:var(--shadow); overflow:hidden; }
.setting-item { display:flex; align-items:center; justify-content:space-between; padding:16px 18px; border-bottom:1px solid #F0F2F5; cursor:pointer; transition:background 0.15s; }
.setting-item:last-child { border-bottom:none; }
.setting-item:active { background:#F8FAFC; }
.setting-item .left { display:flex; align-items:center; gap:12px; }
.setting-item .si-emoji { font-size:22px; }
.setting-item .si-name { font-size:15px; }
.setting-item .arrow { color:var(--sub); font-size:14px; }
.about-hero { text-align:center; padding:30px 20px; background:linear-gradient(135deg, var(--accent), var(--accent-2)); border-radius:20px; color:#fff; margin-top:16px; box-shadow:var(--shadow-lg); }
.about-logo { font-size:48px; margin-bottom:8px; }
.about-name { font-size:22px; font-weight:700; }
.about-ver { font-size:13px; opacity:0.85; margin-top:4px; }
.about-section { background:var(--card); border-radius:16px; padding:18px; margin-top:16px; box-shadow:var(--shadow); }
.about-section h4 { font-size:14px; color:var(--sub); margin-bottom:10px; }
.about-section p { font-size:14px; line-height:1.7; }
.about-section p .hl { color:var(--accent); font-weight:600; }
.modal-mask { position:fixed; inset:0; background:rgba(0,0,0,0.4); display:none; align-items:center; justify-content:center; z-index:100; padding:24px; animation:fadeIn 0.2s; }
.modal-mask.show { display:flex; }
@keyframes fadeIn { from{opacity:0} to{opacity:1} }
.modal { background:#fff; border-radius:20px; padding:24px; width:100%; max-width:320px; text-align:center; animation:popIn 0.25s cubic-bezier(0.34,1.56,0.64,1); }
@keyframes popIn { from{opacity:0;transform:scale(0.85)} to{opacity:1;transform:scale(1)} }
.modal-emoji { font-size:40px; margin-bottom:8px; }
.modal-title { font-size:17px; font-weight:700; }
.modal-desc { font-size:13px; color:var(--sub); margin-top:8px; line-height:1.6; }
.modal-actions { display:flex; gap:10px; margin-top:20px; }
.modal-actions .btn { margin-top:0; flex:1; }
.modal-actions .btn.ghost { background:#F0F2F5; color:var(--text); }
.toast { position:fixed; bottom:40px; left:50%; transform:translateX(-50%); background:rgba(26,29,41,0.92); color:#fff; padding:10px 20px; border-radius:24px; font-size:13px; z-index:200; opacity:0; transition:opacity 0.3s; pointer-events:none; }
.toast.show { opacity:1; }

/* ===== 个性化页 ===== */
.p-preview {
  background: var(--card);
  border-radius: 18px;
  padding: 20px;
  margin-top: 16px;
  box-shadow: var(--shadow);
  text-align: center;
}
.p-preview .pp-card {
  display: inline-block;
  background: var(--card);
  border-radius: 14px;
  padding: 14px 20px;
  box-shadow: var(--shadow);
  margin-bottom: 14px;
}
.p-preview .pp-card .pp-emoji { width:24px; height:24px; margin:0 auto 6px; }
.p-preview .pp-card .pp-name { font-size: 13px; font-weight: 600; margin-top: 4px; }
.p-preview .pp-btn {
  display: inline-block;
  padding: 10px 28px;
  border-radius: 12px;
  background: linear-gradient(135deg, var(--accent), var(--accent-2));
  color: #fff;
  font-size: 13px;
  font-weight: 600;
}
.p-section-title { font-size: 13px; color: var(--sub); margin: 22px 4px 12px; }
.p-swatches { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; }
.p-swatch {
  aspect-ratio: 1.6;
  border-radius: 14px;
  cursor: pointer;
  position: relative;
  border: 3px solid transparent;
  transition: transform 0.15s, border-color 0.2s;
  box-shadow: var(--shadow);
}
.p-swatch:active { transform: scale(0.94); }
.p-swatch.active { border-color: var(--accent); }
.p-swatch.active::after {
  content: '✓';
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%,-50%);
  color: #fff;
  font-size: 18px;
  font-weight: 700;
  text-shadow: 0 1px 3px rgba(0,0,0,0.3);
}
.p-swatch .p-swatch-name {
  position: absolute;
  bottom: 6px; left: 0; right: 0;
  text-align: center;
  font-size: 11px;
  color: #fff;
  text-shadow: 0 1px 3px rgba(0,0,0,0.35);
  font-weight: 500;
}
.p-reset {
  width: 100%;
  padding: 13px;
  margin-top: 28px;
  border: 1.5px solid var(--sub);
  background: transparent;
  color: var(--sub);
  border-radius: 14px;
  font-size: 14px;
  cursor: pointer;
}
.p-reset:active { opacity: 0.6; }

/* ===== 壁纸库 ===== */
.wp-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-top:16px; }
.wp-card { border-radius:16px; overflow:hidden; box-shadow:var(--shadow); cursor:pointer; position:relative; animation:fadeUp 0.4s both; transition:transform 0.15s; aspect-ratio: 0.6; }
.wp-card:active { transform:scale(0.96); }
.wp-card img { width:100%; height:100%; object-fit:cover; display:block; }
.wp-card .wp-info { position:absolute; bottom:0; left:0; right:0; background:linear-gradient(transparent,rgba(0,0,0,0.7)); padding:20px 12px 10px; color:#fff; }
.wp-card .wp-title { font-size:13px; font-weight:600; }
.wp-card .wp-date { font-size:11px; opacity:0.85; margin-top:2px; }
.wp-loading { text-align:center; color:var(--sub); padding:60px 0; font-size:14px; }
.wp-viewer { position:fixed; inset:0; background:rgba(0,0,0,0.92); z-index:300; display:none; align-items:center; justify-content:center; flex-direction:column; }
.wp-viewer.show { display:flex; }
.wp-viewer img { max-width:100%; max-height:85vh; object-fit:contain; border-radius:8px; }
.wp-viewer .wp-close { position:absolute; top:16px; right:20px; color:#fff; font-size:28px; cursor:pointer; z-index:301; }
.wp-viewer .wp-save { margin-top:16px; padding:10px 32px; border-radius:24px; background:linear-gradient(135deg,var(--accent),var(--accent-2)); color:#fff; border:none; font-size:14px; font-weight:600; cursor:pointer; }

/* ===== 单位换算 ===== */
.conv-tabs { display:flex; gap:8px; margin-top:16px; overflow-x:auto; padding-bottom:4px; -webkit-overflow-scrolling:touch; }
.conv-tabs::-webkit-scrollbar { display:none; }
.conv-tab { padding:8px 18px; border-radius:20px; background:var(--card); box-shadow:var(--shadow); font-size:13px; font-weight:500; cursor:pointer; white-space:nowrap; transition:all 0.2s; border:1.5px solid transparent; }
.conv-tab.active { background:linear-gradient(135deg,var(--accent),var(--accent-2)); color:#fff; border-color:transparent; }
.conv-row { display:flex; align-items:center; gap:12px; margin-top:16px; }
.conv-row .input { flex:1; }
.conv-arrow { font-size:20px; color:var(--sub); flex-shrink:0; }
.conv-select { padding:13px 12px; border:1.5px solid #E5E9F0; border-radius:12px; font-size:14px; background:var(--card); outline:none; font-family:inherit; flex:1; appearance:none; -webkit-appearance:none; background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath fill='%238E95A6' d='M6 8L0 0h12z'/%3E%3C/svg%3E"); background-repeat:no-repeat; background-position:right 14px center; padding-right:32px; }

/* ===== BMI ===== */
.bmi-gauge { margin-top:24px; text-align:center; }
.bmi-arc { width:200px; height:120px; margin:0 auto; position:relative; }
.bmi-value { font-size:42px; font-weight:700; color:var(--accent); margin-top:8px; }
.bmi-label { font-size:16px; font-weight:600; margin-top:4px; }
.bmi-bar { width:100%; height:10px; border-radius:5px; margin:20px 0 8px; background:linear-gradient(90deg,#60A5FA,#34D399,#FBBF24,#F87171); position:relative; }
.bmi-pointer { position:absolute; top:-4px; width:4px; height:18px; background:var(--text); border-radius:2px; transform:translateX(-50%); transition:left 0.4s; }
.bmi-scale { display:flex; justify-content:space-between; font-size:10px; color:var(--sub); }

/* ===== 密码生成器 ===== */
.pwd-output { background:var(--card); border-radius:14px; padding:18px; margin-top:16px; box-shadow:var(--shadow); display:flex; align-items:center; justify-content:space-between; gap:10px; }
.pwd-text { font-size:16px; font-family:'SF Mono','Cascadia Code',monospace; word-break:break-all; flex:1; color:var(--accent); font-weight:600; }
.pwd-copy { width:36px; height:36px; border-radius:10px; border:none; background:linear-gradient(135deg,var(--accent),var(--accent-2)); color:#fff; cursor:pointer; display:flex; align-items:center; justify-content:center; flex-shrink:0; }
.pwd-copy:active { transform:scale(0.9); }
.pwd-strength { text-align:center; margin-top:12px; font-size:13px; font-weight:600; }
.pwd-slider-row { display:flex; align-items:center; justify-content:space-between; margin-top:20px; }
.pwd-slider-row .label { margin:0; }
.pwd-len { font-size:18px; font-weight:700; color:var(--accent); }
.pwd-slider { width:100%; margin-top:10px; -webkit-appearance:none; appearance:none; height:6px; border-radius:3px; background:#E5E9F0; outline:none; }
.pwd-slider::-webkit-slider-thumb { -webkit-appearance:none; appearance:none; width:22px; height:22px; border-radius:50%; background:linear-gradient(135deg,var(--accent),var(--accent-2)); cursor:pointer; box-shadow:0 2px 8px rgba(91,141,239,0.3); }
.pwd-checks { margin-top:16px; }
.pwd-check { display:flex; align-items:center; justify-content:space-between; padding:12px 0; border-bottom:1px solid #F0F2F5; }
.pwd-check:last-child { border-bottom:none; }
.pwd-check .pc-label { font-size:14px; }
.pwd-toggle { width:44px; height:26px; border-radius:13px; background:#E5E9F0; position:relative; cursor:pointer; transition:background 0.2s; border:none; }
.pwd-toggle.on { background:linear-gradient(135deg,var(--accent),var(--accent-2)); }
.pwd-toggle::after { content:''; position:absolute; top:3px; left:3px; width:20px; height:20px; border-radius:50%; background:#fff; transition:transform 0.2s; box-shadow:0 1px 3px rgba(0,0,0,0.2); }
.pwd-toggle.on::after { transform:translateX(18px); }

/* ===== 时间戳转换 ===== */
.ts-mode { display:flex; gap:8px; margin-top:16px; }
.ts-mode-btn { flex:1; padding:12px; border-radius:12px; border:1.5px solid #E5E9F0; background:var(--card); font-size:14px; font-weight:500; cursor:pointer; transition:all 0.2s; }
.ts-mode-btn.active { background:linear-gradient(135deg,var(--accent),var(--accent-2)); color:#fff; border-color:transparent; }
.ts-now-btn { width:100%; padding:10px; margin-top:10px; border:1.5px dashed var(--accent); border-radius:12px; background:transparent; color:var(--accent); font-size:13px; cursor:pointer; font-weight:600; }
.ts-result { background:var(--card); border-radius:16px; padding:20px; margin-top:16px; box-shadow:var(--shadow); }
.ts-result-row { display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid #F0F2F5; }
.ts-result-row:last-child { border-bottom:none; }
.ts-result-row .ts-label { font-size:13px; color:var(--sub); }
.ts-result-row .ts-val { font-size:14px; font-weight:600; font-family:'SF Mono','Cascadia Code',monospace; }

/* ===== 主页右上角实时时钟 ===== */
.clock-btn {
  width:auto; min-width:38px; height:38px; padding:0 12px; border-radius:19px; border:none;
  background:linear-gradient(135deg, var(--accent), var(--accent-2));
  color:#fff; box-shadow:0 4px 12px rgba(91,141,239,0.25);
  display:flex; align-items:center; justify-content:center;
  font-size:13px; font-weight:700; font-family:'SF Mono','Cascadia Code',monospace;
  letter-spacing:0.5px; cursor:default; transition:transform 0.15s;
}
.clock-btn:active { transform:scale(0.92); }
.clock-btn .clk-sep { opacity:0.7; animation:clkBlink 1s infinite; }
@keyframes clkBlink { 50% { opacity:0.3; } }

/* ===== 二维码 ===== */
.qr-output { background:var(--card); border-radius:18px; padding:24px; margin-top:16px; box-shadow:var(--shadow); text-align:center; }
.qr-canvas-wrap { display:flex; justify-content:center; padding:12px; background:#fff; border-radius:12px; }
.qr-canvas-wrap canvas { image-rendering:pixelated; }
.qr-actions { display:flex; gap:10px; margin-top:16px; }
.qr-actions .btn { margin-top:0; flex:1; }
.qr-history { margin-top:20px; }
.qr-history-item { background:var(--card); border-radius:12px; padding:12px 16px; margin-top:8px; box-shadow:var(--shadow); display:flex; justify-content:space-between; align-items:center; font-size:13px; }
.qr-history-item .qr-h-text { flex:1; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; color:var(--text); }
.qr-history-item .qr-h-del { color:var(--sub); cursor:pointer; padding:4px 8px; }

/* ===== 网络测速 ===== */
.speed-gauge { text-align:center; margin-top:24px; }
.speed-arc { width:220px; height:130px; margin:0 auto; position:relative; }
.speed-value { font-size:48px; font-weight:700; color:var(--accent); margin-top:8px; }
.speed-unit { font-size:14px; color:var(--sub); }
.speed-status { font-size:15px; font-weight:600; margin-top:8px; min-height:22px; }
.speed-phases { display:flex; justify-content:space-around; margin-top:24px; padding:16px; background:var(--card); border-radius:16px; box-shadow:var(--shadow); }
.speed-phase { text-align:center; }
.speed-phase .sp-icon { width:32px; height:32px; margin:0 auto 6px; opacity:0.4; transition:opacity 0.3s; }
.speed-phase.active .sp-icon { opacity:1; }
.speed-phase .sp-name { font-size:12px; color:var(--sub); }
.speed-phase.active .sp-name { color:var(--accent); font-weight:600; }
.speed-history { margin-top:20px; background:var(--card); border-radius:16px; padding:16px; box-shadow:var(--shadow); }
.speed-history h4 { font-size:13px; color:var(--sub); margin-bottom:10px; }
.speed-history-item { display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid #F0F2F5; font-size:13px; }
.speed-history-item:last-child { border-bottom:none; }

/* ===== 番茄钟 ===== */
.pomo-display { text-align:center; margin-top:30px; }
.pomo-time { font-size:72px; font-weight:300; color:var(--accent); font-family:'SF Mono','Cascadia Code',monospace; letter-spacing:2px; }
.pomo-phase { font-size:16px; color:var(--sub); margin-top:8px; }
.pomo-progress { width:100%; height:8px; border-radius:4px; background:#E5E9F0; margin-top:24px; overflow:hidden; }
.pomo-progress-fill { height:100%; background:linear-gradient(90deg,var(--accent),var(--accent-2)); border-radius:4px; transition:width 1s linear; width:100%; }
.pomo-controls { display:flex; gap:12px; margin-top:24px; }
.pomo-controls .btn { margin-top:0; flex:1; }
.pomo-controls .btn.outline { background:var(--card); color:var(--accent); border:1.5px solid var(--accent); }
.pomo-stats { display:flex; justify-content:space-around; margin-top:24px; padding:16px; background:var(--card); border-radius:16px; box-shadow:var(--shadow); }
.pomo-stat { text-align:center; }
.pomo-stat .v { font-size:24px; font-weight:700; color:var(--accent); }
.pomo-stat .l { font-size:12px; color:var(--sub); margin-top:2px; }
.pomo-mode-tabs { display:flex; gap:8px; margin-top:16px; }
.pomo-mode-btn { flex:1; padding:10px; border-radius:12px; border:1.5px solid #E5E9F0; background:var(--card); font-size:13px; cursor:pointer; transition:all 0.2s; }
.pomo-mode-btn.active { background:linear-gradient(135deg,var(--accent),var(--accent-2)); color:#fff; border-color:transparent; }

/* ===== 颜色取色器 ===== */
.color-preview { height:120px; border-radius:18px; margin-top:16px; box-shadow:var(--shadow); position:relative; overflow:hidden; }
.color-preview .cp-info { position:absolute; bottom:0; left:0; right:0; padding:14px 16px; background:linear-gradient(transparent,rgba(0,0,0,0.5)); color:#fff; }
.color-preview .cp-hex { font-size:20px; font-weight:700; font-family:'SF Mono',monospace; }
.color-preview .cp-rgb { font-size:12px; opacity:0.9; margin-top:2px; }
.color-picker-area { margin-top:16px; }
.color-sl-row { display:flex; align-items:center; gap:12px; margin-top:14px; }
.color-sl-row .label { margin:0; white-space:nowrap; }
.color-input-big { width:60px; height:60px; border-radius:14px; border:2px solid var(--card); box-shadow:var(--shadow); cursor:pointer; -webkit-appearance:none; appearance:none; padding:0; overflow:hidden; }
.color-input-big::-webkit-color-swatch-wrapper { padding:0; }
.color-input-big::-webkit-color-swatch { border:none; border-radius:12px; }
.color-presets { display:grid; grid-template-columns:repeat(8,1fr); gap:8px; margin-top:16px; }
.color-preset { aspect-ratio:1; border-radius:8px; cursor:pointer; border:2px solid transparent; transition:transform 0.15s; }
.color-preset:active { transform:scale(0.88); }
.color-info-rows { background:var(--card); border-radius:16px; padding:16px; margin-top:16px; box-shadow:var(--shadow); }
.color-info-row { display:flex; justify-content:space-between; align-items:center; padding:10px 0; border-bottom:1px solid #F0F2F5; }
.color-info-row:last-child { border-bottom:none; }
.color-info-row .ci-label { font-size:13px; color:var(--sub); }
.color-info-row .ci-val { font-size:14px; font-weight:600; font-family:'SF Mono',monospace; }
.color-copy-all { display:flex; gap:8px; margin-top:12px; }
.color-copy-all .btn { margin-top:0; flex:1; font-size:13px; padding:11px; }

/* ===== 设备信息 ===== */
.dev-section { background:var(--card); border-radius:16px; padding:18px; margin-top:16px; box-shadow:var(--shadow); }
.dev-section h4 { font-size:13px; color:var(--sub); margin-bottom:12px; }
.dev-row { display:flex; justify-content:space-between; align-items:center; padding:12px 0; border-bottom:1px solid #F0F2F5; }
.dev-row:last-child { border-bottom:none; }
.dev-row .dv-label { font-size:14px; color:var(--sub); }
.dev-row .dv-val { font-size:14px; font-weight:600; text-align:right; max-width:60%; word-break:break-all; }
.dev-battery-bar { width:100%; height:8px; border-radius:4px; background:#E5E9F0; margin-top:8px; overflow:hidden; }
.dev-battery-fill { height:100%; background:linear-gradient(90deg,#34D399,#10B981); border-radius:4px; transition:width 0.5s; }
.dev-battery-fill.low { background:linear-gradient(90deg,#FBBF24,#F59E0B); }
.dev-battery-fill.critical { background:linear-gradient(90deg,#F87171,#EF4444); }

</style>
</head>
<body>

<div class="page active" id="page-home">
  <div class="topbar">
    <button class="icon-btn" onclick="go('settings')" title="设置">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 1 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>
    </button>
    <div class="title">百宝箱</div>
    <div class="clock-btn" id="home-clock">--<span class="clk-sep">:</span>--<span class="clk-sep">:</span>--</div>
  </div>
  <div class="grid">
    <div class="tool-card" onclick="go('quote')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/></svg></div><div class="name">每日一言</div><div class="desc">随机金句</div></div>
    <div class="tool-card" onclick="go('weather')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/></svg></div><div class="name">今日天气</div><div class="desc">实时预报</div></div>
    <div class="tool-card" onclick="go('random')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="white" stroke="white" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="3"/><circle cx="8" cy="8" r="1.5" fill="#5B8DEF"/><circle cx="16" cy="8" r="1.5" fill="#5B8DEF"/><circle cx="12" cy="12" r="1.5" fill="#5B8DEF"/><circle cx="8" cy="16" r="1.5" fill="#5B8DEF"/><circle cx="16" cy="16" r="1.5" fill="#5B8DEF"/></svg></div><div class="name">随机数</div><div class="desc">范围抽取</div></div>
    <div class="tool-card" onclick="go('decision')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg></div><div class="name">做决定</div><div class="desc">选择困难症</div></div>
    <div class="tool-card" onclick="go('wallpaper')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="3"/><circle cx="8.5" cy="8.5" r="1.5" fill="white"/><path d="M21 15l-5-5L5 21"/></svg></div><div class="name">壁纸库</div><div class="desc">每日精选</div></div>
    <div class="tool-card" onclick="go('unit')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M7 16V4M7 4L4 7M7 4l3 3M17 8v12M17 20l3-3M17 20l-3-3"/></svg></div><div class="name">单位换算</div><div class="desc">长度温度重量</div></div>
    <div class="tool-card" onclick="go('bmi')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 12h4l3-9 4 18 3-9h4"/></svg></div><div class="name">BMI计算</div><div class="desc">身体指数</div></div>
    <div class="tool-card" onclick="go('pwd')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg></div><div class="name">密码生成</div><div class="desc">安全随机</div></div>
    <div class="tool-card" onclick="go('timestamp')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg></div><div class="name">时间戳</div><div class="desc">日期转换</div></div>
    <div class="tool-card" onclick="go('qrcode')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><line x1="14" y1="14" x2="14" y2="17"/><line x1="14" y1="20" x2="17" y2="20"/><line x1="20" y1="14" x2="20" y2="20"/><line x1="17" y1="17" x2="20" y2="17"/></svg></div><div class="name">二维码</div><div class="desc">生成与扫描</div></div>
    <div class="tool-card" onclick="go('speedtest')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 14l3-3"/><path d="M3 12a9 9 0 0 1 9-9"/><path d="M21 12a9 9 0 0 1-9 9"/><path d="M16 8h4v4"/></svg></div><div class="name">网络测速</div><div class="desc">延迟与带宽</div></div>
    <div class="tool-card" onclick="go('pomodoro')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="13" r="8"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="5" y1="3" x2="2" y2="6"/><line x1="22" y1="6" x2="19" y2="3"/></svg></div><div class="name">番茄钟</div><div class="desc">专注计时</div></div>
    <div class="tool-card" onclick="go('color')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="13.5" cy="6.5" r="2.5"/><circle cx="17.5" cy="10.5" r="2.5"/><circle cx="8.5" cy="7.5" r="2.5"/><circle cx="6.5" cy="12.5" r="2.5"/><path d="M12 22a10 10 0 0 1 0-20c5 0 10 4 10 9 0 3-2 5-4 5h-3a2 2 0 0 0-1 4 2 2 0 0 1-2 2z"/></svg></div><div class="name">取色器</div><div class="desc">调色板</div></div>
    <div class="tool-card" onclick="go('device')"><div class="emoji-wrap"><svg class="ti" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="5" y="2" width="14" height="20" rx="2"/><line x1="12" y1="18" x2="12" y2="18"/></svg></div><div class="name">设备信息</div><div class="desc">硬件一览</div></div>
  </div>
</div>

<div class="page" id="page-quote">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">每日一言</div><div style="width:38px"></div></div>
  <div class="quote-box" id="quote-box">
    <div class="quote-loading" id="quote-loading">加载中…</div>
    <div id="quote-content" style="display:none"><div class="quote-text" id="quote-text"></div><div class="quote-from" id="quote-from"></div></div>
  </div>
  <button class="btn" onclick="loadQuote(true)">换一句</button>
</div>

<div class="page" id="page-weather">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">今日天气</div><div style="width:38px"></div></div>
  <div class="row" style="margin-top:12px"><input id="city-input" class="input" placeholder="输入城市名（如 北京/上海）"><button class="btn" style="margin-top:0;width:auto;padding:13px 20px" onclick="queryByCity()">搜索</button></div>
  <button class="btn outline" onclick="useMyLocation()" style="margin-top:10px">📍 使用我的当前位置</button>
  <div id="weather-content" style="display:none">
    <div class="weather-hero" id="wh-hero">
      <div class="wh-loc"><span id="wh-loc">--</span></div>
      <div class="wh-time" id="wh-time">--</div>
      <div class="wh-main"><div><div class="wh-temp" id="wh-temp">--°</div><div class="wh-cond" id="wh-cond">--</div><div class="wh-feel" id="wh-feel">体感 --°</div></div><div class="wh-icon" id="wh-icon"></div></div>
      <div class="wh-stats"><div class="wh-stat"><div class="v" id="ws-hum">--%</div><div class="l">湿度</div></div><div class="wh-stat"><div class="v" id="ws-wind">-- km/h</div><div class="l">风速</div></div><div class="wh-stat"><div class="v" id="ws-hi">--°</div><div class="l">最高</div></div><div class="wh-stat"><div class="v" id="ws-lo">--°</div><div class="l">最低</div></div></div>
    </div>
    <div class="section-title">逐小时预报</div><div class="hourly" id="hourly"></div>
    <div class="section-title">7 天预报</div><div class="daily" id="daily"></div>
  </div>
  <div id="weather-loading" style="text-align:center;color:var(--sub);padding:40px 0;font-size:14px">输入城市或使用定位查看天气</div>
</div>

<div class="page" id="page-random">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">随机数</div><div style="width:38px"></div></div>
  <div class="row" style="margin-top:12px"><input id="r-min" class="input" type="number" placeholder="最小" value="1"><input id="r-max" class="input" type="number" placeholder="最大" value="100"></div>
  <div style="display:flex;align-items:center;gap:10px;margin-top:10px"><label class="label" style="margin:0;white-space:nowrap">抽几个</label><input id="r-count" class="input" type="number" value="1" style="width:80px"></div>
  <label class="label" style="display:flex;align-items:center;gap:8px;margin-top:14px"><input type="checkbox" id="r-uniq" checked> 不重复</label>
  <button class="btn" onclick="drawNumber()">开始抽取</button>
  <div class="result-card" id="r-result" style="display:none"></div>
</div>

<div class="page" id="page-decision">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">做决定</div><div style="width:38px"></div></div>
  <div class="label">输入选项（每行一个）</div>
  <textarea id="dec-options" class="input" rows="6" placeholder="吃火锅&#10;吃烧烤&#10;吃日料"></textarea>
  <button class="btn" onclick="decide()">帮我决定</button>
  <div class="result-card" id="d-result" style="display:none"></div>
</div>

<!-- ===== 壁纸库 ===== -->
<div class="page" id="page-wallpaper">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">壁纸库</div><div style="width:38px"></div></div>
  <div style="font-size:13px;color:var(--sub);margin-top:12px">每日精选高清壁纸，来自必应每日图片</div>
  <div class="wp-grid" id="wp-grid"><div class="wp-loading">加载壁纸中…</div></div>
</div>

<!-- ===== 单位换算 ===== -->
<div class="page" id="page-unit">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">单位换算</div><div style="width:38px"></div></div>
  <div class="conv-tabs" id="conv-tabs"></div>
  <div class="conv-row">
    <input id="conv-from" class="input" type="number" value="1" oninput="doConvert()">
    <select id="conv-from-unit" class="conv-select" onchange="doConvert()"></select>
  </div>
  <div style="text-align:center;color:var(--sub);font-size:20px;margin:4px 0">⇅</div>
  <div class="conv-row">
    <input id="conv-to" class="input" readonly>
    <select id="conv-to-unit" class="conv-select" onchange="doConvert()"></select>
  </div>
  <div style="font-size:13px;color:var(--sub);margin-top:20px;text-align:center" id="conv-formula"></div>
</div>

<!-- ===== BMI 计算 ===== -->
<div class="page" id="page-bmi">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">BMI 计算</div><div style="width:38px"></div></div>
  <div class="row" style="margin-top:16px">
    <div style="flex:1"><div class="label" style="margin:0 0 8px">身高 (cm)</div><input id="bmi-h" class="input" type="number" placeholder="170" oninput="calcBMI()"></div>
    <div style="flex:1"><div class="label" style="margin:0 0 8px">体重 (kg)</div><input id="bmi-w" class="input" type="number" placeholder="65" oninput="calcBMI()"></div>
  </div>
  <div class="bmi-gauge" id="bmi-gauge" style="display:none">
    <svg class="bmi-arc" viewBox="0 0 200 120"><path d="M10 110 A90 90 0 0 1 190 110" fill="none" stroke="#E5E9F0" stroke-width="10" stroke-linecap="round"/><path d="M10 110 A90 90 0 0 1 190 110" fill="none" stroke="url(#bmi-grad)" stroke-width="10" stroke-linecap="round" stroke-dasharray="283" stroke-dashoffset="0"/><defs><linearGradient id="bmi-grad"><stop offset="0%" stop-color="#60A5FA"/><stop offset="35%" stop-color="#34D399"/><stop offset="60%" stop-color="#FBBF24"/><stop offset="100%" stop-color="#F87171"/></linearGradient></defs></svg>
    <div class="bmi-value" id="bmi-val">--</div>
    <div class="bmi-label" id="bmi-cat">--</div>
    <div class="bmi-bar"><div class="bmi-pointer" id="bmi-ptr" style="left:0%"></div></div>
    <div class="bmi-scale"><span>偏瘦</span><span>正常</span><span>偏胖</span><span>肥胖</span></div>
  </div>
  <div style="text-align:center;color:var(--sub);font-size:13px;margin-top:30px" id="bmi-hint">输入身高和体重开始计算</div>
</div>

<!-- ===== 密码生成器 ===== -->
<div class="page" id="page-pwd">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">密码生成器</div><div style="width:38px"></div></div>
  <div class="pwd-output">
    <div class="pwd-text" id="pwd-text">点击下方生成</div>
    <button class="pwd-copy" onclick="copyPwd()" title="复制"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"/></svg></button>
  </div>
  <div class="pwd-strength" id="pwd-strength"></div>
  <div class="pwd-slider-row"><span class="label">密码长度</span><span class="pwd-len" id="pwd-len-val">16</span></div>
  <input type="range" class="pwd-slider" id="pwd-len" min="4" max="32" value="16" oninput="document.getElementById('pwd-len-val').textContent=this.value">
  <div class="pwd-checks" id="pwd-checks">
    <div class="pwd-check"><span class="pc-label">小写字母 (a-z)</span><button class="pwd-toggle on" data-key="lower"></button></div>
    <div class="pwd-check"><span class="pc-label">大写字母 (A-Z)</span><button class="pwd-toggle on" data-key="upper"></button></div>
    <div class="pwd-check"><span class="pc-label">数字 (0-9)</span><button class="pwd-toggle on" data-key="digit"></button></div>
    <div class="pwd-check"><span class="pc-label">特殊符号 (!@#$…)</span><button class="pwd-toggle" data-key="special"></button></div>
  </div>
  <button class="btn" onclick="genPwd()">生成密码</button>
</div>

<!-- ===== 时间戳转换 ===== -->
<div class="page" id="page-timestamp">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">时间戳转换</div><div style="width:38px"></div></div>
  <div class="ts-mode">
    <button class="ts-mode-btn active" onclick="setTsMode('toHuman')">时间戳 → 日期</button>
    <button class="ts-mode-btn" onclick="setTsMode('toTs')">日期 → 时间戳</button>
  </div>
  <div id="ts-to-human">
    <div class="label">Unix 时间戳（秒）</div>
    <input id="ts-input" class="input" placeholder="如 1696200000" oninput="tsConvert()">
    <button class="ts-now-btn" onclick="useNowTs()">使用当前时间戳</button>
    <div class="ts-result" id="ts-result" style="display:none"></div>
  </div>
  <div id="ts-to-ts" style="display:none">
    <div class="label">选择日期时间</div>
    <input id="ts-date" type="datetime-local" class="input" style="font-family:inherit" oninput="dateToTs()">
    <button class="ts-now-btn" onclick="setNowDate()">使用当前时间</button>
    <div class="ts-result" id="ts-result2" style="display:none"></div>
  </div>
</div>

<!-- ===== 二维码 ===== -->
<div class="page" id="page-qrcode">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">二维码生成</div><div style="width:38px"></div></div>
  <div class="label">输入文本/链接</div>
  <textarea id="qr-input" class="input" rows="3" placeholder="输入文字、网址或任意文本…" oninput="genQR()">https://www.workbuddy.cn</textarea>
  <div class="qr-output" id="qr-output" style="display:none">
    <div class="qr-canvas-wrap"><canvas id="qr-canvas"></canvas></div>
  </div>
  <div class="qr-actions">
    <button class="btn outline" onclick="downloadQR()">保存图片</button>
    <button class="btn" onclick="copyQRText()">复制文本</button>
  </div>
  <div class="label" style="margin-top:24px">最近生成</div>
  <div id="qr-history"></div>
</div>

<!-- ===== 网络测速 ===== -->
<div class="page" id="page-speedtest">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">网络测速</div><div style="width:38px"></div></div>
  <div class="speed-gauge">
    <svg class="speed-arc" viewBox="0 0 220 130"><path d="M15 115 A95 95 0 0 1 205 115" fill="none" stroke="#E5E9F0" stroke-width="12" stroke-linecap="round"/><path id="speed-arc-fill" d="M15 115 A95 95 0 0 1 205 115" fill="none" stroke="url(#speed-grad)" stroke-width="12" stroke-linecap="round" stroke-dasharray="298" stroke-dashoffset="298" style="transition:stroke-dashoffset 0.3s"/><defs><linearGradient id="speed-grad"><stop offset="0%" stop-color="#34D399"/><stop offset="50%" stop-color="#5B8DEF"/><stop offset="100%" stop-color="#8B5CF6"/></linearGradient></defs></svg>
    <div class="speed-value" id="speed-val">0.0</div>
    <div class="speed-unit">Mbps</div>
    <div class="speed-status" id="speed-status">点击下方按钮开始测速</div>
  </div>
  <div class="speed-phases" id="speed-phases">
    <div class="speed-phase" id="sp-ping"><svg class="sp-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2v4M12 18v4M4.93 4.93l2.83 2.83M16.24 16.24l2.83 2.83M2 12h4M18 12h4"/></svg><div class="sp-name">延迟</div></div>
    <div class="speed-phase" id="sp-down"><svg class="sp-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 3v12M7 10l5 5 5-5M5 21h14"/></svg><div class="sp-name">下载</div></div>
    <div class="speed-phase" id="sp-up"><svg class="sp-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 21V9M7 14l5-5 5 5M5 3h14"/></svg><div class="sp-name">上传</div></div>
  </div>
  <button class="btn" id="speed-btn" onclick="startSpeedTest()">开始测速</button>
  <div class="speed-history" id="speed-history-box" style="display:none">
    <h4>历史记录</h4>
    <div id="speed-history-list"></div>
  </div>
</div>

<!-- ===== 番茄钟 ===== -->
<div class="page" id="page-pomodoro">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">番茄钟</div><div style="width:38px"></div></div>
  <div class="pomo-mode-tabs">
    <button class="pomo-mode-btn active" onclick="setPomoMode('work',25)">专注 25分</button>
    <button class="pomo-mode-btn" onclick="setPomoMode('short',5)">短休 5分</button>
    <button class="pomo-mode-btn" onclick="setPomoMode('long',15)">长休 15分</button>
  </div>
  <div class="pomo-display">
    <div class="pomo-time" id="pomo-time">25:00</div>
    <div class="pomo-phase" id="pomo-phase">准备开始专注</div>
  </div>
  <div class="pomo-progress"><div class="pomo-progress-fill" id="pomo-fill"></div></div>
  <div class="pomo-controls">
    <button class="btn outline" id="pomo-reset" onclick="resetPomo()">重置</button>
    <button class="btn" id="pomo-toggle" onclick="togglePomo()">开始</button>
  </div>
  <div class="pomo-stats">
    <div class="pomo-stat"><div class="v" id="pomo-count">0</div><div class="l">今日完成</div></div>
    <div class="pomo-stat"><div class="v" id="pomo-total">0</div><div class="l">专注分钟</div></div>
  </div>
</div>

<!-- ===== 颜色取色器 ===== -->
<div class="page" id="page-color">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">颜色取色器</div><div style="width:38px"></div></div>
  <div class="color-preview" id="color-preview" style="background:#5B8DEF">
    <div class="cp-info"><div class="cp-hex" id="cp-hex">#5B8DEF</div><div class="cp-rgb" id="cp-rgb">RGB(91, 141, 239)</div></div>
  </div>
  <div class="color-sl-row">
    <input type="color" class="color-input-big" id="color-picker" value="#5B8DEF" oninput="onColorPick(this.value)">
    <div style="flex:1"><div class="label" style="margin:0 0 4px">手动输入 HEX</div><input class="input" id="color-hex-input" value="#5B8DEF" oninput="onHexInput(this.value)" style="font-family:'SF Mono',monospace"></div>
  </div>
  <div class="label" style="margin-top:20px">预设色板</div>
  <div class="color-presets" id="color-presets"></div>
  <div class="color-info-rows">
    <div class="color-info-row"><span class="ci-label">HEX</span><span class="ci-val" id="ci-hex">#5B8DEF</span></div>
    <div class="color-info-row"><span class="ci-label">RGB</span><span class="ci-val" id="ci-rgb">91, 141, 239</span></div>
    <div class="color-info-row"><span class="ci-label">HSL</span><span class="ci-val" id="ci-hsl">220°, 82%, 65%</span></div>
    <div class="color-info-row"><span class="ci-label">CMYK</span><span class="ci-val" id="ci-cmyk">62%, 41%, 0%, 6%</span></div>
  </div>
  <div class="color-copy-all">
    <button class="btn outline" onclick="copyColor('hex')">复制 HEX</button>
    <button class="btn outline" onclick="copyColor('rgb')">复制 RGB</button>
  </div>
</div>

<!-- ===== 设备信息 ===== -->
<div class="page" id="page-device">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">设备信息</div><div style="width:38px"></div></div>
  <div class="dev-section">
    <h4>屏幕</h4>
    <div class="dev-row"><span class="dv-label">分辨率</span><span class="dv-val" id="dev-res">--</span></div>
    <div class="dev-row"><span class="dv-label">屏幕尺寸</span><span class="dv-val" id="dev-size">--</span></div>
    <div class="dev-row"><span class="dv-label">像素比 (DPR)</span><span class="dv-val" id="dev-dpr">--</span></div>
    <div class="dev-row"><span class="dv-label">色深</span><span class="dv-val" id="dev-depth">--</span></div>
  </div>
  <div class="dev-section">
    <h4>电池</h4>
    <div class="dev-row"><span class="dv-label">电量</span><span class="dv-val" id="dev-battery">--</span></div>
    <div class="dev-battery-bar"><div class="dev-battery-fill" id="dev-battery-fill" style="width:0%"></div></div>
    <div class="dev-row" style="margin-top:8px"><span class="dv-label">充电状态</span><span class="dv-val" id="dev-charging">--</span></div>
  </div>
  <div class="dev-section">
    <h4>浏览器</h4>
    <div class="dev-row"><span class="dv-label">UA</span><span class="dv-val" id="dev-ua">--</span></div>
    <div class="dev-row"><span class="dv-label">平台</span><span class="dv-val" id="dev-platform">--</span></div>
    <div class="dev-row"><span class="dv-label">语言</span><span class="dv-val" id="dev-lang">--</span></div>
    <div class="dev-row"><span class="dv-label">Cookie</span><span class="dv-val" id="dev-cookie">--</span></div>
    <div class="dev-row"><span class="dv-label">在线状态</span><span class="dv-val" id="dev-online">--</span></div>
  </div>
  <div class="dev-section">
    <h4>网络</h4>
    <div class="dev-row"><span class="dv-label">连接类型</span><span class="dv-val" id="dev-conn">--</span></div>
    <div class="dev-row"><span class="dv-label">下行带宽</span><span class="dv-val" id="dev-downlink">--</span></div>
    <div class="dev-row"><span class="dv-label">网络延迟</span><span class="dv-val" id="dev-rtt">--</span></div>
  </div>
  <div class="dev-section">
    <h4>存储</h4>
    <div class="dev-row"><span class="dv-label">内存</span><span class="dv-val" id="dev-mem">--</span></div>
    <div class="dev-row"><span class="dv-label">CPU 核心</span><span class="dv-val" id="dev-cpu">--</span></div>
    <div class="dev-row"><span class="dv-label">触屏支持</span><span class="dv-val" id="dev-touch">--</span></div>
  </div>
</div>

<div class="page" id="page-settings">
  <div class="topbar"><button class="back" onclick="go('home')">‹</button><div class="title">设置</div><div style="width:38px"></div></div>
  <div class="setting-list">
    <div class="setting-item" onclick="go('personalize')"><div class="left"><span class="si-emoji">🎨</span><span class="si-name">个性化</span></div><span class="arrow">›</span></div>
    <div class="setting-item" onclick="go('about')"><div class="left"><span class="si-emoji">ℹ️</span><span class="si-name">关于</span></div><span class="arrow">›</span></div>
  </div>
  <div style="text-align:center;color:var(--sub);font-size:12px;margin-top:24px">更多设置项即将上线</div>
</div>

<div class="page" id="page-about">
  <div class="topbar"><button class="back" onclick="go('settings')">‹</button><div class="title">关于</div><div style="width:38px"></div></div>
  <div class="about-hero"><div class="about-logo">🧰</div><div class="about-name">百宝箱</div><div class="about-ver">版本 1.0.0</div></div>
  <div class="about-section"><h4>功能</h4><p>• 每日一言：来自 hitokoto.cn 的金句<br>• 今日天气：Open-Meteo 实时+小时+7天预报<br>• 随机数：可设范围、数量、是否不重复<br>• 做决定：让命运替你选<br>• 壁纸库：必应每日精选高清壁纸<br>• 单位换算：长度/温度/重量/面积等<br>• BMI计算：身体质量指数评估<br>• 密码生成器：安全随机密码<br>• 时间戳转换：Unix 与日期互转<br>• 二维码：文本/链接生成与保存<br>• 网络测速：延迟+下载+上传三阶段<br>• 番茄钟：25/5/15 三档专注计时<br>• 颜色取色器：HEX/RGB/HSL/CMYK 互转<br>• 设备信息：屏幕/电池/网络/硬件一览</p></div>
  <div class="about-section"><h4>来源</h4><p>天气数据 © <span class="hl">Open-Meteo</span>（CC BY 4.0）<br>金句来源 © <span class="hl">hitokoto.cn</span><br>壁纸来源 © <span class="hl">必应每日 / Picsum</span></p></div>
</div>

<div class="page" id="page-personalize">
  <div class="topbar"><button class="back" onclick="go('settings')">‹</button><div class="title">个性化</div><div style="width:38px"></div></div>

  <div class="p-preview">
    <div class="pp-card"><svg class="pp-emoji" viewBox="0 0 24 24" fill="none" stroke="#1A1D29" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/></svg><div class="pp-name">每日一言</div></div>
    <br>
    <div class="pp-btn">预览效果</div>
  </div>

  <div class="p-section-title">主题色</div>
  <div class="p-swatches" id="theme-swatches"></div>

  <div class="p-section-title">背景</div>
  <div class="p-swatches" id="bg-swatches"></div>

  <button class="p-reset" onclick="resetPersonalize()">重置默认</button>
</div>

<div class="modal-mask" id="loc-modal">
  <div class="modal">
    <div class="modal-emoji">📍</div>
    <div class="modal-title">获取你的位置以查询所在地天气</div>
    <div class="modal-desc">百宝箱需要访问你的位置信息，用于查询你所在地的实时天气和预报。位置数据仅用于本次查询，不会保存或上传。</div>
    <div class="modal-actions"><button class="btn ghost" onclick="closeLocModal(false)">暂不</button><button class="btn" onclick="closeLocModal(true)">允许</button></div>
  </div>
</div>

<div class="wp-viewer" id="wp-viewer">
  <div class="wp-close" onclick="closeWpViewer()">×</div>
  <img id="wp-viewer-img" src="">
  <button class="wp-save" onclick="downloadWp()">保存壁纸</button>
</div>

<div class="toast" id="toast"></div>

<script>
// ===== QR Code 生成器（基于 nayuki/qrcode-gen，简化版） =====
const QRCodeGen = (function(){
// QR Code generator by Project Nayuki — 简化集成版
function QrCode(version, errorCorrectionLevel, dataCodewords, mask){
  this.version=version; this.errorCorrectionLevel=errorCorrectionLevel;
  const numBlocks=QrCode.NUM_ERROR_CORRECTION_BLOCKS[errorCorrectionLevel.ordinal][version];
  const blockEccLens=QrCode.ECC_CODEWORDS_PER_BLOCK[errorCorrectionLevel.ordinal][version];
  const rawCodewords=QrCode.getNumRawDataModules(version);
  const numShortBlocks=numBlocks-rawCodewords%numBlocks;
  const shortBlockLen=Math.floor(rawCodewords/numBlocks);
  const rsBlock=new ReedSolomonGenerator(blockEccLens);
  const blocks=[];
  for(let i=0,k=0;i<numBlocks;i++){
    const dat=dataCodewords.slice(k,k+shortBlockLen-blockEccLens+(i<numShortBlocks?0:1));
    k+=dat.length;
    const ecc=rsBlock.getRemainder(dat);
    if(i>=numShortBlocks)dat.push(0);
    blocks.push(dat.concat(ecc));
  }
  this.modules=[];
  for(let i=0;i<rawCodewords;i++)this.modules.push(null);
  this.isFunction=[];
  for(let i=0;i<rawCodewords;i++)this.isFunction.push(false);
  this.drawFunctionPatterns();
  const allCodewords=[].concat.apply([],blocks);
  for(let i=0;i<allCodewords.length;i++){
    const bit=i*8;
    for(let j=0;j<8;j++){
      this.modules[bit+j]=((allCodewords[i]>>>j)&1)!==0;
    }
  }
  this.applyMask(mask);
}
QrCode.prototype.getModule=function(x,y){return 0<=x&&x<this.size&&0<=y&&y<this.size&&this.modules[y*this.size+x];};
QrCode.prototype.applyMask=function(mask){
  for(let y=0;y<this.size;y++){
    for(let x=0;x<this.size;x++){
      if(this.isFunction[y*this.size+x])continue;
      this.modules[y*this.size+x]^=this.getMask(mask,x,y);
    }
  }
};
QrCode.prototype.getMask=function(mask,x,y){
  switch(mask){
    case 0:return(x+y)%2===0;
    case 1:return y%2===0;
    case 2:return x%3===0;
    case 3:return(x+y)%3===0;
    case 4:return(Math.floor(x/3)+Math.floor(y/2))%2===0;
    case 5:return x*y%2+x*y%3===0;
    case 6:return(x*y%2+x*y%3)%2===0;
    case 7:return((x+y)%2+x*y%3)%2===0;
  }
  throw new Error('mask');
};
QrCode.prototype.drawFunctionPatterns=function(){
  for(let i=0;i<this.size;i++){
    this.setFunctionModule(6,i,i%2===0);
    this.setFunctionModule(i,6,i%2===0);
  }
  this.drawFinder(3,3);
  this.drawFinder(this.size-4,3);
  this.drawFinder(3,this.size-4);
  this.drawFormatBits(0);
  this.drawVersion();
};
QrCode.prototype.drawFormatBits=function(mask){
  const data=this.errorCorrectionLevel.formatBits<<3|mask;
  let rem=data;
  for(let i=0;i<10;i++)rem=(rem<<1)^((rem>>>9)*0x537);
  const bits=(data<<10|rem)^0x5412;
  for(let i=0;i<=5;i++)this.setFunctionModule(8,i,getBit(bits,i));
  this.setFunctionModule(8,7,getBit(bits,6));
  this.setFunctionModule(8,8,getBit(bits,7));
  this.setFunctionModule(7,8,getBit(bits,8));
  for(let i=9;i<15;i++)this.setFunctionModule(14-i,8,getBit(bits,i));
  for(let i=0;i<8;i++)this.setFunctionModule(this.size-1-i,8,getBit(bits,i));
  for(let i=8;i<15;i++)this.setFunctionModule(8,this.size-15+i,getBit(bits,i));
  this.setFunctionModule(8,this.size-8,true);
};
QrCode.prototype.drawVersion=function(){
  if(this.version<7)return;
  let rem=this.version;
  for(let i=0;i<12;i++)rem=(rem<<1)^((rem>>>11)*0x1F25);
  const bits=this.version<<12|rem;
  for(let i=0;i<18;i++){
    const bit=getBit(bits,i),a=this.size-11+i%3,b=Math.floor(i/3);
    this.setFunctionModule(a,b,bit);
    this.setFunctionModule(b,a,bit);
  }
};
QrCode.prototype.drawFinder=function(x,y){
  for(let dy=-4;dy<=4;dy++){
    for(let dx=-4;dx<=4;dx++){
      const dist=Math.max(Math.abs(dx),Math.abs(dy));
      const xx=x+dx,yy=y+dy;
      if(0<=xx&&xx<this.size&&0<=yy&&yy<this.size)
        this.setFunctionModule(xx,yy,dist!==2&&dist!==4);
    }
  }
};
QrCode.prototype.setFunctionModule=function(x,y,isDark){
  this.modules[y*this.size+x]=isDark;
  this.isFunction[y*this.size+x]=true;
};
Object.defineProperty(QrCode.prototype,'size',{get:function(){return this.version*4+17;}});
QrCode.createDefault=function(text,errorCorrectionLevel){
  const seg=QrSegment.makeFromString(text);
  return QrCode.encodeSegments([seg],errorCorrectionLevel,1,40,2,true);
};
QrCode.encodeSegments=function(segments,ecl,minVersion,maxVersion,mask,boostEcl){
  let result=null,version,dataUsedBits;
  for(version=minVersion;version<=maxVersion;version++){
    const dataCapacityBits=QrCode.getNumDataCodewords(version,ecl)*8;
    const usedBits=QrSegment.getTotalBits(segments,version);
    if(usedBits<=dataCapacityBits){dataUsedBits=usedBits;break;}
  }
  if(!version)throw new Error('overflow');
  const dataCodewords=QrCode.makeDataCodewords(segments,version,ecl,dataUsedBits);
  const ecc=QrCode.ECC;
  const eclObj=ecl;
  result=new QrCode(version,eclObj,dataCodewords,mask);
  return result;
};
QrCode.makeDataCodewords=function(segments,version,ecl,usedBits){
  const bb=new BitBuffer();
  for(const seg of segments)seg.appendToBitBuffer(bb);
  bb.appendBits(0,Math.min(4,(QrCode.getNumDataCodewords(version,ecl)*8-usedBits)));
  bb.appendBits(0,(8-(bb.bitLength%8))%8);
  for(const padWord of[0xEC,0x11])bb.appendBits(padWord,8);
  const dataCodewords=bb.getBytes();
  return dataCodewords;
};
QrCode.getNumRawDataModules=function(ver){
  let result=(128*ver+64)*ver;
  if(ver>=2){const numAlign=ver/7+2;result-=(25*numAlign-10)-(ver===32?1:0);}
  return result;
};
QrCode.getNumDataCodewords=function(ver,ecl){
  return Math.floor(QrCode.getNumRawDataModules(ver)/8)-QrCode.ECC_CODEWORDS_PER_BLOCK[ecl.ordinal][ver]*QrCode.NUM_ERROR_CORRECTION_BLOCKS[ecl.ordinal][ver];
};
QrCode.ECC_CODEWORDS_PER_BLOCK=[[-1,7,10,15,20,26,18,20,24,18,26,30,20,18,20,24,28,30,28,28,28,28,30,30,26,28,30,30,30,30,30,30,30,30,30,30,30,30,30,30],[-1,10,16,26,18,24,16,18,22,22,26,30,22,24,22,24,24,28,28,26,26,26,26,28,28,28,28,28,30,30,30,30,30,30,30,30,30,30,30,30],[-1,13,22,18,26,18,24,18,22,20,24,28,26,24,20,30,24,28,28,26,30,28,30,30,30,30,28,30,30,30,30,30,30,30,30,30,30,30,30,30],[-1,17,28,22,16,22,26,22,28,26,22,26,22,26,26,24,28,28,28,28,28,28,28,28,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30]];
QrCode.NUM_ERROR_CORRECTION_BLOCKS=[[-1,1,1,1,1,1,2,2,2,2,4,4,4,4,4,6,6,6,6,7,8,8,9,9,10,12,12,13,13,15,2,2,2,2,2,2,2,2,2,2,2],[-1,1,1,1,2,2,4,4,4,5,9,9,10,10,16,16,18,16,19,21,25,25,28,28,24,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30],[-1,1,1,2,2,4,4,6,6,8,8,8,10,12,16,12,18,16,19,21,20,22,24,24,30,30,26,28,28,30,30,30,30,30,30,30,30,30,30,30,30],[-1,1,1,2,4,4,4,5,6,8,8,11,11,16,16,18,16,19,21,25,25,28,28,24,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30]];
function QrSegment(mode,numChars,bitData){
  this.mode=mode;this.numChars=numChars;this.bitData=bitData;
}
QrSegment.makeFromString=function(text){
  // 自动选择编码模式：纯数字用 NUMERIC，否则 BYTE
  if(/^[0-9]*$/.test(text))return QrSegment.makeNumeric(text);
  return QrSegment.makeBytes(text);
};
QrSegment.makeNumeric=function(digits){
  const bb=new BitBuffer();
  for(const seg of splitNumeric(digits))bb.appendBits(parseInt(seg,10),seg.length*3+1);
  return new QrSegment(QrSegment.Mode.NUMERIC,digits.length,bb.getBytes());
};
QrSegment.makeBytes=function(text){
  const bytes=[];
  for(let i=0;i<text.length;i++){
    let c=text.charCodeAt(i);
    if(c<128)bytes.push(c);
    else if(c<2048){bytes.push(192|(c>>6),128|(c&63));}
    else if(c<65536){bytes.push(224|(c>>12),128|((c>>6)&63),128|(c&63));}
    else{bytes.push(240|(c>>18),128|((c>>12)&63),128|((c>>6)&63),128|(c&63));}
  }
  const bb=new BitBuffer();
  for(const b of bytes)bb.appendBits(b,8);
  return new QrSegment(QrSegment.Mode.BYTE,bytes.length,bb.getBytes());
};
QrSegment.prototype.appendToBitBuffer=function(bb){
  bb.appendBits(this.mode.modeBits,4);
  bb.appendBits(this.numChars,this.mode.numCharCountBits(this.version||1));
  for(const b of this.bitData)bb.appendBits(b,8);
};
QrSegment.getTotalBits=function(segs,ver){
  let total=0;
  for(const seg of segs){
    const ccBits=seg.mode.numCharCountBits(ver);
    total+=4+ccBits+seg.bitData.length*8;
  }
  return total;
};
function splitNumeric(digits){
  const result=[];
  for(let i=0;i<digits.length;i+=3)result.push(digits.substring(i,i+3));
  return result;
}
QrSegment.Mode=function(modeBits,numCharCountBits){
  this.modeBits=modeBits;
  this._numCharCountBits=numCharCountBits;
};
QrSegment.Mode.prototype.numCharCountBits=function(ver){
  return this._numCharCountBits(ver);
};
QrSegment.Mode.NUMERIC=new QrSegment.Mode(0x1,function(v){return v<10?10:v<27?12:14;});
QrSegment.Mode.BYTE=new QrSegment.Mode(0x4,function(v){return v<10?8:16;});
function BitBuffer(){
  this.data=[];this.bitLength=0;
}
BitBuffer.prototype.appendBits=function(val,len){
  if(len<0||len>31)throw new Error('len');
  for(let i=len-1;i>=0;i--){
    const bit=(val>>>i)&1;
    this.data.push(bit);
    this.bitLength++;
  }
};
BitBuffer.prototype.appendBits=function(val,len){
  if(len<0||len>31)throw new Error('len');
  for(let i=len-1;i>=0;i--){
    const bit=(val>>>i)&1;
    this.data.push(bit);
    this.bitLength++;
  }
};
BitBuffer.prototype.getBytes=function(){
  const result=[];
  for(let i=0;i<this.data.length;i+=8){
    let b=0;
    for(let j=0;j<8&&i+j<this.data.length;j++)b=(b<<1)|this.data[i+j];
    result.push(b<<(8-Math.min(8,this.data.length-i)));
  }
  return result;
};
function ReedSolomonGenerator(degree){
  if(degree<1||degree>255)throw new Error('degree');
  this.coefficients=new Array(degree);
  this.coefficients[degree-1]=1;
  let root=1;
  for(let i=0;i<degree;i++){
    for(let j=0;j<degree;j++){
      this.coefficients[j]=ReedSolomonGenerator.multiply(this.coefficients[j],root);
      if(j+1<degree)this.coefficients[j]^=this.coefficients[j+1];
    }
    root=ReedSolomonGenerator.multiply(root,0x02);
  }
}
ReedSolomonGenerator.prototype.getRemainder=function(data){
  const result=this.coefficients.map(function(){return 0;});
  for(let i=0;i<data.length;i++){
    const factor=data[i]^result.shift();
    result.push(0);
    if(factor!==0){
      for(let j=0;j<result.length;j++){
        result[j]^=ReedSolomonGenerator.multiply(this.coefficients[j],factor);
      }
    }
  }
  return result;
};
ReedSolomonGenerator.multiply=function(x,y){
  let z=0;
  for(let i=7;i>=0;i--){
    z=(z<<1)^((z>>>7)*0x11D);
    z^=((y>>>i)&1)*x;
  }
  return z;
};
function getBit(x,i){return((x>>>i)&1)!==0;}
// ECC 等级枚举
const ECC={LOW:{ordinal:0,formatBits:1},MEDIUM:{ordinal:1,formatBits:0},QUARTILE:{ordinal:2,formatBits:3},HIGH:{ordinal:3,formatBits:2}};
QrCode.ECC=ECC;
// 修复 QrSegment.appendToBitBuffer 中 version 未定义问题
QrSegment.prototype.appendToBitBuffer=function(bb){
  // 简化：直接追加
  bb.appendBits(this.mode.modeBits,4);
  // 字符数位数（按 version 1 简化，实际由 createDefault 调用链处理）
  // 这里我们用 BYTE 模式，version>=1 时 8 位
  const ccBits=this.mode===QrSegment.Mode.NUMERIC?10:8;
  bb.appendBits(this.numChars,ccBits);
  for(const b of this.bitData)bb.appendBits(b,8);
};
return {createDefault:function(text,ecl){
  const seg=QrSegment.makeFromString(text);
  const level=ECC.MEDIUM;
  // 简化：直接用 version 5 + M 级（容量足够大部分场景）
  let version=1;
  for(version=1;version<=40;version++){
    try{
      const dataCapacityBits=QrCode.getNumDataCodewords(version,level)*8;
      const usedBits=QrSegment.getTotalBits([seg],version);
      if(usedBits<=dataCapacityBits)break;
    }catch(e){continue;}
  }
  if(version>40)throw new Error('内容过长');
  const dataCodewords=QrCode.makeDataCodewords([seg],version,level,0);
  const qr=new QrCode(version,level,dataCodewords,0);
  return qr;
}};
})();

const WMO = {0:'晴',1:'晴间多云',2:'多云',3:'阴',45:'雾',48:'冻雾',51:'小毛雨',53:'毛雨',55:'大毛雨',61:'小雨',63:'中雨',65:'大雨',71:'小雪',73:'中雪',75:'大雪',77:'雪粒',80:'阵雨',81:'强阵雨',82:'暴阵雨',85:'阵雪',86:'强阵雪',95:'雷阵雨',96:'雷阵雨伴冰雹',99:'强雷阵雨'};
function wmoCategory(c){if(c===0)return'sunny';if(c===1||c===2)return'sunnyCloud';if(c===3)return'overcast';if(c===45||c===48)return'fog';if([51,53,55,61,63,80].includes(c))return'rain';if([65,81,82].includes(c))return'heavyRain';if([71,73,77,85].includes(c))return'snow';if([75,86].includes(c))return'heavySnow';if([95,96,99].includes(c))return'thunder';return'sunny';}
function wmoName(c){return WMO[c]||'未知';}
function svgSmall(cat){const c={sunny:{sun:'#FFB347'},sunnyCloud:{sun:'#FFB347',cloud:'#fff'},overcast:{cloud:'#C7CCD9',cloud2:'#E5E9F0'},cloudy:{cloud:'#fff',cloud2:'#E1E5EE'},fog:{cloud:'#C7CCD9',line:'#9CA3B0'},rain:{cloud:'#9CA3B0',drop:'#5B8DEF'},heavyRain:{cloud:'#6B7280',drop:'#2563EB'},snow:{cloud:'#C7CCD9',flake:'#9CA3B0'},heavySnow:{cloud:'#9CA3B0',flake:'#6B7280'},thunder:{cloud:'#6B7280',bolt:'#F5B400'}}[cat]||{sun:'#FFB347'};switch(cat){case'sunny':return'<svg viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><circle cx="30" cy="30" r="13" fill="'+c.sun+'"/><g stroke="'+c.sun+'" stroke-width="2.5" stroke-linecap="round"><line x1="30" y1="6" x2="30" y2="13"/><line x1="30" y1="47" x2="30" y2="54"/><line x1="6" y1="30" x2="13" y2="30"/><line x1="47" y1="30" x2="54" y2="30"/><line x1="12" y1="12" x2="17" y2="17"/><line x1="43" y1="43" x2="48" y2="48"/><line x1="48" y1="12" x2="43" y2="17"/><line x1="12" y1="48" x2="17" y2="43"/></g></svg>';case'sunnyCloud':return'<svg viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><circle cx="22" cy="22" r="9" fill="'+c.sun+'"/><g stroke="'+c.sun+'" stroke-width="2" stroke-linecap="round"><line x1="22" y1="6" x2="22" y2="10"/><line x1="6" y1="22" x2="10" y2="22"/><line x1="10" y1="10" x2="13" y2="13"/><line x1="31" y1="13" x2="34" y2="10"/></g><path d="M28 40 Q22 40 22 46 Q22 52 30 52 L46 52 Q52 52 52 46 Q52 40 46 40 Q44 34 36 34 Q28 34 28 40 Z" fill="'+c.cloud+'" stroke="#C7CCD9" stroke-width="1"/></svg>';case'cloudy':case'overcast':return'<svg viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><path d="M14 38 Q8 38 8 44 Q8 50 16 50 L46 50 Q54 50 54 44 Q54 38 46 38 Q44 32 36 32 Q26 32 22 38 Q16 38 14 38 Z" fill="'+c.cloud+'" stroke="#C7CCD9" stroke-width="1"/><path d="M20 46 Q16 46 16 50 Q16 54 22 54 L42 54 Q48 54 48 50 Q48 46 42 46 Q40 42 34 42 Q26 42 22 46 Q20 46 20 46 Z" fill="'+(c.cloud2||c.cloud)+'" stroke="#C7CCD9" stroke-width="1" opacity="0.9"/></svg>';case'fog':return'<svg viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><path d="M14 30 Q8 30 8 36 Q8 42 16 42 L46 42 Q54 42 54 36 Q54 30 46 30 Q44 24 36 24 Q26 24 22 30 Z" fill="'+c.cloud+'"/><g stroke="'+c.line+'" stroke-width="2" stroke-linecap="round" opacity="0.7"><line x1="10" y1="48" x2="50" y2="48"/><line x1="14" y1="54" x2="46" y2="54"/></g></svg>';case'rain':case'heavyRain':return'<svg viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><path d="M14 28 Q8 28 8 34 Q8 40 16 40 L46 40 Q54 40 54 34 Q54 28 46 28 Q44 22 36 22 Q26 22 22 28 Z" fill="'+c.cloud+'"/><g stroke="'+c.drop+'" stroke-width="2.5" stroke-linecap="round"><line x1="20" y1="46" x2="18" y2="54"/><line x1="30" y1="46" x2="28" y2="56"/><line x1="40" y1="46" x2="38" y2="54"/>'+(cat==='heavyRain'?'<line x1="14" y1="46" x2="12" y2="54"/><line x1="46" y1="46" x2="44" y2="54"/>':'')+'</g></svg>';case'snow':case'heavySnow':return'<svg viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><path d="M14 28 Q8 28 8 34 Q8 40 16 40 L46 40 Q54 40 54 34 Q54 28 46 28 Q44 22 36 22 Q26 22 22 28 Z" fill="'+c.cloud+'"/><g fill="'+c.flake+'"><circle cx="20" cy="50" r="2"/><circle cx="30" cy="52" r="2"/><circle cx="40" cy="50" r="2"/>'+(cat==='heavySnow'?'<circle cx="14" cy="48" r="1.5"/><circle cx="46" cy="48" r="1.5"/>':'')+'</g></svg>';case'thunder':return'<svg viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg"><path d="M14 26 Q8 26 8 32 Q8 38 16 38 L46 38 Q54 38 54 32 Q54 26 46 26 Q44 20 36 20 Q26 20 22 26 Z" fill="'+c.cloud+'"/><path d="M30 38 L24 50 L30 50 L26 56 L36 44 L30 44 L34 38 Z" fill="'+c.bolt+'" stroke="#D89B00" stroke-width="1"/></svg>';}return svgSmall('sunny');}
function svgBig(cat){return svgSmall(cat).replace('<svg viewBox="0 0 60 60"','<svg viewBox="0 0 60 60" width="110" height="110"');}
function go(p){document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));const e=document.getElementById('page-'+p);if(e){e.classList.add('active');e.style.animation='none';void e.offsetWidth;e.style.animation='';window.scrollTo(0,0);}if(p==='weather'){const has=document.getElementById('weather-content').style.display!=='none';if(!has)setTimeout(()=>document.getElementById('loc-modal').classList.add('show'),300);}if(p==='quote'&&!document.getElementById('quote-content').dataset.loaded)loadQuote(false);if(p==='wallpaper'&&!wpList.length)loadWallpapers();}
function closeLocModal(a){document.getElementById('loc-modal').classList.remove('show');if(a)useMyLocation();}
function toast(m){const t=document.getElementById('toast');t.textContent=m;t.classList.add('show');setTimeout(()=>t.classList.remove('show'),2200);}
async function loadQuote(r){if(r){document.getElementById('quote-content').style.display='none';document.getElementById('quote-loading').style.display='block';document.getElementById('quote-loading').textContent='换一条中…';}try{const res=await fetch('https://v1.hitokoto.cn/?c=i&c=k&encode=json');const d=await res.json();document.getElementById('quote-text').textContent='「'+d.hitokoto+'」';const f=[d.from,d.from_who].filter(Boolean).join(' · ');document.getElementById('quote-from').textContent=f?'—— '+f:'';document.getElementById('quote-loading').style.display='none';document.getElementById('quote-content').style.display='block';document.getElementById('quote-content').dataset.loaded='1';}catch(e){const l=[['人生没有白走的路，每一步都算数。','俗语'],['愿你出走半生，归来仍是少年。','网络'],['天行健，君子以自强不息。','周易']];const x=l[Math.floor(Math.random()*l.length)];document.getElementById('quote-text').textContent='「'+x[0]+'」';document.getElementById('quote-from').textContent='—— '+x[1];document.getElementById('quote-loading').style.display='none';document.getElementById('quote-content').style.display='block';document.getElementById('quote-content').dataset.loaded='1';}}
async function fetchWeather(lat,lon,loc){document.getElementById('weather-loading').textContent='查询中…';document.getElementById('weather-loading').style.display='block';document.getElementById('weather-content').style.display='none';try{const url=`https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current=temperature_2m,relative_humidity_2m,apparent_temperature,weather_code,wind_speed_10m&hourly=temperature_2m,weather_code&daily=weather_code,temperature_2m_max,temperature_2m_min,sunrise,sunset&timezone=auto&forecast_days=7`;const res=await fetch(url);const d=await res.json();const cur=d.current,code=cur.weather_code,cat=wmoCategory(code);const hero=document.getElementById('wh-hero');hero.className='weather-hero '+mapHeroClass(cat);document.getElementById('wh-loc').textContent=loc||`${lat.toFixed(2)}, ${lon.toFixed(2)}`;const now=new Date();document.getElementById('wh-time').textContent=now.toLocaleString('zh-CN',{weekday:'long',hour:'2-digit',minute:'2-digit'});document.getElementById('wh-temp').textContent=Math.round(cur.temperature_2m)+'°';document.getElementById('wh-cond').textContent=wmoName(code);document.getElementById('wh-feel').textContent='体感 '+Math.round(cur.apparent_temperature)+'°';document.getElementById('wh-icon').innerHTML=svgBig(cat);document.getElementById('ws-hum').textContent=cur.relative_humidity_2m+'%';document.getElementById('ws-wind').textContent=Math.round(cur.wind_speed_10m)+' km/h';document.getElementById('ws-hi').textContent=Math.round(d.daily.temperature_2m_max[0])+'°';document.getElementById('ws-lo').textContent=Math.round(d.daily.temperature_2m_min[0])+'°';const hHTML=[];const startIdx=Math.max(0,Math.ceil((Date.now()-new Date(d.hourly.time[0]).getTime())/36e5));for(let i=startIdx;i<startIdx+12&&i<d.hourly.time.length;i++){const t=new Date(d.hourly.time[i]);const h=t.getHours();const hc=wmoCategory(d.hourly.weather_code[i]);hHTML.push(`<div class="hour-card"><div class="t">${i===startIdx?'现在':(h+':00')}</div><div class="ic">${svgSmall(hc)}</div><div class="tmp">${Math.round(d.hourly.temperature_2m[i])}°</div></div>`);}document.getElementById('hourly').innerHTML=hHTML.join('');const dn=['今天','明天','后天','第4天','第5天','第6天','第7天'];const dHTML=[];for(let i=0;i<d.daily.time.length;i++){const dc=wmoCategory(d.daily.weather_code[i]);const dt=new Date(d.daily.time[i]);const lb=i<3?dn[i]:(dt.getMonth()+1)+'/'+dt.getDate();dHTML.push(`<div class="daily-row"><div class="d">${lb}</div><div class="ic">${svgSmall(dc)}</div><div class="name">${wmoName(d.daily.weather_code[i])}</div><div class="range"><span class="lo">${Math.round(d.daily.temperature_2m_min[i])}°</span>${Math.round(d.daily.temperature_2m_max[i])}°</div></div>`);}document.getElementById('daily').innerHTML=dHTML.join('');document.getElementById('weather-loading').style.display='none';document.getElementById('weather-content').style.display='block';}catch(e){document.getElementById('weather-loading').textContent='查询失败，请检查网络后重试';toast('天气查询失败');}}
function mapHeroClass(c){if(c==='sunny'||c==='sunnyCloud')return'sunny';if(c==='overcast'||c==='cloudy')return'cloud';if(c==='rain'||c==='heavyRain')return'rain';if(c==='snow'||c==='heavySnow')return'snow';if(c==='thunder')return'thunder';if(c==='fog')return'fog';return'sunny';}
async function queryByCity(){const city=document.getElementById('city-input').value.trim();if(!city){toast('请输入城市名');return;}document.getElementById('weather-loading').textContent='搜索「'+city+'」中…';document.getElementById('weather-loading').style.display='block';document.getElementById('weather-content').style.display='none';try{const r=await fetch(`https://wttr.in/${encodeURIComponent(city)}?format=j1`);const d=await r.json();const area=(d.nearest_area||[{}])[0];const lat=parseFloat(area.latitude);const lon=parseFloat(area.longitude);const name=area.areaName&&area.areaName[0]?area.areaName[0].value:city;if(isNaN(lat)||isNaN(lon))throw new Error('nf');await fetchWeather(lat,lon,name);}catch(e){document.getElementById('weather-loading').textContent='找不到「'+city+'」，换个城市试试';toast('城市未找到');}}
function useMyLocation(){if(!navigator.geolocation){toast('当前环境不支持定位');return;}document.getElementById('weather-loading').textContent='正在获取你的位置…';document.getElementById('weather-loading').style.display='block';document.getElementById('weather-content').style.display='none';navigator.geolocation.getCurrentPosition(p=>fetchWeather(p.coords.latitude,p.coords.longitude,'我的位置'),err=>{document.getElementById('weather-loading').style.display='none';toast('未获取到位置，可手动输入城市');fetchWeather(39.9042,116.4074,'北京（演示）');},{timeout:8000});}
function drawNumber(){const min=parseInt(document.getElementById('r-min').value),max=parseInt(document.getElementById('r-max').value),count=parseInt(document.getElementById('r-count').value),uniq=document.getElementById('r-uniq').checked;if(isNaN(min)||isNaN(max)||min>max){toast('范围不对');return;}if(count<1){toast('至少抽 1 个');return;}if(uniq&&count>(max-min+1)){toast('范围不够，无法不重复');return;}const pool=[];for(let i=min;i<=max;i++)pool.push(i);const result=[];for(let i=0;i<count;i++){const idx=Math.floor(Math.random()*pool.length);result.push(pool[idx]);if(uniq)pool.splice(idx,1);}const el=document.getElementById('r-result');if(count===1){el.innerHTML='<div class="result-big">'+result[0]+'</div><div class="result-sub">范围 '+min+' - '+max+'</div>';}else{el.innerHTML='<div class="result-pills">'+result.map(n=>'<span class="pill">'+n+'</span>').join('')+'</div><div class="result-sub">共抽 '+count+' 个</div>';}el.style.display='block';}
function decide(){const text=document.getElementById('dec-options').value.trim();const opts=text.split('\n').map(s=>s.trim()).filter(Boolean);if(opts.length<2){toast('至少写 2 个选项');return;}const r=opts[Math.floor(Math.random()*opts.length)];const el=document.getElementById('d-result');el.innerHTML='<div class="result-big">'+r+'</div><div class="result-sub">从 '+opts.length+' 个选项中随机选</div>';el.style.display='block';}

// ===== 个性化 =====
const THEMES = [
  {id:'blue',   name:'晨曦蓝', c1:'#5B8DEF', c2:'#6366F1'},
  {id:'mint',   name:'薄荷青', c1:'#10B981', c2:'#06B6D4'},
  {id:'sunset', name:'晚霞橙', c1:'#F59E0B', c2:'#EF4444'},
  {id:'grape',  name:'葡萄紫', c1:'#8B5CF6', c2:'#EC4899'},
  {id:'ocean',  name:'深海蓝', c1:'#0EA5E9', c2:'#6366F1'},
  {id:'stone',  name:'石墨黑', c1:'#374151', c2:'#6B7280'},
];
const BGS = [
  {id:'white', name:'极光白', bg:'#F5F7FA', card:'#FFFFFF', text:'#1A1D29', sub:'#8E95A6', dark:false},
  {id:'cream', name:'暖米白', bg:'linear-gradient(180deg,#FFF8F0,#F5E6D3)', card:'#FFFFFFFE', text:'#3A2E1F', sub:'#9A8B70', dark:false},
  {id:'cool',  name:'冷雾蓝', bg:'linear-gradient(180deg,#F0F4FA,#E0EAF5)', card:'#FFFFFF', text:'#1A2A3A', sub:'#6B7B8F', dark:false},
  {id:'night', name:'夜空深', bg:'linear-gradient(180deg,#1A1D29,#2D3142)', card:'#262A38', text:'#F5F7FA', sub:'#9AA0B0', dark:true},
];
let curTheme = 'blue', curBg = 'white';

function applyTheme(id) {
  const t = THEMES.find(x => x.id === id) || THEMES[0];
  const r = document.documentElement.style;
  r.setProperty('--accent', t.c1);
  r.setProperty('--accent-2', t.c2);
  curTheme = id;
  // 更新色块选中态
  document.querySelectorAll('#theme-swatches .p-swatch').forEach(s => {
    s.classList.toggle('active', s.dataset.id === id);
  });
}
function applyBg(id) {
  const b = BGS.find(x => x.id === id) || BGS[0];
  const r = document.documentElement.style;
  r.setProperty('--bg', b.bg);
  r.setProperty('--card', b.card);
  r.setProperty('--text', b.text);
  r.setProperty('--sub', b.sub);
  document.body.classList.toggle('dark', b.dark);
  curBg = id;
  document.querySelectorAll('#bg-swatches .p-swatch').forEach(s => {
    s.classList.toggle('active', s.dataset.id === id);
  });
}
function savePersonalize() {
  try { localStorage.setItem('tb_theme', curTheme); localStorage.setItem('tb_bg', curBg); } catch(e){}
}
function loadPersonalize() {
  let t = 'blue', b = 'white';
  try { t = localStorage.getItem('tb_theme') || 'blue'; b = localStorage.getItem('tb_bg') || 'white'; } catch(e){}
  applyTheme(t); applyBg(b);
}
function resetPersonalize() {
  applyTheme('blue'); applyBg('white'); savePersonalize();
  toast('已重置为默认主题');
}
function initPersonalize() {
  const tBox = document.getElementById('theme-swatches');
  const bBox = document.getElementById('bg-swatches');
  tBox.innerHTML = THEMES.map(t => `<div class="p-swatch" data-id="${t.id}" style="background:linear-gradient(135deg,${t.c1},${t.c2})" onclick="applyTheme('${t.id}');savePersonalize()"><div class="p-swatch-name">${t.name}</div></div>`).join('');
  bBox.innerHTML = BGS.map(b => `<div class="p-swatch" data-id="${b.id}" style="background:${b.bg}" onclick="applyBg('${b.id}');savePersonalize()"><div class="p-swatch-name">${b.name}</div></div>`).join('');
  loadPersonalize();
}
initPersonalize();

// ===== 壁纸库 =====
let wpList = [], curWpUrl = '';
async function loadWallpapers() {
  const grid = document.getElementById('wp-grid');
  grid.innerHTML = '<div class="wp-loading">加载壁纸中…</div>';
  // 第一来源：必应每日壁纸（HPImageArchive 接口支持 CORS）
  try {
    const res = await fetch('https://cn.bing.com/HPImageArchive.aspx?format=js&idx=0&n=8&mkt=zh-CN');
    if (res.ok) {
      const data = await res.json();
      if (data.images && data.images.length) {
        wpList = data.images.map((img, i) => ({
          url: 'https://cn.bing.com' + img.urlbase + '_800x1200.jpg',
          title: (img.copyright || '必应精选').split('(')[0].trim().substring(0, 30),
          date: img.enddate || '',
          src: '必应每日'
        }));
        if (wpList.length) { renderWp(); return; }
      }
    }
  } catch(e) { /* fallthrough */ }
  // 第二来源：Picsum Photos（支持 CORS，每次随机）
  try {
    const res2 = await fetch('https://picsum.photos/v2/list?limit=8&page=' + Math.ceil(Math.random()*30));
    if (res2.ok) {
      const data = await res2.json();
      if (data && data.length) {
        wpList = data.map((item, i) => ({
          url: `https://picsum.photos/id/${item.id}/800/1200`,
          title: item.author || '精选壁纸 #' + (i+1),
          date: '',
          src: 'Picsum'
        }));
        if (wpList.length) { renderWp(); return; }
      }
    }
  } catch(e) { /* fallthrough */ }
  grid.innerHTML = '<div class="wp-loading">壁纸加载失败，请检查网络后重试</div>';
}
function renderWp() {
  const grid = document.getElementById('wp-grid');
  grid.innerHTML = wpList.map((wp, i) => `
    <div class="wp-card" style="animation-delay:${i*0.06}s" onclick="viewWallpaper(${i})">
      <img src="${wp.url}" alt="${wp.title}" loading="lazy" referrerpolicy="no-referrer" onerror="this.parentElement.style.display='none'">
      <div class="wp-info"><div class="wp-title">${wp.title.substring(0, 22)}</div><div class="wp-date">${wp.date ? wp.date + ' · ' : ''}${wp.src}</div></div>
    </div>
  `).join('');
}
function viewWallpaper(i) {
  curWpUrl = wpList[i].url;
  document.getElementById('wp-viewer-img').src = curWpUrl;
  document.getElementById('wp-viewer').classList.add('show');
}
function closeWpViewer() {
  document.getElementById('wp-viewer').classList.remove('show');
}
function downloadWp() {
  const a = document.createElement('a');
  a.href = curWpUrl;
  a.download = 'wallpaper_' + Date.now() + '.jpg';
  a.target = '_blank';
  a.referrerPolicy = 'no-referrer';
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  toast('已打开下载链接');
}

// ===== 单位换算 =====
const UNIT_DATA = {
  length: { name:'长度', units:[
    {id:'mm',name:'毫米',factor:0.001},{id:'cm',name:'厘米',factor:0.01},
    {id:'m',name:'米',factor:1},{id:'km',name:'千米',factor:1000},
    {id:'inch',name:'英寸',factor:0.0254},{id:'ft',name:'英尺',factor:0.3048},{id:'mile',name:'英里',factor:1609.34}
  ]},
  weight: { name:'重量', units:[
    {id:'mg',name:'毫克',factor:0.001},{id:'g',name:'克',factor:1},
    {id:'kg',name:'千克',factor:1000},{id:'t',name:'吨',factor:1000000},
    {id:'lb',name:'磅',factor:453.592},{id:'oz',name:'盎司',factor:28.3495}
  ]},
  temperature: { name:'温度', units:[
    {id:'c',name:'摄氏度 °C'},{id:'f',name:'华氏度 °F'},{id:'k',name:'开尔文 K'}
  ]},
  area: { name:'面积', units:[
    {id:'mm2',name:'平方毫米',factor:0.000001},{id:'cm2',name:'平方厘米',factor:0.0001},
    {id:'m2',name:'平方米',factor:1},{id:'km2',name:'平方千米',factor:1000000},
    {id:'ha',name:'公顷',factor:10000},{id:'mu',name:'亩',factor:666.67},
    {id:'acre',name:'英亩',factor:4046.86},{id:'ft2',name:'平方英尺',factor:0.092903}
  ]},
  volume: { name:'体积', units:[
    {id:'ml',name:'毫升',factor:0.001},{id:'l',name:'升',factor:1},
    {id:'m3',name:'立方米',factor:1000},{id:'gallon',name:'加仑',factor:3.78541}
  ]},
  speed: { name:'速度', units:[
    {id:'ms',name:'米/秒',factor:1},{id:'kmh',name:'千米/时',factor:0.277778},
    {id:'mph',name:'英里/时',factor:0.44704},{id:'knot',name:'节',factor:0.514444}
  ]}
};
let curConvType = 'length';
function initConvTabs() {
  const tabs = document.getElementById('conv-tabs');
  tabs.innerHTML = Object.entries(UNIT_DATA).map(([k,v]) =>
    `<div class="conv-tab ${k===curConvType?'active':''}" onclick="setConvType('${k}')">${v.name}</div>`
  ).join('');
  setConvUnits();
  doConvert();
}
function setConvType(k) {
  curConvType = k;
  document.querySelectorAll('#conv-tabs .conv-tab').forEach(t => t.classList.remove('active'));
  event.target.classList.add('active');
  setConvUnits();
  doConvert();
}
function setConvUnits() {
  const units = UNIT_DATA[curConvType].units;
  const fromSel = document.getElementById('conv-from-unit');
  const toSel = document.getElementById('conv-to-unit');
  fromSel.innerHTML = units.map(u => `<option value="${u.id}">${u.name}</option>`).join('');
  toSel.innerHTML = units.map(u => `<option value="${u.id}">${u.name}</option>`).join('');
  if (units.length > 1) toSel.value = units[1].id;
}
function doConvert() {
  const v = parseFloat(document.getElementById('conv-from').value);
  const units = UNIT_DATA[curConvType].units;
  const fromId = document.getElementById('conv-from-unit').value;
  const toId = document.getElementById('conv-to-unit').value;
  const fromU = units.find(u => u.id === fromId);
  const toU = units.find(u => u.id === toId);
  if (isNaN(v)) { document.getElementById('conv-to').value = ''; return; }
  let result;
  if (curConvType === 'temperature') {
    // 先转 °C
    let c;
    if (fromId === 'c') c = v;
    else if (fromId === 'f') c = (v - 32) * 5/9;
    else c = v - 273.15;
    // 再从 °C 转到目标
    if (toId === 'c') result = c;
    else if (toId === 'f') result = c * 9/5 + 32;
    else result = c + 273.15;
  } else {
    const baseVal = v * fromU.factor;
    result = baseVal / toU.factor;
  }
  document.getElementById('conv-to').value = parseFloat(result.toFixed(6));
  const fName = fromU.name, tName = toU.name;
  document.getElementById('conv-formula').textContent = `1 ${fName} = ${(1 * fromU.factor / toU.factor).toFixed(6)} ${tName}`;
}

// ===== BMI =====
function calcBMI() {
  const h = parseFloat(document.getElementById('bmi-h').value);
  const w = parseFloat(document.getElementById('bmi-w').value);
  const gauge = document.getElementById('bmi-gauge');
  const hint = document.getElementById('bmi-hint');
  if (!h || !w) { gauge.style.display = 'none'; hint.style.display = 'block'; return; }
  const m = h / 100;
  const bmi = w / (m * m);
  gauge.style.display = 'block';
  hint.style.display = 'none';
  document.getElementById('bmi-val').textContent = bmi.toFixed(1);
  let cat, color, pct;
  if (bmi < 18.5) { cat = '偏瘦'; color = '#60A5FA'; pct = Math.max(5, (bmi / 18.5) * 25); }
  else if (bmi < 24) { cat = '正常'; color = '#34D399'; pct = 25 + ((bmi - 18.5) / 5.5) * 35; }
  else if (bmi < 28) { cat = '偏胖'; color = '#FBBF24'; pct = 60 + ((bmi - 24) / 4) * 20; }
  else { cat = '肥胖'; color = '#F87171'; pct = Math.min(95, 80 + ((bmi - 28) / 10) * 15); }
  document.getElementById('bmi-cat').textContent = cat;
  document.getElementById('bmi-cat').style.color = color;
  document.getElementById('bmi-val').style.color = color;
  document.getElementById('bmi-ptr').style.left = pct + '%';
}

// ===== 密码生成器 =====
const PWD_SETS = {
  lower: 'abcdefghijklmnopqrstuvwxyz',
  upper: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
  digit: '0123456789',
  special: '!@#$%^&*()_+-=[]{}|;:,.<>?'
};
function genPwd() {
  const len = parseInt(document.getElementById('pwd-len').value);
  const types = [];
  document.querySelectorAll('#pwd-checks .pwd-toggle').forEach(t => {
    if (t.classList.contains('on')) types.push(t.dataset.key);
  });
  if (types.length === 0) { toast('请至少选一种字符类型'); return; }
  let charset = '', pools = [];
  types.forEach(k => { charset += PWD_SETS[k]; pools.push(PWD_SETS[k]); });
  // 使用 crypto 随机数
  const arr = new Uint32Array(len);
  crypto.getRandomValues(arr);
  let pwd = '';
  for (let i = 0; i < len; i++) pwd += charset[arr[i] % charset.length];
  // 确保每种选中类型至少有1个字符
  if (len >= types.length) {
    pools.forEach((pool, pi) => {
      if (!pool.split('').includes(pwd[pi])) {
        const r = new Uint32Array(1);
        crypto.getRandomValues(r);
        pwd = pwd.substring(0, pi) + pool[r[0] % pool.length] + pwd.substring(pi + 1);
      }
    });
  }
  document.getElementById('pwd-text').textContent = pwd;
  // 强度评估
  const entropy = len * Math.log2(charset.length);
  const strengthEl = document.getElementById('pwd-strength');
  if (entropy < 40) { strengthEl.textContent = '强度：弱'; strengthEl.style.color = '#F87171'; }
  else if (entropy < 60) { strengthEl.textContent = '强度：中'; strengthEl.style.color = '#FBBF24'; }
  else if (entropy < 80) { strengthEl.textContent = '强度：强'; strengthEl.style.color = '#34D399'; }
  else { strengthEl.textContent = '强度：极强 ✓'; strengthEl.style.color = '#10B981'; }
}
document.addEventListener('click', e => {
  if (e.target.classList.contains('pwd-toggle')) e.target.classList.toggle('on');
});
function copyPwd() {
  const text = document.getElementById('pwd-text').textContent;
  if (!text || text === '点击下方生成') { toast('请先生成密码'); return; }
  navigator.clipboard.writeText(text).then(() => toast('已复制到剪贴板')).catch(() => {
    // 兜底
    const ta = document.createElement('textarea');
    ta.value = text; document.body.appendChild(ta); ta.select();
    try { document.execCommand('copy'); toast('已复制'); } catch(e) { toast('复制失败'); }
    document.body.removeChild(ta);
  });
}

// ===== 时间戳转换 =====
let tsMode = 'toHuman';
function setTsMode(m) {
  tsMode = m;
  document.querySelectorAll('.ts-mode-btn').forEach(b => b.classList.remove('active'));
  event.target.classList.add('active');
  document.getElementById('ts-to-human').style.display = m === 'toHuman' ? 'block' : 'none';
  document.getElementById('ts-to-ts').style.display = m === 'toTs' ? 'block' : 'none';
}
function tsConvert() {
  const input = document.getElementById('ts-input').value.trim();
  const resultEl = document.getElementById('ts-result');
  if (!input) { resultEl.style.display = 'none'; return; }
  let ts = parseInt(input);
  if (isNaN(ts)) { resultEl.style.display = 'none'; return; }
  // 支持毫秒
  if (input.length > 10) ts = Math.floor(ts / 1000);
  const d = new Date(ts * 1000);
  resultEl.style.display = 'block';
  resultEl.innerHTML = `
    <div class="ts-result-row"><span class="ts-label">本地时间</span><span class="ts-val">${d.toLocaleString('zh-CN')}</span></div>
    <div class="ts-result-row"><span class="ts-label">UTC 时间</span><span class="ts-val">${d.toISOString().replace('T',' ').replace('.000Z','')}</span></div>
    <div class="ts-result-row"><span class="ts-label">星期</span><span class="ts-val">${'日一二三四五六'[d.getDay()]}曜日</span></div>
    <div class="ts-result-row"><span class="ts-label">距今天数</span><span class="ts-val">${Math.floor((Date.now() - ts*1000) / 86400000)} 天前</span></div>
  `;
}
function useNowTs() {
  document.getElementById('ts-input').value = Math.floor(Date.now() / 1000);
  tsConvert();
}
function dateToTs() {
  const val = document.getElementById('ts-date').value;
  const resultEl = document.getElementById('ts-result2');
  if (!val) { resultEl.style.display = 'none'; return; }
  const d = new Date(val);
  const ts = Math.floor(d.getTime() / 1000);
  const ms = d.getTime();
  resultEl.style.display = 'block';
  resultEl.innerHTML = `
    <div class="ts-result-row"><span class="ts-label">秒级时间戳</span><span class="ts-val">${ts}</span></div>
    <div class="ts-result-row"><span class="ts-label">毫秒时间戳</span><span class="ts-val">${ms}</span></div>
    <div class="ts-result-row"><span class="ts-label">UTC 时间</span><span class="ts-val">${d.toISOString().replace('T',' ').replace('.000Z','')}</span></div>
  `;
}
function setNowDate() {
  const d = new Date();
  const offset = d.getTimezoneOffset() * 60000;
  const local = new Date(d.getTime() - offset).toISOString().slice(0, 16);
  document.getElementById('ts-date').value = local;
  dateToTs();
}

// ===== 主页实时时钟 =====
function updateClock() {
  const d = new Date();
  const h = String(d.getHours()).padStart(2,'0');
  const m = String(d.getMinutes()).padStart(2,'0');
  const s = String(d.getSeconds()).padStart(2,'0');
  const el = document.getElementById('home-clock');
  if (el) el.innerHTML = h + '<span class="clk-sep">:</span>' + m + '<span class="clk-sep">:</span>' + s;
}
updateClock();
setInterval(updateClock, 1000);

// ===== 二维码生成（纯 JS 实现，无依赖） =====
// 使用 QR Code 算法（基于 nayuki/qrcode-gen 的简化版）
let qrHistory = [];
function genQR() {
  const text = document.getElementById('qr-input').value.trim();
  const out = document.getElementById('qr-output');
  if (!text) { out.style.display = 'none'; return; }
  out.style.display = 'block';
  const canvas = document.getElementById('qr-canvas');
  try {
    drawQR(canvas, text);
  } catch(e) {
    // 兜底：用 canvas 画文字
    const ctx = canvas.getContext('2d');
    canvas.width = 200; canvas.height = 200;
    ctx.fillStyle = '#fff'; ctx.fillRect(0,0,200,200);
    ctx.fillStyle = '#000'; ctx.font = '12px monospace';
    ctx.fillText(text.substring(0,100), 10, 100);
  }
}
function drawQR(canvas, text) {
  const qr = QRCodeGen.createDefault(text, 0);
  const size = qr.size;
  const scale = Math.max(4, Math.floor(240 / size));
  canvas.width = size * scale;
  canvas.height = size * scale;
  const ctx = canvas.getContext('2d');
  ctx.fillStyle = '#fff';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = '#000';
  for (let y = 0; y < size; y++) {
    for (let x = 0; x < size; x++) {
      if (qr.getModule(x, y)) {
        ctx.fillRect(x * scale, y * scale, scale, scale);
      }
    }
  }
}
function downloadQR() {
  const canvas = document.getElementById('qr-canvas');
  if (!canvas.width) { toast('请先生成二维码'); return; }
  const a = document.createElement('a');
  a.href = canvas.toDataURL('image/png');
  a.download = 'qrcode_' + Date.now() + '.png';
  a.click();
  toast('已保存二维码图片');
}
function copyQRText() {
  const text = document.getElementById('qr-input').value.trim();
  if (!text) { toast('请输入文本'); return; }
  navigator.clipboard.writeText(text).then(() => toast('已复制文本')).catch(() => toast('复制失败'));
}
function addQRHistory(text) {
  if (!text || qrHistory[0] === text) return;
  qrHistory.unshift(text);
  if (qrHistory.length > 5) qrHistory.pop();
  try { localStorage.setItem('tb_qr_hist', JSON.stringify(qrHistory)); } catch(e){}
  renderQRHistory();
}
function renderQRHistory() {
  const box = document.getElementById('qr-history');
  if (!qrHistory.length) { box.innerHTML = '<div style="color:var(--sub);font-size:13px;text-align:center;padding:12px">暂无历史</div>'; return; }
  box.innerHTML = qrHistory.map((t, i) =>
    `<div class="qr-history-item"><span class="qr-h-text" onclick="useQRHist(${i})">${t.replace(/</g,'&lt;')}</span><span class="qr-h-del" onclick="delQRHist(${i})">×</span></div>`
  ).join('');
}
function useQRHist(i) {
  document.getElementById('qr-input').value = qrHistory[i];
  genQR();
}
function delQRHist(i) {
  qrHistory.splice(i, 1);
  try { localStorage.setItem('tb_qr_hist', JSON.stringify(qrHistory)); } catch(e){}
  renderQRHistory();
}
try { qrHistory = JSON.parse(localStorage.getItem('tb_qr_hist') || '[]'); } catch(e) { qrHistory = []; }
// 监听输入生成并记录历史
let qrTimer = null;
document.addEventListener('input', e => {
  if (e.target.id === 'qr-input') {
    clearTimeout(qrTimer);
    qrTimer = setTimeout(() => {
      if (e.target.value.trim()) addQRHistory(e.target.value.trim());
    }, 1500);
  }
});

// ===== 网络测速 =====
let speedTesting = false;
async function startSpeedTest() {
  if (speedTesting) return;
  speedTesting = true;
  const btn = document.getElementById('speed-btn');
  btn.textContent = '测速中…'; btn.style.opacity = '0.6';
  const valEl = document.getElementById('speed-val');
  const statusEl = document.getElementById('speed-status');
  const arcFill = document.getElementById('speed-arc-fill');
  // 重置
  ['sp-ping','sp-down','sp-up'].forEach(id => document.getElementById(id).classList.remove('active'));
  valEl.textContent = '0.0';
  arcFill.style.strokeDashoffset = 298;

  // 阶段1：延迟
  document.getElementById('sp-ping').classList.add('active');
  statusEl.textContent = '测量延迟中…';
  const pings = [];
  for (let i = 0; i < 5; i++) {
    const t0 = performance.now();
    try {
      await fetch(`https://api.open-meteo.com/v1/forecast?latitude=0&longitude=0&current=temperature_2m&_=${Date.now()}`, {cache:'no-store'});
      pings.push(performance.now() - t0);
    } catch(e) { pings.push(999); }
  }
  const avgPing = Math.round(pings.reduce((a,b)=>a+b,0) / pings.length);
  document.getElementById('sp-ping').classList.remove('active');

  // 阶段2：下载
  document.getElementById('sp-down').classList.add('active');
  statusEl.textContent = '测量下载速度中…';
  let downSpeed = 0;
  const downSizes = [250000, 500000, 1000000]; // 渐进下载
  for (const size of downSizes) {
    const t0 = performance.now();
    try {
      const res = await fetch(`https://speed.cloudflare.com/__down?bytes=${size}&_=${Date.now()}`, {cache:'no-store'});
      const blob = await res.blob();
      const elapsed = (performance.now() - t0) / 1000;
      const speed = (blob.size * 8) / 1000000 / elapsed; // Mbps
      if (speed > downSpeed) downSpeed = speed;
      valEl.textContent = downSpeed.toFixed(1);
      // 更新弧线（最大 200 Mbps）
      const pct = Math.min(1, downSpeed / 200);
      arcFill.style.strokeDashoffset = 298 * (1 - pct);
    } catch(e) {}
  }
  document.getElementById('sp-down').classList.remove('active');

  // 阶段3：上传
  document.getElementById('sp-up').classList.add('active');
  statusEl.textContent = '测量上传速度中…';
  let upSpeed = 0;
  const upData = new Uint8Array(500000);
  crypto.getRandomValues(upData);
  for (let i = 0; i < 2; i++) {
    const t0 = performance.now();
    try {
      await fetch('https://speed.cloudflare.com/__up', {
        method: 'POST',
        body: upData,
        cache: 'no-store'
      });
      const elapsed = (performance.now() - t0) / 1000;
      const speed = (upData.length * 8) / 1000000 / elapsed;
      if (speed > upSpeed) upSpeed = speed;
    } catch(e) {}
  }
  document.getElementById('sp-up').classList.remove('active');

  // 结果
  valEl.textContent = downSpeed.toFixed(1);
  statusEl.innerHTML = `下载 <b style="color:var(--accent)">${downSpeed.toFixed(1)}</b> Mbps · 上传 <b style="color:var(--accent)">${upSpeed.toFixed(1)}</b> Mbps · 延迟 <b style="color:var(--accent)">${avgPing}</b> ms`;
  btn.textContent = '重新测速'; btn.style.opacity = '1';
  speedTesting = false;

  // 保存历史
  const hist = JSON.parse(localStorage.getItem('tb_speed_hist') || '[]');
  hist.unshift({ time: new Date().toLocaleString('zh-CN'), down: downSpeed.toFixed(1), up: upSpeed.toFixed(1), ping: avgPing });
  if (hist.length > 5) hist.pop();
  try { localStorage.setItem('tb_speed_hist', JSON.stringify(hist)); } catch(e){}
  renderSpeedHistory();
}
function renderSpeedHistory() {
  const box = document.getElementById('speed-history-box');
  const list = document.getElementById('speed-history-list');
  const hist = JSON.parse(localStorage.getItem('tb_speed_hist') || '[]');
  if (!hist.length) { box.style.display = 'none'; return; }
  box.style.display = 'block';
  list.innerHTML = hist.map(h =>
    `<div class="speed-history-item"><span>${h.time}</span><span>↓${h.down} ↑${h.up} ${h.ping}ms</span></div>`
  ).join('');
}

// ===== 番茄钟 =====
let pomoMode = 'work', pomoDuration = 25 * 60, pomoRemain = 25 * 60, pomoRunning = false, pomoTimer = null;
let pomoCount = parseInt(localStorage.getItem('tb_pomo_count') || '0');
let pomoTotal = parseInt(localStorage.getItem('tb_pomo_total') || '0');
function setPomoMode(mode, min) {
  pomoMode = mode; pomoDuration = min * 60; pomoRemain = min * 60;
  document.querySelectorAll('.pomo-mode-btn').forEach(b => b.classList.remove('active'));
  event.target.classList.add('active');
  if (pomoRunning) { clearInterval(pomoTimer); pomoRunning = false; }
  document.getElementById('pomo-toggle').textContent = '开始';
  document.getElementById('pomo-toggle').classList.remove('outline');
  updatePomoDisplay();
  const phaseText = mode === 'work' ? '准备开始专注' : mode === 'short' ? '准备短休' : '准备长休';
  document.getElementById('pomo-phase').textContent = phaseText;
}
function updatePomoDisplay() {
  const m = Math.floor(pomoRemain / 60);
  const s = pomoRemain % 60;
  document.getElementById('pomo-time').textContent = String(m).padStart(2,'0') + ':' + String(s).padStart(2,'0');
  const pct = (pomoRemain / pomoDuration) * 100;
  document.getElementById('pomo-fill').style.width = pct + '%';
  document.getElementById('pomo-count').textContent = pomoCount;
  document.getElementById('pomo-total').textContent = pomoTotal;
}
function togglePomo() {
  if (pomoRunning) {
    clearInterval(pomoTimer);
    pomoRunning = false;
    document.getElementById('pomo-toggle').textContent = '继续';
    document.getElementById('pomo-phase').textContent = '已暂停';
  } else {
    pomoRunning = true;
    document.getElementById('pomo-toggle').textContent = '暂停';
    document.getElementById('pomo-phase').textContent = pomoMode === 'work' ? '专注中…' : pomoMode === 'short' ? '短休中…' : '长休中…';
    pomoTimer = setInterval(() => {
      pomoRemain--;
      if (pomoRemain <= 0) {
        clearInterval(pomoTimer);
        pomoRunning = false;
        if (pomoMode === 'work') {
          pomoCount++;
          pomoTotal += pomoDuration / 60;
          try { localStorage.setItem('tb_pomo_count', pomoCount); localStorage.setItem('tb_pomo_total', pomoTotal); } catch(e){}
          toast('专注完成！休息一下');
          // 自动切到短休
          document.querySelectorAll('.pomo-mode-btn').forEach(b => b.classList.remove('active'));
          document.querySelectorAll('.pomo-mode-btn')[1].classList.add('active');
          setPomoModeSilent('short', 5);
        } else {
          toast('休息结束，继续专注');
          document.querySelectorAll('.pomo-mode-btn').forEach(b => b.classList.remove('active'));
          document.querySelectorAll('.pomo-mode-btn')[0].classList.add('active');
          setPomoModeSilent('work', 25);
        }
        // 振动反馈
        if (navigator.vibrate) navigator.vibrate([200, 100, 200]);
      }
      updatePomoDisplay();
    }, 1000);
  }
}
function setPomoModeSilent(mode, min) {
  pomoMode = mode; pomoDuration = min * 60; pomoRemain = min * 60;
  document.getElementById('pomo-toggle').textContent = '开始';
  updatePomoDisplay();
  document.getElementById('pomo-phase').textContent = mode === 'work' ? '准备开始专注' : mode === 'short' ? '准备短休' : '准备长休';
}
function resetPomo() {
  if (pomoRunning) { clearInterval(pomoTimer); pomoRunning = false; }
  pomoRemain = pomoDuration;
  document.getElementById('pomo-toggle').textContent = '开始';
  updatePomoDisplay();
  document.getElementById('pomo-phase').textContent = pomoMode === 'work' ? '准备开始专注' : pomoMode === 'short' ? '准备短休' : '准备长休';
}

// ===== 颜色取色器 =====
const COLOR_PRESETS = ['#EF4444','#F59E0B','#FBBF24','#10B981','#06B6D4','#3B82F6','#6366F1','#8B5CF6','#EC4899','#000000','#FFFFFF','#6B7280','#F5F7FA','#1A1D29','#84CC16','#14B8A6'];
function initColorPresets() {
  document.getElementById('color-presets').innerHTML = COLOR_PRESETS.map(c =>
    `<div class="color-preset" style="background:${c}" onclick="onColorPick('${c}')"></div>`
  ).join('');
}
function onColorPick(hex) {
  document.getElementById('color-picker').value = hex;
  document.getElementById('color-hex-input').value = hex.toUpperCase();
  updateColorInfo(hex);
}
function onHexInput(val) {
  if (/^#?[0-9A-Fa-f]{6}$/.test(val)) {
    const hex = val.startsWith('#') ? val : '#' + val;
    document.getElementById('color-picker').value = hex;
    updateColorInfo(hex);
  }
}
function updateColorInfo(hex) {
  const r = parseInt(hex.substr(1,2), 16);
  const g = parseInt(hex.substr(3,2), 16);
  const b = parseInt(hex.substr(5,2), 16);
  document.getElementById('color-preview').style.background = hex;
  document.getElementById('cp-hex').textContent = hex.toUpperCase();
  document.getElementById('cp-rgb').textContent = `RGB(${r}, ${g}, ${b})`;
  document.getElementById('ci-hex').textContent = hex.toUpperCase();
  document.getElementById('ci-rgb').textContent = `${r}, ${g}, ${b}`;
  // HSL
  const hsl = rgbToHsl(r, g, b);
  document.getElementById('ci-hsl').textContent = `${hsl.h}°, ${hsl.s}%, ${hsl.l}%`;
  // CMYK
  const cmyk = rgbToCmyk(r, g, b);
  document.getElementById('ci-cmyk').textContent = `${cmyk.c}%, ${cmyk.m}%, ${cmyk.y}%, ${cmyk.k}%`;
}
function rgbToHsl(r, g, b) {
  r /= 255; g /= 255; b /= 255;
  const max = Math.max(r,g,b), min = Math.min(r,g,b);
  let h, s, l = (max + min) / 2;
  if (max === min) { h = s = 0; }
  else {
    const d = max - min;
    s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
    switch(max) {
      case r: h = (g - b) / d + (g < b ? 6 : 0); break;
      case g: h = (b - r) / d + 2; break;
      case b: h = (r - g) / d + 4; break;
    }
    h /= 6;
  }
  return { h: Math.round(h * 360), s: Math.round(s * 100), l: Math.round(l * 100) };
}
function rgbToCmyk(r, g, b) {
  const rr = r / 255, gg = g / 255, bb = b / 255;
  const k = 1 - Math.max(rr, gg, bb);
  if (k === 1) return { c:0, m:0, y:0, k:100 };
  const c = (1 - rr - k) / (1 - k);
  const m = (1 - gg - k) / (1 - k);
  const y = (1 - bb - k) / (1 - k);
  return { c: Math.round(c*100), m: Math.round(m*100), y: Math.round(y*100), k: Math.round(k*100) };
}
function copyColor(type) {
  const hex = document.getElementById('ci-hex').textContent;
  const rgb = document.getElementById('ci-rgb').textContent;
  const text = type === 'hex' ? hex : `RGB(${rgb})`;
  navigator.clipboard.writeText(text).then(() => toast('已复制 ' + text)).catch(() => toast('复制失败'));
}

// ===== 设备信息 =====
function loadDeviceInfo() {
  // 屏幕
  document.getElementById('dev-res').textContent = `${screen.width} × ${screen.height}`;
  const diag = Math.sqrt(screen.width**2 + screen.height**2) / (window.devicePixelRatio || 1);
  document.getElementById('dev-size').textContent = diag > 0 ? `${(diag / 96).toFixed(1)} 英寸（估算）` : '未知';
  document.getElementById('dev-dpr').textContent = String(window.devicePixelRatio || 1);
  document.getElementById('dev-depth').textContent = `${screen.colorDepth || 24} 位`;
  // 浏览器
  document.getElementById('dev-ua').textContent = navigator.userAgent.substring(0, 80) + '…';
  document.getElementById('dev-platform').textContent = navigator.platform || '未知';
  document.getElementById('dev-lang').textContent = navigator.language || '未知';
  document.getElementById('dev-cookie').textContent = navigator.cookieEnabled ? '已启用' : '未启用';
  document.getElementById('dev-online').textContent = navigator.onLine ? '在线' : '离线';
  // 网络
  const conn = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
  if (conn) {
    document.getElementById('dev-conn').textContent = conn.effectiveType || '未知';
    document.getElementById('dev-downlink').textContent = conn.downlink ? `${conn.downlink} Mbps` : '未知';
    document.getElementById('dev-rtt').textContent = conn.rtt ? `${conn.rtt} ms` : '未知';
  } else {
    document.getElementById('dev-conn').textContent = '不支持';
    document.getElementById('dev-downlink').textContent = '不支持';
    document.getElementById('dev-rtt').textContent = '不支持';
  }
  // 存储
  document.getElementById('dev-cpu').textContent = navigator.hardwareConcurrency ? `${navigator.hardwareConcurrency} 核` : '未知';
  if (navigator.deviceMemory) {
    document.getElementById('dev-mem').textContent = `${navigator.deviceMemory} GB`;
  } else {
    document.getElementById('dev-mem').textContent = '不支持';
  }
  document.getElementById('dev-touch').textContent = ('ontouchstart' in window) ? '支持' : '不支持';
  // 电池
  if (navigator.getBattery) {
    navigator.getBattery().then(b => {
      const pct = Math.round(b.level * 100);
      document.getElementById('dev-battery').textContent = `${pct}%`;
      const fill = document.getElementById('dev-battery-fill');
      fill.style.width = pct + '%';
      fill.className = 'dev-battery-fill' + (pct < 20 ? ' critical' : pct < 50 ? ' low' : '');
      document.getElementById('dev-charging').textContent = b.charging ? '充电中' : '使用电池';
      b.addEventListener('levelchange', () => {
        const p = Math.round(b.level * 100);
        document.getElementById('dev-battery').textContent = `${p}%`;
        document.getElementById('dev-battery-fill').style.width = p + '%';
      });
      b.addEventListener('chargingchange', () => {
        document.getElementById('dev-charging').textContent = b.charging ? '充电中' : '使用电池';
      });
    }).catch(() => {
      document.getElementById('dev-battery').textContent = '不支持';
      document.getElementById('dev-charging').textContent = '不支持';
    });
  } else {
    document.getElementById('dev-battery').textContent = '不支持';
    document.getElementById('dev-charging').textContent = '不支持';
  }
}

// 初始化新工具
loadWallpapers();
initConvTabs();
initColorPresets();
renderQRHistory();
renderSpeedHistory();
updatePomoDisplay();
// 设备信息延迟加载（进入页面时再读）
document.addEventListener('click', e => {
  if (e.target.closest('[onclick*="go(\'device\')"]')) {
    setTimeout(loadDeviceInfo, 100);
  }
});
</script>
</body>
</html>
# -
aaa
