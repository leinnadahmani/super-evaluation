<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Assessment Robustness Diagnostic</title>
<style>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f6f8;
    margin: 0;
    padding: 20px;
}
.container {
    max-width: 900px;
    margin: auto;
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}
h1 {
    text-align: center;
}
.question {
    margin-bottom: 25px;
}
button {
    padding: 12px 20px;
    font-size: 16px;
    background-color: #222;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
button:hover {
    background-color: #444;
}
.result {
    margin-top: 30px;
    padding: 20px;
    background-color: #eef2f7;
    border-radius: 8px;
}
.score {
    font-size: 20px;
    font-weight: bold;
}
.advice {
    margin-top: 15px;
}
</style>
</head>

<body>
<div class="container">
<h1>AI Assessment Robustness Diagnostic Tool</h1>

<form id="diagnosticForm">

<div id="questions"></div>

<button type="button" onclick="calculateScore()">Calculate My Index</button>

</form>

<div id="results" class="result" style="display:none;"></div>

</div>

<script>

const questions = [
"Does the evaluation rely on unsupervised written production?",
"Could the prompt be copied directly into an AI assistant to generate a satisfactory answer?",
"Does the evaluation rely on generic publicly accessible data?",
"Is only the final product assessed without evaluating the process?",
"Is the evaluation entirely asynchronous without real-time interaction?",
"Are assessment criteria focused exclusively on content without reflective dimension?",
"Could a student obtain a good grade without orally explaining their choices?",
"Does the evaluation rely mainly on factual knowledge restitution?",
"Could the task be completed without referring to personal, local, or lived experience?",
"Does the evaluation exclude justification of methodological or argumentative choices?",
"Could the task be completed in a single step without intermediate submissions?",
"Is there no metacognitive or reflective component included?",
"Does the instructor lack prior knowledge of the student’s typical style or progression?",
"Could a generic well-structured text receive a strong grade?",
"Is there no synchronous validation (oral defense, questioning, discussion)?"
];

const questionsContainer = document.getElementById("questions");

questions.forEach((q, index) => {
    questionsContainer.innerHTML += `
    <div class="question">
        <p><strong>${index + 1}. ${q}</strong></p>
        <label><input type="radio" name="q${index}" value="2" required> Yes (+2)</label><br>
        <label><input type="radio" name="q${index}" value="1"> Partially (+1)</label><br>
        <label><input type="radio" name="q${index}" value="0"> No (0)</label>
    </div>
    `;
});

function calculateScore() {

    let total = 0;
    const form = document.forms["diagnosticForm"];

    for (let i = 0; i < questions.length; i++) {
        const radios = form["q" + i];
        for (let radio of radios) {
            if (radio.checked) {
                total += parseInt(radio.value);
            }
        }
    }

    const maxScore = questions.length * 2;
    const robustness = maxScore - total;

    let interpretation = "";
    let advice = "";

    if (total <= maxScore * 0.25) {
        interpretation = "Low vulnerability – Your assessment appears robust.";
        advice = "Continue integrating contextual anchoring, oral validation, and reflective components.";
    } else if (total <= maxScore * 0.5) {
        interpretation = "Moderate vulnerability – Some adjustments are recommended.";
        advice = "Consider adding process documentation, staged submissions, or metacognitive reflection.";
    } else if (total <= maxScore * 0.75) {
        interpretation = "High vulnerability – Your assessment may be significantly exposed to AI substitution.";
        advice = "Integrate oral defense, contextual specificity, and justification of choices.";
    } else {
        interpretation = "Very high vulnerability – Major redesign is recommended.";
        advice = "Redesign the task to include process evaluation, synchronous validation, and local/personal anchoring.";
    }

    document.getElementById("results").style.display = "block";
    document.getElementById("results").innerHTML = `
        <div class="score">AI Vulnerability Index: ${total} / ${maxScore}</div>
        <div class="score">Assessment Robustness Score: ${robustness} / ${maxScore}</div>
        <p><strong>Interpretation:</strong> ${interpretation}</p>
        <div class="advice"><strong>Recommendations:</strong> ${advice}</div>
    `;
}

</script>

</body>
</html>
