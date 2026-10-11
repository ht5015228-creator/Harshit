
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#10152d">
<title>Study Master Pro</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#0b1024;color:#f5f6ff;font-family:Arial,sans-serif}
header{padding:22px;background:linear-gradient(130deg,#344dba,#752eb1)}
h1{margin:0;font-size:25px}
main{max-width:650px;margin:auto;padding:14px}
.card{background:#171e39;border:1px solid #303c60;border-radius:18px;padding:17px;margin:12px 0}
.hero{text-align:center;background:linear-gradient(145deg,#283e75,#33204e)}
.pet{font-size:76px;margin:8px}
.muted{color:#b5c1df;font-size:13px}
.stats{display:grid;grid-template-columns:repeat(2,1fr);gap:9px}
.stat{background:#222d4d;padding:13px;border-radius:12px}
.stat strong{display:block;font-size:23px;color:#ffda76;margin-top:6px}
button{padding:12px;border:0;border-radius:10px;background:#6388ff;color:white;font-weight:bold}
input,select{width:100%;padding:12px;background:#0d1530;color:white;border:1px solid #39476b;border-radius:9px}
label{display:block;margin:12px 0 6px;color:#bdc9e3;font-size:13px}
.row{display:flex;gap:8px;flex-wrap:wrap}
.row>*{flex:1}
nav{display:grid;grid-template-columns:repeat(3,1fr);gap:7px}
nav button{background:#202c4b;font-size:12px}
section[hidden]{display:none}
#clock{text-align:center;font-size:53px;font-weight:bold;color:#8fc9ff;margin:20px}
.bar{height:9px;background:#303b59;border-radius:10px;overflow:hidden}
.bar div{height:100%;background:#6fe1b5;width:0}
.item{display:flex;gap:8px;align-items:center;padding:12px 0;border-bottom:1px solid #303b59}
.item span{flex:1;overflow-wrap:anywhere}
.item button{padding:8px}
footer{text-align:center;padding:20px;color:#94a2c4;font-size:12px}
</style>
</head>
<body>
<header>
<h1>🎓 Study Master Pro</h1>
<p>Study • Focus • Grow • Earn Coins</p>
</header>
<main>
<nav>
<button onclick="tab('home')">🏠 Home</button>
<button onclick="tab('focus')">⏱ Focus</button>
<button onclick="tab('tasks')">🎯 Targets</button>
<button onclick="tab('schedule')">📅 Timetable</button>
<button onclick="tab('rewards')">🪙 Rewards</button>
<button onclick="tab('progress')">📈 Progress</button>
</nav>

<section id="home">
<div class="card hero">
<div class="pet" id="student">👨‍🎓</div>
<h2 id="greeting">Your Study Buddy!</h2>
<p id="mood">चलो, आज कुछ नया सीखें!</p>
<div class="stats">
<div class="stat">🪙 Coins<strong id="coins">0</strong></div>
<div class="stat">⭐ XP<strong id="xp">0</strong></div>
<div class="stat">📚 आज की पढ़ाई<strong id="minutes">0 min</strong></div>
<div class="stat">🎯 Target<strong id="percent">0%</strong></div>
</div>
</div>
<div class="card">
<h3>🎯 Daily Study Goal</h3>
<label for="goal">आज कितने मिनट पढ़ना है?</label>
<input id="goal" type="number" min="1" max="1440" value="120">
<br><br><button onclick="saveGoal()">Save Goal</button>
<div class="bar" style="margin-top:15px"><div id="goalBar"></div></div>
<p class="muted" id="goalText">शुरुआत करो!</p>
</div>
<div class="card">
<h3>🚀 Quick Start</h3>
<button onclick="tab('focus')">Start Studying →</button>
</div>
</section>

<section id="focus" hidden>
<div class="card">
<h2>⏱ Focus Timer</h2>
<label for="subject">Subject</label>
<select id="subject">
<option>Maths</option><option>Science</option><option>English</option>
<option>Hindi</option><option>Social Science</option><option>Art</option>
</select>
<div id="clock">25:00</div>
<div class="row">
<button onclick="start()">▶ Start</button>
<button onclick="pause()">Ⅱ Pause</button>
<button onclick="reset()">↻ Reset</button>
</div>
<p id="timerMsg" class="muted">एक focus session चुनो और शुरू करो।</p>
<div class="row">
<button onclick="preset(15)">15 min</button>
<button onclick="preset(25)">25 min</button>
<button onclick="preset(45)">45 min</button>
</div>
<p class="muted">Timer पूरा करने पर virtual coins मिलेंगे। Pause करने पर समय रुक जाएगा।</p>
</div>
</section>

<section id="tasks" hidden>
<div class="card">
<h2>🎯 Daily Targets</h2>
<label for="task">आज क्या पूरा करना है?</label>
<input id="task" maxlength="100" placeholder="Maths के 10 सवाल">
<br><br><button onclick="addTask()">+ Add Target</button>
<div id="taskList"></div>
</div>
</section>

<section id="schedule" hidden>
<div class="card">
<h2>📅 My Timetable</h2>
<label for="day">Day</label>
<select id="day">
<option>Every day</option><option>Monday</option><option>Tuesday</option>
<option>Wednesday</option><option>Thursday</option>
<option>Friday</option><option>Saturday</option><option>Sunday</option>
</select>
<label for="activity">Subject / Activity</label>
<input id="activity" maxlength="80" placeholder="Science revision">
<div class="row">
<div><label for="from">Start</label><input id="from" type="time" value="17:00"></div>
<div><label for="to">End</label><input id="to" type="time" value="18:00"></div>
</div>
<br><button onclick="addSchedule()">+ Add Schedule</button>
<div id="scheduleList"></div>
</div>
</section>

<section id="rewards" hidden>
<div class="card hero">
<div class="pet">🏆</div>
<h2>Study Reward Shop</h2>
<p>पढ़ाई करके coins कमाओ और अपने cartoon को upgrade करो!</p>
<div class="stats">
<div class="stat">🪙 Balance<strong id="shopCoins">0</strong></div>
<div class="stat">⭐ Level<strong id="level">1</strong></div>
</div>
</div>
<div class="card">
<h3>🛍️ Items</h3>
<div class="item"><span>📚 Book Pack <small>50 coins</small></span><button onclick="buy(50,'📚')">Unlock</button></div>
<div class="item"><span>🎧 Study Headphones <small>100 coins</small></span><button onclick="buy(100,'🎧')">Unlock</button></div>
<div class="item"><span>🏆 Golden Trophy <small>200 coins</small></span><button onclick="buy(200,'🏆')">Unlock</button></div>
<p class="muted">ये केवल virtual items हैं। Coins को रुपये में बदलने या निकालने की सुविधा नहीं है।</p>
<div id="inventory"></div>
</div>
</section>

<section id="progress" hidden>
<div class="card">
<h2>📈 Your Progress</h2>
<div class="stats">
<div class="stat">आज के मिनट<strong id="pMinutes">0</strong></div>
<div class="stat">पूरे Tasks<strong id="pTasks">0</strong></div>
<div class="stat">Sessions<strong id="pSessions">0</strong></div>
<div class="stat">कुल XP<strong id="pXp">0</strong></div>
</div>
<h3>Study History</h3>
<div id="history"></div>
<button onclick="backup()">Download Backup</button>
</div>
</section>
<footer>Study Master Pro • Every minute of learning counts!</footer>
</main>

<script>
const $=id=>document.getElementById(id);
const KEY='smp_cartoon_v1';
const dateKey=()=>new Date().toLocaleDateString('en-CA');
const initial=()=>({
 coins:0,xp:0,goal:120,tasks:[],schedule:[],
 items:[],logs:{},lastDay:dateKey()
});
function load(){
 try{return {...initial(),...JSON.parse(localStorage.getItem(KEY))};}
 catch(e){return initial();}
}
let d=load();
function save(){
 try{localStorage.setItem(KEY,JSON.stringify(d));}
 catch(e){alert('Storage issue. Backup save karne ki koshish karo.');}
}
function today(){
 if(d.lastDay!==dateKey()){d.lastDay=dateKey();}
 if(!d.logs[dateKey()])d.logs[dateKey()]={minutes:0,sessions:0,subjects:{}};
 return d.logs[dateKey()];
}
function tab(id){
 document.querySelectorAll('main section').forEach(s=>s.hidden=s.id!==id);
 if(id==='home'||id==='progress'||id==='rewards')render();
}
function saveGoal(){
 let n=Number($('goal').value);
 if(!Number.isInteger(n)||n<1||n>1440){alert('1 से 1440 मिनट चुनो।');return;}
 d.goal=n;save();render();
}
function addTask(){
 let t=$('task').value.trim();if(!t){alert('पहले target लिखो।');return;}
 d.tasks.push({id:Date.now()+Math.random(),text:t,done:false});
 $('task').value='';save();render();
}
function addSchedule(){
 let subject=$('activity').value.trim(),from=$('from').value,to=$('to').value;
 if(!subject){alert('Subject लिखो।');return;}
 if(!from||!to||from>=to){alert('सही start और end time चुनो।');return;}
 d.schedule.push({id:Date.now()+Math.random(),day:$('day').value,subject,from,to});
 $('activity').value='';save();render();
}
function row(box,text,remove){
 let el=document.createElement('div');el.className='item';
 let s=document.createElement('span');s.textContent=text;
 let b=document.createElement('button');b.textContent='✕';b.onclick=remove;
 el.append(s,b);box.append(el);
}
function render(){
 today();
 $('coins').textContent=d.coins;$('xp').textContent=d.xp;
 $('shopCoins').textContent=d.coins;
 $('level').textContent=1+Math.floor(d.xp/100);
 $('goal').value=d.goal;
 let m=today().minutes,p=Math.min(100,Math.round(m/d.goal*100));
 $('minutes').textContent=m+' min';$('percent').textContent=p+'%';
 $('goalBar').style.width=p+'%';
 $('goalText').textContent=m>=d.goal?'Goal complete! Great job 🎉':(d.goal-m)+' मिनट बाकी हैं।';
 $('mood').textContent=m>=d.goal?'वाह! तुम्हारा student खुश है! 🎉':'एक focus session शुरू करो!';
 $('student').textContent=m>=d.goal?'🧑‍🎓🏆':m>0?'👨‍🎓✨':'👨‍🎓';
 $('taskList').replaceChildren();
 d.tasks.forEach(t=>{
  let el=document.createElement('div');el.className='item';
  let cb=document.createElement('input');cb.type='checkbox';cb.checked=t.done;cb.style.width='20px';
  cb.onchange=()=>{t.done=cb.checked;save();render();};
  let s=document.createElement('span');s.textContent=t.text;
  if(t.done)s.style.textDecoration='line-through';
  let b=document.createElement('button');b.textContent='✕';
  b.onclick=()=>{d.tasks=d.tasks.filter(x=>x.id!==t.id);save();render();};
  el.append(cb,s,b);$('taskList').append(el);
 });
 $('scheduleList').replaceChildren();
 d.schedule.forEach(s=>row($('scheduleList'),s.day+' • '+s.from+'–'+s.to+' • '+s.subject,()=>{
  d.schedule=d.schedule.filter(x=>x.id!==s.id);save();render();
 }));
 $('inventory').textContent='Unlocked: '+(d.items.join(' ')||'अभी कोई item नहीं');
 $('pMinutes').textContent=m;$('pTasks').textContent=d.tasks.filter(t=>t.done).length;
 $('pSessions').textContent=today().sessions;$('pXp').textContent=d.xp;
 $('history').replaceChildren();
 Object.keys(d.logs).sort().reverse().slice(0,7).forEach(k=>{
  let p=document.createElement('p');p.textContent=k+' — '+d.logs[k].minutes+' minutes';
  $('history').append(p);
 });
}
function buy(cost,item){
 if(d.items.includes(item)){alert('यह item पहले से unlocked है।');return;}
 if(d.coins<cost){alert('Coins कम हैं। पहले पढ़ाई करके कमाओ!');return;}
 d.coins-=cost;d.items.push(item);save();render();alert('Item unlocked '+item);
}
let duration=25*60,left=duration,interval=null,endAt=0;
let running=false;
function showClock(){
 $('clock').textContent=String(Math.floor(left/60)).padStart(2,'0')+':'+String(left%60).padStart(2,'0');
}
function preset(n){pause();duration=n*60;left=duration;showClock();$('timerMsg').textContent=n+' मिनट का focus session';}
function start(){
 if(running)return;
 if(left<=0){left=duration;}
 running=true;endAt=Date.now()+left*1000;
 $('timerMsg').textContent='Focus चालू है — '+$('subject').value;
 interval=setInterval(tick,250);tick();
}
function tick(){
 left=Math.max(0,Math.ceil((endAt-Date.now())/1000));showClock();
 if(left<=0)finish();
}
function pause(){
 if(running){
  left=Math.max(0,Math.ceil((endAt-Date.now())/1000));
  clearInterval(interval);interval=null;running=false;showClock();
  $('timerMsg').textContent='Timer paused';
 }
}
function reset(){
 pause();left=duration;showClock();$('timerMsg').textContent='Timer reset';
}
function finish(){
 clearInterval(interval);interval=null;running=false;left=0;showClock();
 let mins=Math.round(duration/60),log=today(),sub=$('subject').value;
 log.minutes+=mins;log.sessions++;log.subjects[sub]=(log.subjects[sub]||0)+mins;
 d.coins+=mins;d.xp+=mins;save();render();
 $('timerMsg').textContent='Session complete! +'+mins+' coins 🎉';
 alert('बहुत बढ़िया! '+mins+' virtual coins और '+mins+' XP मिले।');
}
function backup(){
 let blob=new Blob([JSON.stringify(d,null,2)],{type:'application/json'});
 let url=URL.createObjectURL(blob),a=document.createElement('a');
 a.href=url;a.download='study-master-backup.json';a.click();
 setTimeout(()=>URL.revokeObjectURL(url),1000);
}
showClock();render();
</script>
</body>
</html>

