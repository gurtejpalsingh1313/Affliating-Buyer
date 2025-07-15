# Affliating-Buyer

<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Affiliate Marketing Hub - Commission Tracker</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        .gradient-bg { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .card-hover:hover { transform: translateY(-2px); transition: all 0.3s ease; }
        .chart-container { height: 300px; }
        .table-scroll { max-height: 400px; overflow-y: auto; }
    </style>
</head>
<body class="bg-gray-50 min-h-screen">
    <!-- Header -->
    <header class="gradient-bg text-white py-6 shadow-lg">
        <div class="container mx-auto px-4">
            <div class="flex items-center justify-between">
                <div>
                    <h1 class="text-3xl font-bold flex items-center">
                        <i class="fas fa-chart-line mr-3"></i>
                        Affiliate Marketing Hub
                    </h1>
                    <p class="text-blue-100 mt-2">आपका Commission Tracking Dashboard</p>
                </div>
                <div class="text-right">
                    <p class="text-sm text-blue-100">Total Earnings</p>
                    <p class="text-2xl font-bold" id="totalEarnings">₹0</p>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <div class="container mx-auto px-4 py-8">
        <!-- Stats Cards -->
        <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
            <div class="bg-white rounded-lg shadow-md p-6 card-hover">
                <div class="flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-600">Total Clicks</p>
                        <p class="text-2xl font-bold text-blue-600" id="totalClicks">0</p>
                    </div>
                    <i class="fas fa-mouse-pointer text-blue-500 text-2xl"></i>
                </div>
            </div>
            <div class="bg-white rounded-lg shadow-md p-6 card-hover">
                <div class="flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-600">Conversions</p>
                        <p class="text-2xl font-bold text-green-600" id="totalConversions">0</p>
                    </div>
                    <i class="fas fa-shopping-cart text-green-500 text-2xl"></i>
                </div>
            </div>
            <div class="bg-white rounded-lg shadow-md p-6 card-hover">
                <div class="flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-600">Conversion Rate</p>
                        <p class="text-2xl font-bold text-purple-600" id="conversionRate">0%</p>
                    </div>
                    <i class="fas fa-percentage text-purple-500 text-2xl"></i>
                </div>
            </div>
            <div class="bg-white rounded-lg shadow-md p-6 card-hover">
                <div class="flex items-center justify-between">
                    <div>
                        <p class="text-sm text-gray-600">Active Links</p>
                        <p class="text-2xl font-bold text-orange-600" id="activeLinks">0</p>
                    </div>
                    <i class="fas fa-link text-orange-500 text-2xl"></i>
                </div>
            </div>
        </div>

        <!-- Add New Product Section -->
        <div class="bg-white rounded-lg shadow-md p-6 mb-8">
            <h2 class="text-xl font-bold mb-4 flex items-center">
                <i class="fas fa-plus-circle mr-2 text-blue-500"></i>
                नया Product/Link Add करें
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Product Name</label>
                    <input type="text" id="productName" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="Product का नाम">
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Platform</label>
                    <select id="platform" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <option value="">Select Platform</option>
                        <option value="Amazon">Amazon</option>
                        <option value="Meesho">Meesho</option>
                        <option value="Flipkart">Flipkart</option>
                        <option value="Myntra">Myntra</option>
                        <option value="Ajio">Ajio</option>
                        <option value="Other">Other</option>
                    </select>
                </div>
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Commission Rate (%)</label>
                    <input type="number" id="commissionRate" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="5">
                </div>
            </div>
            <div class="mt-4">
                <label class="block text-sm font-medium text-gray-700 mb-2">Referral Link</label>
                <input type="url" id="referralLink" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="https://example.com/your-referral-link">
            </div>
            <div class="mt-4">
                <label class="block text-sm font-medium text-gray-700 mb-2">Product Description</label>
                <textarea id="productDescription" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" rows="2" placeholder="Product के बारे में short description"></textarea>
            </div>
            <button onclick="addProduct()" class="mt-4 bg-blue-600 text-white px-6 py-2 rounded-md hover:bg-blue-700 transition duration-300">
                <i class="fas fa-plus mr-2"></i>Add Product
            </button>
        </div>

        <!-- Product Links Table -->
        <div class="bg-white rounded-lg shadow-md p-6 mb-8">
            <h2 class="text-xl font-bold mb-4 flex items-center">
                <i class="fas fa-list mr-2 text-green-500"></i>
                Your Products & Links
            </h2>
            <div class="table-scroll">
                <table class="w-full">
                    <thead class="bg-gray-50">
                        <tr>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Product</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Platform</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Commission</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Clicks</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Conversions</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Earnings</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Actions</th>
                        </tr>
                    </thead>
                    <tbody id="productTableBody">
                        <!-- Products will be populated here -->
                    </tbody>
                </table>
            </div>
        </div>

        <!-- Analytics Charts -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-8">
            <div class="bg-white rounded-lg shadow-md p-6">
                <h3 class="text-lg font-bold mb-4">Monthly Earnings</h3>
                <div class="chart-container">
                    <canvas id="earningsChart"></canvas>
                </div>
            </div>
            <div class="bg-white rounded-lg shadow-md p-6">
                <h3 class="text-lg font-bold mb-4">Platform Performance</h3>
                <div class="chart-container">
                    <canvas id="platformChart"></canvas>
                </div>
            </div>
        </div>

        <!-- Commission Tracking -->
        <div class="bg-white rounded-lg shadow-md p-6 mb-8">
            <h2 class="text-xl font-bold mb-4 flex items-center">
                <i class="fas fa-rupee-sign mr-2 text-yellow-500"></i>
                Commission Tracking
            </h2>
            <div class="table-scroll">
                <table class="w-full">
                    <thead class="bg-gray-50">
                        <tr>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Date</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Product</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Platform</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Order Value</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Commission</th>
                            <th class="px-4 py-2 text-left text-sm font-medium text-gray-700">Status</th>
                        </tr>
                    </thead>
                    <tbody id="commissionTableBody">
                        <!-- Commission data will be populated here -->
                    </tbody>
                </table>
            </div>
        </div>

        <!-- Quick Actions -->
        <div class="bg-white rounded-lg shadow-md p-6">
            <h2 class="text-xl font-bold mb-4 flex items-center">
                <i class="fas fa-tools mr-2 text-purple-500"></i>
                Quick Actions
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <button onclick="generateReport()" class="bg-green-600 text-white px-6 py-3 rounded-md hover:bg-green-700 transition duration-300">
                    <i class="fas fa-file-export mr-2"></i>Generate Report
                </button>
                <button onclick="shareLink()" class="bg-blue-600 text-white px-6 py-3 rounded-md hover:bg-blue-700 transition duration-300">
                    <i class="fas fa-share-alt mr-2"></i>Share Links
                </button>
                <button onclick="clearData()" class="bg-red-600 text-white px-6 py-3 rounded-md hover:bg-red-700 transition duration-300">
                    <i class="fas fa-trash mr-2"></i>Clear Data
                </button>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-6 mt-12">
        <div class="container mx-auto px-4 text-center">
            <p>&copy; 2024 Affiliate Marketing Hub. Made with ❤️ for your success.</p>
            <p class="text-sm text-gray-400 mt-2">Track your referrals, maximize your earnings!</p>
        </div>
    </footer>

    <script>
        // Data Storage
        let products = JSON.parse(localStorage.getItem('affiliateProducts')) || [];
        let commissions = JSON.parse(localStorage.getItem('affiliateCommissions')) || [];

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            loadProducts();
            loadCommissions();
            updateStats();
            initializeCharts();
        });

        // Add Product Function
        function addProduct() {
            const name = document.getElementById('productName').value;
            const platform = document.getElementById('platform').value;
            const commissionRate = document.getElementById('commissionRate').value;
            const referralLink = document.getElementById('referralLink').value;
            const description = document.getElementById('productDescription').value;

            if (!name || !platform || !commissionRate || !referralLink) {
                alert('कृपया सभी required fields भरें');
                return;
            }

            const product = {
                id: Date.now(),
                name: name,
                platform: platform,
                commissionRate: parseFloat(commissionRate),
                referralLink: referralLink,
                description: description,
                clicks: 0,
                conversions: 0,
                earnings: 0,
                dateAdded: new Date().toLocaleDateString()
            };

            products.push(product);
            localStorage.setItem('affiliateProducts', JSON.stringify(products));
            
            // Clear form
            document.getElementById('productName').value = '';
            document.getElementById('platform').value = '';
            document.getElementById('commissionRate').value = '';
            document.getElementById('referralLink').value = '';
            document.getElementById('productDescription').value = '';

            loadProducts();
            updateStats();
            updateCharts();
        }

        // Load Products
        function loadProducts() {
            const tbody = document.getElementById('productTableBody');
            tbody.innerHTML = '';

            products.forEach(product => {
                const row = document.createElement('tr');
                row.className = 'border-b hover:bg-gray-50';
                row.innerHTML = `
                    <td class="px-4 py-2">
                        <div class="font-medium">${product.name}</div>
                        <div class="text-sm text-gray-500">${product.description}</div>
                    </td>
                    <td class="px-4 py-2">
                        <span class="px-2 py-1 bg-blue-100 text-blue-800 rounded-full text-xs">${product.platform}</span>
                    </td>
                    <td class="px-4 py-2">${product.commissionRate}%</td>
                    <td class="px-4 py-2">${product.clicks}</td>
                    <td class="px-4 py-2">${product.conversions}</td>
                    <td class="px-4 py-2 font-medium text-green-600">₹${product.earnings}</td>
                    <td class="px-4 py-2">
                        <button onclick="copyLink('${product.referralLink}')" class="text-blue-600 hover:text-blue-800 mr-2">
                            <i class="fas fa-copy"></i>
                        </button>
                        <button onclick="simulateClick(${product.id})" class="text-green-600 hover:text-green-800 mr-2">
                            <i class="fas fa-mouse-pointer"></i>
                        </button>
                        <button onclick="deleteProduct(${product.id})" class="text-red-600 hover:text-red-800">
                            <i class="fas fa-trash"></i>
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        // Load Commissions
        function loadCommissions() {
            const tbody = document.getElementById('commissionTableBody');
            tbody.innerHTML = '';

            commissions.forEach(commission => {
                const row = document.createElement('tr');
                row.className = 'border-b hover:bg-gray-50';
                row.innerHTML = `
                    <td class="px-4 py-2">${commission.date}</td>
                    <td class="px-4 py-2">${commission.productName}</td>
                    <td class="px-4 py-2">${commission.platform}</td>
                    <td class="px-4 py-2">₹${commission.orderValue}</td>
                    <td class="px-4 py-2 text-green-600 font-medium">₹${commission.commission}</td>
                    <td class="px-4 py-2">
                        <span class="px-2 py-1 bg-green-100 text-green-800 rounded-full text-xs">${commission.status}</span>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        // Update Stats
        function updateStats() {
            const totalClicks = products.reduce((sum, p) => sum + p.clicks, 0);
            const totalConversions = products.reduce((sum, p) => sum + p.conversions, 0);
            const totalEarnings = products.reduce((sum, p) => sum + p.earnings, 0);
            const conversionRate = totalClicks > 0 ? ((totalConversions / totalClicks) * 100).toFixed(1) : 0;

            document.getElementById('totalClicks').textContent = totalClicks;
            document.getElementById('totalConversions').textContent = totalConversions;
            document.getElementById('totalEarnings').textContent = `₹${totalEarnings}`;
            document.getElementById('conversionRate').textContent = `${conversionRate}%`;
            document.getElementById('activeLinks').textContent = products.length;
        }

        // Initialize Charts
        function initializeCharts() {
            // Earnings Chart
            const earningsCtx = document.getElementById('earningsChart').getContext('2d');
            new Chart(earningsCtx, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
                    datasets: [{
                        label: 'Monthly Earnings (₹)',
                        data: [500, 750, 1200, 800, 1500, 2000],
                        borderColor: 'rgb(59, 130, 246)',
                        backgroundColor: 'rgba(59, 130, 246, 0.1)',
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });

            // Platform Chart
            const platformCtx = document.getElementById('platformChart').getContext('2d');
            new Chart(platformCtx, {
                type: 'doughnut',
                data: {
                    labels: ['Amazon', 'Meesho', 'Flipkart', 'Myntra', 'Others'],
                    datasets: [{
                        data: [35, 25, 20, 15, 5],
                        backgroundColor: [
                            '#FF9500',
                            '#E91E63',
                            '#2196F3',
                            '#9C27B0',
                            '#4CAF50'
                        ]
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false
                }
            });
        }

        // Utility Functions
        function copyLink(link) {
            navigator.clipboard.writeText(link);
            alert('Link copied to clipboard!');
        }

        function simulateClick(productId) {
            const product = products.find(p => p.id === productId);
            if (product) {
                product.clicks++;
                // Simulate random conversion
                if (Math.random() < 0.1) { // 10% conversion rate
                    product.conversions++;
                    const orderValue = Math.floor(Math.random() * 2000) + 500;
                    const commission = orderValue * (product.commissionRate / 100);
                    product.earnings += commission;
                    
                    // Add to commission tracking
                    commissions.push({
                        date: new Date().toLocaleDateString(),
                        productName: product.name,
                        platform: product.platform,
                        orderValue: orderValue,
                        commission: commission,
                        status: 'Confirmed'
                    });
                    localStorage.setItem('affiliateCommissions', JSON.stringify(commissions));
                }
                localStorage.setItem('affiliateProducts', JSON.stringify(products));
                loadProducts();
                loadCommissions();
                updateStats();
            }
        }

        function deleteProduct(productId) {
            if (confirm('Are you sure you want to delete this product?')) {
                products = products.filter(p => p.id !== productId);
                localStorage.setItem('affiliateProducts', JSON.stringify(products));
                loadProducts();
                updateStats();
            }
        }

        function generateReport() {
            const report = {
                totalProducts: products.length,
                totalClicks: products.reduce((sum, p) => sum + p.clicks, 0),
                totalConversions: products.reduce((sum, p) => sum + p.conversions, 0),
                totalEarnings: products.reduce((sum, p) => sum + p.earnings, 0),
                products: products
            };
            
            const reportData = JSON.stringify(report, null, 2);
            const blob = new Blob([reportData], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'affiliate_report.json';
            a.click();
            URL.revokeObjectURL(url);
        }

        function shareLink() {
            const shareData = products.map(p => ({
                name: p.name,
                platform: p.platform,
                link: p.referralLink
            }));
            
            const shareText = shareData.map(s => `${s.name} (${s.platform}): ${s.link}`).join('\n\n');
            
            if (navigator.share) {
                navigator.share({
                    title: 'My Affiliate Links',
                    text: shareText
                });
            } else {
                navigator.clipboard.writeText(shareText);
                alert('All links copied to clipboard!');
            }
        }

        function clearData() {
            if (confirm('Are you sure you want to clear all data? This action cannot be undone.')) {
                localStorage.removeItem('affiliateProducts');
                localStorage.removeItem('affiliateCommissions');
                products = [];
                commissions = [];
                loadProducts();
                loadCommissions();
                updateStats();
                location.reload();
            }
        }

        function updateCharts() {
            // This would update the charts with new data
            // For now, we'll just reinitialize them
            setTimeout(() => {
                initializeCharts();
            }, 100);
        }
    </script>
</body>
</html>
