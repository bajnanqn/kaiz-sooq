<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAIZ SOOQ - Boutique Manager</title>
    <!-- Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-color: #0b1120;
            --card-bg: #151e32;
            --card-border: #1e293b;
            --accent-green: #00ff88;
            --accent-blue: #3b82f6;
            --accent-purple: #a855f7;
            --accent-pink: #ec4899;
            --text-main: #ffffff;
            --text-sub: #94a3b8;
            --danger: #ef4444;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-main); padding-bottom: 80px; }

        /* Top Navigation */
        .navbar {
            background-color: var(--card-bg);
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--card-border);
            position: sticky; top: 0; z-index: 100;
        }

        .brand-title { font-size: 1.2rem; font-weight: bold; letter-spacing: 1px; }
        .badge-green {
            background: rgba(0, 255, 136, 0.1);
            color: var(--accent-green);
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 0.8rem;
            border: 1px solid var(--accent-green);
        }

        /* Layout & Cards */
        .container { padding: 15px; max-width: 600px; margin: 0 auto; }
        .card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 15px;
            border: 1px solid var(--card-border);
        }

        .card-header {
            font-size: 0.85rem;
            color: var(--text-sub);
            font-weight: 600;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            text-transform: uppercase;
        }

        .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        .stat-val { font-size: 1.4rem; font-weight: bold; margin-top: 5px; }
        .stat-val.green { color: var(--accent-green); }
        .stat-val.blue { color: var(--accent-blue); }
        .stat-val.pink { color: var(--accent-pink); }

        .btn-shortcut {
            background: #1e293b;
            border: 1px solid var(--card-border);
            color: var(--text-main);
            padding: 12px;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
        }
        .btn-shortcut i { font-size: 1.3rem; display: block; margin-bottom: 5px; color: var(--accent-green); }

        /* Bottom Nav */
        .bottom-nav {
            position: fixed; bottom: 0; left: 0; right: 0;
            background: var(--card-bg);
            display: flex; justify-content: space-around;
            padding: 10px 0;
            border-top: 1px solid var(--card-border);
            z-index: 100;
        }
        .nav-item { color: var(--text-sub); text-align: center; font-size: 0.75rem; cursor: pointer; }
        .nav-item i { font-size: 1.2rem; display: block; margin-bottom: 2px; }
        .nav-item.active { color: var(--accent-green); }

        /* Form */
        .form-group { margin-bottom: 12px; }
        label { display: block; font-size: 0.8rem; color: var(--text-sub); margin-bottom: 4px; }
        input, select {
            width: 100%; padding: 10px;
            background: #0f172a; border: 1px solid var(--card-border);
            color: white; border-radius: 6px; font-size: 0.9rem;
        }
        .hint-text { font-size: 0.75rem; color: #eab308; margin-top: 4px; }

        .btn {
            width: 100%; padding: 12px; border: none;
            border-radius: 6px; font-weight: bold; cursor: pointer;
            background: var(--accent-green); color: #000; margin-top: 10px;
        }
        .btn-status {
            padding: 8px 12px; border-radius: 6px; border: none;
            font-weight: bold; cursor: pointer; font-size: 0.8rem;
        }

        .page { display: none; }
        .page.active { display: block; }

        /* Order Items */
        .order-item {
            background: #0f172a; border-radius: 8px; padding: 12px;
            margin-bottom: 10px; border-left: 4px solid var(--accent-blue);
        }
        .order-header { display: flex; justify-content: space-between; font-weight: bold; margin-bottom: 8px; }
        .badge { background: #1e293b; padding: 2px 6px; border-radius: 4px; font-size: 0.75rem; }

        /* Modal Popup */
        .modal {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.8); z-index: 1000; justify-content: center; align-items: center;
        }
        .modal-content {
            background: var(--card-bg); width: 90%; max-width: 500px;
            padding: 20px; border-radius: 12px; border: 1px solid var(--card-border);
            max-height: 80vh; overflow-y: auto;
        }
        .close-btn { float: right; color: var(--danger); font-size: 1.2rem; cursor: pointer; }
    </style>
</head>
<body>

    <!-- Header Navbar -->
    <div class="navbar">
        <div class="brand-title"><i class="fa-solid fa-scissors" style="color:var(--accent-green)"></i> KAIZ SOOQ</div>
        <div class="badge-green"><i class="fa-solid fa-circle"></i> Active</div>
    </div>

    <div class="container">

        <!-- 1. DASHBOARD PAGE -->
        <div id="page-dashboard" class="page active">
            
            <div class="card">
                <div class="card-header">
                    <span><i class="fa-solid fa-chart-pie"></i> Financial Summary</span>
                </div>
                <div class="grid-2">
                    <div>
                        <small style="color:var(--text-sub)">Total Revenue</small>
                        <div class="stat-val blue" id="dash-revenue">₹0</div>
                    </div>
                    <div>
                        <small style="color:var(--text-sub)">Net Profit</small>
                        <div class="stat-val green" id="dash-profit">₹0</div>
                    </div>
                </div>
                <hr style="border-color:var(--card-border); margin: 12px 0;">
                <div class="grid-2">
                    <div>
                        <small style="color:var(--text-sub)">Owner Amount (₹300)</small>
                        <div class="stat-val" id="dash-owner">₹0</div>
                    </div>
                    <div>
                        <small style="color:var(--text-sub)">Stitch Charges</small>
                        <div class="stat-val" style="color:#f59e0b" id="dash-stitch">₹0</div>
                    </div>
                </div>
            </div>

            <!-- Category Breakdown -->
            <div class="card">
                <div class="card-header">
                    <span><i class="fa-solid fa-layer-group"></i> Category Summary</span>
                </div>
                <div class="grid-2">
                    <div style="background: #0f172a; padding: 10px; border-radius: 8px;">
                        <small style="color:var(--accent-pink)"><i class="fa-solid fa-person-dress"></i> Ledi Wear</small>
                        <div class="stat-val pink" id="dash-ledi-rev">₹0</div>
                        <small style="color:var(--text-sub)" id="dash-ledi-count">0 Orders</small>
                    </div>
                    <div style="background: #0f172a; padding: 10px; border-radius: 8px;">
                        <small style="color:var(--accent-blue)"><i class="fa-solid fa-baby"></i> Bebi Wear</small>
                        <div class="stat-val blue" id="dash-bebi-rev">₹0</div>
                        <small style="color:var(--text-sub)" id="dash-bebi-count">0 Orders</small>
                    </div>
                </div>
            </div>

            <!-- Action Shortcuts -->
            <div class="grid-2">
                <div class="btn-shortcut" onclick="switchPage('add-order')">
                    <i class="fa-solid fa-user-plus"></i>
                    <span>New Order</span>
                </div>
                <div class="btn-shortcut" onclick="switchPage('orders')">
                    <i class="fa-solid fa-boxes-stacked"></i>
                    <span>Active Orders</span>
                </div>
            </div>

            <!-- Next Delivery Card -->
            <div class="card" style="margin-top: 15px;">
                <div class="card-header">
                    <span><i class="fa-solid fa-truck-fast"></i> Next Delivery</span>
                </div>
                <div id="next-delivery-info" style="font-size: 0.9rem; cursor: pointer;">
                    No pending deliveries
                </div>
            </div>

            <!-- Tailor Workload -->
            <div class="card">
                <div class="card-header">
                    <span><i class="fa-solid fa-users"></i> Tailor Workload & Pay</span>
                </div>
                <div id="employee-summary-list"></div>
            </div>
        </div>

        <!-- 2. ADD ORDER PAGE -->
        <div id="page-add-order" class="page">
            <div class="card">
                <div class="card-header">
                    <span id="form-title"><i class="fa-solid fa-cart-plus"></i> Create / Edit Order</span>
                </div>
                <form id="orderForm">
                    <input type="hidden" id="editOrderId">
                    <div class="form-group">
                        <label><i class="fa-solid fa-user"></i> Customer Name</label>
                        <input type="text" id="custName" required placeholder="Name">
                    </div>
                    <div class="form-group">
                        <label><i class="fa-brands fa-whatsapp"></i> WhatsApp Number</label>
                        <input type="tel" id="custPhone" required placeholder="Phone number">
                    </div>
                    
                    <div class="grid-2">
                        <div class="form-group">
                            <label><i class="fa-solid fa-tags"></i> Category</label>
                            <select id="itemCategory">
                                <option value="Ledi Wear">Ledi Wear</option>
                                <option value="Bebi Wear">Bebi Wear</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label><i class="fa-solid fa-calendar-day"></i> Delivery Date</label>
                            <input type="date" id="deliveryDate" required>
                        </div>
                    </div>

                    <div class="grid-2">
                        <div class="form-group">
                            <label><i class="fa-solid fa-indian-rupee-sign"></i> Total Price</label>
                            <input type="number" id="orderPrice" oninput="calculateAdvance()" required placeholder="0">
                        </div>
                        <div class="form-group">
                            <label><i class="fa-solid fa-money-bill-wave"></i> Advance Paid</label>
                            <input type="number" id="advancePaid" required placeholder="0">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label><i class="fa-solid fa-calculator"></i> Total Material Cost</label>
                        <input type="number" id="materialCost" oninput="calculateAdvanceHint()" placeholder="0">
                        <div id="advanceHint" class="hint-text"></div>
                    </div>

                    <div class="grid-2">
                        <div class="form-group">
                            <label><i class="fa-solid fa-user-gear"></i> Assigned Tailor</label>
                            <select id="employeeSelect"></select>
                        </div>
                        <div class="form-group">
                            <label><i class="fa-solid fa-scissors"></i> Stitch Charge</label>
                            <input type="number" id="stitchCharge" required placeholder="0">
                        </div>
                    </div>

                    <button type="button" class="btn" onclick="saveOrder()"><i class="fa-solid fa-floppy-disk"></i> Save Order</button>
                </form>
            </div>

            <!-- Add Employee -->
            <div class="card">
                <div class="card-header">
                    <span><i class="fa-solid fa-user-plus"></i> Add Tailor</span>
                </div>
                <div class="grid-2">
                    <input type="text" id="newEmpName" placeholder="Employee Name">
                    <input type="tel" id="newEmpPhone" placeholder="WhatsApp Number">
                </div>
                <button type="button" class="btn" style="background:var(--accent-blue); color:white;" onclick="addEmployee()"><i class="fa-solid fa-plus"></i> Add Employee</button>
            </div>
        </div>

        <!-- 3. ORDERS LIST PAGE -->
        <div id="page-orders" class="page">
            <div class="card-header">
                <span><i class="fa-solid fa-spinner"></i> Active Processing Orders</span>
            </div>
            <div id="active-orders-list"></div>
        </div>

        <!-- 4. COMPLETED ORDERS PAGE -->
        <div id="page-completed" class="page">
            <div class="card-header">
                <span><i class="fa-solid fa-circle-check" style="color:var(--accent-green)"></i> Completed History</span>
            </div>
            <div id="completed-orders-list"></div>
        </div>

        <!-- 5. REPORTS PAGE -->
        <div id="page-reports" class="page">
            <div class="card">
                <div class="card-header">
                    <span><i class="fa-solid fa-calendar-days"></i> Monthly Analytics</span>
                </div>
                <div class="form-group">
                    <label>Select Month</label>
                    <input type="month" id="reportMonth" onchange="generateReport()">
                </div>
                <div class="grid-2" style="margin-top: 15px;">
                    <div>
                        <small>Total Orders</small>
                        <div class="stat-val" id="rep-orders">0</div>
                    </div>
                    <div>
                        <small>Total Revenue</small>
                        <div class="stat-val blue" id="rep-revenue">₹0</div>
                    </div>
                </div>
                <div class="grid-2" style="margin-top: 15px;">
                    <div>
                        <small>Net Profit</small>
                        <div class="stat-val green" id="rep-profit">₹0</div>
                    </div>
                    <div>
                        <small>Tailor Pay</small>
                        <div class="stat-val" id="rep-stitch">₹0</div>
                    </div>
                </div>
            </div>
        </div>

    </div>

    <!-- CUSTOMER DETAILS POPUP MODAL -->
    <div id="customerModal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">&times;</span>
            <h3 id="modalCustName" style="color:var(--accent-green); margin-bottom: 5px;">Customer Details</h3>
            <p id="modalCustPhone" style="font-size: 0.85rem; color:var(--text-sub); margin-bottom: 15px;"></p>
            <h4 style="font-size:0.9rem; margin-bottom:10px;">Purchase History:</h4>
            <div id="modalOrderList"></div>
        </div>
    </div>

    <!-- Bottom Navigation Bar -->
    <div class="bottom-nav">
        <div class="nav-item active" onclick="switchPage('dashboard')">
            <i class="fa-solid fa-house"></i>
            <span>Home</span>
        </div>
        <div class="nav-item" onclick="switchPage('add-order')">
            <i class="fa-solid fa-plus"></i>
            <span>Add</span>
        </div>
        <div class="nav-item" onclick="switchPage('orders')">
            <i class="fa-solid fa-list-check"></i>
            <span>Orders</span>
        </div>
        <div class="nav-item" onclick="switchPage('completed')">
            <i class="fa-solid fa-users"></i>
            <span>History</span>
        </div>
        <div class="nav-item" onclick="switchPage('reports')">
            <i class="fa-solid fa-chart-pie"></i>
            <span>Reports</span>
        </div>
    </div>

    <script>
        let employees = JSON.parse(localStorage.getItem('kaiz_employees')) || [
            { name: "umma", phone: "8943887325" },
            { name: "ani mol", phone: "+91 99955 49582" },
            { name: "meema (v)", phone: "97450 81002" },
            { name: "nusrah", phone: "+91 75107 02526" }
        ];

        let orders = JSON.parse(localStorage.getItem('kaiz_orders')) || [];
        const OWNER_FIXED_CUT = 300;

        document.addEventListener("DOMContentLoaded", () => {
            populateEmployeeDropdown();
            renderDashboard();
            renderOrders();
            renderCompletedOrders();
        });

        function switchPage(pageId) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            
            document.getElementById(`page-${pageId}`).classList.add('active');
            
            if(pageId === 'dashboard') renderDashboard();
            if(pageId === 'orders') renderOrders();
            if(pageId === 'completed') renderCompletedOrders();
        }

        function calculateAdvance() {
            const price = parseFloat(document.getElementById('orderPrice').value) || 0;
            document.getElementById('advancePaid').value = price / 2;
            calculateAdvanceHint();
        }

        function calculateAdvanceHint() {
            const advance = parseFloat(document.getElementById('advancePaid').value) || 0;
            const cost = parseFloat(document.getElementById('materialCost').value) || 0;
            const hintDiv = document.getElementById('advanceHint');

            if(cost > 0) {
                const balanceAdv = advance - cost;
                hintDiv.innerText = `Remaining Advance Balance: ₹${balanceAdv}`;
            } else {
                hintDiv.innerText = '';
            }
        }

        function addEmployee() {
            const name = document.getElementById('newEmpName').value.trim();
            const phone = document.getElementById('newEmpPhone').value.trim();

            if (!name || !phone) return alert("Fill employee name and phone number");

            employees.push({ name, phone });
            localStorage.setItem('kaiz_employees', JSON.stringify(employees));
            populateEmployeeDropdown();

            document.getElementById('newEmpName').value = '';
            document.getElementById('newEmpPhone').value = '';
            alert("Employee added successfully!");
        }

        function populateEmployeeDropdown() {
            const select = document.getElementById('employeeSelect');
            select.innerHTML = '';
            employees.forEach(e => {
                select.innerHTML += `<option value="${e.name}">${e.name}</option>`;
            });
        }

        function saveOrder() {
            const editId = document.getElementById('editOrderId').value;
            const name = document.getElementById('custName').value.trim();
            const phone = document.getElementById('custPhone').value.trim();
            const category = document.getElementById('itemCategory').value;
            const price = parseFloat(document.getElementById('orderPrice').value) || 0;
            const advance = parseFloat(document.getElementById('advancePaid').value) || 0;
            const cost = parseFloat(document.getElementById('materialCost').value) || 0;
            const employee = document.getElementById('employeeSelect').value;
            const stitch = parseFloat(document.getElementById('stitchCharge').value) || 0;
            const date = document.getElementById('deliveryDate').value;

            if(!name || !phone || !price || !date) return alert("Fill required fields!");

            const calculatedProfit = price - cost - stitch - OWNER_FIXED_CUT;

            if (editId) {
                const idx = orders.findIndex(o => o.id == editId);
                if (idx !== -1) {
                    orders[idx] = { ...orders[idx], name, phone, category, price, advance, cost, employee, stitch, date, profit: calculatedProfit };
                }
            } else {
                const newOrder = {
                    id: Date.now(),
                    name, phone, category, price, advance, cost, employee, stitch, date,
                    profit: calculatedProfit,
                    step: 1, // 1: Adv Paid, 2: Fully Paid, 3: Completed
                    status: 'active'
                };
                orders.push(newOrder);
            }

            localStorage.setItem('kaiz_orders', JSON.stringify(orders));
            document.getElementById('orderForm').reset();
            document.getElementById('editOrderId').value = '';
            alert("Order saved successfully!");
            switchPage('orders');
        }

        function editOrder(id) {
            const order = orders.find(o => o.id === id);
            if (!order || order.step === 3) return alert("Cannot edit finished orders!");

            document.getElementById('editOrderId').value = order.id;
            document.getElementById('custName').value = order.name;
            document.getElementById('custPhone').value = order.phone;
            document.getElementById('itemCategory').value = order.category || 'Ledi Wear';
            document.getElementById('orderPrice').value = order.price;
            document.getElementById('advancePaid').value = order.advance;
            document.getElementById('materialCost').value = order.cost;
            document.getElementById('employeeSelect').value = order.employee;
            document.getElementById('stitchCharge').value = order.stitch;
            document.getElementById('deliveryDate').value = order.date;

            switchPage('add-order');
        }

        function renderDashboard() {
            let totalRev = 0, totalProfit = 0, ownerAmt = 0, stitchAmt = 0;
            let lediRev = 0, lediCount = 0, bebiRev = 0, bebiCount = 0;

            const activeOrders = orders.filter(o => o.status === 'active');

            orders.forEach(o => {
                if(o.step >= 2) {
                    totalRev += o.price;
                    totalProfit += o.profit;
                    ownerAmt += OWNER_FIXED_CUT;
                    stitchAmt += o.stitch;

                    if(o.category === 'Ledi Wear') { lediRev += o.price; lediCount++; }
                    else { bebiRev += o.price; bebiCount++; }
                }
            });

            document.getElementById('dash-revenue').innerText = `₹${totalRev}`;
            document.getElementById('dash-profit').innerText = `₹${totalProfit}`;
            document.getElementById('dash-owner').innerText = `₹${ownerAmt}`;
            document.getElementById('dash-stitch').innerText = `₹${stitchAmt}`;

            document.getElementById('dash-ledi-rev').innerText = `₹${lediRev}`;
            document.getElementById('dash-ledi-count').innerText = `${lediCount} Orders`;
            document.getElementById('dash-bebi-rev').innerText = `₹${bebiRev}`;
            document.getElementById('dash-bebi-count').innerText = `${bebiCount} Orders`;

            // Employee Summary
            const empContainer = document.getElementById('employee-summary-list');
            empContainer.innerHTML = '';
            
            employees.forEach(emp => {
                const empOrders = activeOrders.filter(o => o.employee === emp.name);
                const pendingStitch = empOrders.reduce((sum, o) => sum + o.stitch, 0);
                
                empContainer.innerHTML += `
                    <div style="display:flex; justify-content:space-between; margin-bottom:8px; font-size:0.85rem;">
                        <span><i class="fa-solid fa-user-ninja"></i> ${emp.name} (${empOrders.length} active)</span>
                        <span style="color:var(--accent-green)">Pending: ₹${pendingStitch}</span>
                    </div>
                `;
            });

            // Next Delivery
            const sortedDeliveries = activeOrders.sort((a,b) => new Date(a.date) - new Date(b.date));
            const nextDel = document.getElementById('next-delivery-info');
            if(sortedDeliveries.length > 0) {
                const topOrder = sortedDeliveries[0];
                nextDel.innerHTML = `<i class="fa-solid fa-user"></i> <b>${topOrder.name}</b> (${topOrder.category || 'Order'}) - <i class="fa-solid fa-calendar"></i> ${topOrder.date} <br><small style="color:var(--accent-green)">Click to view active orders</small>`;
                nextDel.onclick = () => switchPage('orders');
            } else {
                nextDel.innerText = "No pending deliveries";
                nextDel.onclick = null;
            }
        }

        function renderOrders() {
            const list = document.getElementById('active-orders-list');
            list.innerHTML = '';

            const activeOrders = orders.filter(o => o.status === 'active');

            if(activeOrders.length === 0) {
                list.innerHTML = `<div style="color:var(--text-sub); text-align:center;">No active orders</div>`;
                return;
            }

            activeOrders.forEach(o => {
                let buttonHtml = '';
                if(o.step === 1) {
                    buttonHtml = `<button class="btn-status" style="background:var(--accent-blue); color:white;" onclick="advanceStatus(${o.id})"><i class="fa-solid fa-money-check-dollar"></i> Mark Fully Paid</button>`;
                } else if(o.step === 2) {
                    buttonHtml = `<button class="btn-status" style="background:var(--accent-purple); color:white;" onclick="advanceStatus(${o.id})"><i class="fa-solid fa-check"></i> Pay Stitch & Complete</button>`;
                }

                list.innerHTML += `
                    <div class="order-item">
                        <div class="order-header">
                            <span>${o.name} <small class="badge" style="color:var(--accent-pink)">${o.category || 'Ledi Wear'}</small></span>
                            <span class="badge"><i class="fa-solid fa-user-gear"></i> ${o.employee}</span>
                        </div>
                        <div style="font-size:0.85rem; color:var(--text-sub); margin-bottom:8px;">
                            <div>Total: ₹${o.price} | Profit: ₹${o.profit}</div>
                            <div>Delivery: ${o.date}</div>
                            ${o.step === 1 && o.cost > 0 ? `<div style="color:#eab308">Adv Bal: ₹${o.advance - o.cost}</div>` : ''}
                        </div>
                        <div style="display:flex; justify-content:space-between; align-items:center;">
                            ${buttonHtml}
                            ${o.step !== 3 ? `<button style="background:none; border:none; color:var(--accent-blue); cursor:pointer;" onclick="editOrder(${o.id})"><i class="fa-solid fa-pen-to-square"></i> Edit</button>` : ''}
                        </div>
                    </div>
                `;
            });
        }

        function advanceStatus(id) {
            const order = orders.find(o => o.id === id);
            
            if(order.step === 1) {
                order.step = 2; // Mark Full Paid
            } else if(order.step === 2) {
                order.step = 3; // Finished & Move to completed
                order.status = 'completed';
            }

            localStorage.setItem('kaiz_orders', JSON.stringify(orders));
            renderOrders();
        }

        function renderCompletedOrders() {
            const list = document.getElementById('completed-orders-list');
            list.innerHTML = '';

            const completed = orders.filter(o => o.status === 'completed');

            const customerMap = {};
            completed.forEach(o => {
                if(!customerMap[o.name]) {
                    customerMap[o.name] = { name: o.name, phone: o.phone, orders: [] };
                }
                customerMap[o.name].orders.push(o);
            });

            if(Object.keys(customerMap).length === 0) {
                list.innerHTML = `<div style="color:var(--text-sub); text-align:center;">No completed orders</div>`;
                return;
            }

            Object.values(customerMap).forEach(cust => {
                list.innerHTML += `
                    <div class="order-item" style="border-left-color: var(--accent-green); cursor:pointer;" onclick="showCustomerDetails('${cust.name}')">
                        <div class="order-header">
                            <span>${cust.name}</span>
                            <span style="color:var(--accent-green)"><i class="fa-solid fa-box-archive"></i> Orders: ${cust.orders.length}</span>
                        </div>
                        <div style="font-size:0.85rem; color:var(--text-sub);">
                            <div>Phone: ${cust.phone}</div>
                            <small style="color:var(--accent-blue)">Click to view purchase details</small>
                        </div>
                    </div>
                `;
            });
        }

        function showCustomerDetails(custName) {
            const custOrders = orders.filter(o => o.name === custName);
            if(custOrders.length === 0) return;

            document.getElementById('modalCustName').innerText = custName;
            document.getElementById('modalCustPhone').innerText = `Phone: ${custOrders[0].phone}`;

            const modalList = document.getElementById('modalOrderList');
            modalList.innerHTML = '';

            custOrders.forEach((o, index) => {
                modalList.innerHTML += `
                    <div style="background:#0f172a; padding:10px; border-radius:6px; margin-bottom:8px; border:1px solid var(--card-border);">
                        <div style="display:flex; justify-content:space-between; font-weight:bold; font-size:0.85rem;">
                            <span>Order #${index+1} (${o.category || 'Item'})</span>
                            <span style="color:${o.status==='completed'?'var(--accent-green)':'#eab308'}">${o.status.toUpperCase()}</span>
                        </div>
                        <div style="font-size:0.8rem; color:var(--text-sub); margin-top:4px;">
                            <div>Amount: ₹${o.price} | Date: ${o.date}</div>
                            <div>Tailor: ${o.employee}</div>
                        </div>
                    </div>
                `;
            });

            document.getElementById('customerModal').style.display = 'flex';
        }

        function closeModal() {
            document.getElementById('customerModal').style.display = 'none';
        }

        function generateReport() {
            const selectedMonth = document.getElementById('reportMonth').value;
            if(!selectedMonth) return;

            let count = 0, revenue = 0, profit = 0, stitch = 0;

            orders.forEach(o => {
                if(o.date.startsWith(selectedMonth)) {
                    count++;
                    if(o.step >= 2) {
                        revenue += o.price;
                        profit += o.profit;
                        stitch += o.stitch;
                    }
                }
            });

            document.getElementById('rep-orders').innerText = count;
            document.getElementById('rep-revenue').innerText = `₹${revenue}`;
            document.getElementById('rep-profit').innerText = `₹${profit}`;
            document.getElementById('rep-stitch').innerText = `₹${stitch}`;
        }
    </script>
</body>
</html>
