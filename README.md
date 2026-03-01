<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>💞 2 Tháng Yêu Nhau 💞</title>

<style>
body{
margin:0;
font-family:monospace;
background:linear-gradient(135deg,#1a001f,#32003d);
color:white;
text-align:center;
overflow:hidden;
}

#loginBox{
position:absolute;
top:50%;
left:50%;
transform:translate(-50%,-50%);
background:rgba(0,0,0,0.7);
padding:30px;
border-radius:15px;
}

input{
padding:10px;
border:none;
border-radius:8px;
margin:10px;
}

button{
padding:10px 15px;
border:none;
border-radius:8px;
background:#ff3399;
color:white;
cursor:pointer;
}

#mainContent{
display:none;
overflow:auto;
height:100vh;
}

h1{color:#ff66cc;}

#ascii{
white-space:pre;
font-size:6px;
line-height:6px;
padding:10px;
overflow:auto;
}

canvas{display:none;}

.counter{
font-size:18px;
margin:10px;
color:#ff99cc;
}

.heart{
position:fixed;
bottom:-20px;
animation:float 6s linear infinite;
color:#ff4da6;
}

@keyframes float{
0%{transform:translateY(0);}
100%{transform:translateY(-110vh);}
}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="loginBox">
<h2>🔐 Nhập mật khẩu để mở 💖</h2>
<input type="password" id="password" placeholder="Nhập mật khẩu">
<br>
<button onclick="checkPassword()">Mở</button>
</div>

<!-- MAIN CONTENT -->
<div id="mainContent">
<h1>💞 Happy 2 Months Anniversary 💞</h1>
<div class="counter" id="counter"></div>
<canvas id="canvas"></canvas>
<pre id="ascii"></pre>
</div>

<audio autoplay loop>
<source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3">
</audio>

<script>
const correctPassword="60"; // 🔐 ĐỔI MẬT KHẨU TẠI ĐÂY
const loveStartDate=new Date("01012026"); // ❤️ ĐỔI NGÀY BẮT ĐẦU YÊU

function checkPassword(){
const input=document.getElementById("password").value;
if(input===correctPassword){
document.getElementById("loginBox").style.display="none";
document.getElementById("mainContent").style.display="block";
startLoveCounter();
loadImage();
}
else{
alert("Sai mật khẩu rồi 😢");
}
}

function startLoveCounter(){
setInterval(()=>{
const now=new Date();
const diff=now-loveStartDate;
const days=Math.floor(diff/(1000*60*60*24));
const hours=Math.floor((diff/(1000*60*60))%24);
const minutes=Math.floor((diff/(1000*60))%60);
const seconds=Math.floor((diff/1000)%60);

document.getElementById("counter").innerHTML=
`⏳ Đã yêu nhau: ${days} ngày ${hours} giờ ${minutes} phút ${seconds} giây 💖`;
},1000);
}

const canvas=document.getElementById("canvas");
const ctx=canvas.getContext("2d");
const asciiDiv=document.getElementById("ascii");
const asciiChars="@#W$9876543210?!abc;:+=-,._ ";

function loadImage(){
const img=new Image();
img.src="couple.jpg";
img.onload=function(){
generateASCII(img);
}
}

function generateASCII(img){
const width=120;
const height=img.height*(width/img.width);
canvas.width=width;
canvas.height=height;
ctx.drawImage(img,0,0,width,height);
const data=ctx.getImageData(0,0,width,height).data;
let ascii="";
for(let y=0;y<height;y++){
for(let x=0;x<width;x++){
const i=(y*width+x)*4;
const r=data[i],g=data[i+1],b=data[i+2];
const bright=(0.299*r+0.587*g+0.114*b);
const index=Math.floor((bright/255)*(asciiChars.length-1));
const char=asciiChars[asciiChars.length-index-1];
ascii+=`<span style="color:rgb(${r},${g},${b})">${char}</span>`;
}
ascii+="\n";
}
asciiDiv.innerHTML=ascii;
}

setInterval(()=>{
const heart=document.createElement("div");
heart.className="heart";
heart.style.left=Math.random()*100+"vw";
heart.style.fontSize=(Math.random()*20+15)+"px";
heart.innerHTML="💖";
document.body.appendChild(heart);
setTimeout(()=>heart.remove(),6000);
},400);

</script>

</body>
</html>
