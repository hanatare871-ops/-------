
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>競技かるた 対戦組</title>
<style>
:root{
  --ai:#22335C;        /* 藍 */
  --ai-deep:#16223F;
  --sumi:#2B2B30;      /* 墨 */
  --kami:#FAFAF7;      /* 紙 */
  --usuzumi:#8A8A93;
  --line:#E3E2DC;
  --aka:#B3342E;       /* 緋 — 競技線・警告のみ */
  --tatami:#5E7355;    /* 畳 — 成立・希望 */
  --card:#FFFFFF;
  --radius:10px;
  --serif:"Shippori Mincho","Hiragino Mincho ProN","Yu Mincho","Noto Serif JP",serif;
  --sans:"Hiragino Kaku Gothic ProN","Yu Gothic","Noto Sans JP",sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:var(--sans);background:var(--kami);color:var(--sumi);line-height:1.6;-webkit-font-smoothing:antialiased}
header{background:var(--ai-deep);color:#F4F3EE;padding:26px 20px 22px;position:relative;overflow:hidden}
header::after{content:"";position:absolute;inset:0;background:repeating-linear-gradient(90deg,transparent 0 46px,rgba(255,255,255,.035) 46px 47px);pointer-events:none}
.header-inner{max-width:860px;margin:0 auto;display:flex;align-items:baseline;gap:14px;flex-wrap:wrap}
h1{font-family:var(--serif);font-size:26px;font-weight:600;letter-spacing:.14em}
.header-sub{font-size:12.5px;color:#B9BFCE;letter-spacing:.06em}
main{max-width:860px;margin:0 auto;padding:20px 16px 80px}
section{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);margin-bottom:18px;overflow:hidden}
.sec-head{display:flex;align-items:center;gap:10px;padding:13px 18px;border-bottom:1px solid var(--line)}
.sec-head h2{font-family:var(--serif);font-size:16.5px;font-weight:600;letter-spacing:.1em;color:var(--ai)}
.sec-tag{writing-mode:vertical-rl;font-family:var(--serif);font-size:10px;letter-spacing:.25em;color:#fff;background:var(--ai);padding:6px 3px;border-radius:3px;line-height:1;min-height:44px;text-align:center;flex:none}
.sec-body{padding:16px 18px}
.usage{
  background:#F4F5F8;border-left:3px solid var(--ai);
  font-size:12.5px;color:#4C4C55;
  padding:8px 12px;border-radius:0 6px 6px 0;margin-bottom:14px;
}
.usage b{color:var(--ai)}
.row{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
input[type=text],input[type=number],select,textarea{font-family:var(--sans);font-size:15px;padding:9px 11px;border:1px solid #CFCEC7;border-radius:7px;background:#fff;color:var(--sumi)}
input[type=text]:focus,input[type=number]:focus,select:focus,textarea:focus,button:focus-visible{outline:2px solid var(--ai);outline-offset:1px}
textarea{width:100%;resize:vertical}
button{font-family:var(--sans);font-size:14.5px;font-weight:600;padding:9px 16px;border:none;border-radius:7px;cursor:pointer;background:var(--ai);color:#fff;letter-spacing:.04em;transition:filter .12s}
button:hover{filter:brightness(1.15)}
button.ghost{background:#fff;color:var(--ai);border:1px solid var(--ai)}
button.small{font-size:12.5px;padding:5px 10px}
button.danger-ghost{background:#fff;color:var(--aka);border:1px solid var(--aka)}
button:disabled{opacity:.6;cursor:default}
.hint{font-size:12px;color:var(--usuzumi);margin-top:6px}
.muted{color:var(--usuzumi)}

/* 選手一覧 */
.rank-group{margin-top:14px}
.rank-group-title{font-size:12.5px;font-weight:700;color:var(--ai);letter-spacing:.08em;margin-bottom:6px;display:flex;align-items:center;gap:8px}
.rank-group-title .cnt{font-weight:400;color:var(--usuzumi)}
.chips{display:flex;flex-wrap:wrap;gap:7px}
.chip{display:inline-flex;align-items:center;gap:6px;background:#F2F2ED;border:1px solid var(--line);border-radius:999px;padding:5px 6px 5px 12px;font-size:14px}
.chip .x{width:20px;height:20px;border-radius:50%;background:#DDDCD5;color:#66666E;border:none;padding:0;font-size:12px;line-height:1;display:flex;align-items:center;justify-content:center}
.chip .x:hover{background:var(--aka);color:#fff;filter:none}
.rank-badge{font-family:var(--serif);font-weight:700;font-size:11.5px;color:#fff;border-radius:4px;padding:1px 6px;letter-spacing:.02em;flex:none;white-space:nowrap}
.rank-Ap{background:#0F1B33}.rank-A{background:#22335C}
.rank-Bp{background:#2C4270}.rank-B{background:#3C5488}
.rank-Cp{background:#47603F}.rank-C{background:#5E7355}
.rank-Dp{background:#7D6330}.rank-D{background:#9A7B3F}
.rank-Ep{background:#6E6E77}.rank-E{background:#8A8A93}
.attr-tag{font-size:10.5px;font-weight:700;border-radius:4px;padding:0 5px;flex:none}
.attr-現役{background:#E8EEF7;color:#2C4270;border:1px solid #C4D2E6}
.attr-OBOG{background:#F1EBDD;color:#7D6330;border:1px solid #E0D3B4}

/* 希望・NGリスト */
.req-list{margin-top:12px;display:flex;flex-direction:column;gap:6px}
.req-item{display:flex;align-items:center;gap:10px;background:#F5F7F3;border:1px solid #DDE4D8;border-radius:7px;padding:7px 12px;font-size:14px}
.req-item .vs{font-family:var(--serif);color:var(--tatami);font-weight:700}
.req-item.ng{background:#FAF1F0;border-color:#E7C8C5}
.req-item.ng .vs{color:var(--aka)}

/* 抜け番 */
.bye-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(190px,1fr));gap:9px;margin-top:4px}
.bye-cell{display:flex;align-items:center;gap:8px;font-size:13.5px}
.bye-cell label{white-space:nowrap;color:var(--ai);font-weight:600}
.bye-cell select{flex:1;min-width:0;font-size:13.5px;padding:6px 8px}
.bye-cell .fixed-mark{color:var(--usuzumi);font-size:12.5px}

/* 確定バナー */
.fixed-banner{background:#EEF1F7;border:1px solid #C9D2E4;color:var(--ai);border-radius:7px;padding:9px 13px;font-size:13.5px;margin-bottom:14px;display:flex;align-items:center;gap:10px;flex-wrap:wrap}

/* 生成ボタン帯 */
.generate-bar{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;margin:6px 0 20px;align-items:center}
.generate-bar button.main-gen{font-size:16px;padding:13px 34px;letter-spacing:.12em}

/* 結果 */
.round-card{margin-bottom:16px}
.round-head{display:flex;align-items:baseline;gap:12px;flex-wrap:wrap;padding:12px 18px;border-bottom:1px solid var(--line);background:linear-gradient(#fff,#FAFAF6)}
.round-head h3{font-family:var(--serif);font-size:17px;color:var(--ai);letter-spacing:.12em}
.round-head .fixed-tag{font-size:11px;font-weight:700;color:#fff;background:var(--usuzumi);border-radius:4px;padding:1px 8px}
.bye-note{font-size:12.5px;color:var(--usuzumi)}
.bye-note b{color:var(--sumi)}
.matches{padding:10px 14px 14px}
.match{display:grid;grid-template-columns:1fr 34px 1fr;align-items:stretch;gap:0;margin:8px 0}
.player-card{background:#FFFFFE;border:1px solid #D8D7D0;border-radius:8px;padding:9px 12px;display:flex;align-items:center;gap:8px;min-height:48px;box-shadow:0 1px 2px rgba(30,35,60,.06)}
.player-card.right{flex-direction:row-reverse;text-align:right}
.player-card .name{font-family:var(--serif);font-size:16px;font-weight:600;overflow-wrap:anywhere}
.center-line{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:2px;position:relative}
.center-line::before{content:"";position:absolute;top:4px;bottom:4px;left:50%;width:2px;background:var(--aka);border-radius:1px;transform:translateX(-50%)}
.center-line span{position:relative;background:var(--kami);font-family:var(--serif);font-size:10px;color:var(--aka);writing-mode:vertical-rl;letter-spacing:.2em;padding:2px 0}
.match-flags{grid-column:1 / -1;display:flex;gap:8px;margin-top:3px;flex-wrap:wrap}
.flag{font-size:11.5px;border-radius:4px;padding:1px 8px;font-weight:600}
.flag.wish{background:#EAF0E6;color:var(--tatami);border:1px solid #C9D6C1}
.flag.cross{background:#F4EFE4;color:#8A6B2C;border:1px solid #E0D3B4}
.flag.repeat{background:#F9E9E8;color:var(--aka);border:1px solid #E7BEBB}
.flag.obog{background:#E8EEF7;color:#2C4270;border:1px solid #C4D2E6}

/* 集計 */
.summary-table{width:100%;border-collapse:collapse;font-size:13.5px;margin-top:4px}
.summary-table th,.summary-table td{border-bottom:1px solid var(--line);padding:7px 8px;text-align:left;vertical-align:top}
.summary-table th{color:var(--ai);font-size:12.5px;letter-spacing:.05em;white-space:nowrap}
.summary-table td.opps{color:#4A4A52}
.empty-note{color:var(--usuzumi);font-size:13.5px;padding:6px 2px}
.warn-banner{background:#F9E9E8;border:1px solid #E7BEBB;color:var(--aka);border-radius:7px;padding:9px 13px;font-size:13.5px;margin-bottom:12px}
.ok-banner{background:#EAF0E6;border:1px solid #C9D6C1;color:#3E5236;border-radius:7px;padding:9px 13px;font-size:13.5px;margin-bottom:12px}

@media (max-width:560px){
  .match{grid-template-columns:1fr 26px 1fr}
  .player-card .name{font-size:14.5px}
  h1{font-size:21px}
}
@media print{
  header,#setup-area,.generate-bar,.no-print{display:none !important}
  body{background:#fff}
  main{padding:0;max-width:none}
  section{border:none;box-shadow:none;break-inside:avoid}
  .player-card{box-shadow:none}
}
</style>
</head>
<body>
<header>
  <div class="header-inner">
    <h1>競技かるた 対戦組</h1>
    <div class="header-sub">同級優先・再戦回避の組み合わせを自動作成</div>
  </div>
</header>
<main>

<div id="fixed-banner-area"></div>

<div id="setup-area">

<!-- 選手登録 -->
<section>
  <div class="sec-head"><span class="sec-tag">選手</span><h2>選手登録</h2></div>
  <div class="sec-body">
    <div class="usage"><b>使い方</b>:名前と級を選んで「追加」。複数人まとめて入れるなら「まとめて追加」で名前を並べて書き、級を1回選ぶだけ。属性(現役/OBOG)はOBOG会モード用で、普段は「なし」のままでOK。名前の×で削除できます。</div>
    <div class="row">
      <input type="text" id="name-input" placeholder="名前" style="flex:1;min-width:120px" maxlength="20">
      <select id="rank-input"></select>
      <select id="attr-input">
        <option value="">属性なし</option>
        <option value="現役">現役</option>
        <option value="OBOG">OBOG</option>
      </select>
      <button id="add-player-btn">追加</button>
      <button class="ghost" id="toggle-bulk-btn">まとめて追加</button>
    </div>
    <div id="bulk-area" style="display:none;margin-top:10px">
      <textarea id="bulk-input" rows="4" placeholder="名前をスペース・「、」・「,」・改行のどれかで区切って入力&#10;例) 佐藤 鈴木 田中、高橋,伊藤"></textarea>
      <div class="row" style="margin-top:8px">
        <span class="muted" style="font-size:13px">全員の級:</span>
        <select id="bulk-rank"></select>
        <span class="muted" style="font-size:13px">属性:</span>
        <select id="bulk-attr">
          <option value="">なし</option>
          <option value="現役">現役</option>
          <option value="OBOG">OBOG</option>
        </select>
        <button id="bulk-add-btn">一括登録</button>
      </div>
      <div class="hint">書いた名前全員が、ここで選んだ級・属性で登録されます。級ごとに繰り返し使ってください。</div>
    </div>
    <div id="player-list"></div>
    <div class="row" style="margin-top:14px;justify-content:space-between">
      <span class="hint" id="player-count">登録 0名</span>
      <span>
        <button class="ghost small" id="sample-btn">サンプル投入</button>
        <button class="danger-ghost small" id="clear-players-btn">全削除</button>
      </span>
    </div>
  </div>
</section>

<!-- 設定 -->
<section>
  <div class="sec-head"><span class="sec-tag">設定</span><h2>試合設定</h2></div>
  <div class="sec-body">
    <div class="usage"><b>使い方</b>:試合数を決め、必要なら「対戦希望」(当てたい2人)と「対戦NG」(当てたくない2人)を追加。人数が奇数のときは試合ごとの抜け番も指定できます(「自動」なら均等に回ります)。</div>
    <div class="row">
      <label for="rounds-input" style="font-weight:600;color:var(--ai)">試合数</label>
      <input type="number" id="rounds-input" min="1" max="20" value="3" style="width:80px">
      <span class="hint">1人あたりの試合数(=回戦数)です。</span>
    </div>

    <div class="row" style="margin-top:16px">
      <label style="display:flex;align-items:center;gap:8px;font-weight:600;color:var(--ai);cursor:pointer">
        <input type="checkbox" id="obog-mode" style="width:17px;height:17px">
        OBOG会モード
      </label>
      <span class="hint" style="margin-top:0">「違う属性×同じ級」を最優先に組みます。難しい場合は級より属性違いを優先。属性なしの人は通常通り。</span>
    </div>

    <div style="margin-top:18px">
      <div style="font-weight:600;color:var(--ai);margin-bottom:6px">対戦希望</div>
      <div class="row">
        <select id="req-a"></select>
        <span class="muted">と</span>
        <select id="req-b"></select>
        <button class="small" id="add-req-btn">希望を追加</button>
      </div>
      <div class="hint">指定した2人が、いずれかの試合で当たるように優先して組みます。</div>
      <div class="req-list" id="req-list"></div>
    </div>

    <div style="margin-top:18px">
      <div style="font-weight:600;color:var(--aka);margin-bottom:6px">対戦NG</div>
      <div class="row">
        <select id="ng-a"></select>
        <span class="muted">と</span>
        <select id="ng-b"></select>
        <button class="small" id="add-ng-btn" style="background:var(--aka)">NGを追加</button>
      </div>
      <div class="hint">指定した2人が当たらないように組みます。</div>
      <div class="req-list" id="ng-list"></div>
    </div>

    <div style="margin-top:18px" id="bye-section">
      <div style="font-weight:600;color:var(--ai);margin-bottom:6px">抜け番の指定 <span class="hint" style="display:inline">(人数が奇数のとき)</span></div>
      <div id="bye-config"></div>
    </div>
  </div>
</section>

<!-- 履歴・データ -->
<section>
  <div class="sec-head"><span class="sec-tag">記録</span><h2>対戦履歴とデータ</h2></div>
  <div class="sec-body">
    <div class="usage"><b>使い方</b>:練習の最後に結果下の「履歴に保存」を押すと対戦が記録され、次回は過去に当たった相手を避けて組めます。メンバーや設定はこの端末に自動保存。別の端末に移すときは「ファイルに書き出し」→相手側で「読み込み」。</div>
    <div class="row" style="justify-content:space-between">
      <label style="display:flex;align-items:center;gap:8px;font-weight:600;color:var(--ai);cursor:pointer">
        <input type="checkbox" id="use-history" checked style="width:17px;height:17px">
        過去の練習の対戦も避けて組む
      </label>
      <span class="hint" id="history-count" style="margin-top:0">記録済み 0件</span>
    </div>
    <div class="row" style="margin-top:12px">
      <button class="ghost small" id="export-btn">ファイルに書き出し</button>
      <button class="ghost small" id="import-btn">ファイルから読み込み</button>
      <input type="file" id="import-file" accept=".json,application/json" style="display:none">
      <button class="danger-ghost small" id="clear-history-btn">履歴を全消去</button>
    </div>
  </div>
</section>

</div><!-- /setup-area -->

<div class="generate-bar">
  <button id="generate-btn" class="main-gen">組み合わせを作成</button>
  <button class="ghost" id="regen-btn" style="display:none">別の組み合わせで再作成</button>
  <button class="ghost no-print" id="print-btn" style="display:none">印刷</button>
</div>

<div id="results"></div>

</main>

<script>
"use strict";
/* ============ 定数・状態 ============ */
const RANKS = ["A+","A","B+","B","C+","C","D+","D","E+","E"]; // 強い順
const STORE_KEY = "karuta_pairing_v2";
let players = [];          // {id, name, rank, attr}  attr: "" | "現役" | "OBOG"
let requests = [];         // {aId, bId} 対戦希望
let ngPairs = [];          // {aId, bId} 対戦NG
let nextId = 1;
let lastResult = null;
let history = {pairs: {}, byes: {}};   // 名前ベースで永続化
let fixedRounds = [];      // 確定済みの回戦 [{round, bye:{name,rank,attr}|null, pairs:[[snap,snap],...]}]
let storageOk = true;

/* ============ ユーティリティ ============ */
const $ = id => document.getElementById(id);
const esc = s => String(s).replace(/[&<>"']/g, c => ({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));
const nameKey = (x, y) => x < y ? x + "|" + y : y + "|" + x;
const rankIdx = r => RANKS.indexOf(r);
const rankClass = r => "rank-" + r.replace("+", "p");
const byId = id => players.find(p => p.id === id);
const useHistory = () => $("use-history").checked;
const obogMode = () => $("obog-mode").checked;
const snap = p => ({name: p.name, rank: p.rank, attr: p.attr || ""});
const badge = p => '<span class="rank-badge ' + rankClass(p.rank) + '">' + esc(p.rank) + '</span>';
const attrTag = p => p.attr ? '<span class="attr-tag attr-' + p.attr + '">' + (p.attr === "OBOG" ? "OB" : p.attr) + '</span>' : '';
const rankOptions = () => RANKS.map(r => '<option value="' + r + '"' + (r === "C" ? " selected" : "") + '>' + r + '級</option>').join("");

/* ============ 保存と復元 ============ */
function saveState(){
  if(!storageOk) return;
  try{
    localStorage.setItem(STORE_KEY, JSON.stringify({
      players, requests, ngPairs, nextId, history, fixedRounds,
      rounds: $("rounds-input").value,
      useHistory: $("use-history").checked,
      obogMode: $("obog-mode").checked
    }));
  }catch(e){ storageOk = false; }
}
function applyData(d){
  players = (d.players || []).filter(p => p && p.name && RANKS.includes(p.rank))
    .map(p => ({id: p.id, name: p.name, rank: p.rank, attr: p.attr || ""}));
  requests = (d.requests || []).filter(r => byId(r.aId) && byId(r.bId));
  ngPairs = (d.ngPairs || []).filter(r => byId(r.aId) && byId(r.bId));
  nextId = typeof d.nextId === "number" ? d.nextId : Math.max(0, ...players.map(p => p.id)) + 1;
  history = (d.history && d.history.pairs) ? d.history : {pairs: {}, byes: {}};
  fixedRounds = Array.isArray(d.fixedRounds) ? d.fixedRounds : [];
  if(d.rounds) $("rounds-input").value = d.rounds;
  if(typeof d.useHistory === "boolean") $("use-history").checked = d.useHistory;
  if(typeof d.obogMode === "boolean") $("obog-mode").checked = d.obogMode;
}
function loadState(){
  try{
    const raw = localStorage.getItem(STORE_KEY);
    if(raw) applyData(JSON.parse(raw));
  }catch(e){ /* 壊れたデータは無視 */ }
}
function historyPairCount(){
  return Object.values(history.pairs).reduce((s, v) => s + v, 0);
}
function renderHistoryCount(){
  $("history-count").textContent = "記録済み " + historyPairCount() + "件" + (storageOk ? "" : "(この環境では自動保存不可)");
}

/* ============ 選手登録 ============ */
function addPlayer(name, rank, attr){
  name = name.trim();
  if(!name) return false;
  if(players.some(p => p.name === name)){
    alert("「" + name + "」は既に登録されています。同名の場合は「佐藤2」のように区別してください。");
    return false;
  }
  players.push({id: nextId++, name, rank: RANKS.includes(rank) ? rank : "C", attr: attr || ""});
  return true;
}
function removePlayer(id){
  players = players.filter(p => p.id !== id);
  requests = requests.filter(r => r.aId !== id && r.bId !== id);
  ngPairs = ngPairs.filter(r => r.aId !== id && r.bId !== id);
  renderAll();
}
function renderPlayers(){
  const wrap = $("player-list");
  wrap.innerHTML = "";
  RANKS.forEach(rank => {
    const group = players.filter(p => p.rank === rank);
    if(!group.length) return;
    const div = document.createElement("div");
    div.className = "rank-group";
    div.innerHTML =
      '<div class="rank-group-title"><span class="rank-badge ' + rankClass(rank) + '">' + esc(rank) + '級</span>' +
      '<span class="cnt">' + group.length + '名</span></div>' +
      '<div class="chips">' +
      group.map(p =>
        '<span class="chip">' + esc(p.name) + attrTag(p) +
        '<button class="x" data-del="' + p.id + '" aria-label="' + esc(p.name) + 'を削除">×</button></span>'
      ).join("") + '</div>';
    wrap.appendChild(div);
  });
  wrap.querySelectorAll("[data-del]").forEach(b =>
    b.addEventListener("click", () => removePlayer(+b.dataset.del)));
  $("player-count").textContent = "登録 " + players.length + "名" +
    (players.length % 2 === 1 && players.length > 0 ? "(奇数:毎試合1名が抜け番)" : "");
}

/* ============ 希望・NG ============ */
function renderPairSelects(){
  ["req-a","req-b","ng-a","ng-b"].forEach(id => {
    const sel = $(id);
    const cur = sel.value;
    sel.innerHTML = players.map(p =>
      '<option value="' + p.id + '">' + esc(p.name) + '(' + esc(p.rank) + ')</option>').join("");
    if(players.some(p => String(p.id) === cur)) sel.value = cur;
  });
}
function renderPairList(listId, arr, isNg){
  const wrap = $(listId);
  wrap.innerHTML = "";
  arr.forEach((r, i) => {
    const a = byId(r.aId), b = byId(r.bId);
    if(!a || !b) return;
    const div = document.createElement("div");
    div.className = "req-item" + (isNg ? " ng" : "");
    div.innerHTML = esc(a.name) + '(' + esc(a.rank) + ') <span class="vs">' + (isNg ? "×" : "対") + '</span> ' +
      esc(b.name) + '(' + esc(b.rank) + ')' +
      '<button class="x small danger-ghost" style="margin-left:auto" data-i="' + i + '">削除</button>';
    wrap.appendChild(div);
  });
  wrap.querySelectorAll("[data-i]").forEach(b =>
    b.addEventListener("click", () => { arr.splice(+b.dataset.i, 1); renderAll(); }));
}
function addPairTo(arr, otherArr, aId, bId, label, otherLabel){
  if(!aId || !bId) return;
  if(aId === bId){ alert("同じ選手同士は指定できません。"); return; }
  const k = nameKey(String(aId), String(bId));
  if(arr.some(r => nameKey(String(r.aId), String(r.bId)) === k)){
    alert("この組み合わせは既に" + label + "に入っています。"); return;
  }
  if(otherArr.some(r => nameKey(String(r.aId), String(r.bId)) === k)){
    alert("この組み合わせは" + otherLabel + "に入っています。先にそちらを削除してください。"); return;
  }
  arr.push({aId, bId});
  renderAll();
}

/* ============ 抜け番設定 ============ */
function renderByeConfig(){
  const wrap = $("bye-config");
  const rounds = clampRounds();
  if(players.length % 2 === 0 || players.length === 0){
    wrap.innerHTML = '<div class="empty-note">現在の人数は' +
      (players.length ? '偶数(' + players.length + '名)のため抜け番はありません。' : '0名です。選手を登録してください。') + '</div>';
    return;
  }
  const prev = {};
  wrap.querySelectorAll("select[data-round]").forEach(s => prev[s.dataset.round] = s.value);
  let html = '<div class="bye-grid">';
  for(let r = 1; r <= rounds; r++){
    if(r <= fixedRounds.length){
      const f = fixedRounds[r - 1];
      html += '<div class="bye-cell"><label>第' + r + '試合</label><span class="fixed-mark">確定済み' +
        (f.bye ? '(抜け:' + esc(f.bye.name) + ')' : '') + '</span></div>';
    }else{
      html += '<div class="bye-cell"><label for="bye-r' + r + '">第' + r + '試合</label>' +
        '<select id="bye-r' + r + '" data-round="' + r + '"><option value="auto">自動(均等に)</option>' +
        players.map(p => '<option value="' + p.id + '">' + esc(p.name) + '(' + esc(p.rank) + ')</option>').join("") +
        '</select></div>';
    }
  }
  html += '</div><div class="hint">「自動」は抜け回数が少ない人から順に抜け番になります。</div>';
  wrap.innerHTML = html;
  wrap.querySelectorAll("select[data-round]").forEach(s => {
    const v = prev[s.dataset.round];
    if(v && [...s.options].some(o => o.value === v)) s.value = v;
  });
}
function clampRounds(){
  let v = parseInt($("rounds-input").value, 10);
  if(isNaN(v) || v < 1) v = 1;
  if(v > 20) v = 20;
  return v;
}

/* ============ 確定(途中からの組み直し) ============ */
function renderFixedBanner(){
  const wrap = $("fixed-banner-area");
  if(!fixedRounds.length){ wrap.innerHTML = ""; return; }
  wrap.innerHTML = '<div class="fixed-banner">第' + fixedRounds.length + '試合まで確定済みです。' +
    'メンバーや設定を変更して「組み合わせを作成」を押すと、第' + (fixedRounds.length + 1) +
    '試合以降だけが組み直されます(確定分との再戦は避けます)。' +
    '<button class="ghost small" id="unfix-btn">確定を解除</button></div>';
  $("unfix-btn").addEventListener("click", () => {
    if(confirm("確定を解除しますか?次回の作成では全試合が組み直されます。")){
      fixedRounds = [];
      renderAll();
    }
  });
}
function fixUpTo(n){
  if(!lastResult) return;
  fixedRounds = lastResult.schedule.slice(0, n).map(rd => ({
    round: rd.round,
    bye: rd.bye ? snap(rd.bye) : null,
    pairs: rd.pairs.map(([a, b]) => [snap(a), snap(b)])
  }));
  renderAll();
  window.scrollTo({top: 0, behavior: "smooth"});
}

/* ============ 組み合わせアルゴリズム ============ */
function buildNgSet(){
  const s = new Set();
  ngPairs.forEach(r => {
    const a = byId(r.aId), b = byId(r.bId);
    if(a && b) s.add(nameKey(a.name, b.name));
  });
  return s;
}
function pairCost(a, b, played, pendingReqs, ngSet){
  let c = 0;
  const k = nameKey(a.name, b.name);
  if(ngSet.has(k)) c += 2000000;                     // NGは最重(事実上組まない)
  c += (played[k] || 0) * 100000;                    // 同日・確定分との再戦
  if(useHistory()) c += (history.pairs[k] || 0) * 60000;  // 過去の練習での対戦
  if(obogMode() && a.attr && b.attr && a.attr === b.attr)
    c += 10000;                                      // OBOG会モード: 同属性ペナルティ(級差より重い)
  const d = Math.abs(rankIdx(a.rank) - rankIdx(b.rank));
  c += d * d * 100;                                  // 級差ペナルティ(近い級を優先)
  if(pendingReqs.some(q => !q.done && nameKey(q.aName, q.bName) === k))
    c -= 50000;                                      // 未消化の対戦希望は強く優先
  return c;
}
function greedyMatch(avail, played, reqs, ngSet){
  const pool = avail.slice();
  for(let i = pool.length - 1; i > 0; i--){
    const j = Math.floor(Math.random() * (i + 1));
    [pool[i], pool[j]] = [pool[j], pool[i]];
  }
  const pairs = [];
  // 未消化の希望ペアを初期配置で先に組む(NG・再戦でない場合のみ。不利なら後の最適化で解消される)
  reqs.filter(q => !q.done).forEach(q => {
    const i = pool.findIndex(p => p.name === q.aName);
    const j = pool.findIndex(p => p.name === q.bName);
    if(i < 0 || j < 0) return;
    const k = nameKey(q.aName, q.bName);
    if(ngSet.has(k) || (played[k] || 0) > 0) return;
    const a = pool[i], b = pool[j];
    pool.splice(Math.max(i, j), 1);
    pool.splice(Math.min(i, j), 1);
    pairs.push([a, b]);
  });
  while(pool.length){
    const a = pool.shift();
    let bestI = 0, bestC = Infinity;
    for(let i = 0; i < pool.length; i++){
      const c = pairCost(a, pool[i], played, reqs, ngSet);
      if(c < bestC){ bestC = c; bestI = i; }
    }
    pairs.push([a, pool.splice(bestI, 1)[0]]);
  }
  return pairs;
}
function improve(pairs, played, reqs, ngSet){
  let improved = true, guard = 0;
  while(improved && guard++ < 200){
    improved = false;
    for(let i = 0; i < pairs.length; i++){
      for(let j = i + 1; j < pairs.length; j++){
        const [a, b] = pairs[i], [c, d] = pairs[j];
        const cur = pairCost(a, b, played, reqs, ngSet) + pairCost(c, d, played, reqs, ngSet);
        const alt1 = pairCost(a, c, played, reqs, ngSet) + pairCost(b, d, played, reqs, ngSet);
        const alt2 = pairCost(a, d, played, reqs, ngSet) + pairCost(b, c, played, reqs, ngSet);
        if(alt1 < cur && alt1 <= alt2){
          pairs[i] = [a, c]; pairs[j] = [b, d]; improved = true;
        }else if(alt2 < cur){
          pairs[i] = [a, d]; pairs[j] = [b, c]; improved = true;
        }
      }
    }
  }
  return pairs;
}
function bestMatching(avail, played, reqs, ngSet){
  let best = null, bestC = Infinity;
  const restarts = Math.min(40, 10 + avail.length);
  for(let k = 0; k < restarts; k++){
    let pairs = greedyMatch(avail, played, reqs, ngSet);
    pairs = improve(pairs, played, reqs, ngSet);
    const c = pairs.reduce((s, [a, b]) => s + pairCost(a, b, played, reqs, ngSet), 0);
    if(c < bestC){ bestC = c; best = pairs; }
  }
  return best || [];
}
function generateSchedule(){
  const rounds = clampRounds();
  const played = {};                 // nameKey → 回数(確定分を含む当日分)
  const byeCount = {};               // 名前 → 当日の抜け回数
  players.forEach(p => byeCount[p.name] = 0);
  const ngSet = buildNgSet();
  const pendingReqs = requests.map(r => {
    const a = byId(r.aId), b = byId(r.bId);
    return {aName: a.name, bName: b.name, done: false, round: null};
  });
  const schedule = [];

  // 確定済みの回戦を組み込む
  fixedRounds.forEach(f => {
    f.pairs.forEach(([a, b]) => {
      const k = nameKey(a.name, b.name);
      played[k] = (played[k] || 0) + 1;
      const q = pendingReqs.find(q => !q.done && nameKey(q.aName, q.bName) === k);
      if(q){ q.done = true; q.round = f.round; }
    });
    if(f.bye && byeCount[f.bye.name] !== undefined) byeCount[f.bye.name]++;
    schedule.push({round: f.round, bye: f.bye, pairs: f.pairs, fixed: true});
  });

  const odd = players.length % 2 === 1;
  for(let r = fixedRounds.length + 1; r <= rounds; r++){
    let bye = null;
    if(odd){
      const sel = document.querySelector('select[data-round="' + r + '"]');
      const choice = sel ? sel.value : "auto";
      const chosen = choice !== "auto" ? byId(+choice) : null;
      if(chosen){
        bye = chosen;
      }else{
        // 優先度: 当日の抜け回数 ≫ 未消化の希望を持つ選手は休ませない ≫ 過去の抜け回数
        const pendingNames = new Set();
        pendingReqs.filter(q => !q.done).forEach(q => { pendingNames.add(q.aName); pendingNames.add(q.bName); });
        const score = p => byeCount[p.name] * 100000 +
          (pendingNames.has(p.name) ? 1000 : 0) +
          (useHistory() ? (history.byes[p.name] || 0) : 0);
        const min = Math.min(...players.map(score));
        const cands = players.filter(p => score(p) === min);
        bye = cands[Math.floor(Math.random() * cands.length)];
      }
      byeCount[bye.name]++;
    }
    const avail = players.filter(p => !bye || p.id !== bye.id);
    const pairs = bestMatching(avail, played, pendingReqs, ngSet);
    pairs.forEach(([a, b]) => {
      const k = nameKey(a.name, b.name);
      played[k] = (played[k] || 0) + 1;
      const q = pendingReqs.find(q => !q.done && nameKey(q.aName, q.bName) === k);
      if(q){ q.done = true; q.round = r; }
    });
    schedule.push({round: r, bye: bye ? snap(bye) : null, pairs, fixed: false});
  }
  return {schedule, pendingReqs, ngSet};
}

/* ============ 結果表示 ============ */
function renderResults(result){
  const wrap = $("results");
  wrap.innerHTML = "";
  const seen = {};
  const unfulfilled = result.pendingReqs.filter(q => !q.done);
  const ngViolations = [];
  result.schedule.forEach(rd => rd.pairs.forEach(([a, b]) => {
    if(result.ngSet.has(nameKey(a.name, b.name))) ngViolations.push(a.name + "×" + b.name);
  }));

  let banner = "";
  if(ngViolations.length){
    banner += '<div class="warn-banner">対戦NGの組み合わせが避けられませんでした:' +
      ngViolations.map(esc).join("、") + '(人数や試合数の関係で他に組みようがない状態です)</div>';
  }
  if(requests.length){
    if(unfulfilled.length){
      banner += '<div class="warn-banner">消化できなかった対戦希望:' +
        unfulfilled.map(q => esc(q.aName) + '×' + esc(q.bName)).join("、") +
        '(試合数を増やすか、抜け番・NGの指定を見直してください)</div>';
    }else{
      banner += '<div class="ok-banner">対戦希望はすべて組み込みました(' + result.pendingReqs.length + '件)。</div>';
    }
  }
  wrap.insertAdjacentHTML("beforeend", banner);

  result.schedule.forEach(round => {
    const sec = document.createElement("section");
    sec.className = "round-card";
    let html = '<div class="round-head"><h3>第' + round.round + '試合</h3>' +
      (round.fixed ? '<span class="fixed-tag">確定</span>' : '') +
      (round.bye ? '<span class="bye-note">抜け番:<b>' + esc(round.bye.name) + '(' + esc(round.bye.rank) + ')</b></span>' : '') +
      '</div><div class="matches">';
    const sorted = round.pairs.slice().sort((p, q) =>
      Math.min(rankIdx(p[0].rank), rankIdx(p[1].rank)) - Math.min(rankIdx(q[0].rank), rankIdx(q[1].rank)));
    sorted.forEach(([a, b]) => {
      const k = nameKey(a.name, b.name);
      const isRepeat = (seen[k] || 0) >= 1;
      seen[k] = (seen[k] || 0) + 1;
      const pastRepeat = useHistory() && (history.pairs[k] || 0) >= 1;
      const isNg = result.ngSet.has(k);
      const isWish = result.pendingReqs.some(q => q.done && q.round === round.round && nameKey(q.aName, q.bName) === k);
      const cross = a.rank !== b.rank;
      const crossAttr = obogMode() && a.attr && b.attr && a.attr !== b.attr;
      let flags = "";
      if(isWish) flags += '<span class="flag wish">希望対戦</span>';
      if(crossAttr) flags += '<span class="flag obog">現役×OBOG</span>';
      if(cross) flags += '<span class="flag cross">' + esc(a.rank) + '級×' + esc(b.rank) + '級</span>';
      if(isNg) flags += '<span class="flag repeat">NG対戦(要確認)</span>';
      if(isRepeat) flags += '<span class="flag repeat">再戦</span>';
      else if(pastRepeat) flags += '<span class="flag repeat">過去に対戦あり</span>';
      html += '<div class="match">' +
        '<div class="player-card">' + badge(a) + '<span class="name">' + esc(a.name) + '</span>' + attrTag(a) + '</div>' +
        '<div class="center-line"><span>対</span></div>' +
        '<div class="player-card right">' + badge(b) + '<span class="name">' + esc(b.name) + '</span>' + attrTag(b) + '</div>' +
        (flags ? '<div class="match-flags">' + flags + '</div>' : '') +
        '</div>';
    });
    html += '</div>';
    sec.innerHTML = html;
    wrap.appendChild(sec);
  });

  // 選手別まとめ(現在登録中の選手のみ)
  const sec = document.createElement("section");
  let rows = "";
  players.slice().sort((a, b) => rankIdx(a.rank) - rankIdx(b.rank) || a.name.localeCompare(b.name, "ja"))
    .forEach(p => {
      const opps = [];
      result.schedule.forEach(rd => {
        if(rd.bye && rd.bye.name === p.name){ opps.push("第" + rd.round + ":抜け"); return; }
        const m = rd.pairs.find(([a, b]) => a.name === p.name || b.name === p.name);
        if(m){
          const o = m[0].name === p.name ? m[1] : m[0];
          opps.push("第" + rd.round + ":" + esc(o.name));
        }
      });
      rows += '<tr><td>' + badge(p) + ' ' + esc(p.name) + attrTag(p) + '</td>' +
        '<td class="opps">' + (opps.join(" / ") || "-") + '</td></tr>';
    });
  sec.innerHTML = '<div class="sec-head"><span class="sec-tag">一覧</span><h2>選手別の対戦一覧</h2></div>' +
    '<div class="sec-body" style="overflow-x:auto"><table class="summary-table">' +
    '<tr><th>選手</th><th>対戦相手</th></tr>' + rows + '</table></div>';
  wrap.appendChild(sec);

  // 操作バー: 確定 / 出力 / 履歴保存
  const bar = document.createElement("section");
  bar.className = "no-print";
  const opts = result.schedule.map(rd => '<option value="' + rd.round + '"' +
    (rd.round === fixedRounds.length && fixedRounds.length ? " selected" : "") + '>第' + rd.round + '試合まで</option>').join("");
  bar.innerHTML =
    '<div class="sec-head"><span class="sec-tag">操作</span><h2>この結果の確定・出力</h2></div>' +
    '<div class="sec-body">' +
    '<div class="usage"><b>使い方</b>:途中でメンバーが増減するときは、消化済みの試合を「確定」してから選手登録を変更し、もう一度「組み合わせを作成」を押してください。確定分はそのまま残り、続きだけが組み直されます。CSVはExcelやGoogleスプレッドシートでそのまま開けます。</div>' +
    '<div class="row"><select id="fix-upto">' + opts + '</select>' +
    '<button id="fix-btn">ここまで確定</button></div>' +
    '<div class="row" style="margin-top:12px">' +
    '<button class="ghost small" id="csv-btn">CSV出力(スプレッドシート用)</button>' +
    '<button class="ghost small" id="txt-btn">テキスト出力</button>' +
    '<button id="commit-btn" class="small" style="background:var(--tatami)">この結果を対戦履歴に保存</button>' +
    '</div>' +
    '<div class="hint">履歴への保存は、実際に使う組み合わせが決まったあと1日1回だけ押してください。</div>' +
    '</div>';
  wrap.appendChild(bar);
  $("fix-btn").addEventListener("click", () => {
    const n = +$("fix-upto").value;
    fixUpTo(n);
    alert("第" + n + "試合までを確定しました。メンバーを変更してから「組み合わせを作成」を押すと続きだけ組み直されます。");
  });
  $("csv-btn").addEventListener("click", () => exportCsv(result));
  $("txt-btn").addEventListener("click", () => exportTxt(result));
  $("commit-btn").addEventListener("click", () => {
    commitHistory(result);
    $("commit-btn").textContent = "履歴に保存しました";
    $("commit-btn").disabled = true;
  });

  $("regen-btn").style.display = "";
  $("print-btn").style.display = "";
  wrap.scrollIntoView({behavior: "smooth", block: "start"});
}

/* ============ CSV / テキスト出力 ============ */
function download(filename, content, mime){
  const blob = new Blob([content], {type: mime});
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = filename;
  a.click();
  URL.revokeObjectURL(a.href);
}
function stamp(){
  const d = new Date();
  return d.getFullYear() + String(d.getMonth() + 1).padStart(2, "0") + String(d.getDate()).padStart(2, "0");
}
function csvCell(s){
  s = String(s);
  return /[",\n]/.test(s) ? '"' + s.replace(/"/g, '""') + '"' : s;
}
function exportCsv(result){
  const rows = [["回戦","選手1","級1","属性1","選手2","級2","属性2","備考"]];
  result.schedule.forEach(rd => {
    rd.pairs.forEach(([a, b]) => {
      const k = nameKey(a.name, b.name);
      const memo = [];
      if(result.pendingReqs.some(q => q.done && q.round === rd.round && nameKey(q.aName, q.bName) === k)) memo.push("希望対戦");
      if(a.rank !== b.rank) memo.push("級またぎ");
      rows.push(["第" + rd.round + "試合", a.name, a.rank, a.attr || "", b.name, b.rank, b.attr || "", memo.join("・")]);
    });
    if(rd.bye) rows.push(["第" + rd.round + "試合", rd.bye.name, rd.bye.rank, rd.bye.attr || "", "", "", "", "抜け番"]);
  });
  const csv = "\uFEFF" + rows.map(r => r.map(csvCell).join(",")).join("\r\n");
  download("対戦組_" + stamp() + ".csv", csv, "text/csv;charset=utf-8");
}
function exportTxt(result){
  let out = "競技かるた 対戦組(" + new Date().toLocaleDateString("ja-JP") + ")\n";
  out += "=".repeat(30) + "\n";
  result.schedule.forEach(rd => {
    out += "\n【第" + rd.round + "試合】" + (rd.fixed ? "(確定済み)" : "") + "\n";
    rd.pairs.forEach(([a, b]) => {
      out += "  " + a.name + "(" + a.rank + ") 対 " + b.name + "(" + b.rank + ")\n";
    });
    if(rd.bye) out += "  抜け番: " + rd.bye.name + "(" + rd.bye.rank + ")\n";
  });
  download("対戦組_" + stamp() + ".txt", out, "text/plain;charset=utf-8");
}

/* ============ 履歴の確定と入出力 ============ */
function commitHistory(result){
  result.schedule.forEach(rd => {
    rd.pairs.forEach(([a, b]) => {
      const k = nameKey(a.name, b.name);
      history.pairs[k] = (history.pairs[k] || 0) + 1;
    });
    if(rd.bye) history.byes[rd.bye.name] = (history.byes[rd.bye.name] || 0) + 1;
  });
  saveState();
  renderHistoryCount();
}
$("export-btn").addEventListener("click", () => {
  const data = JSON.stringify({
    players, requests, ngPairs, nextId, history, fixedRounds,
    rounds: $("rounds-input").value,
    useHistory: $("use-history").checked,
    obogMode: $("obog-mode").checked,
    exportedAt: new Date().toISOString()
  }, null, 2);
  download("かるた対戦組データ_" + stamp() + ".json", data, "application/json");
});
$("import-btn").addEventListener("click", () => $("import-file").click());
$("import-file").addEventListener("change", e => {
  const file = e.target.files[0];
  if(!file) return;
  const reader = new FileReader();
  reader.onload = () => {
    try{
      const d = JSON.parse(reader.result);
      if(!Array.isArray(d.players)) throw new Error("形式が違います");
      if(players.length && !confirm("現在のメンバー・履歴を読み込んだ内容で置き換えます。よろしいですか?")) return;
      applyData(d);
      renderAll();
      alert("読み込みました(選手" + players.length + "名、対戦記録" + historyPairCount() + "件)。");
    }catch(err){
      alert("読み込めませんでした。このアプリで書き出したファイルを選んでください。");
    }
  };
  reader.readAsText(file);
  e.target.value = "";
});
$("clear-history-btn").addEventListener("click", () => {
  if(!historyPairCount() && !Object.keys(history.byes).length){ alert("履歴はまだありません。"); return; }
  if(confirm("対戦履歴(" + historyPairCount() + "件)をすべて消去しますか?メンバー登録は残ります。")){
    history = {pairs: {}, byes: {}};
    saveState();
    renderHistoryCount();
  }
});
$("use-history").addEventListener("change", saveState);
$("obog-mode").addEventListener("change", saveState);

/* ============ イベント ============ */
function renderAll(){
  renderPlayers();
  renderPairSelects();
  renderPairList("req-list", requests, false);
  renderPairList("ng-list", ngPairs, true);
  renderByeConfig();
  renderFixedBanner();
  renderHistoryCount();
  saveState();
}
$("rank-input").innerHTML = rankOptions();
$("bulk-rank").innerHTML = rankOptions();
$("add-player-btn").addEventListener("click", () => {
  if(addPlayer($("name-input").value, $("rank-input").value, $("attr-input").value)){
    $("name-input").value = "";
    $("name-input").focus();
    renderAll();
  }
});
$("name-input").addEventListener("keydown", e => {
  if(e.key === "Enter") $("add-player-btn").click();
});
$("toggle-bulk-btn").addEventListener("click", () => {
  const a = $("bulk-area");
  a.style.display = a.style.display === "none" ? "" : "none";
});
$("bulk-add-btn").addEventListener("click", () => {
  const names = $("bulk-input").value.split(/[\s,、,]+/).map(s => s.trim()).filter(Boolean);
  if(!names.length){ alert("名前を入力してください。"); return; }
  const rank = $("bulk-rank").value, attr = $("bulk-attr").value;
  let added = 0;
  names.forEach(n => { if(addPlayer(n, rank, attr)) added++; });
  if(added){ $("bulk-input").value = ""; renderAll(); }
});
$("sample-btn").addEventListener("click", () => {
  const sample = [["青山","A+","現役"],["石田","A","OBOG"],["上野","B+","現役"],["江口","B","現役"],["大野","B","OBOG"],
    ["加藤","C+","現役"],["木村","C+","OBOG"],["黒田","C","現役"],["小林","C",""],["斎藤","C","OBOG"],
    ["高橋","D+","現役"],["田中","D","現役"],["土屋","D","OBOG"],["中村","E+",""],["西田","E","現役"]];
  sample.forEach(([n, r, a]) => { if(!players.some(p => p.name === n)) addPlayer(n, r, a); });
  renderAll();
});
$("clear-players-btn").addEventListener("click", () => {
  if(players.length && confirm("登録した選手をすべて削除しますか?(確定済みの回戦もリセットされます)")){
    players = []; requests = []; ngPairs = []; fixedRounds = [];
    renderAll();
    $("results").innerHTML = "";
    $("regen-btn").style.display = "none";
    $("print-btn").style.display = "none";
  }
});
$("add-req-btn").addEventListener("click", () =>
  addPairTo(requests, ngPairs, +$("req-a").value, +$("req-b").value, "希望", "対戦NG"));
$("add-ng-btn").addEventListener("click", () =>
  addPairTo(ngPairs, requests, +$("ng-a").value, +$("ng-b").value, "対戦NG", "希望"));
$("rounds-input").addEventListener("input", () => { renderByeConfig(); saveState(); });
$("generate-btn").addEventListener("click", run);
$("regen-btn").addEventListener("click", run);
$("print-btn").addEventListener("click", () => window.print());
function run(){
  if(players.length < 2){ alert("選手を2名以上登録してください。"); return; }
  const rounds = clampRounds();
  if(fixedRounds.length && rounds <= fixedRounds.length){
    alert("試合数(" + rounds + ")が確定済みの回戦数(" + fixedRounds.length + ")以下です。試合数を増やすか、確定を解除してください。");
    return;
  }
  const evenN = players.length % 2 === 0 ? players.length : players.length - 1;
  if(rounds > evenN - 1 + (players.length % 2)){
    if(!confirm("試合数が多いため、再戦が発生する可能性があります。続けますか?")) return;
  }
  lastResult = generateSchedule();
  renderResults(lastResult);
}
loadState();
renderAll();
</script>
</body>
</html>
