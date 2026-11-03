======================
prog1 

===============

Step 1: Create a repository on GitHub.

Create a repository named AWP-Program1.

Step 2: Clone the repository.

git clone https://github.com/username/AWP-Program1.git
cd AWP-Program1
Step 3: Create index.html.
<!DOCTYPE html>
<html>
<head>
    <title>Git Practical</title>
</head>
<body>
    <h1>Hello GitHub!</h1>
    <p>My first Git practical.</p>
</body>
</html>

git status
git add .
git commit -m "First commit"
git push origin main


PROGRAM 2 – Firebase Realtime Database
=======================================

npm create vite@latest Program2 -- --template react
cd Program2
npm install
npm install firebase


src/firebase.js
-------------
//program 2
<html>
<head>
    <title>Student Management</title>
</head>
<body>
    Name: <input id="name"><br><br>
    Roll No: <input id="roll"><br><br>
    Branch: <input id="br"><br><br>
    Year: <input id="yr"><br><br>
    CGPA: <input id="cg"><br><br>

    <button id="b1">INSERT</button>
    <button id="b2">DELETE</button>
    <button id="b3">UPDATE</button>
    <button id="b4">DISPLAY</button>

    <h3 id="d"></h3>
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
<script type="module">
  // Import the functions you need from the SDKs you need
  import { initializeApp } from "https://www.gstatic.com/firebasejs/13.0.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, remove } from "https://www.gstatic.com/firebasejs/13.0.0/firebase-database.js";
  // TODO: Add SDKs for Firebase products that you want to use
  // https://firebase.google.com/docs/web/setup#available-libraries

  // Your web app's Firebase configuration
  const firebaseConfig = {
    apiKey: "AIzaSyC9GzqlB_vxkOekCCpAppdRMrsQd_9yVBI",
    authDomain: "practice-7fa4a.firebaseapp.com",
    databaseURL: "https://practice-7fa4a-default-rtdb.firebaseio.com",
    projectId: "practice-7fa4a",
    storageBucket: "practice-7fa4a.firebasestorage.app",
    messagingSenderId: "648749756693",
    appId: "1:648749756693:web:34aac063cb3467332bb91c"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);

 ///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
  
const db = getDatabase(app);
function data() {
    return {
        name: document.getElementById("name").value,
        branch: document.getElementById("br").value,
        year: document.getElementById("yr").value,
        cgpa: document.getElementById("cg").value
    };
}
function path() {
    return ref(db, "Student/" + document.getElementById("roll").value);
}
b1.onclick = () => set(path(), data()).then(() => alert("Inserted"));
b2.onclick = () => remove(path()).then(() => alert("Deleted"));
b3.onclick = () => update(path(), data()).then(() => alert("Updated"));
b4.onclick = () => get(path()).then(s => {
    if (s.exists()) {
        let x = s.val();
        d.innerHTML = "Name: " + x.name +
            "<br>Branch: " + x.branch +
            "<br>Year: " + x.year +
            "<br>CGPA: " + x.cgpa;
    } else {
        d.innerHTML = "No data found";
    }
});
</script>
</body>
</html>//4&5
const express = require('express');
const app = express();
app.use(express.json());
let students = [{ id: 1, name: "Rahul" }];
// CREATE
app.post('/students', (req, res) => {
    students.push(req.body);
    res.send("Student Added");
});
// READ
app.get('/students', (req, res) => {
    res.json(students);
});
// UPDATE
app.put('/students/:id', (req, res) => {
    let s = students.find(x => x.id == req.params.id);
    if (s) Object.assign(s, req.body);
    res.send("Student Updated");
});
// DELETE
app.delete('/students/:id', (req, res) => {
    students = students.filter(x => x.id != req.params.id);
    res.send("Student Deleted");
});
app.listen(3000, () => console.log("Server running on port 3000"));


3
===========
//3
const os = require('os');
const http = require('http');
const path = require('path');

console.log("Operating System:", os.platform());
console.log("CPU Architecture:", os.arch());
console.log("Free Memory:", os.freemem());
console.log("File Name:", path.basename(__filename));

const server = http.createServer((req, res) => {
    res.write("Hello from Node.js HTTP module!");
    res.end();
});

server.listen(3000, () => {
    console.log("Server running on port 3000");
});










6
==============

//6
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();
const secret = 'abc123';
// Generate token
app.get('/login', (req, res) => {
    const token = jwt.sign({ name: 'Rahul' }, secret);
    res.send(token);
});
// Authorized endpoint
app.get('/home', (req, res) => {
    const token = req.headers.authorization;
    jwt.verify(token, secret, (err) => {
        if (err) 
            return res.send('Access Denied');
        res.send('Access Granted');
    });
});

app.listen(3000, () => console.log('Server started'));













7
======

App.js

import React from 'react';

function Welcome() {

    return (
        <div>
            <h2>Welcome to React!</h2>
            <p>This is a Functional Component.</p>
        </div>
    );

}

function App() {

    return (
        <div>
            <h1>React Components</h1>

            <Welcome />

        </div>
    );

}

export default App;



8
=====
App.js


import React from 'react';

function App() {

    const date = new Date();

    return (
        <div>
            <h2>JSX Rendering</h2>

            <h3>Current Date:</h3>

            <p>{date.toLocaleDateString()}</p>

            <h3>Current Time:</h3>

            <p>{date.toLocaleTimeString()}</p>

        </div>
    );

}

export default App;



9
=========
//9
//Functional Component using Props
/*function Student(props) {
  return <h2>Name: {props.name}</h2>;
}
function App() {
  return (
    <div>
      <Student name="Rahul" />
    </div>
  );
}
export default App;*/

//component using props
import React, { Component } from 'react';

class Student extends Component {
  render() {
    return <h2>Name: {this.props.name}</h2>;
  }
}

function App() {
  return <Student name="sita" />;
}

export default App;


//10
/*import React, { Component } from 'react';

class App extends Component {
  state= { date: new Date().toLocaleString() };

  render() {
    return <h2>Date: {this.state.date}</h2>;
  }
}
export default App;*/

//11
/*import React, { Component } from 'react';
class App extends Component {
  componentDidMount() {
    alert("Component Mounted");
  }
  render() {
    return (
      <div>
        <h2>Component Lifecycle</h2>
        <p>Hello React!</p>
      </div>
    );
  }
}
export default App;*/

//12
/*import React, { useState } from 'react';

function App() {
  const [msg, setMsg] = useState("");

  function showDate() {
    setMsg(new Date().toLocaleString());
  }
  return (
    <div>
      <button onClick={showDate}>Show Date & Time</button>
      <button onClick={() => setMsg("Good Bye")}>Good Bye</button>
      <h3>{msg}</h3>
    </div>
  );
}
export default App;
*/
//14
import React, { useState } from 'react';

function App() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");

  return (
    <form onSubmit={e => { e.preventDefault(); alert("Registration Successful!"); }}>
      <h2>Registration Form</h2>
      Name: <input value={name} onChange={e => setName(e.target.value)} />
      <br /><br />
      Email: <input type="email" value={email} onChange={e => setEmail(e.target.value)} />
      <br /><br />
      <button type="submit">Register</button>
    </form>
  );
}
export default App;


4&5
========
//4&5
const express = require('express');
const app = express();
app.use(express.json());
let students = [{ id: 1, name: "Rahul" }];
// CREATE
app.post('/students', (req, res) => {
    students.push(req.body);
    res.send("Student Added");
});
// READ
app.get('/students', (req, res) => {
    res.json(students);
});
// UPDATE
app.put('/students/:id', (req, res) => {
    let s = students.find(x => x.id == req.params.id);
    if (s) Object.assign(s, req.body);
    res.send("Student Updated");
});
// DELETE
app.delete('/students/:id', (req, res) => {
    students = students.filter(x => x.id != req.params.id);
    res.send("Student Deleted");
});
app.listen(3000, () => console.log("Server running on port 3000"));




