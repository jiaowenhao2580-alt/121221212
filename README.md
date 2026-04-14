# 121221212
121212
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>加密货币合约交易复盘系统</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft Yahei', sans-serif;
        }

        body {
            background-color: #f5f7fa;
            padding: 20px;
        }

        .auth-box {
            max-width: 450px;
            margin: 80px auto;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 15px rgba(0,0,0,0.1);
        }

        .tab-group {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
        }

        .tab {
            flex: 1;
            padding: 10px;
            text-align: center;
            border-radius: 5px;
            cursor: pointer;
            border: 1px solid #eee;
        }

        .tab.active {
            background: #2563eb;
            color: white;
            border-color: #2563eb;
        }

        .form-item {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }

        input, select, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
        }

        .btn {
            width: 100%;
            padding: 12px;
            background: #2563eb;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }

        .btn:hover {
            background: #1d4ed8;
        }

        .form-hide {
            display: none;
        }

        .container {
            max-width: 1600px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 15px rgba(0,0,0,0.1);
        }

        .user-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            background: #f0f7ff;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        .logout-btn {
            padding: 8px 15px;
            background: #ef4444;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        h1 {
            text-align: center;
            margin-bottom: 20px;
            color: #333;
            font-size: 24px;
        }

        .stats-panel {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: #f8fafc;
            padding: 20px;
            border-radius: 8px;
            border-left: 4px solid #2563eb;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        .stat-title {
            font-size: 14px;
            color: #64748b;
            margin-bottom: 8px;
        }

        .stat-value {
            font-size: 22px;
            font-weight: bold;
            color: #1e293b;
        }

        .profit {
            color: #10b981;
        }

        .loss {
            color: #ef4444;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        textarea {
            min-height: 80px;
            resize: vertical;
        }

        .btn-group {
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        .reset-btn {
            background: #6b7280;
        }

        .calc-btn {
            background: #10b981;
        }

        .table-box {
            overflow-x: auto;
            margin-top: 30px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 13px;
        }

        th, td {
            padding: 10px;
            text-align: left;
            border-bottom: 1px solid #eee;
            white-space: nowrap;
        }

        th {
            background: #2563eb;
            color: white;
            position: sticky;
            top: 0;
        }

        tr:hover {
            background: #f9f9f9;
        }

        .action-group {
            display: flex;
            gap: 6px;
        }

        .edit-btn {
            padding: 5px 8px;
            background: #f59e0b;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 12px;
        }

        .del-btn {
            padding: 5px 8px;
            background: #ef4444;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 12px;
        }

        .empty {
            text-align: center;
            padding: 40px;
            color: #999;
        }

        .profit-positive {
            color: #10b981;
            font-weight: 600;
        }

        .profit-negative {
            color: #ef4444;
            font-weight: 600;
        }
    </style>
</head>
<body>

<div id="authPage">
    <div class="auth-box">
        <div class="tab-group">
            <div class="tab active" onclick="switchTab('login')">登录</div>
            <div class="tab active" onclick="switchTab('register')">注册</div>
        </div>

        <div id="loginForm">
            <div class="form-item">
                <label>邮箱</label>
                <input type="email" id="loginEmail" placeholder="请输入登录邮箱">
            </div>
            <div class="form-item">
                <label>密码</label>
                <input type="password" id="loginPwd" placeholder="请输入密码（≥6位）">
            </div>
            <button class="btn" onclick="login()">登录</button>
        </div>

        <div id="registerForm" class="form-hide">
            <div class="form-item">
                <label>邮箱</label>
                <input type="email" id="regEmail" placeholder="请输入注册邮箱">
            </div>
            <div class="form-item">
                <label>密码</label>
                <input type="password" id="regPwd" placeholder="请设置密码（≥6位）">
            </div>
            <button class="btn" onclick="register()">注册</button>
        </div>
    </div>
</div>

<div id="mainPage" style="display: none;">
    <div class="container">
        <div class="user-bar">
            <div>当前用户：<span id="userEmail"></span></div>
            <button class="logout-btn" onclick="logout()">退出登录</button>
        </div>

        <h1>加密货币合约交易复盘系统</h1>

        <div class="stats-panel" id="statsPanel">
            <div class="stat-card">
                <div class="stat-title">总交易次数</div>
                <div class="stat-value" id="totalTrades">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">盈利次数</div>
                <div class="stat-value profit" id="winTrades">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">亏损次数</div>
                <div class="stat-value loss" id="lossTrades">0</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">交易胜率</div>
                <div class="stat-value" id="winRate">0%</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">净总收益率</div>
                <div class="stat-value" id="netProfit">0.00%</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">最大单笔盈利</div>
                <div class="stat-value profit" id="maxProfit">0.00%</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">最大单笔亏损</div>
                <div class="stat-value loss" id="maxLoss">0.00%</div>
            </div>
            <div class="stat-card">
                <div class="stat-title">平均盈亏</div>
                <div class="stat-value" id="avgProfit">0.00%</div>
            </div>
        </div>

        <form id="recordForm">
            <input type="hidden" id="docId">
            <div class="form-grid">
                <div class="form-item">
                    <label>交易币种</label>
                    <select id="coinType" required>
                        <option value="">请选择</option>
                        <option value="BTC">BTC</option>
                        <option value="ETH">ETH</option>
                        <option value="SOL">SOL</option>
                        <option value="BNB">BNB</option>
                        <option value="XRP">XRP</option>
                        <option value="其他">其他</option>
                    </select>
                </div>
                <div class="form-item">
                    <label>开仓时间</label>
                    <input type="datetime-local" id="openTime" required>
                </div>
                <div class="form-item">
                    <label>开仓价格</label>
                    <input type="number" step="0.00001" id="openPrice" required placeholder="开仓价">
                </div>
                <div class="form-item">
                    <label>开仓方向</label>
                    <select id="direction" required>
                        <option value="">请选择</option>
                        <option value="做多">做多</option>
                        <option value="做空">做空</option>
                    </select>
                </div>
                <div class="form-item">
                    <label>K线形态</label>
                    <input type="text" id="kline" placeholder="如：日线金叉、锤子线">
                </div>
                <div class="form-item">
                    <label>影响新闻/消息</label>
                    <input type="text" id="news" placeholder="利好/利空/政策">
                </div>
                <div class="form-item">
                    <label>成交量情况</label>
                    <input type="text" id="volume" placeholder="放量/缩量/巨量">
                </div>
                <div class="form-item">
                    <label>止盈价格</label>
                    <input type="number" step="0.00001" id="takeProfit" placeholder="止盈价">
                </div>
                <div class="form-item">
                    <label>止损价格</label>
                    <input type="number" step="0.00001" id="stopLoss" placeholder="止损价">
                </div>
                <div class="form-item">
                    <label>盈利百分比 (%)</label>
                    <input type="number" step="0.01" id="profitRate" placeholder="自动计算/手动填写">
                </div>
                <div class="form-item">
                    <label>开仓结果</label>
                    <select id="openResult" required>
                        <option value="">请选择</option>
                        <option value="盈利">盈利</option>
                        <option value="亏损">亏损</option>
                        <option value="平本">平本</option>
                        <option value="持仓中">持仓中</option>
                    </select>
                </div>
                <div class="form-item">
                    <label>开仓心得</label>
                    <textarea id="openExperience" placeholder="开仓判断依据、心态"></textarea>
                </div>
                <div class="form-item">
                    <label>复盘总结</label>
                    <textarea id="review" placeholder="交易反思、改进点"></textarea>
                </div>
                <div class="form-item" style="grid-column: 1/-1;">
                    <label>备注（杠杆/交易所/持仓状态）</label>
                    <textarea id="remark" placeholder="如：10倍杠杆、币安、已平仓"></textarea>
                </div>
            </div>
            <div class="btn-group">
                <button type="button" class="btn calc-btn" onclick="autoCalculateProfit()">自动计算盈利</button>
                <button type="submit" class="btn">提交记录</button>
                <button type="reset" class="btn reset-btn">重置表单</button>
            </div>
        </form>

        <div class="table-box">
            <table>
                <thead>
                    <tr>
                        <th>序号</th>
                        <th>币种</th>
                        <th>开仓时间</th>
                        <th>开仓价</th>
                        <th>方向</th>
                        <th>K线形态</th>
                        <th>新闻影响</th>
                        <th>成交量</th>
                        <th>止盈价</th>
                        <th>止损价</th>
                        <th>盈利率%</th>
                        <th>结果</th>
                        <th>开仓心得</th>
                        <th>复盘</th>
                        <th>备注</th>
                        <th>操作</th>
                    </tr>
                </thead>
                <tbody id="tableBody"></tbody>
            </table>
        </div>
    </div>
</div>

<!-- 已完整嵌入你提供的 Firebase 配置 -->
<script type="module">
// Import the functions you need from the SDKs you need
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getAnalytics } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-analytics.js";
// 补充项目必需的登录/数据库SDK
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
import { getFirestore, collection, addDoc, getDocs, doc, updateDoc, deleteDoc, query, where, getDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyAFJaBrPzeD5XA29CEH84zCWacyNoDs5Ek",
  authDomain: "ethusdt-cc310.firebaseapp.com",
  projectId: "ethusdt-cc310",
  storageBucket: "ethusdt-cc310.firebasestorage.app",
  messagingSenderId: "814698911170",
  appId: "1:814698911170:web:530a663f87fe3815f5725b",
  measurementId: "G-EG23E9B8K0"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const analytics = getAnalytics(app);

// 初始化项目服务
const auth = getAuth(app);
const db = getFirestore(app);

let currentUser = null;
let allRecords = [];

window.switchTab = function(type) {
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    event.target.classList.add('active');
    document.getElementById('loginForm').classList.add('form-hide');
    document.getElementById('registerForm').classList.add('form-hide');
    document.getElementById(type+'Form').classList.remove('form-hide');
}

window.register = async function() {
    const email = document.getElementById('regEmail').value.trim();
    const password = document.getElementById('regPwd').value.trim();
    if(!email || !password){ alert('请填写完整信息！'); return; }
    try {
        await createUserWithEmailAndPassword(auth, email, password);
        alert('注册成功！请登录');
        switchTab('login');
    } catch(e) {
        alert('注册失败：' + e.message);
    }
}

window.login = async function() {
    const email = document.getElementById('loginEmail').value.trim();
    const password = document.getElementById('loginPwd').value.trim();
    if(!email || !password){ alert('请填写完整信息！'); return; }
    try {
        await signInWithEmailAndPassword(auth, email, password);
        alert('登录成功！');
    } catch(e) {
        alert('登录失败：' + e.message);
    }
}

window.logout = async function() {
    await signOut(auth);
    alert('已退出登录');
}

onAuthStateChanged(auth, (user) => {
    if (user) {
        currentUser = user;
        document.getElementById('authPage').style.display = 'none';
        document.getElementById('mainPage').style.display = 'block';
        document.getElementById('userEmail').innerText = user.email;
        loadRecords();
    } else {
        currentUser = null;
        document.getElementById('authPage').style.display = 'block';
        document.getElementById('mainPage').style.display = 'none';
    }
});

window.autoCalculateProfit = function() {
    const openPrice = parseFloat(document.getElementById('openPrice').value);
    const closePrice = parseFloat(document.getElementById('takeProfit').value) || parseFloat(document.getElementById('stopLoss').value);
    const direction = document.getElementById('direction').value;

    if(!openPrice || !closePrice){
        alert('请填写开仓价和止盈/止损价！');
        return;
    }

    let profitRate;
    if(direction === '做多'){
        profitRate = ((closePrice - openPrice) / openPrice) * 100;
    } else if(direction === '做空'){
        profitRate = ((openPrice - closePrice) / openPrice) * 100;
    } else {
        alert('请选择开仓方向！');
        return;
    }
    document.getElementById('profitRate').value = profitRate.toFixed(2);
}

async function loadRecords() {
    const q = query(collection(db, "contractRecords"), where("uid", "==", currentUser.uid));
    const snap = await getDocs(q);
    allRecords = [];
    snap.forEach(doc => allRecords.push({ id: doc.id, ...doc.data() }));
    allRecords.sort((a,b) => new Date(b.createTime) - new Date(a.createTime));
    renderTable();
    calculateStats();
}

function calculateStats() {
    const closedTrades = allRecords.filter(item => item.openResult !== '持仓中');
    const total = closedTrades.length;
    if(total === 0){
        document.getElementById('totalTrades').textContent = 0;
        document.getElementById('winTrades').textContent = 0;
        document.getElementById('lossTrades').textContent = 0;
        document.getElementById('winRate').textContent = '0%';
        document.getElementById('netProfit').textContent = '0.00%';
        document.getElementById('maxProfit').textContent = '0.00%';
        document.getElementById('maxLoss').textContent = '0.00%';
        document.getElementById('avgProfit').textContent = '0.00%';
        return;
    }

    const winTrades = closedTrades.filter(item => item.openResult === '盈利').length;
    const lossTrades = closedTrades.filter(item => item.openResult === '亏损').length;
    const winRate = total > 0 ? ((winTrades / total) * 100).toFixed(2) : 0;
    const profits = closedTrades.map(item => parseFloat(item.profitRate || 0));
    const netProfit = profits.reduce((a,b)=>a+b,0).toFixed(2);
    const maxProfit = Math.max(...profits).toFixed(2);
    const maxLoss = Math.min(...profits).toFixed(2);
    const avgProfit = (netProfit / total).toFixed(2);

    document.getElementById('totalTrades').textContent = total;
    document.getElementById('winTrades').textContent = winTrades;
    document.getElementById('lossTrades').textContent = lossTrades;
    document.getElementById('winRate').textContent = `${winRate}%`;
    document.getElementById('netProfit').textContent = `${netProfit}%`;
    document.getElementById('maxProfit').textContent = `${maxProfit}%`;
    document.getElementById('maxLoss').textContent = `${maxLoss}%`;
    document.getElementById('avgProfit').textContent = `${avgProfit}%`;
}

function renderTable() {
    const tbody = document.getElementById('tableBody');
    tbody.innerHTML = '';
    if (allRecords.length === 0) {
        tbody.innerHTML = `<tr><td colspan="16" class="empty">暂无开仓记录</td></tr>`;
        return;
    }

    allRecords.forEach((item, index) => {
        const profit = parseFloat(item.profitRate || 0);
        const profitClass = profit > 0 ? 'profit-positive' : profit < 0 ? 'profit-negative' : '';

        tbody.innerHTML += `
        <tr>
            <td>${index+1}</td>
            <td>${item.coinType || '-'}</td>
            <td>${new Date(item.openTime).toLocaleString()}</td>
            <td>${item.openPrice}</td>
            <td>${item.direction}</td>
            <td>${item.kline || '-'}</td>
            <td>${item.news || '-'}</td>
            <td>${item.volume || '-'}</td>
            <td>${item.takeProfit || '-'}</td>
            <td>${item.stopLoss || '-'}</td>
            <td class="${profitClass}">${item.profitRate || '0.00'}</td>
            <td>${item.openResult}</td>
            <td>${item.openExperience || '-'}</td>
            <td>${item.review || '-'}</td>
            <td>${item.remark || '-'}</td>
            <td class="action-group">
                <button class="edit-btn" onclick="editRecord('${item.id}')">编辑</button>
                <button class="del-btn" onclick="deleteRecord('${item.id}')">删除</button>
            </td>
        </tr>`;
    });
}

document.getElementById('recordForm').addEventListener('submit', async (e) => {
    e.preventDefault();
    const id = document.getElementById('docId').value;
    
    const recordData = {
        coinType: document.getElementById('coinType').value,
        openTime: document.getElementById('openTime').value,
        openPrice: document.getElementById('openPrice').value,
        direction: document.getElementById('direction').value,
        kline: document.getElementById('kline').value,
        news: document.getElementById('news').value,
        volume: document.getElementById('volume').value,
        takeProfit: document.getElementById('takeProfit').value,
        stopLoss: document.getElementById('stopLoss').value,
        profitRate: document.getElementById('profitRate').value,
        openResult: document.getElementById('openResult').value,
        openExperience: document.getElementById('openExperience').value,
        review: document.getElementById('review').value,
        remark: document.getElementById('remark').value,
        uid: currentUser.uid,
        createTime: new Date()
    };

    try {
        if(id){
            await updateDoc(doc(db, "contractRecords", id), recordData);
            alert('记录更新成功！');
        } else {
            await addDoc(collection(db, "contractRecords"), recordData);
            alert('记录添加成功！');
        }
        loadRecords();
        document.getElementById('recordForm').reset();
        document.getElementById('docId').value = '';
    } catch(e) {
        alert('操作失败：' + e.message);
    }
});

window.editRecord = async function(id) {
    const docRef = doc(db, "contractRecords", id);
    const docSnap = await getDoc(docRef);
    if(!docSnap.exists()) return;

    const data = docSnap.data();
    document.getElementById('docId').value = id;
    document.getElementById('coinType').value = data.coinType;
    document.getElementById('openTime').value = data.openTime;
    document.getElementById('openPrice').value = data.openPrice;
    document.getElementById('direction').value = data.direction;
    document.getElementById('kline').value = data.kline || '';
    document.getElementById('news').value = data.news || '';
    document.getElementById('volume').value = data.volume || '';
    document.getElementById('takeProfit').value = data.takeProfit || '';
    document.getElementById('stopLoss').value = data.stopLoss || '';
    document.getElementById('profitRate').value = data.profitRate || '';
    document.getElementById('openResult').value = data.openResult;
    document.getElementById('openExperience').value = data.openExperience || '';
    document.getElementById('review').value = data.review || '';
    document.getElementById('remark').value = data.remark || '';
}

window.deleteRecord = async function(id) {
    if(!confirm('确定删除这条记录吗？')) return;
    await deleteDoc(doc(db, "contractRecords", id));
    alert('删除成功！');
    loadRecords();
}
</script>
</body>
</html>
