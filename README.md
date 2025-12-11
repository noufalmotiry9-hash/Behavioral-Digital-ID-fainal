# Behavioral-Digital-ID-fainal[index.html](https://github.com/user-attachments/files/24107411/index.html)
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>البصمة السلوكية – Behavioral Digital ID</title>
    <style>
        body {
            margin: 0;
            font-family: "Tajawal", sans-serif;
            background:#f2f4f6;
        }
        h2 {
            margin:0 0 20px;
            color:#022;
            text-align:center;
            font-size:22px;
        }
        .login-box {
            width: 380px;
            margin: 80px auto;
            background:#fff;
            padding:30px;
            border-radius:18px;
            box-shadow:0 0 25px rgba(0,0,0,.09);
        }
        input {
            width:100%;
            padding:12px;
            margin-bottom:15px;
            border:1px solid #ddd;
            border-radius:10px;
            font-size:15px;
        }
        button {
            width:100%;
            padding:12px;
            background:#0a8a6a;
            border:none;
            color:#fff;
            font-size:17px;
            border-radius:10px;
            cursor:pointer;
            transition:0.2s;
        }
        button:hover {
            background:#06795c;
        }
        #dashboard {
            display:none;
            max-width:800px;
            margin:40px auto;
            background:#fff;
            padding:25px;
            border-radius:18px;
            box-shadow:0 0 25px rgba(0,0,0,.08);
        }
        .metric {
            background:#f7f9fa;
            padding:18px;
            border-radius:12px;
            margin-bottom:15px;
            font-size:16px;
        }
        #alertBox {
            display:none;
            background:#ffe6e6;
            padding:15px;
            border-radius:10px;
            border:1px solid #ff9999;
            color:#b00000;
            font-weight:bold;
            margin-top:15px;
            animation:fadeIn .4s;
        }
        @keyframes fadeIn { from{opacity:0;} to{opacity:1;} }

        .log-box {
            margin-top:20px;
            background:#f7f8fa;
            padding:12px;
            border-radius:10px;
            max-height:150px;
            overflow-y:auto;
            font-size:14px;
            border:1px solid #ddd;
        }
        .log-entry {
            margin-bottom:6px;
            color:#333;
        }
    </style>
</head>
<body>

<!-- Login -->
<div class="login-box" id="loginBox">
    <h2>تسجيل الدخول</h2>
    <input type="text" id="username" placeholder="اسم المستخدم">
    <input type="password" id="password" placeholder="كلمة المرور"
           oninput="captureTyping(event)">
    <button onclick="login()">دخول</button>
</div>

<!-- Dashboard -->
<div id="dashboard">
    <h2>لوحة مراقبة البصمة السلوكية</h2>

    <div class="metric">درجة التطابق السلوكي: <strong id="score">--</strong></div>
    <div class="metric">حالة النظام: <strong id="status">جاري المراقبة…</strong></div>

    <button style="background:#c62828; margin-top:10px;" onclick="simulateAttack()">
        تشغيل محاولة اختراق وهمية
    </button>

    <div id="alertBox">⚠️ تم رصد سلوك غير مطابق – تنبيه أمني</div>

    <h3 style="margin-top:25px; color:#022;">سجل النشاط Security Log</h3>
    <div class="log-box" id="logBox"></div>
</div>

<script>
let typingData = [];
let mouseMovement = 0;

// تتبع الكتابة
function captureTyping(e){
    typingData.push({
        t: Date.now(),
        key: e.data
    });
}

// تتبع حركة الماوس
document.addEventListener("mousemove", () => {
    mouseMovement += 1;
});

// تسجيل دخول
function login(){
    document.getElementById("loginBox").style.display = "none";
    document.getElementById("dashboard").style.display = "block";

    let score = calculateScore();
    document.getElementById("score").innerHTML = score + "%";
    addLog("دخول المستخدم — السلوك طبيعي");
}

// حساب درجة التطابق
function calculateScore(){
    let base = 85 + Math.random()*10;

    if(mouseMovement < 20 || typingData.length < 3){
        base -= 25;
        addLog("سلوك غير معتاد أثناء تسجيل الدخول");
    }
    return Math.max(20, Math.min(99, base.toFixed(1)));
}

// تشغيل هجوم وهمي
function simulateAttack(){
    document.getElementById("alertBox").style.display = "block";
    document.getElementById("status").innerHTML = "⚠️ نشاط مشبوه";
    let dangerScore = (25 + Math.random()*10).toFixed(1);
    document.getElementById("score").innerHTML = dangerScore + "%";

    addLog("⚠️ محاولة اختراق — تم خفض درجة التطابق إلى " + dangerScore + "%");
}

// إضافة للسجل
function addLog(text){
    let box = document.getElementById("logBox");
    let entry = document.createElement("div");
    entry.classList.add("log-entry");
    entry.textContent = new Date().toLocaleTimeString() + " — " + text;
    box.appendChild(entry);
}
</script>

</body>
</html>
