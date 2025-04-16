# vocabulary-corrector
 VOCABULARY CORRECTOR
 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Login</title>
<style>
body {
background: linear-gradient(to right, #74ebd5, #acb6e5);
font-family: Arial, sans-serif;
display: flex;
justify-content: center;
align-items: center;
height: 100vh;
margin: 0;
}
.login-box {
background: white;
padding: 40px;
border-radius: 12px;
text-align: center;
box-shadow: 0 8px 20px rgba(0,0,0,0.1);
}
input {
padding: 10px;
width: 80%;
margin-top: 10px;
font-size: 1rem;
border-radius: 6px;
border: 1px solid #ccc;
}
button {
margin-top: 20px;
padding: 10px 20px;
background-color: #4a90e2;
color: white;
font-size: 1rem;
border: none;
border-radius: 6px;
cursor: pointer;
}
</style>
</head>
<body>
<div class="login-box">
<h2>Enter Your Name</h2>
<input type="text" id="username" placeholder="Your name" />
<button onclick="login()">Login</button>
</div>
<script>
function login() {
const name = document.getElementById("username").value;
if (name.trim() !== "") {
localStorage.setItem("userName", name);
window.location.href = "vocab.html";
} else {
alert("Please enter your name");
}
}
</script>
</body>
</html>
Vocabulary corrector code:
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Vocabulary Corrector</title>
<style>
body {
font-family: sans-serif;
background: linear-gradient(to right, #c2e9fb, #a1c4fd);
padding: 40px;
}
.container {
max-width: 700px;
margin: auto;
background: white;
padding: 30px;
border-radius: 10px;
box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}
h1 {
text-align: center;
margin-bottom: 10px;
}
.welcome {
text-align: center;
font-size: 1rem;
color: #555;
margin-bottom: 20px;
}
textarea {
width: 100%;
height: 150px;
padding: 10px;
font-size: 1rem;
}
button {
margin-top: 15px;
padding: 10px 20px;
background-color: #1976d2;
color: white;
border: none;
border-radius: 5px;
cursor: pointer;
display: block;
margin-left: auto;
margin-right: auto;
}
.output {
margin-top: 20px;
background: #e3f2fd;
padding: 15px;
border-radius: 8px;
font-size: 1.1rem;
}
</style>
</head>
<body>
<div class="container">
<h1>Smart Vocabulary Corrector</h1>
<div class="welcome" id="welcomeText"></div>
<textarea id="inputText" placeholder="Type a sentence with misspelled
words..."></textarea>
<button onclick="autoCorrect()">Auto-Correct</button>
<div class="output" id="correctedText">Corrected text will appear
here...</div>
</div>
<script>
const userName = localStorage.getItem("userName") || "User";
document.getElementById("welcomeText").innerText = `Welcome,
${userName}!`;
async function autoCorrect() {
const input = document.getElementById("inputText").value;
const words = input.split(/\s+/);
const correctedWords = [];
for (const word of words) {
const clean = word.replace(/[^a-zA-Z]/g, '');
const punctuation = word.replace(/[a-zA-Z]/g, '');
const response = await fetch(`https://api.datamuse.com/sug?s=${clean}`);
const data = await response.json();
if (data.length > 0 && data[0].score > 80) {
correctedWords.push(data[0].word + punctuation);
} else {
correctedWords.push(word);
}
}
document.getElementById("correctedText").innerText =
correctedWords.join(' ');
}
</script>
</body>
</html>
