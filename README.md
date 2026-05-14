[index.html.html](https://github.com/user-attachments/files/27757374/index.html.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>주식 감정 일기 — MindTrade</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Noto+Sans+KR:wght@300;400;500;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f; --surface: #13131c; --surface2: #1c1c2e; --border: #2a2a3e;
    --accent: #00e5a0; --accent2: #ff4d6d; --accent3: #ffc847;
    --text: #e8e8f0; --muted: #6b6b8a; --radius: 16px;
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:var(--bg); color:var(--text); font-family:'Noto Sans KR',sans-serif; min-height:100vh; overflow-x:hidden; }
  body::before {
    content:''; position:fixed; inset:0;
    background-image: linear-gradient(rgba(0,229,160,0.03) 1px,transparent 1px), linear-gradient(90deg,rgba(0,229,160,0.03) 1px,transparent 1px);
    background-size:40px 40px; pointer-events:none; z-index:0;
  }
  .app { max-width:520px; margin:0 auto; padding:24px 16px 100px; position:relative; z-index:1; }
  .header { text-align:center; padding:40px 0 28px; }
  .logo {
    font-family:'Bebas Neue',sans-serif; font-size:48px; letter-spacing:4px;
    background:linear-gradient(135deg,var(--accent),#00b4ff);
    -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; line-height:1;
  }
  .tagline { color:var(--muted); font-size:13px; letter-spacing:2px; text-transform:uppercase; margin-top:8px; }
  .tab-bar {
    position:fixed; bottom:0; left:0; right:0;
    background:rgba(13,13,20,0.96); backdrop-filter:blur(20px);
    border-top:1px solid var(--border); display:flex; z-index:100; padding:8px 0 12px;
  }
  .tab-btn {
    flex:1; display:flex; flex-direction:column; align-items:center; gap:4px; padding:8px 4px;
    background:none; border:none; color:var(--muted); font-family:'Noto Sans KR',sans-serif;
    font-size:10px; cursor:pointer; transition:color 0.2s;
  }
  .tab-btn .ti { font-size:20px; transition:transform 0.2s; }
  .tab-btn.active { color:var(--accent); }
  .tab-btn.active .ti { transform:scale(1.2); }
  .page { display:none; }
  .page.active { display:block; animation:fadeIn 0.3s ease; }
  @keyframes fadeIn { from{opacity:0;transform:translateY(10px)} to{opacity:1;transform:translateY(0)} }
  .card { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:20px; margin-bottom:14px; }
  .card-title { font-size:11px; letter-spacing:2px; text-transform:uppercase; color:var(--accent); margin-bottom:16px; font-weight:500; }
  .ig { margin-bottom:14px; }
  .ig:last-child { margin-bottom:0; }
  label { display:block; font-size:13px; color:var(--muted); margin-bottom:7px; }
  input[type="text"], input[type="date"], textarea {
    width:100%; background:var(--surface2); border:1px solid var(--border); border-radius:10px;
    padding:12px 14px; color:var(--text); font-family:'Noto Sans KR',sans-serif; font-size:14px; outline:none; transition:border-color 0.2s;
  }
  input:focus, textarea:focus { border-color:var(--accent); }
  textarea { resize:none; height:76px; }
  .tg { display:flex; gap:8px; }
  .tb { flex:1; padding:12px; border-radius:10px; border:1px solid var(--border); background:var(--surface2); color:var(--muted); font-family:'Noto Sans KR',sans-serif; font-size:14px; cursor:pointer; transition:all 0.2s; font-weight:500; }
  .tb.sb { background:rgba(0,229,160,0.15); border-color:var(--accent); color:var(--accent); }
  .tb.ss { background:rgba(255,77,109,0.15); border-color:var(--accent2); color:var(--accent2); }
  .egrid { display:grid; grid-template-columns:repeat(5,1fr); gap:8px; }
  .eb { display:flex; flex-direction:column; align-items:center; gap:6px; padding:12px 4px; border-radius:12px; border:1px solid var(--border); background:var(--surface2); cursor:pointer; transition:all 0.2s; }
  .eb.sel { border-color:var(--accent3); background:rgba(255,200,71,0.1); }
  .ei { font-size:24px; }
  .el { font-size:10px; color:var(--muted); font-family:'Noto Sans KR',sans-serif; }
  .eb.sel .el { color:var(--accent3); }
  input[type="range"] { -webkit-appearance:none; width:100%; height:4px; background:var(--border); border-radius:2px; outline:none; border:none; padding:0; }
  input[type="range"]::-webkit-slider-thumb { -webkit-appearance:none; width:20px; height:20px; border-radius:50%; background:var(--accent); cursor:pointer; border:3px solid var(--bg); }
  .slabels { display:flex; justify-content:space-between; margin-top:6px; font-size:11px; color:var(--muted); }
  .sval { text-align:center; font-size:28px; font-family:'Bebas Neue',sans-serif; color:var(--accent); margin-bottom:8px; letter-spacing:2px; }
  .btn-p { width:100%; padding:16px; background:var(--accent); color:#000; border:none; border-radius:var(--radius); font-family:'Noto Sans KR',sans-serif; font-size:16px; font-weight:700; cursor:pointer; transition:all 0.2s; letter-spacing:1px; }
  .btn-p:hover { background:#00ffb3; transform:translateY(-1px); }
  .srow { display:grid; grid-template-columns:repeat(3,1fr); gap:10px; margin-bottom:16px; }
  .sc { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:16px 12px; text-align:center; }
  .sv { font-family:'Bebas Neue',sans-serif; font-size:30px; letter-spacing:2px; line-height:1; }
  .sl { font-size:10px; color:var(--muted); margin-top:4px; letter-spacing:1px; text-transform:uppercase; }
  .rec { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:16px; margin-bottom:10px; animation:fadeIn 0.3s ease; }
  .rec-top { display:flex; justify-content:space-between; align-items:center; margin-bottom:8px; }
  .rec-name { font-weight:700; font-size:16px; }
  .tags { display:flex; gap:6px; flex-wrap:wrap; margin-bottom:8px; }
  .tag { padding:3px 9px; border-radius:20px; font-size:11px; background:var(--surface2); color:var(--muted); }
  .tag.buy { color:var(--accent); border:1px solid rgba(0,229,160,0.25); }
  .tag.sell { color:var(--accent2); border:1px solid rgba(255,77,109,0.25); }
  .ret-wrap { background:var(--surface2); border-radius:10px; padding:10px 12px; margin-top:8px; }
  .ret-lbl { font-size:11px; color:var(--muted); margin-bottom:6px; }
  .ret-row { display:flex; align-items:center; gap:8px; }
  .ret-inp {
    flex:1; background:var(--bg); border:1px solid var(--border); border-radius:8px;
    padding:8px 12px; font-size:13px; color:var(--text); font-family:'Noto Sans KR',sans-serif; outline:none;
    -moz-appearance:textfield;
  }
  .ret-inp::-webkit-outer-spin-button, .ret-inp::-webkit-inner-spin-button { -webkit-appearance:none; }
  .ret-inp:focus { border-color:var(--accent); }
  .ib {
    background:linear-gradient(135deg,rgba(0,229,160,0.1),rgba(0,180,255,0.1));
    border:1px solid rgba(0,229,160,0.2); border-radius:var(--radius); padding:24px 20px; margin-bottom:14px; text-align:center;
  }
  .ii { font-size:40px; margin-bottom:8px; }
  .it { font-family:'Bebas Neue',sans-serif; font-size:22px; letter-spacing:2px; color:var(--accent); }
  .id { font-size:13px; color:var(--muted); margin-top:6px; line-height:1.7; }
  .bar-row { display:flex; align-items:center; gap:10px; margin-bottom:10px; }
  .bar-lbl { width:28px; font-size:20px; flex-shrink:0; text-align:center; }
  .bar-track { flex:1; height:8px; background:var(--surface2); border-radius:4px; overflow:hidden; }
  .bar-fill { height:100%; border-radius:4px; transition:width 1s cubic-bezier(0.4,0,0.2,1); }
  .bar-val { width:48px; text-align:right; font-size:13px; font-family:'Bebas Neue',sans-serif; letter-spacing:1px; flex-shrink:0; }
  .bar-val.pos { color:var(--accent); }
  .bar-val.neg { color:var(--accent2); }
  .empty { text-align:center; padding:60px 20px; color:var(--muted); }
  .empty-icon { font-size:48px; margin-bottom:12px; }
  .empty-text { font-size:14px; line-height:1.7; }
  .toast {
    position:fixed; bottom:80px; left:50%;
    transform:translateX(-50%) translateY(80px);
    background:var(--accent); color:#000; padding:13px 24px; border-radius:50px;
    font-weight:700; font-size:14px; transition:transform 0.4s cubic-bezier(0.175,0.885,0.32,1.275);
    z-index:200; white-space:nowrap;
  }
  .toast.show { transform:translateX(-50%) translateY(0); }
</style>
</head>
<body>
<div class="app">
  <div class="header">
    <div class="logo">MindTrade</div>
    <div class="tagline">감정이 수익률을 결정한다</div>
  </div>

  <div class="page active" id="page-record">
    <div class="card">
      <div class="card-title">매매 정보</div>
      <div class="ig"><label>종목명</label><input type="text" id="stock" placeholder="예: 삼성전자, TSMC, NVDA"></div>
      <div class="ig"><label>날짜</label><input type="date" id="tradeDate"></div>
      <div class="ig"><label>구분</label><div class="tg">
        <button class="tb" id="btn-buy" onclick="selType('buy')">📈 매수</button>
        <button class="tb" id="btn-sell" onclick="selType('sell')">📉 매도</button>
      </div></div>
    </div>
    <div class="card">
      <div class="card-title">지금 감정 상태</div>
      <div class="egrid">
        <button class="eb" onclick="selEmo('excited')" id="eo-excited"><span class="ei">🔥</span><span class="el">흥분</span></button>
        <button class="eb" onclick="selEmo('anxious')" id="eo-anxious"><span class="ei">😰</span><span class="el">불안</span></button>
        <button class="eb" onclick="selEmo('confident')" id="eo-confident"><span class="ei">💪</span><span class="el">확신</span></button>
        <button class="eb" onclick="selEmo('fear')" id="eo-fear"><span class="ei">😱</span><span class="el">두려움</span></button>
        <button class="eb" onclick="selEmo('numb')" id="eo-numb"><span class="ei">😶</span><span class="el">무감각</span></button>
      </div>
    </div>
    <div class="card">
      <div class="card-title">분석 확신도</div>
      <div class="sval" id="cdis">3점</div>
      <input type="range" id="confidence" min="1" max="10" value="5" oninput="document.getElementById('cdis').textContent=this.value+'점'">
      <div class="slabels"><span>충동매매</span><span>완벽분석</span></div>
    </div>
    <div class="card">
      <div class="card-title">수익률 (선택)</div>
      <div style="display:flex;align-items:center;gap:8px;">
        <input type="number" step="0.1" id="returnPctInput" placeholder="예: 3.5 또는 -2.1"
          style="flex:1;background:var(--surface2);border:1px solid var(--border);border-radius:10px;padding:12px 14px;color:var(--text);font-family:'Noto Sans KR',sans-serif;font-size:14px;outline:none;-moz-appearance:textfield;"
          oninput="previewReturn(this.value)">
        <span style="font-size:14px;color:var(--muted);">%</span>
        <span id="ret-preview" style="font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:1px;color:var(--muted);min-width:60px;text-align:right;">-</span>
      </div>
      <div style="font-size:11px;color:var(--muted);margin-top:8px;">나중에 내역에서도 입력 가능해요</div>
    </div>
    <div class="card">
      <div class="card-title">한 줄 메모 (선택)</div>
      <textarea id="memo" placeholder="왜 이 매매를 했나요?"></textarea>
    </div>
    <button class="btn-p" onclick="saveRec()">감정 기록 저장하기</button>
  </div>

  <div class="page" id="page-history">
    <div class="srow">
      <div class="sc"><div class="sv" id="st-tot" style="color:var(--accent)">0</div><div class="sl">총 기록</div></div>
      <div class="sc"><div class="sv" id="st-avg" style="color:var(--accent3)">-</div><div class="sl">평균 수익</div></div>
      <div class="sc"><div class="sv" id="st-win" style="color:var(--accent2)">-</div><div class="sl">승률</div></div>
    </div>
    <button onclick="exportCSV()" style="width:100%;padding:13px;margin-bottom:14px;border-radius:var(--radius);border:1px solid var(--accent);background:rgba(0,229,160,0.08);color:var(--accent);font-family:'Noto Sans KR',sans-serif;font-size:14px;font-weight:700;cursor:pointer;">📥 CSV로 내보내기 (엑셀 백업)</button>
    <div id="hist-list"></div>
  </div>

  <div class="page" id="page-insight">
    <div id="ins-content"></div>
  </div>
</div>

<div class="tab-bar">
  <button class="tab-btn active" onclick="switchTab('record',this)"><span class="ti">📝</span>기록</button>
  <button class="tab-btn" onclick="switchTab('history',this)"><span class="ti">📋</span>내역</button>
  <button class="tab-btn" onclick="switchTab('insight',this)"><span class="ti">📊</span>인사이트</button>
</div>
<div class="toast" id="toast"></div>

<script>
const EMO = {
  excited:{i:'🔥',l:'흥분'}, anxious:{i:'😰',l:'불안'},
  confident:{i:'💪',l:'확신'}, fear:{i:'😱',l:'두려움'}, numb:{i:'😶',l:'무감각'}
};
let sType=null, sEmo=null;
let recs = JSON.parse(localStorage.getItem('mt4')||'[]');
document.getElementById('tradeDate').value = new Date().toISOString().split('T')[0];

function switchTab(t,btn) {
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+t).classList.add('active');
  btn.classList.add('active');
  if(t==='history') renderHist();
  if(t==='insight') renderIns();
}
function selType(t) {
  sType=t;
  document.getElementById('btn-buy').className='tb'+(t==='buy'?' sb':'');
  document.getElementById('btn-sell').className='tb'+(t==='sell'?' ss':'');
}
function selEmo(e) {
  sEmo=e;
  document.querySelectorAll('.eb').forEach(b=>b.classList.remove('sel'));
  document.getElementById('eo-'+e).classList.add('sel');
}
function previewReturn(val) {
  const el = document.getElementById('ret-preview');
  if(val===''||val===null){ el.textContent='-'; el.style.color='var(--muted)'; return; }
  const n = parseFloat(val);
  el.textContent = (n>=0?'+':'')+n.toFixed(1)+'%';
  el.style.color = n>=0?'var(--accent)':'var(--accent2)';
}
function saveRec() {
  const stock=document.getElementById('stock').value.trim();
  const date=document.getElementById('tradeDate').value;
  const memo=document.getElementById('memo').value.trim();
  const conf=parseInt(document.getElementById('confidence').value);
  const retVal=document.getElementById('returnPctInput').value;
  const returnPct=(retVal==='')?null:parseFloat(retVal);
  if(!stock){showToast('❗ 종목명을 입력해주세요');return;}
  if(!sType){showToast('❗ 매수/매도를 선택해주세요');return;}
  if(!sEmo){showToast('❗ 감정 상태를 선택해주세요');return;}
  recs.unshift({id:Date.now(),stock,date,memo,confidence:conf,type:sType,emotion:sEmo,returnPct});
  save();
  document.getElementById('stock').value='';
  document.getElementById('memo').value='';
  document.getElementById('returnPctInput').value='';
  document.getElementById('ret-preview').textContent='-';
  document.getElementById('ret-preview').style.color='var(--muted)';
  document.getElementById('confidence').value=3;
  document.getElementById('cdis').textContent='5점';
  sType=null; sEmo=null;
  document.querySelectorAll('.tb').forEach(b=>b.className='tb');
  document.querySelectorAll('.eb').forEach(b=>b.classList.remove('sel'));
  showToast('✅ 감정 기록 완료!');
}
function renderHist() {
  const list=document.getElementById('hist-list');
  updateStats();
  if(recs.length===0){
    list.innerHTML=`<div class="empty"><div class="empty-icon">📭</div><div class="empty-text">아직 기록이 없어요.<br>첫 매매 감정을 기록해보세요!</div></div>`;
    return;
  }
  list.innerHTML=recs.map(r=>{
    const emo=EMO[r.emotion];
    const pct=r.returnPct;
    const col=pct===null?'var(--muted)':pct>=0?'var(--accent)':'var(--accent2)';
    const pt=pct===null?'-':(pct>=0?'+':'')+pct.toFixed(1)+'%';
    return `<div class="rec">
      <div class="rec-top">
        <div style="display:flex;align-items:center;gap:10px;">
          <span style="font-size:28px;">${emo.i}</span>
          <div><div class="rec-name">${r.stock}</div><div style="font-size:11px;color:var(--muted);">${r.date}</div></div>
        </div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:1px;color:${col}">${pt}</div>
      </div>
      <div class="tags">
        <span class="tag ${r.type}">${r.type==='buy'?'📈 매수':'📉 매도'}</span>
        <span class="tag">${emo.l}</span>
        <span class="tag">확신 ${r.confidence}점</span>
      </div>
      <div class="ret-wrap">
        <div class="ret-lbl">📍 수익률 입력하면 인사이트 분석 가능해요</div>
        <div class="ret-row">
          <input type="number" step="0.1" class="ret-inp" placeholder="예: 3.5 또는 -2.1"
            value="${pct!==null?pct:''}"
            onchange="updRet(${r.id},this.value)">
          <span style="font-size:13px;color:var(--muted);">%</span>
          <span style="font-family:'Bebas Neue',sans-serif;font-size:20px;color:${col};min-width:56px;text-align:right;">${pt}</span>
        </div>
      </div>
      ${r.memo?`<div style="margin-top:10px;font-size:12px;color:var(--muted);background:var(--surface2);padding:10px 12px;border-radius:8px;line-height:1.6;">💬 ${r.memo}</div>`:''}
    </div>`;
  }).join('');
}
function updRet(id,val) {
  const r=recs.find(r=>r.id===id);
  if(r){ r.returnPct=(val===''||val===null)?null:parseFloat(val); save(); renderHist(); }
}
function updateStats() {
  const wr=recs.filter(r=>r.returnPct!==null);
  const avg=wr.length?(wr.reduce((a,b)=>a+b.returnPct,0)/wr.length).toFixed(1):null;
  const win=wr.length?(wr.filter(r=>r.returnPct>0).length/wr.length*100).toFixed(0):null;
  document.getElementById('st-tot').textContent=recs.length;
  document.getElementById('st-avg').textContent=avg!==null?(parseFloat(avg)>=0?'+':'')+avg+'%':'-';
  document.getElementById('st-win').textContent=win!==null?win+'%':'-';
}
function renderIns() {
  const c=document.getElementById('ins-content');
  const wr=recs.filter(r=>r.returnPct!==null);
  if(wr.length<3){
    const need=3-wr.length;
    c.innerHTML=`
      <div class="ib"><div class="ii">🔬</div><div class="it">데이터 수집 중</div>
      <div class="id">수익률 입력된 기록이 <strong style="color:var(--accent)">${need}개</strong> 더 필요해요!<br>내역 탭에서 수익률을 입력해주세요 📝</div></div>
      <div class="card"><div class="card-title">곧 볼 수 있는 인사이트</div>
      <div style="color:var(--muted);font-size:13px;line-height:2.4;">
        🔥 감정별 평균 수익률<br>💪 확신도 높을 때 vs 낮을 때<br>📈 나의 승률 패턴<br>🧠 최고의 매매 감정 찾기
      </div></div>`;
    return;
  }
  const byEmo={};
  for(const k in EMO){
    const rs=wr.filter(r=>r.emotion===k);
    if(rs.length>0) byEmo[k]={avg:rs.reduce((a,b)=>a+b.returnPct,0)/rs.length, count:rs.length};
  }
  let bestE=null,bestV=-Infinity;
  for(const k in byEmo) if(byEmo[k].avg>bestV){bestV=byEmo[k].avg;bestE=k;}
  const maxAbs=Math.max(...Object.values(byEmo).map(v=>Math.abs(v.avg)),0.1);
  const bars=Object.entries(byEmo).map(([k,v])=>{
    const isP=v.avg>=0;
    const pct=(Math.abs(v.avg)/maxAbs*100).toFixed(0);
    return `<div class="bar-row">
      <div class="bar-lbl">${EMO[k].i}</div>
      <div class="bar-track"><div class="bar-fill" style="width:${pct}%;background:${isP?'var(--accent)':'var(--accent2)'};"></div></div>
      <div class="bar-val ${isP?'pos':'neg'}">${isP?'+':''}${v.avg.toFixed(1)}%</div>
    </div>`;
  }).join('');
  const hc=wr.filter(r=>r.confidence>=8), lc=wr.filter(r=>r.confidence<=3);
  const hA=hc.length?(hc.reduce((a,b)=>a+b.returnPct,0)/hc.length).toFixed(1):null;
  const lA=lc.length?(lc.reduce((a,b)=>a+b.returnPct,0)/lc.length).toFixed(1):null;
  const allP=wr.map(r=>r.returnPct);
  const winR=(allP.filter(p=>p>0).length/allP.length*100).toFixed(0);
  c.innerHTML=`
    ${bestE?`<div class="ib"><div class="ii">${EMO[bestE].i}</div><div class="it">${EMO[bestE].l} 상태가 최고!</div>
    <div class="id">${EMO[bestE].l} 상태일 때 평균 <strong style="color:var(--accent)">${bestV>=0?'+':''}${bestV.toFixed(1)}%</strong> 수익률!</div></div>`:''}
    <div class="card"><div class="card-title">감정별 평균 수익률</div>${bars}</div>
    ${(hA||lA)?`<div class="card"><div class="card-title">분석 확신도 vs 수익률</div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:4px;">
      ${hA?`<div style="text-align:center;padding:16px;background:var(--surface2);border-radius:12px;">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:28px;color:${parseFloat(hA)>=0?'var(--accent)':'var(--accent2)'};letter-spacing:2px;">${parseFloat(hA)>=0?'+':''}${hA}%</div>
        <div style="font-size:11px;color:var(--muted);margin-top:4px;">충분히 분석<br>(8~10점)</div></div>`:''}
      ${lA?`<div style="text-align:center;padding:16px;background:var(--surface2);border-radius:12px;">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:28px;color:${parseFloat(lA)>=0?'var(--accent)':'var(--accent2)'};letter-spacing:2px;">${parseFloat(lA)>=0?'+':''}${lA}%</div>
        <div style="font-size:11px;color:var(--muted);margin-top:4px;">충동매매<br>(1~3점)</div></div>`:''}
    </div></div>`:''}
    <div class="card"><div class="card-title">기록 요약</div>
    <div style="color:var(--muted);font-size:13px;line-height:2.6;">
      📊 분석된 거래: <strong style="color:var(--text)">${wr.length}개</strong><br>
      📈 수익 거래: <strong style="color:var(--accent)">${allP.filter(p=>p>0).length}개</strong><br>
      📉 손실 거래: <strong style="color:var(--accent2)">${allP.filter(p=>p<0).length}개</strong><br>
      ⚖️ 승률: <strong style="color:var(--accent3)">${winR}%</strong>
    </div></div>`;
  setTimeout(()=>{
    document.querySelectorAll('.bar-fill').forEach(b=>{
      const w=b.style.width; b.style.width='0%';
      requestAnimationFrame(()=>{ b.style.width=w; });
    });
  },100);
}
function save(){localStorage.setItem('mt4',JSON.stringify(recs));}
function exportCSV(){
  if(recs.length===0){showToast('❗ 저장된 기록이 없어요');return;}
  const header=['날짜','종목명','매수/매도','감정','확신도','수익률(%)','메모'];
  const rows=recs.map(r=>{
    const memo=(r.memo||'').replace(/"/g,'""');
    return [r.date,r.stock,r.type==='buy'?'매수':'매도',EMO[r.emotion].l,r.confidence,r.returnPct!==null?r.returnPct:'','"'+memo+'"'];
  });
  const lines=[header,...rows].map(r=>r.join(','));
  const csv='\uFEFF'+lines.join('\r\n');
  const blob=new Blob([csv],{type:'text/csv;charset=utf-8;'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a');
  a.href=url;
  a.download='MindTrade_'+new Date().toISOString().split('T')[0]+'.csv';
  a.click();
  URL.revokeObjectURL(url);
  showToast('✅ CSV 다운로드 완료!');
}

function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg; t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2500);
}
</script>
</body>
</html>
