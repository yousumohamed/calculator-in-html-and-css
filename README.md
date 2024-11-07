<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="shortcut icon" href="WhatsApp Image 2024-06-19 at 10.50.42 AM.jpeg" type="image/x-icon">
    <style>
        /* General styling */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #a6f2a2;
        }

        .calculator {
            background-color: #333;
            padding: 20px;
            border-radius: 20px;
            width: 280px;
            box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.2);
        }

        .display {
            background-color: #f3f3f3;
            color: #333;
            border-radius: 25px;
            height: 50px;
            text-align: right;
            padding: 0 20px;
            display: flex;
            align-items: center;
            font-size: 2em;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            background-color: #444;
            color: #a6f2a2;
            font-size: 1.5em;
            border: none;
            padding: 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        button:active {
            background-color: #666;
        }

        button.operator {
            color: #f3f3f3;
        }

        /* Specific styling for operators and special buttons */
        .buttons button.c {
            color: #ff6666;
        }

        .buttons button.equal {
            grid-column: span 4;
            background-color: #a6f2a2;
            color: #333;
        }
    </style>
</head>
<body>

    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="c" onclick="clearDisplay()">c</button>
            <button class="operator" onclick="appendOperator('%')">%</button>
            <button class="operator" onclick="appendOperator('/')">÷</button>
            <button class="operator" onclick="appendOperator('*')">×</button>

            <button onclick="appendNumber(7)">7</button>
            <button onclick="appendNumber(8)">8</button>
            <button onclick="appendNumber(9)">9</button>
            <button class="operator" onclick="appendOperator('-')">-</button>

            <button onclick="appendNumber(4)">4</button>
            <button onclick="appendNumber(5)">5</button>
            <button onclick="appendNumber(6)">6</button>
            <button class="operator" onclick="appendOperator('+')">+</button>

            <button onclick="appendNumber(1)">1</button>
            <button onclick="appendNumber(2)">2</button>
            <button onclick="appendNumber(3)">3</button>
            <button onclick="toggleSign()">+/-</button>

            <button onclick="appendNumber(0)">0</button>
            <button class="equal" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let currentInput = '0';
        let operator = null;
        let previousInput = null;

        function clearDisplay() {
            currentInput = '0';
            operator = null;
            previousInput = null;
            updateDisplay();
        }

        function updateDisplay() {
            display.innerText = currentInput;
        }

        function appendNumber(number) {
            if (currentInput === '0') {
                currentInput = number.toString();
            } else {
                currentInput += number.toString();
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (operator !== null) calculate();
            previousInput = currentInput;
            operator = op;
            currentInput = '0';
        }

        function calculate() {
            let result;
            const prev = parseFloat(previousInput);
            const curr = parseFloat(currentInput);

            if (isNaN(prev) || isNaN(curr)) return;

            switch (operator) {
                case '+':
                    result = prev + curr;
                    break;
                case '-':
                    result = prev - curr;
                    break;
                case '*':
                    result = prev * curr;
                    break;
                case '/':
                    result = prev / curr;
                    break;
                case '%':
                    result = prev % curr;
                    break;
            }

            currentInput = result.toString();
            operator = null;
            previousInput = null;
            updateDisplay();
        }

        function toggleSign() {
            currentInput = (-parseFloat(currentInput)).toString();
            updateDisplay();
        }
    </script>

</body>
</html>
