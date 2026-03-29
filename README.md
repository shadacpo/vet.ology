<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Vetology Veterinary Clinic</title>

<style>

body{
font-family:Arial;
margin:0;
background:#f4f7f6;
color:#2f2f2f;
}

header{
background:#2E7D6F;
color:white;
padding:20px;
text-align:center;
}

nav{
display:flex;
justify-content:center;
gap:20px;
padding:10px;
background:#4CAF93;
}

button{
padding:8px 14px;
border:none;
border-radius:5px;
cursor:pointer;
}

.container{
padding:20px;
}

.doctor-card{
background:white;
padding:20px;
margin:15px;
border-radius:10px;
box-shadow:0 3px 10px rgba(0,0,0,0.1);
width:250px;
}

.doctors{
display:flex;
flex-wrap:wrap;
justify-content:center;
}

input, textarea{
padding:8px;
margin:5px;
width:90%;
}

.hidden{
display:none;
}

.rating span{
font-size:20px;
cursor:pointer;
color:gray;
}

</style>

</head>

<body>

<header>
<h1 id="title">Vetology Veterinary Clinic</h1>
<p id="welcome">Welcome to Vetology</p>
</header>

<nav>
<button onclick="showSection('home')">Home</button>
<button onclick="showSection('doctors')">Doctors</button>
<button onclick="showSection('login')">Login</button>
<button onclick="showSection('admin')">Admin</button>
<button onclick="toggleLang()">AR / EN</button>
</nav>

<div class="container">

<!-- HOME -->

<div id="home">

<h2>Clinic Locations</h2>

<ul id="locations">
<li>Cairo</li>
<li>Giza</li>
</ul>

<h2>Contact Numbers</h2>

<ul>
<li>+20 100 000 000</li>
<li>+20 111 000 000</li>
</ul>

</div>


<!-- DOCTORS -->

<div id="doctors" class="hidden">

<h2>Doctors</h2>

<div class="doctors" id="doctorList"></div>

</div>


<!-- LOGIN -->

<div id="login" class="hidden">

<h2>Patient Login</h2>

<input id="userEmail" placeholder="Email">

<input id="userPass" type="password" placeholder="Password">

<button onclick="login()">Login</button>

<h3>Register</h3>

<input id="regEmail" placeholder="Email">

<input id="regPass" type="password" placeholder="Password">

<button onclick="register()">Register</button>

</div>


<!-- ADMIN -->

<div id="admin" class="hidden">

<h2>Admin Login</h2>

<input id="adminEmail" placeholder="Email">

<input id="adminPass" type="password" placeholder="Password">

<button onclick="adminLogin()">Login</button>

<div id="adminPanel" class="hidden">

<h3>Add Doctor</h3>

<input id="docName" placeholder="Doctor Name">
<input id="docSpec" placeholder="Specialization">
<input id="docPhone" placeholder="Phone">
<input id="docLocation" placeholder="Location">
<textarea id="docCert" placeholder="Certifications"></textarea>

<button onclick="addDoctor()">Add Doctor</button>

</div>

</div>

</div>


<script>

let doctors=[]

let users=[]

let adminEmail="vetology.se@gmail.com"
let adminPass="vetologyse2089"

function showSection(id){

document.querySelectorAll(".container > div").forEach(s=>{

s.classList.add("hidden")

})

document.getElementById(id).classList.remove("hidden")

}

function addDoctor(){

let doc={

name:docName.value,

spec:docSpec.value,

phone:docPhone.value,

location:docLocation.value,

cert:docCert.value,

reviews:[]

}

doctors.push(doc)

renderDoctors()

}

function renderDoctors(){

let list=document.getElementById("doctorList")

list.innerHTML=""

doctors.forEach((d,i)=>{

let div=document.createElement("div")

div.className="doctor-card"

div.innerHTML=`

<h3>${d.name}</h3>

<p>${d.spec}</p>

<p>${d.phone}</p>

<p>${d.location}</p>

<p>${d.cert}</p>

<div class="rating">

<span onclick="rate(${i},1)">★</span>

<span onclick="rate(${i},2)">★</span>

<span onclick="rate(${i},3)">★</span>

<span onclick="rate(${i},4)">★</span>

<span onclick="rate(${i},5)">★</span>

</div>

<textarea id="review${i}" placeholder="Write review"></textarea>

<button onclick="addReview(${i})">Submit</button>

<div id="reviews${i}"></div>

`

list.appendChild(div)

})

}

function rate(i,val){

alert("You rated "+val+" stars")

}

function addReview(i){

let text=document.getElementById("review"+i).value

doctors[i].reviews.push(text)

renderReviews(i)

}

function renderReviews(i){

let r=document.getElementById("reviews"+i)

r.innerHTML=""

doctors[i].reviews.forEach(t=>{

let p=document.createElement("p")

p.innerText=t

r.appendChild(p)

})

}

function register(){

users.push({

email:regEmail.value,

pass:regPass.value

})

alert("Registered")

}

function login(){

let user=users.find(u=>u.email==userEmail.value && u.pass==userPass.value)

if(user){

alert("Login successful")

}else{

alert("Invalid login")

}

}

function adminLogin(){

if(adminEmail.value===adminEmail && adminPass.value===adminPass){

adminPanel.classList.remove("hidden")

}else{

alert("Wrong admin login")

}

}

let lang="en"

function toggleLang(){

if(lang==="en"){

document.getElementById("title").innerText="فيتولوجي"

document.getElementById("welcome").innerText="مرحباً بكم في فيتولوجي"

lang="ar"

}else{

document.getElementById("title").innerText="Vetology Veterinary Clinic"

document.getElementById("welcome").innerText="Welcome to Vetology"

lang="en"

}

}

</script>

</body>
</html>
