
   
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GPA Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: #f4f4f9;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        table, th, td {
            border: 1px solid #000;
        }
        th, td {
            padding: 10px;
            text-align: center;
        }
        button {
            margin: 10px 0;
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            font-weight: bold;
            margin-top: 20px;
        }
    </style>
    </head>
    <body>
    <h1>GPA Calculator</h1>
    <form id="gpaForm">
        <div id="subjectInputs">
            <div>
                <label>Subject Name: <input type="text" name="subjectName" required></label>
                <label>Credit Hours: <input type="number" name="creditHours" min="1" max="4" required></label>
                <label>Score: <input type="number" name="score" min="0" max="100" required></label>
            </div>
        </div>
        <button type="button" onclick="addSubject()">Add Another Subject</button>
        <button type="button" onclick="calculateGPA()">Calculate GPA</button>
    </form>
    <div class="result" id="result"></div>

    <script>
        function addSubject() {
            const subjectInputs = document.getElementById('subjectInputs');
            const div = document.createElement('div');
            div.innerHTML = `
                <label>Subject Name: <input type="text" name="subjectName" required></label>
                <label>Credit Hours: <input type="number" name="creditHours" min="1" max="4" required></label>
                <label>Score: <input type="number" name="score" min="0" max="100" required></label>
            `;
            subjectInputs.appendChild(div);
        }

        function calculateGPA() {
            const form = document.getElementById('gpaForm');
            const subjectNames = form.querySelectorAll('input[name="subjectName"]');
            const creditHours = form.querySelectorAll('input[name="creditHours"]');
            const scores = form.querySelectorAll('input[name="score"]');
            let totalQualityPoints = 0;
            let totalCredits = 0;

            for (let i = 0; i < subjectNames.length; i++) {
                const score = parseFloat(scores[i].value);
                const credits = parseInt(creditHours[i].value);
                let gradePoint = 0;

                if (score >= 80) gradePoint = 4.0;
                else if (score >= 75) gradePoint = 3.7;
                else if (score >= 70) gradePoint = 3.3;
                else if (score >= 65) gradePoint = 3.0;
                else if (score >= 60) gradePoint = 2.7;
                else if (score >= 55) gradePoint = 2.3;
                else if (score >= 50) gradePoint = 2.0;
                else if (score >= 47) gradePoint = 1.7;
                else if (score >= 44) gradePoint = 1.3;
                else if (score >= 40) gradePoint = 1.0;
                else gradePoint = 0.0;

                totalQualityPoints += gradePoint * credits;
                totalCredits += credits;
            }

            const gpa = totalQualityPoints / totalCredits;
            const resultDiv = document.getElementById('result');
            resultDiv.innerHTML = `
                <p>Total Quality Points: ${totalQualityPoints.toFixed(2)}</p>
                <p>Total Credits: ${totalCredits}</p>
                <p>Your GPA: ${gpa.toFixed(2)}</p>
            `;
        }
    </script>
    </body>
    </html>
