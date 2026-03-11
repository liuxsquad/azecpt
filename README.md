<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Avropa Futbol Oyunları</title>

<style>

body{
margin:0;
font-family:Arial;
background:#0f172a;
color:white;
padding:20px;
}

h1{
text-align:center;
}

.match{
background:#111827;
padding:15px;
border-radius:10px;
margin-bottom:15px;
display:flex;
align-items:center;
justify-content:space-between;
}

.team{
display:flex;
align-items:center;
gap:10px;
}

.team img{
width:40px;
height:40px;
}

.time{
font-size:18px;
font-weight:bold;
}

</style>
</head>

<body>

<h1>Avropa Oyunları</h1>

<div id="matches"></div>

<script>

let matches=[

{
team1:"Real Madrid",
logo1:"https://crests.football-data.org/86.png",
team2:"Bayern Munich",
logo2:"https://crests.football-data.org/5.png",
time:"2026-03-12 21:00"
},

{
team1:"Manchester City",
logo1:"https://crests.football-data.org/65.png",
team2:"PSG",
logo2:"https://crests.football-data.org/524.png",
time:"2026-03-12 23:00"
},

{
team1:"Barcelona",
logo1:"https://crests.football-data.org/81.png",
team2:"Juventus",
logo2:"https://crests.football-data.org/109.png",
time:"2026-03-13 22:00"
}

]

function loadMatches(){

let container=document.getElementById("matches")
container.innerHTML=""

let now=new Date()

matches.forEach(m=>{

let gameTime=new Date(m.time)

if(gameTime>now){

let div=document.createElement("div")
div.className="match"

div.innerHTML=`

<div class="team">
<img src="${m.logo1}">
${m.team1}
</div>

<div class="time">
VS<br>
${gameTime.toLocaleString()}
</div>

<div class="team">
${m.team2}
<img src="${m.logo2}">
</div>

`

container.appendChild(div)

}

})

}

loadMatches()

setInterval(loadMatches,60000)

</script>

</body>
</html>
