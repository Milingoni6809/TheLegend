<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sum Calculator</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    }

    body {
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: #f0f2f5;
      padding: 20px;
    }

    .card {
      background: #ffffff;
      padding: 32px;
      border-radius: 16px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
      width: 100%;
      max-width: 400px;
    }

    h2 {
      color: #1a1a1a;
      margin-bottom: 24px;
      text-align: center;
      font-size: 1.5rem;
    }

    .input-group {
      margin-bottom: 16px;
    }

    label {
      display: block;
      margin-bottom: 6px;
      color: #4a5568;
      font-weight: 500;
      font-size: 0.9rem;
    }

    input {
      width: 100%;
      padding: 12px 16px;
      border: 2px solid #e2e8f0;
      border-radius: 8px;
      font-size: 1rem;
      outline: none;
      transition: border-color 0.2s ease;
    }

    input:focus {
      border-color: #3b82f6;
    }

    button {
      width: 100%;
      padding: 12px;
      background-color: #3b82f6;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      margin-top: 8px;
      transition: background-color 0.2s ease;
    }

    button:hover {
      background-color: #2563eb;
    }

    .result-box {
      margin-top: 24px;
      padding: 16px;
      border-radius: 8px;
      background-color: #f8fafc;
      border: 1px solid #e2e8f0;
      text-align: center;
      display: none;
    }

    .result-box.active {
      display: block;
    }

    .result-box.error {
      background-color: #fef2f2;
      border-color: #fecaca;
      color: #dc2626;
    }

    .result-title {
      font-size: 0.85rem;
      color: #64748b;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      margin-bottom: 4px;
    }

    .result-value {
      font-size: 1.75rem;
      font-weight: 700;
      color: #0f172a;
    }
  </style>
</head>
<body>

  <div class="card">
    <h2>Sum Calculator</h2>
    
    <div class="input-group">
      <label for="num1">First Number</label>
      <input type="number" id="num1" placeholder="Enter first number" step="any">
    </div>

    <div class="input-group">
      <label for="num2">Second Number</label>
      <input type="number" id="num2" placeholder="Enter second number" step="any">
    </div>

    <button id="calculateBtn">Calculate Sum</button>

    <div class="result-box" id="resultBox">
      <div class="result-title" id="resultTitle">Result</div>
      <div class="result-value" id="resultValue">0</div>
    </div>
  </div>

  <script>
    const num1Input = document.getElementById('num1');
    const num2Input = document.getElementById('num2');
    const calculateBtn = document.getElementById('calculateBtn');
    const resultBox = document.getElementById('resultBox');
    const resultTitle = document.getElementById('resultTitle');
    const resultValue = document.getElementById('resultValue');

    function computeSum() {
      const val1 = num1Input.value.trim();
      const val2 = num2Input.value.trim();

      // Validation check
      if (val1 === '' || val2 === '') {
        showError('Please enter both numbers.');
        return;
      }

      const num1 = parseFloat(val1);
      const num2 = parseFloat(val2);

      if (isNaN(num1) || isNaN(num2)) {
        showError('Please enter valid numeric values.');
        return;
      }

      const sum = num1 + num2;
      showSuccess(sum);
    }

    function showSuccess(val) {
      resultBox.className = 'result-box active';
      resultTitle.textContent = 'Sum Total';
      resultValue.textContent = val;
    }

    function showError(message) {
      resultBox.className = 'result-box active error';
      resultTitle.textContent = 'Error';
      resultValue.textContent = message;
      resultValue.style.fontSize = '1rem';
    }

    // Event Listeners
    calculateBtn.addEventListener('click', computeSum);

    // Allow pressing "Enter" key in inputs to trigger calculation
    [num1Input, num2Input].forEach(input => {
      input.addEventListener('keypress', (e) => {
        if (e.key === 'Enter') {
          computeSum();
        }
      });
    });
  </script>

</body>
</html>
