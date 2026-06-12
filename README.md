let students = JSON.parse(localStorage.getItem("students")) || [];

function saveData() {
    localStorage.setItem("students", JSON.stringify(students));
}

function addStudent() {

    let name = document.getElementById("studentName").value;

    if(name === ""){
        alert("Enter student name");
        return;
    }

    students.push({
        name:name,
        status:"Absent"
    });

    saveData();
    displayStudents();

    document.getElementById("studentName").value="";
}

function markAttendance(index){

    if(students[index].status === "Absent"){
        students[index].status = "Present";
    }
    else{
        students[index].status = "Absent";
    }

    saveData();
    displayStudents();
}

function deleteStudent(index){
    students.splice(index,1);
    saveData();
    displayStudents();
}

function displayStudents(){

    let list = document.getElementById("studentList");

    list.innerHTML="";

    students.forEach((student,index)=>{

        let row = `
        <tr>
            <td>${student.name}</td>

            <td class="${
                student.status === "Present"
                ? "present"
                : "absent"
            }">
                ${student.status}
            </td>

            <td>
                <button onclick="markAttendance(${index})">
                    Toggle
                </button>

                <button onclick="deleteStudent(${index})">
                    Delete
                </button>
            </td>
        </tr>
        `;

        list.innerHTML += row;
    });
}

displayStudents();list.innerHTMLbody{
    font-family: Arial, sans-serif;
    background:#f4f4f4;
    margin:0;
    padding:20px;
}

.container{
    max-width:800px;
    margin:auto;
    background:white;
    padding:20px;
    border-radius:10px;
    box-shadow:0 0 10px rgba(0,0,0,0.2);
}

h1{
    text-align:center;
    color:#333;
}

.input-section{
    display:flex;
    gap:10px;
    margin-bottom:20px;
}

input{
    flex:1;
    padding:10px;
}

button{
    padding:10px 15px;
    border:none;
    background:#007bff;
    color:white;
    cursor:pointer;
    border-radius:5px;
}

button:hover{
    background:#0056b3;
}

table{
    width:100%;
    border-collapse:collapse;
}

table th,
table td{
    border:1px solid #ddd;
    padding:12px;
    text-align:center;
}

.present{
    color:green;
    font-weight:bold;
}

.absent{
    color:red;
    font-weight:bold;
}<!DOCTYPE html>
<html>
<head>
    <title>Attendance Management System</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="container">
    <h1>Attendance Management System</h1>

    <div class="input-section">
        <input type="text" id="studentName" placeholder="Enter Student Name">
        <button onclick="addStudent()">Add Student</button>
    </div>

    <table>
        <thead>
            <tr>
                <th>Student Name</th>
                <th>Status</th>
                <th>Action</th>
            </tr>
        </thead>

        <tbody id="studentList">

        </tbody>
    </table>
</div>

<script src="script.js"></script>

</body>
</html>
