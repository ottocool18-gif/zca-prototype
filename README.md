[ZCA_官網互動原型.html](https://github.com/user-attachments/files/31232259/ZCA_.html)
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<title>ZCA 中誠藝術拍賣 — 互動原型</title>
<style>
  :root{
    --black:#14110F; --ink:#1C1613; --red:#6E1620; --red-dk:#4A0F17;
    --gold:#C9A86A; --cream:#FAF8F4; --paper:#FFFFFF; --muted:#6B6555; --line:#E6E0D4;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;background:#0B0A09;font-family:"Noto Sans TC","PingFang TC","Microsoft JhengHei",sans-serif;}

  /* ---- prototype chrome ---- */
  .stage{max-width:1180px;margin:0 auto;padding:28px 16px 60px;}
  .browser{background:var(--paper);border-radius:10px;overflow:hidden;box-shadow:0 30px 80px rgba(0,0,0,.45);}
  .browser-bar{background:#EDEAE2;padding:10px 14px;display:flex;align-items:center;gap:10px;border-bottom:1px solid var(--line);}
  .dot{width:10px;height:10px;border-radius:50%;}
  .dot.r{background:#E5605A;} .dot.y{background:#E7B84B;} .dot.g{background:#59C168;}
  .addr{flex:1;background:#fff;border:1px solid var(--line);border-radius:6px;padding:5px 12px;font-size:12px;color:var(--muted);font-family:monospace;}
  .screen{position:relative;min-height:680px;background:var(--cream);}

  .hint{position:absolute;top:14px;right:14px;background:var(--black);color:#F2ECE1;font-size:11.5px;padding:8px 14px;border-radius:20px;z-index:50;opacity:.92;pointer-events:none;}

  /* ---- nav ---- */
  nav.site{background:var(--black);display:flex;align-items:center;justify-content:space-between;padding:14px 32px;}
  nav.site .logo{color:#F2ECE1;font-weight:700;letter-spacing:2px;font-size:17px;cursor:pointer;}
  nav.site .links{display:flex;gap:28px;}
  nav.site .links a{color:#CFC7BA;font-size:13px;text-decoration:none;cursor:pointer;transition:color .15s;}
  nav.site .links a:hover, nav.site .links a.active{color:var(--gold);}
  nav.site .cta{background:var(--red);color:#F2ECE1;font-size:12.5px;padding:8px 16px;border-radius:3px;border:none;cursor:pointer;}

  .view{display:none;}
  .view.active{display:block;}

  /* ---- hero ---- */
  .hero{background:linear-gradient(135deg,#1a1210,#3a0f14 55%,#1a1210);padding:64px 40px;position:relative;overflow:hidden;}
  .hero-kicker{color:var(--gold);font-size:11px;letter-spacing:3px;margin-bottom:10px;}
  .hero h1{color:#F2ECE1;font-size:36px;margin:0 0 12px;font-weight:700;max-width:520px;line-height:1.3;}
  .hero p{color:#CFC7BA;font-size:14px;max-width:440px;line-height:1.7;margin:0 0 22px;}
  .hero .btnrow{display:flex;gap:12px;}
  .btn{border:none;cursor:pointer;font-size:13px;padding:11px 22px;border-radius:3px;font-weight:600;}
  .btn.primary{background:var(--red);color:#F2ECE1;}
  .btn.ghost{background:transparent;color:#F2ECE1;border:1px solid #4a433a;}
  .btn:hover{filter:brightness(1.12);}

  /* ---- sections ---- */
  .section{padding:40px 40px;}
  .section h2{font-size:20px;color:var(--ink);margin:0 0 4px;}
  .section .sub{font-size:12.5px;color:var(--muted);margin:0 0 22px;}
  .grid{display:grid;grid-template-columns:repeat(4,1fr);gap:18px;}
  .lot-card{background:var(--paper);border:1px solid var(--line);border-radius:6px;overflow:hidden;cursor:pointer;transition:transform .15s, box-shadow .15s;}
  .lot-card:hover{transform:translateY(-3px);box-shadow:0 10px 24px rgba(0,0,0,.12);}
  .lot-art{height:130px;display:flex;align-items:center;justify-content:center;color:rgba(255,255,255,.85);font-size:11px;letter-spacing:1px;}
  .lot-body{padding:12px 14px;}
  .lot-title{font-size:12.5px;color:var(--ink);font-weight:600;margin:0 0 4px;}
  .lot-est{font-size:11px;color:var(--muted);}

  /* ---- catalogue filter bar ---- */
  .filterbar{display:flex;gap:10px;margin-bottom:22px;flex-wrap:wrap;}
  .chip{background:var(--paper);border:1px solid var(--line);border-radius:16px;padding:6px 14px;font-size:11.5px;color:var(--ink);cursor:pointer;}
  .chip.on{background:var(--red);color:#F2ECE1;border-color:var(--red);}

  /* ---- lot detail ---- */
  .detail-wrap{display:flex;gap:36px;padding:40px;}
  .detail-art{flex:1;min-height:420px;border-radius:6px;display:flex;align-items:center;justify-content:center;color:rgba(255,255,255,.85);font-size:13px;}
  .detail-info{flex:1;max-width:400px;}
  .detail-info .lotno{font-size:11px;color:var(--muted);letter-spacing:1px;margin-bottom:6px;}
  .detail-info h2{font-size:22px;margin:0 0 6px;color:var(--ink);}
  .detail-info .artist{font-size:13px;color:var(--muted);margin-bottom:20px;}
  .bidbox{background:var(--paper);border:1px solid var(--line);border-radius:6px;padding:20px;margin-bottom:20px;}
  .bidbox .row{display:flex;justify-content:space-between;font-size:12.5px;color:var(--muted);margin-bottom:6px;}
  .bidbox .cur{font-size:24px;font-weight:700;color:var(--ink);margin-bottom:14px;}
  .countdown{display:flex;gap:8px;margin:16px 0;}
  .countdown .box{background:var(--black);color:#F2ECE1;border-radius:4px;padding:8px 10px;font-size:16px;font-weight:700;min-width:44px;text-align:center;}
  .countdown .lbl{font-size:9px;color:var(--muted);text-align:center;margin-top:3px;}
  .meta-list{font-size:12px;color:var(--muted);line-height:2;}

  /* ---- member form ---- */
  .form-wrap{max-width:520px;margin:0 auto;padding:40px;}
  .field{margin-bottom:16px;}
  .field label{display:block;font-size:12px;color:var(--muted);margin-bottom:6px;}
  .field input,.field select{width:100%;padding:10px 12px;border:1px solid var(--line);border-radius:4px;font-size:13px;background:var(--paper);color:var(--ink);font-family:inherit;}
  .field-row{display:flex;gap:12px;}
  .field-row .field{flex:1;}

  /* ---- records table ---- */
  table.records{width:100%;border-collapse:collapse;}
  table.records th{text-align:left;font-size:11px;color:var(--muted);border-bottom:1px solid var(--line);padding:10px 12px;font-weight:600;}
  table.records td{padding:12px;font-size:12.5px;color:var(--ink);border-bottom:1px solid var(--line);}
  table.records tr:hover td{background:#F3EEE3;}
  .tag-sold{background:#E8F1EC;color:#2E6B4E;font-size:10px;padding:3px 8px;border-radius:10px;}

  /* ---- toast / modal ---- */
  .toast{position:fixed;left:50%;bottom:26px;transform:translateX(-50%) translateY(100px);background:var(--black);color:#F2ECE1;padding:12px 22px;border-radius:6px;font-size:13px;opacity:0;transition:all .3s;z-index:200;box-shadow:0 10px 30px rgba(0,0,0,.35);}
  .toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

  .foot{background:var(--black);color:#8a8375;font-size:11px;padding:26px 40px;display:flex;justify-content:space-between;}

  .art-1{background:linear-gradient(135deg,#7a1e1e,#2a0f10);}
  .art-2{background:linear-gradient(135deg,#3a4a3f,#12201a);}
  .art-3{background:linear-gradient(135deg,#5c4a2a,#221a0d);}
  .art-4{background:linear-gradient(135deg,#2a3a5c,#0d1522);}
  .art-5{background:linear-gradient(135deg,#4a2a5c,#170d22);}
  .art-6{background:linear-gradient(135deg,#8a5a2a,#2a1a0d);}
  .art-7{background:linear-gradient(135deg,#2a5c52,#0d221d);}
  .art-8{background:linear-gradient(135deg,#5c2a3a,#220d15);}
</style>
</head>
<body>
<div class="stage">
  <div class="browser">
    <div class="browser-bar">
      <span class="dot r"></span><span class="dot y"></span><span class="dot g"></span>
      <div class="addr" id="addr">zhongcheng-auction.com/</div>
    </div>
    <div class="screen" id="screen">
      <div class="hint" id="hint">互動原型 · 點擊導覽列或卡片切換頁面</div>

      <!-- NAV -->
      <nav class="site">
        <div class="logo" onclick="go('home')">ZHONG CHENG</div>
        <div class="links">
          <a onclick="go('home')" data-nav="home">首頁</a>
          <a onclick="go('catalogue')" data-nav="catalogue">線上圖錄</a>
          <a onclick="go('live')" data-nav="live">線上拍賣會</a>
          <a onclick="go('records')" data-nav="records">歷年競賣紀錄</a>
          <a onclick="go('member')" data-nav="member">會員專區</a>
        </div>
        <button class="cta" onclick="go('member')">申請會員</button>
      </nav>

      <!-- HOME -->
      <div class="view active" id="view-home">
        <div class="hero">
          <div class="hero-kicker">2026 AUTUMN · ALL IN: BID ONE</div>
          <h1>當代藝術線上直播競標，即時參與每一口出價。</h1>
          <p>從瀏覽拍品到即時出價一站完成，無法到場的藏家也能參與競標。</p>
          <div class="btnrow">
            <button class="btn primary" onclick="go('live')">進入線上拍賣會</button>
            <button class="btn ghost" onclick="go('catalogue')">瀏覽線上圖錄</button>
          </div>
        </div>
        <div class="section">
          <h2>精選拍品</h2>
          <div class="sub">Featured Lots — 點擊卡片查看拍品詳情與出價</div>
          <div class="grid" id="home-grid"></div>
        </div>
      </div>

      <!-- CATALOGUE -->
      <div class="view" id="view-catalogue">
        <div class="section">
          <h2>線上圖錄</h2>
          <div class="sub">Online Catalogues — 依類別、年代、估價篩選拍品</div>
          <div class="filterbar">
            <div class="chip on">全部</div>
            <div class="chip">當代繪畫</div>
            <div class="chip">雕塑</div>
            <div class="chip">複合媒材</div>
            <div class="chip">2026 秋季拍賣</div>
          </div>
          <div class="grid" id="cat-grid"></div>
        </div>
      </div>

      <!-- LOT DETAIL -->
      <div class="view" id="view-detail">
        <div class="detail-wrap">
          <div class="detail-art" id="detail-art">Lot Artwork</div>
          <div class="detail-info">
            <div class="lotno" id="detail-lotno">LOT 102</div>
            <h2 id="detail-title">霧山</h2>
            <div class="artist" id="detail-artist">周〇芽 · 2019 · 油彩畫布</div>
            <div class="bidbox">
              <div class="row"><span>目前出價</span><span>Current Bid</span></div>
              <div class="cur" id="detail-price">NT$ 1,280,000</div>
              <div class="row"><span>估價區間</span><span id="detail-est">NT$ 1,000,000 - 1,600,000</span></div>
              <div class="countdown">
                <div><div class="box">01</div><div class="lbl">DAYS</div></div>
                <div><div class="box">14</div><div class="lbl">HRS</div></div>
                <div><div class="box">22</div><div class="lbl">MIN</div></div>
              </div>
              <button class="btn primary" style="width:100%;margin-top:6px;" onclick="doBid()">立即出價</button>
            </div>
            <div class="meta-list">
              <div>拍賣場次：2026 秋季當代藝術拍賣</div>
              <div>尺寸：162 × 130 cm</div>
              <div>來源：藝術家工作室直接徵集</div>
            </div>
          </div>
        </div>
      </div>

      <!-- LIVE AUCTION -->
      <div class="view" id="view-live">
        <div class="hero" style="background:linear-gradient(135deg,#3a0f14,#14110F 60%);">
          <div class="hero-kicker">LIVE NOW · 線上直播競標</div>
          <h1>ALL IN: BID ONE</h1>
          <p>當代藝術線上直播拍賣，登入會員即可即時出價，全程可回放直播畫面。</p>
          <div class="countdown">
            <div><div class="box">00</div><div class="lbl">DAYS</div></div>
            <div><div class="box">03</div><div class="lbl">HRS</div></div>
            <div><div class="box">41</div><div class="lbl">MIN</div></div>
            <div><div class="box">09</div><div class="lbl">SEC</div></div>
          </div>
          <div class="btnrow">
            <button class="btn primary" onclick="go('catalogue')">瀏覽本場拍品</button>
            <button class="btn ghost" onclick="toast('已加入直播提醒')">加入提醒</button>
          </div>
        </div>
        <div class="section">
          <h2>本場焦點拍品</h2>
          <div class="sub">正在競標中，點擊卡片查看即時出價</div>
          <div class="grid" id="live-grid"></div>
        </div>
      </div>

      <!-- MEMBER -->
      <div class="view" id="view-member">
        <div class="form-wrap">
          <h2 style="margin-bottom:4px;">線上會員申請</h2>
          <div class="sub" style="margin-bottom:24px;">填寫以下資料即可完成會員申請，取代原本電話辦理流程。</div>
          <div class="field-row">
            <div class="field"><label>姓名</label><input placeholder="王小明"></div>
            <div class="field"><label>手機號碼</label><input placeholder="0912-345-678"></div>
          </div>
          <div class="field"><label>電子郵件</label><input placeholder="name@example.com"></div>
          <div class="field-row">
            <div class="field"><label>會員等級</label><select><option>一般會員</option><option>VIP 會員</option></select></div>
            <div class="field"><label>國籍</label><select><option>台灣</option><option>其他</option></select></div>
          </div>
          <div class="field"><label>地址</label><input placeholder="台北市大安區仁愛路..."></div>
          <button class="btn primary" style="width:100%;margin-top:8px;" onclick="submitMember()">送出申請</button>
        </div>
      </div>

      <!-- RECORDS -->
      <div class="view" id="view-records">
        <div class="section">
          <h2>歷年競賣紀錄</h2>
          <div class="sub">Auction Records — 依作品分類、年份查詢已成交拍品，回應藏家真偽與行情查證需求</div>
          <table class="records">
            <thead><tr><th>LOT</th><th>作品</th><th>藝術家</th><th>拍賣場次</th><th>成交價</th><th>狀態</th></tr></thead>
            <tbody id="records-body"></tbody>
          </table>
        </div>
      </div>

      <div class="foot">
        <span>ZCA 中誠藝術拍賣 — 互動原型 Prototype v1</span>
        <span>設計：Otto Yao · UI/UX Design</span>
      </div>
    </div>
  </div>
</div>
<div class="toast" id="toast"></div>

<script>
const artClasses = ['art-1','art-2','art-3','art-4','art-5','art-6','art-7','art-8'];
const lots = [
  {no:'LOT 101', title:'紅山石', artist:'周〇芽 · 2018', est:'NT$ 2,200,000 - 2,800,000', price:'NT$ 2,400,000'},
  {no:'LOT 102', title:'霧山', artist:'周〇芽 · 2019', est:'NT$ 1,000,000 - 1,600,000', price:'NT$ 1,280,000'},
  {no:'LOT 103', title:'三雙半筷子', artist:'王〇慶 · 2005', est:'NT$ 3,500,000 - 4,200,000', price:'NT$ 3,600,000'},
  {no:'LOT 104', title:'23.3.68', artist:'趙〇極 · 1968', est:'NT$ 8,000,000 - 12,000,000', price:'NT$ 9,200,000'},
  {no:'LOT 105', title:'台灣島', artist:'郭〇國 · 2011', est:'NT$ 900,000 - 1,300,000', price:'NT$ 980,000'},
  {no:'LOT 106', title:'熱蘭遮紀事', artist:'楊〇林 · 1993', est:'NT$ 1,600,000 - 2,000,000', price:'NT$ 1,750,000'},
  {no:'LOT 107', title:'太極系列', artist:'朱〇 · 1997', est:'NT$ 4,500,000 - 5,500,000', price:'NT$ 4,800,000'},
  {no:'LOT 108', title:'塗鴉鳥', artist:'葉〇青 · 2007', est:'NT$ 1,100,000 - 1,500,000', price:'NT$ 1,220,000'},
];

function lotCard(lot, i){
  return `<div class="lot-card" onclick="openLot(${i})">
    <div class="lot-art ${artClasses[i % artClasses.length]}">${lot.no}</div>
    <div class="lot-body">
      <div class="lot-title">${lot.title}</div>
      <div class="lot-est">${lot.est}</div>
    </div>
  </div>`;
}

document.getElementById('home-grid').innerHTML = lots.slice(0,4).map(lotCard).join('');
document.getElementById('cat-grid').innerHTML = lots.map(lotCard).join('');
document.getElementById('live-grid').innerHTML = lots.slice(2,6).map(lotCard).join('');

document.getElementById('records-body').innerHTML = lots.map((l,i)=>`
  <tr>
    <td>${l.no}</td>
    <td>${l.title}</td>
    <td>${l.artist.split(' · ')[0]}</td>
    <td>2026 秋季當代藝術拍賣</td>
    <td>${l.price}</td>
    <td><span class="tag-sold">已成交</span></td>
  </tr>`).join('');

const addrMap = {
  home: 'zhongcheng-auction.com/',
  catalogue: 'zhongcheng-auction.com/catalogue',
  detail: 'zhongcheng-auction.com/lot/102',
  live: 'zhongcheng-auction.com/live/all-in-bid-one',
  member: 'zhongcheng-auction.com/member/apply',
  records: 'zhongcheng-auction.com/records',
};

function go(name){
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.getElementById('view-'+name).classList.add('active');
  document.querySelectorAll('[data-nav]').forEach(a=>a.classList.remove('active'));
  const navEl = document.querySelector('[data-nav="'+name+'"]');
  if(navEl) navEl.classList.add('active');
  document.getElementById('addr').textContent = addrMap[name] || addrMap.home;
  document.getElementById('screen').scrollTop = 0;
  const hint = document.getElementById('hint');
  if(hint){ hint.style.opacity='0.92'; clearTimeout(window._hintT); window._hintT=setTimeout(()=>hint.style.opacity='0',2200); }
}

function openLot(i){
  const l = lots[i];
  document.getElementById('detail-lotno').textContent = l.no;
  document.getElementById('detail-title').textContent = l.title;
  document.getElementById('detail-artist').textContent = l.artist + ' · 油彩畫布';
  document.getElementById('detail-price').textContent = l.price;
  document.getElementById('detail-est').textContent = l.est;
  const art = document.getElementById('detail-art');
  art.className = 'detail-art ' + artClasses[i % artClasses.length];
  art.textContent = l.title;
  go('detail');
}

function doBid(){ toast('出價成功，系統已寄送確認信'); }
function submitMember(){ toast('會員申請已送出，將於 1 個工作天內完成審核'); }

function toast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(window._toastT);
  window._toastT = setTimeout(()=>t.classList.remove('show'), 2600);
}

setTimeout(()=>{ const h=document.getElementById('hint'); if(h) h.style.opacity='0'; }, 3200);
</script>
</body>
</html>
