# Loullie Store
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#1e40af">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="Compara PY">
    <title>Compara PY-BR PRO v4.0 - OCR Real + Histórico</title>
    
    <link rel="icon" type="image/png" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Crect width='100' height='100' fill='%231e40af'/%3E%3Ctext x='50' y='60' font-size='50' fill='white' text-anchor='middle' font-family='Arial'%3E🛒%3C/text%3E%3C/svg%3E">
    <link rel="manifest" id="manifest-placeholder">
    
    <!-- Tesseract.js para OCR Real -->
    <script src='https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js'></script>
    
    <style>
        :root {
            --primary-color: #1e40af;
            --primary-light: #3b82f6;
            --secondary-color: #667eea;
            --success-color: #10b981;
            --danger-color: #ef4444;
            --warning-color: #f59e0b;
            --bg-light: #f8fafc;
            --text-dark: #1e293b;
            --text-light: #64748b;
            --border-color: #e2e8f0;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, var(--secondary-color) 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 10px;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
            animation: slideIn 0.5s ease-out;
        }
        
        @media (min-width: 768px) {
            body { padding: 20px; }
            .container { max-width: 720px; }
            .content { padding: 30px !important; }
            .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
            .form-group.full-width { grid-column: 1 / -1; }
        }
        
        @media (min-width: 1024px) {
            body { padding: 40px; }
            .container { max-width: 1400px; display: grid; grid-template-columns: 1fr 1fr; gap: 0; }
            .header { grid-column: 1 / -1; }
            .content { padding: 40px !important; }
            .left-column { padding-right: 20px; border-right: 2px solid var(--border-color); }
            .right-column { padding-left: 20px; }
            .results { margin-top: 0 !important; }
        }
        
        @media (min-width: 1440px) {
            .container { max-width: 1600px; }
            .content { padding: 50px !important; }
        }
        
        @keyframes slideIn {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-light) 100%);
            color: white;
            padding: 25px 20px;
            text-align: center;
            position: relative;
        }
        
        .header h1 {
            font-size: clamp(18px, 4vw, 24px);
            margin-bottom: 5px;
        }
        
        .header .emoji {
            font-size: clamp(28px, 5vw, 36px);
            margin-bottom: 5px;
            display: block;
        }
        
        .header p {
            font-size: clamp(12px, 2.5vw, 14px);
            opacity: 0.9;
        }
        
        .version-badge {
            position: absolute;
            top: 10px;
            right: 10px;
            background: rgba(255,255,255,0.2);
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 11px;
            font-weight: 600;
        }
        
        .content {
            padding: 20px;
        }
        
        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            border-bottom: 2px solid var(--border-color);
        }
        
        .tab {
            flex: 1;
            padding: 12px;
            background: transparent;
            border: none;
            border-bottom: 3px solid transparent;
            cursor: pointer;
            font-weight: 600;
            color: var(--text-light);
            transition: all 0.3s;
        }
        
        .tab.active {
            color: var(--primary-color);
            border-bottom-color: var(--primary-color);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .exchange-rates-section {
            background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        
        .exchange-rates-section h4 {
            color: #92400e;
            margin-bottom: 15px;
            font-size: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .rate-editor {
            background: white;
            padding: 12px;
            border-radius: 10px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }
        
        .rate-editor label {
            font-weight: 600;
            color: var(--text-dark);
            font-size: 14px;
            min-width: 80px;
            margin: 0;
        }
        
        .rate-editor input {
            flex: 1;
            padding: 10px;
            border: 2px solid var(--border-color);
            border-radius: 8px;
            font-size: 15px;
            font-weight: 600;
            color: var(--primary-color);
        }
        
        .upload-section {
            border: 3px dashed var(--border-color);
            border-radius: 15px;
            padding: 25px 20px;
            text-align: center;
            background: var(--bg-light);
            margin-bottom: 20px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .upload-section.analyzing {
            border-color: var(--warning-color);
            background: #fef3c7;
        }
        
        .upload-section.has-image {
            padding: 15px;
            border-color: var(--success-color);
            background: #ecfdf5;
        }
        
        .upload-buttons {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        
        .upload-btn {
            flex: 1;
            min-width: 140px;
            padding: 12px;
            border: 2px solid var(--primary-light);
            background: white;
            color: var(--primary-light);
            border-radius: 10px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .upload-btn:active {
            background: var(--primary-light);
            color: white;
        }
        
        .preview-image {
            max-width: 100%;
            max-height: 300px;
            border-radius: 10px;
            margin-top: 10px;
            display: none;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }
        
        .ocr-status {
            display: none;
            background: #fef3c7;
            padding: 12px;
            border-radius: 8px;
            margin-top: 10px;
            font-size: 13px;
            color: #92400e;
            text-align: left;
        }
        
        .ocr-status.success {
            background: #dcfce7;
            color: #166534;
        }
        
        .ocr-status.error {
            background: #fee2e2;
            color: #991b1b;
        }
        
        .ocr-progress {
            margin-top: 8px;
            height: 6px;
            background: rgba(0,0,0,0.1);
            border-radius: 3px;
            overflow: hidden;
        }
        
        .ocr-progress-bar {
            height: 100%;
            background: var(--primary-color);
            transition: width 0.3s;
            width: 0%;
        }
        
        .form-group {
            margin-bottom: 18px;
        }
        
        label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
            color: #334155;
            font-size: 14px;
        }
        
        input[type="number"], 
        input[type="text"], 
        select {
            width: 100%;
            padding: 14px;
            border: 2px solid var(--border-color);
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s;
            background: white;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: var(--primary-light);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }
        
        .btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-light) 100%);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 14px rgba(59, 130, 246, 0.4);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .btn:active {
            transform: translateY(2px);
        }
        
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 30px 20px;
        }
        
        .spinner {
            border: 4px solid #f3f4f6;
            border-top: 4px solid var(--primary-light);
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .results {
            display: none;
            margin-top: 25px;
            animation: slideUp 0.5s ease-out;
        }
        
        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .result-card {
            background: var(--bg-light);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }
        
        .result-card h3 {
            color: var(--primary-color);
            margin-bottom: 15px;
            font-size: 17px;
        }
        
        .price-row {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid var(--border-color);
        }
        
        .price-row:last-child {
            border-bottom: none;
            padding-bottom: 0;
        }
        
        .savings {
            background: linear-gradient(135deg, var(--success-color) 0%, #059669 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            margin-top: 15px;
            font-weight: 700;
            font-size: 18px;
        }
        
        .savings.negative {
            background: linear-gradient(135deg, var(--danger-color) 0%, #dc2626 100%);
        }
        
        .best-currency {
            background: linear-gradient(135deg, #8b5cf6 0%, #7c3aed 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            margin-top: 15px;
            font-weight: 700;
        }
        
        .history-item {
            background: white;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
            position: relative;
        }
        
        .history-item h4 {
            color: var(--primary-color);
            margin-bottom: 8px;
            font-size: 16px;
        }
        
        .history-item-info {
            font-size: 13px;
            color: var(--text-light);
            line-height: 1.6;
        }
        
        .history-item-result {
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid var(--border-color);
            font-weight: 600;
        }
        
        .history-item-result.positive {
            color: var(--success-color);
        }
        
        .history-item-result.negative {
            color: var(--danger-color);
        }
        
        .delete-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: var(--danger-color);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
        }
        
        .empty-history {
            text-align: center;
            padding: 40px 20px;
            color: var(--text-light);
        }
        
        .auto-filled {
            animation: highlight 1s ease-out;
        }
        
        @keyframes highlight {
            0% { background-color: #dcfce7; }
            100% { background-color: white; }
        }
        
        input[type="file"] {
            display: none;
        }
        
        .remove-image {
            background: var(--danger-color);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 12px;
            margin-top: 10px;
            cursor: pointer;
            display: none;
        }
        
        .info-box {
            background: #f0f9ff;
            border-left: 4px solid var(--primary-light);
            padding: 12px;
            border-radius: 8px;
            font-size: 13px;
            line-height: 1.6;
            color: var(--primary-color);
            margin-top: 8px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <span class="version-badge">v4.0 PRO</span>
            <span class="emoji">🛒</span>
            <h1>Compara PY-BR PRO</h1>
            <p>OCR Real • Histórico • Melhor Moeda • RTU</p>
        </div>
        
        <div class="content left-column">
            <div class="tabs">
                <button class="tab active" onclick="switchTab('compare')">🔍 Comparar</button>
                <button class="tab" onclick="switchTab('history')">📋 Histórico</button>
            </div>
            
            <div id="compareTab" class="tab-content active">
                <div class="exchange-rates-section">
                    <h4>💱 Taxas de Câmbio (Editável)</h4>
                    <div class="rate-editor">
                        <label>1 US$ =</label>
                        <input type="number" id="rateBRL" value="5.85" step="0.01" min="0">
                        <span style="font-weight: 600;">BRL</span>
                    </div>
                    <div class="rate-editor">
                        <label>1 ₲ =</label>
                        <input type="number" id="rateGuarani" value="0.00070" step="0.00001" min="0">
                        <span style="font-weight: 600;">BRL</span>
                    </div>
                    <div class="rate-editor">
                        <label>1 US$ =</label>
                        <input type="number" id="rateGuaraniUSD" value="8357" step="1" min="0">
                        <span style="font-weight: 600;">₲</span>
                    </div>
                </div>
                
                <div class="upload-section" id="uploadSection">
                    <div id="uploadPrompt">
                        <span style="font-size: 48px; display: block; margin-bottom: 10px;">📸</span>
                        <p style="font-weight: 600; margin-bottom: 5px;">OCR Real - Lê Preço e Nome!</p>
                        <p style="font-size: 13px; color: var(--text-light);">Foto nítida da etiqueta/embalagem</p>
                        <div class="upload-buttons">
                            <button class="upload-btn" id="cameraBtn">📷 Câmera</button>
                            <button class="upload-btn" id="galleryBtn">🖼️ Galeria</button>
                        </div>
                    </div>
                    <input type="file" id="fileInputCamera" accept="image/*" capture="environment">
                    <input type="file" id="fileInputGallery" accept="image/*">
                    <img id="previewImage" class="preview-image" alt="Preview">
                    <div id="ocrStatus" class="ocr-status">
                        <div id="ocrText"></div>
                        <div class="ocr-progress">
                            <div id="ocrProgressBar" class="ocr-progress-bar"></div>
                        </div>
                    </div>
                    <button id="removeImageBtn" class="remove-image">❌ Remover</button>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="currency">💱 Moeda:</label>
                        <select id="currency">
                            <option value="guarani">Guarani (₲)</option>
                            <option value="dolar">Dólar (US$)</option>
                            <option value="real">Real (R$)</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="productPrice" id="priceLabel">💵 Preço (₲):</label>
                        <input type="number" id="productPrice" placeholder="Ex: 150000" step="0.01">
                    </div>
                </div>
                
                <div class="form-group full-width">
                    <label for="productName">📦 Nome do Produto:</label>
                    <input type="text" id="productName" placeholder="Ex: Notebook Dell Inspiron 15">
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="personType">👤 Pessoa:</label>
                        <select id="personType">
                            <option value="fisica">Pessoa Física</option>
                            <option value="juridica">Pessoa Jurídica</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="specialRegime">🎯 Regime:</label>
                        <select id="specialRegime">
                            <option value="none">Normal (60%)</option>
                            <option value="remessaconforme">Remessa Conforme (17%)</option>
                            <option value="rtu">RTU - Remessa Expressa (60%)</option>
                            <option value="isencao">Isenção (0%)</option>
                            <option value="courier">Courier</option>
                            <option value="drawback">Drawback (PJ)</option>
                            <option value="zona_franca">Zona Franca</option>
                            <option value="ex_tarifario">Ex-Tarifário (PJ)</option>
                        </select>
                    </div>
                </div>
                
                <div class="form-group full-width">
                    <div class="info-box" id="regimeInfo" style="display: none;"></div>
                </div>
                
                <button class="btn" id="compareBtn">🔍 Comparar Agora</button>
                
                <div class="loading" id="loading">
                    <div class="spinner"></div>
                    <p style="color: var(--text-light); font-size: 14px;">Calculando...</p>
                </div>
            </div>
            
            <div id="historyTab" class="tab-content">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <h3 style="color: var(--primary-color);">Consultas Salvas</h3>
                    <button onclick="clearHistory()" style="background: var(--danger-color); color: white; border: none; padding: 8px 15px; border-radius: 8px; cursor: pointer; font-size: 13px;">🗑️ Limpar Tudo</button>
                </div>
                <div id="historyList"></div>
            </div>
        </div>
        
        <div class="content right-column">
            <div class="results" id="results">
                <div id="bestCurrencyDiv" class="best-currency">
                    <div id="bestCurrencyText"></div>
                </div>
                
                <div class="result-card">
                    <h3>🇵🇾 Custo no Paraguai</h3>
                    <div class="price-row">
                        <span>Preço original:</span>
                        <span id="priceOriginal" style="font-weight: 700;">-</span>
                    </div>
                    <div class="price-row">
                        <span>Em Real:</span>
                        <span id="priceBRL" style="font-weight: 700;">-</span>
                    </div>
                    <div class="price-row">
                        <span>Impostos:</span>
                        <span id="taxAmount" style="font-weight: 700;">-</span>
                    </div>
                    <div class="price-row">
                        <span><strong>TOTAL:</strong></span>
                        <span id="totalParaguai" style="font-weight: 700; color: var(--primary-color); font-size: 17px;">-</span>
                    </div>
                </div>
                
                <div class="result-card">
                    <h3>🇧🇷 Preço no Brasil</h3>
                    <div class="price-row">
                        <span>Estimado:</span>
                        <span id="priceBrazil" style="font-weight: 700; color: var(--danger-color);">-</span>
                    </div>
                </div>
                
                <div class="savings" id="savingsDiv">
                    <div id="savingsText"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const manifestData = {
            name: "Compara PY-BR PRO v4.0",
            short_name: "ComparaPY",
            start_url: window.location.href,
            display: "standalone",
            background_color: "#ffffff",
            theme_color: "#1e40af",
            icons: [{
                src: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'%3E%3Crect width='512' height='512' fill='%231e40af' rx='100'/%3E%3Ctext x='256' y='340' font-size='280' fill='white' text-anchor='middle'%3E🛒%3C/text%3E%3C/svg%3E",
                sizes: "512x512",
                type: "image/svg+xml"
            }]
        };
        
        const manifestBlob = new Blob([JSON.stringify(manifestData)], {type: 'application/json'});
        document.getElementById('manifest-placeholder').href = URL.createObjectURL(manifestBlob);

        // Service Worker
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                const sw = `self.addEventListener('install',e=>e.waitUntil(self.skipWaiting()));self.addEventListener('activate',e=>e.waitUntil(self.clients.claim()));`;
                navigator.serviceWorker.register(URL.createObjectURL(new Blob([sw], {type: 'application/javascript'})));
            });
        }

        // Elementos DOM
        const fileInputCamera = document.getElementById('fileInputCamera');
        const fileInputGallery = document.getElementById('fileInputGallery');
        const previewImage = document.getElementById('previewImage');
        const ocrStatus = document.getElementById('ocrStatus');
        const ocrText = document.getElementById('ocrText');
        const ocrProgressBar = document.getElementById('ocrProgressBar');
        const uploadSection = document.getElementById('uploadSection');
        const productPriceInput = document.getElementById('productPrice');
        const productNameInput = document.getElementById('productName');
        const currencySelect = document.getElementById('currency');
        const specialRegimeSelect = document.getElementById('specialRegime');
        const regimeInfo = document.getElementById('regimeInfo');
        
        // Funções de Tab
        function switchTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            if (tab === 'compare') {
                document.querySelectorAll('.tab')[0].classList.add('active');
                document.getElementById('compareTab').classList.add('active');
            } else {
                document.querySelectorAll('.tab')[1].classList.add('active');
                document.getElementById('historyTab').classList.add('active');
                loadHistory();
            }
        }
        
        // Upload de imagem
        document.getElementById('cameraBtn').addEventListener('click', () => fileInputCamera.click());
        document.getElementById('galleryBtn').addEventListener('click', () => fileInputGallery.click());
        
        fileInputCamera.addEventListener('change', e => e.target.files[0] && handleImageUpload(e.target.files[0]));
        fileInputGallery.addEventListener('change', e => e.target.files[0] && handleImageUpload(e.target.files[0]));
        
        document.getElementById('removeImageBtn').addEventListener('click', () => {
            previewImage.style.display = 'none';
            document.getElementById('removeImageBtn').style.display = 'none';
            ocrStatus.style.display = 'none';
            document.getElementById('uploadPrompt').style.display = 'block';
            uploadSection.classList.remove('has-image', 'analyzing');
            fileInputCamera.value = '';
            fileInputGallery.value = '';
        });
        
        async function handleImageUpload(file) {
            const reader = new FileReader();
            reader.onload = async (e) => {
                previewImage.src = e.target.result;
                previewImage.style.display = 'block';
                document.getElementById('removeImageBtn').style.display = 'inline-block';
                document.getElementById('uploadPrompt').style.display = 'none';
                uploadSection.classList.add('has-image', 'analyzing');
                
                await performOCR(e.target.result);
            };
            reader.readAsDataURL(file);
        }
        
        // OCR REAL com Tesseract.js
        async function performOCR(imageData) {
            ocrStatus.style.display = 'block';
            ocrStatus.className = 'ocr-status';
            ocrText.innerHTML = '🔍 Analisando imagem com OCR real...';
            ocrProgressBar.style.width = '0%';
            
            try {
                const worker = await Tesseract.createWorker('por+eng', 1, {
                    logger: m => {
                        if (m.status === 'recognizing text') {
                            const progress = Math.round(m.progress * 100);
                            ocrProgressBar.style.width = progress + '%';
                            ocrText.innerHTML = `🔍 Reconhecendo texto: ${progress}%`;
                        }
                    }
                });
                
                const { data: { text } } = await Tesseract.recognize(imageData);
                await worker.terminate();
                
                // Processar texto extraído
                const extractedData = extractProductInfo(text);
                
                if (extractedData.productName || extractedData.price) {
                    ocrStatus.className = 'ocr-status success';
                    ocrText.innerHTML = '<strong>✅ Dados Extraídos com Sucesso!</strong><br>';
                    
                    if (extractedData.productName) {
                        productNameInput.value = extractedData.productName;
                        productNameInput.classList.add('auto-filled');
                        ocrText.innerHTML += `📦 Produto: ${extractedData.productName}<br>`;
                    }
                    
                    if (extractedData.price) {
                        productPriceInput.value = extractedData.price;
                        productPriceInput.classList.add('auto-filled');
                        ocrText.innerHTML += `💵 Preço: ${extractedData.price}<br>`;
                        
                        if (extractedData.currency) {
                            currencySelect.value = extractedData.currency;
                            updatePriceLabel();
                            ocrText.innerHTML += `💱 Moeda: ${extractedData.currency === 'guarani' ? 'Guarani' : extractedData.currency === 'dolar' ? 'Dólar' : 'Real'}<br>`;
                        }
                    }
                    
                    ocrText.innerHTML += '<br><small>Texto completo: ' + text.substring(0, 100) + '...</small>';
                    
                    setTimeout(() => {
                        productNameInput.classList.remove('auto-filled');
                        productPriceInput.classList.remove('auto-filled');
                    }, 2000);
                } else {
                    ocrStatus.className = 'ocr-status error';
                    ocrText.innerHTML = `⚠️ Não consegui extrair dados claramente.<br><small>Texto detectado: ${text.substring(0, 150)}...</small><br><br>💡 Dica: Tire foto mais nítida da etiqueta de preço`;
                }
                
            } catch (error) {
                ocrStatus.className = 'ocr-status error';
                ocrText.textContent = '❌ Erro no OCR: ' + error.message;
            } finally {
                uploadSection.classList.remove('analyzing');
            }
        }
        
        // Extrair informações do texto OCR
        function extractProductInfo(text) {
            let productName = '';
            let price = '';
            let currency = 'guarani';
            
            // Limpar texto
            const cleanText = text.replace(/\n/g, ' ').trim();
            
            // Detectar preço com diferentes formatos
            const pricePatterns = [
                /(?:R\$|RS)\s*(\d{1,3}(?:[.,]\d{3})*(?:[.,]\d{2})?)/i,  // R$ 1.234,56
                /(?:US\$|USD)\s*(\d{1,3}(?:[.,]\d{3})*(?:[.,]\d{2})?)/i, // US$ 123.45
                /₲\s*(\d{1,3}(?:[.,]\d{3})*)/i,                          // ₲ 123.456
                /Gs\s*(\d{1,3}(?:[.,]\d{3})*)/i,                         // Gs 123.456
                /(\d{1,3}(?:[.,]\d{3}){2,})/,                            // 123.456.789 (guarani)
                /(\d{1,3}[.,]\d{2})/                                     // 123.45 (dólar/real)
            ];
            
            for (let pattern of pricePatterns) {
                const match = cleanText.match(pattern);
                if (match) {
                    price = match[1].replace(/[.,]/g, '');
                    
                    // Detectar moeda
                    if (cleanText.match(/R\$|RS|Real/i)) {
                        currency = 'real';
                        // Ajustar para formato decimal
                        if (price.length > 2) {
                            price = price.slice(0, -2) + '.' + price.slice(-2);
                        }
                    } else if (cleanText.match(/US\$|USD|Dólar|Dollar/i)) {
                        currency = 'dolar';
                        if (price.length > 2) {
                            price = price.slice(0, -2) + '.' + price.slice(-2);
                        }
                    } else if (cleanText.match(/₲|Gs|Guarani/i) || price.length >= 5) {
                        currency = 'guarani';
                    }
                    
                    break;
                }
            }
            
            // Extrair nome do produto (primeira linha significativa ou texto antes do preço)
            const lines = text.split('\n').filter(l => l.trim().length > 3);
            if (lines.length > 0) {
                // Pegar primeira linha com mais de 5 caracteres que não seja só números
                for (let line of lines) {
                    if (line.length > 5 && !/^\d+$/.test(line.trim())) {
                        productName = line.trim().substring(0, 100);
                        break;
                    }
                }
            }
            
            return { productName, price, currency };
        }
        
        // Atualizar label
        function updatePriceLabel() {
            const labels = {
                'guarani': '💵 Preço (₲):',
                'dolar': '💵 Preço (US$):',
                'real': '💵 Preço (R$):'
            };
            document.getElementById('priceLabel').textContent = labels[currencySelect.value];
        }
        
        currencySelect.addEventListener('change', updatePriceLabel);
        
        // Info de regime
        specialRegimeSelect.addEventListener('change', () => {
            const regime = specialRegimeSelect.value;
            const infos = {
                'none': 'Regime normal: 60% de Imposto de Importação.',
                'remessaconforme': 'Remessa Conforme: 17% para compras online até US$ 3.000 em sites cadastrados.',
                'rtu': 'RTU (Regime de Tributação Unificada): 60% de imposto para remessas expressas internacionais. Processo simplificado para encomendas aéreas e expressas.',
                'isencao': 'Isenção: Até US$ 1.000 via terrestre para pessoa física.',
                'courier': 'Courier: 60% II + ICMS. Processo rápido.',
                'drawback': 'Drawback (PJ): Suspensão de impostos para exportadores.',
                'zona_franca': 'Zona Franca: Incentivos fiscais especiais.',
                'ex_tarifario': 'Ex-Tarifário (PJ): Redução para bens sem similar nacional.'
            };
            
            regimeInfo.textContent = infos[regime] || '';
            regimeInfo.style.display = regime === 'none' ? 'none' : 'block';
        });
        
        // Taxas
        function getExchangeRates() {
            return {
                USD_TO_BRL: parseFloat(document.getElementById('rateBRL').value) || 5.85,
                GUARANI_TO_BRL: parseFloat(document.getElementById('rateGuarani').value) || 0.00070,
                USD_TO_GUARANI: parseFloat(document.getElementById('rateGuaraniUSD').value) || 8357
            };
        }
        
        function convertToBRL(price, currency) {
            const rates = getExchangeRates();
            return currency === 'guarani' ? price * rates.GUARANI_TO_BRL :
                   currency === 'dolar' ? price * rates.USD_TO_BRL : price;
        }
        
        // Calcular impostos
        function calculateTaxes(priceBRL, priceUSD, personType, regime) {
            let taxRate = 0.60;
            let taxAmount = priceBRL * taxRate;
            let taxDescription = 'II (60%)';
            
            if (regime === 'remessaconforme' && priceUSD <= 3000) {
                taxRate = 0.17;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Remessa Conforme (17%)';
            } else if (regime === 'rtu') {
                taxRate = 0.60;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'RTU (60%)';
            } else if (regime === 'isencao' && priceUSD <= 1000) {
                taxAmount = 0;
                taxDescription = 'Isento';
            } else if (regime === 'drawback' && personType === 'juridica') {
                taxAmount = 0;
                taxDescription = 'Drawback (0%)';
            } else if (regime === 'ex_tarifario' && personType === 'juridica') {
                taxAmount = priceBRL * 0.02;
                taxDescription = 'Ex-Tarifário (2%)';
            } else if (regime === 'zona_franca') {
                taxAmount = priceBRL * 0.20;
                taxDescription = 'Zona Franca (20%)';
            } else if (personType === 'juridica' && regime === 'none') {
                taxAmount = priceBRL * 0.60 + priceBRL * 0.12;
                taxDescription = 'II (60%) + ICMS (12%)';
            }
            
            return { taxAmount, taxDescription };
        }
        
        // Calcular melhor moeda
        function calculateBestCurrency(price, currency) {
            const rates = getExchangeRates();
            
            let results = {
                guarani: { value: 0, text: '' },
                dolar: { value: 0, text: '' },
                real: { value: 0, text: '' }
            };
            
            // Converter preço original para BRL
            const priceBRL = convertToBRL(price, currency);
            const priceUSD = priceBRL / rates.USD_TO_BRL;
            const priceGuarani = priceUSD * rates.USD_TO_GUARANI;
            
            // Simular compra em cada moeda
            results.guarani.value = priceGuarani;
            results.guarani.text = `₲ ${priceGuarani.toLocaleString('pt-BR', {maximumFractionDigits: 0})}`;
            
            results.dolar.value = priceUSD;
            results.dolar.text = `US$ ${priceUSD.toFixed(2)}`;
            
            results.real.value = priceBRL;
            results.real.text = `R$ ${priceBRL.toFixed(2)}`;
            
            // Determinar melhor moeda (menor valor em BRL)
            let best = 'real';
            let bestValueBRL = priceBRL;
            
            // Comparar considerando as taxas
            const guaraniInBRL = priceGuarani * rates.GUARANI_TO_BRL;
            const dolarInBRL = priceUSD * rates.USD_TO_BRL;
            
            if (guaraniInBRL < bestValueBRL) {
                best = 'guarani';
                bestValueBRL = guaraniInBRL;
            }
            if (dolarInBRL < bestValueBRL) {
                best = 'dolar';
                bestValueBRL = dolarInBRL;
            }
            
            return { results, best };
        }
        
        // Buscar preço Brasil
        async function searchBrazilPrice(productName, priceBRL) {
            await new Promise(r => setTimeout(r, 800));
            const multipliers = {
                'notebook': 2.8, 'celular': 2.5, 'iphone': 3.0, 'perfume': 2.8,
                'playstation': 2.5, 'xbox': 2.5, 'default': 2.2
            };
            
            let mult = multipliers.default;
            for (let [key, val] of Object.entries(multipliers)) {
                if (productName.toLowerCase().includes(key)) {
                    mult = val;
                    break;
                }
            }
            return priceBRL * mult;
        }
        
        // Comparação
        document.getElementById('compareBtn').addEventListener('click', async () => {
            const price = parseFloat(productPriceInput.value);
            const currency = currencySelect.value;
            const personType = document.getElementById('personType').value;
            const regime = specialRegimeSelect.value;
            const productName = productNameInput.value || 'Produto';
            
            if (!price || price <= 0 || !productName.trim()) {
                alert('⚠️ Preencha nome e preço!');
                return;
            }
            
            document.getElementById('compareBtn').disabled = true;
            document.getElementById('loading').style.display = 'block';
            document.getElementById('results').style.display = 'none';
            
            try {
                const rates = getExchangeRates();
                const priceBRL = convertToBRL(price, currency);
                const priceUSD = priceBRL / rates.USD_TO_BRL;
                
                const { taxAmount, taxDescription } = calculateTaxes(priceBRL, priceUSD, personType, regime);
                const totalParaguai = priceBRL + taxAmount;
                const priceBrazil = await searchBrazilPrice(productName, priceBRL);
                const savings = priceBrazil - totalParaguai;
                const savingsPercent = ((savings / priceBrazil) * 100).toFixed(1);
                
                // Melhor moeda
                const { results: currencyResults, best } = calculateBestCurrency(price, currency);
                const bestCurrencyNames = {
                    'guarani': 'Guarani (₲)',
                    'dolar': 'Dólar (US$)',
                    'real': 'Real (R$)'
                };
                
                document.getElementById('bestCurrencyText').innerHTML = `
                    💎 MELHOR MOEDA: <strong>${bestCurrencyNames[best]}</strong><br>
                    <small style="font-size: 14px; opacity: 0.9;">
                        ₲ ${currencyResults.guarani.text} • 
                        ${currencyResults.dolar.text} • 
                        ${currencyResults.real.text}
                    </small>
                `;
                
                // Resultados
                const symbols = { 'guarani': '₲', 'dolar': 'US$', 'real': 'R$' };
                document.getElementById('priceOriginal').textContent = `${symbols[currency]} ${price.toLocaleString('pt-BR', {minimumFractionDigits: 2})}`;
                document.getElementById('priceBRL').textContent = `R$ ${priceBRL.toFixed(2)}`;
                document.getElementById('taxAmount').textContent = `R$ ${taxAmount.toFixed(2)} (${taxDescription})`;
                document.getElementById('totalParaguai').textContent = `R$ ${totalParaguai.toFixed(2)}`;
                document.getElementById('priceBrazil').textContent = `R$ ${priceBrazil.toFixed(2)}`;
                
                const savingsDiv = document.getElementById('savingsDiv');
                const savingsText = document.getElementById('savingsText');
                
                if (savings > 0) {
                    savingsDiv.classList.remove('negative');
                    savingsText.innerHTML = `💰 ECONOMIA: R$ ${savings.toFixed(2)}<br><small>Você economiza ${savingsPercent}%!</small>`;
                } else {
                    savingsDiv.classList.add('negative');
                    savingsText.innerHTML = `⚠️ NÃO COMPENSA<br><small>R$ ${Math.abs(savings).toFixed(2)} mais caro</small>`;
                }
                
                document.getElementById('results').style.display = 'block';
                
                // Salvar no histórico
                saveToHistory({
                    productName, price, currency, personType, regime,
                    totalParaguai, priceBrazil, savings, savingsPercent,
                    bestCurrency: best, timestamp: new Date().toISOString()
                });
                
            } catch (error) {
                alert('❌ Erro: ' + error.message);
            } finally {
                document.getElementById('compareBtn').disabled = false;
                document.getElementById('loading').style.display = 'none';
            }
        });
        
        // Histórico
        function saveToHistory(data) {
            let history = JSON.parse(localStorage.getItem('comparapy_history') || '[]');
            history.unshift(data);
            if (history.length > 50) history = history.slice(0, 50);
            localStorage.setItem('comparapy_history', JSON.stringify(history));
        }
        
        function loadHistory() {
            const history = JSON.parse(localStorage.getItem('comparapy_history') || '[]');
            const list = document.getElementById('historyList');
            
            if (history.length === 0) {
                list.innerHTML = '<div class="empty-history">📭<br>Nenhuma consulta salva ainda</div>';
                return;
            }
            
            list.innerHTML = history.map((item, index) => `
                <div class="history-item">
                    <button class="delete-btn" onclick="deleteHistoryItem(${index})">🗑️</button>
                    <h4>${item.productName}</h4>
                    <div class="history-item-info">
                        💵 Preço: ${item.price.toLocaleString('pt-BR')} (${item.currency})<br>
                        👤 ${item.personType === 'fisica' ? 'PF' : 'PJ'} • 
                        🎯 ${item.regime}<br>
                        💎 Melhor moeda: ${item.bestCurrency}<br>
                        📅 ${new Date(item.timestamp).toLocaleString('pt-BR')}
                    </div>
                    <div class="history-item-result ${item.savings > 0 ? 'positive' : 'negative'}">
                        ${item.savings > 0 ? '💰 Economia' : '⚠️ Mais caro'}: 
                        R$ ${Math.abs(item.savings).toFixed(2)} (${Math.abs(item.savingsPercent)}%)
                    </div>
                </div>
            `).join('');
        }
        
        function deleteHistoryItem(index) {
            let history = JSON.parse(localStorage.getItem('comparapy_history') || '[]');
            history.splice(index, 1);
            localStorage.setItem('comparapy_history', JSON.stringify(history));
            loadHistory();
        }
        
        function clearHistory() {
            if (confirm('Tem certeza que deseja limpar todo o histórico?')) {
                localStorage.removeItem('comparapy_history');
                loadHistory();
            }
        }
    </script>
</body>
</html>
