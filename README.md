<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Employee Time Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        table {
            width: 80%;
            margin: auto;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid black;
            padding: 10px;
            text-align: center;
        }
        .time-in {
            background-color: blue;
            color: white;
            cursor: pointer;
        }
        .time-out {
            background-color: red;
            color: white;
            cursor: pointer;
        }
        input {
            width: 100%;
            border: none;
            text-align: center;
        }
    </style>
    <script>
        function updateDateTime() {
            document.getElementById('currentDate').innerText = new Date().toLocaleString();
        }
        setInterval(updateDateTime, 1000);

        function recordTime(button, type) {
            let row = button.parentElement.parentElement;
            let cell = type === 'in' ? row.cells[1] : row.cells[2];
            let now = new Date();
            cell.innerText = now.toLocaleTimeString();
            calculateHours(row);
        }

        function calculateHours(row) {
            let timeIn = row.cells[1].innerText;
            let timeOut = row.cells[2].innerText;
            if (timeIn && timeOut) {
                let inTime = new Date(`1970-01-01T${convertTo24Hour(timeIn)}`);
                let outTime = new Date(`1970-01-01T${convertTo24Hour(timeOut)}`);
                let hours = (outTime - inTime) / (1000 * 60 * 60);
                if (hours < 0) hours += 24; // Handle cases where time-out is after midnight
                row.cells[3].innerText = hours.toFixed(2);
            }
        }

        function convertTo24Hour(timeStr) {
            let [time, modifier] = timeStr.split(' ');
            let [hours, minutes, seconds] = time.split(':');
            if (modifier === 'PM' && hours !== '12') {
                hours = parseInt(hours, 10) + 12;
            } else if (modifier === 'AM' && hours === '12') {
                hours = '00';
            }
            return `${hours}:${minutes}:${seconds}`;
        }

        function calculateNetSale(input) {
            let row = input.parentElement.parentElement;
            let grossSale = parseFloat(input.value) || 0;
            let netSaleCell = row.cells[5].querySelector('input');
            netSaleCell.value = (grossSale * 0.92).toFixed(2); // Assuming an 8% deduction
        }
    </script>
</head>
<body>
    <h2>Employee Time Tracker</h2>
    <p>Date & Time: <span id="currentDate"></span></p>
    <table>
        <tr>
            <th>Names</th>
            <th>Time In</th>
            <th>Time Out</th>
            <th>Total Hours</th>
            <th>Gross Sale</th>
            <th>Net Sale</th>
        </tr>
        <tr>
            <td>Ely</td>
            <td><button class="time-in" onclick="recordTime(this, 'in')">Time In</button></td>
            <td><button class="time-out" onclick="recordTime(this, 'out')">Time Out</button></td>
            <td></td>
            <td><input type="text" oninput="calculateNetSale(this)"></td>
            <td><input type="text" readonly></td>
        </tr>
        <tr>
            <td>Jayson</td>
            <td><button class="time-in" onclick="recordTime(this, 'in')">Time In</button></td>
            <td><button class="time-out" onclick="recordTime(this, 'out')">Time Out</button></td>
            <td></td>
            <td><input type="text" oninput="calculateNetSale(this)"></td>
            <td><input type="text" readonly></td>
        </tr>
        <tr>
            <td>Nich</td>
            <td><button class="time-in" onclick="recordTime(this, 'in')">Time In</button></td>
            <td><button class="time-out" onclick="recordTime(this, 'out')">Time Out</button></td>
            <td></td>
            <td><input type="text" oninput="calculateNetSale(this)"></td>
            <td><input type="text" readonly></td>
        </tr>
        <tr>
            <td>Mhearyl</td>
            <td><button class="time-in" onclick="recordTime(this, 'in')">Time In</button></td>
            <td><button class="time-out" onclick="recordTime(this, 'out')">Time Out</button></td>
            <td></td>
            <td><input type="text" oninput="calculateNetSale(this)"></td>
            <td><input type="text" readonly></td>
        </tr>
    </table>
</body>
</html>
