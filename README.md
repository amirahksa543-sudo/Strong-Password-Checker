# Strong-Password-Checker
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>مقياس قوة كلمة المرور</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body { font-family: 'Cairo', sans-serif; min-height: 100vh; padding: 45px 20px; background: radial-gradient(circle at 10% 10%, #42218c 0%, transparent 35%), radial-gradient(circle at 90% 90%, #075b9e 0%, transparent 35%), linear-gradient(135deg, #09091f, #11113b, #101c48); color: white; }
.container { max-width: 1150px; margin: auto; }
header { text-align: center; margin-bottom: 45px; }
.logo { width: 85px; height: 85px; border-radius: 25px; display: flex; align-items: center; justify-content: center; margin: 0 auto 20px; font-size: 38px; color: white; background: linear-gradient(135deg, #812cff, #087cff); box-shadow: 0 0 35px #783dff88; animation: floating 3s ease-in-out infinite; }
header h1 { font-size: 34px; font-weight: 800; background: linear-gradient(90deg, #fff, #a7dfff, #c9aaff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
header p { color: #bfc8f7; margin-top: 12px; font-size: 15px; }
.cards { display: grid; grid-template-columns: 1fr 1fr; gap: 28px; }
.card { background: rgba(255,255,255,0.09); backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.2); border-radius: 25px; padding: 30px; color: white; box-shadow: 0 15px 45px rgba(0,0,0,.3); transition: .35s ease; }
.card:hover { transform: translateY(-5px); border-color: #8c65ff; box-shadow: 0 20px 55px #5529d333; }
.card h2 { font-size: 21px; margin-bottom: 25px; color: #bca2ff; }
.card h2 i { margin-left: 10px; color: #24d9ff; }
.password-box { position: relative; margin-bottom: 18px; }
input { width: 100%; padding: 16px; border: 1px solid #7772bb; border-radius: 13px; outline: none; font-family: inherit; font-size: 15px; background: rgba(255,255,255,.1); color: white; transition: .3s; }
input::placeholder { color: #b7b4d5; }
input:focus { border-color: #21d9ff; box-shadow: 0 0 15px #21d9ff33; background: rgba(255,255,255,.15); }
.password-box input { padding-left: 50px; }
.toggle { position: absolute; left: 16px; top: 50%; transform: translateY(-50%); cursor: pointer; color: #30d9ff; border: none; background: none; font-size: 18px; }
.main-btn { width: 100%; padding: 15px; border: none; border-radius: 13px; color: white; font-family: inherit; font-size: 16px; font-weight: 700; cursor: pointer; background: linear-gradient(100deg, #792cff, #086eff); box-shadow: 0 6px 20px #6026dc55; transition: .3s; }
.main-btn:hover { transform: translateY(-3px); box-shadow: 0 8px 28px #278aff88; filter: brightness(1.15); }
.result { margin-top: 25px; padding: 22px; border-radius: 18px; background: linear-gradient(135deg, #25205c, #172d65); border: 1px solid #6557b9; text-align: center; }
.result-icon { font-size: 38px; color: #29dfff; margin-bottom: 10px; }
.result h3 { font-size: 20px; margin-bottom: 7px; color: #fff; }
.result p { font-size: 13px; color: #c5d5ff; }
.score-circle { width: 135px; height: 135px; border-radius: 50%; margin: 20px auto; display: flex; align-items: center; justify-content: center; background: conic-gradient(#18d6c3 0%, #292b59 0%); position: relative; box-shadow: 0 0 25px #18d6c344; }
.score-circle::before { content: ""; position: absolute; width: 112px; height: 112px; background: #1b2050; border-radius: 50%; }
.score-circle span { position: relative; font-size: 29px; font-weight: 800; color: #fff; }
.progress-title { margin: 22px 0 10px; font-weight: 700; color: #c7d7ff; }
.progress { height: 13px; border-radius: 20px; background: #28274e; overflow: hidden; }
.progress-fill { height: 100%; width: 0; border-radius: 20px; background: linear-gradient(90deg, #792cff, #16d9d0); transition: width .5s; box-shadow: 0 0 12px #18d6c3; }
.criteria { margin-top: 25px; }
.criteria h3 { font-size: 16px; margin-bottom: 12px; color: #c4aaff; }
.criterion { display: flex; justify-content: space-between; align-items: center; padding: 11px 5px; font-size: 13px; border-bottom: 1px solid #ffffff18; color: #e4e5ff; transition: .3s; }
.criterion i { color: #ff657e; }
.criterion.done i { color: #20e4b3; filter: drop-shadow(0 0 5px #20e4b3); }
.generator-box { background: rgba(255,255,255,.07); padding: 22px; border-radius: 17px; border: 1px solid #55518e; margin-bottom: 20px; }
.generator-box label { font-weight: 700; display: block; margin-bottom: 14px; color: #d5c7ff; }
.length-control { display: flex; gap: 12px; align-items: center; }
.length-control input { text-align: center; font-weight: bold; }
.length-control button { width: 45px; height: 45px; border: none; border-radius: 12px; background: linear-gradient(135deg,#812cff,#087cff); color: white; font-size: 23px; cursor: pointer; transition: .3s; }
.length-control button:hover { transform: scale(1.08); box-shadow: 0 0 15px #812cff88; }
.length-info { font-size: 12px; color: #aaaed5; margin-top: 10px; }
.generated-box { margin-top: 22px; }
.generated-box input { text-align: center; font-weight: bold; direction: ltr; margin-bottom: 13px; letter-spacing: 1px; }
.copy-btn { width: 100%; padding: 14px; border: 1px solid #8060ec; border-radius: 12px; background: linear-gradient(100deg,#34218d,#1253a8); color: white; font-family: inherit; cursor: pointer; font-size: 15px; transition: .3s; }
.copy-btn:hover { background: linear-gradient(100deg,#7534e8,#087cff); box-shadow: 0 0 20px #603bdf77; }
.tips { margin-top: 25px; padding: 20px; background: rgba(255,255,255,.07); border: 1px solid #57518c; border-radius: 16px; }
.tips h3 { color: #33dfff; margin-bottom: 12px; font-size: 16px; }
.tips p { font-size: 13px; margin: 10px 0; color: #e1e5ff; }
.tips i { color: #20e4b3; margin-left: 8px; }
footer { text-align: center; margin-top: 40px; color: #bfc9f5; font-size: 13px; }
footer i { color: #20e4b3; margin-left: 7px; }
@keyframes floating { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
@media(max-width:750px) { body { padding: 25px 14px; } .cards { grid-template-columns: 1fr; } header h1 { font-size: 25px; } .card { padding: 22px; } }
@media(prefers-reduced-motion: reduce) { *, *::before, *::after { animation: none !important; transition: none !important; } }
</style>
</head>
<body>
<div class="container">
<header>
<div class="logo"><i class="fas fa-shield-halved"></i></div>
<h1>مقياس قوة كلمة المرور</h1>
<p>احم حساباتك من خلال كلمات مرور قوية وآمنة</p>
</header>
<div class="cards">
<section class="card">
<h2><i class="fas fa-magnifying-glass-chart"></i> فحص قوة كلمة المرور</h2>
<div class="password-box">
<input type="password" id="passwordInput" placeholder="أدخل كلمة المرور هنا" autocomplete="off" oninput="checkPassword()">
<button class="toggle" type="button" onclick="togglePassword()" aria-label="إظهار كلمة المرور"><i class="fas fa-eye" id="eyeIcon"></i></button>
</div>
<button class="main-btn" onclick="checkPassword()"><i class="fas fa-shield-halved"></i> تحليل كلمة المرور</button>
<div class="result">
<div class="result-icon"><i class="fas fa-lock"></i></div>
<h3 id="resultText">لم يتم الفحص بعد</h3>
<p id="resultDescription">أدخل كلمة المرور لمعرفة مستوى الأمان</p>
<div class="score-circle" id="scoreCircle"><span id="percentage">0%</span></div>
</div>
<div class="progress-title">مستوى القوة</div>
<div class="progress"><div class="progress-fill" id="strengthBar"></div></div>
<div class="criteria">
<h3>متطلبات كلمة المرور الأمنية</h3>
<div class="criterion" id="c1"><span>8 أحرف على الأقل</span><i class="fas fa-circle-xmark"></i></div>
<div class="criterion" id="c2"><span>12 حرفًا أو أكثر</span><i class="fas fa-circle-xmark"></i></div>
<div class="criterion" id="c3"><span>حرف كبير (A-Z)</span><i class="fas fa-circle-xmark"></i></div>
<div class="criterion" id="c4"><span>حرف صغير (a-z)</span><i class="fas fa-circle-xmark"></i></div>
<div class="criterion" id="c5"><span>أرقام (0-9)</span><i class="fas fa-circle-xmark"></i></div>
<div class="criterion" id="c6"><span>رموز خاصة (!@#$)</span><i class="fas fa-circle-xmark"></i></div>
</div>
</section>
<section class="card">
<h2><i class="fas fa-wand-magic-sparkles"></i> توليد كلمة مرور قوية</h2>
<div class="generator-box">
<label for="passLength">اختر طول كلمة المرور:</label>
<div class="length-control">
<button onclick="changeLength(-1)" type="button">−</button>
<input type="number" id="passLength" value="14" min="8" max="32">
<button onclick="changeLength(1)" type="button">+</button>
</div>
<p class="length-info">يمكنك اختيار طول من 8 إلى 32 حرفًا</p>
</div>
<button class="main-btn" onclick="generatePassword()"><i class="fas fa-dice"></i> توليد كلمة مرور جديدة</button>
<div class="generated-box">
<input type="text" id="generatedPassword" placeholder="ستظهر كلمة المرور هنا" readonly>
<button class="copy-btn" onclick="copyPassword()"><i class="fas fa-copy"></i> نسخ كلمة المرور</button>
</div>
<div class="tips">
<h3><i class="fas fa-lightbulb"></i> نصائح أمنية مهمة</h3>
<p><i class="fas fa-check-circle"></i> استخدم مزيجًا من الأحرف والأرقام والرموز.</p>
<p><i class="fas fa-check-circle"></i> تجنب استخدام المعلومات الشخصية.</p>
<p><i class="fas fa-check-circle"></i> لا تستخدم كلمة المرور نفسها في عدة حسابات.</p>
<p><i class="fas fa-check-circle"></i> استخدم مدير كلمات المرور لحفظ كلماتك بأمان.</p>
</div>
</section>
</div>
<footer><i class="fas fa-shield-halved"></i> أمانك يبدأ من كلمة مرور قوية</footer>
</div>
<script>
function togglePassword() {
const input = document.getElementById("passwordInput");
const icon = document.getElementById("eyeIcon");
if(input.type === "password") { input.type = "text"; icon.className = "fas fa-eye-slash"; } else { input.type = "password"; icon.className = "fas fa-eye"; }
}
function updateCriteria(id, condition) {
const item = document.getElementById(id);
item.classList.toggle("done", condition);
item.querySelector("i").className = condition ? "fas fa-circle-check" : "fas fa-circle-xmark";
}
function checkPassword() {
const password = document.getElementById("passwordInput").value;
if(!password) {
document.getElementById("resultText").innerText = "لم يتم الفحص بعد";
document.getElementById("resultDescription").innerText = "أدخل كلمة المرور لمعرفة مستوى الأمان";
document.getElementById("percentage").innerText = "0%";
document.getElementById("strengthBar").style.width = "0%";
document.getElementById("scoreCircle").style.background = "conic-gradient(#18d6c3 0%, #292b59 0%)";
for(let i = 1; i <= 6; i++) { updateCriteria("c" + i, false); }
return;
}
const checks = [password.length >= 8, password.length >= 12, /[A-Z]/.test(password), /[a-z]/.test(password), /[0-9]/.test(password), /[^A-Za-z0-9]/.test(password)];
checks.forEach((value, index) => { updateCriteria("c" + (index + 1), value); });
const weights = [25, 15, 15, 15, 15, 15];
let score = checks.reduce((total, passed, index) => total + (passed ? weights[index] : 0), 0);
if (/^(.)\1+$/.test(password)) { score = Math.min(score, 15); }
const percentage = score;
document.getElementById("percentage").innerText = percentage + "%";
document.getElementById("strengthBar").style.width = percentage + "%";
let color, text, description;
if(percentage < 40) { color = "#ef4444"; text = "كلمة المرور ضعيفة"; description = "تحتاج إلى تحسين مستوى الأمان"; }
else if(percentage < 70) { color = "#f59e0b"; text = "كلمة المرور متوسطة"; description = "يمكن تحسينها بإضافة المزيد من التنوع"; }
else if(percentage < 90) { color = "#16b981"; text = "كلمة المرور قوية"; description = "كلمة المرور تتمتع بمستوى أمان جيد"; }
else { color = "#059669"; text = "كلمة المرور قوية جدًا"; description = "تم استيفاء جميع معايير الفحص"; }
document.getElementById("resultText").innerText = text;
document.getElementById("resultDescription").innerText = description;
document.getElementById("strengthBar").style.background = color;
document.getElementById("scoreCircle").style.background = `conic-gradient(${color} ${percentage}%, #292b59 ${percentage}%)`;
}
function changeLength(amount) {
const input = document.getElementById("passLength");
let length = parseInt(input.value) || 14;
input.value = Math.max(8, Math.min(32, length + amount));
}
function secureRandom(max) {
const array = new Uint32Array(1);
const limit = Math.floor(4294967296 / max) * max;
do { crypto.getRandomValues(array); } while(array[0] >= limit);
return array[0] % max;
}
function generatePassword() {
const lengthInput = document.getElementById("passLength");
const length = Number(lengthInput.value);
if(!Number.isInteger(length) || length < 8 || length > 32) { alert("يرجى اختيار طول بين 8 و32 حرفًا"); return; }
const upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const lower = "abcdefghijklmnopqrstuvwxyz";
const numbers = "0123456789";
const symbols = "!@#$%^&*";
const all = upper + lower + numbers + symbols;
let password = [upper[secureRandom(upper.length)], lower[secureRandom(lower.length)], numbers[secureRandom(numbers.length)], symbols[secureRandom(symbols.length)]];
while(password.length < length) { password.push(all[secureRandom(all.length)]); }
for(let i = password.length - 1; i > 0; i--) { const j = secureRandom(i + 1); [password[i], password[j]] = [password[j], password[i]]; }
document.getElementById("generatedPassword").value = password.join("");
}
async function copyPassword() {
const input = document.getElementById("generatedPassword");
if(!input.value) { alert("يرجى توليد كلمة مرور أولاً"); return; }
try { await navigator.clipboard.writeText(input.value); alert("تم نسخ كلمة المرور بنجاح!"); }
catch(error) { input.select(); const copied = document.execCommand("copy"); alert(copied ? "تم نسخ كلمة المرور!" : "تعذر النسخ، يرجى نسخ كلمة المرور يدويًا"); }
}
</script>
</body>
</html>
