<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>تقويم أم القرى الرسمي</title>

<style>
    body {
        font-family: "Tahoma", sans-serif;
        background: #f0f2f5;
        margin: 0;
        padding: 0;
        transition: 0.3s;
    }

    body.dark {
        background: #1e1e1e;
        color: #fff;
    }
    body.dark .container {
        background: #2c2c2c;
        color: white;
    }
    body.dark td {
        background: #333;
        color: white;
        border-color: #555;
    }
    body.dark th {
        background: #157347;
    }
    body.dark .topbar {
        background: #157347;
    }
    body.dark .hijri {
        color: #ddd !important;
    }
    body.dark .day {
        color: #fff !important;
    }

    .topbar {
        background: #198754;
        padding: 18px;
        text-align: center;
        color: white;
        font-size: 22px;
        font-weight: bold;
        box-shadow: 0 2px 8px rgba(0,0,0,0.15);
    }

    .container {
        max-width: 900px;
        margin: 40px auto;
        background: #ffffff;
        padding: 30px;
        border-radius: 14px;
        box-shadow: 0 4px 20px rgba(0,0,0,0.08);
    }

    #header {
        text-align: center;
        margin-bottom: 25px;
    }

    #header h2 {
        color: #198754;
        font-size: 26px;
        margin-bottom: 15px;
    }

    #header button {
        padding: 10px 22px;
        margin: 5px;
        background: #198754;
        color: white;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        font-size: 15px;
        transition: 0.2s;
    }

    #header button:hover {
        background: #157347;
    }

    .switch-btn {
        background: #0d6efd;
        border-radius: 50%;
        width: 48px;
        height: 48px;
        font-size: 22px;
        display: inline-flex;
        align-items: center;
        justify-content: center;
    }
    .switch-btn:hover {
        background: #0b5ed7;
    }

    table {
        width: 100%;
        border-collapse: collapse;
        background: white;
        border-radius: 12px;
        overflow: hidden;
    }

    th {
        background: #198754;
        color: white;
        padding: 14px;
        font-size: 16px;
        border: 1px solid #ddd;
    }

    td {
        padding: 14px;
        text-align: center;
        border: 1px solid #eee;
        height: 95px;
        vertical-align: top;
        background: #ffffff;
        transition: 0.2s;
    }

    td:hover {
        background: #f8f9fa;
    }

    .event {
        background: #ffefef !important;
        border: 1px solid #ff8a8a !important;
    }

    .day {
        font-size: 20px;
        font-weight: bold;
        color: #333;
    }

    .hijri {
        font-size: 13px;
        color: #777;
        margin-top: 6px;
    }

    .today {
        background: #c8f7c5 !important;
        border: 2px solid #198754 !important;
        box-shadow: 0 0 8px rgba(0,0,0,0.15);
    }
    body.dark .today {
        background: #295f2d !important;
        border-color: #44ff88 !important;
    }

    .event-badge {
        display: inline-block;
        margin-top: 6px;
        padding: 3px 8px;
        background: #b30000;
        color: white;
        font-size: 11px;
        border-radius: 6px;
        font-weight: bold;
    }
    body.dark .event-badge {
        background: #ff5555;
    }

    .convert-box {
        margin-top: 25px;
        padding: 20px;
        background: #f8f9fa;
        border-radius: 10px;
        border: 1px solid #ddd;
    }
    body.dark .convert-box {
        background: #333;
        border-color: #555;
    }
</style>
</head>

<body>

<div class="topbar">
    تقويم أم القرى الرسمي
</div>

<div class="container">

    <div id="header">

        <button class="switch-btn" onclick="toggleView()">🌐</button>

        <button onclick="prevMonth()">السابق</button>
        <button onclick="goToday()">اليوم</button>
        <button onclick="nextMonth()">التالي</button>

        <button onclick="toggleDarkMode()">الوضع الليلي</button>

        <!-- زر الانتقال إلى موقع شامل -->
        <button onclick="window.location.href='https://ksashamel.github.io/shamel/'">
            الانتقال إلى موقع شامل
        </button>

        <h2 id="title"></h2>
    </div>

    <table id="calendar">
        <thead>
            <tr>
                <th>الأحد</th>
                <th>الاثنين</th>
                <th>الثلاثاء</th>
                <th>الأربعاء</th>
                <th>الخميس</th>
                <th>الجمعة</th>
                <th>السبت</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>

    <div class="convert-box">
        <h3 style="color:#198754;text-align:center;">التحويل بين الميلادي والهجري (أم القرى)</h3>

        <select id="convertType" onchange="updateConvertSelectors()">
            <option value="gToH">من ميلادي إلى هجري</option>
            <option value="hToG">من هجري إلى ميلادي</option>
        </select>

        <select id="convertYear"></select>
        <select id="convertMonth"></select>
        <select id="convertDay"></select>

        <button onclick="convertDate()">تحويل</button>

        <h3 id="convertResult" style="text-align:center;margin-top:15px;color:#198754;"></h3>
    </div>

</div>

<script>
let currentYear = new Date().getFullYear();
let currentMonth = new Date().getMonth();
let viewMode = "gregorian";

let hijriYear = null;
let hijriMonth = null;

const events = [
    { name: "اليوم الوطني السعودي", date: "23-09" },
    { name: "يوم التأسيس", date: "22-02" },
    { name: "عيد الفطر", hijri: "01-10" },
    { name: "عيد الأضحى", hijri: "10-12" },
    { name: "وقفة عرفة", hijri: "09-12" },
    { name: "رأس السنة الهجرية", hijri: "01-01" }
];

function toggleDarkMode() {
    document.body.classList.toggle("dark");
}

function goToday() {
    const t = new Date();
    currentYear = t.getFullYear();
    currentMonth = t.getMonth();
    viewMode === "gregorian" ? generateCalendar(currentYear, currentMonth) : convertToHijriAndShow();
}

function prevMonth() {
    if (viewMode === "gregorian") {
        currentMonth--;
        if (currentMonth < 0) { currentMonth = 11; currentYear--; }
        generateCalendar(currentYear, currentMonth);
    } else {
        hijriMonth--;
        if (hijriMonth < 1) { hijriMonth = 12; hijriYear--; }
        generateHijriMonth(hijriYear, hijriMonth);
    }
}

function nextMonth() {
    if (viewMode === "gregorian") {
        currentMonth++;
        if (currentMonth > 11) { currentMonth = 0; currentYear++; }
        generateCalendar(currentYear, currentMonth);
    } else {
        hijriMonth++;
        if (hijriMonth > 12) { hijriMonth = 1; hijriYear++; }
        generateHijriMonth(hijriYear, hijriMonth);
    }
}

function toggleView() {
    viewMode = viewMode === "gregorian" ? "hijri" : "gregorian";
    viewMode === "gregorian" ? generateCalendar(currentYear, currentMonth) : convertToHijriAndShow();
}

async function convertToHijriAndShow() {
    const t = new Date();
    const r = await fetch(`https://api.aladhan.com/v1/gToH?date=${t.getDate()}-${t.getMonth()+1}-${t.getFullYear()}`);
    const d = await r.json();
    hijriYear = d.data.hijri.year;
    hijriMonth = d.data.hijri.month.number;
    generateHijriMonth(hijriYear, hijriMonth);
}

async function getHijri(day, month, year) {
    const r = await fetch(`https://api.aladhan.com/v1/gToH?date=${day}-${month}-${year}`);
    const d = await r.json();
    return d.data.hijri;
}

async function generateCalendar(year, month) {
    viewMode = "gregorian";

    const names = ["يناير","فبراير","مارس","أبريل","مايو","يونيو","يوليو","أغسطس","سبتمبر","أكتوبر","نوفمبر","ديسمبر"];
    document.getElementById("title").textContent = `تقويم شهر ${names[month]} ${year}`;

    const first = new Date(year, month, 1).getDay();
    const days = new Date(year, month+1, 0).getDate();

    const tbody = document.querySelector("#calendar tbody");
    tbody.innerHTML = "";
    let row = document.createElement("tr");

    const today = new Date();

    for (let i=0;i<first;i++) row.appendChild(document.createElement("td"));

    for (let d=1; d<=days; d++) {
        const cell = document.createElement("td");
        const h = await getHijri(d, month+1, year);

        cell.innerHTML = `<div class="day">${d}</div><div class="hijri">${h.day}-${h.month.number} هـ</div>`;

        if (d===today.getDate() && month===today.getMonth() && year===today.getFullYear())
            cell.classList.add("today");

        const gKey = `${String(d).padStart(2,"0")}-${String(month+1).padStart(2,"0")}`;
        const hKey = `${String(h.day).padStart(2,"0")}-${String(h.month.number).padStart(2,"0")}`;

        events.forEach(e=>{
            if (e.date===gKey || e.hijri===hKey) {
                cell.classList.add("event");
                cell.innerHTML += `<div class="event-badge">${e.name}</div>`;
            }
        });

        row.appendChild(cell);
        if ((first+d)%7===0) { tbody.appendChild(row); row=document.createElement("tr"); }
    }
    tbody.appendChild(row);
}

async function generateHijriMonth(hYear, hMonth) {
    viewMode = "hijri";

    hijriYear = hYear;
    hijriMonth = hMonth;

    const tbody = document.querySelector("#calendar tbody");
    tbody.innerHTML = "";

    const r = await fetch(`https://api.aladhan.com/v1/hToG?date=1-${hMonth}-${hYear}`);
    const d = await r.json();
    const g = d.data.gregorian;

    const first = new Date(g.year, g.month.number-1, g.day).getDay();

    document.getElementById("title").textContent = `تقويم شهر ${hMonth} هـ ${hYear}`;

    let row = document.createElement("tr");
    for (let i=0;i<first;i++) row.appendChild(document.createElement("td"));

    for (let day=1; day<=30; day++) {
        const r2 = await fetch(`https://api.aladhan.com/v1/hToG?date=${day}-${hMonth}-${hYear}`);
        const d2 = await r2.json();
        const g2 = d2.data.gregorian;

        const cell = document.createElement("td");
        cell.innerHTML = `<div class="day">${day} هـ</div><div class="hijri">${g2.day}-${g2.month.number}-${g2.year} م</div>`;

        const hKey = `${String(day).padStart(2,"0")}-${String(hMonth).padStart(2,"0")}`;
        const gKey = `${String(g2.day).padStart(2,"0")}-${String(g2.month.number).padStart(2,"0")}`;

        events.forEach(e=>{
            if (e.hijri===hKey || e.date===gKey) {
                cell.classList.add("event");
                cell.innerHTML += `<div class="event-badge">${e.name}</div>`;
            }
        });

        row.appendChild(cell);
        if ((first+day)%7===0) { tbody.appendChild(row); row=document.createElement("tr"); }
    }
    tbody.appendChild(row);
}

function updateConvertSelectors() {
    const type = document.getElementById("convertType").value;
    const y = document.getElementById("convertYear");
    const m = document.getElementById("convertMonth");
    const d = document.getElementById("convertDay");

    y.innerHTML=""; m.innerHTML=""; d.innerHTML="";

    if (type==="gToH") for (let i=1950;i<=2100;i++) y.innerHTML+=`<option>${i}</option>`;
    else for (let i=1400;i<=1500;i++) y.innerHTML+=`<option>${i}</option>`;

    for (let i=1;i<=12;i++) m.innerHTML+=`<option>${i}</option>`;
    for (let i=1;i<=30;i++) d.innerHTML+=`<option>${i}</option>`;
}
updateConvertSelectors();

async function convertDate() {
    const type = document.getElementById("convertType").value;
    const y = document.getElementById("convertYear").value;
    const m = document.getElementById("convertMonth").value;
    const d = document.getElementById("convertDay").value;

    let url = type==="gToH"
        ? `https://api.aladhan.com/v1/gToH?date=${d}-${m}-${y}`
        : `https://api.aladhan.com/v1/hToG?date=${d}-${m}-${y}`;

    const r = await fetch(url);
    const data = await r.json();

    const result = type==="gToH"
        ? `${data.data.hijri.day}-${data.data.hijri.month.number}-${data.data.hijri.year} هـ`
        : `${data.data.gregorian.day}-${data.data.gregorian.month.number}-${data.data.gregorian.year} م`;

    document.getElementById("convertResult").textContent = result;
}

window.onload = ()=>generateCalendar(currentYear, currentMonth);
</script>

</body>
</html>
