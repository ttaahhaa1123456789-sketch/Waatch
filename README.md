<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ساعت هوشمند</title>
    <style>
        *{margin:0;padding:0;box-sizing:border-box;}
        body{font-family:tahoma,sans-serif;background:#0f172a;color:#f1f5f9;direction:rtl;padding:12px;min-height:100vh;-webkit-tap-highlight-color:transparent;user-select:none;-webkit-user-select:none;}
        .c{max-width:600px;margin:0 auto;}
        
        /* Top Bar */
        .top{display:flex;justify-content:space-between;align-items:center;background:#1e293b;padding:12px 16px;border-radius:16px;border:1px solid #334155;margin-bottom:12px;position:relative;z-index:10;}
        .logo{font-weight:900;font-size:16px;display:flex;align-items:center;gap:8px;}
        .logo-icon{background:linear-gradient(135deg,#6366f1,#8b5cf6);width:34px;height:34px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:16px;}
        .hamburger{width:40px;height:40px;background:transparent;border:1.5px solid #334155;border-radius:8px;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:5px;z-index:20;}
        .hamburger span{width:20px;height:2px;background:#cbd5e1;border-radius:2px;transition:0.3s;}
        
        /* Side Menu */
        .menu-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.6);z-index:50;display:none;}
        .menu-overlay.show{display:block;}
        .side-menu{position:fixed;top:0;right:0;bottom:0;width:280px;background:#1e293b;z-index:60;transform:translateX(100%);transition:transform 0.3s;padding:24px 18px;border-left:1px solid #334155;overflow-y:auto;}
        .side-menu.show{transform:translateX(0);}
        .side-menu-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:24px;padding-bottom:16px;border-bottom:1px solid #334155;}
        .side-menu-title{font-size:18px;font-weight:900;}
        .side-menu-close{width:32px;height:32px;background:rgba(255,255,255,0.05);border:1px solid #334155;border-radius:50%;cursor:pointer;color:#cbd5e1;font-size:16px;display:flex;align-items:center;justify-content:center;}
        .side-menu-item{display:flex;align-items:center;gap:10px;padding:14px;border-radius:10px;cursor:pointer;color:#cbd5e1;font-weight:600;font-size:14px;border:none;background:transparent;font-family:inherit;text-align:right;width:100%;margin-bottom:4px;}
        .side-menu-item:active{background:rgba(99,102,241,0.15);}
        .side-menu-icon{font-size:18px;width:34px;height:34px;background:rgba(255,255,255,0.04);border-radius:8px;display:flex;align-items:center;justify-content:center;}
        .side-menu-footer{margin-top:auto;padding-top:16px;border-top:1px solid #334155;text-align:center;font-size:11px;color:#64748b;}
        
        /* Tabs */
        .tabs{display:flex;gap:4px;background:#1e293b;padding:4px;border-radius:16px;border:1px solid #334155;margin-bottom:12px;}
        .tab{flex:1;padding:12px 4px;border:none;background:transparent;color:#64748b;cursor:pointer;border-radius:12px;font-size:11px;font-weight:700;font-family:inherit;text-align:center;}
        .tab.active{background:linear-gradient(135deg,#6366f1,#8b5cf6);color:#fff;box-shadow:0 4px 15px rgba(99,102,241,0.3);}
        
        /* Cards */
        .card{background:#1e293b;border-radius:20px;padding:20px 16px;border:1px solid #334155;}
        .disp{background:#0f172a;border-radius:16px;padding:20px;text-align:center;margin-bottom:16px;border:1px solid #334155;}
        .disp-val{font-size:38px;font-weight:900;letter-spacing:3px;font-variant-numeric:tabular-nums;}
        .disp-label{font-size:10px;color:#64748b;letter-spacing:2px;margin-top:4px;}
        
        /* Inputs */
        .row{display:flex;gap:8px;justify-content:center;align-items:center;margin-bottom:14px;flex-wrap:wrap;}
        .inp{width:65px;padding:12px 8px;border-radius:10px;border:1.5px solid #334155;background:#0f172a;color:#f1f5f9;font-size:16px;text-align:center;font-family:inherit;font-weight:700;outline:none;}
        .inp:focus{border-color:#6366f1;}
        .sep{font-size:20px;color:#818cf8;font-weight:700;}
        
        /* Buttons */
        .btns{display:flex;gap:8px;justify-content:center;flex-wrap:wrap;}
        .btn{padding:14px 20px;border:none;border-radius:10px;font-size:14px;font-weight:700;cursor:pointer;font-family:inherit;min-width:80px;text-align:center;touch-action:manipulation;}
        .btn:active{transform:scale(0.95);opacity:0.8;}
        .btn-b{background:linear-gradient(135deg,#6366f1,#8b5cf6);color:#fff;}
        .btn-g{background:transparent;color:#cbd5e1;border:1.5px solid #334155;}
        .btn-gr{background:linear-gradient(135deg,#10b981,#34d399);color:#fff;}
        .btn-y{background:linear-gradient(135deg,#f59e0b,#fbbf24);color:#1e293b;font-weight:900;}
        .btn-sm{padding:10px 14px;font-size:12px;min-width:auto;}
        
        /* Alarm */
        .alarm-item{background:#273548;border-radius:14px;padding:14px;border:1px solid #334155;display:flex;align-items:center;justify-content:space-between;gap:10px;margin-bottom:8px;}
        .alarm-time{font-size:26px;font-weight:900;letter-spacing:3px;font-variant-numeric:tabular-nums;}
        .alarm-name{font-size:11px;color:#cbd5e1;margin-top:2px;}
        .alarm-days{display:flex;gap:3px;margin-top:4px;flex-wrap:wrap;}
        .alarm-tag{font-size:9px;font-weight:700;padding:2px 6px;border-radius:8px;background:rgba(99,102,241,0.2);color:#818cf8;}
        
        /* Toggle */
        .toggle{position:relative;width:46px;height:24px;display:inline-block;}
        .toggle input{display:none;}
        .toggle-s{position:absolute;inset:0;background:#334155;border-radius:24px;cursor:pointer;transition:0.3s;}
        .toggle-s::before{content:'';position:absolute;width:18px;height:18px;left:3px;bottom:3px;background:#fff;border-radius:50%;transition:0.3s;}
        .toggle input:checked+.toggle-s{background:#10b981;}
        .toggle input:checked+.toggle-s::before{transform:translateX(22px);}
        
        /* Days */
        .days-grid{display:flex;flex-wrap:wrap;gap:6px;justify-content:center;margin-bottom:12px;}
        .day-box{cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:2px;}
        .day-box input{display:none;}
        .day-c{width:36px;height:36px;border-radius:50%;background:#0f172a;border:1.5px solid #334155;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;color:#64748b;transition:0.2s;}
        .day-box input:checked+.day-c{background:#6366f1;color:#fff;border-color:#6366f1;}
        .day-label{font-size:8px;color:#64748b;font-weight:600;}
        
        /* World Clock */
        .world-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(130px,1fr));gap:8px;}
        .city-card{background:#273548;border-radius:12px;padding:14px;border:1px solid #334155;text-align:center;cursor:pointer;}
        .city-name{font-size:13px;font-weight:700;margin-bottom:6px;}
        .city-time{font-size:20px;font-weight:900;color:#818cf8;letter-spacing:1px;margin-bottom:2px;}
        .city-offset{font-size:9px;color:#64748b;}
        
        /* Lap */
        .lap-list{margin-top:12px;max-height:150px;overflow-y:auto;border-radius:10px;border:1.5px solid #334155;background:#0f172a;}
        .lap-item{display:flex;justify-content:space-between;padding:10px 14px;border-bottom:1px solid #1e293b;font-size:13px;font-weight:600;}
        .lap-item:last-child{border-bottom:none;}
        .lap-idx{color:#64748b;}
        .lap-val{color:#818cf8;font-weight:800;}
        
        /* Empty */
        .empty{text-align:center;padding:30px;color:#64748b;}
        .empty-text{font-size:13px;font-weight:600;margin-top:8px;}
        
        /* Content */
        .content{display:none;}
        .content.show{display:block;}
        
        /* Modal */
        .modal-bg{position:fixed;inset:0;background:rgba(0,0,0,0.7);z-index:100;display:none;align-items:center;justify-content:center;padding:16px;}
        .modal-bg.show{display:flex;}
        .modal{background:#1e293b;border-radius:20px;padding:24px 18px;width:100%;max-width:400px;border:1px solid #334155;max-height:85vh;overflow-y:auto;}
        .modal-title{font-size:18px;font-weight:900;text-align:center;margin-bottom:18px;}
        .sel{width:100%;padding:12px;border-radius:10px;border:1.5px solid #334155;background:#0f172a;color:#f1f5f9;font-size:13px;font-family:inherit;font-weight:600;outline:none;margin-bottom:12px;}
        .sel:focus{border-color:#6366f1;}
        
        @media(max-width:400px){.disp-val{font-size:32px;}.alarm-time{font-size:22px;}.tab{font-size:10px;padding:10px 2px;}}
    </style>
</head>
<body>

<!-- Menu Overlay -->
<div class="menu-overlay" id="menuOverlay" onclick="closeMenu()"></div>

<!-- Side Menu -->
<div class="side-menu" id="sideMenu">
    <div class="side-menu-header">
        <span class="side-menu-title">منو</span>
        <button class="side-menu-close" onclick="closeMenu()">X</button>
    </div>
    <button class="side-menu-item" onclick="menuGo('alarm')"><span class="side-menu-icon">Z</span>زنگ هشدار</button>
    <button class="side-menu-item" onclick="menuGo('timer')"><span class="side-menu-icon">T</span>تایمر</button>
    <button class="side-menu-item" onclick="menuGo('sw')"><span class="side-menu-icon">S</span>کرنومتر</button>
    <button class="side-menu-item" onclick="menuGo('world')"><span class="side-menu-icon">W</span>ساعت جهانی</button>
    <button class="side-menu-item" onclick="menuGo('about')"><span class="side-menu-icon">A</span>درباره ما</button>
    <div class="side-menu-footer">
        <p>ساخته شده توسط طاها الهی</p>
        <p>1405/03/22</p>
    </div>
</div>

<div class="c">
    <!-- Top Bar -->
    <div class="top">
        <div class="logo"><div class="logo-icon">T</div>ساعت هوشمند</div>
        <button class="hamburger" onclick="openMenu()">
            <span></span><span></span><span></span>
        </button>
    </div>

    <!-- Tabs -->
    <div class="tabs">
        <button class="tab active" onclick="switchTab('alarm')">زنگ هشدار</button>
        <button class="tab" onclick="switchTab('timer')">تایمر</button>
        <button class="tab" onclick="switchTab('sw')">کرنومتر</button>
        <button class="tab" onclick="switchTab('world')">ساعت جهانی</button>
    </div>

    <!-- About Page -->
    <div class="content" id="about">
        <div class="card" style="text-align:center;">
            <div style="font-size:40px;margin-bottom:12px;">T</div>
            <h2 style="font-size:20px;font-weight:900;margin-bottom:4px;">ساعت هوشمند</h2>
            <p style="font-size:13px;color:#818cf8;margin-bottom:20px;">تایمر، کرنومتر، زنگ هشدار و ساعت جهانی</p>
            <div style="background:#273548;border-radius:10px;padding:12px;margin-bottom:8px;display:flex;justify-content:space-between;"><span style="color:#64748b;">سازنده</span><span style="font-weight:700;">طاها الهی</span></div>
            <div style="background:#273548;border-radius:10px;padding:12px;margin-bottom:8px;display:flex;justify-content:space-between;"><span style="color:#64748b;">سال ساخت</span><span style="font-weight:700;">1405/03/22</span></div>
            <div style="background:#273548;border-radius:10px;padding:12px;margin-bottom:8px;display:flex;justify-content:space-between;"><span style="color:#64748b;">نسخه</span><span style="font-weight:700;">3.0.0</span></div>
            <button class="btn btn-b" style="width:100%;margin-top:16px;" onclick="switchTab('alarm')">بازگشت به برنامه</button>
        </div>
    </div>

    <!-- Alarm -->
    <div class="content show" id="alarm">
        <div class="card">
            <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:16px;">
                <div style="font-size:17px;font-weight:900;">زنگ های هشدار</div>
                <button class="btn btn-b" style="width:40px;height:40px;min-width:40px;border-radius:50%;font-size:22px;padding:0;" onclick="openAdd()">+</button>
            </div>
            <div id="alarmList"><div class="empty"><div class="empty-text">هیچ زنگی تنظیم نشده</div></div></div>
        </div>
    </div>

    <!-- Timer -->
    <div class="content" id="timer">
        <div class="card">
            <div class="disp">
                <div class="disp-val" id="timerDisp">00:00:00</div>
                <div class="disp-label">شمارش معکوس</div>
            </div>
            <div class="row">
                <input type="number" id="th" class="inp" value="0" min="0" max="99"><span class="sep">:</span>
                <input type="number" id="tm" class="inp" value="5" min="0" max="59"><span class="sep">:</span>
                <input type="number" id="ts" class="inp" value="0" min="0" max="59">
            </div>
            <div class="btns">
                <button class="btn btn-b" onclick="startTimer()">شروع</button>
                <button class="btn btn-g" onclick="stopTimer()">توقف</button>
                <button class="btn btn-g" onclick="resetTimer()">بازنشانی</button>
            </div>
        </div>
    </div>

    <!-- Stopwatch -->
    <div class="content" id="sw">
        <div class="card">
            <div class="disp">
                <div class="disp-val" id="swDisp">00:00:00.00</div>
                <div class="disp-label">کرنومتر</div>
            </div>
            <div class="btns">
                <button class="btn btn-b" onclick="startSW()">شروع</button>
                <button class="btn btn-g" onclick="stopSW()">توقف</button>
                <button class="btn btn-g" onclick="resetSW()">بازنشانی</button>
                <button class="btn btn-y" onclick="lapSW()">ثبت دور</button>
            </div>
            <div class="lap-list" id="lapList"><div class="empty"><div class="empty-text">زمان های دور</div></div></div>
        </div>
    </div>

    <!-- World Clock -->
    <div class="content" id="world">
        <div class="card">
            <div style="font-size:17px;font-weight:900;text-align:center;margin-bottom:14px;">ساعت جهانی</div>
            <div class="world-grid" id="worldGrid"></div>
        </div>
    </div>
</div>

<!-- Modal -->
<div class="modal-bg" id="modalBg" onclick="if(event.target===this)closeModal()">
    <div class="modal">
        <div class="modal-title" id="modalTitle">افزودن زنگ جدید</div>
        <div class="row">
            <input type="number" id="modH" class="inp" value="7" min="0" max="23"><span class="sep">:</span>
            <input type="number" id="modM" class="inp" value="0" min="0" max="59">
        </div>
        <div style="text-align:center;font-size:10px;color:#64748b;margin-bottom:12px;">فرمت 24 ساعته</div>
        <input type="text" id="modName" class="inp" style="width:100%;text-align:right;margin-bottom:12px;" value="زنگ هشدار">
        <div style="font-size:10px;font-weight:700;color:#64748b;margin-bottom:8px;">روزهای هفته</div>
        <div class="days-grid" id="daysGrid">
            <label class="day-box"><input type="checkbox" value="6" class="di"><span class="day-c">ش</span><span class="day-label">شنبه</span></label>
            <label class="day-box"><input type="checkbox" value="0" class="di"><span class="day-c">ی</span><span class="day-label">یکشنبه</span></label>
            <label class="day-box"><input type="checkbox" value="1" class="di"><span class="day-c">د</span><span class="day-label">دوشنبه</span></label>
            <label class="day-box"><input type="checkbox" value="2" class="di"><span class="day-c">س</span><span class="day-label">سه شنبه</span></label>
            <label class="day-box"><input type="checkbox" value="3" class="di"><span class="day-c">چ</span><span class="day-label">چهارشنبه</span></label>
            <label class="day-box"><input type="checkbox" value="4" class="di"><span class="day-c">پ</span><span class="day-label">پنجشنبه</span></label>
            <label class="day-box"><input type="checkbox" value="5" class="di"><span class="day-c">ج</span><span class="day-label">جمعه</span></label>
        </div>
        <button class="btn btn-g btn-sm" onclick="toggleAllDays()" style="width:100%;margin-bottom:12px;">انتخاب همه روزها</button>
        <select id="modSound" class="sel">
            <option value="bell">زنگ کلاسیک</option>
            <option value="digital">زنگ دیجیتال</option>
            <option value="melody">ملودی ملایم</option>
            <option value="beep">بوق کوتاه</option>
            <option value="rooster">بانگ خروس</option>
        </select>
        <div class="btns" style="margin-top:16px;">
            <button class="btn btn-gr" onclick="saveAlarm()">ذخیره</button>
            <button class="btn btn-g" onclick="closeModal()">انصراف</button>
        </div>
    </div>
</div>

<script>
// ====== Persian Numbers ======
var pn=['۰','۱','۲','۳','۴','۵','۶','۷','۸','۹'];
function toPn(n){return String(n).replace(/[0-9]/g,function(d){return pn[parseInt(d)];});}
function fmt(h,m,s){
    var r=toPn(String(h).padStart(2,'0'))+':'+toPn(String(m).padStart(2,'0'));
    if(s!==false)r+=':'+toPn(String(s).padStart(2,'0'));
    return r;
}

// ====== Storage ======
var DB={
    get:function(k,d){try{var v=localStorage.getItem(k);return v?JSON.parse(v):d;}catch(e){return d;}},
    set:function(k,v){try{localStorage.setItem(k,JSON.stringify(v));}catch(e){}}
};
function uid(){return 'id_'+Date.now()+'_'+Math.random().toString(36).slice(2,9);}
var dayShorts=['ی','د','س','چ','پ','ج','ش'];

// ====== Menu Functions ======
function openMenu(){
    document.getElementById('menuOverlay').classList.add('show');
    document.getElementById('sideMenu').classList.add('show');
}

function closeMenu(){
    document.getElementById('menuOverlay').classList.remove('show');
    document.getElementById('sideMenu').classList.remove('show');
}

function menuGo(id){
    closeMenu();
    if(id==='about'){
        switchTab('about');
    }else{
        switchTab(id);
    }
}

// ====== Tab Navigation ======
function switchTab(id){
    var tabs=document.querySelectorAll('.tab');
    var contents=document.querySelectorAll('.content');
    for(var i=0;i<tabs.length;i++){tabs[i].classList.remove('active');}
    for(var i=0;i<contents.length;i++){contents[i].classList.remove('show');}
    document.getElementById(id).classList.add('show');
    var tabBtns=document.querySelectorAll('.tab');
    for(var i=0;i<tabBtns.length;i++){
        if(tabBtns[i].getAttribute('onclick').indexOf(id)>=0){
            tabBtns[i].classList.add('active');
        }
    }
    DB.set('tab',id);
}

// ====== Timer Functions ======
var tmrInt=null,tmrSecs=0,tmrRun=false;
function saveTmr(){DB.set('tmr',{s:tmrSecs,r:tmrRun,at:Date.now()});}
function updTmr(){
    var h=Math.floor(tmrSecs/3600),m=Math.floor((tmrSecs%3600)/60),s=tmrSecs%60;
    document.getElementById('timerDisp').textContent=fmt(h,m,s);
}
function stopTimer(){if(tmrInt)clearInterval(tmrInt);tmrInt=null;tmrRun=false;saveTmr();}
function startTimer(){
    if(tmrRun)return;
    if(tmrSecs<=0){
        var h=Math.max(0,parseInt(document.getElementById('th').value)||0);
        var m=Math.max(0,Math.min(59,parseInt(document.getElementById('tm').value)||0));
        var s=Math.max(0,Math.min(59,parseInt(document.getElementById('ts').value)||0));
        tmrSecs=h*3600+m*60+s;
        if(tmrSecs<=0)return;
    }
    tmrRun=true;saveTmr();updTmr();
    tmrInt=setInterval(function(){if(tmrSecs>0){tmrSecs--;updTmr();if(tmrSecs%5===0)saveTmr();}if(tmrSecs<=0){stopTimer();tmrSecs=0;updTmr();saveTmr();}},1000);
}
function resetTimer(){stopTimer();tmrSecs=0;updTmr();saveTmr();}

// ====== Stopwatch Functions ======
var swInt=null,swCs=0,swRun=false,laps=[];
function saveSW(){DB.set('sw',{c:swCs,r:swRun,at:Date.now()});DB.set('laps',laps);}
function updSW(){
    var cs=swCs,h=Math.floor(cs/360000),m=Math.floor((cs%360000)/6000),s=Math.floor((cs%6000)/100),c=cs%100;
    document.getElementById('swDisp').textContent=toPn(String(h).padStart(2,'0'))+':'+toPn(String(m).padStart(2,'0'))+':'+toPn(String(s).padStart(2,'0'))+'.'+toPn(String(c).padStart(2,'0'));
}
function renderLaps(){
    var list=document.getElementById('lapList');
    if(laps.length===0){list.innerHTML='<div class="empty"><div class="empty-text">زمان های دور اینجا ثبت میشوند</div></div>';return;}
    list.innerHTML='';
    for(var i=laps.length-1;i>=0;i--){var d=document.createElement('div');d.className='lap-item';d.innerHTML='<span class="lap-idx">دور '+toPn(laps.length-i)+'</span><span class="lap-val">'+laps[i]+'</span>';list.appendChild(d);}
}
function stopSW(){if(swInt)clearInterval(swInt);swInt=null;swRun=false;saveSW();}
function startSW(){if(swRun)return;swRun=true;saveSW();swInt=setInterval(function(){swCs++;updSW();if(swCs%100===0)saveSW();},10);}
function resetSW(){stopSW();swCs=0;laps=[];updSW();renderLaps();saveSW();}
function lapSW(){if(!swRun&&swCs===0)return;laps.push(document.getElementById('swDisp').textContent);renderLaps();saveSW();}

// ====== Alarm Functions ======
var editId=null;
function getDays(){var cbs=document.querySelectorAll('#daysGrid .di:checked');var days=[];for(var i=0;i<cbs.length;i++){days.push(parseInt(cbs[i].value));}return days;}
function setDays(days){var cbs=document.querySelectorAll('#daysGrid .di');for(var i=0;i<cbs.length;i++){cbs[i].checked=days.includes(parseInt(cbs[i].value));}}
function toggleAllDays(){var cbs=document.querySelectorAll('#daysGrid .di');var all=true;for(var i=0;i<cbs.length;i++){if(!cbs[i].checked)all=false;}for(var i=0;i<cbs.length;i++){cbs[i].checked=!all;}}

function renderAlarms(){
    var alarms=DB.get('alarms',[]),list=document.getElementById('alarmList');
    if(alarms.length===0){list.innerHTML='<div class="empty"><div class="empty-text">هیچ زنگی تنظیم نشده</div></div>';return;}
    list.innerHTML='';
    for(var i=0;i<alarms.length;i++){
        var a=alarms[i];
        var daysTxt=(!a.days||a.days.length===0||a.days.length===7)?'همه روزها':a.days.map(function(d){return dayShorts[d];}).join('،');
        var div=document.createElement('div');
        div.className='alarm-item'+(a.enabled?'':' disabled');
        div.innerHTML='<div class="alarm-info"><div class="alarm-time">'+fmt(a.hours,a.minutes,false)+'</div><div class="alarm-name">'+(a.name||'زنگ هشدار')+'</div><div class="alarm-days"><span class="alarm-tag">'+daysTxt+'</span></div></div><div class="alarm-actions"><label class="toggle"><input type="checkbox" '+(a.enabled?'checked':'')+' onchange="toggleAlarm(\''+a.id+'\',this.checked)"><span class="toggle-s"></span></label><button class="btn btn-g btn-sm" onclick="openEdit(\''+a.id+'\')">ویرایش</button><button class="btn btn-g btn-sm" style="color:#ef4444;border-color:#ef4444;" onclick="deleteAlarm(\''+a.id+'\')">حذف</button></div>';
        list.appendChild(div);
    }
}

function openAdd(){
    editId=null;
    document.getElementById('modalTitle').textContent='افزودن زنگ جدید';
    document.getElementById('modH').value=7;document.getElementById('modM').value=0;
    document.getElementById('modName').value='زنگ هشدار';document.getElementById('modSound').value='bell';
    setDays([]);document.getElementById('modalBg').classList.add('show');
}

function openEdit(id){
    var alarms=DB.get('alarms',[]),a=null;
    for(var i=0;i<alarms.length;i++){if(alarms[i].id===id){a=alarms[i];break;}}
    if(!a)return;editId=id;
    document.getElementById('modalTitle').textContent='ویرایش زنگ';
    document.getElementById('modH').value=a.hours;document.getElementById('modM').value=a.minutes;
    document.getElementById('modName').value=a.name||'';document.getElementById('modSound').value=a.sound||'bell';
    setDays(a.days||[]);document.getElementById('modalBg').classList.add('show');
}

function closeModal(){document.getElementById('modalBg').classList.remove('show');editId=null;}

function saveAlarm(){
    var h=Math.max(0,Math.min(23,parseInt(document.getElementById('modH').value)||0));
    var m=Math.max(0,Math.min(59,parseInt(document.getElementById('modM').value)||0));
    var name=document.getElementById('modName').value.trim()||'زنگ هشدار';
    var sound=document.getElementById('modSound').value||'bell';
    var days=getDays();
    var alarms=DB.get('alarms',[]);
    if(editId){for(var i=0;i<alarms.length;i++){if(alarms[i].id===editId){alarms[i].hours=h;alarms[i].minutes=m;alarms[i].name=name;alarms[i].sound=sound;alarms[i].days=days;break;}}}
    else{alarms.push({id:uid(),hours:h,minutes:m,name:name,sound:sound,days:days,enabled:true});}
    DB.set('alarms',alarms);renderAlarms();closeModal();
}

function toggleAlarm(id,en){var alarms=DB.get('alarms',[]);for(var i=0;i<alarms.length;i++){if(alarms[i].id===id){alarms[i].enabled=en;break;}}DB.set('alarms',alarms);}
function deleteAlarm(id){if(!confirm('حذف شود؟'))return;var alarms=DB.get('alarms',[]);alarms=alarms.filter(function(a){return a.id!==id;});DB.set('alarms',alarms);renderAlarms();}

// ====== World Clock ======
var cities=[{name:'تهران',off:3.5},{name:'نیویورک',off:-4},{name:'لندن',off:1},{name:'توکیو',off:9},{name:'دبی',off:4},{name:'پکن',off:8},{name:'مسکو',off:3},{name:'سیدنی',off:10},{name:'پاریس',off:2},{name:'برلین',off:2},{name:'استانبول',off:3},{name:'دهلی نو',off:5.5}];
function getCityTime(oh){var now=new Date();var utc=now.getTime()+(now.getTimezoneOffset()*60000);var ct=new Date(utc+(oh*3600000));return fmt(ct.getHours(),ct.getMinutes(),ct.getSeconds());}
function formatOff(off){var sign=off>=0?'+':'';var h=Math.floor(Math.abs(off));var m=Math.round((Math.abs(off)-h)*60);return sign+h+':'+(m===30?'30':'00');}
function updWorld(){
    var grid=document.getElementById('worldGrid');grid.innerHTML='';
    for(var i=0;i<cities.length;i++){var c=cities[i];var t=getCityTime(c.off);var offStr=formatOff(c.off);var card=document.createElement('div');card.className='city-card';card.innerHTML='<div class="city-name">'+c.name+'</div><div class="city-time">'+t+'</div><div class="city-offset">UTC '+offStr+'</div>';grid.appendChild(card);}
}
setInterval(updWorld,1000);

// ====== Init ======
switchTab('alarm');updTmr();updSW();updWorld();renderAlarms();renderLaps();
var s=DB.get('tmr',null);if(s&&s.s>0){var e=Math.floor((Date.now()-(s.at||Date.now()))/1000);tmrSecs=s.r?Math.max(0,s.s-e):s.s;updTmr();}
s=DB.get('sw',null);laps=DB.get('laps',[]);if(s&&s.c>0){var e=Math.floor((Date.now()-(s.at||Date.now()))/10);swCs=s.r?s.c+e:s.c;updSW();}renderLaps();
</script>
</body>
</html>
