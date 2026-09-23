<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ôn Tập Tin Học 12 - Bài 3: Một Số Thiết Bị Mạng Thông Dụng</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        .perspective-1000 { perspective: 1000px; }
        .transform-style-3d { transform-style: preserve-3d; }
        .backface-hidden { backface-visibility: hidden; }
        .rotate-y-180 { transform: rotateY(180deg); }
    </style>
</head>
<body class="bg-slate-50 min-h-screen text-slate-800 flex flex-col">

    <!-- Header -->
    <header class="bg-gradient-to-r from-blue-700 via-indigo-700 to-cyan-600 text-white shadow-lg sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4 py-3 flex flex-wrap justify-between items-center gap-2">
            <div class="flex items-center space-x-3">
                <div class="bg-white/10 p-2 rounded-lg backdrop-blur-sm">
                    <i data-lucide="network" class="w-6 h-6 text-cyan-200"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg leading-tight">TIN HỌC 12 - KẾT NỐI TRI THỨC</h1>
                    <p class="text-xs text-cyan-100">Bài 3: Một số thiết bị mạng thông dụng</p>
                </div>
            </div>
            <!-- Navigation Tabs -->
            <nav class="flex space-x-1 bg-black/20 p-1 rounded-xl text-sm font-medium">
                <button onclick="switchTab('quiz')" id="tab-quiz" class="px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 bg-white text-blue-700 shadow">
                    <i data-lucide="file-question" class="w-4 h-4"></i> Luyện Tập & Bài Thi
                </button>
                <button onclick="switchTab('theory')" id="tab-theory" class="px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 text-white/80 hover:text-white hover:bg-white/10">
                    <i data-lucide="book-open" class="w-4 h-4"></i> Lý Thuyết
                </button>
                <button onclick="switchTab('flashcards')" id="tab-flashcards" class="px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 text-white/80 hover:text-white hover:bg-white/10">
                    <i data-lucide="layers" class="w-4 h-4"></i> Flashcards
                </button>
            </nav>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-5xl mx-auto px-4 py-6 flex-1 w-full">

        <!-- TAB 1: QUIZ SECTION -->
        <section id="section-quiz" class="space-y-6">
            <!-- Mode & Filter Selector Card -->
            <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-200 flex flex-wrap justify-between items-center gap-4">
                <div class="flex items-center gap-3">
                    <span class="text-sm font-semibold text-slate-500 uppercase tracking-wider">Chế độ:</span>
                    <div class="inline-flex rounded-xl bg-slate-100 p-1">
                        <button onclick="setMode('practice')" id="mode-practice" class="px-4 py-1.5 rounded-lg text-sm font-medium transition bg-white text-blue-600 shadow-sm">
                            <i data-lucide="sparkles" class="w-4 h-4 inline mr-1"></i> Luyện Tập (Có Nút Kiểm Tra)
                        </button>
                        <button onclick="setMode('exam')" id="mode-exam" class="px-4 py-1.5 rounded-lg text-sm font-medium transition text-slate-600 hover:text-slate-900">
                            <i data-lucide="timer" class="w-4 h-4 inline mr-1"></i> Thi Thử (Bấm Giờ)
                        </button>
                    </div>
                </div>

                <div id="exam-timer-box" class="hidden flex items-center gap-2 bg-amber-50 text-amber-800 font-bold px-4 py-1.5 rounded-xl border border-amber-200">
                    <i data-lucide="clock" class="w-4 h-4 animate-pulse"></i>
                    <span>Thời gian: <span id="timer-display">20:00</span></span>
                </div>
            </div>

            <!-- Quiz Main View -->
            <div id="quiz-container" class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                <!-- Progress Header -->
                <div class="bg-slate-50 border-b border-slate-200 px-6 py-4 flex justify-between items-center">
                    <div class="flex items-center space-x-2">
                        <span class="text-xs font-bold text-blue-600 bg-blue-100 px-2.5 py-1 rounded-full uppercase tracking-wider" id="q-category">
                            Trắc Nghiệm
                        </span>
                        <span class="text-sm font-semibold text-slate-600" id="q-counter">Câu 1/20</span>
                    </div>
                    <div class="w-1/3 bg-slate-200 rounded-full h-2.5 overflow-hidden">
                        <div id="progress-bar" class="bg-blue-600 h-2.5 rounded-full transition-all duration-300" style="width: 5%"></div>
                    </div>
                </div>

                <!-- Question Body -->
                <div class="p-6 md:p-8 space-y-6">
                    <h2 id="q-text" class="text-lg md:text-xl font-bold text-slate-800 leading-snug">
                        Đang tải câu hỏi...
                    </h2>

                    <!-- Options Container -->
                    <div id="q-options" class="space-y-3">
                        <!-- Options injected by JS -->
                    </div>

                    <!-- Explanation Box (Appears after Check in Practice Mode or after Submission) -->
                    <div id="explanation-box" class="hidden bg-slate-50 border-l-4 border-blue-500 p-4 rounded-r-xl space-y-2">
                        <div class="flex items-center gap-2 text-blue-800 font-semibold text-sm">
                            <i data-lucide="info" class="w-4 h-4"></i> Lời giải chi tiết:
                        </div>
                        <p id="explanation-text" class="text-slate-700 text-sm leading-relaxed"></p>
                    </div>
                </div>

                <!-- Footer Navigation Buttons -->
                <div class="bg-slate-50 border-t border-slate-200 px-6 py-4 flex justify-between items-center">
                    <button onclick="prevQuestion()" id="btn-prev" class="px-4 py-2 rounded-xl text-slate-600 hover:bg-slate-200 font-medium text-sm flex items-center gap-1 disabled:opacity-40">
                        <i data-lucide="chevron-left" class="w-4 h-4"></i> Câu trước
                    </button>

                    <div class="flex gap-2">
                        <!-- Practice Mode Check Button -->
                        <button onclick="checkAnswerPractice()" id="btn-check" class="px-5 py-2 rounded-xl bg-amber-500 hover:bg-amber-600 text-white font-medium text-sm flex items-center gap-1.5 shadow-sm transition">
                            <i data-lucide="check-circle" class="w-4 h-4"></i> Kiểm Tra Đáp Án
                        </button>

                        <button onclick="nextQuestion()" id="btn-next" class="px-5 py-2 rounded-xl bg-blue-600 hover:bg-blue-700 text-white font-medium text-sm flex items-center gap-1 shadow-sm transition">
                            Tiếp theo <i data-lucide="chevron-right" class="w-4 h-4"></i>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Quiz Results / Summary Modal (Hidden by default) -->
            <div id="result-modal" class="hidden fixed inset-0 bg-black/50 backdrop-blur-sm z-50 flex items-center justify-center p-4">
                <div class="bg-white rounded-3xl max-w-lg w-full p-6 text-center space-y-5 shadow-2xl animate-in fade-in zoom-in duration-200">
                    <div class="w-16 h-16 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center mx-auto">
                        <i data-lucide="trophy" class="w-8 h-8"></i>
                    </div>
                    <h3 class="text-2xl font-bold text-slate-800">Kết Quả Bài Thi</h3>
                    <div class="bg-slate-50 p-4 rounded-2xl flex justify-around items-center border border-slate-100">
                        <div>
                            <p class="text-xs text-slate-500 font-medium">ĐIỂM SỐ</p>
                            <p id="res-score" class="text-3xl font-extrabold text-blue-600">0 / 10</p>
                        </div>
                        <div class="w-px h-10 bg-slate-200"></div>
                        <div>
                            <p class="text-xs text-slate-500 font-medium">SỐ CÂU ĐÚNG</p>
                            <p id="res-correct" class="text-3xl font-extrabold text-emerald-600">0 / 20</p>
                        </div>
                    </div>
                    <p id="res-feedback" class="text-sm text-slate-600 italic">Em đã nắm rất tốt kiến thức bài học!</p>
                    <div class="flex gap-3">
                        <button onclick="closeResultModal()" class="flex-1 py-3 bg-slate-200 hover:bg-slate-300 font-semibold text-slate-700 rounded-xl text-sm transition">Xem Lại Bài Làm</button>
                        <button onclick="restartQuiz()" class="flex-1 py-3 bg-blue-600 hover:bg-blue-700 font-semibold text-white rounded-xl text-sm transition shadow-md">Làm Lai Bài Thi</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- TAB 2: THEORY SECTION -->
        <section id="section-theory" class="hidden space-y-6">
            <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200">
                <h2 class="text-xl font-bold text-slate-800 mb-4 flex items-center gap-2 border-b pb-3">
                    <i data-lucide="book-open" class="text-blue-600"></i> Tóm Tắt Lý Thuyết Bài 3: Một Số Thiết Bị Mạng Thông Dụng
                </h2>
                
                <div class="grid md:grid-cols-2 gap-4 text-sm leading-relaxed">
                    <!-- Hub vs Switch -->
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 space-y-2">
                        <h3 class="font-bold text-blue-700 text-base border-b pb-1">1. Hub & Switch</h3>
                        <p><strong>Hub:</strong> Phát tán tín hiệu đến <em>tất cả các cổng</em>. Dễ gây xung đột tín hiệu (collision), phù hợp mạng nhỏ gia đình.</p>
                        <p><strong>Switch:</strong> Tạo đường truyền tạm thời <em>đúng giữa thiết bị gửi và nhận</em>. Không gây xung đột, hiệu năng cao, dùng cho mạng vừa và lớn.</p>
                    </div>

                    <!-- WAP -->
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 space-y-2">
                        <h3 class="font-bold text-blue-700 text-base border-b pb-1">2. Wireless Access Point (WAP)</h3>
                        <p>Điểm truy cập không dây giúp các thiết bị đầu cuối kết nối vào mạng LAN bằng <strong>sóng Wi-Fi</strong> mà không cần cáp mạng, mở rộng phạm vi hoạt động của mạng LAN.</p>
                    </div>

                    <!-- Router -->
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 space-y-2">
                        <h3 class="font-bold text-blue-700 text-base border-b pb-1">3. Router (Bộ định tuyến)</h3>
                        <p>Chuyển tiếp và chọn đường (định tuyến) cho gói dữ liệu giữa <strong>các mạng LAN khác nhau</strong> hoặc ra Internet.</p>
                        <p>Có cổng <strong>LAN</strong> (nối LAN nội bộ) và cổng <strong>WAN</strong> (nối với ISP/mạng ngoài).</p>
                    </div>

                    <!-- Modem -->
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 space-y-2">
                        <h3 class="font-bold text-blue-700 text-base border-b pb-1">4. Modem</h3>
                        <p>Viết tắt từ <strong>Modulation</strong> (Điều chế) & <strong>Demodulation</strong> (Giải điều chế).</p>
                        <p>Chuyển đổi tín hiệu số (Digital) từ máy tính thành tín hiệu tương tự (Analog) truyền đi trên môi trường và ngược lại.</p>
                    </div>

                    <!-- Cables & Connectors -->
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 space-y-2 md:col-span-2">
                        <h3 class="font-bold text-blue-700 text-base border-b pb-1">5. Cáp Mạng & Thực Hành Kết Nối</h3>
                        <div class="grid sm:grid-cols-2 gap-2">
                            <p><strong>Cáp có dây:</strong> Dùng cáp xoắn đôi <strong>UTP</strong> với đầu cắm <strong>RJ45</strong> cắm vào cổng RJ45 (kết nối vật lý).</p>
                            <p><strong>Kết nối Wi-Fi:</strong> Tìm trạm thu phát WAP $\rightarrow$ Chọn tên mạng (SSID) $\rightarrow$ Nhập mật khẩu $\rightarrow$ Kết nối.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- TAB 3: FLASHCARDS SECTION -->
        <section id="section-flashcards" class="hidden space-y-6">
            <div class="text-center space-y-2">
                <h2 class="text-xl font-bold text-slate-800">Thẻ Ghi Nhớ (Flashcards)</h2>
                <p class="text-sm text-slate-500">Bấm vào thẻ để lật xem đáp án / định nghĩa</p>
            </div>

            <div class="flex justify-center">
                <div onclick="flipCard()" class="w-full max-w-md h-64 perspective-1000 cursor-pointer">
                    <div id="fc-card" class="relative w-full h-full duration-500 transform-style-3d bg-white rounded-3xl shadow-lg border border-slate-200 p-8 flex items-center justify-center text-center">
                        <!-- Front Face -->
                        <div class="absolute inset-0 backface-hidden p-8 flex flex-col justify-between items-center rounded-3xl bg-gradient-to-br from-blue-500 to-indigo-600 text-white">
                            <span class="text-xs bg-white/20 px-3 py-1 rounded-full font-semibold">Khái Niệm</span>
                            <p id="fc-front" class="text-2xl font-bold">Hub</p>
                            <span class="text-xs text-white/70">Nhấp để lật thẻ ➔</span>
                        </div>
                        <!-- Back Face -->
                        <div class="absolute inset-0 backface-hidden rotate-y-180 p-8 flex flex-col justify-between items-center rounded-3xl bg-slate-800 text-slate-100">
                            <span class="text-xs bg-slate-700 text-cyan-300 px-3 py-1 rounded-full font-semibold">Định Nghĩa / Chức Năng</span>
                            <p id="fc-back" class="text-sm leading-relaxed">Thiết bị kết nối LAN, truyền tín hiệu nhận được từ 1 cổng đến tất cả các cổng còn lại. Dễ gây xung đột tín hiệu.</p>
                            <span class="text-xs text-slate-400">Nhấp để lật lại ↺</span>
                        </div>
                    </div>
                </div>
            </div>

            <div class="flex justify-center items-center gap-4">
                <button onclick="prevFlashcard()" class="p-3 bg-white rounded-full shadow border hover:bg-slate-50 text-slate-700">
                    <i data-lucide="arrow-left" class="w-5 h-5"></i>
                </button>
                <span id="fc-index" class="text-sm font-semibold text-slate-600">1 / 6</span>
                <button onclick="nextFlashcard()" class="p-3 bg-white rounded-full shadow border hover:bg-slate-50 text-slate-700">
                    <i data-lucide="arrow-right" class="w-5 h-5"></i>
                </button>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 py-4 text-center text-xs text-slate-500">
        Trường THPT Lý Thường Kiệt - Ngân hàng câu hỏi trắc nghiệm Tin học 12 (Kết nối tri thức)
    </footer>

    <!-- SCRIPT DATA & LOGIC -->
    <script>
        // --- 20 QUESTIONS DATASET ---
        const questions = [
            {
                id: 1,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Thiết bị mạng nào có chức năng nhận dữ liệu từ một cổng và gửi phát tán đến tất cả các cổng còn lại trong cùng mạng LAN?",
                options: ["Switch", "Hub", "Router", "Modem"],
                correct: 1,
                explanation: "Hub hoạt động theo cơ chế phát tán: khi nhận dữ liệu qua một cổng, tín hiệu sẽ được gửi đến tất cả các cổng còn lại."
            },
            {
                id: 2,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Lý do chính khiến việc sử dụng Hub trong các mạng LAN lớn dễ gây ra hiện tượng xung đột (collision) tín hiệu là gì?",
                options: [
                    "Do Hub không được kết nối với Internet.",
                    "Do Hub phát tán tín hiệu ra tất cả các cổng, làm nhiều máy gửi dữ liệu đồng thời lên đường truyền chung.",
                    "Do Hub không hỗ trợ chuẩn cáp mạng UTP.",
                    "Do Hub chỉ có tối đa 4 cổng kết nối."
                ],
                correct: 1,
                explanation: "Khi nhiều máy tính gửi dữ liệu đồng thời lên Hub, việc tín hiệu bị phát tán rộng khắp sẽ khiến chúng đâm châm vào nhau gây hiện tượng xung đột (collision)."
            },
            {
                id: 3,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Điểm truy cập không dây (Wireless Access Point - WAP) giúp kết nối các thiết bị đầu cuối vào mạng LAN bằng phương thức nào?",
                options: ["Cáp đồng trục", "Sóng Wi-Fi (sóng vô tuyến)", "Cáp quang", "Đường dây điện thoại"],
                correct: 1,
                explanation: "WAP đóng vai trò là trạm thu phát sóng Wi-Fi, kết nối các thiết bị không dây vào mạng cục bộ."
            },
            {
                id: 4,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Để kết nối hai máy tính thuộc hai mạng LAN khác nhau qua môi trường Internet, thiết bị mạng nào bắt buộc phải tham gia vào quá trình định tuyến dữ liệu?",
                options: ["Hub", "Switch", "Router", "Cáp mạng UTP"],
                correct: 2,
                explanation: "Router (Bộ định tuyến) có chức năng dẫn đường cho dữ liệu truyền giữa các mạng LAN khác nhau hoặc nối LAN ra WAN/Internet."
            },
            {
                id: 5,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Cổng WAN trên một Router thông thường được sử dụng cho mục đích nào?",
                options: [
                    "Nối trực tiếp tới các máy tính trong mạng LAN nội bộ.",
                    "Kết nối với mạng diện rộng (WAN) hoặc Modem của nhà cung cấp dịch vụ Internet (ISP).",
                    "Cắm thẻ nhớ chứa dữ liệu cá nhân.",
                    "Cắm cáp màn hình để hiển thị sơ đồ mạng."
                ],
                correct: 1,
                explanation: "Cổng LAN kết nối các máy nội bộ, còn cổng WAN kết nối Router với mạng ngoài (ISP)."
            },
            {
                id: 6,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Thuật ngữ Modem được ghép từ hai từ tiếng Anh nào thể hiện đúng chức năng của thiết bị này?",
                options: [
                    "Module và Demodule",
                    "Modulation và Demodulation",
                    "Model và Modern",
                    "Monitor và Demonstration"
                ],
                correct: 1,
                explanation: "Modem = Modulation (Điều chế tín hiệu) + Demodulation (Giải điều chế tín hiệu)."
            },
            {
                id: 7,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Khi kết nối máy tính vào Internet thông qua đường truyền cáp quang, Modem quang thực hiện nhiệm vụ biến đổi tín hiệu như thế nào?",
                options: [
                    "Chuyển đổi giữa tín hiệu số (Digital) và tín hiệu ánh sáng.",
                    "Chuyển đổi tín hiệu vô tuyến sang tín hiệu âm thanh.",
                    "Tăng tốc độ bộ nhớ RAM của máy tính.",
                    "Chuyển điện áp 220V thành điện áp 12V."
                ],
                correct: 0,
                explanation: "Modem quang chuyển tín hiệu số của máy tính thành tín hiệu ánh sáng truyền qua sợi quang và ngược lại."
            },
            {
                id: 8,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Chuẩn đầu cắm mạng thông dụng được sử dụng ở hai đầu dây cáp xoắn đôi UTP để cắm vào cổng mạng máy tính là loại nào?",
                options: ["USB Type-C", "HDMI", "RJ45", "VGA"],
                correct: 2,
                explanation: "Đầu cắm mạng có dây tiêu chuẩn cho dây cáp UTP kết nối máy tính/Switch là giắc RJ45."
            },
            {
                id: 9,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Thao tác cắm cáp UTP từ máy tính vào cổng LAN của Switch đại diện cho loại kết nối nào?",
                options: ["Kết nối logic", "Kết nối vật lý", "Kết nối đám mây", "Kết nối định tuyến"],
                correct: 1,
                explanation: "Cắm dây cáp vật lý là kết nối vật lý. Để giao tiếp được còn cần thiết lập kết nối logic (địa chỉ IP)."
            },
            {
                id: 10,
                type: "mcq",
                category: "Trắc Nghiệm 4 Lựa Chọn",
                text: "Thao tác đầu tiên để kết nối Wi-Fi trên máy tính chạy Windows 11 là gì?",
                options: [
                    "Nhấp chuột vào biểu tượng sóng Wi-Fi ở góc phải thanh công việc (Taskbar).",
                    "Tháo dây cáp mạng ra khỏi máy tính.",
                    "Mở phần mềm Word để gõ mật khẩu.",
                    "Khởi động lại máy tính."
                ],
                correct: 0,
                explanation: "Trên Windows 11, bước 1 là nhấp chuột vào biểu tượng sóng mạng ở góc phải Taskbar để mở bảng kết nối không dây."
            },
            {
                id: 11,
                type: "tf",
                category: "Trắc Nghiệm Đúng / Sai",
                text: "Khi so sánh giữa Hub và Switch trong mạng LAN, các nhận định sau đây ĐÚNG hay SAI?",
                items: [
                    "a) Hub và Switch đều dùng để kết nối các máy tính trong cùng một mạng LAN.",
                    "b) Switch xác định chính xác cổng kết nối giữa thiết bị gửi và nhận để truyền dữ liệu.",
                    "c) Dùng Hub giúp giảm tối đa hiện tượng xung đột tín hiệu so với Switch.",
                    "d) Mạng LAN có hàng trăm máy tính nên ưu tiên sử dụng Switch nhiều tầng."
                ],
                correct: [true, true, false, true],
                explanation: "Ý c SAI vì Hub làm tăng xung đột tín hiệu, Switch mới là thiết bị giảm thiểu xung đột."
            },
            {
                id: 12,
                type: "tf",
                category: "Trắc Nghiệm Đúng / Sai",
                text: "Đánh giá các phát biểu sau về Điểm truy cập không dây (WAP) và Wi-Fi:",
                items: [
                    "a) Wi-Fi là chữ viết tắt của Wireless Fidelity.",
                    "b) Sử dụng WAP giúp mở rộng phạm vi địa lý làm việc của mạng LAN.",
                    "c) Tất cả máy tính để bàn (PC) luôn tích hợp sẵn khả năng bắt sóng Wi-Fi mà không cần thêm thiết bị.",
                    "d) WAP kết nối các thiết bị không dây thông qua sóng vô tuyến điện."
                ],
                correct: [true, true, false, true],
                explanation: "Ý c SAI vì nhiều máy tính để bàn truyền thống không có card Wi-Fi, cần lắp thêm bảng mạch mở rộng hoặc USB Wi-Fi."
            },
            {
                id: 13,
                type: "tf",
                category: "Trắc Nghiệm Đúng / Sai",
                text: "Xét chức năng của Router (Bộ định tuyến) trong các mệnh đề sau:",
                items: [
                    "a) Router chỉ có thể kết nối các máy tính trong cùng một mạng LAN nội bộ.",
                    "b) Thuật ngữ định tuyến (routing) hàm ý Router chọn đường đi thích hợp để chuyển gói dữ liệu đến đích.",
                    "c) Router gia đình thường được tích hợp luôn bộ thu phát Wi-Fi.",
                    "d) Dữ liệu từ LAN này sang LAN khác qua Internet có thể phải trung chuyển qua nhiều Router."
                ],
                correct: [false, true, true, true],
                explanation: "Ý a SAI vì Router dùng để nối các LAN khác nhau và ra Internet, việc nối nội bộ 1 LAN do Switch/Hub đảm nhận."
            },
            {
                id: 14,
                type: "tf",
                category: "Trắc Nghiệm Đúng / Sai",
                text: "Xét về thiết bị Modem và nguyên lý hoạt động:",
                items: [
                    "a) Modem làm thay đổi hoàn toàn nội dung dữ liệu mang bởi tín hiệu.",
                    "b) Modem GSM cho phép truy cập Internet thông qua SIM điện thoại di động.",
                    "c) Tín hiệu trong mạng LAN là tín hiệu số (Digital).",
                    "d) Ngày nay, chức năng Modem thường được tích hợp sẵn vào Router gia đình."
                ],
                correct: [false, true, true, true],
                explanation: "Ý a SAI vì Modem chỉ thay đổi dạng thức biểu diễn của tín hiệu (tương tự <-> số) chứ không làm thay đổi nội dung dữ liệu."
            },
            {
                id: 15,
                type: "tf",
                category: "Trắc Nghiệm Đúng / Sai",
                text: "Khi thực hành kết nối mạng có dây và không dây:",
                items: [
                    "a) Cáp UTP thông dụng dùng giắc cắm RJ45 có 4 đôi dây xoắn.",
                    "b) Để kết nối Wi-Fi có mật khẩu, bắt buộc phải nhập đúng mật khẩu mạng.",
                    "c) Tích chọn 'Connect automatically' giúp tự động kết nối Wi-Fi cho các lần sau.",
                    "d) Chỉ cần cắm cáp mạng vào cổng RJ45 là máy tính chắc chắn vào được Internet ngay mà không cần cấu hình logic."
                ],
                correct: [true, true, true, false],
                explanation: "Ý d SAI vì cắm dây chỉ là kết nối vật lý, cần có cấu hình logic (Cấp IP, DNS,...) thì mới vào được Internet."
            },
            {
                id: 16,
                type: "matching",
                category: "Nối / Ghép Đôi Thiết Bị",
                text: "Hãy nối các thiết bị mạng ở Cột A với Chức năng chính tương ứng ở Cột B:",
                pairs: [
                    { key: "1. Hub", value: "A. Phát tán tín hiệu ra tất cả các cổng, dễ xung đột" },
                    { key: "2. Switch", value: "B. Thiết lập kênh truyền riêng giữa 2 cổng, hạn chế xung đột" },
                    { key: "3. Router", value: "C. Định tuyến gói dữ liệu giữa các mạng LAN khác nhau" },
                    { key: "4. Modem", value: "D. Điều chế và giải điều chế tín hiệu (Digital <-> Analog)" }
                ],
                explanation: "Hub phát tán -> Switch chia cổng riêng -> Router định tuyến ngoài LAN -> Modem biến đổi tín hiệu."
            },
            {
                id: 17,
                type: "matching",
                category: "Nối / Ghép Đôi Cổng Kết Nối",
                text: "Hãy nối tên loại cổng/thiết bị ở Cột A với đặc điểm phù hợp ở Cột B:",
                pairs: [
                    { key: "1. Cổng RJ45", value: "A. Cổng cắm cáp mạng xoắn đôi UTP trên máy tính hoặc Switch" },
                    { key: "2. Cổng WAN", value: "B. Cổng trên Router dùng để nối ra Modem hoặc ISP" },
                    { key: "3. Modem ADSL", value: "C. Dùng đường dây điện thoại để truyền dữ liệu Internet" },
                    { key: "4. WAP", value: "D. Điểm truy cập không dây phát sóng Wi-Fi" }
                ],
                explanation: "Cổng RJ45 gắn cáp UTP, Cổng WAN nối ISP, ADSL dùng cáp điện thoại, WAP phát Wi-Fi."
            },
            {
                id: 18,
                type: "mcq",
                category: "Vận Dụng Thực Tế",
                text: "Một phòng thực hành Tin học có 40 máy tính để bàn. Thiết bị kết nối trung tâm phù hợp và tối ưu nhất để nối các máy tính này thành mạng LAN là gì?",
                options: ["1 bộ Hub 48 cổng", "1 hoặc 2 Switch quản lý cổng", "1 Modem 3G cắm SIM", "1 Router không dây đơn lẻ"],
                correct: 1,
                explanation: "Mạng 40 máy tính nên dùng Switch để đảm bảo băng thông và tránh xung đột đường truyền."
            },
            {
                id: 19,
                type: "mcq",
                category: "Vận Dụng Thực Tế",
                text: "Khi đi xe khách đường dài, hành khách có thể truy cập Wi-Fi trên xe. Xe khách này thường sử dụng thiết bị mạng nào để cung cấp Internet?",
                options: [
                    "Router Wi-Fi kết nối cáp quang",
                    "Bộ phát Wi-Fi tích hợp Modem GSM (3G/4G/5G cắm SIM)",
                    "Bộ chia tín hiệu Hub nối dây",
                    "Cáp mạng UTP nối từ trạm thu phát cố định"
                ],
                correct: 1,
                explanation: "Xe khách di chuyển liên tục nên dùng Modem GSM cắm SIM 4G/5G phát Wi-Fi cho hành khách."
            },
            {
                id: 20,
                type: "tf",
                category: "Trắc Nghiệm Đúng / Sai - Tổng Hợp",
                text: "Xét các câu hỏi mở rộng về thực hành mạng:",
                items: [
                    "a) Bật chức năng Điểm truy cập di động (Hotspot) trên điện thoại giúp biến điện thoại thành một WAP.",
                    "b) Dây cáp mạng UTP chỉ truyền được tín hiệu vô tuyến.",
                    "c) Mạng Wi-Fi không có biểu tượng khóa là mạng mở, không yêu cầu mật khẩu.",
                    "d) Tên mạng Wi-Fi hiển thị khi tìm kiếm còn được gọi là SSID."
                ],
                correct: [true, false, true, true],
                explanation: "Ý b SAI vì cáp UTP là cáp đồng xoắn đôi truyền tín hiệu điện chứ không phải sóng vô tuyến."
            }
        ];

        // --- FLASHCARDS DATA ---
        const flashcards = [
            { front: "Hub", back: "Bộ chia tín hiệu mạng LAN. Chuyển tín hiệu từ 1 cổng đến TẤT CẢ các cổng còn lại. Dễ gây xung đột (collision)." },
            { front: "Switch", back: "Bộ chuyển mạch. Thiết lập kênh truyền riêng giữa cổng gửi và nhận. Giảm thiểu xung đột, dùng cho mạng LAN vừa và lớn." },
            { front: "WAP (Access Point)", back: "Điểm truy cập không dây. Kết nối thiết bị vào mạng LAN thông qua sóng Wi-Fi." },
            { front: "Router", back: "Bộ định tuyến. Chuyển tiếp dữ liệu giữa các mạng LAN khác nhau hoặc nối LAN ra Internet qua cổng WAN." },
            { front: "Modem", back: "Bộ điều chế & giải điều chế (Modulation/Demodulation). Chuyển tín hiệu số (Digital) thành Analog và ngược lại." },
            { front: "Cáp UTP & RJ45", back: "Cáp xoắn đôi UTP ghép nối với đầu cắm RJ45 dùng cho kết nối mạng có dây vật lý." }
        ];

        // --- APP STATE ---
        let currentIdx = 0;
        let userAnswers = {}; // { qId: answerValue }
        let isChecked = {}; // { qId: boolean }
        let mode = 'practice'; // 'practice' | 'exam'
        let timerInterval = null;
        let timeLeft = 1200; // 20 mins
        let currentFcIdx = 0;
        let isFcFlipped = false;

        // --- INIT APP ---
        document.addEventListener("DOMContentLoaded", () => {
            lucide.createIcons();
            renderQuestion();
            updateFlashcard();
        });

        // --- TAB SWITCHING ---
        function switchTab(tab) {
            document.getElementById('section-quiz').classList.add('hidden');
            document.getElementById('section-theory').classList.add('hidden');
            document.getElementById('section-flashcards').classList.add('hidden');

            document.getElementById('tab-quiz').className = "px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 text-white/80 hover:text-white hover:bg-white/10";
            document.getElementById('tab-theory').className = "px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 text-white/80 hover:text-white hover:bg-white/10";
            document.getElementById('tab-flashcards').className = "px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 text-white/80 hover:text-white hover:bg-white/10";

            if(tab === 'quiz') {
                document.getElementById('section-quiz').classList.remove('hidden');
                document.getElementById('tab-quiz').className = "px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 bg-white text-blue-700 shadow";
            } else if(tab === 'theory') {
                document.getElementById('section-theory').classList.remove('hidden');
                document.getElementById('tab-theory').className = "px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 bg-white text-blue-700 shadow";
            } else if(tab === 'flashcards') {
                document.getElementById('section-flashcards').classList.remove('hidden');
                document.getElementById('tab-flashcards').className = "px-3 py-1.5 rounded-lg transition-all flex items-center gap-1.5 bg-white text-blue-700 shadow";
            }
        }

        // --- MODE SWITCHING ---
        function setMode(newMode) {
            mode = newMode;
            const btnPrac = document.getElementById('mode-practice');
            const btnExam = document.getElementById('mode-exam');
            const timerBox = document.getElementById('exam-timer-box');
            const btnCheck = document.getElementById('btn-check');

            if(mode === 'practice') {
                btnPrac.className = "px-4 py-1.5 rounded-lg text-sm font-medium transition bg-white text-blue-600 shadow-sm";
                btnExam.className = "px-4 py-1.5 rounded-lg text-sm font-medium transition text-slate-600 hover:text-slate-900";
                timerBox.classList.add('hidden');
                btnCheck.classList.remove('hidden');
                clearInterval(timerInterval);
            } else {
                btnExam.className = "px-4 py-1.5 rounded-lg text-sm font-medium transition bg-white text-blue-600 shadow-sm";
                btnPrac.className = "px-4 py-1.5 rounded-lg text-sm font-medium transition text-slate-600 hover:text-slate-900";
                timerBox.classList.remove('hidden');
                btnCheck.classList.add('hidden');
                startTimer();
            }
            renderQuestion();
        }

        function startTimer() {
            clearInterval(timerInterval);
            timeLeft = 1200;
            timerInterval = setInterval(() => {
                timeLeft--;
                let m = Math.floor(timeLeft / 60);
                let s = timeLeft % 60;
                document.getElementById('timer-display').innerText = `${m}:${s < 10 ? '0':''}${s}`;
                if(timeLeft <= 0) {
                    clearInterval(timerInterval);
                    submitExam();
                }
            }, 1000);
        }

        // --- RENDER QUESTION ---
        function renderQuestion() {
            const q = questions[currentIdx];
            document.getElementById('q-category').innerText = q.category;
            document.getElementById('q-counter').innerText = `Câu ${currentIdx + 1}/${questions.length}`;
            document.getElementById('progress-bar').style.width = `${((currentIdx + 1) / questions.length) * 100}%`;
            document.getElementById('q-text').innerText = q.text;

            const optContainer = document.getElementById('q-options');
            optContainer.innerHTML = '';

            const expBox = document.getElementById('explanation-box');
            expBox.classList.add('hidden');

            // Render MCQ
            if (q.type === 'mcq') {
                q.options.forEach((opt, idx) => {
                    const isSelected = userAnswers[q.id] === idx;
                    const btn = document.createElement('button');
                    btn.onclick = () => selectMcqOption(q.id, idx);
                    btn.className = `w-full text-left p-4 rounded-xl border text-sm font-medium transition flex items-center justify-between ${
                        isSelected 
                            ? 'border-blue-600 bg-blue-50/70 text-blue-900 ring-2 ring-blue-500/20' 
                            : 'border-slate-200 hover:bg-slate-50 text-slate-700'
                    }`;
                    btn.innerHTML = `
                        <div class="flex items-center gap-3">
                            <span class="w-7 h-7 rounded-lg font-bold text-xs flex items-center justify-center ${isSelected ? 'bg-blue-600 text-white' : 'bg-slate-100 text-slate-600'}">
                                ${String.fromCharCode(65 + idx)}
                            </span>
                            <span>${opt}</span>
                        </div>
                    `;
                    optContainer.appendChild(btn);
                });
            } 
            // Render True/False
            else if (q.type === 'tf') {
                if (!userAnswers[q.id]) userAnswers[q.id] = [null, null, null, null];
                q.items.forEach((itemText, itemIdx) => {
                    const userChoice = userAnswers[q.id][itemIdx];
                    const row = document.createElement('div');
                    row.className = "p-3.5 bg-slate-50 rounded-xl border border-slate-200 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3";
                    row.innerHTML = `
                        <span class="text-sm font-medium text-slate-800 flex-1">${itemText}</span>
                        <div class="flex gap-2">
                            <button onclick="selectTfOption(${q.id}, ${itemIdx}, true)" class="px-3 py-1.5 rounded-lg text-xs font-bold transition ${
                                userChoice === true ? 'bg-emerald-600 text-white shadow-sm' : 'bg-white border text-slate-600 hover:bg-slate-100'
                            }">Đúng</button>
                            <button onclick="selectTfOption(${q.id}, ${itemIdx}, false)" class="px-3 py-1.5 rounded-lg text-xs font-bold transition ${
                                userChoice === false ? 'bg-rose-600 text-white shadow-sm' : 'bg-white border text-slate-600 hover:bg-slate-100'
                            }">Sai</button>
                        </div>
                    `;
                    optContainer.appendChild(row);
                });
            }
            // Render Matching
            else if (q.type === 'matching') {
                const box = document.createElement('div');
                box.className = "space-y-2 bg-slate-50 p-4 rounded-xl border border-slate-200";
                q.pairs.forEach(p => {
                    box.innerHTML += `
                        <div class="flex justify-between items-center bg-white p-3 rounded-lg border text-sm font-medium text-slate-700">
                            <span>${p.key}</span>
                            <span class="text-blue-600 font-bold">➔ ${p.value}</span>
                        </div>
                    `;
                });
                optContainer.appendChild(box);
            }

            // Handle Check state in Practice Mode
            if (mode === 'practice' && isChecked[q.id]) {
                showExplanation(q);
            }

            // Prev/Next buttons
            document.getElementById('btn-prev').disabled = currentIdx === 0;
            if (currentIdx === questions.length - 1) {
                document.getElementById('btn-next').innerHTML = mode === 'exam' ? 'Nộp Bài Thi <i data-lucide="send" class="w-4 h-4 ml-1 inline"></i>' : 'Hoàn Thành <i data-lucide="check" class="w-4 h-4 ml-1 inline"></i>';
            } else {
                document.getElementById('btn-next').innerHTML = 'Tiếp theo <i data-lucide="chevron-right" class="w-4 h-4 ml-1 inline"></i>';
            }
            lucide.createIcons();
        }

        // --- USER INTERACTIONS ---
        function selectMcqOption(qId, optIdx) {
            userAnswers[qId] = optIdx;
            renderQuestion();
        }

        function selectTfOption(qId, itemIdx, val) {
            if (!userAnswers[qId]) userAnswers[qId] = [null, null, null, null];
            userAnswers[qId][itemIdx] = val;
            renderQuestion();
        }

        function checkAnswerPractice() {
            const q = questions[currentIdx];
            isChecked[q.id] = true;
            showExplanation(q);
        }

        function showExplanation(q) {
            const expBox = document.getElementById('explanation-box');
            const expText = document.getElementById('explanation-text');
            expText.innerText = q.explanation;
            expBox.classList.remove('hidden');
        }

        function prevQuestion() {
            if (currentIdx > 0) {
                currentIdx--;
                renderQuestion();
            }
        }

        function nextQuestion() {
            if (currentIdx < questions.length - 1) {
                currentIdx++;
                renderQuestion();
            } else {
                submitExam();
            }
        }

        // --- SUBMIT / CALCULATE SCORE ---
        function submitExam() {
            let totalCorrect = 0;

            questions.forEach(q => {
                if (q.type === 'mcq') {
                    if (userAnswers[q.id] === q.correct) totalCorrect++;
                } else if (q.type === 'tf') {
                    const ans = userAnswers[q.id] || [];
                    let allRight = true;
                    q.correct.forEach((cVal, cIdx) => {
                        if (ans[cIdx] !== cVal) allRight = false;
                    });
                    if (allRight) totalCorrect++;
                } else if (q.type === 'matching') {
                    totalCorrect++; // Free point for reviewed matching
                }
            });

            const score = ((totalCorrect / questions.length) * 10).toFixed(1);
            document.getElementById('res-score').innerText = `${score} / 10`;
            document.getElementById('res-correct').innerText = `${totalCorrect} / ${questions.length}`;
            
            let feedback = "Hãy tiếp tục ôn tập lại lý thuyết để nắm vững hơn nhé!";
            if(score >= 8) feedback = "Xuất sắc! Em đã nắm rất vững toàn bộ kiến thức Bài 3!";
            else if(score >= 6.5) feedback = "Khá tốt! Hãy rà soát lại các câu làm sai nhé.";
            
            document.getElementById('res-feedback').innerText = feedback;
            document.getElementById('result-modal').classList.remove('hidden');
        }

        function closeResultModal() {
            document.getElementById('result-modal').classList.add('hidden');
        }

        function restartQuiz() {
            currentIdx = 0;
            userAnswers = {};
            isChecked = {};
            closeResultModal();
            if(mode === 'exam') startTimer();
            renderQuestion();
        }

        // --- FLASHCARDS LOGIC ---
        function updateFlashcard() {
            const fc = flashcards[currentFcIdx];
            document.getElementById('fc-front').innerText = fc.front;
            document.getElementById('fc-back').innerText = fc.back;
            document.getElementById('fc-index').innerText = `${currentFcIdx + 1} / ${flashcards.length}`;
            
            // Reset rotation
            isFcFlipped = false;
            document.getElementById('fc-card').classList.remove('rotate-y-180');
        }

        function flipCard() {
            isFcFlipped = !isFcFlipped;
            const card = document.getElementById('fc-card');
            if(isFcFlipped) card.classList.add('rotate-y-180');
            else card.classList.remove('rotate-y-180');
        }

        function prevFlashcard() {
            if(currentFcIdx > 0) {
                currentFcIdx--;
                updateFlashcard();
            }
        }

        function nextFlashcard() {
            if(currentFcIdx < flashcards.length - 1) {
                currentFcIdx++;
                updateFlashcard();
            }
        }
    </script>
</body>
</html>
