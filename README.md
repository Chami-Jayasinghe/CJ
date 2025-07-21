# CJ
A Quiz for College Assignment
<!DOCTYPE html>
<html>
<head>
  <title>PSS-10 Stress Quiz</title>
  <style>
    body { font-family: Arial; max-width: 600px; margin: 0 auto; padding: 20px; }
    .question { margin-bottom: 20px; }
    label { display: block; margin: 5px 0; }
    button { margin-top: 20px; }
    #result { margin-top: 30px; font-weight: bold; font-size: 1.2em; }
  </style>
</head>
<body>

<h2>🧠 How Stressed Are You?</h2>
<form id="stressForm">
  <!-- Dynamically insert 10 questions -->
</form>

<button onclick="calculateScore()">Submit</button>
<div id="result"></div>

<script>
  const questions = [
    { q: "How often have you been upset by something unexpected?", reverse: false },
    { q: "How often have you felt unable to control important things?", reverse: false },
    { q: "How often have you felt nervous and stressed?", reverse: false },
    { q: "How often have you felt confident about handling personal problems?", reverse: true },
    { q: "How often have you felt things were going your way?", reverse: true },
    { q: "How often have you felt unable to cope with all you had to do?", reverse: false },
    { q: "How often have you been able to control irritations in your life?", reverse: true },
    { q: "How often have you felt on top of things?", reverse: true },
    { q: "How often have you been angered by things outside your control?", reverse: false },
    { q: "How often have you felt difficulties piling up too high?", reverse: false },
  ];

  const options = ["Never", "Almost Never", "Sometimes", "Fairly Often", "Very Often"];

  const form = document.getElementById("stressForm");

  questions.forEach((item, i) => {
    const div = document.createElement("div");
    div.className = "question";
    div.innerHTML = `<strong>Q${i+1}:</strong> ${item.q}`;
    options.forEach((opt, index) => {
      div.innerHTML += `
        <label>
          <input type="radio" name="q${i}" value="${item.reverse ? 4 - index : index}" required> ${opt}
        </label>`;
    });
    form.appendChild(div);
  });

  function calculateScore() {
    let score = 0;
    for (let i = 0; i < questions.length; i++) {
      const val = document.querySelector(`input[name="q${i}"]:checked`);
      if (val) score += parseInt(val.value);
    }

    let resultText = "";
    if (score <= 13) {
      resultText = "🟢 Low Stress (0–13): You're doing great!";
    } else if (score <= 26) {
      resultText = "🟠 Moderate Stress (14–26): You're handling a lot, take some mindful breaks.";
    } else {
      resultText = "🔴 High Stress (27–40): Consider self-care or talking to someone you trust.";
    }

    document.getElementById("result").innerText = `Your Score: ${score}\n${resultText}`;
  }
</script>

</body>
</html>
