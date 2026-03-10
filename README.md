
<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Azecpt v1</title>

<style>

body{
margin:0;
font-family:Arial;
background:#0f172a;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
}

.container{
width:95%;
max-width:500px;
background:#111827;
border-radius:12px;
padding:15px;
color:white;
}

h1{
text-align:center;
margin-bottom:10px;
}

#chat{
height:400px;
overflow-y:auto;
background:#020617;
padding:10px;
border-radius:8px;
margin-bottom:10px;
}

.msg{
margin:6px 0;
padding:8px;
border-radius:6px;
}

.user{
background:#2563eb;
text-align:right;
}

.bot{
background:#374151;
}

.input{
display:flex;
}

input{
flex:1;
padding:10px;
border:none;
border-radius:6px;
}

button{
padding:10px;
margin-left:5px;
border:none;
background:#22c55e;
color:white;
border-radius:6px;
}

</style>
</head>

<body>

<div class="container">

<h1>Azecpt v1</h1>

<div id="chat"></div>

<div class="input">
<input id="text" placeholder="Mesaj yaz..." />
<button onclick="send()">Gönder</button>
</div>

</div>

<script>

let chat=document.getElementById("chat")

function send(){

let input=document.getElementById("text")
let msg=input.value

if(msg.trim()=="")return

add(msg,"user")

let reply=ai(msg)

setTimeout(()=>{
add(reply,"bot")
},500)

input.value=""

}

function add(text,type){

let div=document.createElement("div")
div.className="msg "+type
div.innerText=text

chat.appendChild(div)
chat.scrollTop=chat.scrollHeight

}

function ai(msg){

msg=msg.toLowerCase()

if(msg.includes("salam"))
return "Salam. Mən Azecpt v1 süni zəka modeliyəm."

if(msg.includes("adın"))
return "Mənim adım Azecpt v1-dir."

if(msg.includes("kim yaratdı"))
return "Məni İbrahim Həmzəyev yaratdı."

if(msg.includes("necəsən"))
return "Mən yaxşıyam."

if(msg.includes("saat"))
return new Date().toLocaleTimeString()

if(msg.includes("tarix"))
return new Date().toLocaleDateString()

return "Bu sualı hələ başa düşmürəm."

}

</script>

</body>
</html>
