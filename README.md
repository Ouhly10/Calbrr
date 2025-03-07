# Calbrr
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ouhllycalc</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #000;
            margin: 0;
        }
        .calculator {
            width: 300px;
            background-color: #1c1c1c;
            border-radius: 20px;
            padding: 15px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5);
        }
        .display {
            width: 100%;
            height: 60px;
            background-color: #000;
            color: #fff;
            font-size: 2em;
            text-align: right;
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 10px;
            overflow-x: auto;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        button {
            width: 100%;
            height: 60px;
            font-size: 1.5em;
            border: none;
            border-radius: 50%;
            cursor: pointer;
            transition: 0.2s;
        }
        .btn-grey { background-color: #a5a5a5; color: #000; }
        .btn-orange { background-color: #ff9500; color: #fff; }
        .btn-dark { background-color: #333; color: #fff; }
        .btn-zero {
            grid-column: span 2;
            border-radius: 30px;
        }
        button:active {
            filter: brightness(85%);
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="btn-grey" onclick="clearDisplay()">AC</button>
            <button class="btn-grey" onclick="toggleSign()">±</button>
            <button class="btn-grey" onclick="percent()">%</button>
            <button class="btn-orange" onclick="operator('/')">÷</button>
            
            <button class="btn-dark" onclick="appendNumber(7)">7</button>
            <button class="btn-dark" onclick="appendNumber(8)">8</button>
            <button class="btn-dark" onclick="appendNumber(9)">9</button>
            <button class="btn-orange" onclick="operator('*')">×</button>
            
            <button class="btn-dark" onclick="appendNumber(4)">4</button>
            <button class="btn-dark" onclick="appendNumber(5)">5</button>
            <button class="btn-dark" onclick="appendNumber(6)">6</button>
            <button class="btn-orange" onclick="operator('-')">−</button>
            
            <button class="btn-dark" onclick="appendNumber(1)">1</button>
            <button class="btn-dark" onclick="appendNumber(2)">2</button>
            <button class="btn-dark" onclick="appendNumber(3)">3</button>
            <button class="btn-orange" onclick="operator('+')">+</button>
            
            <button class="btn-dark btn-zero" onclick="appendNumber(0)">0</button>
            <button class="btn-dark" onclick="appendDot()">.</button>
            <button class="btn-orange" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById("display");
        let currentInput = "";
        let operatorClicked = false;
        let lastOperator = null;

        function appendNumber(num) {
            if (display.innerText === "0" || operatorClicked) {
                display.innerText = num;
            } else {
                display.innerText += num;
            }
            currentInput = display.innerText;
            operatorClicked = false;
        }

        function appendDot() {
            if (!display.innerText.includes(".")) {
                display.innerText += ".";
                currentInput = display.innerText;
            }
        }

        function clearDisplay() {
            display.innerText = "0";
            currentInput = "";
            lastOperator = null;
        }

        function toggleSign() {
            display.innerText = display.innerText.startsWith("-") 
                ? display.innerText.slice(1) 
                : "-" + display.innerText;
            currentInput = display.innerText;
        }

        function percent() {
            display.innerText = parseFloat(display.innerText) / 100;
            currentInput = display.innerText;
        }

        function operator(op) {
            if (lastOperator) {
                calculate();
            }
            currentInput = display.innerText;
            lastOperator = op;
            operatorClicked = true;
        }

        function calculate() {
            if (!lastOperator) return;
            
            let expression = display.innerText;
            try {
                display.innerText = eval(currentInput + lastOperator + expression);
            } catch (error) {
                display.innerText = "خطأ";
            }

            lastOperator = null;
            operatorClicked = false;
        }
    </script>
</body>
</html>
