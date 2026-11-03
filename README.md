# csma

---------------------------------------------------------------------------------------
task -14  resgistration
--------------------------------------------------------------------------------------
import React, { useState } from "react";
function App() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
 function register(e) {
    e.preventDefault();
    alert("Registration Successful!");
  }
return (
    <div>
      <h1>Student Registration</h1>
<form onSubmit={register}>
        <input
          type="text"
          placeholder="Enter Name"
          value={name}
          onChange={e => setName(e.target.value)}
          required
        />
<br /><br />
<input
          type="email"
          placeholder="Enter Email"
          value={email}
          onChange={e => setEmail(e.target.value)}
          required
        />
<br /><br />
<input
          type="password"
          placeholder="Enter Password"
          value={password}
          onChange={e => setPassword(e.target.value)}
          required
          minLength={6}
        />

        <br /><br />

        <button type="submit">Register</button>
      </form>


    </div>
  );
}

export default App;

----------------------------------------------------------------------------------------------------------------------------
task-13 calculator 
-----------------------------------------------------------------------------------------------------------------------------
import React, { useState } from 'react';
function App() {
  const [v, setV] = useState('');
  return (<>
      <style>{`
        .calc { width: 250px;
         margin: 50px auto; 
        text-align: center; }
        button { padding: 10px; 
        margin: 3px; }
      `}</style>

      <div className="calc">
        <h2>Calculator</h2>
        <input value={v} readOnly />
        <br />
        <button onClick={() => setV(v + '7')}>7</button>
        <button onClick={() => setV(v + '8')}>8</button>
        <button onClick={() => setV(v + '9')}>9</button>
        <button onClick={() => setV(v + '/')}>/</button>
        <br />

        <button onClick={() => setV(v + '4')}>4</button>
        <button onClick={() => setV(v + '5')}>5</button>
        <button onClick={() => setV(v + '6')}>6</button>
        <button onClick={() => setV(v + '*')}>*</button>
        <br />

        <button onClick={() => setV(v + '1')}>1</button>
        <button onClick={() => setV(v + '2')}>2</button>
        <button onClick={() => setV(v + '3')}>3</button>
        <button onClick={() => setV(v + '-')}>-</button>
        <br />
        <button onClick={() => setV(v + '0')}>0</button>
        <button onClick={() => setV(v + '+')}>+</button>
        <button onClick={() => setV(String(eval(v)))}>=</button>
        <button onClick={() => setV('')}>C</button>
      </div>
    </>
  );
}

export default App;
------------------------------------------------------------------------------------------------------------------------------------
task-12 goodbye
-----------------------------------------------------------------------------------------------------------------------------------

import React, { useState } from "react";

function App() {
  const [message, setMessage] = useState("");

  function showDate() {
    setMessage(new Date().toLocaleString());
  }

  const showBye = () => {
    setMessage("Good Bye");
  };

  return (
    <div>
      <h1>Event Handling</h1>

      <button onClick={showDate}>Show Date and Time</button>

      <button onClick={showBye}>Good Bye</button>

      <h2>{message}</h2>
    </div>
  );
}

export default App;

---------------------------------------------------------------------------------------------------------
task-11
--------------------------------------------------------------------------------------------------------
import React, { Component } from "react";

class App extends Component {
  constructor() {
    super();
    this.state = { count: 0 };
    console.log("Constructor called");
  }

  componentDidMount() {
    console.log("Component Mounted");
  }

  componentDidUpdate() {
    console.log("Component Updated");
  }

  render() {
    return (
      <div>
        <h1>React Lifecycle</h1>
        <h2>Count: {this.state.count}</h2>

        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increase
        </button>
      </div>
    );
  }
}

export default App;
--------------------------------------------------------------------------------------------------------------------
task-10
----------------------------------------------------------------------------------------------------------------------
 import React,{Component} from 'react';
class App extends Component{
  constructor(){
    super();
    this.state={
      date:new Date().toLocaleString()

    };
  }
  render(){
    return(
      <div>
        <p>Date :{this.state.date}</p>
      </div>
    )
  }
}
export default App;

------------------------------------------------------------------------------------------------------------------------------------------------
task -9a
import React from 'react';

function Student(props) {
  return (
    <div>
      <h2>Student Details</h2>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}

function App() {
  return (
    <div>
      <Student name="Sravya" age={20} />
    </div>
  );
}

export default App;
-----------------------------------------------------------------------------------------------------------------------------------------------
task -9b
import React, { Component } from 'react';

class Student extends Component {
  render() {
    return (
      <div>
        <h2>Student Details</h2>
        <p>Name: {this.props.name}</p>
        <p>Age: {this.props.age}</p>
      </div>
    );
  }
}

class App extends Component {
  render() {
    return (
      <div>
        <Student name="Sravya" age={20} />
      </div>
    );
  }
}

export default App;

------------------------------------------------------------------------------------------
task - 8
-------------------------------------------------------------------------------------

function App() {
  const x=new Date();
  return (
      <header>
        <h1>Current Date and Time</h1>
        <h1>({x.toString()})</h1>
      </header>
  );
}

export default App;

task-7

task -7 

function App() {
  return (
      <header>
        <h1>Hello World</h1>
      </header>
  );
}

export default App;
----------------------------------------------------------------------------------------------------
task-6 jwt
----------------------------------------------------------------------------------------------------
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
--------------------------------------------------------------------------------------------
task -4,5
----------------------------------------------------------------------------------------------------
const express = require('express');
const app = express();

app.use(express.json());

let students = [
    { id: 1, name: "Ravi" },
    { id: 2, name: "Priya" }
];

// Read students
app.get('/students', (req, res) => {
    res.json(students);
});

// Create student
app.post('/students', (req, res) => {
    students.push(req.body);
    res.send("Student added successfully");
});

// Update student
app.put('/students/:id', (req, res) => {
    const student = students.find(s => s.id == req.params.id);

    if (student) {
        student.name = req.body.name;
        res.send("Student updated successfully");
    } else {
        res.send("Student not found");
    }
});

// Delete student
app.delete('/students/:id', (req, res) => {
    students = students.filter(s => s.id != req.params.id);
    res.send("Student deleted successfully");
});

app.listen(3000);
console.log("Server running on port 3000");
-------------------------------------------------------------------------------------------------------------
task -3
--------------------------------------------------------------------------------------------------------------------
const os = require('os');
const fs = require('fs');
const http = require('http');

// OS Module
console.log("Platform:", os.platform());
console.log("Architecture:", os.arch());
console.log("Hostname:", os.hostname());
console.log("OS Type:", os.type());
console.log("Release:", os.release());
console.log("Total Memory:", os.totalmem());
console.log("Free Memory:", os.freemem());
console.log("Home Directory:", os.homedir());
console.log("Temporary Directory:", os.tmpdir());
console.log("CPU Details:", os.cpus().length);

// FS Module
fs.writeFileSync('sample.txt', 'Hello Node.js!');
console.log("File created successfully.");

const data = fs.readFileSync('sample.txt', 'utf8');
console.log("File Content:", data);

fs.appendFileSync('sample.txt', '\nWelcome to File System Module!');
console.log("Data appended successfully.");

console.log("File Exists:", fs.existsSync('sample.txt'));

// HTTP Module
const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end("<h1>Hello World!</h1>");
});

server.listen(3000, () => {
    console.log("Server running at http://localhost:3000");
});
-----------------------------------------------------------------------------------------------------------
task-2
----------------------------------------------------------------------------------------------------------
import { initializeApp } from "https://www.gstatic.com/firebasejs/13.0.0/firebase-app.js";

import { getDatabase, ref, set } from "https://www.gstatic.com/firebasejs/13.0.0/firebase-database.js";

const firebaseConfig = {
    apiKey: "AIzaSyCKhANiY2FpF9Q_DGo4rgizLDNM_32x40g",
    authDomain: "project4-98287.firebaseapp.com",
    databaseURL: "https://project4-98287-default-rtdb.firebaseio.com",
    projectId: "project4-98287",
    storageBucket: "project4-98287.firebasestorage.app",
    messagingSenderId: "535843877964",
    appId: "1:535843877964:web:5cae77fc150a01283bf0e9"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);

window.addStudent = function() {
    let roll = document.getElementById("roll").value.trim();
    let name = document.getElementById("name").value.trim();

    if (roll === "" || name === "") {
        alert("Enter roll number and student name");
        return;
    }

    set(ref(db, "students/" + roll), {
        rollNumber: roll,
        name: name
    })
    .then(() => {
        alert("Student Added Successfully");
    })
    .catch(error => {
        alert("Error: " + error.message);
    });
};
<!DOCTYPE html>
<html>
<head>
    <title>Student Management System</title>
</head>
<body>
    <h2>Student Management System</h2>

    <input id="roll" placeholder="Roll Number">
    <input id="name" placeholder="Student Name">

    <button onclick="addStudent()">Add Student</button>

   

    <script type="module" src="s1.js"></script>
</body>
</html>
---------------------------------------------------------------------------------------
task1
-------------------------------------------------------------------------------------------
git init
git add .
git commit -m "Initial commit"
create repository and copy url
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git branch -M main
git push -u origin main
your filess will appear on github
