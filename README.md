<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>나만의 단어장 퀴즈</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family:
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        "Noto Sans KR",
        sans-serif;

      background: #f5f7fb;
      color: #222;
      margin: 0;
      padding: 30px 15px;
    }

    .container {
      max-width: 900px;
      margin: 0 auto;
    }

    h1 {
      text-align: center;
      margin-bottom: 8px;
      color: #222;
    }

    .subtitle {
      text-align: center;
      color: #777;
      margin-bottom: 30px;
    }

    .box {
      background: white;
      border-radius: 14px;
      padding: 24px;
      margin-bottom: 20px;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.06);
    }

    .box h2 {
      margin-top: 0;
      margin-bottom: 18px;
      font-size: 20px;
    }

    .box h3 {
      margin-top: 0;
    }

    .input-flex {
      display: flex;
      gap: 20px;
    }

    .input-group {
      flex: 1;
    }

    label {
      display: block;
      font-weight: bold;
      margin-bottom: 8px;
    }

    textarea {
      width: 100%;
      height: 220px;
      resize: vertical;
      padding: 12px;
      border: 1px solid #d5d9e2;
      border-radius: 10px;
      font-size: 15px;
      line-height: 1.6;
      outline: none;
      transition: border-color 0.2s, box-shadow 0.2s;
    }

    textarea:focus,
    input[type="text"]:focus {
      border-color: #4f7cff;
      box-shadow: 0 0 0 3px rgba(79, 124, 255, 0.12);
    }

    .settings {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 15px;
      margin-top: 20px;
    }

    .setting-card {
      border: 1px solid #e1e5ec;
      border-radius: 10px;
      padding: 15px;
      background: #fafbfe;
    }

    .setting-card strong {
      display: block;
      margin-bottom: 10px;
    }

    .radio-group {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    .radio-option {
      cursor: pointer;
    }

    .radio-option input {
      margin-right: 5px;
    }

    button {
      border: none;
      border-radius: 9px;
      padding: 10px 17px;
      font-size: 15px;
      font-weight: 600;
      cursor: pointer;
      transition: transform 0.1s, opacity 0.2s;
    }

    button:hover {
      opacity: 0.9;
    }

    button:active {
      transform: scale(0.97);
    }

    .btn-primary {
      background: #4f7cff;
      color: white;
    }

    .btn-success {
      background: #18a66a;
      color: white;
    }

    .btn-danger {
      background: #ef5350;
      color: white;
    }

    .btn-gray {
      background: #e9edf3;
      color: #333;
    }

    .btn-orange {
      background: #ff9800;
      color: white;
    }

    .button-row {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 18px;
    }

    .word-count {
      margin-top: 10px;
      color: #777;
      font-size: 14px;
    }

    .quiz-info {
      background: #f1f5ff;
      border-radius: 10px;
      padding: 12px 15px;
      margin-bottom: 18px;
      color: #3157b7;
      font-size: 14px;
    }

    .q-row {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 14px 5px;
      border-bottom: 1px solid #edf0f5;
      flex-wrap: wrap;
    }

    .question-text {
      min-width: 180px;
      flex: 1;
    }

    .answer-input {
      width: 220px;
      padding: 9px 11px;
      border: 1px solid #ccd2dc;
      border-radius: 7px;
      font-size: 15px;
      outline: none;
    }

    .result {
      min-width: 170px;
      font-size: 14px;
    }

    .correct {
      color: #15945b;
      font-weight: bold;
    }

    .wrong {
      color: #e53935;
      font-weight: bold;
    }

    .score-box {
      display: none;
      text-align: center;
      padding: 20px;
      margin-top: 20px;
      border-radius: 12px;
      background: #f7f9ff;
    }

    .score-number {
      font-size: 36px;
      font-weight: bold;
      color: #4f7cff;
      margin: 5px 0;
    }

    .score-detail {
      color: #666;
    }

    .hidden {
      display: none !important;
    }

    .empty-message {
      text-align: center;
      color: #888;
      padding: 30px 10px;
    }

    .saved-status {
      font-size: 13px;
      color: #15945b;
      margin-top: 8px;
    }

    @media (max-width: 700px) {
      body {
        padding: 15px 10px;
      }

      .box {
        padding: 18px;
      }

      .input-flex {
        flex-direction: column;
      }

      .settings {
        grid-template-columns: 1fr;
      }

      .q-row {
        display: block;
      }

      .question-text {
        margin-bottom: 8px;
      }

      .answer-input {
        width: 100%;
      }

      .result {
        margin-top: 8px;
      }

      .button-row button {
        flex: 1;
      }
    }
  </style>
</head>

<body>

<div class="container">

  <h1>📝 나만의 단어장 퀴즈</h1>
  <div class="subtitle">
    직접 만든 단어장으로 영어 단어를 연습해 보세요.
  </div>

  <!-- 단어 입력 -->
  <div class="box">

    <h2>1. 단어장 만들기</h2>

    <div class="input-flex">

      <div class="input-group">
        <label for="qList">🇰🇷 한글 뜻</label>

        <textarea
          id="qList"
          placeholder="근육
정기적인
줄이다
성공하다"></textarea>
      </div>

      <div class="input-group">
        <label for="aList">🇺🇸 영어 단어</label>

        <textarea
          id="aList"
          placeholder="muscle
regular
reduce
succeed"></textarea>
      </div>

    </div>

    <div id="wordCount" class="word-count">
      단어를 입력해 주세요.
    </div>

    <div id="savedStatus" class="saved-status">
      ✓ 입력 내용은 자동으로 저장됩니다.
    </div>

    <div class="button-row">

      <button
        class="btn-primary"
        onclick="startQuiz()">
        🎯 시험 시작
      </button>

      <button
        class="btn-gray"
        onclick="clearVocabulary()">
        🗑️ 단어장 비우기
      </button>

    </div>

  </div>


  <!-- 시험 설정 -->
  <div
    id="settingsArea"
    class="box hidden">

    <h2>⚙️ 시험 설정</h2>

    <div class="settings">

      <!-- 출제 방향 -->
      <div class="setting-card">

        <strong>📚 문제 방향</strong>

        <div class="radio-group">

          <label class="radio-option">
            <input
              type="radio"
              name="direction"
              value="ko-en"
              checked>
            한글 → 영어
          </label>

          <label class="radio-option">
            <input
              type="radio"
              name="direction"
              value="en-ko">
            영어 → 한글
          </label>

        </div>

      </div>


      <!-- 문제 순서 -->
      <div class="setting-card">

        <strong>🔀 문제 순서</strong>

        <div class="radio-group">

          <label class="radio-option">
            <input
              type="radio"
              name="order"
              value="normal"
              checked>
            입력 순서
          </label>

          <label class="radio-option">
            <input
              type="radio"
              name="order"
              value="random">
            랜덤 출제
          </label>

        </div>

      </div>

    </div>

    <div class="button-row">

      <button
        class="btn-primary"
        onclick="beginQuiz()">
        🚀 시험 시작하기
      </button>

      <button
        class="btn-gray"
        onclick="cancelSettings()">
        취소
      </button>

    </div>

  </div>


  <!-- 퀴즈 -->
  <div
    id="quizArea"
    class="box hidden">

    <h2>2. 문제 풀기</h2>

    <div
      id="quizInfo"
      class="quiz-info">
    </div>

    <div id="quizForm"></div>

    <div class="button-row">

      <button
        class="btn-success"
        onclick="checkAnswers()">
        ✅ 채점하기
      </button>

      <button
        class="btn-orange hidden"
        id="retryWrongButton"
        onclick="retryWrong()">
        🔥 오답만 다시 풀기
      </button>

      <button
        class="btn-primary hidden"
        id="restartButton"
        onclick="restartQuiz()">
        🔄 다시 풀기
      </button>

      <button
        class="btn-gray"
        onclick="backToSettings()">
        ⚙️ 시험 설정
      </button>

    </div>


    <!-- 점수 -->
    <div
      id="scoreBox"
      class="score-box">

      <div>이번 시험 점수</div>

      <div
        id="scoreNumber"
        class="score-number">
        0점
      </div>

      <div
        id="scoreDetail"
        class="score-detail">
      </div>

    </div>

  </div>

</div>


<script>

  /*
   * ==========================================
   * 전역 변수
   * ==========================================
   */

  let vocabulary = [];

  let currentQuiz = [];

  let currentDirection = "ko-en";

  let currentOrder = "normal";

  let lastWrongIndexes = [];

  const STORAGE_KEY = "myVocabularyQuiz";


  /*
   * ==========================================
   * 페이지 시작
   * ==========================================
   */

  window.addEventListener("DOMContentLoaded", () => {

    loadVocabulary();

    updateWordCount();

    document
      .getElementById("qList")
      .addEventListener("input", saveVocabulary);

    document
      .getElementById("aList")
      .addEventListener("input", saveVocabulary);

  });


  /*
   * ==========================================
   * 단어장 저장
   * ==========================================
   */

  function saveVocabulary() {

    const questions = getLines(
      document.getElementById("qList").value
    );

    const answers = getLines(
      document.getElementById("aList").value
    );

    const data = {
      questions: questions,
      answers: answers
    };

    localStorage.setItem(
      STORAGE_KEY,
      JSON.stringify(data)
    );

    updateWordCount();

    const savedStatus =
      document.getElementById("savedStatus");

    savedStatus.textContent =
      "✓ 자동 저장됨 " +
      new Date().toLocaleTimeString();
  }


  /*
   * ==========================================
   * 단어장 불러오기
   * ==========================================
   */

  function loadVocabulary() {

    const saved =
      localStorage.getItem(STORAGE_KEY);

    if (!saved) {
      return;
    }

    try {

      const data = JSON.parse(saved);

      if (
        Array.isArray(data.questions) &&
        Array.isArray(data.answers)
      ) {

        document.getElementById("qList").value =
          data.questions.join("\n");

        document.getElementById("aList").value =
          data.answers.join("\n");

      }

    } catch (error) {

      console.error(
        "저장된 단어장을 불러올 수 없습니다.",
        error
      );

    }
  }


  /*
   * ==========================================
   * 줄 정리
   * ==========================================
   */

  function getLines(text) {

    return text
      .split(/\r?\n/)
      .map(line => line.trim())
      .filter(line => line !== "");

  }


  /*
   * ==========================================
   * 단어 수 표시
   * ==========================================
   */

  function updateWordCount() {

    const questions = getLines(
      document.getElementById("qList").value
    );

    const answers = getLines(
      document.getElementById("aList").value
    );

    const countElement =
      document.getElementById("wordCount");

    if (
      questions.length === 0 &&
      answers.length === 0
    ) {

      countElement.textContent =
        "단어를 입력해 주세요.";

      return;
    }

    countElement.textContent =
      `한글 ${questions.length}개 / ` +
      `영어 ${answers.length}개`;

  }


  /*
   * ==========================================
   * 단어장 비우기
   * ==========================================
   */

  function clearVocabulary() {

    const confirmed =
      confirm(
        "저장된 단어장을 모두 삭제할까요?"
      );

    if (!confirmed) {
      return;
    }

    document.getElementById("qList").value = "";
    document.getElementById("aList").value = "";

    localStorage.removeItem(STORAGE_KEY);

    updateWordCount();

    document.getElementById("savedStatus")
      .textContent =
      "단어장이 삭제되었습니다.";

  }


  /*
   * ==========================================
   * 시험 시작 버튼
   * ==========================================
   */

  function startQuiz() {

    const questions = getLines(
      document.getElementById("qList").value
    );

    const answers = getLines(
      document.getElementById("aList").value
    );


    if (
      questions.length === 0 ||
      answers.length === 0
    ) {

      alert(
        "한글 뜻과 영어 단어를 모두 입력해 주세요!"
      );

      return;
    }


    if (
      questions.length !== answers.length
    ) {

      alert(
        `문제와 정답의 개수가 다릅니다.\n\n` +
        `한글 뜻: ${questions.length}개\n` +
        `영어 단어: ${answers.length}개`
      );

      return;
    }


    /*
     * 단어를 객체 형태로 저장
     */

    vocabulary = questions.map(
      (question, index) => ({
        question: question,
        answer: answers[index]
      })
    );


    /*
     * 시험 설정 화면 표시
     */

    document
      .getElementById("settingsArea")
      .classList.remove("hidden");

    document
      .getElementById("settingsArea")
      .scrollIntoView({
        behavior: "smooth"
      });

  }


  /*
   * ==========================================
   * 시험 시작
   * ==========================================
   */

  function beginQuiz() {

    currentDirection =
      document.querySelector(
        'input[name="direction"]:checked'
      ).value;

    currentOrder =
      document.querySelector(
        'input[name="order"]:checked'
      ).value;


    createQuiz(vocabulary);


    document
      .getElementById("settingsArea")
      .classList.add("hidden");

    document
      .getElementById("quizArea")
      .classList.remove("hidden");

    document
      .getElementById("quizArea")
      .scrollIntoView({
        behavior: "smooth"
      });

  }


  /*
   * ==========================================
   * 퀴즈 생성
   * ==========================================
   */

  function createQuiz(words) {

    currentQuiz = [...words];


    /*
     * 랜덤 출제
     */

    if (currentOrder === "random") {

      shuffle(currentQuiz);

    }


    renderQuiz();

  }


  /*
   * ==========================================
   * 랜덤 섞기
   * Fisher-Yates Shuffle
   * ==========================================
   */

  function shuffle(array) {

    for (
      let i = array.length - 1;
      i > 0;
      i--
    ) {

      const j =
        Math.floor(
          Math.random() * (i + 1)
        );

      [
        array[i],
        array[j]
      ] = [
        array[j],
        array[i]
      ];

    }

  }


  /*
   * ==========================================
   * 퀴즈 화면 만들기
   * ==========================================
   */

  function renderQuiz() {

    const quizForm =
      document.getElementById("quizForm");

    quizForm.innerHTML = "";

    const directionText =
      currentDirection === "ko-en"
        ? "🇰🇷 한글 → 🇺🇸 영어"
        : "🇺🇸 영어 → 🇰🇷 한글";

    const orderText =
      currentOrder === "random"
        ? "🔀 랜덤"
        : "📋 입력 순서";


    document.getElementById("quizInfo")
      .textContent =
      `${directionText} · ${orderText} · ` +
      `${currentQuiz.length}문제`;


    currentQuiz.forEach(
      (item, index) => {

        const row =
          document.createElement("div");

        row.className = "q-row";


        /*
         * 문제
         */

        const question =
          document.createElement("span");

        question.className =
          "question-text";

        const questionText =
          currentDirection === "ko-en"
            ? item.question
            : item.answer;

        question.textContent =
          `${index + 1}. ${questionText}`;


        /*
         * 입력칸
         */

        const input =
          document.createElement("input");

        input.type = "text";

        input.className =
          "answer-input";

        input.id =
          `answer-${index}`;

        input.autocomplete =
          "off";

        input.spellcheck = false;


        /*
         * 결과
         */

        const result =
          document.createElement("span");

        result.className =
          "result";

        result.id =
          `result-${index}`;


        row.appendChild(question);
        row.appendChild(input);
        row.appendChild(result);

        quizForm.appendChild(row);


        /*
         * Enter → 다음 문제
         */

        input.addEventListener(
          "keydown",
          event => {

            if (
              event.key !== "Enter"
            ) {

              return;

            }

            event.preventDefault();

            const next =
              document.getElementById(
                `answer-${index + 1}`
              );

            if (next) {

              next.focus();

            } else {

              checkAnswers();

            }

          }
        );

      }
    );


    /*
     * 첫 번째 입력칸 자동 포커스
     */

    const firstInput =
      document.getElementById("answer-0");

    if (firstInput) {
      firstInput.focus();
    }


    /*
     * 점수 초기화
     */

    document
      .getElementById("scoreBox")
      .style.display = "none";

    document
      .getElementById("retryWrongButton")
      .classList.add("hidden");

    document
      .getElementById("restartButton")
      .classList.add("hidden");

  }


  /*
   * ==========================================
   * 정답 비교용
   * ==========================================
   */

  function normalizeAnswer(text) {

    return text
      .trim()
      .toLowerCase()
      .replace(/\s+/g, " ");

  }


  /*
   * ==========================================
   * 채점
   * ==========================================
   */

  function checkAnswers() {

    let correctCount = 0;

    lastWrongIndexes = [];


    currentQuiz.forEach(
      (item, index) => {

        const input =
          document.getElementById(
            `answer-${index}`
          );

        const result =
          document.getElementById(
            `result-${index}`
          );


        if (!input || !result) {
          return;
        }


        const userAnswer =
          normalizeAnswer(
            input.value
          );


        const realAnswer =
          currentDirection === "ko-en"
            ? item.answer
            : item.question;


        const normalizedRealAnswer =
          normalizeAnswer(
            realAnswer
          );


        if (
          userAnswer ===
          normalizedRealAnswer
        ) {

          correctCount++;

          result.textContent =
            " ⭕ 정답!";

          result.className =
            "result correct";

          input.style.borderColor =
            "#18a66a";

        } else {

          lastWrongIndexes.push(index);

          result.textContent =
            ` ❌ 오답 (정답: ${realAnswer})`;

          result.className =
            "result wrong";

          input.style.borderColor =
            "#ef5350";

        }

      }
    );


    /*
     * 점수 계산
     */

    const total =
      currentQuiz.length;

    const percentage =
      total === 0
        ? 0
        : Math.round(
            correctCount / total * 100
          );


    document.getElementById(
      "scoreNumber"
    ).textContent =
      `${percentage}점`;


    document.getElementById(
      "scoreDetail"
    ).textContent =
      `${total}문제 중 ${correctCount}개 정답 · ` +
      `${lastWrongIndexes.length}개 오답`;


    document.getElementById(
      "scoreBox"
    ).style.display = "block";


    /*
     * 오답만 다시 풀기 버튼
     */

    const retryButton =
      document.getElementById(
        "retryWrongButton"
      );


    if (lastWrongIndexes.length > 0) {

      retryButton.classList.remove(
        "hidden"
      );

    } else {

      retryButton.classList.add(
        "hidden"
      );

    }


    /*
     * 다시 풀기 버튼
     */

    document.getElementById(
      "restartButton"
    ).classList.remove(
      "hidden"
    );


    document.getElementById(
      "scoreBox"
    ).scrollIntoView({
      behavior: "smooth"
    });

  }


  /*
   * ==========================================
   * 오답만 다시 풀기
   * ==========================================
   */

  function retryWrong() {

    if (
      lastWrongIndexes.length === 0
    ) {

      alert(
        "다시 풀 오답이 없습니다!"
      );

      return;
    }


    const wrongWords =
      lastWrongIndexes.map(
        index => currentQuiz[index]
      );


    /*
     * 오답 시험에서도 랜덤 설정 적용
     */

    currentQuiz =
      [...wrongWords];


    if (currentOrder === "random") {

      shuffle(currentQuiz);

    }


    renderQuiz();


    document.getElementById(
      "quizArea"
    ).scrollIntoView({
      behavior: "smooth"
    });

  }


  /*
   * ==========================================
   * 같은 설정으로 다시 풀기
   * ==========================================
   */

  function restartQuiz() {

    createQuiz(vocabulary);

    document.getElementById(
      "quizArea"
    ).scrollIntoView({
      behavior: "smooth"
    });

  }


  /*
   * ==========================================
   * 시험 설정으로 돌아가기
   * ==========================================
   */

  function backToSettings() {

    document
      .getElementById("quizArea")
      .classList.add("hidden");

    document
      .getElementById("settingsArea")
      .classList.remove("hidden");

    document
      .getElementById("settingsArea")
      .scrollIntoView({
        behavior: "smooth"
      });

  }


  /*
   * ==========================================
   * 설정 취소
   * ==========================================
   */

  function cancelSettings() {

    document
      .getElementById("settingsArea")
      .classList.add("hidden");

  }


</script>

</body>
</html>
