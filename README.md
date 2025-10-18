<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>三国杀主公随机选将</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            padding: 30px;
            margin-top: 20px;
        }
        
        h1 {
            text-align: center;
            color: #c62828;
            margin-bottom: 20px;
            font-size: 2.2rem;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }
        
        .description {
            text-align: center;
            margin-bottom: 30px;
            color: #555;
            line-height: 1.6;
        }
        
        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }
        
        button {
            background: #c62828;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 50px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        button:hover {
            background: #b71c1c;
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }
        
        .results {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .faction-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            border: 2px solid transparent;
            transition: all 0.3s ease;
        }
        
        .faction-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
        }
        
        .faction-card.wei {
            border-color: #1e88e5;
        }
        
        .faction-card.shu {
            border-color: #4caf50;
        }
        
        .faction-card.wu {
            border-color: #ff9800;
        }
        
        .faction-card.qun {
            border-color: #9c27b0;
        }
        
        .faction-card.jin {
            border-color: #795548;
        }
        
        .faction-name {
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 10px;
            color: #333;
        }
        
        .lord-name {
            font-size: 1.5rem;
            font-weight: bold;
            color: #c62828;
            margin: 10px 0;
            min-height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .faction-card.wei .faction-name {
            color: #1e88e5;
        }
        
        .faction-card.shu .faction-name {
            color: #4caf50;
        }
        
        .faction-card.wu .faction-name {
            color: #ff9800;
        }
        
        .faction-card.qun .faction-name {
            color: #9c27b0;
        }
        
        .faction-card.jin .faction-name {
            color: #795548;
        }
        
        .faction-generals {
            font-size: 0.85rem;
            color: #666;
            margin-top: 10px;
            line-height: 1.4;
        }
        
        .history {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #eee;
        }
        
        .history h2 {
            text-align: center;
            margin-bottom: 15px;
            color: #555;
        }
        
        .history-list {
            max-height: 200px;
            overflow-y: auto;
            padding: 10px;
            background: #f9f9f9;
            border-radius: 8px;
        }
        
        .history-item {
            padding: 8px 12px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
        }
        
        .history-item:last-child {
            border-bottom: none;
        }
        
        .faction-tag {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 20px;
            font-size: 0.8rem;
            color: white;
            margin-right: 8px;
        }
        
        .faction-tag.wei {
            background: #1e88e5;
        }
        
        .faction-tag.shu {
            background: #4caf50;
        }
        
        .faction-tag.wu {
            background: #ff9800;
        }
        
        .faction-tag.qun {
            background: #9c27b0;
        }
        
        .faction-tag.jin {
            background: #795548;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 15px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .results {
                grid-template-columns: 1fr;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
            
            button {
                width: 100%;
                max-width: 250px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>三国杀主公随机选将</h1>
        <p class="description">从魏、蜀、吴、群、晋五个势力中各随机选择一名主公武将</p>
        
        <div class="controls">
            <button id="selectLords">随机选将</button>
            <button id="rerollWei">重选魏</button>
            <button id="rerollShu">重选蜀</button>
            <button id="rerollWu">重选吴</button>
            <button id="rerollQun">重选群</button>
            <button id="rerollJin">重选晋</button>
        </div>
        
        <div class="results">
            <div class="faction-card wei">
                <div class="faction-name">魏势力</div>
                <div class="lord-name" id="weiLord">-</div>
                <div class="faction-generals">可选: 曹操, 曹丕, 曹叡</div>
            </div>
            
            <div class="faction-card shu">
                <div class="faction-name">蜀势力</div>
                <div class="lord-name" id="shuLord">-</div>
                <div class="faction-generals">可选: 刘备, 刘禅, 刘谌</div>
            </div>
            
            <div class="faction-card wu">
                <div class="faction-name">吴势力</div>
                <div class="lord-name" id="wuLord">-</div>
                <div class="faction-generals">可选: 孙权, 孙亮, 孙休, 孙皓, 孙策</div>
            </div>
            
            <div class="faction-card qun">
                <div class="faction-name">群势力</div>
                <div class="lord-name" id="qunLord">-</div>
                <div class="faction-generals">可选: 董卓, 袁绍, 张角, 刘辩</div>
            </div>
            
            <div class="faction-card jin">
                <div class="faction-name">晋势力</div>
                <div class="lord-name" id="jinLord">-</div>
                <div class="faction-generals">可选: 司马炎, 司马师, 司马昭</div>
            </div>
        </div>
        
        <div class="history">
            <h2>选将历史</h2>
            <div class="history-list" id="historyList">
                <!-- 历史记录将在这里显示 -->
            </div>
        </div>
    </div>

    <script>
        // 主公武将库（已根据要求更新）
        const lordGenerals = {
            "wei": ["曹操", "曹丕", "曹叡"],
            "shu": ["刘备", "刘禅", "刘谌"],
            "wu": ["孙权", "孙亮", "孙休", "孙皓", "孙策"],
            "qun": ["董卓", "袁绍", "张角", "刘辩"],
            "jin": ["司马炎", "司马师", "司马昭"]
        };

        // 当前选中的主公
        let currentLords = {
            wei: "",
            shu: "",
            wu: "",
            qun: "",
            jin: ""
        };

        // 选将历史
        let selectionHistory = [];

        // 随机选择一名武将
        function selectRandomLord(faction) {
            const generals = lordGenerals[faction];
            let selectedLord;
            
            // 确保不会重复选择相同的武将（除非只有一个可选）
            do {
                selectedLord = generals[Math.floor(Math.random() * generals.length)];
            } while (generals.length > 1 && selectedLord === currentLords[faction]);
            
            return selectedLord;
        }

        // 更新显示
        function updateDisplay() {
            document.getElementById('weiLord').textContent = currentLords.wei || '-';
            document.getElementById('shuLord').textContent = currentLords.shu || '-';
            document.getElementById('wuLord').textContent = currentLords.wu || '-';
            document.getElementById('qunLord').textContent = currentLords.qun || '-';
            document.getElementById('jinLord').textContent = currentLords.jin || '-';
        }

        // 从所有势力中选择主公
        function selectAllLords() {
            currentLords.wei = selectRandomLord('wei');
            currentLords.shu = selectRandomLord('shu');
            currentLords.wu = selectRandomLord('wu');
            currentLords.qun = selectRandomLord('qun');
            currentLords.jin = selectRandomLord('jin');
            
            updateDisplay();
            addToHistory();
        }

        // 重选特定势力
        function rerollFaction(faction) {
            currentLords[faction] = selectRandomLord(faction);
            updateDisplay();
            addToHistory();
        }

        // 添加到历史记录
        function addToHistory() {
            const timestamp = new Date().toLocaleTimeString();
            const historyItem = {
                time: timestamp,
                wei: currentLords.wei,
                shu: currentLords.shu,
                wu: currentLords.wu,
                qun: currentLords.qun,
                jin: currentLords.jin
            };
            
            selectionHistory.unshift(historyItem);
            
            // 只保留最近10条记录
            if (selectionHistory.length > 10) {
                selectionHistory = selectionHistory.slice(0, 10);
            }
            
            updateHistoryDisplay();
        }

        // 更新历史记录显示
        function updateHistoryDisplay() {
            const historyList = document.getElementById('historyList');
            historyList.innerHTML = '';
            
            selectionHistory.forEach(item => {
                const historyItem = document.createElement('div');
                historyItem.className = 'history-item';
                
                const timeSpan = document.createElement('span');
                timeSpan.textContent = item.time;
                
                const lordsSpan = document.createElement('span');
                lordsSpan.innerHTML = `
                    <span class="faction-tag wei">魏:${item.wei}</span>
                    <span class="faction-tag shu">蜀:${item.shu}</span>
                    <span class="faction-tag wu">吴:${item.wu}</span>
                    <span class="faction-tag qun">群:${item.qun}</span>
                    <span class="faction-tag jin">晋:${item.jin}</span>
                `;
                
                historyItem.appendChild(timeSpan);
                historyItem.appendChild(lordsSpan);
                historyList.appendChild(historyItem);
            });
        }

        // 绑定按钮事件
        document.getElementById('selectLords').addEventListener('click', selectAllLords);
        document.getElementById('rerollWei').addEventListener('click', () => rerollFaction('wei'));
        document.getElementById('rerollShu').addEventListener('click', () => rerollFaction('shu'));
        document.getElementById('rerollWu').addEventListener('click', () => rerollFaction('wu'));
        document.getElementById('rerollQun').addEventListener('click', () => rerollFaction('qun'));
        document.getElementById('rerollJin').addEventListener('click', () => rerollFaction('jin'));

        // 初始化显示
        updateDisplay();
    </script>
</body>
</html>
