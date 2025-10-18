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
                    <button onclick="showLoginMessage()" class="nav-link text-white hover:text-green-200 px-4 py-2 rounded-md text-sm font-medium flex items-center">
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
                <button onclick="showLoginMessage()" class="block w-full text-left px-3 py-2 text-gray-700 hover:text-green-600">
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
                    <button onclick="showLoginMessage()" class="bg-yellow-400 hover:bg-yellow-500 text-gray-900 font-bold py-4 px-8 rounded-full text-lg transition-all duration-300 transform hover:scale-105 pulse-green shadow-lg">
                        Get Started
                    </button>
                    <button onclick="showLoginMessage()" class="bg-transparent border-2 border-white text-white hover:bg-white hover:text-green-600 font-bold py-4 px-8 rounded-full text-lg transition-all duration-300 shadow-lg">
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
        // Simple notification system
        function showToast(message, type = 'info') {
            const toast = document.createElement('div');
            const bgColor = type === 'success' ? 'bg-green-500' : type === 'error' ? 'bg-red-500' : 'bg-blue-500';
            const icon = type === 'success' ? '✅' : type === 'error' ? '❌' : 'ℹ️';
            
            toast.className = `fixed top-4 right-4 ${bgColor} text-white px-6 py-3 rounded-lg shadow-lg z-50 transform translate-x-full transition-transform duration-300`;
            toast.innerHTML = `
                <div class="flex items-center space-x-2">
                    <span>${icon}</span>
                    <span>${message}</span>
                </div>
            `;
            
            document.body.appendChild(toast);
            
            setTimeout(() => {
                toast.style.transform = 'translateX(0)';
            }, 100);
            
            setTimeout(() => {
                toast.style.transform = 'translateX(100%)';
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }

        // Simple login message
        function showLoginMessage() {
            showToast('Login feature coming soon! Stay tuned for updates.', 'info');
        }

        // Notification modals
        function showNotifyModal() {
            const modal = document.createElement('div');
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="bg-white rounded-lg p-6 max-w-md mx-4">
                    <h3 class="text-xl font-bold mb-4">📧 Get Notified</h3>
                    <p class="text-gray-600 mb-4">Enter your email to be notified when ECOCOIN machines are available in your area.</p>
                    <input type="email" placeholder="Enter your email" class="w-full px-3 py-2 border rounded-md mb-4">
                    <div class="flex space-x-3">
                        <button onclick="this.closest('.fixed').remove()" class="flex-1 bg-gray-300 text-gray-700 py-2 rounded-md">Cancel</button>
                        <button onclick="showToast('Thank you! We\\'ll notify you soon.', 'success'); this.closest('.fixed').remove()" class="flex-1 bg-blue-500 text-white py-2 rounded-md">Notify Me</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

        function showPartnerModal() {
            const modal = document.createElement('div');
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="bg-white rounded-lg p-6 max-w-md mx-4">
                    <h3 class="text-xl font-bold mb-4">🤝 Partner With Us</h3>
                    <p class="text-gray-600 mb-4">Interested in hosting an ECOCOIN machine at your location?</p>
                    <input type="text" placeholder="Your name" class="w-full px-3 py-2 border rounded-md mb-3">
                    <input type="email" placeholder="Your email" class="w-full px-3 py-2 border rounded-md mb-3">
                    <input type="text" placeholder="Location/Business name" class="w-full px-3 py-2 border rounded-md mb-4">
                    <div class="flex space-x-3">
                        <button onclick="this.closest('.fixed').remove()" class="flex-1 bg-gray-300 text-gray-700 py-2 rounded-md">Cancel</button>
                        <button onclick="showToast('Thank you! We\\'ll contact you soon.', 'success'); this.closest('.fixed').remove()" class="flex-1 bg-green-500 text-white py-2 rounded-md">Submit</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

        function showNotifyRewardsModal() {
            const modal = document.createElement('div');
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="bg-white rounded-lg p-6 max-w-md mx-4">
                    <h3 class="text-xl font-bold mb-4">🎁 Rewards Coming Soon</h3>
                    <p class="text-gray-600 mb-4">Be the first to know when our reward system launches!</p>
                    <input type="email" placeholder="Enter your email" class="w-full px-3 py-2 border rounded-md mb-4">
                    <div class="flex space-x-3">
                        <button onclick="this.closest('.fixed').remove()" class="flex-1 bg-gray-300 text-gray-700 py-2 rounded-md">Cancel</button>
                        <button onclick="showToast('Thank you! We\\'ll notify you when rewards are available.', 'success'); this.closest('.fixed').remove()" class="flex-1 bg-yellow-500 text-white py-2 rounded-md">Notify Me</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

        function showNotifyMarketplaceModal() {
            const modal = document.createElement('div');
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="bg-white rounded-lg p-6 max-w-md mx-4">
                    <h3 class="text-xl font-bold mb-4">🛒 Marketplace Coming Soon</h3>
                    <p class="text-gray-600 mb-4">Get notified when our eco-friendly marketplace launches!</p>
                    <input type="email" placeholder="Enter your email" class="w-full px-3 py-2 border rounded-md mb-4">
                    <div class="flex space-x-3">
                        <button onclick="this.closest('.fixed').remove()" class="flex-1 bg-gray-300 text-gray-700 py-2 rounded-md">Cancel</button>
                        <button onclick="showToast('Thank you! We\\'ll notify you when the marketplace is ready.', 'success'); this.closest('.fixed').remove()" class="flex-1 bg-green-500 text-white py-2 rounded-md">Notify Me</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
        }

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
                    // Close mobile menu if open
                    document.getElementById('mobile-menu').classList.add('hidden');
                }
            });
        });

        // Contact form submission
        document.getElementById('contact-form').addEventListener('submit', function(e) {
            e.preventDefault();
            showToast('Thank you for your message! We\'ll get back to you soon.', 'success');
            this.reset();
        });

        // Animate counters when dashboard section is visible
        function animateCounters() {
            const counters = [
                { id: 'total-waste', target: 0 },
                { id: 'co2-saved', target: 0 },
                { id: 'active-users', target: 0 },
                { id: 'machines', target: 0 }
            ];

            counters.forEach(counter => {
                const element = document.getElementById(counter.id);
                if (element) {
                    let current = 0;
                    const increment = counter.target / 50;
                    const timer = setInterval(() => {
                        current += increment;
                        if (current >= counter.target) {
                            element.textContent = counter.target;
                            clearInterval(timer);
                        } else {
                            element.textContent = Math.floor(current);
                        }
                    }, 50);
                }
            });
        }

        // Intersection Observer for counter animation
        const dashboardSection = document.getElementById('dashboard');
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    animateCounters();
                    observer.unobserve(entry.target);
                }
            });
        });

        if (dashboardSection) {
            observer.observe(dashboardSection);
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'990ae33971f6ca8c',t:'MTc2MDgyMDQxMi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
