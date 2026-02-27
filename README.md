<!DOCTYPE html>
<html>
<head>
<title>SkillConnect</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body {
    font-family: Arial;
    margin: 0;
    background: #f4f6f9;
}

header {
    background: #4CAF50;
    color: white;
    padding: 15px;
    text-align: center;
}

.container {
    padding: 20px;
}

input, select, button {
    width: 100%;
    padding: 10px;
    margin: 8px 0;
    border-radius: 5px;
    border: 1px solid #ccc;
}

button {
    background: #4CAF50;
    color: white;
    border: none;
    cursor: pointer;
}

button:hover {
    background: #45a049;
}

.card {
    background: white;
    padding: 15px;
    margin: 10px 0;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.chat-box {
    height: 150px;
    overflow-y: auto;
    background: #eee;
    padding: 10px;
    border-radius: 5px;
}

.message {
    background: white;
    padding: 5px;
    margin: 5px 0;
    border-radius: 5px;
}
</style>
</head>

<body>

<header>
<h2>SkillConnect</h2>
</header>

<div class="container">

<h3>Register</h3>
<input type="text" id="name" placeholder="Your Name">
<input type="text" id="skill" placeholder="Skill (Guitar, Cricket, Design)">
<select id="role">
<option value="Teacher">Teacher</option>
<option value="Learner">Learner</option>
</select>
<button onclick="register()">Register</button>

<h3>Available Teachers</h3>
<div id="teachers"></div>

<h3>Chat</h3>
<div class="chat-box" id="chatBox"></div>
<input type="text" id="chatInput" placeholder="Type message">
<button onclick="sendMessage()">Send</button>

</div>

<script>
let users = [];
let messages = [];

function register() {
    let name = document.getElementById("name").value;
    let skill = document.getElementById("skill").value;
    let role = document.getElementById("role").value;

    if(name === "" || skill === "") {
        alert("Please fill all fields");
        return;
    }

    users.push({name, skill, role});
    displayTeachers();
    alert("Registered Successfully!");
}

function displayTeachers() {
    let teacherDiv = document.getElementById("teachers");
    teacherDiv.innerHTML = "";

    users.forEach(user => {
        if(user.role === "Teacher") {
            teacherDiv.innerHTML += `
                <div class="card">
                    <strong>${user.name}</strong><br>
                    Skill: ${user.skill}<br>
                    <button onclick="startChat('${user.name}')">Chat</button>
                </div>
            `;
        }
    });
}

function startChat(name) {
    alert("Chatting with " + name);
}

function sendMessage() {
    let input = document.getElementById("chatInput");
    let chatBox = document.getElementById("chatBox");

    if(input.value === "") return;

    messages.push(input.value);

    chatBox.innerHTML += `
        <div class="message">${input.value}</div>
    `;

    input.value = "";
    chatBox.scrollTop = chatBox.scrollHeight;
}
</script>

</body>
</html>
