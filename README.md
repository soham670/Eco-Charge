# Eco-Charge
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EcoCharge - Find EV Charging Stations Near You</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Montserrat', sans-serif;
            scroll-behavior: smooth;
        }
        
        .gradient-bg {
            background: linear-gradient(135deg, #34d399 0%, #0ea5e9 100%);
        }
        
        .subscription-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        
        .map-container {
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='600' height='400' viewBox='0 0 600 400'%3E%3Crect width='600' height='400' fill='%23e5e7eb'/%3E%3Cpath d='M100,100 L500,100 L500,300 L100,300 Z' fill='%23d1d5db' stroke='%239ca3af' stroke-width='2'/%3E%3Ccircle cx='250' cy='200' r='10' fill='%230ea5e9'/%3E%3Ccircle cx='350' cy='150' r='10' fill='%2334d399'/%3E%3Ccircle cx='180' cy='250' r='10' fill='%2334d399'/%3E%3Ccircle cx='400' cy='220' r='10' fill='%2334d399'/%3E%3Ccircle cx='300' cy='200' r='15' fill='%23f97316' stroke='%23fff' stroke-width='3'/%3E%3C/svg%3E");
            background-size: cover;
            background-position: center;
        }
        
        .booking-modal {
            transition: opacity 0.3s ease, visibility 0.3s ease;
        }
        
        .notification {
            transform: translateX(100%);
            transition: transform 0.5s ease;
        }
        
        .notification.show {
            transform: translateX(0);
        }
        
        .station-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        
        .review-card {
            transition: all 0.3s ease;
        }
        
        .review-card:hover {
            transform: translateY(-5px);
        }
        
        .star-rating input {
            display: none;
        }
        
        .star-rating label {
            cursor: pointer;
            transition: color 0.2s ease;
        }
        
        .star-rating label:hover,
        .star-rating label:hover ~ label,
        .star-rating input:checked ~ label {
            color: #f59e0b;
        }
        
        .team-member:hover .team-social {
            opacity: 1;
        }
        
        .timeline-item::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 2px;
            background: #34d399;
        }
        
        .timeline-dot {
            position: absolute;
            left: -9px;
            top: 0;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: #34d399;
            border: 4px solid white;
        }
        
        .plan-feature {
            display: flex;
            align-items: center;
            margin-bottom: 0.5rem;
        }
        
        .plan-feature svg {
            flex-shrink: 0;
            margin-right: 0.5rem;
        }
        
        .plan-comparison-table th,
        .plan-comparison-table td {
            padding: 0.75rem 1rem;
            text-align: center;
        }
        
        .plan-comparison-table tbody tr:nth-child(odd) {
            background-color: rgba(243, 244, 246, 0.5);
        }
        
        .weekly-plan-card {
            transition: all 0.3s ease;
        }
        
        .weekly-plan-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Navigation -->
    <nav class="bg-white shadow-md sticky top-0 z-50">
        <div class="container mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <svg class="w-10 h-10" viewBox="0 0 50 50" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <circle cx="25" cy="25" r="23" fill="#34d399" stroke="#0ea5e9" stroke-width="4"/>
                    <path d="M25,10 L25,30 M25,30 L18,23 M25,30 L32,23" stroke="#fff" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M25,30 C25,38 18,40 18,40 L32,40 C32,40 25,38 25,30z" fill="#f97316" stroke="#fff" stroke-width="2"/>
                </svg>
                <span class="text-2xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-green-500 to-blue-500">EcoCharge</span>
            </div>
            <div class="hidden md:flex space-x-8">
                <a href="#home" class="font-medium text-gray-700 hover:text-green-500 transition">Home</a>
                <a href="#how-it-works" class="font-medium text-gray-700 hover:text-green-500 transition">How It Works</a>
                <a href="#booking" class="font-medium text-gray-700 hover:text-green-500 transition">Book Now</a>
                <a href="#reviews" class="font-medium text-gray-700 hover:text-green-500 transition">Reviews</a>
                <a href="#about-us" class="font-medium text-gray-700 hover:text-green-500 transition">About Us</a>
                <a href="#subscriptions" class="font-medium text-gray-700 hover:text-green-500 transition">Subscriptions</a>
            </div>
            <div class="flex items-center space-x-4">
                <button class="hidden md:block px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition">Sign In</button>
                <button class="px-4 py-2 gradient-bg text-white rounded-lg hover:opacity-90 transition">Get Started</button>
                <button class="md:hidden text-gray-700">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                    </svg>
                </button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="relative overflow-hidden">
        <div class="absolute inset-0 z-0">
            <svg class="w-full h-full" viewBox="0 0 1200 600" xmlns="http://www.w3.org/2000/svg">
                <path d="M0,100 Q300,150 600,100 T1200,150 V600 H0 Z" fill="#e6fffa" opacity="0.5"/>
                <path d="M0,200 Q300,250 600,200 T1200,250 V600 H0 Z" fill="#d1fae5" opacity="0.5"/>
                <path d="M0,300 Q300,350 600,300 T1200,350 V600 H0 Z" fill="#bfdbfe" opacity="0.3"/>
            </svg>
        </div>
        <div class="container mx-auto px-4 py-20 relative z-10">
            <div class="flex flex-col md:flex-row items-center">
                <div class="md:w-1/2 mb-10 md:mb-0">
                    <h1 class="text-4xl md:text-5xl font-bold mb-6 leading-tight">Find & Book EV Charging Stations <span class="bg-clip-text text-transparent bg-gradient-to-r from-green-500 to-blue-500">Near You</span></h1>
                    <p class="text-lg text-gray-600 mb-8">Discover affordable charging stations, book in advance, and save with our subscription plans. The smarter way to keep your EV powered.</p>
                    <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4">
                        <a href="#booking" class="px-8 py-3 gradient-bg text-white rounded-lg hover:opacity-90 transition font-medium text-center">Book a Station Now</a>
                        <a href="#subscriptions" class="px-8 py-3 border-2 border-blue-500 text-blue-500 rounded-lg hover:bg-blue-50 transition font-medium text-center">View Subscription Plans</a>
                    </div>
                </div>
                <div class="md:w-1/2">
                    <svg class="w-full h-auto" viewBox="0 0 600 400" xmlns="http://www.w3.org/2000/svg">
                        <!-- EV Car -->
                        <rect x="100" y="230" width="400" height="70" rx="20" fill="#3b82f6" />
                        <rect x="150" y="180" width="300" height="80" rx="40" fill="#3b82f6" />
                        <circle cx="200" cy="300" r="30" fill="#1f2937" />
                        <circle cx="200" cy="300" r="15" fill="#9ca3af" />
                        <circle cx="400" cy="300" r="30" fill="#1f2937" />
                        <circle cx="400" cy="300" r="15" fill="#9ca3af" />
                        <rect x="450" y="220" width="30" height="20" rx="5" fill="#34d399" />
                        
                        <!-- Charging Station -->
                        <rect x="500" y="150" width="60" height="150" rx="5" fill="#9ca3af" />
                        <rect x="510" y="160" width="40" height="80" rx="3" fill="#1f2937" />
                        <circle cx="530" cy="200" r="15" fill="#34d399" />
                        <rect x="520" y="250" width="20" height="10" rx="2" fill="#34d399" />
                        
                        <!-- Charging Cable -->
                        <path d="M480,230 Q500,200 520,230" stroke="#1f2937" stroke-width="8" fill="none" />
                        
                        <!-- Trees -->
                        <circle cx="80" cy="200" r="30" fill="#34d399" />
                        <rect x="75" y="230" width="10" height="70" fill="#7c3aed" />
                        <circle cx="40" cy="180" r="20" fill="#34d399" />
                        <rect x="35" y="200" width="10" height="100" fill="#7c3aed" />
                        
                        <!-- Sun -->
                        <circle cx="100" cy="80" r="30" fill="#f97316" />
                        <line x1="100" y1="30" x2="100" y2="10" stroke="#f97316" stroke-width="4" />
                        <line x1="100" y1="130" x2="100" y2="150" stroke="#f97316" stroke-width="4" />
                        <line x1="50" y1="80" x2="30" y2="80" stroke="#f97316" stroke-width="4" />
                        <line x1="150" y1="80" x2="170" y2="80" stroke="#f97316" stroke-width="4" />
                        <line x1="65" y1="45" x2="50" y2="30" stroke="#f97316" stroke-width="4" />
                        <line x1="135" y1="115" x2="150" y2="130" stroke="#f97316" stroke-width="4" />
                        <line x1="65" y1="115" x2="50" y2="130" stroke="#f97316" stroke-width="4" />
                        <line x1="135" y1="45" x2="150" y2="30" stroke="#f97316" stroke-width="4" />
                    </svg>
                </div>
            </div>
        </div>
    </section>

    <!-- Search Section -->
    <section class="py-10 bg-white">
        <div class="container mx-auto px-4">
            <div class="max-w-4xl mx-auto bg-white rounded-xl shadow-lg p-6 -mt-20 relative z-20">
                <h2 class="text-2xl font-semibold mb-6 text-center">Find Charging Stations Near You</h2>
                <div class="flex flex-col md:flex-row space-y-4 md:space-y-0 md:space-x-4">
                    <div class="flex-1">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Location</label>
                        <input type="text" placeholder="Enter your location" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition">
                    </div>
                    <div class="md:w-1/4">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Radius</label>
                        <select class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition">
                            <option>5 km</option>
                            <option>10 km</option>
                            <option>20 km</option>
                            <option>50 km</option>
                        </select>
                    </div>
                    <div class="md:w-1/4">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Connector Type</label>
                        <select class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition">
                            <option>Any Type</option>
                            <option>Type 2</option>
                            <option>CCS</option>
                            <option>CHAdeMO</option>
                        </select>
                    </div>
                    <div class="md:w-1/6 flex items-end">
                        <button class="w-full px-4 py-2 gradient-bg text-white rounded-lg hover:opacity-90 transition">Search</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- How It Works -->
    <section id="how-it-works" class="py-20 bg-gray-50">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl font-bold mb-4">How EcoCharge Works</h2>
                <p class="text-lg text-gray-600 max-w-2xl mx-auto">Our platform makes finding and booking EV charging stations simple, affordable, and convenient.</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div class="bg-white p-8 rounded-xl shadow-md text-center">
                    <div class="w-20 h-20 gradient-bg rounded-full flex items-center justify-center mx-auto mb-6">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                        </svg>
                    </div>
                    <h3 class="text-xl font-semibold mb-3">Find Nearby Stations</h3>
                    <p class="text-gray-600">Locate available charging stations near you with real-time availability and pricing information.</p>
                </div>
                
                <div class="bg-white p-8 rounded-xl shadow-md text-center">
                    <div class="w-20 h-20 gradient-bg rounded-full flex items-center justify-center mx-auto mb-6">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                        </svg>
                    </div>
                    <h3 class="text-xl font-semibold mb-3">Book in Advance</h3>
                    <p class="text-gray-600">Reserve your charging slot ahead of time to ensure availability when you need it most.</p>
                </div>
                
                <div class="bg-white p-8 rounded-xl shadow-md text-center">
                    <div class="w-20 h-20 gradient-bg rounded-full flex items-center justify-center mx-auto mb-6">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                    </div>
                    <h3 class="text-xl font-semibold mb-3">Get Confirmation</h3>
                    <p class="text-gray-600">Receive instant booking confirmations and reminders for your upcoming charging sessions.</p>
                </div>
                
                <div class="bg-white p-8 rounded-xl shadow-md text-center">
                    <div class="w-20 h-20 gradient-bg rounded-full flex items-center justify-center mx-auto mb-6">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                        </svg>
                    </div>
                    <h3 class="text-xl font-semibold mb-3">Save with Subscriptions</h3>
                    <p class="text-gray-600">Choose from our weekly, monthly, or yearly plans to save money on your regular charging needs.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Booking Section -->
    <section id="booking" class="py-20 bg-white">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl font-bold mb-4">Book a Charging Station</h2>
                <p class="text-lg text-gray-600 max-w-2xl mx-auto">Find and reserve your charging slot in just a few clicks. Both you and the station owner will receive instant confirmations.</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Station 1 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden transition-all duration-300 station-card">
                    <div class="relative">
                        <div class="h-48 bg-gray-200 flex items-center justify-center">
                            <svg class="w-full h-full" viewBox="0 0 400 200" xmlns="http://www.w3.org/2000/svg">
                                <!-- Station Building -->
                                <rect x="100" y="50" width="200" height="100" fill="#e5e7eb" />
                                <rect x="110" y="60" width="180" height="90" fill="#f3f4f6" />
                                
                                <!-- Roof -->
                                <polygon points="100,50 200,20 300,50" fill="#d1d5db" />
                                
                                <!-- Door -->
                                <rect x="180" y="110" width="40" height="40" fill="#9ca3af" />
                                
                                <!-- Charging Points -->
                                <rect x="120" y="150" width="20" height="30" fill="#9ca3af" />
                                <rect x="150" y="150" width="20" height="30" fill="#9ca3af" />
                                <rect x="230" y="150" width="20" height="30" fill="#9ca3af" />
                                <rect x="260" y="150" width="20" height="30" fill="#9ca3af" />
                                
                                <!-- Charging Indicators -->
                                <circle cx="130" cy="160" r="5" fill="#34d399" />
                                <circle cx="160" cy="160" r="5" fill="#f97316" />
                                <circle cx="240" cy="160" r="5" fill="#34d399" />
                                <circle cx="270" cy="160" r="5" fill="#f97316" />
                                
                                <!-- Car -->
                                <rect x="30" y="140" width="60" height="20" rx="5" fill="#3b82f6" />
                                <rect x="40" y="130" width="40" height="15" rx="5" fill="#3b82f6" />
                                <circle cx="45" cy="160" r="8" fill="#1f2937" />
                                <circle cx="75" cy="160" r="8" fill="#1f2937" />
                            </svg>
                        </div>
                        <div class="absolute top-4 right-4 bg-green-500 text-white text-xs font-bold px-3 py-1 rounded-full">AVAILABLE</div>
                    </div>
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-4">
                            <div>
                                <h3 class="text-xl font-semibold">Green Energy Hub</h3>
                                <p class="text-gray-500">Connaught Place, Delhi</p>
                            </div>
                            <div class="flex items-center">
                                <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                                    <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                                </svg>
                                <span class="ml-1 font-medium">4.8</span>
                                <span class="ml-1 text-gray-500">(124)</span>
                            </div>
                        </div>
                        <div class="flex flex-wrap gap-2 mb-4">
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">Type 2</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">CCS</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">22kW</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">50kW DC</span>
                        </div>
                        <div class="flex justify-between items-center mb-4">
                            <div>
                                <p class="text-sm text-gray-500">Price</p>
                                <p class="text-lg font-semibold">₹15/kWh</p>
                            </div>
                            <div>
                                <p class="text-sm text-gray-500">Distance</p>
                                <p class="text-lg font-semibold">2.5 km</p>
                            </div>
                            <div>
                                <p class="text-sm text-gray-500">Open</p>
                                <p class="text-lg font-semibold">24/7</p>
                            </div>
                        </div>
                        <div class="flex space-x-2">
                            <button onclick="openBookingModal('Green Energy Hub', 'Connaught Place, Delhi')" class="flex-1 py-3 gradient-bg text-white rounded-lg hover:opacity-90 transition font-medium">Book Now</button>
                            <button onclick="openReviewModal('Green Energy Hub')" class="px-4 py-3 border-2 border-blue-500 text-blue-500 rounded-lg hover:bg-blue-50 transition">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
                
                <!-- Station 2 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden transition-all duration-300 station-card">
                    <div class="relative">
                        <div class="h-48 bg-gray-200 flex items-center justify-center">
                            <svg class="w-full h-full" viewBox="0 0 400 200" xmlns="http://www.w3.org/2000/svg">
                                <!-- Mall Building -->
                                <rect x="50" y="30" width="300" height="120" fill="#e5e7eb" />
                                <rect x="60" y="40" width="280" height="110" fill="#f3f4f6" />
                                
                                <!-- Windows -->
                                <rect x="80" y="60" width="40" height="30" fill="#bfdbfe" />
                                <rect x="130" y="60" width="40" height="30" fill="#bfdbfe" />
                                <rect x="180" y="60" width="40" height="30" fill="#bfdbfe" />
                                <rect x="230" y="60" width="40" height="30" fill="#bfdbfe" />
                                <rect x="280" y="60" width="40" height="30" fill="#bfdbfe" />
                                
                                <!-- Door -->
                                <rect x="175" y="110" width="50" height="40" fill="#9ca3af" />
                                
                                <!-- Parking Area -->
                                <rect x="50" y="150" width="300" height="30" fill="#d1d5db" />
                                
                                <!-- Charging Points -->
                                <rect x="70" y="155" width="20" height="20" fill="#9ca3af" />
                                <rect x="100" y="155" width="20" height="20" fill="#9ca3af" />
                                <rect x="280" y="155" width="20" height="20" fill="#9ca3af" />
                                <rect x="310" y="155" width="20" height="20" fill="#9ca3af" />
                                
                                <!-- Charging Indicators -->
                                <circle cx="80" cy="165" r="5" fill="#34d399" />
                                <circle cx="110" cy="165" r="5" fill="#f97316" />
                                <circle cx="290" cy="165" r="5" fill="#34d399" />
                                <circle cx="320" cy="165" r="5" fill="#f97316" />
                                
                                <!-- Mall Sign -->
                                <rect x="150" y="20" width="100" height="20" fill="#3b82f6" />
                                <text x="200" y="35" font-size="14" text-anchor="middle" fill="white" font-weight="bold">MALL</text>
                            </svg>
                        </div>
                        <div class="absolute top-4 right-4 bg-green-500 text-white text-xs font-bold px-3 py-1 rounded-full">AVAILABLE</div>
                    </div>
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-4">
                            <div>
                                <h3 class="text-xl font-semibold">City Center Mall</h3>
                                <p class="text-gray-500">Bandra, Mumbai</p>
                            </div>
                            <div class="flex items-center">
                                <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                                    <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                                </svg>
                                <span class="ml-1 font-medium">4.6</span>
                                <span class="ml-1 text-gray-500">(89)</span>
                            </div>
                        </div>
                        <div class="flex flex-wrap gap-2 mb-4">
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">Type 2</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">CHAdeMO</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">11kW</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">Free Parking</span>
                        </div>
                        <div class="flex justify-between items-center mb-4">
                            <div>
                                <p class="text-sm text-gray-500">Price</p>
                                <p class="text-lg font-semibold">₹18/kWh</p>
                            </div>
                            <div>
                                <p class="text-sm text-gray-500">Distance</p>
                                <p class="text-lg font-semibold">4.2 km</p>
                            </div>
                            <div>
                                <p class="text-sm text-gray-500">Open</p>
                                <p class="text-lg font-semibold">10AM-10PM</p>
                            </div>
                        </div>
                        <div class="flex space-x-2">
                            <button onclick="openBookingModal('City Center Mall', 'Bandra, Mumbai')" class="flex-1 py-3 gradient-bg text-white rounded-lg hover:opacity-90 transition font-medium">Book Now</button>
                            <button onclick="openReviewModal('City Center Mall')" class="px-4 py-3 border-2 border-blue-500 text-blue-500 rounded-lg hover:bg-blue-50 transition">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
                
                <!-- Station 3 -->
                <div class="bg-white rounded-xl shadow-lg overflow-hidden transition-all duration-300 station-card">
                    <div class="relative">
                        <div class="h-48 bg-gray-200 flex items-center justify-center">
                            <svg class="w-full h-full" viewBox="0 0 400 200" xmlns="http://www.w3.org/2000/svg">
                                <!-- Gas Station Building -->
                                <rect x="150" y="50" width="100" height="80" fill="#e5e7eb" />
                                <rect x="160" y="60" width="80" height="70" fill="#f3f4f6" />
                                
                                <!-- Roof -->
                                <polygon points="150,50 200,30 250,50" fill="#d1d5db" />
                                
                                <!-- Door -->
                                <rect x="185" y="90" width="30" height="40" fill="#9ca3af" />
                                
                                <!-- Gas Pumps -->
                                <rect x="80" y="80" width="40" height="60" fill="#9ca3af" />
                                <rect x="280" y="80" width="40" height="60" fill="#9ca3af" />
                                
                                <!-- Canopy -->
                                <rect x="50" y="40" width="300" height="10" fill="#d1d5db" />
                                <rect x="60" y="30" width="280" height="10" fill="#9ca3af" />
                                
                                <!-- EV Charging Points -->
                                <rect x="80" y="150" width="20" height="30" fill="#34d399" />
                                <rect x="110" y="150" width="20" height="30" fill="#34d399" />
                                <rect x="270" y="150" width="20" height="30" fill="#34d399" />
                                <rect x="300" y="150" width="20" height="30" fill="#34d399" />
                                
                                <!-- Charging Indicators -->
                                <circle cx="90" cy="160" r="5" fill="#34d399" />
                                <circle cx="120" cy="160" r="5" fill="#f97316" />
                                <circle cx="280" cy="160" r="5" fill="#34d399" />
                                <circle cx="310" cy="160" r="5" fill="#f97316" />
                                
                                <!-- Car -->
                                <rect x="270" y="120" width="60" height="20" rx="5" fill="#3b82f6" />
                                <rect x="280" y="110" width="40" height="15" rx="5" fill="#3b82f6" />
                                <circle cx="285" cy="140" r="8" fill="#1f2937" />
                                <circle cx="315" cy="140" r="8" fill="#1f2937" />
                            </svg>
                        </div>
                        <div class="absolute top-4 right-4 bg-orange-500 text-white text-xs font-bold px-3 py-1 rounded-full">BUSY</div>
                    </div>
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-4">
                            <div>
                                <h3 class="text-xl font-semibold">Highway Energy Point</h3>
                                <p class="text-gray-500">Electronic City, Bangalore</p>
                            </div>
                            <div class="flex items-center">
                                <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                                    <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                                </svg>
                                <span class="ml-1 font-medium">4.9</span>
                                <span class="ml-1 text-gray-500">(156)</span>
                            </div>
                        </div>
                        <div class="flex flex-wrap gap-2 mb-4">
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">CCS</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">CHAdeMO</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">120kW DC</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">Cafe</span>
                        </div>
                        <div class="flex justify-between items-center mb-4">
                            <div>
                                <p class="text-sm text-gray-500">Price</p>
                                <p class="text-lg font-semibold">₹20/kWh</p>
                            </div>
                            <div>
                                <p class="text-sm text-gray-500">Distance</p>
                                <p class="text-lg font-semibold">8.7 km</p>
                            </div>
                            <div>
                                <p class="text-sm text-gray-500">Open</p>
                                <p class="text-lg font-semibold">24/7</p>
                            </div>
                        </div>
                        <div class="flex space-x-2">
                            <button onclick="openBookingModal('Highway Energy Point', 'Electronic City, Bangalore')" class="flex-1 py-3 gradient-bg text-white rounded-lg hover:opacity-90 transition font-medium">Book Now</button>
                            <button onclick="openReviewModal('Highway Energy Point')" class="px-4 py-3 border-2 border-blue-500 text-blue-500 rounded-lg hover:bg-blue-50 transition">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="mt-12 text-center">
                <button class="px-8 py-3 border-2 border-blue-500 text-blue-500 rounded-lg hover:bg-blue-50 transition font-medium">View More Stations</button>
            </div>
        </div>
    </section>

    <!-- Reviews Section -->
    <section id="reviews" class="py-20 bg-gray-50">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl font-bold mb-4">Customer Reviews</h2>
                <p class="text-lg text-gray-600 max-w-2xl mx-auto">See what our users have to say about their charging experiences across India.</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-12">
                <!-- Review 1 -->
                <div class="bg-white p-6 rounded-xl shadow-md review-card">
                    <div class="flex items-center mb-4">
                        <div class="w-12 h-12 rounded-full bg-blue-100 flex items-center justify-center text-blue-500 font-bold text-xl mr-4">
                            RK
                        </div>
                        <div>
                            <h4 class="font-semibold">Rahul Kumar</h4>
                            <p class="text-gray-500 text-sm">Delhi • Tata Nexon EV</p>
                        </div>
                    </div>
                    <div class="flex mb-3">
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                    </div>
                    <h5 class="font-semibold mb-2">Game changer for EV owners!</h5>
                    <p class="text-gray-600 mb-4">The booking system is so convenient. I never have to worry about finding an available charging station anymore. The instant confirmations give me peace of mind.</p>
                    <div class="flex justify-between items-center">
                        <span class="text-sm text-gray-500">Green Energy Hub</span>
                        <span class="text-sm text-gray-500">2 weeks ago</span>
                    </div>
                </div>
                
                <!-- Review 2 -->
                <div class="bg-white p-6 rounded-xl shadow-md review-card">
                    <div class="flex items-center mb-4">
                        <div class="w-12 h-12 rounded-full bg-green-100 flex items-center justify-center text-green-500 font-bold text-xl mr-4">
                            SP
                        </div>
                        <div>
                            <h4 class="font-semibold">Sneha Patel</h4>
                            <p class="text-gray-500 text-sm">Mumbai • MG ZS EV</p>
                        </div>
                    </div>
                    <div class="flex mb-3">
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-gray-300" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                    </div>
                    <h5 class="font-semibold mb-2">Great subscription value</h5>
                    <p class="text-gray-600 mb-4">The Standard Plan saves me so much money each month. I love that I can book in advance and the station owners are always notified of my arrival time.</p>
                    <div class="flex justify-between items-center">
                        <span class="text-sm text-gray-500">City Center Mall</span>
                        <span class="text-sm text-gray-500">1 month ago</span>
                    </div>
                </div>
                
                <!-- Review 3 -->
                <div class="bg-white p-6 rounded-xl shadow-md review-card">
                    <div class="flex items-center mb-4">
                        <div class="w-12 h-12 rounded-full bg-purple-100 flex items-center justify-center text-purple-500 font-bold text-xl mr-4">
                            VR
                        </div>
                        <div>
                            <h4 class="font-semibold">Vikram Reddy</h4>
                            <p class="text-gray-500 text-sm">Bangalore • Hyundai Kona</p>
                        </div>
                    </div>
                    <div class="flex mb-3">
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                        <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                        </svg>
                    </div>
                    <h5 class="font-semibold mb-2">Perfect for road trips</h5>
                    <p class="text-gray-600 mb-4">I recently drove from Bangalore to Chennai and used EcoCharge to book all my charging stops in advance. The notifications to station owners meant they were always ready for me.</p>
                    <div class="flex justify-between items-center">
                        <span class="text-sm text-gray-500">Highway Energy Point</span>
                        <span class="text-sm text-gray-500">3 days ago</span>
                    </div>
                </div>
            </div>
            
            <!-- Station Owner Review -->
            <div class="max-w-3xl mx-auto bg-white p-8 rounded-xl shadow-md mb-12">
                <div class="flex items-center mb-6">
                    <div class="w-16 h-16 rounded-full bg-orange-100 flex items-center justify-center text-orange-500 font-bold text-2xl mr-5">
                        AM
                    </div>
                    <div>
                        <div class="flex items-center mb-1">
                            <h4 class="font-semibold text-xl">Anand Mehta</h4>
                            <span class="ml-3 px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">Station Owner</span>
                        </div>
                        <p class="text-gray-500">Green Energy Hub, Delhi</p>
                    </div>
                </div>
                <p class="text-gray-600 text-lg mb-6">"As a charging station owner, EcoCharge has increased my daily customers by 40%. The booking system is seamless, and I receive instant notifications when someone books a slot. The platform has made managing my station much more efficient."</p>
                <div class="flex items-center">
                    <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                        <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                    </svg>
                    <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                        <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                    </svg>
                    <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                        <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                    </svg>
                    <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                        <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                    </svg>
                    <svg class="w-5 h-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                        <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                    </svg>
                </div>
            </div>
            
            <div class="text-center">
                <button onclick="openReviewModal('EcoCharge')" class="px-8 py-3 gradient-bg text-white rounded-lg hover:opacity-90 transition font-medium">Write a Review</button>
            </div>
        </div>
    </section>

    <!-- About Us Section -->
    <section id="about-us" class="py-20 bg-white">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl font-bold mb-4">About EcoCharge</h2>
                <p class="text-lg text-gray-600 max-w-2xl mx-auto">We're on a mission to accelerate the adoption of electric vehicles in India by making charging convenient, affordable, and accessible.</p>
            </div>
            
            <div class="flex flex-col md:flex-row items-center mb-20">
                <div class="md:w-1/2 mb-10 md:mb-0">
                    <svg class="w-full h-auto" viewBox="0 0 600 400" xmlns="http://www.w3.org/2000/svg">

                        <!--```
