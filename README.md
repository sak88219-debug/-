# 
بوابة وزارة العدل الرقمية للرول بلاي هي منصة إلكترونية رسمية لتنظيم التقاضي وحفظ الحقوق. تتيح للمواطنين رفع القضايا ومتابعتها، وللمحامين تقديم الدفاع، وللقضاة إصدار الأحكام وتحديد الجلسات بسهولة تامة وبأجواء واقعية ومنظمة
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>وزارة العدل - نظام الرول بلاي</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header class="navbar">
        <div class="logo">⚖️ وزارة العدل - نظام القضايا (RP)</div>
        <nav>
            <a href="#" onclick="showSection('home')">الرئيسية</a>
            <a href="#" onclick="showSection('file-case')">رفع قضية</a>
            <a href="#" onclick="showSection('cases-list')">سجل القضايا</a>
        </nav>
    </header>

    <main class="container">
        <!-- قسم الرئيسية -->
        <section id="home" class="page active">
            <div class="hero">
                <h1>منصة العدالة الرقمية للسيرفر</h1>
                <p>تقديم الشكاوى، متابعة الجلسات، واستعراض الأحكام القضائية بكل سهولة.</p>
                <button class="btn-primary" onclick="showSection('file-case')">رفع قضية جديدة</button>
            </div>
        </section>

        <!-- قسم رفع قضية -->
        <section id="file-case" class="page">
            <h2>نموذج رفع قضية / شكوى</h2>
            <form id="caseForm" onsubmit="submitCase(event)">
                <label>اسم المدعي (المشتكي):</label>
                <input type="text" id="plaintiff" required placeholder="مثال: أحمد (ID: 102)">

                <label>اسم المدعى عليه (المشكو في حقه):</label>
                <input type="text" id="defendant" required placeholder="مثال: خالد (ID: 405)">

                <label>نوع القضية:</label>
                <select id="caseType">
                    <option value="جنائية">جنائية (اعتداء، سرقة)</option>
                    <option value="مرورية">مرورية (صدم وهروب)</option>
                    <option value="مالية">مالية (نصب، ديون)</option>
                    <option value="خلاف شخصي">خلاف شخصي / إزعاج</option>
                </select>

                <label>تفاصيل الشكوى (قصة الحدث):</label>
                <textarea id="caseDetails" rows="4" required placeholder="اكتب تفاصيل القصة هنا..."></textarea>

                <button type="submit" class="btn-primary">إرسال القضية للمحكمة</button>
            </form>
        </section>

        <!-- قسم سجل القضايا -->
        <section id="cases-list" class="page">
            <h2>قائمة القضايا المسجلة</h2>
            <div id="casesContainer">
                <!-- سيتم تعبئتها تلقائياً -->
            </div>
        </section>
    </main>

    <script src="script.js"></script>
</body>
</html>

* {
    box-sizing: border-box;
    font-family: 'Cairo', sans-serif;
    margin: 0;
    padding: 0;
}

body {
    background-color: #0f172a;
    color: #f8fafc;
}

.navbar {
    background-color: #022c22;
    border-bottom: 2px solid #d4af37;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.navbar .logo {
    font-weight: 700;
    color: #d4af37;
    font-size: 1.2rem;
}

.navbar nav a {
    color: #fff;
    text-decoration: none;
    margin-left: 20px;
    font-weight: 600;
    transition: 0.3s;
}

.navbar nav a:hover {
    color: #d4af37;
}

.container {
    max-width: 800px;
    margin: 40px auto;
    padding: 20px;
    background: #1e293b;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.5);
}

.page {
    display: none;
}

.page.active {
    display: block;
}

.hero {
    text-align: center;
    padding: 40px 0;
}

.hero h1 {
    color: #d4af37;
    margin-bottom: 15px;
}

.hero p {
    color: #94a3b8;
    margin-bottom: 25px;
}

form {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

label {
    font-weight: 600;
    color: #cbd5e1;
}

input, select, textarea {
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #475569;
    background: #0f172a;
    color: #fff;
}

.btn-primary {
    background-color: #166534;
    color: white;
    padding: 12px;
    border: none;
    border-radius: 5px;
    font-weight: bold;
    cursor: pointer;
    transition: 0.3s;
    border: 1px solid #d4af37;
}

.btn-primary:hover {
    background-color: #14532d;
}

.case-card {
    background: #0f172a;
    padding: 15px;
    margin-top: 10px;
    border-radius: 5px;
    border-right: 4px solid #d4af37;
}
function showSection(sectionId) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(sectionId).classList.add('active');
    if(sectionId === 'cases-list') {
        loadCases();
    }
}

function submitCase(event) {
    event.preventDefault();
    
    const newCase = {
        id: '#RP-' + Math.floor(1000 + Math.random() * 9000),
        plaintiff: document.getElementById('plaintiff').value,
        defendant: document.getElementById('defendant').value,
        type: document.getElementById('caseType').value,
        details: document.getElementById('caseDetails').value,
        status: 'جديدة - تحت المراجعة'
    };

    let cases = JSON.parse(localStorage.getItem('rp_cases')) || [];
    cases.push(newCase);
    localStorage.setItem('rp_cases', JSON.stringify(cases));

    alert('تم رفع القضية بنجاح! رقم القضية: ' + newCase.id);
    document.getElementById('caseForm').reset();
    showSection('cases-list');
}

function loadCases() {
    const container = document.getElementById('casesContainer');
    let cases = JSON.parse(localStorage.getItem('rp_cases')) || [];
    
    if(cases.length === 0) {
        container.innerHTML = '<p style="color: #94a3b8; text-align: center;">لا توجد قضايا مسجلة حالياً.</p>';
        return;
    }

    container.innerHTML = cases.map(c => `
        <div class="case-card">
            <h3>رقم القضية: ${c.id} (${c.type})</h3>
            <p><strong>المدعي:</strong> ${c.plaintiff}</p>
            <p><strong>المدعى عليه:</strong> ${c.defendant}</p>
            <p><strong>التفاصيل:</strong> ${c.details}</p>
            <p><strong>الحالة:</strong> <span style="color: #d4af37;">${c.status}</span></p>
        </div>
    `).join('');
}
<!-- قسم التوظيف والتقديم في وزارة العدل -->
<section id="careers" class="page" style="text-align: center; padding: 30px;">
    <h2 style="color: #d4af37; margin-bottom: 15px;">الانضمام إلى سلك القضاء والادعاء</h2>
    <p style="color: #cbd5e1; margin-bottom: 25px; line-height: 1.6;">
        هل تمتلك الخبرة الكافية في النظام القضائي وتطبيقات الرول بلاي؟ 
        تعلن وزارة العدل عن فتح باب التقديم لشغل وظائف (قضاة، محامين معتمدين، وموظفي محكمة). 
        بادر بتقديم طلبك الآن للانضمام إلى فريق العدالة والمساهمة في تنظيم سيرفرنا!
    </p>
    
    <a href="https://forms.gle/cYoHpd7k1W434QfP9" target="_blank" class="btn-primary" style="display: inline-block; text-decoration: none; padding: 12px 25px; font-size: 1.1rem;">
         التقديم على وزارة العدل
    </a>
</section>
<a href="#" onclick="showSection('careers')">التوظيف والتقديم</a>
