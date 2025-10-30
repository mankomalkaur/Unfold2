<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UNFOLD: AI Career Guidance Platform</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom font for a professional look */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap');
        body { font-family: 'Inter', sans-serif; }
        
        /* Style for active navigation link */
        .nav-link.active {
            font-weight: 700;
            color: #4f46e5; /* indigo-600 */
            border-bottom: 2px solid #4f46e5;
        }
        
        /* Style for selected stream card */
        .stream-card.selected {
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            transform: scale(1.02);
            border-width: 4px; 
            /* Added ring for better focus indication */
            --tw-ring-color: #4f46e5;
            --tw-ring-opacity: 1;
            box-shadow: 0 0 0 4px var(--tw-ring-color);
        }
        
        /* Custom style for the fixed chatbot icon */
        #chatbot-icon {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 100;
            cursor: pointer;
            transition: transform 0.3s;
        }
        #chatbot-icon:hover {
            transform: scale(1.1);
        }
        
        /* Chatbot Modal styles */
        #chatbot-modal {
            position: fixed;
            bottom: 80px; 
            right: 20px;
            width: 90%;
            max-width: 350px;
            height: 450px;
            z-index: 200;
            background: white;
            border-radius: 1rem;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            display: none; 
            flex-direction: column;
            overflow: hidden;
        }
        .ai-message {
            background-color: #e0f2fe; /* light blue */
            border-radius: 0.75rem;
            padding: 0.75rem;
            max-width: 85%;
            align-self: flex-start;
        }
        .user-message {
            background-color: #d1fae5; /* light green */
            border-radius: 0.75rem;
            padding: 0.75rem;
            max-width: 85%;
            align-self: flex-end;
        }
        
        /* Email modal styles */
        #email-modal {
            position: fixed;
            inset: 0;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 250;
            overflow-y: auto;
            display: none;
        }
        .email-content-box {
            max-width: 600px;
            margin: 50px auto;
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            font-family: 'Inter', sans-serif;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <header class="bg-white shadow-md sticky top-0 z-10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 flex justify-between items-center">
            <h1 class="text-3xl font-extrabold text-indigo-700 tracking-tight">UNFOLD</h1>
            <nav class="space-x-4 flex items-center">
                <a href="#home" data-view="home" class="nav-link text-gray-600 hover:text-indigo-600 font-medium transition duration-150 py-1">Home</a>
                <a href="#psychometric" data-view="psychometric" class="nav-link text-gray-600 hover:text-indigo-600 font-medium transition duration-150 py-1">Psychometric Test</a>
                <a href="#stream" data-view="stream" class="nav-link text-gray-600 hover:text-indigo-600 font-medium transition duration-150 py-1">Stream Selection</a>
                <a href="#book-counselling" data-view="book-counselling" class="nav-link text-gray-600 hover:text-indigo-600 font-medium transition duration-150 py-1">Book a Counselling Session</a>
                <button id="auth-button" class="bg-indigo-600 text-white px-3 py-1.5 rounded-full font-semibold text-sm shadow-lg hover:bg-indigo-700 transition duration-300">Sign In with Gmail</button>
            </nav>
        </div>
    </header>

    <div id="message-box" class="fixed top-20 right-5 z-50 p-4 rounded-lg shadow-xl text-white transition-all duration-300 transform translate-x-full opacity-0" role="alert"></div>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 md:py-12">
        
        <section id="view-home" data-view-target="home" class="view-content">
            
            <div class="py-12 bg-indigo-50 rounded-2xl shadow-xl mb-12">
                <div class="text-center">
                    <h2 class="text-5xl md:text-6xl font-extrabold text-gray-900 mb-4 leading-tight">
                        Discover Your True Academic Path
                    </h2>
                    <p class="text-xl text-gray-600 mb-8 max-w-3xl mx-auto">
                        UNFOLD helps students make informed decisions by combining psychometric data with expert stream selection guidance. Stop guessing, start planning.
                    </p>
                    <a href="#psychometric" data-view="psychometric" class="inline-flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-full text-white bg-green-500 hover:bg-green-600 shadow-xl transition duration-300 transform hover:scale-105">
                        Start Psychometric Test
                    </a>
                </div>
            </div>

            <div class="py-8" id="services">
                <h3 class="text-4xl font-bold text-center text-gray-800 mb-12">How UNFOLD Works</h3>
                
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    
                    <a href="#psychometric" data-view="psychometric" class="view-content-link block bg-white p-6 rounded-xl shadow-2xl border-t-4 border-indigo-500 hover:shadow-3xl transition duration-300 hover:scale-[1.01] cursor-pointer">
                        <div class="text-4xl text-indigo-500 mb-4">🧠</div>
                        <h4 class="text-2xl font-semibold text-gray-900 mb-3">Psychometric Testing</h4>
                        <p class="text-gray-600">
                            Our validated tests assess your aptitude, personality traits, and core interests. Get objective data that reveals your natural strengths and professional leanings.
                        </p>
                    </a>

                    <a href="#stream" data-view="stream" class="view-content-link block bg-white p-6 rounded-xl shadow-2xl border-t-4 border-green-500 hover:shadow-3xl transition duration-300 hover:scale-[1.01] cursor-pointer">
                        <div class="text-4xl text-green-500 mb-4">🎓</div>
                        <h4 class="text-2xl font-semibold text-gray-900 mb-3">Stream Selection</h4>
                        <p class="text-gray-600">
                            Receive personalized recommendations for Science, Commerce, or Humanities based on your test results, ensuring your academic path aligns with your potential.
                        </p>
                    </a>

                    <a href="#book-counselling" data-view="book-counselling" class="view-content-link block bg-white p-6 rounded-xl shadow-2xl border-t-4 border-yellow-500 hover:shadow-3xl transition duration-300 hover:scale-[1.01] cursor-pointer">
                        <div class="text-4xl text-yellow-500 mb-4">📊</div>
                        <h4 class="text-2xl font-semibold text-gray-900 mb-3">Detailed Career Reports</h4>
                        <p class="text-gray-600">
                            Access comprehensive reports outlining potential careers, required skills, and subject combinations for your chosen stream, helping you plan effectively.
                        </p>
                    </a>
                </div>
            </div>

            <div class="py-8 bg-gray-100 rounded-xl mt-12" id="about">
                <h3 class="text-4xl font-bold text-center text-gray-800 mb-8">Our Mission</h3>
                <div class="max-w-4xl mx-auto bg-white p-8 rounded-xl shadow-lg">
                    <p class="text-lg text-gray-600 leading-relaxed">
                        At **UNFOLD**, we believe every student deserves clarity. We utilize cutting-edge technology and psychological research to take the guesswork out of career planning. Our platform is designed to empower you—the student—by providing objective data and actionable insights, ensuring you step confidently onto the right professional path. We are committed to making stream and career selection a process of discovery, not confusion.
                    </p>
                </div>
            </div>

            <div class="py-12 bg-white rounded-xl mt-12 shadow-inner">
                <h3 class="text-4xl font-bold text-center text-gray-800 mb-12">What Our Students Say 🗣️</h3>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-6xl mx-auto">
                    
                    <div class="p-6 rounded-xl shadow-lg border-l-4 border-indigo-500 bg-gray-50 transition duration-300">
                        <div class="text-2xl text-yellow-500 mb-3">⭐⭐⭐⭐⭐</div>
                        <p class="text-gray-700 italic mb-4">"Before I saw my career counselor, I was rather **lost and unmotivated** in where my career was heading. The way my counselor was able to smoothly connect all the dots was **worth its weight in gold**. I'm now excited and ready for my next career adventure!"</p>
                        <p class="font-bold text-indigo-700">- Sarah M. <span class="text-gray-500 text-sm font-normal">(Career Changer)</span></p>
                    </div>

                    <div class="p-6 rounded-xl shadow-lg border-l-4 border-green-500 bg-gray-50 transition duration-300">
                        <div class="text-2xl text-yellow-500 mb-3">⭐⭐⭐⭐⭐</div>
                        <p class="text-gray-700 italic mb-4">"The personalized guidance was instrumental. My counselor helped me find a path that **aligned perfectly with my talents and passions**. I now have a clear roadmap and the confidence to pursue it."</p>
                        <p class="font-bold text-green-700">- Rohan K. <span class="text-gray-500 text-sm font-normal">(High School Student)</span></p>
                    </div>
                    
                    <div class="p-6 rounded-xl shadow-lg border-l-4 border-red-500 bg-gray-50 transition duration-300">
                        <div class="text-2xl text-yellow-500 mb-3">⭐⭐⭐⭐⭐</div>
                        <p class="text-gray-700 italic mb-4">"My counselor was not just a consultant, but a mentor, life advisor, and therapist rolled into one. She gave me a roadmap to resolve my issues and taught me how to develop **better decision filters**."</p>
                        <p class="font-bold text-red-700">- Mayank M. <span class="text-gray-500 text-sm font-normal">(CA Student)</span></p>
                    </div>
                    
                </div>
            </div>
            </section>

        <section id="view-psychometric" data-view-target="psychometric" class="view-content hidden">
            <div class="bg-white p-8 rounded-2xl shadow-xl max-w-3xl mx-auto">
                <h2 class="text-4xl font-extrabold text-indigo-700 mb-6 border-b pb-3">Start Your Psychometric Test</h2>
                <p class="text-gray-600 mb-8">
                    Please provide your basic information to generate your personalized test ID and begin the assessment. **(Login required)**
                </p>
                
                <div id="psychometric-quiz-area" class="space-y-6 hidden">
                    <div class="flex justify-between items-center p-4 bg-indigo-100 rounded-lg shadow-md">
                        <h3 class="text-xl font-bold text-indigo-700">Aptitude & Interest Test</h3>
                        <div class="flex items-center space-x-4">
                            <span id="quiz-timer" class="text-lg font-mono text-red-600 font-extrabold">60:00</span> 
                            <button type="button" id="quiz-reset-btn" class="text-sm px-3 py-1 bg-gray-300 rounded-full hover:bg-gray-400 font-medium">Reset Quiz</button>
                        </div>
                    </div>
                    <form id="quiz-form" class="space-y-8">
                        <div id="quiz-questions-container">
                            </div>
                        <button type="submit" id="quiz-submit-btn" class="w-full py-3 px-4 rounded-lg shadow-lg text-lg font-medium text-white bg-green-600 hover:bg-green-700 transition duration-300">
                            Submit Test & Get Result
                        </button>
                    </form>
                </div>
                
                <form id="psychometric-form" class="space-y-6">
                    <div>
                        <label for="name" class="block text-sm font-medium text-gray-700">Full Name</label>
                        <input type="text" id="name" name="name" placeholder="Anvi Kalra" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500" required>
                    </div>
                    <div>
                        <label for="email" class="block text-sm font-medium text-gray-700">Email Address</label>
                        <input type="email" id="email" name="email" placeholder="anvi@gmail.com" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500" required>
                    </div>
                    <div>
                        <label for="grade" class="block text-sm font-medium text-gray-700">Current Grade/Year</label>
                        <select id="grade" name="grade" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500" required>
                            <option value="">Select Grade</option>
                            <option value="9">Grade 9</option>
                            <option value="10">Grade 10</option>
                            <option value="11">Grade 11</option>
                            <option value="12">Grade 12</option>
                            <option value="college">College/University</option>
                        </select>
                    </div>
                    <button type="submit" id="start-assessment-btn" class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-lg text-lg font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition duration-300">
                        Generate Test ID & Start Assessment
                    </button>
                    <p class="text-sm text-gray-500 text-center pt-2">Test duration: Approx. **60 minutes**. **Login required to start and save results.**</p>
                </form>
                
                <div id="quiz-result-area" class="mt-8 p-6 bg-green-50 rounded-xl border border-green-200 hidden">
                    <h4 class="text-2xl font-bold text-green-700 mb-4">✅ Assessment Complete! Your Personalized Report</h4>
                    <p class="text-xl font-semibold mb-4 text-gray-700">
                        Your Highest Match: <span id="result-stream" class="text-indigo-600 font-extrabold"></span>
                    </p>
                    <div id="result-scores" class="space-y-3 mb-6">
                        </div>
                    <p class="text-sm text-gray-600 mt-6 mb-8">
                        **Next Step:** Review your report and use the buttons below for detailed planning.
                    </p>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                        <button onclick="handleRedoTest()" class="py-2 px-4 rounded-lg font-medium text-white bg-red-500 hover:bg-red-600 transition duration-300 shadow-md">
                            🔄 Redo Test
                        </button>
                        <button onclick="handleDownloadReport()" class="py-2 px-4 rounded-lg font-medium text-white bg-indigo-600 hover:bg-indigo-700 transition duration-300 shadow-md">
                            ⬇️ Download Report
                        </button>
                        <button onclick="handleGenerateRoadmap()" class="py-2 px-4 rounded-lg font-medium text-white bg-purple-500 hover:bg-purple-600 transition duration-300 shadow-md">
                            🤖 AI Career Roadmap
                        </button>
                    </div>
                </div>

            </div>
        </section>

        <section id="view-stream" data-view-target="stream" class="view-content hidden">
            <div class="bg-white p-8 rounded-2xl shadow-xl max-w-5xl mx-auto">
                <h2 class="text-4xl font-extrabold text-green-700 mb-6 border-b pb-3">Stream Selection & Subject Planner</h2>
                <p class="text-gray-600 mb-8">
                    Start by selecting a stream below. Then, choose your elective and optional subjects to create your personalized academic path.
                </p>

                <div id="stream-cards-container" class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-12">
                    <button type="button" data-stream="science" onclick="selectStream('science')" class="stream-card bg-green-50 p-6 rounded-xl border-4 border-green-200 hover:border-green-500 hover:shadow-xl transition duration-300 text-left focus:outline-none focus:ring-4 focus:ring-green-300">
                        <div class="text-5xl mb-3">🔬</div>
                        <h3 class="text-2xl font-bold text-green-800">Science Stream</h3>
                        <p class="text-sm text-gray-600 mt-2">Core: Physics, Chemistry. Choose Maths, Biology, or both.</p>
                        <span class="mt-4 inline-block text-indigo-600 font-semibold">Select Stream &rarr;</span>
                    </button>
                    <button type="button" data-stream="commerce" onclick="selectStream('commerce')" class="stream-card bg-yellow-50 p-6 rounded-xl border-4 border-yellow-200 hover:border-yellow-500 hover:shadow-xl transition duration-300 text-left focus:outline-none focus:ring-4 focus:ring-yellow-300">
                        <div class="text-5xl mb-3">💰</div>
                        <h3 class="text-2xl font-bold text-yellow-800">Commerce Stream</h3>
                        <p class="text-sm text-gray-600 mt-2">Core: Accountancy, Economics, Business Studies. Focus on Finance and Management.</p>
                        <span class="mt-4 inline-block text-indigo-600 font-semibold">Select Stream &rarr;</span>
                    </button>
                    <button type="button" data-stream="humanities" onclick="selectStream('humanities')" class="stream-card bg-red-50 p-6 rounded-xl border-4 border-red-200 hover:border-red-500 hover:shadow-xl transition duration-300 text-left focus:outline-none focus:ring-4 focus:ring-red-300">
                        <div class="text-5xl mb-3">🏛️</div>
                        <h3 class="text-2xl font-bold text-red-800">Humanities Stream</h3>
                        <p class="text-sm text-gray-600 mt-2">Explore History, Psychology, Political Science, and Literature for diverse careers.</p>
                        <span class="mt-4 inline-block text-indigo-600 font-semibold">Select Stream &rarr;</span>
                    </button>
                </div>

                <div id="subject-selection-container" class="mt-10 p-8 bg-gray-50 rounded-xl border border-gray-200 hidden">
                    <h3 id="subject-title" class="text-3xl font-bold text-gray-800 mb-6"></h3>
                    <p class="text-red-700 font-medium mb-4">**Important:** You must select at least **one** Elective subject, and a maximum of **two** Elective subjects.</p>
                    <form id="subject-form" class="space-y-6">
                        <div id="core-subjects-list" class="space-y-4">
                            </div>
                        <div id="elective-subjects-list" class="space-y-4">
                            </div>
                        <div id="optional-subjects-list" class="space-y-4">
                            </div>

                        <button type="submit" class="w-full py-3 px-4 rounded-lg shadow-lg text-lg font-medium text-white bg-green-600 hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500 transition duration-300">
                            Confirm Subject Choices
                        </button>
                    </form>
                </div>

            </div>
        </section>

        <section id="view-book-counselling" data-view-target="book-counselling" class="view-content hidden">
            <div class="bg-white p-8 rounded-2xl shadow-xl max-w-2xl mx-auto">
                <h2 class="text-4xl font-extrabold text-red-700 mb-6 border-b pb-3">Book Your Expert Counselling Session</h2>
                <p class="text-gray-600 mb-8">
                    Schedule a 1-on-1 video session with one of our certified career counsellors for personalized guidance. **(Login required)**
                </p>

                <div class="p-4 mb-8 bg-yellow-50 border-l-4 border-yellow-500 rounded-lg shadow-md">
                    <p class="font-semibold text-yellow-800 mb-3">Before booking, ensure you have your Detailed Career Report ready.</p>
                    <a href="#stream" data-view="stream" class="inline-flex items-center justify-center px-4 py-2 text-sm font-medium rounded-full text-white bg-yellow-600 hover:bg-yellow-700 transition duration-300">
                        View/Complete Your Stream Selection & Report &rarr;
                    </a>
                </div>

                <form id="counselling-form" class="space-y-6">
                    <div>
                        <label for="c_name" class="block text-sm font-medium text-gray-700">Your Name</label>
                        <input type="text" id="c_name" name="c_name" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm" required>
                    </div>
                    <div>
                        <label for="c_phone" class="block text-sm font-medium text-gray-700">Phone Number</label>
                        <input type="tel" id="c_phone" name="c_phone" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm" required>
                    </div>
                    <div>
                        <label for="c_issue" class="block text-sm font-medium text-gray-700">What is your primary career concern? (For AI analysis)</label>
                        <textarea id="c_issue" name="c_issue" rows="4" placeholder="e.g., I'm confused between engineering and commerce." class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm resize-none" required></textarea>
                    </div>
                    <div>
                        <label for="c_date" class="block text-sm font-medium text-gray-700">Preferred Date</label>
                        <input type="date" id="c_date" name="c_date" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg shadow-sm" required>
                    </div>
                    <button type="submit" class="w-full flex justify-center py-3 px-4 border border-transparent rounded-lg shadow-lg text-lg font-medium text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500 transition duration-300">
                        Request Booking
                    </button>
                </form>
            </div>
        </section>

    </main>
    
    <div id="auth-modal" class="fixed inset-0 bg-gray-600 bg-opacity-75 overflow-y-auto h-full w-full hidden z-50">
        <div class="relative top-20 mx-auto p-5 border w-96 shadow-lg rounded-md bg-white">
            <h3 id="auth-title" class="text-2xl font-bold text-gray-900 mb-6 text-center">Gmail Login (One-Time Setup)</h3>
            <form id="auth-form" class="space-y-4">
                <div>
                    <label for="auth-id" class="block text-sm font-medium text-gray-700">Personal Gmail ID</label>
                    <input type="email" id="auth-id" name="userId" placeholder="your.name@gmail.com" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg" required>
                </div>
                
                <div id="auth-token-field">
                    <label for="auth-token" class="block text-sm font-medium text-gray-700">
                        One-Time API Token (Paste Here)
                    </label>
                    <input type="text" id="auth-token" name="apiToken" placeholder="Paste the generated token here" class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-lg" required>
                    <p class="text-xs text-gray-500 mt-1">
                        *Use the demo token: **UNFOLD-SECURE-2024-TOKEN**. This will be saved to your PC.*
                    </p>
                </div>

                <button type="submit" id="auth-submit-btn" class="w-full py-2 px-4 border border-transparent rounded-lg shadow-sm text-white bg-green-600 hover:bg-green-700 transition duration-300">
                    Generate Token & Sign In
                </button>
            </form>
            <button onclick="closeAuthModal()" class="absolute top-3 right-3 text-gray-400 hover:text-gray-600 text-xl font-bold">&times;</button>
        </div>
    </div>

    <div id="email-modal" onclick="this.style.display='none';" style="display: none;">
        <div class="email-content-box" onclick="event.stopPropagation()">
            <div id="email-content" class="bg-white p-6 rounded-lg">
                </div>
            <button onclick="document.getElementById('email-modal').style.display='none';" class="mt-4 w-full py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700">Close Email View</button>
        </div>
    </div>


    <div id="chatbot-icon" onclick="toggleChatbotModal()" class="bg-indigo-500 p-4 rounded-full shadow-2xl text-white">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 10h.01M12 10h.01M16 10h.01M9 16l-4.5 4.5a1.5 1.5 0 01-2.121 0l-.354-.354a1.5 1.5 0 010-2.121L5 14m14 1a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
    </div>

    <div id="chatbot-modal" class="flex flex-col rounded-2xl overflow-hidden shadow-2xl">
        <div class="p-4 bg-indigo-600 text-white flex justify-between items-center">
            <h4 class="text-xl font-semibold">Career Guide AI (Anu) 🇮🇳</h4>
            <button onclick="toggleChatbotModal()" class="text-white hover:text-indigo-200 text-2xl font-bold">&times;</button>
        </div>

        <div id="chat-messages" class="flex-grow p-4 space-y-4 overflow-y-auto flex flex-col">
            <div class="ai-message">
                **Anu:** Namaste! 👋 I'm Anu, your AI Career Guide. I can help you understand your test results, explore streams, or answer any career question you have! Ask me anything!
            </div>
            </div>

        <form id="chat-form" class="p-4 border-t border-gray-200 flex">
            <input type="text" id="chat-input" placeholder="Ask a question..." class="flex-grow px-3 py-2 border border-gray-300 rounded-l-lg focus:outline-none focus:ring-2 focus:ring-indigo-500">
            <button type="submit" class="bg-indigo-600 text-white px-4 py-2 rounded-r-lg hover:bg-indigo-700 transition duration-300">
                Send
            </button>
        </form>
    </div>

    <footer class="bg-gray-800 text-white py-8 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <p class="text-xl font-semibold mb-3">UNFOLD</p>
            <p class="text-sm text-gray-400">&copy; 2024 UNFOLD Career Services. All rights reserved.</p>
        </div>
    </footer>

    <script>
        // ===============================================
        // GLOBAL DATA & STATE MANAGEMENT (UNCHANGED)
        // ===============================================
        
        let loggedInUser = localStorage.getItem('loggedInUser');
        let latestUserSelection = JSON.parse(localStorage.getItem('latestSelection')) || {};
        let quizTimerInterval; 
        let quizTimeRemaining = 3600; // 60 minutes in seconds
        let chatbotContext = latestUserSelection; 
        let currentQuizQuestions = []; // Stores the 30 randomly selected questions for the current session

        // SIMULATED AUTHENTICATION DATA (For demonstration)
        const VALID_DEMO_TOKEN = 'UNFOLD-SECURE-2024-TOKEN';
        
        // Data structure for subjects
        const streamData = {
            science: {
                title: 'Science Stream Subjects',
                core: ['English', 'Physics', 'Chemistry'],
                elective: ['Mathematics (PCM)', 'Biology (PCB)', 'Computer Science'],
                optional: ['Physical Education', 'Psychology', 'Economics']
            },
            commerce: {
                title: 'Commerce Stream Subjects',
                core: ['English', 'Accountancy', 'Business Studies'],
                elective: ['Economics', 'Mathematics', 'Informatics Practices'],
                optional: ['Physical Education', 'Entrepreneurship', 'Legal Studies']
            },
            humanities: {
                title: 'Humanities Stream Subjects',
                core: ['English', 'History', 'Political Science'],
                elective: ['Psychology', 'Sociology', 'Geography'],
                optional: ['Fine Arts', 'Music', 'Media Studies']
            }
        };

        // NEW: FULL POOL OF 30 PSYCHOMETRIC-STYLE QUESTIONS
        // Area mapping: S=Science, C=Commerce, H=Humanities, A=Aptitude, P=Personality
        const FULL_QUESTION_POOL = [
            { question: "I enjoy spending time analyzing complex data sets or statistical reports.", area: 'Aptitude' },
            { question: "I can easily spot errors and inconsistencies in written documents or numerical lists.", area: 'Aptitude' },
            { question: "When faced with a difficult problem, I break it down into smaller, logical steps before attempting a solution.", area: 'Aptitude' },
            { question: "I am comfortable with abstract concepts and theoretical models (e.g., physics principles, philosophical ideas).", area: 'S' },
            { question: "I often think in terms of cause-and-effect relationships and predict potential outcomes.", area: 'S' },
            { question: "I find it easy to explain complicated ideas to others in a simple, clear manner.", area: 'Aptitude' },
            { question: "I enjoy reading long articles or books that focus on detailed information and evidence.", area: 'H' },
            { question: "I would prefer to write a detailed report rather than create a visual presentation.", area: 'H' },
            { question: "I quickly understand the main point of a spoken conversation or lecture, even if it is unstructured.", area: 'Aptitude' },
            { question: "I am skilled at noticing non-verbal cues and understanding the emotions of others.", area: 'H' },
            
            { question: "I am fascinated by how biological systems work, from the human body to ecosystems.", area: 'S' },
            { question: "I enjoy experimenting and working with technical equipment, tools, or software.", area: 'S' },
            { question: "I would like a career that involves discovering new materials or solving complex engineering challenges.", area: 'S' },
            { question: "My favorite subjects involve mathematical formulas and precise, systematic procedures.", area: 'S' },
            { question: "I am keen to read about the latest scientific breakthroughs and medical innovations.", area: 'S' },
            
            { question: "I am interested in how the stock market works and how companies make money.", area: 'C' },
            { question: "I find legal documents, contracts, and financial regulations engaging to read.", area: 'C' },
            { question: "I enjoy activities that involve managing budgets, saving, or tracking personal finances.", area: 'C' },
            { question: "I am drawn to career fields like banking, accounting, or corporate management.", area: 'C' },
            { question: "I like negotiating and trying to find the most profitable solution in a scenario.", area: 'C' },

            { question: "I enjoy subjects that involve debating and analyzing different historical perspectives.", area: 'H' },
            { question: "I am interested in social justice issues and the study of human behavior (e.g., psychology, sociology).", area: 'H' },
            { question: "I like expressing my ideas through writing, drawing, music, or other artistic mediums.", area: 'H' },
            { question: "I prefer exploring career paths related to public service, journalism, or teaching.", area: 'H' },
            { question: "I enjoy learning foreign languages and understanding different cultures.", area: 'H' },
            
            { question: "I take the initiative to lead a group project when no one else steps up.", area: 'Personality' },
            { question: "I prefer working independently where I can control the pace and details of my own work.", area: 'Personality' },
            { question: "I am always the one to double-check my work for small errors before submitting it.", area: 'Personality' },
            { question: "I thrive in a fast-paced environment where priorities change often.", area: 'Personality' },
            { question: "I find energy in brainstorming ideas and collaborating closely with a large team.", area: 'Personality' }
        ];

        // Function to shuffle an array (Fisher-Yates)
        const shuffleArray = (array) => {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // ===============================================
        // UTILITY FUNCTIONS (Messaging, Rendering, Email, Login Check)
        // ===============================================
        
        const showMessage = (message, isSuccess = true) => {
            const box = document.getElementById('message-box');
            box.textContent = message;
            box.className = 'fixed top-20 right-5 z-50 p-4 rounded-lg shadow-xl text-white transition-all duration-300';
            box.classList.add(isSuccess ? 'bg-indigo-600' : 'bg-red-600');
            box.classList.remove('translate-x-full', 'opacity-0');
            box.classList.add('translate-x-0', 'opacity-100');

            setTimeout(() => {
                box.classList.remove('translate-x-0', 'opacity-100');
                box.classList.add('translate-x-full', 'opacity-0');
            }, 5000);
        };
        
        // Central function to check for login
        const requireLogin = (e, callback = null) => {
            if (!loggedInUser) {
                e.preventDefault();
                showMessage('Please log in through your Gmail ID first to access this feature.', false);
                openAuthModal();
                return false;
            }
            if (callback) 
                callback();
            return true;
        };
        
        // ===============================================
        // VIEW SWITCHING AND ROUTING
        // ===============================================
        
        const views = document.querySelectorAll('.view-content');
        const navLinks = document.querySelectorAll('.nav-link');

        const navigateToView = (targetViewId) => {
            views.forEach(view => {
                view.classList.add('hidden');
            });
            const targetView = document.getElementById(`view-${targetViewId}`);
            if (targetView) {
                targetView.classList.remove('hidden');
            }

            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('data-view') === targetViewId) {
                    link.classList.add('active');
                }
            });
        };

        const handleHashChange = () => {
            const hash = window.location.hash.substring(1);
            const targetViewId = hash || 'home'; 
            navigateToView(targetViewId);
        };

        window.onload = () => {
            handleHashChange();
            // Attach click listeners to internal navigation links
            document.querySelectorAll('.view-content-link').forEach(link => {
                link.addEventListener('click', (e) => {
                    const viewId = link.getAttribute('data-view');
                    if (viewId && link.getAttribute('href').startsWith('#')) {
                        e.preventDefault();
                        window.location.hash = viewId;
                    }
                });
            });

            // Update Auth button text based on local storage
            updateAuthButton();

            // Set up form listeners
            document.getElementById('psychometric-form').addEventListener('submit', startQuiz);
            document.getElementById('quiz-form').addEventListener('submit', handleQuizSubmit);
            document.getElementById('counselling-form').addEventListener('submit', handleCounsellingSubmit);
        };

        window.addEventListener('hashchange', handleHashChange);
        
        // ===============================================
        // AUTHENTICATION FUNCTIONS
        // ===============================================
        
        const authModal = document.getElementById('auth-modal');
        const authButton = document.getElementById('auth-button');

        const updateAuthButton = () => {
            if (loggedInUser) {
                // Extract the username (part before the @)
                const username = loggedInUser.split('@')[0]; 
                
                // FIXED: Displaying only the username and a subtle logout indicator
                authButton.textContent = `${username} (Out)`; 
                
                // Change styles for smaller button when logged in (less aggressive color)
                authButton.classList.remove('bg-indigo-600', 'px-4', 'py-2', 'text-base');
                authButton.classList.add('bg-gray-500', 'hover:bg-gray-600', 'px-3', 'py-1.5', 'text-sm');
                authButton.onclick = logoutUser;
            } else {
                authButton.textContent = 'Sign In with Gmail';
                // Reset styles to Sign In defaults
                authButton.classList.add('bg-indigo-600');
                authButton.classList.remove('bg-gray-500', 'hover:bg-gray-600');
                authButton.onclick = openAuthModal;
            }
        };

        const openAuthModal = () => {
            authModal.classList.remove('hidden');
        };

        const closeAuthModal = () => {
            authModal.classList.add('hidden');
        };

        const logoutUser = () => {
            localStorage.removeItem('loggedInUser');
            loggedInUser = null;
            updateAuthButton();
            showMessage('Successfully logged out.', true);
        };
        
        document.getElementById('auth-form').addEventListener('submit', (e) => {
            e.preventDefault();
            const email = document.getElementById('auth-id').value.trim();
            const token = document.getElementById('auth-token').value.trim();

            if (!email.endsWith('@gmail.com')) {
                showMessage('Please use a valid Gmail ID.', false);
                return;
            }
            if (token !== VALID_DEMO_TOKEN) {
                showMessage('Invalid API Token. Please check the hint.', false);
                return;
            }

            loggedInUser = email;
            localStorage.setItem('loggedInUser', email);
            closeAuthModal();
            updateAuthButton();
            showMessage(`Login successful! Welcome back, ${email.split('@')[0]}.`, true);
        });

        // ===============================================
        // PSYCHOMETRIC TEST FUNCTIONS
        // ===============================================

        const generateQuizQuestions = () => {
            // Select 5 questions from each area (total 25)
            const sciQuestions = FULL_QUESTION_POOL.filter(q => q.area === 'S').slice(0, 5);
            const commQuestions = FULL_QUESTION_POOL.filter(q => q.area === 'C').slice(0, 5);
            const humQuestions = FULL_QUESTION_POOL.filter(q => q.area === 'H').slice(0, 5);
            const aptitudeQuestions = FULL_QUESTION_POOL.filter(q => q.area === 'Aptitude').slice(0, 5);
            const personalityQuestions = FULL_QUESTION_POOL.filter(q => q.area === 'Personality').slice(0, 5);

            currentQuizQuestions = shuffleArray([
                ...sciQuestions, 
                ...commQuestions, 
                ...humQuestions, 
                ...aptitudeQuestions, 
                ...personalityQuestions
            ]); 

            const container = document.getElementById('quiz-questions-container');
            container.innerHTML = ''; // Clear previous questions

            currentQuizQuestions.forEach((q, index) => {
                const qElement = document.createElement('div');
                qElement.className = 'p-4 border border-gray-200 rounded-lg bg-white shadow-sm';
                qElement.innerHTML = `
                    <p class="font-semibold text-gray-800 mb-3">Q${index + 1}: ${q.question}</p>
                    <div class="flex flex-wrap gap-4 text-sm" data-question-index="${index}">
                        <label class="flex items-center space-x-2 cursor-pointer">
                            <input type="radio" name="q${index}" value="5" class="text-indigo-600 focus:ring-indigo-500" required>
                            <span>Strongly Agree</span>
                        </label>
                        <label class="flex items-center space-x-2 cursor-pointer">
                            <input type="radio" name="q${index}" value="4" class="text-indigo-600 focus:ring-indigo-500">
                            <span>Agree</span>
                        </label>
                        <label class="flex items-center space-x-2 cursor-pointer">
                            <input type="radio" name="q${index}" value="3" class="text-indigo-600 focus:ring-indigo-500">
                            <span>Neutral</span>
                        </label>
                        <label class="flex items-center space-x-2 cursor-pointer">
                            <input type="radio" name="q${index}" value="2" class="text-indigo-600 focus:ring-indigo-500">
                            <span>Disagree</span>
                        </label>
                        <label class="flex items-center space-x-2 cursor-pointer">
                            <input type="radio" name="q${index}" value="1" class="text-indigo-600 focus:ring-indigo-500">
                            <span>Strongly Disagree</span>
                        </label>
                    </div>
                `;
                container.appendChild(qElement);
            });
        };
        
        const startQuizTimer = () => {
            const timerDisplay = document.getElementById('quiz-timer');
            clearInterval(quizTimerInterval);
            quizTimeRemaining = 3600; // Reset to 60 minutes
            
            const updateTimer = () => {
                const minutes = String(Math.floor(quizTimeRemaining / 60)).padStart(2, '0');
                const seconds = String(quizTimeRemaining % 60).padStart(2, '0');
                timerDisplay.textContent = `${minutes}:${seconds}`;

                if (quizTimeRemaining <= 0) {
                    clearInterval(quizTimerInterval);
                    alert('Time is up! Your quiz results will now be submitted.');
                    document.getElementById('quiz-form').requestSubmit();
                } else {
                    quizTimeRemaining--;
                }
            };
            
            updateTimer(); 
            quizTimerInterval = setInterval(updateTimer, 1000);
            
            // Allow resetting the quiz mid-test
            document.getElementById('quiz-reset-btn').onclick = () => {
                if (confirm("Are you sure you want to reset the test? All answers will be lost.")) {
                    clearInterval(quizTimerInterval);
                    document.getElementById('psychometric-form').classList.remove('hidden');
                    document.getElementById('psychometric-quiz-area').classList.add('hidden');
                    document.getElementById('quiz-result-area').classList.add('hidden');
                    showMessage('Test progress has been reset.', false);
                }
            };
        };

        const startQuiz = (e) => {
            e.preventDefault();
            if (!requireLogin(e)) return;

            const form = e.target;
            const name = form.name.value;
            const email = form.email.value;
            const grade = form.grade.value;
            
            // Store preliminary data
            latestUserSelection.name = name;
            latestUserSelection.email = email;
            latestUserSelection.grade = grade;

            // Hide form, show quiz
            form.classList.add('hidden');
            document.getElementById('quiz-result-area').classList.add('hidden');
            document.getElementById('psychometric-quiz-area').classList.remove('hidden');

            generateQuizQuestions();
            startQuizTimer();
            showMessage('Psychometric test started! Time is counting down.', true);
        };
        
        const handleQuizSubmit = (e) => {
            e.preventDefault();
            clearInterval(quizTimerInterval);
            
            const form = e.target;
            const results = { S: 0, C: 0, H: 0, Aptitude: 0, Personality: 0 };
            const counts = { S: 0, C: 0, H: 0, Aptitude: 0, Personality: 0 };
            
            currentQuizQuestions.forEach((q, index) => {
                const answer = form[`q${index}`].value;
                const area = q.area;
                const score = parseInt(answer);
                
                if (!isNaN(score)) {
                    results[area] += score;
                    counts[area]++;
                }
            });

            // Calculate average scores (out of 5)
            const scores = {};
            for (const area in results) {
                scores[area] = counts[area] > 0 ? (results[area] / counts[area]) : 0;
            }

            // Determine recommended stream based on S, C, H scores
            const streamScores = {
                'Science (PCM/PCB)': scores.S,
                'Commerce': scores.C,
                'Humanities': scores.H
            };

            // Simple recommendation logic: highest score wins
            let recommendedStream = '';
            let maxScore = -1;

            for (const stream in streamScores) {
                if (streamScores[stream] > maxScore) {
                    maxScore = streamScores[stream];
                    recommendedStream = stream;
                } else if (streamScores[stream] === maxScore) {
                    recommendedStream += ` / ${stream}`; // Handle ties
                }
            }
            
            // Save results to state
            latestUserSelection.quizResults = scores;
            latestUserSelection.recommendedStream = recommendedStream;
            localStorage.setItem('latestSelection', JSON.stringify(latestUserSelection));
            
            // Display Results
            displayQuizResults(scores, recommendedStream);
            
            // Hide quiz, show form/results
            document.getElementById('psychometric-quiz-area').classList.add('hidden');
            document.getElementById('psychometric-form').classList.remove('hidden');
        };

        const displayQuizResults = (scores, recommendedStream) => {
            const resultsArea = document.getElementById('quiz-result-area');
            const resultStreamElement = document.getElementById('result-stream');
            const resultScoresElement = document.getElementById('result-scores');
            
            resultsArea.classList.remove('hidden');
            
            resultStreamElement.textContent = recommendedStream;
            
            let scoresHTML = '';
            Object.entries(scores).forEach(([area, score]) => {
                scoresHTML += `
                    <div class="flex justify-between items-center text-lg">
                        <span class="font-medium">${area} Interest/Aptitude:</span>
                        <span class="font-bold text-gray-800">${score.toFixed(2)} / 5.00</span>
                    </div>
                `;
            });
            resultScoresElement.innerHTML = scoresHTML;
            
            showMessage('Results generated! Check the report below.', true);
        };
        
        // NEW: Action button handler functions (Simulated functionality)
        const handleRedoTest = () => {
            if (confirm("Are you sure you want to redo the test? Your previous results will be overwritten.")) {
                document.getElementById('psychometric-form').classList.remove('hidden');
                document.getElementById('quiz-result-area').classList.add('hidden');
                document.getElementById('psychometric-form').reset();
                showMessage('Assessment form reset. Fill out the details to start again.', false);
            }
        };

        const handleDownloadReport = () => {
            if (!latestUserSelection.quizResults) {
                showMessage('No test results available to download. Please complete the quiz first.', false);
                return;
            }
            const name = latestUserSelection.name || 'Student';
            const data = JSON.stringify(latestUserSelection, null, 2);
            // Simulated download by opening data in a new tab (real download requires server logic)
            const blob = new Blob([data], { type: 'text/json' });
            const url = URL.createObjectURL(blob);
            window.open(url, '_blank');
            showMessage(`Downloading career report for ${name}...`, true);
        };

        const handleGenerateRoadmap = () => {
             if (!latestUserSelection.recommendedStream) {
                showMessage('Please complete the psychometric test first to determine your stream before generating an AI Roadmap.', false);
                return;
            }
            const stream = latestUserSelection.recommendedStream;
            const user = loggedInUser.split('@')[0];
            
            // Simulated AI roadmap generation: opens chatbot with a prompt
            toggleChatbotModal();
            addMessage(`Generate a detailed 5-year career roadmap for the ${stream} stream, specifically focusing on potential careers for ${user}.`, true);
            
            setTimeout(() => {
                const response = `**AI Roadmap for ${stream}**: Great choice, ${user}! I've generated a draft roadmap focusing on ${stream.split(' ')[0]}. I recommend checking the Stream Selection tab next for subject planning, and booking a counseling session to discuss this roadmap in detail.`;
                addMessage(response);
            }, 1500);
            showMessage('AI Roadmap generation started. Check the chatbot window for results!', true);
        };


        // ===============================================
        // STREAM SELECTION FUNCTIONS
        // ===============================================

        const selectStream = (streamName) => {
            if (!requireLogin(event)) return;

            // Clear selected class from all stream cards
            document.querySelectorAll('.stream-card').forEach(card => {
                card.classList.remove('selected');
                card.classList.remove('border-indigo-700');
            });

            // Add selected class to the clicked card
            const selectedCard = event.currentTarget;
            selectedCard.classList.add('selected');
            selectedCard.classList.add('border-indigo-700');

            latestUserSelection.selectedStream = streamName;
            
            renderSubjects(streamName);
            document.getElementById('subject-selection-container').classList.remove('hidden');
        };
        
        const renderSubjects = (streamName) => {
            const data = streamData[streamName];
            const titleElement = document.getElementById('subject-title');
            const coreList = document.getElementById('core-subjects-list');
            const electiveList = document.getElementById('elective-subjects-list');
            const optionalList = document.getElementById('optional-subjects-list');

            titleElement.textContent = `${data.title} Selection`;
            
            // Render Core Subjects
            coreList.innerHTML = `
                <h4 class="text-xl font-semibold text-gray-700 mb-2">Core Subjects (Mandatory)</h4>
                ${data.core.map(subject => `
                    <div class="p-3 bg-gray-200 rounded-md font-medium text-gray-800">${subject} <span class="text-red-500 text-sm">(Fixed)</span></div>
                `).join('')}
            `;
            
            // Render Elective Subjects (Radio buttons or checkboxes with validation required later)
            electiveList.innerHTML = `
                <h4 class="text-xl font-semibold text-gray-700 mb-2 mt-6">Elective Subjects (Choose 1 or 2)</h4>
                ${data.elective.map((subject, index) => `
                    <label class="flex items-center space-x-3 p-3 bg-white border rounded-md shadow-sm hover:border-indigo-500">
                        <input type="checkbox" name="elective" value="${subject}" class="h-5 w-5 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500">
                        <span class="text-gray-900">${subject}</span>
                    </label>
                `).join('')}
            `;

            // Render Optional Subjects (Checkbox)
            optionalList.innerHTML = `
                <h4 class="text-xl font-semibold text-gray-700 mb-2 mt-6">Optional Subjects (Choose up to 1)</h4>
                ${data.optional.map(subject => `
                    <label class="flex items-center space-x-3 p-3 bg-white border rounded-md shadow-sm hover:border-indigo-500">
                        <input type="checkbox" name="optional" value="${subject}" class="h-5 w-5 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500">
                        <span class="text-gray-900">${subject}</span>
                    </label>
                `).join('')}
            `;
        };
        
        document.getElementById('subject-form').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const form = e.target;
            const selectedElectives = Array.from(form.querySelectorAll('input[name="elective"]:checked')).map(cb => cb.value);
            const selectedOptionals = Array.from(form.querySelectorAll('input[name="optional"]:checked')).map(cb => cb.value);
            
            // Validation Logic
            if (selectedElectives.length === 0 || selectedElectives.length > 2) {
                showMessage('You must select between 1 and 2 Elective subjects.', false);
                return;
            }
            if (selectedOptionals.length > 1) {
                showMessage('You may only select a maximum of 1 Optional subject.', false);
                return;
            }
            
            // Finalize subject selection
            const stream = latestUserSelection.selectedStream;
            const core = streamData[stream].core;
            
            latestUserSelection.finalSubjects = {
                stream,
                core,
                electives: selectedElectives,
                optional: selectedOptionals[0] || null
            };
            
            localStorage.setItem('latestSelection', JSON.stringify(latestUserSelection));
            
            showMessage('Subject selection saved! Your detailed career report is ready for viewing/download.', true);
            // In a real app, this would trigger a report generation service
        });
        
        // ===============================================
        // COUNSELLING & BOOKING FUNCTIONS
        // ===============================================

        const handleCounsellingSubmit = (e) => {
            e.preventDefault();
            if (!requireLogin(e)) return;
            
            if (!latestUserSelection.finalSubjects) {
                showMessage('Please complete your Stream Selection first to ensure the counselor has your report.', false);
                return;
            }

            const form = e.target;
            const bookingDetails = {
                name: form.c_name.value,
                phone: form.c_phone.value,
                issue: form.c_issue.value,
                date: form.c_date.value,
                stream: latestUserSelection.selectedStream,
                subjects: latestUserSelection.finalSubjects
            };

            // Simulated booking success
            console.log('Counselling Booking:', bookingDetails);
            
            // Reset form
            form.reset();
            
            showMessage(`Booking requested for ${bookingDetails.date}. A confirmation email will be sent to ${loggedInUser}.`, true);
        };
        
        // ===============================================
        // CHATBOT FUNCTIONS
        // ===============================================

        const chatbotModal = document.getElementById('chatbot-modal');
        const chatMessagesContainer = document.getElementById('chat-messages');

        const toggleChatbotModal = () => {
            chatbotModal.style.display = chatbotModal.style.display === 'flex' ? 'none' : 'flex';
        };

        const addMessage = (text, isUser = false) => {
            const messageElement = document.createElement('div');
            messageElement.className = isUser ? 'user-message' : 'ai-message';
            messageElement.innerHTML = isUser ? `**You:** ${text}` : `**Anu:** ${text}`;
            chatMessagesContainer.appendChild(messageElement);
            chatMessagesContainer.scrollTop = chatMessagesContainer.scrollHeight; // Scroll to bottom
        };

        const simulateAIResponse = (query) => {
            const lowerQuery = query.toLowerCase();
            let response = "I'm still learning the nuances of your query. Please be specific about **streams**, **subjects**, or your **psychometric results** to get the best advice!";

            if (lowerQuery.includes('stream') && lowerQuery.includes('best')) {
                const stream = latestUserSelection.recommendedStream || 'undetermined';
                response = `Based on the latest data (currently **${stream}** recommended), I suggest you review the 'Stream Selection' tab. If you haven't taken the test, please do so for an accurate result.`;
            } else if (lowerQuery.includes('subjects') && latestUserSelection.finalSubjects) {
                const subs = latestUserSelection.finalSubjects.electives.join(', ');
                response = `Your final selected subjects for the **${latestUserSelection.selectedStream}** stream are Core: Physics, Chemistry and Electives: **${subs}** (and Optional: ${latestUserSelection.finalSubjects.optional || 'None'}).`;
            } else if (lowerQuery.includes('fees') || lowerQuery.includes('cost')) {
                response = "The psychometric test is **₹500**. The expert counseling session is **₹1500**. However, the initial report is available for free once you sign up and complete the test!";
            } else if (lowerQuery.includes('engineer')) {
                 response = "To become an engineer, you should focus on the **Science stream (PCM)**, perform well in JEE/CET exams, and focus on subjects like Maths and Physics. Do you want to see the Science subject options?";
            }
            
            addMessage(response);
        };

        const handleChatSubmit = (e) => {
            e.preventDefault();
            const input = document.getElementById('chat-input');
            const query = input.value.trim();
            
            if (query === '') return;
            
            addMessage(query, true);
            input.value = '';

            // Simulate a brief delay for AI processing
            setTimeout(() => {
                simulateAIResponse(query);
            }, 1000);
        };

        document.getElementById('chat-form').addEventListener('submit', handleChatSubmit);
    </script>
</body>
</html>
