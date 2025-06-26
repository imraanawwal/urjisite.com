<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>urji accademy school (UAS)</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <!-- Font Awesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            overflow-x: hidden; /* Prevent horizontal scrolling */
            scroll-behavior: smooth; /* Smooth scrolling for anchor links */
        }
        .hero-background {
            background-image: url('https://placehold.co/1920x1080/4F46E5/FFFFFF?text=Modern+Education+Campus'); /* Updated education-themed background */
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            position: relative;
        }

        /* Hero text animations */
        .text-reveal-container {
            overflow: hidden;
            display: inline-block; /* Essential for containing the animation */
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(100%);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .animated-heading span {
            display: block;
            opacity: 0;
            animation: slideInUp 1s ease-out forwards;
        }
        .animated-heading span:nth-child(2) { animation-delay: 0.3s; }
        .animated-heading span:nth-child(3) { animation-delay: 0.6s; }
        .animated-subheading { animation: fadeIn 1.5s ease-out forwards; animation-delay: 1s; opacity: 0; }
        .animated-cta { animation: fadeIn 1.5s ease-out forwards; animation-delay: 1.5s; opacity: 0; }


        /* Scroll reveal animations */
        .scroll-reveal {
            opacity: 0;
            transform: translateY(50px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        .scroll-reveal.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* Message box styling */
        .message-box {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            z-index: 1000;
            display: none;
            text-align: center;
        }
        .message-box button {
            background-color: #3b82f6;
            color: white;
            padding: 8px 15px;
            border-radius: 5px;
            margin-top: 15px;
            cursor: pointer;
            border: none;
            transition: background-color 0.2s;
        }
        .message-box button:hover {
            background-color: #2563eb;
        }
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 999;
            display: none;
        }

        /* Hide scrollbar for comments/student lists but allow scrolling */
        .scrollable-content {
            -ms-overflow-style: none;  /* IE and Edge */
            scrollbar-width: none;  /* Firefox */
        }
        .scrollable-content::-webkit-scrollbar {
            display: none; /* Chrome, Safari, Opera */
        }

        /* Button hover animation */
        .animated-button {
            transition: transform 0.2s ease, box-shadow 0.2s ease, background-color 0.3s;
        }
        .animated-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }
        .animated-button:active {
            transform: translateY(0);
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }

        /* Carousel specific styles (for testimonial) */
        .testimonial-item {
            display: none;
            opacity: 0;
            transition: opacity 0.5s ease-in-out;
        }
        .testimonial-item.active {
            display: block;
            opacity: 1;
        }

        /* FAQ Accordion styles */
        .accordion-header {
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .accordion-header:hover {
            background-color: #e0e7ff; /* Light blue-50 hover */
        }
        .accordion-content {
            display: none;
            overflow: hidden;
            max-height: 0; /* Important for CSS transition */
            transition: max-height 0.3s ease-out;
        }
        .accordion-content.open {
            max-height: 500px; /* Adjust based on expected content height */
        }

        /* Back to Top button */
        #backToTopBtn {
            display: none; /* Hidden by default */
            position: fixed; /* Fixed/sticky position */
            bottom: 20px; /* Place the button at the bottom of the page */
            right: 30px; /* Place the button 30px from the right */
            z-index: 99; /* Make sure it does not overlap */
            border: none; /* Remove borders */
            outline: none; /* Remove outline */
            background-color: #3b82f6; /* Set a background color */
            color: white; /* Text color */
            cursor: pointer; /* Add a mouse pointer on hover */
            padding: 10px 15px; /* Some padding */
            border-radius: 10px; /* Rounded corners */
            font-size: 18px; /* Increase font size */
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            transition: background-color 0.3s, opacity 0.5s;
            opacity: 0; /* Start hidden for fade-in */
        }

        #backToTopBtn.show {
            opacity: 1;
        }

        #backToTopBtn:hover {
            background-color: #2563eb;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <!-- Message Box and Overlay -->
    <div id="messageBox" class="message-box">
        <p id="messageText"></p>
        <button onclick="hideMessageBox()">OK</button>
    </div>
    <div id="overlay" class="overlay"></div>

    <!-- Header / Navigation -->
    <header class="bg-white shadow-md p-4 sticky top-0 z-50">
        <nav class="container mx-auto flex justify-between items-center">
            <h1 class="text-2xl font-bold text-blue-700">urji accademy</h1>
            <ul class="hidden md:flex items-center space-x-6">
                <li><a href="#home" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Home</a></li>
                <li><a href="#info" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">About</a></li>
                <li><a href="#programs" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Programs</a></li>
                <li><a href="#why-us" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Why Us?</a></li>
                <li><a href="#faculty" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Faculty</a></li>
                <li><a href="#admissions" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Admissions</a></li>
                <li><a href="#events" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Events</a></li>
                <li><a href="#gallery" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Gallery</a></li>
                <li><a href="#testimonials" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Testimonials</a></li>
                <li><a href="#stats" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Stats</a></li>
                <li><a href="#faq" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">FAQ</a></li>
                <li><a href="#comments" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Comments</a></li>
                <li><a href="#registration" class="text-blue-600 hover:text-blue-800 font-medium transition-all duration-200">Register</a></li>
                <!-- Telegram Icon in Header -->
                <li>
                    <a href="https://t.me/+Lp3nk_k81WQ2MjA0" target="_blank" class="text-blue-600 hover:text-blue-800 transition-colors duration-200" title="Join our Telegram Group">
                        <i class="fab fa-telegram-plane text-2xl ml-2"></i>
                    </a>
                </li>
            </ul>
            <!-- Mobile Menu Button -->
            <button id="mobile-menu-button" class="md:hidden text-blue-600 text-2xl focus:outline-none">
                <i class="fas fa-bars"></i>
            </button>
        </nav>
    </header>

    <!-- Mobile Menu (Hidden by default) -->
    <div id="mobile-menu" class="hidden md:hidden bg-white shadow-lg py-4 z-40 fixed w-full top-[68px]"> <!-- Adjusted top to be below header -->
        <ul class="flex flex-col items-center space-y-4">
            <li><a href="#home" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Home</a></li>
            <li><a href="#info" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">About</a></li>
            <li><a href="#programs" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Programs</a></li>
            <li><a href="#why-us" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Why Us?</a></li>
            <li><a href="#faculty" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Faculty</a></li>
            <li><a href="#admissions" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Admissions</a></li>
            <li><a href="#events" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Events</a></li>
            <li><a href="#gallery" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Gallery</a></li>
            <li><a href="#testimonials" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Testimonials</a></li>
            <li><a href="#stats" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Stats</a></li>
            <li><a href="#faq" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">FAQ</a></li>
            <li><a href="#comments" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Comments</a></li>
            <li><a href="#registration" class="text-blue-600 hover:text-blue-800 font-medium block w-full text-center py-2 transition-all duration-200" onclick="hideMobileMenu()">Register</a></li>
            <li>
                <a href="https://t.me/+Lp3nk_k81WQ2MjA0" target="_blank" class="text-blue-600 hover:text-blue-800 transition-colors duration-200 flex items-center justify-center mt-2" title="Join our Telegram Group">
                    <i class="fab fa-telegram-plane text-2xl mr-2"></i> Telegram Group
                </a>
            </li>
        </ul>
    </div>

    <!-- Welcome Section / Home Page -->
    <section id="home" class="relative h-screen flex items-center justify-center text-center overflow-hidden hero-background">
        <div class="absolute inset-0 bg-blue-900 opacity-70"></div> <!-- Darker blue overlay -->

        <div class="relative z-10 p-8 rounded-xl max-w-5xl mx-auto shadow-2xl bg-gradient-to-br from-blue-700 to-blue-900 bg-opacity-80 backdrop-filter backdrop-blur-sm">
            <h2 class="text-5xl md:text-7xl font-extrabold text-white mb-4 animated-heading">
                <span class="text-reveal-container">Welcome to</span>
                <span class="text-reveal-container">urji accademy</span>
            </h2>
            <p class="mt-4 text-2xl md:text-3xl font-semibold text-blue-200 animated-subheading">
                urji accademy school (UAS)
            </p>
            <p class="mt-6 text-xl text-white animated-subheading">
                Empowering Minds, Shaping Futures: Dedicated to academic excellence and holistic development in Adama, Oromia, Ethiopia.
            </p>
            <a href="#admissions" class="mt-8 inline-block bg-yellow-400 text-blue-900 px-10 py-4 rounded-full shadow-lg text-lg font-bold hover:bg-yellow-300 transition-colors duration-300 animated-button animated-cta">
                Discover Our Programs
            </a>
        </div>
    </section>

    <!-- Information Section (About Us) -->
    <section id="info" class="py-16 md:py-24 bg-gradient-to-r from-blue-100 to-indigo-100 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-blue-700 mb-12">About urji accademy</h2>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
                <!-- Purpose -->
                <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal">
                    <i class="fas fa-bullseye text-5xl text-blue-500 mb-4"></i>
                    <h3 class="text-2xl font-semibold text-blue-800 mb-4">Our Purpose</h3>
                    <p class="text-gray-700 leading-relaxed">
                        To provide an exceptional learning environment that fosters critical thinking, creativity, and a lifelong passion for knowledge, preparing students to be future leaders and responsible citizens.
                    </p>
                </div>

                <!-- Vision -->
                <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.2s;">
                    <i class="fas fa-eye text-5xl text-indigo-500 mb-4"></i>
                    <h3 class="text-2xl font-semibold text-indigo-800 mb-4">Our Vision</h3>
                    <p class="text-gray-700 leading-relaxed">
                        To be a beacon of educational excellence, inspiring students to achieve their full potential and contribute positively to a rapidly changing world, embracing diversity and innovation.
                    </p>
                </div>

                <!-- Contact Info -->
                <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.4s;">
                    <i class="fas fa-address-book text-5xl text-green-500 mb-4"></i>
                    <h3 class="text-2xl font-semibold text-green-800 mb-4">Contact & Location</h3>
                    <p class="text-gray-700 mb-2"><i class="fas fa-phone mr-2 text-green-600"></i> Phone: +251707733696</p>
                    <p class="text-gray-700 mb-2"><i class="fas fa-map-marker-alt mr-2 text-green-600"></i> Location: Asella, Oromia, Ethiopia</p>
                    <p class="text-gray-700"><i class="fas fa-envelope mr-2 text-green-600"></i> Email: info@urjiaccademy.edu</p>
                </div>
            </div>

            <!-- Telegram Call to Action in Body -->
            <div class="mt-16 bg-white p-8 rounded-xl shadow-lg max-w-2xl mx-auto transform hover:scale-105 transition-transform duration-300 scroll-reveal">
                <h3 class="text-2xl font-semibold text-blue-800 mb-4">Connect With Us!</h3>
                <p class="text-gray-700 mb-4">Join our vibrant community on Telegram for instant updates, announcements, and direct engagement with the urji accademy family:</p>
                <a href="https://t.me/+Lp3nk_k81WQ2MjA0" target="_blank" class="inline-flex items-center px-6 py-3 bg-blue-500 text-white font-bold rounded-full shadow-lg hover:bg-blue-600 transition-colors duration-300 animated-button">
                    <!-- Telegram Logo SVG -->
                    <svg class="w-6 h-6 mr-3" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path d="M18.3 5.3c-.4-.4-1.1-.5-1.5-.1L3.9 10.9c-.6.3-.9.9-.9 1.5s.3 1.2.9 1.5l12.9 5.7c.4.2.8.2 1.2 0 .4-.2.6-.6.6-1V6c0-.4-.2-.8-.6-1zm-1.8 11.2L6.8 12l9.7-4.5v9z"/>
                    </svg>
                    urji accademy Telegram Group
                </a>
            </div>
        </div>
    </section>

    <!-- Our Programs Section -->
    <section id="programs" class="py-16 md:py-24 bg-gradient-to-r from-green-50 to-teal-50 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-green-700 mb-12">Our Academic Programs</h2>
            <p class="text-lg text-gray-700 mb-10 max-w-3xl mx-auto">We offer a diverse range of programs designed to nurture every student's potential from early childhood to preparation for higher education.</p>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
                <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal">
                    <i class="fas fa-child text-5xl text-green-500 mb-4"></i>
                    <h3 class="text-2xl font-semibold text-green-800 mb-4">Pre-Kindergarten</h3>
                    <p class="text-gray-700 leading-relaxed">
                        A foundational program focusing on early childhood development, playful learning, and social skills for our youngest learners.
                    </p>
                </div>
                <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.2s;">
                    <i class="fas fa-school text-5xl text-teal-500 mb-4"></i>
                    <h3 class="text-2xl font-semibold text-teal-800 mb-4">Primary Education (Grades KG1-KG3)</h3>
                    <p class="text-gray-700 leading-relaxed">
                        Comprehensive curriculum emphasizing core subjects, critical thinking, and a holistic approach to student growth.
                    </p>
                </div>
                <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.4s;">
                    <i class="fas fa-graduation-cap text-5xl text-blue-500 mb-4"></i>
                    <h3 class="text-2xl font-semibold text-blue-800 mb-4">Secondary Education (Grades 1-8)</h3>
                    <p class="text-gray-700 leading-relaxed">
                        Advanced academic programs, specialized electives, and college preparatory courses to equip students for future success.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- Why Choose Us Section -->
    <section id="why-us" class="py-16 md:py-24 bg-gradient-to-l from-purple-50 to-pink-50 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-purple-700 mb-12">Why Choose urji accademy?</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal">
                    <i class="fas fa-chalkboard-teacher text-4xl text-purple-600 mb-3"></i>
                    <h3 class="text-xl font-semibold text-purple-800 mb-2">Experienced Faculty</h3>
                    <p class="text-gray-700 text-sm">Dedicated and highly qualified teachers committed to student success.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.1s;">
                    <i class="fas fa-flask text-4xl text-pink-600 mb-3"></i>
                    <h3 class="text-xl font-semibold text-pink-800 mb-2">Modern Facilities</h3>
                    <p class="text-gray-700 text-sm">State-of-the-art labs, library, and sports amenities for holistic development.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.2s;">
                    <i class="fas fa-handshake text-4xl text-indigo-600 mb-3"></i>
                    <h3 class="text-xl font-semibold text-indigo-800 mb-2">Supportive Community</h3>
                    <p class="text-gray-700 text-sm">A nurturing environment that promotes collaboration and mutual respect.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.3s;">
                    <i class="fas fa-lightbulb text-4xl text-yellow-600 mb-3"></i>
                    <h3 class="text-xl font-semibold text-yellow-800 mb-2">Innovative Learning</h3>
                    <p class="text-gray-700 text-sm">Integrating modern teaching methods and technology for effective learning.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Our Faculty Section -->
    <section id="faculty" class="py-16 md:py-24 bg-gradient-to-r from-indigo-50 to-blue-50 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-indigo-700 mb-12">we have</h2>
            <p class="text-lg text-gray-700 mb-10 max-w-3xl mx-auto">these</p>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                <!-- Faculty Member 1 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden transform hover:scale-105 transition-transform duration-300 scroll-reveal">
                    <img src="https://placehold.co/400x400/93C5FD/000000?text=tutorial on class" alt="tutorial on class" class="w-full h-56 object-cover object-top">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-indigo-800"></h3>
                        <p class="text-blue-600">Principal</p>
                        <p class="text-gray-600 text-sm mt-2">With over 20 years of experience, Prof. Tesfaye leads our academic vision.</p>
                    </div>
                </div>
                <!-- Faculty Member 2 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden transform hover:scale-105 transition-transform duration-300 scroll-reveal" style="animation-delay: 0.1s;">
                    <img src="https://placehold.co/400x400/BFDBFE/000000?text=it lab" alt="it lab" class="w-full h-56 object-cover object-top">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-indigo-800"></h3>
                        <p class="text-blue-600">Head of Primary</p>
                        <p class="text-gray-600 text-sm mt-2">A passionate educator specializing in early childhood development.</p>
                    </div>
                </div>
                <!-- Faculty Member 3 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden transform hover:scale-105 transition-transform duration-300 scroll-reveal" style="animation-delay: 0.2s;">
                    <img src="https://placehold.co/400x400/DBEAFE/000000?text=1. +language" alt="language" class="w-full h-56 object-cover object-top">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-indigo-800"></h3>
                        <p class="text-blue-600">Head of Sciences</p>
                        <p class="text-gray-600 text-sm mt-2">Inspiring the next generation of scientists and innovators.</p>
                    </div>
                </div>
                <!-- Faculty Member 4 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden transform hover:scale-105 transition-transform duration-300 scroll-reveal" style="animation-delay: 0.3s;">
                    <img src="https://placehold.co/400x400/C7D2FE/000000?text=" alt="maths tutorial" class="w-full h-56 object-cover object-top">
                    <div class="p-6">
                        <h3 class="text-xl font-semibold text-indigo-800"></h3>
                        <p class="text-blue-600">Sports Coordinator</p>
                        <p class="text-gray-600 text-sm mt-2">Promoting physical well-being and teamwork among students.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Admissions Process Section (Improved Visuals) -->
    <section id="admissions" class="py-16 md:py-24 bg-gradient-to-l from-blue-50 to-indigo-50 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-blue-700 mb-12">Our Simple Admissions Process</h2>
            <div class="max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Step 1 -->
                <div class="bg-white p-8 rounded-xl shadow-lg transition-all duration-300 hover:shadow-xl hover:scale-105 scroll-reveal">
                    <div class="w-16 h-16 bg-blue-500 text-white rounded-full flex items-center justify-center mx-auto mb-6 text-2xl font-bold">1</div>
                    <h3 class="text-2xl font-semibold text-blue-800 mb-3">Apply Online</h3>
                    <p class="text-gray-700">Fill out our easy-to-use online registration form with all required details.</p>
                </div>
                <!-- Step 2 -->
                <div class="bg-white p-8 rounded-xl shadow-lg transition-all duration-300 hover:shadow-xl hover:scale-105 scroll-reveal" style="animation-delay: 0.2s;">
                    <div class="w-16 h-16 bg-indigo-500 text-white rounded-full flex items-center justify-center mx-auto mb-6 text-2xl font-bold">2</div>
                    <h3 class="text-2xl font-semibold text-indigo-800 mb-3">Assessment & Interview</h3>
                    <p class="text-gray-700">Students may undergo a brief assessment, followed by an interview with parents/guardians.</p>
                </div>
                <!-- Step 3 -->
                <div class="bg-white p-8 rounded-xl shadow-lg transition-all duration-300 hover:shadow-xl hover:scale-105 scroll-reveal" style="animation-delay: 0.4s;">
                    <div class="w-16 h-16 bg-green-500 text-white rounded-full flex items-center justify-center mx-auto mb-6 text-2xl font-bold">3</div>
                    <h3 class="text-2xl font-semibold text-green-800 mb-3">Enrollment Confirmation</h3>
                    <p class="text-gray-700">Receive your admission offer and complete the enrollment to secure your child's place.</p>
                </div>
            </div>
            <a href="#registration" class="mt-12 inline-block bg-blue-700 text-white px-10 py-4 rounded-full shadow-lg text-lg font-bold hover:bg-blue-800 transition-colors duration-300 animated-button scroll-reveal" style="animation-delay: 0.6s;">
                Start Your Child's Future
            </a>
        </div>
    </section>

    <!-- Events & News Section -->
    <section id="events" class="py-16 md:py-24 bg-purple-50 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-purple-700 mb-12">Latest from urji accademy</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- Event 1 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 scroll-reveal">
                    <h3 class="text-2xl font-semibold text-purple-800 mb-2">Annual Science Fair</h3>
                    <p class="text-gray-600 mb-3"><i class="fas fa-calendar-alt mr-2"></i>October 26, 2025</p>
                    <p class="text-gray-700 leading-relaxed">Join us for our exciting annual science fair showcasing innovative projects from students of all grades.</p>
                </div>
                <!-- Event 2 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 scroll-reveal" style="animation-delay: 0.1s;">
                    <h3 class="text-2xl font-semibold text-purple-800 mb-2">Parent-Teacher Conference</h3>
                    <p class="text-gray-600 mb-3"><i class="fas fa-calendar-alt mr-2"></i>November 15, 2025</p>
                    <p class="text-gray-700 leading-relaxed">An opportunity for parents to meet with teachers to discuss student progress and academic goals.</p>
                </div>
                <!-- News 1 -->
                <div class="bg-white p-6 rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 scroll-reveal" style="animation-delay: 0.2s;">
                    <h3 class="text-2xl font-semibold text-purple-800 mb-2">New Robotics Club Launched!</h3>
                    <p class="text-gray-600 mb-3"><i class="fas fa-newspaper mr-2"></i>September 1, 2025</p>
                    <p class="text-gray-700 leading-relaxed">urji accademy is proud to announce the launch of its new Robotics Club. Enroll now!</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Gallery Section -->
    <section id="gallery" class="py-16 md:py-24 bg-teal-50 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-teal-700 mb-12">Our Campus & Activities</h2>
            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
                <div class="rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal">
                    <img src="https://placehold.co/600x400/87CEEB/000000?text=Students+Learning" alt="Students Learning" class="w-full h-48 object-cover">
                    <p class="p-4 text-gray-700 font-medium">Engaged Learning</p>
                </div>
                <div class="rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.1s;">
                    <img src="https://placehold.co/600x400/90EE90/000000?text=School+Playground" alt="School Playground" class="w-full h-48 object-cover">
                    <p class="p-4 text-gray-700 font-medium">Playground Fun</p>
                </div>
                <div class="rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.2s;">
                    <img src="https://placehold.co/600x400/FFD700/000000?text=Library+Reading" alt="Library Reading" class="w-full h-48 object-cover">
                    <p class="p-4 text-gray-700 font-medium">Quiet Reading Time</p>
                </div>
                <div class="rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.3s;">
                    <img src="https://placehold.co/600x400/FFA07A/000000?text=Science+Lab" alt="Science Lab" class="w-full h-48 object-cover">
                    <p class="p-4 text-gray-700 font-medium">Science Experiment</p>
                </div>
                <div class="rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.4s;">
                    <img src="https://placehold.co/600x400/DA70D6/000000?text=Art+Class" alt="Art Class" class="w-full h-48 object-cover">
                    <p class="p-4 text-gray-700 font-medium">Creative Arts</p>
                </div>
                <div class="rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 transform hover:scale-105 scroll-reveal" style="animation-delay: 0.5s;">
                    <img src="https://placehold.co/600x400/ADD8E6/000000?text=Sports+Day" alt="Sports Day" class="w-full h-48 object-cover">
                    <p class="p-4 text-gray-700 font-medium">Sports Activities</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Testimonials Section -->
    <section id="testimonials" class="py-16 md:py-24 bg-gradient-to-r from-yellow-50 to-orange-50 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-yellow-700 mb-12">What Our Community Says</h2>
            <div class="relative w-full max-w-3xl mx-auto">
                <div id="testimonialCarousel" class="overflow-hidden rounded-xl shadow-xl bg-white p-8">
                    <div class="testimonial-item active">
                        <p class="text-lg italic text-gray-800 mb-4">"urji accademy has transformed my child's learning journey. The teachers are incredible, and the environment is so supportive!"</p>
                        <p class="font-semibold text-yellow-800">- Parent of Grade 5 Student</p>
                    </div>
                    <div class="testimonial-item hidden">
                        <p class="text-lg italic text-gray-800 mb-4">"I love coming to school every day! The classes are fun, and I've made so many great friends here. Robotics Club is my favorite!"</p>
                        <p class="font-semibold text-yellow-800">- Elias, Grade 8 Student</p>
                    </div>
                    <div class="testimonial-item hidden">
                        <p class="text-lg italic text-gray-800 mb-4">"The school's vision aligns perfectly with our family values. They truly prepare students not just academically, but as responsible individuals."</p>
                        <p class="font-semibold text-yellow-800">- Community Member</p>
                    </div>
                </div>
                <!-- Carousel Navigation Dots -->
                <div class="flex justify-center mt-6 space-x-2">
                    <button class="testimonial-dot w-3 h-3 bg-yellow-400 rounded-full cursor-pointer opacity-70 hover:opacity-100 transition-opacity duration-200 active-dot"></button>
                    <button class="testimonial-dot w-3 h-3 bg-yellow-400 rounded-full cursor-pointer opacity-70 hover:opacity-100 transition-opacity duration-200"></button>
                    <button class="testimonial-dot w-3 h-3 bg-yellow-400 rounded-full cursor-pointer opacity-70 hover:opacity-100 transition-opacity duration-200"></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Animated Statistics Section -->
    <section id="stats" class="py-16 md:py-24 bg-blue-800 text-white scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold mb-12">urji accademy By The Numbers</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="p-6 rounded-xl bg-blue-700 shadow-lg scroll-reveal" data-target="students">
                    <i class="fas fa-users text-5xl mb-4 text-blue-200"></i>
                    <div class="text-5xl font-extrabold mb-2" id="studentsCount">0</div>
                    <p class="text-blue-100 text-xl">Students Enrolled</p>
                </div>
                <div class="p-6 rounded-xl bg-blue-700 shadow-lg scroll-reveal" data-target="years">
                    <i class="fas fa-calendar-check text-5xl mb-4 text-blue-200"></i>
                    <div class="text-5xl font-extrabold mb-2" id="yearsCount">0</div>
                    <p class="text-blue-100 text-xl">Years of Excellence</p>
                </div>
                <div class="p-6 rounded-xl bg-blue-700 shadow-lg scroll-reveal" data-target="graduates">
                    <i class="fas fa-user-graduate text-5xl mb-4 text-blue-200"></i>
                    <div class="text-5xl font-extrabold mb-2" id="graduatesCount">0</div>
                    <p class="text-blue-100 text-xl">Graduates Impacting the World</p>
                </div>
            </div>
        </div>
    </section>

    <!-- FAQ Section -->
    <section id="faq" class="py-16 md:py-24 bg-gray-100 scroll-reveal">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-4xl font-bold text-gray-800 mb-12">Frequently Asked Questions</h2>
            <div class="max-w-3xl mx-auto space-y-4 text-left">
                <!-- FAQ Item 1 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden scroll-reveal">
                    <div class="accordion-header p-5 flex justify-between items-center bg-blue-50 text-blue-800 font-semibold">
                        <span>What are the school timings?</span>
                        <i class="fas fa-chevron-down transform transition-transform duration-300"></i>
                    </div>
                    <div class="accordion-content p-5 text-gray-700 bg-white">
                        Classes typically run from 8:00 AM to 3:30 PM, Monday to Friday. After-school programs are available until 5:00 PM.
                    </div>
                </div>
                <!-- FAQ Item 2 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden scroll-reveal" style="animation-delay: 0.1s;">
                    <div class="accordion-header p-5 flex justify-between items-center bg-blue-50 text-blue-800 font-semibold">
                        <span>Do you offer scholarships?</span>
                        <i class="fas fa-chevron-down transform transition-transform duration-300"></i>
                    </div>
                    <div class="accordion-content p-5 text-gray-700 bg-white">
                        Yes, urji accademy offers a limited number of merit-based and need-based scholarships. Please contact our admissions office for more details.
                    </div>
                </div>
                <!-- FAQ Item 3 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden scroll-reveal" style="animation-delay: 0.2s;">
                    <div class="accordion-header p-5 flex justify-between items-center bg-blue-50 text-blue-800 font-semibold">
                        <span>What extracurricular activities are available?</span>
                        <i class="fas fa-chevron-down transform transition-transform duration-300"></i>
                    </div>
                    <div class="accordion-content p-5 text-gray-700 bg-white">
                        We offer a wide range of extracurricular activities including sports, robotics, drama, music, art, debate, and various clubs.
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Student Comments Section (Local, Non-Persistent) -->
    <section id="comments" class="py-16 md:py-24 bg-gray-100 scroll-reveal">
        <div class="container mx-auto px-6">
            <h2 class="text-4xl font-bold text-blue-700 text-center mb-12">Student & Parent Feedback</h2>

            <div class="max-w-2xl mx-auto bg-white rounded-xl shadow-lg p-6">
                <h3 class="text-2xl font-semibold text-gray-800 mb-4">Leave a Comment</h3>
                <p class="text-sm text-red-500 mb-4 text-center">
                    * Important: This is a local preview. Comments are for demonstration and **not saved permanently**. For full functionality with data saving, please deploy this website to a live server with a backend database.
                </p>
                <form id="commentForm" class="space-y-4">
                    <div>
                        <label for="commentName" class="block text-sm font-medium text-gray-700">Your Name</label>
                        <input type="text" id="commentName" name="commentName" required
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="commentText" class="block text-sm font-medium text-gray-700">Your Comment</label>
                        <textarea id="commentText" name="commentText" rows="4" required
                                  class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm"></textarea>
                    </div>
                    <button type="submit" class="w-full bg-blue-600 text-white py-2 px-4 rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 transition-colors duration-300 animated-button">
                        Post Comment
                    </button>
                </form>

                <div class="mt-8">
                    <h3 class="text-2xl font-semibold text-gray-800 mb-4">What Our Community Says:</h3>
                    <div id="commentsList" class="space-y-6 max-h-96 overflow-y-auto scrollable-content pr-4">
                        <!-- Comments will be displayed here locally -->
                        <p class="text-gray-500 text-center py-4">No comments yet. Be the first!</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Registration Section (Local, Non-Persistent) -->
    <section id="registration" class="py-16 md:py-24 bg-gradient-to-l from-indigo-50 to-blue-50 scroll-reveal">
        <div class="container mx-auto px-6">
            <h2 class="text-4xl font-bold text-blue-700 text-center mb-12">Student Registration</h2>

            <div class="max-w-3xl mx-auto bg-white rounded-xl shadow-lg p-8">
                <p class="text-gray-600 text-center mb-6">Your temporary User ID: <span id="userIdDisplay" class="font-bold text-blue-600">Local Session Only</span></p>
                <p class="text-sm text-red-500 mb-4 text-center">
                    * Important: This is a local preview. Registrations are for demonstration and **not saved permanently**. For full functionality with data saving, please deploy this website to a live server with a backend database.
                </p>
                <form id="registrationForm" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div>
                        <label for="studentName" class="block text-sm font-medium text-gray-700">Student Name</label>
                        <input type="text" id="studentName" name="studentName" required
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="fatherName" class="block text-sm font-medium text-gray-700">Father's Name</label>
                        <input type="text" id="fatherName" name="fatherName" required
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="age" class="block text-sm font-medium text-gray-700">Age</label>
                        <input type="number" id="age" name="age" required min="5" max="18"
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="gender" class="block text-sm font-medium text-gray-700">Gender</label>
                        <select id="gender" name="gender" required
                                class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                            <option value="">Select Gender</option>
                            <option value="Male">Male</option>
                            <option value="Female">Female</option>
                            <option value="Other">Other</option>
                        </select>
                    </div>
                    <div>
                        <label for="dob" class="block text-sm font-medium text-gray-700">Date of Birth</label>
                        <input type="date" id="dob" name="dob" required
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="grade" class="block text-sm font-medium text-gray-700">Grade</label>
                        <input type="number" id="grade" name="grade" required min="1" max="12"
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div class="md:col-span-2">
                        <label for="gradeLevel" class="block text-sm font-medium text-gray-700">Grade Level (e.g., Freshman, Sophomore)</label>
                        <input type="text" id="gradeLevel" name="gradeLevel" required
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div class="md:col-span-2">
                        <label for="averageGrade" class="block text-sm font-medium text-gray-700">Previous Year Average Grade (%)</label>
                        <input type="number" id="averageGrade" name="averageGrade" required min="0" max="100"
                               class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm">
                    </div>
                    <div class="md:col-span-2">
                        <button type="submit" class="w-full bg-green-600 text-white py-3 px-4 rounded-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-offset-2 transition-colors duration-300 font-semibold animated-button">
                            Register Student
                        </button>
                    </div>
                </form>

                <div class="mt-12">
                    <h3 class="text-2xl font-semibold text-gray-800 mb-4">Temporarily Registered Students</h3>
                    <div id="registeredStudentsList" class="space-y-4 max-h-96 overflow-y-auto scrollable-content pr-4">
                        <!-- Registered students will be displayed here locally (non-persistent) -->
                        <p class="text-gray-500 text-center py-4">No students registered yet in this session.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Call to Action (Enrollment) -->
    <section class="py-16 bg-blue-900 text-white text-center scroll-reveal">
        <div class="container mx-auto px-6">
            <h2 class="text-3xl md:text-4xl font-bold mb-6">Ready to Join the urji accademy Family?</h2>
            <p class="text-xl mb-8 max-w-2xl mx-auto">Take the first step towards a brighter future for your child. Enroll today and experience educational excellence!</p>
            <a href="#registration" class="inline-block bg-yellow-400 text-blue-900 px-10 py-4 rounded-full shadow-lg text-lg font-bold hover:bg-yellow-300 transition-colors duration-300 animated-button">
                Enroll Your Child Now!
            </a>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-blue-800 text-white py-8 text-center">
        <div class="container mx-auto px-6">
            <p>&copy; 2025 urji accademy. All rights reserved.</p>
            <p class="mt-2 text-sm">Designed with passion for learning.</p>
            <div class="flex justify-center space-x-6 mt-4">
                <a href="#" class="text-white hover:text-blue-200 transition-colors duration-200" title="Facebook"><i class="fab fa-facebook-f text-xl"></i></a>
                <a href="#" class="text-white hover:text-blue-200 transition-colors duration-200" title="Twitter"><i class="fab fa-twitter text-xl"></i></a>
                <a href="https://t.me/+Lp3nk_k81WQ2MjA0" target="_blank" class="text-white hover:text-blue-200 transition-colors duration-200" title="Telegram"><i class="fab fa-telegram-plane text-xl"></i></a>
                <a href="#" class="text-white hover:text-blue-200 transition-colors duration-200" title="Instagram"><i class="fab fa-instagram text-xl"></i></a>
            </div>
        </div>
    </footer>

    <!-- Back to Top Button -->
    <button onclick="scrollToTop()" id="backToTopBtn" title="Go to top">
        <i class="fas fa-arrow-up"></i>
    </button>

    <!-- JavaScript for dynamic functionality -->
    <script type="module">
        // Global utility functions for message boxes
        function showMessageBox(message) {
            document.getElementById('messageText').innerText = message;
            document.getElementById('messageBox').style.display = 'block';
            document.getElementById('overlay').style.display = 'block';
        }

        function hideMessageBox() {
            document.getElementById('messageBox').style.display = 'none';
            document.getElementById('overlay').style.display = 'none';
        }

        // Mobile menu toggle
        const mobileMenuButton = document.getElementById('mobile-menu-button');
        const mobileMenu = document.getElementById('mobile-menu');

        mobileMenuButton.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });

        function hideMobileMenu() {
            mobileMenu.classList.add('hidden');
        }

        // Testimonial Carousel
        const testimonialItems = document.querySelectorAll('#testimonialCarousel .testimonial-item');
        const testimonialDots = document.querySelectorAll('.testimonial-dot');
        let currentTestimonialIndex = 0;

        function showTestimonial(index) {
            testimonialItems.forEach((item, i) => {
                if (i === index) {
                    item.classList.add('active');
                } else {
                    item.classList.remove('active');
                }
            });
            testimonialDots.forEach((dot, i) => {
                if (i === index) {
                    dot.classList.add('active-dot');
                    dot.style.opacity = '1';
                } else {
                    dot.classList.remove('active-dot');
                    dot.style.opacity = '0.7';
                }
            });
        }

        testimonialDots.forEach((dot, index) => {
            dot.addEventListener('click', () => {
                currentTestimonialIndex = index;
                showTestimonial(currentTestimonialIndex);
            });
        });

        function nextTestimonial() {
            currentTestimonialIndex = (currentTestimonialIndex + 1) % testimonialItems.length;
            showTestimonial(currentTestimonialIndex);
        }
        setInterval(nextTestimonial, 7000); // Auto-advance every 7 seconds
        showTestimonial(currentTestimonialIndex); // Initial display


        // FAQ Accordion functionality
        document.querySelectorAll('.accordion-header').forEach(header => {
            header.addEventListener('click', () => {
                const content = header.nextElementSibling;
                const icon = header.querySelector('i');

                // Close other open accordions
                document.querySelectorAll('.accordion-content.open').forEach(openContent => {
                    if (openContent !== content) {
                        openContent.style.maxHeight = null;
                        openContent.classList.remove('open');
                        openContent.previousElementSibling.querySelector('i').classList.remove('rotate-180');
                    }
                });

                // Toggle current accordion
                if (content.classList.contains('open')) {
                    content.style.maxHeight = null;
                    content.classList.remove('open');
                    icon.classList.remove('rotate-180');
                } else {
                    content.style.maxHeight = content.scrollHeight + "px"; // Set max-height to natural height
                    content.classList.add('open');
                    icon.classList.add('rotate-180');
                }
            });
        });


        // Local (non-persistent) storage for comments and students
        // This data will be lost when the page is refreshed or closed.
        let localComments = [];
        let localStudents = [];

        // Function to render local comments
        function renderLocalComments() {
            const commentsList = document.getElementById('commentsList');
            commentsList.innerHTML = '';
            if (localComments.length === 0) {
                commentsList.innerHTML = '<p class="text-gray-500 text-center py-4">No comments yet in this session.</p>';
                return;
            }
            localComments.forEach(comment => {
                const commentElement = document.createElement('div');
                commentElement.className = 'bg-gray-50 p-4 rounded-lg shadow-sm border border-gray-200';
                const avatarBgColor = `hsl(${Math.random() * 360}, 70%, 70%)`; // Random color for avatar background
                commentElement.innerHTML = `
                    <div class="flex items-start space-x-3">
                        <div class="flex-shrink-0 w-10 h-10 rounded-full flex items-center justify-center text-white font-bold" style="background-color: ${avatarBgColor};">
                            ${comment.name ? comment.name.charAt(0).toUpperCase() : '?'}
                        </div>
                        <div class="flex-grow">
                            <p class="font-semibold text-gray-900">${comment.name || 'Anonymous'}</p>
                            <p class="text-sm text-gray-600 mt-1">${comment.text}</p>
                            <p class="text-xs text-gray-400 mt-1">
                                ${new Date(comment.timestamp).toLocaleString()} (Local)
                            </p>
                        </div>
                    </div>
                `;
                commentsList.prepend(commentElement); // Add new comments at the top
            });
        }

        // Function to render local students
        function renderLocalStudents() {
            const studentsList = document.getElementById('registeredStudentsList');
            studentsList.innerHTML = '';
            if (localStudents.length === 0) {
                studentsList.innerHTML = '<p class="text-gray-500 text-center py-4">No students registered yet in this session.</p>';
                return;
            }
            localStudents.forEach(student => {
                const studentElement = document.createElement('div');
                studentElement.className = 'bg-blue-50 p-4 rounded-lg shadow-sm border border-blue-200 flex justify-between items-center';
                studentElement.innerHTML = `
                    <div>
                        <p class="font-semibold text-blue-800">${student.studentName} (Grade ${student.grade})</p>
                        <p class="text-sm text-gray-700">Father: ${student.fatherName}</p>
                        <p class="text-sm text-gray-700">Age: ${student.age}, Gender: ${student.gender}, DOB: ${student.dob}</p>
                        <p class="text-sm text-gray-700">Grade Level: ${student.gradeLevel}, Average Grade: ${student.averageGrade}%</p>
                        <p class="text-xs text-gray-500 mt-2">Registered (Local Session)</p>
                    </div>
                `;
                studentsList.prepend(studentElement); // Add new students at the top
            });
        }

        // Handle Comment Form Submission (Local, Non-Persistent)
        document.getElementById('commentForm').addEventListener('submit', (e) => {
            e.preventDefault();

            const form = e.target;
            const name = form.commentName.value.trim();
            const text = form.commentText.value.trim();

            if (!name || !text) {
                showMessageBox("Please enter your name and comment.");
                return;
            }

            const newComment = {
                name: name,
                text: text,
                timestamp: new Date().getTime() // Use local timestamp
            };
            localComments.push(newComment);
            renderLocalComments(); // Re-render comments
            showMessageBox("Comment posted successfully! (Local Preview - Not saved permanently)");
            form.reset();
        });

        // Handle Registration Form Submission (Local, Non-Persistent)
        document.getElementById('registrationForm').addEventListener('submit', (e) => {
            e.preventDefault();

            const form = e.target;
            const studentName = form.studentName.value.trim();
            const fatherName = form.fatherName.value.trim();
            const age = parseInt(form.age.value);
            const gender = form.gender.value;
            const dob = form.dob.value;
            const grade = parseInt(form.grade.value);
            const gradeLevel = form.gradeLevel.value.trim();
            const averageGrade = parseFloat(form.averageGrade.value);

            if (averageGrade < 40) {
                showMessageBox("Registration failed: Student's previous year average grade must be 40% or above.");
                return;
            }

            const newStudent = {
                studentName,
                fatherName,
                age,
                gender,
                dob,
                grade,
                gradeLevel,
                averageGrade,
                timestamp: new Date().getTime() // Use local timestamp
            };
            localStudents.push(newStudent);
            renderLocalStudents(); // Re-render students
            showMessageBox("Student registered successfully! (Local Preview - Not saved permanently)");
            form.reset();
        });

        // Back to Top button logic
        const backToTopBtn = document.getElementById("backToTopBtn");

        window.onscroll = function() { scrollFunction() };

        function scrollFunction() {
            if (document.body.scrollTop > 200 || document.documentElement.scrollTop > 200) {
                backToTopBtn.classList.add('show');
            } else {
                backToTopBtn.classList.remove('show');
            }
        }

        function scrollToTop() {
            document.body.scrollTop = 0; // For Safari
            document.documentElement.scrollTop = 0; // For Chrome, Firefox, IE and Opera
        }

        // Scroll Reveal Intersection Observer
        const scrollRevealElements = document.querySelectorAll('.scroll-reveal');

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                } else {
                    // Optional: Remove active class when out of view if you want re-triggering
                    // entry.target.classList.remove('active');
                }
            });
        }, {
            threshold: 0.1, // Trigger when 10% of the element is visible
            rootMargin: '0px 0px -50px 0px' // Adjust to trigger a bit earlier
        });

        scrollRevealElements.forEach(el => observer.observe(el));


        // Animated Stats Counter
        function animateValue(obj, start, end, duration) {
            let startTimestamp = null;
            const step = (timestamp) => {
                if (!startTimestamp) startTimestamp = timestamp;
                const progress = Math.min((timestamp - startTimestamp) / duration, 1);
                obj.innerHTML = Math.floor(progress * (end - start) + start).toLocaleString();
                if (progress < 1) {
                    window.requestAnimationFrame(step);
                }
            };
            window.requestAnimationFrame(step);
        }

        const statsObserver = new IntersectionObserver((entries, observer) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const target = entry.target.dataset.target;
                    if (target === 'students' && entry.target.querySelector('#studentsCount').innerText === '0') {
                        animateValue(document.getElementById("studentsCount"), 0, 1500, 2000);
                    } else if (target === 'years' && entry.target.querySelector('#yearsCount').innerText === '0') {
                        animateValue(document.getElementById("yearsCount"), 0, 10, 2500);
                    } else if (target === 'graduates' && entry.target.querySelector('#graduatesCount').innerText === '0') {
                        animateValue(document.getElementById("graduatesCount"), 0, 500, 2200);
                    }
                    observer.unobserve(entry.target); // Stop observing once animated
                }
            });
        }, {
            threshold: 0.5 // Trigger when 50% of the element is visible
        });

        document.querySelectorAll('.scroll-reveal[data-target]').forEach(el => {
            statsObserver.observe(el);
        });


        // Initial render for local comments and students on load
        window.onload = () => {
            renderLocalComments();
            renderLocalStudents();
            document.getElementById('userIdDisplay').innerText = 'Local Session Only'; // Indicate no real user ID
        };
    </script>
</body>
</html>
