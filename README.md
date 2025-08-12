# test
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trắc nghiệm Khoa học Vật liệu</title>
    <!-- Thư viện Tailwind CSS để tạo giao diện đẹp và responsive -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6; /* Nền xám nhạt */
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen">


    <div id="app" class="bg-white p-8 md:p-12 rounded-2xl shadow-xl w-full max-w-lg mx-4 text-center">


        <!-- Màn hình bắt đầu -->
        <div id="start-screen" class="">
            <h1 class="text-3xl font-bold mb-4 text-gray-800">Trắc nghiệm Khoa học Vật liệu</h1>
            <p class="text-gray-600 mb-8">Hãy cùng ôn tập kiến thức từ tài liệu của bạn!</p>
            <button id="start-btn" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-8 rounded-full shadow-lg transition duration-300 transform hover:scale-105 focus:outline-none">
                Bắt đầu
            </button>
        </div>


        <!-- Container chính của bài trắc nghiệm -->
        <div id="quiz-container" class="hidden">
            <h2 id="question-text" class="text-xl md:text-2xl font-semibold mb-6 text-gray-800">Câu hỏi</h2>
           
            <div id="options-container" class="space-y-4">
                <!-- Các nút tùy chọn sẽ được thêm vào đây bằng JavaScript -->
            </div>


            <!-- Vùng phản hồi kết quả -->
            <div id="feedback-container" class="mt-6 h-6">
                <!-- Thông báo đúng/sai sẽ hiển thị ở đây -->
            </div>


            <!-- Nút điều hướng -->
            <div class="mt-8">
                <button id="next-btn" class="bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-8 rounded-full shadow-lg transition duration-300 transform hover:scale-105 focus:outline-none hidden">
                    Câu tiếp theo
                </button>
            </div>
        </div>


        <!-- Màn hình kết quả -->
        <div id="result-screen" class="hidden">
            <h2 class="text-3xl font-bold mb-4 text-gray-800">Kết quả của bạn</h2>
            <p class="text-5xl font-extrabold text-blue-600 mb-4">
                <span id="score-display">0</span>/<span id="total-questions">0</span>
            </p>
            <p id="result-message" class="text-gray-600 mb-8"></p>
            <button id="restart-btn" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-8 rounded-full shadow-lg transition duration-300 transform hover:scale-105 focus:outline-none">
                Làm lại
            </button>
        </div>


    </div>


    <script>
        // Mảng chứa các câu hỏi trắc nghiệm
        const quizQuestions = [
            {
                question: "Công thức nào sau đây biểu diễn định luật Bragg?",
                options: ["$n\\lambda = d\\sin\\theta$", "$n\\lambda = 2d\\sin\\theta$", "$n\\lambda = 2d\\cos\\theta$", "$2n\\lambda = d\\sin\\theta$"],
                correctAnswer: "$n\\lambda = 2d\\sin\\theta$"
            },
            {
                question: "Theo tài liệu, cơ chế chính của hiện tượng nhiễu xạ tia X trong tinh thể là gì?",
                options: [
                    "Sự sắp xếp ngẫu nhiên của các nguyên tử làm tăng cường chùm tán xạ.",
                    "Các nguyên tử sắp xếp có trật tự, tuần hoàn trong không gian làm các chùm tán xạ tăng cường nhau.",
                    "Sự dao động nhiệt của nguyên tử quanh vị trí cân bằng.",
                    "Hiện tượng quang điện."
                ],
                correctAnswer: "Các nguyên tử sắp xếp có trật tự, tuần hoàn trong không gian làm các chùm tán xạ tăng cường nhau."
            },
            {
                question: "Kỹ thuật phân tích nào sau đây dựa trên lý thuyết về hiệu ứng quang điện để xác định thành phần và trạng thái hóa học trên bề mặt vật liệu?",
                options: ["Nhiễu xạ kế tia X (XRD)", "Kính hiển vi lực nguyên tử (AFM)", "Phổ kế quang điện tử tia X (XPS)", "Kính hiển vi điện tử quét (SEM)"],
                correctAnswer: "Phổ kế quang điện tử tia X (XPS)"
            },
            {
                question: "Kỹ thuật nào sau đây cho phép quan sát hình thái học bề mặt của vật rắn ở cấp độ nguyên tử, nhưng yêu cầu mẫu phải là vật liệu dẫn điện?",
                options: ["Kính hiển vi lực nguyên tử (AFM)", "Kính hiển vi điện tử quét (SEM)", "Kính hiển vi quét chui ngầm (STM)", "Nhiễu xạ kế tia X (XRD)"],
                correctAnswer: "Kính hiển vi quét chui ngầm (STM)"
            },
            {
                question: "Đâu là một ưu điểm nổi bật của Kính hiển vi lực nguyên tử (AFM) so với Kính hiển vi quét chui ngầm (STM)?",
                options: [
                    "Tốc độ ghi ảnh nhanh hơn.",
                    "Có thể quan sát cấu trúc nguyên tử riêng lẻ.",
                    "Không yêu cầu mẫu dẫn điện.",
                    "Phải thực hiện trong môi trường chân không cao."
                ],
                correctAnswer: "Không yêu cầu mẫu dẫn điện."
            },
            {
                question: "Theo tài liệu, cơ chế hoạt động của Kính hiển vi lực nguyên tử (AFM) dựa trên nguyên lý nào?",
                options: [
                    "Dòng chui hầm lượng tử.",
                    "Sự tương tác Van der Waals giữa đầu mũi dò và bề mặt mẫu.",
                    "Sự phản xạ của chùm điện tử.",
                    "Hiện tượng quang điện."
                ],
                correctAnswer: "Sự tương tác Van der Waals giữa đầu mũi dò và bề mặt mẫu."
            },
            {
                question: "Trong Kính hiển vi điện tử quét (SEM), hệ thấu kính từ có vai trò chính là gì?",
                options: [
                    "Phát ra chùm điện tử.",
                    "Thu nhận ảnh từ các điện tử thứ cấp.",
                    "Tập trung và điều khiển chùm điện tử.",
                    "Giữ mẫu vật."
                ],
                correctAnswer: "Tập trung và điều khiển chùm điện tử."
            },
            {
                question: "Kỹ thuật chế tạo màng mỏng nào dựa trên nguyên lý truyền động năng bằng cách dùng các ion khí hiếm bắn phá bề mặt bia vật liệu?",
                options: ["Bốc bay nhiệt (Thermal evaporation)", "Quang khắc (Photolithography)", "Phún xạ (Sputtering)", "Khắc chùm tia điện tử (EBL)"],
                correctAnswer: "Phún xạ (Sputtering)"
            },
            {
                question: "Sự khác biệt chính giữa phún xạ DC và phún xạ RF là gì?",
                options: [
                    "Phún xạ DC dùng bia không dẫn điện, phún xạ RF dùng bia dẫn điện.",
                    "Phún xạ DC dùng hiệu điện thế một chiều, phún xạ RF dùng hiệu điện thế xoay chiều.",
                    "Phún xạ DC có tốc độ cao hơn.",
                    "Phún xạ RF không yêu cầu chân không."
                ],
                correctAnswer: "Phún xạ DC dùng hiệu điện thế một chiều, phún xạ RF dùng hiệu điện thế xoay chiều."
            },
            {
                question: "Hiện tượng nào sau đây mô tả sự cộng hưởng của các điện tử tự do trên bề mặt hạt nano kim loại khi tương tác với sóng ánh sáng?",
                options: [
                    "Nhiễu xạ Bragg",
                    "Hiệu ứng quang điện",
                    "Cộng hưởng plasmon bề mặt (SPR)",
                    "Giam hãm lượng tử (Quantum confinement)"
                ],
                correctAnswer: "Cộng hưởng plasmon bề mặt (SPR)"
            }
        ];


        let currentQuestionIndex = 0;
        let score = 0;
        let selectedAnswer = null;


        const app = document.getElementById('app');
        const startScreen = document.getElementById('start-screen');
        const quizContainer = document.getElementById('quiz-container');
        const resultScreen = document.getElementById('result-screen');
       
        const startBtn = document.getElementById('start-btn');
        const questionText = document.getElementById('question-text');
        const optionsContainer = document.getElementById('options-container');
        const feedbackContainer = document.getElementById('feedback-container');
        const nextBtn = document.getElementById('next-btn');
        const restartBtn = document.getElementById('restart-btn');
       
        const scoreDisplay = document.getElementById('score-display');
        const totalQuestionsDisplay = document.getElementById('total-questions');
        const resultMessage = document.getElementById('result-message');


        // Bắt đầu quiz
        startBtn.addEventListener('click', startQuiz);
        nextBtn.addEventListener('click', nextQuestion);
        restartBtn.addEventListener('click', restartQuiz);


        function startQuiz() {
            startScreen.classList.add('hidden');
            quizContainer.classList.remove('hidden');
            score = 0;
            currentQuestionIndex = 0;
            showQuestion();
        }


        function showQuestion() {
            // Xóa các tùy chọn cũ và phản hồi
            optionsContainer.innerHTML = '';
            feedbackContainer.textContent = '';
            nextBtn.classList.add('hidden');


            const currentQuestion = quizQuestions[currentQuestionIndex];
            questionText.textContent = `${currentQuestionIndex + 1}. ${currentQuestion.question}`;
           
            // Xóa các thẻ cũ nếu có để tránh lỗi khi render LaTeX
            const existingScript = document.getElementById('mathjax-script');
            if (existingScript) {
                existingScript.remove();
            }


            // Render lại question text để hiển thị LaTeX nếu có
            if (window.MathJax) {
                window.MathJax.typeset([questionText]);
            }
           
            currentQuestion.options.forEach((option, index) => {
                const button = document.createElement('button');
                button.textContent = option;
                button.classList.add(
                    'w-full', 'py-3', 'px-6', 'rounded-xl', 'text-left', 'text-gray-700',
                    'bg-gray-100', 'hover:bg-gray-200', 'transition', 'duration-200',
                    'focus:outline-none', 'focus:ring-2', 'focus:ring-blue-400'
                );
                button.addEventListener('click', () => selectAnswer(index));
                optionsContainer.appendChild(button);
            });


            // Sau khi thêm các nút, render lại LaTeX trong các nút
            if (window.MathJax) {
                optionsContainer.querySelectorAll('button').forEach(btn => {
                    window.MathJax.typeset([btn]);
                });
            }
        }


        function selectAnswer(selectedIndex) {
            if (selectedAnswer !== null) return; // Ngăn người dùng chọn lại


            selectedAnswer = selectedIndex;
            const currentQuestion = quizQuestions[currentQuestionIndex];
            const options = optionsContainer.querySelectorAll('button');


            options.forEach((option, index) => {
                option.disabled = true; // Vô hiệu hóa tất cả các nút


                // Tô màu cho các nút
                if (index === selectedIndex) {
                    if (option.textContent === currentQuestion.correctAnswer) {
                        option.classList.remove('bg-gray-100');
                        option.classList.add('bg-green-200');
                        score++;
                        feedbackContainer.textContent = "Chính xác!";
                        feedbackContainer.classList.add('text-green-600');
                    } else {
                        option.classList.remove('bg-gray-100');
                        option.classList.add('bg-red-200');
                        feedbackContainer.textContent = "Sai rồi.";
                        feedbackContainer.classList.add('text-red-600');
                    }
                }
                // Tô màu cho câu trả lời đúng nếu người dùng chọn sai
                if (option.textContent === currentQuestion.correctAnswer) {
                    option.classList.remove('bg-gray-100');
                    option.classList.add('bg-green-300');
                }
            });


            nextBtn.classList.remove('hidden');
        }


        function nextQuestion() {
            selectedAnswer = null; // Reset trạng thái chọn
            feedbackContainer.textContent = ''; // Xóa phản hồi
            currentQuestionIndex++;


            if (currentQuestionIndex < quizQuestions.length) {
                showQuestion();
            } else {
                showResult();
            }
        }


        function showResult() {
            quizContainer.classList.add('hidden');
            resultScreen.classList.remove('hidden');
            scoreDisplay.textContent = score;
            totalQuestionsDisplay.textContent = quizQuestions.length;


            let message = "";
            const percentage = (score / quizQuestions.length) * 100;
            if (percentage >= 80) {
                message = "Xuất sắc! Bạn có kiến thức rất vững chắc.";
            } else if (percentage >= 50) {
                message = "Khá tốt! Hãy cố gắng hơn nữa nhé.";
            } else {
                message = "Bạn cần xem lại tài liệu và ôn tập kỹ hơn.";
            }
            resultMessage.textContent = message;
        }


        function restartQuiz() {
            resultScreen.classList.add('hidden');
            startScreen.classList.remove('hidden');
            selectedAnswer = null;
        }
       
        // Cấu hình MathJax để render công thức toán học
        // Thêm thư viện MathJax để xử lý LaTeX
        const script = document.createElement('script');
        script.id = 'mathjax-script';
        script.src = "https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js";
        script.async = true;
        script.onload = () => {
             // Đảm bảo MathJax đã load và sẵn sàng trước khi hiển thị câu hỏi
             if (currentQuestionIndex === 0 && startScreen.classList.contains('hidden')) {
                showQuestion();
             }
        };
        document.head.appendChild(script);


    </script>
</body>
</html>



