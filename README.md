<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule & Points Table Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .hidden-section { display: none; }
    </style>
</head>
<body class="bg-slate-100 font-sans text-gray-800">

    <!-- Navbar -->
    <nav class="bg-emerald-700 text-white p-4 shadow-md flex justify-between items-center">
        <h1 class="text-xl font-bold">🏏 Cricket Portal</h1>
        <div id="nav-user-info" class="flex items-center gap-4 hidden-section">
            <span id="nav-phone" class="text-sm bg-emerald-800 px-3 py-1 rounded"></span>
            <span id="nav-wallet" class="text-sm bg-amber-500 text-slate-900 font-bold px-3 py-1 rounded"></span>
            <button onclick="logout()" class="bg-red-600 px-3 py-1 text-sm rounded hover:bg-red-700">Logout</button>
        </div>
    </nav>

    <div class="container mx-auto p-4 max-w-5xl">

        <!-- 1. LOGIN SECTION -->
        <div id="login-section" class="bg-white p-6 rounded-lg shadow-md max-w-md mx-auto mt-10">
            <h2 class="text-2xl font-bold text-center mb-4 text-emerald-700">Login / Register</h2>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Mobile Number:</label>
                <input type="text" id="login-phone" placeholder="Enter Mobile Number" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Unique User ID (Must be Unique):</label>
                <input type="text" id="login-userid" placeholder="e.g. user_abc123" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <button onclick="handleLogin()" class="w-full bg-emerald-600 text-white py-2 rounded font-bold hover:bg-emerald-700">Login</button>
            <p class="text-xs text-gray-500 mt-3 text-center">Note: 50 Points free on new number. Special number `9569981484` gets 5000 points!</p>
        </div>

        <!-- 2. MAIN DASHBOARD -->
        <div id="dashboard-section" class="hidden-section">
            <!-- Tabs -->
            <div class="flex flex-wrap gap-2 mb-6 border-b pb-2">
                <button onclick="switchTab('matches')" class="px-4 py-2 bg-emerald-600 text-white rounded font-medium tab-btn" id="btn-matches">Match Schedule</button>
                <button onclick="switchTab('points')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-points">Points Table</button>
                <button onclick="switchTab('subscription')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-subscription">Subscriptions</button>
                <button onclick="switchTab('admin')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn hidden-section" id="btn-admin">Admin Panel</button>
            </div>

            <!-- TAB 1: MATCH SCHEDULE -->
            <div id="tab-matches" class="space-y-4">
                <h3 class="text-xl font-bold text-emerald-800">Scheduled Matches</h3>
                <div id="matches-list" class="grid gap-4">
                    <!-- Dynamic Matches -->
                </div>
            </div>

            <!-- TAB 2: POINTS TABLE -->
            <div id="tab-points" class="hidden-section space-y-6">
                <h3 class="text-xl font-bold text-emerald-800">ICC Points Table</h3>
                <div id="points-tables-container" class="space-y-6">
                    <!-- Dynamic Groups Points Table -->
                </div>
            </div>

            <!-- TAB 3: SUBSCRIPTION -->
            <div id="tab-subscription" class="hidden-section bg-white p-6 rounded-lg shadow-md">
                <h3 class="text-xl font-bold mb-4 text-emerald-800">Active Admin Subscription</h3>
                <div id="subscription-status" class="mb-6 p-4 bg-amber-50 border border-amber-200 rounded">
                    <!-- Sub Status -->
                </div>
                <h4 class="text-lg font-semibold mb-3">Buy / Activate Subscription (Deduct Points)</h4>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">30 Minutes Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 149 Points</p>
                        <button onclick="buySubscription('30min', 149)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Half Monthly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 400 Points</p>
                        <button onclick="buySubscription('half_monthly', 400)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Monthly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 600 Points</p>
                        <button onclick="buySubscription('monthly', 600)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Half Yearly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 6000 Points</p>
                        <button onclick="buySubscription('half_yearly', 6000)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm col-span-full">
                        <p class="font-bold">Yearly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: 8000 Points</p>
                        <button onclick="buySubscription('yearly', 8000)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                </div>

                <div class="bg-emerald-50 p-4 rounded border border-emerald-200">
                    <h4 class="font-bold text-emerald-900">Point Packages (Contact: 9569981484)</h4>
                    <p class="text-sm">₹80 = 1500 Points | ₹249 = 22000 Points</p>
                </div>
            </div>

            <!-- TAB 4: ADMIN PANEL -->
            <div id="tab-admin" class="hidden-section space-y-6">
                <div class="bg-white p-6 rounded-lg shadow-md border-t-4 border-emerald-600">
                    <h3 class="text-xl font-bold text-emerald-800 mb-4">👑 Admin Panel</h3>

                    <!-- Schedule Match Form -->
                    <div class="border-b pb-6 mb-6">
                        <h4 class="font-semibold mb-3 text-lg">Schedule New Match</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm">Series Type:</label>
                                <select id="admin-series-type" class="w-full p-2 border rounded" onchange="toggleSeriesInput()">
                                    <option value="existing">Usi Series ka Match (Same Series)</option>
                                    <option value="new">New Series ka Match</option>
                                </select>
                            </div>
                            <div id="series-name-box">
                                <label class="block text-sm">Series Name:</label>
                                <input type="text" id="admin-series-name" placeholder="Series Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team 1:</label>
                                <input type="text" id="admin-team1" placeholder="Team 1 Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team 2:</label>
                                <input type="text" id="admin-team2" placeholder="Team 2 Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Match Date:</label>
                                <input type="date" id="admin-date" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Match Time:</label>
                                <input type="time" id="admin-time" class="w-full p-2 border rounded">
                            </div>
                            <div class="col-span-full">
                                <label class="block text-sm">Venue:</label>
                                <input type="text" id="admin-venue" placeholder="Stadium / Venue" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <button onclick="scheduleMatch()" class="mt-4 bg-emerald-600 text-white px-4 py-2 rounded font-bold hover:bg-emerald-700">Publish / Schedule Match</button>
                    </div>

                    <!-- Points Table Updater -->
                    <div class="border-b pb-6 mb-6">
                        <h4 class="font-semibold mb-3 text-lg">Update Points Table & Match Score</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                            <div>
                                <label class="block text-sm">Select Group:</label>
                                <select id="admin-group-select" class="w-full p-2 border rounded" onchange="loadGroupTeamsForUpdate()">
                                    <option value="Group A">Group A</option>
                                    <option value="Group B">Group B</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Select Team to Update:</label>
                                <select id="admin-team-select" class="w-full p-2 border rounded">
                                    <!-- Dynamic Teams -->
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Match Result / Status:</label>
                                <select id="admin-match-result" class="w-full p-2 border rounded">
                                    <option value="won">Won</option>
                                    <option value="lost">Lost</option>
                                    <option value="tied">Tied / NR</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Net Run Rate (NRR) increment/decrement (+/-):</label>
                                <input type="number" step="0.01" id="admin-nrr-change" placeholder="e.g. +0.45 or -0.2" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <button onclick="updatePointsTable()" class="bg-blue-600 text-white px-4 py-2 rounded font-bold hover:bg-blue-700">Update ICC Points Table</button>
                    </div>

                    <!-- Admin Point Sender -->
                    <div>
                        <h4 class="font-semibold mb-3 text-lg">Send Points to User (Admin Only)</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm">Recipient User ID:</label>
                                <input type="text" id="admin-send-userid" placeholder="Enter User ID" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Points Amount:</label>
                                <input type="number" id="admin-send-points" placeholder="Points to send" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <button onclick="adminSendPoints()" class="mt-4 bg-amber-600 text-white px-4 py-2 rounded font-bold hover:bg-amber-700">Send Points</button>
                    </div>

                </div>
            </div>

        </div>

    </div>

    <!-- JavaScript Logic -->
    <script>
        // Database simulation using LocalStorage
        const DB_KEY = "cricket_portal_db_v1";

        function getDB() {
            let data = localStorage.getItem(DB_KEY);
            if (!data) {
                let initial = {
                    users: {}, // phone -> {phone, userid, wallet}
                    devices: {}, // deviceId -> [phones]
                    userIDs: [], // array of all active userIDs to prevent duplicates
                    matches: [], // list of matches
                    pointsTable: {
                        "Group A": [
                            { team: "India", p: 0, w: 0, l: 0, t: 0, pts: 0, nrr: 0.0 },
                            { team: "Pakistan", p: 0, w: 0, l: 0, t: 0, pts: 0, nrr: 0.0 }
                        ],
                        "Group B": [
                            { team: "Australia", p: 0, w: 0, l: 0, t: 0, pts: 0, nrr: 0.0 },
                            { team: "England", p: 0, w: 0, l: 0, t: 0, pts: 0, nrr: 0.0 }
                        ]
                    },
                    subscription: { activeUntil: 0 } // timestamp
                };
                localStorage.setItem(DB_KEY, JSON.stringify(initial));
                return initial;
            }
            return JSON.parse(data);
        }

        function saveDB(db) {
            localStorage.setItem(DB_KEY, JSON.stringify(db));
        }

        let currentUser = null;
        let currentDeviceId = localStorage.getItem("device_id");
        if (!currentDeviceId) {
            currentDeviceId = "dev_" + Math.random().toString(36).substring(2, 9);
            localStorage.setItem("device_id", currentDeviceId);
        }

        // Login Handler
        function handleLogin() {
            let phone = document.getElementById("login-phone").value.trim();
            let userid = document.getElementById("login-userid").value.trim();

            if (!phone || !userid) {
                alert("Please enter both Mobile Number and User ID.");
                return;
            }

            let db = getDB();

            // Check duplicate User ID across all users
            if (db.userIDs.includes(userid) && (!db.users[phone] || db.users[phone].userid !== userid)) {
                alert("This User ID is already taken by another user. Please choose a unique User ID.");
                return;
            }

            // Device limit check (Max 3 numbers per device)
            if (!db.devices[currentDeviceId]) {
                db.devices[currentDeviceId] = [];
            }

            let devicePhones = db.devices[currentDeviceId];
            if (!devicePhones.includes(phone) && devicePhones.length >= 3) {
                alert("Maximum 3 numbers allowed per device!");
                return;
            }

            // Register or Login user
            if (!db.users[phone]) {
                let initialPoints = 50;
                if (phone === "9569981484") {
                    initialPoints = 5000;
                }
                db.users[phone] = { phone: phone, userid: userid, wallet: initialPoints };
                db.userIDs.push(userid);
                if (!devicePhones.includes(phone)) {
                    devicePhones.push(phone);
                }
            } else {
                // Update User ID if changed and unique
                if (db.users[phone].userid !== userid) {
                    let idx = db.userIDs.indexOf(db.users[phone].userid);
                    if (idx !== -1) db.userIDs.splice(idx, 1);
                    db.userIDs.push(userid);
                    db.users[phone].userid = userid;
                }
                if (!devicePhones.includes(phone)) {
                    devicePhones.push(phone);
                }
            }

            saveDB(db);
            currentUser = phone;
            initDashboard();
        }

        function logout() {
            currentUser = null;
            document.getElementById("login-section").classList.remove("hidden-section");
            document.getElementById("dashboard-section").classList.add("hidden-section");
            document.getElementById("nav-user-info").classList.add("hidden-section");
        }

        function initDashboard() {
            document.getElementById("login-section").classList.add("hidden-section");
            document.getElementById("dashboard-section").classList.remove("hidden-section");
            document.getElementById("nav-user-info").classList.remove("hidden-section");

            let db = getDB();
            let user = db.users[currentUser];

            document.getElementById("nav-phone").innerText = `📞 ${user.phone} (${user.userid})`;
            document.getElementById("nav-wallet").innerText = `💰 Wallet: ${user.wallet} Pts`;

            // Check Subscription for Admin Panel visibility
            let now = new Date().getTime();
            let isAdminActive = db.subscription.activeUntil > now;

            if (isAdminActive || currentUser === "9569981484") {
                document.getElementById("btn-admin").classList.remove("hidden-section");
            } else {
                document.getElementById("btn-admin").classList.add("hidden-section");
            }

            renderMatches();
            renderPointsTable();
            renderSubscriptionStatus();
            loadGroupTeamsForUpdate();
        }

        function switchTab(tabName) {
            ['matches', 'points', 'subscription', 'admin'].forEach(t => {
                document.getElementById(`tab-${t}`).classList.add("hidden-section");
                document.getElementById(`btn-${t}`).classList.remove("bg-emerald-600", "text-white");
                document.getElementById(`btn-${t}`).classList.add("bg-gray-200", "text-gray-700");
            });

            document.getElementById(`tab-${tabName}`).classList.remove("hidden-section");
            document.getElementById(`btn-${tabName}`).classList.remove("bg-gray-200", "text-gray-700");
            document.getElementById(`btn-${tabName}`).classList.add("bg-emerald-600", "text-white");
        }

        // Match Scheduling
        function toggleSeriesInput() {
            let type = document.getElementById("admin-series-type").value;
            let box = document.getElementById("series-name-box");
            if (type === "existing") {
                box.style.display = "block";
            } else {
                box.style.display = "block"; // New series needs name too
            }
        }

        function scheduleMatch() {
            let db = getDB();
            let now = new Date().getTime();
            if (db.subscription.activeUntil < now && currentUser !== "9569981484") {
                alert("Admin subscription required to schedule matches!");
                return;
            }

            let seriesType = document.getElementById("admin-series-type").value;
            let seriesName = document.getElementById("admin-series-name").value.trim();
            let team1 = document.getElementById("admin-team1").value.trim();
            let team2 = document.getElementById("admin-team2").value.trim();
            let date = document.getElementById("admin-date").value;
            let time = document.getElementById("admin-time").value;
            let venue = document.getElementById("admin-venue").value.trim();

            if (!team1 || !team2 || !date || !time || !venue || !seriesName) {
                alert("Please fill all match details.");
                return;
            }

            db.matches.push({
                seriesType,
                seriesName,
                team1,
                team2,
                date,
                time,
                venue,
                status: "Upcoming",
                score: "Yet to start"
            });

            saveDB(db);
            alert("Match scheduled successfully!");
            renderMatches();
            switchTab("matches");
        }

        function renderMatches() {
            let db = getDB();
            let container = document.getElementById("matches-list");
            container.innerHTML = "";

            if (db.matches.length === 0) {
                container.innerHTML = `<p class="text-gray-500">No matches scheduled yet.</p>`;
                return;
            }

            let lastSeries = "";
            db.matches.forEach((m, idx) => {
                let showGap = m.seriesType === 'new' || m.seriesName !== lastSeries;
                lastSeries = m.seriesName;

                let html = "";
                if (showGap && idx > 0) {
                    html += `<div class="my-6 border-t-2 border-dashed border-gray-300"></div>`;
                }

                html += `
                    <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
                        <span class="text-xs bg-emerald-100 text-emerald-800 font-bold px-2 py-1 rounded">${m.seriesName}</span>
                        <div class="flex justify-between items-center mt-3">
                            <div class="text-lg font-bold">${m.team1} vs ${m.team2}</div>
                            <div class="text-sm bg-gray-100 px-2 py-1 rounded">📅 ${m.date} | ⏰ ${m.time}</div>
                        </div>
                        <p class="text-xs text-gray-600 mt-1">🏟️ Venue: ${m.venue}</p>
                        <p class="text-sm font-semibold text-emerald-700 mt-2">Status: ${m.status} | Score: ${m.score}</p>
                    </div>
                `;
                container.innerHTML += html;
            });
        }

        // Points Table & ICC Logic
        function loadGroupTeamsForUpdate() {
            let db = getDB();
            let group = document.getElementById("admin-group-select").value;
            let teamSelect = document.getElementById("admin-team-select");
            teamSelect.innerHTML = "";

            if (db.pointsTable[group]) {
                db.pointsTable[group].forEach(t => {
                    teamSelect.innerHTML += `<option value="${t.team}">${t.team}</option>`;
                });
            }
        }

        function updatePointsTable() {
            let db = getDB();
            let group = document.getElementById("admin-group-select").value;
            let teamName = document.getElementById("admin-team-select").value;
            let result = document.getElementById("admin-match-result").value;
            let nrrChange = parseFloat(document.getElementById("admin-nrr-change").value) || 0.0;

            let teamObj = db.pointsTable[group].find(t => t.team === teamName);
            if (teamObj) {
                teamObj.p += 1;
                if (result === "won") {
                    teamObj.w += 1;
                    teamObj.pts += 2; // ICC formula: Win = 2 points
                } else if (result === "lost") {
                    teamObj.l += 1;
                } else if (result === "tied") {
                    teamObj.t += 1;
                    teamObj.pts += 1; // ICC formula: Tie/NR = 1 point
                }
                teamObj.nrr = parseFloat((teamObj.nrr + nrrChange).toFixed(2));
            }

            saveDB(db);
            alert("Points Table updated successfully!");
            renderPointsTable();
        }

        function renderPointsTable() {
            let db = getDB();
            let container = document.getElementById("points-tables-container");
            container.innerHTML = "";

            for (let group in db.pointsTable) {
                // Sort by Points descending, then NRR descending (ICC standard)
                let teams = db.pointsTable[group].sort((a, b) => b.pts - a.pts || b.nrr - a.nrr);

                let rows = "";
                teams.forEach((t, i) => {
                    rows += `
                        <tr class="border-b text-center">
                            <td class="p-2 text-left">${i + 1}. ${t.team}</td>
                            <td class="p-2">${t.p}</td>
                            <td class="p-2">${t.w}</td>
                            <td class="p-2">${t.l}</td>
                            <td class="p-2">${t.t}</td>
                            <td class="p-2 font-bold text-emerald-700">${t.pts}</td>
                            <td class="p-2">${t.nrr}</td>
                        </tr>
                    `;
                });

                container.innerHTML += `
                    <div class="bg-white rounded-lg shadow-md overflow-hidden">
                        <div class="bg-emerald-700 text-white p-3 font-bold">${group}</div>
                        <table class="w-full text-sm">
                            <tr class="bg-gray-100 border-b text-center text-xs text-gray-600">
                                <th class="p-2 text-left">Team</th>
                                <th class="p-2">P</th>
                                <th class="p-2">W</th>
                                <th class="p-2">L</th>
                                <th class="p-2">T</th>
                                <th class="p-2">Pts</th>
                                <th class="p-2">NRR</th>
                            </tr>
                            ${rows}
                        </table>
                    </div>
                `;
            }
        }

        // Subscriptions
        function buySubscription(plan, cost) {
            let db = getDB();
            let user = db.users[currentUser];

            if (user.wallet < cost) {
                alert("Insufficient points in wallet! Please contact 9569981484 to purchase points.");
                return;
            }

            user.wallet -= cost;

            let durationMs = 0;
            if (plan === '30min') durationMs = 30 * 60 * 1000;
            else if (plan === 'half_monthly') durationMs = 15 * 24 * 60 * 60 * 1000;
            else if (plan === 'monthly') durationMs = 30 * 24 * 60 * 60 * 1000;
            else if (plan === 'half_yearly') durationMs = 182 * 24 * 60 * 60 * 1000;
            else if (plan === 'yearly') durationMs = 365 * 24 * 60 * 60 * 1000;

            let now = new Date().getTime();
            if (db.subscription.activeUntil > now) {
                db.subscription.activeUntil += durationMs;
            } else {
                db.subscription.activeUntil = now + durationMs;
            }

            saveDB(db);
            alert("Subscription activated successfully!");
            initDashboard();
        }

        function renderSubscriptionStatus() {
            let db = getDB();
            let now = new Date().getTime();
            let statusBox = document.getElementById("subscription-status");

            if (db.subscription.activeUntil > now) {
                let timeLeft = Math.ceil((db.subscription.activeUntil - now) / (1000 * 60));
                statusBox.innerHTML = `<p class="text-emerald-700 font-bold">Status: Active</p><p class="text-sm">Expires in approximately ${timeLeft} minutes (or valid period).</p>`;
            } else {
                statusBox.innerHTML = `<p class="text-red-600 font-bold">Status: Inactive</p><p class="text-sm">Buy a subscription below to unlock the Admin Panel.</p>`;
            }
        }

        // Admin Point Transfer
        function adminSendPoints() {
            let db = getDB();
            let recipientId = document.getElementById("admin-send-userid").value.trim();
            let amount = parseInt(document.getElementById("admin-send-points").value);

            if (!recipientId || isNaN(amount) || amount <= 0) {
                alert("Please enter a valid recipient User ID and points amount.");
                return;
            }

            let recipientPhone = null;
            for (let ph in db.users) {
                if (db.users[ph].userid === recipientId) {
                    recipientPhone = ph;
                    break;
                }
            }

            if (!recipientPhone) {
                alert("User ID not found!");
                return;
            }

            db.users[recipientPhone].wallet += amount;
            saveDB(db);
            alert(`Successfully sent ${amount} points to User ID: ${recipientId}`);
            document.getElementById("admin-send-userid").value = "";
            document.getElementById("admin-send-points").value = "";
        }
    </script>
</body>
</html>
