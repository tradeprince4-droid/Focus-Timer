
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Focus Timer</title>
<style>
*{box-sizing:border-box}
body{margin:0;min-height:100vh;display:grid;place-items:center;background:radial-gradient(circle,#243b55,#090d18 65%);color:white;font-family:Arial;text-align:center;padding:20px}
.app{max-width:500px;width:100%;background:#111a2b;border:1px solid #334660;border-radius:25px;padding:30px}
button{padding:12px 16px;margin:5px;border:0;border-radius:10px;cursor:pointer;font-weight:bold}
.mode button{background:#243651;color:white}
.mode .active,.primary{background:#68f0ca;color:#09221c}
.time{font-size:clamp(60px,17vw,100px);font-weight:bold;margin:30px 0}
</style>
</head>
<body>
<main class="app">
<p>FOCUS • BREATHE • REPEAT</p><h1>Deep Work Timer</h1>
<div class="mode">
<button class="active" onclick="setMode(25,this)">Focus</button>
<button onclick="setMode(5,this)">Short Break</button>
<button onclick="setMode(15,this)">Long Break</button>
</div>
<div class="time" id="time">25:00</div>
<p id="status">Ready when you are.</p>
<button class="primary" id="start">Start</button><button onclick="reset()">Reset</button>
</main>
<script>
let duration=1500,left=1500,timer=null;
const time=document.getElementById("time");
const status=document.getElementById("status");
const start=document.getElementById("start");
function paint(){time.textContent=String(Math.floor(left/60)).padStart(2,"0")+":"+String(left%60).padStart(2,"0")}
function setMode(min,btn){
clearInterval(timer);timer=null;duration=min*60;left=duration;
start.textContent="Start";status.textContent="Ready when you are.";
document.querySelectorAll(".mode button").forEach(b=>b.classList.remove("active"));
btn.classList.add("active");paint();
}
start.onclick=()=>{
if(timer){clearInterval(timer);timer=null;start.textContent="Resume";status.textContent="Paused.";return}
start.textContent="Pause";status.textContent="Stay focused.";
timer=setInterval(()=>{
left--;paint();
if(left<=0){clearInterval(timer);timer=null;start.textContent="Start Again";status.textContent="Session complete!";alert("Session complete!")}
},1000);
};
function reset(){clearInterval(timer);timer=null;left=duration;paint();start.textContent="Start";status.textContent="Timer reset."}
paint();
</script>
</body>
</html>
# Focus-Timer
