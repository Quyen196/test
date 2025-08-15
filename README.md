# test
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trò Chơi Ba Định Luật Newton</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cabin:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #F9F6F3;
            --accent-color: #F5C9B0;
            --correct-color: #A6B28B;
            --primary-color: #1C352D;
            --border-radius: 1rem;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        body {
            font-family: 'Cabin', sans-serif;
            background-color: var(--bg-color);
            color: var(--primary-color);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            padding: 1rem;
            box-sizing: border-box;
            text-align: center;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        .game-container {
            background-color: #fff;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            padding: 2rem;
            max-width: 600px;
            width: 100%;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            box-sizing: border-box;
        }

        h1, h2 {
            margin: 0;
            font-weight: 700;
        }

        input {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid var(--accent-color);
            border-radius: 0.5rem;
            font-family: 'Cabin', sans-serif;
            font-size: 1rem;
            box-sizing: border-box;
            transition: border-color 0.3s;
        }
        
        input:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        button {
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 0.5rem;
            font-family: 'Cabin', sans-serif;
            font-weight: 700;
            font-size: 1rem;
            cursor: pointer;
            background-color: var(--accent-color);
            color: var(--primary-color);
            transition: background-color 0.3s, transform 0.1s;
            box-shadow: var(--shadow);
        }

        button:hover {
            background-color: var(--correct-color);
            color: #fff;
            transform: translateY(-2px);
        }

        button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
            transform: none;
        }

        /* Start Screen */
        .start-screen {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        /* Game Screen */
        .game-screen {
            display: none;
            flex-direction: column;
            gap: 1.5rem;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 1.2rem;
            font-weight: 700;
        }

        .question-box {
            background-color: #f5f5f5;
            padding: 1.5rem;
            border-radius: var(--border-radius);
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.05);
            min-height: 100px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            text-align: left;
        }
        
        .question-text {
            font-size: 1.2rem;
            line-height: 1.5;
            font-weight: 700;
            margin-bottom: 1rem;
        }

        .options-container {
            display: flex;
            flex-direction: column;
            gap: 0.75rem;
        }

        .option-button {
            width: 100%;
            background-color: #f5f5f5;
            color: var(--primary-color);
            text-align: left;
            padding: 1rem;
            box-shadow: var(--shadow);
            transition: background-color 0.3s, color 0.3s, transform 0.1s;
        }

        .option-button:hover:not(.selected) {
            background-color: #e0e0e0;
        }

        .option-button.selected {
            background-color: var(--accent-color);
            color: #fff;
        }

        .option-button.correct {
            background-color: var(--correct-color);
            color: #fff;
        }
        
        .option-button.wrong {
            background-color: #e74c3c;
            color: #fff;
        }

        .action-buttons {
            display: flex;
            justify-content: space-between;
            gap: 1rem;
        }

        .action-buttons button {
            flex-grow: 1;
        }

        /* Fill-in-the-blank */
        .fill-in-blank-container {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            text-align: left;
        }

        .fill-in-blank-container input {
            text-align: center;
            font-size: 1.2rem;
            font-weight: 700;
        }

        /* Matching */
        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.75rem;
        }

        .matching-item {
            background-color: #f5f5f5;
            padding: 1rem;
            border-radius: 0.5rem;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.1s;
            box-shadow: var(--shadow);
            user-select: none;
        }

        .matching-item.selected {
            background-color: var(--accent-color);
            color: #fff;
            transform: scale(1.05);
        }

        .matching-item.matched {
            background-color: var(--correct-color);
            color: #fff;
            cursor: default;
        }

        .explanation {
            background-color: var(--accent-color);
            color: var(--primary-color);
            padding: 1rem;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            margin-top: 1rem;
            display: none;
        }
        
        .explanation.show {
            display: block;
        }
        
        /* Result Screen */
        .result-screen {
            display: none;
            flex-direction: column;
            gap: 1.5rem;
        }
        
        .result-screen-capture {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            padding: 2rem;
            background-color: var(--bg-color);
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            margin-bottom: 1rem;
        }
        
        .result-screen-capture h2 {
            color: var(--correct-color);
        }
        
        .score-display {
            font-size: 3rem;
            font-weight: 700;
            color: var(--primary-color);
        }
        
        .message {
            font-size: 1.2rem;
        }

        .icon-container {
            width: 100px;
            height: 100px;
            margin: 0 auto;
            border-radius: 50%;
            background-color: var(--accent-color);
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .icon-container svg {
            width: 60px;
            height: 60px;
            fill: var(--primary-color);
        }
        
        #result-canvas {
            display: none;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .correct-answer-animation {
            animation: pulse 0.5s ease-in-out;
        }

    </style>
</head>
<body>

<div class="game-container">
    <!-- Start Screen -->
    <div id="start-screen" class="start-screen">
        <h2>Trò Chơi Ba Định Luật Newton</h2>
        <p>Hành trình khám phá thế giới vật lý bắt đầu!</p>
        <input type="text" id="user-name" placeholder="Nhập tên của bạn" required>
        <input type="text" id="user-stt" placeholder="Nhập số thứ tự" required>
        <button id="start-button">Bắt đầu</button>
    </div>

    <!-- Game Screen -->
    <div id="game-screen" class="game-screen">
        <div class="header">
            <span id="timer">⏰ 60s</span>
            <span id="score">⭐ Điểm: 0</span>
        </div>
        <div class="question-box">
            <p id="question-text" class="question-text"></p>
            <div id="options-container" class="options-container"></div>
        </div>
        <div id="explanation-box" class="explanation"></div>
        <div class="action-buttons">
            <button id="hint-button">Gợi ý</button>
            <button id="skip-button">Bỏ qua câu hỏi</button>
        </div>
    </div>

    <!-- Result Screen -->
    <div id="result-screen" class="result-screen">
        <div id="result-screen-capture">
            <h2>Kết Quả Trò Chơi</h2>
            <div class="score-display">
                <span id="final-score"></span>/10
            </div>
            <p id="result-message" class="message"></p>
        </div>
        <button id="save-image-button">Lưu ảnh kết quả</button>
        <button onclick="window.location.reload()">Chơi lại</button>
    </div>
    
    <canvas id="result-canvas"></canvas>

</div>

<audio id="correct-sound" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" preload="auto"></audio>
<audio id="wrong-sound" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-13.mp3" preload="auto"></audio>

<script>
    // --- Global Variables and Constants ---
    const startScreen = document.getElementById('start-screen');
    const gameScreen = document.getElementById('game-screen');
    const resultScreen = document.getElementById('result-screen');
    const userNameInput = document.getElementById('user-name');
    const userSttInput = document.getElementById('user-stt');
    const startButton = document.getElementById('start-button');
    const timerDisplay = document.getElementById('timer');
    const scoreDisplay = document.getElementById('score');
    const questionTextElement = document.getElementById('question-text');
    const optionsContainer = document.getElementById('options-container');
    const explanationBox = document.getElementById('explanation-box');
    const hintButton = document.getElementById('hint-button');
    const skipButton = document.getElementById('skip-button');
    const finalScoreDisplay = document.getElementById('final-score');
    const resultMessage = document.getElementById('result-message');
    const saveImageButton = document.getElementById('save-image-button');
    const resultCanvas = document.getElementById('result-canvas');

    const correctSound = document.getElementById('correct-sound');
    const wrongSound = document.getElementById('wrong-sound');

    let currentQuestionIndex = 0;
    let score = 0;
    let timeRemaining = 60;
    let timerInterval;
    let userName, userStt;

    // --- Question Data (Vietnamese) ---
    const questions = [
        // 4 Multiple-choice questions (Trắc nghiệm)
        {
            type: 'multiple_choice',
            question: "Định luật I Newton còn được gọi là gì?",
            options: ["Định luật bảo toàn động lượng", "Định luật quán tính", "Định luật hấp dẫn", "Định luật bảo toàn năng lượng"],
            answer: "Định luật quán tính",
            explanation: "Định luật I Newton mô tả trạng thái của một vật khi không có lực tác dụng, đó chính là tính quán tính của vật.",
            hint: "Nó liên quan đến khả năng duy trì trạng thái chuyển động của vật."
        },
        {
            type: 'multiple_choice',
            question: "Trong công thức $F = ma$, F là gì?",
            options: ["Vận tốc", "Gia tốc", "Lực", "Khối lượng"],
            answer: "Lực",
            explanation: "Trong công thức $F = ma$ của định luật II Newton, F là lực tác dụng lên vật, m là khối lượng, và a là gia tốc.",
            hint: "Nó là nguyên nhân làm thay đổi vận tốc của vật."
        },
        {
            type: 'multiple_choice',
            question: "Một chiếc xe đang di chuyển trên đường thì dừng lại đột ngột. Hành khách bị đổ người về phía trước. Hiện tượng này giải thích bằng định luật nào?",
            options: ["Định luật I Newton", "Định luật II Newton", "Định luật III Newton", "Định luật bảo toàn năng lượng"],
            answer: "Định luật I Newton",
            explanation: "Đây là ví dụ về quán tính. Khi xe dừng lại, hành khách vẫn có xu hướng tiếp tục chuyển động về phía trước.",
            hint: "Nó liên quan đến quán tính của vật."
        },
        {
            type: 'multiple_choice',
            question: "Định luật III Newton nói về điều gì?",
            options: ["Mối quan hệ giữa lực, khối lượng và gia tốc", "Tác dụng giữa hai vật là những lực trực đối", "Vật sẽ giữ nguyên trạng thái nếu không có lực tác dụng", "Sự bảo toàn năng lượng trong va chạm"],
            answer: "Tác dụng giữa hai vật là những lực trực đối",
            explanation: "Định luật III Newton khẳng định rằng khi vật A tác dụng lên vật B một lực, vật B cũng tác dụng lại vật A một lực. Hai lực này có cùng phương, cùng độ lớn nhưng ngược chiều.",
            hint: "Từ khóa là 'lực và phản lực'."
        },
        // 3 Fill-in-the-blank questions (Điền từ)
        {
            type: 'fill_in_blank',
            question: "Theo định luật I Newton, một vật sẽ giữ nguyên trạng thái _____ hoặc chuyển động thẳng đều nếu không có lực nào tác dụng lên nó.",
            answer: "đứng yên",
            explanation: "Định luật I Newton: Một vật sẽ giữ nguyên trạng thái đứng yên hoặc chuyển động thẳng đều nếu không có lực nào tác dụng lên nó, hoặc tổng hợp các lực tác dụng lên nó bằng không.",
            hint: "Trạng thái ngược với chuyển động."
        },
        {
            type: 'fill_in_blank',
            question: "Theo định luật II Newton, gia tốc của một vật có cùng hướng với _____ tác dụng lên vật và độ lớn của nó tỉ lệ thuận với độ lớn của lực và tỉ lệ nghịch với khối lượng của vật.",
            answer: "lực",
            explanation: "Định luật II Newton: Gia tốc của một vật có cùng hướng với lực tác dụng lên vật và độ lớn của nó tỉ lệ thuận với độ lớn của lực và tỉ lệ nghịch với khối lượng của vật.",
            hint: "F trong công thức $F = ma$."
        },
        {
            type: 'fill_in_blank',
            question: "Theo định luật III Newton, hai lực tác dụng và phản lực có cùng phương, cùng _____ nhưng ngược chiều.",
            answer: "độ lớn",
            explanation: "Định luật III Newton: Khi vật A tác dụng lên vật B một lực, thì vật B cũng tác dụng lại vật A một lực. Hai lực này có cùng phương, cùng độ lớn nhưng ngược chiều.",
            hint: "Lượng lực bằng nhau."
        },
        // 3 Matching questions (Nối cặp)
        {
            type: 'matching',
            question: "Hãy nối các định luật với khái niệm liên quan của chúng.",
            options: [
                { id: 'q1', text: 'Định luật I Newton' },
                { id: 'q2', text: 'Định luật II Newton' },
                { id: 'q3', text: 'Định luật III Newton' },
                { id: 'a1', text: 'Lực và phản lực' },
                { id: 'a2', text: 'Công thức $F = ma$' },
                { id: 'a3', text: 'Tính quán tính' }
            ],
            answer: [
                { q: 'q1', a: 'a3' },
                { q: 'q2', a: 'a2' },
                { q: 'q3', a: 'a1' }
            ],
            explanation: "• Định luật I Newton liên quan đến tính quán tính của vật.\n• Định luật II Newton thiết lập mối quan hệ giữa lực, khối lượng và gia tốc qua công thức $F = ma$.\n• Định luật III Newton mô tả mối quan hệ giữa lực tác dụng và lực phản tác dụng.",
            hint: "Định luật thứ ba là về lực và phản lực."
        }
    ];

    // --- Game Logic Functions ---
    
    // Play sound effects
    function playCorrectSound() {
        correctSound.play();
    }
    
    function playWrongSound() {
        wrongSound.play();
    }

    // Initialize the game
    function startGame() {
        userName = userNameInput.value;
        userStt = userSttInput.value;
        if (!userName || !userStt) {
            alert('Vui lòng nhập tên và số thứ tự để bắt đầu!');
            return;
        }

        startScreen.style.display = 'none';
        gameScreen.style.display = 'flex';
        score = 0;
        currentQuestionIndex = 0;
        timeRemaining = 60;
        updateScoreDisplay();
        updateTimer();
        loadQuestion();
    }

    // Update the timer display
    function updateTimer() {
        timerInterval = setInterval(() => {
            timeRemaining--;
            timerDisplay.textContent = `⏰ ${timeRemaining}s`;
            if (timeRemaining <= 0) {
                clearInterval(timerInterval);
                endGame();
            }
        }, 1000);
    }
    
    // Update the score display
    function updateScoreDisplay() {
        scoreDisplay.textContent = `⭐ Điểm: ${score.toFixed(1)}`;
    }

    // Load and display the current question
    function loadQuestion() {
        explanationBox.textContent = '';
        explanationBox.classList.remove('show');
        optionsContainer.innerHTML = '';
        hintButton.disabled = false;

        if (currentQuestionIndex >= questions.length) {
            endGame();
            return;
        }

        const currentQ = questions[currentQuestionIndex];
        questionTextElement.innerHTML = currentQ.question;

        switch (currentQ.type) {
            case 'multiple_choice':
                renderMultipleChoice(currentQ);
                break;
            case 'fill_in_blank':
                renderFillInBlank(currentQ);
                break;
            case 'matching':
                renderMatching(currentQ);
                break;
        }
    }

    // Render multiple choice questions
    function renderMultipleChoice(q) {
        optionsContainer.classList.remove('fill-in-blank-container', 'matching-container');
        optionsContainer.classList.add('options-container');

        q.options.forEach(option => {
            const button = document.createElement('button');
            button.className = 'option-button';
            button.textContent = option;
            button.onclick = () => handleAnswer(button, option);
            optionsContainer.appendChild(button);
        });
    }

    // Handle multiple choice answer
    function handleMultipleChoiceAnswer(selectedButton, selectedAnswer) {
        const correct = selectedAnswer === questions[currentQuestionIndex].answer;
        const allButtons = document.querySelectorAll('.option-button');

        allButtons.forEach(btn => {
            btn.disabled = true;
            if (btn.textContent === questions[currentQuestionIndex].answer) {
                btn.classList.add('correct');
            }
        });

        if (correct) {
            selectedButton.classList.add('correct');
            score += 1;
            playCorrectSound();
        } else {
            selectedButton.classList.add('wrong');
            playWrongSound();
        }

        updateScoreDisplay();
        showExplanation();
        setTimeout(() => {
            currentQuestionIndex++;
            loadQuestion();
        }, 3000);
    }

    // Render fill-in-the-blank questions
    function renderFillInBlank(q) {
        optionsContainer.classList.remove('options-container', 'matching-container');
        optionsContainer.classList.add('fill-in-blank-container');

        const input = document.createElement('input');
        input.type = 'text';
        input.placeholder = 'Nhập từ của bạn...';
        input.id = 'fill-in-input';
        optionsContainer.appendChild(input);

        const submitButton = document.createElement('button');
        submitButton.textContent = 'Gửi câu trả lời';
        submitButton.onclick = () => handleFillInBlankAnswer(input.value);
        optionsContainer.appendChild(submitButton);
    }
    
    // Handle fill-in-the-blank answer
    function handleFillInBlankAnswer(answer) {
        const correct = answer.trim().toLowerCase() === questions[currentQuestionIndex].answer.toLowerCase();
        
        if (correct) {
            score += 1;
            playCorrectSound();
        } else {
            playWrongSound();
        }
        
        updateScoreDisplay();
        showExplanation();
        document.getElementById('fill-in-input').disabled = true;
        document.querySelector('.fill-in-blank-container button').disabled = true;

        setTimeout(() => {
            currentQuestionIndex++;
            loadQuestion();
        }, 3000);
    }
    
    // Render matching questions
    function renderMatching(q) {
        optionsContainer.classList.remove('options-container', 'fill-in-blank-container');
        optionsContainer.classList.add('matching-container');
        
        const qOptions = q.options.filter(o => o.id.startsWith('q'));
        const aOptions = q.options.filter(o => o.id.startsWith('a'));
        
        // Shuffle the answer options to make it a challenge
        aOptions.sort(() => Math.random() - 0.5);

        let selectedQ = null;
        let matchedCount = 0;
        const correctMatches = q.answer.map(pair => ({ ...pair }));

        function checkMatch(qId, aId) {
            const foundMatch = correctMatches.find(m => m.q === qId && m.a === aId);
            if (foundMatch) {
                matchedCount++;
                const qElem = document.getElementById(qId);
                const aElem = document.getElementById(aId);
                qElem.classList.add('matched');
                aElem.classList.add('matched');
                qElem.classList.remove('selected');
                aElem.classList.remove('selected');
                score += 1/3; // Add a third of a point for each correct match

                if (matchedCount === q.answer.length) {
                    playCorrectSound();
                    updateScoreDisplay();
                    showExplanation();
                    setTimeout(() => {
                        currentQuestionIndex++;
                        loadQuestion();
                    }, 3000);
                }
            } else {
                playWrongSound();
                selectedQ = null;
                document.getElementById(qId).classList.remove('selected');
                document.getElementById(aId).classList.remove('selected');
            }
        }
        
        qOptions.forEach(item => {
            const button = document.createElement('button');
            button.className = 'matching-item';
            button.id = item.id;
            button.textContent = item.text;
            button.onclick = () => {
                if (button.classList.contains('matched')) return;
                if (selectedQ && selectedQ.id !== button.id) {
                    selectedQ.classList.remove('selected');
                }
                button.classList.add('selected');
                selectedQ = button;
            };
            optionsContainer.appendChild(button);
        });

        aOptions.forEach(item => {
            const button = document.createElement('button');
            button.className = 'matching-item';
            button.id = item.id;
            button.textContent = item.text;
            button.onclick = () => {
                if (button.classList.contains('matched')) return;
                if (selectedQ) {
                    button.classList.add('selected');
                    checkMatch(selectedQ.id, button.id);
                    selectedQ = null;
                }
            };
            optionsContainer.appendChild(button);
        });

        // Hide hint and skip for this question type
        hintButton.style.display = 'none';
        skipButton.style.display = 'none';
    }


    // Unified answer handler
    function handleAnswer(selectedElement, selectedAnswer) {
        if (questions[currentQuestionIndex].type === 'multiple_choice') {
            handleMultipleChoiceAnswer(selectedElement, selectedAnswer);
        }
    }
    
    // Show the explanation for the current question
    function showExplanation() {
        explanationBox.textContent = questions[currentQuestionIndex].explanation;
        explanationBox.classList.add('show');
    }

    // Handle hint button click
    function handleHint() {
        score = Math.max(0, score - 0.5);
        updateScoreDisplay();
        explanationBox.textContent = `Gợi ý: ${questions[currentQuestionIndex].hint}`;
        explanationBox.classList.add('show');
        hintButton.disabled = true;
    }

    // Handle skip button click
    function handleSkip() {
        explanationBox.textContent = 'Câu hỏi đã được bỏ qua.';
        explanationBox.classList.add('show');
        
        // Wait for a second to show the message before moving on
        setTimeout(() => {
            currentQuestionIndex++;
            loadQuestion();
        }, 1000);
    }
    
    // End the game and show the result screen
    function endGame() {
        clearInterval(timerInterval);
        gameScreen.style.display = 'none';
        resultScreen.style.display = 'flex';
        
        const finalScore = score.toFixed(1);
        finalScoreDisplay.textContent = finalScore;
        
        let message = '';
        if (finalScore >= 5) {
            message = 'Chúc mừng! Bạn đã hoàn thành xuất sắc trò chơi!';
        } else {
            message = 'Đừng buồn! Hãy thử lại và ôn tập thêm nhé!';
        }
        resultMessage.textContent = message;
    }

    // Save the result screen as an image
    saveImageButton.onclick = function() {
        const captureArea = document.getElementById('result-screen-capture');
        const canvas = document.getElementById('result-canvas');
        const ctx = canvas.getContext('2d');
        const dpi = window.devicePixelRatio || 1;
        const width = captureArea.offsetWidth * dpi;
        const height = captureArea.offsetHeight * dpi;

        canvas.width = width;
        canvas.height = height;
        ctx.scale(dpi, dpi);

        // Draw background
        ctx.fillStyle = getComputedStyle(document.body).getPropertyValue('--bg-color');
        ctx.fillRect(0, 0, captureArea.offsetWidth, captureArea.offsetHeight);

        // Draw text and scores
        ctx.fillStyle = getComputedStyle(document.body).getPropertyValue('--primary-color');
        ctx.font = `bold 24px 'Cabin', sans-serif`;
        ctx.textAlign = 'center';
        ctx.fillText('Kết Quả Trò Chơi', captureArea.offsetWidth / 2, 40);
        
        ctx.font = `bold 16px 'Cabin', sans-serif`;
        ctx.fillText(`Học sinh: ${userName}`, captureArea.offsetWidth / 2, 70);
        ctx.fillText(`S.T.T: ${userStt}`, captureArea.offsetWidth / 2, 95);

        ctx.font = `bold 48px 'Cabin', sans-serif`;
        ctx.fillStyle = getComputedStyle(document.body).getPropertyValue('--correct-color');
        ctx.fillText(finalScoreDisplay.textContent + '/10', captureArea.offsetWidth / 2, 160);
        
        ctx.font = `18px 'Cabin', sans-serif`;
        ctx.fillStyle = getComputedStyle(document.body).getPropertyValue('--primary-color');
        ctx.fillText(resultMessage.textContent, captureArea.offsetWidth / 2, 210);

        // Trigger the download
        const link = document.createElement('a');
        link.download = `Ket_qua_tro_choi_vat_ly_${userName}.png`;
        link.href = canvas.toDataURL('image/png');
        link.click();
    };

    // --- Event Listeners ---
    startButton.addEventListener('click', startGame);
    hintButton.addEventListener('click', handleHint);
    skipButton.addEventListener('click', handleSkip);

</script>

</body>
</html>
