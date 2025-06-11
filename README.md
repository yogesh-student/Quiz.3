<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Class 12 PCM Quiz</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #f0f2f5;
      color: #333;
    }
    h2 {
      color: #2c3e50;
    }
    .question {
      margin-bottom: 20px;
      padding: 15px;
      background: #fff;
      border-radius: 8px;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }
    .result {
      font-size: 20px;
      margin-top: 20px;
      font-weight: bold;
    }
    #timer {
      font-size: 18px;
      color: darkred;
      font-weight: bold;
      margin-bottom: 15px;
    }
  </style>
</head>
<body>

  <h2>Class 12 PCM Quiz</h2>
  <div id="timer">Time Remaining: 20:00</div>

  <form id="quizForm">
    <!-- Questions will load here -->
  </form>

  <button id="submitBtn" onclick="submitQuiz()">Submit Quiz</button>
  <div class="result" id="resultBox"></div>

  <script>
    const quizData = [
      {
        question: "Q1. Which of the following statements is correct?",
        options: ["Melting point: Cu > Ag > Au", "Heat of atomization: Cu > Ag > Au", "Ionisation energy (2nd): Cr > Mn > Fe", "Atomic size: Fe > Co > Ni"],
        answer: 1
      },
      {
        question: "Q2. What is the IUPAC name of cinnamic acid?",
        options: ["3-Phenyl Prop-2-ene-1-carboxylic acid", "4-Phenyl But-2-ene-1-oic acid", "3-Phenyl Prop-2-ene-1-oic acid", "1-Phenyl Prop-1-ene-3-oic acid"],
        answer: 2
      },
      {
        question: "Q3. A galvanometer of 100 Ω gives full-scale deflection at 1 mA. Resistance to convert it into 10 A ammeter?",
        options: ["0.1", "3", "0.01", "2"],
        answer: 2
      },
      {
        question: "Q4. Drift speed of electrons in a copper wire with 1.5 A current and 5 mm² area is?",
        options: ["0.02", "3", "2", "0.2"],
        answer: 0
      },
      {
        question: "Q5. Orthocenter A(–3,5), centroid B(3,3). Radius of circle with AC as diameter is?",
        options: ["2√10", "3√5/√2", "3/2√5", "√10"],
        answer: 1
      },
      {
        question: "Q6. Committee from 6 Indians and 8 foreigners, 2 Indians & twice foreigners. No. of ways?",
        options: ["1625", "575", "560", "1050"],
        answer: 0
      },
      {
        question: "Q7. Triangular matrix X, Water hardness Y, particle displacement y. Value of XY + y?",
        options: ["135", "261", "245", "150"],
        answer: 0
      }
    ];

    const form = document.getElementById("quizForm");
    const submitBtn = document.getElementById("submitBtn");
    const resultBox = document.getElementById("resultBox");

    // Load questions
    quizData.forEach((q, idx) => {
      const div = document.createElement("div");
      div.className = "question";
      div.innerHTML = `<p><strong>${q.question}</strong></p>` + 
        q.options.map((opt, i) =>
          `<label><input type="radio" name="q${idx}" value="${i}"> ${opt}</label><br>`
        ).join('');
      form.appendChild(div);
    });

    // Timer setup (20 minutes)
    let totalTime = 20 * 60; // 20 minutes in seconds
    const timerDisplay = document.getElementById("timer");
    const timer = setInterval(() => {
      const minutes = String(Math.floor(totalTime / 60)).padStart(2, '0');
      const seconds = String(totalTime % 60).padStart(2, '0');
      timerDisplay.innerText = `Time Remaining: ${minutes}:${seconds}`;
      totalTime--;

      if (totalTime < 0) {
        clearInterval(timer);
        if (!submitBtn.disabled) {
          submitQuiz(true);
        }
      }
    }, 1000);

    function submitQuiz(autoSubmit = false) {
      let score = 0;
      quizData.forEach((q, idx) => {
        const selected = document.querySelector(`input[name="q${idx}"]:checked`);
        if (!selected) {
          score -= 2; // Skipped
        } else if (parseInt(selected.value) === q.answer) {
          score += 5;
        } else {
          score -= 5;
        }
      });

      resultBox.innerText = autoSubmit
        ? `⏰ Time's up! Your score: ${score} / 35`
        : `✅ Your score: ${score} / 35`;

      // Disable further input
      submitBtn.disabled = true;
      const inputs = document.querySelectorAll("input");
      inputs.forEach(input => input.disabled = true);
    }
  </script>

</body>
</html>
