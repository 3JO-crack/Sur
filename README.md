<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>공군 해커톤 퀴즈</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      text-align: center;
      background-color: #eef2f5;
      padding: 30px;
      overflow-x: hidden;
    }
    .quiz-container {
      max-width: 600px;
      margin: auto;
      background-color: #ffffff;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    }
    h1 {
      color: #003366;
    }
    .question {
      font-size: 20px;
      margin-bottom: 20px;
    }
    .choices button {
      display: block;
      margin: 10px auto;
      padding: 12px 24px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      background-color: #cfd8dc;
      cursor: pointer;
      transition: 0.3s;
    }
    .choices button:hover {
      background-color: #607d8b;
      color: white;
    }
    #result {
      font-size: 22px;
      margin-top: 30px;
      color: #4caf50;
    }
    #photo {
      max-width: 300px;
      margin-top: 20px;
      border-radius: 20px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>2025 공군 해커톤 퀴즈</h1>
    <div id="quiz">
      <div class="question" id="questionText"></div>
      <div class="choices" id="choices"></div>
    </div>
    <div id="result"></div>
    <audio id="bgm"
      src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_57a6e9b0cb.mp3?filename=romantic-day-112194.mp3"
      loop>
    </audio>
  </div>

  <script>
    const quizData = [
      {
        question: "공군 해커톤의 주제 중 하나는?",
        choices: ["AI 기반 조종사 훈련", "우주탐사 로켓 개발", "해양 쓰레기 정화"],
        answer: "ALL"
      },
      {
        question: "해커톤에서 가장 중요한 것은?",
        choices: ["속도", "정확도", "팀워크"],
        answer: "ALL"
      },
      {
        question: "우리의 첫 데이트 장소는?",
        choices: ["행궁동", "광안리", "동탄"],
        answer: "행궁동"
      },
      {
        question: "내가 준 선물 중 없는 것은?",
        choices: ["목걸이", "시계", "다이슨 에어랩"],
        answer: "다이슨 에어랩"
      },
      {
        question: "내가 세상에서 제일 사랑하는 사람은?",
        choices: ["수진", "슈얌보", "황조롱이"],
        answer: "ALL"
      }
    ];

    let currentQuiz = 0;
    let score = 0;
    const questionEl = document.getElementById("questionText");
    const choicesEl = document.getElementById("choices");
    const resultEl = document.getElementById("result");
    const bgm = document.getElementById("bgm");

    function loadQuiz() {
      const current = quizData[currentQuiz];
      questionEl.textContent = current.question;
      choicesEl.innerHTML = "";
      current.choices.forEach(choice => {
        const btn = document.createElement("button");
        btn.textContent = choice;
        btn.onclick = () => checkAnswer(choice);
        choicesEl.appendChild(btn);
      });
    }

    function checkAnswer(choice) {
      const current = quizData[currentQuiz];
      if (current.answer === "ALL" || choice === current.answer) {
        score++;
      }
      currentQuiz++;
      if (currentQuiz < quizData.length) {
        loadQuiz();
      } else {
        showResult();
      }
    }

    function showResult() {
      document.getElementById("quiz").style.display = "none";
      resultEl.innerHTML = `
        <h2>✅ ${score}/${quizData.length}문제 정답!</h2>
        <p>사실은... 이건 공군 해커톤 퀴즈가 아니었어 🥲</p>
        <p>오늘은 우리가 <strong>500일</strong>을 맞이한 날이야 🎉</p>
        <p>500일 동안 함께 해줘서 정말 고마워 수진아 💖</p>
        <p style="font-size: 26px; margin-top: 15px;">💌 영원히 사랑해, 그리고 축하해 💌</p>
        <img id="photo" src="https://i.imgur.com/ZK4YeKw.jpg" alt="우리 사진">
      `;
      bgm.play();
    }

    loadQuiz();
  </script>
</body>
</html>
