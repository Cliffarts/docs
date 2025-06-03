<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>📊 Business Stock & Sales Manager</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      padding: 20px;
      color: #333;
    }
    
    .container {
      max-width: 1200px;
      margin: 0 auto;
    }
    
    h1 {
      text-align: center;
      color: white;
      margin-bottom: 30px;
      font-size: 2.5rem;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    }
    
    .section {
      background: rgba(255, 255, 255, 0.95);
      margin-bottom: 20px;
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 8px 32px rgba(0,0,0,0.1);
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 255, 255, 0.2);
    }
    
    .section h2, .section h3 {
      color: #333;
      margin-bottom: 20px;
      padding-bottom: 10px;
      border-bottom: 2px solid #667eea;
    }
    
    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 15px;
      margin-bottom: 20px;
    }
    
    .form-group {
      display: flex;
      flex-direction: column;
    }
    
    label {
      font-weight: 600;
      margin-bottom: 5px;
      color: #555;
    }
    
    input[type="text"],
    input[type="number"],
    input[type="password"],
    input[type="date"],
    select,
    button {
      padding: 12px 15px;
      border: 2px solid #ddd;
      border-radius: 8px;
      font-size: 14px;
      transition: all 0.3s ease;
      background: white;
    }
    
    input:focus, select:focus {
      outline: none;
      border-color: #667eea;
      box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
    }
    
    button {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      border: none;
      cursor: pointer;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      transition: all 0.3s ease;
    }
    
    button:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
    }
    
    .hidden {
      display: none;
    }
    
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      margin: 20px 0;
    }
    
    .stat-card {
      background: linear-gradient(135deg, #4CAF50, #45a049);
      color: white;
      padding: 20px;
      border-radius: 10px;
      text-align: center;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }
    
    .stat-card.profit {
      background: linear-gradient(135deg, #2196F3, #1976D2);
    }
    
    .stat-card.revenue {
      background: linear-gradient(135deg, #FF9800, #F57C00);
    }
    
    .stat-card h4 {
      font-size: 0.9rem;
      opacity: 0.9;
      margin-bottom: 5px;
    }
    
    .stat-card .value {
      font-size: 1.5rem;
      font-weight: bold;
    }
    
    canvas {
      max-width: 100%;
      height: 400px !important;
      border-radius: 10px;
      background: white;
    }
    
    ul {
      list-style-type: none;
      padding: 0;
    }
    
    li {
      background: #f8f9fa;
      margin: 8px 0;
      padding: 15px;
      border-radius: 8px;
      border-left: 4px solid #667eea;
      display: flex;
      justify-content: space-between;
      align-items: center;
      transition: all 0.3s ease;
    }
    
    li:hover {
      transform: translateX(5px);
      background: #e9ecef;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    
    li .item-info {
      flex-grow: 1;
    }
    
    li .item-info strong {
      display: block;
      color: #333;
      margin-bottom: 5px;
    }
    
    li .item-info small {
      color: #666;
    }
    
    .delete-btn {
      background: linear-gradient(135deg, #ff4757, #ff3742) !important;
      padding: 8px 12px !important;
      font-size: 12px !important;
      margin: 0 !important;
      opacity: 0.7;
      transition: all 0.3s ease;
    }
    
    .delete-btn:hover {
      opacity: 1;
      transform: scale(1.05);
    }
    
    .alert {
      padding: 15px;
      margin: 15px 0;
      border-radius: 8px;
      font-weight: 500;
    }
    
    .alert-success {
      background: #d4edda;
      color: #155724;
      border: 1px solid #c3e6cb;
    }
    
    .alert-error {
      background: #f8d7da;
      color: #721c24;
      border: 1px solid #f5c6cb;
    }
    
    .alert-warning {
      background: #fff3cd;
      color: #856404;
      border: 1px solid #ffeaa7;
    }
    
    .low-stock-item {
      border-left-color: #ff9800 !important;
      background: linear-gradient(90deg, #fff3e0, #f8f9fa) !important;
    }
    
    .chart-controls {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }
    
    .loading {
      text-align: center;
      color: #666;
      font-style: italic;
    }
    
    @media (max-width: 768px) {
      .form-grid {
        grid-template-columns: 1fr;
      }
      
      .stats-grid {
        grid-template-columns: 1fr;
      }
      
      h1 {
        font-size: 2rem;
      }
      
      .section {
        padding: 15px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>📊 Business Stock & Sales Manager</h1>

    <!-- Admin Login -->
    <div class="section">
      <h2>🔐 Admin Access</h2>
      <div class="form-grid">
        <div class="form-group">
          <label for="adminPassword">Admin Password:</label>
          <input type="password" id="adminPassword" placeholder="Enter password">
        </div>
        <div class="form-group">
          <button onclick="checkAdminPassword()">Login</button>
        </div>
      </div>
      <div id="loginAlert"></div>
    </div>

    <!-- Stock Management (Admin Only) -->
    <div id="adminSection" class="hidden section">
      <h3>📦 Stock Management</h3>
      <div class="form-grid">
        <div class="form-group">
          <label for="stockItem">Item Name:</label>
          <input type="text" id="stockItem" placeholder="Enter item name">
        </div>
        <div class="form-group">
          <label for="stockCost">Cost Price (KES):</label>
          <input type="number" step="0.01" id="stockCost" placeholder="0.00">
        </div>
        <div class="form-group">
          <label for="stockQuantity">Initial Quantity:</label>
          <input type="number" step="1" id="stockQuantity" placeholder="0" value="1">
        </div>
        <div class="form-group">
          <label for="stockSellingPrice">Suggested Selling Price (KES):</label>
          <input type="number" step="0.01" id="stockSellingPrice" placeholder="0.00">
        </div>
      </div>
      <button onclick="addStock()">Add to Stock</button>
      <div id="stockAlert"></div>
      
      <h4>📋 Current Stock</h4>
      <ul id="stockList"></ul>
    </div>

    <!-- Sales Entry -->
    <div class="section">
      <h3>💰 Sales Entry</h3>
      <div class="form-grid">
        <div class="form-group">
          <label for="saleItemDropdown">Select Item:</label>
          <select id="saleItemDropdown">
            <option value="" disabled selected>Choose an item</option>
          </select>
        </div>
        <div class="form-group">
          <label for="saleQuantity">Quantity:</label>
          <input type="number" step="0.01" id="saleQuantity" placeholder="1" min="0.01">
        </div>
        <div class="form-group">
          <label for="salePrice">Selling Price per item (KES):</label>
          <input type="number" step="0.01" id="salePrice" placeholder="0.00">
        </div>
        <div class="form-group">
          <label for="saleDate">Sale Date:</label>
          <input type="date" id="saleDate">
        </div>
      </div>
      <button onclick="addSale()">Record Sale</button>
      <div id="saleAlert"></div>
    </div>

    <!-- Business Analytics -->
    <div class="section">
      <h3>📈 Business Analytics</h3>
      <div class="stats-grid">
        <div class="stat-card">
          <h4>Today's Sales</h4>
          <div class="value" id="dailyTotal">KES 0.00</div>
        </div>
        <div class="stat-card profit">
          <h4>Today's Profit</h4>
          <div class="value" id="dailyProfit">KES 0.00</div>
        </div>
        <div class="stat-card revenue">
          <h4>Total Revenue</h4>
          <div class="value" id="totalRevenue">KES 0.00</div>
        </div>
        <div class="stat-card">
          <h4>Total Profit</h4>
          <div class="value" id="totalProfit">KES 0.00</div>
        </div>
      </div>
      <div id="lowStockAlert"></div>
    </div>

    <!-- Sales Records -->
    <div class="section">
      <h3>📋 Sales Records</h3>
      <div class="chart-controls">
        <button onclick="showAllSales()">Show All Sales</button>
        <button onclick="showTodaySales()">Today's Sales Only</button>
        <button onclick="exportSales()">Export Sales Data</button>
      </div>
      <ul id="salesList"></ul>
    </div>

    <!-- Sales Chart -->
    <div class="section">
      <h3>📊 Sales Analytics Chart</h3>
      <div class="chart-controls">
        <button onclick="updateChart('daily')">Daily Sales</button>
        <button onclick="updateChart('items')">By Items</button>
        <button onclick="updateChart('profit')">Profit Analysis</button>
      </div>
      <canvas id="salesChart"></canvas>
    </div>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
  <script>
    // In-memory storage (Claude.ai compatible)
    let stock = [
      { item: "Sample Product", cost: 50, quantity: 10, sellingPrice: 80 }
    ];
    let sales = [
      { item: "Sample Product", quantity: 2, price: 80, cost: 50, profit: 60, date: new Date().toISOString().split('T')[0] }
    ];
    
    let salesChartInstance = null;
    let showingAllSales = true;
    
    // Initialize date input to today
    document.getElementById('saleDate').valueAsDate = new Date();

    function showAlert(elementId, message, type = 'success') {
      const element = document.getElementById(elementId);
      element.innerHTML = `<div class="alert alert-${type}">${message}</div>`;
      setTimeout(() => {
        element.innerHTML = '';
      }, 3000);
    }

    function checkAdminPassword() {
      const pwd = document.getElementById('adminPassword').value;
      if (pwd === 'Cliff') {
        document.getElementById('adminSection').classList.remove('hidden');
        showAlert('loginAlert', '✅ Admin access granted successfully!');
        document.getElementById('adminPassword').value = '';
      } else {
        showAlert('loginAlert', '❌ Invalid password. Please try again.', 'error');
      }
    }

    function addStock() {
      const item = document.getElementById('stockItem').value.trim();
      const cost = parseFloat(document.getElementById('stockCost').value);
      const quantity = parseInt(document.getElementById('stockQuantity').value) || 1;
      const sellingPrice = parseFloat(document.getElementById('stockSellingPrice').value) || 0;
      
      if (!item || isNaN(cost) || cost <= 0) {
        showAlert('stockAlert', '❌ Please provide valid item name and cost price.', 'error');
        return;
      }
      
      const existingStock = stock.find(s => s.item.toLowerCase() === item.toLowerCase());
      if (existingStock) {
        existingStock.quantity += quantity;
        existingStock.cost = cost; // Update cost
        if (sellingPrice > 0) existingStock.sellingPrice = sellingPrice;
        showAlert('stockAlert', `✅ Updated ${item} - Added ${quantity} units`);
      } else {
        stock.push({ item, cost, quantity, sellingPrice });
        showAlert('stockAlert', `✅ Added new item: ${item}`);
      }
      
      // Clear form
      document.getElementById('stockItem').value = '';
      document.getElementById('stockCost').value = '';
      document.getElementById('stockQuantity').value = '1';
      document.getElementById('stockSellingPrice').value = '';
      
      updateAll();
    }

    function updateStockList() {
      const ul = document.getElementById('stockList');
      if (stock.length === 0) {
        ul.innerHTML = '<li class="loading">No stock items available</li>';
        return;
      }
      
      ul.innerHTML = '';
      stock.forEach((s, index) => {
        const li = document.createElement('li');
        const isLowStock = s.quantity <= 5;
        if (isLowStock) li.classList.add('low-stock-item');
        
        const itemInfo = document.createElement('div');
        itemInfo.className = 'item-info';
        itemInfo.innerHTML = `
          <strong>${s.item}</strong>
          <small>Stock: ${s.quantity} units | Cost: KES ${s.cost.toFixed(2)} | 
          Suggested Price: KES ${(s.sellingPrice || 0).toFixed(2)} | 
          Margin: ${s.sellingPrice ? (((s.sellingPrice - s.cost) / s.cost) * 100).toFixed(1) : 0}%
          ${isLowStock ? ' ⚠️ LOW STOCK' : ''}</small>
        `;
        li.appendChild(itemInfo);
        
        const delBtn = document.createElement('button');
        delBtn.textContent = 'Delete';
        delBtn.className = 'delete-btn';
        delBtn.onclick = () => deleteStock(index);
        li.appendChild(delBtn);
        
        ul.appendChild(li);
      });
      
      checkLowStock();
    }

    function checkLowStock() {
      const lowStockItems = stock.filter(s => s.quantity <= 5 && s.quantity > 0);
      const outOfStockItems = stock.filter(s => s.quantity === 0);
      
      let alertHtml = '';
      if (outOfStockItems.length > 0) {
        alertHtml += `<div class="alert alert-error">🚨 OUT OF STOCK: ${outOfStockItems.map(s => s.item).join(', ')}</div>`;
      }
      if (lowStockItems.length > 0) {
        alertHtml += `<div class="alert alert-warning">⚠️ LOW STOCK: ${lowStockItems.map(s => `${s.item} (${s.quantity})`).join(', ')}</div>`;
      }
      
      document.getElementById('lowStockAlert').innerHTML = alertHtml;
    }

    function deleteStock(index) {
      const itemToDelete = stock[index].item;
      const hasSales = sales.some(sale => sale.item === itemToDelete);
      
      if (hasSales) {
        if (!confirm(`"${itemToDelete}" has sales records. Deleting will affect your analytics. Continue?`)) {
          return;
        }
      }
      
      if (confirm(`Are you sure you want to delete "${itemToDelete}" from stock?`)) {
        stock.splice(index, 1);
        updateAll();
        showAlert('stockAlert', `✅ Deleted ${itemToDelete} from stock`);
      }
    }

    function updateDropdown() {
      const dropdown = document.getElementById('saleItemDropdown');
      dropdown.innerHTML = '<option value="" disabled selected>Choose an item</option>';
      
      stock.filter(s => s.quantity > 0).forEach(s => {
        const option = document.createElement('option');
        option.value = s.item;
        option.textContent = `${s.item} (${s.quantity} available)`;
        dropdown.appendChild(option);
      });
      
      // Auto-fill selling price when item is selected
      dropdown.onchange = function() {
        const selectedStock = stock.find(s => s.item === this.value);
        if (selectedStock && selectedStock.sellingPrice) {
          document.getElementById('salePrice').value = selectedStock.sellingPrice;
        }
      };
    }

    function addSale() {
      const item = document.getElementById('saleItemDropdown').value;
      const quantity = parseFloat(document.getElementById('saleQuantity').value);
      const price = parseFloat(document.getElementById('salePrice').value);
      const date = document.getElementById('saleDate').value;
      
      if (!item || isNaN(quantity) || isNaN(price) || !date || quantity <= 0 || price <= 0) {
        showAlert('saleAlert', '❌ Please fill all fields with valid values.', 'error');
        return;
      }
      
      const stockItem = stock.find(s => s.item === item);
      if (!stockItem) {
        showAlert('saleAlert', `❌ Item "${item}" not found in stock.`, 'error');
        return;
      }
      
      if (stockItem.quantity < quantity) {
        showAlert('saleAlert', `❌ Insufficient stock. Available: ${stockItem.quantity}`, 'error');
        return;
      }
      
      // Process sale
      const cost = stockItem.cost;
      const profit = (price - cost) * quantity;
      stockItem.quantity -= quantity;
      
      sales.push({ item, quantity, price, cost, profit, date });
      
      // Clear form
      document.getElementById('saleQuantity').value = '';
      document.getElementById('salePrice').value = '';
      
      showAlert('saleAlert', `✅ Sale recorded! Revenue: KES ${(price * quantity).toFixed(2)}, Profit: KES ${profit.toFixed(2)}`);
      updateAll();
    }

    function showAllSales() {
      showingAllSales = true;
      updateSalesList();
    }

    function showTodaySales() {
      showingAllSales = false;
      updateSalesList();
    }

    function updateSalesList() {
      const ul = document.getElementById('salesList');
      const today = new Date().toISOString().split('T')[0];
      
      let displaySales = showingAllSales ? sales : sales.filter(s => s.date === today);
      
      if (displaySales.length === 0) {
        ul.innerHTML = '<li class="loading">No sales records found</li>';
        return;
      }
      
      ul.innerHTML = '';
      displaySales.slice(-20).reverse().forEach((s, i) => {
        const li = document.createElement('li');
        const actualIndex = sales.indexOf(s);
        
        const saleInfo = document.createElement('div');
        saleInfo.className = 'item-info';
        saleInfo.innerHTML = `
          <strong>${s.item}</strong>
          <small>${s.date} | Qty: ${s.quantity} | Unit Price: KES ${s.price.toFixed(2)} | 
          Revenue: KES ${(s.price * s.quantity).toFixed(2)} | Profit: KES ${s.profit.toFixed(2)}</small>
        `;
        li.appendChild(saleInfo);
        
        const delBtn = document.createElement('button');
        delBtn.textContent = 'Delete';
        delBtn.className = 'delete-btn';
        delBtn.onclick = () => deleteSale(actualIndex);
        li.appendChild(delBtn);
        
        ul.appendChild(li);
      });
      
      if (displaySales.length > 20) {
        const info = document.createElement('li');
        info.className = 'loading';
        info.innerHTML = `Showing latest 20 of ${displaySales.length} ${showingAllSales ? 'total' : "today's"} sales`;
        ul.insertBefore(info, ul.firstChild);
      }
    }

    function deleteSale(index) {
      if (confirm('Are you sure you want to delete this sale record?')) {
        const sale = sales[index];
        const stockItem = stock.find(s => s.item === sale.item);
        if (stockItem) {
          stockItem.quantity += sale.quantity; // Restore stock
        }
        sales.splice(index, 1);
        updateAll();
        showAlert('saleAlert', '✅ Sale record deleted and stock restored');
      }
    }

    function updateAnalytics() {
      const today = new Date().toISOString().split('T')[0];
      const todaySales = sales.filter(s => s.date === today);
      
      const dailyTotal = todaySales.reduce((sum, s) => sum + (s.price * s.quantity), 0);
      const dailyProfit = todaySales.reduce((sum, s) => sum + s.profit, 0);
      const totalRevenue = sales.reduce((sum, s) => sum + (s.price * s.quantity), 0);
      const totalProfit = sales.reduce((sum, s) => sum + s.profit, 0);
      
      document.getElementById('dailyTotal').textContent = `KES ${dailyTotal.toLocaleString('en-KE', {minimumFractionDigits: 2})}`;
      document.getElementById('dailyProfit').textContent = `KES ${dailyProfit.toLocaleString('en-KE', {minimumFractionDigits: 2})}`;
      document.getElementById('totalRevenue').textContent = `KES ${totalRevenue.toLocaleString('en-KE', {minimumFractionDigits: 2})}`;
      document.getElementById('totalProfit').textContent = `KES ${totalProfit.toLocaleString('en-KE', {minimumFractionDigits: 2})}`;
    }

    function updateChart(type = 'daily') {
      const ctx = document.getElementById('salesChart').getContext('2d');
      
      if (sales.length === 0) {
        if (salesChartInstance) salesChartInstance.destroy();
        ctx.font = "16px Arial";
        ctx.fillStyle = "#666";
        ctx.textAlign = "center";
        ctx.fillText("No sales data available for chart", ctx.canvas.width / 2, ctx.canvas.height / 2);
        return;
      }
      
      let chartData;
      
      if (type === 'daily') {
        const groupedByDate = {};
        sales.forEach(sale => {
          if (!groupedByDate[sale.date]) {
            groupedByDate[sale.date] = 0;
          }
          groupedByDate[sale.date] += sale.price * sale.quantity;
        });
        
        chartData = {
          labels: Object.keys(groupedByDate).sort(),
          datasets: [{
            label: 'Daily Revenue (KES)',
            data: Object.values(groupedByDate),
            borderColor: '#667eea',
            backgroundColor: 'rgba(102, 126, 234, 0.1)',
            tension: 0.4,
            fill: true
          }]
        };
      } else if (type === 'items') {
        const groupedByItem = {};
        sales.forEach(sale => {
          if (!groupedByItem[sale.item]) {
            groupedByItem[sale.item] = 0;
          }
          groupedByItem[sale.item] += sale.quantity;
        });
        
        const colors = ['#667eea', '#764ba2', '#f093fb', '#f5576c', '#4facfe', '#00f2fe'];
        chartData = {
          labels: Object.keys(groupedByItem),
          datasets: [{
            label: 'Quantity Sold',
            data: Object.values(groupedByItem),
            backgroundColor: Object.keys(groupedByItem).map((_, i) => colors[i % colors.length])
          }]
        };
      } else if (type === 'profit') {
        const groupedByDate = {};
        sales.forEach(sale => {
          if (!groupedByDate[sale.date]) {
            groupedByDate[sale.date] = 0;
          }
          groupedByDate[sale.date] += sale.profit;
        });
        
        chartData = {
          labels: Object.keys(groupedByDate).sort(),
          datasets: [{
            label: 'Daily Profit (KES)',
            data: Object.values(groupedByDate),
            borderColor: '#4CAF50',
            backgroundColor: 'rgba(76, 175, 80, 0.1)',
            tension: 0.4,
            fill: true
          }]
        };
      }
      
      if (salesChartInstance) {
        salesChartInstance.destroy();
      }
      
      salesChartInstance = new Chart(ctx, {
        type: type === 'items' ? 'doughnut' : 'line',
        data: chartData,
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: {
            legend: {
              position: 'bottom'
            },
            title: {
              display: true,
              text: type === 'daily' ? 'Daily Revenue Trends' : 
                    type === 'items' ? 'Sales by Product' : 'Profit Analysis'
            }
          },
          scales: type !== 'items' ? {
            y: {
              beginAtZero: true,
              title: {
                display: true,
                text: type === 'profit' ? 'Profit (KES)' : 'Revenue (KES)'
              }
            },
            x: {
              title: {
                display: true,
                text: 'Date'
              }
            }
          } : {}
        }
      });
    }

    function exportSales() {
      if (sales.length === 0) {
        alert('No sales data to export');
        return;
      }
      
      let csvContent = "Date,Item,Quantity,Unit Price,Total Revenue,Profit\n";
      sales.forEach(sale => {
        csvContent += `${sale.date},${sale.item},${sale.quantity},${sale.price},${(sale.price * sale.quantity).toFixed(2)},${sale.profit.toFixed(2)}\n`;
      });
      
      const blob = new Blob([csvContent], { type: 'text/csv' });
      const url = window.URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `sales_data_${new Date().toISOString().split('T')[0]}.csv`;
      a.click();
      window.URL.revokeObjectURL(url);
    }

    function updateAll() {
      updateStockList();
      updateDropdown();
      updateSalesList();
      updateAnalytics();
      updateChart();
    }

    // Initialize app
    updateAll();
  </script>
</body>
</html>