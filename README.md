    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GPA Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 20px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            font-weight: bold;
        }
        header img {
            width: 50px; /* Adjust logo size */
            height: auto;
            margin-right: 15px;
        }
        main {
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        table, th, td {
            border: 1px solid #ddd;
        }
        th, td {
            padding: 10px;
            text-align: center;
        }
        th:nth-child(2),
        td:nth-child(2) {
            width: 150px; /* Set wider column width for Credits */
        }
        button {
            margin: 10px 0;
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 4px;
        }
        button:hover {
            background-color: #45a049;
        }
        .delete-btn {
            background-color: #f44336;
            color: white;
            padding: 5px 10px;
            border: none;
            cursor: pointer;
            border-radius: 4px;
        }
        .delete-btn:hover {
            background-color: #d32f2f;
        }
        .result-table {
            display: none;
            margin-top: 20px;
        }
    </style>
    </head>
    <body>
    <header>
        <!-- Insert logo image here -->
        <img src=".png" alt="https://images.app.goo.gl/qvmqJwbnM176x2427">
        <h1>UTeM GPA Calculator</h1>
    </header>
    <main>
        <form id="gpaForm">
            <table id="subjectsTable">
                <thead>
                    <tr>
                        <th>Subject</th>
                        <th>Credits</th>
                        <th>Grade</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="subjectRows">
                </tbody>
            </table>
            <button type="button" onclick="addSubject()">Add Subject</button>
            <button type="button" onclick="calculateGPA()">Calculate GPA</button>
        </form>

        <!-- Table to display GPA calculation results -->
        <table id="resultTable" class="result-table">
            <thead>
                <tr>
                    <th>Total Quality Points</th>
                    <th>Total Credits</th>
                    <th>Your GPA</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td id="totalQualityPoints"></td>
                    <td id="totalCredits"></td>
                    <td id="gpa"></td>
                </tr>
            </tbody>
        </table>
    </main>

    <script>
        function addSubject() {
            const tableBody = document.getElementById('subjectRows');
            const row = document.createElement('tr');

            row.innerHTML = `
                <td><input type="text" name="subjectName" placeholder="Enter subject" required></td>
                <td><input type="number" name="creditHours" placeholder="Enter credits" min="1" max="4" required></td>
                <td>
                    <select name="grade" required>
                        <option value="" disabled selected>Select grade</option>
                        <option value="4.0">A</option>
                        <option value="3.7">A-</option>
                        <option value="3.3">B+</option>
                        <option value="3.0">B</option>
                        <option value="2.7">B-</option>
                        <option value="2.3">C+</option>
                        <option value="2.0">C</option>
                        <option value="1.7">C-</option>
                        <option value="1.3">D+</option>
                        <option value="1.0">D</option>
                        <option value="0.0">E</option>
                    </select>
                </td>
                <td><button type="button" class="delete-btn" onclick="deleteSubject(this)">Delete</button></td>
            `;

            tableBody.appendChild(row);
        }

        function deleteSubject(button) {
            button.parentElement.parentElement.remove();
        }

        function calculateGPA() {
            const tableBody = document.getElementById('subjectRows');
            const rows = tableBody.querySelectorAll('tr');
            let totalQualityPoints = 0;
            let totalCredits = 0;

            rows.forEach(row => {
                const credits = row.querySelector('input[name="creditHours"]').value;
                const grade = row.querySelector('select[name="grade"]').value;

                if (credits && grade) {
                    const creditValue = parseFloat(credits);
                    const gradeValue = parseFloat(grade);

                    totalQualityPoints += creditValue * gradeValue;
                    totalCredits += creditValue;
                }
            });

            const gpa = totalCredits > 0 ? totalQualityPoints / totalCredits : 0;

            // Update the results table
            document.getElementById('totalQualityPoints').textContent = totalQualityPoints.toFixed(2);
            document.getElementById('totalCredits').textContent = totalCredits;
            document.getElementById('gpa').textContent = gpa.toFixed(2);

            // Show the results table
            document.getElementById('resultTable').style.display = 'table';
        }
    </script>
    </body>
    </html>
