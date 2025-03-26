<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Colorful Flashcard App</title>
    <style>
        /* CSS Styles with decorative enhancements */
        :root {
            --primary-color: #6a11cb;
            --secondary-color: #2575fc;
            --accent-color: #ff8a00;
            --light-color: #f8f9fa;
            --dark-color: #343a40;
            --success-color: #28a745;
            --danger-color: #dc3545;
            --border-radius: 12px;
            --box-shadow: 0 8px 20px rgba(0, 0, 0, 0.12);
            --transition: all 0.3s ease;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            color: var(--dark-color);
            line-height: 1.6;
        }
        
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        .container {
            width: 100%;
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            position: relative;
        }
        
        h1 {
            color: var(--primary-color);
            font-size: 2.5rem;
            margin-bottom: 10px;
            font-weight: 700;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
            background: linear-gradient(to right, var(--primary-color), var(--secondary-color));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            display: inline-block;
        }
        
        .subtitle {
            color: var(--secondary-color);
            font-size: 1.1rem;
            font-weight: 300;
        }
        
        .flashcard-container {
            perspective: 1000px;
            margin-bottom: 30px;
            height: 350px;
        }
        
        .flashcard {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
            cursor: pointer;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }
        
        .flashcard.flipped {
            transform: rotateY(180deg);
        }
        
        .flashcard-front, .flashcard-back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 30px;
            box-sizing: border-box;
            border-radius: var(--border-radius);
            background: white;
            transition: var(--transition);
        }
        
        .flashcard-front {
            background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
            border: 1px solid rgba(0, 0, 0, 0.05);
        }
        
        .flashcard-back {
            transform: rotateY(180deg);
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border: 1px solid rgba(0, 0, 0, 0.05);
        }
        
        .flashcard-content {
            font-size: 1.5rem;
            text-align: center;
            word-wrap: break-word;
            overflow-y: auto;
            max-height: 100%;
            width: 100%;
            padding: 20px;
            color: var(--dark-color);
        }
        
        .flashcard-front .flashcard-content {
            border-left: 5px solid var(--primary-color);
        }
        
        .flashcard-back .flashcard-content {
            border-left: 5px solid var(--secondary-color);
        }
        
        .controls {
            display: flex;
            justify-content: space-between;
            margin-bottom: 30px;
            gap: 15px;
        }
        
        button {
            background: linear-gradient(to right, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 500;
            transition: var(--transition);
            box-shadow: 0 4px 15px rgba(106, 17, 203, 0.3);
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(106, 17, 203, 0.4);
        }
        
        button:active {
            transform: translateY(0);
        }
        
        button:disabled {
            background: #cccccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .btn-secondary {
            background: linear-gradient(to right, #6c757d, #495057);
        }
        
        .btn-accent {
            background: linear-gradient(to right, var(--accent-color), #ff5e00);
        }
        
        .btn-danger {
            background: linear-gradient(to right, var(--danger-color), #bd2130);
        }
        
        .progress-container {
            background: white;
            padding: 15px;
            border-radius: var(--border-radius);
            margin-bottom: 20px;
            box-shadow: var(--box-shadow);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .progress {
            font-size: 1.1rem;
            color: var(--dark-color);
            font-weight: 500;
        }
        
        .progress-number {
            font-weight: 600;
            color: var(--primary-color);
        }
        
        .add-card-form {
            background: white;
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            margin-bottom: 30px;
            transition: var(--transition);
        }
        
        .add-card-form:hover {
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.15);
        }
        
        .form-title {
            color: var(--primary-color);
            margin-bottom: 20px;
            font-size: 1.5rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .form-title svg {
            width: 24px;
            height: 24px;
            fill: var(--primary-color);
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark-color);
        }
        
        textarea, input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: var(--border-radius);
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
            transition: var(--transition);
        }
        
        textarea:focus, input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(106, 17, 203, 0.2);
        }
        
        textarea {
            height: 100px;
            resize: vertical;
        }
        
        .card-list {
            background: white;
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
        }
        
        .card-list-title {
            color: var(--primary-color);
            margin-bottom: 20px;
            font-size: 1.5rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .card-list-title svg {
            width: 24px;
            height: 24px;
            fill: var(--primary-color);
        }
        
        .card-item {
            padding: 15px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: var(--transition);
            border-radius: 8px;
        }
        
        .card-item:hover {
            background-color: #f8f9fa;
            transform: translateX(5px);
        }
        
        .card-item:last-child {
            border-bottom: none;
        }
        
        .card-text {
            flex: 1;
            font-weight: 500;
        }
        
        .card-actions {
            display: flex;
            gap: 10px;
        }
        
        .empty-state {
            text-align: center;
            padding: 30px;
            color: #6c757d;
        }
        
        .empty-state svg {
            width: 60px;
            height: 60px;
            fill: #dee2e6;
            margin-bottom: 15px;
        }
        
        .empty-state p {
            font-size: 1.1rem;
        }
        
        /* Animation for new card addition */
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .new-card {
            animation: slideIn 0.4s ease-out;
        }
        
        /* Floating decoration elements */
        .decoration {
            position: fixed;
            border-radius: 50%;
            z-index: -1;
            opacity: 0.15;
        }
        
        .decoration-1 {
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, var(--primary-color) 0%, transparent 70%);
            top: -100px;
            right: -100px;
        }
        
        .decoration-2 {
            width: 200px;
            height: 200px;
            background: radial-gradient(circle, var(--secondary-color) 0%, transparent 70%);
            bottom: -50px;
            left: -50px;
        }
        
        /* Responsive adjustments */
        @media (max-width: 768px) {
            .flashcard-container {
                height: 300px;
            }
            
            .flashcard-content {
                font-size: 1.2rem;
            }
            
            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <!-- Decorative background elements -->
    <div class="decoration decoration-1"></div>
    <div class="decoration decoration-2"></div>
    
    <div class="container">
        <header>
            <h1>Flashcard Master</h1>
            <p class="subtitle">Turn your learning into an interactive experience</p>
        </header>
        
        <div class="progress-container">
            <div class="progress">
                Progress: <span class="progress-number" id="current-card">1</span> of <span class="progress-number" id="total-cards">0</span>
            </div>
        </div>
        
        <div class="flashcard-container">
            <div class="flashcard" id="flashcard" onclick="flipCard()">
                <div class="flashcard-front">
                    <div class="flashcard-content" id="front-content">
                        No cards available. Add some flashcards to get started!
                    </div>
                </div>
                <div class="flashcard-back">
                    <div class="flashcard-content" id="back-content"></div>
                </div>
            </div>
        </div>
        
        <div class="controls">
            <button id="prev-btn" onclick="prevCard()" disabled>
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                    <path fill-rule="evenodd" d="M11.354 1.646a.5.5 0 0 1 0 .708L5.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z"/>
                </svg>
                Previous
            </button>
            <button id="flip-btn" onclick="flipCard()" class="btn-accent">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                    <path d="M11.534 7h3.932a.25.25 0 0 1 .192.41l-1.966 2.36a.25.25 0 0 1-.384 0l-1.966-2.36a.25.25 0 0 1 .192-.41zm-11 2h3.932a.25.25 0 0 0 .192-.41L2.692 6.23a.25.25 0 0 0-.384 0L.342 8.59A.25.25 0 0 0 .534 9z"/>
                    <path fill-rule="evenodd" d="M8 3c-1.552 0-2.94.707-3.857 1.818a.5.5 0 1 1-.771-.636A6.002 6.002 0 0 1 13.917 7H12.9A5.002 5.002 0 0 0 8 3zM3.1 9a5.002 5.002 0 0 0 8.757 2.182.5.5 0 1 1 .771.636A6.002 6.002 0 0 1 2.083 9H3.1z"/>
                </svg>
                Flip Card
            </button>
            <button id="next-btn" onclick="nextCard()" disabled>
                Next
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                    <path fill-rule="evenodd" d="M4.646 1.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1 0 .708l-6 6a.5.5 0 0 1-.708-.708L10.293 8 4.646 2.354a.5.5 0 0 1 0-.708z"/>
                </svg>
            </button>
        </div>
        
        <div class="add-card-form">
            <h3 class="form-title">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                    <path d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2z"/>
                </svg>
                Create New Flashcard
            </h3>
            <div class="form-group">
                <label for="front-text">Question/Term</label>
                <textarea id="front-text" placeholder="What is the capital of France?"></textarea>
            </div>
            <div class="form-group">
                <label for="back-text">Answer/Definition</label>
                <textarea id="back-text" placeholder="Paris"></textarea>
            </div>
            <button onclick="addCard()" class="btn-secondary">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
                    <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
                    <path d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"/>
                </svg>
                Add Flashcard
            </button>
        </div>
        
        <div class="card-list">
            <h3 class="card-list-title">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                    <path d="M19 5v14H5V5h14m0-2H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2z"/>
                    <path d="M14 17H7v-2h7v2zm3-4H7v-2h10v2zm0-4H7V7h10v2z"/>
                </svg>
                Your Flashcards
            </h3>
            <div id="cards-container">
                <div class="empty-state">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                        <path d="M19 5v14H5V5h14m0-2H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-4.86 8.86l-3 3.87L9 13.14 6 17h12l-3.86-5.14z"/>
                    </svg>
                    <p>No flashcards yet. Add your first card above!</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // JavaScript for the flashcard app
        let cards = [];
        let currentCardIndex = 0;
        
        // DOM elements
        const flashcardElement = document.getElementById('flashcard');
        const frontContentElement = document.getElementById('front-content');
        const backContentElement = document.getElementById('back-content');
        const prevButton = document.getElementById('prev-btn');
        const nextButton = document.getElementById('next-btn');
        const currentCardSpan = document.getElementById('current-card');
        const totalCardsSpan = document.getElementById('total-cards');
        const cardsContainer = document.getElementById('cards-container');
        
        // Load cards from localStorage if available
        function loadCards() {
            const savedCards = localStorage.getItem('flashcards');
            if (savedCards) {
                cards = JSON.parse(savedCards);
                updateCardDisplay();
                updateCardsList();
            }
            updateTotalCards();
        }
        
        // Save cards to localStorage
        function saveCards() {
            localStorage.setItem('flashcards', JSON.stringify(cards));
            updateTotalCards();
        }
        
        // Flip the current card
        function flipCard() {
            if (cards.length > 0) {
                flashcardElement.classList.toggle('flipped');
            }
        }
        
        // Show the current card
        function showCard(index) {
            if (cards.length > 0 && index >= 0 && index < cards.length) {
                currentCardIndex = index;
                frontContentElement.textContent = cards[index].front;
                backContentElement.textContent = cards[index].back;
                
                // Reset card to front view
                if (flashcardElement.classList.contains('flipped')) {
                    flashcardElement.classList.remove('flipped');
                }
                
                // Update buttons
                prevButton.disabled = index === 0;
                nextButton.disabled = index === cards.length - 1;
                
                // Update progress
                currentCardSpan.textContent = index + 1;
            }
        }
        
        // Go to the next card
        function nextCard() {
            if (currentCardIndex < cards.length - 1) {
                showCard(currentCardIndex + 1);
            }
        }
        
        // Go to the previous card
        function prevCard() {
            if (currentCardIndex > 0) {
                showCard(currentCardIndex - 1);
            }
        }
        
        // Add a new card
        function addCard() {
            const frontText = document.getElementById('front-text').value.trim();
            const backText = document.getElementById('back-text').value.trim();
            
            if (frontText && backText) {
                const newCard = {
                    front: frontText,
                    back: backText
                };
                
                cards.push(newCard);
                saveCards();
                showCard(cards.length - 1);
                updateCardsList();
                
                // Clear the form
                document.getElementById('front-text').value = '';
                document.getElementById('back-text').value = '';
                
                // Focus back to the first input
                document.getElementById('front-text').focus();
            } else {
                alert('Please enter both question and answer for the flashcard.');
            }
        }
        
        // Delete a card
        function deleteCard(index) {
            if (confirm('Are you sure you want to delete this flashcard?')) {
                cards.splice(index, 1);
                saveCards();
                
                if (cards.length === 0) {
                    frontContentElement.textContent = 'No cards available. Add some flashcards to get started!';
                    backContentElement.textContent = '';
                    currentCardIndex = 0;
                } else if (currentCardIndex >= cards.length) {
                    showCard(cards.length - 1);
                } else {
                    showCard(currentCardIndex);
                }
                
                updateCardsList();
            }
        }
        
        // Update the cards list display
        function updateCardsList() {
            if (cards.length === 0) {
                cardsContainer.innerHTML = `
                    <div class="empty-state">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                            <path d="M19 5v14H5V5h14m0-2H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-4.86 8.86l-3 3.87L9 13.14 6 17h12l-3.86-5.14z"/>
                        </svg>
                        <p>No flashcards yet. Add your first card above!</p>
                    </div>
                `;
                return;
            }
            
            cardsContainer.innerHTML = '';
            
            cards.forEach((card, index) => {
                const cardElement = document.createElement('div');
                cardElement.className = 'card-item new-card';
                
                const cardText = document.createElement('div');
                cardText.className = 'card-text';
                cardText.textContent = card.front;
                
                const cardActions = document.createElement('div');
                cardActions.className = 'card-actions';
                
                const viewButton = document.createElement('button');
                viewButton.className = 'btn-secondary';
                viewButton.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" fill="currentColor" viewBox="0 0 16 16">
                        <path d="M10.5 8a2.5 2.5 0 1 1-5 0 2.5 2.5 0 0 1 5 0z"/>
                        <path d="M0 8s3-5.5 8-5.5S16 8 16 8s-3 5.5-8 5.5S0 8 0 8zm8 3.5a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7z"/>
                    </svg>
                `;
                viewButton.onclick = (e) => {
                    e.stopPropagation();
                    showCard(index);
                    // Scroll to the flashcard view
                    document.querySelector('.flashcard-container').scrollIntoView({ behavior: 'smooth' });
                };
                
                const deleteButton = document.createElement('button');
                deleteButton.className = 'btn-danger';
                deleteButton.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" fill="currentColor" viewBox="0 0 16 16">
                        <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
                        <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
                    </svg>
                `;
                deleteButton.onclick = (e) => {
                    e.stopPropagation();
                    deleteCard(index);
                };
                
                cardActions.appendChild(viewButton);
                cardActions.appendChild(deleteButton);
                
                cardElement.appendChild(cardText);
                cardElement.appendChild(cardActions);
                
                cardElement.onclick = () => {
                    showCard(index);
                    // Scroll to the flashcard view
                    document.querySelector('.flashcard-container').scrollIntoView({ behavior: 'smooth' });
                };
                
                cardsContainer.appendChild(cardElement);
                
                // Remove animation class after it's done
                setTimeout(() => {
                    cardElement.classList.remove('new-card');
                }, 400);
            });
        }
        
        // Update the main card display
        function updateCardDisplay() {
            if (cards.length > 0) {
                showCard(currentCardIndex);
            } else {
                frontContentElement.textContent = 'No cards available. Add some flashcards to get started!';
                backContentElement.textContent = '';
                prevButton.disabled = true;
                nextButton.disabled = true;
            }
        }
        
        // Update the total cards count
        function updateTotalCards() {
            totalCardsSpan.textContent = cards.length;
        }
        
        // Initialize the app
        loadCards();
        
        // Add keyboard shortcuts
        document.addEventListener('keydown', function(e) {
            if (e.code === 'Space' || e.code === 'Enter') {
                flipCard();
            } else if (e.code === 'ArrowRight') {
                nextCard();
            } else if (e.code === 'ArrowLeft') {
                prevCard();
            }
        });
    </script>
</body>
</html>
