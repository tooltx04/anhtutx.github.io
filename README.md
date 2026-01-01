
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Casino Hub Pro</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}
body{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    font-family:Segoe UI,Arial,sans-serif;
    background:linear-gradient(270deg,red,orange,yellow,green,cyan,blue,violet);
    background-size:1600% 1600%;
    animation:rainbow 14s ease infinite;
}
@keyframes rainbow{
    0%{background-position:0% 50%}
    50%{background-position:100% 50%}
    100%{background-position:0% 50%}
}
.container{
    width:500px;
    background:rgba(0,0,0,.65);
    border-radius:22px;
    padding:26px;
    box-shadow:0 0 40px rgba(255,255,255,.4);
    color:#fff;
}
h1{
    text-align:center;
    font-size:34px;
    margin-bottom:16px;
    text-shadow:-2px -2px 0 #fff,2px -2px 0 #fff,-2px 2px 0 #fff,2px 2px 0 #fff,0 0 12px gold;
}
.tabs{display:flex;gap:10px;margin-bottom:16px}
.tab{
    flex:1;
    padding:12px;
    text-align:center;
    border-radius:12px;
    border:2px solid #fff;
    cursor:pointer;
    font-weight:bold;
}
.tab.active{background:rgba(255,255,255,.25);box-shadow:0 0 12px gold}
.content{display:none}
.content.active{display:block}

/* ===== COMMON ===== */
.history{
    margin-top:14px;
    background:rgba(255,255,255,.1);
    border-radius:10px;
    padding:10px;
    font-size:13px;
}
.history h3{
    margin-bottom:6px;
    color:#ffd9a3;
}
.history div{
    border-bottom:1px solid rgba(255,255,255,.15);
    padding:4px 0;
}
.history div:last-child{border-bottom:none}

/* ===== SICBO ===== */
.sicbo-box{
    background:#181c3a;
    padding:20px;
    border-radius:16px;
}
.sicbo-box input{width:100%;padding:10px;border-radius:6px;border:none;margin-bottom:10px}
.sicbo-box button{width:100%;padding:10px;border:none;border-radius:6px;background:#3b82f6;color:white}
.sicbo-box pre{background:#0b0e1d;padding:12px;border-radius:8px;margin-top:10px}

/* ===== SUNWIN ===== */
.sunwin-box{
    background:linear-gradient(145deg,#6a2b2b,#2a0f0f);
    border-radius:18px;
    padding:20px;
    border:2px solid #caa46a;
}
.timer{text-align:center;color:#ffd9a3;margin-bottom:12px}
.row{display:flex;justify-content:space-between;padding:6px 0;border-bottom:1px solid rgba(255,255,255,.15)}
.row:last-child{border-bottom:none}
.label{color:#ffd9a3}
.value{font-weight:bold}
.footer{text-align:center;margin-top:16px;font-size:13px;opacity:.85}
</style>
</head>

<body>
<div class="container">
<h1>🎰 anhtubantool</h1>

<div class="tabs">
    <div class="tab active" onclick="showTab('sicbo',this)">🎲 SICBO</div>
    <div class="tab" onclick="showTab('sunwin',this)">🔥 SUNWIN</div>
</div>

<!-- ===== SICBO ===== -->
<div id="sicbo" class="content active">
    <div class="sicbo-box">
        <input id="md5Input" placeholder="Nhập MD5 32 ký tự hex">
        <button onclick="analyze()">PHÂN TÍCH</button>
        <pre id="output"></pre>

        <div class="history">
            <h3>📜 Lịch sử SICBO</h3>
            <div id="sicboHistory"></div>
        </div>
    </div>
</div>

<!-- ===== SUNWIN ===== -->
<div id="sunwin" class="content">
    <div class="sunwin-box">
        <div class="timer">⏳ Làm mới sau <span id="countdown">60</span>s</div>

        <div class="row"><span class="label">Phiên</span><span id="phien" class="value">--</span></div>
        <div class="row"><span class="label">Xúc xắc</span><span id="xx" class="value">--</span></div>
        <div class="row"><span class="label">Tổng</span><span id="tong" class="value">--</span></div>
        <div class="row"><span class="label">Kết quả</span><span id="ketqua" class="value">--</span></div>
        <div class="row"><span class="label">Dự đoán</span><span id="dudoan" class="value">--</span></div>

        <div class="history">
            <h3>📜 Lịch sử SUNWIN</h3>
            <div id="sunwinHistory"></div>
        </div>
    </div>
</div>

<div class="footer">© Casino Hub | GitHub Pages</div>
</div>

<script>
function showTab(id,el){
    document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
    document.querySelectorAll('.content').forEach(c=>c.classList.remove('active'));
    el.classList.add('active');
    document.getElementById(id).classList.add('active');
}

/* ===== SICBO ===== */
let sicboHist=[];
function seededRandom(s){let x=Math.sin(s++)*10000;return x-Math.floor(x);}
function analyze(){
    const md5=md5Input.value.trim().toLowerCase();
    if(!/^[0-9a-f]{32}$/.test(md5)){output.textContent="❌ MD5 không hợp lệ";return;}
    let s=parseInt(md5.slice(0,16),16);
    let d1=1+Math.floor(seededRandom(s++)*6);
    let d2=1+Math.floor(seededRandom(s++)*6);
    let d3=1+Math.floor(seededRandom(s++)*6);
    const sum=d1+d2+d3;
    const kq=sum>=11?"TÀI":"XỈU";

    output.textContent=`🎲 ${d1}-${d2}-${d3} | ${kq}`;

    sicboHist.unshift(`🎲 ${d1}-${d2}-${d3} | ${kq}`);
    sicboHist=sicboHist.slice(0,5);
    sicboHistory.innerHTML=sicboHist.map(i=>`<div>${i}</div>`).join("");
}

/* ===== SUNWIN ===== */
let sunwinHist=[];
const REFRESH=60; let cd=REFRESH;

async function loadSunwin(){
    try{
        const r=await fetch("https://sunwinsaygex-tzz9.onrender.com/api/sun");
        const d=await r.json();
        phien.textContent=d.phien;
        xx.textContent=`${d.xuc_xac_1}-${d.xuc_xac_2}-${d.xuc_xac_3}`;
        tong.textContent=d.tong;
        ketqua.textContent=d.ket_qua;
        dudoan.textContent=d.du_doan;

        sunwinHist.unshift(`Phiên ${d.phien}: ${d.ket_qua} (${d.tong})`);
        sunwinHist=sunwinHist.slice(0,5);
        sunwinHistory.innerHTML=sunwinHist.map(i=>`<div>${i}</div>`).join("");
    }catch{
        ketqua.textContent="Lỗi API";
    }
}

setInterval(()=>{
    countdown.textContent=cd;
    cd--;
    if(cd<0){cd=REFRESH;loadSunwin();}
},1000);

loadSunwin();
</script>
</body>
</html>

