<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Morning Flow - Run For Recovery</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Billabong&display=swap" rel="stylesheet">
<style>
body { margin:0; font-family:'Poppins',sans-serif; background: linear-gradient(160deg,#FFD194,#D6A4A4); color:#fff; }
header{text-align:center;padding:1rem;}
header h1{ font-family:'Billabong', cursive; font-size:3rem; text-shadow:0 0 12px #fff; margin:0; letter-spacing:1px;}
main{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:1rem;padding:1rem;justify-items:center;}
.card{ background: rgba(255,255,255,0.15); backdrop-filter: blur(15px); border-radius:20px; padding:1rem; box-shadow:0 12px 25px rgba(0,0,0,0.25); width:90%; max-width:360px; position:relative; }
.time-boxes {display:flex;justify-content:space-between;margin-top:1rem;}
.time-box{ flex:1; margin:0 0.3rem; background: rgba(255,111,97,0.3); border-radius:12px; text-align:center; padding:0.5rem; font-weight:600;}
textarea#journalInput{ width:100%; height:100px; border-radius:15px; border:none; padding:0.75rem; background: rgba(255,255,255,0.08); backdrop-filter: blur(10px); color:#fff; font-family:'Poppins',sans-serif; font-size:1rem; resize:vertical; box-shadow: 0 4px 15px rgba(0,0,0,0.25);}
#journalEntries{ max-height:180px; overflow-y:auto; margin-top:0.5rem;}
#journalEntries p{ background: rgba(255,255,255,0.08); padding:0.5rem; border-radius:12px; margin-bottom:0.5rem; word-wrap:break-word; font-family:'Poppins',sans-serif; font-size:0.95rem;}
button{ padding:0.5rem 1rem; border:none; border-radius:12px; background:#FF6F61; color:#fff; font-weight:600; cursor:pointer; margin-top:0.5rem; transition: transform 0.2s;}
button:hover{transform: scale(1.05);}
.habit-item{ display:flex; align-items:center; margin:0.5rem 0;}
.habit-item input[type="checkbox"]{ width:24px; height:24px; margin-right:0.6rem; cursor:pointer; accent-color:#FF6F61; transition: transform 0.2s;}
.habit-item input[type="checkbox"]:hover{transform: scale(1.2);}
.breathing-circle{ width:100px; height:100px; margin:1rem auto; border-radius:50%; background: linear-gradient(135deg,#FFD194,#FF6F61); display:flex; align-items:center; justify-content:center; font-weight:600; font-size:1.2rem; color:#fff; transition: width 4s ease-in-out, height 4s ease-in-out;}
footer{background: rgba(0,0,0,0.2); padding: 1.5rem; text-align:center; border-top: 2px solid #FF6F61;}
footer a{color:#FF6F61; text-decoration:none; font-weight:600;}
.start-day-box{ background: rgba(255,255,255,0.12); padding:1rem; border-radius:18px; text-align:center; margin-bottom:1rem; box-shadow:0 6px 15px rgba(0,0,0,0.2);}
select#moodSelect{ width:100%; border-radius:12px; padding:0.5rem; margin-bottom:0.5rem; border:none; background: rgba(255,255,255,0.08); color:#fff; backdrop-filter: blur(5px); }
.confetti-piece{position:fixed;width:10px;height:10px;pointer-events:none;z-index:9999;}
</style>
</head>
<body>
<header>
<h1>Morning Flow</h1>
</header>
<main>

<!-- Sobriety Timer -->
<div class="card">
<h2>Sobriety Timer</h2>
<input type="date" id="sobrietyDate" style="border-radius:15px; padding:0.5rem; border:none; background:rgba(255,255,255,0.1); color:#fff; text-align:center;">
<div class="time-boxes">
<div class="time-box"><span id="days">00</span><br>Days</div>
<div class="time-box"><span id="hours">00</span><br>Hours</div>
<div class="time-box"><span id="minutes">00</span><br>Minutes</div>
<div class="time-box"><span id="seconds">00</span><br>Seconds</div>
</div>
<button id="shareSobrietyBtn">Share My Sobriety</button>
</div>

<!-- Daily Reflection -->
<div class="card start-day-box">
<h2>Daily Reflection</h2>
<a href="https://www.aa.org/daily-reflection" target="_blank"><button>Read Daily Reflection</button></a>
</div>

<!-- Box Breathing -->
<div class="card">
<h2>Box Breathing</h2>
<div class="breathing-circle" id="breathingCircle">Inhale</div>
</div>

<!-- Daily Habits -->
<div class="card">
<h2>Daily Habits</h2>
<div class="habit-item"><input type="checkbox" class="habit-check"> Pray / Reflect</div>
<div class="habit-item"><input type="checkbox" class="habit-check"> Call Someone</div>
<div class="habit-item"><input type="checkbox" class="habit-check"> Read Daily Reflection</div>
<button id="completeHabitsBtn">Complete Habits</button>
</div>

<!-- Journal -->
<div class="card">
<h2>Journal</h2>
<label for="moodSelect">How are you feeling today?</label>
<select id="moodSelect">
<option value="" disabled selected>Select your mood</option>
<option value="Happy 😊">Happy 😊</option>
<option value="Sad 😢">Sad 😢</option>
<option value="Anxious 😰">Anxious 😰</option>
<option value="Excited 😃">Excited 😃</option>
<option value="Grateful 🙏">Grateful 🙏</option>
<option value="Tired 😴">Tired 😴</option>
<option value="Angry 😡">Angry 😡</option>
</select>
<textarea id="journalInput" placeholder="Write your gratitude or thoughts..."></textarea>
<div style="display:flex;gap:0.5rem;margin-top:0.5rem;">
<button id="saveJournalBtn">Save Entry</button>
</div>
<div id="journalEntries"></div>
</div>

<!-- Daily Quote & Bible Verse -->
<div class="card">
<h2>Daily Quote</h2>
<div id="quote">Tap for another quote</div>
<button id="nextQuoteBtn">Tap for another quote</button>
<h2>Action for Today</h2>
<div id="word">Take one positive step today.</div>
<h2>Bible Verse</h2>
<div id="verse">Tap for another verse</div>
<button id="nextVerseBtn">Tap for another verse</button>
</div>

<!-- Meetings & Big Book -->
<div class="card">
<h2>Meetings & Big Book</h2>
<p><a href="https://www.aa.org/pages/en_US/find-aa-resources" target="_blank">Online Meetings</a></p>
<p><a href="https://www.aa.org/pages/en_US/meeting-guide" target="_blank">In-Person Meetings</a></p>
<p><a href="https://share.google/C3Sj4Qc2yk8mIjMtV" target="_blank">Digital Big Book</a></p>
</div>

</main>

<footer>
<p>Designed by Corey © RunForRecovery Productions</p>
<p>Follow us: <a href="https://www.instagram.com/reverserunners" target="_blank">Instagram</a> | <a href="https://www.facebook.com/" target="_blank">Facebook</a></p>
<p>Suicide & Support Hotline: <strong>1-800-273-8255</strong></p>
</footer>

<script>
// ===== SOBRIETY TIMER =====
const sobrietyDateInput = document.getElementById('sobrietyDate');
function updateTimer() {
    if(!sobrietyDateInput.value) return;
    const now = new Date();
    const date = new Date(sobrietyDateInput.value);
    let diff = now - date;
    if(diff < 0) diff = 0;
    document.getElementById('days').textContent = Math.floor(diff/1000/60/60/24);
    document.getElementById('hours').textContent = Math.floor(diff/1000/60/60)%24;
    document.getElementById('minutes').textContent = Math.floor(diff/1000/60)%60;
    document.getElementById('seconds').textContent = Math.floor(diff/1000)%60;
}
sobrietyDateInput.addEventListener('change', updateTimer);
setInterval(updateTimer, 1000);
document.getElementById('shareSobrietyBtn').addEventListener('click',()=>alert(`I've been sober since ${sobrietyDateInput.value || 'N/A'}`));

// ===== BOX BREATHING =====
const circle = document.getElementById('breathingCircle');
const phases = [
    { name: "Inhale", size: 150 },
    { name: "Hold", size: 150 },
    { name: "Exhale", size: 100 },
    { name: "Hold", size: 100 }
];
let currentPhase = 0;
function nextPhase() {
    const phase = phases[currentPhase];
    circle.textContent = phase.name;
    circle.style.width = phase.size + "px";
    circle.style.height = phase.size + "px";
    currentPhase = (currentPhase + 1) % phases.length;
}
nextPhase();
setInterval(nextPhase, 4000);

// ===== DAILY HABITS =====
function createConfetti() {
    for(let i=0;i<50;i++){
        const c=document.createElement('div');
        c.classList.add('confetti-piece');
        c.style.left=Math.random()*window.innerWidth+'px';
        c.style.backgroundColor=`hsl(${Math.random()*360},100%,50%)`;
        document.body.appendChild(c);
        setTimeout(()=>c.remove(),2000);
    }
}
document.getElementById('completeHabitsBtn').addEventListener('click',()=>{
    const checks=document.querySelectorAll('.habit-check');
    let allChecked=true;
    checks.forEach(c=>{if(!c.checked) allChecked=false;});
    if(allChecked){createConfetti(); alert("Well done! All habits completed!");}
    else alert("Please complete all habits first.");
});

// ===== JOURNAL =====
const journalInput = document.getElementById('journalInput');
const journalEntriesDiv = document.getElementById('journalEntries');
document.getElementById('saveJournalBtn').addEventListener('click', ()=>{
    if(journalInput.value.trim()==='') return;
    const p=document.createElement('p');
    const mood=document.getElementById('moodSelect').value || '';
    p.textContent=mood + ' - ' + journalInput.value;
    journalEntriesDiv.prepend(p);
    journalInput.value='';
});

// ===== QUOTES & VERSES =====
const quotes=[
"Keep pushing forward!","Small steps every day.","Courage conquers fear","One day at a time",
"Progress, not perfection","You are stronger than you think","Recovery is a journey, not a race",
"Believe in yourself and your path","Every sunrise is a new beginning","Let go of what you cannot control",
"Strength grows in moments of challenge","Your story is not over yet","Change is possible, one choice at a time",
"Focus on what you can do today","Gratitude turns what we have into enough","Healing is not linear",
"Small victories lead to big wins","Stay present, breathe, and move forward","You are capable of more than you imagine","Hope is stronger than fear"
];
const verses=[
"Philippians 4:13 - I can do all things through Christ who strengthens me.",
"Jeremiah 29:11 - For I know the plans I have for you, declares the Lord.",
"Psalm 23:1 - The Lord is my shepherd; I shall not want.",
"Isaiah 40:31 - Those who hope in the Lord will renew their strength.",
"Romans 12:12 - Be joyful in hope, patient in affliction, faithful in prayer."
];
let quoteIndex=0;
let verseIndex=0;
document.getElementById('nextQuoteBtn').addEventListener('click',()=>{
    quoteIndex=(quoteIndex+1)%quotes.length;
    document.getElementById('quote').textContent=quotes[quoteIndex];
});
document.getElementById('nextVerseBtn').addEventListener('click',()=>{
    verseIndex=(verseIndex+1)%verses.length;
    document.getElementById('verse').textContent=verses[verseIndex];
});
</script>
</body>
</html>
