# Loullie Store
index.html
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
    <title>Compara PY-BR - Comparador de Preços Completo</title>
    
    <link rel="icon" type="image/png" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Crect width='100' height='100' fill='%231e40af'/%3E%3Ctext x='50' y='60' font-size='50' fill='white' text-anchor='middle' font-family='Arial'%3E🛒%3C/text%3E%3C/svg%3E">
    
    <link rel="manifest" id="manifest-placeholder">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
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
        
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .header {
            background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
            color: white;
            padding: 25px 20px;
            text-align: center;
            position: relative;
        }
        
        .header h1 {
            font-size: 22px;
            margin-bottom: 5px;
        }
        
        .header .emoji {
            font-size: 32px;
            margin-bottom: 5px;
            display: block;
        }
        
        .header p {
            font-size: 13px;
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
        
        .install-banner {
            background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
            color: #78350f;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
            text-align: center;
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }
        
        .install-banner strong {
            display: block;
            font-size: 16px;
            margin-bottom: 5px;
        }
        
        .install-banner p {
            font-size: 13px;
            margin-bottom: 10px;
        }
        
        .install-banner button {
            background: white;
            color: #f59e0b;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            font-weight: 700;
            font-size: 14px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            transition: transform 0.2s;
        }
        
        .install-banner button:active {
            transform: scale(0.95);
        }
        
        .upload-section {
            border: 3px dashed #cbd5e1;
            border-radius: 15px;
            padding: 25px 20px;
            text-align: center;
            background: #f8fafc;
            margin-bottom: 20px;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
        }
        
        .upload-section:active {
            background: #eff6ff;
            border-color: #3b82f6;
        }
        
        .upload-section.has-image {
            padding: 15px;
            border-color: #10b981;
            background: #ecfdf5;
        }
        
        .upload-buttons {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 15px;
        }
        
        .upload-btn {
            flex: 1;
            padding: 12px;
            border: 2px solid #3b82f6;
            background: white;
            color: #3b82f6;
            border-radius: 10px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .upload-btn:active {
            background: #3b82f6;
            color: white;
        }
        
        .upload-icon {
            font-size: 48px;
            margin-bottom: 10px;
            display: block;
        }
        
        .upload-text {
            font-size: 15px;
            color: #1e293b;
            font-weight: 600;
            margin-bottom: 5px;
        }
        
        .upload-hint {
            font-size: 13px;
            color: #64748b;
        }
        
        input[type="file"] {
            display: none;
        }
        
        .preview-image {
            max-width: 100%;
            max-height: 250px;
            border-radius: 10px;
            margin-top: 10px;
            display: none;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }
        
        .remove-image {
            background: #ef4444;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 12px;
            margin-top: 10px;
            cursor: pointer;
            display: none;
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
            border: 2px solid #e2e8f0;
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s;
            background: white;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }
        
        .info-box {
            background: #f0f9ff;
            border-left: 4px solid #3b82f6;
            padding: 12px;
            border-radius: 8px;
            font-size: 13px;
            line-height: 1.6;
            color: #1e40af;
            margin-top: 8px;
        }
        
        .btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
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
            box-shadow: 0 2px 8px rgba(59, 130, 246, 0.4);
        }
        
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 30px 20px;
            animation: fadeIn 0.3s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .spinner {
            border: 4px solid #f3f4f6;
            border-top: 4px solid #3b82f6;
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
        
        .loading-text {
            color: #64748b;
            font-size: 14px;
        }
        
        .results {
            display: none;
            margin-top: 25px;
            animation: slideUp 0.5s ease-out;
        }
        
        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .result-card {
            background: #f8fafc;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }
        
        .result-card h3 {
            color: #1e40af;
            margin-bottom: 15px;
            font-size: 17px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .price-row {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #e2e8f0;
        }
        
        .price-row:last-child {
            border-bottom: none;
            padding-bottom: 0;
        }
        
        .price-label {
            color: #64748b;
            font-size: 14px;
        }
        
        .price-value {
            font-weight: 700;
            color: #1e293b;
            font-size: 15px;
        }
        
        .conversion-info {
            background: #fef3c7;
            padding: 12px;
            border-radius: 8px;
            margin-top: 12px;
            font-size: 12px;
            color: #78350f;
        }
        
        .savings {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            margin-top: 15px;
            font-weight: 700;
            font-size: 18px;
            box-shadow: 0 4px 14px rgba(16, 185, 129, 0.4);
        }
        
        .savings.negative {
            background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
            box-shadow: 0 4px 14px rgba(239, 68, 68, 0.4);
        }
        
        .savings-subtitle {
            font-size: 13px;
            margin-top: 5px;
            opacity: 0.95;
            font-weight: 500;
        }
        
        .tax-info {
            background: #fff7ed;
            border-left: 4px solid #f59e0b;
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
            font-size: 13px;
            line-height: 1.6;
        }
        
        .tax-info strong {
            display: block;
            margin-bottom: 8px;
            color: #92400e;
        }
        
        .regime-highlight {
            background: #dcfce7;
            border-left: 4px solid #10b981;
            padding: 12px;
            border-radius: 8px;
            margin-top: 12px;
            font-size: 13px;
            color: #166534;
        }
        
        .product-info {
            background: linear-gradient(135deg, #eff6ff 0%, #dbeafe 100%);
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 15px;
        }
        
        .product-info h4 {
            color: #1e40af;
            margin-bottom: 8px;
            font-size: 15px;
        }
        
        .product-info p {
            color: #1e293b;
            font-size: 14px;
        }
        
        .footer {
            text-align: center;
            padding: 20px;
            color: white;
            font-size: 12px;
            opacity: 0.8;
        }
        
        .quick-tips {
            background: #f0f9ff;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 20px;
            border-left: 4px solid #3b82f6;
        }
        
        .quick-tips h4 {
            color: #1e40af;
            font-size: 14px;
            margin-bottom: 8px;
        }
        
        .quick-tips ul {
            margin-left: 20px;
            font-size: 13px;
            color: #475569;
            line-height: 1.8;
        }
        
        .exchange-rates {
            background: #f8fafc;
            border-radius: 10px;
            padding: 12px;
            margin-bottom: 15px;
            font-size: 12px;
        }
        
        .exchange-rates h5 {
            color: #1e40af;
            margin-bottom: 8px;
            font-size: 13px;
        }
        
        .rate-item {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
            color: #64748b;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <span class="version-badge">v2.0</span>
            <span class="emoji">🛒</span>
            <h1>Compara PY-BR PRO</h1>
            <p>Comparador Completo com Regimes Especiais</p>
        </div>
        
        <div class="content">
            <div id="installBanner" class="install-banner" style="display: none;">
                <strong>📱 Instale o App!</strong>
                <p>Use como aplicativo nativo no seu celular</p>
                <button id="installBtn">🚀 Instalar Agora</button>
            </div>
            
            <div class="quick-tips">
                <h4>💡 Novidades v2.0:</h4>
                <ul>
                    <li>✅ Importar imagens da galeria</li>
                    <li>✅ Conversão Guarani, Dólar e Real</li>
                    <li>✅ Regimes tributários especiais</li>
                    <li>✅ Cálculos precisos PF e PJ</li>
                </ul>
            </div>
            
            <div class="exchange-rates">
                <h5>💱 Taxas de Câmbio Atuais:</h5>
                <div class="rate-item">
                    <span>1 US$ =</span>
                    <span><strong>R$ 5,85</strong></span>
                </div>
                <div class="rate-item">
                    <span>1 ₲ =</span>
                    <span><strong>R$ 0,00070</strong></span>
                </div>
                <div class="rate-item">
                    <span>1 US$ =</span>
                    <span><strong>₲ 8.357</strong></span>
                </div>
            </div>
            
            <div class="upload-section" id="uploadSection">
                <div id="uploadPrompt">
                    <span class="upload-icon">📸</span>
                    <p class="upload-text">Adicionar Foto do Produto</p>
                    <p class="upload-hint">Escolha uma opção abaixo:</p>
                    <div class="upload-buttons">
                        <button class="upload-btn" id="cameraBtn">📷 Câmera</button>
                        <button class="upload-btn" id="galleryBtn">🖼️ Galeria</button>
                    </div>
                </div>
                <input type="file" id="fileInputCamera" accept="image/*" capture="environment">
                <input type="file" id="fileInputGallery" accept="image/*">
                <img id="previewImage" class="preview-image" alt="Preview">
                <button id="removeImageBtn" class="remove-image">❌ Remover Foto</button>
            </div>
            
            <div class="form-group">
                <label for="currency">💱 Moeda do Preço:</label>
                <select id="currency">
                    <option value="guarani">Guarani Paraguaio (₲)</option>
                    <option value="dolar">Dólar Americano (US$)</option>
                    <option value="real">Real Brasileiro (R$)</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="productPrice" id="priceLabel">💵 Preço (₲):</label>
                <input type="number" id="productPrice" placeholder="Ex: 150000" step="0.01" inputmode="decimal">
            </div>
            
            <div class="form-group">
                <label for="productName">📦 Nome do Produto:</label>
                <input type="text" id="productName" placeholder="Ex: Notebook Dell Inspiron 15">
            </div>
            
            <div class="form-group">
                <label for="personType">👤 Tipo de Pessoa:</label>
                <select id="personType">
                    <option value="fisica">Pessoa Física</option>
                    <option value="juridica">Pessoa Jurídica (Simples Nacional)</option>
                </select>
            </div>
            
            <div class="form-group" id="specialRegimeGroup">
                <label for="specialRegime">🎯 Regime Tributário Especial:</label>
                <select id="specialRegime">
                    <option value="none">Regime Normal (60% II)</option>
                    <option value="remessaconforme">Remessa Conforme (até US$ 3.000 - 17%)</option>
                    <option value="courier">Courier/Importação Expressa (60% + taxas)</option>
                    <option value="drawback">Drawback - Suspensão (PJ)</option>
                    <option value="zona_franca">Zona Franca de Manaus</option>
                    <option value="ex_tarifario">Ex-Tarifário (Redução II)</option>
                    <option value="isencao">Isenção (Bagagem até US$ 1.000)</option>
                </select>
                <div class="info-box" id="regimeInfo"></div>
            </div>
            
            <button class="btn" id="compareBtn">🔍 Comparar Agora</button>
            
            <div class="loading" id="loading">
                <div class="spinner"></div>
                <p class="loading-text">Analisando produto e calculando impostos...</p>
            </div>
            
            <div class="results" id="results">
                <div id="productInfoDiv" class="product-info">
                    <h4>✅ Produto Analisado:</h4>
                    <p id="detectedProduct"></p>
                </div>
                
                <div class="conversion-info" id="conversionInfo"></div>
                
                <div class="result-card">
                    <h3>🇵🇾 Custo Total no Paraguai</h3>
                    <div class="price-row">
                        <span class="price-label">Preço original:</span>
                        <span class="price-value" id="priceOriginal">-</span>
                    </div>
                    <div class="price-row">
                        <span class="price-label">Preço em Real (R$):</span>
                        <span class="price-value" id="priceBRL">-</span>
                    </div>
                    <div class="price-row" id="taxRow">
                        <span class="price-label">Impostos:</span>
                        <span class="price-value" id="taxAmount">-</span>
                    </div>
                    <div class="price-row">
                        <span class="price-label"><strong>💰 TOTAL FINAL:</strong></span>
                        <span class="price-value" style="color: #1e40af; font-size: 17px;" id="totalParaguai">-</span>
                    </div>
                </div>
                
                <div id="regimeHighlight" class="regime-highlight" style="display: none;"></div>
                
                <div class="result-card">
                    <h3>🇧🇷 Preço no Brasil</h3>
                    <div class="price-row">
                        <span class="price-label">Preço estimado:</span>
                        <span class="price-value" style="color: #dc2626;" id="priceBrazil">-</span>
                    </div>
                    <p style="font-size: 12px; color: #64748b; margin-top: 12px; font-style: italic;">
                        * Estimativa baseada em produtos similares no mercado brasileiro
                    </p>
                </div>
                
                <div class="savings" id="savingsDiv">
                    <div id="savingsText"></div>
                </div>
                
                <div class="tax-info">
                    <strong>ℹ️ Informação Tributária Completa:</strong>
                    <p id="taxInfo"></p>
                </div>
            </div>
        </div>
    </div>
    
    <div class="footer">
        Compara PY-BR PRO v2.0 | Feito com 💙 para economizar
    </div>

    <script>
        // Configuração do manifest dinamicamente
        const manifestData = {
            name: "Compara PY-BR PRO",
            short_name: "ComparaPY",
            description: "Comparador Completo de Preços Paraguai x Brasil",
            start_url: window.location.href,
            display: "standalone",
            background_color: "#ffffff",
            theme_color: "#1e40af",
            orientation: "portrait",
            icons: [
                {
                    src: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'%3E%3Crect width='512' height='512' fill='%231e40af' rx='100'/%3E%3Ctext x='256' y='340' font-size='280' fill='white' text-anchor='middle' font-family='Arial'%3E🛒%3C/text%3E%3C/svg%3E",
                    sizes: "512x512",
                    type: "image/svg+xml",
                    purpose: "any maskable"
                }
            ]
        };
        
        const manifestBlob = new Blob([JSON.stringify(manifestData)], { type: 'application/json' });
        const manifestURL = URL.createObjectURL(manifestBlob);
        document.getElementById('manifest-placeholder').setAttribute('href', manifestURL);

        // Service Worker
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                const swCode = `
                    self.addEventListener('install', e => {
                        e.waitUntil(self.skipWaiting());
                    });
                    self.addEventListener('activate', e => {
                        e.waitUntil(self.clients.claim());
                    });
                    self.addEventListener('fetch', e => {
                        e.respondWith(fetch(e.request));
                    });
                `;
                const swBlob = new Blob([swCode], { type: 'application/javascript' });
                const swURL = URL.createObjectURL(swBlob);
                navigator.serviceWorker.register(swURL);
            });
        }

        // Variáveis globais
        let deferredPrompt;
        const fileInputCamera = document.getElementById('fileInputCamera');
        const fileInputGallery = document.getElementById('fileInputGallery');
        const cameraBtn = document.getElementById('cameraBtn');
        const galleryBtn = document.getElementById('galleryBtn');
        const previewImage = document.getElementById('previewImage');
        const removeImageBtn = document.getElementById('removeImageBtn');
        const compareBtn = document.getElementById('compareBtn');
        const loading = document.getElementById('loading');
        const results = document.getElementById('results');
        const currencySelect = document.getElementById('currency');
        const priceLabel = document.getElementById('priceLabel');
        const personTypeSelect = document.getElementById('personType');
        const specialRegimeSelect = document.getElementById('specialRegime');
        const regimeInfo = document.getElementById('regimeInfo');
        
        // Taxas de câmbio (Fevereiro 2026)
        const EXCHANGE_RATES = {
            USD_TO_BRL: 5.85,
            GUARANI_TO_BRL: 0.00070,
            USD_TO_GUARANI: 8357
        };
        
        // Instalação PWA
        window.addEventListener('beforeinstallprompt', (e) => {
            e.preventDefault();
            deferredPrompt = e;
            document.getElementById('installBanner').style.display = 'block';
        });
        
        document.getElementById('installBtn').addEventListener('click', async () => {
            if (deferredPrompt) {
                deferredPrompt.prompt();
                const { outcome } = await deferredPrompt.userChoice;
                if (outcome === 'accepted') {
                    document.getElementById('installBanner').style.display = 'none';
                }
                deferredPrompt = null;
            } else {
                alert('📱 Para instalar:\n\n1. Toque nos 3 pontinhos (⋮) no Chrome\n2. Selecione "Adicionar à tela inicial"\n3. Confirme a instalação\n\nOu use o menu "Compartilhar" → "Adicionar à Tela de Início"');
            }
        });
        
        // Upload de imagem - Câmera
        cameraBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            fileInputCamera.click();
        });
        
        // Upload de imagem - Galeria
        galleryBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            fileInputGallery.click();
        });
        
        fileInputCamera.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) handleImageUpload(file);
        });
        
        fileInputGallery.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) handleImageUpload(file);
        });
        
        removeImageBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            previewImage.style.display = 'none';
            removeImageBtn.style.display = 'none';
            document.getElementById('uploadPrompt').style.display = 'block';
            fileInputCamera.value = '';
            fileInputGallery.value = '';
        });
        
        function handleImageUpload(file) {
            const reader = new FileReader();
            reader.onload = (e) => {
                previewImage.src = e.target.result;
                previewImage.style.display = 'block';
                removeImageBtn.style.display = 'inline-block';
                document.getElementById('uploadPrompt').style.display = 'none';
            };
            reader.readAsDataURL(file);
        }
        
        // Atualizar label do preço conforme moeda
        currencySelect.addEventListener('change', () => {
            const currency = currencySelect.value;
            const labels = {
                'guarani': '💵 Preço (₲):',
                'dolar': '💵 Preço (US$):',
                'real': '💵 Preço (R$):'
            };
            priceLabel.textContent = labels[currency];
            
            const placeholders = {
                'guarani': 'Ex: 150000',
                'dolar': 'Ex: 250.00',
                'real': 'Ex: 1200.00'
            };
            document.getElementById('productPrice').placeholder = placeholders[currency];
        });
        
        // Mostrar informações de regime
        specialRegimeSelect.addEventListener('change', () => {
            const regime = specialRegimeSelect.value;
            const personType = personTypeSelect.value;
            
            const regimeInfos = {
                'none': 'Regime normal de importação com Imposto de Importação padrão de 60%.',
                'remessaconforme': 'Remessa Conforme: Alíquota reduzida de 17% para compras até US$ 3.000. Válido apenas para compras via e-commerce com empresas cadastradas no programa.',
                'courier': 'Importação expressa via Courier: 60% de II + taxas de ICMS estadual (7-18%). Processo mais rápido mas custos adicionais.',
                'drawback': personType === 'juridica' ? 'Drawback: Suspensão ou isenção de impostos para empresas que exportam. Necessário comprovar exportação posterior.' : 'Drawback disponível apenas para Pessoa Jurídica.',
                'zona_franca': 'Zona Franca de Manaus: Incentivos fiscais especiais. Produtos fabricados na ZFM têm isenção ou redução de impostos.',
                'ex_tarifario': personType === 'juridica' ? 'Ex-Tarifário: Redução temporária da alíquota do II para bens de capital, informática ou telecomunicações sem produção nacional. Requer aprovação CAMEX.' : 'Ex-Tarifário disponível apenas para Pessoa Jurídica.',
                'isencao': 'Isenção de bagagem: Até US$ 1.000 via terrestre para pessoa física. Acima desse valor, aplica-se 60% de II sobre o excedente.'
            };
            
            regimeInfo.textContent = regimeInfos[regime] || '';
            regimeInfo.style.display = regime === 'none' ? 'none' : 'block';
        });
        
        // Converter preço para BRL
        function convertToBRL(price, currency) {
            switch(currency) {
                case 'guarani':
                    return price * EXCHANGE_RATES.GUARANI_TO_BRL;
                case 'dolar':
                    return price * EXCHANGE_RATES.USD_TO_BRL;
                case 'real':
                    return price;
                default:
                    return price;
            }
        }
        
        // Calcular impostos baseado no regime
        function calculateTaxes(priceBRL, priceUSD, personType, regime) {
            let taxRate = 0;
            let taxAmount = 0;
            let taxDescription = '';
            let regimeUsed = '';
            
            if (regime === 'remessaconforme' && priceUSD <= 3000) {
                taxRate = 0.17;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Remessa Conforme (17%)';
                regimeUsed = '✅ Regime Especial Aplicado: Remessa Conforme com alíquota reduzida de 17%';
            } else if (regime === 'isencao' && personType === 'fisica' && priceUSD <= 1000) {
                taxRate = 0;
                taxAmount = 0;
                taxDescription = 'Isento (Bagagem)';
                regimeUsed = '✅ Isenção Aplicada: Produto dentro do limite de US$ 1.000 para bagagem';
            } else if (regime === 'drawback' && personType === 'juridica') {
                taxRate = 0;
                taxAmount = 0;
                taxDescription = 'Drawback (Suspensão)';
                regimeUsed = '✅ Regime Drawback: Suspensão de impostos mediante comprovação de exportação';
            } else if (regime === 'ex_tarifario' && personType === 'juridica') {
                taxRate = 0.02;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Ex-Tarifário (2%)';
                regimeUsed = '✅ Ex-Tarifário Aplicado: Alíquota reduzida para bens de capital sem similar nacional';
            } else if (regime === 'zona_franca') {
                taxRate = 0.20;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Zona Franca (20%)';
                regimeUsed = '✅ Incentivo Zona Franca: Redução significativa nos impostos';
            } else {
                // Regime normal
                taxRate = 0.60;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Imposto Importação (60%)';
                
                if (personType === 'juridica') {
                    // Adicionar estimativa de ICMS
                    const icmsRate = 0.12; // média 12%
                    const icmsAmount = priceBRL * icmsRate;
                    taxAmount += icmsAmount;
                    taxDescription = 'II (60%) + ICMS (~12%)';
                }
            }
            
            return { taxRate, taxAmount, taxDescription, regimeUsed };
        }
        
        // Simulação de análise de imagem
        async function analyzeImage(imageData) {
            await new Promise(resolve => setTimeout(resolve, 1500));
            const productName = document.getElementById('productName').value;
            
            if (productName) {
                return {
                    name: productName,
                    category: detectCategory(productName),
                    confidence: 0.85
                };
            }
            
            return {
                name: 'Produto detectado na imagem',
                category: 'geral',
                confidence: 0.75
            };
        }
        
        function detectCategory(name) {
            const lowerName = name.toLowerCase();
            if (lowerName.includes('notebook') || lowerName.includes('laptop')) return 'eletrônicos';
            if (lowerName.includes('celular') || lowerName.includes('smartphone')) return 'eletrônicos';
            if (lowerName.includes('perfume') || lowerName.includes('fragrância')) return 'perfumaria';
            if (lowerName.includes('whisky') || lowerName.includes('vinho')) return 'bebidas';
            return 'geral';
        }
        
        // Simulação de busca de preços
        async function searchBrazilPrice(productName, priceBRL) {
            await new Promise(resolve => setTimeout(resolve, 1200));
            
            const priceMultipliers = {
                'notebook': 2.8,
                'laptop': 2.8,
                'celular': 2.5,
                'smartphone': 2.5,
                'iphone': 3.0,
                'samsung': 2.4,
                'tablet': 2.3,
                'ipad': 2.6,
                'fone': 2.0,
                'headphone': 2.2,
                'mouse': 1.8,
                'teclado': 1.9,
                'monitor': 2.4,
                'tv': 2.3,
                'playstation': 2.5,
                'xbox': 2.5,
                'nintendo': 2.4,
                'perfume': 2.8,
                'whisky': 2.5,
                'default': 2.2
            };
            
            let multiplier = priceMultipliers.default;
            const lowerName = productName.toLowerCase();
            
            for (const [key, value] of Object.entries(priceMultipliers)) {
                if (lowerName.includes(key)) {
                    multiplier = value;
                    break;
                }
            }
            
            return priceBRL * multiplier;
        }
        
        // Comparação de preços
        compareBtn.addEventListener('click', async () => {
            const price = parseFloat(document.getElementById('productPrice').value);
            const currency = currencySelect.value;
            const personType = personTypeSelect.value;
            const regime = specialRegimeSelect.value;
            const productName = document.getElementById('productName').value || 'Produto';
            
            if (!price || price <= 0) {
                alert('⚠️ Por favor, insira um preço válido!');
                return;
            }
            
            if (!productName.trim() || productName === 'Produto') {
                alert('⚠️ Por favor, informe o nome do produto para uma comparação mais precisa!');
                return;
            }
            
            // Mostrar loading
            compareBtn.disabled = true;
            loading.style.display = 'block';
            results.style.display = 'none';
            
            try {
                // Analisar imagem se houver
                let detectedProduct = productName;
                if (previewImage.src && previewImage.style.display === 'block') {
                    const analysis = await analyzeImage(previewImage.src);
                    detectedProduct = analysis.name;
                }
                
                // Converter para BRL e USD
                const priceBRL = convertToBRL(price, currency);
                const priceUSD = priceBRL / EXCHANGE_RATES.USD_TO_BRL;
                
                // Calcular impostos
                const { taxAmount, taxDescription, regimeUsed } = calculateTaxes(priceBRL, priceUSD, personType, regime);
                const totalParaguai = priceBRL + taxAmount;
                
                // Buscar preço no Brasil
                const priceBrazil = await searchBrazilPrice(detectedProduct, priceBRL);
                
                // Calcular economia
                const savings = priceBrazil - totalParaguai;
                const savingsPercent = ((savings / priceBrazil) * 100).toFixed(1);
                
                // Mostrar conversão
                const currencySymbols = {
                    'guarani': '₲',
                    'dolar': 'US$',
                    'real': 'R$'
                };
                
                let conversionText = '';
                if (currency === 'guarani') {
                    conversionText = `Conversão: ₲ ${price.toLocaleString('pt-BR')} = R$ ${priceBRL.toFixed(2)} = US$ ${priceUSD.toFixed(2)}`;
                } else if (currency === 'dolar') {
                    conversionText = `Conversão: US$ ${price.toFixed(2)} = R$ ${priceBRL.toFixed(2)} = ₲ ${(price * EXCHANGE_RATES.USD_TO_GUARANI).toLocaleString('pt-BR')}`;
                } else {
                    conversionText = `Valor em Real: R$ ${price.toFixed(2)} = US$ ${priceUSD.toFixed(2)} = ₲ ${(priceUSD * EXCHANGE_RATES.USD_TO_GUARANI).toLocaleString('pt-BR')}`;
                }
                
                document.getElementById('conversionInfo').textContent = conversionText;
                
                // Mostrar resultados
                document.getElementById('detectedProduct').textContent = detectedProduct;
                document.getElementById('priceOriginal').textContent = `${currencySymbols[currency]} ${price.toLocaleString('pt-BR', {minimumFractionDigits: 2})}`;
                document.getElementById('priceBRL').textContent = `R$ ${priceBRL.toFixed(2)}`;
                document.getElementById('taxAmount').textContent = `R$ ${taxAmount.toFixed(2)} (${taxDescription})`;
                document.getElementById('totalParaguai').textContent = `R$ ${totalParaguai.toFixed(2)}`;
                document.getElementById('priceBrazil').textContent = `R$ ${priceBrazil.toFixed(2)}`;
                
                // Mostrar regime especial se aplicado
                const regimeHighlight = document.getElementById('regimeHighlight');
                if (regimeUsed) {
                    regimeHighlight.textContent = regimeUsed;
                    regimeHighlight.style.display = 'block';
                } else {
                    regimeHighlight.style.display = 'none';
                }
                
                // Informação tributária completa
                let taxInfoText = '';
                if (personType === 'fisica') {
                    if (regime === 'isencao' && priceUSD <= 1000) {
                        taxInfoText = `<strong>Pessoa Física - Isenção:</strong> Seu produto está dentro do limite de isenção de bagagem (US$ 1.000 via terrestre). Não há impostos a pagar! Mantenha a nota fiscal e documente a compra.`;
                    } else if (regime === 'remessaconforme' && priceUSD <= 3000) {
                        taxInfoText = `<strong>Pessoa Física - Remessa Conforme:</strong> Alíquota reduzida de 17% aplicada. Válido para compras de até US$ 3.000 em sites cadastrados. Economia significativa comparada aos 60% tradicionais!`;
                    } else {
                        taxInfoText = `<strong>Pessoa Física - Regime Normal:</strong> Imposto de Importação de 60% sobre o valor do produto. Compras acima de US$ 1.000 ou em quantidades comerciais podem exigir declaração e fiscalização adicional na alfândega. Limite de isenção: US$ 500 por via terrestre (atualização 2024).`;
                    }
                } else {
                    if (regime === 'drawback') {
                        taxInfoText = `<strong>Pessoa Jurídica - Drawback:</strong> Suspensão de impostos mediante comprovação de exportação. Ideal para empresas que importam insumos e exportam produtos acabados. Necessário processo junto à Receita Federal.`;
                    } else if (regime === 'ex_tarifario') {
                        taxInfoText = `<strong>Pessoa Jurídica - Ex-Tarifário:</strong> Alíquota reduzida do Imposto de Importação para bens de capital, informática ou telecomunicações sem produção nacional equivalente. Requer aprovação da CAMEX. Válido por até 2 anos.`;
                    } else {
                        taxInfoText = `<strong>Pessoa Jurídica (Simples Nacional):</strong> Imposto de Importação de 60% + ICMS estadual (média de 12%, varia de 7% a 18% por estado). É necessário formalizar a importação com nota fiscal e registro no SISCOMEX. Considere também custos de transporte, armazenagem e despachante aduaneiro. Empresas no Simples não podem aproveitar créditos de ICMS.`;
                    }
                }
                
                document.getElementById('taxInfo').innerHTML = taxInfoText;
                
                // Calcular economia
                const savingsDiv = document.getElementById('savingsDiv');
                const savingsText = document.getElementById('savingsText');
                
                if (savings > 0) {
                    savingsDiv.classList.remove('negative');
                    savingsText.innerHTML = `
                        💰 ECONOMIA DE R$ ${savings.toFixed(2)}
                        <div class="savings-subtitle">Você economiza ${savingsPercent}% comprando no Paraguai! ✅</div>
                    `;
                } else {
                    savingsDiv.classList.add('negative');
                    savingsText.innerHTML = `
                        ⚠️ NÃO VALE A PENA
                        <div class="savings-subtitle">Você pagaria R$ ${Math.abs(savings).toFixed(2)} a mais no Paraguai</div>
                    `;
                }
                
                results.style.display = 'block';
                results.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
                
            } catch (error) {
                alert('❌ Erro ao processar: ' + error.message);
            } finally {
                compareBtn.disabled = false;
                loading.style.display = 'none';
            }
        });
        
        // Vibração de feedback
        function vibrate(duration = 50) {
            if ('vibrate' in navigator) {
                navigator.vibrate(duration);
            }
        }
        
        compareBtn.addEventListener('click', () => vibrate(30));
        cameraBtn.addEventListener('click', () => vibrate(20));
        galleryBtn.addEventListener('click', () => vibrate(20));
    </script>
</body>
</html>
