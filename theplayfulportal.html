<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kids Learning Hub</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- FIREBASE IMPORTS (REQUIRED FOR SCHEDULING) -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, onSnapshot, serverTimestamp, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global variables provided by the environment
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : null;
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        window.firebase = {
            app: null,
            db: null,
            auth: null,
            userId: null,
            getAuth: getAuth,
            signInAnonymously: signInAnonymously,
            signInWithCustomToken: signInWithCustomToken,
            onAuthStateChanged: onAuthStateChanged,
            getFirestore: getFirestore,
            collection: collection,
            addDoc: addDoc,
            onSnapshot: onSnapshot,
            serverTimestamp: serverTimestamp,
            setLogLevel: setLogLevel
        };

        window.userEvents = {}; // Global store for calendar events

        async function initializeFirebase() {
            if (!firebaseConfig) {
                console.error("Firebase config not found. Cannot initialize scheduling.");
                return;
            }
            
            try {
                const firebase = window.firebase;
                firebase.app = initializeApp(firebaseConfig);
                firebase.db = getFirestore(firebase.app);
                firebase.setLogLevel('Debug'); 
                firebase.auth = getAuth(firebase.app);
                
                if (initialAuthToken) {
                    await firebase.signInWithCustomToken(firebase.auth, initialAuthToken);
                } else {
                    await firebase.signInAnonymously(firebase.auth);
                }

                firebase.onAuthStateChanged(firebase.auth, (user) => {
                    if (user) {
                        firebase.userId = user.uid;
                        console.log("Firebase initialized. User ID:", firebase.userId);
                        window.loadEvents(); // Start listening for data once authenticated
                    } else {
                        console.log("User signed out or anonymous.");
                    }
                });

            } catch (error) {
                console.error("Firebase initialization failed:", error);
            }
        }

        function getEventsCollectionRef() {
            const firebase = window.firebase;
            if (!firebase.db || !firebase.userId) {
                console.error("Database or User ID not ready.");
                return null;
            }
            const collectionPath = `/artifacts/${appId}/users/${firebase.userId}/calendar_events`;
            return firebase.collection(firebase.db, collectionPath);
        }

        window.saveEvent = async (event) => {
            const eventsRef = getEventsCollectionRef();
            if (!eventsRef) return;

            try {
                await firebase.addDoc(eventsRef, {
                    title: event.title,
                    date: event.date, // YYYY-MM-DD string
                    emoji: event.emoji,
                    timestamp: firebase.serverTimestamp(),
                });
                console.log("Event saved successfully.");
            } catch (error) {
                console.error("Error saving event:", error);
            }
        };

        window.loadEvents = () => {
            const eventsRef = getEventsCollectionRef();
            if (!eventsRef) return;

            firebase.onSnapshot(eventsRef, (snapshot) => {
                const tempEvents = {};
                snapshot.docs.forEach(doc => {
                    const data = doc.data();
                    const dateKey = data.date; // YYYY-MM-DD
                    
                    if (!tempEvents[dateKey]) {
                        tempEvents[dateKey] = [];
                    }
                    tempEvents[dateKey].push({
                        id: doc.id,
                        ...data
                    });
                });

                window.userEvents = tempEvents;
                console.log("Events loaded:", window.userEvents);
                
                // Re-render the calendar with the new data
                window.renderCalendar(); 
            }, (error) => {
                console.error("Error listening to events:", error);
            });
        };

        // Initialize Firebase when the DOM is ready
        document.addEventListener('DOMContentLoaded', initializeFirebase);
    </script>

    <!-- Configure Inter Font and Custom Colors -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        'kids-blue': '#4F46E5', // Indigo 600
                        'kids-yellow': '#FBBF24', // Amber 400
                        'kids-green': '#10B981', // Emerald 500
                        'kids-red': '#EF4444', // Red 500
                        'kids-bg': '#F3F4F6', // Gray 100
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom styles for fun border and shadows */
        .card {
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            border-bottom: 8px solid var(--card-border-color, #4F46E5);
            transition: all 0.3s ease;
        }
        .nav-link.active {
            background-color: white;
            color: #4F46E5;
            box-shadow: 0 -4px 10px rgba(0, 0, 0, 0.1);
            position: relative;
        }
        /* Hide content sections initially */
        .content-section {
            display: none;
        }
    </style>
</head>
<body class="bg-kids-bg min-h-screen pt-20 font-sans">

    <!-- Navbar/Header (Fixed to Top) -->
    <header class="fixed top-0 left-0 right-0 bg-kids-blue shadow-lg z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex justify-between items-center h-20">
            <!-- Logo/Title -->
            <div class="text-3xl font-extrabold text-kids-yellow tracking-tight cursor-pointer" onclick="showView('home')">
                ✨ Play & Learn Hub
            </div>
            
            <!-- Navigation Links -->
            <nav class="flex space-x-2 sm:space-x-4">
                <button id="nav-home" class="nav-link px-3 py-2 sm:px-4 sm:py-2 text-sm sm:text-lg font-semibold rounded-full text-white hover:bg-kids-yellow hover:text-kids-blue transition active" onclick="showView('home')">
                    Home
                </button>
                <button id="nav-calendar" class="nav-link px-3 py-2 sm:px-4 sm:py-2 text-sm sm:text-lg font-semibold rounded-full text-white hover:bg-kids-yellow hover:text-kids-blue transition" onclick="showView('calendar')">
                    Calendar
                </button>
                <button id="nav-dictionary" class="nav-link px-3 py-2 sm:px-4 sm:py-2 text-sm sm:text-lg font-semibold rounded-full text-white hover:bg-kids-yellow hover:text-kids-blue transition" onclick="showView('dictionary')">
                    Dictionary
                </button>
                <button id="nav-quiz" class="nav-link px-3 py-2 sm:px-4 sm:py-2 text-sm sm:text-lg font-semibold rounded-full text-white hover:bg-kids-yellow hover:text-kids-blue transition" onclick="showView('quiz')">
                    Quiz Game
                </button>
            </nav>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- 1. Home Section -->
        <section id="home-section" class="content-section" data-border-color="#4F46E5">
            <div class="card bg-white p-8 rounded-2xl text-center" style="--card-border-color: #4F46E5;">
                <h1 class="text-5xl font-extrabold text-kids-blue mb-4">Welcome, Awesome Learner! 🎉</h1>
                <p class="text-xl text-gray-700 max-w-3xl mx-auto">
                    This is your special place to explore, discover new words, and test your knowledge with fun games. Click a tab above to get started!
                </p>
                <div class="mt-8 flex justify-center space-x-4">
                    <button class="bg-kids-green text-white text-xl font-bold py-3 px-6 rounded-xl shadow-lg hover:bg-green-600 transition" onclick="showView('dictionary')">
                        📚 Find a Word
                    </button>
                    <button class="bg-kids-red text-white text-xl font-bold py-3 px-6 rounded-xl shadow-lg hover:bg-red-600 transition" onclick="showView('quiz')">
                        🎮 Start Quiz
                    </button>
                </div>
            </div>
        </section>

        <!-- 2. Calendar Section -->
        <section id="calendar-section" class="content-section" data-border-color="#10B981">
            <div class="card bg-white p-6 sm:p-8 rounded-2xl" style="--card-border-color: #10B981;">
                <h2 class="text-4xl font-extrabold text-kids-green mb-6 text-center">Calendar Fun! 📅</h2>
                <div class="flex justify-between items-center mb-4">
                    <button id="prevMonth" class="bg-gray-200 p-2 rounded-full text-gray-700 hover:bg-gray-300 transition">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path></svg>
                    </button>
                    <h3 id="currentMonthYear" class="text-2xl font-bold text-gray-800"></h3>
                    <button id="nextMonth" class="bg-gray-200 p-2 rounded-full text-gray-700 hover:bg-gray-300 transition">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
                    </button>
                </div>

                <div class="grid grid-cols-7 gap-1 sm:gap-2 text-center text-sm sm:text-base font-medium text-gray-500 mb-2">
                    <div>Sun</div><div>Mon</div><div>Tue</div><div>Wed</div><div>Thu</div><div>Fri</div><div>Sat</div>
                </div>
                
                <div id="calendarGrid" class="grid grid-cols-7 gap-1 sm:gap-2">
                    <!-- Calendar cells will be injected here -->
                </div>
            </div>
        </section>
        
        <!-- Event Modal (Hidden by Default) -->
        <div id="event-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-[100] flex items-center justify-center p-4">
            <div class="bg-white p-6 rounded-2xl shadow-2xl max-w-md w-full border-b-8 border-kids-green">
                <div class="flex justify-between items-center mb-4 border-b pb-2">
                    <h3 class="text-2xl font-bold text-kids-green">Schedule for <span id="modal-date-display"></span></h3>
                    <button class="text-gray-500 hover:text-gray-800" onclick="closeModal()">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
                    </button>
                </div>

                <!-- Existing Events List -->
                <div id="existing-events" class="mb-4 space-y-2 max-h-40 overflow-y-auto p-2 bg-gray-50 rounded-lg">
                    <p class="text-gray-500 text-center text-sm" id="no-events-message">No plans yet for this day! Add one below.</p>
                </div>
                
                <h4 class="text-lg font-semibold text-gray-700 mt-6 mb-3 border-t pt-3">Add New Plan ✏️</h4>
                <form id="event-form">
                    <div class="mb-3">
                        <label class="block text-sm font-medium text-gray-700 mb-1" for="event-title-input">What is the plan?</label>
                        <input type="text" id="event-title-input" required maxlength="50" placeholder="e.g., Soccer Practice, Read a book" class="w-full p-2 border border-gray-300 rounded-lg focus:border-kids-green">
                    </div>

                    <div class="mb-4">
                        <label class="block text-sm font-medium text-gray-700 mb-2">Pick an Emoji/Sticker</label>
                        <div id="emoji-picker" class="flex flex-wrap gap-2 text-2xl p-2 bg-kids-bg rounded-lg">
                            <!-- Emojis populated by JS -->
                        </div>
                        <input type="hidden" id="event-date-input" required>
                        <input type="hidden" id="event-emoji-input" required>
                    </div>

                    <button type="submit" class="w-full bg-kids-green text-white font-bold py-3 rounded-xl shadow-lg hover:bg-green-600 transition">
                        Save Schedule Item
                    </button>
                </form>
            </div>
        </div>

        <!-- 3. Dictionary Section -->
        <section id="dictionary-section" class="content-section" data-border-color="#FBBF24">
            <div class="card bg-white p-6 sm:p-8 rounded-2xl" style="--card-border-color: #FBBF24;">
                <h2 class="text-4xl font-extrabold text-kids-yellow mb-6 text-center">Kid's Awesome Dictionary 📚</h2>
                
                <!-- NEW: Search Input -->
                <div class="mb-6">
                    <input type="text" id="dictionary-search-input" placeholder="Search for a word or definition..." 
                           class="w-full p-3 border-2 border-kids-yellow rounded-xl focus:outline-none focus:ring-2 focus:ring-kids-yellow/50 transition text-lg">
                </div>
                
                <!-- Alphabet Navigation -->
                <div id="alphabet-nav" class="flex flex-wrap justify-center gap-1 sm:gap-2 mb-6">
                    <!-- Buttons A-Z generated by JS -->
                </div>

                <!-- Word List -->
                <div id="word-list-container" class="space-y-4">
                    <p id="word-list-placeholder" class="text-center text-lg text-gray-500">
                        Select a letter above to see the list of cool words!
                    </p>
                    <!-- Words will be injected here -->
                </div>
            </div>
        </section>

        <!-- 4. Quiz Game Section -->
        <section id="quiz-section" class="content-section" data-border-color="#EF4444">
            <div class="card bg-white p-6 sm:p-8 rounded-2xl" style="--card-border-color: #EF4444;">
                <h2 class="text-4xl font-extrabold text-kids-red mb-6 text-center">The Brainy Quiz Game! 🧠</h2>
                
                <div id="quiz-start" class="text-center">
                    <p class="text-xl text-gray-700 mb-6">Ready to test your smarts? Match the word to its correct definition!</p>
                    <button id="start-quiz-btn" class="bg-kids-red text-white text-2xl font-bold py-4 px-8 rounded-xl shadow-lg hover:bg-red-600 transition">
                        Start Quiz! 🚀
                    </button>
                </div>

                <div id="quiz-game" class="hidden">
                    <p class="text-lg text-kids-blue font-semibold mb-2">Question <span id="current-question-num">1</span> of <span id="total-questions">5</span></p>
                    <div class="bg-kids-blue text-white p-6 rounded-xl mb-6 shadow-md">
                        <p id="question-text" class="text-2xl font-bold text-center"></p>
                    </div>

                    <div id="answer-options" class="space-y-3">
                        <!-- Answer buttons will be injected here -->
                    </div>

                    <p id="quiz-feedback" class="mt-4 text-center font-bold text-lg"></p>
                    <div class="flex justify-center mt-6">
                        <button id="next-question-btn" class="hidden bg-kids-green text-white font-bold py-3 px-6 rounded-xl shadow-md hover:bg-green-600 transition">
                            Next Question
                        </button>
                    </div>
                </div>

                <div id="quiz-results" class="hidden text-center">
                    <h3 class="text-3xl font-extrabold text-kids-blue mb-4">Quiz Finished! 🎉</h3>
                    <p id="final-score" class="text-5xl font-extrabold text-kids-green mb-6"></p>
                    <button class="bg-kids-blue text-white font-bold py-3 px-6 rounded-xl shadow-md hover:bg-indigo-600 transition" onclick="document.getElementById('start-quiz-btn').click();">
                        Play Again!
                    </button>
                </div>
            </div>
        </section>

    </main>

    <script>
        // --- Global State Management ---
        let currentView = 'home';
        const sections = ['home', 'calendar', 'dictionary', 'quiz'];

        function showView(viewId) {
            currentView = viewId;
            sections.forEach(id => {
                const section = document.getElementById(`${id}-section`);
                const navBtn = document.getElementById(`nav-${id}`);
                
                if (id === viewId) {
                    section.style.display = 'block';
                    navBtn.classList.add('active');
                } else {
                    section.style.display = 'none';
                    navBtn.classList.remove('active');
                }
            });
            // Run specific initialization functions when switching views
            if (viewId === 'calendar') {
                window.renderCalendar(); // Call globally defined renderCalendar
            } else if (viewId === 'dictionary') {
                renderAlphabetNav();
                // When showing the dictionary, we reset the search bar and show words for the active letter
                document.getElementById('dictionary-search-input').value = '';
                showWords(activeLetter, ''); 
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            showView('home');
            renderEmojiPicker(); // Initialize emoji selection
            setupEventForm();     // Setup form submission
            
            // NEW: Dictionary Search Listener
            document.getElementById('dictionary-search-input').addEventListener('input', (e) => {
                // When searching, we filter words for the currently active letter based on the input value
                const searchTerm = e.target.value;
                showWords(activeLetter, searchTerm);
            });
        });


        // ----------------------------------------------------------------------
        // --- 1. Calendar Logic (Updated for Scheduling) ---
        // ----------------------------------------------------------------------

        let currentDate = new Date();
        const calendarGrid = document.getElementById('calendarGrid');
        const currentMonthYear = document.getElementById('currentMonthYear');
        const prevMonthBtn = document.getElementById('prevMonth');
        const nextMonthBtn = document.getElementById('nextMonth');

        const monthNames = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];

        window.renderCalendar = function() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth();

            currentMonthYear.textContent = `${monthNames[month]} ${year}`;
            calendarGrid.innerHTML = ''; // Clear previous grid

            // 1. Get the first day of the month and the number of days
            const firstDayOfMonth = new Date(year, month, 1).getDay(); // 0 (Sun) to 6 (Sat)
            const daysInMonth = new Date(year, month + 1, 0).getDate();

            // 2. Add empty cells for preceding days
            for (let i = 0; i < firstDayOfMonth; i++) {
                calendarGrid.innerHTML += '<div class="p-2 sm:p-3"></div>';
            }

            // 3. Add day cells
            const today = new Date();
            const isCurrentMonth = today.getFullYear() === year && today.getMonth() === month;

            for (let day = 1; day <= daysInMonth; day++) {
                const dayString = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                const hasEvents = window.userEvents[dayString] && window.userEvents[dayString].length > 0;
                
                let cellClasses = "p-2 sm:p-3 rounded-xl cursor-pointer text-gray-800 font-bold transition duration-150 transform hover:scale-105 relative min-h-[5rem]";
                
                if (isCurrentMonth && day === today.getDate()) {
                    cellClasses += " bg-kids-yellow text-white shadow-lg border-2 border-kids-blue"; // Today's date
                } else {
                    cellClasses += " bg-gray-100 hover:bg-gray-200";
                }

                let eventMarkers = '';
                if (hasEvents) {
                    // Show up to 3 emojis
                    const eventCount = window.userEvents[dayString].length;
                    const emojis = window.userEvents[dayString].slice(0, 3).map(e => e.emoji).join('');
                    eventMarkers = `
                        <div class="text-xs absolute bottom-1 left-0 right-0 p-1 bg-white/70 backdrop-blur-sm rounded-b-xl text-center">
                            ${emojis}
                            ${eventCount > 3 ? `<span class="text-gray-500 ml-1">+${eventCount - 3}</span>` : ''}
                        </div>`;
                    
                    if (isCurrentMonth && day === today.getDate()) {
                        cellClasses = cellClasses.replace('text-white', 'text-gray-800'); // Ensure day number is visible over background
                    }
                }

                calendarGrid.innerHTML += `
                    <div class="${cellClasses} text-center" 
                        data-date="${dayString}" 
                        onclick="openEventModal('${dayString}')">
                        <div class="text-lg">${day}</div>
                        ${eventMarkers}
                    </div>`;
            }
        }

        prevMonthBtn.addEventListener('click', () => {
            currentDate.setMonth(currentDate.getMonth() - 1);
            window.renderCalendar();
        });

        nextMonthBtn.addEventListener('click', () => {
            currentDate.setMonth(currentDate.getMonth() + 1);
            window.renderCalendar();
        });
        
        // --- Modal Functions ---
        const eventModal = document.getElementById('event-modal');
        const modalDateDisplay = document.getElementById('modal-date-display');
        const eventDateInput = document.getElementById('event-date-input');
        const existingEventsContainer = document.getElementById('existing-events');

        window.openEventModal = (dateString) => {
            modalDateDisplay.textContent = dateString;
            eventDateInput.value = dateString;
            eventModal.classList.remove('hidden');

            const events = window.userEvents[dateString] || [];
            existingEventsContainer.innerHTML = '';
            
            if (events.length === 0) {
                existingEventsContainer.innerHTML = `<p class="text-gray-500 text-center text-sm p-2" id="no-events-message">No plans yet for this day! Add one below.</p>`;
            } else {
                events.forEach(event => {
                    const eventItem = document.createElement('div');
                    eventItem.className = 'flex items-center p-2 bg-white rounded-lg shadow-sm border-l-4 border-kids-green';
                    eventItem.innerHTML = `
                        <span class="text-2xl mr-3">${event.emoji}</span>
                        <span class="text-gray-800 font-medium">${event.title}</span>
                    `;
                    existingEventsContainer.appendChild(eventItem);
                });
            }
        };

        window.closeModal = () => {
            eventModal.classList.add('hidden');
            // Reset form
            document.getElementById('event-title-input').value = '';
            document.getElementById('event-emoji-input').value = '';
            // Reset emoji highlight
            document.querySelectorAll('#emoji-picker button').forEach(btn => btn.classList.remove('bg-kids-green/50', 'ring-2', 'ring-kids-green'));
        };

        const availableEmojis = ['📚', '⚽', '🎨', '🎂', '🦷', '🧺', '🐕', '🎉', '🚌', '🍜'];
        function renderEmojiPicker() {
            const picker = document.getElementById('emoji-picker');
            picker.innerHTML = '';
            availableEmojis.forEach(emoji => {
                const btn = document.createElement('button');
                btn.type = 'button';
                btn.textContent = emoji;
                btn.className = 'p-1 rounded-lg hover:bg-kids-yellow/50 transition';
                btn.onclick = () => selectEmoji(emoji, btn);
                picker.appendChild(btn);
            });
        }

        function selectEmoji(emoji, selectedButton) {
            document.getElementById('event-emoji-input').value = emoji;
            document.querySelectorAll('#emoji-picker button').forEach(btn => btn.classList.remove('bg-kids-green/50', 'ring-2', 'ring-kids-green'));
            selectedButton.classList.add('bg-kids-green/50', 'ring-2', 'ring-kids-green');
        }

        function setupEventForm() {
            document.getElementById('event-form').addEventListener('submit', async (e) => {
                e.preventDefault();
                
                const title = document.getElementById('event-title-input').value;
                const date = document.getElementById('event-date-input').value;
                const emoji = document.getElementById('event-emoji-input').value;

                if (!title || !date || !emoji) {
                    console.error("Missing event details.");
                    return;
                }

                await window.saveEvent({ title, date, emoji });
                
                closeModal();
            });
        }


        // ----------------------------------------------------------------------
        // --- 2. Dictionary Logic ---
        // ----------------------------------------------------------------------

        // Mock data structure: Simulating 100 words per letter (2600 total)
        const dictionaryData = {
            'A': [
  { "word": "A", "definition": "The word we use before one thing or person." },
  { "word": "Apple", "definition": "A round fruit that grows on trees and is often red or green." },
  { "word": "Ant", "definition": "A very small insect that lives in large groups." },
  { "word": "Astronaut", "definition": "A person trained to travel in a spacecraft." },
  { "word": "Alligator", "definition": "A large reptile with a strong jaw and sharp teeth." },
  { "word": "Airplane", "definition": "A vehicle with wings that flies through the air." },
  { "word": "Award", "definition": "A prize you get for doing something well." },
  { "word": "Amazing", "definition": "Something that is surprising and very wonderful." },
  { "word": "Ask", "definition": "To say you want an answer or information." },
  { "word": "Art", "definition": "Things you create, like drawings, paintings, or sculptures." },
  { "word": "Adventure", "definition": "An exciting or unusual journey or experience." },
  { "word": "Add", "definition": "To put things together to find the total." },
  { "word": "Age", "definition": "How old a person or thing is." },
  { "word": "Air", "definition": "The invisible gas all around us that we breathe." },
  { "word": "Aim", "definition": "To point or try to hit a target." },
  { "word": "Alphabet", "definition": "All the letters used in a language, from A to Z." },
  { "word": "An", "definition": "The word we use before one word that starts with a vowel sound (like 'an orange')." },
  { "word": "And", "definition": "A word that joins things together (like 'milk and cookies')." },
  { "word": "Arm", "definition": "The part of your body from your shoulder to your hand." },
  { "word": "At", "definition": "Shows where something is (like 'at the park')." },
  { "word": "Aunt", "definition": "Your parent's sister." },
  { "word": "Away", "definition": "To another place; not here." },
  { "word": "Act", "definition": "To do something, or pretend to be someone else." },
  { "word": "All", "definition": "Every single one." },
  { "word": "Any", "definition": "One of some things; it doesn't matter which." },
  { "word": "Animal", "definition": "A living creature that is not a plant." },
  { "word": "Arrow", "definition": "A pointed sign or shaft that shows direction." },
  { "word": "Ash", "definition": "The soft, gray powder left after something burns." },
  { "word": "Afraid", "definition": "Feeling scared or fearful." },
  { "word": "Awesome", "definition": "Super cool or extremely impressive." },
  { "word": "Across", "definition": "To the other side of something." },
  { "word": "After", "definition": "Happening later than something else." },
  { "word": "Agree", "definition": "To have the same idea or say 'yes'." },
  { "word": "Alive", "definition": "Living; not dead." },
  { "word": "Along", "definition": "Moving forward in a line next to something." },
  { "word": "Also", "definition": "Too, or in addition." },
  { "word": "Always", "definition": "Every time; forever." },
  { "word": "Angry", "definition": "A strong feeling of being very mad." },
  { "word": "Answer", "definition": "To reply to a question." },
  { "word": "Ape", "definition": "A large kind of monkey without a tail." },
  { "word": "April", "definition": "The fourth month of the year." },
  { "word": "Area", "definition": "A certain space or part of a place." },
  { "word": "Arrive", "definition": "To get to a place." },
  { "word": "Attack", "definition": "To try to hurt or capture someone or something." },
  { "word": "Awake", "definition": "Not sleeping." },
  { "word": "Awful", "definition": "Something very bad or unpleasant." },
  { "word": "Album", "definition": "A book for holding photos or a collection of songs." },
  { "word": "Alarm", "definition": "A loud sound or signal to warn you." },
  { "word": "Alien", "definition": "A creature from another planet." },
  { "word": "Ambulance", "definition": "A special vehicle that takes sick or hurt people to the hospital." },
  { "word": "Arc", "definition": "A smooth, curved line." },
  { "word": "Arcade", "definition": "A place filled with video games and fun machines." },
  { "word": "Artist", "definition": "A person who creates art." },
  { "word": "Able", "definition": "To be capable of doing something." },
  { "word": "About", "definition": "On the topic of, or nearly." },
  { "word": "Above", "definition": "At a higher place." },
  { "word": "Acorn", "definition": "The small nut that grows on an oak tree." },
  { "word": "Active", "definition": "Full of energy and moving around a lot." },
  { "word": "Adult", "definition": "Someone who is fully grown up." },
  { "word": "Ago", "definition": "Before now, or in the past." },
  { "word": "Agreeable", "definition": "Pleasant or easy to get along with." },
  { "word": "Ahead", "definition": "In front or in the future." },
  { "word": "Aid", "definition": "To help or assist someone." },
  { "word": "Alike", "definition": "Having many things that are the same." },
  { "word": "Almost", "definition": "Very nearly, but not quite." },
  { "word": "Alone", "definition": "By yourself, with no one else." },
  { "word": "Amount", "definition": "How much of something there is." },
  { "word": "Amuse", "definition": "To entertain or make someone smile or laugh." },
  { "word": "Ancient", "definition": "Something that is very, very old." },
  { "word": "Animal", "definition": "A living creature, like a dog or a bird." },
  { "word": "Announce", "definition": "To say something loudly for everyone to hear." },
  { "word": "Antlers", "definition": "The big horns that grow on the head of a deer." },
  { "word": "Applaud", "definition": "To clap your hands to show you like something." },
  { "word": "Apply", "definition": "To put something onto a surface, like glue or paint." },
  { "word": "Aquarium", "definition": "A glass tank for fish and other sea creatures." },
  { "word": "Argue", "definition": "To disagree with words, sometimes loudly." },
  { "word": "Around", "definition": "On every side, or close by." },
  { "word": "Assemble", "definition": "To put pieces together to build something." },
  { "word": "Assist", "definition": "To help someone with a task." },
  { "word": "Athletic", "definition": "Good at sports and physical activities." },
  { "word": "Attic", "definition": "The room right under the roof of a house." },
  { "word": "Audience", "definition": "The group of people watching a show or event." },
  { "word": "Author", "definition": "A person who writes books." },
  { "word": "Auto", "definition": "A short word for 'automobile' or car." },
  { "word": "Avoid", "definition": "To keep away from something." },
  { "word": "Awaken", "definition": "To wake up." },
  { "word": "Ax", "definition": "A tool with a long handle and a sharp blade for chopping wood." },
  { "word": "Accurate", "definition": "Exactly correct; no mistakes." },
  { "word": "Achieve", "definition": "To successfully reach a goal after hard work." },
  { "word": "Acquire", "definition": "To get or gain something." },
  { "word": "Adorable", "definition": "Very cute and easy to love." },
  { "word": "Advise", "definition": "To offer an idea or suggestion to help someone." },
  { "word": "Aloud", "definition": "To say something so others can hear it." },
  { "word": "Ambition", "definition": "A strong wish to do or achieve something big." },
  { "word": "Ancestor", "definition": "A family member who lived a very long time ago." },
  { "word": "Anger", "definition": "The feeling of being very mad." },
  { "word": "Annual", "definition": "Happening once every year." },
  { "word": "Approve", "definition": "To say something is good or okay." },
  { "word": "Arrest", "definition": "When the police catch and hold someone." },
  { "word": "Attract", "definition": "To make something come closer or be interested." }
            ],
            'B': [
                { "word": "Baby", "definition": "A very young child or animal." },
  { "word": "Ball", "definition": "A round object used for playing games." },
  { "word": "Bag", "definition": "A container used to hold and carry things." },
  { "word": "Bed", "definition": "A piece of furniture used for sleeping." },
  { "word": "Bee", "definition": "A yellow and black flying insect that makes honey." },
  { "word": "Big", "definition": "Large in size or importance." },
  { "word": "Bird", "definition": "An animal with wings and feathers that can fly." },
  { "word": "Blue", "definition": "The color of the sky on a sunny day." },
  { "word": "Boat", "definition": "A small vehicle used for traveling on water." },
  { "word": "Book", "definition": "A set of pages with words and pictures that are bound together." },
  { "word": "Box", "definition": "A container, usually square, for keeping things." },
  { "word": "Boy", "definition": "A young male person." },
  { "word": "Brush", "definition": "A tool with stiff hairs used for cleaning or painting." },
  { "word": "Bus", "definition": "A large vehicle that carries many people." },
  { "word": "Buy", "definition": "To get something by paying money for it." },
  { "word": "By", "definition": "Close to, or near something." },
  { "word": "Bad", "definition": "Not good, or causing trouble." },
  { "word": "Bake", "definition": "To cook food in an oven, like a cake or cookies." },
  { "word": "Balloon", "definition": "A rubber bag filled with air or gas that floats." },
  { "word": "Banana", "definition": "A long, curved yellow fruit." },
  { "word": "Band", "definition": "A group of people who play music together." },
  { "word": "Bank", "definition": "A place where people keep their money." },
  { "word": "Bark", "definition": "The sound a dog makes, or the outer skin of a tree." },
  { "word": "Barn", "definition": "A large building on a farm for keeping animals or crops." },
  { "word": "Basket", "definition": "A container woven from thin materials." },
  { "word": "Bath", "definition": "Washing your body while sitting in a tub of water." },
  { "word": "Bat", "definition": "A flying mammal that comes out at night, or a wooden stick used in baseball." },
  { "word": "Bay", "definition": "A large area of water partly surrounded by land." },
  { "word": "Be", "definition": "To exist or to happen (like 'I will be happy')." },
  { "word": "Beach", "definition": "A sandy or stony shore next to a sea or lake." },
  { "word": "Bear", "definition": "A large, furry, wild animal." },
  { "word": "Beat", "definition": "To hit something many times, or to win a game." },
  { "word": "Beautiful", "definition": "Something that is very pleasing to look at." },
  { "word": "Become", "definition": "To grow to be something." },
  { "word": "Before", "definition": "Earlier than or in front of something else." },
  { "word": "Begin", "definition": "To start doing something." },
  { "word": "Behind", "definition": "At the back of someone or something." },
  { "word": "Bell", "definition": "A metal cup-shaped device that makes a ringing sound." },
  { "word": "Belt", "definition": "A strip of cloth or leather worn around the waist." },
  { "word": "Bench", "definition": "A long seat for several people." },
  { "word": "Bend", "definition": "To curve or make something crooked." },
  { "word": "Berry", "definition": "A small, round, sweet fruit." },
  { "word": "Best", "definition": "Better than all the others." },
  { "word": "Between", "definition": "In the middle of two things." },
  { "word": "Bib", "definition": "A cloth tied around a baby's neck to keep clothes clean." },
  { "word": "Bicycle", "definition": "A vehicle with two wheels that you pedal." },
  { "word": "Bite", "definition": "To cut or grip with your teeth." },
  { "word": "Black", "definition": "The darkest color, like the color of the night sky." },
  { "word": "Blanket", "definition": "A warm cover used on a bed." },
  { "word": "Blast", "definition": "A sudden loud noise or explosion." },
  { "word": "Block", "definition": "A solid piece of wood or stone, or a toy used for building." },
  { "word": "Bloom", "definition": "When a flower opens up." },
  { "word": "Blow", "definition": "To push air out of your mouth." },
  { "word": "Bone", "definition": "The hard, white parts inside a body." },
  { "word": "Borrow", "definition": "To take something for a short time and promise to give it back." },
  { "word": "Both", "definition": "The two things together." },
  { "word": "Bottle", "definition": "A container for liquids with a narrow neck." },
  { "word": "Bottom", "definition": "The lowest part of something." },
  { "word": "Bounce", "definition": "To spring back after hitting a surface." },
  { "word": "Bowl", "definition": "A round, deep dish for food." },
  { "word": "Brain", "definition": "The organ inside your head that controls your body." },
  { "word": "Branch", "definition": "A part of a tree that grows out from the trunk." },
  { "word": "Brave", "definition": "Ready to face danger or fear; courageous." },
  { "word": "Bread", "definition": "A food made from baked flour and water." },
  { "word": "Break", "definition": "To snap or split something into pieces." },
  { "word": "Breeze", "definition": "A gentle, light wind." },
  { "word": "Bridge", "definition": "A structure built to cross over water or a road." },
  { "word": "Bright", "definition": "Full of light, or smart." },
  { "word": "Bring", "definition": "To carry or take something with you." },
  { "word": "Brother", "definition": "A male sibling." },
  { "word": "Brown", "definition": "A color like dirt or chocolate." },
  { "word": "Bubble", "definition": "A thin layer of liquid filled with air, usually in a sphere." },
  { "word": "Bucket", "definition": "A round, open container with a handle for carrying liquids." },
  { "word": "Bud", "definition": "A small knob on a plant that grows into a flower or leaf." },
  { "word": "Build", "definition": "To make or construct something, like a house or tower." },
  { "word": "Bulb", "definition": "A glass sphere that produces light (like a light bulb)." },
  { "word": "Bump", "definition": "A light blow or hit, or a raised lump." },
  { "word": "Bunny", "definition": "A cute, common name for a rabbit." },
  { "word": "Burn", "definition": "To be damaged by fire or heat." },
  { "word": "Bush", "definition": "A thick, short plant with many branches." },
  { "word": "Busy", "definition": "Working or having a lot to do." },
  { "word": "Button", "definition": "A small round piece used to fasten clothes." },
  { "word": "Buzz", "definition": "The humming sound a bee makes." },
  { "word": "Back", "definition": "The rear part of your body or an object." },
  { "word": "Borrow", "definition": "To use something that belongs to someone else for a while." },
  { "word": "Bother", "definition": "To annoy or worry someone." },
  { "word": "Branch", "definition": "A large part of a tree growing out from the trunk." },
  { "word": "Brick", "definition": "A block of baked clay used for building walls." },
  { "word": "Bully", "definition": "A person who hurts or frightens weaker people." },
  { "word": "Burrow", "definition": "A hole in the ground dug by an animal like a rabbit." },
  { "word": "Buyer", "definition": "A person who purchases something." },
  { "word": "Balance", "definition": "To keep steady and not fall over." },
  { "word": "Blaze", "definition": "A very large or fierce fire." },
  { "word": "Blizzard", "definition": "A severe storm with a lot of snow and wind." },
  { "word": "Blossom", "definition": "A flower or cluster of flowers on a tree." },
  { "word": "Bound", "definition": "Tied up, or jumping/leaping." },
  { "word": "Bulky", "definition": "Taking up a lot of space; large and awkward." },
  { "word": "Brilliant", "definition": "Very bright, or very smart." },
  { "word": "Bless", "definition": "To ask for favor and protection for someone." }
            ],
            'C': [
                { "word": "Cabbage", "definition": "A large, round vegetable with green or purple leaves." },
  { "word": "Cage", "definition": "A box made of wire or bars to hold an animal." },
  { "word": "Cake", "definition": "A sweet baked treat, often served for birthdays." },
  { "word": "Call", "definition": "To shout or speak loudly; to contact by phone." },
  { "word": "Calm", "definition": "Quiet, peaceful, and not excited." },
  { "word": "Camp", "definition": "To live outside in a tent for a short time." },
  { "word": "Can", "definition": "To be able to do something, or a metal container." },
  { "word": "Candy", "definition": "A sweet food or treat." },
  { "word": "Car", "definition": "A vehicle with an engine that has four wheels." },
  { "word": "Card", "definition": "A small, thick piece of paper used for games or messages." },
  { "word": "Care", "definition": "To look after someone or something." },
  { "word": "Carry", "definition": "To hold and move something from one place to another." },
  { "word": "Cat", "definition": "A small, furry pet that meows." },
  { "word": "Catch", "definition": "To grab something that is moving or falling." },
  { "word": "Cave", "definition": "A large hole in the side of a cliff or hill." },
  { "word": "Cell", "definition": "The smallest unit of a living thing, or a small room." },
  { "word": "Chair", "definition": "A seat for one person, usually with four legs and a back." },
  { "word": "Change", "definition": "To make or become different." },
  { "word": "Chant", "definition": "To repeat a word or phrase over and over." },
  { "word": "Charge", "definition": "To ask for payment, or to rush forward." },
  { "word": "Cheap", "definition": "Not costing much money." },
  { "word": "Cheer", "definition": "To shout happily to show approval or support." },
  { "word": "Check", "definition": "To look closely to make sure something is correct." },
  { "word": "Cheek", "definition": "The soft part of your face below your eye." },
  { "word": "Cheese", "definition": "A food made from milk." },
  { "word": "Chef", "definition": "A skilled cook, especially in a restaurant." },
  { "word": "Child", "definition": "A young person who is not yet an adult." },
  { "word": "Chill", "definition": "To feel slightly cold." },
  { "word": "China", "definition": "A country in Asia, or fine dishes and cups." },
  { "word": "Chirp", "definition": "The short, sharp sound a small bird makes." },
  { "word": "Chocolate", "definition": "A sweet brown food made from cocoa beans." },
  { "word": "Chop", "definition": "To cut something into small pieces." },
  { "word": "Circle", "definition": "A perfectly round shape." },
  { "word": "City", "definition": "A large town where many people live and work." },
  { "word": "Claim", "definition": "To say that something belongs to you." },
  { "word": "Clap", "definition": "To hit your hands together to make a sound." },
  { "word": "Clean", "definition": "Free from dirt or mess." },
  { "word": "Clear", "definition": "Easy to see through or easy to understand." },
  { "word": "Climb", "definition": "To go up or over something using your hands and feet." },
  { "word": "Clock", "definition": "A device that tells the time." },
  { "word": "Close", "definition": "To shut something, or to be near to something." },
  { "word": "Cloth", "definition": "Material made by weaving fibers, like fabric." },
  { "word": "Cloud", "definition": "A white or gray mass floating in the sky." },
  { "word": "Clown", "definition": "A performer with a painted face and funny clothes." },
  { "word": "Coast", "definition": "The land next to the sea." },
  { "word": "Coat", "definition": "A piece of clothing worn over others for warmth." },
  { "word": "Coin", "definition": "A small, flat piece of metal used as money." },
  { "word": "Cold", "definition": "Having a low temperature; not warm." },
  { "word": "Color", "definition": "The way light looks, like red, blue, or yellow." },
  { "word": "Come", "definition": "To move toward a person or place." },
  { "word": "Comfort", "definition": "To make someone feel better when they are upset." },
  { "word": "Common", "definition": "Happening often or shared by many people." },
  { "word": "Cookie", "definition": "A small, flat, sweet biscuit." },
  { "word": "Cool", "definition": "Slightly cold, or very stylish and interesting." },
  { "word": "Copy", "definition": "To make an exact duplicate of something." },
  { "word": "Corn", "definition": "A tall plant that grows yellow kernels that we eat." },
  { "word": "Cost", "definition": "The amount of money needed to buy something." },
  { "word": "Couch", "definition": "A long, soft seat for several people; a sofa." },
  { "word": "Count", "definition": "To name numbers in order." },
  { "word": "Country", "definition": "A nation with its own government, or the opposite of a city." },
  { "word": "Court", "definition": "An area marked out for playing a sport." },
  { "word": "Cover", "definition": "To place something over or on top of something else." },
  { "word": "Cow", "definition": "A large farm animal kept for its milk or meat." },
  { "word": "Crack", "definition": "To break without coming completely apart." },
  { "word": "Crawl", "definition": "To move slowly on your hands and knees." },
  { "word": "Crazy", "definition": "Silly, confused, or not sensible." },
  { "word": "Cream", "definition": "The thick, fatty part of milk." },
  { "word": "Create", "definition": "To make something new." },
  { "word": "Creep", "definition": "To move slowly and quietly." },
  { "word": "Crew", "definition": "A team of people who work together." },
  { "word": "Cry", "definition": "To shed tears because you are sad or hurt." },
  { "word": "Cube", "definition": "A solid object with six equal square sides." },
  { "word": "Cuddle", "definition": "To hold someone close in a loving way." },
  { "word": "Cup", "definition": "A small container with a handle for drinking." },
  { "word": "Cure", "definition": "To make a sick person well again." },
  { "word": "Curl", "definition": "To twist into a rounded or spiral shape." },
  { "word": "Curve", "definition": "A smooth, continuous bend." },
  { "word": "Custom", "definition": "A way of doing things that is typical for a group of people." },
  { "word": "Cut", "definition": "To divide something using a sharp tool." },
  { "word": "Cute", "definition": "Pleasing and charming in a sweet way." },
  { "word": "Cycle", "definition": "A series of events that repeat in the same order." },
  { "word": "Cabin", "definition": "A small, simple house made of wood." },
  { "word": "Canvas", "definition": "A strong, heavy cloth used for painting or tents." },
  { "word": "Capital", "definition": "The most important city in a country, or a large letter." },
  { "word": "Captain", "definition": "The leader of a ship or a team." },
  { "word": "Castle", "definition": "A large, strong building with thick walls, built long ago." },
  { "word": "Celebration", "definition": "A party or event to mark a special occasion." },
  { "word": "Cereal", "definition": "A breakfast food made from grains." },
  { "word": "Charm", "definition": "A special quality that makes someone liked." },
  { "word": "Chorus", "definition": "A group of people singing together." },
  { "word": "Clue", "definition": "A piece of information that helps solve a problem." },
  { "word": "Compass", "definition": "A tool that shows directions (north, south, east, west)." }
            ],
            'D': [
            { "word": "Dad", "definition": "A common name for a father." },
  { "word": "Dance", "definition": "To move your body to the rhythm of music." },
  { "word": "Danger", "definition": "Something that could cause harm or injury." },
  { "word": "Dark", "definition": "Having little or no light; the opposite of bright." },
  { "word": "Dash", "definition": "To run or move very quickly for a short distance." },
  { "word": "Date", "definition": "A specific day, month, and year." },
  { "word": "Day", "definition": "The time when the sun is up, or a 24-hour period." },
  { "word": "Dead", "definition": "No longer alive." },
  { "word": "Deal", "definition": "An agreement or a bargain." },
  { "word": "Dear", "definition": "Loved or valued a lot." },
  { "word": "Death", "definition": "The end of life." },
  { "word": "Decide", "definition": "To make a choice after thinking about it." },
  { "word": "Deep", "definition": "Going far down from the top or surface." },
  { "word": "Deer", "definition": "A wild animal with long legs, often having antlers." },
  { "word": "Defend", "definition": "To protect someone or something from harm." },
  { "word": "Delay", "definition": "To make something happen later." },
  { "word": "Den", "definition": "A wild animal's home, or a cozy room in a house." },
  { "word": "Deny", "definition": "To say that something is not true." },
  { "word": "Depend", "definition": "To rely on someone or something." },
  { "word": "Desk", "definition": "A piece of furniture with a flat top, used for working or writing." },
  { "word": "Detail", "definition": "A small, specific piece of information." },
  { "word": "Devil", "definition": "An evil spirit or creature." },
  { "word": "Dig", "definition": "To move dirt or soil to make a hole." },
  { "word": "Dinner", "definition": "The main meal of the day, usually eaten in the evening." },
  { "word": "Dirt", "definition": "Loose soil or earth." },
  { "word": "Dirty", "definition": "Not clean; covered in dirt." },
  { "word": "Dive", "definition": "To jump headfirst into water." },
  { "word": "Do", "definition": "To perform an action or task." },
  { "word": "Doctor", "definition": "A person trained to treat people who are sick or hurt." },
  { "word": "Dog", "definition": "A common pet animal that barks." },
  { "word": "Doll", "definition": "A toy made to look like a baby or person." },
  { "word": "Done", "definition": "Finished or completed." },
  { "word": "Door", "definition": "A movable barrier used to open or close an entrance." },
  { "word": "Double", "definition": "Twice as much or having two of something." },
  { "word": "Doubt", "definition": "A feeling of being unsure about something." },
  { "word": "Down", "definition": "To a lower position." },
  { "word": "Draft", "definition": "A first version of a drawing or writing." },
  { "word": "Drag", "definition": "To pull something heavy along the ground." },
  { "word": "Draw", "definition": "To make a picture with a pencil or pen." },
  { "word": "Dream", "definition": "Images, ideas, and feelings that pass through your mind while sleeping." },
  { "word": "Dress", "definition": "A piece of clothing with a top and a skirt." },
  { "word": "Drink", "definition": "To swallow a liquid." },
  { "word": "Drive", "definition": "To control a car or other vehicle." },
  { "word": "Drop", "definition": "To let go of something so it falls." },
  { "word": "Dry", "definition": "Free from water or moisture." },
  { "word": "Duck", "definition": "A water bird with a flat bill." },
  { "word": "Due", "definition": "Expected at a certain time." },
  { "word": "Dump", "definition": "To drop or throw something in a careless way." },
  { "word": "During", "definition": "At some point in a period of time." },
  { "word": "Dust", "definition": "Fine, dry powder made of tiny pieces of dirt." },
  { "word": "Duty", "definition": "Something you are required or expected to do." },
  { "word": "Dwarf", "definition": "A person, animal, or plant much smaller than normal." },
  { "word": "Daily", "definition": "Happening every day." },
  { "word": "Damage", "definition": "Physical harm that makes something less valuable or useful." },
  { "word": "Dare", "definition": "To be brave enough to do something." },
  { "word": "Dawn", "definition": "The time when the sun first comes up." },
  { "word": "Dazzle", "definition": "To impress someone with something amazing." },
  { "word": "Debate", "definition": "A discussion where people argue different sides of a topic." },
  { "word": "Decay", "definition": "To rot or break down slowly." },
  { "word": "Decorate", "definition": "To make something look more attractive." },
  { "word": "Delight", "definition": "Great pleasure or joy." },
  { "word": "Deliver", "definition": "To take goods or letters to a person or place." },
  { "word": "Depart", "definition": "To leave a place." },
  { "word": "Design", "definition": "To plan or draw something before it is made." },
  { "word": "Destroy", "definition": "To ruin or break something completely." },
  { "word": "Develop", "definition": "To grow or change over time." },
  { "word": "Diagonal", "definition": "A straight line connecting opposite corners." },
  { "word": "Diamond", "definition": "A very hard, clear, shiny jewel." },
  { "word": "Dinosaur", "definition": "A huge reptile that lived long ago." },
  { "word": "Discover", "definition": "To find something new that was unknown." },
  { "word": "Disease", "definition": "An illness that harms the body." },
  { "word": "Distant", "definition": "Far away in space or time." },
  { "word": "Divide", "definition": "To split something into smaller parts." },
  { "word": "Dizzy", "definition": "Feeling like you are spinning and might fall over." },
  { "word": "Dodge", "definition": "To quickly move out of the way." },
  { "word": "Donate", "definition": "To give money or goods to help a good cause." },
  { "word": "Donkey", "definition": "An animal like a small horse with long ears." },
  { "word": "Doodle", "definition": "To draw carelessly or without a plan." },
  { "word": "Doubtful", "definition": "Feeling unsure or uncertain." },
  { "word": "Dragon", "definition": "A mythical creature, usually a giant winged lizard that breathes fire." },
  { "word": "Drain", "definition": "To let liquid flow out of something." },
  { "word": "Dramatic", "definition": "Exciting, sudden, or full of emotion." },
  { "word": "Drill", "definition": "A tool used to make holes." },
  { "word": "Drown", "definition": "To die from being under water for too long." },
  { "word": "Dull", "definition": "Not sharp, not shiny, or not interesting." },
  { "word": "Duet", "definition": "A song or performance done by two people." },
  { "word": "Dune", "definition": "A hill of sand formed by the wind." },
  { "word": "Durable", "definition": "Strong and able to last a long time." },
  { "word": "Dynamic", "definition": "Full of energy and always changing." },
  { "word": "Display", "definition": "To show something so people can see it." },
  { "word": "Delicate", "definition": "Easily broken or damaged; gentle." },
  { "word": "Delicious", "definition": "Having a very pleasing taste." }
              ],
              'E': [
                { "word": "Each", "definition": "Every single one of a group." },
  { "word": "Ear", "definition": "The part of the body used for hearing." },
  { "word": "Early", "definition": "Happening near the beginning of a time." },
  { "word": "Earn", "definition": "To get money by working." },
  { "word": "Earth", "definition": "The planet we live on; soil or dirt." },
  { "word": "East", "definition": "One of the four main directions, where the sun rises." },
  { "word": "Easy", "definition": "Simple to do; not difficult." },
  { "word": "Eat", "definition": "To chew and swallow food." },
  { "word": "Edge", "definition": "The line where something ends; the border." },
  { "word": "Educate", "definition": "To teach or train a person." },
  { "word": "Effort", "definition": "Using energy or hard work to do something." },
  { "word": "Egg", "definition": "A shell-covered object from which some young animals hatch." },
  { "word": "Eight", "definition": "The number that comes after seven." },
  { "word": "Elbow", "definition": "The joint in the middle of your arm." },
  { "word": "Electric", "definition": "Having to do with a kind of energy used for power and light." },
  { "word": "Eleven", "definition": "The number that comes after ten." },
  { "word": "Else", "definition": "Other or different." },
  { "word": "End", "definition": "The final part of something; the finish." },
  { "word": "Energy", "definition": "The strength and power needed to be active." },
  { "word": "Engine", "definition": "A machine that uses fuel to make something move." },
  { "word": "Enjoy", "definition": "To get pleasure from something." },
  { "word": "Enough", "definition": "As much as is needed." },
  { "word": "Enter", "definition": "To go into a place." },
  { "word": "Equal", "definition": "Being the same in size, amount, or value." },
  { "word": "Even", "definition": "Flat or smooth, or a number that can be divided by two." },
  { "word": "Evening", "definition": "The time of day between afternoon and night." },
  { "word": "Ever", "definition": "At any time; always." },
  { "word": "Every", "definition": "All the members of a group." },
  { "word": "Evil", "definition": "Very bad or harmful." },
  { "word": "Exact", "definition": "Completely correct; precise." },
  { "word": "Example", "definition": "A thing or idea used to show what a group is like." },
  { "word": "Excite", "definition": "To make someone feel happy, interested, or eager." },
  { "word": "Excuse", "definition": "A reason given to explain a mistake or failure." },
  { "word": "Exit", "definition": "A way out of a place." },
  { "word": "Expect", "definition": "To think that something will happen." },
  { "word": "Explain", "definition": "To make an idea clear and easy to understand." },
  { "word": "Explore", "definition": "To travel through an area to learn about it." },
  { "word": "Eye", "definition": "The part of the body used for seeing." },
  { "word": "Empty", "definition": "Containing nothing; hollow." },
  { "word": "Elephant", "definition": "A very large gray animal with a long trunk." },
  { "word": "Envelope", "definition": "A paper cover for a letter." },
  { "word": "Erase", "definition": "To rub out or wipe away something written." },
  { "word": "Escape", "definition": "To get away from a place or person." },
  { "word": "Everyone", "definition": "Every person." },
  { "word": "Everything", "definition": "All things." },
  { "word": "Excellent", "definition": "Extremely good; top quality." },
  { "word": "Except", "definition": "Not including a certain thing or person." },
  { "word": "Expensive", "definition": "Costing a lot of money." },
  { "word": "Exclaim", "definition": "To cry out suddenly in surprise or strong feeling." },
  { "word": "Expert", "definition": "A person who knows a lot about a subject." },
  { "word": "Eel", "definition": "A long, slippery fish that looks like a snake." },
  { "word": "Echo", "definition": "A sound that is repeated because sound waves bounce off a surface." },
  { "word": "Editor", "definition": "A person who checks and corrects books or articles." },
  { "word": "Effect", "definition": "A change that is a result of an action." },
  { "word": "Elastic", "definition": "Able to stretch and return to its original shape." },
  { "word": "Elegant", "definition": "Graceful and stylish in appearance or behavior." },
  { "word": "Elevator", "definition": "A machine that lifts people or things to different floors." },
  { "word": "Embrace", "definition": "To hold someone closely in your arms; to hug." },
  { "word": "Emerald", "definition": "A precious stone that is bright green." },
  { "word": "Emotion", "definition": "A strong feeling such as joy, sadness, or anger." },
  { "word": "Emperor", "definition": "The male ruler of an empire." },
  { "word": "Encourage", "definition": "To give someone support or hope." },
  { "word": "Endure", "definition": "To suffer something difficult patiently." },
  { "word": "Enormous", "definition": "Extremely large; huge." },
  { "word": "Entire", "definition": "All of something; whole." },
  { "word": "Envy", "definition": "A feeling of wanting what someone else has." },
  { "word": "Epic", "definition": "A long, exciting story, or something grand." },
  { "word": "Episode", "definition": "One part of a TV show or a series of events." },
  { "word": "Era", "definition": "A long and important period of time." },
  { "word": "Erupt", "definition": "To burst out suddenly, like a volcano." },
  { "word": "Establish", "definition": "To set up or create something permanently." },
  { "word": "Estimate", "definition": "To guess the approximate amount or size." },
  { "word": "Evolve", "definition": "To change and grow slowly over time." },
  { "word": "Evidence", "definition": "Facts or objects that help prove something." },
  { "word": "Exaggerate", "definition": "To describe something as bigger or better than it really is." },
  { "word": "Examine", "definition": "To look at something very closely and carefully." },
  { "word": "Exhibit", "definition": "To show something publicly, like art in a museum." },
  { "word": "Expand", "definition": "To become larger or wider." },
  { "word": "Expense", "definition": "The cost of something." },
  { "word": "Experience", "definition": "Knowledge or skill gained from doing things." },
  { "word": "Express", "definition": "To show or tell your feelings or ideas." },
  { "word": "Extra", "definition": "More than is needed or expected." },
  { "word": "Extreme", "definition": "Very severe or very far from the usual." },
  { "word": "Eyesight", "definition": "The ability to see." },
  { "word": "Efficient", "definition": "Working well without wasting time or energy." },
  { "word": "Echoing", "definition": "The sound of an echo repeating." },
  { "word": "Eagle", "definition": "A large, powerful bird of prey." },
  { "word": "Entertain", "definition": "To amuse someone with a show or activity." },
  { "word": "Edible", "definition": "Safe and okay to eat." }
              ],
              'F': [
                { "word": "Face", "definition": "The front part of the head, from the forehead to the chin." },
  { "word": "Fact", "definition": "Something that is known to be true." },
  { "word": "Fail", "definition": "To not succeed or not pass a test." },
  { "word": "Fair", "definition": "Treating everyone equally and correctly." },
  { "word": "Fall", "definition": "To drop down suddenly, or the season after summer." },
  { "word": "False", "definition": "Not true or not real." },
  { "word": "Family", "definition": "A group of people related to each other, like parents and children." },
  { "word": "Famous", "definition": "Known about by many people." },
  { "word": "Fan", "definition": "A device that moves air, or someone who loves a sport or person." },
  { "word": "Far", "definition": "A long distance away." },
  { "word": "Farm", "definition": "Land used for growing crops or raising animals." },
  { "word": "Fast", "definition": "Moving or happening quickly." },
  { "word": "Fat", "definition": "Having too much flesh, or a greasy substance in food." },
  { "word": "Father", "definition": "A male parent." },
  { "word": "Fault", "definition": "The responsibility for a mistake or bad result." },
  { "word": "Fear", "definition": "A strong, unpleasant feeling caused by danger." },
  { "word": "Feather", "definition": "One of the light growths that cover a bird's body." },
  { "word": "Feed", "definition": "To give food to a person or animal." },
  { "word": "Feel", "definition": "To touch or sense something, or to have an emotion." },
  { "word": "Female", "definition": "Relating to women or girls, or animals that lay eggs or give birth." },
  { "word": "Few", "definition": "A small number of things." },
  { "word": "Field", "definition": "An area of open ground, often used for crops or sports." },
  { "word": "Fight", "definition": "To struggle or battle against someone or something." },
  { "word": "Figure", "definition": "A shape or drawing, or a number." },
  { "word": "File", "definition": "A set of papers, or a tool used to smooth things." },
  { "word": "Fill", "definition": "To make something full." },
  { "word": "Film", "definition": "A movie, or a thin layer of something." },
  { "word": "Final", "definition": "Coming at the end; last." },
  { "word": "Find", "definition": "To discover or locate something." },
  { "word": "Fine", "definition": "Very good, or a small punishment of money." },
  { "word": "Finger", "definition": "One of the five parts at the end of your hand." },
  { "word": "Finish", "definition": "To complete something." },
  { "word": "Fire", "definition": "The heat and light from burning material." },
  { "word": "First", "definition": "Before all others." },
  { "word": "Fish", "definition": "A cold-blooded animal with gills that lives in water." },
  { "word": "Fit", "definition": "To be the right size or shape, or to be healthy." },
  { "word": "Five", "definition": "The number that comes after four." },
  { "word": "Fix", "definition": "To repair or mend something broken." },
  { "word": "Flag", "definition": "A piece of cloth with a special design, used as a symbol." },
  { "word": "Flash", "definition": "A sudden burst of light." },
  { "word": "Flat", "definition": "Smooth and level; not curved." },
  { "word": "Floor", "definition": "The part of a room that you walk on." },
  { "word": "Flower", "definition": "The colorful, often sweet-smelling part of a plant." },
  { "word": "Fly", "definition": "To move through the air with wings, or a small insect." },
  { "word": "Follow", "definition": "To go after or come behind someone or something." },
  { "word": "Food", "definition": "Something you eat to stay alive." },
  { "word": "Foot", "definition": "The lowest part of your leg that you stand on." },
  { "word": "For", "definition": "In support of, or meant to be given to." },
  { "word": "Force", "definition": "A push or pull that causes motion." },
  { "word": "Forest", "definition": "A large area of land covered mainly with trees." },
  { "word": "Forget", "definition": "To not remember something." },
  { "word": "Form", "definition": "The shape or structure of something." },
  { "word": "Fort", "definition": "A strong building used by soldiers for defense." },
  { "word": "Forward", "definition": "Toward the front." },
  { "word": "Four", "definition": "The number that comes after three." },
  { "word": "Free", "definition": "Not held or owned by anyone, or costing nothing." },
  { "word": "Fresh", "definition": "New, clean, or not spoiled." },
  { "word": "Friend", "definition": "A person you know well and like." },
  { "word": "From", "definition": "Starting at a place or time." },
  { "word": "Front", "definition": "The forward part of something." },
  { "word": "Fruit", "definition": "The sweet, fleshy part of a plant that holds seeds." },
  { "word": "Full", "definition": "Holding as much as possible; complete." },
  { "word": "Fun", "definition": "Enjoyment or playful activity." },
  { "word": "Funny", "definition": "Causing laughter." },
  { "word": "Future", "definition": "The time that is yet to come." },
  { "word": "Fable", "definition": "A short story that teaches a lesson." },
  { "word": "Factory", "definition": "A building where products are made." },
  { "word": "Faint", "definition": "To suddenly lose consciousness, or weak." },
  { "word": "Fantasy", "definition": "An imagined world or story that is not real." },
  { "word": "Faucet", "definition": "A handle controlling the flow of water from a pipe." },
  { "word": "Favorite", "definition": "The thing or person liked best." },
  { "word": "Ferry", "definition": "A boat used to carry people or vehicles across water." },
  { "word": "Fierce", "definition": "Very strong, aggressive, or violent." },
  { "word": "Float", "definition": "To rest on top of water or in the air without sinking." },
  { "word": "Flock", "definition": "A group of birds or sheep together." },
  { "word": "Fluffy", "definition": "Soft and light like cotton." },
  { "word": "Foil", "definition": "A very thin sheet of metal, like aluminum." },
  { "word": "Fond", "definition": "Having a liking or love for something." },
  { "word": "Foreign", "definition": "From another country or unfamiliar." },
  { "word": "Fossil", "definition": "The preserved remains of a plant or animal from long ago." },
  { "word": "Frame", "definition": "A border that surrounds a picture or window." },
  { "word": "Freeze", "definition": "To turn into ice because of extreme cold." },
  { "word": "Frighten", "definition": "To make someone afraid or scared." },
  { "word": "Frown", "definition": "To wrinkle your forehead to show sadness or anger." },
  { "word": "Fuel", "definition": "Material that is burned to create heat or power." },
  { "word": "Funnel", "definition": "A wide cone-shaped tool for pouring liquids into small openings." },
  { "word": "Fuss", "definition": "Unnecessary excitement or worry about a small thing." },
  { "word": "Furry", "definition": "Covered with soft hair or fur." },
  { "word": "Fiction", "definition": "A story that is invented or made up." },
  { "word": "Fragile", "definition": "Easily broken or damaged." },
  { "word": "Feast", "definition": "A very large, rich, or special meal." },
  { "word": "Fiddle", "definition": "A musical instrument, like a violin." },
  { "word": "Flute", "definition": "A musical pipe instrument played by blowing across a hole." }
                ],
              'G': [
                { "word": "Gain", "definition": "To get or acquire something, like knowledge or weight." },
  { "word": "Game", "definition": "An activity or sport with rules, played for fun." },
  { "word": "Garden", "definition": "A piece of ground used for growing flowers, fruit, or vegetables." },
  { "word": "Gas", "definition": "A substance like air that is not solid or liquid." },
  { "word": "Gate", "definition": "A barrier that opens and closes, usually in a fence or wall." },
  { "word": "Gather", "definition": "To bring things together; to collect." },
  { "word": "Gay", "definition": "Happy and cheerful; also means homosexual." },
  { "word": "Gear", "definition": "Equipment used for a specific purpose, like camping or fishing." },
  { "word": "General", "definition": "Relating to all or most people or things; not specific." },
  { "word": "Gentle", "definition": "Kind and soft; not rough." },
  { "word": "Get", "definition": "To obtain, receive, or become." },
  { "word": "Giant", "definition": "Much larger than normal." },
  { "word": "Gift", "definition": "Something given to someone without asking for payment." },
  { "word": "Girl", "definition": "A young female person." },
  { "word": "Give", "definition": "To hand over or offer something to someone." },
  { "word": "Glad", "definition": "Happy or pleased." },
  { "word": "Glass", "definition": "A hard, clear material used for windows or cups." },
  { "word": "Glide", "definition": "To move smoothly and quietly." },
  { "word": "Globe", "definition": "A sphere with a map of the world on it." },
  { "word": "Glove", "definition": "A covering for the hand with separate sections for fingers." },
  { "word": "Go", "definition": "To move from one place to another." },
  { "word": "Goal", "definition": "The end point of a game, or something you plan to achieve." },
  { "word": "Goat", "definition": "A small animal with horns, raised on farms." },
  { "word": "God", "definition": "A supreme being or creator, usually in a religion." },
  { "word": "Gold", "definition": "A precious, shiny, yellow metal." },
  { "word": "Gone", "definition": "Away from a place; missing." },
  { "word": "Good", "definition": "Of high quality; morally right." },
  { "word": "Grab", "definition": "To take hold of something suddenly or quickly." },
  { "word": "Grade", "definition": "A level in school, or a mark showing the quality of schoolwork." },
  { "word": "Grain", "definition": "Small, hard seeds of plants like wheat and rice." },
  { "word": "Grand", "definition": "Magnificent, large, or very important." },
  { "word": "Grass", "definition": "A common green plant covering the ground." },
  { "word": "Grave", "definition": "A place where a dead person is buried." },
  { "word": "Gray", "definition": "A color that is a mix of black and white." },
  { "word": "Great", "definition": "Very large or very important." },
  { "word": "Green", "definition": "The color of grass and leaves." },
  { "word": "Greet", "definition": "To welcome someone with a cheerful word or gesture." },
  { "word": "Grin", "definition": "A wide smile." },
  { "word": "Ground", "definition": "The solid surface of the Earth." },
  { "word": "Group", "definition": "A number of people or things that are together." },
  { "word": "Grow", "definition": "To become larger or taller over time." },
  { "word": "Guard", "definition": "To watch over and protect someone or something." },
  { "word": "Guess", "definition": "To make a judgment without knowing all the facts." },
  { "word": "Guide", "definition": "A person who leads or shows the way." },
  { "word": "Gun", "definition": "A weapon that fires bullets." },
  { "word": "Gut", "definition": "The stomach and intestines." },
  { "word": "Guy", "definition": "An informal word for a man or boy." },
  { "word": "Gym", "definition": "A place for indoor exercise and sports." },
  { "word": "Galaxy", "definition": "A huge group of stars, gas, and dust in space." },
  { "word": "Giggle", "definition": "To laugh lightly in a silly or nervous way." },
  { "word": "Glacier", "definition": "A large, slow-moving mass of ice." },
  { "word": "Glimmer", "definition": "A faint, unsteady light." },
  { "word": "Gossip", "definition": "Casual talk about other people's private lives." },
  { "word": "Govern", "definition": "To rule or manage a country or area." },
  { "word": "Grape", "definition": "A small, round, sweet fruit that grows in bunches." },
  { "word": "Gratitude", "definition": "The feeling of being thankful; appreciation." },
  { "word": "Greedy", "definition": "Wanting more than you need." },
  { "word": "Grip", "definition": "To hold something tightly." },
  { "word": "Grumpy", "definition": "Bad-tempered and easily annoyed." },
  { "word": "Gull", "definition": "A type of bird, often found near the sea; a seagull." },
  { "word": "Gasp", "definition": "To take a quick, short breath because of surprise or pain." },
  { "word": "Genuine", "definition": "Truly what something is said to be; real." },
  { "word": "Glance", "definition": "To take a quick look." },
  { "word": "Gloomy", "definition": "Dark and sad." },
  { "word": "Grateful", "definition": "Feeling or showing thanks." },
  { "word": "Gravity", "definition": "The force that pulls things toward the Earth's center." },
  { "word": "Grill", "definition": "A metal frame used for cooking food over fire." },
  { "word": "Guest", "definition": "A person who is visiting another person or place." },
  { "word": "Gum", "definition": "A sticky, chewy candy." },
  { "word": "Goose", "definition": "A large water bird, bigger than a duck." },
  { "word": "Gasping", "definition": "The sound of struggling to breathe." },
  { "word": "Gel", "definition": "A thick, jelly-like substance." },
  { "word": "Gem", "definition": "A beautiful, valuable stone; a jewel." },
  { "word": "Glitter", "definition": "To shine with tiny, bright flashes of light." },
  { "word": "Gobble", "definition": "To eat food quickly and noisily." },
  { "word": "Golden", "definition": "Made of or colored like gold." },
  { "word": "Gorgeous", "definition": "Very beautiful or attractive." },
  { "word": "Gracious", "definition": "Kind, polite, and pleasant." },
  { "word": "Graduate", "definition": "To finish a course of study at a school or college." },
  { "word": "Graffiti", "definition": "Writing or drawings scribbled on public walls." },
  { "word": "Gravel", "definition": "Small stones and pebbles." },
  { "word": "Grocery", "definition": "Food and household supplies sold in a store." },
  { "word": "Grotto", "definition": "A small, picturesque cave, often by water." },
  { "word": "Grumble", "definition": "To complain in a quiet, bad-tempered way." },
  { "word": "Guarantee", "definition": "A promise that something will be done or will work." },
  { "word": "Habit", "definition": "A regular thing you do without thinking." },
  { "word": "Hair", "definition": "Fine thread-like strands that grow on the head and body." },
  { "word": "Half", "definition": "One of two equal parts of something." },
  { "word": "Hall", "definition": "A long passage in a building, or a large room for events." }
                ],
              'H': [
                { "word": "Hand", "definition": "The end part of the arm, used for holding and grasping." },
  { "word": "Handle", "definition": "The part of an object you use to hold or carry it." },
  { "word": "Hang", "definition": "To attach or be suspended from above." },
  { "word": "Happen", "definition": "To take place or occur." },
  { "word": "Happy", "definition": "Feeling or showing pleasure and contentment." },
  { "word": "Hard", "definition": "Solid and firm; difficult to do." },
  { "word": "Harm", "definition": "Physical injury or damage." },
  { "word": "Hat", "definition": "A covering for the head." },
  { "word": "Hate", "definition": "To dislike intensely." },
  { "word": "Have", "definition": "To own, possess, or hold something." },
  { "word": "He", "definition": "A word used for a male person or boy." },
  { "word": "Head", "definition": "The top part of the body that contains the brain, eyes, and mouth." },
  { "word": "Heal", "definition": "To become sound or healthy again; to recover." },
  { "word": "Hear", "definition": "To perceive sounds with the ears." },
  { "word": "Heart", "definition": "The organ that pumps blood, or the center of feelings." },
  { "word": "Heat", "definition": "The quality of being hot; warmth." },
  { "word": "Heavy", "definition": "Weighing a lot; difficult to lift." },
  { "word": "Heel", "definition": "The back part of the human foot." },
  { "word": "Height", "definition": "The measurement of how tall something or someone is." },
  { "word": "Hello", "definition": "A word used to greet someone." },
  { "word": "Help", "definition": "To make it easier for someone to do something." },
  { "word": "Her", "definition": "A word used to refer to a female person or girl." },
  { "word": "Here", "definition": "In this place." },
  { "word": "Hide", "definition": "To put something in a place where it cannot be found." },
  { "word": "High", "definition": "Extending far upward; tall." },
  { "word": "Hill", "definition": "A raised area of land, smaller than a mountain." },
  { "word": "Him", "definition": "A word used as the object of a verb or preposition for a male." },
  { "word": "Hire", "definition": "To employ someone for a job." },
  { "word": "His", "definition": "Belonging to a male person." },
  { "word": "Hit", "definition": "To strike something with force." },
  { "word": "Hold", "definition": "To grasp, carry, or keep something." },
  { "word": "Hole", "definition": "An empty space or gap in a solid object or surface." },
  { "word": "Home", "definition": "The place where one lives." },
  { "word": "Honey", "definition": "A sweet, sticky food made by bees." },
  { "word": "Hook", "definition": "A curved piece of metal used for catching or holding things." },
  { "word": "Hope", "definition": "A feeling of expectation and desire for a certain thing to happen." },
  { "word": "Horn", "definition": "A hard, pointed growth on the head of some animals." },
  { "word": "Horse", "definition": "A large animal used for riding or pulling heavy things." },
  { "word": "Hospital", "definition": "A place where sick or injured people are treated." },
  { "word": "Hot", "definition": "Having a high temperature." },
  { "word": "Hour", "definition": "A unit of time equal to sixty minutes." },
  { "word": "House", "definition": "A building for human habitation." },
  { "word": "How", "definition": "In what way or manner." },
  { "word": "Huge", "definition": "Extremely large; enormous." },
  { "word": "Human", "definition": "Relating to people; a person." },
  { "word": "Humble", "definition": "Not proud or arrogant; modest." },
  { "word": "Humor", "definition": "The quality of being amusing or funny." },
  { "word": "Hundred", "definition": "The number equal to ten multiplied by ten (100)." },
  { "word": "Hunger", "definition": "A feeling of needing to eat food." },
  { "word": "Hunt", "definition": "To search for or chase wild animals for food or sport." },
  { "word": "Hurt", "definition": "To cause injury or pain to a person or animal." },
  { "word": "Hurry", "definition": "To move or act quickly." },
  { "word": "Hut", "definition": "A small, simple house or shelter." },
  { "word": "Hygiene", "definition": "Practices that keep you clean and healthy." },
  { "word": "Hail", "definition": "Small balls of ice falling from the sky." },
  { "word": "Haircut", "definition": "The act of trimming or shaping the hair." },
  { "word": "Hammer", "definition": "A tool with a heavy metal head used for hitting things." },
  { "word": "Harbor", "definition": "A place on the coast where boats can safely shelter." },
  { "word": "Harvest", "definition": "The time of year when crops are gathered." },
  { "word": "Hazard", "definition": "A danger or a risk." },
  { "word": "Headline", "definition": "The title of a newspaper article." },
  { "word": "Helmet", "definition": "A hard hat worn for protection." },
  { "word": "Herd", "definition": "A large group of animals, especially hoofed ones." },
  { "word": "Hero", "definition": "A person admired for their courage or achievements." },
  { "word": "Hiccup", "definition": "A sudden, repeated, and loud gulping sound from the throat." },
  { "word": "Highway", "definition": "A major road for fast travel." },
  { "word": "History", "definition": "The study of past events." },
  { "word": "Hobby", "definition": "An activity done for pleasure in one's spare time." },
  { "word": "Holiday", "definition": "A special day off from work or school." },
  { "word": "Honest", "definition": "Telling the truth and not cheating." },
  { "word": "Honor", "definition": "High respect or great esteem." },
  { "word": "Horizon", "definition": "The line where the earth and sky seem to meet." },
  { "word": "Host", "definition": "A person who invites guests or organizes an event." },
  { "word": "Hug", "definition": "To hold someone tightly and lovingly in your arms." },
  { "word": "Hum", "definition": "To sing with your mouth closed, or a low, steady sound." },
  { "word": "Hut", "definition": "A small, simple house or shelter." },
  { "word": "Habit", "definition": "A regular thing you do without thinking." },
  { "word": "Hair", "definition": "Fine thread-like strands that grow on the head and body." },
  { "word": "Half", "definition": "One of two equal parts of something." },
  { "word": "Hall", "definition": "A long passage in a building, or a large room for events." },
  { "word": "Hammer", "definition": "A tool with a heavy metal head used for hitting things." },
  { "word": "Hamster", "definition": "A small rodent often kept as a pet." },
  { "word": "Handy", "definition": "Useful or clever at fixing things." },
  { "word": "Harsh", "definition": "Extremely rough, cruel, or severe." },
  { "word": "Haul", "definition": "To pull or drag something heavy." },
  { "word": "Haven", "definition": "A safe place or shelter." },
  { "word": "Hedge", "definition": "A row of closely planted bushes or small trees." },
  { "word": "Hike", "definition": "A long walk, especially in the countryside." },
  { "word": "Hollow", "definition": "Empty space inside a solid object." },
  { "word": "Homeless", "definition": "Having no place to live." },
  { "word": "Huddle", "definition": "To crowd together closely." }
                ],
              'I': [
                { "word": "I", "definition": "The word you use when speaking about yourself." },
  { "word": "Ice", "definition": "Frozen water that is very cold and hard." },
  { "word": "Idea", "definition": "A thought or plan formed in your mind." },
  { "word": "If", "definition": "Used to say that something depends on something else." },
  { "word": "Ill", "definition": "Sick or unwell." },
  { "word": "Imagine", "definition": "To form a picture in your mind of something that is not real." },
  { "word": "Import", "definition": "To bring goods into a country from somewhere else." },
  { "word": "Important", "definition": "Having great meaning or value." },
  { "word": "Impossible", "definition": "Something that cannot happen or be done." },
  { "word": "In", "definition": "Inside a place or container." },
  { "word": "Inch", "definition": "A small unit of measurement for length." },
  { "word": "Include", "definition": "To make something a part of a larger group or set." },
  { "word": "Income", "definition": "Money that a person earns." },
  { "word": "Indeed", "definition": "Truly or certainly." },
  { "word": "India", "definition": "A large country in southern Asia." },
  { "word": "Individual", "definition": "A single person or thing." },
  { "word": "Indoor", "definition": "Inside a building." },
  { "word": "Infect", "definition": "To give someone a sickness or disease." },
  { "word": "Inform", "definition": "To tell someone facts or information." },
  { "word": "Injury", "definition": "Harm or damage to a person's body." },
  { "word": "Inner", "definition": "Located on the inside." },
  { "word": "Inquire", "definition": "To ask a question." },
  { "word": "Insect", "definition": "A very small animal with six legs, like an ant or bee." },
  { "word": "Inside", "definition": "The inner part of something." },
  { "word": "Instant", "definition": "Happening immediately; a very short moment of time." },
  { "word": "Instead", "definition": "In place of someone or something else." },
  { "word": "Instruct", "definition": "To teach or tell someone what to do." },
  { "word": "Instrument", "definition": "A tool or device, especially one used for music." },
  { "word": "Interest", "definition": "A feeling of wanting to know or learn about something." },
  { "word": "Into", "definition": "Moving to the inside of something." },
  { "word": "Invite", "definition": "To ask someone to come to a place or event." },
  { "word": "Iron", "definition": "A strong, heavy metal, or a tool used to press wrinkles out of clothes." },
  { "word": "Island", "definition": "A piece of land completely surrounded by water." },
  { "word": "Issue", "definition": "An important topic or problem for debate or discussion." },
  { "word": "It", "definition": "A word used for a thing or animal." },
  { "word": "Item", "definition": "A single thing in a list or group." },
  { "word": "Its", "definition": "Belonging to a thing or animal." },
  { "word": "Identical", "definition": "Exactly the same." },
  { "word": "Ignite", "definition": "To set something on fire." },
  { "word": "Illegal", "definition": "Against the law." },
  { "word": "Illusion", "definition": "Something that seems different from what it really is." },
  { "word": "Image", "definition": "A picture or reflection of someone or something." },
  { "word": "Imitate", "definition": "To copy the way someone else acts or talks." },
  { "word": "Immediately", "definition": "Right away; without delay." },
  { "word": "Immense", "definition": "Extremely large or great." },
  { "word": "Impact", "definition": "The strong effect one thing has on another." },
  { "word": "Imply", "definition": "To suggest something without saying it directly." },
  { "word": "Improve", "definition": "To make something better." },
  { "word": "Impulse", "definition": "A sudden urge or quick thought to do something." },
  { "word": "Incline", "definition": "A slope or slant." },
  { "word": "Independent", "definition": "Not controlled by others; free to make your own choices." },
  { "word": "Influence", "definition": "The power to change how someone thinks or acts." },
  { "word": "Initial", "definition": "Happening at the very beginning; the first letter of a name." },
  { "word": "Innocent", "definition": "Not guilty of a crime or not meaning to do harm." },
  { "word": "Inspire", "definition": "To fill someone with the urge to do or feel something." },
  { "word": "Intend", "definition": "To have something in mind as a plan." },
  { "word": "Intense", "definition": "Very strong or extreme." },
  { "word": "Interact", "definition": "To talk or work with other people." },
  { "word": "Invent", "definition": "To create or design something that has never existed before." },
  { "word": "Investigate", "definition": "To look into something carefully to find out the truth." },
  { "word": "Invisible", "definition": "Impossible to see." },
  { "word": "Icy", "definition": "Covered with or made of ice; very cold." },
  { "word": "Illness", "definition": "A sickness or disease." },
  { "word": "Illustrate", "definition": "To draw a picture or explain with an example." },
  { "word": "Imitate", "definition": "To copy the actions or voice of another person." },
  { "word": "Incredible", "definition": "Hard to believe; amazing." },
  { "word": "Industry", "definition": "All the businesses that make one type of product." },
  { "word": "Inhale", "definition": "To breathe air into your lungs." },
  { "word": "Inject", "definition": "To push a liquid into the body using a needle." },
  { "word": "Ink", "definition": "A colored liquid used for writing or drawing." },
  { "word": "Input", "definition": "Information put into a computer or system." },
  { "word": "Install", "definition": "To put equipment into place and make it ready for use." },
  { "word": "Insult", "definition": "To say something mean or disrespectful to someone." },
  { "word": "Intelligent", "definition": "Having great smartness or knowledge." },
  { "word": "Interfere", "definition": "To get in the way of something or stop it from happening." },
  { "word": "Internal", "definition": "Inside the body or a machine." },
  { "word": "Interpret", "definition": "To explain the meaning of something." },
  { "word": "Interview", "definition": "A meeting where questions are asked and answered." },
  { "word": "Introduce", "definition": "To present one person to another for the first time." },
  { "word": "Invade", "definition": "To enter a country or area by force." },
  { "word": "Invisible", "definition": "Cannot be seen." },
  { "word": "Invoice", "definition": "A bill that shows how much someone owes." },
  { "word": "Irregular", "definition": "Not regular or not following the usual pattern." },
  { "word": "Irritate", "definition": "To annoy or bother someone." },
  { "word": "Irony", "definition": "Saying one thing but meaning the opposite, often in a funny way." },
  { "word": "Itch", "definition": "An uncomfortable feeling on the skin that makes you want to scratch." },
  { "word": "Ivory", "definition": "A hard, white substance that forms the tusks of elephants." },
  { "word": "Jungle", "definition": "A large area of land filled with thick, hot rainforest." },
  { "word": "Jealous", "definition": "Feeling unhappy because you want what someone else has." },
  { "word": "Jewel", "definition": "A precious stone, often cut and polished." },
  { "word": "Jelly", "definition": "A soft, sweet, clear food made from fruit juice." }
                ],
              'J': [
                { "word": "Jackal", "definition": "A wild dog-like animal that eats dead animals." },
  { "word": "Jacket", "definition": "A piece of clothing worn over the upper body for warmth." },
  { "word": "Jaguar", "definition": "A large spotted wild cat found in Central and South America." },
  { "word": "Jail", "definition": "A place where people who break the law are kept." },
  { "word": "Jam", "definition": "A sweet spread made from cooked fruit, or to get stuck." },
  { "word": "Jar", "definition": "A glass container with a wide mouth and a lid." },
  { "word": "Jaw", "definition": "The bony part of the face that holds the teeth." },
  { "word": "Jazz", "definition": "A style of music that has strong, lively rhythms." },
  { "word": "Jeans", "definition": "Trousers made from a thick cotton fabric called denim." },
  { "word": "Jet", "definition": "An aircraft that moves very fast using jet engines." },
  { "word": "Job", "definition": "Work that a person does regularly for money." },
  { "word": "Join", "definition": "To connect or become a member of a group." },
  { "word": "Joint", "definition": "The place where two things or bones connect." },
  { "word": "Joke", "definition": "Something said or done to make people laugh." },
  { "word": "Journal", "definition": "A book where you write down daily events and thoughts." },
  { "word": "Journey", "definition": "A trip from one place to another." },
  { "word": "Joy", "definition": "A feeling of great happiness." },
  { "word": "Judge", "definition": "A public official who decides court cases; to form an opinion." },
  { "word": "Jug", "definition": "A large container with a handle, used for holding and pouring liquids." },
  { "word": "Juice", "definition": "The liquid squeezed from fruit or vegetables." },
  { "word": "Jumble", "definition": "A confused mess of things." },
  { "word": "Jump", "definition": "To push yourself off the ground into the air." },
  { "word": "Just", "definition": "Fair and right, or happening right now." },
  { "word": "Justice", "definition": "Fairness and moral rightness." },
  { "word": "Juvenile", "definition": "Relating to young people or children." },
  { "word": "Jab", "definition": "To poke or push something quickly and sharply." },
  { "word": "Jailbird", "definition": "A humorous name for a person who has been in jail." },
  { "word": "Jargon", "definition": "Special words used only by people in a specific group or job." },
  { "word": "Javelin", "definition": "A light spear thrown in a sports competition." },
  { "word": "Jeer", "definition": "To shout mean or mocking words at someone." },
  { "word": "Jerk", "definition": "A quick, sudden pull or movement." },
  { "word": "Jingle", "definition": "A light, ringing sound, or a short song used in ads." },
  { "word": "Jockey", "definition": "A person who rides horses in races." },
  { "word": "Jot", "definition": "To quickly write down a note." },
  { "word": "Jovial", "definition": "Cheerful and friendly." },
  { "word": "Jubilee", "definition": "A special celebration of an anniversary, often 50 years." },
  { "word": "Judo", "definition": "A Japanese sport of self-defense." },
  { "word": "Juggler", "definition": "A person who keeps several objects moving in the air at once." },
  { "word": "Junior", "definition": "Younger or lower in rank." },
  { "word": "Junk", "definition": "Old, useless things; trash." },
  { "word": "Jury", "definition": "A group of people in a court who decide if someone is guilty." },
  { "word": "Jigsaw", "definition": "A puzzle made of small, interlocking pieces." },
  { "word": "Jiggle", "definition": "To shake lightly and quickly." },
  { "word": "Jailbreak", "definition": "When a prisoner escapes from jail." },
  { "word": "Jamb", "definition": "The side post or vertical part of a doorframe." },
  { "word": "January", "definition": "The first month of the year." },
  { "word": "Jester", "definition": "A person in old times who made people laugh." },
  { "word": "Jolt", "definition": "A sudden, strong, and surprising movement." },
  { "word": "Jostle", "definition": "To push, elbow, or bump against someone." },
  { "word": "Journalism", "definition": "The work of writing and reporting news." },
  { "word": "Jovial", "definition": "Cheerful and friendly." },
  { "word": "Jubilant", "definition": "Feeling or showing great joy." },
  { "word": "Junction", "definition": "A place where two or more roads or lines meet." },
  { "word": "Junior", "definition": "Younger or lower in rank." },
  { "word": "Junket", "definition": "A trip taken by an official that is paid for with public money." },
  { "word": "Jut", "definition": "To stick out or project sharply." },
  { "word": "Jade", "definition": "A green or white precious stone." },
  { "word": "Jellyfish", "definition": "A sea creature with a soft body and stinging tentacles." },
  { "word": "Jeopardy", "definition": "Danger or risk of harm." },
  { "word": "Jingle", "definition": "A light, ringing sound, or a short, catchy tune." },
  { "word": "Jockey", "definition": "A person who rides horses in races." },
  { "word": "Jolt", "definition": "A sudden, strong, and surprising movement." },
  { "word": "Journal", "definition": "A daily record of news or events, or a personal diary." },
  { "word": "Joust", "definition": "A sport where two knights ride horses and fight with lances." },
  { "word": "Jumble", "definition": "A confused mess or mix." },
  { "word": "Jury", "definition": "A group of people in a court who decide if someone is guilty." },
  { "word": "Jute", "definition": "A strong fiber used for making ropes and sacks." },
  { "word": "Jackhammer", "definition": "A noisy tool used to break up concrete." },
  { "word": "Jargon", "definition": "Special words used only by people in a specific group or job." },
  { "word": "Jester", "definition": "A person in old times who made people laugh." },
  { "word": "Jewelry", "definition": "Small ornamental things, like necklaces or rings." },
  { "word": "Jiggle", "definition": "To shake lightly and quickly." },
  { "word": "Jittery", "definition": "Feeling nervous and shaky." },
  { "word": "Jog", "definition": "To run slowly, often for exercise." },
  { "word": "Jumble", "definition": "A confused mess or mix." },
  { "word": "Junior", "definition": "Younger or lower in rank." },
  { "word": "Jungle", "definition": "A thick, dense tropical forest." },
  { "word": "Junket", "definition": "A pleasure trip taken by an official, often with public money." },
  { "word": "Justify", "definition": "To show or prove that something is right or reasonable." },
  { "word": "Jig", "definition": "A lively, fast dance." },
  { "word": "Jerk", "definition": "A quick, sudden pull or movement." },
  { "word": "Jolly", "definition": "Happy and cheerful." },
  { "word": "Jumpy", "definition": "Nervous or easily startled." },
  { "word": "Jungle", "definition": "A thick, dense tropical forest." },
  { "word": "Jigsaw", "definition": "A puzzle made of small, interlocking pieces." },
  { "word": "Jolt", "definition": "A sudden, strong, and surprising movement." }
                ],
              'K': [
                { "word": "Kangaroo", "definition": "A large Australian animal with strong back legs that jumps." },
  { "word": "Karate", "definition": "A Japanese sport of self-defense using quick hand and foot movements." },
  { "word": "Kitten", "definition": "A baby cat." },
  { "word": "Keep", "definition": "To hold onto something or store it safely." },
  { "word": "Kernel", "definition": "A grain or seed of corn or other plants." },
  { "word": "Ketchup", "definition": "A thick, sweet sauce made from tomatoes." },
  { "word": "Kettle", "definition": "A pot, usually metal, for boiling water." },
  { "word": "Key", "definition": "A shaped piece of metal used to open a lock." },
  { "word": "Kick", "definition": "To hit something with your foot." },
  { "word": "Kid", "definition": "A child; a young person." },
  { "word": "Kill", "definition": "To cause a person or animal to die." },
  { "word": "Kind", "definition": "To be friendly, generous, and thoughtful." },
  { "word": "King", "definition": "A male ruler of a country." },
  { "word": "Kiss", "definition": "To touch with the lips as a sign of love or greeting." },
  { "word": "Kit", "definition": "A set of tools or equipment needed for a specific activity." },
  { "word": "Kitchen", "definition": "A room where food is cooked." },
  { "word": "Knee", "definition": "The joint that connects the upper and lower parts of your leg." },
  { "word": "Kneel", "definition": "To rest your body on your knees." },
  { "word": "Knife", "definition": "A tool with a sharp blade used for cutting." },
  { "word": "Knight", "definition": "A soldier in the Middle Ages who rode a horse and wore armor." },
  { "word": "Knit", "definition": "To make cloth by looping yarn with long needles." },
  { "word": "Knob", "definition": "A rounded handle used for opening a door or pulling a drawer." },
  { "word": "Knock", "definition": "To hit a door or surface to get attention." },
  { "word": "Knot", "definition": "A fastening made by tying string or rope together." },
  { "word": "Know", "definition": "To have information or be familiar with something." },
  { "word": "Knowledge", "definition": "Facts, information, and skills learned through experience." },
  { "word": "Koala", "definition": "A small, furry Australian animal that looks like a teddy bear." },
  { "word": "Kayak", "definition": "A small, narrow boat pointed at both ends." },
  { "word": "Kelp", "definition": "A large, brown seaweed that grows in the ocean." },
  { "word": "Kennel", "definition": "A small shelter for a dog." },
  { "word": "Kerchief", "definition": "A piece of cloth worn as a covering on the head or neck." },
  { "word": "Kickstand", "definition": "A folding metal bar used to keep a bicycle standing up." },
  { "word": "Kindness", "definition": "The quality of being friendly and thoughtful." },
  { "word": "Kingdom", "definition": "A country ruled by a king or queen." },
  { "word": "Kinship", "definition": "A close connection or relationship." },
  { "word": "Kiosk", "definition": "A small, open-sided stall or booth selling things." },
  { "word": "Kite", "definition": "A light frame covered in paper or cloth that flies in the air." },
  { "word": "Klutz", "definition": "A clumsy person (a funny, informal word)." },
  { "word": "Kneecap", "definition": "The small, flat bone at the front of the knee joint." },
  { "word": "Knickknack", "definition": "A small, inexpensive object or ornament." },
  { "word": "Knightly", "definition": "Behaving like a brave and honest knight." },
  { "word": "Kookaburra", "definition": "An Australian bird known for its loud, laughing call." },
  { "word": "Krill", "definition": "Tiny shrimp-like sea animals eaten by whales." },
  { "word": "Keeper", "definition": "A person who looks after animals in a zoo or guards something." },
  { "word": "Kudos", "definition": "Praise or honor given for an achievement." },
  { "word": "Keen", "definition": "Having or showing eagerness or enthusiasm." },
  { "word": "Keystone", "definition": "The central stone at the top of an arch that holds the others in place." },
  { "word": "Kidnap", "definition": "To take someone away illegally by force." },
  { "word": "Kilt", "definition": "A knee-length skirt with pleats, traditionally worn by men in Scotland." },
  { "word": "Kiosk", "definition": "A small, open-sided stall or booth selling things." },
  { "word": "Kiwi", "definition": "A flightless bird from New Zealand, or a fuzzy brown fruit." },
  { "word": "Klaxon", "definition": "A loud electric horn or warning device." },
  { "word": "Kneading", "definition": "Pressing and folding dough with your hands before baking." },
  { "word": "Knickers", "definition": "Loose-fitting short pants gathered at the knee." },
  { "word": "Kook", "definition": "A strange or eccentric person (informal)." },
  { "word": "Krypton", "definition": "A gas that is an element on the Periodic Table." },
  { "word": "Karma", "definition": "The idea that good or bad actions in life bring similar results later." },
  { "word": "Karat", "definition": "A unit used to measure the purity of gold." },
  { "word": "Keel", "definition": "The long, heavy piece of wood or metal along the bottom of a boat." },
  { "word": "Keeper", "definition": "A person who guards or protects something." },
  { "word": "Kryptonite", "definition": "A fictional rock that is harmful to Superman." },
  { "word": "Kneel", "definition": "To go down and rest on your knees." },
  { "word": "Knapsack", "definition": "A bag worn on the back; a backpack." },
  { "word": "Knuckle", "definition": "A joint of a finger, especially where it connects to the hand." },
  { "word": "Kickoff", "definition": "The start of a football game or an event." },
  { "word": "Kindly", "definition": "In a gentle and friendly way." },
  { "word": "Kinetic", "definition": "Relating to or caused by motion." },
  { "word": "Knead", "definition": "To press and fold dough before baking." },
  { "word": "Knowledgeable", "definition": "Having a lot of information and understanding." },
  { "word": "Krill", "definition": "Tiny shrimp-like sea animals eaten by whales." },
  { "word": "Keystone", "definition": "The center stone at the top of an arch that holds the others in place." },
  { "word": "Kindred", "definition": "Having similar interests or feelings; related." },
  { "word": "Kleptomania", "definition": "A mental illness that makes a person want to steal things." },
  { "word": "Knee-jerk", "definition": "A quick reaction made without thinking." },
  { "word": "Knighthood", "definition": "The rank or status of a knight." },
  { "word": "Kryptic", "definition": "Having a hidden or mysterious meaning (like 'cryptic')." },
  { "word": "Keepsake", "definition": "A small item kept in memory of a person or event." },
  { "word": "Khaki", "definition": "A dull yellowish-brown color, often used for clothes." },
  { "word": "Kilo", "definition": "A short form for 'kilogram' (1000 grams) or 'kilometer' (1000 meters)." },
  { "word": "Kiosk", "definition": "A small, open-sided stall or booth selling things." },
  { "word": "Kismet", "definition": "Fate or destiny." },
  { "word": "Kudos", "definition": "Praise or honor given for an achievement." },
  { "word": "Kibble", "definition": "Dry, crunchy food for pets, like dogs or cats." },
  { "word": "Kickback", "definition": "A secret payment made in return for favorable treatment." },
  { "word": "Kickball", "definition": "A game similar to baseball, but the ball is kicked." },
  { "word": "Kickoff", "definition": "The beginning of a football game or a large event." },
  { "word": "Kingly", "definition": "Grand, splendid, or appropriate for a king." },
  { "word": "Knack", "definition": "A clever skill or talent for doing something easily." },
  { "word": "Kneecap", "definition": "The bone at the front of the knee joint." },
  { "word": "Knockout", "definition": "To win a boxing match by knocking the opponent down." },
  { "word": "Koala", "definition": "A furry Australian animal that looks like a teddy bear." }
                ],
              'L': [
                { "word": "Label", "definition": "A small piece of paper or cloth attached to show what something is." },
  { "word": "Labor", "definition": "Hard work, or the process of giving birth." },
  { "word": "Lace", "definition": "A cord used to tie shoes, or a delicate fabric." },
  { "word": "Lack", "definition": "The state of not having enough of something." },
  { "word": "Ladder", "definition": "A structure with rungs for climbing up and down." },
  { "word": "Lady", "definition": "A polite name for a woman." },
  { "word": "Lake", "definition": "A large body of water surrounded by land." },
  { "word": "Lamb", "definition": "A baby sheep." },
  { "word": "Lame", "definition": "Unable to walk properly because of an injury." },
  { "word": "Lamp", "definition": "A device that gives light." },
  { "word": "Land", "definition": "The solid part of the Earth's surface; to arrive on the ground." },
  { "word": "Language", "definition": "The system of words used by people of a nation to talk." },
  { "word": "Lap", "definition": "The flat area formed by the upper legs of a seated person." },
  { "word": "Large", "definition": "Big in size or amount." },
  { "word": "Last", "definition": "Coming after all the others; final." },
  { "word": "Late", "definition": "Happening after the usual or expected time." },
  { "word": "Laugh", "definition": "To make sounds showing you are happy or amused." },
  { "word": "Law", "definition": "A rule made by a government that everyone must follow." },
  { "word": "Lay", "definition": "To put something down gently; to produce an egg." },
  { "word": "Lead", "definition": "To guide someone or show them the way." },
  { "word": "Leaf", "definition": "A flat, green part of a plant or tree." },
  { "word": "Lean", "definition": "To bend your body or an object in one direction." },
  { "word": "Learn", "definition": "To gain knowledge or skill by studying or experiencing." },
  { "word": "Least", "definition": "The smallest amount or smallest degree." },
  { "word": "Leave", "definition": "To go away from a place." },
  { "word": "Leg", "definition": "A limb used for walking or standing." },
  { "word": "Lemon", "definition": "A yellow, sour citrus fruit." },
  { "word": "Lend", "definition": "To give something to someone for a short time." },
  { "word": "Less", "definition": "A smaller amount." },
  { "word": "Lesson", "definition": "A period of teaching or instruction." },
  { "word": "Let", "definition": "To allow someone to do something." },
  { "word": "Letter", "definition": "A symbol in the alphabet, or a written message." },
  { "word": "Level", "definition": "A flat surface; a stage or rank." },
  { "word": "Lie", "definition": "To say something that is not true, or to rest flat on a surface." },
  { "word": "Life", "definition": "The period from being born to dying; existence." },
  { "word": "Lift", "definition": "To raise something to a higher position." },
  { "word": "Light", "definition": "The energy that makes things visible; the opposite of heavy." },
  { "word": "Like", "definition": "To find something pleasing, or similar to." },
  { "word": "Line", "definition": "A long, narrow mark, or a row of people or things." },
  { "word": "Lip", "definition": "One of the two fleshy parts surrounding the mouth." },
  { "word": "List", "definition": "A number of connected items written or printed one after another." },
  { "word": "Listen", "definition": "To pay attention to sounds with your ears." },
  { "word": "Little", "definition": "Small in size or amount." },
  { "word": "Live", "definition": "To be alive; to have a home in a place." },
  { "word": "Load", "definition": "A heavy or large amount of something carried." },
  { "word": "Local", "definition": "Relating to a particular area or neighborhood." },
  { "word": "Lock", "definition": "A device that keeps a door or container fastened shut." },
  { "word": "Long", "definition": "Measuring a great distance from end to end." },
  { "word": "Look", "definition": "To use your eyes to see." },
  { "word": "Loop", "definition": "A shape made by a line or rope curving back to cross itself." },
  { "word": "Loose", "definition": "Not firmly fixed in place; not tight." },
  { "word": "Lord", "definition": "A master or ruler." },
  { "word": "Lose", "definition": "To no longer have something; to be defeated in a game." },
  { "word": "Loss", "definition": "The state of losing or being lost." },
  { "word": "Lot", "definition": "A large amount or number of something." },
  { "word": "Loud", "definition": "Easy to hear because of high volume." },
  { "word": "Love", "definition": "A very strong feeling of affection." },
  { "word": "Low", "definition": "Close to the ground; not high." },
  { "word": "Luck", "definition": "Good or bad fortune." },
  { "word": "Lunch", "definition": "A meal eaten in the middle of the day." },
  { "word": "Lace", "definition": "A fine, decorative, open fabric, or a cord to tie shoes." },
  { "word": "Lantern", "definition": "A lamp in a protective covering with a handle." },
  { "word": "Library", "definition": "A building where books are kept for people to borrow." },
  { "word": "License", "definition": "An official permit to do something, like driving." },
  { "word": "Lizard", "definition": "A reptile with four legs and a long tail." },
  { "word": "Locate", "definition": "To find the exact position of something." },
  { "word": "Lollipop", "definition": "A hard candy on a stick." },
  { "word": "Luxury", "definition": "Something expensive that gives comfort and pleasure." },
  { "word": "Loyal", "definition": "Being faithful and committed to someone or something." },
  { "word": "Lava", "definition": "Hot, melted rock flowing from a volcano." },
  { "word": "Leather", "definition": "A material made from the skin of an animal." },
  { "word": "Legend", "definition": "An old story passed down that may or may not be true." },
  { "word": "Lemonade", "definition": "A sweet drink made with lemon juice and water." },
  { "word": "Leopard", "definition": "A large, spotted wild cat." },
  { "word": "Lever", "definition": "A bar used to lift or open a heavy object." },
  { "word": "Lighthouse", "definition": "A tall tower with a strong light to guide ships." },
  { "word": "Limit", "definition": "A point or boundary that cannot be passed." },
  { "word": "Llama", "definition": "A South American animal related to the camel." },
  { "word": "Log", "definition": "A section of a tree trunk that has been cut." },
  { "word": "Lotion", "definition": "A liquid cream rubbed into the skin." },
  { "word": "Lyric", "definition": "The words of a song." },
  { "word": "Ladder", "definition": "A frame with steps for climbing up and down." },
  { "word": "Lantern", "definition": "A lamp in a protective casing with a handle." },
  { "word": "Lecture", "definition": "An educational talk given to an audience." },
  { "word": "Locker", "definition": "A small cupboard with a lock, used for storage." },
  { "word": "Locomotive", "definition": "A powered rail vehicle used to pull trains." },
  { "word": "Lullaby", "definition": "A quiet song sung to help a child fall asleep." },
  { "word": "Luminous", "definition": "Shining brightly, especially in the dark." }
                ],
              'M': [
                { "word": "Machine", "definition": "A device with moving parts that does work." },
  { "word": "Mad", "definition": "Angry, or silly and crazy." },
  { "word": "Magic", "definition": "The power to make impossible things happen." },
  { "word": "Mail", "definition": "Letters and packages sent through a postal service." },
  { "word": "Main", "definition": "Most important or largest." },
  { "word": "Make", "definition": "To create or build something." },
  { "word": "Male", "definition": "Relating to men or boys." },
  { "word": "Man", "definition": "An adult male human." },
  { "word": "Manage", "definition": "To be in charge of or successfully control something." },
  { "word": "Many", "definition": "A large number of things." },
  { "word": "Map", "definition": "A drawing of an area, like a country or a city." },
  { "word": "March", "definition": "To walk with regular, measured steps." },
  { "word": "Mark", "definition": "A small spot or line, or a written symbol." },
  { "word": "Market", "definition": "A place where people buy and sell things." },
  { "word": "Married", "definition": "Joined in a special legal partnership." },
  { "word": "Master", "definition": "A person who is skilled or in control." },
  { "word": "Match", "definition": "To be the same as, or a small stick used to start a fire." },
  { "word": "Matter", "definition": "Anything that takes up space and has weight; a topic or problem." },
  { "word": "May", "definition": "Used to ask for permission, or the fifth month of the year." },
  { "word": "Me", "definition": "The word you use when you are the object of an action." },
  { "word": "Meal", "definition": "An occasion when food is eaten, like breakfast or dinner." },
  { "word": "Mean", "definition": "To intend to say; or to be unkind." },
  { "word": "Meat", "definition": "The flesh of an animal used as food." },
  { "word": "Medicine", "definition": "Something you take to treat sickness." },
  { "word": "Meet", "definition": "To come together with someone." },
  { "word": "Melt", "definition": "To turn from a solid to a liquid because of heat." },
  { "word": "Member", "definition": "A person belonging to a group or club." },
  { "word": "Memory", "definition": "The ability to recall past events." },
  { "word": "Men", "definition": "More than one adult male human." },
  { "word": "Mental", "definition": "Relating to the mind or thinking." },
  { "word": "Menu", "definition": "A list of food and drinks offered at a restaurant." },
  { "word": "Message", "definition": "A piece of information sent from one person to another." },
  { "word": "Metal", "definition": "A hard, shiny, solid material like iron or gold." },
  { "word": "Meter", "definition": "A unit of length, or a device that measures things." },
  { "word": "Middle", "definition": "The center point of something." },
  { "word": "Might", "definition": "Used to show possibility, or great strength." },
  { "word": "Mile", "definition": "A long unit of distance." },
  { "word": "Milk", "definition": "A white liquid produced by female mammals as food for their young." },
  { "word": "Mind", "definition": "The part of a person that thinks, feels, and remembers." },
  { "word": "Mine", "definition": "Belonging to me, or a deep hole dug to find minerals." },
  { "word": "Minute", "definition": "A unit of time equal to sixty seconds." },
  { "word": "Mirror", "definition": "A surface that reflects an image." },
  { "word": "Miss", "definition": "To fail to hit or catch, or to feel sad that someone is absent." },
  { "word": "Mistake", "definition": "An action or judgment that is wrong." },
  { "word": "Mix", "definition": "To put different things together." },
  { "word": "Model", "definition": "A small copy of something, or a person who shows clothes." },
  { "word": "Modern", "definition": "Relating to the present time; new." },
  { "word": "Mom", "definition": "A common name for a mother." },
  { "word": "Moment", "definition": "A very brief period of time." },
  { "word": "Money", "definition": "Coins or paper notes used to buy things." },
  { "word": "Month", "definition": "One of the twelve periods of time a year is divided into." },
  { "word": "Moon", "definition": "The natural object that orbits the Earth." },
  { "word": "Moral", "definition": "A lesson about right and wrong, or relating to what is right." },
  { "word": "More", "definition": "A greater amount or number." },
  { "word": "Morning", "definition": "The part of the day from sunrise to noon." },
  { "word": "Most", "definition": "The greatest amount or number." },
  { "word": "Mother", "definition": "A female parent." },
  { "word": "Motion", "definition": "The action of moving or changing position." },
  { "word": "Mountain", "definition": "A very large, high hill." },
  { "word": "Mouse", "definition": "A small rodent, or a device used with a computer." },
  { "word": "Mouth", "definition": "The opening in the face used for eating and speaking." },
  { "word": "Move", "definition": "To change place or position." },
  { "word": "Movie", "definition": "A series of images projected onto a screen." },
  { "word": "Much", "definition": "A large amount of something." },
  { "word": "Mud", "definition": "Soft, wet earth." },
  { "word": "Music", "definition": "Sounds arranged in a pleasing or expressive way." },
  { "word": "Must", "definition": "Used to say that something is required or necessary." },
  { "word": "My", "definition": "Belonging to me." },
  { "word": "Mystery", "definition": "Something that is difficult or impossible to understand or explain." },
  { "word": "Magic", "definition": "The art of producing surprising effects by impossible means." },
  { "word": "Magnet", "definition": "A piece of metal that can attract other metals." },
  { "word": "Major", "definition": "Very important or serious." },
  { "word": "Marble", "definition": "A hard, colorful rock, or a small glass ball used in a game." },
  { "word": "Mass", "definition": "A large body of material, or the weight of an object." },
  { "word": "Mature", "definition": "Fully developed or grown." },
  { "word": "Maximum", "definition": "The greatest amount or number possible." },
  { "word": "Measure", "definition": "To find the size, amount, or degree of something." },
  { "word": "Medium", "definition": "In the middle range of size, amount, or degree." },
  { "word": "Memory", "definition": "Something remembered from the past." },
  { "word": "Merge", "definition": "To combine or blend together." },
  { "word": "Messy", "definition": "Untidy or dirty." },
  { "word": "Mild", "definition": "Gentle and not severe or harsh." },
  { "word": "Mineral", "definition": "A naturally occurring solid substance found in the earth." },
  { "word": "Minimum", "definition": "The smallest amount or number possible." },
  { "word": "Minor", "definition": "Less important or serious." },
  { "word": "Misplace", "definition": "To put something in the wrong place and lose it." },
  { "word": "Moist", "definition": "Slightly wet; damp." },
  { "word": "Monitor", "definition": "A screen that shows images, or to watch and check on something." },
  { "word": "Multiply", "definition": "To increase in number or quantity; a math operation." },
  { "word": "Museum", "definition": "A building where objects of historical or scientific interest are kept." },
  { "word": "Mutter", "definition": "To say something in a low or unclear voice." },
  { "word": "Myth", "definition": "An ancient story that explains something about nature or history." }
                ],
              'N': [
                { "word": "Nail", "definition": "A small metal spike hammered into wood, or the hard part at the end of a finger." },
  { "word": "Name", "definition": "A word or set of words that a person or thing is known by." },
  { "word": "Nap", "definition": "A short sleep, usually during the day." },
  { "word": "Narrow", "definition": "Small in width; the opposite of wide." },
  { "word": "Nation", "definition": "A large group of people who share a common history and live in a country." },
  { "word": "Nature", "definition": "The world outside that is not made by people, like animals and plants." },
  { "word": "Near", "definition": "A short distance away; close by." },
  { "word": "Necessary", "definition": "Needed to be done or achieved; required." },
  { "word": "Neck", "definition": "The part of the body that joins the head to the shoulders." },
  { "word": "Need", "definition": "To require something because it is essential or very important." },
  { "word": "Negative", "definition": "Meaning 'no' or 'not true'; showing the bad side of something." },
  { "word": "Neighbor", "definition": "A person living next door or very close by." },
  { "word": "Neither", "definition": "Not one and not the other of two things." },
  { "word": "Nerve", "definition": "A thin fiber that sends messages between the brain and the body." },
  { "word": "Nest", "definition": "A place built by a bird or other animal to lay eggs or raise young." },
  { "word": "Net", "definition": "A material made of knotted string or wire with holes." },
  { "word": "Never", "definition": "Not ever; at no time." },
  { "word": "New", "definition": "Not existing before; recently made or found." },
  { "word": "News", "definition": "Information about recent events." },
  { "word": "Next", "definition": "Coming immediately after." },
  { "word": "Nice", "definition": "Pleasant, friendly, or attractive." },
  { "word": "Night", "definition": "The time between sunset and sunrise when it is dark." },
  { "word": "Nine", "definition": "The number that comes after eight." },
  { "word": "No", "definition": "A word used to refuse or disagree." },
  { "word": "Noise", "definition": "A sound, especially a loud or unpleasant one." },
  { "word": "None", "definition": "Not any of something." },
  { "word": "Normal", "definition": "Usual, standard, or expected." },
  { "word": "North", "definition": "One of the four main directions, opposite of south." },
  { "word": "Nose", "definition": "The part of the face used for breathing and smelling." },
  { "word": "Not", "definition": "A word used to make a statement negative." },
  { "word": "Note", "definition": "A short written message; a single sound in music." },
  { "word": "Nothing", "definition": "No single thing; the absence of anything." },
  { "word": "Notice", "definition": "To see or become aware of something." },
  { "word": "Noun", "definition": "A word that names a person, place, or thing." },
  { "word": "Now", "definition": "At the present moment." },
  { "word": "Number", "definition": "A symbol used to count or measure." },
  { "word": "Nurse", "definition": "A person trained to care for the sick or injured." },
  { "word": "Nut", "definition": "A dry fruit with a hard shell, or a small block of metal used with a bolt." },
  { "word": "Noodle", "definition": "A strip of pasta, often eaten in soup." },
  { "word": "Nail-polish", "definition": "A colored liquid applied to fingernails or toenails." },
  { "word": "Nanny", "definition": "A person employed to look after a child." },
  { "word": "Native", "definition": "Born in a particular place, or belonging there naturally." },
  { "word": "Navel", "definition": "The small hollow spot in the middle of your stomach; the belly button." },
  { "word": "Navy", "definition": "The part of a country's military that fights at sea; a dark blue color." },
  { "word": "Nebula", "definition": "A cloud of gas and dust in outer space." },
  { "word": "Needle", "definition": "A thin piece of metal with a sharp point, used for sewing." },
  { "word": "Nifty", "definition": "Particularly good, skillful, or clever." },
  { "word": "Nimble", "definition": "Quick and light in movement." },
  { "word": "Nocturnal", "definition": "Active mainly during the night." },
  { "word": "Nomad", "definition": "A person who moves from place to place instead of living in one spot." },
  { "word": "Nonstop", "definition": "Continuing without stopping." },
  { "word": "Noticeable", "definition": "Easy to see or observe." },
  { "word": "Nugget", "definition": "A small, lump of something, like gold or chicken." },
  { "word": "Numb", "definition": "Lacking feeling, usually because of cold or injury." },
  { "word": "Nursery", "definition": "A room for young children, or a place where plants are grown." },
  { "word": "Nutrition", "definition": "The process of taking in food for health and growth." },
  { "word": "Nylon", "definition": "A strong, light, and elastic plastic material." },
  { "word": "Nappy", "definition": "A cloth or disposable covering worn by a baby; a diaper." },
  { "word": "Nectar", "definition": "A sweet liquid produced by flowers." },
  { "word": "Nerd", "definition": "A person who is very interested in school subjects or a certain hobby (informal)." },
  { "word": "Neutral", "definition": "Not supporting either side in an argument or war." },
  { "word": "Nickname", "definition": "A familiar or funny name given to a person instead of their real name." },
  { "word": "Noble", "definition": "Having high moral qualities; grand and impressive." },
  { "word": "Nostril", "definition": "One of the two openings of the nose." },
  { "word": "Novel", "definition": "A long, fictional story, or something new and unusual." },
  { "word": "Nuisance", "definition": "A person or thing causing annoyance or trouble." },
  { "word": "Nuzzle", "definition": "To rub or push gently with the nose." },
  { "word": "Navigate", "definition": "To plan and direct the route of a ship, plane, or car." },
  { "word": "Nervous", "definition": "Easily worried and fearful; anxious." },
  { "word": "Nominate", "definition": "To suggest someone for an office, role, or award." },
  { "word": "Nostalgia", "definition": "A longing for a happy time or place in the past." },
  { "word": "Notion", "definition": "A general idea or belief." },
  { "word": "Numerous", "definition": "Many; a large number." },
  { "word": "Niche", "definition": "A comfortable or suitable position in life or work." },
  { "word": "Nightmare", "definition": "A frightening or unpleasant dream." },
  { "word": "Nip", "definition": "To pinch, bite, or snap lightly." },
  { "word": "Nonchalant", "definition": "Appearing calm and relaxed; not showing worry." },
  { "word": "Novelty", "definition": "The quality of being new, original, or unusual." },
  { "word": "Nullify", "definition": "To make something legally void or useless." },
  { "word": "Nymph", "definition": "A mythical spirit of nature, like a beautiful young woman." },
  { "word": "Nod", "definition": "To lower and raise your head quickly to show agreement or greeting." },
  { "word": "Nudge", "definition": "To gently push someone with your elbow to get their attention." },
  { "word": "Nugget", "definition": "A small, valuable lump, like a gold nugget." },
  { "word": "Numb", "definition": "Lacking feeling, often from cold or injury." },
  { "word": "Nurture", "definition": "To care for and encourage the growth of something." },
  { "word": "Nylon", "definition": "A strong, elastic synthetic material." }
                ],
              'O': [
                { "word": "Offer", "definition": "To present something for someone to accept or reject." },
  { "word": "Office", "definition": "A room or building where people work." },
  { "word": "Often", "definition": "Many times; frequently." },
  { "word": "Oil", "definition": "A thick, slippery liquid that can be burned for fuel." },
  { "word": "Old", "definition": "Having existed for a long time; not new." },
  { "word": "On", "definition": "In contact with a surface; working." },
  { "word": "Once", "definition": "One time, or at some time in the past." },
  { "word": "One", "definition": "The number before two; a single unit." },
  { "word": "Only", "definition": "Just one; no more than." },
  { "word": "Open", "definition": "To unlock or remove the cover; not closed." },
  { "word": "Operate", "definition": "To work or function; to control a machine." },
  { "word": "Opinion", "definition": "A person's thoughts or beliefs about something." },
  { "word": "Opposite", "definition": "Completely different; facing the other way." },
  { "word": "Or", "definition": "Used to introduce another choice or possibility." },
  { "word": "Orange", "definition": "A round, sweet citrus fruit, or the color of that fruit." },
  { "word": "Order", "definition": "To arrange things correctly, or a command." },
  { "word": "Ordinary", "definition": "Normal or common; not special." },
  { "word": "Organ", "definition": "A part of the body with a specific job, like the heart." },
  { "word": "Other", "definition": "Different from the one already mentioned." },
  { "word": "Ounce", "definition": "A very small unit of weight." },
  { "word": "Our", "definition": "Belonging to us." },
  { "word": "Out", "definition": "Away from the inside; outside." },
  { "word": "Outdoor", "definition": "Outside a building." },
  { "word": "Outer", "definition": "On the outside." },
  { "word": "Oven", "definition": "A kitchen appliance used for baking or roasting food." },
  { "word": "Over", "definition": "Above or across something; finished." },
  { "word": "Own", "definition": "To possess or belong to yourself." },
  { "word": "Ox", "definition": "A large animal similar to a bull, used for pulling carts." },
  { "word": "Oyster", "definition": "A sea animal with a hard shell, sometimes producing a pearl." },
  { "word": "Oblige", "definition": "To do something because you are asked or because it is a duty." },
  { "word": "Obscure", "definition": "Not discovered or known about; difficult to see clearly." },
  { "word": "Occasion", "definition": "A particular time or event." },
  { "word": "Occupied", "definition": "Being used or lived in." },
  { "word": "October", "definition": "The tenth month of the year." },
  { "word": "Official", "definition": "Related to a position of authority or a public duty." },
  { "word": "Omnivore", "definition": "An animal that eats both plants and meat." },
  { "word": "Orbit", "definition": "The curved path an object takes around a planet or star." },
  { "word": "Original", "definition": "Existing since the beginning; new and not a copy." },
  { "word": "Outlet", "definition": "A point in a wall where electrical devices can be connected." },
  { "word": "Outrage", "definition": "A feeling of great anger and shock." },
  { "word": "Overall", "definition": "Including everything; in general." },
  { "word": "Overcome", "definition": "To succeed in dealing with a problem or difficulty." },
  { "word": "Owe", "definition": "To be required to pay money to someone." },
  { "word": "Oxygen", "definition": "A gas that living things need to breathe." },
  { "word": "Oblong", "definition": "A shape that is longer than it is wide; rectangular." },
  { "word": "Obtain", "definition": "To get or acquire something." },
  { "word": "Occupant", "definition": "A person who lives or works in a place." },
  { "word": "Octopus", "definition": "A sea creature with a soft body and eight long arms." },
  { "word": "Online", "definition": "Connected to the internet." },
  { "word": "Opaque", "definition": "Not letting light shine through." },
  { "word": "Opportunity", "definition": "A set of circumstances that makes it possible to do something." },
  { "word": "Opt", "definition": "To choose one thing over another." },
  { "word": "Optimist", "definition": "A person who usually expects the best outcome." },
  { "word": "Outline", "definition": "A line that shows the shape of an object; a summary." },
  { "word": "Outlook", "definition": "A person's general way of thinking about things." },
  { "word": "Outpost", "definition": "A small settlement far away from the main group." },
  { "word": "Outstanding", "definition": "Extremely good; excellent." },
  { "word": "Overdue", "definition": "Not having arrived or been done by the expected time." },
  { "word": "Overlook", "definition": "To miss something, or to have a view from above." },
  { "word": "Oversee", "definition": "To supervise or manage a task or group." },
  { "word": "Overwhelm", "definition": "To affect deeply or defeat completely." },
  { "word": "Oval", "definition": "A round shape that is longer than it is wide, like an egg." },
  { "word": "Ouch", "definition": "A sound you make when you are hurt." },
  { "word": "Outfit", "definition": "A set of clothes worn together." },
  { "word": "Outgrow", "definition": "To become too big for something." },
  { "word": "Outlaw", "definition": "A criminal who is hiding from the law." },
  { "word": "Owner", "definition": "A person who owns something." },
  { "word": "Owl", "definition": "A bird of prey that hunts at night." },
  { "word": "Obsession", "definition": "Thinking about something constantly and too much." },
  { "word": "Octagon", "definition": "A shape with eight straight sides and eight angles." },
  { "word": "Opinionated", "definition": "Having very strong opinions and expressing them often." },
  { "word": "Opponent", "definition": "Someone who competes against you in a game or contest." },
  { "word": "Organize", "definition": "To arrange things in a neat, planned, or orderly way." },
  { "word": "Orphan", "definition": "A child whose parents are dead." },
  { "word": "Otherwise", "definition": "In a different way or in different circumstances." },
  { "word": "Outrageous", "definition": "Shockingly bad or extremely unfair." },
  { "word": "Overcast", "definition": "Covered with clouds; gray and cloudy." },
  { "word": "Overhear", "definition": "To accidentally hear what other people are saying." },
                ],
              'P': [
                { "word": "Pace", "definition": "A single step, or the speed of movement." },
  { "word": "Pack", "definition": "To place things into a container, or a group of animals." },
  { "word": "Page", "definition": "One side of a sheet of paper in a book." },
  { "word": "Pain", "definition": "An unpleasant feeling caused by injury or illness." },
  { "word": "Paint", "definition": "A colored liquid applied to a surface, or the act of applying it." },
  { "word": "Pair", "definition": "Two of something that belong together." },
  { "word": "Palace", "definition": "A large, beautiful house where a king or queen lives." },
  { "word": "Pan", "definition": "A metal container used for cooking." },
  { "word": "Paper", "definition": "Thin material made from wood pulp, used for writing or drawing." },
  { "word": "Parade", "definition": "A public procession of people walking or riding to celebrate something." },
  { "word": "Parent", "definition": "A mother or father." },
  { "word": "Park", "definition": "A large public green area for recreation." },
  { "word": "Part", "definition": "A piece or section of a whole." },
  { "word": "Party", "definition": "A social gathering for fun or celebration." },
  { "word": "Pass", "definition": "To move or go ahead of; to hand something to someone." },
  { "word": "Past", "definition": "The time that has already happened." },
  { "word": "Path", "definition": "A narrow way made by walking or built for a purpose." },
  { "word": "Pay", "definition": "To give money for goods or services." },
  { "word": "Peace", "definition": "Freedom from war and violence; quiet and calm." },
  { "word": "Peach", "definition": "A round, fuzzy fruit with sweet, yellow flesh." },
  { "word": "Peak", "definition": "The pointed top of a mountain." },
  { "word": "Pen", "definition": "A tool used for writing with ink." },
  { "word": "Pencil", "definition": "A tool used for writing or drawing with graphite." },
  { "word": "People", "definition": "Human beings in general." },
  { "word": "Perfect", "definition": "Having no flaws or mistakes; exactly right." },
  { "word": "Period", "definition": "A length of time." },
  { "word": "Permit", "definition": "To allow something to happen." },
  { "word": "Person", "definition": "A single human being." },
  { "word": "Pet", "definition": "A domesticated animal kept for company, like a dog or cat." },
  { "word": "Photo", "definition": "A picture made using a camera." },
  { "word": "Pick", "definition": "To choose, or to lift something up." },
  { "word": "Piece", "definition": "A part separated from a whole." },
  { "word": "Pig", "definition": "A pink or brown farm animal." },
  { "word": "Pillow", "definition": "A soft cushion for resting your head on." },
  { "word": "Pilot", "definition": "A person who operates the controls of an aircraft." },
  { "word": "Pin", "definition": "A thin piece of metal with a sharp point, used for fastening things." },
  { "word": "Pipe", "definition": "A long tube used for carrying water or gas." },
  { "word": "Place", "definition": "A particular position or area." },
  { "word": "Plan", "definition": "A detailed idea for doing something." },
  { "word": "Planet", "definition": "A large round object orbiting a star, like Earth." },
  { "word": "Plant", "definition": "A living thing that grows in the ground, like a tree or flower." },
  { "word": "Plate", "definition": "A flat dish for holding food." },
  { "word": "Play", "definition": "To take part in a game or activity for fun." },
  { "word": "Pleasant", "definition": "Enjoyable, attractive, or friendly." },
  { "word": "Please", "definition": "Used to ask for something politely." },
  { "word": "Pocket", "definition": "A small pouch sewn into clothing." },
  { "word": "Point", "definition": "The sharp end of something; a specific idea." },
  { "word": "Poison", "definition": "A substance that can cause sickness or death." },
  { "word": "Police", "definition": "The people who enforce laws and prevent crime." },
  { "word": "Pond", "definition": "A small body of still water." },
  { "word": "Pool", "definition": "A basin of water used for swimming." },
  { "word": "Poor", "definition": "Having very little money, or not good in quality." },
  { "word": "Pop", "definition": "A sudden, short, explosive sound; a fizzy drink." },
  { "word": "Popular", "definition": "Liked by many people." },
  { "word": "Post", "definition": "Mail; a vertical pole or pillar." },
  { "word": "Pot", "definition": "A round, deep container used for cooking or holding plants." },
  { "word": "Pound", "definition": "A unit of weight, or to hit repeatedly with force." },
  { "word": "Power", "definition": "The ability to do something or to control others." },
  { "word": "Practice", "definition": "To do something repeatedly to improve a skill." },
  { "word": "Praise", "definition": "To express approval or admiration for someone." },
  { "word": "Pray", "definition": "To speak to a god or spirit." },
  { "word": "Precious", "definition": "Of great value; loved and treasured." },
  { "word": "Prepare", "definition": "To make something ready for use or action." },
  { "word": "Present", "definition": "A gift; the time now; to show or introduce something." },
  { "word": "Pretty", "definition": "Attractive or pleasing to look at." },
  { "word": "Prevent", "definition": "To stop something from happening." },
  { "word": "Price", "definition": "The amount of money required to buy something." },
  { "word": "Pride", "definition": "A feeling of deep pleasure or satisfaction in one's own achievements." },
  { "word": "Prince", "definition": "The son of a king or queen." },
  { "word": "Print", "definition": "To produce words or pictures on paper using a machine." },
  { "word": "Prison", "definition": "A building where criminals are kept." },
  { "word": "Private", "definition": "For the use of one person or group; secret." },
  { "word": "Prize", "definition": "An award won in a competition." },
  { "word": "Problem", "definition": "A matter or situation that is difficult to deal with." },
  { "word": "Product", "definition": "Something that is made or grown to be sold." },
  { "word": "Promise", "definition": "To say that you will certainly do something." },
  { "word": "Proud", "definition": "Feeling satisfaction because of achievements or possessions." },
  { "word": "Prove", "definition": "To show that something is true." },
  { "word": "Pull", "definition": "To draw or drag something toward yourself." },
  { "word": "Pump", "definition": "A machine used to push liquid or air into or out of something." },
  { "word": "Punch", "definition": "To hit hard with your fist." },
  { "word": "Pup", "definition": "A young dog; a puppy." },
  { "word": "Pure", "definition": "Not mixed with anything else; clean and clear." },
  { "word": "Push", "definition": "To move something away from yourself." },
  { "word": "Put", "definition": "To move something to a specific position or place." },
  { "word": "Puzzle", "definition": "A game or toy designed to test cleverness." }
                ],
              'Q': [
                { "word": "Quack", "definition": "The sound a duck makes, or a fake doctor." },
  { "word": "Quad", "definition": "A short form for a square area, or something with four parts." },
  { "word": "Quake", "definition": "To shake or tremble violently, like an earthquake." },
  { "word": "Quality", "definition": "How good or bad something is." },
  { "word": "Quarter", "definition": "One of four equal parts; a 25-cent coin." },
  { "word": "Queen", "definition": "A female ruler of a country." },
  { "word": "Queer", "definition": "Strange or odd; different from what is usual." },
  { "word": "Quench", "definition": "To satisfy a thirst by drinking, or to put out a fire." },
  { "word": "Query", "definition": "A question or inquiry." },
  { "word": "Quest", "definition": "A long and difficult search for something." },
  { "word": "Question", "definition": "A sentence asking for information." },
  { "word": "Quick", "definition": "Fast in movement or time." },
  { "word": "Quiet", "definition": "Making little or no noise; silent." },
  { "word": "Quilt", "definition": "A warm blanket made by sewing two layers of cloth together with padding." },
  { "word": "Quit", "definition": "To stop doing something or give up a habit." },
  { "word": "Quite", "definition": "Completely, or very (like 'quite happy')." },
  { "word": "Quiz", "definition": "A short test." },
  { "word": "Quota", "definition": "A fixed number or amount of something that is required." },
  { "word": "Quiver", "definition": "To shake with a slight, rapid motion." },
  { "word": "Quarry", "definition": "A large pit dug into the earth to get stone or materials." },
  { "word": "Quaint", "definition": "Attractively old-fashioned or charmingly unusual." },
  { "word": "Quandary", "definition": "A state of confusion over what to do." },
  { "word": "Quantify", "definition": "To measure or express something as a number." },
  { "word": "Quarantine", "definition": "To keep sick people or animals apart to stop a disease from spreading." },
  { "word": "Quarrel", "definition": "An angry argument or disagreement." },
  { "word": "Quartz", "definition": "A very common, hard mineral that looks like clear or milky rock." },
  { "word": "Quell", "definition": "To put an end to something, often a rebellion or a bad feeling." },
  { "word": "Quip", "definition": "A witty or clever remark." },
  { "word": "Quirk", "definition": "A strange habit or unusual trait." },
  { "word": "Quibble", "definition": "To argue or complain about a small, unimportant matter." },
  { "word": "Quotient", "definition": "The answer to a division problem in math." },
  { "word": "Quash", "definition": "To officially reject or put down completely." },
  { "word": "Queasy", "definition": "Feeling sick to your stomach; nauseous." },
  { "word": "Quenchable", "definition": "Able to be satisfied, like a thirst." },
  { "word": "Questionnaire", "definition": "A list of questions used to gather information from many people." },
  { "word": "Queue", "definition": "A line of people or vehicles waiting for something." },
  { "word": "Quicken", "definition": "To make something faster or to become faster." },
  { "word": "Quickly", "definition": "Done in a fast way." },
  { "word": "Quietly", "definition": "Done with little to no noise." },
  { "word": "Quill", "definition": "A feather used as a pen, or a sharp spine of an animal like a porcupine." },
  { "word": "Quirkiness", "definition": "The state of being unusual or having funny habits." },
  { "word": "Quote", "definition": "To repeat words that someone else has said or written." },
  { "word": "Quota", "definition": "A fixed number or amount of something that is required." },
  { "word": "Quorum", "definition": "The minimum number of members needed to be present to vote." },
  { "word": "Quackery", "definition": "Dishonest practices that claim to have medical knowledge." },
  { "word": "Quandary", "definition": "A difficult situation where you don't know what to do." },
  { "word": "Quarry", "definition": "A large, deep pit where stone is dug out of the ground." },
  { "word": "Quart", "definition": "A unit of liquid measurement." },
  { "word": "Quash", "definition": "To put an end to something forcefully and completely." },
  { "word": "Queasy", "definition": "Feeling sick to your stomach; nauseous." },
  { "word": "Quirk", "definition": "A peculiar behavioral trait; a small oddity." },
  { "word": "Quibble", "definition": "To argue over small, unimportant things." },
  { "word": "Quiche", "definition": "A baked dish made with a crust and a filling of custard and cheese." },
  { "word": "Quick-witted", "definition": "Able to think and respond very fast and cleverly." },
  { "word": "Quitter", "definition": "A person who gives up easily." },
  { "word": "Quorum", "definition": "The minimum number of members needed to be present to vote." },
  { "word": "Quail", "definition": "A small bird often hunted for food." },
  { "word": "Quake", "definition": "To shake or tremble violently." },
  { "word": "Qualify", "definition": "To meet the requirements or conditions for something." },
  { "word": "Quantity", "definition": "The amount or number of something." },
  { "word": "Quarrelsome", "definition": "A person who often argues or fights." },
  { "word": "Questionable", "definition": "Doubtful or uncertain; perhaps not correct." },
  { "word": "Quickie", "definition": "Something done very fast." },
  { "word": "Quietude", "definition": "A state of rest, calm, and stillness." },
  { "word": "Quiver", "definition": "A container for holding arrows." },
  { "word": "Quotation", "definition": "The exact words someone has said or written." },
  { "word": "Quarry", "definition": "An object or person that is hunted or searched for." },
  { "word": "Quasar", "definition": "A very bright, distant object in space that looks like a star." },
  { "word": "Quell", "definition": "To put an end to something, often a bad feeling." },
  { "word": "Querulous", "definition": "Complaining in a whining, cranky way." },
  { "word": "Quirk", "definition": "A strange habit or funny unusual trait." },
  { "word": "Quicken", "definition": "To speed up or make faster." },
  { "word": "Quaintness", "definition": "The quality of being charmingly old-fashioned." },
  { "word": "Quake-proof", "definition": "Built to withstand earthquakes." },
  { "word": "Quadruple", "definition": "To multiply by four; four times as much." },
  { "word": "Quarry", "definition": "A large, deep pit where stone is dug out of the ground." },
  { "word": "Queenly", "definition": "Like a queen; noble and dignified." },
  { "word": "Questing", "definition": "The act of searching for something important." },
  { "word": "Quietly", "definition": "Done without making much noise." },
  { "word": "Quiltmaker", "definition": "A person who makes quilts." },
  { "word": "Quittance", "definition": "A release from a debt or obligation." },
  { "word": "Quipster", "definition": "A person who often makes clever, witty remarks." },
  { "word": "Quiver", "definition": "To shake with a slight, rapid motion." },
  { "word": "Quixotic", "definition": "Very idealistic but not practical." },
  { "word": "Quizzical", "definition": "Expressing confusion, doubt, or curiosity." },
  { "word": "Quoin", "definition": "An external angle of a wall or building." },
  { "word": "Quoit", "definition": "A flat ring used in a throwing game." }
                ],
              'R': [
                { "word": "Rabbit", "definition": "A small, furry animal with long ears that hops." },
  { "word": "Race", "definition": "A competition of speed, or a group of people with shared features." },
  { "word": "Radio", "definition": "A device that receives sounds broadcast through the air." },
  { "word": "Raft", "definition": "A flat structure, usually of logs, used for floating on water." },
  { "word": "Rag", "definition": "A piece of old, torn cloth." },
  { "word": "Rail", "definition": "A bar or track for trains to run on." },
  { "word": "Rain", "definition": "Water falling from the sky in drops." },
  { "word": "Raise", "definition": "To lift up or move to a higher position; to grow." },
  { "word": "Range", "definition": "The area covered by something; a set of different things." },
  { "word": "Rank", "definition": "A position in a series or hierarchy." },
  { "word": "Rapid", "definition": "Happening quickly or fast." },
  { "word": "Rare", "definition": "Not common; seldom seen or found." },
  { "word": "Rat", "definition": "A large rodent with a long tail." },
  { "word": "Rate", "definition": "A measure of speed or frequency." },
  { "word": "Raw", "definition": "Not cooked; in its natural state." },
  { "word": "Reach", "definition": "To stretch out an arm to touch or grab something." },
  { "word": "Read", "definition": "To look at and understand the meaning of written words." },
  { "word": "Ready", "definition": "Prepared for an action or event." },
  { "word": "Real", "definition": "Actually existing; not imagined or fake." },
  { "word": "Reason", "definition": "A cause, explanation, or justification for an action." },
  { "word": "Receive", "definition": "To be given something." },
  { "word": "Recent", "definition": "Having happened or started only a short time ago." },
  { "word": "Recognize", "definition": "To know someone or something because you have seen or heard it before." },
  { "word": "Record", "definition": "To write down or save information; a vinyl disc for music." },
  { "word": "Red", "definition": "A primary color, like the color of blood or a stop sign." },
  { "word": "Refuse", "definition": "To say no to something; to reject." },
  { "word": "Region", "definition": "A large area of land." },
  { "word": "Regular", "definition": "Following a pattern; happening often." },
  { "word": "Reject", "definition": "To refuse to accept or consider something." },
  { "word": "Relate", "definition": "To connect to or have a connection with something else." },
  { "word": "Relax", "definition": "To become less tense or nervous." },
  { "word": "Release", "definition": "To let go of something or set it free." },
  { "word": "Remember", "definition": "To bring back an image or idea from the past to your mind." },
  { "word": "Repair", "definition": "To fix something that is broken or damaged." },
  { "word": "Repeat", "definition": "To say or do something again." },
  { "word": "Reply", "definition": "To answer a question or letter." },
  { "word": "Report", "definition": "To give a formal account of something seen or heard." },
  { "word": "Represent", "definition": "To stand for or act on behalf of someone or something." },
  { "word": "Require", "definition": "To need something essential." },
  { "word": "Respect", "definition": "A feeling of deep admiration for someone or something." },
  { "word": "Rest", "definition": "To stop working or moving to relax." },
  { "word": "Result", "definition": "An outcome or effect of an action." },
  { "word": "Return", "definition": "To go back to a place, or to give something back." },
  { "word": "Reveal", "definition": "To show or make known something that was secret." },
  { "word": "Rich", "definition": "Having a lot of money or valuable things." },
  { "word": "Ride", "definition": "To travel in or on a vehicle or animal." },
  { "word": "Right", "definition": "Correct or true; the opposite of left." },
  { "word": "Ring", "definition": "A small circle worn on a finger; a circular sound." },
  { "word": "Rise", "definition": "To move from a lower position to a higher one." },
  { "word": "River", "definition": "A large natural stream of water flowing to the sea or a lake." },
  { "word": "Road", "definition": "A wide way between places used by cars and other vehicles." },
  { "word": "Rock", "definition": "A hard, solid material found in the ground." },
  { "word": "Role", "definition": "The part played by a person in a situation or a play." },
  { "word": "Roof", "definition": "The structure forming the top covering of a building." },
  { "word": "Room", "definition": "A section or area within a building." },
  { "word": "Rope", "definition": "A thick cord, usually made of twisted fibers." },
  { "word": "Rough", "definition": "Having an uneven or bumpy surface; not gentle." },
  { "word": "Round", "definition": "Shaped like a circle or sphere." },
  { "word": "Route", "definition": "A way or course taken to get from one place to another." },
  { "word": "Row", "definition": "A number of people or things in a straight line." },
  { "word": "Rub", "definition": "To move one object against another with pressure." },
  { "word": "Rule", "definition": "A set of regulations or instructions that must be followed." },
  { "word": "Run", "definition": "To move rapidly on foot." },
  { "word": "Rush", "definition": "To move or act with great speed." },
  { "word": "Rust", "definition": "A reddish-brown coating that forms on iron when exposed to air and water." },
  { "word": "Rage", "definition": "A very strong and violent anger." },
  { "word": "Rally", "definition": "A large public meeting to support a cause, or to recover." },
  { "word": "Ramble", "definition": "To talk or write at length in a confused, wandering way." },
  { "word": "Ranch", "definition": "A large farm used for raising cattle or horses." },
  { "word": "Random", "definition": "Made or chosen without a plan or purpose." },
  { "word": "Razor", "definition": "A sharp-bladed tool used for shaving hair." },
  { "word": "Realm", "definition": "A kingdom, or an area of interest or activity." },
  { "word": "Rebate", "definition": "A partial refund of the cost of a product." },
  { "word": "Rebel", "definition": "A person who fights against the rules or government." },
  { "word": "Recipe", "definition": "A set of instructions for preparing food." },
  { "word": "Recycle", "definition": "To convert waste material into reusable material." },
  { "word": "Reflect", "definition": "To throw back light, heat, or sound; to think deeply." },
  { "word": "Refuge", "definition": "A safe place or shelter from danger." },
  { "word": "Regret", "definition": "To feel sad, disappointed, or repentant about something that happened." },
  { "word": "Relief", "definition": "A feeling of ease after pain or stress is gone." },
  { "word": "Remark", "definition": "A short comment or statement." },
  { "word": "Remind", "definition": "To cause someone to remember something." },
  { "word": "Remove", "definition": "To take something away or off." },
  { "word": "Renovate", "definition": "To restore something old to a good state of repair." },
  { "word": "Rescue", "definition": "To save someone from a dangerous or difficult situation." },
  { "word": "Reserve", "definition": "To set something aside for future use." },
  { "word": "Resign", "definition": "To officially quit a job or position." },
  { "word": "Retire", "definition": "To stop working because of old age." },
  { "word": "Reward", "definition": "A prize for an action or service." },
  { "word": "Rhinestone", "definition": "A fake diamond made of shiny, clear glass." },
  { "word": "Rhythm", "definition": "A strong, regular, repeated pattern of sound or movement." },
  { "word": "Riddle", "definition": "A question or statement that is difficult to understand; a puzzle." },
  { "word": "Ritual", "definition": "A set of actions always done in the same way." }
                ],
              'S': [
                { "word": "Sad", "definition": "Feeling unhappy or sorrowful." },
  { "word": "Safe", "definition": "Protected from danger or harm." },
  { "word": "Sail", "definition": "To travel across water in a boat; the cloth used to catch wind." },
  { "word": "Salt", "definition": "A white substance used to flavor and preserve food." },
  { "word": "Same", "definition": "Identical; not different." },
  { "word": "Sand", "definition": "Tiny pieces of rock found on beaches and in deserts." },
  { "word": "Save", "definition": "To keep something safe; to store money or data." },
  { "word": "Say", "definition": "To speak words." },
  { "word": "School", "definition": "A place where children go to learn." },
  { "word": "Science", "definition": "The study of the natural world through observation and experiment." },
  { "word": "Score", "definition": "The number of points a team or player has in a game." },
  { "word": "Scout", "definition": "A person sent out to gather information, or a member of a youth organization." },
  { "word": "Screen", "definition": "A flat surface where images are projected, like a TV or computer monitor." },
  { "word": "Sea", "definition": "A large body of salt water, smaller than an ocean." },
  { "word": "Search", "definition": "To look for something carefully." },
  { "word": "Season", "definition": "One of the four main periods of the year (spring, summer, fall, winter)." },
  { "word": "Seat", "definition": "A place where someone can sit." },
  { "word": "Second", "definition": "Coming after the first; a very small unit of time." },
  { "word": "Secret", "definition": "Something that is kept hidden or known only by a few people." },
  { "word": "See", "definition": "To look at something with your eyes." },
  { "word": "Seed", "definition": "A small object produced by a plant that can grow into a new plant." },
  { "word": "Seek", "definition": "To try to find or obtain something." },
  { "word": "Seem", "definition": "To appear to be something." },
  { "word": "Sell", "definition": "To give something in exchange for money." },
  { "word": "Send", "definition": "To cause something to go to a different place." },
  { "word": "Sense", "definition": "Any of the five physical abilities (sight, smell, hearing, taste, touch)." },
  { "word": "Separate", "definition": "To move or keep apart." },
  { "word": "Serious", "definition": "Thoughtful, solemn, or important and not joking." },
  { "word": "Serve", "definition": "To perform a duty; to give food or drinks to someone." },
  { "word": "Set", "definition": "To place something in a particular position; a group of similar things." },
  { "word": "Seven", "definition": "The number that comes after six." },
  { "word": "Several", "definition": "More than two but not many." },
  { "word": "Shake", "definition": "To move quickly and often from side to side or up and down." },
  { "word": "Shape", "definition": "The outer form or outline of something." },
  { "word": "Share", "definition": "To have or use something with others." },
  { "word": "Sharp", "definition": "Having a fine point or edge; intelligent." },
  { "word": "She", "definition": "A word used for a female person or girl." },
  { "word": "Sheep", "definition": "A farm animal with thick wool." },
  { "word": "Shelf", "definition": "A flat board attached to a wall or frame for holding things." },
  { "word": "Shell", "definition": "The hard outer covering of some animals or eggs." },
  { "word": "Shine", "definition": "To give off or reflect light." },
  { "word": "Ship", "definition": "A large boat used for traveling across the sea." },
  { "word": "Shirt", "definition": "A piece of clothing for the upper body." },
  { "word": "Shock", "definition": "A sudden, powerful feeling of surprise or distress." },
  { "word": "Shoe", "definition": "A covering for the foot." },
  { "word": "Shoot", "definition": "To fire a gun, or to move quickly." },
  { "word": "Shop", "definition": "A place where goods are sold; to buy things." },
  { "word": "Short", "definition": "Not long; small in height." },
  { "word": "Should", "definition": "Used to say what is correct or best to do." },
  { "word": "Show", "definition": "To let someone see something; an entertainment performance." },
  { "word": "Shut", "definition": "To close." },
  { "word": "Sick", "definition": "Ill or unwell." },
  { "word": "Side", "definition": "A flat area or part of an object; a position next to another." },
  { "word": "Sign", "definition": "A mark or object that gives information; to write your name." },
  { "word": "Silent", "definition": "Making or having no sound; quiet." },
  { "word": "Simple", "definition": "Easy to understand or do; not complicated." },
  { "word": "Since", "definition": "From a particular time until now." },
  { "word": "Sing", "definition": "To make musical sounds with your voice." },
  { "word": "Single", "definition": "Only one." },
  { "word": "Sister", "definition": "A female sibling." },
  { "word": "Sit", "definition": "To rest your body on a seat." },
  { "word": "Six", "definition": "The number that comes after five." },
  { "word": "Size", "definition": "How big or small something is." },
  { "word": "Skill", "definition": "The ability to do something well." },
  { "word": "Skin", "definition": "The outer covering of the human or animal body." },
  { "word": "Skirt", "definition": "A woman's or girl's garment that hangs from the waist." },
  { "word": "Sky", "definition": "The space above the Earth where clouds and the sun are seen." },
  { "word": "Sleep", "definition": "A natural, resting state where your eyes are closed and you are unconscious." },
  { "word": "Slide", "definition": "To move smoothly along a surface." },
  { "word": "Slow", "definition": "Moving at a low speed; not fast." },
  { "word": "Small", "definition": "Little in size; the opposite of big." },
  { "word": "Smart", "definition": "Intelligent or clever." },
  { "word": "Smell", "definition": "To sense odors with your nose; the odor itself." },
  { "word": "Smile", "definition": "To turn the corners of your mouth up to show happiness." },
  { "word": "Smoke", "definition": "A visible mass of gas and soot from a fire." },
  { "word": "Smooth", "definition": "Having an even surface; not rough." },
  { "word": "Snake", "definition": "A long, limbless reptile." },
  { "word": "Snap", "definition": "To break suddenly with a sharp sound." },
  { "word": "Snow", "definition": "Small, white flakes of ice that fall from the sky." },
  { "word": "So", "definition": "To a great extent; for that reason." },
  { "word": "Soap", "definition": "A substance used with water for washing and cleaning." },
  { "word": "Soft", "definition": "Easy to press or bend; gentle." },
  { "word": "Soil", "definition": "The top layer of the Earth in which plants grow; dirt." },
  { "word": "Solar", "definition": "Relating to the sun." },
  { "word": "Solid", "definition": "Firm and stable in shape; not liquid or gas." },
  { "word": "Some", "definition": "An unspecified amount or number." },
  { "word": "Son", "definition": "A male child." },
  { "word": "Song", "definition": "A short poem or words set to music." },
  { "word": "Soon", "definition": "In a short time." },
  { "word": "Sorry", "definition": "Feeling regret or sympathy." },
  { "word": "Sort", "definition": "A category or kind; to arrange according to type." },
  { "word": "Sound", "definition": "Vibrations that travel through the air or water and can be heard." },
  { "word": "Soup", "definition": "A liquid food made by cooking meat, fish, or vegetables in water." },
  { "word": "South", "definition": "One of the four main directions, opposite of north." },
  { "word": "Space", "definition": "The area beyond the Earth's atmosphere; an area for something." },
  { "word": "Speak", "definition": "To say words; to talk." },
  { "word": "Special", "definition": "Better, greater, or otherwise different from what is usual." },
  { "word": "Speech", "definition": "The ability to speak, or a formal talk." },
  { "word": "Speed", "definition": "The rate at which someone or something moves." },
  { "word": "Spell", "definition": "To write or name the letters of a word." },
  { "word": "Spend", "definition": "To use money to pay for something; to use time." },
  { "word": "Spider", "definition": "A small creature with eight legs that makes webs." },
  { "word": "Spirit", "definition": "The part of a person that is not physical; courage or enthusiasm." }
                ],
              'T': [
                { "word": "Table", "definition": "A piece of furniture with a flat top and legs, used for eating or working." },
  { "word": "Tail", "definition": "A part of an animal's body that extends from the back end." },
  { "word": "Take", "definition": "To move something into your hands or possession." },
  { "word": "Talk", "definition": "To speak to someone." },
  { "word": "Tall", "definition": "Of great height." },
  { "word": "Tap", "definition": "To hit something lightly and quickly; a faucet." },
  { "word": "Taste", "definition": "The sense that lets you detect flavor with your tongue." },
  { "word": "Tax", "definition": "Money that people must pay to the government." },
  { "word": "Tea", "definition": "A drink made by soaking leaves in hot water." },
  { "word": "Teach", "definition": "To show or explain how to do something; to instruct." },
  { "word": "Team", "definition": "A group of people working together in a sport or activity." },
  { "word": "Tear", "definition": "To rip or pull apart; a drop of water from the eye." },
  { "word": "Teen", "definition": "A person between the ages of 13 and 19." },
  { "word": "Teeth", "definition": "The hard, white parts in the mouth used for chewing." },
  { "word": "Tell", "definition": "To communicate information or a story." },
  { "word": "Ten", "definition": "The number that comes after nine." },
  { "word": "Tense", "definition": "Stretched tight or strained; feeling nervous." },
  { "word": "Tent", "definition": "A portable shelter made of cloth or plastic, held up by poles." },
  { "word": "Term", "definition": "A word or phrase; a fixed period of time." },
  { "word": "Terrible", "definition": "Extremely bad or severe." },
  { "word": "Test", "definition": "A procedure to find out the quality or ability of someone or something." },
  { "word": "Than", "definition": "Used to introduce the second part of a comparison (e.g., 'bigger than')." },
  { "word": "Thank", "definition": "To express gratitude or appreciation." },
  { "word": "That", "definition": "Used to point to a specific person, thing, or idea." },
  { "word": "The", "definition": "A word used before a noun to refer to a specific one." },
  { "word": "Their", "definition": "Belonging to them." },
  { "word": "Them", "definition": "Used as the object of a verb or preposition to refer to people." },
  { "word": "Then", "definition": "At that time; next in a series." },
  { "word": "There", "definition": "In or at that place." },
  { "word": "These", "definition": "Used to point to multiple people or things near you." },
  { "word": "They", "definition": "Used to refer to two or more people or things." },
  { "word": "Thick", "definition": "Having a large distance between opposite sides; not thin." },
  { "word": "Thing", "definition": "An object, fact, or matter." },
  { "word": "Think", "definition": "To use your mind to consider or reason." },
  { "word": "Third", "definition": "Coming after the second." },
  { "word": "This", "definition": "Used to point to a single person or thing near you." },
  { "word": "Those", "definition": "Used to point to multiple people or things farther away." },
  { "word": "Though", "definition": "Despite the fact that; although." },
  { "word": "Thought", "definition": "An idea or opinion produced by thinking." },
  { "word": "Three", "definition": "The number that comes after two." },
  { "word": "Through", "definition": "Moving from one side of something to the other." },
  { "word": "Throw", "definition": "To propel something through the air with force." },
  { "word": "Tie", "definition": "To fasten with a knot; a strip of cloth worn around the neck." },
  { "word": "Tiger", "definition": "A large, striped wild cat." },
  { "word": "Tight", "definition": "Firmly fixed or drawn together; not loose." },
  { "word": "Time", "definition": "The ongoing sequence of events; a moment or period." },
  { "word": "Tiny", "definition": "Extremely small." },
  { "word": "Tip", "definition": "The pointed end of something; a useful suggestion." },
  { "word": "Tired", "definition": "Feeling a need to rest or sleep." },
  { "word": "To", "definition": "Used to show movement or direction toward a place." },
  { "word": "Today", "definition": "This present day." },
  { "word": "Together", "definition": "In the same place or at the same time." },
  { "word": "Told", "definition": "Past tense of 'tell'; communicated information." },
  { "word": "Tomorrow", "definition": "The day after today." },
  { "word": "Tone", "definition": "The general character or attitude expressed by a voice or writing." },
  { "word": "Tongue", "definition": "The fleshy organ in the mouth used for tasting and speaking." },
  { "word": "Too", "definition": "In addition; more than enough." },
  { "word": "Tool", "definition": "A device or implement used to carry out a particular function." },
  { "word": "Tooth", "definition": "A hard, bony structure in the mouth used for biting and chewing." },
  { "word": "Top", "definition": "The highest part or point of something." },
  { "word": "Total", "definition": "The whole number or amount." },
  { "word": "Touch", "definition": "To make physical contact with something." },
  { "word": "Tough", "definition": "Strong enough to withstand hard conditions; difficult." },
  { "word": "Town", "definition": "A place where people live and work, smaller than a city." },
  { "word": "Toy", "definition": "An object for a child to play with." },
  { "word": "Track", "definition": "A path or trail; to follow the movement of someone or something." },
  { "word": "Trade", "definition": "The action of buying and selling goods; a specific job or skill." },
  { "word": "Train", "definition": "A series of connected railway cars; to teach a skill." },
  { "word": "Trap", "definition": "A device or hole used for catching animals; to catch someone." },
  { "word": "Travel", "definition": "To go on a journey." },
  { "word": "Treat", "definition": "To behave toward someone; a sweet snack." },
  { "word": "Tree", "definition": "A large plant with a single wooden trunk and branches." },
  { "word": "Trick", "definition": "A clever or playful action meant to deceive or amuse." },
  { "word": "Trip", "definition": "A journey; to fall over." },
  { "word": "True", "definition": "In accordance with fact or reality; real." },
  { "word": "Try", "definition": "To attempt to do something." },
  { "word": "Tube", "definition": "A long, hollow cylinder for carrying liquid or gas." },
  { "word": "Turn", "definition": "To move in a circle around a fixed point." },
  { "word": "Twelve", "definition": "The number that comes after eleven." },
  { "word": "Twenty", "definition": "The number equal to two sets of ten." },
  { "word": "Two", "definition": "The number that comes after one." },
  { "word": "Type", "definition": "A category of people or things; to write using a keyboard." }
                ],
              'U': [
                { "word": "Ugly", "definition": "Unpleasant or unattractive to look at." },
  { "word": "Ultimate", "definition": "The final or most important part." },
  { "word": "Umbrella", "definition": "A device used to protect from rain or sun." },
  { "word": "Unable", "definition": "Lacking the power or skill to do something." },
  { "word": "Unbelievable", "definition": "Difficult to accept as true; amazing." },
  { "word": "Uncertain", "definition": "Not sure or not definitely known." },
  { "word": "Uncle", "definition": "The brother of your mother or father." },
  { "word": "Under", "definition": "In a position below or beneath something." },
  { "word": "Understand", "definition": "To know the meaning of something." },
  { "word": "Undertake", "definition": "To take on a task or responsibility." },
  { "word": "Underwater", "definition": "Located or carried out beneath the surface of the water." },
  { "word": "Uniform", "definition": "A special set of clothes worn by a group of people, like soldiers or students." },
  { "word": "Unit", "definition": "A single, separate piece or object." },
  { "word": "United", "definition": "Joined together as one group or team." },
  { "word": "Universal", "definition": "Relating to everyone or everything." },
  { "word": "Unless", "definition": "Except if; only if not." },
  { "word": "Unlike", "definition": "Different from; not similar to." },
  { "word": "Until", "definition": "Up to the time that; before a certain time." },
  { "word": "Unusual", "definition": "Not common or ordinary; strange." },
  { "word": "Up", "definition": "To a higher level or position." },
  { "word": "Upon", "definition": "On top of something." },
  { "word": "Upper", "definition": "Located on a higher level." },
  { "word": "Upset", "definition": "Unhappy, disappointed, or angry." },
  { "word": "Upstairs", "definition": "On a higher floor of a building." },
  { "word": "Urgent", "definition": "Requiring immediate action or attention." },
  { "word": "Us", "definition": "The word used when speaking about yourself and others." },
  { "word": "Use", "definition": "To put something into action or service." },
  { "word": "Useful", "definition": "Able to be used for a practical purpose." },
  { "word": "Usual", "definition": "Normal, regular, or customary." },
  { "word": "Utter", "definition": "To say or speak something; complete or total." },
  { "word": "U-turn", "definition": "The turning of a vehicle in a semicircle to go back the way it came." },
  { "word": "Umpire", "definition": "A person who enforces the rules in certain sports like baseball." },
  { "word": "Unpack", "definition": "To take things out of a container or luggage." },
  { "word": "Unsure", "definition": "Not confident or certain; doubtful." },
  { "word": "Update", "definition": "To give the most recent information; a newer version." },
  { "word": "Urge", "definition": "A strong desire or need to do something." },
  { "word": "Utensil", "definition": "A tool or instrument used, especially in the kitchen." },
  { "word": "Unicorn", "definition": "A mythical creature, usually a horse with one horn on its head." },
  { "word": "Unite", "definition": "To come together for a common purpose." },
  { "word": "Unfair", "definition": "Not right or just; not treating everyone equally." },
  { "word": "Unfold", "definition": "To open or spread out something that was folded." },
  { "word": "Unhappy", "definition": "Sad; not joyful." },
  { "word": "Unique", "definition": "Being the only one of its kind." },
  { "word": "Unplug", "definition": "To disconnect an electrical appliance by pulling the plug out." },
  { "word": "Untidy", "definition": "Messy or not neat." },
  { "word": "Upcoming", "definition": "Happening soon." },
  { "word": "Upfront", "definition": "Paid in advance, or honest and direct." },
  { "word": "Usage", "definition": "The action of using something." },
  { "word": "Utility", "definition": "The state of being useful or helpful." },
  { "word": "Ultimate", "definition": "The greatest or extreme limit." },
  { "word": "Uncover", "definition": "To remove a covering from, or discover something secret." },
  { "word": "Undertake", "definition": "To take on a task or enterprise." },
  { "word": "Unicorn", "definition": "A mythical horse with one horn on its head." },
  { "word": "Uplift", "definition": "To raise the spirit or morale; to inspire." },
  { "word": "Uproar", "definition": "A loud, confused noise or disturbance." },
  { "word": "Urban", "definition": "Relating to a city or town." },
  { "word": "Urchin", "definition": "A poor and often mischievous child, or a sea creature." },
  { "word": "Uterus", "definition": "The organ in a female body where a baby grows." },
  { "word": "Utterance", "definition": "A spoken word or statement." },
  { "word": "Unbroken", "definition": "Not damaged or interrupted; complete." },
  { "word": "Uncork", "definition": "To remove the cork from a bottle." },
  { "word": "Undergo", "definition": "To experience or be subjected to something." },
  { "word": "Underline", "definition": "To draw a line beneath a word or phrase." },
  { "word": "Undermine", "definition": "To weaken something gradually." },
  { "word": "Underneath", "definition": "Directly below; under." },
  { "word": "Unemployed", "definition": "Without a job." },
  { "word": "Unfasten", "definition": "To open or loosen something that was closed or tied." },
  { "word": "Unfit", "definition": "Not suitable or good enough." },
  { "word": "Unforgettable", "definition": "Impossible to forget." },
  { "word": "Unfold", "definition": "To open or spread out something that was folded." },
  { "word": "Unhealthy", "definition": "Not good for your health." },
  { "word": "Unify", "definition": "To make or become united or single." },
  { "word": "Unison", "definition": "Speaking or singing at the same time." },
  { "word": "Unload", "definition": "To remove goods or contents from a vehicle." },
  { "word": "Unreal", "definition": "Imaginary or not seeming real." },
  { "word": "Unripe", "definition": "Not ready to be eaten; not fully mature." },
  { "word": "Unselfish", "definition": "Putting other people's needs before your own." },
  { "word": "Unsteady", "definition": "Not firm or stable; shaky." },
  { "word": "Unwrap", "definition": "To remove the paper or covering from something." },
  { "word": "Upgrade", "definition": "To improve something by adding a newer or better part." },
  { "word": "Uphill", "definition": "Toward a higher place; difficult." },
  { "word": "Uplift", "definition": "To raise up or improve someone's spirits." },
  { "word": "Urban", "definition": "Relating to a city or town." },
  { "word": "Usage", "definition": "The action of using something." },
  { "word": "Usher", "definition": "A person who shows people to their seats." },
  { "word": "Utility", "definition": "The state of being useful, or a public service like electricity." }
                ],
              'V': [
                { "word": "Vacant", "definition": "Empty or not occupied." },
  { "word": "Vacuum", "definition": "A space entirely empty of matter; a machine that cleans floors." },
  { "word": "Vague", "definition": "Uncertain, unclear, or not specific." },
  { "word": "Valid", "definition": "Based on truth or fact; acceptable." },
  { "word": "Valley", "definition": "A low area of land between hills or mountains." },
  { "word": "Value", "definition": "The importance or worth of something; to consider something important." },
  { "word": "Van", "definition": "A large vehicle used for transporting goods or people." },
  { "word": "Vanish", "definition": "To disappear suddenly and completely." },
  { "word": "Various", "definition": "Different kinds of things." },
  { "word": "Vegetable", "definition": "A plant or part of a plant used as food, like carrots or broccoli." },
  { "word": "Vehicle", "definition": "A machine used for transporting people or goods, like a car or bus." },
  { "word": "Velvet", "definition": "A type of fabric with a thick, soft surface." },
  { "word": "Venture", "definition": "A risky or daring journey or business idea." },
  { "word": "Verb", "definition": "A word that describes an action, state, or occurrence (like 'run' or 'feel')." },
  { "word": "Verse", "definition": "Writing arranged in a rhythmic pattern, like a line of poetry." },
  { "word": "Version", "definition": "A particular form of something that is slightly different from others." },
  { "word": "Very", "definition": "To a great degree; extremely." },
  { "word": "Vessel", "definition": "A ship or large boat; a hollow container, like a cup." },
  { "word": "Veteran", "definition": "A person who has served in the military." },
  { "word": "Vibrate", "definition": "To move continuously and rapidly back and forth." },
  { "word": "Victim", "definition": "A person who has been harmed or injured." },
  { "word": "Victory", "definition": "The act of winning a battle or game; triumph." },
  { "word": "View", "definition": "What you can see from a particular place; an opinion." },
  { "word": "Village", "definition": "A small group of houses in a country area." },
  { "word": "Violent", "definition": "Using or involving physical force to hurt or damage." },
  { "word": "Violet", "definition": "A color between blue and red; a small flower." },
  { "word": "Virus", "definition": "A tiny particle that can infect living cells and cause disease." },
  { "word": "Visit", "definition": "To go to see a person or place." },
  { "word": "Voice", "definition": "The sound produced by the mouth when speaking or singing." },
  { "word": "Volume", "definition": "The amount of space an object takes up; the loudness of a sound." },
  { "word": "Volunteer", "definition": "A person who offers to do a job without being paid." },
  { "word": "Vote", "definition": "To formally express a choice, like for a person or idea." },
  { "word": "Voyage", "definition": "A long journey involving travel by sea or in space." },
  { "word": "Vulture", "definition": "A large bird that eats the remains of dead animals." },
  { "word": "Vaccine", "definition": "A substance given to protect the body against a specific disease." },
  { "word": "Vanish", "definition": "To disappear suddenly." },
  { "word": "Vast", "definition": "Of very great extent or size; immense." },
  { "word": "Velvet", "definition": "A type of fabric with a soft, smooth surface." },
  { "word": "Vend", "definition": "To sell something." },
  { "word": "Vibrate", "definition": "To move continuously and rapidly back and forth." },
  { "word": "Vicious", "definition": "Intentionally cruel or violent." },
  { "word": "Vigilant", "definition": "Keeping careful watch for possible danger or difficulty." },
  { "word": "Violin", "definition": "A wooden musical instrument with four strings played with a bow." },
  { "word": "Visible", "definition": "Able to be seen." },
  { "word": "Vivid", "definition": "Producing powerful feelings or strong, clear images in the mind." },
  { "word": "Volcano", "definition": "A mountain or hill with a vent where lava and gas come out." },
  { "word": "Vowel", "definition": "A speech sound made without closing the mouth (A, E, I, O, U)." },
  { "word": "Vacation", "definition": "A time when you are free from work or school; a holiday." },
  { "word": "Vapor", "definition": "A substance diffused or suspended in the air, like steam." },
  { "word": "Variety", "definition": "A number of different kinds of things." },
  { "word": "Vault", "definition": "A large room or chamber used for storage, often in a bank." },
  { "word": "Veer", "definition": "To change direction suddenly." },
  { "word": "Vengeance", "definition": "Punishment for an injury or wrongdoing; revenge." },
  { "word": "Venom", "definition": "A poisonous substance secreted by animals like snakes or spiders." },
  { "word": "Vertical", "definition": "Straight up and down." },
  { "word": "Vest", "definition": "A sleeveless garment worn over a shirt." },
  { "word": "Vex", "definition": "To make someone feel annoyed or worried." },
  { "word": "Vibrant", "definition": "Full of energy and enthusiasm." },
  { "word": "Vice", "definition": "A bad or immoral habit." },
  { "word": "Vine", "definition": "A climbing plant that produces grapes or other fruit." },
  { "word": "Virgin", "definition": "A person who has never had sexual intercourse." },
  { "word": "Virtue", "definition": "Behavior showing high moral standards; goodness." },
  { "word": "Vital", "definition": "Absolutely necessary or important." },
  { "word": "Vocation", "definition": "A person's main occupation or calling." },
  { "word": "Vogue", "definition": "The current style or fashion." },
  { "word": "Voucher", "definition": "A small slip of paper that can be exchanged for goods or services." },
  { "word": "Vulnerable", "definition": "Open to attack or damage; easily hurt." },
  { "word": "Valid", "definition": "Logical, true, or acceptable." },
  { "word": "Vampire", "definition": "A mythical creature that sucks blood from sleeping people." },
  { "word": "Vandal", "definition": "A person who deliberately destroys or damages public property." },
  { "word": "Vaporize", "definition": "To turn into gas or steam." },
  { "word": "Veil", "definition": "A piece of fine material worn by women to protect or hide the face." },
  { "word": "Vicious", "definition": "Intentionally cruel or violent." },
  { "word": "Victorious", "definition": "Having won a victory." },
  { "word": "Viking", "definition": "A Norse explorer and warrior from the Middle Ages." },
  { "word": "Villain", "definition": "A wicked or evil character in a story." },
  { "word": "Vineyard", "definition": "A plantation of grapevines, often used to make wine." },
  { "word": "Vision", "definition": "The ability to see; a mental image of what the future could be." },
  { "word": "Visualize", "definition": "To form a picture of something in your mind." },
  { "word": "Vocabulary", "definition": "All the words a person knows or uses." },
  { "word": "Void", "definition": "A completely empty space; invalid or useless." },
  { "word": "Volleyball", "definition": "A game where two teams hit a ball over a high net." },
  { "word": "Vortex", "definition": "A mass of swirling fluid or air, like a whirlpool." },
  { "word": "Vow", "definition": "A solemn promise." },
  { "word": "Vulture", "definition": "A large bird that eats the remains of dead animals." }
                ],
              'W': [
                { "word": "Waffle", "definition": "A light, crisp cake cooked in a special iron with a pattern." },
  { "word": "Wait", "definition": "To stay in one place until something happens." },
  { "word": "Wake", "definition": "To stop sleeping or to make someone stop sleeping." },
  { "word": "Walk", "definition": "To move on foot at a slow pace." },
  { "word": "Wall", "definition": "A vertical structure that forms the side of a room or building." },
  { "word": "Want", "definition": "To desire or wish for something." },
  { "word": "War", "definition": "A state of armed conflict between countries or groups." },
  { "word": "Warm", "definition": "Having a high but comfortable temperature; not cold." },
  { "word": "Warn", "definition": "To inform someone of a possible danger or problem." },
  { "word": "Wash", "definition": "To clean with water and often soap." },
  { "word": "Waste", "definition": "To use something carelessly or unnecessarily; unwanted material." },
  { "word": "Watch", "definition": "To look at something for a period of time; a small clock worn on the wrist." },
  { "word": "Water", "definition": "A clear liquid essential for life." },
  { "word": "Wave", "definition": "A ridge of water moving across the surface of a sea or lake; a gesture with the hand." },
  { "word": "Way", "definition": "A method or course for achieving something; a direction." },
  { "word": "We", "definition": "Used to refer to yourself and one or more other people." },
  { "word": "Weak", "definition": "Lacking physical strength or power; easily broken." },
  { "word": "Wear", "definition": "To have clothing or jewelry on your body." },
  { "word": "Weather", "definition": "The state of the atmosphere (hot, cold, sunny, rainy, etc.)." },
  { "word": "Web", "definition": "A net made by a spider; the internet." },
  { "word": "Week", "definition": "A period of seven days." },
  { "word": "Weigh", "definition": "To find out how heavy something is." },
  { "word": "Welcome", "definition": "To greet someone kindly on their arrival; pleasing or gladly received." },
  { "word": "Well", "definition": "In a good or satisfactory way; in good health; a deep hole for drawing water." },
  { "word": "West", "definition": "One of the four main directions, where the sun sets." },
  { "word": "Wet", "definition": "Covered or soaked with water or liquid." },
  { "word": "What", "definition": "Asking for information about something." },
  { "word": "Wheel", "definition": "A circular frame that turns on an axle." },
  { "word": "When", "definition": "Asking about the time something happens." },
  { "word": "Where", "definition": "Asking about the place or position of something." },
  { "word": "Which", "definition": "Asking for a choice between two or more options." },
  { "word": "While", "definition": "During the time that; a period of time." },
  { "word": "Whisper", "definition": "To speak very softly using only your breath." },
  { "word": "White", "definition": "The color of snow or milk; the opposite of black." },
  { "word": "Who", "definition": "Asking about a person." },
  { "word": "Whole", "definition": "All of something; complete." },
  { "word": "Why", "definition": "Asking for the reason or explanation for something." },
  { "word": "Wide", "definition": "Of great extent from side to side; broad." },
  { "word": "Wife", "definition": "A married woman." },
  { "word": "Wild", "definition": "Living or growing in a natural state; untamed." },
  { "word": "Will", "definition": "Used to show that something is certain to happen in the future; strong determination." },
  { "word": "Win", "definition": "To be successful in a game, contest, or fight." },
  { "word": "Wind", "definition": "A natural movement of air." },
  { "word": "Window", "definition": "An opening in a wall or roof to let in light or air." },
  { "word": "Wing", "definition": "A limb of a bird or bat used for flying." },
  { "word": "Winter", "definition": "The coldest season of the year." },
  { "word": "Wipe", "definition": "To clean or dry something with a cloth or hand." },
  { "word": "Wire", "definition": "A thin, flexible strand of metal." },
  { "word": "Wise", "definition": "Having great experience, knowledge, and good judgment." },
  { "word": "Wish", "definition": "To want something that is unlikely to happen; a desire." },
  { "word": "With", "definition": "Accompanied by or using something." },
  { "word": "Within", "definition": "Inside of something." },
  { "word": "Without", "definition": "Not having or lacking something." },
  { "word": "Woman", "definition": "An adult female human." },
  { "word": "Wonder", "definition": "A feeling of surprise and admiration; to be curious about something." },
  { "word": "Wood", "definition": "The hard material from trees, used for building or burning." },
  { "word": "Word", "definition": "A single unit of language that is spoken or written." },
  { "word": "Work", "definition": "Activity involving mental or physical effort done to achieve a purpose." },
  { "word": "World", "definition": "The Earth and all its inhabitants." },
  { "word": "Worry", "definition": "To feel or cause to feel anxious or troubled." },
  { "word": "Worse", "definition": "More unfavorable or more serious." },
  { "word": "Worth", "definition": "The value of a thing; how important or useful something is." },
  { "word": "Would", "definition": "Used to express a wish or a possible event." },
  { "word": "Wrap", "definition": "To cover something by winding or folding a material around it." },
  { "word": "Write", "definition": "To mark symbols on a surface to form letters or words." },
  { "word": "Wrong", "definition": "Incorrect or bad; not right." },
  { "word": "Waist", "definition": "The part of the body between the ribs and the hips." },
  { "word": "Wagon", "definition": "A vehicle with four wheels used for carrying heavy loads." },
  { "word": "Wander", "definition": "To walk aimlessly without a set destination." },
  { "word": "Wasp", "definition": "A flying insect with a sting, similar to a bee." },
  { "word": "Weasel", "definition": "A small, fierce, long-bodied mammal." },
  { "word": "Whisker", "definition": "A long, stiff hair on the face of animals like cats and mice." },
  { "word": "Wizard", "definition": "A man who practices magic; a sorcerer." },
  { "word": "Wolf", "definition": "A wild animal that is part of the dog family." },
  { "word": "Worm", "definition": "A small, soft, long creature that lives in the soil." },
  { "word": "Wrinkle", "definition": "A small line or fold in a smooth surface." },
  { "word": "Wrestle", "definition": "To fight by grappling and trying to throw an opponent down." },
  { "word": "Wig", "definition": "A covering of false hair worn on the head." },
  { "word": "Wigwam", "definition": "A dome-shaped hut traditionally built by Native Americans." },
  { "word": "Willing", "definition": "Ready, eager, or prepared to do something." },
  { "word": "Witch", "definition": "A woman thought to have magic powers." },
  { "word": "Witness", "definition": "A person who sees an event happen." },
  { "word": "Wrestler", "definition": "A person who takes part in wrestling." },
  { "word": "Wreath", "definition": "An arrangement of flowers or leaves in a circle." },
  { "word": "Warrior", "definition": "A brave or experienced soldier or fighter." },
  { "word": "Whirlwind", "definition": "A column of air rotating rapidly." }
                ],
              'X': [
                { "word": "Apology Note", "definition": "For the letter X, the English language has a very limited number of common words."},
  { "word": "X-ray", "definition": "A kind of invisible light used to see inside the body or objects." },
  { "word": "Xylophone", "definition": "A musical instrument made of wooden bars you hit with mallets." },
  { "word": "Xenon", "definition": "A gas that is a chemical element, often used in lights." },
  { "word": "Xerox", "definition": "To make a copy of a document using a machine." },
  { "word": "Xenophobia", "definition": "The fear or dislike of people from other countries." },
  { "word": "Xenops", "definition": "A small, tropical bird found in Central and South America." },
  { "word": "Xeriscape", "definition": "Landscaping that uses very little water." },
  { "word": "Xmas", "definition": "A short way to write Christmas." },
  { "word": "Xenia", "definition": "The effect of pollen on the seed or fruit of a plant." },
  { "word": "Xylose", "definition": "A type of sugar found in wood." },
                ],
              'Y': [
                { "word": "Yacht", "definition": "A large boat used for pleasure or racing." },
  { "word": "Yawn", "definition": "To open your mouth wide and breathe deeply when tired or bored." },
  { "word": "Year", "definition": "A period of 365 or 366 days." },
  { "word": "Yearly", "definition": "Happening once every year." },
  { "word": "Yell", "definition": "To shout loudly." },
  { "word": "Yellow", "definition": "A primary color, like the color of a lemon or the sun." },
  { "word": "Yes", "definition": "A word used to give an affirmative answer or consent." },
  { "word": "Yesterday", "definition": "The day before today." },
  { "word": "Yet", "definition": "Up to the present time; still." },
  { "word": "Yield", "definition": "To produce or provide a natural product; to give way." },
  { "word": "You", "definition": "The person or people being addressed." },
  { "word": "Young", "definition": "In an early stage of life; not old." },
  { "word": "Your", "definition": "Belonging to you." },
  { "word": "Youth", "definition": "The time of life when one is young; young people collectively." },
  { "word": "Yummy", "definition": "Delicious or very tasty." },
  { "word": "Yak", "definition": "A large, shaggy ox with long horns, found in Tibet." },
  { "word": "Yard", "definition": "A unit of length equal to three feet; the ground around a house." },
  { "word": "Yarn", "definition": "Spun fiber used for knitting or weaving." },
  { "word": "Yelp", "definition": "A sharp, short cry, especially of pain or surprise." },
  { "word": "Yen", "definition": "The basic unit of money in Japan; a strong desire." },
  { "word": "Yoga", "definition": "A system of physical and mental exercise that originated in India." },
  { "word": "Yogurt", "definition": "A creamy food made from milk that has been curdled." },
  { "word": "Yolk", "definition": "The yellow part in the center of an egg." },
  { "word": "Youngster", "definition": "A child or young person." },
  { "word": "Yuk", "definition": "A sound you make when something is gross or disgusting." },
  { "word": "Yummy", "definition": "Delicious or very tasty." },
  { "word": "Yippee", "definition": "A shout of joy or excitement." },
  { "word": "Yodel", "definition": "To sing in a way that rapidly changes from a normal voice to a high voice." },
  { "word": "Yoke", "definition": "A wooden cross-piece fastened over the necks of two animals (like oxen) to pull a cart." },
  { "word": "Yonder", "definition": "At some distance in the direction indicated; over there." },
  { "word": "Yore", "definition": "Of long ago or the past (used in phrases like 'days of yore')." },
  { "word": "Yowl", "definition": "A prolonged, loud, mournful cry, like that of a cat or dog." },
  { "word": "Yardstick", "definition": "A ruler one yard long; a standard used for comparison." },
  { "word": "Yummy-licious", "definition": "A funny word meaning extra yummy." },
  { "word": "Yachting", "definition": "The sport of sailing in a yacht." },
  { "word": "Yam", "definition": "A long, edible root that is a staple food in tropical countries." },
  { "word": "Yawned", "definition": "Opened the mouth wide and breathed deeply (past tense)." },
  { "word": "Yearbook", "definition": "A book published annually, usually by a school, reviewing the past year." },
  { "word": "Yeoman", "definition": "A small landowner, or an attendant in a royal household." },
  { "word": "Yesteryear", "definition": "Last year or the recent past." },
  { "word": "Yeti", "definition": "A mythical snowman-like creature said to live in the Himalayas." },
  { "word": "Yoke", "definition": "To join two animals together with a yoke." },
  { "word": "Yuck", "definition": "An exclamation of strong dislike or disgust." },
  { "word": "Yuppie", "definition": "A young, educated person who has a good-paying job." },
  { "word": "Yeast", "definition": "A tiny fungus used to make bread rise and beer ferment." },
  { "word": "Yesterday's", "definition": "Belonging to the day before today." },
  { "word": "Yummy", "definition": "Delicious or very tasty." },
  { "word": "Yodel", "definition": "To sing in a high, clear, and rapidly changing voice." },
  { "word": "Yonder", "definition": "At some distance in the direction indicated; over there." },
  { "word": "Yowza", "definition": "An exclamation of surprise or excitement." },
  { "word": "Yawned", "definition": "Opened the mouth wide and breathed deeply (past tense)." },
  { "word": "Yellowish", "definition": "Slightly yellow." },
  { "word": "Yummy-scrummy", "definition": "A funny word meaning very, very delicious." },
  { "word": "Yester-", "definition": "A prefix meaning 'yesterday' or 'last' (used in old words)." },
  { "word": "Yawn", "definition": "To open your mouth wide and breathe deeply when tired or bored." },
  { "word": "Yearly", "definition": "Happening once every year." },
  { "word": "Yelp", "definition": "A sharp, short cry, especially of pain or surprise." },
  { "word": "Yield", "definition": "To produce or provide a natural product; to give way." },
  { "word": "Youngest", "definition": "The one that is the least old." },
  { "word": "Youthful", "definition": "Having the characteristics of youth; young and energetic." },
  { "word": "Yachtsman", "definition": "A person who sails a yacht." },
  { "word": "Yachting", "definition": "The activity of sailing a yacht." },
  { "word": "Yams", "definition": "More than one edible root (yam)." },
  { "word": "Yarn-spinner", "definition": "A storyteller, often of tall tales (informal)." },
  { "word": "Yearn", "definition": "To have an intense feeling of longing for something." },
  { "word": "Yeast", "definition": "A fungus used to make bread rise." },
  { "word": "Yell", "definition": "To shout loudly." },
  { "word": "Yellowing", "definition": "Turning yellow." },
  { "word": "Yen", "definition": "A strong desire." },
  { "word": "Yes-man", "definition": "A person who always agrees with their boss (negative term)." },
  { "word": "Yet-to-be", "definition": "Something that is going to happen in the future." },
  { "word": "Yipe", "definition": "A sudden, sharp sound of surprise or pain." },
  { "word": "Yodel", "definition": "To sing in a high, clear voice that changes pitch rapidly." },
  { "word": "Yogurt", "definition": "A creamy, slightly sour food made from milk." },
  { "word": "Yolk", "definition": "The yellow part in the center of an egg." },
  { "word": "Youngster", "definition": "A child or young person." },
  { "word": "Yourself", "definition": "Used to refer to you and no one else." },
  { "word": "Yuck", "definition": "An exclamation of strong dislike or disgust." },
  { "word": "Yummy-tummy", "definition": "A funny word for a delicious treat." }
                ],
              'Z': [
                 { "word": "Apology Note", "definition": "For the letter Z, the English language has a very limited number of common words."},
  { "word": "Zebra", "definition": "An African wild animal like a horse with black and white stripes." },
  { "word": "Zero", "definition": "The number representing nothing; 0." },
  { "word": "Zip", "definition": "To move very fast; a fastener with interlocking teeth (zipper)." },
  { "word": "Zone", "definition": "An area or region distinguished by some feature." },
  { "word": "Zoo", "definition": "A place where wild animals are kept and shown to the public." },
  { "word": "Zoom", "definition": "To move quickly, often with a buzzing sound." },
  { "word": "Zigzag", "definition": "A line or path having a sharp, alternating turns." },
  { "word": "Zest", "definition": "Great enthusiasm and energy; the skin of a citrus fruit." },
  { "word": "Zillion", "definition": "An imaginary very large number." },
  { "word": "Zither", "definition": "A flat musical instrument with many strings stretched across a shallow box." },
  { "word": "Zodiac", "definition": "A band of sky containing the paths of the sun, moon, and planets." },
  { "word": "Zucchini", "definition": "A long, green vegetable; a type of squash." },
  { "word": "Zeal", "definition": "Great enthusiasm or passion." },
  { "word": "Zesty", "definition": "Having a strong, pleasant, and spicy flavor." },
  { "word": "Zodiacal", "definition": "Relating to the zodiac." },
  { "word": "Zombify", "definition": "To turn someone into a zombie." },
  { "word": "Zig", "definition": "One part of a zigzag turn." },
  { "word": "Zap", "definition": "To move or act quickly; to attack with a burst of energy." },
  { "word": "Zephyr", "definition": "A soft, gentle breeze." },
  { "word": "Zillionaire", "definition": "A person with a huge, imaginary amount of money." },
  { "word": "Zing", "definition": "A sudden burst of energy or liveliness." },
  { "word": "Zodiacal", "definition": "Related to the zodiac." },
  { "word": "Zonked", "definition": "Extremely tired or exhausted." },
  { "word": "Zooming", "definition": "Moving very quickly." },
  { "word": "Zany", "definition": "Amusingly unconventional and eccentric." },
  { "word": "Zapper", "definition": "A device that emits a sudden burst of energy (informal)." },
  { "word": "Zeroing", "definition": "Setting a measurement to zero; focusing on a target." },
  { "word": "Zingy", "definition": "Full of zest or energy." }
                ],
              
            // ... (Rest of the letters would have 100 entries each)
        };

        const alphabetNav = document.getElementById('alphabet-nav');
        const wordListContainer = document.getElementById('word-list-container');
        let activeLetter = 'A';

        function renderAlphabetNav() {
            alphabetNav.innerHTML = '';
            for (let i = 65; i <= 90; i++) {
                const letter = String.fromCharCode(i);
                const isActive = letter === activeLetter;
                const button = document.createElement('button');
                
                button.textContent = letter;
                button.className = `p-2 w-10 h-10 font-bold rounded-lg transition-all shadow-sm ${
                    isActive ? 'bg-kids-yellow text-kids-blue text-xl border-2 border-kids-blue' : 'bg-gray-100 text-gray-700 hover:bg-kids-yellow/50'
                }`;
                // Fixed: The click handler now sets activeLetter, updates the buttons, and shows words without recursion
                button.onclick = () => {
                    activeLetter = letter;
                    renderAlphabetNav(); 
                    // When clicking a letter, clear the search bar and show words
                    document.getElementById('dictionary-search-input').value = '';
                    showWords(letter, '');
                };
                alphabetNav.appendChild(button);
            }
        }

        function showWords(letter, searchTerm = '') {
            const wordsForLetter = dictionaryData[letter] || [];
            wordListContainer.innerHTML = '';
            
            const lowerCaseSearch = searchTerm.toLowerCase();

            // Filter words based on search term (checks word OR definition)
            const filteredWords = wordsForLetter.filter(item => 
                item.word.toLowerCase().includes(lowerCaseSearch) || 
                item.definition.toLowerCase().includes(lowerCaseSearch)
            );
            
            if (filteredWords.length === 0) {
                 // Re-add the placeholder text if no words are found for the letter or search term
                 let message = '';
                 if (searchTerm) {
                    message = `No words found for "${searchTerm}" under letter ${letter}. Try a different word!`;
                 } else {
                    message = `No words loaded for letter ${letter} (This is mock data).`;
                 }
                 wordListContainer.innerHTML = `<p class="text-center text-lg text-gray-500 p-4">${message}</p>`;
                 return;
            }

            // If there are words, we don't need a placeholder, so we just add the words.
            filteredWords.forEach(item => {
                const wordElement = document.createElement('div');
                wordElement.className = 'bg-kids-bg p-4 rounded-xl border-l-4 border-kids-yellow shadow-sm';
                wordElement.innerHTML = `
                    <p class="text-xl font-extrabold text-kids-blue">${item.word}</p>
                    <p class="text-gray-700 mt-1">${item.definition}</p>
                `;
                wordListContainer.appendChild(wordElement);
            });
        }


        // ----------------------------------------------------------------------
        // --- 3. Quiz Game Logic ---
        // ----------------------------------------------------------------------

        let score = 0;
        let currentQuestionIndex = 0;

        // Combine all dictionary words for the quiz (using mock data)
        const allDictionaryWords = Object.values(dictionaryData).flat();
        
        // Use a subset of words for a manageable quiz size
        const QUIZ_SIZE = 5; 
        let quizQuestions = [];

        const quizStart = document.getElementById('quiz-start');
        const quizGame = document.getElementById('quiz-game');
        const quizResults = document.getElementById('quiz-results');
        const questionText = document.getElementById('question-text');
        const answerOptions = document.getElementById('answer-options');
        const quizFeedback = document.getElementById('quiz-feedback');
        const nextQuestionBtn = document.getElementById('next-question-btn');
        const currentQuestionNum = document.getElementById('current-question-num');
        const totalQuestions = document.getElementById('total-questions');
        const startQuizBtn = document.getElementById('start-quiz-btn');

        startQuizBtn.addEventListener('click', startQuiz);

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        function getQuizQuestions() {
            if (allDictionaryWords.length < 4) {
                // Not enough unique words for a quiz
                return []; 
            }
            
            // 1. Shuffle all words and pick the required number of questions
            shuffleArray(allDictionaryWords);
            const selectedWords = allDictionaryWords.slice(0, QUIZ_SIZE);

            return selectedWords.map(correctWord => {
                const options = [correctWord];
                let wrongOptions = allDictionaryWords.filter(w => w.word !== correctWord.word);
                
                // 2. Select 3 random wrong definitions (if available)
                shuffleArray(wrongOptions);
                wrongOptions.slice(0, 3).forEach(w => options.push(w));

                // 3. Shuffle the final options
                shuffleArray(options);

                // The question is the DEFINITION, and the answers are the WORDS
                return {
                    question: correctWord.definition,
                    options: options,
                    correctAnswer: correctWord.word,
                };
            });
        }

        function startQuiz() {
            quizQuestions = getQuizQuestions();
            
            if (quizQuestions.length === 0) {
                // IMPORTANT: Replace alert() with a custom message box or console log
                console.error("Need more words in the dictionary to start the quiz!");
                quizFeedback.textContent = "Error: Not enough words in the dictionary to start the quiz!";
                quizFeedback.className = 'mt-4 text-center font-bold text-lg text-kids-red';
                return;
            }

            score = 0;
            currentQuestionIndex = 0;
            totalQuestions.textContent = quizQuestions.length;
            
            quizStart.classList.add('hidden');
            quizResults.classList.add('hidden');
            quizGame.classList.remove('hidden');
            
            nextQuestionBtn.classList.add('hidden');
            quizFeedback.textContent = '';
            
            loadQuestion();
        }

        function loadQuestion() {
            if (currentQuestionIndex >= quizQuestions.length) {
                showResults();
                return;
            }

            const q = quizQuestions[currentQuestionIndex];

            // Update UI
            currentQuestionNum.textContent = currentQuestionIndex + 1;
            questionText.textContent = q.question;
            answerOptions.innerHTML = '';
            quizFeedback.textContent = '';
            nextQuestionBtn.classList.add('hidden');

            // Render options
            q.options.forEach((option, index) => {
                const btn = document.createElement('button');
                btn.textContent = option.word;
                btn.setAttribute('data-answer', option.word);
                btn.className = 'answer-btn w-full bg-kids-bg text-gray-800 font-semibold p-4 rounded-xl shadow-md hover:bg-gray-200 transition text-left';
                btn.onclick = () => checkAnswer(btn, q.correctAnswer);
                answerOptions.appendChild(btn);
            });
        }

        function checkAnswer(selectedButton, correctAnswer) {
            const allButtons = document.querySelectorAll('.answer-btn');
            const selectedAnswer = selectedButton.getAttribute('data-answer');
            let isCorrect = selectedAnswer === correctAnswer;

            // Disable all buttons after selection
            allButtons.forEach(btn => {
                btn.disabled = true;
                btn.classList.remove('hover:bg-gray-200');
                if (btn.getAttribute('data-answer') === correctAnswer) {
                    btn.classList.add('bg-kids-green', 'text-white');
                    btn.classList.remove('bg-kids-bg', 'text-gray-800');
                } else if (btn === selectedButton) {
                    btn.classList.add('bg-kids-red', 'text-white');
                    btn.classList.remove('bg-kids-bg', 'text-gray-800');
                }
            });

            if (isCorrect) {
                score++;
                quizFeedback.textContent = 'Correct! Great job!';
                quizFeedback.className = 'mt-4 text-center font-bold text-lg text-kids-green';
            } else {
                quizFeedback.textContent = `Oops! The correct word was "${correctAnswer}".`;
                quizFeedback.className = 'mt-4 text-center font-bold text-lg text-kids-red';
            }

            nextQuestionBtn.classList.remove('hidden');
            nextQuestionBtn.onclick = () => {
                currentQuestionIndex++;
                loadQuestion();
            };
        }

        function showResults() {
            quizGame.classList.add('hidden');
            quizResults.classList.remove('hidden');
            document.getElementById('final-score').textContent = `${score} / ${quizQuestions.length}`;
            showView('quiz'); // Ensure the current view remains 'quiz' and updates the card color
        }
    </script>
</body>
</html>
