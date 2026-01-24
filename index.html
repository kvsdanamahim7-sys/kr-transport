<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>KR Service - Premium Coordinator</title>
    
    <!-- Google Fonts: Noto Sans Thai -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            --kr-primary: #6366f1;
            --kr-secondary: #ec4899;
            --kr-accent: #8b5cf6;
        }

        body {
            font-family: 'Noto Sans Thai', sans-serif;
            background-color: #f3f6f9;
            color: #1e293b;
            margin: 0;
            padding: 0;
        }

        .top-accent-bar {
            height: 6px;
            width: 100%;
            background: linear-gradient(90deg, #6366f1, #a855f7, #ec4899, #f43f5e);
            position: sticky;
            top: 0;
            z-index: 50;
        }

        .app-shell {
            max-width: 480px;
            margin: 0 auto;
            min-height: 100vh;
            background: white;
            position: relative;
            box-shadow: 0 0 40px rgba(0,0,0,0.03);
            display: flex;
            flex-direction: column;
        }

        .glass-nav {
            background: rgba(255, 255, 255, 0.8);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--kr-primary), var(--kr-accent));
            transition: all 0.3s ease;
            box-shadow: 0 10px 15px -3px rgba(99, 102, 241, 0.3);
        }
        .btn-primary:active { transform: scale(0.97); }

        .service-card {
            border-radius: 28px;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            background: #ffffff;
            border: 1px solid #f1f5f9;
        }
        .service-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.05);
        }

        .input-group input, .input-group select {
            border-radius: 16px;
            border: 1.5px solid #f1f5f9;
            background: #f8fafc;
            transition: all 0.2s;
        }
        .input-group input:focus {
            border-color: var(--kr-primary);
            background: white;
            outline: none;
            box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.1);
        }

        .radio-tab input { display: none; }
        .radio-tab label {
            cursor: pointer;
            border: 1.5px solid #f1f5f9;
            border-radius: 18px;
            transition: all 0.3s;
        }
        .radio-tab input:checked + label {
            border-color: var(--kr-primary);
            background: #eef2ff;
            color: var(--kr-primary);
        }

        .page-transition {
            animation: slideIn 0.4s ease-out;
        }
        @keyframes slideIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .legal-box {
            background: #fdf2f8;
            border: 1px solid #fce7f3;
            border-radius: 20px;
        }

        #toast {
            visibility: hidden;
            min-width: 200px;
            background-color: #333;
            color: #fff;
            text-align: center;
            border-radius: 50px;
            padding: 12px;
            position: fixed;
            z-index: 100;
            left: 50%;
            bottom: 30px;
            transform: translateX(-50%);
            font-size: 14px;
            font-weight: 600;
        }
        #toast.show {
            visibility: visible;
            animation: fadein 0.5s, fadeout 0.5s 2.5s;
        }
        @keyframes fadein { from {bottom: 0; opacity: 0;} to {bottom: 30px; opacity: 1;} }
        @keyframes fadeout { from {bottom: 30px; opacity: 1;} to {bottom: 0; opacity: 0;} }
    </style>
</head>
<body>

    <div id="toast">คัดลอกข้อมูลเรียบร้อยแล้ว!</div>

    <div class="app-shell">
        <div class="top-accent-bar"></div>

        <nav class="glass-nav sticky top-[6px] z-40 px-6 py-4 flex justify-between items-center border-b border-gray-50">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-indigo-600 rounded-2xl flex items-center justify-center text-white font-black italic shadow-lg">KR</div>
                <div>
                    <h1 class="font-extrabold text-slate-800 text-lg leading-tight tracking-tight">KR SERVICE</h1>
                    <div class="flex items-center gap-1">
                        <span class="w-1.5 h-1.5 bg-green-500 rounded-full"></span>
                        <span class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Platform Ready</span>
                    </div>
                </div>
            </div>
            
            <button onclick="window.location.href='https://line.me/ti/p/~pkzd_3012'" class="bg-slate-900 text-white px-4 py-2 rounded-2xl text-xs font-bold hover:bg-slate-800 transition-colors flex items-center gap-2">
                <i class="fa-solid fa-headset text-indigo-400"></i>
                แอดมิน
            </button>
        </nav>

        <main id="app-content" class="flex-grow p-6 overflow-x-hidden">
            <!-- Dynamic Content -->
        </main>

        <footer class="p-6 text-center">
            <p class="text-[10px] text-slate-300 font-medium tracking-widest">© 2024 KR LOGISTICS COORDINATOR</p>
        </footer>
    </div>

    <script>
        const services = [
            { id: 'moving', title: 'ย้ายงาน / ขนของ', icon: 'fa-truck-fast', color: 'text-indigo-500', bg: 'bg-indigo-50', desc: 'ย้ายงาน ขนของ ย้ายงานพิเศษ ' },
            { id: 'medical', title: 'โรงพยาบาล / คลินิก', icon: 'fa-hospital-user', color: 'text-rose-500', bg: 'bg-rose-50', desc: 'รับส่งพบแพทย์ จัดฟัน ศัลยกรรม' },
            { id: 'document', title: 'พาสปอร์ต / สถานทูต', icon: 'fa-id-card-clip', color: 'text-amber-500', bg: 'bg-amber-50', desc: 'ทำพาสปอร์ต บัตร ปชช. รายงายตัวกลับ ส่งสนามบิน สถานทูต' }
        ];

        const content = document.getElementById('app-content');

        function showHome() {
            let html = `
                <div class="page-transition">
                    <div class="mb-8">
                        <h2 class="text-3xl font-black text-slate-900">สวัสดีครับ <span class="text-indigo-600 underline decoration-indigo-200 underline-offset-4">ต้องการไปที่ไหน?</span></h2>
                        <p class="text-slate-400 text-sm mt-2 font-medium">เราประสานงานรถให้คุณฟรี ไม่มีค่าธรรมเนียมแอป</p>
                    </div>

                    <div class="space-y-4">
            `;

            services.forEach(s => {
                html += `
                    <div onclick="showForm('${s.id}')" class="service-card p-5 cursor-pointer flex items-center gap-5 group">
                        <div class="w-16 h-16 ${s.bg} ${s.color} rounded-3xl flex items-center justify-center text-2xl group-hover:scale-110 transition-transform shadow-sm">
                            <i class="fa-solid ${s.icon}"></i>
                        </div>
                        <div class="flex-1">
                            <h3 class="font-bold text-slate-800 text-lg">${s.title}</h3>
                            <p class="text-xs text-slate-400 font-medium">${s.desc}</p>
                        </div>
                        <div class="w-8 h-8 rounded-full bg-slate-50 flex items-center justify-center text-slate-300">
                            <i class="fa-solid fa-chevron-right text-[10px]"></i>
                        </div>
                    </div>
                `;
            });

            html += `
                    </div>

                    <!-- นำคำอธิบายกลับมาแสดงที่หน้าแรก -->
                    <div class="legal-box mt-10 p-5 relative overflow-hidden">
                        <div class="absolute -right-4 -bottom-4 text-pink-100 text-6xl rotate-12">
                            <i class="fa-solid fa-scale-balanced"></i>
                        </div>
                        <h4 class="text-pink-600 font-bold text-sm mb-2 flex items-center gap-2">
                            <i class="fa-solid fa-circle-info"></i>
                            ข้อกำหนดทางกฎหมาย
                        </h4>
                        <div class="text-[11px] text-pink-900/70 leading-relaxed font-medium">
                            KR Service เป็นเพียงผู้ประสานงาน (Coordinator) เท่านั้น การจองไม่มีค่าธรรมเนียมใดๆ แอบแฝง ค่าบริการจริงจะตกลงกับคนขับรถโดยตรง เราไม่ใช่ผู้ขนส่งและไม่รับผิดชอบต่อความเสียหายใดๆ
                        </div>
                    </div>
                </div>
            `;
            content.innerHTML = html;
        }

        function showForm(serviceId) {
            const service = services.find(s => s.id === serviceId);
            content.innerHTML = `
                <div class="page-transition">
                    <button onclick="showHome()" class="mb-6 text-slate-400 font-bold text-xs flex items-center gap-2 hover:text-indigo-600 transition">
                        <i class="fa-solid fa-arrow-left"></i> ย้อนกลับ
                    </button>
                    <div class="mb-8">
                        <span class="text-[10px] font-black text-indigo-500 uppercase tracking-[0.2em]">Service Request</span>
                        <h2 class="text-2xl font-black text-slate-900">${service.title}</h2>
                    </div>
                    <form onsubmit="handleReview(event, '${service.title}')" class="space-y-6">
                        <div class="space-y-4">
                            <div>
                                <label class="text-xs font-extrabold text-slate-800 mb-3 block uppercase">ประเภทรถ</label>
                                <div class="grid grid-cols-3 gap-2">
                                    <div class="radio-tab">
                                        <input type="radio" name="car" id="small" value="รถเล็ก" checked>
                                        <label for="small" class="flex flex-col items-center p-4"><i class="fa-solid fa-car-side text-lg mb-1"></i><span class="text-[10px] font-bold">รถเล็ก</span></label>
                                    </div>
                                    <div class="radio-tab">
                                        <input type="radio" name="car" id="large" value="รถใหญ่">
                                        <label for="large" class="flex flex-col items-center p-4"><i class="fa-solid fa-van-shuttle text-lg mb-1"></i><span class="text-[10px] font-bold">รถใหญ่</span></label>
                                    </div>
                                    <div class="radio-tab">
                                        <input type="radio" name="car" id="truck" value="รถ 6 ล้อ">
                                        <label for="truck" class="flex flex-col items-center p-4"><i class="fa-solid fa-truck text-lg mb-1"></i><span class="text-[10px] font-bold">6 ล้อ</span></label>
                                    </div>
                                </div>
                            </div>
                            <div class="input-group">
                                <label class="text-[10px] font-black text-slate-400 mb-1 block uppercase">ที่อยู่ต้นทาง</label>
                                <input type="text" id="origin" placeholder="ระบุจุดรับ..." class="w-full px-4 py-3.5 text-sm font-bold" required>
                            </div>
                            <div class="input-group">
                                <label class="text-[10px] font-black text-slate-400 mb-1 block uppercase">ที่อยู่ปลายทาง</label>
                                <input type="text" id="destination" placeholder="ระบุจุดส่ง..." class="w-full px-4 py-3.5 text-sm font-bold" required>
                            </div>
                            <div class="input-group">
                                <label class="text-[10px] font-black text-slate-400 mb-1 block uppercase">ไอดีไลน์ (Line ID)</label>
                                <input type="text" id="lineId" placeholder="ระบุไอดีไลน์..." class="w-full px-4 py-3.5 text-sm font-bold" required>
                            </div>
                            <div class="grid grid-cols-2 gap-4">
                                <div class="input-group">
                                    <label class="text-[10px] font-black text-slate-400 mb-1 block uppercase">เวลานัดหมาย</label>
                                    <input type="datetime-local" id="time" class="w-full px-4 py-3.5 text-xs font-bold" required>
                                </div>
                                <div class="input-group">
                                    <label class="text-[10px] font-black text-slate-400 mb-1 block uppercase">จำนวนคน</label>
                                    <input type="number" id="pax" value="1" min="1" class="w-full px-4 py-3.5 text-sm font-bold text-center">
                                </div>
                            </div>
                            <div class="input-group">
                                <label class="text-[10px] font-black text-slate-400 mb-1 block uppercase">ปริมาณของ</label>
                                <select id="luggage" class="w-full px-4 py-3.5 text-sm font-bold appearance-none">
                                    <option value="ของน้อย">ของน้อย (กระเป๋าเดินทางทั่วไป)</option>
                                    <option value="ของปานกลาง">ของปานกลาง (ลัง 3-5 ใบ)</option>
                                    <option value="ของเยอะ">ของเยอะ (เฟอร์นิเจอร์/ตู้/เตียง)</option>
                                </select>
                            </div>
                        </div>

                        <!-- คำอธิบายหน้ากรอกฟอร์ม -->
                        <div class="bg-indigo-50 border border-indigo-100 rounded-xl p-3 flex gap-3 items-center">
                            <div class="text-indigo-500 text-lg"><i class="fa-solid fa-circle-check"></i></div>
                            <p class="text-[10px] font-bold text-indigo-900 leading-tight">
                                กรุณาตรวจสอบข้อมูลในขั้นตอนถัดไป ข้อมูลจะถูกคัดลอกเมื่อคุณกดยืนยันในหน้าสุดท้าย
                            </p>
                        </div>

                        <button type="submit" class="btn-primary w-full py-4 rounded-2xl text-white font-extrabold text-sm tracking-widest uppercase flex items-center justify-center gap-3 shadow-indigo-200 mt-4">
                            ตรวจสอบข้อมูล (Review Detail)
                            <i class="fa-solid fa-magnifying-glass text-xs opacity-70"></i>
                        </button>
                    </form>
                </div>
            `;
        }

        function handleReview(e, serviceTitle) {
            e.preventDefault();
            const bookingData = {
                id: 'KR' + Math.floor(100000 + Math.random() * 900000),
                service: serviceTitle,
                car: document.querySelector('input[name="car"]:checked').value,
                origin: document.getElementById('origin').value,
                destination: document.getElementById('destination').value,
                lineId: document.getElementById('lineId').value,
                time: document.getElementById('time').value.replace('T', ' '),
                pax: document.getElementById('pax').value,
                luggage: document.getElementById('luggage').value
            };

            showFinalReview(bookingData);
        }

        function showFinalReview(data) {
            const message = `แจ้งงานใหม่: ${data.id}\n` +
                            `------------------\n` +
                            `บริการ: ${data.service}\n` +
                            `ประเภทรถ: ${data.car}\n` +
                            `ต้นทาง: ${data.origin}\n` +
                            `ปลายทาง: ${data.destination}\n` +
                            `ID Line: ${data.lineId}\n` +
                            `วัน/เวลา: ${data.time}\n` +
                            `จำนวนคน: ${data.pax} คน\n` +
                            `ปริมาณของ: ${data.luggage}\n` +
                            `------------------\n` +
                            `ประสานงานโดย KR Service`;

            content.innerHTML = `
                <div class="page-transition">
                    <button onclick="showHome()" class="mb-6 text-slate-400 font-bold text-xs flex items-center gap-2 hover:text-indigo-600 transition">
                        <i class="fa-solid fa-xmark"></i> ยกเลิก
                    </button>

                    <div class="mb-6">
                        <span class="text-[10px] font-black text-indigo-500 uppercase tracking-[0.2em]">Final Verification</span>
                        <h2 class="text-2xl font-black text-slate-900">ตรวจสอบรายละเอียด</h2>
                        <p class="text-slate-400 text-xs font-medium">กรุณาตรวจสอบข้อมูลก่อนส่งให้แอดมิน</p>
                    </div>

                    <div class="bg-slate-50 border border-slate-100 rounded-3xl p-6 space-y-4 mb-8">
                        <div class="flex justify-between border-b border-slate-200 pb-2">
                            <span class="text-[10px] font-bold text-slate-400 uppercase">บริการ</span>
                            <span class="text-xs font-black text-slate-800">${data.service}</span>
                        </div>
                        <div class="flex justify-between border-b border-slate-200 pb-2">
                            <span class="text-[10px] font-bold text-slate-400 uppercase">รถที่เลือก</span>
                            <span class="text-xs font-black text-slate-800">${data.car}</span>
                        </div>
                        <div class="space-y-1">
                            <span class="text-[10px] font-bold text-slate-400 uppercase block text-indigo-500">ต้นทาง - ปลายทาง</span>
                            <p class="text-xs font-bold text-slate-800 leading-relaxed">${data.origin} <i class="fa-solid fa-arrow-right mx-1 opacity-30"></i> ${data.destination}</p>
                        </div>
                        <div class="grid grid-cols-2 gap-4 pt-2">
                            <div>
                                <span class="text-[10px] font-bold text-slate-400 uppercase block">เวลานัดหมาย</span>
                                <span class="text-xs font-black text-slate-800">${data.time}</span>
                            </div>
                            <div>
                                <span class="text-[10px] font-bold text-slate-400 uppercase block">ไอดีไลน์</span>
                                <span class="text-xs font-black text-indigo-600 underline">${data.lineId}</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-amber-50 border border-amber-200 rounded-2xl p-4 mb-6">
                        <div class="flex gap-3">
                            <i class="fa-solid fa-copy text-amber-500 mt-1"></i>
                            <div>
                                <p class="text-[11px] font-black text-amber-900 mb-1">ขั้นตอนถัดไป:</p>
                                <p class="text-[10px] text-amber-800/80 leading-relaxed">
                                    กดปุ่ม <b>"ประสานงานเลย"</b> ระบบจะคัดลอกข้อความข้างต้น และนำท่านไปยังแอป Line จากนั้นให้กด <b>"วาง"</b> เพื่อส่งข้อมูลให้แอดมินครับ
                                </p>
                            </div>
                        </div>
                    </div>

                    <button onclick="finalizeAndSend(\`${message.replace(/`/g, '\\`').replace(/\n/g, '\\n')}\`)" class="btn-primary w-full py-5 rounded-2xl text-white font-extrabold text-sm tracking-widest uppercase flex items-center justify-center gap-3 shadow-indigo-200">
                        ประสานงานเลย (Copy & Send)
                        <i class="fa-solid fa-paper-plane text-xs opacity-70"></i>
                    </button>
                    
                    <button onclick="showForm('${services.find(s=>s.title===data.service).id}')" class="w-full mt-4 py-4 text-slate-400 font-bold text-xs uppercase tracking-widest text-center">
                        แก้ไขข้อมูล
                    </button>
                </div>
            `;
        }

        function finalizeAndSend(message) {
            // Copy to Clipboard
            const textArea = document.createElement("textarea");
            textArea.value = message;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand('copy');
            document.body.removeChild(textArea);

            showToast();

            // Open Line
            setTimeout(() => {
                window.location.href = 'https://line.me/ti/p/~@445ltjiu';
                showFinalStep(message);
            }, 600);
        }

        function showFinalStep(message) {
            content.innerHTML = `
                <div class="page-transition flex flex-col items-center justify-center py-10 text-center">
                    <div class="w-24 h-24 bg-indigo-600 text-white rounded-full flex items-center justify-center text-4xl mb-6 shadow-xl animate-bounce">
                        <i class="fa-brands fa-line"></i>
                    </div>
                    <h2 class="text-2xl font-black text-slate-900 mb-2">เข้าสู่แอป Line แล้ว</h2>
                    <p class="text-slate-400 text-sm font-medium px-8 mb-8">หากแอปไม่เปิดขึ้นมา ให้กดเปิดใหม่อีกครั้งที่ปุ่มด้านล่าง และอย่าลืมกด <b>"วาง"</b> ข้อความที่คัดลอกไว้</p>
                    
                    <button onclick="window.location.href='https://line.me/ti/p/~@445ltjiu'" class="bg-indigo-600 text-white px-8 py-4 rounded-2xl font-black text-sm uppercase flex items-center gap-3 shadow-lg mb-4">
                        <i class="fa-solid fa-arrow-up-right-from-square"></i> เปิดแอป Line อีกครั้ง
                    </button>
                    
                    <button onclick="window.location.reload()" class="text-slate-300 font-bold text-xs uppercase tracking-widest">
                        กลับหน้าหลัก
                    </button>
                </div>
            `;
        }

        function showToast() {
            const x = document.getElementById("toast");
            x.className = "show";
            setTimeout(function(){ x.className = x.className.replace("show", ""); }, 3000);
        }

        showHome();
    </script>
</body>
</html>

