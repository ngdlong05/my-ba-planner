<!DOCTYPE html>
<html lang="vi" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BA Career Pathfinder - Enterprise Edition V5.0</title>
    
    <!-- Libraries -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">

    <!-- Configuration -->
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: { 
                        sans: ['Inter', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace']
                    },
                    colors: {
                        brand: { 50: '#eff6ff', 100: '#dbeafe', 200: '#bfdbfe', 300: '#93c5fd', 400: '#60a5fa', 500: '#3b82f6', 600: '#2563eb', 700: '#1d4ed8', 800: '#1e40af', 900: '#1e3a8a', 950: '#172554' },
                        accent: { 500: '#10b981', 600: '#059669' },
                        dark: { 800: '#1e293b', 900: '#0f172a' }
                    },
                    animation: {
                        'float': 'float 3s ease-in-out infinite',
                        'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'slide-in': 'slideIn 0.3s ease-out forwards'
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-10px)' },
                        },
                        slideIn: {
                            '0%': { transform: 'translateX(20px)', opacity: 0 },
                            '100%': { transform: 'translateX(0)', opacity: 1 }
                        }
                    }
                }
            }
        }
    </script>

    <style>
        :root {
            --glass-border: 1px solid rgba(255, 255, 255, 0.1);
            --glass-bg: rgba(255, 255, 255, 0.9);
            --glass-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.07);
        }
        
        .dark {
            --glass-border: 1px solid rgba(255, 255, 255, 0.05);
            --glass-bg: rgba(15, 23, 42, 0.9);
        }

        body {
            background-color: #f1f5f9;
            transition: background-color 0.3s ease;
        }

        .dark body {
            background-color: #0f172a;
            color: #e2e8f0;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .dark ::-webkit-scrollbar-thumb { background: #475569; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }

        /* Glassmorphism Utilities */
        .glass {
            background: var(--glass-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: var(--glass-border);
            box-shadow: var(--glass-shadow);
        }

        /* Skill Card Hover Effects */
        .skill-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .skill-card:hover {
            transform: translateY(-4px) scale(1.01);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        .dark .skill-card:hover {
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.3);
        }

        /* Print Optimization */
        @media print {
            body { background: white !important; color: black !important; }
            .no-print, #sidebar, #mobile-header, .auth-container, #chatbot-widget { display: none !important; }
            #main-content { margin-left: 0 !important; padding: 0 !important; width: 100% !important; }
            .skill-card { break-inside: avoid; border: 1px solid #ccc; box-shadow: none; }
            .tab-content { display: grid !important; grid-template-columns: 1fr 1fr; gap: 15px; }
            #mermaid-container svg { max-width: 100%; }
        }

        /* Custom Checkbox */
        .custom-checkbox input:checked + div {
            background-color: #2563eb;
            border-color: #2563eb;
        }
        .custom-checkbox input:checked + div svg {
            display: block;
        }
    </style>
</head>
<body class="text-slate-800 antialiased">

    <!-- ==================== AUTH & ONBOARDING ==================== -->
    <div id="auth-screen" class="fixed inset-0 z-[100] flex items-center justify-center bg-slate-50 dark:bg-slate-900 transition-colors duration-500">
        <div class="absolute inset-0 overflow-hidden">
            <div class="absolute -top-[40%] -left-[20%] w-[70%] h-[70%] rounded-full bg-brand-400/20 blur-[120px] animate-float"></div>
            <div class="absolute top-[20%] -right-[20%] w-[60%] h-[60%] rounded-full bg-purple-400/20 blur-[120px] animate-float" style="animation-delay: 2s"></div>
        </div>

        <div class="relative glass w-full max-w-5xl h-[600px] rounded-2xl shadow-2xl flex overflow-hidden animate-scale-in mx-4">
            <!-- Left Side: Login -->
            <div class="w-full md:w-1/2 p-12 flex flex-col justify-center relative z-10 bg-white/50 dark:bg-slate-800/50">
                <div class="mb-8">
                    <div class="inline-flex items-center justify-center w-12 h-12 rounded-xl bg-brand-600 text-white text-xl mb-4 shadow-lg shadow-brand-500/30">
                        <i class="fa-solid fa-compass"></i>
                    </div>
                    <h1 class="text-3xl font-bold text-slate-900 dark:text-white tracking-tight">BA Pathfinder <span class="text-brand-600">Pro</span></h1>
                    <p class="text-slate-500 dark:text-slate-400 mt-2">Nền tảng định hướng sự nghiệp toàn diện dành cho Business Analyst.</p>
                </div>

                <form id="login-form" class="space-y-5">
                    <div>
                        <label class="block text-sm font-medium text-slate-700 dark:text-slate-300 mb-1">Tên của bạn</label>
                        <div class="relative">
                            <i class="fa-regular fa-user absolute left-4 top-3.5 text-slate-400"></i>
                            <input type="text" id="username" required 
                                class="w-full pl-11 pr-4 py-3 rounded-xl border border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-900 focus:ring-2 focus:ring-brand-500 outline-none transition dark:text-white"
                                placeholder="Nhập tên hiển thị...">
                        </div>
                    </div>
                    
                    <button type="submit" class="w-full bg-brand-600 hover:bg-brand-700 text-white font-bold py-3.5 rounded-xl transition shadow-lg shadow-brand-500/20 flex items-center justify-center gap-2 group">
                        <span>Bắt đầu ngay</span> 
                        <i class="fa-solid fa-arrow-right group-hover:translate-x-1 transition-transform"></i>
                    </button>
                </form>

                <div class="mt-8 pt-8 border-t border-slate-200 dark:border-slate-700">
                    <div class="flex items-center gap-4 text-sm text-slate-500 dark:text-slate-400">
                        <span class="flex items-center gap-1"><i class="fa-solid fa-check text-green-500"></i> 50+ Skills</span>
                        <span class="flex items-center gap-1"><i class="fa-solid fa-check text-green-500"></i> Job Matching</span>
                        <span class="flex items-center gap-1"><i class="fa-solid fa-check text-green-500"></i> AI Mentor</span>
                    </div>
                </div>
            </div>

            <!-- Right Side: Hero Image/Graphics -->
            <div class="hidden md:block w-1/2 bg-slate-900 relative overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-brand-600 to-purple-700 opacity-90"></div>
                <img src="https://images.unsplash.com/photo-1551434678-e076c223a692?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Office" class="absolute inset-0 w-full h-full object-cover mix-blend-overlay opacity-50">
                <div class="absolute inset-0 flex flex-col justify-center px-12 text-white">
                    <h2 class="text-3xl font-bold mb-4 leading-tight">Xây dựng lộ trình từ dữ liệu thực tế.</h2>
                    <p class="text-brand-100 text-lg leading-relaxed">Hệ thống phân tích hàng trăm tin tuyển dụng để đưa ra gợi ý chính xác nhất cho sự nghiệp của bạn.</p>
                    
                    <!-- Mock Statistics -->
                    <div class="grid grid-cols-2 gap-4 mt-8">
                        <div class="bg-white/10 backdrop-blur p-4 rounded-xl">
                            <div class="text-2xl font-bold">150+</div>
                            <div class="text-sm text-brand-100">Câu hỏi Quiz</div>
                        </div>
                        <div class="bg-white/10 backdrop-blur p-4 rounded-xl">
                            <div class="text-2xl font-bold">24/7</div>
                            <div class="text-sm text-brand-100">Virtual Mentor</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- ==================== APP SHELL ==================== -->
    <div id="app-shell" class="hidden min-h-screen flex bg-slate-50 dark:bg-slate-900">
        
        <!-- Sidebar Navigation -->
        <aside id="sidebar" class="w-64 bg-white dark:bg-slate-800 border-r border-slate-200 dark:border-slate-700 flex-col fixed h-full z-30 hidden md:flex transition-colors">
            <div class="h-16 flex items-center px-6 border-b border-slate-200 dark:border-slate-700">
                <div class="w-8 h-8 rounded-lg bg-brand-600 text-white flex items-center justify-center mr-3">
                    <i class="fa-solid fa-layer-group"></i>
                </div>
                <span class="font-bold text-lg text-slate-800 dark:text-white">BA Path Pro</span>
            </div>

            <div class="flex-1 overflow-y-auto py-4 px-3 space-y-1">
                <div class="px-3 mb-2 text-xs font-bold text-slate-400 uppercase tracking-wider">Main Menu</div>
                <button onclick="App.nav.go('dashboard')" class="nav-item w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-brand-50 dark:hover:bg-slate-700 hover:text-brand-600 transition group active">
                    <i class="fa-solid fa-chart-pie w-5 group-hover:text-brand-600"></i> Dashboard
                </button>
                <button onclick="App.nav.go('roadmap')" class="nav-item w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-brand-50 dark:hover:bg-slate-700 hover:text-brand-600 transition group">
                    <i class="fa-solid fa-road w-5 group-hover:text-brand-600"></i> Lộ Trình Học
                </button>
                <button onclick="App.nav.go('jobs')" class="nav-item w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-brand-50 dark:hover:bg-slate-700 hover:text-brand-600 transition group">
                    <i class="fa-solid fa-briefcase w-5 group-hover:text-brand-600"></i> Job Market <span class="ml-auto bg-red-100 text-red-600 text-xs font-bold px-2 py-0.5 rounded-full">Hot</span>
                </button>
                <button onclick="App.nav.go('resources')" class="nav-item w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-brand-50 dark:hover:bg-slate-700 hover:text-brand-600 transition group">
                    <i class="fa-solid fa-book-open w-5 group-hover:text-brand-600"></i> Kho Tài Liệu
                </button>

                <div class="px-3 mt-6 mb-2 text-xs font-bold text-slate-400 uppercase tracking-wider">Tools</div>
                <button onclick="App.nav.go('settings')" class="nav-item w-full flex items-center gap-3 px-3 py-2.5 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-brand-50 dark:hover:bg-slate-700 hover:text-brand-600 transition group">
                    <i class="fa-solid fa-gear w-5 group-hover:text-brand-600"></i> Cài Đặt
                </button>
            </div>

            <!-- User Profile Mini -->
            <div class="p-4 border-t border-slate-200 dark:border-slate-700">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-brand-500 to-purple-500 flex items-center justify-center text-white font-bold" id="sidebar-avatar">
                        U
                    </div>
                    <div class="flex-1 min-w-0">
                        <p class="text-sm font-medium text-slate-900 dark:text-white truncate" id="sidebar-name">User</p>
                        <p class="text-xs text-slate-500 dark:text-slate-400 truncate" id="sidebar-role">Business Analyst</p>
                    </div>
                    <button onclick="App.auth.logout()" class="text-slate-400 hover:text-red-500 transition"><i class="fa-solid fa-right-from-bracket"></i></button>
                </div>
            </div>
        </aside>

        <!-- Mobile Header -->
        <header id="mobile-header" class="md:hidden fixed top-0 left-0 right-0 h-16 bg-white dark:bg-slate-800 border-b border-slate-200 dark:border-slate-700 z-30 flex items-center justify-between px-4">
            <div class="flex items-center gap-2 font-bold text-slate-800 dark:text-white">
                <div class="w-8 h-8 rounded bg-brand-600 text-white flex items-center justify-center"><i class="fa-solid fa-layer-group"></i></div>
                BA Path Pro
            </div>
            <button onclick="document.getElementById('sidebar').classList.toggle('hidden'); document.getElementById('sidebar').classList.toggle('flex'); document.getElementById('sidebar').classList.toggle('w-full');" class="text-slate-600 dark:text-slate-300">
                <i class="fa-solid fa-bars text-xl"></i>
            </button>
        </header>

        <!-- Main Content Area -->
        <main id="main-content" class="flex-1 md:ml-64 pt-16 md:pt-0 overflow-y-auto h-screen bg-slate-50 dark:bg-slate-900 transition-colors">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
                
                <!-- Top Bar -->
                <div class="flex justify-between items-center mb-8">
                    <div>
                        <h2 id="page-title" class="text-2xl font-bold text-slate-800 dark:text-white">Dashboard</h2>
                        <p id="page-subtitle" class="text-slate-500 dark:text-slate-400 text-sm">Chào mừng trở lại, hãy kiểm tra tiến độ hôm nay.</p>
                    </div>
                    <div class="flex items-center gap-3">
                        <button onclick="App.ui.toggleDark()" class="w-10 h-10 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-yellow-400 shadow-sm hover:bg-slate-50 transition flex items-center justify-center">
                            <i class="fa-solid fa-moon dark:hidden"></i>
                            <i class="fa-solid fa-sun hidden dark:block"></i>
                        </button>
                        <div class="relative group">
                             <button class="w-10 h-10 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 shadow-sm flex items-center justify-center">
                                <i class="fa-regular fa-bell"></i>
                                <span class="absolute top-2 right-2 w-2.5 h-2.5 bg-red-500 rounded-full border-2 border-white dark:border-slate-800"></span>
                            </button>
                            <!-- Notification Dropdown (Mock) -->
                            <div class="absolute right-0 mt-2 w-80 bg-white dark:bg-slate-800 rounded-xl shadow-xl border border-slate-100 dark:border-slate-700 p-4 hidden group-hover:block z-50 animate-fade-in">
                                <h4 class="font-bold text-slate-800 dark:text-white mb-3">Thông báo mới</h4>
                                <div class="space-y-3">
                                    <div class="flex gap-3 items-start">
                                        <div class="w-8 h-8 rounded-full bg-blue-100 text-blue-600 flex items-center justify-center shrink-0"><i class="fa-solid fa-briefcase text-xs"></i></div>
                                        <div>
                                            <p class="text-sm text-slate-600 dark:text-slate-300">Job mới phù hợp: Senior BA tại Techcombank.</p>
                                            <span class="text-xs text-slate-400">2 giờ trước</span>
                                        </div>
                                    </div>
                                    <div class="flex gap-3 items-start">
                                        <div class="w-8 h-8 rounded-full bg-green-100 text-green-600 flex items-center justify-center shrink-0"><i class="fa-solid fa-check text-xs"></i></div>
                                        <div>
                                            <p class="text-sm text-slate-600 dark:text-slate-300">Bạn đã hoàn thành 80% kỹ năng SQL.</p>
                                            <span class="text-xs text-slate-400">5 giờ trước</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- DYNAMIC CONTENT SECTIONS -->
                
                <!-- 1. DASHBOARD VIEW -->
                <div id="view-dashboard" class="view-section space-y-6">
                    <!-- Stats Grid -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                        <div class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 flex items-center gap-4">
                            <div class="w-12 h-12 rounded-xl bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 flex items-center justify-center text-xl">
                                <i class="fa-solid fa-bullseye"></i>
                            </div>
                            <div>
                                <p class="text-sm text-slate-500 dark:text-slate-400 font-medium">Kỹ năng mục tiêu</p>
                                <h3 class="text-2xl font-bold text-slate-900 dark:text-white" id="stat-total-skills">0</h3>
                            </div>
                        </div>
                        <div class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 flex items-center gap-4">
                            <div class="w-12 h-12 rounded-xl bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 dark:text-emerald-400 flex items-center justify-center text-xl">
                                <i class="fa-solid fa-check-circle"></i>
                            </div>
                            <div>
                                <p class="text-sm text-slate-500 dark:text-slate-400 font-medium">Đã hoàn thành</p>
                                <h3 class="text-2xl font-bold text-slate-900 dark:text-white" id="stat-completed-skills">0</h3>
                            </div>
                        </div>
                        <div class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 flex items-center gap-4">
                            <div class="w-12 h-12 rounded-xl bg-purple-50 dark:bg-purple-900/30 text-purple-600 dark:text-purple-400 flex items-center justify-center text-xl">
                                <i class="fa-solid fa-fire"></i>
                            </div>
                            <div>
                                <p class="text-sm text-slate-500 dark:text-slate-400 font-medium">Job Matching</p>
                                <h3 class="text-2xl font-bold text-slate-900 dark:text-white" id="stat-job-match">0 Job</h3>
                            </div>
                        </div>
                    </div>

                    <!-- Charts & Activity -->
                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                        <div class="lg:col-span-2 bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700">
                            <h3 class="font-bold text-lg text-slate-800 dark:text-white mb-4">Biểu đồ năng lực</h3>
                            <div class="h-64 w-full">
                                <canvas id="competencyChart"></canvas>
                            </div>
                        </div>
                        <div class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700">
                            <h3 class="font-bold text-lg text-slate-800 dark:text-white mb-4">Mentor Lời khuyên</h3>
                            <div id="mentor-widget" class="bg-brand-50 dark:bg-slate-700/50 rounded-xl p-4 border border-brand-100 dark:border-slate-600">
                                <div class="flex items-center gap-3 mb-3">
                                    <img src="https://ui-avatars.com/api/?name=AI+Mentor&background=2563eb&color=fff" class="w-10 h-10 rounded-full">
                                    <div>
                                        <p class="font-bold text-sm dark:text-white">AI Mentor</p>
                                        <p class="text-xs text-slate-500 dark:text-slate-400">Online ngay bây giờ</p>
                                    </div>
                                </div>
                                <p class="text-sm text-slate-700 dark:text-slate-300 italic" id="mentor-msg">
                                    "Chào bạn! Dựa trên hồ sơ, bạn nên tập trung học SQL nâng cao trong tuần này để cải thiện khả năng xử lý dữ liệu."
                                </p>
                                <button onclick="App.ui.openChat()" class="mt-3 w-full py-2 bg-white dark:bg-slate-600 text-brand-600 dark:text-brand-300 text-sm font-bold rounded-lg border border-brand-200 dark:border-slate-500 hover:bg-brand-50 transition">
                                    Chat với Mentor
                                </button>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Quick Actions -->
                    <div class="bg-gradient-to-r from-slate-800 to-slate-900 rounded-2xl p-8 text-white relative overflow-hidden">
                        <div class="absolute top-0 right-0 w-64 h-64 bg-white opacity-5 rounded-full blur-3xl -mr-16 -mt-16"></div>
                        <div class="relative z-10 flex justify-between items-center">
                            <div>
                                <h3 class="text-xl font-bold mb-2">Sẵn sàng cho bước tiếp theo?</h3>
                                <p class="text-slate-300 max-w-lg">Hãy hoàn thành bài Quiz kiểm tra kiến thức SQL để nhận chứng chỉ hoàn thành giai đoạn 1.</p>
                            </div>
                            <button onclick="App.nav.go('roadmap')" class="px-6 py-3 bg-brand-600 hover:bg-brand-500 rounded-xl font-bold transition shadow-lg shadow-brand-900/50">
                                Đi đến bài kiểm tra
                            </button>
                        </div>
                    </div>
                </div>

                <!-- 2. ROADMAP VIEW -->
                <div id="view-roadmap" class="view-section hidden">
                    <!-- Filters/Role Select (Only if not set) -->
                    <div class="mb-6 bg-white dark:bg-slate-800 p-4 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-wrap gap-4 items-center justify-between" id="roadmap-controls">
                        <div class="flex items-center gap-2">
                            <span class="text-sm font-bold text-slate-500 dark:text-slate-400 uppercase">Role:</span>
                            <select id="role-select" onchange="App.logic.changeRole(this.value)" class="bg-slate-100 dark:bg-slate-700 border-none rounded-lg px-3 py-1.5 text-sm font-bold text-slate-700 dark:text-white focus:ring-2 focus:ring-brand-500">
                                <option value="tech_ba">Technical BA</option>
                                <option value="biz_ba">Business BA</option>
                                <option value="lead_ba">Strategic BA</option>
                            </select>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="App.ui.toggleViewMode('grid')" class="p-2 rounded-lg bg-brand-100 dark:bg-brand-900 text-brand-600 dark:text-brand-400"><i class="fa-solid fa-grid-2"></i></button>
                            <button onclick="App.ui.toggleViewMode('list')" class="p-2 rounded-lg bg-slate-100 dark:bg-slate-700 text-slate-500"><i class="fa-solid fa-list"></i></button>
                        </div>
                    </div>

                    <!-- Dynamic Phases -->
                    <div class="space-y-8" id="roadmap-container">
                        <!-- Rendered via JS -->
                    </div>
                </div>

                <!-- 3. JOBS VIEW -->
                <div id="view-jobs" class="view-section hidden">
                     <div class="flex justify-between items-end mb-6">
                        <div>
                            <h3 class="text-lg font-bold text-slate-800 dark:text-white">Cơ hội nghề nghiệp phù hợp</h3>
                            <p class="text-sm text-slate-500">Dựa trên bộ kỹ năng hiện tại của bạn (Match > 60%)</p>
                        </div>
                        <div class="flex gap-2">
                            <span class="px-3 py-1 bg-green-100 text-green-700 rounded-full text-xs font-bold">Junior: 5</span>
                            <span class="px-3 py-1 bg-blue-100 text-blue-700 rounded-full text-xs font-bold">Middle: 12</span>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-4" id="jobs-container">
                        <!-- Jobs Rendered via JS -->
                    </div>
                </div>
                
                <!-- 4. RESOURCE HUB VIEW -->
                <div id="view-resources" class="view-section hidden">
                    <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
                        <div class="lg:col-span-1">
                            <div class="bg-white dark:bg-slate-800 p-4 rounded-xl sticky top-4 border border-slate-200 dark:border-slate-700">
                                <h4 class="font-bold text-slate-800 dark:text-white mb-4">Bộ lọc</h4>
                                <div class="space-y-2">
                                    <label class="flex items-center gap-2 text-sm text-slate-600 dark:text-slate-300 cursor-pointer">
                                        <input type="checkbox" checked class="rounded text-brand-600 focus:ring-brand-500"> Sách (Books)
                                    </label>
                                    <label class="flex items-center gap-2 text-sm text-slate-600 dark:text-slate-300 cursor-pointer">
                                        <input type="checkbox" checked class="rounded text-brand-600 focus:ring-brand-500"> Khóa học (Courses)
                                    </label>
                                    <label class="flex items-center gap-2 text-sm text-slate-600 dark:text-slate-300 cursor-pointer">
                                        <input type="checkbox" checked class="rounded text-brand-600 focus:ring-brand-500"> Video
                                    </label>
                                </div>
                            </div>
                        </div>
                        <div class="lg:col-span-3 space-y-6" id="resources-container">
                            <!-- Resources Rendered Here -->
                        </div>
                    </div>
                </div>

            </div>
        </main>
    </div>

    <!-- ==================== MODALS & WIDGETS ==================== -->
    
    <!-- Quiz Modal -->
    <div id="quiz-modal" class="fixed inset-0 z-[80] hidden bg-slate-900/80 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 w-full max-w-2xl rounded-2xl shadow-2xl overflow-hidden flex flex-col max-h-[90vh]">
            <div class="p-6 border-b border-slate-100 dark:border-slate-700 flex justify-between items-center bg-slate-50 dark:bg-slate-900">
                <div>
                    <h3 class="text-xl font-bold text-slate-900 dark:text-white" id="quiz-title">Kiểm tra kỹ năng SQL</h3>
                    <p class="text-sm text-slate-500">Trả lời đúng 2/3 câu để mở khóa kỹ năng này.</p>
                </div>
                <button onclick="App.quiz.close()" class="text-slate-400 hover:text-slate-600 dark:hover:text-white"><i class="fa-solid fa-xmark text-xl"></i></button>
            </div>
            <div class="p-6 overflow-y-auto flex-1" id="quiz-content">
                <!-- Questions go here -->
            </div>
            <div class="p-6 border-t border-slate-100 dark:border-slate-700 flex justify-end gap-3 bg-slate-50 dark:bg-slate-900">
                <button onclick="App.quiz.close()" class="px-4 py-2 text-slate-600 dark:text-slate-300 font-bold hover:bg-slate-200 dark:hover:bg-slate-700 rounded-lg">Hủy bỏ</button>
                <button onclick="App.quiz.submit()" class="px-6 py-2 bg-brand-600 hover:bg-brand-700 text-white font-bold rounded-lg shadow-lg shadow-brand-500/30">Nộp bài</button>
            </div>
        </div>
    </div>

    <!-- Chatbot Widget -->
    <div id="chatbot-widget" class="fixed bottom-6 right-6 z-40 flex flex-col items-end">
        <!-- Chat Window -->
        <div id="chat-window" class="hidden bg-white dark:bg-slate-800 w-80 h-96 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-700 flex flex-col mb-4 overflow-hidden animate-scale-in origin-bottom-right">
            <div class="bg-brand-600 p-4 text-white flex justify-between items-center">
                <div class="flex items-center gap-2">
                    <div class="w-2 h-2 bg-green-400 rounded-full animate-pulse"></div>
                    <span class="font-bold">Virtual Mentor</span>
                </div>
                <button onclick="App.ui.toggleChat()" class="text-white/80 hover:text-white"><i class="fa-solid fa-minus"></i></button>
            </div>
            <div class="flex-1 p-4 overflow-y-auto space-y-3 bg-slate-50 dark:bg-slate-900" id="chat-messages">
                <!-- Messages -->
                <div class="flex items-start gap-2">
                    <div class="w-8 h-8 rounded-full bg-brand-100 flex items-center justify-center text-brand-600 text-xs"><i class="fa-solid fa-robot"></i></div>
                    <div class="bg-white dark:bg-slate-800 p-3 rounded-r-xl rounded-bl-xl shadow-sm border border-slate-100 dark:border-slate-700 text-sm text-slate-700 dark:text-slate-300">
                        Chào bạn! Tôi có thể giúp gì cho lộ trình BA của bạn hôm nay?
                    </div>
                </div>
            </div>
            <div class="p-3 border-t border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800">
                <div class="relative">
                    <input type="text" id="chat-input" class="w-full pl-4 pr-10 py-2 rounded-full bg-slate-100 dark:bg-slate-700 border-none text-sm focus:ring-2 focus:ring-brand-500 dark:text-white" placeholder="Hỏi tôi về SQL, Agile...">
                    <button onclick="App.mentor.send()" class="absolute right-2 top-1.5 text-brand-600 hover:text-brand-700 dark:text-brand-400"><i class="fa-solid fa-paper-plane"></i></button>
                </div>
            </div>
        </div>
        <!-- Trigger Button -->
        <button onclick="App.ui.toggleChat()" class="w-14 h-14 bg-brand-600 hover:bg-brand-700 text-white rounded-full shadow-lg shadow-brand-600/40 flex items-center justify-center text-2xl transition transform hover:scale-110">
            <i class="fa-solid fa-comment-dots"></i>
        </button>
    </div>

    <!-- ==================== JAVASCRIPT LOGIC ==================== -->
    <script>
        /**
         * DATABASE SYSTEM
         * ----------------
         * Massive expanded data for Enterprise functionality.
         */
        const DB = {
            skills: [
                // Technical
                { id: 'sql', name: 'SQL Fundamentals', cat: 'tech', phase: 1, desc: 'Truy vấn cơ bản: SELECT, FROM, WHERE, JOINs.', questions: [
                    { q: 'Lệnh nào dùng để lấy dữ liệu?', a: ['GET', 'SELECT', 'FETCH', 'PULL'], c: 1 },
                    { q: 'JOIN nào trả về bản ghi khớp ở cả 2 bảng?', a: ['LEFT', 'RIGHT', 'INNER', 'OUTER'], c: 2 },
                    { q: 'Dấu % trong LIKE đại diện cho?', a: ['1 ký tự', '0 hoặc nhiều ký tự', 'Số', 'Ký tự đặc biệt'], c: 1 }
                ], res: 'https://www.w3schools.com/sql/' },
                { id: 'data_modeling', name: 'Data Modeling', cat: 'tech', phase: 1, desc: 'Hiểu ERD, Quan hệ 1-1, 1-n, n-n.', questions: [
                    { q: 'ERD là viết tắt của?', a: ['Entity Relational Diagram', 'Entity Relationship Diagram', 'Engine Run Data', 'None'], c: 1 },
                    { q: 'Khóa chính (Primary Key) phải?', a: ['Null', 'Trùng lặp', 'Duy nhất & Không Null', 'Text'], c: 2 },
                    { q: 'Quan hệ Một-Nhiều thể hiện bằng?', a: ['Crow\'s foot', 'Single line', 'Double line', 'Circle'], c: 0 }
                ], res: 'https://www.lucidchart.com/pages/er-diagrams' },
                { id: 'api', name: 'REST API Basics', cat: 'tech', phase: 2, desc: 'Hiểu HTTP Methods, Status Codes, JSON.', questions: [
                    { q: 'Method nào để tạo mới resource?', a: ['GET', 'POST', 'PUT', 'DELETE'], c: 1 },
                    { q: 'Status 200 nghĩa là?', a: ['Error', 'Not Found', 'OK', 'Created'], c: 2 },
                    { q: 'JSON là viết tắt của?', a: ['Java Standard Object', 'JavaScript Object Notation', 'Java Syntax On', 'None'], c: 1 }
                ], res: 'https://restfulapi.net/' },
                { id: 'python', name: 'Python for Analysis', cat: 'tech', phase: 3, desc: 'Pandas, NumPy để xử lý dữ liệu.', questions: [
                    { q: 'Thư viện nào dùng cho Dataframe?', a: ['NumPy', 'Pandas', 'Matplotlib', 'Flask'], c: 1 },
                    { q: 'Lệnh đọc file CSV?', a: ['pd.read_csv()', 'csv.read()', 'import_csv()', 'load()'], c: 0 },
                    { q: 'Jupyter Notebook dùng để?', a: ['Code web', 'Code Data Interactive', 'Design UI', 'DB Admin'], c: 1 }
                ], res: 'https://kaggle.com/learn/python' },
                
                // Business
                { id: 'req_eng', name: 'Requirement Engineering', cat: 'biz', phase: 1, desc: 'Khơi gợi, Phân tích, Tài liệu hóa yêu cầu.', questions: [
                    { q: 'Kỹ thuật nào KHÔNG dùng để khơi gợi yêu cầu?', a: ['Phỏng vấn', 'Quan sát', 'Coding', 'Hội thảo'], c: 2 },
                    { q: 'SMART trong mục tiêu là?', a: ['Specific, Measurable...', 'Super, Master...', 'Small, Medium...', 'None'], c: 0 },
                    { q: 'Ai là người sở hữu yêu cầu?', a: ['Dev', 'Stakeholder', 'Tester', 'PM'], c: 1 }
                ], res: 'https://iiba.org' },
                { id: 'user_stories', name: 'User Stories', cat: 'biz', phase: 1, desc: 'Viết User Story chuẩn INVEST.', questions: [
                    { q: 'Cấu trúc chuẩn của User Story?', a: ['As a... I want... So that...', 'If... Then... Else...', 'When... Do...', 'Given... When... Then'], c: 0 },
                    { q: 'Chữ I trong INVEST là?', a: ['Independent', 'Important', 'Immediate', 'Internal'], c: 0 },
                    { q: 'Acceptance Criteria dùng để?', a: ['Code', 'Design', 'Verify story done', 'Deploy'], c: 2 }
                ], res: 'https://www.mountaingoatsoftware.com/agile/user-stories' },
                { id: 'bpmn', name: 'BPMN 2.0', cat: 'biz', phase: 2, desc: 'Mô hình hóa quy trình nghiệp vụ chuẩn.', questions: [
                    { q: 'Hình thoi trong BPMN biểu diễn?', a: ['Task', 'Gateway (Rẽ nhánh)', 'Event', 'Data'], c: 1 },
                    { q: 'Pool và Lane dùng để?', a: ['Trang trí', 'Phân chia trách nhiệm', 'Lưu data', 'Kết thúc'], c: 1 },
                    { q: 'Sự kiện bắt đầu hình gì?', a: ['Tròn nét đơn', 'Tròn nét đậm', 'Vuông', 'Tam giác'], c: 0 }
                ], res: 'https://camunda.com/bpmn/' },
                
                // Soft/Domain
                { id: 'comm', name: 'Communication', cat: 'soft', phase: 1, desc: 'Giao tiếp hiệu quả với các bên.', questions: [
                    { q: 'Khi giao tiếp với Dev, nên?', a: ['Nói chung chung', 'Dùng ngôn ngữ kỹ thuật chính xác', 'Ra lệnh', 'Im lặng'], c: 1 },
                    { q: 'Active Listening là?', a: ['Nghe và làm việc khác', 'Nghe và phản hồi/xác nhận', 'Nghe nhạc', 'Nghe thụ động'], c: 1 },
                    { q: 'Kênh nào tốt nhất cho việc khẩn cấp?', a: ['Email', 'Chat/Gọi trực tiếp', 'Jira comment', 'Wiki'], c: 1 }
                ], res: 'https://hbr.org/topic/communication' },
                { id: 'banking', name: 'Banking Domain', cat: 'domain', phase: 3, desc: 'Kiến thức Core Banking, Tín dụng.', questions: [
                    { q: 'CIF là gì?', a: ['Customer Information File', 'Cash In Flow', 'Credit Info Form', 'None'], c: 0 },
                    { q: 'Casa là?', a: ['Tiền gửi không kỳ hạn', 'Tiền tiết kiệm', 'Vay thế chấp', 'Thẻ tín dụng'], c: 0 },
                    { q: 'SWIFT code dùng để?', a: ['Chuyển tiền quốc tế', 'Đăng nhập', 'Mã hóa', 'Tính lãi'], c: 0 }
                ], res: 'https://www.investopedia.com/' }
            ],
            jobs: [
                { id: 1, title: "Junior Business Analyst", company: "Techcombank", salary: "15-20M", match: 0.8, req: ['sql', 'req_eng', 'comm'], type: 'Junior' },
                { id: 2, title: "Product Owner (Banking)", company: "MB Bank", salary: "30-45M", match: 0.4, req: ['banking', 'user_stories', 'bpmn', 'agile'], type: 'Senior' },
                { id: 3, title: "Data Analyst / BA", company: "Momo", salary: "20-30M", match: 0.6, req: ['sql', 'python', 'data_modeling', 'api'], type: 'Middle' },
                { id: 4, title: "ERP Consultant", company: "FPT Software", salary: "25-35M", match: 0.3, req: ['req_eng', 'bpmn', 'comm', 'sql'], type: 'Middle' }
            ],
            mentorKnowledge: {
                'sql': "SQL là kỹ năng sống còn. Bạn nên luyện tập trên HackerRank ít nhất 30 phút mỗi ngày.",
                'req_eng': "Đừng chỉ ghi chép, hãy hỏi 'Tại sao' 5 lần (5 Whys) để tìm ra nhu cầu thực sự của Stakeholder.",
                'python': "Với BA, bạn chỉ cần tập trung vào thư viện Pandas để xử lý data, không cần học quá sâu về thuật toán."
            }
        };

        /**
         * CORE APPLICATION CLASS
         * ----------------------
         * Manages State, UI, Logic, Auth
         */
        class Application {
            constructor() {
                this.user = null;
                this.role = 'tech_ba';
                this.progress = []; // Array of completed skill IDs
                this.currentView = 'dashboard';
                
                // Sub-modules
                this.auth = {
                    login: (username) => {
                        this.user = { name: username, joined: new Date() };
                        localStorage.setItem('ba_pro_user', JSON.stringify(this.user));
                        this.ui.showApp();
                    },
                    logout: () => {
                        localStorage.removeItem('ba_pro_user');
                        location.reload();
                    },
                    check: () => {
                        const saved = localStorage.getItem('ba_pro_user');
                        if(saved) {
                            this.user = JSON.parse(saved);
                            const savedProg = localStorage.getItem(`ba_prog_${this.user.name}`);
                            if(savedProg) this.progress = JSON.parse(savedProg);
                            this.ui.showApp();
                        } else {
                            this.ui.showAuth();
                        }
                    }
                };

                this.nav = {
                    go: (viewId) => {
                        document.querySelectorAll('.view-section').forEach(el => el.classList.add('hidden'));
                        document.getElementById(`view-${viewId}`).classList.remove('hidden');
                        
                        // Update Sidebar Active State
                        document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('bg-brand-50', 'dark:bg-slate-700', 'text-brand-600'));
                        // Note: Simple logic, in real app use ID matching
                        
                        this.currentView = viewId;
                        document.getElementById('page-title').innerText = viewId === 'dashboard' ? 'Dashboard' : 
                                                                        viewId === 'roadmap' ? 'Lộ Trình Chi Tiết' :
                                                                        viewId === 'jobs' ? 'Thị Trường Việc Làm' : 'Kho Tài Liệu';
                        
                        if(viewId === 'dashboard') this.logic.updateDashboard();
                        if(viewId === 'roadmap') this.logic.renderRoadmap();
                        if(viewId === 'jobs') this.logic.renderJobs();
                        if(viewId === 'resources') this.logic.renderResources();
                    }
                };

                this.quiz = {
                    currentSkillId: null,
                    open: (skillId) => {
                        const skill = DB.skills.find(s => s.id === skillId);
                        if(!skill) return;
                        this.quiz.currentSkillId = skillId;
                        
                        document.getElementById('quiz-title').innerText = `Kiểm tra: ${skill.name}`;
                        const container = document.getElementById('quiz-content');
                        container.innerHTML = '';
                        
                        skill.questions.forEach((q, idx) => {
                            let html = `<div class="mb-6">
                                <p class="font-bold text-slate-800 dark:text-white mb-2">Câu ${idx+1}: ${q.q}</p>
                                <div class="space-y-2">`;
                            q.a.forEach((opt, optIdx) => {
                                html += `<label class="flex items-center gap-3 p-3 rounded-lg border border-slate-200 dark:border-slate-700 hover:bg-slate-50 dark:hover:bg-slate-700 cursor-pointer transition">
                                    <input type="radio" name="q${idx}" value="${optIdx}" class="text-brand-600 focus:ring-brand-500">
                                    <span class="text-sm text-slate-600 dark:text-slate-300">${opt}</span>
                                </label>`;
                            });
                            html += `</div></div>`;
                            container.innerHTML += html;
                        });
                        
                        document.getElementById('quiz-modal').classList.remove('hidden');
                        document.getElementById('quiz-modal').classList.add('flex');
                    },
                    close: () => {
                        document.getElementById('quiz-modal').classList.add('hidden');
                        document.getElementById('quiz-modal').classList.remove('flex');
                    },
                    submit: () => {
                        const skill = DB.skills.find(s => s.id === this.quiz.currentSkillId);
                        let score = 0;
                        skill.questions.forEach((q, idx) => {
                            const selected = document.querySelector(`input[name="q${idx}"]:checked`);
                            if(selected && parseInt(selected.value) === q.c) score++;
                        });

                        if(score >= 2) {
                            alert(`Chúc mừng! Bạn đúng ${score}/${skill.questions.length} câu. Kỹ năng đã được mở khóa!`);
                            if(!this.progress.includes(this.quiz.currentSkillId)) {
                                this.progress.push(this.quiz.currentSkillId);
                                this.logic.saveProgress();
                            }
                            this.quiz.close();
                            this.logic.renderRoadmap(); // Refresh UI
                            confetti({ particleCount: 100, spread: 70, origin: { y: 0.6 } });
                        } else {
                            alert(`Rất tiếc, bạn chỉ đúng ${score}/${skill.questions.length}. Hãy ôn lại kiến thức và thử lại sau nhé!`);
                        }
                    }
                };

                this.mentor = {
                    send: () => {
                        const input = document.getElementById('chat-input');
                        const msg = input.value.trim();
                        if(!msg) return;
                        
                        // User msg
                        this.ui.addChatMsg(msg, 'user');
                        input.value = '';
                        
                        // Bot logic (Mock AI)
                        setTimeout(() => {
                            let reply = "Tôi chưa hiểu rõ câu hỏi lắm. Bạn có thể hỏi cụ thể về SQL, Python hoặc Quy trình BA được không?";
                            const lower = msg.toLowerCase();
                            
                            if(lower.includes('sql')) reply = DB.mentorKnowledge['sql'];
                            else if(lower.includes('hỏi') || lower.includes('khơi gợi')) reply = DB.mentorKnowledge['req_eng'];
                            else if(lower.includes('python') || lower.includes('code')) reply = DB.mentorKnowledge['python'];
                            else if(lower.includes('chào') || lower.includes('hi')) reply = "Chào bạn! Sẵn sàng chinh phục kỹ năng mới chưa?";
                            else if(lower.includes('job') || lower.includes('việc')) reply = "Thị trường đang rất cần Tech BA biết SQL và Power BI. Bạn hãy check mục Job Market nhé.";
                            
                            this.ui.addChatMsg(reply, 'bot');
                        }, 1000);
                    }
                };

                this.ui = {
                    showAuth: () => {
                        document.getElementById('auth-screen').classList.remove('hidden');
                        document.getElementById('app-shell').classList.add('hidden');
                    },
                    showApp: () => {
                        document.getElementById('auth-screen').classList.add('hidden');
                        document.getElementById('app-shell').classList.remove('hidden');
                        document.getElementById('sidebar-name').innerText = this.user.name;
                        document.getElementById('sidebar-avatar').innerText = this.user.name.charAt(0).toUpperCase();
                        this.nav.go('dashboard');
                    },
                    toggleDark: () => {
                        document.documentElement.classList.toggle('dark');
                    },
                    toggleChat: () => {
                        const win = document.getElementById('chat-window');
                        win.classList.toggle('hidden');
                        if(!win.classList.contains('hidden')) document.getElementById('chat-input').focus();
                    },
                    addChatMsg: (text, sender) => {
                        const container = document.getElementById('chat-messages');
                        const isUser = sender === 'user';
                        const html = `
                        <div class="flex items-start gap-2 ${isUser ? 'flex-row-reverse' : ''} animate-slide-in">
                            <div class="w-8 h-8 rounded-full ${isUser ? 'bg-purple-100 text-purple-600' : 'bg-brand-100 text-brand-600'} flex items-center justify-center text-xs shrink-0">
                                <i class="fa-solid ${isUser ? 'fa-user' : 'fa-robot'}"></i>
                            </div>
                            <div class="${isUser ? 'bg-purple-600 text-white' : 'bg-white dark:bg-slate-800 text-slate-700 dark:text-slate-300 border border-slate-100 dark:border-slate-700'} p-3 rounded-xl shadow-sm max-w-[80%] text-sm">
                                ${text}
                            </div>
                        </div>`;
                        container.insertAdjacentHTML('beforeend', html);
                        container.scrollTop = container.scrollHeight;
                    },
                    toggleViewMode: (mode) => {
                        const container = document.getElementById('roadmap-container');
                        if (mode === 'list') container.classList.add('list-view');
                        else container.classList.remove('list-view');
                        // Simplified: In real implementation, this adds classes to change grid cols
                        alert("Chế độ xem " + mode + " đã được kích hoạt (Demo UI update)");
                    }
                };

                this.logic = {
                    changeRole: (newRole) => {
                        this.role = newRole;
                        this.logic.renderRoadmap();
                    },
                    saveProgress: () => {
                        localStorage.setItem(`ba_prog_${this.user.name}`, JSON.stringify(this.progress));
                        this.logic.updateDashboard();
                    },
                    updateDashboard: () => {
                        // Calc Stats
                        const total = DB.skills.length; // In reality, filter by role
                        const done = this.progress.length;
                        document.getElementById('stat-total-skills').innerText = total;
                        document.getElementById('stat-completed-skills').innerText = done;
                        
                        // Job Match Logic
                        let matches = DB.jobs.filter(j => {
                            const had = j.req.filter(r => this.progress.includes(r)).length;
                            return (had / j.req.length) >= 0.5; // >50% match
                        });
                        document.getElementById('stat-job-match').innerText = `${matches.length} Jobs`;

                        // Chart.js update
                        this.logic.renderChart(total, done);
                    },
                    renderChart: (total, done) => {
                        const ctx = document.getElementById('competencyChart').getContext('2d');
                        if(window.myChart) window.myChart.destroy();
                        window.myChart = new Chart(ctx, {
                            type: 'doughnut',
                            data: {
                                labels: ['Hoàn thành', 'Chưa hoàn thành'],
                                datasets: [{
                                    data: [done, total - done],
                                    backgroundColor: ['#10b981', '#e2e8f0'],
                                    borderWidth: 0
                                }]
                            },
                            options: { cutout: '70%', responsive: true, maintainAspectRatio: false }
                        });
                    },
                    renderRoadmap: () => {
                        const container = document.getElementById('roadmap-container');
                        container.innerHTML = '';
                        
                        // Group by Phase
                        [1, 2, 3].forEach(phase => {
                            const skills = DB.skills.filter(s => s.phase === phase); // Should filter by role map in real app
                            if(skills.length === 0) return;
                            
                            let html = `
                            <div class="relative pl-8 border-l-2 border-slate-200 dark:border-slate-700 pb-8 last:pb-0">
                                <div class="absolute -left-[11px] top-0 w-5 h-5 rounded-full bg-brand-600 border-4 border-white dark:border-slate-900"></div>
                                <h3 class="text-xl font-bold text-slate-800 dark:text-white mb-4">Giai đoạn ${phase}</h3>
                                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">`;
                                
                            skills.forEach(s => {
                                const isDone = this.progress.includes(s.id);
                                html += `
                                <div class="skill-card bg-white dark:bg-slate-800 p-5 rounded-2xl border border-slate-100 dark:border-slate-700 relative overflow-hidden group">
                                    ${isDone ? '<div class="absolute top-0 right-0 bg-green-500 text-white text-xs font-bold px-2 py-1 rounded-bl-lg"><i class="fa-solid fa-check"></i> Done</div>' : ''}
                                    <div class="flex items-center gap-3 mb-3">
                                        <div class="w-10 h-10 rounded-lg bg-${s.cat === 'tech' ? 'blue' : s.cat === 'biz' ? 'emerald' : 'purple'}-100 text-${s.cat === 'tech' ? 'blue' : s.cat === 'biz' ? 'emerald' : 'purple'}-600 flex items-center justify-center text-lg">
                                            <i class="fa-solid ${s.icon ? s.icon : 'fa-code'}"></i>
                                        </div>
                                        <h4 class="font-bold text-slate-800 dark:text-white">${s.name}</h4>
                                    </div>
                                    <p class="text-sm text-slate-500 dark:text-slate-400 mb-4 line-clamp-2">${s.desc}</p>
                                    <button onclick="App.quiz.open('${s.id}')" ${isDone ? 'disabled' : ''} class="w-full py-2 rounded-lg text-sm font-bold transition ${isDone ? 'bg-slate-100 text-slate-400 cursor-not-allowed' : 'bg-brand-50 dark:bg-slate-700 text-brand-600 dark:text-white hover:bg-brand-600 hover:text-white'}">
                                        ${isDone ? 'Đã hoàn thành' : 'Làm bài kiểm tra'}
                                    </button>
                                </div>`;
                            });
                            
                            html += `</div></div>`;
                            container.innerHTML += html;
                        });
                    },
                    renderJobs: () => {
                        const container = document.getElementById('jobs-container');
                        container.innerHTML = '';
                        
                        DB.jobs.forEach(j => {
                            const matchPct = Math.round(j.match * 100);
                            const missing = j.req.filter(r => !this.progress.includes(r));
                            
                            container.innerHTML += `
                            <div class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-100 dark:border-slate-700 hover:border-brand-300 transition group">
                                <div class="flex justify-between items-start mb-4">
                                    <div>
                                        <h4 class="text-lg font-bold text-slate-800 dark:text-white group-hover:text-brand-600 transition">${j.title}</h4>
                                        <p class="text-sm text-slate-500 dark:text-slate-400">${j.company}</p>
                                    </div>
                                    <span class="bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 text-xs font-bold px-3 py-1 rounded-full">${j.salary}</span>
                                </div>
                                <div class="mb-4">
                                    <div class="flex justify-between text-xs font-bold mb-1">
                                        <span class="${matchPct > 70 ? 'text-green-600' : 'text-yellow-600'}">${matchPct}% Phù hợp</span>
                                    </div>
                                    <div class="w-full bg-slate-100 dark:bg-slate-700 rounded-full h-2">
                                        <div class="bg-brand-600 h-2 rounded-full" style="width: ${matchPct}%"></div>
                                    </div>
                                </div>
                                <div class="flex flex-wrap gap-2 mb-4">
                                    ${missing.map(m => `<span class="text-xs bg-red-50 text-red-600 px-2 py-1 rounded border border-red-100">Thiếu: ${m}</span>`).join('')}
                                </div>
                                <button class="w-full py-2 border border-slate-200 dark:border-slate-600 rounded-lg text-sm font-bold text-slate-600 dark:text-slate-300 hover:bg-slate-50 dark:hover:bg-slate-700 transition">Xem chi tiết</button>
                            </div>`;
                        });
                    },
                    renderResources: () => {
                        const container = document.getElementById('resources-container');
                        container.innerHTML = DB.skills.map(s => `
                            <div class="bg-white dark:bg-slate-800 p-4 rounded-xl border border-slate-200 dark:border-slate-700 flex justify-between items-center">
                                <div class="flex items-center gap-3">
                                    <div class="w-10 h-10 bg-slate-100 dark:bg-slate-700 rounded-lg flex items-center justify-center"><i class="fa-solid fa-book text-slate-500"></i></div>
                                    <div>
                                        <h5 class="font-bold text-slate-800 dark:text-white">${s.name} Guide</h5>
                                        <p class="text-xs text-slate-500">Nguồn: Official Docs</p>
                                    </div>
                                </div>
                                <a href="${s.res}" target="_blank" class="px-4 py-2 bg-brand-50 dark:bg-slate-700 text-brand-600 dark:text-white text-sm font-bold rounded-lg hover:bg-brand-100 transition">Mở <i class="fa-solid fa-external-link-alt ml-1"></i></a>
                            </div>
                        `).join('');
                    }
                };
            }
        }

        // Initialize App
        const App = new Application();

        // DOM Ready
        document.addEventListener('DOMContentLoaded', () => {
            // Initial Theme Check
            if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }

            // Attach Login Handler
            document.getElementById('login-form').addEventListener('submit', (e) => {
                e.preventDefault();
                App.auth.login(document.getElementById('username').value);
            });

            // Check Session
            App.auth.check();
        });

    </script>
</body>
</html>
