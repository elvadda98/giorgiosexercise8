<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Health & Everyday Words</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #ff6b6b, #ff9a9e);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #ff6b6b, #ff9a9e);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #fff5f5, #fff0f3);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #ff6b6b;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.2);
        }

        .word-bank h3 {
            color: #ff6b6b;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #ff6b6b, #ff9a9e);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(255, 107, 107, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 107, 107, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #ff6b6b;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #ff6b6b;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #ff6b6b;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.2);
        }

        .option.selected {
            background: #ff6b6b;
            color: white;
            border-color: #ff6b6b;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #ff6b6b;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #ff6b6b;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.2);
        }

        .match-item.selected {
            background: #fff0f3;
            border-color: #ff6b6b;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #ff6b6b, #ff9a9e);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #ff6b6b, #ff9a9e);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #ff6b6b;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #ff6b6b;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #ff6b6b;
            margin-top: 10px;
        }

        .story-box {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            border: 2px solid #ff6b6b;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .story-box h3 {
            color: #ff6b6b;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .story-box p {
            line-height: 1.8;
            margin-bottom: 15px;
            font-size: 1.1em;
        }

        .highlight {
            background-color: #ffeaa7;
            padding: 2px 5px;
            border-radius: 3px;
            font-weight: bold;
        }

        /* Image placeholders for visual context */
        .visual-hint {
            display: inline-block;
            width: 24px;
            height: 24px;
            margin: 0 5px;
            vertical-align: middle;
            border-radius: 50%;
        }

        .hair { background-color: #8b4513; }
        .fall { background-color: #ff6b6b; }
        .above { background-color: #3498db; }
        .swollen { background-color: #f39c12; }
        .sneeze { background-color: #2ecc71; }
        .throat { background-color: #9b59b6; }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/6</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Health & Everyday Words</h1>
            <p>Learn and practice these useful English words!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('story')">Read the Story</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff6b6b;">Vocabulary Words and Meanings</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>hairdresser <span class="visual-hint hair"></span></h3>
                    <p><strong>Definition:</strong> A person whose occupation is cutting, styling, and arranging hair.</p>
                    <p><strong>Usage:</strong> Professional who works in a salon or barbershop; also called a hairstylist.</p>
                    <p class="example"><strong>Example:</strong> "I have an appointment with my hairdresser on Friday for a haircut."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>fall over <span class="visual-hint fall"></span></h3>
                    <p><strong>Definition:</strong> To lose one's balance and collapse to the ground; to trip and fall.</p>
                    <p><strong>Usage:</strong> Describes accidentally dropping to the ground, often due to slipping or tripping.</p>
                    <p class="example"><strong>Example:</strong> "Be careful on the ice or you might fall over and hurt yourself."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>above <span class="visual-hint above"></span></h3>
                    <p><strong>Definition:</strong> In or to a higher place than something else; over.</p>
                    <p><strong>Usage:</strong> Indicates a higher position relative to something else; opposite of "below."</p>
                    <p class="example"><strong>Example:</strong> "The picture hangs above the fireplace in the living room."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>swollen <span class="visual-hint swollen"></span></h3>
                    <p><strong>Definition:</strong> Enlarged or puffed up, typically as a result of injury, infection, or inflammation.</p>
                    <p><strong>Usage:</strong> Describes body parts that have increased in size due to medical conditions.</p>
                    <p class="example"><strong>Example:</strong> "After twisting her ankle, it became swollen and painful."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>sneeze <span class="visual-hint sneeze"></span></h3>
                    <p><strong>Definition:</strong> To make a sudden, involuntary expulsion of air from the nose and mouth.</p>
                    <p><strong>Usage:</strong> A reflex action often caused by irritation in the nasal passages or allergies.</p>
                    <p class="example"><strong>Example:</strong> "Cover your mouth when you sneeze to prevent spreading germs."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>sore throat <span class="visual-hint throat"></span></h3>
                    <p><strong>Definition:</strong> A painful, dry, or scratchy feeling in the throat.</p>
                    <p><strong>Usage:</strong> Common symptom of colds, flu, or other respiratory infections.</p>
                    <p class="example"><strong>Example:</strong> "She had a sore throat and couldn't speak properly for three days."</p>
                </div>
            </div>
        </div>

        <!-- Story Section -->
        <div id="story" class="game-section">
            <div class="story-box">
                <h3><i class="fas fa-book-open icon"></i> An Unfortunate Day</h3>
                <p>Sarah had booked an appointment with her <span class="highlight">hairdresser</span> for weeks. She was excited to get a new hairstyle. The salon was located on the second floor, <span class="highlight">above</span> a coffee shop. As she walked up the stairs, she didn't notice the wet floor and almost <span class="highlight">fall over</span>!</p>
                
                <p>She managed to catch herself but twisted her ankle in the process. By the time she reached the salon, her ankle was already starting to feel <span class="highlight">swollen</span>. "Are you okay?" asked the hairdresser, noticing her limping.</p>
                
                <p>"I think so," Sarah replied, but her voice was hoarse. She had also been feeling unwell since morning. As she sat in the chair, she suddenly had to <span class="highlight">sneeze</span>. "Bless you!" said the hairdresser, handing her a tissue.</p>
                
                <p>Sarah realized she was coming down with a cold. Her <span class="highlight">sore throat</span> was getting worse by the minute. What started as a day for a new look had turned into a visit to the doctor instead!</p>
                
                <p>After getting her hair done (which looked beautiful despite everything), Sarah went straight to the clinic. The doctor confirmed she had a cold and prescribed rest and medicine for her swollen ankle and sore throat.</p>
            </div>
            
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Vocabulary Words from the Story</h3>
                <div class="word-options">
                    <span class="word-option">hairdresser</span>
                    <span class="word-option">fall over</span>
                    <span class="word-option">above</span>
                    <span class="word-option">swollen</span>
                    <span class="word-option">sneeze</span>
                    <span class="word-option">sore throat</span>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">hairdresser</span>
                    <span class="word-option">fall over</span>
                    <span class="word-option">above</span>
                    <span class="word-option">swollen</span>
                    <span class="word-option">sneeze</span>
                    <span class="word-option">sore throat</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff6b6b;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="hairdresser" onclick="selectMatch(this)">hairdresser</div>
                    <div class="match-item" data-word="fall over" onclick="selectMatch(this)">fall over</div>
                    <div class="match-item" data-word="above" onclick="selectMatch(this)">above</div>
                    <div class="match-item" data-word="swollen" onclick="selectMatch(this)">swollen</div>
                    <div class="match-item" data-word="sneeze" onclick="selectMatch(this)">sneeze</div>
                    <div class="match-item" data-word="sore throat" onclick="selectMatch(this)">sore throat</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "hairdresser", text: "A person who cuts and styles hair professionally" },
            { meaning: "fall over", text: "To lose balance and collapse to the ground" },
            { meaning: "above", text: "In or to a higher place than something else" },
            { meaning: "swollen", text: "Enlarged or puffed up, usually from injury" },
            { meaning: "sneeze", text: "To expel air suddenly from the nose and mouth" },
            { meaning: "sore throat", text: "A painful, scratchy feeling in the throat" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "I have an appointment with my <input type='text' class='fill-blank' data-answer='hairdresser' placeholder='answer'> on Friday for a haircut.", answer: "hairdresser" },
            { text: "Be careful on the ice or you might <input type='text' class='fill-blank' data-answer='fall over' placeholder='answer'> and hurt yourself.", answer: "fall over" },
            { text: "The picture hangs <input type='text' class='fill-blank' data-answer='above' placeholder='answer'> the fireplace in the living room.", answer: "above" },
            { text: "After twisting her ankle, it became <input type='text' class='fill-blank' data-answer='swollen' placeholder='answer'> and painful.", answer: "swollen" },
            { text: "Cover your mouth when you <input type='text' class='fill-blank' data-answer='sneeze' placeholder='answer'> to prevent spreading germs.", answer: "sneeze" },
            { text: "She had a <input type='text' class='fill-blank' data-answer='sore throat' placeholder='answer'> and couldn't speak properly for three days.", answer: "sore throat" },
            { text: "The <input type='text' class='fill-blank' data-answer='hairdresser' placeholder='answer'> suggested a new style that would suit my face shape.", answer: "hairdresser" },
            { text: "Children learning to walk often <input type='text' class='fill-blank' data-answer='fall over' placeholder='answer'> many times before they become steady.", answer: "fall over" },
            { text: "The temperature dropped to 10 degrees <input type='text' class='fill-blank' data-answer='above' placeholder='answer'> freezing last night.", answer: "above" },
            { text: "His finger was <input type='text' class='fill-blank' data-answer='swollen' placeholder='answer'> after he accidentally hit it with a hammer.", answer: "swollen" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences and take only 6
            const shuffledSentences = shuffleArray([...sentences]).slice(0, 6);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Fill in the blank ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score from all sections
            score = fillBlanksCorrect + matchingCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
