<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Age Calculator</title>
  <style>
    * {
      box-sizing: border-box;
      font-family: "Poppins", sans-serif;
    }

    body {
      background-image: url('ages.jpg');
      background-position: center;
      background-repeat: no-repeat;
      background-size: cover;
      background-attachment: fixed;
      height: 100vh;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      color: #fff;
    }

    .home, .calculator {
      background: rgba(3, 29, 75, 0.6);
      border-radius: 20px;
      padding: 40px 30px;
      text-align: center;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.4);
      width: 90%;
      max-width: 400px;
      backdrop-filter: blur(5px);
      transition: all 0.5s ease;
    }

    h1 {
      font-size: 28px;
      color: #00e5ff;
      margin-bottom: 15px;
    }

    p {
      font-size: 16px;
      line-height: 1.5;
      color: #f0f0f0;
    }

    .round-btn {
      background-color: #00e5ff;
      border: none;
      color: #000;
      font-weight: bold;
      border-radius: 50%;
      width: 120px;
      height: 120px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 30px;
      transition: 0.4s ease;
      box-shadow: 0 5px 20px rgba(0, 229, 255, 0.4);
    }

    .round-btn:hover {
      background-color: #1de9b6;
      transform: scale(1.05);
    }

    input[type="date"] {
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      border: none;
      outline: none;
      font-size: 16px;
      margin-bottom: 20px;
    }

    button.calc-btn {
      background-color: #00e5ff;
      border: none;
      color: #000;
      padding: 10px 25px;
      font-size: 16px;
      font-weight: bold;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s ease;
    }

    button.calc-btn:hover {
      background-color: #1de9b6;
      transform: scale(1.05);
    }

    .result {
      margin-top: 20px;
      font-size: 18px;
      color: #fff;
    }

    .error {
      color: #ff5252;
      font-size: 14px;
    }

    /* Hide calculator initially */
    .calculator {
      display: none;
    }
  </style>
</head>
<body>

  <!-- Home Page -->
  <div class="home" id="homePage">
    <h1>Age Calculator</h1>
    <p>
      Knowing your age is more than just a number — it helps track health, plan life goals, 
      calculate milestones, and even know your eligibility for various activities and benefits. 
      Let’s find out your exact age in years, months, and days!
    </p>
    <button class="round-btn" onclick="openCalculator()">Start</button>
  </div>

  <!-- Calculator Page -->
  <div class="calculator" id="calculatorPage">
    <h1>Age Calculator</h1>
    <label for="dob">Select Your Date of Birth:</label><br>
    <input type="date" id="dob">
    <div class="error" id="error"></div>
    <button class="calc-btn" onclick="calculateAge()">Calculate</button>
    <div class="result" id="result"></div>
  </div>

  <script>
    function openCalculator() {
      document.getElementById("homePage").style.display = "none";
      document.getElementById("calculatorPage").style.display = "block";
    }

    function calculateAge() {
      const dobInput = document.getElementById("dob").value;
      const result = document.getElementById("result");
      const error = document.getElementById("error");
      result.innerHTML = "";
      error.innerHTML = "";

      if (!dobInput) {
        error.textContent = "⚠ Please select your date of birth.";
        return;
      }

      const dob = new Date(dobInput);
      const today = new Date();

      if (dob > today) {
        error.textContent = "❌ Date of birth cannot be in the future!";
        return;
      }

      let years = today.getFullYear() - dob.getFullYear();
      let months = today.getMonth() - dob.getMonth();
      let days = today.getDate() - dob.getDate();

      if (days < 0) {
        months--;
        const prevMonth = new Date(today.getFullYear(), today.getMonth(), 0);
        days += prevMonth.getDate();
      }

      if (months < 0) {
        years--;
        months += 12;
      }

      result.innerHTML = `
        🎉 You are <b>${(years)}</b> years, <b>${months}</b> months, and <b>${days}</b> days old.
      `;
    }
  </script>

</body>
</html>
