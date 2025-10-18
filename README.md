<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ECOCOIN - Turn Your E-Waste into Rewards</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        * {
            font-family: 'Montserrat', sans-serif;
        }
        
        body {
            box-sizing: border-box;
            font-family: 'Montserrat', sans-serif;
        }
        
        /* Loading Animation Styles */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #fbbf24 0%, #10b981 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            animation: fadeOut 0.8s ease-in-out 3.5s forwards;
        }
        
        .coin-container {
            position: relative;
            width: 200px;
            height: 200px;
        }
        
        .falling-coin {
            position: absolute;
            top: -100px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 80px;
            animation: coinFall 1.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards,
                       coinSpin 1.5s linear;
        }
        
        .ecocoin-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 32px;
            font-weight: 900;
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            opacity: 0;
            animation: textEmerge 1s ease-out 1.8s forwards;
        }
        
        .loading-dots {
            position: absolute;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 8px;
        }
        
        .dot {
            width: 12px;
            height: 12px;
            background: white;
            border-radius: 50%;
            animation: dotBounce 1.4s ease-in-out infinite;
        }
        
        .dot:nth-child(1) { animation-delay: -0.32s; }
        .dot:nth-child(2) { animation-delay: -0.16s; }
        .dot:nth-child(3) { animation-delay: 0s; }
        
        @keyframes coinFall {
            0% {
                top: -100px;
                transform: translateX(-50%) scale(0.5);
            }
            70% {
                top: 90px;
                transform: translateX(-50%) scale(1.2);
            }
            85% {
                top: 80px;
                transform: translateX(-50%) scale(0.95);
            }
            100% {
                top: 85px;
                transform: translateX(-50%) scale(1);
            }
        }
        
        @keyframes coinSpin {
            0% { transform: translateX(-50%) rotateY(0deg); }
            100% { transform: translateX(-50%) rotateY(720deg); }
        }
        
        @keyframes textEmerge {
            0% {
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.3);
                filter: blur(10px);
            }
            50% {
                opacity: 0.7;
                transform: translate(-50%, -50%) scale(1.1);
                filter: blur(2px);
            }
            100% {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
                filter: blur(0px);
            }
        }
        
        @keyframes dotBounce {
            0%, 80%, 100% {
                transform: scale(0.8);
                opacity: 0.5;
            }
            40% {
                transform: scale(1.2);
                opacity: 1;
            }
        }
        
        @keyframes fadeOut {
            0% {
                opacity: 1;
                visibility: visible;
            }
            100% {
                opacity: 0;
                visibility: hidden;
            }
        }
        
        .main-content {
            opacity: 0;
            animation: fadeIn 0.8s ease-in-out 4s forwards;
        }
        
        @keyframes fadeIn {
            0% {
                opacity: 0;
                transform: translateY(20px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .gradient-bg {
            background: linear-gradient(135deg, #fbbf24 0%, #10b981 100%);
        }
        
        .eco-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .counter-animation {
            animation: countUp 2s ease-out;
        }
        
        @keyframes countUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .pulse-green {
            animation: pulseGreen 2s infinite;
        }
        
        @keyframes pulseGreen {
            0%, 100% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(16, 185, 129, 0); }
        }
        
        .step-icon {
            transition: all 0.3s ease;
        }
        
        .step-icon:hover {
            transform: scale(1.15) translateY(-8px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        
        .nav-link {
            transition: all 0.3s ease;
        }
        
        .nav-link:hover {
            color: #10b981;
            transform: translateY(-2px);
        }
        
        .mission-card {
            transition: all 0.3s ease;
        }
        
        .mission-card:hover {
            transform: scale(1.08) translateY(-8px);
            box-shadow: 0 25px 35px -5px rgba(0, 0, 0, 0.15), 0 15px 20px -5px rgba(0, 0, 0, 0.08);
        }
        
        .hover-card {
            transition: all 0.3s ease;
        }
        
        .hover-card:hover {
            transform: scale(1.08) translateY(-8px);
            box-shadow: 0 25px 35px -5px rgba(0, 0, 0, 0.15), 0 15px 20px -5px rgba(0, 0, 0, 0.08);
        }
        
        .hover-button {
            transition: all 0.3s ease;
        }
        
        .hover-button:hover {
            transform: scale(1.1) translateY(-4px);
            box-shadow: 0 15px 25px -3px rgba(0, 0, 0, 0.15), 0 8px 12px -2px rgba(0, 0, 0, 0.08);
        }
        
        .dashboard-stat {
            transition: all 0.3s ease;
        }
        
        .dashboard-stat:hover {
            transform: scale(1.15) translateY(-12px);
            box-shadow: 0 30px 40px -5px rgba(0, 0, 0, 0.2), 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }
        
        .location-card {
            transition: all 0.3s ease;
        }
        
        .location-card:hover {
            transform: scale(1.05) translateY(-6px);
            box-shadow: 0 20px 30px -3px rgba(0, 0, 0, 0.12), 0 10px 15px -2px rgba(0, 0, 0, 0.06);
        }

        .login-tab {
            transition: all 0.2s ease;
        }

        .login-tab.active {
            background-color: #10b981;
            color: white;
        }

        .login-tab:not(.active) {
            color: #6b7280;
        }

        .login-tab:not(.active):hover {
            background-color: #f3f4f6;
        }
    </style>
</head>
<body class="min-h-full bg-gray-50">
    <!-- Loading Screen -->
    <div class="loading-screen">
        <div class="coin-container">
            <div class="falling-coin">🪙</div>
            <div class="ecocoin-text">ECOCOIN</div>
        </div>
        <div class="loading-dots">
            <div class="dot"></div>
            <div class="dot"></div>
            <div class="dot"></div>
        </div>
    </div>

    <!-- Main Content -->
    <div class="main-content">
    <!-- Navigation -->
    <nav id="main-nav" class="bg-green-800 shadow-lg fixed w-full top-0 z-50 transition-transform duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center">
                    <div class="text-2xl font-bold text-white">
                        <span class="inline-flex items-center">
                            <span class="text-yellow-400 text-2xl mr-2">🪙</span>
                            <span>ECOCOIN</span>
                        </span>
                    </div>
                </div>
                <div id="nav-links" class="hidden md:flex flex-1 justify-center transition-opacity duration-300">
                    <div class="flex items-baseline space-x-4">
                        <a href="#home" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">Home</a>
                        <a href="#about" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">About</a>
                        <a href="#founders" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">Founders</a>
                        <a href="#why-ecocoin" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">Why ECOCOIN</a>
                        <a href="#how-it-works" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">How It Works</a>
                        <a href="#rewards" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">Rewards</a>
                        <a href="#dashboard" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">Dashboard</a>
                        <a href="#marketplace" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium bg-yellow-500 border border-yellow-400">🛒 Marketplace</a>
                        <a href="#locator" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">Find Machines</a>
                        <a href="#contact" class="nav-link text-white hover:text-green-200 px-3 py-2 rounded-md text-sm font-medium">Contact</a>
                    </div>
                </div>
                <div id="login-btn" class="hidden md:block transition-opacity duration-300">
                    <button onclick="showLoginModal()" class="nav-link text-white hover:text-green-200 px-4 py-2 rounded-md text-sm font-medium flex items-center">
                        Login
                    </button>
                </div>
                <div class="md:hidden">
                    <button id="mobile-menu-btn" class="text-white hover:text-green-200">
                        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div id="mobile-menu" class="md:hidden hidden bg-white border-t">
            <div class="px-2 pt-2 pb-3 space-y-1">
                <a href="#home" class="block px-3 py-2 text-gray-700 hover:text-green-600">Home</a>
                <a href="#about" class="block px-3 py-2 text-gray-700 hover:text-green-600">About</a>
                <a href="#founders" class="block px-3 py-2 text-gray-700 hover:text-green-600">Founders</a>
                <a href="#why-ecocoin" class="block px-3 py-2 text-gray-700 hover:text-green-600">Why ECOCOIN</a>
                <a href="#how-it-works" class="block px-3 py-2 text-gray-700 hover:text-green-600">How It Works</a>
                <a href="#rewards" class="block px-3 py-2 text-gray-700 hover:text-green-600">Rewards</a>
                <a href="#dashboard" class="block px-3 py-2 text-gray-700 hover:text-green-600">Dashboard</a>
                <a href="#marketplace" class="block px-3 py-2 text-gray-700 hover:text-green-600">Marketplace</a>
                <a href="#locator" class="block px-3 py-2 text-gray-700 hover:text-green-600">Find Machines</a>
                <a href="#contact" class="block px-3 py-2 text-gray-700 hover:text-green-600">Contact</a>
                <button onclick="showLoginModal()" class="block w-full text-left px-3 py-2 text-gray-700 hover:text-green-600">
                    Login
                </button>
            </div>
        </div>
    </nav>

    <!-- Home Page -->
    <section id="home" class="relative min-h-screen flex items-center pt-16 overflow-hidden">
        <!-- Background Image -->
        <div class="absolute inset-0 z-0">
            <img src="https://www.shutterstock.com/image-photo/concept-bioplastic-system-development-take-600nw-2287992323.jpg" 
                 alt="Sustainable technology and bioplastic development concept" 
                 class="w-full h-full object-cover"
                 onerror="this.style.display='none'; this.nextElementSibling.style.display='block';">
            <!-- Fallback background in case image fails to load -->
            <div class="w-full h-full bg-gradient-to-br from-green-400 via-blue-500 to-purple-600" style="display: none;"></div>
        </div>
        
        <!-- Overlay for better text readability -->
        <div class="absolute inset-0 bg-black bg-opacity-40 z-10"></div>
        
        <!-- Content -->
        <div class="relative z-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
            <div class="text-center">
                <h1 class="text-5xl md:text-7xl font-bold text-white mb-6 drop-shadow-lg">
                    Turn Your E-Waste into <span class="text-yellow-300">Rewards</span>
                </h1>
                <p class="text-xl md:text-2xl text-green-100 mb-8 max-w-3xl mx-auto drop-shadow-md">
                    Join the smart e-waste revolution. Recycle your electronics at our AI-powered vending machines and earn eco-coins for sustainable rewards.
                </p>
                <div class="space-x-4">
                    <button onclick="showLoginModal()" class="bg-yellow-400 hover:bg-yellow-500 text-gray-900 font-bold py-4 px-8 rounded-full text-lg transition-all duration-300 transform hover:scale-105 pulse-green shadow-lg">
                        Get Started
                    </button>
                    <button onclick="showLoginModal()" class="bg-transparent border-2 border-white text-white hover:bg-white hover:text-green-600 font-bold py-4 px-8 rounded-full text-lg transition-all duration-300 shadow-lg">
                        Login
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- About Us Page -->
    <section id="about" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">About ECOCOIN</h2>
                <p class="text-xl text-gray-600 max-w-3xl mx-auto">
                    We're solving the global e-waste crisis through innovative technology and community engagement.
                </p>
            </div>
            
            <div class="grid md:grid-cols-2 gap-12 items-center">
                <div>
                    <h3 class="text-3xl font-bold text-gray-900 mb-6">The E-Waste Problem</h3>
                    <p class="text-gray-600 mb-6">
                        Every year, the world generates over 50 million tons of electronic waste. Only 20% is properly recycled, 
                        while the rest ends up in landfills, polluting our environment and wasting valuable resources.
                    </p>
                    <div class="bg-red-50 border-l-4 border-red-400 p-4 mb-6">
                        <p class="text-red-700">
                            <strong>80%</strong> of e-waste is improperly disposed of, releasing toxic materials into our ecosystem.
                        </p>
                    </div>
                </div>
                <div class="text-center">
                    <div class="w-32 h-32 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <div class="w-16 h-16 bg-green-500 rounded-full flex items-center justify-center">
                            <svg class="w-8 h-8 text-white" fill="currentColor" viewBox="0 0 24 24">
                                <path d="M12,2A10,10 0 0,1 22,12A10,10 0 0,1 12,22A10,10 0 0,1 2,12A10,10 0 0,1 12,2M12,4A8,8 0 0,0 4,12A8,8 0 0,0 12,20A8,8 0 0,0 20,12A8,8 0 0,0 12,4M12,6L15.5,10.5L14.08,11.92L12,9.84L9.92,11.92L8.5,10.5L12,6M8.5,13.5L9.92,12.08L12,14.16L14.08,12.08L15.5,13.5L12,18L8.5,13.5Z"/>
                            </svg>
                        </div>
                    </div>
                    <p class="text-gray-600">Smart recycling for a sustainable future</p>
                </div>
            </div>
            
            <div class="mt-16 grid md:grid-cols-3 gap-8">
                <div class="text-center eco-card mission-card rounded-lg p-6 shadow-lg cursor-pointer">
                    <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <svg class="w-8 h-8 text-green-600" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M12 2C13.1 2 14 2.9 14 4C14 5.1 13.1 6 12 6C10.9 6 10 5.1 10 4C10 2.9 10.9 2 12 2ZM21 9V7L15 1H5C3.9 1 3 1.9 3 3V21C3 22.1 3.9 23 5 23H19C20.1 23 21 22.1 21 21V9H21ZM19 21H5V3H13V9H19V21Z"/>
                        </svg>
                    </div>
                    <h4 class="text-xl font-bold text-gray-900 mb-2">Our Mission</h4>
                    <p class="text-gray-600">
                        To make e-waste recycling accessible, rewarding, and impactful for everyone through smart technology.
                    </p>
                </div>
                <div class="text-center eco-card mission-card rounded-lg p-6 shadow-lg cursor-pointer">
                    <div class="w-16 h-16 bg-yellow-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <svg class="w-8 h-8 text-yellow-600" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M12 4.5C7 4.5 2.73 7.61 1 12C2.73 16.39 7 19.5 12 19.5S21.27 16.39 23 12C21.27 7.61 17 4.5 12 4.5ZM12 17C9.24 17 7 14.76 7 12S9.24 7 12 7S17 9.24 17 12S14.76 17 12 17ZM12 9C10.34 9 9 10.34 9 12S10.34 15 12 15S15 13.66 15 12S13.66 9 12 9Z"/>
                        </svg>
                    </div>
                    <h4 class="text-xl font-bold text-gray-900 mb-2">Our Vision</h4>
                    <p class="text-gray-600">
                        A world where every piece of electronic waste and recyclable waste is properly recycled and transformed into value.
                    </p>
                </div>
                <div class="text-center eco-card mission-card rounded-lg p-6 shadow-lg cursor-pointer">
                    <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <svg class="w-8 h-8 text-green-600" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M17,8C8,10 5.9,16.17 3.82,21.34L5.71,22L6.66,19.7C7.14,19.87 7.64,20 8,20C19,20 22,3 22,3C21,5 14,5.25 9,6.25C4,7.25 2,11.5 2,13.5C2,15.5 3.75,17.25 3.75,17.25C7,8 17,8 17,8Z"/>
                        </svg>
                    </div>
                    <h4 class="text-xl font-bold text-gray-900 mb-2">Sustainability Goals</h4>
                    <p class="text-gray-600">
                        Reduce e-waste by 50% in participating communities and create a circular economy for electronics.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- Founders Section -->
    <section id="founders" class="py-20 bg-gray-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">Meet Our Founders</h2>
                <p class="text-xl text-gray-600">The visionaries behind ECOCOIN</p>
            </div>

            <div class="grid md:grid-cols-2 gap-12 max-w-4xl mx-auto">
                <!-- Founder -->
                <div class="bg-white rounded-lg shadow-lg overflow-hidden hover-card cursor-pointer">
                    <div class="bg-gradient-to-br from-green-300 to-green-400 p-6 text-white text-center">
                        <div class="w-20 h-20 bg-white rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl font-bold text-green-500">HN</span>
                        </div>
                        <h4 class="text-xl font-bold mb-2">Hemanth M Naik</h4>
                        <p class="text-green-50">Founder & CEO</p>
                    </div>
                    <div class="p-6">
                        <p class="text-gray-600 mb-4">
                            "I believe technology should serve humanity and our planet. Through ECOCOIN, 
                            I'm creating a world where discarded devices become catalysts for environmental healing."
                        </p>
                        <div class="bg-green-50 rounded-lg p-4">
                            <p class="text-green-600 font-medium">Building a global ecosystem where technology meets environmental responsibility</p>
                        </div>
                    </div>
                </div>

                <!-- Co-Founder -->
                <div class="bg-white rounded-lg shadow-lg overflow-hidden hover-card cursor-pointer">
                    <div class="bg-gradient-to-br from-amber-300 to-yellow-400 p-6 text-white text-center">
                        <div class="w-20 h-20 bg-white rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-2xl font-bold text-amber-500">SK</span>
                        </div>
                        <h4 class="text-xl font-bold mb-2">Sachin K</h4>
                        <p class="text-amber-50">Co-Founder & CTO</p>
                    </div>
                    <div class="p-6">
                        <p class="text-gray-600 mb-4">
                            "I'm passionate about building intelligent systems that make environmental action effortless. 
                            My goal is to create AI-powered solutions for waste management."
                        </p>
                        <div class="bg-amber-50 rounded-lg p-4">
                            <p class="text-amber-600 font-medium">Engineering smart machines that make recycling simple and rewarding</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Why ECOCOIN Page -->
    <section id="why-ecocoin" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">Why ECOCOIN?</h2>
                <p class="text-xl text-gray-600">Understanding our revolutionary approach to sustainable recycling</p>
            </div>

            <div class="max-w-4xl mx-auto">
                <!-- Main Question -->
                <div class="bg-gradient-to-r from-green-50 to-blue-50 rounded-2xl p-8 mb-12 border-l-8 border-green-500">
                    <h3 class="text-3xl font-bold text-gray-900 mb-6 text-center">What is ECOCOIN? 💡</h3>
                    <div class="bg-white rounded-xl p-8 shadow-lg">
                        <p class="text-lg text-gray-700 leading-relaxed text-center font-medium">
                            <span class="text-green-600 font-bold">EcoCoin</span> is a digital reward system that motivates people to recycle responsibly. 
                            It connects users, smart vending machines, and recycling companies through a simple app where users earn 
                            <span class="text-yellow-600 font-bold">EcoCoins</span> every time they deposit e-waste or recyclable materials. 
                            These coins can be redeemed for <span class="text-blue-600 font-bold">discounts, offers, or eco-friendly rewards</span> — 
                            making sustainability rewarding! 🌱
                        </p>
                    </div>
                </div>

                <!-- Key Benefits Grid -->
                <div class="grid md:grid-cols-3 gap-8 mb-12">
                    <div class="text-center hover-card bg-gradient-to-br from-green-50 to-emerald-50 rounded-xl p-6 shadow-lg cursor-pointer">
                        <div class="w-20 h-20 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-3xl">🎯</span>
                        </div>
                        <h4 class="text-xl font-bold text-green-700 mb-3">Motivation Through Rewards</h4>
                        <p class="text-gray-600">
                            Turn recycling into a rewarding experience. Every action earns you valuable EcoCoins!
                        </p>
                    </div>

                    <div class="text-center hover-card bg-gradient-to-br from-green-50 to-emerald-50 rounded-xl p-6 shadow-lg cursor-pointer">
                        <div class="w-20 h-20 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-3xl">🤖</span>
                        </div>
                        <h4 class="text-xl font-bold text-green-700 mb-3">Smart Technology</h4>
                        <p class="text-gray-600">
                            AI-powered vending machines make recycling effortless and accurate for everyone.
                        </p>
                    </div>

                    <div class="text-center hover-card bg-gradient-to-br from-yellow-50 to-amber-50 rounded-xl p-6 shadow-lg cursor-pointer">
                        <div class="w-20 h-20 bg-yellow-100 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-3xl">🌐</span>
                        </div>
                        <h4 class="text-xl font-bold text-yellow-700 mb-3">Connected Ecosystem</h4>
                        <p class="text-gray-600">
                            Seamlessly connects users, machines, and recycling companies in one platform.
                        </p>
                    </div>
                </div>

                <!-- How It Makes a Difference -->
                <div class="bg-gradient-to-r from-green-200 via-emerald-200 to-green-300 rounded-2xl p-8 text-gray-800 text-center">
                    <h3 class="text-3xl font-bold mb-6">Making Sustainability Rewarding! 🏆</h3>
                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <div class="text-5xl mb-4">♻️</div>
                            <h4 class="text-xl font-bold mb-3 text-green-800">For You</h4>
                            <p class="text-green-700">
                                Earn rewards while making a positive environmental impact. 
                                Get discounts, offers, and eco-friendly products!
                            </p>
                        </div>
                        <div>
                            <div class="text-5xl mb-4">🌍</div>
                            <h4 class="text-xl font-bold mb-3 text-green-800">For Earth</h4>
                            <p class="text-green-700">
                                Reduce e-waste pollution, save natural resources, 
                                and contribute to a cleaner, greener planet!
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- How It Works Page -->
    <section id="how-it-works" class="py-20 bg-gray-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">How ECOCOIN Works</h2>
                <p class="text-xl text-gray-600">
                    Simple steps to turn your e-waste into valuable rewards
                </p>
            </div>
            
            <div class="grid md:grid-cols-5 gap-8">
                <div class="text-center">
                    <div class="step-icon bg-gradient-to-br from-green-400 to-green-500 text-white rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4 cursor-pointer shadow-lg">
                        <span class="text-3xl">📱</span>
                    </div>
                    <h4 class="text-lg font-bold text-gray-900 mb-2">1. Scan QR Code</h4>
                    <p class="text-gray-600">Find an ECOCOIN machine and scan the QR code to start</p>
                </div>
                <div class="text-center">
                    <div class="step-icon bg-gradient-to-br from-yellow-400 to-amber-500 text-white rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4 cursor-pointer shadow-lg">
                        <span class="text-3xl">🗂️</span>
                    </div>
                    <h4 class="text-lg font-bold text-gray-900 mb-2">2. Deposit E-Waste</h4>
                    <p class="text-gray-600">Place your electronic devices in the machine</p>
                </div>
                <div class="text-center">
                    <div class="step-icon bg-gradient-to-br from-green-400 to-emerald-500 text-white rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4 cursor-pointer shadow-lg">
                        <span class="text-3xl">🤖</span>
                    </div>
                    <h4 class="text-lg font-bold text-gray-900 mb-2">3. AI Detection</h4>
                    <p class="text-gray-600">Machine detects, categorizes, and weighs your items</p>
                </div>
                <div class="text-center">
                    <div class="step-icon bg-gradient-to-br from-yellow-400 to-yellow-500 text-white rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4 cursor-pointer shadow-lg">
                        <span class="text-3xl">🪙</span>
                    </div>
                    <h4 class="text-lg font-bold text-gray-900 mb-2">4. Earn Eco-Coins</h4>
                    <p class="text-gray-600">Receive eco-coins based on the value of your e-waste</p>
                </div>
                <div class="text-center">
                    <div class="step-icon bg-gradient-to-br from-green-400 to-green-600 text-white rounded-full w-20 h-20 flex items-center justify-center mx-auto mb-4 cursor-pointer shadow-lg">
                        <span class="text-3xl">🎁</span>
                    </div>
                    <h4 class="text-lg font-bold text-gray-900 mb-2">5. Redeem Rewards</h4>
                    <p class="text-gray-600">Use your eco-coins for discounts and eco-friendly products</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Rewards & Wallet Page -->
    <section id="rewards" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">Your Eco-Wallet & Rewards</h2>
                <p class="text-xl text-gray-600">Track your impact and redeem amazing rewards</p>
            </div>
            
            <div class="grid md:grid-cols-2 gap-8 mb-12">
                <div class="eco-card hover-card rounded-lg p-6 shadow-lg text-center cursor-pointer">
                    <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <span class="text-green-600 font-bold text-xl">D</span>
                    </div>
                    <h3 class="text-2xl font-bold text-green-600 mb-2">0</h3>
                    <p class="text-gray-600">Devices Recycled</p>
                </div>
                <div class="eco-card hover-card rounded-lg p-6 shadow-lg text-center cursor-pointer">
                    <div class="w-16 h-16 bg-yellow-100 rounded-full flex items-center justify-center mx-auto mb-4">
                        <span class="text-yellow-600 font-bold text-xl">E</span>
                    </div>
                    <h3 class="text-2xl font-bold text-yellow-600 mb-2">0 kg</h3>
                    <p class="text-gray-600">CO₂ Saved</p>
                </div>
            </div>
            
            <div class="text-center mb-8">
                <h3 class="text-2xl font-bold text-gray-900 mb-4">🎁 Rewards Not Available Yet</h3>
                <div class="bg-gradient-to-r from-yellow-50 to-orange-50 border-2 border-yellow-200 rounded-xl p-6 max-w-2xl mx-auto">
                    <div class="text-6xl mb-4">🚧</div>
                    <p class="text-lg text-gray-700 mb-4">
                        Our reward system is currently under development and not available yet.
                    </p>
                    <div class="bg-white rounded-lg p-4 mb-4">
                        <p class="text-gray-600 font-medium">
                            We're working hard to bring you an amazing rewards experience. Please check back soon!
                        </p>
                    </div>
                    <button onclick="showNotifyRewardsModal()" class="bg-yellow-500 hover:bg-yellow-600 text-white px-6 py-3 rounded-lg transition-colors font-semibold">
                        📧 Notify Me When Available
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Live Dashboard Page -->
    <section id="dashboard" class="py-20 bg-gray-900 text-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold mb-4">Live Impact Dashboard</h2>
                <p class="text-xl text-gray-300">Real-time data showing our collective environmental impact</p>
            </div>
            
            <div class="grid md:grid-cols-4 gap-8 mb-12">
                <div class="text-center dashboard-stat cursor-pointer p-4 rounded-lg">
                    <div class="text-5xl font-bold text-yellow-400 mb-2 counter-animation" id="total-waste">0</div>
                    <p class="text-gray-300">Tons of E-Waste Collected</p>
                </div>
                <div class="text-center dashboard-stat cursor-pointer p-4 rounded-lg">
                    <div class="text-5xl font-bold text-green-400 mb-2 counter-animation" id="co2-saved">0</div>
                    <p class="text-gray-300">Tons of CO₂ Saved</p>
                </div>
                <div class="text-center dashboard-stat cursor-pointer p-4 rounded-lg">
                    <div class="text-5xl font-bold text-yellow-400 mb-2 counter-animation" id="active-users">0</div>
                    <p class="text-gray-300">Active Users</p>
                </div>
                <div class="text-center dashboard-stat cursor-pointer p-4 rounded-lg">
                    <div class="text-5xl font-bold text-green-400 mb-2 counter-animation" id="machines">0</div>
                    <p class="text-gray-300">Active Machines</p>
                </div>
            </div>
            
            <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-gray-800 hover-card rounded-lg p-6 cursor-pointer">
                    <h3 class="text-xl font-bold mb-4">Monthly Collection Trend</h3>
                    <div class="h-48 bg-gray-700 rounded-lg flex items-center justify-center">
                        <div class="text-center">
                            <div class="w-16 h-16 bg-gray-600 rounded-full flex items-center justify-center mx-auto mb-2">
                                <svg class="w-8 h-8 text-white" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M22,21H2V3H4V19H6V17H10V19H12V16H16V19H18V17H22V21Z"/>
                                </svg>
                            </div>
                            <p class="text-gray-400">Interactive chart showing monthly e-waste collection growth</p>
                        </div>
                    </div>
                </div>
                <div class="bg-gray-800 hover-card rounded-lg p-6 cursor-pointer">
                    <h3 class="text-xl font-bold mb-4">Device Categories</h3>
                    <div class="space-y-4">
                        <div class="flex justify-between items-center">
                            <span>Smartphones</span>
                            <div class="w-32 bg-gray-700 rounded-full h-2">
                                <div class="bg-yellow-400 h-2 rounded-full" style="width: 65%"></div>
                            </div>
                            <span class="text-sm">65%</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span>Laptops</span>
                            <div class="w-32 bg-gray-700 rounded-full h-2">
                                <div class="bg-blue-400 h-2 rounded-full" style="width: 25%"></div>
                            </div>
                            <span class="text-sm">25%</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span>Accessories</span>
                            <div class="w-32 bg-gray-700 rounded-full h-2">
                                <div class="bg-yellow-400 h-2 rounded-full" style="width: 10%"></div>
                            </div>
                            <span class="text-sm">10%</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Marketplace Page -->
    <section id="marketplace" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">Eco Marketplace</h2>
                <p class="text-xl text-gray-600">Shop sustainable and refurbished products with your eco-coins</p>
            </div>
            
            <!-- Marketplace Status Notice -->
            <div class="text-center mb-8">
                <div class="bg-gradient-to-r from-blue-50 to-green-50 border-2 border-blue-200 rounded-xl p-6 max-w-2xl mx-auto">
                    <div class="text-6xl mb-4">🚧</div>
                    <h3 class="text-2xl font-bold text-gray-900 mb-4">🛒 Marketplace Coming Soon</h3>
                    <p class="text-lg text-gray-700 mb-4">
                        Our eco-friendly marketplace is currently under development and not available yet.
                    </p>
                    <div class="bg-white rounded-lg p-4 mb-4">
                        <p class="text-gray-600 font-medium">
                            We're working hard to bring you amazing sustainable products. Please check back soon!
                        </p>
                    </div>
                    <button onclick="showNotifyMarketplaceModal()" class="bg-green-500 hover:bg-green-600 text-white px-6 py-3 rounded-lg transition-colors font-semibold">
                        📧 Notify Me When Available
                    </button>
                </div>
            </div>
            
            <!-- Preview Products (Disabled) -->
            <div class="flex justify-center mb-8">
                <div class="flex space-x-4">
                    <button class="marketplace-filter hover-button bg-gray-300 text-gray-500 px-4 py-2 rounded-md cursor-not-allowed" disabled>All Products</button>
                    <button class="marketplace-filter hover-button bg-gray-200 text-gray-400 px-4 py-2 rounded-md cursor-not-allowed" disabled>Refurbished</button>
                    <button class="marketplace-filter hover-button bg-gray-200 text-gray-400 px-4 py-2 rounded-md cursor-not-allowed" disabled>Eco-Friendly</button>
                    <button class="marketplace-filter hover-button bg-gray-200 text-gray-400 px-4 py-2 rounded-md cursor-not-allowed" disabled>Accessories</button>
                </div>
            </div>
            
            <div class="grid md:grid-cols-4 gap-6 opacity-60" id="marketplace-products">
                <div class="product-card bg-gray-100 rounded-lg shadow-lg overflow-hidden cursor-not-allowed" data-category="refurbished">
                    <div class="p-6">
                        <div class="w-20 h-20 bg-gray-200 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-gray-400 font-bold text-2xl">P</span>
                        </div>
                        <h4 class="text-lg font-bold text-gray-500 mb-2">Refurbished iPhone 12</h4>
                        <p class="text-gray-400 mb-4">Like new condition, 1-year warranty</p>
                        <div class="flex justify-between items-center mb-4">
                            <span class="text-gray-400 font-bold">1,200 coins</span>
                        </div>
                        <div class="space-y-2">
                            <button disabled class="w-full bg-gray-300 text-gray-500 py-2 rounded-md cursor-not-allowed">
                                Coming Soon
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="product-card bg-gray-100 rounded-lg shadow-lg overflow-hidden cursor-not-allowed" data-category="eco-friendly">
                    <div class="p-6">
                        <div class="w-20 h-20 bg-gray-200 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-gray-400 font-bold text-2xl">B</span>
                        </div>
                        <h4 class="text-lg font-bold text-gray-500 mb-2">Bamboo Phone Case</h4>
                        <p class="text-gray-400 mb-4">100% biodegradable, multiple sizes</p>
                        <div class="flex justify-between items-center mb-4">
                            <span class="text-gray-400 font-bold">150 coins</span>
                        </div>
                        <div class="space-y-2">
                            <button disabled class="w-full bg-gray-300 text-gray-500 py-2 rounded-md cursor-not-allowed">
                                Coming Soon
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="product-card bg-gray-100 rounded-lg shadow-lg overflow-hidden cursor-not-allowed" data-category="refurbished">
                    <div class="p-6">
                        <div class="w-20 h-20 bg-gray-200 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-gray-400 font-bold text-2xl">L</span>
                        </div>
                        <h4 class="text-lg font-bold text-gray-500 mb-2">Refurbished MacBook Air</h4>
                        <p class="text-gray-400 mb-4">M1 chip, excellent condition</p>
                        <div class="flex justify-between items-center mb-4">
                            <span class="text-gray-400 font-bold">2,500 coins</span>
                        </div>
                        <div class="space-y-2">
                            <button disabled class="w-full bg-gray-300 text-gray-500 py-2 rounded-md cursor-not-allowed">
                                Coming Soon
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="product-card bg-gray-100 rounded-lg shadow-lg overflow-hidden cursor-not-allowed" data-category="accessories">
                    <div class="p-6">
                        <div class="w-20 h-20 bg-gray-200 rounded-full flex items-center justify-center mx-auto mb-4">
                            <span class="text-gray-400 font-bold text-2xl">S</span>
                        </div>
                        <h4 class="text-lg font-bold text-gray-500 mb-2">Solar Power Bank</h4>
                        <p class="text-gray-400 mb-4">20,000mAh with solar charging</p>
                        <div class="flex justify-between items-center mb-4">
                            <span class="text-gray-400 font-bold">400 coins</span>
                        </div>
                        <div class="space-y-2">
                            <button disabled class="w-full bg-gray-300 text-gray-500 py-2 rounded-md cursor-not-allowed">
                                Coming Soon
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Machine Locator Page -->
    <section id="locator" class="py-20 bg-gray-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">Find ECOCOIN Machines</h2>
                <p class="text-xl text-gray-600">Locate the nearest e-waste recycling machine in your area</p>
            </div>
            
            <div class="grid md:grid-cols-3 gap-8">
                <div class="md:col-span-2">
                    <div class="bg-white rounded-lg shadow-lg p-6 h-96">
                        <div class="h-full bg-gray-200 rounded-lg flex items-center justify-center">
                            <div class="text-center">
                                <div class="w-20 h-20 bg-gray-400 rounded-full flex items-center justify-center mx-auto mb-4">
                                    <svg class="w-10 h-10 text-white" fill="currentColor" viewBox="0 0 24 24">
                                        <path d="M12,2C15.31,2 18,4.66 18,7.95C18,12.41 12,19 12,19S6,12.41 6,7.95C6,4.66 8.69,2 12,2M12,6A2,2 0 0,0 10,8A2,2 0 0,0 12,10A2,2 0 0,0 14,8A2,2 0 0,0 12,6M20,19C20,21.21 16.42,23 12,23C7.58,23 4,21.21 4,19C4,17.71 5.22,16.56 7.11,15.94L7.75,16.74C6.67,17.19 6,17.81 6,18.5C6,19.88 8.69,21 12,21C15.31,21 18,19.88 18,18.5C18,17.81 17.33,17.19 16.25,16.74L16.89,15.94C18.78,16.56 20,17.71 20,19Z"/>
                                    </svg>
                                </div>
                                <p class="text-gray-600 mb-4">Interactive Map</p>
                                <p class="text-sm text-gray-500">Showing ECOCOIN machine locations near you</p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="space-y-4">
                    <div class="bg-white location-card rounded-lg shadow-lg p-6 text-center">
                        <div class="text-6xl mb-4">🚧</div>
                        <h4 class="font-bold text-gray-900 text-lg mb-2">Coming Soon!</h4>
                        <p class="text-gray-600 mb-4">ECOCOIN machines are not yet available in your area</p>
                        <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-4 mb-4">
                            <p class="text-yellow-800 text-sm">
                                <strong>📍 Expansion Plans:</strong><br>
                                We're working to bring ECOCOIN machines to your neighborhood soon!
                            </p>
                        </div>
                    </div>
                    
                    <div class="bg-white location-card rounded-lg shadow-lg p-4">
                        <h5 class="font-bold text-gray-900 mb-3">🎯 Planned Locations</h5>
                        <div class="space-y-3">
                            <div class="flex items-center space-x-3 opacity-60">
                                <div class="w-3 h-3 bg-gray-400 rounded-full"></div>
                                <div>
                                    <h6 class="font-medium text-gray-700">Downtown Mall</h6>
                                    <p class="text-xs text-gray-500">Coming Q2 2024</p>
                                </div>
                            </div>
                            <div class="flex items-center space-x-3 opacity-60">
                                <div class="w-3 h-3 bg-gray-400 rounded-full"></div>
                                <div>
                                    <h6 class="font-medium text-gray-700">University Campus</h6>
                                    <p class="text-xs text-gray-500">Coming Q3 2024</p>
                                </div>
                            </div>
                            <div class="flex items-center space-x-3 opacity-60">
                                <div class="w-3 h-3 bg-gray-400 rounded-full"></div>
                                <div>
                                    <h6 class="font-medium text-gray-700">Tech Park</h6>
                                    <p class="text-xs text-gray-500">Coming Q3 2024</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <button onclick="showNotifyModal()" class="w-full bg-blue-500 hover:bg-blue-600 text-white py-3 rounded-md transition-colors hover-button">
                        📧 Notify Me When Available
                    </button>
                    
                    <button onclick="showPartnerModal()" class="w-full bg-green-500 hover:bg-green-600 text-white py-3 rounded-md transition-colors hover-button">
                        🤝 Partner With Us
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact / Join Us Page -->
    <section id="contact" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold text-gray-900 mb-4">Join the Movement</h2>
                <p class="text-xl text-gray-600">Partner with us or get in touch to learn more</p>
            </div>
            
            <div class="grid md:grid-cols-2 gap-12">
                <div>
                    <h3 class="text-2xl font-bold text-gray-900 mb-6">Get in Touch</h3>
                    <form id="contact-form" class="space-y-6">
                        <div>
                            <label for="contact-name" class="block text-sm font-medium text-gray-700 mb-2">Name</label>
                            <input type="text" id="contact-name" name="name" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500">
                        </div>
                        <div>
                            <label for="contact-email" class="block text-sm font-medium text-gray-700 mb-2">Email</label>
                            <input type="email" id="contact-email" name="email" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500">
                        </div>
                        <div>
                            <label for="contact-type" class="block text-sm font-medium text-gray-700 mb-2">I'm interested in</label>
                            <select id="contact-type" name="type" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500">
                                <option value="">Select an option</option>
                                <option value="user">Becoming a user</option>
                                <option value="partner">Partnership opportunities</option>
                                <option value="location">Hosting a machine</option>
                                <option value="investor">Investment opportunities</option>
                                <option value="intern">Joining as intern</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                        <div>
                            <label for="contact-message" class="block text-sm font-medium text-gray-700 mb-2">Message</label>
                            <textarea id="contact-message" name="message" rows="4" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500"></textarea>
                        </div>
                        <button type="submit" class="w-full bg-green-500 hover:bg-green-600 text-white py-3 rounded-md transition-colors">
                            Send Message
                        </button>
                    </form>
                </div>
                
                <div>
                    <h3 class="text-2xl font-bold text-gray-900 mb-6">Connect With Us</h3>
                    <div class="space-y-4 mb-8">
                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 bg-green-100 rounded-full flex items-center justify-center">
                                <svg class="w-5 h-5 text-green-600" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M20,8L12,13L4,8V6L12,11L20,6M20,4H4C2.89,4 2,4.89 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V6C22,4.89 21.1,4 20,4Z"/>
                                </svg>
                            </div>
                            <div>
                                <p class="font-medium">Email</p>
                                <p class="text-gray-600">info@ecocoin.com</p>
                            </div>
                        </div>

                        <div class="flex items-center space-x-3">
                            <div class="w-10 h-10 bg-green-100 rounded-full flex items-center justify-center">
                                <svg class="w-5 h-5 text-green-600" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M12,11.5A2.5,2.5 0 0,1 9.5,9A2.5,2.5 0 0,1 12,6.5A2.5,2.5 0 0,1 14.5,9A2.5,2.5 0 0,1 12,11.5M12,2A7,7 0 0,0 5,9C5,14.25 12,22 12,22S19,14.25 19,9A7,7 0 0,0 12,2Z"/>
                                </svg>
                            </div>
                            <div>
                                <p class="font-medium">Address</p>
                                <p class="text-gray-600">Kalluballu Cross, Jigani APC<br>Bengaluru, Karnataka 560105</p>
                            </div>
                        </div>
                    </div>
                    
                    <h4 class="text-lg font-bold text-gray-900 mb-4">Follow Us</h4>
                    <div class="flex space-x-4">
                        <a href="#" class="w-10 h-10 bg-green-100 rounded-full flex items-center justify-center hover:bg-yellow-100 transition-colors">
                            <svg class="w-5 h-5 text-green-600" fill="currentColor" viewBox="0 0 24 24">
                                <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
                            </svg>
                        </a>
                        <a href="#" class="w-10 h-10 bg-yellow-100 rounded-full flex items-center justify-center hover:bg-green-100 transition-colors">
                            <svg class="w-5 h-5 text-yellow-600" fill="currentColor" viewBox="0 0 24 24">
                                <path d="M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z"/>
                            </svg>
                        </a>
                        <a href="#" class="w-10 h-10 bg-green-100 rounded-full flex items-center justify-center hover:bg-yellow-100 transition-colors">
                            <svg class="w-5 h-5 text-green-600" fill="currentColor" viewBox="0 0 24 24">
                                <path d="M12.017 0C5.396 0 .029 5.367.029 11.987c0 5.079 3.158 9.417 7.618 11.174-.105-.949-.199-2.403.041-3.439.219-.937 1.406-5.957 1.406-5.957s-.359-.72-.359-1.781c0-1.663.967-2.911 2.168-2.911 1.024 0 1.518.769 1.518 1.688 0 1.029-.653 2.567-.992 3.992-.285 1.193.6 2.165 1.775 2.165 2.128 0 3.768-2.245 3.768-5.487 0-2.861-2.063-4.869-5.008-4.869-3.41 0-5.409 2.562-5.409 5.199 0 1.033.394 2.143.889 2.741.097.118.112.221.085.345-.09.375-.293 1.199-.334 1.363-.053.225-.172.271-.402.165-1.495-.69-2.433-2.878-2.433-4.646 0-3.776 2.748-7.252 7.92-7.252 4.158 0 7.392 2.967 7.392 6.923 0 4.135-2.607 7.462-6.233 7.462-1.214 0-2.357-.629-2.748-1.378l-.748 2.853c-.271 1.043-1.002 2.35-1.492 3.146C9.57 23.812 10.763 24.009 12.017 24.009c6.624 0 11.99-5.367 11.99-11.988C24.007 5.367 18.641.001.012.001z"/>
                            </svg>
                        </a>
                        <a href="#" class="w-10 h-10 bg-yellow-100 rounded-full flex items-center justify-center hover:bg-green-100 transition-colors">
                            <svg class="w-5 h-5 text-yellow-600" fill="currentColor" viewBox="0 0 24 24">
                                <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                            </svg>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid md:grid-cols-4 gap-8">
                <div>
                    <div class="text-2xl font-bold text-yellow-400 mb-4">
                        <span class="inline-flex items-center">
                            <span class="text-yellow-400 text-2xl mr-2">🪙</span>
                            ECOCOIN
                        </span>
                    </div>
                    <p class="text-gray-300 mb-4">
                        Transforming e-waste into rewards for a sustainable future.
                    </p>
                    <div class="bg-gray-800 rounded-lg p-4 mb-4 border-l-4 border-green-400">
                        <p class="text-green-300 italic text-sm font-medium">
                            "Our vision for tomorrow is a world where every piece of electronic waste becomes a stepping stone to environmental healing."
                        </p>
                    </div>
                    <p class="text-sm text-gray-400">
                        Recycle Today for a Greener Tomorrow
                    </p>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">Quick Links</h4>
                    <ul class="space-y-2">
                        <li><a href="#home" class="text-gray-300 hover:text-yellow-400 transition-colors">Home</a></li>
                        <li><a href="#about" class="text-gray-300 hover:text-yellow-400 transition-colors">About</a></li>
                        <li><a href="#how-it-works" class="text-gray-300 hover:text-yellow-400 transition-colors">How It Works</a></li>
                        <li><a href="#rewards" class="text-gray-300 hover:text-yellow-400 transition-colors">Rewards</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">Services</h4>
                    <ul class="space-y-2">
                        <li><a href="#dashboard" class="text-gray-300 hover:text-yellow-400 transition-colors">Dashboard</a></li>
                        <li><a href="#marketplace" class="text-gray-300 hover:text-yellow-400 transition-colors">Marketplace</a></li>
                        <li><a href="#locator" class="text-gray-300 hover:text-yellow-400 transition-colors">Find Machines</a></li>
                        <li><a href="#contact" class="text-gray-300 hover:text-yellow-400 transition-colors">Contact</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-bold mb-4">Legal</h4>
                    <ul class="space-y-2">
                        <li><a href="#" class="text-gray-300 hover:text-yellow-400 transition-colors">Privacy Policy</a></li>
                        <li><a href="#" class="text-gray-300 hover:text-yellow-400 transition-colors">Terms of Service</a></li>
                        <li><a href="#" class="text-gray-300 hover:text-yellow-400 transition-colors">Cookie Policy</a></li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-gray-800 mt-8 pt-8 text-center">
                <p class="text-gray-400">
                    © 2024 ECOCOIN. All rights reserved. | Recycle Today for a Greener Tomorrow
                </p>
            </div>
        </div>
    </footer>
    </div>
    <!-- End Main Content -->

    <script>
        // Database System
        class EcoCoinDatabase {
            constructor() {
                this.users = this.loadUsers();
                this.currentUser = this.loadCurrentUser();
                this.adminEmail = 'princehemanth753@gmail.com';
            }

            loadUsers() {
                const users = localStorage.getItem('ecocoin_users');
                return users ? JSON.parse(users) : [];
            }

            saveUsers() {
                localStorage.setItem('ecocoin_users', JSON.stringify(this.users));
            }

            loadCurrentUser() {
                const user = localStorage.getItem('ecocoin_current_user');
                return user ? JSON.parse(user) : null;
            }

            saveCurrentUser(user) {
                this.currentUser = user;
                localStorage.setItem('ecocoin_current_user', JSON.stringify(user));
            }

            registerUser(userData) {
                const existingUser = this.users.find(user => user.email === userData.email);
                if (existingUser) {
                    throw new Error('Email already registered');
                }

                const newUser = {
                    id: Date.now().toString(),
                    username: userData.username,
                    email: userData.email,
                    password: userData.password,
                    phone: userData.phone || '',
                    ecoCoins: 50, // Welcome bonus
                    devicesRecycled: 0,
                    co2Saved: 0,
                    registrationDate: new Date().toISOString(),
                    isAdmin: userData.email === 'princehemanth753@gmail.com'
                };

                this.users.push(newUser);
                this.saveUsers();
                return newUser;
            }

            loginUser(email, password) {
                const user = this.users.find(u => u.email === email);
                if (user && user.password === password) {
                    this.saveCurrentUser(user);
                    return user;
                } else {
                    throw new Error('Invalid email or password');
                }
            }

            loginWithMobile(mobile, otp) {
                // In real app, verify OTP with SMS service
                if (otp === '123456') { // Demo OTP
                    let user = this.users.find(u => u.phone === mobile);
                    
                    if (!user) {
                        throw new Error('Mobile number not registered');
                    }
                    
                    this.saveCurrentUser(user);
                    return user;
                } else {
                    throw new Error('Invalid OTP');
                }
            }

            logoutUser() {
                this.currentUser = null;
                localStorage.removeItem('ecocoin_current_user');
            }
        }

        // Initialize database
        const database = new EcoCoinDatabase();

        // Smart Navigation Scroll Behavior
        let lastScrollTop = 0;
        let isScrollingDown = false;
        
        window.addEventListener('scroll', function() {
            const currentScroll = window.pageYOffset || document.documentElement.scrollTop;
            const nav = document.getElementById('main-nav');
            
            // Determine scroll direction
            if (currentScroll > lastScrollTop && currentScroll > 100) {
                // Scrolling down and past 100px
                if (!isScrollingDown) {
                    isScrollingDown = true;
                    // Hide entire navigation bar
                    nav.style.transform = 'translateY(-100%)';
                }
            } else if (currentScroll < lastScrollTop || currentScroll <= 100) {
                // Scrolling up or at top of page
                if (isScrollingDown || currentScroll <= 100) {
                    isScrollingDown = false;
                    // Show entire navigation bar
                    nav.style.transform = 'translateY(0)';
                }
            }
            
            lastScrollTop = currentScroll <= 0 ? 0 : currentScroll; // For Mobile or negative scrolling
        });

        // Mobile menu toggle
        document.getElementById('mobile-menu-btn').addEventListener('click', function() {
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenu.classList.toggle('hidden');
        });

        // Smooth scrolling for navigation links
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
                document.getElementById('mobile-menu').classList.add('hidden');
            });
        });

        // Counter animation for dashboard
        function animateCounter(element, target, duration = 2000) {
            let start = 0;
            const increment = target / (duration / 16);
            const timer = setInterval(() => {
                start += increment;
                if (start >= target) {
                    element.textContent = target;
                    clearInterval(timer);
                } else {
                    element.textContent = Math.floor(start);
                }
            }, 16);
        }

        // Get live dashboard data from database
        function getLiveDashboardData() {
            const allUsers = database.users;
            const totalUsers = allUsers.length;
            const totalDevices = allUsers.reduce((sum, u) => sum + u.devicesRecycled, 0);
            const totalCO2 = allUsers.reduce((sum, u) => sum + u.co2Saved, 0);
            const totalWaste = Math.floor(totalDevices * 0.5); // Estimate waste in tons
            const activeMachines = Math.min(12, Math.max(1, Math.floor(totalUsers / 10))); // Dynamic machine count
            
            return {
                totalWaste,
                totalCO2,
                totalUsers,
                activeMachines
            };
        }

        // Intersection Observer for dashboard counters
        const dashboardObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const data = getLiveDashboardData();
                    animateCounter(document.getElementById('total-waste'), data.totalWaste);
                    animateCounter(document.getElementById('co2-saved'), data.totalCO2);
                    animateCounter(document.getElementById('active-users'), data.totalUsers);
                    animateCounter(document.getElementById('machines'), data.activeMachines);
                    dashboardObserver.unobserve(entry.target);
                }
            });
        });

        const dashboardSection = document.getElementById('dashboard');
        if (dashboardSection) {
            dashboardObserver.observe(dashboardSection);
        }

        // Marketplace filter functionality
        document.querySelectorAll('.marketplace-filter').forEach(button => {
            button.addEventListener('click', function() {
                document.querySelectorAll('.marketplace-filter').forEach(btn => {
                    btn.classList.remove('bg-green-500', 'text-white');
                    btn.classList.add('bg-gray-200', 'text-gray-700');
                });
                this.classList.remove('bg-gray-200', 'text-gray-700');
                this.classList.add('bg-green-500', 'text-white');

                const category = this.getAttribute('data-category');
                const products = document.querySelectorAll('.product-card');
                
                products.forEach(product => {
                    if (category === 'all' || product.getAttribute('data-category') === category) {
                        product.style.display = 'block';
                    } else {
                        product.style.display = 'none';
                    }
                });
            });
        });

        // Contact form submission
        document.getElementById('contact-form').addEventListener('submit', function(e) {
            e.preventDefault();
            showSuccessMessage('Message sent successfully! We will get back to you soon.');
            this.reset();
        });

        // Login Modal Function
        function showLoginModal() {
            const modal = document.createElement('div');
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4">
                    <h3 class="text-2xl font-bold text-gray-900 mb-6">Welcome to ECOCOIN</h3>
                    
                    <!-- Login Method Selection -->
                    <div class="mb-6">
                        <div class="flex space-x-2 bg-gray-100 rounded-lg p-1">
                            <button type="button" id="email-login-tab" class="login-tab active flex-1 py-2 px-4 rounded-md font-medium transition-all duration-200">
                                📧 Email & Password
                            </button>
                            <button type="button" id="mobile-login-tab" class="login-tab flex-1 py-2 px-4 rounded-md font-medium transition-all duration-200">
                                📱 Mobile & OTP
                            </button>
                        </div>
                    </div>

                    <!-- Email Login Form -->
                    <form id="email-login-form" class="login-form">
                        <div class="mb-4">
                            <label for="login-email" class="block text-sm font-medium text-gray-700 mb-2">Email Address</label>
                            <input type="email" id="login-email" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500" placeholder="Enter your email">
                        </div>
                        <div class="mb-6">
                            <label for="login-password" class="block text-sm font-medium text-gray-700 mb-2">Password</label>
                            <input type="password" id="login-password" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500" placeholder="Enter your password">
                        </div>
                        <button type="submit" class="w-full bg-green-500 hover:bg-green-600 text-white py-3 rounded-md transition-colors font-medium mb-4">
                            🔐 Login with Email
                        </button>
                    </form>

                    <!-- Mobile Login Form -->
                    <form id="mobile-login-form" class="login-form hidden">
                        <div class="mb-4">
                            <label for="login-mobile" class="block text-sm font-medium text-gray-700 mb-2">Mobile Number</label>
                            <div class="flex">
                                <select class="px-3 py-2 border border-gray-300 rounded-l-md focus:outline-none focus:ring-2 focus:ring-green-500 bg-gray-50">
                                    <option value="+91">🇮🇳 +91</option>
                                    <option value="+1">🇺🇸 +1</option>
                                    <option value="+44">🇬🇧 +44</option>
                                </select>
                                <input type="tel" id="login-mobile" required class="flex-1 px-3 py-2 border border-gray-300 rounded-r-md focus:outline-none focus:ring-2 focus:ring-green-500" placeholder="Enter mobile number">
                            </div>
                        </div>
                        <button type="submit" id="send-otp-btn" class="w-full bg-blue-500 hover:bg-blue-600 text-white py-3 rounded-md transition-colors font-medium mb-4">
                            📲 Send OTP
                        </button>
                        
                        <!-- OTP Input (Hidden initially) -->
                        <div id="otp-input-section" class="hidden">
                            <div class="mb-4">
                                <label for="otp-code" class="block text-sm font-medium text-gray-700 mb-2">Enter OTP</label>
                                <input type="text" id="otp-code" maxlength="6" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500 text-center text-xl font-mono" placeholder="123456">
                                <div class="text-center mt-2">
                                    <span class="text-sm text-gray-600">Demo OTP: <strong>123456</strong></span>
                                </div>
                            </div>
                            <button type="button" id="verify-otp-btn" class="w-full bg-green-500 hover:bg-green-600 text-white py-3 rounded-md transition-colors font-medium">
                                ✅ Verify OTP
                            </button>
                        </div>
                    </form>

                    <!-- Action Buttons -->
                    <div class="flex space-x-4 mb-4">
                        <button type="button" id="close-modal" class="flex-1 bg-gray-200 hover:bg-gray-300 text-gray-700 py-2 rounded-md transition-colors">
                            Cancel
                        </button>
                    </div>
                    
                    <div class="text-center">
                        <p class="text-gray-600 mb-2">Don't have an account?</p>
                        <button type="button" id="register-btn" class="w-full bg-yellow-500 hover:bg-yellow-600 text-white py-2 rounded-md transition-colors">
                            Register New Account
                        </button>
                    </div>
                </div>
            `;
            
            document.body.appendChild(modal);
            
            // Tab switching functionality
            const emailTab = document.getElementById('email-login-tab');
            const mobileTab = document.getElementById('mobile-login-tab');
            const emailForm = document.getElementById('email-login-form');
            const mobileForm = document.getElementById('mobile-login-form');
            
            function switchToEmailTab() {
                emailTab.classList.add('active');
                mobileTab.classList.remove('active');
                emailForm.classList.remove('hidden');
                mobileForm.classList.add('hidden');
            }
            
            function switchToMobileTab() {
                mobileTab.classList.add('active');
                emailTab.classList.remove('active');
                mobileForm.classList.remove('hidden');
                emailForm.classList.add('hidden');
            }
            
            emailTab.addEventListener('click', switchToEmailTab);
            mobileTab.addEventListener('click', switchToMobileTab);
            
            // Email login form submission
            document.getElementById('email-login-form').addEventListener('submit', function(e) {
                e.preventDefault();
                
                const email = document.getElementById('login-email').value;
                const password = document.getElementById('login-password').value;
                
                try {
                    let user = database.loginUser(email, password);
                    modal.remove();
                    
                    if (user.email === 'princehemanth753@gmail.com') {
                        showSuccessMessage(`Welcome Admin! Redirecting to Admin Dashboard...`);
                        setTimeout(() => showAdminDashboard(user), 2000);
                    } else {
                        showSuccessMessage(`Welcome back, ${user.username}!`);
                        setTimeout(() => showPersonalDashboard(user), 2000);
                    }
                    
                } catch (error) {
                    if (error.message === 'Invalid email or password') {
                        // Check if email exists but password is wrong
                        const existingUser = database.users.find(u => u.email === email);
                        if (existingUser) {
                            showErrorMessage('Incorrect password. Please try again.');
                        } else {
                            // Email not found - prompt to register
                            showErrorMessage('Email not found. Please register first.');
                            setTimeout(() => {
                                modal.remove();
                                showRegisterModal(email); // Pre-fill email in registration
                            }, 2000);
                        }
                    } else {
                        showErrorMessage(error.message);
                    }
                }
            });
            
            // Mobile OTP functionality
            document.getElementById('mobile-login-form').addEventListener('submit', function(e) {
                e.preventDefault();
                
                const mobile = document.getElementById('login-mobile').value;
                if (!mobile || mobile.length < 10) {
                    showErrorMessage('Please enter a valid mobile number');
                    return;
                }
                
                document.getElementById('otp-input-section').classList.remove('hidden');
                document.getElementById('send-otp-btn').textContent = '📲 OTP Sent!';
                document.getElementById('send-otp-btn').disabled = true;
                
                showSuccessMessage('OTP sent to your mobile! Use: 123456');
            });
            
            // Verify OTP
            document.getElementById('verify-otp-btn').addEventListener('click', function() {
                const mobile = document.getElementById('login-mobile').value;
                const otp = document.getElementById('otp-code').value;
                
                if (otp !== '123456') {
                    showErrorMessage('Invalid OTP. Please try again.');
                    return;
                }
                
                // Check if mobile number exists in database
                const existingUser = database.users.find(u => u.phone === mobile);
                
                if (existingUser) {
                    // User exists, log them in
                    database.saveCurrentUser(existingUser);
                    modal.remove();
                    showSuccessMessage(`Welcome back, ${existingUser.username}!`);
                    setTimeout(() => showPersonalDashboard(existingUser), 2000);
                } else {
                    // Mobile number not found - prompt to register
                    modal.remove();
                    showErrorMessage('Mobile number not registered. Please register first.');
                    setTimeout(() => {
                        showRegisterModal('', mobile); // Pre-fill mobile in registration
                    }, 2000);
                }
            });
            
            // Close modal
            document.getElementById('close-modal').addEventListener('click', function() {
                modal.remove();
            });
            
            modal.addEventListener('click', function(e) {
                if (e.target === modal) {
                    modal.remove();
                }
            });
            
            // Register button
            document.getElementById('register-btn').addEventListener('click', function() {
                modal.remove();
                showRegisterModal();
            });
        }

        // Register Modal Function
        function showRegisterModal(prefilledEmail = '', prefilledMobile = '') {
            const modal = document.createElement('div');
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4">
                    <h3 class="text-2xl font-bold text-gray-900 mb-6">Create Your ECOCOIN Account</h3>
                    <form id="register-form">
                        <div class="mb-4">
                            <label for="register-username" class="block text-sm font-medium text-gray-700 mb-2">Username</label>
                            <input type="text" id="register-username" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500" placeholder="Choose a username">
                        </div>
                        <div class="mb-4">
                            <label for="register-email" class="block text-sm font-medium text-gray-700 mb-2">Email (will be used as login)</label>
                            <input type="email" id="register-email" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500" placeholder="Enter your email" value="${prefilledEmail}">
                        </div>
                        <div class="mb-4">
                            <label for="register-phone" class="block text-sm font-medium text-gray-700 mb-2">Phone Number ${prefilledMobile ? '(Required)' : '(Optional)'}</label>
                            <input type="tel" id="register-phone" ${prefilledMobile ? 'required' : ''} class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500" placeholder="Enter phone number" value="${prefilledMobile}">
                        </div>
                        <div class="mb-6">
                            <label for="register-password" class="block text-sm font-medium text-gray-700 mb-2">Password</label>
                            <input type="password" id="register-password" required class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500" placeholder="Create a password">
                        </div>
                        <div class="flex space-x-4 mb-4">
                            <button type="submit" class="flex-1 bg-yellow-500 hover:bg-yellow-600 text-white py-2 rounded-md transition-colors">
                                Create Account
                            </button>
                            <button type="button" id="close-register-modal" class="flex-1 bg-gray-200 hover:bg-gray-300 text-gray-700 py-2 rounded-md transition-colors">
                                Cancel
                            </button>
                        </div>
                        <div class="text-center">
                            <p class="text-gray-600 mb-2">Already have an account?</p>
                            <button type="button" id="back-to-login" class="w-full bg-green-500 hover:bg-green-600 text-white py-2 rounded-md transition-colors">
                                Back to Login
                            </button>
                        </div>
                    </form>
                </div>
            `;
            
            document.body.appendChild(modal);
            
            // Register form submission
            document.getElementById('register-form').addEventListener('submit', function(e) {
                e.preventDefault();
                
                try {
                    const userData = {
                        username: document.getElementById('register-username').value,
                        email: document.getElementById('register-email').value,
                        phone: document.getElementById('register-phone').value,
                        password: document.getElementById('register-password').value
                    };
                    
                    const newUser = database.registerUser(userData);
                    database.saveCurrentUser(newUser);
                    modal.remove();
                    
                    if (newUser.email === 'princehemanth753@gmail.com') {
                        showSuccessMessage('Admin account created! Redirecting to Admin Dashboard...');
                        setTimeout(() => showAdminDashboard(newUser), 2000);
                    } else {
                        showSuccessMessage('Account created successfully! Welcome to ECOCOIN!');
                        setTimeout(() => showPersonalDashboard(newUser), 2000);
                    }
                    
                } catch (error) {
                    showErrorMessage(error.message);
                }
            });
            
            // Close register modal
            document.getElementById('close-register-modal').addEventListener('click', function() {
                modal.remove();
            });
            
            modal.addEventListener('click', function(e) {
                if (e.target === modal) {
                    modal.remove();
                }
            });
            
            // Back to login
            document.getElementById('back-to-login').addEventListener('click', function() {
                modal.remove();
                showLoginModal();
            });
        }

        // Personal Dashboard Function
        function showPersonalDashboard(user) {
            document.body.innerHTML = `
                <div class="min-h-screen bg-gradient-to-br from-amber-50 via-green-50 to-emerald-50">
                    <!-- Personal Dashboard Header -->
                    <header class="bg-white shadow-xl border-b-4 border-gradient-to-r from-amber-400 to-green-500">
                        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                            <div class="flex justify-between items-center h-20">
                                <div class="flex items-center">
                                    <div class="text-3xl font-bold text-amber-600 mr-12">
                                        <span class="inline-flex items-center">
                                            <span class="text-yellow-400 text-3xl mr-3">🪙</span>
                                            <span>ECOCOIN</span>
                                        </span>
                                    </div>
                                    <nav class="hidden lg:flex space-x-8">
                                        <a href="#dashboard-home" class="text-gray-700 hover:text-amber-600 font-semibold text-lg transition-all duration-300 hover:scale-105">Dashboard</a>
                                        <a href="#recycle-now" class="text-gray-700 hover:text-green-600 font-semibold text-lg transition-all duration-300 hover:scale-105">Recycle Now</a>
                                        <a href="#my-rewards" class="text-gray-700 hover:text-amber-600 font-semibold text-lg transition-all duration-300 hover:scale-105">My Rewards</a>
                                        <a href="#transaction-history" class="text-gray-700 hover:text-green-600 font-semibold text-lg transition-all duration-300 hover:scale-105">History</a>
                                    </nav>
                                </div>
                                <div class="flex items-center space-x-6">
                                    <button onclick="location.reload()" class="bg-gradient-to-r from-green-500 to-emerald-600 hover:from-green-600 hover:to-emerald-700 text-white px-6 py-3 rounded-xl transition-all duration-300 font-semibold transform hover:scale-105 hover:shadow-lg">
                                        🏠 Back to Main Site
                                    </button>
                                    <div class="text-right">
                                        <div class="text-amber-600 font-bold text-lg">${user.username}</div>
                                        <div class="text-sm text-gray-500">${user.email}</div>
                                    </div>
                                    <div class="bg-gradient-to-r from-amber-100 to-green-100 rounded-full p-4 transform hover:scale-110 transition-all duration-300">
                                        <div class="text-3xl">👤</div>
                                    </div>
                                    <button onclick="database.logoutUser(); location.reload();" class="bg-gradient-to-r from-red-500 to-red-600 hover:from-red-600 hover:to-red-700 text-white px-6 py-3 rounded-xl transition-all duration-300 font-semibold transform hover:scale-105 hover:shadow-lg">
                                        🚪 Logout
                                    </button>
                                </div>
                            </div>
                        </div>
                    </header>

                    <!-- Personal Dashboard Content -->
                    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
                        <!-- Welcome Section -->
                        <div class="mb-8 text-center">
                            <h1 class="text-4xl font-bold bg-gradient-to-r from-amber-600 to-green-600 bg-clip-text text-transparent mb-4">Welcome back, ${user.username}! 👋</h1>
                            <p class="text-xl text-gray-600 font-medium">Track your eco-impact and manage your rewards</p>
                        </div>



                        <!-- Eco-Wallet Overview -->
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                            <div class="bg-gradient-to-r from-amber-400 to-yellow-500 rounded-xl p-6 text-white transform hover:scale-105 transition-all duration-300 cursor-pointer">
                                <div class="flex items-center justify-between">
                                    <div>
                                        <div class="text-3xl font-bold mb-2">${user.ecoCoins}</div>
                                        <div class="text-amber-100 text-lg font-semibold">Eco-Coins Balance</div>
                                    </div>
                                    <div class="text-5xl opacity-80">🪙</div>
                                </div>
                            </div>
                            <div class="bg-gradient-to-r from-green-500 to-emerald-600 rounded-xl p-6 text-white transform hover:scale-105 transition-all duration-300 cursor-pointer">
                                <div class="flex items-center justify-between">
                                    <div>
                                        <div class="text-3xl font-bold mb-2">${user.devicesRecycled}</div>
                                        <div class="text-green-100 text-lg font-semibold">Devices Recycled</div>
                                    </div>
                                    <div class="text-5xl opacity-80">📱</div>
                                </div>
                            </div>
                            <div class="bg-gradient-to-r from-blue-500 to-cyan-600 rounded-xl p-6 text-white transform hover:scale-105 transition-all duration-300 cursor-pointer">
                                <div class="flex items-center justify-between">
                                    <div>
                                        <div class="text-3xl font-bold mb-2">${user.co2Saved} kg</div>
                                        <div class="text-blue-100 text-lg font-semibold">CO₂ Saved</div>
                                    </div>
                                    <div class="text-5xl opacity-80">🌍</div>
                                </div>
                            </div>
                        </div>

                        <!-- Quick Actions -->
                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-6 mb-8">
                            <button onclick="simulateRecycling()" class="bg-white rounded-xl p-6 shadow-lg hover:shadow-xl transition-all duration-300 text-center transform hover:scale-110 hover:-translate-y-2 group">
                                <div class="text-5xl mb-3 group-hover:scale-125 transition-transform duration-300">📱</div>
                                <div class="font-bold text-gray-900 mb-2 text-lg">Recycle Device</div>
                                <div class="text-gray-600 text-sm">Simulate recycling process</div>
                            </button>
                            <button onclick="showDumpingOptions()" class="bg-white rounded-xl p-6 shadow-lg hover:shadow-xl transition-all duration-300 text-center transform hover:scale-110 hover:-translate-y-2 group">
                                <div class="text-5xl mb-3 group-hover:scale-125 transition-transform duration-300">🗑️</div>
                                <div class="font-bold text-gray-900 mb-2 text-lg">Dump Waste</div>
                                <div class="text-gray-600 text-sm">Plastic bottles & E-waste</div>
                            </button>
                            <button onclick="showRewards()" class="bg-white rounded-xl p-6 shadow-lg hover:shadow-xl transition-all duration-300 text-center transform hover:scale-110 hover:-translate-y-2 group">
                                <div class="text-5xl mb-3 group-hover:scale-125 transition-transform duration-300">🎁</div>
                                <div class="font-bold text-gray-900 mb-2 text-lg">View Rewards</div>
                                <div class="text-gray-600 text-sm">Redeem your eco-coins</div>
                            </button>
                            <button onclick="earnBonus()" class="bg-white rounded-xl p-6 shadow-lg hover:shadow-xl transition-all duration-300 text-center transform hover:scale-110 hover:-translate-y-2 group">
                                <div class="text-5xl mb-3 group-hover:scale-125 transition-transform duration-300">💰</div>
                                <div class="font-bold text-gray-900 mb-2 text-lg">Earn Bonus</div>
                                <div class="text-gray-600 text-sm">Daily check-in rewards</div>
                            </button>
                            <button onclick="inviteFriends()" class="bg-white rounded-xl p-6 shadow-lg hover:shadow-xl transition-all duration-300 text-center transform hover:scale-110 hover:-translate-y-2 group">
                                <div class="text-5xl mb-3 group-hover:scale-125 transition-transform duration-300">👥</div>
                                <div class="font-bold text-gray-900 mb-2 text-lg">Invite Friends</div>
                                <div class="text-gray-600 text-sm">Earn referral bonuses</div>
                            </button>
                        </div>

                        <!-- Environmental Impact -->
                        <div class="bg-gradient-to-r from-green-500 via-emerald-500 to-teal-500 rounded-2xl p-8 text-white transform hover:scale-[1.02] transition-all duration-300 hover:shadow-xl">
                            <h3 class="text-3xl font-bold mb-6 text-center">🌍 Your Environmental Impact</h3>
                            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 text-center">
                                <div class="transform hover:scale-110 transition-all duration-300 cursor-pointer">
                                    <div class="text-5xl mb-3 hover:rotate-12 transition-transform duration-300">🌳</div>
                                    <div class="text-3xl font-bold mb-2">${Math.floor(user.co2Saved / 10)}</div>
                                    <div class="text-green-100 text-lg font-semibold">Trees Equivalent</div>
                                </div>
                                <div class="transform hover:scale-110 transition-all duration-300 cursor-pointer">
                                    <div class="text-5xl mb-3 hover:rotate-12 transition-transform duration-300">⚡</div>
                                    <div class="text-3xl font-bold mb-2">${Math.floor(user.devicesRecycled * 2.5)} kWh</div>
                                    <div class="text-green-100 text-lg font-semibold">Energy Saved</div>
                                </div>
                                <div class="transform hover:scale-110 transition-all duration-300 cursor-pointer">
                                    <div class="text-5xl mb-3 hover:rotate-12 transition-transform duration-300">💧</div>
                                    <div class="text-3xl font-bold mb-2">${Math.floor(user.devicesRecycled * 15)} L</div>
                                    <div class="text-green-100 text-lg font-semibold">Water Saved</div>
                                </div>
                            </div>
                        </div>
                    </main>
                </div>
            `;
        }

        // Admin Dashboard Function
        function showAdminDashboard(user) {
            const allUsers = database.users;
            const totalUsers = allUsers.length;
            const totalCoins = allUsers.reduce((sum, u) => sum + u.ecoCoins, 0);
            const totalDevices = allUsers.reduce((sum, u) => sum + u.devicesRecycled, 0);
            const totalCO2 = allUsers.reduce((sum, u) => sum + u.co2Saved, 0);

            document.body.innerHTML = `
                <div class="min-h-screen bg-gradient-to-br from-yellow-50 via-orange-50 to-red-50">
                    <!-- Admin Header -->
                    <header class="bg-white shadow-xl border-b-4 border-yellow-500">
                        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                            <div class="flex justify-between items-center h-20">
                                <div class="flex items-center">
                                    <div class="text-2xl font-bold text-yellow-600 mr-8">
                                        <span class="inline-flex items-center">
                                            <span class="text-yellow-400 text-2xl mr-2">🪙</span>
                                            <span>ECOCOIN</span>
                                            <span class="ml-2 text-sm bg-red-100 text-red-800 px-2 py-1 rounded">ADMIN</span>
                                        </span>
                                    </div>
                                    <nav class="hidden md:flex space-x-6">
                                        <a href="#admin-dashboard" class="text-gray-700 hover:text-yellow-600 font-medium">Dashboard</a>
                                        <a href="#user-management" class="text-gray-700 hover:text-yellow-600 font-medium">
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'990aa29610173d28',t:'MTc2MDgxNzc2NS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script>
