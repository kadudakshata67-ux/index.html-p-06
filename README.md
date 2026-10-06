<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Student Grade Calculator</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }

    body {
      min-height: 100vh;
      background: #f3f4f6;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .calculator {
      width: 100%;
      max-width: 450px;
      background: white;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    }

    h1 {
      text-align: center;
      color: #1f2937;
      margin-bottom: 25px;
    }

    .input-group {
      margin-bottom: 15px;
    }

    label {
      display: block;
      margin-bottom: 6px;
      font-weight: bold;
      color: #374151;
    }

    input {
      width: 100%;
      padding: 12px;
      border: 1px solid #d1d5db;
      border-radius: 8px;
      font-size: 16px;
      outline: none;
    }

    input:focus {
      border-color: #4f46e5;
    }

    button {
      width: 100%;
      padding: 13px;
      margin-top: 10px;
      background: #4f46e5;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }

    button:hover {
      background: #4338ca;
    }

    .result {
      display: none;
      margin-top: 25px;
      padding: 20px;
      background: #f9fafb;
      border-radius: 10px;
      border-left: 5px solid #4f46e5;
    }

    .result p {
      margin: 10px 0;
      font-size: 18px;
      color: #374151;
    }

    .grade {
      font-size: 24px !important;
      font-weight: bold;
      color: #4f46e5 !important;
    }

    .error {
      color: #dc2626;
      margin-top: 15px;
      text-align: center;
    }
  </style>
</head>

<body>

  <div class="calculator">

    <h1>Student Grade Calculator</h1>

    <div class="input-group">
      <label for="math">Mathematics</label>
      <input type="number" id="math" min="0" max="100"
             placeholder="Enter marks (0-100)">
    </div>

    <div class="input-group">
      <label for="science">Science</label>
      <input type="number" id="science" min="0" max="100"
             placeholder="Enter marks (0-100)">
    </div>

    <div class="input-group">
      <label for="english">English</label>
      <input type="number" id="english" min="0" max="100"
             placeholder="Enter marks (0-100)">
    </div>

    <div class="input-group">
      <label for="history">History</label>
      <input type="number" id="history" min="0" max="100"
             placeholder="Enter marks (0-100)">
    </div>

    <div class="input-group">
      <label for="computer">Computer</label>
      <input type="number" id="computer" min="0" max="100"
             placeholder="Enter marks (0-100)">
    </div>

    <button onclick="calculateGrade()">
      Calculate Grade
    </button>

    <p id="error" class="error"></p>

    <div id="result" class="result">
      <p>
        <strong>Total Marks:</strong>
        <span id="total"></span> / 500
      </p>

      <p>
        <strong>Percentage:</strong>
        <span id="percentage"></span>%
      </p>

      <p class="grade">
        Grade: <span id="grade"></span>
      </p>
    </div>

  </div>

  <script>
    function calculateGrade() {

      // Get marks from input fields
      const math = Number(document.getElementById("math").value);
      const science = Number(document.getElementById("science").value);
      const english = Number(document.getElementById("english").value);
      const history = Number(document.getElementById("history").value);
      const computer = Number(document.getElementById("computer").value);

      const marks = [math, science, english, history, computer];

      const error = document.getElementById("error");
      const result = document.getElementById("result");

      // Validate marks
      if (
        marks.some(mark => isNaN(mark) || mark < 0 || mark > 100)
      ) {
        error.textContent =
          "Please enter valid marks between 0 and 100 for all subjects.";

        result.style.display = "none";
        return;
      }

      error.textContent = "";

      // Calculate total
      const total = marks.reduce((sum, mark) => sum + mark, 0);

      // Calculate percentage
      const percentage = (total / 500) * 100;

      // Determine grade
      let grade;

      if (percentage >= 90) {
        grade = "A+";
      } else if (percentage >= 80) {
        grade = "A";
      } else if (percentage >= 70) {
        grade = "B";
      } else if (percentage >= 60) {
        grade = "C";
      } else if (percentage >= 50) {
        grade = "D";
      } else {
        grade = "F";
      }

      // Display results
      document.getElementById("total").textContent = total;
      document.getElementById("percentage").textContent =
        percentage.toFixed(2);
      document.getElementById("grade").textContent = grade;

      result.style.display = "block";
    }
  </script>

</body>
</html>
