<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>スマホ電源OFFタイマー</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        @keyframes pulseGlow {
            0%, 100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.4); }
            50% { box-shadow: 0 0 0 16px rgba(239, 68, 68, 0); }
        }
        .pulse-warning {
            animation: pulseGlow 2s infinite;
        }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen flex flex-col justify-between selection:bg-indigo-500 selection:text-white">

    <header class="w-full py-4 px-6 bg-slate-800/80 backdrop-blur-md border-b border-slate-700/60 flex items-center justify-between sticky top-0 z-50">
        <div class="flex items-center gap-2.5">
            <div class="w-8 h-8 rounded-lg bg-indigo-600 flex items-center justify-center font-bold text-white shadow-md shadow-indigo-500/20">
                ⏱️
            </div>
            <h1 class="font-bold text-base tracking-tight text-slate-100">電源OFFタイマー</h1>
        </div>
        <div class="flex items-center gap-2">
            <button id="login-btn" onclick="openLoginModal()" class="text-xs font-medium text-slate-200 hover:text-white bg-slate-800 hover:bg-slate-700 px-3.5 py-2 rounded-xl transition flex items-center gap-2 cursor-pointer border border-slate-600/40 shadow-sm">
                <svg class="w-4 h-4" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
                    <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
                    <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
                    <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
                </svg>
                ログイン
            </button>
            <button onclick="showHistoryView()" class="text-xs font-medium text-slate-300 hover:text-white bg-slate-700/60 hover:bg-slate-700 px-3.5 py-2 rounded-xl transition flex items-center gap-1.5 cursor-pointer border border-slate-600/40">
                📊 履歴を見る
            </button>
        </div>
    </header>

    <main class="flex-1 flex flex-col items-center justify-center p-4 max-w-md mx-auto w-full">

        <div id="view-initial" class="w-full bg-slate-800 border border-slate-700/80 rounded-3xl p-7 shadow-2xl text-center">
            <div class="mb-6">
                <div class="w-16 h-16 bg-indigo-500/10 text-indigo-400 rounded-2xl flex items-center justify-center mx-auto mb-4 text-3xl border border-indigo-500/20 shadow-inner">
                    ⚡
                </div>
                <h2 class="text-xl font-semibold text-white mb-2">電源OFFの時間を計測</h2>
                <p class="text-sm text-slate-400 leading-relaxed">
                    計測開始ボタンを押した後、10秒以内にスマホの電源を切ってください。再び電源を入れてこの画面に戻ると、自動で計測がストップします。
                </p>
            </div>
            
            <div class="space-y-3">
                <button onclick="startTimerFlow()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3.5 px-6 rounded-2xl transition shadow-lg shadow-indigo-600/25 active:scale-[0.98] cursor-pointer">
                    計測を開始する
                </button>
                <button onclick="showHistoryView()" class="w-full bg-slate-700/50 hover:bg-slate-700 text-slate-300 hover:text-white font-medium py-3 px-6 rounded-2xl transition border border-slate-600/50 cursor-pointer flex items-center justify-center gap-2">
                    過去の計測履歴
                </button>
            </div>
        </div>

        <div id="view-warning" class="hidden w-full bg-slate-800 border-2 border-rose-500/80 rounded-3xl p-7 shadow-2xl text-center pulse-warning">
            <div class="mb-4">
                <span class="inline-block bg-rose-500/10 text-rose-400 text-xs font-semibold px-3 py-1 rounded-full uppercase tracking-wider mb-2 border border-rose-500/20">
                    ⚠️ 10秒の猶予期間
                </span>
                <h2 class="text-2xl font-bold text-rose-400 mb-2">今すぐ電源を切れ！</h2>
                <p class="text-sm text-slate-300">
                    スマホ本体の電源ボタンを長押ししてシャットダウンしてください。このタブから離れるとタイマーが有効になります。
                </p>
            </div>
            
            <div class="my-6">
                <div id="countdown-number" class="text-6xl font-black text-rose-400 tracking-tight">10</div>
                <p class="text-xs text-slate-400 mt-2">秒以内に電源を切る必要があります</p>
            </div>

            <div class="bg-amber-500/10 p-3.5 rounded-2xl text-xs text-amber-300 border border-amber-500/20 text-left mb-4">
                💡 10秒以内に電源を切らなかった場合、自動でやり直しになります。
            </div>
            
            <button onclick="cancelTimer()" class="text-xs text-slate-400 hover:text-slate-200 underline cursor-pointer">
                キャンセルする
            </button>
        </div>

        <div id="view-failed" class="hidden w-full bg-slate-800 border border-slate-700/80 rounded-3xl p-7 shadow-2xl text-center">
            <div class="mb-6">
                <div class="w-16 h-16 bg-amber-500/10 text-amber-400 rounded-2xl flex items-center justify-center mx-auto mb-3 text-2xl border border-amber-500/20">
                    ⏱️
                </div>
                <h2 class="text-xl font-semibold text-white mb-2">電源が切られませんでした</h2>
                <p class="text-sm text-slate-400 leading-relaxed">
                    10秒以内にブラウザから離れなかったため、安全のためタイマーをリセットしました。もう一度お試しください。
                </p>
            </div>
            <button onclick="resetApp()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3.5 px-6 rounded-2xl transition shadow-lg cursor-pointer">
                もう一度やり直す
            </button>
        </div>

        <div id="view-waiting" class="hidden w-full bg-slate-800 border border-slate-700/80 rounded-3xl p-7 shadow-2xl text-center">
            <div class="mb-6">
                <div class="relative w-16 h-16 mx-auto mb-4">
                    <div class="absolute inset-0 border-4 border-indigo-500/20 rounded-full"></div>
                    <div class="absolute inset-0 border-4 border-indigo-500 border-t-transparent rounded-full animate-spin"></div>
                </div>
                <h2 class="text-xl font-semibold text-white mb-2">電源OFF計測中...</h2>
                <p class="text-sm text-slate-400 leading-relaxed">
                    スマホの電源が切れている間、時間を記録しています。再びスマホの電源を入れてこの画面を開いてください。
                </p>
            </div>
            <button onclick="resetApp()" class="text-xs text-slate-400 hover:text-slate-200 underline cursor-pointer">
                強制リセットする
            </button>
        </div>

        <div id="view-result" class="hidden w-full bg-slate-800 border border-slate-700/80 rounded-3xl p-7 shadow-2xl text-center">
            <div class="mb-6">
                <div class="w-16 h-16 bg-emerald-500/10 text-emerald-400 rounded-2xl flex items-center justify-center mx-auto mb-3 text-2xl border border-emerald-500/20">
                    🎉
                </div>
                <h2 class="text-xl font-semibold text-white mb-1">電源の復旧を確認しました！</h2>
                <p class="text-xs text-slate-400">お疲れ様でした。電源OFFだった時間はこちらです：</p>
            </div>

            <div class="bg-slate-900/80 border border-slate-700/80 rounded-2xl p-5 mb-6 shadow-inner">
                <div id="result-time" class="text-3xl font-bold text-indigo-400">0時間 00分 00秒</div>
                <div id="result-detail" class="text-xs text-slate-400 mt-2"></div>
            </div>

            <div class="space-y-3">
                <button onclick="resetApp()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-semibold py-3.5 px-6 rounded-2xl transition shadow-lg cursor-pointer">
                    もう一度計測する
                </button>
                <button onclick="showHistoryView()" class="w-full bg-slate-700/50 hover:bg-slate-700 text-slate-300 hover:text-white font-medium py-3 px-6 rounded-2xl transition border border-slate-600/50 cursor-pointer">
                    履歴を確認する
                </button>
            </div>
        </div>

        <div id="view-history" class="hidden w-full bg-slate-800 border border-slate-700/80 rounded-3xl p-6 shadow-2xl text-left">
            <div class="flex items-center justify-between mb-4 pb-3 border-b border-slate-700/80">
                <h2 class="text-base font-semibold text-white flex items-center gap-2">
                    📊 過去の計測履歴
                </h2>
                <button onclick="resetApp()" class="text-xs text-indigo-400 hover:bg-indigo-500/10 px-3 py-1.5 rounded-xl transition cursor-pointer font-medium">
                    ← ホームに戻る
                </button>
            </div>

            <div id="history-list" class="space-y-3 max-h-72 overflow-y-auto pr-1">
                <!-- 動的に挿入されます -->
            </div>

            <div class="mt-6 flex justify-between items-center pt-3 border-t border-slate-700/80">
                <button onclick="clearHistory()" class="text-xs text-rose-400 hover:underline transition cursor-pointer font-medium">
                    🗑️ 履歴をすべて削除
                </button>
                <span id="history-count" class="text-xs text-slate-400">全 0 件</span>
            </div>
        </div>

        <!-- ログインモーダル -->
        <div id="login-modal" class="hidden fixed inset-0 z-[100] flex items-center justify-center bg-slate-950/80 backdrop-blur-sm p-4">
            <div class="bg-slate-800 border border-slate-700 rounded-3xl p-6 w-full max-w-sm shadow-2xl relative">
                <button onclick="closeLoginModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white text-xl leading-none">&times;</button>
                <div class="text-center mb-6">
                    <div class="w-14 h-14 bg-white rounded-full flex items-center justify-center mx-auto mb-3 shadow-md">
                        <svg class="w-7 h-7" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
                            <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
                            <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
                            <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
                        </svg>
                    </div>
                    <h2 class="text-lg font-bold text-white">アカウントでログイン</h2>
                    <p class="text-xs text-slate-400 mt-2 text-left leading-relaxed">
                        アカウントを連携すると、計測した電源OFF時間をクラウドに永続的に記録できます。<br>
                        端末の変更やキャッシュのクリアをしてもデータが消えません。
                    </p>
                </div>
                <div id="login-actions" class="space-y-3">
                    <button onclick="startLogin()" class="w-full bg-white hover:bg-slate-100 text-slate-700 font-semibold py-3 px-6 rounded-2xl transition shadow-lg flex items-center justify-center gap-3 cursor-pointer border border-slate-200">
                        <svg class="w-5 h-5" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
                            <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
                            <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
                            <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
                        </svg>
                        Google アカウントで続行
                    </button>
                </div>
            </div>
        </div>

        <!-- トースト通知コンテナ -->
        <div id="toast-container" class="fixed bottom-6 left-1/2 transform -translate-x-1/2 z-[100] flex flex-col gap-2 pointer-events-none"></div>

    </main>

    <footer class="w-full py-4 text-center text-xs text-slate-500 bg-slate-800/40 border-t border-slate-800">
        電源OFFタイマー &copy; 2026
    </footer>

    <script>
        const STORAGE_KEY_STATE = 'phone_timer_state';
        const STORAGE_KEY_START = 'phone_timer_start';
        const STORAGE_KEY_HISTORY = 'phone_timer_history';

        let countdownInterval = null;
        let timeLeft = 10;

        window.onload = function() {
            checkCurrentState();
        };

        // バックグラウンドに移行したとき（電源オフ操作など）の処理
        function handleBackground() {
            const state = localStorage.getItem(STORAGE_KEY_STATE);
            if (state === 'countdown') {
                if (countdownInterval) clearInterval(countdownInterval);
                startActualMeasurement();
            }
        }

        // フォアグラウンドに復帰したとき（電源オンしてブラウザを開いたとき）の処理
        function handleForeground() {
            const state = localStorage.getItem(STORAGE_KEY_STATE);
            if (state === 'running') {
                const startTime = parseInt(localStorage.getItem(STORAGE_KEY_START), 10);
                if (startTime) {
                    const now = Date.now();
                    const elapsedMs = now - startTime;
                    saveHistory(startTime, now, elapsedMs);
                    showResult(elapsedMs, startTime, now);
                }
            }
        }

        // Page Visibility API による自動判定
        document.addEventListener('visibilitychange', function() {
            if (document.hidden) {
                handleBackground();
            } else {
                handleForeground();
            }
        });

        // スマホのシャットダウン画面が出た際のフォーカス外れも検知
        window.addEventListener('blur', handleBackground);
        window.addEventListener('focus', function() {
            if (!document.hidden) handleForeground();
        });

        // 複数タブ間の状態同期（別タブで操作した時に現在のタブにも反映）
        window.addEventListener('storage', function(e) {
            if (e.key === STORAGE_KEY_STATE || e.key === STORAGE_KEY_START) {
                checkCurrentState();
            }
        });

        function checkCurrentState() {
            const state = localStorage.getItem(STORAGE_KEY_STATE);
            const startTime = parseInt(localStorage.getItem(STORAGE_KEY_START), 10);

            if (state === 'running' && startTime) {
                const now = Date.now();
                const elapsedMs = now - startTime;
                saveHistory(startTime, now, elapsedMs);
                showResult(elapsedMs, startTime, now);
            } else if (state === 'waiting') {
                showView('view-waiting');
            } else {
                resetApp();
            }
        }

        function startTimerFlow() {
            showView('view-warning');
            timeLeft = 15; // シャットダウン操作の余裕を持たせるため15秒に変更
            document.getElementById('countdown-number').textContent = timeLeft;

            localStorage.setItem(STORAGE_KEY_STATE, 'countdown');

            if (countdownInterval) clearInterval(countdownInterval);

            countdownInterval = setInterval(() => {
                timeLeft--;
                document.getElementById('countdown-number').textContent = timeLeft;

                if (timeLeft <= 0) {
                    clearInterval(countdownInterval);
                    if (!document.hidden && document.hasFocus()) {
                        // 15秒経ってもタブから離れなかった場合
                        localStorage.setItem(STORAGE_KEY_STATE, 'failed');
                        showView('view-failed');
                    }
                }
            }, 1000);
        }

        function cancelTimer() {
            if (countdownInterval) clearInterval(countdownInterval);
            resetApp();
        }

        function startActualMeasurement() {
            const now = Date.now();
            localStorage.setItem(STORAGE_KEY_START, now);
            localStorage.setItem(STORAGE_KEY_STATE, 'running');
            showView('view-waiting');
        }

        function saveHistory(startTime, endTime, elapsedMs) {
            let history = JSON.parse(localStorage.getItem(STORAGE_KEY_HISTORY) || '[]');
            const lastItem = history[0];
            if (!lastItem || lastItem.startTime !== startTime) {
                const newRecord = {
                    id: Date.now().toString(),
                    startTime: startTime,
                    endTime: endTime,
                    duration: elapsedMs
                };
                history.unshift(newRecord);
                localStorage.setItem(STORAGE_KEY_HISTORY, JSON.stringify(history));

                // クラウドにも同期（ログイン中であれば）
                if (window.syncToCloud) {
                    window.syncToCloud(newRecord);
                }
            }
        }

        function showResult(elapsedMs, startTime, endTime) {
            localStorage.removeItem(STORAGE_KEY_STATE);
            localStorage.removeItem(STORAGE_KEY_START);

            showView('view-result');

            const totalSeconds = Math.max(0, Math.floor(elapsedMs / 1000));
            const hours = Math.floor(totalSeconds / 3600);
            const minutes = Math.floor((totalSeconds % 3600) / 60);
            const seconds = totalSeconds % 60;

            document.getElementById('result-time').innerText = 
                `${hours}時間 ${minutes}分 ${seconds}秒`;

            const startDateStr = new Date(startTime).toLocaleTimeString();
            const endDateStr = new Date(endTime).toLocaleTimeString();
            document.getElementById('result-detail').innerText = 
                 `計測開始: ${startDateStr} 〜 復旧確認: ${endDateStr}`;
        }

        function showHistoryView() {
            showView('view-history');
            renderHistoryList();
        }

        function renderHistoryList() {
            const historyListEl = document.getElementById('history-list');
            const historyCountEl = document.getElementById('history-count');
            
            // クラウドデータが存在していれば優先表示、なければローカルデータを表示
            const history = window.cloudHistory ? window.cloudHistory : JSON.parse(localStorage.getItem(STORAGE_KEY_HISTORY) || '[]');

            const sourceText = window.cloudHistory ? ' (☁️ クラウド同期中)' : ' (📱 ローカル保存)';
            historyCountEl.textContent = `全 ${history.length} 件${sourceText}`;

            if (history.length === 0) {
                historyListEl.innerHTML = `
                    <div class="text-center py-8 text-slate-500 text-sm">
                        まだ計測履歴がありません
                    </div>
                `;
                return;
            }

            let html = '';
            history.forEach(item => {
                const totalSeconds = Math.max(0, Math.floor(item.duration / 1000));
                const hours = Math.floor(totalSeconds / 3600);
                const minutes = Math.floor((totalSeconds % 3600) / 60);
                const seconds = totalSeconds % 60;

                const dateStr = new Date(item.startTime).toLocaleDateString();
                const startTimeStr = new Date(item.startTime).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
                const endTimeStr = new Date(item.endTime).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});

                html += `
                    <div class="bg-slate-900/60 border border-slate-700/80 rounded-2xl p-4 flex items-center justify-between">
                        <div>
                            <div class="text-xs text-slate-400 mb-1">${dateStr} (${startTimeStr} 〜 ${endTimeStr})</div>
                            <div class="text-base font-bold text-indigo-400">
                                ${hours > 0 ? hours + '時間 ' : ''}${minutes}分 ${seconds}秒
                            </div>
                        </div>
                        <div class="text-right">
                            <span class="bg-emerald-500/10 text-emerald-400 text-xs px-2.5 py-1 rounded-full border border-emerald-500/20 font-medium">完了</span>
                        </div>
                    </div>
                `;
            });
            historyListEl.innerHTML = html;
        }

        function clearHistory() {
            if (window.cloudHistory && window.clearCloudHistory) {
                window.clearCloudHistory();
            } else {
                localStorage.removeItem(STORAGE_KEY_HISTORY);
                renderHistoryList();
                showToast("ローカルの履歴を削除しました", "success");
            }
        }

        function resetApp() {
            localStorage.removeItem(STORAGE_KEY_STATE);
            localStorage.removeItem(STORAGE_KEY_START);
            if (countdownInterval) clearInterval(countdownInterval);

            showView('view-initial');
        }

        function showView(viewId) {
            const views = ['view-initial', 'view-warning', 'view-failed', 'view-waiting', 'view-result', 'view-history'];
            views.forEach(id => {
                const el = document.getElementById(id);
                if (el) {
                    if (id === viewId) {
                        el.classList.remove('hidden');
                    } else {
                        el.classList.add('hidden');
                    }
                }
            });
        }

        // --- UI Utility Functions ---
        function openLoginModal() {
            document.getElementById('login-modal').classList.remove('hidden');
        }
        
        function closeLoginModal() {
            document.getElementById('login-modal').classList.add('hidden');
        }

        function startLogin() {
            closeLoginModal();
            if (window.initFirebase) {
                window.initFirebase();
            } else {
                showToast("システム準備中です。少し待ってからお試しください。", "error");
            }
        }

        function showToast(message, type = 'success') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            const bgColor = type === 'success' ? 'bg-emerald-600/95' : 'bg-rose-600/95';
            toast.className = `${bgColor} text-white text-xs font-semibold px-5 py-3 rounded-full shadow-lg backdrop-blur-md transform transition-all duration-300 translate-y-8 opacity-0 flex items-center gap-2 border border-white/10`;
            toast.innerHTML = type === 'success' ? `✅ ${message}` : `⚠️ ${message}`;
            container.appendChild(toast);

            requestAnimationFrame(() => {
                toast.classList.remove('translate-y-8', 'opacity-0');
            });

            setTimeout(() => {
                toast.classList.add('translate-y-8', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInWithCustomToken, signInAnonymously, signOut, GoogleAuthProvider, signInWithPopup, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, collection, addDoc, getDocs, deleteDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const appId = typeof __app_id !== 'undefined' ? __app_id : 'timer-app-123';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : null;
        const initialToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        let app, auth, db, currentUser = null;
        let unsubscribeHistory = null;
        
        // グローバル変数として保持し、通常のscriptタグから参照できるようにする
        window.cloudHistory = null; 

        // Firebaseの初期化を即時実行
        if (firebaseConfig && !app) {
            app = initializeApp(firebaseConfig);
            auth = getAuth(app);
            db = getFirestore(app);

            // 認証状態の監視（別タブでログイン/ログアウトした際にも同期される）
            onAuthStateChanged(auth, (user) => {
                if (user && !user.isAnonymous) {
                    currentUser = user;
                    updateLoginButtonUI();
                    listenToCloudHistory();
                    syncLocalToCloudInitial();
                } else {
                    currentUser = null;
                    updateLogoutButtonUI();
                }
            });

            // 初回認証
            if (initialToken) {
                signInWithCustomToken(auth, initialToken).catch(console.error);
            } else {
                signInAnonymously(auth).catch(console.error);
            }
        }

        // ログイン処理のエントリーポイント
        window.initFirebase = async () => {
            if (!firebaseConfig) {
                window.showToast("ここではクラウド機能が使えません。画面右側の「Preview」から実行してください。", "error");
                return;
            }
            try {
                if (initialToken) {
                    await signInWithCustomToken(auth, initialToken);
                    window.showToast("ログイン完了！データを同期します。");
                } else {
                    // Googleプロバイダを使用したログインポップアップ
                    const provider = new GoogleAuthProvider();
                    await signInWithPopup(auth, provider);
                    window.showToast("Googleアカウントでログインしました！");
                }
                closeLoginModal();
            } catch(e) {
                console.error("Login failed:", e);
                window.showToast("ログインに失敗しました。", "error");
            }
        };

        // UIをログイン状態に変更
        function updateLoginButtonUI() {
            const btn = document.getElementById('login-btn');
            const loginActions = document.getElementById('login-actions');

            if (currentUser) {
                // ヘッダーボタンの変更（アバターアイコン表示）
                btn.innerHTML = `<img src="https://ui-avatars.com/api/?name=${currentUser.uid.substring(0,2)}&background=random&color=fff&rounded=true" class="w-5 h-5 rounded-full"> ${currentUser.uid.substring(0,4)}...`;
                btn.classList.replace('bg-slate-800', 'bg-emerald-600/20');
                btn.classList.replace('text-slate-200', 'text-emerald-400');
                btn.classList.replace('border-slate-600/40', 'border-emerald-500/30');
                btn.onclick = () => openLoginModal();
                
                // モーダル内のボタンを「ログアウト」に変更
                if(loginActions) {
                    loginActions.innerHTML = `
                        <button onclick="startLogout()" class="w-full bg-slate-700 hover:bg-slate-600 text-white font-semibold py-3 px-6 rounded-2xl transition shadow-lg flex items-center justify-center gap-2 cursor-pointer border border-slate-600">
                            🚪 ログアウトする
                        </button>
                    `;
                }
            }
        }

        function updateLogoutButtonUI() {
            const btn = document.getElementById('login-btn');
            if (btn) {
                btn.innerHTML = `
                    <svg class="w-4 h-4" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
                        <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
                        <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
                        <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
                    </svg>
                    ログイン
                `;
                btn.className = "text-xs font-medium text-slate-200 hover:text-white bg-slate-800 hover:bg-slate-700 px-3.5 py-2 rounded-xl transition flex items-center gap-2 cursor-pointer border border-slate-600/40 shadow-sm";
            }
            
            const loginActions = document.getElementById('login-actions');
            if(loginActions) {
                loginActions.innerHTML = `
                    <button onclick="startLogin()" class="w-full bg-white hover:bg-slate-100 text-slate-700 font-semibold py-3 px-6 rounded-2xl transition shadow-lg flex items-center justify-center gap-3 cursor-pointer border border-slate-200">
                        <svg class="w-5 h-5" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
                            <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
                            <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
                            <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
                        </svg>
                        Google アカウントで続行
                    </button>
                `;
            }

            // 履歴画面を開いていたら再描画してローカル保存モードへ切り替え
            if (!document.getElementById('view-history').classList.contains('hidden')) {
                if (window.renderHistoryList) window.renderHistoryList();
            }
        }

        // ログアウト処理
        window.startLogout = async () => {
            if (!auth) return;
            try {
                await signOut(auth);
                await signInAnonymously(auth); // ログアウト後は匿名ユーザーとして継続
                window.cloudHistory = null;
                if (unsubscribeHistory) {
                    unsubscribeHistory();
                    unsubscribeHistory = null;
                }
                closeLoginModal();
                window.showToast("ログアウトしました");
            } catch(e) {
                console.error("Logout failed", e);
                window.showToast("ログアウトに失敗しました", "error");
            }
        };

        // Firestoreの変更をリアルタイムで監視
        function listenToCloudHistory() {
            if (!currentUser) return;
            const colRef = collection(db, 'artifacts', appId, 'users', currentUser.uid, 'history');
            
            unsubscribeHistory = onSnapshot(colRef, (snapshot) => {
                const data = [];
                snapshot.forEach(doc => {
                    data.push({ firestoreId: doc.id, ...doc.data() });
                });
                // 新しい順にソート
                data.sort((a, b) => b.startTime - a.startTime);
                window.cloudHistory = data;

                // 履歴画面を開いていたら再描画をかける
                if (!document.getElementById('view-history').classList.contains('hidden')) {
                    if (window.renderHistoryList) window.renderHistoryList();
                }
            }, (error) => {
                console.error("Firestore Listen Error:", error);
            });
        }

        // 計測完了時にクラウドにも追加
        window.syncToCloud = async (newRecord) => {
            if (!currentUser || !db) return;
            try {
                const colRef = collection(db, 'artifacts', appId, 'users', currentUser.uid, 'history');
                await addDoc(colRef, newRecord);
            } catch(e) {
                console.error("Save to cloud failed:", e);
            }
        };

        // 初回ログイン時に、これまでローカルに溜まっていた履歴をクラウドに上げる
        async function syncLocalToCloudInitial() {
            if (!currentUser || !db) return;
            const local = JSON.parse(localStorage.getItem(STORAGE_KEY_HISTORY) || '[]');
            if (local.length === 0) return;

            try {
                const colRef = collection(db, 'artifacts', appId, 'users', currentUser.uid, 'history');
                const snap = await getDocs(colRef);
                const cloudIds = new Set();
                snap.forEach(d => cloudIds.add(d.data().id));

                let syncedCount = 0;
                for (const item of local) {
                    if (!cloudIds.has(item.id.toString())) {
                        await addDoc(colRef, item);
                        syncedCount++;
                    }
                }
                if (syncedCount > 0) window.showToast(`${syncedCount}件の過去データをクラウドに同期しました`);
            } catch (e) {
                console.error("Initial sync failed", e);
            }
        }

        // クラウドの履歴を全削除
        window.clearCloudHistory = async () => {
            if (!currentUser || !db) return;
            try {
                window.showToast("削除中...");
                const colRef = collection(db, 'artifacts', appId, 'users', currentUser.uid, 'history');
                const snap = await getDocs(colRef);
                const deletePromises = [];
                snap.forEach(d => {
                    deletePromises.push(deleteDoc(doc(db, 'artifacts', appId, 'users', currentUser.uid, 'history', d.id)));
                });
                await Promise.all(deletePromises);
                
                // ローカルも消去
                localStorage.removeItem(STORAGE_KEY_HISTORY);
                window.cloudHistory = [];
                
                window.showToast("すべての履歴を削除しました");
                if (window.renderHistoryList) window.renderHistoryList();
            } catch (e) {
                console.error("Delete all failed:", e);
                window.showToast("削除に失敗しました", "error");
            }
        };
    </script>
</body>
</html>
