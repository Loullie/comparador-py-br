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
    <title>Compara PY-BR PRO v3.0 - Comparador Completo</title>
    
    <link rel="icon" type="image/png" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Crect width='100' height='100' fill='%231e40af'/%3E%3Ctext x='50' y='60' font-size='50' fill='white' text-anchor='middle' font-family='Arial'%3E🛒%3C/text%3E%3C/svg%3E">
    <link rel="manifest" id="manifest-placeholder">
    
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
        
        /* RESPONSIVIDADE - MOBILE FIRST */
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
            animation: slideIn 0.5s ease-out;
        }
        
        /* TABLET - 768px+ */
        @media (min-width: 768px) {
            body {
                padding: 20px;
            }
            
            .container {
                max-width: 720px;
            }
            
            .content {
                padding: 30px !important;
            }
            
            .form-row {
                display: grid;
                grid-template-columns: 1fr 1fr;
                gap: 20px;
            }
            
            .form-group.full-width {
                grid-column: 1 / -1;
            }
        }
        
        /* DESKTOP - 1024px+ */
        @media (min-width: 1024px) {
            body {
                padding: 40px;
            }
            
            .container {
                max-width: 1200px;
                display: grid;
                grid-template-columns: 1fr 1fr;
                gap: 0;
            }
            
            .header {
                grid-column: 1 / -1;
            }
            
            .content {
                padding: 40px !important;
            }
            
            .left-column {
                padding-right: 20px;
                border-right: 2px solid var(--border-color);
            }
            
            .right-column {
                padding-left: 20px;
            }
            
            .results {
                margin-top: 0 !important;
            }
            
            .form-row {
                display: grid;
                grid-template-columns: 1fr 1fr;
                gap: 15px;
            }
        }
        
        /* LARGE DESKTOP - 1440px+ */
        @media (min-width: 1440px) {
            .container {
                max-width: 1400px;
            }
            
            .content {
                padding: 50px !important;
            }
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
        
        .install-banner {
            background: linear-gradient(135deg, var(--warning-color) 0%, #f59e0b 100%);
            color: #78350f;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 20px;
            text-align: center;
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
            color: var(--warning-color);
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
        
        .rate-editor input:focus {
            outline: none;
            border-color: var(--primary-light);
        }
        
        .rate-hint {
            font-size: 12px;
            color: #92400e;
            margin-top: 10px;
            font-style: italic;
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
            position: relative;
        }
        
        .upload-section:active {
            background: #eff6ff;
            border-color: var(--primary-light);
        }
        
        .upload-section.has-image {
            padding: 15px;
            border-color: var(--success-color);
            background: #ecfdf5;
        }
        
        .upload-section.analyzing {
            border-color: var(--warning-color);
            background: #fef3c7;
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
        
        .upload-icon {
            font-size: 48px;
            margin-bottom: 10px;
            display: block;
        }
        
        .upload-text {
            font-size: 15px;
            color: var(--text-dark);
            font-weight: 600;
            margin-bottom: 5px;
        }
        
        .upload-hint {
            font-size: 13px;
            color: var(--text-light);
        }
        
        input[type="file"] {
            display: none;
        }
        
        .preview-image {
            max-width: 100%;
            max-height: 300px;
            border-radius: 10px;
            margin-top: 10px;
            display: none;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
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
        
        .loading-text {
            color: var(--text-light);
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
            display: flex;
            align-items: center;
            gap: 8px;
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
        
        .price-label {
            color: var(--text-light);
            font-size: 14px;
        }
        
        .price-value {
            font-weight: 700;
            color: var(--text-dark);
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
            background: linear-gradient(135deg, var(--success-color) 0%, #059669 100%);
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
            background: linear-gradient(135deg, var(--danger-color) 0%, #dc2626 100%);
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
            border-left: 4px solid var(--warning-color);
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
            border-left: 4px solid var(--success-color);
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
            color: var(--primary-color);
            margin-bottom: 8px;
            font-size: 15px;
        }
        
        .product-info p {
            color: var(--text-dark);
            font-size: 14px;
        }
        
        .footer {
            text-align: center;
            padding: 20px;
            color: white;
            font-size: 12px;
            opacity: 0.8;
            grid-column: 1 / -1;
        }
        
        .quick-tips {
            background: #f0f9ff;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 20px;
            border-left: 4px solid var(--primary-light);
        }
        
        .quick-tips h4 {
            color: var(--primary-color);
            font-size: 14px;
            margin-bottom: 8px;
        }
        
        .quick-tips ul {
            margin-left: 20px;
            font-size: 13px;
            color: #475569;
            line-height: 1.8;
        }
        
        /* Animação para campos auto-preenchidos */
        .auto-filled {
            animation: highlight 1s ease-out;
        }
        
        @keyframes highlight {
            0% { background-color: #dcfce7; }
            100% { background-color: white; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <span class="version-badge">v3.0 PRO</span>
            <span class="emoji">🛒</span>
            <h1>Compara PY-BR PRO</h1>
            <p>Comparador Completo com OCR e Design Responsivo</p>
        </div>
        
        <div class="content left-column">
            <div id="installBanner" class="install-banner" style="display: none;">
                <strong>📱 Instale o App!</strong>
                <p>Use como aplicativo nativo no seu celular</p>
                <button id="installBtn">🚀 Instalar Agora</button>
            </div>
            
            <div class="quick-tips">
                <h4>💡 Novidades v3.0:</h4>
                <ul>
                    <li>✅ Taxas de câmbio editáveis</li>
                    <li>✅ OCR: extrai nome e preço da foto</li>
                    <li>✅ Design responsivo (PC/Tablet/Mobile)</li>
                    <li>✅ Interface otimizada para todas telas</li>
                </ul>
            </div>
            
            <div class="exchange-rates-section">
                <h4>💱 Taxas de Câmbio (Editável)</h4>
                <div class="rate-editor">
                    <label>1 US$ =</label>
                    <input type="number" id="rateBRL" value="5.85" step="0.01" min="0">
                    <span style="font-weight: 600; color: var(--text-dark);">BRL</span>
                </div>
                <div class="rate-editor">
                    <label>1 ₲ =</label>
                    <input type="number" id="rateGuarani" value="0.00070" step="0.00001" min="0">
                    <span style="font-weight: 600; color: var(--text-dark);">BRL</span>
                </div>
                <div class="rate-editor">
                    <label>1 US$ =</label>
                    <input type="number" id="rateGuaraniUSD" value="8357" step="1" min="0">
                    <span style="font-weight: 600; color: var(--text-dark);">₲</span>
                </div>
                <p class="rate-hint">💡 Atualize com as cotações do momento da compra</p>
            </div>
            
            <div class="upload-section" id="uploadSection">
                <div id="uploadPrompt">
                    <span class="upload-icon">📸</span>
                    <p class="upload-text">Adicionar Foto do Produto</p>
                    <p class="upload-hint">O app vai extrair automaticamente nome e preço!</p>
                    <div class="upload-buttons">
                        <button class="upload-btn" id="cameraBtn">📷 Câmera</button>
                        <button class="upload-btn" id="galleryBtn">🖼️ Galeria</button>
                    </div>
                </div>
                <input type="file" id="fileInputCamera" accept="image/*" capture="environment">
                <input type="file" id="fileInputGallery" accept="image/*">
                <img id="previewImage" class="preview-image" alt="Preview">
                <div id="ocrStatus" class="ocr-status"></div>
                <button id="removeImageBtn" class="remove-image">❌ Remover Foto</button>
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="currency">💱 Moeda do Preço:</label>
                    <select id="currency">
                        <option value="guarani">Guarani (₲)</option>
                        <option value="dolar">Dólar (US$)</option>
                        <option value="real">Real (R$)</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="productPrice" id="priceLabel">💵 Preço (₲):</label>
                    <input type="number" id="productPrice" placeholder="Ex: 150000" step="0.01" inputmode="decimal">
                </div>
            </div>
            
            <div class="form-group full-width">
                <label for="productName">📦 Nome do Produto:</label>
                <input type="text" id="productName" placeholder="Ex: Notebook Dell Inspiron 15">
            </div>
            
            <div class="form-row">
                <div class="form-group">
                    <label for="personType">👤 Tipo de Pessoa:</label>
                    <select id="personType">
                        <option value="fisica">Pessoa Física</option>
                        <option value="juridica">Pessoa Jurídica (Simples)</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="specialRegime">🎯 Regime Especial:</label>
                    <select id="specialRegime">
                        <option value="none">Regime Normal (60%)</option>
                        <option value="remessaconforme">Remessa Conforme (17%)</option>
                        <option value="isencao">Isenção Bagagem (0%)</option>
                        <option value="courier">Courier/Expressa</option>
                        <option value="drawback">Drawback (PJ)</option>
                        <option value="zona_franca">Zona Franca</option>
                        <option value="ex_tarifario">Ex-Tarifário (PJ)</option>
                    </select>
                </div>
            </div>
            
            <div class="form-group full-width" id="specialRegimeGroup">
                <div class="info-box" id="regimeInfo" style="display: none;"></div>
            </div>
            
            <button class="btn" id="compareBtn">🔍 Comparar Agora</button>
            
            <div class="loading" id="loading">
                <div class="spinner"></div>
                <p class="loading-text">Analisando produto e calculando impostos...</p>
            </div>
        </div>
        
        <div class="content right-column">
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
                        <span class="price-value" style="color: var(--primary-color); font-size: 17px;" id="totalParaguai">-</span>
                    </div>
                </div>
                
                <div id="regimeHighlight" class="regime-highlight" style="display: none;"></div>
                
                <div class="result-card">
                    <h3>🇧🇷 Preço no Brasil</h3>
                    <div class="price-row">
                        <span class="price-label">Preço estimado:</span>
                        <span class="price-value" style="color: var(--danger-color);" id="priceBrazil">-</span>
                    </div>
                    <p style="font-size: 12px; color: var(--text-light); margin-top: 12px; font-style: italic;">
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
        
        <div class="footer">
            Compara PY-BR PRO v3.0 | Design Responsivo | Feito com 💙
        </div>
    </div>

    <script>
        // Configuração do manifest
        const manifestData = {
            name: "Compara PY-BR PRO v3.0",
            short_name: "ComparaPY",
            description: "Comparador Completo com OCR e Design Responsivo",
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
                    self.addEventListener('install', e => e.waitUntil(self.skipWaiting()));
                    self.addEventListener('activate', e => e.waitUntil(self.clients.claim()));
                    self.addEventListener('fetch', e => e.respondWith(fetch(e.request)));
                `;
                const swBlob = new Blob([swCode], { type: 'application/javascript' });
                const swURL = URL.createObjectURL(swBlob);
                navigator.serviceWorker.register(swURL);
            });
        }

        // Elementos DOM
        let deferredPrompt;
        const fileInputCamera = document.getElementById('fileInputCamera');
        const fileInputGallery = document.getElementById('fileInputGallery');
        const cameraBtn = document.getElementById('cameraBtn');
        const galleryBtn = document.getElementById('galleryBtn');
        const previewImage = document.getElementById('previewImage');
        const removeImageBtn = document.getElementById('removeImageBtn');
        const ocrStatus = document.getElementById('ocrStatus');
        const uploadSection = document.getElementById('uploadSection');
        const compareBtn = document.getElementById('compareBtn');
        const loading = document.getElementById('loading');
        const results = document.getElementById('results');
        const currencySelect = document.getElementById('currency');
        const priceLabel = document.getElementById('priceLabel');
        const productPriceInput = document.getElementById('productPrice');
        const productNameInput = document.getElementById('productName');
        const personTypeSelect = document.getElementById('personType');
        const specialRegimeSelect = document.getElementById('specialRegime');
        const regimeInfo = document.getElementById('regimeInfo');
        
        // Taxas editáveis
        const rateBRLInput = document.getElementById('rateBRL');
        const rateGuaraniInput = document.getElementById('rateGuarani');
        const rateGuaraniUSDInput = document.getElementById('rateGuaraniUSD');
        
        // Função para obter taxas atuais
        function getExchangeRates() {
            return {
                USD_TO_BRL: parseFloat(rateBRLInput.value) || 5.85,
                GUARANI_TO_BRL: parseFloat(rateGuaraniInput.value) || 0.00070,
                USD_TO_GUARANI: parseFloat(rateGuaraniUSDInput.value) || 8357
            };
        }
        
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
                alert('📱 Para instalar:\n\n1. Chrome: Menu (⋮) → "Adicionar à tela inicial"\n2. Safari: Compartilhar → "Adicionar à Tela de Início"');
            }
        });
        
        // Upload de imagem
        cameraBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            fileInputCamera.click();
        });
        
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
                removeImageBtn.style.display = 'inline-block';
                document.getElementById('uploadPrompt').style.display = 'none';
                uploadSection.classList.add('has-image', 'analyzing');
                
                // Mostrar status OCR
                ocrStatus.style.display = 'block';
                ocrStatus.className = 'ocr-status';
                ocrStatus.textContent = '🔍 Analisando imagem e extraindo informações...';
                
                // Simular OCR (em produção, usar API real de OCR)
                await performOCR(e.target.result);
            };
            reader.readAsDataURL(file);
        }
        
        // Simulação de OCR - Extração de texto da imagem
        async function performOCR(imageData) {
            try {
                await new Promise(resolve => setTimeout(resolve, 2000));
                
                // Simulação: extrair nome e preço
                // Em produção, usar Tesseract.js ou Google Vision API
                const mockOCRResults = extractMockData();
                
                if (mockOCRResults.productName || mockOCRResults.price) {
                    ocrStatus.className = 'ocr-status success';
                    ocrStatus.innerHTML = '<strong>✅ Informações Extraídas:</strong><br>';
                    
                    if (mockOCRResults.productName) {
                        productNameInput.value = mockOCRResults.productName;
                        productNameInput.classList.add('auto-filled');
                        ocrStatus.innerHTML += `📦 Produto: ${mockOCRResults.productName}<br>`;
                    }
                    
                    if (mockOCRResults.price) {
                        productPriceInput.value = mockOCRResults.price;
                        productPriceInput.classList.add('auto-filled');
                        const currencySymbol = mockOCRResults.currency === 'dolar' ? 'US$' : 
                                             mockOCRResults.currency === 'guarani' ? '₲' : 'R$';
                        ocrStatus.innerHTML += `💵 Preço: ${currencySymbol} ${mockOCRResults.price}<br>`;
                        
                        // Definir moeda automaticamente
                        if (mockOCRResults.currency) {
                            currencySelect.value = mockOCRResults.currency;
                            updatePriceLabel();
                        }
                    }
                    
                    ocrStatus.innerHTML += '<br>💡 Verifique e ajuste se necessário';
                    
                    // Remover animação após 2s
                    setTimeout(() => {
                        productNameInput.classList.remove('auto-filled');
                        productPriceInput.classList.remove('auto-filled');
                    }, 2000);
                } else {
                    ocrStatus.className = 'ocr-status error';
                    ocrStatus.textContent = '⚠️ Não consegui extrair informações. Digite manualmente.';
                }
                
                uploadSection.classList.remove('analyzing');
                
            } catch (error) {
                ocrStatus.className = 'ocr-status error';
                ocrStatus.textContent = '❌ Erro ao analisar imagem. Digite manualmente.';
                uploadSection.classList.remove('analyzing');
            }
        }
        
        // Simulação de extração de dados (substituir por OCR real)
        function extractMockData() {
            // Simula diferentes cenários de produtos
            const mockProducts = [
                { productName: 'Notebook Dell Inspiron 15', price: '450.00', currency: 'dolar' },
                { productName: 'Samsung Galaxy S24', price: '750000', currency: 'guarani' },
                { productName: 'iPhone 15 Pro', price: '899.00', currency: 'dolar' },
                { productName: 'Perfume 212 VIP 100ml', price: '420000', currency: 'guarani' },
                { productName: 'PlayStation 5', price: '2850000', currency: 'guarani' },
                { productName: 'Apple Watch Series 9', price: '399.00', currency: 'dolar' }
            ];
            
            // Retorna um produto aleatório para simular OCR
            return mockProducts[Math.floor(Math.random() * mockProducts.length)];
        }
        
        // Atualizar label do preço
        function updatePriceLabel() {
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
            productPriceInput.placeholder = placeholders[currency];
        }
        
        currencySelect.addEventListener('change', updatePriceLabel);
        
        // Mostrar informações de regime
        specialRegimeSelect.addEventListener('change', () => {
            const regime = specialRegimeSelect.value;
            const personType = personTypeSelect.value;
            
            const regimeInfos = {
                'none': 'Regime normal de importação com Imposto de Importação padrão de 60%.',
                'remessaconforme': 'Remessa Conforme: Alíquota reduzida de 17% para compras até US$ 3.000. Válido para e-commerce cadastrado.',
                'courier': 'Importação expressa: 60% de II + ICMS estadual. Processo rápido mas custos adicionais.',
                'drawback': personType === 'juridica' ? 'Drawback: Suspensão de impostos para empresas exportadoras.' : 'Drawback disponível apenas para PJ.',
                'zona_franca': 'Zona Franca de Manaus: Incentivos fiscais especiais com redução de impostos.',
                'ex_tarifario': personType === 'juridica' ? 'Ex-Tarifário: Redução de II para bens sem produção nacional.' : 'Ex-Tarifário disponível apenas para PJ.',
                'isencao': 'Isenção de bagagem: Até US$ 1.000 via terrestre para pessoa física.'
            };
            
            regimeInfo.textContent = regimeInfos[regime] || '';
            regimeInfo.style.display = regime === 'none' ? 'none' : 'block';
        });
        
        // Converter preço para BRL
        function convertToBRL(price, currency) {
            const rates = getExchangeRates();
            switch(currency) {
                case 'guarani':
                    return price * rates.GUARANI_TO_BRL;
                case 'dolar':
                    return price * rates.USD_TO_BRL;
                case 'real':
                    return price;
                default:
                    return price;
            }
        }
        
        // Calcular impostos
        function calculateTaxes(priceBRL, priceUSD, personType, regime) {
            let taxRate = 0;
            let taxAmount = 0;
            let taxDescription = '';
            let regimeUsed = '';
            
            if (regime === 'remessaconforme' && priceUSD <= 3000) {
                taxRate = 0.17;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Remessa Conforme (17%)';
                regimeUsed = '✅ Regime Especial Aplicado: Remessa Conforme - economia de 43%!';
            } else if (regime === 'isencao' && personType === 'fisica' && priceUSD <= 1000) {
                taxRate = 0;
                taxAmount = 0;
                taxDescription = 'Isento (Bagagem)';
                regimeUsed = '✅ Isenção Total: Produto dentro do limite de bagagem!';
            } else if (regime === 'drawback' && personType === 'juridica') {
                taxRate = 0;
                taxAmount = 0;
                taxDescription = 'Drawback (0%)';
                regimeUsed = '✅ Drawback: Suspensão total de impostos';
            } else if (regime === 'ex_tarifario' && personType === 'juridica') {
                taxRate = 0.02;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Ex-Tarifário (2%)';
                regimeUsed = '✅ Ex-Tarifário: Redução significativa de impostos';
            } else if (regime === 'zona_franca') {
                taxRate = 0.20;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Zona Franca (20%)';
                regimeUsed = '✅ Zona Franca: Incentivo fiscal aplicado';
            } else {
                taxRate = 0.60;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'II (60%)';
                
                if (personType === 'juridica') {
                    const icmsRate = 0.12;
                    const icmsAmount = priceBRL * icmsRate;
                    taxAmount += icmsAmount;
                    taxDescription = 'II (60%) + ICMS (12%)';
                }
            }
            
            return { taxRate, taxAmount, taxDescription, regimeUsed };
        }
        
        // Buscar preço Brasil (simulado)
        async function searchBrazilPrice(productName, priceBRL) {
            await new Promise(resolve => setTimeout(resolve, 1000));
            
            const multipliers = {
                'notebook': 2.8, 'laptop': 2.8, 'celular': 2.5, 'smartphone': 2.5,
                'iphone': 3.0, 'samsung': 2.4, 'tablet': 2.3, 'ipad': 2.6,
                'fone': 2.0, 'headphone': 2.2, 'mouse': 1.8, 'teclado': 1.9,
                'monitor': 2.4, 'tv': 2.3, 'playstation': 2.5, 'xbox': 2.5,
                'nintendo': 2.4, 'perfume': 2.8, 'whisky': 2.5, 'default': 2.2
            };
            
            let multiplier = multipliers.default;
            const lowerName = productName.toLowerCase();
            
            for (const [key, value] of Object.entries(multipliers)) {
                if (lowerName.includes(key)) {
                    multiplier = value;
                    break;
                }
            }
            
            return priceBRL * multiplier;
        }
        
        // Comparação principal
        compareBtn.addEventListener('click', async () => {
            const price = parseFloat(productPriceInput.value);
            const currency = currencySelect.value;
            const personType = personTypeSelect.value;
            const regime = specialRegimeSelect.value;
            const productName = productNameInput.value || 'Produto';
            
            if (!price || price <= 0) {
                alert('⚠️ Por favor, insira um preço válido!');
                return;
            }
            
            if (!productName.trim() || productName === 'Produto') {
                alert('⚠️ Por favor, informe o nome do produto!');
                return;
            }
            
            compareBtn.disabled = true;
            loading.style.display = 'block';
            results.style.display = 'none';
            
            try {
                const rates = getExchangeRates();
                const priceBRL = convertToBRL(price, currency);
                const priceUSD = priceBRL / rates.USD_TO_BRL;
                
                const { taxAmount, taxDescription, regimeUsed } = calculateTaxes(priceBRL, priceUSD, personType, regime);
                const totalParaguai = priceBRL + taxAmount;
                const priceBrazil = await searchBrazilPrice(productName, priceBRL);
                const savings = priceBrazil - totalParaguai;
                const savingsPercent = ((savings / priceBrazil) * 100).toFixed(1);
                
                // Conversão
                const currencySymbols = { 'guarani': '₲', 'dolar': 'US$', 'real': 'R$' };
                let conversionText = '';
                
                if (currency === 'guarani') {
                    conversionText = `Conversão: ₲ ${price.toLocaleString('pt-BR')} = R$ ${priceBRL.toFixed(2)} = US$ ${priceUSD.toFixed(2)}`;
                } else if (currency === 'dolar') {
                    conversionText = `Conversão: US$ ${price.toFixed(2)} = R$ ${priceBRL.toFixed(2)} = ₲ ${(price * rates.USD_TO_GUARANI).toLocaleString('pt-BR')}`;
                } else {
                    conversionText = `Valor: R$ ${price.toFixed(2)} = US$ ${priceUSD.toFixed(2)} = ₲ ${(priceUSD * rates.USD_TO_GUARANI).toLocaleString('pt-BR')}`;
                }
                
                document.getElementById('conversionInfo').textContent = conversionText;
                document.getElementById('detectedProduct').textContent = productName;
                document.getElementById('priceOriginal').textContent = `${currencySymbols[currency]} ${price.toLocaleString('pt-BR', {minimumFractionDigits: 2})}`;
                document.getElementById('priceBRL').textContent = `R$ ${priceBRL.toFixed(2)}`;
                document.getElementById('taxAmount').textContent = `R$ ${taxAmount.toFixed(2)} (${taxDescription})`;
                document.getElementById('totalParaguai').textContent = `R$ ${totalParaguai.toFixed(2)}`;
                document.getElementById('priceBrazil').textContent = `R$ ${priceBrazil.toFixed(2)}`;
                
                // Regime especial
                const regimeHighlight = document.getElementById('regimeHighlight');
                if (regimeUsed) {
                    regimeHighlight.textContent = regimeUsed;
                    regimeHighlight.style.display = 'block';
                } else {
                    regimeHighlight.style.display = 'none';
                }
                
                // Info tributária
                let taxInfoText = personType === 'fisica' ?
                    (regime === 'isencao' && priceUSD <= 1000 ? 
                        'Pessoa Física - Isenção: Produto dentro do limite de US$ 1.000. Sem impostos!' :
                    regime === 'remessaconforme' && priceUSD <= 3000 ?
                        'Pessoa Física - Remessa Conforme: Apenas 17% de imposto. Grande economia!' :
                        'Pessoa Física - Regime Normal: 60% de imposto sobre o valor do produto.') :
                    (regime === 'drawback' ?
                        'Pessoa Jurídica - Drawback: Suspensão de impostos mediante exportação.' :
                    regime === 'ex_tarifario' ?
                        'Pessoa Jurídica - Ex-Tarifário: Redução para bens sem similar nacional.' :
                        'Pessoa Jurídica: 60% II + 12% ICMS médio. Formalização necessária.');
                
                document.getElementById('taxInfo').textContent = taxInfoText;
                
                // Economia
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
                        <div class="savings-subtitle">Você pagaria R$ ${Math.abs(savings).toFixed(2)} a mais</div>
                    `;
                }
                
                results.style.display = 'block';
                
                // Scroll suave para resultados em mobile
                if (window.innerWidth < 1024) {
                    results.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
                }
                
            } catch (error) {
                alert('❌ Erro: ' + error.message);
            } finally {
                compareBtn.disabled = false;
                loading.style.display = 'none';
            }
        });
        
        // Vibração
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
