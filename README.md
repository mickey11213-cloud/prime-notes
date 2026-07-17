<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
  <title>prime×notes</title>
  <style>
    :root {
      color-scheme: light;
      --ink: #152033;
      --paper: #f7f4ee;
      --primary: #244b6f;
      --primary-ink: #ffffff;
      --disabled: #d4d7dc;
      --disabled-ink: #687080;
    }

    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }

    html,
    body {
      height: 100%;
      margin: 0;
      width: 100%;
    }

    body {
      align-items: center;
      background:
        radial-gradient(circle at 20% 16%, rgba(36, 75, 111, .12), transparent 28%),
        linear-gradient(180deg, #fbfaf7 0%, var(--paper) 100%);
      color: var(--ink);
      display: flex;
      font-family: ui-rounded, "SF Pro Rounded", "Hiragino Sans", "Yu Gothic UI", system-ui, sans-serif;
      justify-content: center;
      min-height: 100svh;
      overflow: hidden;
      padding: env(safe-area-inset-top) 0 env(safe-area-inset-bottom);
    }

    .app {
      display: grid;
      height: 100svh;
      max-width: 520px;
      min-height: 0;
      padding: 24px 10px 18px;
      width: 100%;
    }

    .screen {
      display: grid;
      grid-template-rows: auto 1fr auto;
      height: 100%;
    }

    .screen[hidden] {
      display: none;
    }

    .brand {
      display: grid;
      justify-items: center;
      padding-top: 16px;
      text-align: center;
    }

    .app-name {
      font-size: clamp(2.6rem, 13vw, 4.2rem);
      font-weight: 900;
      letter-spacing: 0;
      line-height: .95;
      margin: 0;
      text-transform: lowercase;
    }

    .center-space {
      min-height: 0;
    }

    .mode-grid {
      display: grid;
      gap: 10px;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      padding-bottom: max(0px, env(safe-area-inset-bottom));
    }

    .mode-button {
      align-items: center;
      appearance: none;
      border: 0;
      border-radius: 8px;
      display: flex;
      font: inherit;
      font-size: clamp(.82rem, 3.7vw, .98rem);
      font-weight: 900;
      justify-content: center;
      letter-spacing: 0;
      line-height: 1.15;
      min-height: 68px;
      padding: 12px 10px;
      text-align: center;
      touch-action: manipulation;
      width: 100%;
    }

    .mode-button.stacked {
      flex-direction: column;
      gap: 5px;
    }

    .mode-label {
      display: block;
      font-size: .66em;
      font-weight: 800;
      line-height: 1;
      opacity: .82;
    }

    .mode-title {
      display: block;
      line-height: 1.2;
    }

    .mode-button.primary {
      background: var(--primary);
      box-shadow: 0 12px 28px rgba(36, 75, 111, .22);
      color: var(--primary-ink);
    }

    .mode-button.disabled {
      background: var(--disabled);
      color: var(--disabled-ink);
    }

    .mode-button:focus-visible {
      outline: 3px solid rgba(36, 75, 111, .34);
      outline-offset: 3px;
    }

    .factor-menu {
      display: grid;
      grid-template-rows: auto auto auto auto 1fr;
      gap: 12px;
      height: 100%;
      padding: 26px 0 28px;
    }

    .back-button {
      appearance: none;
      background: rgba(36, 75, 111, .12);
      border: 0;
      border-radius: 8px;
      color: var(--primary);
      font: inherit;
      font-size: .9rem;
      font-weight: 900;
      justify-self: start;
      letter-spacing: 0;
      min-height: 38px;
      padding: 0 14px;
      touch-action: manipulation;
    }

    .ranking-button,
    .menu-tab {
      appearance: none;
      border: 0;
      border-radius: 8px;
      color: var(--primary-ink);
      font: inherit;
      font-weight: 900;
      letter-spacing: 0;
      line-height: 1.2;
      min-height: 64px;
      padding: 14px 12px;
      text-align: center;
      touch-action: manipulation;
      width: 100%;
    }

    .ranking-button {
      background: #b4442d;
      box-shadow: 0 14px 30px rgba(180, 68, 45, .24);
      font-size: clamp(1.05rem, 5vw, 1.3rem);
      min-height: 72px;
    }

    .menu-tab {
      background: var(--primary);
      font-size: clamp(.98rem, 4.4vw, 1.16rem);
    }

    .back-button:focus-visible,
    .ranking-button:focus-visible,
    .menu-tab:focus-visible {
      outline: 3px solid rgba(36, 75, 111, .34);
      outline-offset: 3px;
    }

    .game-screen {
      display: grid;
      gap: 10px;
      grid-template-rows: auto auto minmax(0, 1fr) auto;
      height: 100%;
      padding: 10px 0 0;
    }

    .game-top {
      align-items: center;
      display: flex;
      justify-content: space-between;
      min-height: 40px;
    }

    .question-count {
      color: var(--primary);
      font-size: .95rem;
      font-weight: 900;
    }

    .question-area {
      display: grid;
      gap: 10px;
      grid-template-rows: minmax(112px, 1fr) auto;
      min-height: 0;
    }

    .main-number {
      align-items: center;
      background: rgba(36, 75, 111, .1);
      border: 2px solid rgba(36, 75, 111, .24);
      border-radius: 8px;
      display: flex;
      font-size: clamp(3.2rem, 22vw, 6rem);
      font-weight: 900;
      justify-content: center;
      letter-spacing: 0;
      min-height: 112px;
    }

    .next-row {
      display: grid;
      gap: 8px;
      grid-template-columns: minmax(0, 1fr);
    }

    .next-number {
      align-items: center;
      background: rgba(21, 32, 51, .07);
      border-radius: 8px;
      color: rgba(21, 32, 51, .72);
      display: flex;
      font-size: clamp(1.2rem, 7vw, 1.8rem);
      font-weight: 900;
      justify-content: center;
      min-height: 54px;
    }

    .answer-display {
      align-items: center;
      background: rgba(255, 253, 248, .78);
      border: 2px solid rgba(36, 75, 111, .2);
      border-radius: 8px;
      display: flex;
      font-size: clamp(1.5rem, 8vw, 2.3rem);
      font-weight: 900;
      justify-content: center;
      min-height: 58px;
      padding: 4px 10px;
    }

    .game-keyboard {
      display: grid;
      gap: 0;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      grid-template-rows: repeat(4, minmax(54px, 1fr));
      min-height: 228px;
    }

    .key-button {
      appearance: none;
      background: var(--primary);
      border: 1px solid rgba(247, 244, 238, .34);
      color: var(--primary-ink);
      font: inherit;
      font-size: clamp(1.5rem, 9vw, 2.35rem);
      font-weight: 900;
      letter-spacing: 0;
      min-height: 54px;
      touch-action: manipulation;
    }

    .key-button.utility {
      font-size: clamp(1rem, 5.2vw, 1.35rem);
    }

    .result-panel {
      display: grid;
      grid-template-rows: auto 1fr auto;
      gap: 14px;
      height: 100%;
      justify-items: stretch;
      padding: 26px 0 28px;
      text-align: center;
    }

    .result-title {
      color: var(--ink);
      font-size: clamp(1.4rem, 7vw, 2rem);
      font-weight: 900;
      letter-spacing: 0;
      line-height: 1.2;
      margin: 0;
    }

    .score-block {
      align-content: center;
      display: grid;
      gap: 10px;
      justify-items: center;
    }

    .score-value {
      color: var(--primary);
      font-size: clamp(3rem, 18vw, 5rem);
      font-weight: 900;
      letter-spacing: 0;
      line-height: 1;
    }

    @media (max-height: 620px) {
      .app {
        padding-bottom: 10px;
        padding-top: 10px;
      }

      .brand {
        padding-top: 6px;
      }

      .mode-button {
        min-height: 58px;
      }

      .game-keyboard {
        grid-template-rows: repeat(4, minmax(46px, 1fr));
        min-height: 190px;
      }

      .main-number {
        min-height: 92px;
      }
    }

    @media (max-width: 520px) {
      body {
        align-items: stretch;
        justify-content: stretch;
      }

      .app {
        max-width: none;
        padding-left: 6px;
        padding-right: 6px;
        width: 100vw;
      }

      .factor-menu,
      .result-panel {
        padding-bottom: 10px;
      }

      .game-screen {
        gap: 7px;
        grid-template-rows: auto minmax(0, 1fr) auto minmax(220px, 42svh);
        padding-top: 4px;
      }

      .question-area {
        gap: 7px;
        grid-template-rows: minmax(96px, 1fr) auto;
      }

      .main-number {
        min-height: 96px;
      }

      .answer-display {
        min-height: 48px;
      }

      .game-keyboard {
        min-height: 220px;
      }
    }
  </style>
</head>
<body>
  <main class="app" aria-label="prime×notes home">
    <section class="screen" id="homeScreen">
      <header class="brand">
        <h1 class="app-name">prime×notes</h1>
      </header>

      <div class="center-space" aria-hidden="true"></div>

      <nav class="mode-grid" aria-label="game modes">
        <button class="mode-button primary stacked" id="openFactorMenu" type="button">
          <span class="mode-label">simple factorization</span>
          <span class="mode-title">素因数分解ゲーム</span>
        </button>
        <button class="mode-button disabled" type="button" disabled>coming soon</button>
      </nav>
    </section>

    <section class="screen" id="factorScreen" hidden>
      <nav class="factor-menu" aria-label="simple factorization">
        <button class="back-button" id="backHome" type="button">ホーム</button>
        <button class="ranking-button" type="button">ランキング</button>
        <button class="menu-tab" id="openSimpleLevels" type="button">単純素因数分解</button>
        <button class="menu-tab" type="button">N重素因数分解</button>
      </nav>
    </section>

    <section class="screen" id="simpleLevelScreen" hidden>
      <nav class="factor-menu" aria-label="単純素因数分解">
        <button class="back-button" id="backFactorMenu" type="button">戻る</button>
        <button class="menu-tab" id="startLevelOne" type="button">素因数分解lv1</button>
        <button class="menu-tab" type="button">素因数分解lv2</button>
      </nav>
    </section>

    <section class="screen" id="levelOneGameScreen" hidden>
      <div class="game-screen">
        <div class="game-top">
          <button class="back-button" id="backSimpleLevels" type="button">戻る</button>
          <div class="question-count" id="questionCount">1/20</div>
        </div>

        <section class="question-area" aria-label="素因数分解lv1">
          <div class="main-number" id="mainNumber">10</div>
          <div class="next-row" aria-label="ネクスト1">
            <div class="next-number" id="nextNumberOne"></div>
          </div>
        </section>

        <div class="answer-display" id="answerDisplay" aria-live="polite"></div>

        <div class="game-keyboard" id="gameKeyboard" aria-label="素因数分解ジェネラルキーボード">
          <button class="key-button" type="button" data-key="7">7</button>
          <button class="key-button" type="button" data-key="8">8</button>
          <button class="key-button" type="button" data-key="9">9</button>
          <button class="key-button" type="button" data-key="4">4</button>
          <button class="key-button" type="button" data-key="5">5</button>
          <button class="key-button" type="button" data-key="6">6</button>
          <button class="key-button" type="button" data-key="1">1</button>
          <button class="key-button" type="button" data-key="2">2</button>
          <button class="key-button" type="button" data-key="3">3</button>
          <button class="key-button utility" type="button" data-key="B">B</button>
          <button class="key-button" type="button" data-key="0">0</button>
          <button class="key-button utility" id="acSkipButton" type="button" data-key="AC">AC</button>
        </div>
      </div>
    </section>

    <section class="screen" id="resultScreen" hidden>
      <div class="result-panel">
        <h2 class="result-title">素因数分解lv1</h2>
        <div class="score-block">
          <div class="score-value" id="finalScore">0</div>
        </div>
        <button class="menu-tab" id="resultBackSimpleLevels" type="button">戻る</button>
      </div>
    </section>
  </main>
  <script>
    const homeScreen = document.querySelector("#homeScreen");
    const factorScreen = document.querySelector("#factorScreen");
    const simpleLevelScreen = document.querySelector("#simpleLevelScreen");
    const levelOneGameScreen = document.querySelector("#levelOneGameScreen");
    const resultScreen = document.querySelector("#resultScreen");
    const openFactorMenu = document.querySelector("#openFactorMenu");
    const openSimpleLevels = document.querySelector("#openSimpleLevels");
    const startLevelOne = document.querySelector("#startLevelOne");
    const backHome = document.querySelector("#backHome");
    const backFactorMenu = document.querySelector("#backFactorMenu");
    const backSimpleLevels = document.querySelector("#backSimpleLevels");
    const resultBackSimpleLevels = document.querySelector("#resultBackSimpleLevels");
    const questionCount = document.querySelector("#questionCount");
    const mainNumber = document.querySelector("#mainNumber");
    const nextNumberOne = document.querySelector("#nextNumberOne");
    const answerDisplay = document.querySelector("#answerDisplay");
    const finalScore = document.querySelector("#finalScore");
    const gameKeyboard = document.querySelector("#gameKeyboard");
    const acSkipButton = document.querySelector("#acSkipButton");

    const screens = [homeScreen, factorScreen, simpleLevelScreen, levelOneGameScreen, resultScreen];
    const totalQuestions = 20;
    const scoreUnit = 36000 / totalQuestions;
    let questions = [];
    let questionIndex = 0;
    let questionStartedAt = 0;
    let inputValue = "";
    let score = 0;
    let acPressCount = 0;
    let skipReady = false;

    function showScreen(screen) {
      screens.forEach((item) => {
        item.hidden = item !== screen;
      });
    }

    function factorize(value) {
      const factors = [];
      let rest = value;
      for (let divisor = 2; divisor <= rest; divisor += 1) {
        while (rest % divisor === 0) {
          factors.push(divisor);
          rest /= divisor;
        }
      }
      return factors;
    }

    function isComposite(value) {
      return factorize(value).length > 1;
    }

    function shuffle(list) {
      const shuffled = list.slice();
      for (let index = shuffled.length - 1; index > 0; index -= 1) {
        const swapIndex = Math.floor(Math.random() * (index + 1));
        [shuffled[index], shuffled[swapIndex]] = [shuffled[swapIndex], shuffled[index]];
      }
      return shuffled;
    }

    function buildQuestions() {
      const values = [];
      for (let value = 10; value < 100; value += 1) {
        if (isComposite(value)) values.push(value);
      }
      const pool = shuffle(values).map((value) => {
        const factors = factorize(value);
        return {
          value,
          inputLength: factors.map((factor) => String(factor).length).reduce((sum, length) => sum + length, 0),
          answers: buildAnswers(factors),
        };
      });
      return pickQuestionsWithInputTotal(pool, totalQuestions, 70);
    }

    function pickQuestionsWithInputTotal(pool, count, targetTotal) {
      const ordered = shuffle(pool);
      const memo = new Set();

      function search(startIndex, picked, inputTotal) {
        if (picked.length === count) {
          return inputTotal === targetTotal ? picked : null;
        }
        if (inputTotal >= targetTotal) return null;
        const remaining = count - picked.length;
        if (ordered.length - startIndex < remaining) return null;
        const key = `${startIndex}:${picked.length}:${inputTotal}`;
        if (memo.has(key)) return null;

        for (let index = startIndex; index < ordered.length; index += 1) {
          const question = ordered[index];
          const result = search(index + 1, picked.concat(question), inputTotal + question.inputLength);
          if (result) return result;
        }

        memo.add(key);
        return null;
      }

      const picked = search(0, [], 0);
      return shuffle(picked ?? ordered.slice(0, count));
    }

    function buildAnswers(factors) {
      const answers = new Set();
      const used = Array(factors.length).fill(false);
      const parts = factors.map(String);

      function walk(current) {
        if (current.length === parts.length) {
          answers.add(current.join(""));
          return;
        }
        const seen = new Set();
        for (let index = 0; index < parts.length; index += 1) {
          if (used[index] || seen.has(parts[index])) continue;
          seen.add(parts[index]);
          used[index] = true;
          current.push(parts[index]);
          walk(current);
          current.pop();
          used[index] = false;
        }
      }

      walk([]);
      return [...answers];
    }

    function startGame() {
      questions = buildQuestions();
      questionIndex = 0;
      inputValue = "";
      score = 0;
      acPressCount = 0;
      setSkipReady(false);
      showScreen(levelOneGameScreen);
      showQuestion();
    }

    function setSkipReady(ready) {
      skipReady = ready;
      acSkipButton.textContent = ready ? "skip" : "AC";
      acSkipButton.dataset.key = ready ? "SKIP" : "AC";
    }

    function showQuestion() {
      const current = questions[questionIndex];
      questionCount.textContent = `${questionIndex + 1}/${totalQuestions}`;
      mainNumber.textContent = current.value;
      nextNumberOne.textContent = questions[questionIndex + 1]?.value ?? "";
      inputValue = "";
      answerDisplay.textContent = "";
      acPressCount = 0;
      setSkipReady(false);
      questionStartedAt = performance.now();
    }

    function currentQuestion() {
      return questions[questionIndex];
    }

    function inputCanStillMatch() {
      return currentQuestion().answers.some((answer) => answer.startsWith(inputValue));
    }

    function inputIsCorrect() {
      return currentQuestion().answers.includes(inputValue);
    }

    function applyScore() {
      const elapsed = (performance.now() - questionStartedAt) / 1000;
      const seconds = Math.min(30, Math.round(elapsed * 100) / 100);
      score += Math.round(scoreUnit * (30 - seconds));
    }

    function finishGame() {
      finalScore.textContent = String(score);
      showScreen(resultScreen);
    }

    function advanceQuestion() {
      applyScore();
      moveToNextQuestion();
    }

    function skipQuestion() {
      moveToNextQuestion();
    }

    function moveToNextQuestion() {
      questionIndex += 1;
      if (questionIndex >= totalQuestions) {
        finishGame();
        return;
      }
      showQuestion();
    }

    function renderInput() {
      answerDisplay.textContent = inputValue;
    }

    function handleKey(key) {
      if (levelOneGameScreen.hidden) return;
      if (key === "SKIP") {
        acPressCount = 0;
        setSkipReady(false);
        skipQuestion();
        return;
      }
      if (skipReady) {
        setSkipReady(false);
      }
      if (key === "AC") {
        acPressCount += 1;
        inputValue = "";
        renderInput();
        if (acPressCount >= 2) {
          acPressCount = 0;
          setSkipReady(true);
        }
        return;
      }
      acPressCount = 0;
      if (key === "B") {
        inputValue = inputValue.slice(0, -1);
        renderInput();
        return;
      }
      if (!/^[0-9]$/.test(key)) return;
      const maxLength = Math.max(...currentQuestion().answers.map((answer) => answer.length));
      if (inputValue.length >= maxLength) return;
      inputValue += key;
      renderInput();
      if (inputIsCorrect()) {
        advanceQuestion();
      }
    }

    openFactorMenu.addEventListener("click", () => {
      showScreen(factorScreen);
    });

    backHome.addEventListener("click", () => {
      showScreen(homeScreen);
    });

    openSimpleLevels.addEventListener("click", () => {
      showScreen(simpleLevelScreen);
    });

    backFactorMenu.addEventListener("click", () => {
      showScreen(factorScreen);
    });

    startLevelOne.addEventListener("click", startGame);

    backSimpleLevels.addEventListener("click", () => {
      showScreen(simpleLevelScreen);
    });

    resultBackSimpleLevels.addEventListener("click", () => {
      showScreen(simpleLevelScreen);
    });

    gameKeyboard.addEventListener("click", (event) => {
      const button = event.target.closest("[data-key]");
      if (!button) return;
      handleKey(button.dataset.key);
    });
  </script>
</body>
</html>
