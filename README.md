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
overflow-x:hidden;
}

h1{
color:#ff66cc;
margin-top:20px;
}

#ascii{
white-space:pre;
font-size:6px;
line-height:6px;
padding:10px;
text-shadow:0 0 8px #ff99cc;
overflow:auto;
}

canvas{display:none;}

button{
padding:8px 15px;
border:none;
border-radius:10px;
background:#ff3399;
color:white;
cursor:pointer;
margin:10px;
}

button:hover{background:#ff0066;}

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

.footer{
margin:20px;
color:#ff99cc;
}
</style>
</head>
<body>

<h1>💞 Happy 2 Months Anniversary 💞</h1>

<button onclick="downloadTXT()">💾 Tải TXT</button>

<canvas id="canvas"></canvas>
<pre id="ascii"></pre>

<div class="footer">
Made with ❤️ for 2 Months
</div>

<audio autoplay loop>
<source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3">
</audio>

<script>
const canvas=document.getElementById("canvas");
const ctx=canvas.getContext("2d");
const asciiDiv=document.getElementById("ascii");

const asciiChars="@#W$9876543210?!abc;:+=-,._ ";
let currentASCII="";

window.onload=function(){
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
currentASCII=ascii.replace(/<[^>]*>/g,"");
asciiDiv.innerHTML=ascii;
}

function downloadTXT(){
const blob=new Blob([currentASCII],{type:"text/plain"});
const link=document.createElement("a");
link.href=URL.createObjectURL(blob);
link.download="2months_ascii.txt";
link.click();
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
