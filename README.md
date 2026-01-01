<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Casino Hub Pro</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: "Segoe UI", Arial, sans-serif;
    background: linear-gradient(
        270deg,
        red, orange, yellow, green, cyan, blue, violet
    );
    background-size: 1600% 1600%;
    animation: rainbow 14s ease infinite;
}

@keyframes rainbow {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

.container {
    width: 440px;
    background: rgba(0,0,0,0.6);
    border-radius: 22px;
    padding: 30px;
    text-align: center;
    box-shadow: 0 0 35px rgba(255,255,255,0.35);
    animation: glow 2s infinite alternate;
}

@keyframes glow {
    from { box-shadow: 0 0 20px rgba(255,255,255,0.3); }
    to { box-shadow: 0 0 45px rgba(255,255,255,0.6); }
}

h1 {
    font-size: 36px;
    margin-bottom: 20px;
    color: #fff;
    text-shadow:
        -2px -2px 0 #fff,
         2px -2px 0 #fff,
        -2px  2px 0 #fff,
         2px  2px 0 #fff,
         0 0 12px gold;
}

.tabs {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.tab {
    flex: 1;
    padding: 12px;
    border-radius: 12px;
    border: 2px solid #fff;
    color: white;
    cursor: pointer;
    font-weight: bold;
    background: transparent;
    transition: 0.3s;
}

.tab.active {
    background: rgba(255,255,255,0.25);
    box-shadow: 0 0 12px gold;
}

.content {
    display: none;
    margin-top: 20px;
}

.content.active {
    display: block;
}

.card {
    background: rgba(255,255,255,0.1);
    border-radius: 16px;
    padding: 25px;
    margin-top: 10px;
    border: 2px solid white;
    animation: pulse 2.5s infinite;
}

@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.03); }
    100% { transform: scale(1); }
}

.card h2 {
    font-size: 26px;
    margin-bottom: 10px;
    color: gold;
    text-shadow: 0 0 10px gold;
}

.card p {
    font-size: 16px;
    color: #fff;
    margin-top: 8px;
}

.footer {
    margin-top: 25px;
    font-size: 14px;
    color: #fff;
    opacity: 0.85;
}

@media (max-width: 500px) {
    .container {
        width: 90%;
    }
}
</style>
</head>

<body>

<div class="container">
    <h1>🎰 CASINO HUB</h1>

    <div class="tabs">
        <div class="tab active" onclick="showTab('sicbo')">🎲 SICBO</div>
        <div class="tab" onclick="showTab('sunwin')">🔥 SUNWIN</div>
    </div>

    <div id="sicbo" class="content active">
        <div class="card">
            <h2>SICBO AI</h2>
            <p>✔ Phân tích MD5</p>
            <p>✔ Dự đoán Tài / Xỉu</p>
            <p>✔ Độ tin cậy cao</p>
        </div>
    </div>

    <div id="sunwin" class="content">
        <div class="card">
            <h2>SUNWIN</h2>
            <p>✔ Dữ liệu realtime</p>
            <p>✔ Cầu & dự đoán</p>
            <p>✔ Theo phiên tự động</p>
        </div>
    </div>

    <div class="footer">
        © Casino Dashboard | GitHub Pages
    </div>
</div>

<script>
function showTab(tab) {
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    document.querySelectorAll('.content').forEach(c => c.classList.remove('active'));

    document.querySelector(`[onclick="showTab('${tab}')"]`).classList.add('active');
    document.getElementById(tab).classList.add('active');
}
</script>

</body>
</html>
