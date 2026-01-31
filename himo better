<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>HIMO BETTER | Player Console</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700;800&display=swap');
        body { font-family: 'Poppins', sans-serif; background-color: #f8fafc; -webkit-tap-highlight-color: transparent; padding-bottom: 80px; }
        
        /* Navigation & UI Fixes */
        nav { position: fixed; bottom: 0; left: 0; right: 0; height: 70px; background: white; display: flex; justify-content: space-around; align-items: center; border-top: 1px solid #e2e8f0; z-index: 50; box-shadow: 0 -4px 12px rgba(0,0,0,0.05); }
        .nav-btn { flex: 1; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 4px; color: #94a3b8; transition: 0.3s; border: none; background: none; }
        .nav-active { color: #0d9488 !important; }
        .nav-btn i { font-size: 20px; }
        .nav-btn span { font-size: 10px; font-weight: 700; text-transform: uppercase; }

        .tab-content { display: none; }
        .tab-content.active { display: block; animation: slideUp 0.3s ease-out; }
        @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        
        .glass-card { background: white; border-radius: 1.5rem; border: 1px solid #e2e8f0; }
        .hide-scroll::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <div id="auth-overlay" class="fixed inset-0 z-[100] bg-white flex flex-col justify-center p-8">
        <div class="text-center mb-8">
            <h1 class="text-3xl font-black text-teal-600 tracking-tighter uppercase">HIMO BETTER</h1>
            <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest mt-1">Free Fire E-Sports</p>
        </div>
        <div class="bg-slate-100 p-1 rounded-2xl flex mb-6">
            <button onclick="toggleAuth('login')" id="tab-l" class="flex-1 py-3 rounded-xl font-bold text-xs bg-white shadow-sm text-teal-600">LOGIN</button>
            <button onclick="toggleAuth('signup')" id="tab-s" class="flex-1 py-3 rounded-xl font-bold text-xs text-slate-400">SIGN UP</button>
        </div>
        <form id="auth-form" class="space-y-4">
            <div id="signup-fields" class="hidden space-y-4">
                <input type="text" id="reg-name" placeholder="Full Name" class="w-full p-4 bg-slate-50 border rounded-2xl outline-none font-bold">
                <input type="tel" id="reg-phone" placeholder="Phone Number" class="w-full p-4 bg-slate-50 border rounded-2xl outline-none font-bold">
                <input type="text" id="reg-ffuid" placeholder="Free Fire UID" class="w-full p-4 bg-slate-50 border rounded-2xl outline-none font-bold">
            </div>
            <input type="email" id="auth-email" placeholder="Email" class="w-full p-4 bg-slate-50 border rounded-2xl font-bold" required>
            <input type="password" id="auth-pass" placeholder="Password" class="w-full p-4 bg-slate-50 border rounded-2xl font-bold" required>
            <button type="submit" id="auth-btn" class="w-full py-4 bg-teal-600 text-white font-black rounded-2xl shadow-xl active:scale-95 transition-all">START PLAYING</button>
        </form>
        <p onclick="forgotPass()" class="text-center text-xs font-bold text-slate-400 mt-6 cursor-pointer underline">Forgot Password?</p>
    </div>

    <header class="bg-white/90 backdrop-blur-md border-b p-4 flex justify-between items-center sticky top-0 z-40">
        <div>
            <h2 class="text-lg font-black text-slate-800 leading-none">HIMO <span class="text-teal-600">PRO</span></h2>
            <p id="head-ffuid" class="text-[9px] font-bold text-slate-400 mt-1 uppercase">UID: Loading...</p>
        </div>
        <div onclick="switchTab('wallet')" class="bg-teal-50 border border-teal-100 px-3 py-1.5 rounded-full flex items-center gap-2 cursor-pointer">
            <i class="fas fa-wallet text-teal-600 text-xs"></i>
            <span id="head-bal" class="font-black text-teal-700 text-sm">₹0</span>
        </div>
    </header>

    <main class="p-4 space-y-6">

        <div id="tab-dash" class="tab-content active space-y-6">
            <div class="bg-slate-900 rounded-[2.5rem] p-6 text-white relative overflow-hidden shadow-xl">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold text-teal-400 uppercase tracking-widest leading-none">Welcome,</p>
                    <h1 class="text-2xl font-black mt-1" id="dash-name">Username</h1>
                    <div class="mt-6 flex gap-4 text-center">
                        <div class="bg-white/10 p-3 rounded-2xl flex-1"><p class="text-[8px] font-bold opacity-60 uppercase">Joined</p><h4 class="text-lg font-black" id="dash-joined">0</h4></div>
                        <div class="bg-white/10 p-3 rounded-2xl flex-1"><p class="text-[8px] font-bold opacity-60 uppercase">Active</p><h4 class="text-lg font-black" id="stat-active">0</h4></div>
                    </div>
                </div>
                <i class="fas fa-crosshairs absolute -bottom-6 -right-6 text-9xl text-white/5 rotate-12"></i>
            </div>
            <h3 class="font-black text-slate-700 px-1 uppercase text-xs tracking-widest">Active Lobby</h3>
            <div id="lobby-list" class="space-y-4"></div>
        </div>

        <div id="tab-matches" class="tab-content space-y-4">
            <div class="flex bg-slate-100 p-1 rounded-2xl">
                <button onclick="renderMatches('Upcoming')" class="m-tab flex-1 py-2.5 rounded-xl text-[10px] font-black bg-white text-teal-600 shadow-sm transition-all">UPCOMING</button>
                <button onclick="renderMatches('Live')" class="m-tab flex-1 py-2.5 rounded-xl text-[10px] font-black text-slate-400 transition-all">LIVE</button>
                <button onclick="renderMatches('Completed')" class="m-tab flex-1 py-2.5 rounded-xl text-[10px] font-black text-slate-400 transition-all">RESULTS</button>
            </div>
            <div id="my-matches-render" class="space-y-4"></div>
        </div>

        <div id="tab-wallet" class="tab-content space-y-6">
            <div class="glass-card p-8 text-center border-b-4 border-teal-500 shadow-sm">
                <p class="text-[10px] font-bold text-slate-400 uppercase">Available Balance</p>
                <h2 class="text-5xl font-black text-slate-800 my-4">₹<span id="wallet-bal">0</span></h2>
                <div class="flex gap-4 mt-8">
                    <button onclick="openModal('dep')" class="flex-1 py-4 bg-teal-600 text-white font-black rounded-2xl shadow-xl active:scale-95 transition-all">ADD CASH</button>
                    <button onclick="openModal('with')" class="flex-1 py-4 bg-slate-900 text-white font-black rounded-2xl active:scale-95 transition-all">WITHDRAW</button>
                </div>
            </div>
            <h3 class="font-black text-slate-700 px-1 uppercase text-xs">Transaction History</h3>
            <div id="txn-list" class="space-y-3"></div>
        </div>

        <div id="tab-notif" class="tab-content space-y-3">
            <h3 class="font-black text-slate-700 px-1 uppercase text-xs">Alert Inbox</h3>
            <div id="notif-render" class="space-y-3"></div>
        </div>

        <div id="tab-profile" class="tab-content space-y-6">
            <div class="bg-white p-8 rounded-[2.5rem] border shadow-sm text-center">
                <div class="w-24 h-24 bg-teal-500 rounded-full mx-auto flex items-center justify-center text-3xl font-black text-white shadow-xl mb-4 border-4 border-white" id="prof-char">P</div>
                <h2 class="text-xl font-black text-slate-800" id="prof-name">Username</h2>
                <div class="mt-8 space-y-3 text-left">
                    <a href="https://t.me/himanshu9311" target="_blank" class="flex items-center gap-4 p-4 bg-slate-50 rounded-2xl border border-slate-100">
                        <i class="fab fa-telegram text-blue-500 text-2xl"></i>
                        <div class="flex-1 text-xs font-black">Support Group</div>
                        <i class="fas fa-chevron-right text-slate-300 text-xs"></i>
                    </a>
                    <button onclick="logout()" class="w-full flex items-center gap-4 p-4 bg-red-50 rounded-2xl border border-red-100">
                        <i class="fas fa-sign-out-alt text-red-500 text-2xl"></i>
                        <div class="flex-1 text-left text-xs font-black text-red-600">Logout</div>
                    </button>
                </div>
            </div>
        </div>

    </main>

    <nav>
        <button onclick="switchTab('dash')" class="nav-btn nav-active" id="btn-dash"><i class="fas fa-gamepad"></i><span>Lobby</span></button>
        <button onclick="switchTab('matches')" class="nav-btn" id="btn-matches"><i class="fas fa-trophy"></i><span>Match</span></button>
        <button onclick="switchTab('wallet')" class="nav-btn" id="btn-wallet"><i class="fas fa-wallet"></i><span>Wallet</span></button>
        <button onclick="switchTab('notif')" class="nav-btn" id="btn-notif"><i class="fas fa-bell"></i><span>Alerts</span></button>
        <button onclick="switchTab('profile')" class="nav-btn" id="btn-profile"><i class="fas fa-user-circle"></i><span>Me</span></button>
    </nav>

    <div id="modal-dep" class="hidden fixed inset-0 z-[110] bg-slate-900/80 backdrop-blur-sm flex items-end justify-center">
        <div class="bg-white w-full max-w-md rounded-t-[3rem] p-8 space-y-6">
            <div class="flex justify-between items-center"><h3 class="font-black text-xl">Deposit</h3><button onclick="closeModal('dep')" class="text-slate-300"><i class="fas fa-times text-xl"></i></button></div>
            <div class="bg-slate-50 p-6 rounded-3xl border border-slate-100 text-center">
                <img src="https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=upi://pay?pa=bnote977-2@okhdfcbank%26pn=Note%2520Book%26aid=uGICAgICf24L7KA" class="w-44 h-44 mx-auto rounded-3xl border-4 border-white shadow-xl mb-4">
                <p class="text-[8px] font-black text-slate-400 uppercase">Scan QR & Submit UTR (Min ₹10)</p>
            </div>
            <input type="number" id="in-dep-amt" placeholder="Amount (Min ₹10)" class="w-full p-4 bg-slate-50 border rounded-2xl font-black text-center text-xl">
            <input type="text" id="in-dep-utr" placeholder="12 Digit Transaction ID" class="w-full p-4 bg-slate-50 border rounded-2xl font-bold">
            <button onclick="submitDep()" class="w-full py-4 bg-teal-600 text-white font-black rounded-2xl shadow-xl">SUBMIT PAYMENT</button>
        </div>
    </div>

    <div id="modal-with" class="hidden fixed inset-0 z-[110] bg-slate-900/80 backdrop-blur-sm flex items-end justify-center">
        <div class="bg-white w-full max-w-md rounded-t-[3rem] p-8 space-y-5">
            <div class="flex justify-between items-center"><h3 class="font-black text-xl">Withdraw</h3><button onclick="closeModal('with')" class="text-slate-300"><i class="fas fa-times text-xl"></i></button></div>
            <input type="number" id="in-with-amt" placeholder="Amount (Min ₹10)" class="w-full p-4 bg-slate-50 border rounded-2xl font-black outline-none focus:border-teal-500">
            <input type="text" id="in-with-upi" placeholder="UPI ID (e.g. name@paytm)" class="w-full p-4 bg-slate-50 border rounded-2xl font-bold outline-none focus:border-teal-500">
            <button onclick="submitWithdrawal()" class="w-full py-4 bg-slate-900 text-white font-black rounded-2xl shadow-xl active:scale-95 transition-all">REQUEST PAYOUT</button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-app.js";
        import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged, signOut, sendPasswordResetEmail } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-auth.js";
        import { getDatabase, ref, set, push, onValue, update, get } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyC5xpOfGrDdQKEf_Axg2uInjTwxlmIGKMI", authDomain: "himo-better-tournament.firebaseapp.com", databaseURL: "https://himo-better-tournament-default-rtdb.firebaseio.com", projectId: "himo-better-tournament", storageBucket: "himo-better-tournament.firebasestorage.app", messagingSenderId: "908980157528", appId: "1:908980157528:web:281795a5fa304d9e3dde2d" };
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getDatabase(app);

        let currentUser = null, isSignup = false;

        onAuthStateChanged(auth, u => { if(u) { currentUser = u; document.getElementById('auth-overlay').classList.add('hidden'); initUser(); } else { document.getElementById('auth-overlay').classList.remove('hidden'); } });

        document.getElementById('auth-form').onsubmit = async e => {
            e.preventDefault(); const em = document.getElementById('auth-email').value, ps = document.getElementById('auth-pass').value;
            try { if(isSignup) {
                const n = document.getElementById('reg-name').value, ph = document.getElementById('reg-phone').value, uid = document.getElementById('reg-ffuid').value;
                const c = await createUserWithEmailAndPassword(auth, em, ps);
                await set(ref(db, `users/${c.user.uid}`), { username: n, phone: ph, ff_uid: uid, email: em, wallet: 0 });
            } else await signInWithEmailAndPassword(auth, em, ps); } catch(err) { alert(err.message); }
        };

        function initUser() {
            onValue(ref(db, `users/${currentUser.uid}`), snap => {
                const u = snap.val(); if(!u) return;
                document.getElementById('head-bal').innerText = `₹${u.wallet||0}`;
                document.getElementById('wallet-bal').innerText = u.wallet||0;
                document.getElementById('head-ffuid').innerText = `UID: ${u.ff_uid}`;
                document.getElementById('dash-name').innerText = u.username;
                document.getElementById('prof-name').innerText = u.username;
                document.getElementById('prof-char').innerText = u.username[0].toUpperCase();
                
                const txns = document.getElementById('txn-list'); txns.innerHTML = '';
                if(u.transactions) Object.values(u.transactions).reverse().forEach(t => {
                    const cr = t.type === 'credit';
                    txns.innerHTML += `<div class="bg-white p-4 rounded-2xl border shadow-sm flex justify-between items-center"><div class="flex gap-3 items-center"><div class="w-8 h-8 rounded-full ${cr?'bg-green-100 text-green-600':'bg-red-100 text-red-600'} flex items-center justify-center text-xs"><i class="fas ${cr?'fa-arrow-down':'fa-arrow-up'}"></i></div><div><p class="text-[10px] font-black leading-none">${t.note}</p><p class="text-[9px] text-slate-400 mt-1">${new Date(t.date).toLocaleDateString()}</p></div></div><span class="font-black ${cr?'text-green-600':'text-red-500'}">${cr?'+':'-'}₹${t.amount}</span></div>`;
                });
            });

            onValue(ref(db, 'tournaments'), snap => {
                const lobby = document.getElementById('lobby-list'); lobby.innerHTML = ''; let ac = 0, jc = 0;
                snap.forEach(c => {
                    const t = c.val(); if(t.status === 'Completed') return; ac++;
                    const jCount = t.participants ? Object.keys(t.participants).length : 0;
                    const isJoined = t.participants && t.participants[currentUser.uid]; if(isJoined) jc++;
                    lobby.innerHTML += `<div class="glass-card p-5 space-y-4"><div class="flex justify-between items-start"><div><h4 class="font-black text-slate-800 text-sm leading-tight">${t.title}</h4><p class="text-[10px] font-bold text-slate-400 mt-1 uppercase"><i class="far fa-clock text-teal-500"></i> ${t.match_time}</p></div><div class="text-right font-black text-teal-600">₹${t.prize_pool}</div></div><button onclick="joinMatch('${c.key}',${t.entry_fee},'${t.title}')" class="w-full py-3 rounded-xl font-black text-[10px] uppercase tracking-widest ${isJoined?'bg-slate-50 text-teal-600 border border-teal-100 shadow-none':'bg-teal-600 text-white shadow-lg'}">${isJoined?'Already Joined ✅':'Join Match (₹'+t.entry_fee+')'}</button></div>`;
                });
                document.getElementById('stat-active').innerText = ac; document.getElementById('dash-joined').innerText = jc;
            });

            onValue(ref(db, `users/${currentUser.uid}/notifications`), snap => {
                const l = document.getElementById('notif-render'); l.innerHTML = ''; let un = false;
                snap.forEach(c => { const n = c.val(); if(!n.read) un = true; l.innerHTML += `<div class="bg-white p-4 rounded-2xl border shadow-sm"><h4 class="text-xs font-black text-slate-800">${n.title}</h4><p class="text-[10px] text-slate-500 mt-1">${n.msg}</p></div>`; });
                document.getElementById('notif-dot').classList.toggle('hidden', !un);
            });
        }

        window.joinMatch = async (tid, fee, name) => {
            const uRef = ref(db, `users/${currentUser.uid}`); const u = (await get(uRef)).val();
            const partRef = ref(db, `tournaments/${tid}/participants/${currentUser.uid}`);
            if((await get(partRef)).exists()) return alert("Already joined!");
            if(u.wallet < fee) return alert("Min balance ₹" + fee + " required.");
            if(confirm(`Join ${name}? Entry fee ₹${fee} will be deducted.`)) {
                await update(uRef, { wallet: u.wallet - fee });
                await set(partRef, { username: u.username, joinedAt: Date.now() });
                await push(ref(db, `users/${currentUser.uid}/transactions`), { type: 'debit', amount: fee, note: 'Joined: ' + name, date: Date.now() });
                alert("Joined Successfully!");
            }
        };

        window.renderMatches = async (f) => {
            const list = document.getElementById('my-matches-render'); list.innerHTML = '';
            const snap = await get(ref(db, 'tournaments'));
            snap.forEach(c => {
                const t = c.val();
                if(t.participants && t.participants[currentUser.uid] && t.status === f) {
                    let room = f==='Live' ? `<div class="bg-slate-900 p-4 rounded-2xl text-center mt-3 animate-pulse"><p class="text-[8px] text-teal-400 font-black uppercase">Match Credentials</p><div class="flex justify-center gap-6 text-white font-mono mt-1"><span>ID: ${t.room_id||'Wait'}</span><span>PS: ${t.room_password||'...'}</span></div></div>` : '';
                    let res = f==='Completed' ? `<div class="flex gap-2 mt-2"><div class="flex-1 bg-teal-50 p-2 rounded-xl text-center"><p class="text-[8px] font-black text-teal-600 uppercase leading-none">Rank</p><p class="font-black text-slate-800 text-xs mt-1">#${t.participants[currentUser.uid].rank||'-'}</p></div><div class="flex-1 bg-teal-600 p-2 rounded-xl text-center"><p class="text-[8px] font-black text-white/50 uppercase leading-none">Winnings</p><p class="font-black text-white text-xs mt-1">₹${t.participants[currentUser.uid].winningAmount||0}</p></div></div>` : '';
                    list.innerHTML += `<div class="bg-white p-4 rounded-3xl border shadow-sm"><h4 class="font-black text-slate-800 text-sm uppercase">${t.title}</h4>${room}${res}</div>`;
                }
            });
            document.querySelectorAll('.m-tab').forEach(b => b.className = "m-tab flex-1 py-2.5 rounded-xl text-[10px] font-black text-slate-400 transition-all");
            event.currentTarget.className = "m-tab flex-1 py-2.5 rounded-xl text-[10px] font-black bg-white text-teal-600 shadow-sm transition-all";
        };

        window.submitDep = async () => {
            const a = parseInt(document.getElementById('in-dep-amt').value), u = document.getElementById('in-dep-utr').value;
            if(a < 10 || u.length < 6) return alert("Min ₹10 & valid UTR required.");
            await push(ref(db, 'addMoneyRequests'), { uid: currentUser.uid, amount: a, txnId: u, status: 'pending', date: Date.now() });
            alert("Verification Sent!"); closeModal('dep');
        };

        window.submitWithdrawal = async () => {
            const a = parseInt(document.getElementById('in-with-amt').value), upi = document.getElementById('in-with-upi').value;
            const u = (await get(ref(db, `users/${currentUser.uid}`))).val();
            if(a < 10 || a > u.wallet) return alert("Min ₹10 or Low Balance!");
            await push(ref(db, 'withdrawRequests'), { uid: currentUser.uid, amount: a, upi_id: upi, status: 'pending', date: Date.now() });
            alert("Requested Successfully!"); closeModal('with');
        };

        window.switchTab = id => { 
            document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
            document.getElementById(`tab-${id}`).classList.add('active');
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('nav-active'));
            document.getElementById(`btn-${id}`).classList.add('nav-active');
            if(id==='matches') renderMatches('Upcoming');
        };
        
        window.toggleAuth = m => { isSignup = (m==='signup'); document.getElementById('signup-fields').classList.toggle('hidden', !isSignup); document.getElementById('tab-l').className = isSignup ? "flex-1 py-3 font-bold text-xs text-slate-400" : "flex-1 py-3 font-bold text-xs bg-white shadow-sm text-teal-600"; };
        window.openModal = id => document.getElementById(`modal-${id}`).classList.remove('hidden');
        window.closeModal = id => document.getElementById(`modal-${id}`).classList.add('hidden');
        window.logout = () => signOut(auth);
        window.forgotPass = () => { const e = prompt("Email:"); if(e) sendPasswordResetEmail(auth, e).then(()=>alert("Sent!")); };
    </script>
</body>
</html>
