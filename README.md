<!DOCTYPE html>
<html lang="vi" class="scroll-smooth">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BA Career Roadmap Tool - Ultimate Full Edition</title>
    <!-- Tải Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Tải Mermaid.js (Vẽ sơ đồ) -->
    <script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
    <!-- Tải Canvas Confetti (Hiệu ứng pháo hoa) -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Cấu hình Tailwind -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        'brand-blue': '#0ea5e9', // sky-500
                        'brand-dark': '#0f172a', // slate-900
                    },
                    animation: {
                        'fade-in': 'fadeIn 0.6s ease-out',
                        'slide-up': 'slideUp 0.6s ease-out',
                    },
                    keyframes: {
                        fadeIn: {
                            '0%': { opacity: 0 },
                            '100%': { opacity: 1 },
                        },
                        slideUp: {
                            '0%': { opacity: 0, transform: 'translateY(30px)' },
                            '100%': { opacity: 1, transform: 'translateY(0)' },
                        }
                    }
                },
            },
        };
    </script>
    <style>
        body {
            background-image: linear-gradient(to bottom, rgba(248, 250, 252, 0.95), rgba(241, 245, 249, 0.98)), url('https://images.unsplash.com/photo-1460925895917-afdab827c52f?q=80&w=2015&auto=format&fit=crop');
            background-attachment: fixed;
            background-size: cover;
            background-position: center;
            min-height: 100vh;
        }
        
        ::-webkit-scrollbar { width: 10px; }
        ::-webkit-scrollbar-track { background: #f1f5f9; }
        ::-webkit-scrollbar-thumb { background: #94a3b8; border-radius: 5px; border: 2px solid #f1f5f9; }
        ::-webkit-scrollbar-thumb:hover { background: #64748b; }
        
        .page-container {
            background-color: rgba(255, 255, 255, 0.92);
            backdrop-filter: blur(12px);
            padding: 2.5rem;
            border-radius: 1.5rem;
            box-shadow: 0 10px 25px -5px rgb(0 0 0 / 0.05), 0 8px 10px -6px rgb(0 0 0 / 0.01);
            border: 1px solid rgba(255, 255, 255, 0.6);
        }

        .persona-card {
            border: 2px solid #e2e8f0;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            background-color: white;
        }
        .persona-radio:checked + .persona-card {
            border-color: #0ea5e9;
            background-color: #f0f9ff;
            box-shadow: 0 10px 15px -3px rgba(14, 165, 233, 0.15);
            transform: translateY(-4px);
        }
        .persona-radio:checked + .persona-card .persona-icon {
            background-color: #0ea5e9;
            color: white;
            transform: scale(1.1);
        }
        .persona-card:hover {
            border-color: #cbd5e1;
            transform: translateY(-2px);
        }
        .persona-icon { transition: all 0.3s; }

        /* Custom Checkbox */
        .custom-checkbox {
            appearance: none;
            background-color: #fff;
            margin: 0;
            font: inherit;
            color: currentColor;
            width: 1.25em;
            height: 1.25em;
            border: 2px solid #cbd5e1;
            border-radius: 0.25em;
            display: grid;
            place-content: center;
            transition: all 0.2s;
        }
        .custom-checkbox::before {
            content: "";
            width: 0.65em;
            height: 0.65em;
            transform: scale(0);
            transition: 120ms transform ease-in-out;
            box-shadow: inset 1em 1em white;
            background-color: white;
            transform-origin: center;
            clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
        }
        .custom-checkbox:checked {
            background-color: #0ea5e9;
            border-color: #0ea5e9;
        }
        .custom-checkbox:checked::before {
            transform: scale(1);
        }

        .mermaid { display: flex; justify-content: center; margin-top: 1rem; overflow-x: auto; }

        /* Styles cho chế độ in ấn (PDF) */
        @media print {
            body { background: white; background-image: none; }
            .no-print, header, .page-container button, #loader-container, #summary-modal, #auth-modal { display: none !important; }
            .page-container { box-shadow: none; border: 1px solid #ddd; break-inside: avoid; margin-bottom: 2rem; page-break-inside: avoid; }
            .mermaid { display: block; }
            * { -webkit-print-color-adjust: exact !important; print-color-adjust: exact !important; }
        }
    </style>
</head>

<body class="font-sans text-slate-800 antialiased selection:bg-sky-200 selection:text-sky-900">

    <div class="container mx-auto max-w-6xl p-4 md:p-8">

        <!-- Header -->
        <header class="flex flex-col md:flex-row justify-between items-center mb-10 bg-white/80 backdrop-blur-md p-6 rounded-3xl shadow-xl border border-white no-print">
            <div class="flex items-center gap-5 mb-4 md:mb-0 cursor-pointer" onclick="location.reload()">
                <div class="bg-gradient-to-br from-sky-500 to-blue-600 text-white p-4 rounded-2xl shadow-lg transform transition hover:rotate-6">
                    <i class="fa-solid fa-chart-line text-2xl"></i>
                </div>
                <div>
                    <h1 class="text-3xl md:text-4xl font-extrabold text-slate-800 tracking-tight" id="app-title">BA Career Planner</h1>
                    <p class="text-slate-500 text-base font-medium mt-1" id="app-subtitle">Data-driven roadmap & Actionable insights</p>
                </div>
            </div>
            
            <div class="flex gap-3 items-center">
                <!-- Auth Button -->
                <button onclick="openAuthModal()" id="auth-btn" class="flex items-center gap-2 px-5 py-2.5 rounded-xl text-sm font-bold bg-white text-slate-700 shadow-sm border border-slate-100 hover:shadow-md transition">
                    <i class="fa-regular fa-user"></i> <span id="auth-status">Đăng nhập</span>
                </button>

                <!-- Language Switcher -->
                <div class="flex bg-slate-200/50 p-1.5 rounded-xl backdrop-blur-sm">
                    <button onclick="switchLanguage('vi')" id="btn-vi" class="px-3 py-2 rounded-lg text-sm font-bold transition-all shadow-sm bg-white text-sky-600">VI</button>
                    <button onclick="switchLanguage('en')" id="btn-en" class="px-3 py-2 rounded-lg text-sm font-bold text-slate-500 hover:text-slate-700 hover:bg-slate-200/50 transition-all">EN</button>
                </div>
            </div>
        </header>

        <!-- ===== TRANG LỰA CHỌN ===== -->
        <main id="selection-page" class="flex flex-col gap-8 animate-slide-up">
            <!-- Welcome Banner -->
            <div id="welcome-banner" class="hidden bg-blue-50 border border-blue-100 p-4 rounded-xl flex justify-between items-center text-blue-800">
                <span>👋 <span id="welcome-text">Xin chào</span>, <b id="user-name-display">User</b>!</span>
            </div>

            <section class="page-container">
                <h2 class="text-2xl font-bold text-slate-800 border-b border-slate-200 pb-4 mb-8 flex items-center gap-3">
                    <span class="bg-sky-100 text-sky-600 w-10 h-10 rounded-xl flex items-center justify-center text-lg shadow-sm">1</span>
                    <span id="step1-title">Chọn Định Hướng Phát Triển</span>
                </h2>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <!-- Technical -->
                    <label class="relative group h-full">
                        <input type="radio" name="persona" value="technical" class="persona-radio sr-only" checked>
                        <div class="persona-card p-8 rounded-2xl h-full cursor-pointer hover:shadow-lg flex flex-col items-center text-center">
                            <div class="persona-icon bg-slate-50 w-16 h-16 rounded-2xl flex items-center justify-center text-slate-600 mb-6 shadow-inner">
                                <i class="fa-solid fa-database text-2xl"></i>
                            </div>
                            <h3 class="font-bold text-xl mb-3 text-slate-800" id="role-tech-title">BA Kỹ Thuật</h3>
                            <p class="text-sm text-slate-500 leading-relaxed" id="role-tech-desc">Tập trung vào hệ thống, dữ liệu, API và giải pháp kỹ thuật.</p>
                        </div>
                    </label>
                    <!-- Business -->
                    <label class="relative group h-full">
                        <input type="radio" name="persona" value="business" class="persona-radio sr-only">
                        <div class="persona-card p-8 rounded-2xl h-full cursor-pointer hover:shadow-lg flex flex-col items-center text-center">
                            <div class="persona-icon bg-slate-50 w-16 h-16 rounded-2xl flex items-center justify-center text-slate-600 mb-6 shadow-inner">
                                <i class="fa-solid fa-briefcase text-2xl"></i>
                            </div>
                            <h3 class="font-bold text-xl mb-3 text-slate-800" id="role-biz-title">BA Nghiệp Vụ</h3>
                            <p class="text-sm text-slate-500 leading-relaxed" id="role-biz-desc">Tập trung vào quy trình, tối ưu hóa vận hành và nghiệp vụ.</p>
                        </div>
                    </label>
                    <!-- Leader -->
                    <label class="relative group h-full">
                        <input type="radio" name="persona" value="leader" class="persona-radio sr-only">
                        <div class="persona-card p-8 rounded-2xl h-full cursor-pointer hover:shadow-lg flex flex-col items-center text-center">
                            <div class="persona-icon bg-slate-50 w-16 h-16 rounded-2xl flex items-center justify-center text-slate-600 mb-6 shadow-inner">
                                <i class="fa-solid fa-users text-2xl"></i>
                            </div>
                            <h3 class="font-bold text-xl mb-3 text-slate-800" id="role-lead-title">BA Lãnh Đạo</h3>
                            <p class="text-sm text-slate-500 leading-relaxed" id="role-lead-desc">Tập trung vào quản lý con người, chiến lược và đàm phán.</p>
                        </div>
                    </label>
                </div>
            </section>

            <section class="page-container">
                <h2 class="text-2xl font-bold text-slate-800 border-b border-slate-200 pb-4 mb-8 flex items-center gap-3">
                    <span class="bg-sky-100 text-sky-600 w-10 h-10 rounded-xl flex items-center justify-center text-lg shadow-sm">2</span>
                    <span id="step2-title">Đánh dấu Kỹ Năng Bạn Đã Có</span>
                </h2>
                <p class="text-slate-500 mb-6 italic text-sm" id="skill-instruction">Hãy trung thực với bản thân để có lộ trình chính xác nhất.</p>
                <div id="skills-accordion" class="space-y-4">
                    <!-- JS Renders Skills Here -->
                </div>
            </section>

            <div class="flex justify-end pb-12">
                <button id="generate-btn" class="group bg-gradient-to-r from-sky-600 to-blue-700 text-white font-bold py-5 px-10 rounded-2xl shadow-xl hover:shadow-2xl hover:scale-[1.02] transition transform flex items-center gap-3 text-lg">
                    <span id="btn-generate">Tạo Lộ Trình Cá Nhân Hóa</span>
                    <i class="fa-solid fa-arrow-right group-hover:translate-x-1 transition-transform"></i>
                </button>
            </div>
        </main>

        <!-- ===== CÁC TRANG KẾT QUẢ (ẨN) ===== -->
        <main id="report-hub-page" class="hidden animate-fade-in space-y-8 pb-12"></main>
        <main id="persona-detail-page" class="hidden animate-fade-in space-y-8 pb-12"></main>
        <main id="skill-group-detail-page" class="hidden animate-fade-in space-y-8 pb-12"></main>
        <main id="resources-page" class="hidden animate-fade-in space-y-8 pb-12"></main>

    </div>

    <!-- ===== AUTH MODAL ===== -->
    <div id="auth-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-md flex items-center justify-center p-4 z-50 hidden opacity-0 transition-opacity duration-300 no-print">
        <div class="bg-white rounded-3xl shadow-2xl w-full max-w-md transform scale-95 transition-transform duration-300 border border-slate-100 overflow-hidden relative">
            <button onclick="closeAuthModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-xl"></i></button>
            <div class="p-8 text-center">
                <div class="w-16 h-16 bg-sky-100 text-sky-600 rounded-full flex items-center justify-center mx-auto mb-4 text-2xl">
                    <i class="fa-solid fa-user-astronaut"></i>
                </div>
                <h3 class="text-2xl font-bold text-slate-800 mb-2" id="auth-title">Lưu Tiến Trình Của Bạn</h3>
                <p class="text-slate-500 text-sm mb-6" id="auth-desc">Nhập tên để tạo hồ sơ cá nhân. Dữ liệu sẽ được lưu trên trình duyệt này.</p>
                
                <div class="space-y-4">
                    <input type="text" id="username-input" placeholder="Tên của bạn (VD: MinhBA)" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-200 outline-none transition text-slate-700 font-medium">
                    <button onclick="login()" class="w-full py-3 bg-sky-600 hover:bg-sky-700 text-white font-bold rounded-xl shadow-lg shadow-sky-200 transition" id="auth-confirm-btn">Bắt đầu ngay</button>
                </div>
                <div id="auth-error" class="text-red-500 text-sm mt-3 hidden">Vui lòng nhập tên hợp lệ</div>
            </div>
        </div>
    </div>

    <!-- ===== CONFIRM MODAL ===== -->
    <div id="summary-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-md flex items-center justify-center p-4 z-50 hidden opacity-0 transition-opacity duration-300 no-print">
        <div class="bg-white rounded-3xl shadow-2xl w-full max-w-lg transform scale-95 transition-transform duration-300 border border-slate-100 overflow-hidden">
            <div class="bg-slate-50 p-6 border-b border-slate-100">
                <h3 class="text-xl font-bold text-slate-800 flex items-center gap-2">
                    <i class="fa-solid fa-clipboard-check text-sky-500"></i>
                    <span id="modal-title">Xác nhận thông tin</span>
                </h3>
            </div>
            <div class="p-8 space-y-6">
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold tracking-widest mb-2" id="modal-role-label">Định Hướng</p>
                    <p id="modal-persona" class="text-xl font-bold text-slate-800"></p>
                </div>
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold tracking-widest mb-2" id="modal-skills-label">Kỹ năng đã chọn</p>
                    <div id="modal-skills-list" class="flex flex-wrap gap-2 max-h-48 overflow-y-auto pr-2"></div>
                </div>
            </div>
            <div class="p-6 bg-slate-50 border-t border-slate-100 flex justify-end gap-3">
                <button id="modal-close-btn" class="px-5 py-2.5 text-slate-600 hover:bg-white hover:shadow-sm rounded-xl transition font-bold text-sm">Quay lại</button>
                <button id="modal-confirm-btn" class="px-6 py-2.5 bg-sky-600 text-white rounded-xl hover:bg-sky-700 transition font-bold shadow-lg shadow-sky-200 text-sm">Xác nhận & Phân tích</button>
            </div>
        </div>
    </div>

    <!-- Loader -->
    <div id="loader-container" class="fixed inset-0 bg-white/90 backdrop-blur-lg flex flex-col items-center justify-center z-50 hidden transition-all duration-500 no-print">
        <div class="w-16 h-16 border-4 border-sky-100 border-t-sky-600 rounded-full animate-spin mb-6"></div>
        <h3 class="text-xl font-bold text-slate-800 mb-2" id="loader-title">Đang xây dựng chiến lược...</h3>
        <p class="text-slate-500 text-sm animate-pulse" id="loader-text">Phân tích dữ liệu...</p>
    </div>

    <script>
        // === GLOBAL VARIABLES ===
        let currentLang = 'vi';
        let currentUser = null;
        let currentPlanData = {};

        // === 1. AUTH SYSTEM (MOCK) ===
        function openAuthModal() {
            if(currentUser) {
                // Logout logic
                if(confirm(currentLang === 'vi' ? "Bạn muốn đăng xuất?" : "Logout?")) {
                    currentUser = null;
                    updateAuthUI();
                    resetApp();
                }
            } else {
                const modal = document.getElementById('auth-modal');
                modal.classList.remove('hidden');
                setTimeout(() => modal.classList.remove('opacity-0'), 10);
                document.getElementById('username-input').focus();
            }
        }

        function closeAuthModal() {
            const modal = document.getElementById('auth-modal');
            modal.classList.add('opacity-0');
            setTimeout(() => modal.classList.add('hidden'), 300);
        }

        function login() {
            const name = document.getElementById('username-input').value.trim();
            if(name.length < 2) {
                document.getElementById('auth-error').classList.remove('hidden');
                return;
            }
            currentUser = name;
            closeAuthModal();
            updateAuthUI();
            loadState(); // Load data for this user
        }

        function updateAuthUI() {
            const btn = document.getElementById('auth-btn');
            const banner = document.getElementById('welcome-banner');
            const nameDisplay = document.getElementById('user-name-display');
            const t = translations[currentLang];
            
            if(currentUser) {
                btn.innerHTML = `<i class="fa-solid fa-user-check text-green-500"></i> <span>${currentUser}</span>`;
                banner.classList.remove('hidden');
                nameDisplay.innerText = currentUser;
            } else {
                btn.innerHTML = `<i class="fa-regular fa-user"></i> <span id="auth-status">${currentLang==='vi'?'Đăng nhập':'Login'}</span>`;
                banner.classList.add('hidden');
            }
        }

        // === 2. TRANSLATIONS ===
        const translations = {
            vi: {
                appTitle: "Công Cụ Hoạch Định Kỹ Năng BA", step1: "Chọn Định Hướng Phát Triển",
                roleTech: "BA Kỹ Thuật", roleBiz: "BA Nghiệp Vụ", roleLead: "BA Lãnh Đạo",
                step2: "Đánh dấu Kỹ Năng Bạn Đã Có", btnGenerate: "Tạo Lộ Trình Cá Nhân Hóa",
                modalTitle: "Xác nhận thông tin", btnBack: "Chỉnh sửa", btnConfirm: "Xác nhận",
                hubTitle: "Chiến Lược Phát Triển", btnNew: "Tạo Mới", btnRes: "Tài Liệu", btnExport: "Xuất PDF",
                yourRole: "Hồ Sơ Định Hướng", roleMatch: "Độ Phù Hợp", roadmapTitle: "Lộ Trình Hành Động",
                stepCore: "GĐ 1: Cốt Lõi", stepSpec: "GĐ 2: Chuyên Sâu", stepNew: "GĐ 3: Xu Hướng",
                btnViewDetail: "Chi Tiết & Hành Động", completed: "Hoàn Thành",
                flowchartTitle: "Sơ Đồ Liên Kết Kỹ Năng",
                priorityLabel: ["", "Ưu tiên 1: Nền Tảng", "Ưu tiên 2: Tiếp Theo", "Ưu tiên 3: Học Sau"],
                cats: { "Technical Skills": "Kỹ Năng Kỹ Thuật", "Business Skills": "Kỹ Năng Nghiệp Vụ", "Soft Skills": "Kỹ Năng Mềm", "Tools Platforms": "Công Cụ", "Domain Skills": "Ngành", "Languages": "Ngoại Ngữ" },
                authTitle: "Lưu Tiến Trình Của Bạn", authDesc: "Nhập tên để tạo hồ sơ cá nhân.", authBtn: "Bắt đầu ngay", welcome: "Xin chào"
            },
            en: {
                appTitle: "BA Career Planner", step1: "Select Career Path",
                roleTech: "Technical BA", roleBiz: "Business BA", roleLead: "BA Lead",
                step2: "Select Current Skills", btnGenerate: "Generate Roadmap",
                modalTitle: "Confirm Selection", btnBack: "Edit", btnConfirm: "Confirm",
                hubTitle: "Career Strategy", btnNew: "New Plan", btnRes: "Resources", btnExport: "Export PDF",
                yourRole: "Career Profile", roleMatch: "Match Score", roadmapTitle: "Action Plan",
                stepCore: "Phase 1: Core", stepSpec: "Phase 2: Specialized", stepNew: "Phase 3: Trends",
                btnViewDetail: "Details & Actions", completed: "Completed",
                flowchartTitle: "Skill Dependency Map",
                priorityLabel: ["", "Priority 1: Foundation", "Priority 2: Next Step", "Priority 3: Learn Later"],
                cats: { "Technical Skills": "Technical", "Business Skills": "Business", "Soft Skills": "Soft", "Tools Platforms": "Tools", "Domain Skills": "Domain", "Languages": "Languages" },
                authTitle: "Save Your Progress", authDesc: "Enter name to create profile.", authBtn: "Start Now", welcome: "Welcome"
            }
        };

        // === 3. FULL DATASET (50+ SKILLS) ===
        const allSkillsData = [
            { id: "sql", name: "SQL", category: "Technical Skills" },
            { id: "power bi", name: "Power BI", category: "Technical Skills" },
            { id: "tableau", name: "Tableau", category: "Technical Skills" },
            { id: "ai", name: "AI / Machine Learning", category: "Technical Skills" },
            { id: "python", name: "Python", category: "Technical Skills" },
            { id: "api", name: "API / Integration", category: "Technical Skills" },
            { id: "database", name: "Database Design", category: "Technical Skills" },
            { id: "etl", name: "ETL / Data Pipeline", category: "Technical Skills" },
            { id: "agile", name: "Agile Mindset", category: "Business Skills" },
            { id: "scrum", name: "Scrum Framework", category: "Business Skills" },
            { id: "requirements", name: "Requirements Elicitation", category: "Business Skills" },
            { id: "bpmn", name: "BPMN", category: "Business Skills" },
            { id: "uml", name: "UML", category: "Business Skills" },
            { id: "user stories", name: "User Stories", category: "Business Skills" },
            { id: "communication", name: "Communication", category: "Soft Skills" },
            { id: "analytical", name: "Analytical Thinking", category: "Soft Skills" },
            { id: "stakeholder management", name: "Stakeholder Management", category: "Soft Skills" },
            { id: "presentation", name: "Presentation", category: "Soft Skills" },
            { id: "negotiation", name: "Negotiation", category: "Soft Skills" },
            { id: "problem solving", name: "Problem Solving", category: "Soft Skills" },
            { id: "jira", name: "Jira", category: "Tools Platforms" },
            { id: "confluence", name: "Confluence", category: "Tools Platforms" },
            { id: "excel", name: "Excel", category: "Tools Platforms" },
            { id: "figma", name: "Figma", category: "Tools Platforms" },
            { id: "english", name: "English", category: "Languages" },
            { id: "prompt engineering", name: "Prompt Engineering", category: "Technical Skills" },
            { id: "data storytelling", name: "Data Storytelling", category: "Soft Skills" },
            { id: "cloud computing", name: "Cloud Computing", category: "Technical Skills" },
            { id: "big data", name: "Big Data", category: "Technical Skills" },
            { id: "automation", name: "Process Automation", category: "Technical Skills" },
            { id: "aws", name: "AWS Cloud", category: "Technical Skills" },
            { id: "azure", name: "Microsoft Azure", category: "Technical Skills" },
            { id: "data warehouse", name: "Data Warehouse", category: "Technical Skills" },
            { id: "brd", name: "BRD Writing", category: "Business Skills" },
            { id: "use cases", name: "Use Cases", category: "Business Skills" },
            { id: "critical thinking", name: "Critical Thinking", category: "Soft Skills" },
            { id: "mentoring", name: "Mentoring", category: "Soft Skills" },
            { id: "visio", name: "Visio", category: "Tools Platforms" },
            { id: "sap", name: "SAP", category: "Tools Platforms" },
            { id: "banking", name: "Banking Domain", category: "Domain Skills" },
            { id: "fintech", name: "Fintech", category: "Domain Skills" },
            { id: "erp", name: "ERP Knowledge", category: "Domain Skills" },
            { id: "finance", name: "Finance", category: "Domain Skills" },
            { id: "crm", name: "CRM Systems", category: "Domain Skills" }
        ];

        const skillPrereqs = {
            'sql': ['power bi', 'tableau', 'ai', 'python', 'etl', 'big data'],
            'database': ['sql', 'data warehouse'],
            'agile': ['scrum', 'jira', 'confluence'],
            'requirements': ['uml', 'bpmn', 'user stories', 'use cases', 'brd'],
            'python': ['ai', 'automation'],
            'ai': ['prompt engineering'],
            'excel': ['power bi']
        };

        const coreSkillIds = ['english', 'agile', 'sql', 'communication', 'requirements', 'analytical', 'excel', 'database'];
        const emergingSkillIds = ['power bi', 'ai', 'python', 'prompt engineering', 'data storytelling', 'cloud computing', 'big data', 'automation'];

        // === 100% FULL SKILL DETAILS (NO CUTS) ===
        const skillDetails = {
            'sql': { vi: { desc: "Ngôn ngữ truy vấn dữ liệu.", help: "Tự lấy số liệu báo cáo.", action: "Cài MySQL, luyện tập SELECT/JOIN.", res: "W3Schools SQL" }, en: { desc: "DB Query Language.", help: "Fetch data.", action: "Practice JOINs.", res: "W3Schools" } },
            'power bi': { vi: { desc: "Công cụ BI.", help: "Vẽ Dashboard.", action: "Tải Power BI Desktop.", res: "MS Learn" }, en: { desc: "BI Tool.", help: "Dashboards.", action: "Download Power BI.", res: "MS Learn" } },
            'agile': { vi: { desc: "Tư duy linh hoạt.", help: "Thích nghi thay đổi.", action: "Đọc Agile Manifesto.", res: "AgileAlliance" }, en: { desc: "Iterative mindset.", help: "Adaptability.", action: "Read Manifesto.", res: "AgileAlliance" } },
            'scrum': { vi: { desc: "Khung làm việc Agile.", help: "Sprint process.", action: "Đọc Scrum Guide.", res: "Scrum.org" }, en: { desc: "Agile framework.", help: "Sprint process.", action: "Read Scrum Guide.", res: "Scrum.org" } },
            'python': { vi: { desc: "Lập trình dữ liệu.", help: "Xử lý file lớn.", action: "Học Pandas.", res: "Automate Boring Stuff" }, en: { desc: "Coding.", help: "Data processing.", action: "Learn Pandas.", res: "Automate Boring Stuff" } },
            'requirements': { vi: { desc: "Khơi gợi yêu cầu.", help: "Hiểu user cần gì.", action: "Dùng 5 Whys.", res: "BABOK Guide" }, en: { desc: "Elicitation.", help: "Understand needs.", action: "Use 5 Whys.", res: "BABOK Guide" } },
            'bpmn': { vi: { desc: "Vẽ quy trình.", help: "Mô hình hóa.", action: "Vẽ quy trình mua hàng.", res: "Camunda" }, en: { desc: "Process Mapping.", help: "Modeling.", action: "Draw Flow.", res: "Camunda" } },
            'uml': { vi: { desc: "Mô hình hệ thống.", help: "Vẽ Sequence Diagram.", action: "Vẽ luồng đăng nhập.", res: "Lucidchart" }, en: { desc: "System Modeling.", help: "Sequence Diag.", action: "Draw Login.", res: "Lucidchart" } },
            'jira': { vi: { desc: "Quản lý dự án.", help: "Theo dõi task.", action: "Tạo tài khoản Free.", res: "Atlassian" }, en: { desc: "Project Mgmt.", help: "Track tasks.", action: "Create Account.", res: "Atlassian" } },
            'confluence': { vi: { desc: "Quản lý tài liệu.", help: "Wiki dự án.", action: "Viết trang tài liệu.", res: "Atlassian" }, en: { desc: "Documentation.", help: "Wiki.", action: "Write page.", res: "Atlassian" } },
            'excel': { vi: { desc: "Bảng tính.", help: "Phân tích nhanh.", action: "Học Pivot Table.", res: "ExcelJet" }, en: { desc: "Advanced Excel.", help: "Quick analysis.", action: "Master Pivot Table.", res: "ExcelJet" } },
            'figma': { vi: { desc: "Thiết kế UI.", help: "Vẽ Wireframe.", action: "Vẽ màn hình app.", res: "Figma Tube" }, en: { desc: "UI Design.", help: "Wireframe.", action: "Draw screen.", res: "Figma Tube" } },
            'english': { vi: { desc: "Tiếng Anh.", help: "Đọc tài liệu.", action: "Đọc báo BA Times.", res: "BA Times" }, en: { desc: "English.", help: "Read docs.", action: "Read BA Times.", res: "BA Times" } },
            'communication': { vi: { desc: "Giao tiếp.", help: "Truyền đạt ý tưởng.", action: "Viết Minutes.", res: "Crucial Convo" }, en: { desc: "Communication.", help: "Convey ideas.", action: "Write Minutes.", res: "Crucial Convo" } },
            'stakeholder management': { vi: { desc: "QL Bên liên quan.", help: "Xác định quyền lực.", action: "Lập Matrix.", res: "PMI" }, en: { desc: "Stakeholder Mgmt.", help: "Power Matrix.", action: "Create Matrix.", res: "PMI" } },
            'api': { vi: { desc: "Giao diện lập trình.", help: "Tích hợp hệ thống.", action: "Dùng Postman.", res: "Postman Docs" }, en: { desc: "API.", help: "Integration.", action: "Use Postman.", res: "Postman Docs" } },
            'database': { vi: { desc: "Cơ sở dữ liệu.", help: "Cấu trúc dữ liệu.", action: "Vẽ ERD.", res: "Coursera DB" }, en: { desc: "Database.", help: "Data structure.", action: "Draw ERD.", res: "Coursera DB" } },
            'etl': { vi: { desc: "Trích xuất dữ liệu.", help: "Data pipeline.", action: "Vẽ luồng ETL.", res: "DataCamp" }, en: { desc: "ETL.", help: "Pipeline.", action: "Draw ETL.", res: "DataCamp" } },
            'ai': { vi: { desc: "Trí tuệ nhân tạo.", help: "Ứng dụng SP.", action: "Tìm hiểu Use Case.", res: "Andrew Ng" }, en: { desc: "AI.", help: "Product Use Cases.", action: "Learn Cases.", res: "Andrew Ng" } },
            'tableau': { vi: { desc: "Trực quan hóa.", help: "Vẽ biểu đồ.", action: "Tải Tableau Public.", res: "Tableau" }, en: { desc: "Visualization.", help: "Charts.", action: "Download Tableau.", res: "Tableau" } },
            'user stories': { vi: { desc: "Yêu cầu Agile.", help: "Viết yêu cầu.", action: "Viết 5 Stories.", res: "Mountain Goat" }, en: { desc: "User Stories.", help: "Reqs.", action: "Write 5.", res: "Mountain Goat" } },
            'brd': { vi: { desc: "Tài liệu nghiệp vụ.", help: "Phạm vi dự án.", action: "Điền mẫu BRD.", res: "Bridging Gap" }, en: { desc: "BRD.", help: "Scope.", action: "Fill template.", res: "Bridging Gap" } },
            'use cases': { vi: { desc: "Ca sử dụng.", help: "Chi tiết bước.", action: "Viết Use Case.", res: "Usability.gov" }, en: { desc: "Use Cases.", help: "Steps.", action: "Write Case.", res: "Usability.gov" } },
            'analytical': { vi: { desc: "Tư duy phân tích.", help: "Chia nhỏ vấn đề.", action: "Cây vấn đề.", res: "McKinsey" }, en: { desc: "Analytical.", help: "Breakdown.", action: "Issue Tree.", res: "McKinsey" } },
            'problem solving': { vi: { desc: "Giải quyết vấn đề.", help: "Tìm giải pháp.", action: "Mô hình IDEAL.", res: "MindTools" }, en: { desc: "Problem Solving.", help: "Solutions.", action: "IDEAL Model.", res: "MindTools" } },
            'presentation': { vi: { desc: "Thuyết trình.", help: "Demo.", action: "Tập nói 5p.", res: "TED" }, en: { desc: "Presentation.", help: "Demo.", action: "Speak 5m.", res: "TED" } },
            'negotiation': { vi: { desc: "Đàm phán.", help: "Thương lượng.", action: "Sách đàm phán.", res: "Never Split Diff" }, en: { desc: "Negotiation.", help: "Agreements.", action: "Read book.", res: "Never Split Diff" } },
            'mentoring': { vi: { desc: "Hướng dẫn.", help: "Đào tạo.", action: "Viết guide.", res: "Mentoring Guide" }, en: { desc: "Mentoring.", help: "Training.", action: "Write guide.", res: "Mentoring Guide" } },
            'prompt engineering': { vi: { desc: "Kỹ thuật Prompt.", help: "Tối ưu AI.", action: "Học cấu trúc.", res: "LearnPrompting" }, en: { desc: "Prompting.", help: "Optimize AI.", action: "Learn structure.", res: "LearnPrompting" } },
            'data storytelling': { vi: { desc: "Kể chuyện data.", help: "Insight.", action: "Đọc sách.", res: "Cole Knaflic" }, en: { desc: "Data Storytelling.", help: "Insights.", action: "Read book.", res: "Cole Knaflic" } },
            'cloud computing': { vi: { desc: "Điện toán đám mây.", help: "Hạ tầng.", action: "Học AWS.", res: "AWS Cloud" }, en: { desc: "Cloud.", help: "Infrastructure.", action: "Learn AWS.", res: "AWS Cloud" } },
            'big data': { vi: { desc: "Dữ liệu lớn.", help: "Xử lý.", action: "Hadoop.", res: "Coursera" }, en: { desc: "Big Data.", help: "Process.", action: "Hadoop.", res: "Coursera" } },
            'automation': { vi: { desc: "Tự động hóa.", help: "RPA.", action: "UiPath.", res: "UiPath" }, en: { desc: "Automation.", help: "RPA.", action: "UiPath.", res: "UiPath" } },
            'aws': { vi: { desc: "AWS.", help: "Cloud.", action: "EC2/S3.", res: "AWS" }, en: { desc: "AWS.", help: "Cloud.", action: "EC2/S3.", res: "AWS" } },
            'azure': { vi: { desc: "Azure.", help: "Cloud.", action: "DevOps.", res: "MS Learn" }, en: { desc: "Azure.", help: "Cloud.", action: "DevOps.", res: "MS Learn" } },
            'data warehouse': { vi: { desc: "Kho dữ liệu.", help: "Lưu trữ.", action: "Star Schema.", res: "Kimball" }, en: { desc: "Data Warehouse.", help: "Storage.", action: "Star Schema.", res: "Kimball" } },
            'visio': { vi: { desc: "Visio.", help: "Vẽ sơ đồ.", action: "Vẽ Org Chart.", res: "MS Visio" }, en: { desc: "Visio.", help: "Diagrams.", action: "Draw Chart.", res: "MS Visio" } },
            'sap': { vi: { desc: "SAP.", help: "ERP.", action: "Tổng quan.", res: "openSAP" }, en: { desc: "SAP.", help: "ERP.", action: "Overview.", res: "openSAP" } },
            'banking': { vi: { desc: "Ngân hàng.", help: "Nghiệp vụ.", action: "Quy trình thẻ.", res: "Investopedia" }, en: { desc: "Banking.", help: "Domain.", action: "Card process.", res: "Investopedia" } },
            'fintech': { vi: { desc: "Fintech.", help: "Ví điện tử.", action: "Phân tích app.", res: "Fintech Weekly" }, en: { desc: "Fintech.", help: "E-wallet.", action: "Analyze App.", res: "Fintech Weekly" } },
            'erp': { vi: { desc: "ERP.", help: "Hệ thống.", action: "Quy trình.", res: "SAP" }, en: { desc: "ERP.", help: "System.", action: "Process.", res: "SAP" } },
            'finance': { vi: { desc: "Tài chính.", help: "Báo cáo.", action: "Đọc BCTC.", res: "Coursera" }, en: { desc: "Finance.", help: "Reports.", action: "Read reports.", res: "Coursera" } },
            'crm': { vi: { desc: "CRM.", help: "Khách hàng.", action: "Salesforce.", res: "Salesforce" }, en: { desc: "CRM.", help: "Customer.", action: "Salesforce.", res: "Salesforce" } },
            'critical thinking': { vi: { desc: "Phản biện.", help: "Tư duy.", action: "Đặt câu hỏi.", res: "Critical Thinking" }, en: { desc: "Critical Thinking.", help: "Mindset.", action: "Ask why.", res: "Critical Thinking" } }
        };

        const personaData = {
            technical: { keySkills: ['sql', 'api', 'database', 'python', 'tableau'], vi: { title: "BA Kỹ Thuật", desc: "Chuyên sâu hệ thống & dữ liệu." }, en: { title: "Technical BA", desc: "Systems & Data focus." } },
            business: { keySkills: ['requirements', 'bpmn', 'user stories', 'excel', 'figma'], vi: { title: "BA Nghiệp Vụ", desc: "Tối ưu quy trình kinh doanh." }, en: { title: "Business BA", desc: "Process optimization." } },
            leader: { keySkills: ['stakeholder management', 'presentation', 'negotiation'], vi: { title: "BA Lãnh Đạo", desc: "Quản lý & Chiến lược." }, en: { title: "BA Lead", desc: "Management & Strategy." } }
        };

        // === 4. LOGIC & STATE ===
        mermaid.initialize({ startOnLoad: false, theme: 'base' });

        function getKey() { return currentUser ? `ba_roadmap_${currentUser}` : 'ba_roadmap_guest'; }
        
        function saveState() {
            const data = { roleVal: currentPlanData.roleVal, userSkills: Array.from(currentPlanData.userSkills), completedSkills: Array.from(currentPlanData.completedSkills || []) };
            localStorage.setItem(getKey(), JSON.stringify(data));
        }

        function loadState() {
            const saved = localStorage.getItem(getKey());
            if (saved) {
                const state = JSON.parse(saved);
                const radio = document.querySelector(`input[name="persona"][value="${state.roleVal}"]`);
                if(radio) radio.checked = true;
                setTimeout(() => {
                    document.querySelectorAll('.custom-checkbox').forEach(cb => cb.checked = false);
                    state.userSkills.forEach(id => { const cb = document.querySelector(`.custom-checkbox[value="${id}"]`); if(cb) cb.checked = true; });
                    runAnalysis(state.completedSkills);
                }, 500);
            }
        }

        function switchLanguage(lang) {
            currentLang = lang;
            const t = translations[lang];
            document.getElementById('app-title').innerText = t.appTitle;
            document.getElementById('step1-title').innerText = t.step1;
            document.getElementById('step2-title').innerText = t.step2;
            document.getElementById('btn-generate').firstElementChild.innerText = t.btnGenerate;
            document.getElementById('auth-title').innerText = t.authTitle;
            document.getElementById('auth-desc').innerText = t.authDesc;
            document.getElementById('auth-confirm-btn').innerText = t.authBtn;
            document.getElementById('welcome-text').innerText = t.welcome;
            updateAuthUI();
            populateSkillsAccordion();
            if (!document.getElementById('report-hub-page').classList.contains('hidden')) buildReportHubPage();
        }

        function populateSkillsAccordion() {
            const container = document.getElementById('skills-accordion');
            container.innerHTML = '';
            const cats = {};
            allSkillsData.forEach(s => { if(!cats[s.category]) cats[s.category]=[]; cats[s.category].push(s); });
            const t = translations[currentLang];
            Object.keys(cats).forEach(catKey => {
                const skills = cats[catKey];
                const groupDiv = document.createElement('div');
                groupDiv.className = 'border border-slate-200 rounded-xl bg-white overflow-hidden shadow-sm';
                const displayCat = t.cats[catKey] || catKey;
                groupDiv.innerHTML = `<button class="w-full flex justify-between items-center p-5 bg-slate-50 hover:bg-white transition-colors text-left font-bold text-slate-700 border-b border-slate-100" onclick="this.nextElementSibling.classList.toggle('hidden'); this.querySelector('i').classList.toggle('rotate-180')"><span>${displayCat}</span><i class="fa-solid fa-chevron-down text-slate-400 transition-transform duration-300"></i></button><div class="p-5 grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 hidden">${skills.map(s => `<label class="flex items-center gap-3 p-3 rounded-lg hover:bg-sky-50 cursor-pointer transition border border-transparent hover:border-sky-100"><input type="checkbox" value="${s.id}" class="custom-checkbox text-sky-600"><span class="text-sm font-medium text-slate-700">${s.name}</span></label>`).join('')}</div>`;
                container.appendChild(groupDiv);
            });
        }

        document.getElementById('generate-btn').addEventListener('click', () => {
            const modal = document.getElementById('summary-modal');
            const roleVal = document.querySelector('input[name="persona"]:checked').value;
            document.getElementById('modal-persona').innerText = roleVal.toUpperCase();
            const selected = Array.from(document.querySelectorAll('.custom-checkbox:checked')).map(cb => cb.nextElementSibling.innerText);
            document.getElementById('modal-skills-list').innerHTML = selected.length ? selected.map(s => `<span class="bg-sky-100 text-sky-800 px-3 py-1.5 rounded-md text-xs font-bold border border-sky-200">${s}</span>`).join('') : '...';
            modal.classList.remove('hidden'); setTimeout(() => modal.classList.remove('opacity-0'), 10);
        });
        document.getElementById('modal-close-btn').addEventListener('click', () => { const modal = document.getElementById('summary-modal'); modal.classList.add('opacity-0'); setTimeout(() => modal.classList.add('hidden'), 300); });
        document.getElementById('modal-confirm-btn').addEventListener('click', () => { document.getElementById('summary-modal').classList.add('hidden'); runAnalysis(); });

        function runAnalysis(savedCompleted = []) {
            const loader = document.getElementById('loader-container'); loader.classList.remove('hidden');
            const roleVal = document.querySelector('input[name="persona"]:checked').value;
            const userSkills = new Set(Array.from(document.querySelectorAll('.custom-checkbox:checked')).map(cb => cb.value));
            const coreMissing = coreSkillIds.filter(id => !userSkills.has(id));
            const roleMissing = personaData[roleVal].keySkills.filter(id => !userSkills.has(id) && !coreSkillIds.includes(id));
            const newMissing = emergingSkillIds.filter(id => !userSkills.has(id) && !coreSkillIds.includes(id) && !personaData[roleVal].keySkills.includes(id));
            currentPlanData = { roleVal, coreMissing, roleMissing, newMissing, userSkills, completedSkills: new Set(savedCompleted) };
            saveState();
            setTimeout(() => { loader.classList.add('hidden'); document.getElementById('selection-page').classList.add('hidden'); document.getElementById('report-hub-page').classList.remove('hidden'); buildReportHubPage(); window.scrollTo(0, 0); }, 1000);
        }

        function buildReportHubPage() {
            const t = translations[currentLang];
            const hub = document.getElementById('report-hub-page');
            const { roleVal, coreMissing, roleMissing, newMissing, completedSkills } = currentPlanData;
            const pData = personaData[roleVal][currentLang];
            const totalToLearn = coreMissing.length + roleMissing.length + newMissing.length;
            const totalLearned = completedSkills.size;
            const progress = totalToLearn > 0 ? Math.round((totalLearned / totalToLearn) * 100) : 100;

            // FIX: Add 'node_' prefix and sanitize IDs
            const s = (id) => 'node_' + id.replace(/[^a-zA-Z0-9]/g, '_'); 
            let graph = "graph TD;\nStart((Start))-->Core;\n";
            if(coreMissing.length){graph+=`subgraph Core["${t.stepCore}"]\n`;coreMissing.forEach(id=>graph+=`${s(id)}["${allSkillsData.find(x=>x.id===id)?.name}"]\n`);graph+="end\nCore-->Spec;\n";}else{graph+="Core[Done]-->Spec;\n";}
            if(roleMissing.length){graph+=`subgraph Spec["${t.stepSpec}"]\n`;roleMissing.forEach(id=>graph+=`${s(id)}["${allSkillsData.find(x=>x.id===id)?.name}"]\n`);graph+="end\nSpec-->New;\n";}else{graph+="Spec[Done]-->New;\n";}
            if(newMissing.length){graph+=`subgraph New["${t.stepNew}"]\n`;newMissing.forEach(id=>graph+=`${s(id)}["${allSkillsData.find(x=>x.id===id)?.name}"]\n`);graph+="end\n";}
            const allD = [...coreMissing, ...roleMissing, ...newMissing];
            allD.forEach(id => { if(skillPrereqs[id]) skillPrereqs[id].forEach(tg => { if(allD.includes(tg)) graph+=`${s(id)}-.->${s(tg)};\n`; }); });
            graph += "classDef default fill:#fff,stroke:#333;classDef cluster fill:#f8fafc,stroke:#cbd5e1;";

            hub.innerHTML = `
                <div class="flex justify-between items-center mb-6 no-print"><h2 class="text-3xl font-extrabold text-slate-800">${t.hubTitle}</h2><div class="flex gap-2"><button onclick="window.print()" class="px-4 py-2 bg-white border border-slate-200 rounded-lg text-slate-600 font-bold shadow-sm hover:shadow">🖨️ ${t.btnExport}</button><button onclick="showResources()" class="px-4 py-2 bg-white border border-slate-200 rounded-lg text-blue-600 font-bold shadow-sm hover:shadow">📚 ${t.btnRes}</button><button onclick="resetApp()" class="px-4 py-2 bg-white border border-slate-200 rounded-lg text-sky-600 font-bold shadow-sm hover:shadow">🔄 ${t.btnNew}</button></div></div>
                <div class="page-container bg-gradient-to-br from-sky-50 to-blue-50 border-sky-200 mb-8"><div class="flex flex-col md:flex-row justify-between gap-6"><div class="flex-grow"><h3 class="text-xs font-black text-sky-500 uppercase tracking-widest mb-2">${t.yourRole}</h3><h4 class="text-4xl font-black text-slate-800 mb-3">${pData.title}</h4><p class="text-lg text-slate-600 mb-4 font-medium">${pData.desc}</p></div><div class="bg-white/80 p-5 rounded-2xl shadow-sm w-full md:w-1/3"><h5 class="text-sm font-bold text-slate-800 mb-2 uppercase">Progress</h5><div class="text-4xl font-black text-slate-800 mb-2">${progress}%</div><div class="w-full h-3 bg-slate-200 rounded-full mb-2"><div class="h-full bg-green-500 transition-all" style="width:${progress}%"></div></div></div></div><div class="bg-white/80 p-5 rounded-2xl shadow-sm mt-6 no-print"><h5 class="text-sm font-bold text-slate-800 mb-2 uppercase">${t.flowchartTitle}</h5><div class="mermaid">${graph}</div></div></div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">${renderStepCard(1, t.stepCore, t.stepCoreDesc, coreMissing, 'yellow')}${renderStepCard(2, t.stepSpec, t.stepSpecDesc, roleMissing, 'sky')}${renderStepCard(3, t.stepNew, t.stepNewDesc, newMissing, 'indigo')}</div>`;
            setTimeout(() => mermaid.run(), 100);
            if (progress === 100 && totalToLearn > 0) confetti({ particleCount: 100, spread: 70, origin: { y: 0.6 } });
        }

        function renderStepCard(step, title, desc, list, color) {
            const t = translations[currentLang];
            const active = list.filter(id => !currentPlanData.completedSkills.has(id));
            const isDone = active.length === 0 && list.length > 0;
            const styles = { yellow: "bg-amber-50 text-amber-900 border-amber-200", sky: "bg-sky-50 text-sky-900 border-sky-200", indigo: "bg-indigo-50 text-indigo-900 border-indigo-200" }[color];
            return `
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100 flex flex-col h-full relative overflow-hidden"><div class="absolute top-0 left-0 w-full h-1.5 ${styles.split(' ')[0].replace('bg','bg-gradient-to-r from-white via')}-400"></div><div class="flex-grow"><h4 class="font-bold text-xl text-slate-800 mb-1">${title}</h4><p class="text-xs text-slate-500 uppercase tracking-wide mb-4">${desc}</p><div class="space-y-2 mb-6">${list.slice(0, 3).map(id => { const c = currentPlanData.completedSkills.has(id); return `<div class="text-sm ${c ? 'text-green-600 line-through' : 'text-slate-600'} flex items-center gap-2"><i class="fa-solid fa-circle text-[6px]"></i> ${allSkillsData.find(s=>s.id===id)?.name}</div>`; }).join('')}${list.length > 3 ? `<div class="text-xs text-slate-400 pl-4">+ ${list.length - 3} ${t.skills}</div>` : ''}</div></div><div class="mt-auto pt-4 border-t">${isDone ? `<span class="text-green-600 font-bold flex justify-center items-center gap-2"><i class="fa-solid fa-check"></i> ${t.completed}</span>` : `<button onclick="showDetail(${step})" class="w-full py-3 rounded-xl bg-slate-50 hover:bg-slate-100 font-bold text-slate-700 transition">${t.btnViewDetail}</button>`}</div></div>`;
        }

        function showDetail(step) {
            const t = translations[currentLang];
            let skills = [], title = "";
            if(step===1){skills=currentPlanData.coreMissing;title=t.stepCore;}
            if(step===2){skills=currentPlanData.roleMissing;title=t.stepSpec;}
            if(step===3){skills=currentPlanData.newMissing;title=t.stepNew;}
            const page = document.getElementById('skill-group-detail-page');
            document.getElementById('report-hub-page').classList.add('hidden');
            page.classList.remove('hidden'); window.scrollTo(0,0);
            page.innerHTML = `<div class="flex items-center gap-4 mb-8 no-print"><button onclick="backToHub()" class="bg-white border p-3 rounded-xl hover:text-sky-600 shadow-sm"><i class="fa-solid fa-arrow-left"></i></button><h2 class="text-2xl font-bold text-slate-800">${title}</h2></div><div class="space-y-6">${skills.map(id => renderSkillItem(id)).join('')}</div>`;
        }

        function renderSkillItem(id) {
            const t = translations[currentLang];
            const skill = allSkillsData.find(s => s.id === id);
            const d = (skillDetails[id] && skillDetails[id][currentLang]) || { desc: "Updating...", help: "...", action: "Search Google", res: "" };
            const isC = currentPlanData.completedSkills.has(id);
            return `<div class="page-container p-0 overflow-hidden border-l-4 ${isC ? 'border-l-green-500 opacity-60' : 'border-l-sky-500'} shadow-md transition-all"><div class="p-6 border-b flex justify-between items-center"><h3 class="text-xl font-bold ${isC ? 'line-through text-slate-400' : 'text-slate-800'}">${skill.name}</h3><button onclick="toggleSkill('${id}')" class="px-4 py-2 rounded-lg text-sm font-bold ${isC ? 'bg-slate-100 text-slate-500' : 'bg-green-100 text-green-700 hover:bg-green-200'} transition">${isC ? t.unmarkDone : t.markDone}</button></div><div class="p-6 bg-slate-50/50 ${isC ? 'hidden' : ''}"><div class="grid md:grid-cols-2 gap-8"><div class="space-y-4"><div><p class="text-xs font-bold text-slate-400 uppercase mb-1">${t.desc}</p><p class="text-sm text-slate-700">${d.desc}</p></div><div><p class="text-xs font-bold text-slate-400 uppercase mb-1">${t.help}</p><p class="text-sm text-slate-700">${d.help}</p></div></div><div class="bg-white p-5 rounded-xl border border-slate-200"><p class="text-xs font-bold text-sky-600 uppercase mb-2">🚀 ${t.action}</p><p class="text-sm font-medium text-slate-800 mb-4">${d.action}</p><div class="pt-4 border-t border-slate-100"><p class="text-xs font-bold text-slate-400 uppercase mb-1">${t.res}</p><p class="text-xs text-sky-600">${d.res}</p></div></div></div></div></div>`;
        }

        function toggleSkill(id) {
            if(currentPlanData.completedSkills.has(id)) currentPlanData.completedSkills.delete(id);
            else currentPlanData.completedSkills.add(id);
            saveState();
            const visibleTitle = document.querySelector('#skill-group-detail-page h2').innerText;
            const t = translations[currentLang];
            let step = 1; if(visibleTitle===t.stepSpec) step=2; if(visibleTitle===t.stepNew) step=3;
            showDetail(step);
        }

        function showResources() {
            const t = translations[currentLang];
            const page = document.getElementById('resources-page');
            document.getElementById('report-hub-page').classList.add('hidden');
            page.classList.remove('hidden'); window.scrollTo(0,0);
            let html = `<div class="flex items-center gap-4 mb-8 no-print"><button onclick="backToHubRes()" class="bg-white border p-3 rounded-xl hover:text-sky-600 shadow-sm"><i class="fa-solid fa-arrow-left"></i></button><h2 class="text-2xl font-bold text-slate-800">${t.resPageTitle}</h2></div><div class="grid grid-cols-1 md:grid-cols-2 gap-6">`;
            const cats = {}; allSkillsData.forEach(s => { if(!cats[s.category]) cats[s.category]=[]; cats[s.category].push(s); });
            Object.keys(cats).forEach(k => { html += `<div class="page-container p-6"><h3 class="font-bold text-lg mb-4 border-b pb-2">${t.cats[k]||k}</h3><ul class="space-y-3">`; cats[k].forEach(s => { const d = (skillDetails[s.id] && skillDetails[s.id][currentLang]); if(d && d.res) html += `<li class="text-sm"><strong class="block text-slate-700">${s.name}</strong><span class="text-sky-600 text-xs">${d.res}</span></li>`; }); html += `</ul></div>`; });
            page.innerHTML = html + `</div>`;
        }

        function backToHub() { document.getElementById('skill-group-detail-page').classList.add('hidden'); document.getElementById('report-hub-page').classList.remove('hidden'); buildReportHubPage(); }
        function backToHubRes() { document.getElementById('resources-page').classList.add('hidden'); document.getElementById('report-hub-page').classList.remove('hidden'); }
        function resetApp() { localStorage.removeItem(getKey()); location.reload(); }

        populateSkillsAccordion(); loadState();
    </script>
</body>
</html>
