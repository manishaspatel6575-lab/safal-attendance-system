# safal-attendance-system
<!DOCTYPE html>
<html>
<head>
  <title>Safal Attendance System</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #4e73df, #1cc88a);
      margin: 0;
      padding: 0;
      text-align: center;
    }

    h1 {
      color: white;
      margin-top: 30px;
      font-size: 36px;
    }

    .card {
      background: white;
      width: 350px;
      margin: 30px auto;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0px 8px 20px rgba(0,0,0,0.2);
    }

    input {
      width: 90%;
      padding: 8px;
      margin: 10px 0;
      border-radius: 6px;
      border: 1px solid #ccc;
    }

    button {
      padding: 8px 15px;
      border: none;
      border-radius: 6px;
      background-color: #4e73df;
      color: white;
      cursor: pointer;
      font-weight: bold;
    }

    button:hover {
      background-color: #2e59d9;
    }

    ul {
      list-style-type: none;
      padding: 0;
    }

    li {
      background: #f8f9fc;
      margin: 8px 0;
      padding: 8px;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    #attendanceSection {
      display: none;
    }

  </style>
</head>

<body>

  <h1>Safal Attendance System</h1>

  <div class="card" id="standardSection">
    <h2>Enter Standard</h2>
    <input type="text" id="standardInput" placeholder="Enter Standard (e.g., 8th)">
    <br>
    <button onclick="setStandard()">Start</button>
  </div>

  <div class="card" id="attendanceSection">
    <h2 id="standardHeading"></h2>

    <input type="text" id="studentName" placeholder="Enter Student Name">
    <br>
    <button onclick="addStudent()">Add Student</button>

    <h3>Student List</h3>
    <ul id="studentList"></ul>
  </div>

<script>
  let students = [];
  let selectedStandard = "";

  function setStandard() {
    selectedStandard = document.getElementById("standardInput").value;

    if (selectedStandard === "") {
      alert("Please enter standard!");
      return;
    }

    document.getElementById("standardSection").style.display = "none";
    document.getElementById("attendanceSection").style.display = "block";
    document.getElementById("standardHeading").innerText =
      "Attendance - Standard " + selectedStandard;
  }

  function addStudent() {
    let name = document.getElementById("studentName").value;
    if (name === "") return;

    students.push({ name: name, present: false });
    document.getElementById("studentName").value = "";
    displayStudents();
  }

  function markAttendance(index) {
    students[index].present = !students[index].present;
    displayStudents();
  }

  function displayStudents() {
    let list = document.getElementById("studentList");
    list.innerHTML = "";

    students.forEach((student, index) => {
      list.innerHTML += `
        <li>
          ${student.name}
          <button onclick="markAttendance(${index})">
            ${student.present ? "Present" : "Absent"}
          </button>
        </li>
      `;
    });
  }
</script>

</body>
</html>
