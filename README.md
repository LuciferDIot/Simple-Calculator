<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Calculator</title>
        <!-- Add the Google Fonts link -->
        <link
            rel="stylesheet"
            href="https://fonts.googleapis.com/css2?family=Roboto:wght@400&display=swap"
        />
        <link
            href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
            rel="stylesheet"
            integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN"
            crossorigin="anonymous"
        />
        <script
            src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"
            integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL"
            crossorigin="anonymous"
        ></script>
    </head>
    <body
        class="text-bg-dark d-flex align-items-center justify-content-center vh-100"
        style="font-family: 'Roboto', sans-serif"
    >
        <div class="calculator-container text-bg-primary card p-4">
            <div class="screen" style="height: 50px">
                <div
                    class="w-100 text-bg-light py-2 px-3 card text-end fs-5 fw-bolder display"
                >
                    0
                </div>
            </div>
            <div class="btn-group">
                <div class="btn-group-vertical">
                    <div class="btn-group-lg" role="group">
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('1')"
                        >
                            1
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('2')"
                        >
                            2
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('3')"
                        >
                            3
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendOperator('+')"
                        >
                            +
                        </button>
                    </div>
                    <div class="btn-group-lg" role="group">
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('4')"
                        >
                            4
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('5')"
                        >
                            5
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('6')"
                        >
                            6
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendOperator('-')"
                        >
                            -
                        </button>
                    </div>
                    <div class="btn-group-lg" role="group">
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('7')"
                        >
                            7
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('8')"
                        >
                            8
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="appendValue('9')"
                        >
                            9
                        </button>
                        <button
                            type="button"
                            class="btn btn-primary m-1"
                            onclick="calculateResult()"
                        >
                            =
                        </button>
                    </div>
                </div>
            </div>
        </div>
        <script>
            let currentValue = "";
            let currentOperator = "";
            let resultDisplayed = false;
            function appendValue(value) {
                if (resultDisplayed) {
                    document.querySelector(".display").textContent = "";
                    resultDisplayed = false;
                }
                currentValue += value;
                document.querySelector(".display").textContent = currentValue;
            }
            function appendOperator(operator) {
                currentOperator = operator;
                currentValue += " " + operator + " ";
                document.querySelector(".display").textContent = currentValue;
            }
            function calculateResult() {
                const expression = currentValue.split(" ");
                let operator;
                let result = 0;
                for (let i = 0; i < expression.length; i++) {
                    switch (expression[i]) {
                        case "+":
                            operator = "+";
                            break;
                        case "-":
                            operator = "-";
                            break;
                        default:
                            if (operator) {
                                const operand = parseFloat(
                                    expression[i].replace(" ", "")
                                );
                                if (!isNaN(operand)) {
                                    switch (operator) {
                                        case "+":
                                            result += operand;
                                            break;
                                        case "-":
                                            result -= operand;
                                            break;
                                        default:
                                            break;
                                    }
                                }
                            } else {
                                // If no operator is set, just accumulate the result
                                const operand = parseFloat(
                                    expression[i].replace(" ", "")
                                );
                                if (!isNaN(operand)) {
                                    result += operand;
                                }
                            }
                            break;
                    }
                }
                document.querySelector(".display").textContent = result;
                resultDisplayed = true;
                currentValue = "";
                currentOperator = "";
            }
        </script>
    </body>
</html>
