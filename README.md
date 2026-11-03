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

//2
src/firebase.js
---------------
import { initializeApp } from "firebase/app";
import { getDatabase } from "firebase/database";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};

const app = initializeApp(firebaseConfig);

export const db = getDatabase(app);


src/App.jsx
--------
import React, { useEffect, useState } from "react";
import { db } from "./firebase";
import {
    ref, push, onValue, remove, update
} from "firebase/database";

function App() {
    const [name, setName] = useState("");
    const [marks, setMarks] = useState("");
    const [students, setStudents] = useState([]);

    useEffect(() => {
        const studentRef = ref(db, "students");

        const unsubscribe = onValue(studentRef, (snapshot) => {
            const data = snapshot.val() || {};

            const list = Object.entries(data).map(
                ([id, value]) => ({ id, ...value })
            );

            setStudents(list);
        });

        return () => unsubscribe();
    }, []);

    function addStudent(e) {
        e.preventDefault();

        push(ref(db, "students"), {
            name: name,
            marks: Number(marks)
        });

        setName("");
        setMarks("");
    }

    function deleteStudent(id) {
        remove(ref(db, "students/" + id));
    }

    function updateStudent(student) {
        const newName = prompt("Enter new name", student.name);

        if (newName) {
            update(ref(db, "students/" + student.id), {
                name: newName
            });
        }
    }

    return (
        <div>
            <h2>Student Management System</h2>

            <form onSubmit={addStudent}>
                <input
                    placeholder="Enter Name"
                    value={name}
                    onChange={e => setName(e.target.value)}
                    required
                />

                <input
                    type="number"
                    placeholder="Enter Marks"
                    value={marks}
                    onChange={e => setMarks(e.target.value)}
                    required
                />

                <button type="submit">Add Student</button>
            </form>

            <h3>Student Details</h3>

            {students.map(s => (
                <p key={s.id}>
                    {s.name} - {s.marks}

                    <button onClick={() => updateStudent(s)}>
                        Update
                    </button>

                    <button onClick={() => deleteStudent(s.id)}>
                        Delete
                    </button>
                </p>
            ))}
        </div>
    );
}

export default App;



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




