<!DOCTYPE html>
<html lang="si">
<head>
<meta charset="UTF-8">
<title>🌟 Vihan Sesath</title>
<link rel="icon" href="favicon.png">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
body{
  font-family:"Segoe UI",sans-serif;
  margin:0;
  background:linear-gradient(135deg,#667eea,#764ba2);
}
/* NAVBAR */
.navbar{
  background:white;
  padding:15px 30px;
  display:flex;
  justify-content:space-between;
  align-items:center;
  box-shadow:0 5px 15px rgba(0,0,0,0.2);
}
.navbar h2{
  color:#667eea;
  display:flex;
  align-items:center;
  font-size:22px;
}
.navbar h2 img{
  width:35px;
  height:35px;
  margin-right:10px;
  border-radius:50%;
}
.nav-icons i{
  font-size:22px;
  margin-left:20px;
  cursor:pointer;
  color:#764ba2;
}
.nav-icons i:hover{color:#ff4b5c;}

/* HOME */
.container{
  width:90%;
  max-width:1000px;
  margin:50px auto;
  background:white;
  padding:30px;
  border-radius:15px;
  box-shadow:0 15px 30px rgba(0,0,0,0.25);
}
h1{text-align:center;color:#667eea;}
#displayText{white-space:pre-line;line-height:1.8;font-size:16px;}
#mediaPreview{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
  gap:15px;
  margin-top:20px;
}
#mediaPreview img,#mediaPreview video{width:100%;border-radius:10px;}
#mediaPreview video{max-height:300px;}

/* EDIT AREA */
#editArea{margin-top:20px;display:none;}
textarea{width:100%;height:250px;padding:12px;border-radius:10px;border:1px solid #ccc;font-size:15px;margin-top:10px;}
#dropZone{margin-top:10px;padding:20px;border:2px dashed #667eea;text-align:center;border-radius:10px;color:#667eea;font-weight:bold;cursor:pointer;}
input[type="file"]{display:none;}
button{padding:12px 25px;border:none;border-radius:25px;cursor:pointer;margin-top:15px;font-size:15px;}
.save-btn{background:linear-gradient(135deg,#667eea,#764ba2);color:white;}
.logout-btn{background:#ff4b5c;color:white;margin-left:10px;}

/* LOGIN MODAL FULLSCREEN */
.modal{
  display:none;
  position:fixed;
  top:0; left:0;
  width:100%;
  height:100%;
  background:rgba(0,0,0,0.8);
  justify-content:center;
  align-items:center;
  z-index:9999;
}
.modal-content{
  background:white;
  padding:30px;
  border-radius:12px;
  width:90%;
  max-width:400px;
  text-align:center;
  box-shadow:0 15px 30px rgba(0,0,0,0.3);
}

/* ERROR */
#error{color:red;font-size:14px;}

@media(max-width:600px){
  textarea{height:180px;}
  #mediaPreview video{max-height:200px;}
}
</style>
</head>
<body>

<!-- NAVBAR -->
<div class="navbar">
  <!-- HOME ICON + TITLE -->
  <h2><img src="favicon.png" alt="Home Icon"> Vihan Sesath</h2>
  <!-- LOGIN ICON -->
  <div class="nav-icons">
    <i class="fa-solid fa-right-to-bracket" onclick="openModal()" title="Login"></i>
  </div>
</div>

<!-- HOME -->
<div class="container">
  <h1>මා පිළිබඳ විස්තරය</h1>
  <div id="displayText"></div>
  <div id="mediaPreview"></div>

  <!-- EDIT AREA -->
  <div id="editArea">
    <textarea id="content"></textarea>
    <div id="dropZone">Drag & Drop Photos/Videos here or Click to Select</div>
    <input type="file" id="mediaInput" multiple accept="image/*,video/*">
    <br>
    <button class="save-btn" onclick="saveContent()">💾 Save</button>
    <button class="logout-btn" onclick="logout()">🚪 Logout</button>
  </div>
</div>

<!-- LOGIN MODAL -->
<div id="loginModal" class="modal">
  <div class="modal-content">
    <h3>🔐 Login</h3>
    <input id="username" placeholder="Username"><br><br>
    <input id="password" type="password" placeholder="Password"><br><br>
    <button class="save-btn" onclick="login()">Login</button>
    <p id="error"></p>
  </div>
</div>

<script>
// USERS
const users=[{u:"vihara",p:"1234"}];

// ELEMENTS
const username=document.getElementById("username");
const password=document.getElementById("password");
const error=document.getElementById("error");
const editArea=document.getElementById("editArea");
const content=document.getElementById("content");
const mediaInput=document.getElementById("mediaInput");
const mediaPreview=document.getElementById("mediaPreview");
const displayText=document.getElementById("displayText");
const loginModal=document.getElementById("loginModal");
const dropZone=document.getElementById("dropZone");

// DEFAULT TEXT
const defaultText=`මෙම අවස්ථාවේදී මා පිළිබඳ අදහස් කිහිපයක්...
(ඔයාගේ සම්පූර්ණ විස්තර paste කරන්න)`;

// LOAD HOME
function loadContent(){
  displayText.innerText=localStorage.getItem("aboutText")||defaultText;
  displayMedia();
}
function displayMedia(){
  const mediaData=JSON.parse(localStorage.getItem("mediaFiles")||"[]");
  mediaPreview.innerHTML="";
  mediaData.forEach(m=>{
      if(m.type.startsWith("image/")){
          const img=document.createElement("img"); img.src=m.data; mediaPreview.appendChild(img);
      }else if(m.type.startsWith("video/")){
          const vid=document.createElement("video"); vid.src=m.data; vid.controls=true; mediaPreview.appendChild(vid);
      }
  });
}
loadContent();

// LOGIN MODAL
function openModal(){loginModal.style.display="flex";}
window.onclick=function(e){if(e.target==loginModal){loginModal.style.display="none";}}

// LOGIN FUNCTION
function login(){
  const ok=users.find(x=>x.u===username.value && x.p===password.value);
  if(ok){
    loginModal.style.display="none";
    editArea.style.display="block";
    content.value=localStorage.getItem("aboutText")||defaultText;
    displayMedia();
    error.innerText="";
  }else{error.innerText="❌ Username හෝ Password වැරදි";}
}

// SAVE FUNCTION
function saveContent(){
  localStorage.setItem("aboutText",content.value);
  const files=mediaInput.files;
  const mediaData=JSON.parse(localStorage.getItem("mediaFiles")||"[]");
  const promises=[];
  for(let i=0;i<files.length;i++){
      const file=files[i];
      const reader=new FileReader();
      promises.push(new Promise(res=>{
          reader.onload=function(e){mediaData.push({type:file.type,data:e.target.result}); res();}
          reader.readAsDataURL(file);
      }));
  }
  Promise.all(promises).then(()=>{
      localStorage.setItem("mediaFiles",JSON.stringify(mediaData));
      displayMedia();
      alert("✅ Saved Successfully!");
  });
}

// LOGOUT
function logout(){editArea.style.display="none"; username.value=""; password.value=""; error.innerText="";}

// DRAG & DROP
dropZone.addEventListener("click",()=>mediaInput.click());
dropZone.addEventListener("dragover",e=>{e.preventDefault(); dropZone.style.borderColor="#ff4b5c";});
dropZone.addEventListener("dragleave",e=>{e.preventDefault(); dropZone.style.borderColor="#667eea";});
dropZone.addEventListener("drop",e=>{e.preventDefault(); dropZone.style.borderColor="#667eea"; mediaInput.files=e.dataTransfer.files;});
</script>

</body>
</html>
