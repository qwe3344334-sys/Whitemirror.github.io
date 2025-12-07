# Whitemirror.github.io
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>White Mirror 白鏡美甲 - 預約系統 (分頁版)</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Load Lucide Icons for aesthetic visual elements -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Use Inter font -->
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #e5e7eb; /* Cool Grey 200 - Darker background for depth */
        }
        .ins-card {
            background-color: #ffffff;
            border-radius: 1.5rem; /* Slightly larger radius */
            box-shadow: 
                0 25px 50px -12px rgba(0, 0, 0, 0.25),
                0 0 0 1px rgba(0, 0, 0, 0.05);
            border: 1px solid #f3f4f6;
        }
        /* Updated button style for Silver/Grey Mirror theme - Enhanced Depth */
        .grey-button { 
            background-color: #d1d5db; /* Cool Grey 300 */
            color: #1f2937; /* Dark Slate text */
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), inset 0 2px 4px 0 rgba(0, 0, 0, 0.06); /* Inner shadow for clickable depth */
            border-bottom: 3px solid #9ca3af; /* Stronger bottom border for push effect */
            transition: background-color 0.2s ease, transform 0.1s ease, border-bottom 0.1s ease;
        }
        .grey-button:hover:not(:disabled) {
            background-color: #9ca3af; /* Cooler hover state */
            transform: translateY(1px); /* Push down effect */
            border-bottom: 1px solid #9ca3af;
        }
        .grey-button:disabled {
            background-color: #f3f4f6;
            color: #9ca3af;
            cursor: not-allowed;
            box-shadow: none;
            border-bottom: 3px solid #e5e7eb;
        }
        /* Updated accent color for Deep Slate/Silver */
        .gold-accent {
            color: #374151; /* Deeper Slate Grey for prominence */
            font-weight: 700;
        }
        /* Style for selected date - Stronger contrast */
        .date-selected {
            background-color: #4b5563; /* Deep Slate for selection */
            color: white;
            box-shadow: 0 6px 10px -2px rgba(0, 0, 0, 0.3);
            border: 2px solid #374151;
        }
        .date-available {
             border: 2px solid #e5e7eb;
             box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
        }
        /* Tab Navigation Styles */
        .tab-btn {
            padding: 0.75rem 1.5rem;
            border-radius: 1rem 1rem 0 0;
            font-weight: 600;
            color: #6b7280;
            transition: all 0.2s ease;
            position: relative;
            background-color: #f9fafb;
            border-bottom: 2px solid #e5e7eb;
        }
        .tab-btn.active {
            color: #374151; /* Darker text for active tab */
            background-color: #ffffff;
            border-bottom: 3px solid #374151; /* Strong accent line */
            z-index: 10;
        }

        /* Styling for the Hand Model radio group */
        .radio-scroll-container {
            display: flex;
            overflow-x: auto;
            border: 1px solid #9ca3af;
            border-radius: 0.75rem;
            background-color: #f5f5f5;
        }
        .radio-scroll-item {
            flex: 1 0 auto;
            min-width: 33%; /* Ensure responsiveness on small screens */
            padding: 0.75rem 1.5rem;
            cursor: pointer;
            transition: background-color 0.2s, color 0.2s;
            text-align: center;
            border-right: 1px solid #d1d5db;
        }
        .radio-scroll-item:last-child {
            border-right: none;
        }
        .radio-scroll-item input {
            display: none;
        }
        .radio-scroll-item input:checked + span {
            background-color: #4b5563;
            color: white;
            font-weight: bold;
            border-radius: 0.6rem;
            display: block;
            margin: -0.75rem -1.5rem;
            padding: 0.75rem 1.5rem;
            box-shadow: inset 0 0 8px rgba(0, 0, 0, 0.4);
        }
    </style>
</head>
<body class="p-4 md:p-8 min-h-screen flex justify-center items-start">

    <div id="app" class="w-full max-w-4xl ins-card p-0">

        <!-- Header/Title Section -->
        <header class="text-center pt-8 px-6 md:px-10 border-b pb-4 border-stone-200">
            <div class="flex items-center justify-center mb-4">
                 <i data-lucide="gem" class="w-8 h-8 mr-3 gold-accent"></i>
                 <h1 class="text-5xl font-extralight gold-accent tracking-widest">White mirror</h1>
            </div>
            <h2 class="text-2xl font-bold text-stone-700">白鏡美甲 預約服務</h2>
            <p class="text-sm text-stone-500 mt-2">冷靜、高級、極致簡約的美甲藝術。</p>
        </header>

        <!-- Tab Navigation Bar -->
        <div id="tab-nav" class="flex justify-around bg-stone-100/50 border-b border-stone-300 px-2 md:px-8">
            <button class="tab-btn" data-tab-index="1" onclick="changeTab(1)">
                <i data-lucide="info" class="w-4 h-4 inline mr-2"></i>須知
            </button>
            <button class="tab-btn" data-tab-index="2" onclick="changeTab(2)">
                <i data-lucide="piggy-bank" class="w-4 h-4 inline mr-2"></i>服務價目
            </button>
            <button class="tab-btn" data-tab-index="3" onclick="changeTab(3)">
                <i data-lucide="calendar-check" class="w-4 h-4 inline mr-2"></i>預約流程
            </button>
        </div>

        <!-- Main Content Area -->
        <div class="p-6 md:p-10 space-y-10">

            <!-- Tab 1: Policies (預約須知 & 注意事項) -->
            <div id="tab-content-1" class="tab-content space-y-8">
                <h3 class="text-2xl font-bold gold-accent text-center">--- 白鏡美甲 重要須知 ---</h3>

                <!-- 預約須知 -->
                <div class="p-6 ins-card border-l-4 border-gray-500 shadow-sm">
                    <h4 class="text-xl font-semibold text-stone-700 mb-4 flex items-center">
                        <i data-lucide="file-text" class="w-5 h-5 mr-2 text-gray-700"></i>預約須知 (Booking Policy)
                    </h4>
                    <ul class="text-stone-600 space-y-2 list-disc list-inside text-sm">
                        <!-- CRITICAL POLICY -->
                        <li class="p-2 bg-red-100 border border-red-300 rounded-lg shadow-inner">
                            <span class="font-bold text-red-700">!! 新手美甲師特點 - 務必久坐 !!</span><br>
                            本次服務由新手美甲師施作，請務必空出 4-5 小時，確保有足夠時間完成服務。此為最重要的注意事項！
                        </li>
                        <li>**預約時間：** 目前僅開放每週一、三、四的 12:00, 15:00, 18:00 三個時段。</li>
                        <li>**時段保留：** 成功送出預約後，請務必於 12 小時內透過官方 LINE (@702nkzdn) 聯繫確認細節，否則系統將自動取消預約。</li>
                        <li>
                            **遲到取消：** 遲到超過 <span class="font-bold text-red-500">10 分鐘</span>者，視同自動取消。
                        </li>
                        <li>
                            **改期規定：** 如需改期，請提前 <span class="font-bold text-red-500">3 天 (72 小時)</span> 告知。
                        </li>
                        <li>
                            **重複違規定金政策：** <span class="font-bold text-red-500">若有兩次以上遲到/未提前改期記錄者，下次預約須先支付 $500 定金。</span>
                        </li>
                        <li>**攜伴規定：** 為了提供更舒適的服務空間，請勿攜帶寵物或未預約的親友陪同。</li>
                    </ul>
                </div>

                <!-- 美甲注意事項 -->
                <div class="p-6 ins-card border-l-4 border-gray-500 shadow-sm">
                    <h4 class="text-xl font-semibold text-stone-700 mb-4 flex items-center">
                        <i data-lucide="hand-metal" class="w-5 h-5 mr-2 text-gray-700"></i>美甲注意事項 (Nail Care Precautions)
                    </h4>
                    <ul class="text-stone-600 space-y-2 list-disc list-inside text-sm">
                        <li>**清潔保養：** 美甲後 24 小時內應避免長時間接觸熱水或清潔劑。</li>
                        <li>
                            **日常習慣：** <span class="font-bold text-red-500">請盡量避免用指尖做事</span>，建議使用指腹或工具。
                        </li>
                        <li>
                            **7天售後保固：** 若施作後 <span class="font-bold text-red-500">7 天內</span> 非人為因素造成美甲瑕疵，可免費補受損的指甲。
                        </li>
                        <li>**指甲油/凝膠維護：** 請勿自行摳剝凝膠，若有嚴重破損請儘速回店修補。</li>
                        <li>**基礎護理：** 平日可塗抹指緣油或護手霜加強保濕。</li>
                        <li>**過敏反應：** 若有任何皮膚過敏或不適，請立即停止使用。</li>
                    </ul>
                </div>
                
                <div class="flex justify-center pt-4">
                    <button onclick="changeTab(2)" class="py-2 px-6 bg-stone-700 text-white rounded-xl font-semibold shadow-md hover:bg-stone-800 transition duration-150">
                        查看價目表
                    </button>
                </div>
            </div>

            <!-- Tab 2: Price List (服務價目表) -->
            <div id="tab-content-2" class="tab-content hidden">
                <h3 class="text-2xl font-bold gold-accent text-center mb-6">--- 服務價目表 ---</h3>
                
                <div class="ins-card p-0 overflow-hidden">
                    <div class="bg-stone-100 p-6 md:p-8">
                        <!-- Text Price List -->
                        <table class="min-w-full divide-y divide-stone-300">
                            <thead class="bg-stone-200">
                                <tr>
                                    <th class="px-3 py-3 text-left text-xs font-bold text-stone-700 uppercase tracking-wider">項目</th>
                                    <th class="px-3 py-3 text-right text-xs font-bold text-stone-700 uppercase tracking-wider">價格</th>
                                </tr>
                            </thead>
                            <tbody class="bg-white divide-y divide-stone-200 text-stone-700">
                                <tr>
                                    <td class="px-3 py-3 font-medium">手部保養 - 甘皮、修型</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$250</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">單色</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$499</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">跳色 (2色或以上)</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$599</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">貓眼</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$899</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">造型 - 複雜程度另計</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$999 up</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">延甲 (1指)</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$100</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">十指全延</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$800</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">本店卸甲 (續作/單卸)</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$200 / $250</td>
                                </tr>
                                <tr>
                                    <td class="px-3 py-3 font-medium">它店卸甲 (續作/單卸)</td>
                                    <td class="px-3 py-3 text-right text-gold-accent font-bold">$400 / $450</td>
                                </tr>
                            </tbody>
                        </table>

                        <!-- Price List Notes and Discounts -->
                        <div class="mt-6 p-4 bg-stone-100 rounded-lg space-y-3 text-sm text-stone-600 border border-stone-300 shadow-inner">
                            <p class="font-bold text-stone-800">費用說明與注意事項：</p>
                            <ul class="list-disc list-inside space-y-1">
                                <li>所有凝膠美甲價格皆<span class="font-semibold text-gray-700">含基礎保養、建構加厚</span>。</li>
                                <li>本店/它店作品皆<span class="font-semibold text-red-600">無法 100% 複製</span>。</li>
                            </ul>
                        </div>
                    </div>
                </div>
                
                <div class="flex justify-center pt-4">
                    <button onclick="changeTab(3)" class="py-2 px-6 bg-stone-700 text-white rounded-xl font-semibold shadow-md hover:bg-stone-800 transition duration-150">
                        開始預約流程
                    </button>
                </div>
            </div>

            <!-- Tab 3: Booking (選擇日期, 時段, 填寫資料) -->
            <div id="tab-content-3" class="tab-content hidden space-y-10">

                <!-- Step 1: Date Selection -->
                <div class="pt-4 border-t border-stone-300">
                    <h3 class="text-xl font-semibold text-stone-700 mb-4 border-b pb-2"><i data-lucide="calendar" class="w-5 h-5 inline mr-2 gold-accent"></i>1. 選擇日期 (週一、三、四)</h3>
                    <div id="calendar-view" class="grid grid-cols-3 sm:grid-cols-4 md:grid-cols-7 gap-3 max-h-96 overflow-y-auto pr-2">
                        <!-- Dates will be populated here by JavaScript -->
                        <div class="text-center p-4 col-span-full text-stone-500">載入中...</div>
                    </div>
                </div>

                <!-- Step 2: Time Slot Selection -->
                <div id="time-selection-container" class="opacity-50 pointer-events-none">
                    <h3 class="text-xl font-semibold text-stone-700 mb-4 border-b pb-2"><i data-lucide="clock" class="w-5 h-5 inline mr-2 gold-accent"></i>2. 選擇時段 (<span id="selected-date-display" class="gold-accent">請先選擇日期</span>)</h3>
                    <div id="time-slots-view" class="grid grid-cols-3 sm:grid-cols-6 gap-4">
                        <!-- Time slots will be populated here -->
                    </div>
                </div>

                <!-- Step 3: Confirmation and Form -->
                <div id="confirmation-container" class="opacity-50 pointer-events-none">
                    <h3 class="text-xl font-semibold text-stone-700 mb-4 border-b pb-2"><i data-lucide="user-check" class="w-5 h-5 inline mr-2 gold-accent"></i>3. 填寫資料並確認預約</h3>
                    <div id="slot-summary" class="p-4 bg-red-100 text-red-700 rounded-xl mb-4 font-medium shadow-inner">請選擇日期與時段</div>

                    <form id="booking-form" class="space-y-4">
                        
                        <!-- Service Selection -->
                        <div>
                            <label for="service" class="block text-sm font-medium text-stone-700 mb-1 flex items-center">
                                <i data-lucide="paintbrush" class="w-4 h-4 mr-2 gold-accent"></i> 預約服務項目 (必選)
                            </label>
                            <select id="service" required class="mt-1 block w-full px-4 py-2 border border-stone-400 rounded-lg shadow-inner focus:ring-gold-accent focus:border-gold-accent transition duration-150">
                                <option value="" disabled selected>請選擇您需要的服務</option>
                                <option value="單色">單色 ($499)</option>
                                <option value="跳色">跳色 ($599)</option>
                                <option value="貓眼">貓眼 ($899)</option>
                                <option value="造型">造型 ($999 up) - (手模不可選)</option>
                                <option value="手部保養">手部保養 ($250) - (手模不可選)</option>
                                <option value="十指全延">十指全延 ($800)</option>
                                <option value="卸甲-本店續作">本店卸甲 (續作)</option>
                                <option value="卸甲-本店單卸">本店卸甲 (單卸)</option>
                                <option value="卸甲-它店續作">它店卸甲 (續作)</option>
                                <option value="卸甲-它店單卸">它店卸甲 (單卸)</option>
                            </select>
                        </div>

                        <!-- Hand Model Status -->
                        <div>
                            <label class="block text-sm font-medium text-stone-700 mb-1 flex items-center">
                                <i data-lucide="hand" class="w-4 h-4 mr-2 gold-accent"></i> 是否為手模 (請根據約定選擇)
                            </label>
                            <div class="radio-scroll-container">
                                <label class="radio-scroll-item">
                                    <input type="radio" name="isHandModel" value="no" required checked>
                                    <span>否 (一般顧客)</span>
                                </label>
                                <label class="radio-scroll-item">
                                    <input type="radio" name="isHandModel" value="yes" required>
                                    <span>是 (手模，服務受限)</span>
                                </label>
                            </div>
                            <p id="model-restriction-tip" class="text-xs text-red-500 mt-1 hidden">
                                手模限定項目：單色、跳色、貓眼、十指全延、它店卸甲（續作/單卸）。
                            </p>
                        </div>

                        <div>
                            <label for="name" class="block text-sm font-medium text-stone-700">您的姓名 (必填)</label>
                            <input type="text" id="name" required class="mt-1 block w-full px-4 py-2 border border-stone-400 rounded-lg shadow-inner focus:ring-gold-accent focus:border-gold-accent transition duration-150">
                        </div>
                        <div>
                            <label for="lineId" class="block text-sm font-medium text-stone-700">您的 LINE ID (必填，用於聯繫)</label>
                            <input type="text" id="lineId" required class="mt-1 block w-full px-4 py-2 border border-stone-400 rounded-lg shadow-inner focus:ring-gold-accent focus:border-gold-accent transition duration-150">
                        </div>
                        
                        <!-- Contact Phone Number Field (必填) -->
                        <div>
                            <label for="phone" class="block text-sm font-medium text-stone-700">聯絡電話 (必填)</label>
                            <input type="tel" id="phone" required class="mt-1 block w-full px-4 py-2 border border-stone-400 rounded-lg shadow-inner focus:ring-gold-accent focus:border-gold-accent transition duration-150" placeholder="例如: 0912-345-678">
                        </div>
                        
                        <button type="submit" id="submit-booking-btn" class="w-full py-3 grey-button rounded-xl font-bold text-lg hover:shadow-lg" disabled>
                            確認預約此時段
                        </button>
                        <p id="error-message" class="text-sm text-red-600 mt-2 hidden"></p>
                    </form>
                </div>
                
            </div><!-- End Tab 3 -->
            

        </div> <!-- End Main Content Area -->


        <!-- Footer/Contact Links Section (Instagram and LINE) -->
        <footer class="mt-4 pt-8 border-t border-stone-300 text-center px-6 md:px-10 pb-8">
            <h3 class="text-xl font-bold text-stone-700 mb-6">聯繫我們 / 查看更多作品</h3>
            <div class="flex flex-col sm:flex-row justify-center space-y-3 sm:space-y-0 sm:space-x-4">
                
                <!-- Instagram Link -->
                <a href="https://www.instagram.com/white.mirror_nail?igsh=MW5qb2g1ajNzamhsNQ%3D%3D&utm_source=qr" target="_blank" class="py-3 px-8 grey-button rounded-xl font-bold flex items-center justify-center hover:border-b-1 border-stone-300">
                    <i data-lucide="instagram" class="w-5 h-5 mr-2"></i>
                    作品集 IG 連動
                </a>

                <!-- LINE Contact Link (@702nkzdn) - Enhanced style for main action -->
                <a href="https://line.me/R/ti/p/@702nkzdn" target="_blank" class="py-3 px-8 rounded-xl font-bold flex items-center justify-center bg-gray-700 text-white hover:bg-gray-800 transition duration-150 shadow-lg border-b-4 border-gray-900">
                    <i data-lucide="message-circle" class="w-5 h-5 mr-2"></i>
                    官方 LINE 聯繫 (@702nkzdn)
                </a>
            </div>
            <p class="text-xs text-stone-400 mt-6">© 2024 White Mirror Nail. All rights reserved.</p>
        </footer>


        <!-- Success/Modal Message Box (Custom implementation to replace alert()) -->
        <div id="modal-container" class="fixed inset-0 bg-black bg-opacity-50 z-50 items-center justify-center hidden">
            <div id="modal-content" class="ins-card p-8 w-11/12 max-w-md text-center">
                <h4 id="modal-title" class="text-2xl font-bold gold-accent mb-4"></h4>
                <p id="modal-body" class="text-stone-700 mb-6"></p>
                <button onclick="closeModal()" class="py-2 px-6 grey-button rounded-xl font-semibold">關閉</button>
            </div>
        </div>

    </div>

    <!-- Firebase SDK Imports (使用 mock 變數，以便您在本地儲存和開啟時不會報錯) -->
    <script type="module">
        // 為了讓您在本地開啟檔案不報錯，我們使用虛擬的 Firebase SDK 引入路徑，
        // 並定義 `mock` 變數來取代 Canvas 環境中的全域變數。
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, addDoc, onSnapshot, collection, query, where, Timestamp, setDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        import { setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        
        document.addEventListener('DOMContentLoaded', () => {
            // 載入 Lucide Icons
            lucide.createIcons();
            // 初始化時顯示第一個 Tab
            changeTab(1);
        });

        // --- 模擬 Canvas 環境變數 (Mock Environment Variables) ---
        // **警告:** 當您在本地開啟此檔案時，這些是虛擬值，數據將無法真正存儲。
        // **欲正常運作，請在 Immersive 環境中運行。**
        const MOCK_FIREBASE_CONFIG = {
            apiKey: "MOCK_API_KEY", 
            authDomain: "mock-project.firebaseapp.com",
            projectId: "mock-project-id",
            storageBucket: "mock-project.appspot.com",
            messagingSenderId: "123456789",
            appId: "1:123456789:web:abcdef123456"
        };
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : MOCK_FIREBASE_CONFIG;
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        let db;
        let auth;
        let userId = null;
        let isAuthReady = false;
        let currentTab = 1; // 追蹤目前顯示的分頁

        // --- STATE MANAGEMENT (狀態管理) ---
        let selectedDate = null; // 格式: YYYY-MM-DD
        let selectedTime = null; // 格式: HH:MM
        
        // 預約資料的陣列 (在 Immersive 環境中會被即時更新)
        let appointments = [
             // 範例：假設 2024-12-16 12:00 已被預約
            { date: '2025-12-16', time: '12:00' }
        ]; 

        const APPOINTMENT_TIMES = ['12:00', '15:00', '18:00'];
        // 0=Sun(日), 1=Mon(一), 2=Tue(二), 3=Wed(三), 4=Thu(四), 5=Fri(五), 6=Sat(六)
        const AVAILABLE_DAYS = [1, 3, 4]; 

        // --- UI ELEMENTS (使用者介面元素) ---
        const tabContents = {
            1: document.getElementById('tab-content-1'),
            2: document.getElementById('tab-content-2'),
            3: document.getElementById('tab-content-3'),
        };
        const tabButtons = document.querySelectorAll('.tab-btn');

        const calendarView = document.getElementById('calendar-view');
        const timeSlotsView = document.getElementById('time-slots-view');
        const selectedDateDisplay = document.getElementById('selected-date-display');
        const timeContainer = document.getElementById('time-selection-container');
        const confirmationContainer = document.getElementById('confirmation-container');
        const slotSummary = document.getElementById('slot-summary');
        const bookingForm = document.getElementById('booking-form');
        const submitBtn = document.getElementById('submit-booking-btn');
        const errorMessage = document.getElementById('error-message');
        const modelRestrictionTip = document.getElementById('model-restriction-tip');
        const serviceSelect = document.getElementById('service');
        const isHandModelRadios = document.querySelectorAll('input[name="isHandModel"]');
        
        // 手模允許的服務項目
        const HAND_MODEL_ALLOWED_SERVICES = ['單色', '跳色', '貓眼', '十指全延', '卸甲-它店續作', '卸甲-它店單卸'];

        // --- TAB CONTROL FUNCTIONS (分頁控制函式) ---

        /**
         * 切換分頁顯示
         * @param {number} tabIndex - 要切換到的分頁索引 (1, 2, or 3)
         */
        window.changeTab = function(tabIndex) {
            currentTab = tabIndex;
            
            // 隱藏所有分頁內容
            Object.values(tabContents).forEach(content => content.classList.add('hidden'));

            // 移除所有按鈕的 active 狀態
            tabButtons.forEach(btn => btn.classList.remove('active'));

            // 顯示選定的分頁內容
            if (tabContents[tabIndex]) {
                tabContents[tabIndex].classList.remove('hidden');
                document.querySelector(`.tab-btn[data-tab-index="${tabIndex}"]`).classList.add('active');
            }
        }

        // --- UTILITY FUNCTIONS (工具函式) ---

        /**
         * 顯示自定義的 Modal/訊息框 (取代 alert())
         */
        window.showModal = function(title, body) {
            document.getElementById('modal-title').textContent = title;
            document.getElementById('modal-body').textContent = body;
            document.getElementById('modal-container').classList.remove('hidden');
            document.getElementById('modal-container').classList.add('flex');
        }

        /**
         * 關閉自定義的 Modal/訊息框
         */
        window.closeModal = function() {
            document.getElementById('modal-container').classList.remove('flex');
            document.getElementById('modal-container').classList.add('hidden');
            // 成功預約後，強制跳轉回預約 Tab
            if (document.getElementById('modal-title').textContent.includes('成功')) {
                changeTab(3);
                // 成功後重置表單狀態
                resetBookingForm();
            }
        }

        /**
         * 重置預約表單和相關 UI 狀態
         */
        function resetBookingForm() {
            selectedDate = null;
            selectedTime = null;
            renderCalendar();
            renderTimeSlots();

            selectedDateDisplay.textContent = '請先選擇日期';
            timeContainer.classList.add('opacity-50', 'pointer-events-none');
            confirmationContainer.classList.add('opacity-50', 'pointer-events-none');
            slotSummary.innerHTML = '請選擇日期與時段';
            slotSummary.classList.remove('bg-stone-100', 'text-stone-700');
            slotSummary.classList.add('bg-red-100', 'text-red-700');
            submitBtn.disabled = true;
            errorMessage.classList.add('hidden');
            bookingForm.reset();
        }

        /**
         * 生成並渲染未來四周內可預約的日期 (週一、三、四)
         */
        function renderCalendar() {
            calendarView.innerHTML = '<div class="text-center p-4 col-span-full text-stone-500">載入日期中...</div>';
            const dates = [];
            const today = new Date();
            today.setHours(0, 0, 0, 0);

            // 生成未來 4 週 (最多 28 天) 的日期
            for (let i = 0; i < 28; i++) {
                const date = new Date(today);
                date.setDate(today.getDate() + i);
                
                const dayOfWeek = date.getDay(); 

                if (AVAILABLE_DAYS.includes(dayOfWeek)) {
                    dates.push(date);
                }
            }

            // 渲染日期按鈕
            calendarView.innerHTML = '';
            dates.forEach(date => {
                const dateString = date.toISOString().split('T')[0];
                const dayName = ['日', '一', '二', '三', '四', '五', '六'][date.getDay()];
                const isSelected = dateString === selectedDate;
                
                const dateBtn = document.createElement('button');
                dateBtn.setAttribute('data-date', dateString);
                dateBtn.className = `p-3 flex flex-col items-center justify-center rounded-xl font-semibold text-sm ${isSelected ? 'date-selected' : 'bg-white text-stone-700 hover:bg-stone-100 date-available'}`;

                dateBtn.innerHTML = `
                    <span class="text-xs text-stone-500 ${isSelected ? 'text-white/80' : ''}">週${dayName}</span>
                    <span class="text-xl">${date.getDate()}</span>
                    <span class="text-xs">${date.getMonth() + 1}月</span>
                `;

                dateBtn.addEventListener('click', () => handleDateSelection(dateString));
                calendarView.appendChild(dateBtn);
            });
        }

        /**
         * 處理日期選擇，更新狀態並渲染時段
         */
        function handleDateSelection(dateString) {
            // 如果點擊的是同一個日期，則取消選擇
            if (selectedDate === dateString) {
                selectedDate = null;
            } else {
                selectedDate = dateString;
            }
            
            selectedTime = null;
            renderCalendar();
            renderTimeSlots();

            if (selectedDate) {
                // 更新 UI 顯示
                const dateParts = selectedDate.split('-');
                selectedDateDisplay.textContent = `${dateParts[1]}月${dateParts[2]}日`;

                // 啟用時段選擇區域
                timeContainer.classList.remove('opacity-50', 'pointer-events-none');
                // 禁用確認預約區域
                confirmationContainer.classList.add('opacity-50', 'pointer-events-none');
                slotSummary.innerHTML = '請選擇時段';
                submitBtn.disabled = true;
                errorMessage.classList.add('hidden');
            } else {
                 // 如果取消選擇日期
                selectedDateDisplay.textContent = '請先選擇日期';
                timeContainer.classList.add('opacity-50', 'pointer-events-none');
                confirmationContainer.classList.add('opacity-50', 'pointer-events-none');
                timeSlotsView.innerHTML = ''; // 清除時段顯示
            }
        }

        /**
         * 渲染所選日期的時段，並標記已預約的時段
         */
        function renderTimeSlots() {
            timeSlotsView.innerHTML = '';
            if (!selectedDate) return;

            APPOINTMENT_TIMES.forEach(time => {
                const isBooked = appointments.some(app => app.date === selectedDate && app.time === time);
                const isSelected = selectedTime === time;

                const timeBtn = document.createElement('button');
                timeBtn.setAttribute('data-time', time);
                timeBtn.disabled = isBooked;

                let classes = 'p-3 rounded-xl font-bold transition duration-150';

                if (isBooked) {
                    classes += ' bg-red-100 text-red-500 line-through cursor-not-allowed';
                    timeBtn.innerHTML = `${time} (已預約)`;
                } else if (isSelected) {
                    classes += ' bg-gray-600 text-white shadow-lg border-b-4 border-gray-900 shadow-inner'; 
                    timeBtn.innerHTML = `${time} (已選)`;
                } else {
                    classes += ' bg-white text-stone-700 grey-button hover:shadow-md';
                    timeBtn.innerHTML = time;
                }

                timeBtn.className = classes;

                if (!isBooked) {
                    timeBtn.addEventListener('click', () => handleTimeSelection(time));
                }
                timeSlotsView.appendChild(timeBtn);
            });
        }

        /**
         * 處理時段選擇，更新狀態並啟用確認表單
         */
        function handleTimeSelection(time) {
            selectedTime = time;
            renderTimeSlots();

            confirmationContainer.classList.remove('opacity-50', 'pointer-events-none');
            
            checkFormValidity();
            
            const dateParts = selectedDate.split('-');
            slotSummary.innerHTML = `<span class="font-bold gold-accent">您已選擇:</span> ${dateParts[1]}月${dateParts[2]}日, ${selectedTime}`;
            slotSummary.classList.remove('bg-red-100', 'text-red-700');
            slotSummary.classList.add('bg-stone-100', 'text-stone-700');
            errorMessage.classList.add('hidden');
            
            // 強制捲動到預約表單
            confirmationContainer.scrollIntoView({ behavior: 'smooth', block: 'start' });
        }

        /**
         * 檢查表單欄位及手模限制的有效性，並更新提交按鈕狀態
         */
        function checkFormValidity() {
            const isTimeSelected = selectedTime !== null;
            const isServiceSelected = serviceSelect.value !== "";
            const isNameFilled = document.getElementById('name').value.trim() !== "";
            const isLineIdFilled = document.getElementById('lineId').value.trim() !== "";
            const isPhoneFilled = document.getElementById('phone').value.trim() !== "";
            
            let isFormValid = isTimeSelected && isServiceSelected && isNameFilled && isLineIdFilled && isPhoneFilled; 
            let handModelRestrictionMet = true;
            
            const isHandModel = document.querySelector('input[name="isHandModel"]:checked').value === 'yes';
            const selectedService = serviceSelect.value;

            if (isHandModel) {
                if (!HAND_MODEL_ALLOWED_SERVICES.includes(selectedService)) {
                    handModelRestrictionMet = false;
                    modelRestrictionTip.classList.remove('hidden');
                } else {
                    modelRestrictionTip.classList.add('hidden');
                }
            } else {
                modelRestrictionTip.classList.add('hidden');
            }
            
            submitBtn.disabled = !(isFormValid && handModelRestrictionMet);
        }

        // 為表單欄位新增事件監聽器，以便在輸入/變更時進行驗證
        serviceSelect.addEventListener('change', checkFormValidity);
        document.getElementById('name').addEventListener('input', checkFormValidity);
        document.getElementById('lineId').addEventListener('input', checkFormValidity);
        document.getElementById('phone').addEventListener('input', checkFormValidity);
        isHandModelRadios.forEach(radio => radio.addEventListener('change', checkFormValidity));


        /**
         * 提交預約資料到 Firestore (在 Immersive 環境中) 或模擬提交 (在本地環境中)
         */
        async function submitBooking(event) {
            event.preventDefault();
            
            checkFormValidity();
            if (submitBtn.disabled) {
                errorMessage.textContent = '請檢查所有欄位及手模服務限制是否符合規定。';
                errorMessage.classList.remove('hidden');
                return;
            }

            submitBtn.disabled = true;
            submitBtn.textContent = '預約中...';

            const name = document.getElementById('name').value.trim();
            const lineId = document.getElementById('lineId').value.trim();
            const phone = document.getElementById('phone').value.trim();
            const selectedService = serviceSelect.value;
            const isHandModel = document.querySelector('input[name="isHandModel"]:checked').value === 'yes';

            const appointmentData = {
                date: selectedDate,
                time: selectedTime,
                service: selectedService, 
                isHandModel: isHandModel, 
                name: name,
                lineId: lineId,
                phone: phone,
                userId: userId, 
                timestamp: new Date().toISOString() // 使用 ISO 格式字串
            };

            // 再次檢查時段是否被搶走 (防止競態條件)
            const isBooked = appointments.some(app => app.date === selectedDate && app.time === selectedTime);
            if (isBooked) {
                showModal('預約失敗', '您選擇的時段剛好被預約走了，請重新選擇其他時段。');
                submitBtn.disabled = false;
                submitBtn.textContent = '確認預約此時段';
                return;
            }

            // --- IMPORTANT: Mocking Firebase interaction for local file saving (本地模擬) ---
            if (firebaseConfig === MOCK_FIREBASE_CONFIG) {
                console.warn("--- MOCK DATA SUBMISSION (數據模擬提交) ---");
                console.log("Mock appointment data:", appointmentData);
                
                // 將預約新增到模擬陣列中並重新渲染
                appointments.push({ date: selectedDate, time: selectedTime });
                renderTimeSlots(); 

                showModal(
                    '預約成功! (本地模擬)',
                    `[模擬模式] 恭喜您，已成功預約 ${selectedDate} ${selectedTime} 的美甲服務。您的資料已儲存到瀏覽器的記憶體中。
                    \n**請注意：** 如果您希望資料永久保存並發送通知，請將此程式碼貼回 Immersive 環境中運行。`
                );

            } else {
                // --- REAL Firebase Interaction (真實的 Firebase 互動，僅在 Canvas 環境中運行) ---
                try {
                    // 使用日期_時間作為文件的 ID，確保唯一性
                    const docId = `${selectedDate}_${selectedTime}`; 
                    // 引用公開數據的 Firestore 路徑
                    const collectionRef = collection(db, `/artifacts/${appId}/public/data/nail_appointments`);
                    
                    // 使用 setDoc 來確保 document ID 是我們定義的
                    await setDoc(doc(collectionRef, docId), {
                        ...appointmentData,
                        timestamp: Timestamp.now()
                    });

                    showModal(
                        '預約成功!',
                        `恭喜您，已成功預約 ${selectedDateDisplay.textContent} ${selectedTime} 的美甲服務。
                        \n請點擊下方的 LINE 按鈕 (或搜尋 @702nkzdn) 聯繫我們確認細節，完成最後確認！`
                    );

                } catch (error) {
                    console.error("Error submitting appointment: ", error);
                    showModal('預約失敗', `發生錯誤，請稍後再試。錯誤訊息: ${error.message}`);
                    errorMessage.textContent = `預約提交失敗: ${error.message}`;
                    errorMessage.classList.remove('hidden');
                }
            }
            
            submitBtn.disabled = false;
            submitBtn.textContent = '確認預約此時段';
        }

        // --- FIREBASE AND INITIALIZATION (Firebase 初始化) ---

        /**
         * 開始監聽即時預約數據變化 (僅在 Canvas 環境中有效)
         */
        function startAppointmentListener() {
            if (!db || !isAuthReady || firebaseConfig === MOCK_FIREBASE_CONFIG) {
                console.log("Firestore 或 Auth 尚未就緒，或處於本地模擬模式。跳過即時監聽。");
                return;
            }
            
            // 引用公開集合路徑
            const collectionPath = `/artifacts/${appId}/public/data/nail_appointments`;
            const appointmentsRef = collection(db, collectionPath);
            const q = query(appointmentsRef); 

            // 設置即時監聽
            onSnapshot(q, (snapshot) => {
                const newAppointments = [];
                snapshot.forEach((doc) => {
                    newAppointments.push(doc.data());
                });
                
                appointments = newAppointments;
                console.log("Appointments updated:", appointments);
                
                // 重新渲染 UI 以反映最新的已預約時段
                renderCalendar();
                renderTimeSlots();
            }, (error) => {
                console.error("Error listening to appointments: ", error);
            });
        }

        /**
         * 初始化 Firebase 並處理身份驗證
         */
        async function initializeAppAndAuth() {
            if (firebaseConfig === MOCK_FIREBASE_CONFIG) {
                console.warn("--- 應用程式以本地模擬模式啟動 ---");
                userId = 'MOCK_USER_ID';
                isAuthReady = true;
                renderCalendar();
                bookingForm.addEventListener('submit', submitBooking);
                return;
            }

            try {
                // 初始化 (在 Canvas 環境中)
                const app = initializeApp(firebaseConfig);
                db = getFirestore(app);
                auth = getAuth(app);
                setLogLevel('Debug');

                // 嘗試使用提供的 Custom Token 登入
                if (initialAuthToken) {
                    await signInWithCustomToken(auth, initialAuthToken);
                } else {
                    // 否則，匿名登入
                    await signInAnonymously(auth);
                }

                // 監聽身份驗證狀態變化
                onAuthStateChanged(auth, (user) => {
                    if (user) {
                        userId = user.uid;
                        console.log("Authenticated User ID:", userId);
                    } else {
                        // 使用隨機 ID 作為匿名用戶的唯一識別符
                        userId = crypto.randomUUID(); 
                        console.log("User signed out, using fallback ID:", userId);
                    }
                    isAuthReady = true;
                    // 身份驗證完成後才開始監聽 Firestore
                    startAppointmentListener();
                    renderCalendar(); 
                });

                bookingForm.addEventListener('submit', submitBooking);

            } catch (error) {
                console.error("Firebase Initialization or Auth Error: ", error);
                showModal('認證錯誤', `無法連接到預約服務。錯誤: ${error.message}`);
            }
        }

        // --- 啟動應用程式 ---
        initializeAppAndAuth();
        
    </script>
</body>
</html>

