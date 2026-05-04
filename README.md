# Birthday
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For You ❤️</title>

<style>
body{
    margin:0;
    overflow:hidden;
    font-family:'Segoe UI',sans-serif;
    background:linear-gradient(45deg,#ff004c,#000,#1e3cff,#8000ff);
    color:white;
}

/* Pages */
.page{display:none;height:100vh;justify-content:center;align-items:center;flex-direction:column;text-align:center;padding:20px;}
.active{display:flex;}

/* Typing */
.typing{font-size:26px;border-right:2px solid white;}

/* Heart */
.heart{width:130px;cursor:pointer;animation:pulse 1.2s infinite;}
@keyframes pulse{50%{transform:scale(1.15);}}

/* Timeline */
.timeline{max-width:300px;text-align:left;}
.timeline div{margin:10px 0;padding:10px;background:#111;border-radius:10px;}

/* Chat */
.chat{background:#111;padding:10px;border-radius:12px;width:90%;max-width:300px;}
.msg{padding:8px;margin:5px;border-radius:8px;}
.me{background:#1e88e5;text-align:right;}

/* Buttons */
button{padding:12px 25px;border:none;border-radius:12px;margin:10px;font-size:18px;}
.yes{background:#00c853;color:white;}
.no{background:red;color:white;position:absolute;}

/* Final */
.big{font-size:42px;animation:glow 1s infinite alternate;}
@keyframes glow{from{text-shadow:0 0 10px pink;}to{text-shadow:0 0 40px red;}}

canvas{position:fixed;top:0;left:0;pointer-events:none;}
</style>
</head>

<body>

<canvas id="fx"></canvas>

<!-- PAGE 1 -->
<div class="page active" id="p1">
    <div id="typing" class="typing"></div>

    <svg onclick="openHeart()" class="heart" viewBox="0 0 100 100">
        <path d="M50 90 L10 50 A20 20 0 0 1 50 20 A20 20 0 0 1 90 50 Z" fill="red"/>
    </svg>

    <p>(tap the heart)</p>
</div>

<!-- PAGE 2 STORY -->
<div class="page" id="p2">
    <h2 id="storyTitle"></h2>
    <div class="timeline">
        <div>✨ First time we talked</div>
<div>💬 Late night chats</div>
<div>😂 All our stupid jokes</div>
<div>❤️ And now... your birthday</div>
    </div>
    <button onclick="next(3)">Next ➡️</button>
</div>

<!-- PAGE 3 CHAT -->
<div class="page" id="p3">
    <div class="chat" id="chat"></div>
    <button onclick="next(4)">Next ➡️</button>
</div>

<!-- PAGE 4 ASK -->
<div class="page" id="p4">
    <h2 id="ask"></h2>
    <button class="yes" onclick="yes()">Yes 😍</button>
    <button class="no" id="no">No 😢</button>
</div>

<!-- PAGE 5 FINAL -->
<div class="page" id="p5">
    <div class="big">I LOVE YOU ❤️</div>
    <p id="finalMsg"></p>
</div>

<audio id="music" loop>
<source src="music.mp3">
</audio>

<script>

/* CHANGE NAME */
const HER_NAME="Sanvi";

/* Typing */
let t="Hey "+HER_NAME+"... I made this just for you ❤️";
let i=0;
function type(){
    if(i<t.length){
        typing.innerHTML+=t[i++];
        setTimeout(type,40);
    }
}
type();

/* Open */
function openHeart(){
    music.play();
    next(2);
}

/* Navigation */
function next(n){
    document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
    document.getElementById("p"+n).classList.add("active");

    if(n==3) startChat();
    if(n==5) fireworks();
}

/* Story */
storyTitle.innerText="Our Story 💫";

const msgs=[
"Hey Sanvi ❤️",
"Kal se hi soch raha tha...",
"Tera birthday special kaise banaun 🎉",
"Tu sach me bohot important hai mere liye 🥺",
"I love you ❤️"
];

function startChat(){
    let c=document.getElementById("chat");
    let i=0;
    function add(){
        if(i<msgs.length){
            let d=document.createElement("div");
            d.className="msg me";
            d.innerText=msgs[i++];
            c.appendChild(d);
            setTimeout(add,1000);
        }
    }
    add();
}

/* DATE QUESTION WITH MOMOS */
ask.innerHTML="exam ke baad bhook lg jayegi motiiiiii "+" 💖<br><br>momos khane chale 🥟";

/* No button escapes */
no.onmouseover=()=>{
    no.style.top=Math.random()*80+"%";
    no.style.left=Math.random()*80+"%";
};

/* Yes */
function yes(){
    next(5);
}

/* Final */
finalMsg.innerText="Best birthday ever, right "+HER_NAME+"? 😘";

/* Fireworks */
function fireworks(){
    let c=fx,ctx=c.getContext("2d");
    c.width=innerWidth;c.height=innerHeight;

    setInterval(()=>{
        let x=Math.random()*c.width;
        let y=Math.random()*c.height/2;
        for(let i=0;i<30;i++){
            ctx.fillRect(x+Math.random()*50,y+Math.random()*50,3,3);
        }
    },200);
}

</script>

</body>
</html>
