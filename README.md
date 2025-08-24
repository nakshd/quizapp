# quizapp
<html lang="en">
 <head>
  <meta charset="utf-8"/>
  <meta content="width=device-width, initial-scale=1" name="viewport"/>
  <title>
   Quiz Management System
  </title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" rel="stylesheet"/>
  <style>
   .hidden {
            display: none;
        }
        .question-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.12);
        }
        .option-item:hover {
            background-color: #f0f7ff;
        }
        .correct-answer {
            background-color: #e6ffed;
            border-left: 4px solid #38a169;
        }
        .wrong-answer {
            background-color: #fff5f5;
            border-left: 4px solid #e53e3e;
        }
        #quizTimer {
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        /* Animation for login buttons */
        .btn-animate {
            position: relative;
            overflow: hidden;
            transition: color 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        .btn-animate::before {
            content: '';
            position: absolute;
            top: 50%;
            left: -100%;
            width: 200%;
            height: 100%;
            background: linear-gradient(90deg, rgba(255,255,255,0) 0%, rgba(255,255,255,0.5) 50%, rgba(255,255,255,0) 100%);
            transform: translateY(-50%) skewX(-20deg);
            transition: left 0.7s ease;
            pointer-events: none;
            border-radius: 0.5rem;
        }
        .btn-animate:hover::before {
            left: 100%;
        }
        /* Header shadow and gradient */
        header {
            background: linear-gradient(90deg, #4c51bf, #667eea);
            box-shadow: 0 4px 12px rgba(102,126,234,0.4);
        }
        header.bg-green-600 {
            background: linear-gradient(90deg, #38a169, #48bb78);
            box-shadow: 0 4px 12px rgba(72,187,120,0.4);
        }
        /* Scrollbar styling for tables */
        ::-webkit-scrollbar {
            height: 8px;
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb {
            background: #a0aec0;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #718096;
        }
        /* Table header background */
        thead.bg-gray-50 {
            background: #f7fafc;
            box-shadow: inset 0 -1px 0 #e2e8f0;
        }
        /* Card shadows */
        .card-shadow {
            box-shadow: 0 8px 20px rgba(0,0,0,0.08);
            transition: box-shadow 0.3s ease;
        }
        .card-shadow:hover {
            box-shadow: 0 12px 30px rgba(0,0,0,0.12);
        }
        /* Smooth transitions */
        button, input, textarea {
            transition: all 0.3s ease;
        }
        /* Form focus */
        input:focus, textarea:focus {
            outline: none;
            box-shadow: 0 0 0 3px rgba(99,102,241,0.5);
            border-color: #6366f1;
        }
        /* Responsive container max width */
        .container {
            max-width: 1024px;
        }
        /* Subtle button hover */
        button:hover {
            filter: brightness(1.05);
        }
        /* Rounded inputs */
        input, textarea {
            border-radius: 0.5rem;
        }
        /* Question review styling */
        #questionReview > div {
            border-left-width: 6px;
            padding-left: 1rem;
            border-radius: 0.5rem;
        }
        /* Scrollable quiz questions container */
        #quizQuestionsTaking {
            max-height: 60vh;
            overflow-y: auto;
            padding-right: 0.5rem;
        }
        /* Scrollbar for quiz questions */
        #quizQuestionsTaking::-webkit-scrollbar {
            width: 6px;
        }
        #quizQuestionsTaking::-webkit-scrollbar-thumb {
            background-color: #a0aec0;
            border-radius: 3px;
        }
        /* Responsive image */
        img {
            max-width: 100%;
            height: auto;
        }
  </style>
 </head>
 <body class="bg-gradient-to-br from-gray-100 via-white to-gray-100 font-sans text-gray-800">
  <!-- Main Container -->
  <div class="min-h-screen flex flex-col">
   <!-- Login Selection Screen -->
   <div class="flex flex-col items-center justify-center flex-grow p-6" id="loginSelectionScreen">
    <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl overflow-hidden border border-gray-200">
     <div class="bg-indigo-700 py-8 px-10 text-center">
      <h1 class="text-4xl font-extrabold text-white tracking-tight drop-shadow-lg">
       Quiz Management System
      </h1>
      <p class="text-indigo-200 mt-2 text-lg font-medium">
       Select your role to continue
      </p>
     </div>
     <div class="p-10 space-y-8">
      <button class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold py-4 px-6 rounded-xl transition duration-300 flex items-center justify-center btn-animate shadow-lg shadow-indigo-300/50" onclick="showLoginForm('teacher')">
       <svg class="h-7 w-7 mr-3" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
       </svg>
       I'm a Teacher
      </button>
      <button class="w-full bg-green-600 hover:bg-green-700 text-white font-extrabold py-4 px-6 rounded-xl transition duration-300 flex items-center justify-center btn-animate shadow-lg shadow-green-300/50" onclick="showLoginForm('student')">
       <svg class="h-7 w-7 mr-3" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
       </svg>
       I'm a Student
      </button>
      <div class="mt-10 rounded-xl overflow-hidden border border-gray-200 shadow-lg">
       <img alt="Illustration of a diverse group of students and teachers collaborating in an interactive classroom environment with digital devices and educational materials" src="https://storage.googleapis.com/a1aa/image/936781e1-722d-42fd-9562-2bf6ad405d93.jpg" class="w-full h-auto object-cover"/>
      </div>
     </div>
    </div>
   </div>
   <!-- Teacher Login Form -->
   <div class="hidden flex-col items-center justify-center flex-grow p-6 bg-indigo-50" id="teacherLoginForm">
    <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl overflow-hidden border border-indigo-300">
     <div class="bg-gradient-to-r from-indigo-700 to-indigo-500 py-8 px-10 text-center">
      <h2 class="text-3xl font-extrabold text-white tracking-wide drop-shadow-md">
       Teacher Login
      </h2>
     </div>
     <div class="p-10">
      <form class="space-y-8" id="teacherLogin" onsubmit="loginTeacher(event)">
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="teacherEmail">
         Email
        </label>
        <input autocomplete="email" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="teacherEmail" required="" type="email"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="teacherPassword">
         Password
        </label>
        <input autocomplete="current-password" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="teacherPassword" required="" type="password"/>
       </div>
       <button class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold py-4 rounded-2xl transition duration-300 btn-animate shadow-lg shadow-indigo-400/50" type="submit">
        Sign In
       </button>
       <p class="text-center text-sm text-gray-600 mt-4">
        Don't have an account?
        <span class="text-indigo-600 cursor-pointer hover:underline font-semibold" onclick="showRegisterForm('teacher')">
         Register
        </span>
       </p>
      </form>
     </div>
    </div>
   </div>
   <!-- Teacher Registration Form -->
   <div class="hidden flex-col items-center justify-center flex-grow p-6 bg-indigo-50" id="teacherRegisterForm">
    <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl overflow-hidden border border-indigo-300">
     <div class="bg-gradient-to-r from-indigo-700 to-indigo-500 py-8 px-10 text-center">
      <h2 class="text-3xl font-extrabold text-white tracking-wide drop-shadow-md">
       Teacher Registration
      </h2>
     </div>
     <div class="p-10">
      <form class="space-y-8" id="teacherRegister" onsubmit="registerTeacher(event)">
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="teacherRegName">
         Full Name
        </label>
        <input autocomplete="name" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="teacherRegName" required="" type="text"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="teacherRegEmail">
         Email
        </label>
        <input autocomplete="email" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="teacherRegEmail" required="" type="email"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="teacherRegPassword">
         Password
        </label>
        <input autocomplete="new-password" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="teacherRegPassword" required="" type="password"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="teacherRegConfirmPassword">
         Confirm Password
        </label>
        <input autocomplete="new-password" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="teacherRegConfirmPassword" required="" type="password"/>
       </div>
       <button class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold py-4 rounded-2xl transition duration-300 btn-animate shadow-lg shadow-indigo-400/50" type="submit">
        Register
       </button>
       <p class="text-center text-sm text-gray-600 mt-4">
        Already have an account?
        <span class="text-indigo-600 cursor-pointer hover:underline font-semibold" onclick="showLoginForm('teacher')">
         Sign In
        </span>
       </p>
      </form>
     </div>
    </div>
   </div>
   <!-- Student Login Form -->
   <div class="hidden flex-col items-center justify-center flex-grow p-6 bg-green-50" id="studentLoginForm">
    <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl overflow-hidden border border-green-300">
     <div class="bg-gradient-to-r from-green-700 to-green-500 py-8 px-10 text-center">
      <h2 class="text-3xl font-extrabold text-white tracking-wide drop-shadow-md">
       Student Login
      </h2>
     </div>
     <div class="p-10">
      <form class="space-y-8" id="studentLogin" onsubmit="loginStudent(event)">
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="studentEmail">
         Email
        </label>
        <input autocomplete="email" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-green-500 focus:border-green-500 shadow-sm" id="studentEmail" required="" type="email"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="studentPassword">
         Password
        </label>
        <input autocomplete="current-password" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-green-500 focus:border-green-500 shadow-sm" id="studentPassword" required="" type="password"/>
       </div>
       <button class="w-full bg-green-600 hover:bg-green-700 text-white font-extrabold py-4 rounded-2xl transition duration-300 btn-animate shadow-lg shadow-green-400/50" type="submit">
        Sign In
       </button>
       <p class="text-center text-sm text-gray-600 mt-4">
        Don't have an account?
        <span class="text-green-600 cursor-pointer hover:underline font-semibold" onclick="showRegisterForm('student')">
         Register
        </span>
       </p>
      </form>
     </div>
    </div>
   </div>
   <!-- Student Registration Form -->
   <div class="hidden flex-col items-center justify-center flex-grow p-6 bg-green-50" id="studentRegisterForm">
    <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl overflow-hidden border border-green-300">
     <div class="bg-gradient-to-r from-green-700 to-green-500 py-8 px-10 text-center">
      <h2 class="text-3xl font-extrabold text-white tracking-wide drop-shadow-md">
       Student Registration
      </h2>
     </div>
     <div class="p-10">
      <form class="space-y-8" id="studentRegister" onsubmit="registerStudent(event)">
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="studentRegName">
         Full Name
        </label>
        <input autocomplete="name" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-green-500 focus:border-green-500 shadow-sm" id="studentRegName" required="" type="text"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="studentRegEmail">
         Email
        </label>
        <input autocomplete="email" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-green-500 focus:border-green-500 shadow-sm" id="studentRegEmail" required="" type="email"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="studentRegRoll">
         Roll Number
        </label>
        <input autocomplete="off" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-green-500 focus:border-green-500 shadow-sm" id="studentRegRoll" required="" type="text"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="studentRegPassword">
         Password
        </label>
        <input autocomplete="new-password" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-green-500 focus:border-green-500 shadow-sm" id="studentRegPassword" required="" type="password"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="studentRegConfirmPassword">
         Confirm Password
        </label>
        <input autocomplete="new-password" class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-green-500 focus:border-green-500 shadow-sm" id="studentRegConfirmPassword" required="" type="password"/>
       </div>
       <button class="w-full bg-green-600 hover:bg-green-700 text-white font-extrabold py-4 rounded-2xl transition duration-300 btn-animate shadow-lg shadow-green-400/50" type="submit">
        Register
       </button>
       <p class="text-center text-sm text-gray-600 mt-4">
        Already have an account?
        <span class="text-green-600 cursor-pointer hover:underline font-semibold" onclick="showLoginForm('student')">
         Sign In
        </span>
       </p>
      </form>
     </div>
    </div>
   </div>
   <!-- Teacher Dashboard -->
   <div class="hidden min-h-screen flex flex-col" id="teacherDashboard">
    <!-- Header -->
    <header class="text-white shadow-md">
     <div class="container mx-auto px-6 py-5 flex justify-between items-center">
      <h1 class="text-3xl font-extrabold tracking-wide drop-shadow-lg">
       Teacher Dashboard
      </h1>
      <div class="flex items-center space-x-6">
       <div class="flex items-center space-x-3 bg-indigo-700 bg-opacity-80 rounded-full px-4 py-2 shadow-lg">
        <svg class="h-7 w-7 text-indigo-300" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
         <path d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
        </svg>
        <span id="teacherNameDisplay" class="font-semibold text-lg select-none">
         Teacher
        </span>
       </div>
       <button class="bg-white text-indigo-700 px-4 py-2 rounded-full font-semibold shadow-md hover:bg-indigo-50 transition" onclick="logout()">
        Logout
       </button>
      </div>
     </div>
    </header>
    <main class="container mx-auto px-6 py-10 flex-grow">
     <!-- Create New Quiz Section -->
     <section class="mb-12 bg-white rounded-3xl shadow-2xl p-8 card-shadow">
      <h2 class="text-2xl font-extrabold mb-6 text-gray-900 tracking-wide">
       Create New Quiz
      </h2>
      <form class="space-y-6" id="createQuizForm" onsubmit="createQuiz(event)">
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="quizTitle">
         Quiz Title
        </label>
        <input class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="quizTitle" required="" type="text"/>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="quizDescription">
         Description
        </label>
        <textarea class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm resize-none" id="quizDescription" rows="4" placeholder="Optional"></textarea>
       </div>
       <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div>
         <label class="block text-sm font-semibold text-gray-700 mb-2" for="quizTimeLimit">
          Time Limit (minutes)
         </label>
         <input class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="quizTimeLimit" max="120" min="1" type="number" value="30"/>
        </div>
        <div>
         <label class="block text-sm font-semibold text-gray-700 mb-2" for="quizMaxAttempts">
          Max Attempts
         </label>
         <input class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="quizMaxAttempts" max="10" min="1" type="number" value="1"/>
        </div>
       </div>
       <div class="flex justify-end">
        <button class="bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold py-3 px-8 rounded-3xl transition duration-300 shadow-lg shadow-indigo-400/50" type="submit">
         Create Quiz
        </button>
       </div>
      </form>
     </section>
     <!-- Quiz Questions Area (Visible when a quiz is selected) -->
     <section class="hidden bg-white rounded-3xl shadow-2xl p-8 mb-10 card-shadow" id="quizQuestionsSection">
      <div class="flex justify-between items-center mb-6">
       <h3 class="text-2xl font-extrabold text-gray-900 tracking-wide" id="quizQuestionsTitle">
        Quiz:
        <span id="currentQuizTitle" class="text-indigo-600"></span>
       </h3>
       <button class="text-indigo-600 hover:text-indigo-900 font-semibold tracking-wide" onclick="backToQuizzes()">
        &larr; Back to All Quizzes
       </button>
      </div>
      <!-- Add New Question -->
      <form class="space-y-6 mb-10" id="addQuestionForm" onsubmit="addQuestion(event)">
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2" for="questionText">
         Question Text
        </label>
        <textarea class="w-full px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm resize-none" id="questionText" required="" rows="4" placeholder="Enter your question here"></textarea>
       </div>
       <div>
        <label class="block text-sm font-semibold text-gray-700 mb-2">
         Question Type
        </label>
        <div class="flex space-x-8">
         <label class="inline-flex items-center cursor-pointer">
          <input checked="" class="text-indigo-600 focus:ring-indigo-500" name="questionType" type="radio" value="single" onchange="updateOptionsInputType()"/>
          <span class="ml-3 text-gray-800 font-semibold">
           Single Correct Answer
          </span>
         </label>
         <label class="inline-flex items-center cursor-pointer">
          <input class="text-indigo-600 focus:ring-indigo-500" name="questionType" type="radio" value="multiple" onchange="updateOptionsInputType()"/>
          <span class="ml-3 text-gray-800 font-semibold">
           Multiple Correct Answers
          </span>
         </label>
        </div>
       </div>
       <div id="optionsContainer">
        <label class="block text-sm font-semibold text-gray-700 mb-2">
         Options (Mark the correct one(s))
        </label>
        <div class="space-y-3">
         <div class="flex items-center space-x-3">
          <input checked="" class="text-indigo-600 focus:ring-indigo-500" name="correctOption" type="radio" value="0"/>
          <input class="flex-grow px-4 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" placeholder="Option text" required="" type="text"/>
          <button class="text-red-500 hover:text-red-700 transition" onclick="removeOption(this)" type="button" title="Remove Option" aria-label="Remove Option">
           <svg class="h-6 w-6" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
           </svg>
          </button>
         </div>
         <div class="flex items-center space-x-3">
          <input class="text-indigo-600 focus:ring-indigo-500" name="correctOption" type="radio" value="1"/>
          <input class="flex-grow px-4 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" placeholder="Option text" required="" type="text"/>
          <button class="text-red-500 hover:text-red-700 transition" onclick="removeOption(this)" type="button" title="Remove Option" aria-label="Remove Option">
           <svg class="h-6 w-6" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
           </svg>
          </button>
         </div>
        </div>
        <button class="mt-3 text-indigo-600 hover:text-indigo-900 font-semibold flex items-center space-x-2 transition" onclick="addOption()" type="button" aria-label="Add Another Option">
         <svg class="h-5 w-5" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
          <path d="M12 6v6m0 0v6m0-6h6m-6 0H6" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
         </svg>
         <span>Add Another Option</span>
        </button>
       </div>
       <div class="flex justify-end">
        <button class="bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold py-3 px-8 rounded-3xl transition duration-300 shadow-lg shadow-indigo-400/50" type="submit">
         Add Question
        </button>
       </div>
      </form>
      <!-- Existing Questions -->
      <div class="space-y-6" id="questionsList">
       <!-- Questions will be displayed here -->
      </div>
     </section>
     <!-- List of Quizzes -->
     <section>
      <h2 class="text-3xl font-extrabold mb-6 text-gray-900 tracking-wide">
       Your Quizzes
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8" id="quizzesContainer">
       <!-- Quizzes will be displayed here -->
      </div>
     </section>
     <!-- Student Results Section -->
     <section class="mt-16 bg-white rounded-3xl shadow-2xl p-8 card-shadow">
      <h2 class="text-3xl font-extrabold mb-6 text-gray-900 tracking-wide">
       Student Results
      </h2>
      <div class="mb-6 flex space-x-4">
       <input class="flex-grow px-5 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" id="studentSearch" placeholder="Search by student name or email" type="text"/>
       <button class="bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold px-6 rounded-3xl shadow-lg shadow-indigo-400/50 transition" onclick="searchStudentResults()">
        Search
       </button>
      </div>
      <div class="overflow-x-auto rounded-2xl border border-gray-200 shadow-inner">
       <table class="min-w-full divide-y divide-gray-200">
        <thead class="bg-gray-50">
         <tr>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Student
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Quiz
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Score
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Date
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Attempt
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Actions
          </th>
         </tr>
        </thead>
        <tbody class="bg-white divide-y divide-gray-200" id="resultsTableBody">
         <!-- Results will be displayed here -->
        </tbody>
       </table>
      </div>
     </section>
    </main>
   </div>
   <!-- Student Dashboard -->
   <div class="hidden min-h-screen flex flex-col" id="studentDashboard">
    <!-- Header -->
    <header class="text-white shadow-md">
     <div class="container mx-auto px-6 py-5 flex justify-between items-center">
      <h1 class="text-3xl font-extrabold tracking-wide drop-shadow-lg">
       Student Dashboard
      </h1>
      <div class="flex items-center space-x-6">
       <div class="flex items-center space-x-3 bg-green-700 bg-opacity-80 rounded-full px-4 py-2 shadow-lg">
        <svg class="h-7 w-7 text-green-300" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
         <path d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
        </svg>
        <span id="studentNameDisplay" class="font-semibold text-lg select-none">
         Student
        </span>
       </div>
       <button class="bg-white text-green-700 px-4 py-2 rounded-full font-semibold shadow-md hover:bg-green-50 transition" onclick="logout()">
        Logout
       </button>
      </div>
     </div>
    </header>
    <main class="container mx-auto px-6 py-10 flex-grow">
     <!-- Available Quizzes -->
     <section>
      <h2 class="text-3xl font-extrabold mb-8 text-gray-900 tracking-wide">
       Available Quizzes
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8" id="studentQuizzesContainer">
       <!-- Quizzes will be displayed here -->
      </div>
     </section>
     <!-- Previous Attempts -->
     <section class="mt-16">
      <h2 class="text-3xl font-extrabold mb-6 text-gray-900 tracking-wide">
       Your Previous Attempts
      </h2>
      <div class="bg-white rounded-3xl shadow-2xl p-8 card-shadow overflow-x-auto">
       <table class="min-w-full divide-y divide-gray-200 rounded-3xl overflow-hidden">
        <thead class="bg-gray-50">
         <tr>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Quiz
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Score
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Date
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Attempt
          </th>
          <th class="px-8 py-4 text-left text-xs font-semibold text-gray-500 uppercase tracking-wider" scope="col">
           Action
          </th>
         </tr>
        </thead>
        <tbody class="bg-white divide-y divide-gray-200" id="studentAttemptsTableBody">
         <!-- Attempts will be displayed here -->
        </tbody>
       </table>
      </div>
     </section>
    </main>
   </div>
   <!-- Quiz Taking Interface -->
   <div class="hidden min-h-screen bg-gray-50 flex flex-col" id="quizTakingInterface">
    <div class="container mx-auto px-6 py-10 flex-grow flex flex-col">
     <div class="flex justify-between items-center mb-8">
      <h1 class="text-4xl font-extrabold text-gray-900 tracking-wide" id="quizTitleTaking">
      </h1>
      <div class="flex items-center bg-white px-5 py-3 rounded-3xl shadow-lg border border-red-300">
       <svg class="h-6 w-6 text-red-500 mr-2" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
       </svg>
       <span class="font-semibold text-gray-700 text-lg" id="quizTimer">
        30:00
       </span>
      </div>
     </div>
     <p class="text-gray-600 mb-10 text-lg max-w-3xl" id="quizDescriptionTaking">
     </p>
     <div class="space-y-8 overflow-y-auto flex-grow pr-4" id="quizQuestionsTaking" tabindex="0" aria-label="Quiz questions container">
      <!-- Questions will be displayed here -->
     </div>
     <div class="mt-10 flex justify-end">
      <button class="bg-green-600 hover:bg-green-700 text-white font-extrabold py-4 px-10 rounded-3xl shadow-lg shadow-green-400/50 transition" onclick="submitQuiz()">
       Submit Quiz
      </button>
     </div>
    </div>
   </div>
   <!-- Quiz Result Display -->
   <div class="hidden min-h-screen bg-gray-50 flex flex-col" id="quizResultDisplay">
    <div class="container mx-auto px-6 py-10 flex-grow flex flex-col items-center">
     <div class="max-w-4xl w-full bg-white rounded-3xl shadow-2xl overflow-hidden card-shadow">
      <div class="bg-gradient-to-r from-green-400 to-blue-500 p-10 text-center">
       <h1 class="text-5xl font-extrabold text-white mb-4 tracking-wide" id="resultQuizTitle">
       </h1>
       <div class="text-white text-xl mb-6 font-semibold tracking-wide">
        Your Result
       </div>
       <div class="w-40 h-40 mx-auto bg-white rounded-full flex items-center justify-center shadow-2xl">
        <span class="text-6xl font-extrabold text-gray-900" id="resultScore">
         80%
        </span>
       </div>
      </div>
      <div class="p-10">
       <div class="grid grid-cols-3 gap-8 text-center mb-12">
        <div class="bg-gray-50 p-6 rounded-3xl shadow-inner">
         <div class="text-sm text-gray-500 font-semibold tracking-wide">
          Correct Answers
         </div>
         <div class="text-4xl font-extrabold text-green-600 mt-2" id="correctCount">
          8
         </div>
        </div>
        <div class="bg-gray-50 p-6 rounded-3xl shadow-inner">
         <div class="text-sm text-gray-500 font-semibold tracking-wide">
          Wrong Answers
         </div>
         <div class="text-4xl font-extrabold text-red-600 mt-2" id="wrongCount">
          2
         </div>
        </div>
        <div class="bg-gray-50 p-6 rounded-3xl shadow-inner">
         <div class="text-sm text-gray-500 font-semibold tracking-wide">
          Time Taken
         </div>
         <div class="text-4xl font-extrabold text-indigo-600 mt-2" id="timeTaken">
          15:32
         </div>
        </div>
       </div>
       <h2 class="text-3xl font-extrabold mb-8 text-gray-900 tracking-wide">
        Question Review
       </h2>
       <div class="space-y-8" id="questionReview" aria-live="polite" aria-atomic="true">
        <!-- Questions with answers will be displayed here -->
       </div>
       <div class="mt-12 flex justify-between">
        <button class="bg-gray-200 hover:bg-gray-300 text-gray-900 font-extrabold py-3 px-8 rounded-3xl transition duration-300 shadow-md" onclick="backToStudentDashboard()">
         &larr; Back to Dashboard
        </button>
        <button class="bg-indigo-600 hover:bg-indigo-700 text-white font-extrabold py-3 px-8 rounded-3xl transition duration-300 shadow-lg flex items-center space-x-3" onclick="downloadResult()">
         <svg class="h-6 w-6" fill="none" stroke="currentColor" viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
          <path d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"></path>
         </svg>
         <span>Download Result</span>
        </button>
       </div>
      </div>
     </div>
    </div>
   </div>
  </div>
  <script>
   // Data storage with localStorage persistence
    let users = {
        teachers: [],
        students: []
    };

    let quizzes = [];
    let results = [];

    // Load data from localStorage if available
    function loadData() {
        const usersData = localStorage.getItem('qms_users');
        if (usersData) {
            try {
                users = JSON.parse(usersData);
            } catch {}
        }
        const quizzesData = localStorage.getItem('qms_quizzes');
        if (quizzesData) {
            try {
                quizzes = JSON.parse(quizzesData);
            } catch {}
        }
        const resultsData = localStorage.getItem('qms_results');
        if (resultsData) {
            try {
                results = JSON.parse(resultsData);
            } catch {}
        }
    }

    // Save data to localStorage
    function saveData() {
        localStorage.setItem('qms_users', JSON.stringify(users));
        localStorage.setItem('qms_quizzes', JSON.stringify(quizzes));
        localStorage.setItem('qms_results', JSON.stringify(results));
    }

    // Initialize with sample data if empty
    function initializeSampleData() {
        if(users.teachers.length === 0) {
            users.teachers.push({ email: 'teacher@example.com', password: 'password123', name: 'Mr. Smith' });
        }
        if(users.students.length === 0) {
            users.students.push({ email: 'student@example.com', password: 'password123', name: 'John Doe', rollNumber: 'S001' });
        }
        if(quizzes.length === 0) {
            quizzes.push({
                id: '1',
                title: 'Sample Quiz',
                description: 'This is a sample quiz for demonstration purposes.',
                timeLimit: 30,
                maxAttempts: 1,
                teacherEmail: 'teacher@example.com',
                questions: [
                    {
                        id: '1',
                        text: 'What is the capital of France?',
                        type: 'single',
                        options: ['Paris', 'London', 'Berlin', 'Madrid'],
                        correctAnswers: [0]
                    },
                    {
                        id: '2',
                        text: 'Which of these are programming languages? (Select all that apply)',
                        type: 'multiple',
                        options: ['JavaScript', 'Python', 'HTML', 'CSS'],
                        correctAnswers: [0, 1]
                    }
                ]
            });
        }
        if(results.length === 0) {
            results.push({
                id: '1',
                quizId: '1',
                studentEmail: 'student@example.com',
                studentName: 'John Doe',
                quizTitle: 'Sample Quiz',
                score: 80,
                correctAnswers: 8,
                totalQuestions: 10,
                answers: [
                    { questionId: '1', selectedOptions: [0], correct: true },
                    { questionId: '2', selectedOptions: [0, 1], correct: false }
                ],
                date: new Date().toISOString(),
                attemptNumber: 1,
                timeTaken: '15:32'
            });
        }
        saveData();
    }

    // Current user and state
    let currentUser = null;
    let currentQuiz = null;
    let currentQuizTaking = null;
    let currentQuestionAnswers = [];
    let timerInterval = null;
    let timeLeft = 0;

    // Helper functions
    function generateId() {
        return Math.random().toString(36).substring(2, 15) + Math.random().toString(36).substring(2, 15);
    }

    function formatDate(dateString) {
        const options = { year: 'numeric', month: 'short', day: 'numeric', hour: '2-digit', minute: '2-digit' };
        return new Date(dateString).toLocaleDateString(undefined, options);
    }

    // Hide all main sections
    function hideAllSections() {
        const sections = [
            'loginSelectionScreen',
            'teacherLoginForm',
            'teacherRegisterForm',
            'studentLoginForm',
            'studentRegisterForm',
            'teacherDashboard',
            'studentDashboard',
            'quizTakingInterface',
            'quizResultDisplay',
            'quizQuestionsSection'
        ];
        sections.forEach(id => {
            const el = document.getElementById(id);
            if(el) el.classList.add('hidden');
        });
    }

    // Authentication functions
    function showLoginForm(role) {
        hideAllSections();
        document.getElementById(role + 'LoginForm').classList.remove('hidden');
    }

    function showRegisterForm(role) {
        hideAllSections();
        document.getElementById(role + 'RegisterForm').classList.remove('hidden');
    }

    function loginTeacher(event) {
        event.preventDefault();
        const email = document.getElementById('teacherEmail').value.trim();
        const password = document.getElementById('teacherPassword').value;
        
        const teacher = users.teachers.find(u => u.email === email && u.password === password);
        if (teacher) {
            currentUser = { ...teacher, role: 'teacher' };
            document.getElementById('teacherNameDisplay').textContent = teacher.name;
            hideAllSections();
            document.getElementById('teacherDashboard').classList.remove('hidden');
            renderTeacherDashboard();
        } else {
            alert('Invalid email or password');
        }
    }

    function loginStudent(event) {
        event.preventDefault();
        const email = document.getElementById('studentEmail').value.trim();
        const password = document.getElementById('studentPassword').value;
        
        const student = users.students.find(u => u.email === email && u.password === password);
        if (student) {
            currentUser = { ...student, role: 'student' };
            document.getElementById('studentNameDisplay').textContent = student.name;
            hideAllSections();
            document.getElementById('studentDashboard').classList.remove('hidden');
            renderStudentDashboard();
        } else {
            alert('Invalid email or password');
        }
    }

    function registerTeacher(event) {
        event.preventDefault();
        const name = document.getElementById('teacherRegName').value.trim();
        const email = document.getElementById('teacherRegEmail').value.trim();
        const password = document.getElementById('teacherRegPassword').value;
        const confirmPassword = document.getElementById('teacherRegConfirmPassword').value;
        
        if (password !== confirmPassword) {
            alert('Passwords do not match');
            return;
        }
        
        if (users.teachers.some(u => u.email === email)) {
            alert('Teacher with this email already exists');
            return;
        }
        
        users.teachers.push({ email, password, name });
        saveData();
        alert('Registration successful! You are now logged in.');
        currentUser = { email, password, name, role: 'teacher' };
        document.getElementById('teacherNameDisplay').textContent = name;
        hideAllSections();
        document.getElementById('teacherDashboard').classList.remove('hidden');
        renderTeacherDashboard();
    }

    function registerStudent(event) {
        event.preventDefault();
        const name = document.getElementById('studentRegName').value.trim();
        const email = document.getElementById('studentRegEmail').value.trim();
        const rollNumber = document.getElementById('studentRegRoll').value.trim();
        const password = document.getElementById('studentRegPassword').value;
        const confirmPassword = document.getElementById('studentRegConfirmPassword').value;
        
        if (password !== confirmPassword) {
            alert('Passwords do not match');
            return;
        }
        
        if (users.students.some(u => u.email === email)) {
            alert('Student with this email already exists');
            return;
        }
        
        users.students.push({ email, password, name, rollNumber });
        saveData();
        alert('Registration successful! You are now logged in.');
        currentUser = { email, password, name, rollNumber, role: 'student' };
        document.getElementById('studentNameDisplay').textContent = name;
        hideAllSections();
        document.getElementById('studentDashboard').classList.remove('hidden');
        renderStudentDashboard();
    }

    function logout() {
        currentUser = null;
        clearInterval(timerInterval);
        hideAllSections();
        document.getElementById('loginSelectionScreen').classList.remove('hidden');
    }

    // Teacher dashboard functions
    function renderTeacherDashboard() {
        saveData();
        // Render quizzes
        const quizzesContainer = document.getElementById('quizzesContainer');
        quizzesContainer.innerHTML = '';
        
        const filteredQuizzes = quizzes.filter(q => q.teacherEmail === currentUser.email);
        
        if (filteredQuizzes.length === 0) {
            quizzesContainer.innerHTML = `
                <div class="col-span-full text-center py-16">
                    <img src="https://placehold.co/400x300/png?text=Empty+Classroom+Illustration" alt="Illustration of an empty classroom with a chalkboard and empty desks, representing no quizzes available yet" class="mx-auto mb-6 rounded-2xl shadow-lg" />
                    <h3 class="text-2xl font-semibold text-gray-900">No quizzes created yet</h3>
                    <p class="mt-3 text-lg text-gray-500">Create your first quiz to get started</p>
                </div>
            `;
        } else {
            filteredQuizzes.forEach(quiz => {
                const quizCard = document.createElement('div');
                quizCard.className = 'bg-white rounded-3xl shadow-lg overflow-hidden hover:shadow-2xl transition duration-300 cursor-pointer card-shadow';
                quizCard.innerHTML = `
                    <div class="p-6">
                        <div class="flex justify-between items-start">
                            <h3 class="text-xl font-extrabold text-gray-900">${quiz.title}</h3>
                            <span class="inline-flex items-center px-3 py-1 rounded-full text-sm font-semibold bg-indigo-100 text-indigo-800 select-none">
                                ${quiz.questions.length} ${quiz.questions.length === 1 ? 'question' : 'questions'}
                            </span>
                        </div>
                        <p class="mt-3 text-gray-600 text-base">${quiz.description || 'No description provided'}</p>
                        <div class="mt-5 flex justify-between items-center text-sm text-gray-500 font-semibold tracking-wide select-none">
                            <span>⏱️ ${quiz.timeLimit} min</span>
                            <span>🔁 Max attempts: ${quiz.maxAttempts}</span>
                        </div>
                    </div>
                    <div class="bg-gray-50 px-6 py-4 flex justify-between border-t border-gray-200">
                        <button onclick="viewQuiz('${quiz.id}')" class="text-indigo-600 hover:text-indigo-900 font-semibold tracking-wide focus:outline-none focus:ring-2 focus:ring-indigo-400 rounded">
                            Edit Questions
                        </button>
                        <button onclick="viewQuizResults('${quiz.id}')" class="text-gray-600 hover:text-gray-900 font-semibold tracking-wide focus:outline-none focus:ring-2 focus:ring-gray-400 rounded">
                            View Results
                        </button>
                    </div>
                `;
                quizzesContainer.appendChild(quizCard);
            });
        }
        
        // Render results
        renderResultsTable();
    }

    function viewQuiz(quizId) {
        currentQuiz = quizzes.find(q => q.id === quizId);
        document.getElementById('currentQuizTitle').textContent = currentQuiz.title;
        document.getElementById('quizQuestionsSection').classList.remove('hidden');
        renderQuizQuestions();
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function backToQuizzes() {
        currentQuiz = null;
        document.getElementById('quizQuestionsSection').classList.add('hidden');
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function renderQuizQuestions() {
        const questionsList = document.getElementById('questionsList');
        questionsList.innerHTML = '';
        
        if (currentQuiz.questions.length === 0) {
            questionsList.innerHTML = `
                <div class="text-center py-16">
                    <img src="https://placehold.co/400x300/png?text=Empty+Questionnaire+Illustration" alt="Illustration of an empty questionnaire with a pencil, representing no questions added yet" class="mx-auto mb-6 rounded-2xl shadow-lg" />
                    <h3 class="text-2xl font-semibold text-gray-900">No questions added yet</h3>
                    <p class="mt-3 text-lg text-gray-500">Add your first question to this quiz</p>
                </div>
            `;
        } else {
            currentQuiz.questions.forEach((question, index) => {
                const questionElement = document.createElement('div');
                questionElement.className = 'bg-gray-50 p-6 rounded-3xl border border-gray-200 question-card transition duration-300';
                questionElement.innerHTML = `
                    <div class="flex justify-between items-start">
                        <div>
                            <h4 class="font-semibold text-gray-900 text-lg">Q${index + 1}: ${question.text}</h4>
                            <p class="text-sm text-gray-500 mt-1 select-none">
                                ${question.type === 'single' ? 'Single correct answer' : 'Multiple correct answers'}
                            </p>
                        </div>
                        <button onclick="deleteQuestion('${question.id}')" class="text-red-600 hover:text-red-800 transition rounded focus:outline-none focus:ring-2 focus:ring-red-400" title="Delete Question" aria-label="Delete Question">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                            </svg>
                        </button>
                    </div>
                    <div class="mt-5 space-y-3">
                        ${question.options.map((option, i) => `
                            <div class="flex items-center space-x-3 select-none">
                                <input 
                                    type="${question.type === 'single' ? 'radio' : 'checkbox'}" 
                                    ${question.correctAnswers.includes(i) ? 'checked' : ''} 
                                    disabled
                                    class="text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded cursor-default">
                                <span class="text-gray-800 text-base">${option}</span>
                            </div>
                        `).join('')}
                    </div>
                `;
                questionsList.appendChild(questionElement);
            });
        }
    }

    function createQuiz(event) {
        event.preventDefault();
        const title = document.getElementById('quizTitle').value.trim();
        const description = document.getElementById('quizDescription').value.trim();
        const timeLimit = parseInt(document.getElementById('quizTimeLimit').value);
        const maxAttempts = parseInt(document.getElementById('quizMaxAttempts').value);
        
        if (!title) {
            alert('Quiz title is required');
            return;
        }
        if (timeLimit < 1 || timeLimit > 120) {
            alert('Time limit must be between 1 and 120 minutes');
            return;
        }
        if (maxAttempts < 1 || maxAttempts > 10) {
            alert('Max attempts must be between 1 and 10');
            return;
        }
        
        const newQuiz = {
            id: generateId(),
            title,
            description,
            timeLimit,
            maxAttempts,
            teacherEmail: currentUser.email,
            questions: []
        };
        
        quizzes.push(newQuiz);
        saveData();
        document.getElementById('createQuizForm').reset();
        renderTeacherDashboard();
        
        alert('Quiz created successfully! Now you can add questions to it.');
    }

    function addOption() {
        const optionsContainer = document.querySelector('#optionsContainer .space-y-3');
        const newOption = document.createElement('div');
        newOption.className = 'flex items-center space-x-3';
        const optionCount = optionsContainer.children.length;
        const questionType = document.querySelector('input[name="questionType"]:checked').value;
        const inputType = questionType === 'single' ? 'radio' : 'checkbox';
        const inputName = questionType === 'single' ? 'correctOption' : `correctOptionMultiple_${Date.now()}`;
        
        newOption.innerHTML = `
            <input type="${inputType}" name="${inputName}" value="${optionCount}" class="text-indigo-600 focus:ring-indigo-500" />
            <input type="text" required class="flex-grow px-4 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" placeholder="Option text" />
            <button type="button" onclick="removeOption(this)" class="text-red-500 hover:text-red-700 transition rounded focus:outline-none focus:ring-2 focus:ring-red-400" title="Remove Option" aria-label="Remove Option">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                </svg>
            </button>
        `;
        
        optionsContainer.appendChild(newOption);
        updateOptionsInputType();
    }

    function removeOption(button) {
        const optionDiv = button.closest('div');
        if (document.querySelectorAll('#optionsContainer .space-y-3 > div').length > 2) {
            optionDiv.remove();
            updateOptionsInputType();
        } else {
            alert('A question must have at least 2 options');
        }
    }

    function updateOptionsInputType() {
        const questionType = document.querySelector('input[name="questionType"]:checked').value;
        const optionsContainer = document.querySelector('#optionsContainer .space-y-3');
        const optionDivs = optionsContainer.querySelectorAll('div');
        optionDivs.forEach((div, index) => {
            const input = div.querySelector('input[type="radio"], input[type="checkbox"]');
            if (questionType === 'single') {
                input.type = 'radio';
                input.name = 'correctOption';
                input.value = index;
                if (index === 0) input.checked = true;
            } else {
                input.type = 'checkbox';
                input.name = 'correctOptionMultiple';
                input.value = index;
                input.checked = false;
            }
        });
    }

    function addQuestion(event) {
        event.preventDefault();
        const questionText = document.getElementById('questionText').value.trim();
        const questionType = document.querySelector('input[name="questionType"]:checked').value;
        
        const optionInputs = document.querySelectorAll('#optionsContainer input[type="text"]');
        const options = Array.from(optionInputs).map(input => input.value.trim());
        
        if (options.some(opt => !opt)) {
            alert('All option texts must be filled');
            return;
        }
        
        let correctOptions = [];
        if (questionType === 'single') {
            const selectedRadio = document.querySelector('#optionsContainer input[type="radio"]:checked');
            if (!selectedRadio) {
                alert('Please select exactly one correct answer for single-answer questions');
                return;
            }
            correctOptions = [parseInt(selectedRadio.value)];
        } else {
            const selectedCheckboxes = Array.from(document.querySelectorAll('#optionsContainer input[type="checkbox"]:checked'));
            if (selectedCheckboxes.length === 0) {
                alert('Please select at least one correct answer for multiple-answer questions');
                return;
            }
            correctOptions = selectedCheckboxes.map(cb => parseInt(cb.value));
        }
        
        if (correctOptions.length === 0) {
            alert('Please select at least one correct answer');
            return;
        }
        
        const newQuestion = {
            id: generateId(),
            text: questionText,
            type: questionType,
            options: options,
            correctAnswers: correctOptions
        };
        
        currentQuiz.questions.push(newQuestion);
        saveData();
        document.getElementById('addQuestionForm').reset();
        
        // Reset to 2 default options with radio buttons
        const optionsContainer = document.querySelector('#optionsContainer .space-y-3');
        optionsContainer.innerHTML = `
            <div class="flex items-center space-x-3">
                <input type="radio" name="correctOption" value="0" checked class="text-indigo-600 focus:ring-indigo-500" />
                <input type="text" required class="flex-grow px-4 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" placeholder="Option text" />
                <button type="button" onclick="removeOption(this)" class="text-red-500 hover:text-red-700 transition rounded focus:outline-none focus:ring-2 focus:ring-red-400" title="Remove Option" aria-label="Remove Option">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                    </svg>
                </button>
            </div>
            <div class="flex items-center space-x-3">
                <input type="radio" name="correctOption" value="1" class="text-indigo-600 focus:ring-indigo-500" />
                <input type="text" required class="flex-grow px-4 py-3 border border-gray-300 rounded-2xl focus:ring-indigo-500 focus:border-indigo-500 shadow-sm" placeholder="Option text" />
                <button type="button" onclick="removeOption(this)" class="text-red-500 hover:text-red-700 transition rounded focus:outline-none focus:ring-2 focus:ring-red-400" title="Remove Option" aria-label="Remove Option">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                    </svg>
                </button>
            </div>
        `;
        updateOptionsInputType();
        renderQuizQuestions();
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function deleteQuestion(questionId) {
        if (confirm('Are you sure you want to delete this question?')) {
            currentQuiz.questions = currentQuiz.questions.filter(q => q.id !== questionId);
            saveData();
            renderQuizQuestions();
        }
    }

    function searchStudentResults() {
        const searchTerm = document.getElementById('studentSearch').value.toLowerCase();
        renderResultsTable(searchTerm);
    }

    function renderResultsTable(searchTerm = '') {
        const tbody = document.getElementById('resultsTableBody');
        tbody.innerHTML = '';
        
        const teacherResults = results.filter(result => {
            const quiz = quizzes.find(q => q.id === result.quizId);
            return quiz && quiz.teacherEmail === currentUser.email &&
                (result.studentName.toLowerCase().includes(searchTerm) || 
                 result.studentEmail.toLowerCase().includes(searchTerm));
        });
        
        if (teacherResults.length === 0) {
            tbody.innerHTML = `
                <tr>
                    <td colspan="6" class="px-8 py-6 text-center text-lg text-gray-500 select-none">
                        <img src="https://placehold.co/200x150/png?text=No+Results" alt="Illustration of a clipboard with no data, representing no results available yet" class="mx-auto mb-4 rounded-2xl shadow-md" />
                        No results available yet
                    </td>
                </tr>
            `;
        } else {
            teacherResults.forEach(result => {
                const quiz = quizzes.find(q => q.id === result.quizId);
                const row = document.createElement('tr');
                row.className = 'hover:bg-indigo-50 transition cursor-pointer';
                row.innerHTML = `
                    <td class="px-8 py-5 whitespace-nowrap text-sm font-semibold text-gray-900">
                        ${result.studentName}
                        <p class="text-gray-500 text-xs mt-1 select-text">${result.studentEmail}</p>
                    </td>
                    <td class="px-8 py-5 whitespace-nowrap text-sm text-gray-600 select-text">
                        ${quiz ? quiz.title : 'Unknown Quiz'}
                    </td>
                    <td class="px-8 py-5 whitespace-nowrap text-sm">
                        <span class="px-3 py-1 rounded-full text-xs font-semibold 
                            ${result.score >= 80 ? 'bg-green-100 text-green-800' : 
                            result.score >= 50 ? 'bg-yellow-100 text-yellow-800' : 'bg-red-100 text-red-800'}">
                            ${result.score}%
                        </span>
                    </td>
                    <td class="px-8 py-5 whitespace-nowrap text-sm text-gray-600 select-text">
                        ${formatDate(result.date)}
                    </td>
                    <td class="px-8 py-5 whitespace-nowrap text-sm text-gray-600 select-text">
                        ${result.attemptNumber}
                    </td>
                    <td class="px-8 py-5 whitespace-nowrap text-right text-sm font-semibold">
                        <button onclick="viewStudentResult('${result.id}')" class="text-indigo-600 hover:text-indigo-900 focus:outline-none focus:ring-2 focus:ring-indigo-400 rounded">
                            View Details
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }
    }

    function viewQuizResults(quizId) {
        alert('Viewing results for quiz ID: ' + quizId);
    }

    function viewStudentResult(resultId) {
        const result = results.find(r => r.id === resultId);
        if (result) {
            document.getElementById('resultQuizTitle').textContent = result.quizTitle;
            document.getElementById('resultScore').textContent = result.score + '%';
            document.getElementById('correctCount').textContent = result.correctAnswers;
            document.getElementById('wrongCount').textContent = result.totalQuestions - result.correctAnswers;
            document.getElementById('timeTaken').textContent = result.timeTaken;
            
            const quiz = quizzes.find(q => q.id === result.quizId);
            const questionReview = document.getElementById('questionReview');
            questionReview.innerHTML = '';
            
            if (quiz) {
                quiz.questions.forEach((q, index) => {
                    const answer = result.answers.find(a => a.questionId === q.id);
                    const isCorrect = answer ? answer.correct : false;
                    
                    const questionElement = document.createElement('div');
                    questionElement.className = `p-6 rounded-3xl ${isCorrect ? 'bg-green-50 border-green-400 border-l-8' : 'bg-red-50 border-red-400 border-l-8'}`;
                    questionElement.innerHTML = `
                        <h4 class="text-xl font-semibold ${isCorrect ? 'text-green-800' : 'text-red-800'} mb-3">Q${index+1}: ${q.text}</h4>
                        <div class="space-y-3">
                            ${q.options.map((opt, i) => `
                                <div class="flex items-center space-x-3 select-none">
                                    <input type="${q.type === 'single' ? 'radio' : 'checkbox'}" ${answer && answer.selectedOptions.includes(i) ? 'checked' : ''} disabled class="border-gray-300 rounded cursor-default" />
                                    <span class="${answer && answer.selectedOptions.includes(i) ? 
                                        (q.correctAnswers.includes(i) ? 'text-green-600 font-semibold' : 'text-red-600 font-semibold') : 
                                        (q.correctAnswers.includes(i) ? 'font-semibold' : 'text-gray-700')} text-lg">
                                        ${opt}
                                    </span>
                                </div>
                            `).join('')}
                        </div>
                        ${!isCorrect ? `<div class="mt-4 text-sm text-gray-600 font-semibold">Correct answer: ${q.correctAnswers.map(i => q.options[i]).join(', ')}</div>` : ''}
                    `;
                    questionReview.appendChild(questionElement);
                });
            }
            
            hideAllSections();
            document.getElementById('quizResultDisplay').classList.remove('hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
    }

    // Student dashboard functions
    function renderStudentDashboard() {
        saveData();
        // Render available quizzes
        const quizzesContainer = document.getElementById('studentQuizzesContainer');
        quizzesContainer.innerHTML = '';
        
        if (quizzes.length === 0) {
            quizzesContainer.innerHTML = `
                <div class="col-span-full text-center py-16">
                    <img src="https://placehold.co/400x300/png?text=Empty+Classroom" alt="Illustration of an empty classroom with chairs and desks, representing no quizzes available yet" class="mx-auto mb-6 rounded-2xl shadow-lg" />
                    <h3 class="text-2xl font-semibold text-gray-900">No quizzes available yet</h3>
                    <p class="mt-3 text-lg text-gray-500">Check back later or contact your teacher</p>
                </div>
            `;
        } else {
            quizzes.forEach(quiz => {
                const quizCard = document.createElement('div');
                quizCard.className = 'bg-white rounded-3xl shadow-lg overflow-hidden hover:shadow-2xl transition duration-300 cursor-pointer card-shadow';
                
                // Check if student has attempts for this quiz
                const studentResultsForQuiz = results.filter(r => 
                    r.quizId === quiz.id && r.studentEmail === currentUser.email
                );
                const attemptsLeft = quiz.maxAttempts - studentResultsForQuiz.length;
                const canTakeQuiz = attemptsLeft > 0;
                
                const bestAttempt = studentResultsForQuiz.reduce((max, result) => 
                    result.score > max.score ? result : max
                , { score: 0 });
                
                quizCard.innerHTML = `
                    <div class="p-6">
                        <div class="flex justify-between items-start">
                            <h3 class="text-xl font-extrabold text-gray-900">${quiz.title}</h3>
                            ${studentResultsForQuiz.length > 0 ? `
                                <span class="inline-flex items-center px-3 py-1 rounded-full text-sm font-semibold 
                                    ${bestAttempt.score >= 80 ? 'bg-green-100 text-green-800' : 
                                      bestAttempt.score >= 50 ? 'bg-yellow-100 text-yellow-800' : 'bg-red-100 text-red-800'} select-none">
                                    Best: ${bestAttempt.score}%
                                </span>
                            ` : ''}
                        </div>
                        <p class="mt-3 text-gray-600 text-base">${quiz.description || 'No description provided'}</p>
                        <div class="mt-5 flex justify-between items-center text-sm text-gray-500 font-semibold tracking-wide select-none">
                            <span>⏱️ ${quiz.timeLimit} min</span>
                            ${canTakeQuiz ? `
                                <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold bg-blue-100 text-blue-800">
                                    Attempts left: ${attemptsLeft} of ${quiz.maxAttempts}
                                </span>
                            ` : `
                                <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold bg-gray-200 text-gray-700">
                                    No attempts left
                                </span>
                            `}
                        </div>
                    </div>
                    <div class="bg-gray-50 px-6 py-4 border-t border-gray-200">
                        ${canTakeQuiz ? `
                            <button onclick="startQuiz('${quiz.id}')" class="w-full bg-green-600 hover:bg-green-700 text-white font-extrabold py-3 rounded-3xl shadow-lg shadow-green-400/50 transition">
                                Take Quiz
                            </button>
                        ` : `
                            <button onclick="viewAttempts('${quiz.id}')" class="w-full text-gray-600 hover:text-gray-900 font-semibold py-3 rounded-3xl transition">
                                View Attempts
                            </button>
                        `}
                    </div>
                `;
                quizzesContainer.appendChild(quizCard);
            });
        }
        
        // Render student's previous attempts
        renderStudentAttempts();
    }

    function renderStudentAttempts() {
        const tbody = document.getElementById('studentAttemptsTableBody');
        tbody.innerHTML = '';
        
        const studentAttempts = results.filter(result => 
            result.studentEmail === currentUser.email
        );
        
        if (studentAttempts.length === 0) {
            tbody.innerHTML = `
                <tr>
                    <td colspan="5" class="px-8 py-6 text-center text-lg text-gray-500 select-none">
                        <img src="https://placehold.co/200x150/png?text=No+Attempts" alt="Illustration of an empty clipboard with a pencil, representing no quiz attempts yet" class="mx-auto mb-4 rounded-2xl shadow-md" />
                        No quiz attempts yet
                    </td>
                </tr>
            `;
        } else {
            studentAttempts.forEach(attempt => {
                const quiz = quizzes.find(q => q.id === attempt.quizId);
                const row = document.createElement('tr');
                row.className = 'hover:bg-green-50 transition cursor-pointer';
                row.innerHTML = `
                    <td class="px-8 py-5 whitespace-nowrap text-sm font-semibold text-gray-900 select-text">${quiz ? quiz.title : 'Unknown Quiz'}</td>
                    <td class="px-8 py-5 whitespace-nowrap text-sm text-gray-600 select-text">${attempt.score}%</td>
                    <td class="px-8 py-5 whitespace-nowrap text-sm text-gray-600 select-text">${formatDate(attempt.date)}</td>
                    <td class="px-8 py-5 whitespace-nowrap text-sm text-gray-600 select-text">${attempt.attemptNumber}</td>
                    <td class="px-8 py-5 whitespace-nowrap text-right text-sm font-semibold">
                        <button onclick="viewStudentResult('${attempt.id}')" class="text-green-600 hover:text-green-900 focus:outline-none focus:ring-2 focus:ring-green-400 rounded">
                            View Result
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }
    }

    // Quiz taking functions
    function startQuiz(quizId) {
        currentQuizTaking = quizzes.find(q => q.id === quizId);
        if (!currentQuizTaking) {
            alert('Quiz not found');
            return;
        }
        currentQuestionAnswers = [];
        timeLeft = currentQuizTaking.timeLimit * 60;
        hideAllSections();
        document.getElementById('quizTakingInterface').classList.remove('hidden');
        document.getElementById('quizTitleTaking').textContent = currentQuizTaking.title;
        document.getElementById('quizDescriptionTaking').textContent = currentQuizTaking.description || '';
        renderQuizQuestionsTaking();
        startTimer();
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function renderQuizQuestionsTaking() {
        const container = document.getElementById('quizQuestionsTaking');
        container.innerHTML = '';
        currentQuizTaking.questions.forEach((q, index) => {
            const questionDiv = document.createElement('div');
            questionDiv.className = 'bg-white p-6 rounded-3xl shadow-lg card-shadow';
            questionDiv.innerHTML = `
                <h3 class="font-extrabold text-gray-900 text-xl mb-4 select-text">Q${index + 1}: ${q.text}</h3>
                <div class="space-y-4">
                    ${q.options.map((opt, i) => `
                        <label class="flex items-center space-x-4 cursor-pointer select-none">
                            <input type="${q.type === 'single' ? 'radio' : 'checkbox'}" name="question_${q.id}" value="${i}" class="form-input text-green-600 focus:ring-green-400" />
                            <span class="text-gray-800 text-lg">${opt}</span>
                        </label>
                    `).join('')}
                </div>
            `;
            container.appendChild(questionDiv);
        });
    }

    function startTimer() {
        updateTimerDisplay();
        clearInterval(timerInterval);
        timerInterval = setInterval(() => {
            timeLeft--;
            if (timeLeft <= 0) {
                clearInterval(timerInterval);
                alert('Time is up! Submitting quiz...');
                submitQuiz();
            } else {
                updateTimerDisplay();
            }
        }, 1000);
    }

    function updateTimerDisplay() {
        const minutes = Math.floor(timeLeft / 60);
        const seconds = timeLeft % 60;
        document.getElementById('quizTimer').textContent = `${minutes.toString().padStart(2,'0')}:${seconds.toString().padStart(2,'0')}`;
    }

    function submitQuiz() {
        clearInterval(timerInterval);
        // Collect answers
        const answers = [];
        let correctCount = 0;
        currentQuizTaking.questions.forEach(q => {
            const selectedInputs = Array.from(document.querySelectorAll(`#quizQuestionsTaking input[name="question_${q.id}"]:checked`));
            const selectedOptions = selectedInputs.map(input => parseInt(input.value));
            // Check correctness
            let correct = false;
            if (q.type === 'single') {
                correct = selectedOptions.length === 1 && q.correctAnswers.includes(selectedOptions[0]);
            } else {
                // For multiple, check if arrays equal (ignoring order)
                correct = selectedOptions.length === q.correctAnswers.length && selectedOptions.every(val => q.correctAnswers.includes(val));
            }
            if (correct) correctCount++;
            answers.push({ questionId: q.id, selectedOptions, correct });
        });
        const totalQuestions = currentQuizTaking.questions.length;
        const score = Math.round((correctCount / totalQuestions) * 100);
        const attemptNumber = (results.filter(r => r.quizId === currentQuizTaking.id && r.studentEmail === currentUser.email).length) + 1;
        const timeTakenSeconds = currentQuizTaking.timeLimit * 60 - timeLeft;
        const timeTaken = `${Math.floor(timeTakenSeconds / 60)}:${(timeTakenSeconds % 60).toString().padStart(2,'0')}`;

        // Save result
        const newResult = {
            id: generateId(),
            quizId: currentQuizTaking.id,
            studentEmail: currentUser.email,
            studentName: currentUser.name,
            quizTitle: currentQuizTaking.title,
            score,
            correctAnswers: correctCount,
            totalQuestions,
            answers,
            date: new Date().toISOString(),
            attemptNumber,
            timeTaken
        };
        results.push(newResult);
        saveData();

        // Show result
        showQuizResult(newResult);
    }

    function showQuizResult(result) {
        document.getElementById('resultQuizTitle').textContent = result.quizTitle;
        document.getElementById('resultScore').textContent = result.score + '%';
        document.getElementById('correctCount').textContent = result.correctAnswers;
        document.getElementById('wrongCount').textContent = result.totalQuestions - result.correctAnswers;
        document.getElementById('timeTaken').textContent = result.timeTaken;

        const quiz = quizzes.find(q => q.id === result.quizId);
        const questionReview = document.getElementById('questionReview');
        questionReview.innerHTML = '';

        if (quiz) {
            quiz.questions.forEach((q, index) => {
                const answer = result.answers.find(a => a.questionId === q.id);
                const isCorrect = answer ? answer.correct : false;

                const questionElement = document.createElement('div');
                questionElement.className = `p-6 rounded-3xl ${isCorrect ? 'bg-green-50 border-green-400 border-l-8' : 'bg-red-50 border-red-400 border-l-8'}`;
                questionElement.innerHTML = `
                    <h4 class="text-xl font-semibold ${isCorrect ? 'text-green-800' : 'text-red-800'} mb-4 select-text">Q${index+1}: ${q.text}</h4>
                    <div class="space-y-4">
                        ${q.options.map((opt, i) => `
                            <div class="flex items-center space-x-4 select-none">
                                <input type="${q.type === 'single' ? 'radio' : 'checkbox'}" ${answer && answer.selectedOptions.includes(i) ? 'checked' : ''} disabled class="border-gray-300 rounded cursor-default" />
                                <span class="${answer && answer.selectedOptions.includes(i) ? 
                                    (q.correctAnswers.includes(i) ? 'text-green-600 font-semibold' : 'text-red-600 font-semibold') : 
                                    (q.correctAnswers.includes(i) ? 'font-semibold' : 'text-gray-700')} text-lg">
                                    ${opt}
                                </span>
                            </div>
                        `).join('')}
                    </div>
                    ${!isCorrect ? `<div class="mt-5 text-sm text-gray-600 font-semibold select-text">Correct answer: ${q.correctAnswers.map(i => q.options[i]).join(', ')}</div>` : ''}
                `;
                questionReview.appendChild(questionElement);
            });
        }

        hideAllSections();
        document.getElementById('quizResultDisplay').classList.remove('hidden');
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function backToStudentDashboard() {
        hideAllSections();
        document.getElementById('studentDashboard').classList.remove('hidden');
        renderStudentDashboard();
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function downloadResult() {
        const quizTitle = document.getElementById('resultQuizTitle').textContent;
        const score = document.getElementById('resultScore').textContent;
        const correct = document.getElementById('correctCount').textContent;
        const wrong = document.getElementById('wrongCount').textContent;
        const time = document.getElementById('timeTaken').textContent;
        const questionReview = document.getElementById('questionReview').innerText;

        const content = `
Quiz Title: ${quizTitle}
Score: ${score}
Correct Answers: ${correct}
Wrong Answers: ${wrong}
Time Taken: ${time}

Question Review:
${questionReview}
        `;

        const blob = new Blob([content], { type: 'text/plain' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = `${quizTitle.replace(/\s+/g, '_')}_Result.txt`;
        a.click();
        URL.revokeObjectURL(url);
    }

    // View attempts for student (just show alert for now)
    function viewAttempts(quizId) {
        alert('Viewing attempts is not implemented yet.');
    }

    // Initialize
    loadData();
    initializeSampleData();
    hideAllSections();
    document.getElementById('loginSelectionScreen').classList.remove('hidden');
  </script>
 </body>
</html>
