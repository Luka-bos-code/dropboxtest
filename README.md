<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Box Compression Drop Test</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      max-width: 800px;
      margin: auto;
    }
    table, th, td {
      border: 1px solid #aaa;
      border-collapse: collapse;
      padding: 8px;
    }
    th {
      background-color: #f0f0f0;
    }
    input, textarea {
      width: 100%;
      box-sizing: border-box;
    }
    .section {
      margin-top: 30px;
    }
    .no-print {
      margin-top: 20px;
    }
    .logo {
      max-width: 150px;
      margin-bottom: 20px;
    }
  </style>
</head>
<body>
  <img src="https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg" class="logo" alt="Logo">
  <h1>Box Compression Drop Test</h1>

  <div class="section" id="formContent">
    <h2>Header Section</h2>
    <label>Date of Test: <input type="date" /></label><br /><br />
    <label>Tester’s Name: <input type="text" /></label><br /><br />
    <label>Box ID or Type: <input type="text" /></label><br /><br />
    <label>Box Dimensions (A × B in cm):<br />
      A: <input type="number" id="aInput" />
      B: <input type="number" id="bInput" />
    </label><br /><br />
    <label>Box Contents and Packed Weight: <input type="text" /></label>

    <div class="section">
      <h2>Auto Calculation</h2>
      <p>
        Area: <span id="areaOutput">-</span> cm²<br />
        Required Weight (A × B × 0.12): <span id="weightOutput">-</span> kg
      </p>
      <button onclick="calculate()">Calculate</button>
    </div>

    <div class="section">
      <h2>Drop Test Results</h2>
      <table>
        <thead>
          <tr>
            <th>Drop #</th>
            <th>Drop Height (cm)</th>
            <th>Damage Observed</th>
            <th>Pass/Fail</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td><input type="number" /></td>
            <td><input type="text" /></td>
            <td><input type="text" /></td>
          </tr>
          <tr>
            <td>2</td>
            <td><input type="number" /></td>
            <td><input type="text" /></td>
            <td><input type="text" /></td>
          </tr>
          <tr>
            <td>3</td>
            <td><input type="number" /></td>
            <td><input type="text" /></td>
            <td><input type="text" /></td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="section">
      <h2>Final Evaluation</h2>
      <label>Did the box withstand all tests successfully? (Yes/No):<br />
        <input type="text" />
      </label><br /><br />
      <label>Summary of issues (if any):<br />
        <textarea rows="3"></textarea>
      </label><br /><br />
      <label>Recommendation for packaging changes:<br />
        <textarea rows="3"></textarea>
      </label>
    </div>
  </div>

  <div class="no-print">
    <button onclick="downloadPDF()">Export as PDF</button>
  </div>

  <script>
    function calculate() {
      const a = parseFloat(document.getElementById("aInput").value);
      const b = parseFloat(document.getElementById("bInput").value);
      if (!isNaN(a) && !isNaN(b)) {
        const area = a * b;
        const weight = area * 0.12;
        document.getElementById("areaOutput").innerText = area.toFixed(2);
        document.getElementById("weightOutput").innerText = weight.toFixed(2);
      } else {
        alert("Please enter both A and B values.");
      }
    }

    async function downloadPDF() {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();

      const content = document.getElementById("formContent");
      await doc.html(document.body, {
        callback: function (doc) {
          doc.save("box-drop-test.pdf");
        },
        x: 10,
        y: 10,
        width: 180,
        windowWidth: 800
      });
    }
  </script>
</body>
</html>
