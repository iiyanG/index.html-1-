<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>CyberEuropa: Defensores Digitales</title>

<style>
body{
    font-family: Arial, sans-serif;
    background: linear-gradient(120deg,#003399,#0066cc);
    color:white;
    text-align:center;
    padding:30px;
}

.container{
    max-width:700px;
    margin:auto;
    background:white;
    color:black;
    padding:20px;
    border-radius:15px;
    box-shadow:0 0 20px rgba(0,0,0,0.3);
}

button{
    background:#0066cc;
    color:white;
    border:none;
    padding:12px 20px;
    margin:10px;
    border-radius:8px;
    cursor:pointer;
    font-size:16px;
}

button:hover{
    background:#004999;
}

.hide{display:none;}
.correct{color:green;font-weight:bold;}
.wrong{color:red;font-weight:bold;}
</style>
</head>

<body>

<div class="container">

<h1>🌍 CyberEuropa</h1>
<h2>Defensores Digitales</h2>

<div id="start">
<p>Europa necesita tu ayuda para proteger a los ciudadanos de los peligros de Internet.</p>
<button onclick="startGame()">Comenzar misión</button>
</div>

<div id="quiz" class="hide">
<h3 id="question"></h3>
<div id="answers"></div>
<p id="feedback"></p>
</div>

<div id="end" class="hide">
<h2>Misión completada</h2>
<h3 id="scoreText"></h3>
<button onclick="location.reload()">Jugar otra vez</button>
</div>

</div>

<script>
let questions = [
{question:"¿Cuál es la contraseña más segura?",answers:["123456","MiNombre2005","T7$k!9Lp#"],correct:2},
{question:"Recibes un email del banco pidiendo tu clave. ¿Qué haces?",answers:["Se la envío","Lo ignoro y aviso al banco","Hago clic en el enlace"],correct:1},
{question:"¿La Inteligencia Artificial puede decidir todo sola?",answers:["Sí","No, necesita supervisión humana","Solo en videojuegos"],correct:1},
{question:"Según el RGPD, tus datos personales...",answers:["Son de las empresas","Son tuyos","Son públicos"],correct:1},
{question:"¿Cómo detectar fake news?",answers:["Mirar varias fuentes","Compartir rápido","Creer titulares"],correct:0}
];

let currentQuestion = 0;
let score = 0;

function startGame(){
document.getElementById("start").classList.add("hide");
document.getElementById("quiz").classList.remove("hide");
showQuestion();
}

function showQuestion(){
let q = questions[currentQuestion];
document.getElementById("question").textContent = q.question;
let answersDiv = document.getElementById("answers");
answersDiv.innerHTML="";
q.answers.forEach((answer,index)=>{
let btn = document.createElement("button");
btn.textContent = answer;
btn.onclick = ()=>checkAnswer(index);
answersDiv.appendChild(btn);
});
}

function checkAnswer(index){
let feedback = document.getElementById("feedback");
if(index === questions[currentQuestion].correct){
score +=10;
feedback.textContent="✔️ Correcto!";
feedback.className="correct";
}else{
feedback.textContent="❌ Incorrecto";
feedback.className="wrong";
}
currentQuestion++;
setTimeout(()=>{
feedback.textContent="";
if(currentQuestion < questions.length){showQuestion();}
else{endGame();}
},1000);
}

function endGame(){
document.getElementById("quiz").classList.add("hide");
document.getElementById("end").classList.remove("hide");
let message="";
if(score<=20) message="Aprendiz digital 🟡";
else if(score<=40) message="Agente europeo 🔵";
else message="Defensor digital de Europa 🟢";
document.getElementById("scoreText").textContent =
"Tu puntuación: " + score + " - " + message;
}
</script>

</body>
</html>
