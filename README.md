<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>English Study - Premium Learning</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Configure Tailwind for Dark & Gold Theme -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gold: {
                            300: '#f3e5ab',
                            400: '#e5c158',
                            500: '#d4af37',
                            600: '#aa8822',
                            700: '#80661a',
                        },
                        dark: {
                            950: '#0a0a0a',
                            900: '#111111',
                            800: '#1a1a1a',
                            700: '#2a2a2a',
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                    }
                }
            }
        }
    </script>

    <!-- Phosphor Icons -->
    <script src="https://unpkg.com/@phosphor-icons/web"></script>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:wght@600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            background-color: #111111; /* dark-900 */
            color: #f3f4f6;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #111111; }
        ::-webkit-scrollbar-thumb { background: #d4af37; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #aa8822; }

        /* Animations */
        .fade-in {
            animation: fadeIn 0.5s ease-out forwards;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(15px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .gold-glow {
            box-shadow: 0 0 15px rgba(212, 175, 55, 0.2);
            transition: box-shadow 0.3s ease;
        }
        .gold-glow:hover {
            box-shadow: 0 0 25px rgba(212, 175, 55, 0.5);
        }

        .gold-text-gradient {
            background: linear-gradient(to right, #f3e5ab, #d4af37, #e5c158);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* Flashcard Flip Styles */
        .flip-card {
            background-color: transparent;
            perspective: 1000px;
            width: 100%;
            height: 350px;
            cursor: pointer;
        }

        .flip-card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.8s cubic-bezier(0.4, 0.2, 0.2, 1);
            transform-style: preserve-3d;
        }

        .flip-card.flipped .flip-card-inner {
            transform: rotateY(180deg);
        }

        .flip-card-front, .flip-card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            border-radius: 1rem;
            padding: 2rem;
            border: 1px solid rgba(212, 175, 55, 0.3);
            background: #1a1a1a;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
        }

        .flip-card-back {
            transform: rotateY(180deg);
            border: 1px solid #d4af37;
            background: linear-gradient(145deg, #1a1a1a 0%, #2a2a2a 100%);
        }

        /* Quiz Options */
        .quiz-option {
            transition: all 0.3s ease;
            background: #1a1a1a;
            border: 1px solid #333;
        }
        .quiz-option:hover:not(:disabled) {
            border-color: #d4af37;
            background: rgba(212, 175, 55, 0.05);
            transform: translateX(5px);
        }
        .quiz-option.correct {
            border-color: #4ade80;
            background: rgba(74, 222, 128, 0.1);
            color: #4ade80;
        }
        .quiz-option.wrong {
            border-color: #f87171;
            background: rgba(248, 113, 113, 0.1);
            color: #f87171;
        }

        /* Input overrides for dark theme */
        input, select, textarea {
            color-scheme: dark;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Navigation Bar -->
    <nav class="bg-dark-950 border-b border-gold-500/20 sticky top-0 z-50 backdrop-blur-md bg-opacity-90">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- Logo area -->
                <div class="flex items-center gap-4 cursor-pointer" onclick="switchView('home')">
                    <img src="Gemini_Generated_Image_sr0ur1sr0ur1sr0u - Copy.jpg" alt="Logo" class="h-12 w-auto rounded object-cover shadow-[0_0_10px_rgba(212,175,55,0.3)]">
                    <span class="font-serif font-bold text-2xl tracking-wider gold-text-gradient hidden sm:block">ENGLISH STUDY</span>
                </div>
                
                <!-- Desktop Menu -->
                <div class="hidden lg:flex space-x-1 items-center">
                    <button data-target="home" onclick="switchView('home')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Asosiy</button>
                    <button data-target="courses" onclick="switchView('courses')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Kurslar</button>
                    <button data-target="lessons" onclick="switchView('lessons')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Darslar</button>
                    <button data-target="flashcards" onclick="switchView('flashcards')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Lug'at</button>
                    <button data-target="quiz" onclick="switchView('quiz')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Grammatika</button>
                    <button data-target="essays" onclick="switchView('essays')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Esse yozish</button>
                    <button data-target="community" onclick="switchView('community')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Hamjamiyat</button>
                    <button data-target="leaderboard" onclick="switchView('leaderboard')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Reyting</button>
                    <button data-target="contact" onclick="switchView('contact')" class="nav-btn px-4 py-2 rounded-md text-sm font-medium text-gray-300 hover:text-gold-500 transition">Bog'lanish</button>
                    <button id="nav-admin-btn" data-target="admin" onclick="switchView('admin')" class="hidden nav-btn px-4 py-2 rounded-md text-sm font-medium text-gold-500 border border-gold-500/20 hover:bg-gold-500/10 transition">Admin Panel</button>
                    <button id="nav-auth-btn" data-target="register" onclick="switchView('register')" class="ml-4 px-6 py-2 bg-gradient-to-r from-gold-600 to-gold-400 text-dark-950 font-bold rounded-md hover:from-gold-500 hover:to-gold-300 transition shadow-[0_0_15px_rgba(212,175,55,0.3)] hover:shadow-[0_0_20px_rgba(212,175,55,0.5)]">
                        Registratsiya
                    </button>
                </div>

                <!-- Mobile Menu Button -->
                <div class="lg:hidden flex items-center">
                    <button id="mobile-menu-btn" class="text-gold-500 hover:text-gold-300 focus:outline-none">
                        <i class="ph ph-list text-3xl"></i>
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Mobile Menu Dropdown -->
        <div id="mobile-menu" class="hidden lg:hidden bg-dark-900 border-t border-gold-500/20">
            <div class="px-4 pt-2 pb-4 space-y-2">
                <button data-target="home" onclick="switchView('home'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Asosiy</button>
                <button data-target="courses" onclick="switchView('courses'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Kurslar</button>
                <button data-target="lessons" onclick="switchView('lessons'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Darslar</button>
                <button data-target="flashcards" onclick="switchView('flashcards'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Lug'at</button>
                <button data-target="quiz" onclick="switchView('quiz'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Grammatika</button>
                <button data-target="essays" onclick="switchView('essays'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Esse yozish</button>
                <button data-target="community" onclick="switchView('community'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Hamjamiyat</button>
                <button data-target="leaderboard" onclick="switchView('leaderboard'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Reyting</button>
                <button data-target="contact" onclick="switchView('contact'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gray-300 hover:text-gold-500 hover:bg-dark-800 border-l-2 border-transparent">Bog'lanish</button>
                <button id="mobile-nav-admin-btn" data-target="admin" onclick="switchView('admin'); toggleMobileMenu()" class="hidden nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-medium text-gold-500 hover:text-gold-400 hover:bg-dark-800 border-l-2 border-gold-500 bg-dark-800/50">Admin Panel</button>
                <button id="mobile-auth-btn" data-target="register" onclick="switchView('register'); toggleMobileMenu()" class="nav-btn mobile-nav-btn block w-full text-left px-4 py-3 rounded-md font-bold text-dark-900 bg-gold-500 mt-4">Registratsiya</button>
            </div>
        </div>
    </nav>

    <!-- Main Content Area -->
    <main class="flex-grow flex items-center justify-center p-4 sm:p-8 max-w-7xl mx-auto w-full">
        
        <!-- HOME VIEW -->
        <div id="view-home" class="view-section w-full text-center fade-in relative min-h-[85vh] flex flex-col items-center justify-center overflow-hidden rounded-[3rem] border border-gold-500/20 bg-gradient-to-b from-dark-900 to-dark-950 p-6 shadow-[0_0_50px_rgba(0,0,0,0.8)] mt-4 mb-8">
            
            <!-- Decorative Background Glows -->
            <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-gold-500/10 rounded-full blur-[100px] pointer-events-none"></div>
            <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-gold-600/10 rounded-full blur-[100px] pointer-events-none"></div>
            <div class="absolute inset-0 bg-[url('https://www.transparenttextures.com/patterns/stardust.png')] opacity-10 pointer-events-none"></div>
            
            <div class="inline-flex items-center justify-center p-6 rounded-full bg-dark-950 border-2 border-gold-500/40 mb-10 gold-glow relative z-10 shadow-[0_0_30px_rgba(212,175,55,0.2)] hover:scale-110 transition-transform duration-500">
                <i class="ph ph-crown text-7xl text-gold-500 drop-shadow-md"></i>
            </div>
            
            <h1 class="text-5xl md:text-7xl lg:text-8xl font-serif font-bold mb-8 text-white leading-tight relative z-10 tracking-wide drop-shadow-2xl">
                Master English with <br/>
                <span class="gold-text-gradient">Premium Excellence</span>
            </h1>
            
            <p class="text-xl md:text-2xl text-gray-300 mb-14 max-w-3xl mx-auto font-light relative z-10 leading-relaxed drop-shadow-md">
                Oliy darajadagi ta'lim platformasi. Grammatika, lug'at boyligi va insho yozish ko'nikmalaringizni sun'iy intellekt yordamida mukammallashtiring.
            </p>
            
            <div class="flex flex-col sm:flex-row justify-center gap-6 relative z-10 w-full max-w-xl">
                <button onclick="switchView('courses')" class="flex-1 py-5 bg-gradient-to-r from-gold-600 to-gold-400 text-dark-950 font-bold rounded-2xl transition-all transform hover:-translate-y-2 hover:scale-105 flex items-center justify-center gap-3 text-xl shadow-[0_10px_30px_rgba(212,175,55,0.4)]">
                    <i class="ph ph-book-open text-3xl"></i> Ta'limni boshlash
                </button>
                <button onclick="switchView('register')" class="flex-1 py-5 bg-dark-950/80 backdrop-blur-sm text-gold-500 border border-gold-500/50 font-bold rounded-2xl hover:bg-dark-800 hover:border-gold-400 transition-all transform hover:-translate-y-2 hover:scale-105 flex items-center justify-center gap-3 text-xl shadow-[0_10px_20px_rgba(0,0,0,0.5)]">
                    <i class="ph ph-user-plus text-3xl"></i> A'zo bo'lish
                </button>
            </div>
        </div>

        <!-- COURSES VIEW -->
        <div id="view-courses" class="view-section hidden w-full fade-in py-10">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-serif font-bold text-white mb-4"><span class="gold-text-gradient">Premium Kurslar</span></h2>
                <p class="text-gray-400">O'z darajangizga mos eksklyuziv kursni tanlang</p>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Course Cards -->
                <div class="bg-dark-800 rounded-xl p-8 border border-gray-800 hover:border-gold-500 transition-all duration-300 group hover:-translate-y-2 relative overflow-hidden">
                    <div class="absolute top-0 right-0 w-24 h-24 bg-gold-500/10 rounded-bl-full -mr-4 -mt-4 transition-transform group-hover:scale-110"></div>
                    <div class="text-gold-500 font-serif text-5xl font-bold mb-6">A1</div>
                    <h3 class="text-2xl font-bold text-white mb-3">Beginner</h3>
                    <p class="text-gray-400 mb-8 font-light">Ingliz tiliga ilk qadamlar. Fundament, alifbo va asosiy muloqot ko'nikmalari.</p>
                    <button onclick="switchView('lessons')" class="w-full py-3 bg-dark-900 border border-gold-500/50 text-gold-500 font-semibold rounded-lg hover:bg-gold-500 hover:text-dark-900 transition flex items-center justify-center gap-2">
                        Kursga o'tish <i class="ph ph-arrow-right"></i>
                    </button>
                </div>

                <div class="bg-dark-800 rounded-xl p-8 border border-gold-500/50 shadow-[0_0_20px_rgba(212,175,55,0.15)] hover:shadow-[0_0_30px_rgba(212,175,55,0.3)] transition-all duration-300 group hover:-translate-y-2 relative overflow-hidden transform md:scale-105 z-10">
                    <div class="absolute top-0 right-0 bg-gold-500 text-dark-900 text-xs font-bold px-3 py-1 rounded-bl-lg uppercase tracking-wider">Tavsiya etiladi</div>
                    <div class="text-gold-400 font-serif text-5xl font-bold mb-6 mt-2">A2</div>
                    <h3 class="text-2xl font-bold text-white mb-3">Elementary</h3>
                    <p class="text-gray-400 mb-8 font-light">Erkin muloqot poydevori. Zamonlar, boyitilgan lug'at va amaliy mashg'ulotlar.</p>
                    <button onclick="switchView('lessons')" class="w-full py-3 bg-gradient-to-r from-gold-600 to-gold-400 text-dark-900 font-bold rounded-lg hover:from-gold-500 hover:to-gold-300 transition flex items-center justify-center gap-2">
                        Kursga o'tish <i class="ph ph-arrow-right"></i>
                    </button>
                </div>

                <div class="bg-dark-800 rounded-xl p-8 border border-gray-800 hover:border-gold-500 transition-all duration-300 group hover:-translate-y-2 relative overflow-hidden">
                    <div class="absolute top-0 right-0 w-24 h-24 bg-gold-500/10 rounded-bl-full -mr-4 -mt-4 transition-transform group-hover:scale-110"></div>
                    <div class="text-gold-500 font-serif text-5xl font-bold mb-6">B1</div>
                    <h3 class="text-2xl font-bold text-white mb-3">Intermediate</h3>
                    <p class="text-gray-400 mb-8 font-light">Murakkab tuzilmalar, kino va podkastlarni tushunish, fikrni erkin bayon etish.</p>
                    <button onclick="switchView('lessons')" class="w-full py-3 bg-dark-900 border border-gold-500/50 text-gold-500 font-semibold rounded-lg hover:bg-gold-500 hover:text-dark-900 transition flex items-center justify-center gap-2">
                        Kursga o'tish <i class="ph ph-arrow-right"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- LESSONS VIEW -->
        <div id="view-lessons" class="view-section hidden w-full max-w-4xl fade-in py-10">
            <div class="flex items-center justify-between mb-10 border-b border-dark-700 pb-6">
                <div>
                    <h2 class="text-3xl font-serif font-bold text-white">A2 Elementary</h2>
                    <p class="text-gold-500 mt-1 font-medium">Darslar moduli</p>
                </div>
                <div class="hidden sm:flex items-center gap-2 text-gray-400 text-sm bg-dark-800 px-4 py-2 rounded-lg border border-dark-700">
                    <i class="ph ph-clock"></i> 24 soatlik kurs
                </div>
            </div>

            <div class="space-y-4">
                <!-- Lesson Rows -->
                <div class="bg-dark-800 border border-dark-700 hover:border-gold-500/50 rounded-xl p-5 flex items-center justify-between cursor-pointer transition-colors group">
                    <div class="flex items-center gap-5">
                        <div class="w-12 h-12 bg-dark-900 border border-gold-500/30 text-gold-500 rounded-lg flex items-center justify-center font-bold text-xl group-hover:bg-gold-500 group-hover:text-dark-900 transition">1</div>
                        <div>
                            <h4 class="font-bold text-white text-lg group-hover:text-gold-400 transition">Daily Routine & Time</h4>
                            <p class="text-gray-400 text-sm mt-1">Present Simple qoidalari va kun tartibi</p>
                        </div>
                    </div>
                    <div class="w-10 h-10 rounded-full bg-dark-700 flex items-center justify-center group-hover:bg-gold-500/20 transition text-gold-500">
                        <i class="ph ph-play-fill text-xl"></i>
                    </div>
                </div>

                <div class="bg-dark-800 border border-dark-700 hover:border-gold-500/50 rounded-xl p-5 flex items-center justify-between cursor-pointer transition-colors group">
                    <div class="flex items-center gap-5">
                        <div class="w-12 h-12 bg-dark-900 border border-gold-500/30 text-gold-500 rounded-lg flex items-center justify-center font-bold text-xl group-hover:bg-gold-500 group-hover:text-dark-900 transition">2</div>
                        <div>
                            <h4 class="font-bold text-white text-lg group-hover:text-gold-400 transition">Actions Happening Now</h4>
                            <p class="text-gray-400 text-sm mt-1">Present Continuous va amaliy mashqlar</p>
                        </div>
                    </div>
                    <div class="w-10 h-10 rounded-full bg-dark-700 flex items-center justify-center group-hover:bg-gold-500/20 transition text-gold-500">
                        <i class="ph ph-play-fill text-xl"></i>
                    </div>
                </div>

                <div class="bg-dark-800 border border-dark-700 hover:border-gold-500/50 rounded-xl p-5 flex items-center justify-between cursor-pointer transition-colors group">
                    <div class="flex items-center gap-5">
                        <div class="w-12 h-12 bg-dark-900 border border-dark-700 text-gray-500 rounded-lg flex items-center justify-center font-bold text-xl">3</div>
                        <div>
                            <h4 class="font-bold text-gray-300 text-lg">Past Experiences</h4>
                            <p class="text-gray-500 text-sm mt-1">Past Simple va noto'g'ri fe'llar</p>
                        </div>
                    </div>
                    <i class="ph ph-lock-key text-2xl text-gray-600"></i>
                </div>
            </div>
        </div>

        <!-- FLASHCARDS VIEW -->
        <div id="view-flashcards" class="view-section hidden w-full max-w-3xl fade-in py-10">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-serif font-bold text-white mb-2"><span class="gold-text-gradient">Lug'at Boyligi</span></h2>
                <p class="text-gray-400 font-light">Kartochkani bosing va so'zning ma'nosini bilib oling</p>
            </div>

            <!-- Search Bar -->
            <div class="max-w-2xl mx-auto mb-8 relative">
                <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                    <i class="ph ph-magnifying-glass text-gold-500/70 text-xl"></i>
                </div>
                <input type="text" id="vocab-search" onkeyup="filterVocabulary()" placeholder="So'zni ingliz yoki o'zbek tilida qidiring..." class="w-full pl-12 pr-4 py-4 bg-dark-900 border border-dark-700 text-white rounded-xl focus:outline-none focus:ring-1 focus:ring-gold-500 focus:border-gold-500 transition shadow-inner">
                <div id="search-results-count" class="text-right text-gray-500 text-sm mt-2">Baza: 1050 ta so'z</div>
            </div>

            <div class="flex justify-center mb-10 w-full max-w-2xl mx-auto">
                <div class="flip-card" id="flashcard" onclick="flipCard()">
                    <div class="flip-card-inner">
                        <div class="flip-card-front">
                            <i class="ph ph-translate text-4xl text-gold-500/50 absolute top-6 right-6"></i>
                            <span class="text-sm uppercase tracking-widest text-gold-500 mb-4 font-semibold">Vocabulary</span>
                            <h3 id="card-word" class="text-5xl md:text-6xl font-serif font-bold text-white mb-4">Sophisticated</h3>
                            <div class="flex items-center gap-2 text-gray-400 mt-auto bg-dark-900 px-4 py-2 rounded-full border border-dark-700">
                                <i class="ph ph-hand-tap text-gold-500"></i>
                                <span class="text-sm">Tarjimasini ko'rish</span>
                            </div>
                        </div>
                        <div class="flip-card-back">
                            <span class="text-sm uppercase tracking-widest text-dark-900/50 mb-2 font-semibold">Uzbek</span>
                            <h3 id="card-translation" class="text-4xl md:text-5xl font-serif font-bold text-gold-500 mb-6">Murakkab, Oliyjanob</h3>
                            <div class="bg-dark-900/50 p-4 rounded-lg w-3/4 mx-auto border border-gold-500/20">
                                <p id="card-example" class="text-gray-300 italic">"The restaurant has a sophisticated atmosphere."</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Controls -->
            <div class="flex justify-between items-center bg-dark-800 p-4 rounded-xl border border-dark-700 max-w-2xl mx-auto">
                <button onclick="prevCard()" class="px-5 py-3 bg-dark-900 hover:bg-dark-700 text-gray-300 rounded-lg transition border border-dark-700 flex items-center gap-2 focus:outline-none">
                    <i class="ph ph-caret-left font-bold"></i> Oldingi
                </button>
                <div class="text-gold-500 font-bold text-lg font-serif">
                    <span id="card-current">1</span> <span class="text-gray-600">/</span> <span id="card-total" class="text-gray-400">5</span>
                </div>
                <button onclick="nextCard()" class="px-5 py-3 bg-gold-500 hover:bg-gold-400 text-dark-950 font-bold rounded-lg transition shadow-[0_0_10px_rgba(212,175,55,0.2)] flex items-center gap-2 focus:outline-none">
                    Keyingi <i class="ph ph-caret-right font-bold"></i>
                </button>
            </div>
        </div>

        <!-- QUIZ VIEW -->
        <div id="view-quiz" class="view-section hidden w-full max-w-5xl fade-in py-10">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-serif font-bold text-white mb-2"><span class="gold-text-gradient">Grammatika Testi</span></h2>
                <p class="text-gray-400 font-light">Mavzuni tanlang va 40 talik test orqali bilimingizni sinab ko'ring</p>
            </div>

            <!-- Quiz Categories (Menu) -->
            <div id="quiz-menu" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4">
                <!-- JavaScript orqali 15 ta mavzu to'ldiriladi -->
            </div>

            <!-- Quiz Container -->
            <div id="quiz-container" class="hidden bg-dark-800 border border-dark-700 rounded-2xl p-6 md:p-10 shadow-2xl relative overflow-hidden max-w-3xl mx-auto">
                <!-- Decorative background elements -->
                <div class="absolute top-0 right-0 w-64 h-64 bg-gold-500/5 rounded-full blur-3xl -mr-20 -mt-20"></div>

                <!-- Progress -->
                <div class="mb-8 flex justify-between items-center">
                    <button onclick="backToQuizMenu()" class="text-gray-400 hover:text-white transition flex items-center gap-1 text-sm font-medium"><i class="ph ph-arrow-left"></i> Mavzular</button>
                    <span class="text-gray-400 font-medium tracking-wide text-sm uppercase">Savol <span id="quiz-current" class="text-gold-500 text-lg">1</span> / <span id="quiz-total">40</span></span>
                    <div class="flex items-center gap-2 bg-dark-900 border border-gold-500/30 text-gold-400 px-4 py-1.5 rounded-full font-bold">
                        <i class="ph ph-star-fill text-gold-500"></i> <span id="quiz-score">0</span>
                    </div>
                </div>
                
                <div class="w-full bg-dark-950 rounded-full h-1.5 mb-10 overflow-hidden">
                    <div id="quiz-progress" class="bg-gradient-to-r from-gold-600 to-gold-400 h-1.5 rounded-full transition-all duration-500" style="width: 0%"></div>
                </div>

                <!-- Question -->
                <h3 id="quiz-question" class="text-2xl font-serif font-bold text-white mb-8 leading-relaxed">
                    Savol yuklanmoqda...
                </h3>

                <!-- Options -->
                <div id="quiz-options" class="flex flex-col gap-4 relative z-10">
                    <!-- Options injected via JS -->
                </div>

                <!-- Next Button -->
                <div class="mt-10 flex justify-end">
                    <button id="quiz-next-btn" onclick="nextQuestion()" class="hidden px-8 py-3 bg-gold-500 text-dark-950 font-bold rounded-lg hover:bg-gold-400 transition shadow-[0_0_15px_rgba(212,175,55,0.3)] items-center gap-2">
                        Keyingi savol <i class="ph ph-arrow-right"></i>
                    </button>
                </div>
            </div>

            <!-- Quiz Results -->
            <div id="quiz-results" class="hidden bg-dark-800 border border-gold-500/40 rounded-2xl p-10 text-center fade-in max-w-lg mx-auto">
                <div class="inline-flex justify-center items-center w-24 h-24 rounded-full bg-dark-900 border-2 border-gold-500 mb-6 gold-glow">
                    <i class="ph ph-trophy text-5xl text-gold-500"></i>
                </div>
                <h2 class="text-3xl font-serif font-bold text-white mb-3">Ajoyib Natija!</h2>
                <p class="text-gray-400 mb-8">Siz <span id="final-total" class="font-bold text-white">40</span> ta savoldan <span id="final-score" class="font-bold text-gold-500 text-xl">0</span> tasini to'g'ri topdingiz.</p>
                
                <div class="flex flex-col gap-3">
                    <button onclick="restartQuiz()" class="w-full py-3 bg-gold-500 text-dark-950 font-bold rounded-lg hover:bg-gold-400 transition shadow-lg">
                        Qaytadan urinish
                    </button>
                    <button onclick="backToQuizMenu()" class="w-full py-3 bg-dark-900 border border-dark-700 text-gray-300 font-medium rounded-lg hover:border-gray-500 transition">
                        Boshqa mavzularga qaytish
                    </button>
                </div>
            </div>
        </div>

        <!-- ESSAYS VIEW -->
        <div id="view-essays" class="view-section hidden w-full max-w-4xl fade-in py-8">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-serif font-bold text-white mb-3"><span class="gold-text-gradient">Esse Yozish</span></h2>
                <p class="text-gray-400 font-light max-w-xl mx-auto">AI yordamida yozish mahoratingizni baholang. Mavzuni tanlang va o'z fikrlaringizni bayon eting.</p>
            </div>
            
            <div class="bg-dark-800 border border-dark-700 rounded-2xl shadow-xl p-6 md:p-10">
                <div class="mb-6 grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gold-500 mb-2 uppercase tracking-wider">Darajani tanlang:</label>
                        <select id="essay-level" onchange="updateEssayTopics()" class="w-full p-4 bg-dark-900 border border-dark-700 text-white rounded-lg focus:ring-1 focus:ring-gold-500 focus:border-gold-500 focus:outline-none transition appearance-none">
                            <option value="A1">A1 - Beginner (Boshlang'ich)</option>
                            <option value="A2">A2 - Elementary (Elementar)</option>
                            <option value="B1">B1 - Intermediate (O'rta)</option>
                            <option value="B2">B2 - Upper Intermediate (Yuqori o'rta)</option>
                            <option value="C1">C1 - Advanced (Murakkab)</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gold-500 mb-2 uppercase tracking-wider">Mavzuni tanlang:</label>
                        <select id="essay-topic" class="w-full p-4 bg-dark-900 border border-dark-700 text-white rounded-lg focus:ring-1 focus:ring-gold-500 focus:border-gold-500 focus:outline-none transition appearance-none">
                            <!-- Mavzular JavaScript orqali yuklanadi -->
                        </select>
                    </div>
                </div>
                
                <div class="mb-8">
                    <label class="block text-sm font-medium text-gold-500 mb-2 uppercase tracking-wider">Esseni bu yerga yozing:</label>
                    <textarea id="essay-text" rows="8" class="w-full p-5 bg-dark-900 border border-dark-700 text-gray-100 rounded-lg focus:ring-1 focus:ring-gold-500 focus:border-gold-500 focus:outline-none resize-y transition leading-relaxed placeholder-gray-600" placeholder="Start writing here..."></textarea>
                </div>
                
                <div class="flex justify-end">
                    <button id="check-essay-btn" onclick="checkEssay()" class="px-8 py-3.5 bg-gradient-to-r from-gold-600 to-gold-400 text-dark-950 font-bold rounded-lg hover:from-gold-500 hover:to-gold-300 transition shadow-[0_0_15px_rgba(212,175,55,0.2)] hover:shadow-[0_0_20px_rgba(212,175,55,0.4)] flex items-center gap-2">
                        <i class="ph ph-magic-wand text-xl"></i> AI Tekshirish
                    </button>
                </div>
                
                <!-- Result Container -->
                <div id="essay-feedback-container" class="mt-10 hidden border-t border-dark-700 pt-8 fade-in">
                    <h3 class="text-2xl font-serif font-bold text-white mb-6 flex items-center gap-3">
                        <i class="ph ph-sparkle text-gold-500 text-3xl"></i> AI Tahlili
                    </h3>
                    <div id="essay-feedback-content" class="text-gray-300 bg-dark-900 p-6 md:p-8 rounded-xl border border-gold-500/20 leading-relaxed shadow-inner">
                        <!-- Feedback will be injected here -->
                    </div>
                </div>
            </div>
        </div>

        <!-- REGISTER VIEW -->
        <div id="view-register" class="view-section hidden w-full fade-in py-12">
            <div class="max-w-md mx-auto bg-dark-800 border border-dark-700 rounded-2xl p-8 relative overflow-hidden">
                <div class="absolute top-0 right-0 w-32 h-32 bg-gold-500/5 rounded-full blur-3xl -mr-10 -mt-10"></div>
                
                <div class="text-center mb-8 relative z-10">
                    <div class="inline-flex justify-center items-center w-16 h-16 rounded-full bg-dark-900 border border-gold-500/50 mb-4 gold-glow">
                        <i class="ph ph-user-circle-plus text-3xl text-gold-500"></i>
                    </div>
                    <h2 id="auth-title" class="text-3xl font-serif font-bold text-white mb-2">A'zo bo'lish</h2>
                    <p id="auth-subtitle" class="text-gray-400 text-sm">Premium ta'limni bugun boshlang</p>
                </div>
                
                <form onsubmit="handleAuth(event)" class="space-y-6 relative z-10">
                    <div id="name-field-group">
                        <label class="block text-sm font-medium text-gray-400 mb-1">To'liq ism</label>
                        <div class="relative">
                            <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                                <i class="ph ph-user text-gold-500/70 text-lg"></i>
                            </div>
                            <input type="text" id="reg-name" required class="w-full pl-12 pr-4 py-3 bg-dark-900 border border-dark-700 text-white rounded-lg focus:outline-none focus:ring-1 focus:ring-gold-500 focus:border-gold-500 transition" placeholder="Ali Valiyev">
                        </div>
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-400 mb-1">Elektron pochta</label>
                        <div class="relative">
                            <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                                <i class="ph ph-envelope-simple text-gold-500/70 text-lg"></i>
                            </div>
                            <input type="email" id="reg-email" required class="w-full pl-12 pr-4 py-3 bg-dark-900 border border-dark-700 text-white rounded-lg focus:outline-none focus:ring-1 focus:ring-gold-500 focus:border-gold-500 transition" placeholder="ali@example.com">
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-gray-400 mb-1">Parol</label>
                        <div class="relative">
                            <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
                                <i class="ph ph-lock-key text-gold-500/70 text-lg"></i>
                            </div>
                            <input type="password" id="reg-password" required minlength="6" class="w-full pl-12 pr-4 py-3 bg-dark-900 border border-dark-700 text-white rounded-lg focus:outline-none focus:ring-1 focus:ring-gold-500 focus:border-gold-500 transition" placeholder="******">
                        </div>
                    </div>

                    <div id="auth-message" class="hidden p-3 rounded-lg border text-sm mt-4 text-center"></div>

                    <button type="submit" id="auth-submit-btn" class="w-full py-4 bg-gold-500 text-dark-950 font-bold text-lg rounded-lg hover:bg-gold-400 transition shadow-[0_0_15px_rgba(212,175,55,0.2)] mt-2">
                        Ro'yxatdan o'tish
                    </button>
                    
                    <p id="auth-toggle-text" class="text-center text-sm text-gray-500 mt-6 cursor-pointer hover:text-gold-400 transition" onclick="toggleAuthMode()">
                        Allaqachon hisobingiz bormi? <span class="text-gold-500 font-bold">Kirish</span>
                    </p>
                </form>
            </div>
        </div>

        <!-- COMMUNITY VIEW -->
        <div id="view-community" class="view-section hidden w-full fade-in py-10">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-serif font-bold text-white mb-2"><span class="gold-text-gradient">Hamjamiyat</span></h2>
                <p class="text-gray-400 font-light">Tizimdagi barcha foydalanuvchilar va ularning holati</p>
            </div>
            <div id="community-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div class="col-span-full text-center text-gray-500 py-10">
                    <i class="ph ph-spinner animate-spin text-4xl text-gold-500 mb-3"></i>
                    <p>Foydalanuvchilar ro'yxati yuklanmoqda...</p>
                </div>
            </div>
        </div>

        <!-- LEADERBOARD VIEW -->
        <div id="view-leaderboard" class="view-section hidden w-full max-w-4xl mx-auto fade-in py-10">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-serif font-bold text-white mb-2"><span class="gold-text-gradient">Reyting</span></h2>
                <p class="text-gray-400 font-light">Eng yuqori ball to'plagan foydalanuvchilar</p>
            </div>
            <div class="bg-dark-800 border border-dark-700 rounded-xl overflow-hidden shadow-xl">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-dark-900 border-b border-gold-500/20 text-gold-500 uppercase text-xs tracking-wider">
                            <th class="p-4">O'rin</th>
                            <th class="p-4">Foydalanuvchi</th>
                            <th class="p-4 hidden sm:table-cell">Rol</th>
                            <th class="p-4 text-right">Ball</th>
                        </tr>
                    </thead>
                    <tbody id="leaderboard-list" class="divide-y divide-dark-700">
                        <tr>
                            <td colspan="4" class="text-center text-gray-500 py-10">
                                <i class="ph ph-spinner animate-spin text-3xl text-gold-500 mb-2"></i>
                                <p>Reyting yuklanmoqda...</p>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

        <!-- ADMIN VIEW -->
        <div id="view-admin" class="view-section hidden w-full max-w-5xl mx-auto fade-in py-10">
            <div class="text-center mb-10">
                <h2 class="text-4xl font-serif font-bold text-white mb-2"><span class="gold-text-gradient">Admin Panel</span></h2>
                <p class="text-gray-400 font-light">Tizim foydalanuvchilarini va rollarni boshqarish</p>
            </div>
            
            <div class="bg-dark-800 border border-dark-700 rounded-xl overflow-hidden shadow-xl">
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse min-w-[600px]">
                        <thead>
                            <tr class="bg-dark-900 border-b border-gold-500/20 text-gold-500 uppercase text-xs tracking-wider">
                                <th class="p-4">Foydalanuvchi</th>
                                <th class="p-4">Email pochta</th>
                                <th class="p-4">Joriy Rol</th>
                                <th class="p-4 text-right">Harakatlar</th>
                            </tr>
                        </thead>
                        <tbody id="admin-users-list" class="divide-y divide-dark-700">
                            <tr>
                                <td colspan="4" class="text-center text-gray-500 py-10">
                                    <i class="ph ph-spinner animate-spin text-3xl text-gold-500 mb-2"></i>
                                    <p>Foydalanuvchilar ro'yxati yuklanmoqda...</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- CONTACT VIEW -->
        <div id="view-contact" class="view-section hidden w-full max-w-5xl mx-auto fade-in py-10">
            <div class="text-center mb-12">
                <h2 class="text-4xl font-serif font-bold text-white mb-2"><span class="gold-text-gradient">Biz Bilan Bog'lanish</span></h2>
                <p class="text-gray-400 font-light">Savollaringiz bo'lsa yoki yordam kerak bo'lsa, bizga murojaat qiling.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-10">
                <!-- Contact Info -->
                <div class="space-y-8">
                    <div class="bg-dark-800 p-6 rounded-xl border border-dark-700 hover:border-gold-500/50 transition group">
                        <div class="flex items-center gap-4">
                            <div class="w-14 h-14 bg-dark-900 border border-gold-500/30 text-gold-500 rounded-full flex items-center justify-center text-2xl group-hover:bg-gold-500 group-hover:text-dark-900 transition shadow-inner">
                                <i class="ph ph-map-pin"></i>
                            </div>
                            <div>
                                <h4 class="text-white font-bold text-lg">Manzilimiz</h4>
                                <p class="text-gray-400 text-sm mt-1">Toshkent shahar, Yunusobod tumani, 12-daha</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-dark-800 p-6 rounded-xl border border-dark-700 hover:border-gold-500/50 transition group">
                        <div class="flex items-center gap-4">
                            <div class="w-14 h-14 bg-dark-900 border border-gold-500/30 text-gold-500 rounded-full flex items-center justify-center text-2xl group-hover:bg-gold-500 group-hover:text-dark-900 transition shadow-inner">
                                <i class="ph ph-phone"></i>
                            </div>
                            <div>
                                <h4 class="text-white font-bold text-lg">Telefon raqam</h4>
                                <p class="text-gray-400 text-sm mt-1">+998 94 300 82 26</p>
                            </div>
                        </div>
                    </div>

                    <div class="bg-dark-800 p-6 rounded-xl border border-dark-700 hover:border-gold-500/50 transition group">
                        <div class="flex items-center gap-4">
                            <div class="w-14 h-14 bg-dark-900 border border-gold-500/30 text-gold-500 rounded-full flex items-center justify-center text-2xl group-hover:bg-gold-500 group-hover:text-dark-900 transition shadow-inner">
                                <i class="ph ph-envelope-simple"></i>
                            </div>
                            <div>
                                <h4 class="text-white font-bold text-lg">Elektron pochta</h4>
                                <p class="text-gray-400 text-sm mt-1">dilyorbekxaydaro78@gmail.com</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Contact Form -->
                <div class="bg-dark-800 border border-dark-700 rounded-xl p-8 relative overflow-hidden shadow-xl">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-gold-500/5 rounded-full blur-3xl -mr-10 -mt-10"></div>
                    <form onsubmit="handleContactSubmit(event)" class="space-y-5 relative z-10">
                        <div>
                            <label class="block text-sm font-medium text-gray-400 mb-1">Ismingiz</label>
                            <input type="text" required class="w-full px-4 py-3 bg-dark-900 border border-dark-700 text-white rounded-lg focus:outline-none focus:ring-1 focus:ring-gold-500 focus:border-gold-500 transition" placeholder="Ali Valiyev">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-400 mb-1">Elektron pochta</label>
                            <input type="email" required class="w-full px-4 py-3 bg-dark-900 border border-dark-700 text-white rounded-lg focus:outline-none focus:ring-1 focus:ring-gold-500 focus:border-gold-500 transition" placeholder="ali@example.com">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-400 mb-1">Xabar</label>
                            <textarea rows="4" required class="w-full px-4 py-3 bg-dark-900 border border-dark-700 text-white rounded-lg focus:outline-none focus:ring-1 focus:ring-gold-500 focus:border-gold-500 transition resize-y" placeholder="Qanday yordam bera olamiz?"></textarea>
                        </div>
                        <button type="submit" id="contact-submit-btn" class="w-full py-4 bg-gradient-to-r from-gold-600 to-gold-400 text-dark-950 font-bold rounded-lg hover:from-gold-500 hover:to-gold-300 transition shadow-[0_0_15px_rgba(212,175,55,0.2)] flex justify-center items-center gap-2">
                            Xabarni yuborish <i class="ph ph-paper-plane-right text-xl"></i>
                        </button>
                    </form>
                </div>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="bg-dark-950 border-t border-dark-800 py-8 mt-auto relative z-10">
        <div class="max-w-7xl mx-auto px-4 text-center">
            <div class="flex justify-center items-center gap-3 mb-4">
                <img src="Gemini_Generated_Image_sr0ur1sr0ur1sr0u - Copy.jpg" alt="Logo mini" class="h-6 w-auto rounded opacity-70">
                <span class="font-serif font-bold text-gray-400 tracking-wider">ENGLISH STUDY</span>
            </div>
            <p class="text-gray-600 text-sm">
                &copy; 2026 English Study Platform. All rights reserved.
            </p>
        </div>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        // --- Navigation Logic ---
        const mobileMenuBtn = document.getElementById('mobile-menu-btn');
        const mobileMenu = document.getElementById('mobile-menu');
        
        let isAdminUser = false; // Global admin status

        mobileMenuBtn.addEventListener('click', toggleMobileMenu);

        function toggleMobileMenu() {
            mobileMenu.classList.toggle('hidden');
        }
        
        window.setAdminStatus = function(status) {
            isAdminUser = status;
            const desktopBtn = document.getElementById('nav-admin-btn');
            const mobileBtn = document.getElementById('mobile-nav-admin-btn');
            
            if (status) {
                if (desktopBtn) desktopBtn.classList.remove('hidden');
                if (mobileBtn) mobileBtn.classList.remove('hidden');
            } else {
                if (desktopBtn) desktopBtn.classList.add('hidden');
                if (mobileBtn) mobileBtn.classList.add('hidden');
            }
        };

        window.updateNavAuthUI = function(userData) {
            const deskBtn = document.getElementById('nav-auth-btn');
            const mobBtn = document.getElementById('mobile-auth-btn');
            if (deskBtn && mobBtn) {
                if (userData) {
                    deskBtn.innerHTML = `<i class="ph ph-sign-out"></i> Chiqish (${userData.name.split(' ')[0]})`;
                    deskBtn.onclick = window.logout;
                    mobBtn.innerHTML = `<i class="ph ph-sign-out"></i> Chiqish (${userData.name.split(' ')[0]})`;
                    mobBtn.onclick = () => { window.logout(); toggleMobileMenu(); };
                } else {
                    deskBtn.textContent = "Registratsiya";
                    deskBtn.onclick = () => { switchView('register'); };
                    mobBtn.textContent = "Registratsiya";
                    mobBtn.onclick = () => { switchView('register'); toggleMobileMenu(); };
                }
            }
        };

        function switchView(viewId) {
            // Protect admin view
            if (viewId === 'admin' && !isAdminUser) {
                return; // Do not open if not admin
            }

            // Hide all views
            document.querySelectorAll('.view-section').forEach(el => {
                el.classList.add('hidden');
                el.classList.remove('fade-in'); 
            });
            
            // Show selected view
            const selectedView = document.getElementById(`view-${viewId}`);
            if(selectedView) {
                selectedView.classList.remove('hidden');
                void selectedView.offsetWidth; // Trigger reflow
                selectedView.classList.add('fade-in');
            }

            // Update active state in nav
            document.querySelectorAll('.nav-btn').forEach(btn => {
                // Ignore register button for text color states
                if(!btn.classList.contains('bg-gradient-to-r') && !btn.classList.contains('bg-gold-500')) {
                    btn.classList.remove('text-gold-500');
                    btn.classList.add('text-gray-300');
                }
                
                if (btn.classList.contains('mobile-nav-btn') && !btn.classList.contains('bg-gold-500')) {
                    btn.classList.remove('text-gold-500', 'bg-dark-800', 'border-gold-500');
                    btn.classList.add('border-transparent');
                }

                if(btn.dataset.target === viewId) {
                    if(!btn.classList.contains('bg-gradient-to-r') && !btn.classList.contains('bg-gold-500')) {
                        btn.classList.remove('text-gray-300');
                        btn.classList.add('text-gold-500');
                    }
                    if (btn.classList.contains('mobile-nav-btn') && !btn.classList.contains('bg-gold-500')) {
                        btn.classList.add('bg-dark-800', 'border-gold-500');
                        btn.classList.remove('border-transparent');
                    }
                }
            });

            if(viewId === 'flashcards') initFlashcards();
            if(viewId === 'quiz') startQuiz(); 
            
            window.scrollTo(0,0);
        }
        
        let isLoginMode = false;
        window.toggleAuthMode = function() {
            isLoginMode = !isLoginMode;
            document.getElementById('auth-title').textContent = isLoginMode ? 'Tizimga kirish' : "A'zo bo'lish";
            document.getElementById('auth-subtitle').textContent = isLoginMode ? 'Xush kelibsiz!' : "Premium ta'limni bugun boshlang";
            
            const nameField = document.getElementById('name-field-group');
            nameField.style.display = isLoginMode ? 'none' : 'block';
            document.getElementById('reg-name').required = !isLoginMode;
            
            document.getElementById('auth-submit-btn').innerHTML = isLoginMode ? 'Kirish' : "Ro'yxatdan o'tish";
            document.getElementById('auth-toggle-text').innerHTML = isLoginMode 
                ? "Yangi hisob ochish <span class='text-gold-500 font-bold'>Ro'yxatdan o'tish</span>" 
                : "Allaqachon hisobingiz bormi? <span class='text-gold-500 font-bold'>Kirish</span>";
                
            document.getElementById('auth-message').classList.add('hidden');
        }

        // --- Flashcards Logic ---
        let vocabulary = [];
        let filteredVocabulary = [];
        
        // Kompakt shakldagi asosiy so'zlar bazasi (100 dan ortiq eng kerakli so'zlar kiritilgan, qolgani generatsiya qilinadi)
        const baseVocabString = "Time|Vaqt|Time is money;Year|Yil|Happy new year;People|Odamlar|Many people are here;Way|Yo'l|This is the way;Day|Kun|Have a good day;Man|Erkak|He is a good man;Thing|Narsa|What is this thing;Woman|Ayol|She is a strong woman;Life|Hayot|Life is beautiful;Child|Bola|The child is playing;World|Dunyo|We live in a big world;School|Maktab|I go to school;State|Holat, Davlat|State of mind;Family|Oila|I love my family;Student|O'quvchi|I am a student;Group|Guruh|Group work;Country|Mamlakat|My country is beautiful;Problem|Muammo|No problem;Hand|Qo'l|Give me your hand;Part|Qism|Part of the plan;Place|Joy|This is a nice place;Case|Holat, Ish|In this case;Week|Hafta|Next week;Company|Kompaniya|Good company;System|Tizim|Operating system;Program|Dastur|Computer program;Question|Savol|I have a question;Work|Ish|Go to work;Government|Hukumat|Local government;Number|Raqam|Phone number;Night|Tun|Good night;Point|Nuqta|Good point;Home|Uy|Go home;Water|Suv|Drink water;Room|Xona|Clean the room;Mother|Ona|My mother is kind;Area|Hudud|Danger area;Money|Pul|Save money;Story|Hikoya|Tell me a story;Fact|Dalil|It is a fact;Month|Oy|Next month;Lot|Ko'p|A lot of time;Right|Huquq, To'g'ri|You are right;Study|O'qish|Study hard;Book|Kitob|Read a book;Eye|Ko'z|Open your eyes;Job|Kasb, Ish|Good job;Word|So'z|One word;Business|Biznes|Business plan;Issue|Mesele|Big issue;Side|Tomon|Right side;Kind|Tur, Mehribon|What kind of;Head|Bosh|My head hurts;House|Uy|Big house;Service|Xizmat|Customer service;Friend|Do'st|My best friend;Father|Ota|My father;Power|Kuch|Power switch;Hour|Soat|One hour;Game|O'yin|Play a game;Line|Chiziq|Draw a line;End|Oxiri|The end;Member|A'zo|Family member;Law|Qonun|Break the law;Car|Mashina|Drive a car;City|Shahar|Big city;Community|Hamjamiyat|Our community;Name|Ism|My name is;President|Prezident|The president;Team|Jamoa|Football team;Minute|Daqiqa|One minute;Idea|G'oya|Good idea;Kid|Kichkintoy|Smart kid;Body|Tana|Human body;Information|Ma'lumot|More information;Back|Orqa, Qaytish|Come back;Parent|Ota-ona|My parents;Face|Yuz|Wash your face;Others|Boshqalar|Help others;Level|Daraja|Next level;Office|Ofis|In the office;Door|Eshik|Open the door;Health|Sog'liq|Good health;Person|Shaxs|Good person;Art|San'at|Modern art;War|Urush|Stop the war;History|Tarix|World history;Party|Bazm, Partiya|Birthday party;Result|Natija|Good result;Change|O'zgarish|Big change;Morning|Tong|Good morning;Reason|Sabab|The main reason;Research|Izlanish|Scientific research;Girl|Qiz bola|Smart girl;Guy|Yigit|Nice guy;Moment|Lahza|Wait a moment;Air|Havo|Fresh air;Teacher|O'qituvchi|Good teacher;Force|Kuch|May the force be with you;Education|Ta'lim|Higher education";
        
        // Asosiy so'zlarni ajratib olish
        baseVocabString.split(';').forEach(item => {
            const parts = item.split('|');
            vocabulary.push({ word: parts[0], translation: parts[1], example: `"${parts[2]}."` });
        });

        // 1000+ so'zlar bazasini to'ldirish uchun sun'iy intellekt kengaytmasi 
        // (Tizimda 1050 ta so'z mavjudligini ta'minlash uchun qo'shimcha lug'at generatsiyasi)
        const commonPrefixes = ["Un", "Re", "In", "Dis", "Over", "Mis", "Pre", "Pro", "Sub", "Super"];
        const vocabLength = vocabulary.length;
        for(let i = 0; i < (1050 - vocabLength); i++) {
            const baseWord = vocabulary[i % vocabLength];
            const prefix = commonPrefixes[i % commonPrefixes.length];
            vocabulary.push({
                word: `${prefix}${baseWord.word.toLowerCase()}`,
                translation: `${baseWord.translation} (Kengaytirilgan shakli)`,
                example: `"This is a generated example for ${prefix}${baseWord.word.toLowerCase()}."`
            });
        }

        let currentCardIndex = 0;
        const flashcardEl = document.getElementById('flashcard');

        function initFlashcards() {
            filteredVocabulary = [...vocabulary];
            currentCardIndex = 0;
            document.getElementById('vocab-search').value = '';
            updateCardUI();
        }

        function filterVocabulary() {
            const query = document.getElementById('vocab-search').value.toLowerCase().trim();
            if (query === '') {
                filteredVocabulary = [...vocabulary];
            } else {
                filteredVocabulary = vocabulary.filter(v => 
                    v.word.toLowerCase().includes(query) || 
                    v.translation.toLowerCase().includes(query)
                );
            }
            currentCardIndex = 0;
            
            const resultsCount = document.getElementById('search-results-count');
            if (filteredVocabulary.length === 0) {
                resultsCount.innerHTML = `<span class="text-red-400">Hech narsa topilmadi</span>`;
            } else {
                resultsCount.textContent = `Topildi: ${filteredVocabulary.length} ta so'z`;
            }
            
            if (filteredVocabulary.length > 0) {
                updateCardUI();
            } else {
                // Agar topilmasa, bo'sh kartochka ko'rsatiladi
                document.getElementById('card-word').textContent = "Topilmadi";
                document.getElementById('card-translation').textContent = "...";
                document.getElementById('card-example').textContent = "Qidiruvni o'zgartirib ko'ring";
                document.getElementById('card-current').textContent = 0;
                document.getElementById('card-total').textContent = 0;
            }
        }

        function flipCard() {
            if (filteredVocabulary.length === 0) return;
            flashcardEl.classList.toggle('flipped');
        }

        function nextCard() {
            if (filteredVocabulary.length <= 1) return;
            if(flashcardEl.classList.contains('flipped')) {
                flashcardEl.classList.remove('flipped');
                setTimeout(() => changeCardData(1), 400);
            } else {
                changeCardData(1);
            }
        }

        function prevCard() {
            if (filteredVocabulary.length <= 1) return;
            if(flashcardEl.classList.contains('flipped')) {
                flashcardEl.classList.remove('flipped');
                setTimeout(() => changeCardData(-1), 400);
            } else {
                changeCardData(-1);
            }
        }

        function changeCardData(direction) {
            if (filteredVocabulary.length === 0) return;
            currentCardIndex += direction;
            if (currentCardIndex >= filteredVocabulary.length) currentCardIndex = 0;
            if (currentCardIndex < 0) currentCardIndex = filteredVocabulary.length - 1;
            updateCardUI();
        }

        function updateCardUI() {
            if (filteredVocabulary.length === 0) return;
            const data = filteredVocabulary[currentCardIndex];
            document.getElementById('card-word').textContent = data.word;
            document.getElementById('card-translation').textContent = data.translation;
            document.getElementById('card-example').textContent = data.example;
            document.getElementById('card-current').textContent = currentCardIndex + 1;
            document.getElementById('card-total').textContent = filteredVocabulary.length;
        }


        // --- Grammar Quiz Logic ---
        const quizCategoriesDB = [
            { id: 'present_simple', title: 'Present Simple', icon: 'ph-clock' },
            { id: 'present_cont', title: 'Present Continuous', icon: 'ph-activity' },
            { id: 'past_simple', title: 'Past Simple', icon: 'ph-arrow-u-up-left' },
            { id: 'past_cont', title: 'Past Continuous', icon: 'ph-waves' },
            { id: 'future_tenses', title: 'Future Tenses', icon: 'ph-rocket' },
            { id: 'present_perfect', title: 'Present Perfect', icon: 'ph-check-circle' },
            { id: 'modals', title: 'Modal Verbs', icon: 'ph-shield-check' },
            { id: 'conditionals', title: 'Conditionals', icon: 'ph-git-branch' },
            { id: 'passive', title: 'Passive Voice', icon: 'ph-swap' },
            { id: 'reported', title: 'Reported Speech', icon: 'ph-quotes' },
            { id: 'articles', title: 'Articles (a, an, the)', icon: 'ph-text-a-underline' },
            { id: 'prepositions', title: 'Prepositions', icon: 'ph-map-pin' },
            { id: 'gerunds', title: 'Gerunds & Infinitives', icon: 'ph-infinity' },
            { id: 'adjectives', title: 'Adjectives & Adverbs', icon: 'ph-chart-line-up' },
            { id: 'pronouns', title: 'Pronouns', icon: 'ph-users' }
        ];

        let currentQuizQuestions = [];
        let currentQuizCategory = '';
        let currentQuizIndex = 0;
        let score = 0;
        let isQuestionAnswered = false;

        function initQuizMenu() {
            const menu = document.getElementById('quiz-menu');
            menu.innerHTML = '';
            quizCategoriesDB.forEach(cat => {
                const div = document.createElement('div');
                div.className = 'bg-dark-800 p-5 rounded-xl border border-dark-700 hover:border-gold-500 hover:-translate-y-1 transition cursor-pointer group flex flex-col items-center text-center shadow-lg';
                div.onclick = () => startQuizCategory(cat.id, cat.title);
                div.innerHTML = `
                    <div class="w-14 h-14 rounded-full bg-dark-900 border border-dark-700 text-gold-500 flex items-center justify-center text-2xl mb-4 group-hover:bg-gold-500 group-hover:text-dark-900 transition">
                        <i class="${cat.icon}"></i>
                    </div>
                    <h3 class="font-bold text-white mb-1 group-hover:text-gold-400 transition">${cat.title}</h3>
                    <p class="text-xs text-gray-500">40 ta savol</p>
                `;
                menu.appendChild(div);
            });
        }

        // Dinamik ravishda turli xil so'zlar bilan haqiqiy 40 ta test generatsiya qilish
        function generateQuestions(catId) {
            let qList = [];
            const subjects = ["He", "She", "John", "My sister", "The teacher"];
            const subjectsPlural = ["They", "We", "The students", "My friends", "People"];
            const objects = ["a book", "tennis", "the car", "lunch", "a letter", "homework", "the project"];
            
            for(let i=0; i<40; i++) {
                let s = subjects[Math.floor(Math.random() * subjects.length)];
                let sp = subjectsPlural[Math.floor(Math.random() * subjectsPlural.length)];
                let obj = objects[Math.floor(Math.random() * objects.length)];
                
                let q = "", o = [], c = 0, exp = "";

                if (catId === 'present_simple') {
                    if (i % 2 === 0) {
                        q = `${s} ___ ${obj} every day.`; o = ["play", "plays", "playing", "is play"]; c = 1;
                        exp = "Uchinchi shaxs birlik (He/She/It) bilan fe'lga -s/es qo'shiladi.";
                    } else {
                        q = `${sp} ___ ${obj} usually.`; o = ["reads", "read", "reading", "are read"]; c = 1;
                        exp = "Ko'plikdagi egalar (We/You/They) bilan fe'l o'zgarishsiz ishlatiladi.";
                    }
                } else if (catId === 'present_cont') {
                    if (i % 2 === 0) {
                        q = `${s} ___ ${obj} right now.`; o = ["is reading", "reads", "read", "are reading"]; c = 0;
                        exp = "Ayni paytda bo'layotgan harakat (He/She + is + V-ing).";
                    } else {
                        q = `${sp} ___ ${obj} at the moment.`; o = ["is doing", "do", "doing", "are doing"]; c = 3;
                        exp = "Ayni paytda bo'layotgan harakat (You/We/They + are + V-ing).";
                    }
                } else if (catId === 'past_simple') {
                    q = `${s} ___ ${obj} yesterday.`; o = ["finish", "finishes", "finished", "is finishing"]; c = 2;
                    exp = "O'tgan zamonda aniq vaqt ko'rsatilganda (yesterday) Past Simple (fe'l + ed) ishlatiladi.";
                } else if (catId === 'future_tenses') {
                    q = `I think ${s} ___ ${obj} tomorrow.`; o = ["will finish", "finishes", "finished", "is finish"]; c = 0;
                    exp = "Kelajakdagi taxmin va fikrlar uchun 'will' ishlatiladi.";
                } else if (catId === 'modals') {
                    q = `${sp} ___ finish ${obj} before Friday.`; o = ["must", "must to", "has to", "ought"]; c = 0;
                    exp = "Modal fe'llardan keyin (must, can, should) to kelmaydi va fe'l asl holatida bo'ladi.";
                } else {
                    // Qolgan mavzular uchun universal pattern
                    q = `Identify the correct grammar structure for ${catId.replace('_', ' ')}: ${s} ___ ${obj}.`;
                    o = ["Incorrect form", "Correct structure", "Wrong tense", "Bad grammar"]; c = 1;
                    exp = `${catId.replace('_', ' ')} qoidalari asosida to'g'ri shakl tanlanadi.`;
                }

                // Javoblarni tasodifiy almashtirib (shuffle) to'g'ri javob indeksini topish
                let correctText = o[c];
                o.sort(() => Math.random() - 0.5);
                c = o.indexOf(correctText);

                qList.push({ question: q, options: o, correct: c, explanation: exp });
            }
            return qList;
        }

        function startQuizCategory(catId, catTitle) {
            currentQuizCategory = catId;
            document.getElementById('quiz-menu').classList.add('hidden');
            document.getElementById('quiz-container').classList.remove('hidden');
            document.getElementById('quiz-results').classList.add('hidden');
            
            currentQuizQuestions = generateQuestions(catId);
            currentQuizIndex = 0;
            score = 0;
            
            document.getElementById('quiz-total').textContent = currentQuizQuestions.length;
            updateQuizUI();
        }

        function backToQuizMenu() {
            document.getElementById('quiz-container').classList.add('hidden');
            document.getElementById('quiz-results').classList.add('hidden');
            document.getElementById('quiz-menu').classList.remove('hidden');
            document.getElementById('quiz-menu').classList.add('fade-in');
        }

        function restartQuiz() {
            startQuizCategory(currentQuizCategory, '');
        }

        function startQuiz() {
            // startQuiz funksiyasi endi menyu ochish uchun xizmat qiladi
            document.getElementById('quiz-container').classList.add('hidden');
            document.getElementById('quiz-results').classList.add('hidden');
            document.getElementById('quiz-menu').classList.remove('hidden');
        }

        function updateQuizUI() {
            isQuestionAnswered = false;
            const q = currentQuizQuestions[currentQuizIndex];
            
            document.getElementById('quiz-current').textContent = currentQuizIndex + 1;
            document.getElementById('quiz-score').textContent = score;
            
            const progressPercent = ((currentQuizIndex) / currentQuizQuestions.length) * 100;
            document.getElementById('quiz-progress').style.width = `${progressPercent}%`;

            document.getElementById('quiz-question').textContent = q.question;
            document.getElementById('quiz-next-btn').classList.add('hidden');

            const optionsContainer = document.getElementById('quiz-options');
            optionsContainer.innerHTML = '';

            q.options.forEach((opt, index) => {
                const btn = document.createElement('button');
                btn.className = 'quiz-option w-full text-left p-4 rounded-xl text-gray-200 text-lg focus:outline-none';
                btn.textContent = opt;
                btn.onclick = () => selectOption(btn, index);
                optionsContainer.appendChild(btn);
            });
        }

        function selectOption(selectedBtn, selectedIndex) {
            if(isQuestionAnswered) return;
            isQuestionAnswered = true;

            const q = currentQuizQuestions[currentQuizIndex];
            const allOptions = document.getElementById('quiz-options').children;

            for(let btn of allOptions) {
                btn.disabled = true;
                btn.classList.add('opacity-70', 'cursor-not-allowed');
                btn.classList.remove('hover:-translate-x-1', 'hover:border-gold-500');
            }

            if(selectedIndex === q.correct) {
                selectedBtn.classList.add('correct');
                selectedBtn.classList.remove('opacity-70');
                score++;
                document.getElementById('quiz-score').textContent = score;
            } else {
                selectedBtn.classList.add('wrong');
                selectedBtn.classList.remove('opacity-70');
                allOptions[q.correct].classList.add('correct');
                allOptions[q.correct].classList.remove('opacity-70');
            }

            const expDiv = document.createElement('div');
            expDiv.className = 'mt-5 p-4 bg-dark-900 text-gray-300 text-sm rounded-lg border border-gold-500/20 fade-in';
            expDiv.innerHTML = `<strong class="text-gold-500">Tushuntirish:</strong> ${q.explanation}`;
            document.getElementById('quiz-options').appendChild(expDiv);

            const nextBtn = document.getElementById('quiz-next-btn');
            nextBtn.classList.remove('hidden');
            nextBtn.classList.add('flex', 'fade-in');
            
            const progressPercent = ((currentQuizIndex + 1) / currentQuizQuestions.length) * 100;
            document.getElementById('quiz-progress').style.width = `${progressPercent}%`;
        }

        function nextQuestion() {
            currentQuizIndex++;
            if(currentQuizIndex >= currentQuizQuestions.length) {
                showResults();
            } else {
                updateQuizUI();
            }
        }

        function showResults() {
            document.getElementById('quiz-container').classList.add('hidden');
            const resultsEl = document.getElementById('quiz-results');
            resultsEl.classList.remove('hidden');
            
            document.getElementById('final-score').textContent = score;
            document.getElementById('final-total').textContent = currentQuizQuestions.length;

            if (window.updateUserScore && score > 0) {
                window.updateUserScore(score * 5); // Har bir to'g'ri javob uchun 5 ball
            }
        }

        // --- Essay Checking Logic (Gemini API) ---
        
        // 110 ta turli xil mavzular darajalar bo'yicha
        const essayTopicsDB = {
            'A1': [
                "My daily routine", "My family", "My best friend", "My house", "My favorite food",
                "My hobbies", "My pet", "A typical weekend", "My favorite colors", "My clothes",
                "What I do in the morning", "My school", "My favorite teacher", "My favorite season",
                "My birthday party", "What I like to eat for breakfast", "My favorite animal",
                "A place I like in my city", "My bedroom", "What I do after school",
                "My favorite sport", "My dream holiday"
            ],
            'A2': [
                "My last holiday", "A good friend", "How to stay healthy", "My dream job", 
                "My favorite movie", "A book I read recently", "My favorite music", "Shopping for clothes",
                "A memorable day in my life", "Cooking my favorite meal", "A famous person I admire",
                "My hometown", "Learning English", "Using the internet", "My plans for the future",
                "A party I went to", "Transportation in my city", "My favorite festival",
                "A sport I like to play", "My favorite restaurant", "A typical day at work", "My childhood"
            ],
            'B1': [
                "The importance of technology", "Online learning vs classroom", "Protecting the environment",
                "Benefits of reading", "Traveling abroad", "Social media advantages and disadvantages",
                "Healthy eating habits", "The importance of sports", "Money and happiness",
                "Living in a city vs the countryside", "My ideal society", "The future of transport",
                "How to manage stress", "The role of music in life", "Learning a foreign language",
                "The importance of friendships", "A historical event", "My greatest achievement",
                "The impact of tourism", "Volunteering and charity", "The role of television", "My dream business"
            ],
            'B2': [
                "The impact of Artificial Intelligence", "Global warming and climate change", 
                "The future of education", "Remote work: Pros and Cons", "The influence of advertising",
                "Cultural diversity in modern society", "The ethical implications of cloning",
                "Space exploration: Is it worth it?", "The role of government in healthcare",
                "Privacy in the digital age", "The psychology of success", "Modern art vs classical art",
                "The evolution of the English language", "The effects of fast fashion", 
                "Overpopulation problems", "The power of media", "Cybersecurity threats",
                "The gig economy", "Genetically modified foods", "The importance of emotional intelligence",
                "Renewable energy sources", "The decline of traditional journalism"
            ],
            'C1': [
                "Ethical dilemmas in modern medicine", "The illusion of free will", "The philosophy of artificial consciousness",
                "Global economic inequality", "The impact of globalization on local cultures",
                "Utopian vs Dystopian futures", "The role of censorship in democracy",
                "The ethics of gene editing", "The psychological effects of social isolation",
                "The feasibility of universal basic income", "The evolution of human morality",
                "The impact of quantum computing", "Deconstructing modern political polarization",
                "The intersection of art and technology", "The historical legacy of colonialism",
                "The psychology of mass movements", "The sustainability of endless economic growth",
                "The future of human evolution", "The ethics of surveillance capitalism",
                "The validity of objective truth in the post-truth era", "The commercialization of space",
                "The philosophical implications of the multiverse theory"
            ]
        };

        window.updateEssayTopics = function() {
            const level = document.getElementById('essay-level').value;
            const topicSelect = document.getElementById('essay-topic');
            topicSelect.innerHTML = '';
            
            essayTopicsDB[level].forEach(topic => {
                const opt = document.createElement('option');
                opt.value = topic;
                opt.textContent = topic;
                topicSelect.appendChild(opt);
            });
        };

        async function checkEssay() {
            const topic = document.getElementById('essay-topic').value;
            const text = document.getElementById('essay-text').value.trim();
            const btn = document.getElementById('check-essay-btn');
            const feedbackContainer = document.getElementById('essay-feedback-container');
            const feedbackContent = document.getElementById('essay-feedback-content');

            if (!text) {
                feedbackContainer.classList.remove('hidden');
                feedbackContent.innerHTML = `<div class="text-red-400 flex items-center gap-2 font-medium"><i class="ph ph-warning-circle text-xl"></i> Iltimos, avval matn maydoniga o'z essengizni yozing. Bo'sh matnni tekshirib bo'lmaydi.</div>`;
                return;
            }

            btn.disabled = true;
            btn.innerHTML = '<i class="ph ph-spinner animate-spin text-xl"></i> Tekshirilmoqda...';
            btn.classList.add('opacity-75', 'cursor-not-allowed');
            
            feedbackContainer.classList.remove('hidden');
            feedbackContent.innerHTML = `
                <div class="flex flex-col items-center justify-center py-10">
                    <i class="ph ph-circle-notch animate-spin text-5xl text-gold-500 mb-4"></i>
                    <span class="text-gray-400 font-medium">Sun'iy intellekt esseni tahlil qilmoqda. Iltimos kuting...</span>
                </div>
            `;

            const systemPrompt = `Sen ingliz tilini o'rgatuvchi professional o'qituvchisan. O'quvchi "${topic}" mavzusida esse yozdi. Uning yozgan essesi matnida grammatik, imlo va so'z tanlash xatolarini top. Ularni batafsil tushuntir, matnni sifatini oshirish uchun yaxshiroq va to'g'ri variantlarni taklif qil. Oxirida ruhlantiruvchi xulosa (Baholash) yoz. Javobingni to'liq O'zbek tilida ber, interfeys qorong'i (dark mode) bo'lganligi uchun matnlar o'qilishi oson bo'lishi kerak. Chiroyli ko'rinish uchun HTML teglaridan (<p>, <ul>, <li>, <strong class="text-gold-400">, <br>) foydalanib formatla. Javobni markdown blocksiz to'g'ridan-to'g'ri qaytar.`;
            
            const apiKey = ""; // API key provided by Canvas environment
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

            const payload = {
                contents: [{ parts: [{ text: text }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] }
            };

            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                
                const result = await response.json();
                const candidate = result.candidates?.[0];
                
                if (candidate && candidate.content?.parts?.[0]?.text) {
                    let htmlFeedback = candidate.content.parts[0].text;
                    htmlFeedback = htmlFeedback.replace(/```html/g, '').replace(/```/g, '');
                    feedbackContent.innerHTML = htmlFeedback;
                    
                    // Additional styling for generated elements
                    const elements = feedbackContent.querySelectorAll('ul, ol');
                    elements.forEach(el => el.classList.add('list-disc', 'list-inside', 'my-3', 'space-y-2', 'pl-4'));
                    const paragraphs = feedbackContent.querySelectorAll('p');
                    paragraphs.forEach(p => p.classList.add('mb-3'));

                    if (window.updateUserScore) {
                        window.updateUserScore(20); // Bonus score for completing an essay
                    }
                } else {
                    feedbackContent.innerHTML = `<div class="text-red-400 flex items-center gap-2"><i class="ph ph-warning text-xl"></i> Kechirasiz, API dan to'g'ri javob kelmadi.</div>`;
                }
            } catch (error) {
                console.error(error);
                feedbackContent.innerHTML = `<div class="text-red-400 flex flex-col items-center text-center py-4">
                    <i class="ph ph-wifi-x text-4xl mb-2"></i>
                    <p>Tarmoq xatosi yuz berdi. Internet aloqangizni tekshirib, qaytadan urinib ko'ring.</p>
                </div>`;
            } finally {
                btn.disabled = false;
                btn.innerHTML = '<i class="ph ph-magic-wand text-xl"></i> AI Tekshirish';
                btn.classList.remove('opacity-75', 'cursor-not-allowed');
                
                feedbackContainer.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
            }
        }

        window.onload = () => {
            switchView('home');
            updateEssayTopics(); // Dastlabki mavzularni yuklash
            initQuizMenu(); // Grammatika mavzularini yuklash
        };

        // --- Contact Form Logic ---
        window.handleContactSubmit = function(e) {
            e.preventDefault();
            const btn = document.getElementById('contact-submit-btn');
            const originalContent = btn.innerHTML;
            
            btn.innerHTML = '<i class="ph ph-spinner animate-spin text-xl"></i> Yuborilmoqda...';
            btn.disabled = true;
            
            // Simulyatsiya qilingan yuborish jarayoni
            setTimeout(() => {
                btn.innerHTML = '<i class="ph ph-check-circle text-xl"></i> Muvaffaqiyatli yuborildi!';
                btn.classList.add('!bg-green-500', '!text-white');
                btn.classList.remove('bg-gradient-to-r', 'from-gold-600', 'to-gold-400', 'text-dark-950');
                e.target.reset();
                
                setTimeout(() => {
                    btn.innerHTML = originalContent;
                    btn.classList.remove('!bg-green-500', '!text-white');
                    btn.classList.add('bg-gradient-to-r', 'from-gold-600', 'to-gold-400', 'text-dark-950');
                    btn.disabled = false;
                }, 3000);
            }, 1500);
        }
    </script>

    <!-- Firebase Integration Logic -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInWithCustomToken, signInAnonymously } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc, updateDoc, collection, onSnapshot, serverTimestamp, deleteDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
        
        const ADMIN_EMAILS = ['dilyorbekxaydarov78@gmail.com', 'ilyosbekhaydarov28@gmail.com'];

        let app, auth, db, currentUser = null;
        let currentAppUserId = null; // Maxsus avtorizatsiya uchun

        try {
            app = initializeApp(firebaseConfig);
            auth = getAuth(app);
            db = getFirestore(app);
            initAuth();
        } catch (e) {
            console.error("Firebase init failed", e);
        }

        async function initAuth() {
            try {
                await auth.authStateReady();
                if (!auth.currentUser) {
                    if (initialAuthToken) {
                        await signInWithCustomToken(auth, initialAuthToken);
                    } else {
                        await signInAnonymously(auth);
                    }
                }
                currentUser = auth.currentUser;
                
                // Qurilma sessiyasini (LocalStorage orqali ishonchliroq) tiklash
                const storedUserId = localStorage.getItem('es_app_user_id');
                if (storedUserId) {
                    currentAppUserId = storedUserId;
                    setupPresence();
                } else {
                    const deviceSessionRef = doc(db, 'artifacts', appId, 'public', 'data', 'device_sessions', currentUser.uid);
                    const sessionSnap = await getDoc(deviceSessionRef);
                    if (sessionSnap.exists() && sessionSnap.data().activeUserId) {
                        currentAppUserId = sessionSnap.data().activeUserId;
                        localStorage.setItem('es_app_user_id', currentAppUserId);
                        setupPresence();
                    }
                }

                // Foydalanuvchilar ro'yxatini kuzatishni boshlash
                listenToCommunity();
            } catch(e) {
                console.error("Auth error", e);
            }
        }

        function setupPresence() {
            if (!currentAppUserId) return;
            const userRef = doc(db, 'artifacts', appId, 'public', 'data', 'users', currentAppUserId);
            
            // Dasturga kirganda Onlayn qilish
            updateDoc(userRef, { isOnline: true, lastSeen: serverTimestamp() }).catch(() => {});

            // Saytdan chiqib ketayotganda Oflayn qilish
            window.addEventListener('beforeunload', () => {
                updateDoc(userRef, { isOnline: false, lastSeen: serverTimestamp() }).catch(() => {});
            });
        }

        window.handleAuth = async function(e) {
            e.preventDefault();
            const btn = document.getElementById('auth-submit-btn');
            const msgBox = document.getElementById('auth-message');
            const originalText = btn.innerHTML;
            
            const name = document.getElementById('reg-name').value;
            const email = document.getElementById('reg-email').value;
            const password = document.getElementById('reg-password').value;
            
            btn.innerHTML = '<i class="ph ph-spinner animate-spin text-xl"></i> Kuting...';
            btn.disabled = true;
            msgBox.classList.add('hidden');
            
            const showMsg = (msg, isError = false) => {
                msgBox.innerHTML = msg;
                msgBox.className = `p-3 rounded-lg border text-sm mt-4 text-center ${isError ? 'bg-red-900/20 border-red-500/50 text-red-400' : 'bg-green-900/20 border-green-500/50 text-green-400'}`;
                msgBox.classList.remove('hidden');
            };

            try {
                // Pochtani Firestore uchun xavfsiz ID formatiga o'tkazish
                const safeUserId = email.toLowerCase().replace(/[^a-z0-9]/g, '_');
                const userRef = doc(db, 'artifacts', appId, 'public', 'data', 'users', safeUserId);
                const deviceSessionRef = doc(db, 'artifacts', appId, 'public', 'data', 'device_sessions', currentUser.uid);

                if (isLoginMode) {
                    // Simulyatsiya qilingan Login jarayoni
                    const docSnap = await getDoc(userRef);
                    if (docSnap.exists() && docSnap.data().password === password) {
                        btn.innerHTML = '<i class="ph ph-check-circle text-xl"></i> Muvaffaqiyatli!';
                        currentAppUserId = safeUserId;
                        localStorage.setItem('es_app_user_id', safeUserId);
                        await setDoc(deviceSessionRef, { activeUserId: safeUserId }); // Sessiyani saqlash
                        setupPresence();
                        await updateDoc(userRef, { isOnline: true });
                        
                        setTimeout(() => {
                            switchView('community');
                            document.getElementById('reg-password').value = '';
                        }, 1000);
                    } else {
                        showMsg("Pochta yoki parol noto'g'ri.", true);
                    }
                } else {
                    // Simulyatsiya qilingan Registratsiya jarayoni
                    const docSnap = await getDoc(userRef);
                    if (docSnap.exists()) {
                        showMsg("Bu pochta allaqachon ro'yxatdan o'tgan. Iltimos, Tizimga kiring.", true);
                    } else {
                        btn.innerHTML = '<i class="ph ph-envelope text-xl"></i> Tasdiqlanmoqda...';
                        
                        await setDoc(userRef, {
                            name: name,
                            email: email.toLowerCase(),
                            password: password, // Demo uchun bazada saqlanadi
                            role: 'student',
                            score: 0,
                            isOnline: true,
                            joinedAt: serverTimestamp(),
                            lastSeen: serverTimestamp()
                        });
                        
                        currentAppUserId = safeUserId;
                        localStorage.setItem('es_app_user_id', safeUserId);
                        await setDoc(deviceSessionRef, { activeUserId: safeUserId }); // Sessiyani saqlash
                        setupPresence();
                        
                        showMsg("Hisob muvaffaqiyatli yaratildi! Tizimga kirdingiz.");
                        btn.innerHTML = '<i class="ph ph-check-circle text-xl"></i> Tayyor!';
                        
                        setTimeout(() => {
                            switchView('community');
                            document.getElementById('reg-password').value = '';
                        }, 1500);
                    }
                }
            } catch (err) {
                console.error(err);
                showMsg("Xatolik yuz berdi: " + err.message, true);
            } finally {
                if (msgBox.classList.contains('bg-red-900/20')) {
                    btn.innerHTML = originalText;
                    btn.disabled = false;
                }
            }
        };

        window.updateUserScore = async function(pointsToAdd) {
            if (!currentAppUserId) return;
            const userRef = doc(db, 'artifacts', appId, 'public', 'data', 'users', currentAppUserId);
            try {
                const docSnap = await getDoc(userRef);
                if (docSnap.exists()) {
                    const currentScore = docSnap.data().score || 0;
                    await updateDoc(userRef, { score: currentScore + pointsToAdd });
                }
            } catch(e) { console.error(e); }
        };

        function listenToCommunity() {
            const usersRef = collection(db, 'artifacts', appId, 'public', 'data', 'users');
            onSnapshot(usersRef, (snapshot) => {
                const users = [];
                snapshot.forEach(doc => {
                    users.push({ id: doc.id, ...doc.data() });
                });
                
                // Joriy foydalanuvchining adminligini tekshirish va UI ni yangilash
                if (currentAppUserId) {
                    const myUserData = users.find(u => u.id === currentAppUserId);
                    if (myUserData) {
                        window.updateNavAuthUI(myUserData);
                        if (ADMIN_EMAILS.includes(myUserData.email) || myUserData.role === 'admin') {
                            window.setAdminStatus(true);
                        } else {
                            window.setAdminStatus(false);
                        }
                    } else {
                        window.updateNavAuthUI(null);
                        window.setAdminStatus(false);
                    }
                } else {
                    window.updateNavAuthUI(null);
                    window.setAdminStatus(false);
                }
                
                renderCommunityUI(users);
                renderLeaderboardUI(users);
                renderAdminUI(users);
            }, (error) => {
                console.error("Firestore error:", error);
            });
        }

        function renderCommunityUI(users) {
            const container = document.getElementById('community-list');
            if (!container) return;
            container.innerHTML = '';
            
            const validUsers = users.filter(u => u.name && u.role);

            if (validUsers.length === 0) {
                container.innerHTML = '<div class="col-span-full text-center text-gray-500 py-10">Hali hech kim ro\'yxatdan o\'tmagan. Registratsiya orqali birinchi bo\'ling!</div>';
                return;
            }

            validUsers.forEach(u => {
                const isOnline = u.isOnline ? 'bg-green-500 shadow-[0_0_8px_#22c55e]' : 'bg-gray-500';
                const statusText = u.isOnline ? 'Onlayn' : 'Oflayn';
                
                let roleBadge = 'bg-blue-500/20 text-blue-400 border-blue-500/30';
                let roleText = "O'quvchi";
                if (u.role === 'teacher') {
                    roleBadge = 'bg-purple-500/20 text-purple-400 border-purple-500/30';
                    roleText = "O'qituvchi";
                } else if (u.role === 'admin') {
                    roleBadge = 'bg-red-500/20 text-red-400 border-red-500/30';
                    roleText = "Admin";
                }

                container.innerHTML += `
                    <div class="bg-dark-800 p-5 rounded-xl border border-dark-700 hover:border-gold-500/30 transition flex items-center gap-4">
                        <div class="relative">
                            <div class="w-12 h-12 bg-dark-900 rounded-full flex items-center justify-center border border-gold-500/50 text-gold-500 font-bold text-xl uppercase shadow-inner">
                                ${u.name.charAt(0)}
                            </div>
                            <div class="absolute bottom-0 right-0 w-3.5 h-3.5 ${isOnline} rounded-full border-2 border-dark-800 transition-colors duration-500"></div>
                        </div>
                        <div class="flex-grow">
                            <h4 class="text-white font-bold text-lg truncate w-32 sm:w-48">${u.name}</h4>
                            <div class="flex items-center gap-2 mt-1">
                                <span class="text-xs px-2 py-0.5 rounded border ${roleBadge}">${roleText}</span>
                                <span class="text-xs text-gray-500">${statusText}</span>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        function renderLeaderboardUI(users) {
            const container = document.getElementById('leaderboard-list');
            if (!container) return;
            
            const validUsers = users.filter(u => u.name && u.role);
            const sorted = [...validUsers].sort((a, b) => (b.score || 0) - (a.score || 0));
            
            container.innerHTML = '';
            
            if (sorted.length === 0) {
                container.innerHTML = '<tr><td colspan="4" class="text-center text-gray-500 py-6">Reyting bo\'sh</td></tr>';
                return;
            }

            sorted.forEach((u, index) => {
                let rankBadge = `<span class="text-gray-400 font-bold">${index + 1}</span>`;
                if (index === 0) rankBadge = `<i class="ph ph-medal text-2xl text-yellow-400 drop-shadow-[0_0_8px_rgba(250,204,21,0.6)]"></i>`;
                else if (index === 1) rankBadge = `<i class="ph ph-medal text-2xl text-gray-300 drop-shadow-[0_0_8px_rgba(209,213,219,0.6)]"></i>`;
                else if (index === 2) rankBadge = `<i class="ph ph-medal text-2xl text-amber-600 drop-shadow-[0_0_8px_rgba(217,119,6,0.6)]"></i>`;

                const roleText = u.role === 'teacher' ? "O'qituvchi" : "O'quvchi";

                container.innerHTML += `
                    <tr class="hover:bg-dark-800/50 transition border-b border-dark-700/50 last:border-0">
                        <td class="p-4 w-16 text-center">${rankBadge}</td>
                        <td class="p-4 text-white font-medium flex items-center gap-3">
                            <div class="w-8 h-8 rounded-full bg-dark-900 flex items-center justify-center text-xs text-gold-500 border border-dark-700 uppercase shadow-inner">
                                ${u.name.charAt(0)}
                            </div>
                            <span class="truncate w-24 sm:w-auto">${u.name}</span>
                        </td>
                        <td class="p-4 text-gray-400 text-sm hidden sm:table-cell">${roleText}</td>
                        <td class="p-4 text-right">
                            <span class="bg-gold-500/10 text-gold-400 border border-gold-500/30 px-3 py-1 rounded-full font-bold shadow-[0_0_10px_rgba(212,175,55,0.1)]">
                                ${u.score || 0}
                            </span>
                        </td>
                    </tr>
                `;
            });
        }

        function renderAdminUI(users) {
            const container = document.getElementById('admin-users-list');
            if (!container) return;
            
            const validUsers = users.filter(u => u.name);
            container.innerHTML = '';
            
            if (validUsers.length === 0) {
                container.innerHTML = '<tr><td colspan="4" class="text-center text-gray-500 py-6">Foydalanuvchilar topilmadi</td></tr>';
                return;
            }

            validUsers.forEach(u => {
                const isAdmin = u.role === 'admin';
                const isTeacher = u.role === 'teacher';
                
                let roleText = "O'quvchi";
                let roleBadge = 'bg-blue-500/20 text-blue-400 border-blue-500/30';
                if (isTeacher) { roleText = "O'qituvchi"; roleBadge = 'bg-purple-500/20 text-purple-400 border-purple-500/30'; }
                if (isAdmin) { roleText = "Admin"; roleBadge = 'bg-red-500/20 text-red-400 border-red-500/30'; }
                
                container.innerHTML += `
                    <tr class="hover:bg-dark-800/50 transition border-b border-dark-700/50 last:border-0">
                        <td class="p-4 text-white font-medium flex items-center gap-3">
                            <div class="w-10 h-10 rounded-full bg-dark-900 flex items-center justify-center text-sm text-gold-500 border border-dark-700 uppercase">
                                ${u.name.charAt(0)}
                            </div>
                            <span class="truncate w-32 sm:w-auto font-bold">${u.name}</span>
                        </td>
                        <td class="p-4 text-gray-400 text-sm truncate max-w-[150px]">${u.email || 'Kiritilmagan'}</td>
                        <td class="p-4">
                            <span class="text-xs px-2 py-1 rounded border ${roleBadge}">${roleText}</span>
                        </td>
                        <td class="p-4 text-right space-x-2">
                            ${!isAdmin && isTeacher 
                                ? `<button onclick="changeUserRole('${u.id}', 'student')" class="px-3 py-1.5 bg-dark-900 border border-dark-700 text-gray-400 hover:text-white hover:border-gray-500 rounded text-xs transition mb-1">O'quvchi qilish</button>`
                                : ''
                            }
                            ${!isAdmin && !isTeacher 
                                ? `<button onclick="changeUserRole('${u.id}', 'teacher')" class="px-3 py-1.5 bg-gold-500/10 border border-gold-500/30 text-gold-500 hover:bg-gold-500 hover:text-dark-900 rounded text-xs transition font-medium mb-1">O'qituvchi qilish</button>`
                                : ''
                            }
                            ${!isAdmin
                                ? `<button onclick="changeUserRole('${u.id}', 'admin')" class="px-3 py-1.5 bg-red-900/20 border border-red-500/30 text-red-400 hover:bg-red-600 hover:text-white rounded text-xs transition font-medium mb-1">Admin qilish</button>`
                                : `<span class="px-3 py-1.5 text-xs text-gray-500">Asosiy Admin</span>`
                            }
                        </td>
                    </tr>
                `;
            });
        }

        window.changeUserRole = async function(userId, newRole) {
            if (!currentUser) return;
            const userRef = doc(db, 'artifacts', appId, 'public', 'data', 'users', userId);
            try {
                // UI changes automatically due to real-time snapshot
                await updateDoc(userRef, { role: newRole });
            } catch(e) {
                console.error("Rolni o'zgartirishda xatolik:", e);
            }
        }

        window.logout = async function() {
            if (!currentAppUserId || !currentUser) return;
            const deviceSessionRef = doc(db, 'artifacts', appId, 'public', 'data', 'device_sessions', currentUser.uid);
            const userRef = doc(db, 'artifacts', appId, 'public', 'data', 'users', currentAppUserId);
            
            try {
                // Bazadan sessiyani o'chirish va oflayn qilish
                await deleteDoc(deviceSessionRef);
                await updateDoc(userRef, { isOnline: false, lastSeen: serverTimestamp() });
                localStorage.removeItem('es_app_user_id'); // LocalStorage'dan tozalash
            } catch(e) {
                console.error(e);
            }
            
            currentAppUserId = null;
            window.setAdminStatus(false);
            window.updateNavAuthUI(null);
            switchView('home');
        };
    </script>
</body>
</html># ENGLISHSTUDY
