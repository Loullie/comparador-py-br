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
    <title>Compara PY-BR PRO v5.0 - QR Code + Barcode</title>
    
    <link rel="icon" type="image/png" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Crect width='100' height='100' fill='%231e40af'/%3E%3Ctext x='50' y='60' font-size='50' fill='white' text-anchor='middle' font-family='Arial'%3E🛒%3C/text%3E%3C/svg%3E">
    <link rel="manifest" id="manifest-placeholder">
    
    <!-- Bibliotecas para OCR, QR Code e Código de Barras -->
    <script src='https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js'></script>
    <script src='https://cdn.jsdelivr.net/npm/jsqr@1.4.0/dist/jsQR.min.js'></script>
    <script src='https://cdn.jsdelivr.net/npm/@ericblade/quagga2@1.8.4/dist/quagga.min.js'></script>
    
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
            font-size: clamp(11px, 2.5vw, 13px);
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
            font-size: 13px;
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
        
        .scan-section {
            background: linear-gradient(135deg, #e0e7ff 0%, #c7d2fe 100%);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .scan-section h4 {
            color: var(--primary-color);
            margin-bottom: 15px;
            font-size: 16px;
        }
        
        .scan-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }
        
        .scan-btn {
            padding: 15px;
            background: white;
            border: 2px solid var(--primary-light);
            border-radius: 12px;
            color: var(--primary-color);
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }
        
        .scan-btn:active {
            transform: scale(0.95);
            background: var(--primary-light);
            color: white;
        }
        
        .scan-btn .icon {
            font-size: 32px;
        }
        
        #scannerVideo {
            width: 100%;
            max-width: 100%;
            border-radius: 10px;
            margin-top: 15px;
            display: none;
        }
        
        #scannerCanvas {
            display: none;
        }
        
        .scan-result {
            background: #dcfce7;
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
            display: none;
            text-align: left;
        }
        
        .scan-result.active {
            display: block;
        }
        
        .scan-result h5 {
            color: #166534;
            margin-bottom: 8px;
        }
        
        .scan-result p {
            color: #166534;
            font-size: 13px;
            line-height: 1.6;
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
            margin-bottom: 15px;
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
        
        .stop-scan-btn {
            background: var(--danger-color);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            margin-top: 15px;
            display: none;
        }
        
        /* Seção de Publicidade */
        .advertising-section {
            margin-top: 25px;
            padding-top: 25px;
            border-top: 2px solid var(--border-color);
        }
        
        .ad-label {
            font-size: 11px;
            color: var(--text-light);
            text-align: center;
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 600;
        }
        
        .ad-banner {
            background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
        }
        
        .ad-banner::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, transparent 30%, rgba(255,255,255,0.3) 50%, transparent 70%);
            transform: translateX(-100%);
            transition: transform 0.6s;
        }
        
        .ad-banner:hover::before {
            transform: translateX(100%);
        }
        
        .ad-banner:active {
            transform: scale(0.98);
        }
        
        .ad-banner-secondary {
            background: linear-gradient(135deg, #dbeafe 0%, #bfdbfe 100%);
        }
        
        .ad-content {
            display: flex;
            align-items: center;
            gap: 15px;
            position: relative;
            z-index: 1;
        }
        
        .ad-icon {
            font-size: 42px;
            flex-shrink: 0;
        }
        
        .ad-text {
            flex: 1;
        }
        
        .ad-title {
            font-size: 16px;
            font-weight: 700;
            color: var(--text-dark);
            margin-bottom: 4px;
        }
        
        .ad-subtitle {
            font-size: 13px;
            color: var(--text-light);
        }
        
        .ad-manage-btn {
            width: 100%;
            padding: 12px;
            background: white;
            border: 2px solid var(--border-color);
            border-radius: 10px;
            color: var(--text-dark);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 10px;
        }
        
        .ad-manage-btn:hover {
            border-color: var(--primary-light);
            color: var(--primary-color);
        }
        
        /* Modal de Gerenciamento de Anúncios */
        .ad-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .ad-modal.active {
            display: flex;
        }
        
        .ad-modal-content {
            background: white;
            border-radius: 20px;
            padding: 30px;
            max-width: 600px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
            animation: modalSlideIn 0.3s ease-out;
        }
        
        @keyframes modalSlideIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .ad-modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--border-color);
        }
        
        .ad-modal-header h3 {
            color: var(--primary-color);
            font-size: 22px;
        }
        
        .ad-modal-close {
            background: var(--danger-color);
            color: white;
            border: none;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: transform 0.2s;
        }
        
        .ad-modal-close:active {
            transform: scale(0.9);
        }
        
        .ad-form-group {
            margin-bottom: 20px;
        }
        
        .ad-form-group label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
            color: var(--text-dark);
            font-size: 14px;
        }
        
        .ad-form-group input,
        .ad-form-group textarea,
        .ad-form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid var(--border-color);
            border-radius: 10px;
            font-size: 15px;
            transition: border-color 0.3s;
        }
        
        .ad-form-group textarea {
            resize: vertical;
            min-height: 80px;
        }
        
        .ad-form-group input:focus,
        .ad-form-group textarea:focus,
        .ad-form-group select:focus {
            outline: none;
            border-color: var(--primary-light);
        }
        
        .ad-preview {
            background: var(--bg-light);
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
        }
        
        .ad-preview h4 {
            color: var(--primary-color);
            margin-bottom: 15px;
            font-size: 16px;
        }
        
        .ad-color-picker {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 10px;
            margin-top: 10px;
        }
        
        .color-option {
            width: 100%;
            aspect-ratio: 1;
            border-radius: 8px;
            border: 3px solid transparent;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .color-option:hover {
            transform: scale(1.1);
        }
        
        .color-option.selected {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 2px white, 0 0 0 4px var(--primary-color);
        }
        
        .ad-save-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, var(--success-color) 0%, #059669 100%);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            transition: transform 0.2s;
        }
        
        .ad-save-btn:active {
            transform: scale(0.98);
        }
        
        /* Sistema de Login */
        .login-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--secondary-color) 0%, #764ba2 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            padding: 20px;
        }
        
        .login-container {
            background: white;
            border-radius: 25px;
            box-shadow: 0 30px 80px rgba(0,0,0,0.4);
            max-width: 450px;
            width: 100%;
            overflow: hidden;
            animation: loginSlideIn 0.5s ease-out;
        }
        
        @keyframes loginSlideIn {
            from {
                opacity: 0;
                transform: translateY(-50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .login-header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-light) 100%);
            color: white;
            padding: 40px 30px;
            text-align: center;
        }
        
        .login-emoji {
            font-size: 64px;
            display: block;
            margin-bottom: 15px;
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        
        .login-header h1 {
            font-size: 24px;
            margin-bottom: 8px;
        }
        
        .login-header p {
            font-size: 14px;
            opacity: 0.9;
        }
        
        .login-content {
            padding: 35px 30px;
        }
        
        .login-form .form-group {
            margin-bottom: 25px;
        }
        
        .login-form label {
            display: block;
            font-weight: 600;
            margin-bottom: 10px;
            color: var(--text-dark);
            font-size: 15px;
        }
        
        .login-form input {
            width: 100%;
            padding: 15px;
            border: 2px solid var(--border-color);
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s;
            text-align: center;
            letter-spacing: 2px;
            font-weight: 600;
        }
        
        .login-form input:focus {
            outline: none;
            border-color: var(--primary-light);
            box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.1);
        }
        
        .login-error {
            background: #fee2e2;
            color: #991b1b;
            padding: 12px;
            border-radius: 10px;
            margin-top: 15px;
            text-align: center;
            font-size: 14px;
            font-weight: 600;
            animation: shake 0.5s;
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }
        
        .login-info {
            background: #f0f9ff;
            padding: 20px;
            border-radius: 12px;
            margin-top: 25px;
            text-align: center;
        }
        
        .login-info p {
            font-size: 14px;
            color: var(--text-dark);
            margin-bottom: 5px;
        }
        
        .login-info code {
            background: var(--primary-color);
            color: white;
            padding: 8px 15px;
            border-radius: 8px;
            font-size: 18px;
            font-weight: 700;
            letter-spacing: 2px;
            display: inline-block;
            margin-top: 8px;
        }
        
        .login-footer {
            background: var(--bg-light);
            padding: 20px;
            text-align: center;
            font-size: 13px;
            color: var(--text-light);
        }
        
        .app-container {
            min-height: 100vh;
        }
        
        /* Botão Trocar Senha no Header */
        .change-password-btn {
            position: absolute;
            top: 10px;
            left: 10px;
            background: rgba(255,255,255,0.2);
            color: white;
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            font-size: 20px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .change-password-btn:hover {
            background: rgba(255,255,255,0.3);
            transform: scale(1.1);
        }
        
        .change-password-btn:active {
            transform: scale(0.95);
        }
        
        /* Alerta de Senha Provisória */
        .provisional-password-alert {
            position: absolute;
            top: 55px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
            color: #92400e;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            animation: blink 2s infinite;
            border: 2px solid #f59e0b;
            box-shadow: 0 2px 8px rgba(245, 158, 11, 0.4);
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        
        @media (max-width: 768px) {
            .provisional-password-alert {
                font-size: 9px;
                padding: 6px 10px;
                top: 50px;
            }
        }
        
        /* Modal Trocar Senha */
        .password-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 10000;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .password-modal.active {
            display: flex;
        }
        
        .password-modal-content {
            background: white;
            border-radius: 20px;
            padding: 30px;
            max-width: 500px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            animation: modalSlideIn 0.3s ease-out;
        }
        
        .password-modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--border-color);
        }
        
        .password-modal-header h3 {
            color: var(--primary-color);
            font-size: 22px;
        }
        
        .password-strength {
            margin: 15px 0;
        }
        
        .strength-bar {
            height: 8px;
            background: #e5e7eb;
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 8px;
        }
        
        .strength-fill {
            height: 100%;
            transition: all 0.3s;
            width: 0%;
        }
        
        .strength-fill.weak {
            width: 33%;
            background: #ef4444;
        }
        
        .strength-fill.medium {
            width: 66%;
            background: #f59e0b;
        }
        
        .strength-fill.strong {
            width: 100%;
            background: #10b981;
        }
        
        .strength-text {
            font-size: 13px;
            font-weight: 600;
        }
        
        .strength-text.weak {
            color: #ef4444;
        }
        
        .strength-text.medium {
            color: #f59e0b;
        }
        
        .strength-text.strong {
            color: #10b981;
        }
        
        .password-info {
            background: #f0f9ff;
            padding: 15px;
            border-radius: 10px;
            margin-top: 20px;
        }
        
        .password-info p {
            font-size: 13px;
            color: var(--primary-color);
            margin-bottom: 10px;
            font-weight: 600;
        }
        
        .password-info ul {
            margin-left: 20px;
            font-size: 13px;
            color: var(--text-dark);
            line-height: 1.8;
        }
    </style>
</head>
<body>
    <!-- Tela de Login -->
    <div class="login-screen" id="loginScreen">
        <div class="login-container">
            <div class="login-header">
                <span class="login-emoji">🔐</span>
                <h1>Compara PY-BR PRO</h1>
                <p>Sistema de Comparação de Preços</p>
            </div>
            
            <div class="login-content">
                <div class="login-form">
                    <div class="form-group">
                        <label for="loginPassword">🔑 Senha de Acesso:</label>
                        <input 
                            type="password" 
                            id="loginPassword" 
                            placeholder="Digite a senha"
                            maxlength="20"
                            autocomplete="off"
                        >
                    </div>
                    
                    <button class="btn" id="loginBtn" onclick="doLogin()">🚀 Entrar</button>
                    
                    <div class="login-error" id="loginError" style="display: none;">
                        ❌ Senha incorreta! Tente novamente.
                    </div>
                    
                    <div class="login-info">
                        <p>🔐 <strong>Senha Provisória</strong></p>
                        <p style="font-size: 13px; line-height: 1.6;">
                            Se este é seu primeiro acesso, utilize a <strong>senha provisória</strong> 
                            fornecida pelo administrador do sistema.
                        </p>
                        <p style="margin-top: 12px; font-size: 13px; color: #dc2626; font-weight: 600;">
                            ⚠️ Após o primeiro login, você <strong>DEVE</strong> alterar sua senha 
                            imediatamente para garantir a segurança.
                        </p>
                    </div>
                </div>
            </div>
            
            <div class="login-footer">
                <p>🛡️ Acesso seguro e protegido</p>
                <p style="font-size: 11px; margin-top: 5px;">v5.0 FINAL</p>
            </div>
        </div>
    </div>
    
    <!-- App Principal (oculto até login) -->
    <div class="app-container" id="appContainer" style="display: none;">
    <div class="container">
        <div class="header">
            <span class="version-badge">v5.0 FINAL</span>
            <button class="change-password-btn" onclick="openChangePassword()" title="Trocar Senha">🔐</button>
            <div class="provisional-password-alert" id="provisionalAlert" style="display: none;">
                <span>⚠️ SENHA PROVISÓRIA ATIVA</span>
            </div>
            <span class="emoji">🛒</span>
            <h1>Compara PY-BR PRO</h1>
            <p>OCR • QR Code • Código de Barras • RTU</p>
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
                
                <div class="scan-section">
                    <h4>📱 Escanear QR Code / Código de Barras</h4>
                    <div class="scan-buttons">
                        <button class="scan-btn" onclick="startQRScan()">
                            <span class="icon">📷</span>
                            <span>QR Code</span>
                        </button>
                        <button class="scan-btn" onclick="startBarcodeScan()">
                            <span class="icon">📊</span>
                            <span>Cód. Barras</span>
                        </button>
                    </div>
                    <video id="scannerVideo" autoplay playsinline></video>
                    <canvas id="scannerCanvas"></canvas>
                    <button class="stop-scan-btn" id="stopScanBtn" onclick="stopScan()">⏹️ Parar Scan</button>
                    <div class="scan-result" id="scanResult">
                        <h5 id="scanResultTitle">✅ Código Detectado!</h5>
                        <p id="scanResultText"></p>
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
                            <option value="rtu_online">RTU Online (60%)</option>
                            <option value="rtu_presencial">RTU Presencial (60%)</option>
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
                
                <!-- Espaço para Marketing e Propaganda -->
                <div class="advertising-section">
                    <div class="ad-label">📢 Publicidade</div>
                    <div id="adBanner1" class="ad-banner" onclick="handleAdClick(1)">
                        <div class="ad-content">
                            <div class="ad-icon">🏪</div>
                            <div class="ad-text">
                                <div class="ad-title">Anuncie Aqui!</div>
                                <div class="ad-subtitle">Seu negócio em destaque</div>
                            </div>
                        </div>
                    </div>
                    
                    <div id="adBanner2" class="ad-banner ad-banner-secondary" onclick="handleAdClick(2)">
                        <div class="ad-content">
                            <div class="ad-icon">💼</div>
                            <div class="ad-text">
                                <div class="ad-title">Espaço Publicitário</div>
                                <div class="ad-subtitle">Alcance milhares de compradores</div>
                            </div>
                        </div>
                    </div>
                    
                    <button class="ad-manage-btn" onclick="openAdManager()">⚙️ Gerenciar Anúncios</button>
                </div>
                
                <div class="loading" id="loading">
                    <div class="spinner"></div>
                    <p style="color: var(--text-light); font-size: 14px;">Calculando...</p>
                </div>
            </div>
            
            <div id="historyTab" class="tab-content">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <h3 style="color: var(--primary-color);">Consultas Salvas</h3>
                    <button onclick="clearHistory()" style="background: var(--danger-color); color: white; border: none; padding: 8px 15px; border-radius: 8px; cursor: pointer; font-size: 13px;">🗑️ Limpar</button>
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
    </div>
    
    <!-- Modal de Trocar Senha -->
    <div class="password-modal" id="passwordModal">
        <div class="password-modal-content">
            <div class="password-modal-header">
                <h3>🔐 Trocar Senha</h3>
                <button class="ad-modal-close" onclick="closeChangePassword()">✕</button>
            </div>
            
            <div class="ad-form-group">
                <label>🔑 Senha Atual:</label>
                <input type="password" id="currentPassword" placeholder="Digite a senha atual" maxlength="20">
            </div>
            
            <div class="ad-form-group">
                <label>🆕 Nova Senha:</label>
                <input type="password" id="newPassword" placeholder="Digite a nova senha" maxlength="20">
            </div>
            
            <div class="ad-form-group">
                <label>✅ Confirmar Nova Senha:</label>
                <input type="password" id="confirmPassword" placeholder="Confirme a nova senha" maxlength="20">
            </div>
            
            <div class="password-strength" id="passwordStrength" style="display: none;">
                <div class="strength-bar">
                    <div class="strength-fill" id="strengthFill"></div>
                </div>
                <p class="strength-text" id="strengthText"></p>
            </div>
            
            <button class="ad-save-btn" onclick="changePassword()">💾 Alterar Senha</button>
            
            <div class="password-info">
                <p>💡 <strong>Dicas de segurança:</strong></p>
                <ul>
                    <li>Use pelo menos 6 caracteres</li>
                    <li>Combine números e letras</li>
                    <li>Não compartilhe sua senha</li>
                </ul>
            </div>
        </div>
    </div>
    
    <!-- Modal de Gerenciamento de Anúncios -->
    <div class="ad-modal" id="adModal">
        <div class="ad-modal-content">
            <div class="ad-modal-header">
                <h3>⚙️ Gerenciar Anúncios</h3>
                <button class="ad-modal-close" onclick="closeAdManager()">✕</button>
            </div>
            
            <div class="ad-form-group">
                <label>Selecione o Banner:</label>
                <select id="adBannerSelect" onchange="loadAdData()">
                    <option value="1">Banner 1 (Principal)</option>
                    <option value="2">Banner 2 (Secundário)</option>
                </select>
            </div>
            
            <div class="ad-form-group">
                <label>Título do Anúncio:</label>
                <input type="text" id="adTitle" placeholder="Ex: Casa de Câmbio Dollar" maxlength="30">
            </div>
            
            <div class="ad-form-group">
                <label>Subtítulo:</label>
                <input type="text" id="adSubtitle" placeholder="Ex: Melhores taxas da região" maxlength="50">
            </div>
            
            <div class="ad-form-group">
                <label>Link do Anúncio (URL):</label>
                <input type="url" id="adLink" placeholder="https://seusite.com">
            </div>
            
            <div class="ad-form-group">
                <label>Telefone (WhatsApp):</label>
                <input type="tel" id="adPhone" placeholder="Ex: 5545999999999">
            </div>
            
            <div class="ad-form-group">
                <label>Ícone do Anúncio:</label>
                <select id="adIcon">
                    <option value="🏪">🏪 Loja</option>
                    <option value="💱">💱 Câmbio</option>
                    <option value="🏢">🏢 Empresa</option>
                    <option value="🛒">🛒 Supermercado</option>
                    <option value="🏨">🏨 Hotel</option>
                    <option value="🍔">🍔 Restaurante</option>
                    <option value="⛽">⛽ Posto</option>
                    <option value="🚗">🚗 Transporte</option>
                    <option value="📱">📱 Eletrônicos</option>
                    <option value="👕">👕 Roupas</option>
                    <option value="💄">💄 Cosméticos</option>
                    <option value="🎮">🎮 Games</option>
                    <option value="📚">📚 Livraria</option>
                    <option value="💊">💊 Farmácia</option>
                    <option value="🏋️">🏋️ Academia</option>
                </select>
            </div>
            
            <div class="ad-form-group">
                <label>Cor do Banner:</label>
                <div class="ad-color-picker">
                    <div class="color-option selected" style="background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);" data-color="yellow" onclick="selectColor(this)"></div>
                    <div class="color-option" style="background: linear-gradient(135deg, #dbeafe 0%, #bfdbfe 100%);" data-color="blue" onclick="selectColor(this)"></div>
                    <div class="color-option" style="background: linear-gradient(135deg, #dcfce7 0%, #bbf7d0 100%);" data-color="green" onclick="selectColor(this)"></div>
                    <div class="color-option" style="background: linear-gradient(135deg, #fce7f3 0%, #fbcfe8 100%);" data-color="pink" onclick="selectColor(this)"></div>
                    <div class="color-option" style="background: linear-gradient(135deg, #f3e8ff 0%, #e9d5ff 100%);" data-color="purple" onclick="selectColor(this)"></div>
                    <div class="color-option" style="background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%);" data-color="red" onclick="selectColor(this)"></div>
                </div>
            </div>
            
            <div class="ad-preview">
                <h4>👁️ Prévia do Anúncio:</h4>
                <div class="ad-banner" id="adPreview" style="margin: 0;">
                    <div class="ad-content">
                        <div class="ad-icon" id="previewIcon">🏪</div>
                        <div class="ad-text">
                            <div class="ad-title" id="previewTitle">Título do Anúncio</div>
                            <div class="ad-subtitle" id="previewSubtitle">Subtítulo do anúncio</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <button class="ad-save-btn" onclick="saveAd()">💾 Salvar Anúncio</button>
        </div>
    </div>

    <script>
        const manifestData = {
            name: "Compara PY-BR PRO v5.0",
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

        if ('serviceWorker' in navigator) {
            window.addEventListener('load', () => {
                const sw = `self.addEventListener('install',e=>e.waitUntil(self.skipWaiting()));self.addEventListener('activate',e=>e.waitUntil(self.clients.claim()));`;
                navigator.serviceWorker.register(URL.createObjectURL(new Blob([sw], {type: 'application/javascript'})));
            });
        }

        // ============================================
        // SISTEMA DE LOGIN E AUTENTICAÇÃO
        // ============================================
        
        const DEFAULT_PASSWORD = '15252724';
        
        // Verificar se já está logado
        window.addEventListener('load', () => {
            const isLoggedIn = sessionStorage.getItem('comparapy_logged_in');
            if (isLoggedIn === 'true') {
                showApp();
            }
        });
        
        // Fazer login
        function doLogin() {
            const password = document.getElementById('loginPassword').value;
            const storedPassword = localStorage.getItem('comparapy_password') || DEFAULT_PASSWORD;
            
            if (password === storedPassword) {
                sessionStorage.setItem('comparapy_logged_in', 'true');
                document.getElementById('loginError').style.display = 'none';
                showApp();
                
                // Limpar campo de senha
                document.getElementById('loginPassword').value = '';
            } else {
                document.getElementById('loginError').style.display = 'block';
                document.getElementById('loginPassword').value = '';
                document.getElementById('loginPassword').focus();
                
                // Vibrar em caso de erro
                if ('vibrate' in navigator) {
                    navigator.vibrate([100, 50, 100]);
                }
            }
        }
        
        // Mostrar app
        function showApp() {
            document.getElementById('loginScreen').style.display = 'none';
            document.getElementById('appContainer').style.display = 'block';
            
            // Verificar se é primeiro acesso com senha padrão
            const storedPassword = localStorage.getItem('comparapy_password') || DEFAULT_PASSWORD;
            const firstLoginDone = localStorage.getItem('comparapy_first_login_done');
            
            // Mostrar alerta visual se senha provisória
            if (storedPassword === DEFAULT_PASSWORD) {
                document.getElementById('provisionalAlert').style.display = 'block';
            } else {
                document.getElementById('provisionalAlert').style.display = 'none';
            }
            
            if (storedPassword === DEFAULT_PASSWORD && !firstLoginDone) {
                // Mostrar alerta para trocar senha
                setTimeout(() => {
                    if (confirm('🔐 IMPORTANTE: Senha Provisória Detectada!\n\n' +
                        'Você está usando a senha padrão provisória do sistema.\n\n' +
                        'Por motivos de SEGURANÇA, é OBRIGATÓRIO trocar sua senha agora.\n\n' +
                        'Deseja alterar sua senha agora?')) {
                        openChangePassword();
                        localStorage.setItem('comparapy_first_login_done', 'true');
                    } else {
                        alert('⚠️ ATENÇÃO!\n\nVocê optou por não trocar a senha agora.\n\n' +
                            'LEMBRE-SE: Esta é uma senha PROVISÓRIA e deve ser alterada o quanto antes.\n\n' +
                            'Use o botão 🔐 no canto superior esquerdo para trocar sua senha.');
                        localStorage.setItem('comparapy_first_login_done', 'true');
                    }
                }, 500);
            }
            
            // Carregar anúncios
            const ad1 = JSON.parse(localStorage.getItem('ad_banner_1'));
            if (ad1) updateBannerDisplay('1', ad1);
            
            const ad2 = JSON.parse(localStorage.getItem('ad_banner_2'));
            if (ad2) updateBannerDisplay('2', ad2);
        }
        
        // Enter para fazer login
        document.getElementById('loginPassword').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                doLogin();
            }
        });
        
        // ============================================
        // TROCAR SENHA
        // ============================================
        
        function openChangePassword() {
            document.getElementById('passwordModal').classList.add('active');
            document.getElementById('currentPassword').value = '';
            document.getElementById('newPassword').value = '';
            document.getElementById('confirmPassword').value = '';
            document.getElementById('passwordStrength').style.display = 'none';
        }
        
        function closeChangePassword() {
            document.getElementById('passwordModal').classList.remove('active');
        }
        
        // Verificar força da senha
        document.getElementById('newPassword').addEventListener('input', (e) => {
            const password = e.target.value;
            const strengthDiv = document.getElementById('passwordStrength');
            const strengthFill = document.getElementById('strengthFill');
            const strengthText = document.getElementById('strengthText');
            
            if (password.length === 0) {
                strengthDiv.style.display = 'none';
                return;
            }
            
            strengthDiv.style.display = 'block';
            
            let strength = 0;
            if (password.length >= 6) strength++;
            if (password.length >= 8) strength++;
            if (/[0-9]/.test(password) && /[a-zA-Z]/.test(password)) strength++;
            
            strengthFill.className = 'strength-fill';
            strengthText.className = 'strength-text';
            
            if (strength <= 1) {
                strengthFill.classList.add('weak');
                strengthText.classList.add('weak');
                strengthText.textContent = '⚠️ Senha fraca - Use mais caracteres';
            } else if (strength === 2) {
                strengthFill.classList.add('medium');
                strengthText.classList.add('medium');
                strengthText.textContent = '⚡ Senha média - Pode melhorar';
            } else {
                strengthFill.classList.add('strong');
                strengthText.classList.add('strong');
                strengthText.textContent = '✅ Senha forte - Ótima escolha!';
            }
        });
        
        function changePassword() {
            const currentPassword = document.getElementById('currentPassword').value;
            const newPassword = document.getElementById('newPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            
            const storedPassword = localStorage.getItem('comparapy_password') || DEFAULT_PASSWORD;
            
            // Validações
            if (!currentPassword || !newPassword || !confirmPassword) {
                alert('⚠️ Preencha todos os campos!');
                return;
            }
            
            if (currentPassword !== storedPassword) {
                alert('❌ Senha atual incorreta!');
                document.getElementById('currentPassword').value = '';
                document.getElementById('currentPassword').focus();
                return;
            }
            
            if (newPassword.length < 6) {
                alert('⚠️ A nova senha deve ter pelo menos 6 caracteres!');
                return;
            }
            
            if (newPassword !== confirmPassword) {
                alert('❌ As senhas não coincidem!');
                document.getElementById('confirmPassword').value = '';
                document.getElementById('confirmPassword').focus();
                return;
            }
            
            if (newPassword === storedPassword) {
                alert('⚠️ A nova senha deve ser diferente da atual!');
                return;
            }
            
            // Validação adicional: não permitir senha padrão
            if (newPassword === DEFAULT_PASSWORD) {
                alert('❌ Você não pode usar a senha provisória padrão!\n\nEscolha uma senha personalizada e segura.');
                document.getElementById('newPassword').value = '';
                document.getElementById('confirmPassword').value = '';
                document.getElementById('newPassword').focus();
                return;
            }
            
            // Salvar nova senha
            localStorage.setItem('comparapy_password', newPassword);
            
            // Marcar que senha foi alterada
            if (storedPassword === DEFAULT_PASSWORD) {
                localStorage.setItem('comparapy_password_changed', 'true');
                // Ocultar alerta de senha provisória
                document.getElementById('provisionalAlert').style.display = 'none';
            }
            
            alert('✅ Senha alterada com sucesso!\n\n' +
                '🔐 Sua senha foi atualizada e está segura.\n\n' +
                '⚠️ IMPORTANTE: Guarde sua nova senha em local seguro!\n\n' +
                'Você precisará dela no próximo login.');
            
            closeChangePassword();
            
            // Vibração de sucesso
            if ('vibrate' in navigator) {
                navigator.vibrate([50, 100, 50]);
            }
        }
        
        // Fechar modal ao clicar fora
        document.getElementById('passwordModal').addEventListener('click', (e) => {
            if (e.target.id === 'passwordModal') {
                closeChangePassword();
            }
        });

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
        const scannerVideo = document.getElementById('scannerVideo');
        const scannerCanvas = document.getElementById('scannerCanvas');
        const scanResult = document.getElementById('scanResult');
        const scanResultText = document.getElementById('scanResultText');
        const stopScanBtn = document.getElementById('stopScanBtn');
        
        let scanStream = null;
        let scanMode = null;
        let qrScanInterval = null;
        
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
        
        // Scanner QR Code
        async function startQRScan() {
            try {
                scanMode = 'qr';
                scanResult.classList.remove('active');
                
                scanStream = await navigator.mediaDevices.getUserMedia({ 
                    video: { facingMode: 'environment' } 
                });
                
                scannerVideo.srcObject = scanStream;
                scannerVideo.style.display = 'block';
                stopScanBtn.style.display = 'block';
                
                scannerCanvas.width = 640;
                scannerCanvas.height = 480;
                const ctx = scannerCanvas.getContext('2d');
                
                qrScanInterval = setInterval(() => {
                    if (scannerVideo.readyState === scannerVideo.HAVE_ENOUGH_DATA) {
                        ctx.drawImage(scannerVideo, 0, 0, scannerCanvas.width, scannerCanvas.height);
                        const imageData = ctx.getImageData(0, 0, scannerCanvas.width, scannerCanvas.height);
                        const code = jsQR(imageData.data, imageData.width, imageData.height);
                        
                        if (code) {
                            handleScanResult('QR Code', code.data);
                            stopScan();
                        }
                    }
                }, 100);
                
            } catch (error) {
                alert('❌ Erro ao acessar câmera: ' + error.message);
            }
        }
        
        // Scanner Código de Barras
        async function startBarcodeScan() {
            try {
                scanMode = 'barcode';
                scanResult.classList.remove('active');
                
                scannerVideo.style.display = 'block';
                stopScanBtn.style.display = 'block';
                
                Quagga.init({
                    inputStream: {
                        name: "Live",
                        type: "LiveStream",
                        target: scannerVideo,
                        constraints: {
                            facingMode: "environment"
                        }
                    },
                    decoder: {
                        readers: [
                            "code_128_reader",
                            "ean_reader",
                            "ean_8_reader",
                            "code_39_reader",
                            "upc_reader",
                            "upc_e_reader"
                        ]
                    }
                }, function(err) {
                    if (err) {
                        alert('❌ Erro ao iniciar scanner: ' + err);
                        return;
                    }
                    Quagga.start();
                });
                
                Quagga.onDetected(function(result) {
                    const code = result.codeResult.code;
                    handleScanResult('Código de Barras', code);
                    stopScan();
                });
                
            } catch (error) {
                alert('❌ Erro ao acessar câmera: ' + error.message);
            }
        }
        
        function stopScan() {
            if (qrScanInterval) {
                clearInterval(qrScanInterval);
                qrScanInterval = null;
            }
            
            if (scanStream) {
                scanStream.getTracks().forEach(track => track.stop());
                scanStream = null;
            }
            
            if (scanMode === 'barcode') {
                Quagga.stop();
            }
            
            scannerVideo.style.display = 'none';
            stopScanBtn.style.display = 'none';
            scanMode = null;
        }
        
        async function handleScanResult(type, code) {
            scanResult.classList.add('active');
            scanResultText.innerHTML = `<strong>${type}:</strong> ${code}<br><br>🔍 Buscando informações do produto...`;
            
            // Simular busca de produto (em produção, usar API real)
            setTimeout(async () => {
                const productInfo = await searchProductByCode(code);
                
                if (productInfo) {
                    productNameInput.value = productInfo.name;
                    productPriceInput.value = productInfo.price;
                    currencySelect.value = productInfo.currency;
                    updatePriceLabel();
                    
                    productNameInput.classList.add('auto-filled');
                    productPriceInput.classList.add('auto-filled');
                    
                    scanResultText.innerHTML = `
                        <strong>${type}:</strong> ${code}<br>
                        ✅ <strong>Produto encontrado!</strong><br>
                        📦 ${productInfo.name}<br>
                        💵 ${productInfo.currency === 'guarani' ? '₲' : productInfo.currency === 'dolar' ? 'US$' : 'R$'} ${productInfo.price}
                    `;
                    
                    setTimeout(() => {
                        productNameInput.classList.remove('auto-filled');
                        productPriceInput.classList.remove('auto-filled');
                    }, 2000);
                } else {
                    scanResultText.innerHTML = `
                        <strong>${type}:</strong> ${code}<br>
                        ⚠️ Produto não encontrado na base de dados.<br>
                        💡 Digite manualmente o nome e preço.
                    `;
                }
            }, 1500);
        }
        
        // Simular busca de produto (substituir por API real)
        async function searchProductByCode(code) {
            await new Promise(r => setTimeout(r, 1000));
            
            const mockProducts = {
                '7891234567890': { name: 'Notebook Dell Inspiron 15', price: '2499.00', currency: 'real' },
                '7899876543210': { name: 'Samsung Galaxy S24', price: '750000', currency: 'guarani' },
                '0123456789012': { name: 'iPhone 15 Pro', price: '899.00', currency: 'dolar' },
            };
            
            return mockProducts[code] || null;
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
                    
                    setTimeout(() => {
                        productNameInput.classList.remove('auto-filled');
                        productPriceInput.classList.remove('auto-filled');
                    }, 2000);
                } else {
                    ocrStatus.className = 'ocr-status error';
                    ocrText.innerHTML = `⚠️ Não consegui extrair dados claramente.<br><small>Texto: ${text.substring(0, 100)}...</small>`;
                }
                
            } catch (error) {
                ocrStatus.className = 'ocr-status error';
                ocrText.textContent = '❌ Erro no OCR: ' + error.message;
            } finally {
                uploadSection.classList.remove('analyzing');
            }
        }
        
        function extractProductInfo(text) {
            let productName = '';
            let price = '';
            let currency = 'guarani';
            
            const cleanText = text.replace(/\n/g, ' ').trim();
            
            const pricePatterns = [
                /(?:R\$|RS)\s*(\d{1,3}(?:[.,]\d{3})*(?:[.,]\d{2})?)/i,
                /(?:US\$|USD)\s*(\d{1,3}(?:[.,]\d{3})*(?:[.,]\d{2})?)/i,
                /₲\s*(\d{1,3}(?:[.,]\d{3})*)/i,
                /Gs\s*(\d{1,3}(?:[.,]\d{3})*)/i,
                /(\d{1,3}(?:[.,]\d{3}){2,})/,
                /(\d{1,3}[.,]\d{2})/
            ];
            
            for (let pattern of pricePatterns) {
                const match = cleanText.match(pattern);
                if (match) {
                    price = match[1].replace(/[.,]/g, '');
                    
                    if (cleanText.match(/R\$|RS|Real/i)) {
                        currency = 'real';
                        if (price.length > 2) price = price.slice(0, -2) + '.' + price.slice(-2);
                    } else if (cleanText.match(/US\$|USD|Dólar|Dollar/i)) {
                        currency = 'dolar';
                        if (price.length > 2) price = price.slice(0, -2) + '.' + price.slice(-2);
                    } else if (cleanText.match(/₲|Gs|Guarani/i) || price.length >= 5) {
                        currency = 'guarani';
                    }
                    break;
                }
            }
            
            const lines = text.split('\n').filter(l => l.trim().length > 3);
            if (lines.length > 0) {
                for (let line of lines) {
                    if (line.length > 5 && !/^\d+$/.test(line.trim())) {
                        productName = line.trim().substring(0, 100);
                        break;
                    }
                }
            }
            
            return { productName, price, currency };
        }
        
        function updatePriceLabel() {
            const labels = {
                'guarani': '💵 Preço (₲):',
                'dolar': '💵 Preço (US$):',
                'real': '💵 Preço (R$):'
            };
            document.getElementById('priceLabel').textContent = labels[currencySelect.value];
        }
        
        currencySelect.addEventListener('change', updatePriceLabel);
        
        specialRegimeSelect.addEventListener('change', () => {
            const regime = specialRegimeSelect.value;
            const infos = {
                'none': 'Regime normal: 60% de Imposto de Importação.',
                'remessaconforme': 'Remessa Conforme: 17% para compras online até US$ 3.000.',
                'rtu_online': 'RTU Online: 60% para remessas expressas internacionais via courier/encomendas aéreas.',
                'rtu_presencial': 'RTU Presencial: 60% de imposto aplicado em compras presenciais no Paraguai ao cruzar a fronteira. Regime de Tributação Unificada para bagagem acompanhada.',
                'isencao': 'Isenção: Até US$ 1.000 via terrestre para pessoa física.',
                'courier': 'Courier: 60% II + ICMS. Processo rápido.',
                'drawback': 'Drawback (PJ): Suspensão de impostos para exportadores.',
                'zona_franca': 'Zona Franca: Incentivos fiscais especiais.',
                'ex_tarifario': 'Ex-Tarifário (PJ): Redução para bens sem similar nacional.'
            };
            
            regimeInfo.textContent = infos[regime] || '';
            regimeInfo.style.display = regime === 'none' ? 'none' : 'block';
        });
        
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
        
        function calculateTaxes(priceBRL, priceUSD, personType, regime) {
            let taxRate = 0.60;
            let taxAmount = priceBRL * taxRate;
            let taxDescription = 'II (60%)';
            
            if (regime === 'remessaconforme' && priceUSD <= 3000) {
                taxRate = 0.17;
                taxAmount = priceBRL * taxRate;
                taxDescription = 'Remessa Conforme (17%)';
            } else if (regime === 'rtu_online' || regime === 'rtu_presencial') {
                taxRate = 0.60;
                taxAmount = priceBRL * taxRate;
                taxDescription = regime === 'rtu_online' ? 'RTU Online (60%)' : 'RTU Presencial (60%)';
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
        
        function calculateBestCurrency(price, currency) {
            const rates = getExchangeRates();
            const priceBRL = convertToBRL(price, currency);
            const priceUSD = priceBRL / rates.USD_TO_BRL;
            const priceGuarani = priceUSD * rates.USD_TO_GUARANI;
            
            let results = {
                guarani: { value: priceGuarani, text: `₲ ${priceGuarani.toLocaleString('pt-BR', {maximumFractionDigits: 0})}` },
                dolar: { value: priceUSD, text: `US$ ${priceUSD.toFixed(2)}` },
                real: { value: priceBRL, text: `R$ ${priceBRL.toFixed(2)}` }
            };
            
            let best = 'real';
            let bestValueBRL = priceBRL;
            
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
                
                const { results: currencyResults, best } = calculateBestCurrency(price, currency);
                const bestCurrencyNames = {
                    'guarani': 'Guarani (₲)',
                    'dolar': 'Dólar (US$)',
                    'real': 'Real (R$)'
                };
                
                document.getElementById('bestCurrencyText').innerHTML = `
                    💎 MELHOR MOEDA: <strong>${bestCurrencyNames[best]}</strong><br>
                    <small style="font-size: 14px; opacity: 0.9;">
                        ${currencyResults.guarani.text} • 
                        ${currencyResults.dolar.text} • 
                        ${currencyResults.real.text}
                    </small>
                `;
                
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
                        💵 ${item.price.toLocaleString('pt-BR')} (${item.currency})<br>
                        👤 ${item.personType === 'fisica' ? 'PF' : 'PJ'} • 🎯 ${item.regime}<br>
                        💎 Melhor: ${item.bestCurrency}<br>
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
            if (confirm('Limpar todo o histórico?')) {
                localStorage.removeItem('comparapy_history');
                loadHistory();
            }
        }
        
        // ============================================
        // SISTEMA DE PUBLICIDADE E MARKETING
        // ============================================
        
        let selectedColor = 'yellow';
        const colorGradients = {
            yellow: 'linear-gradient(135deg, #fef3c7 0%, #fde68a 100%)',
            blue: 'linear-gradient(135deg, #dbeafe 0%, #bfdbfe 100%)',
            green: 'linear-gradient(135deg, #dcfce7 0%, #bbf7d0 100%)',
            pink: 'linear-gradient(135deg, #fce7f3 0%, #fbcfe8 100%)',
            purple: 'linear-gradient(135deg, #f3e8ff 0%, #e9d5ff 100%)',
            red: 'linear-gradient(135deg, #fee2e2 0%, #fecaca 100%)'
        };
        
        // Abrir gerenciador de anúncios
        function openAdManager() {
            document.getElementById('adModal').classList.add('active');
            loadAdData();
        }
        
        // Fechar gerenciador
        function closeAdManager() {
            document.getElementById('adModal').classList.remove('active');
        }
        
        // Carregar dados do anúncio
        function loadAdData() {
            const bannerId = document.getElementById('adBannerSelect').value;
            const adData = JSON.parse(localStorage.getItem(`ad_banner_${bannerId}`)) || {
                title: 'Anuncie Aqui!',
                subtitle: bannerId === '1' ? 'Seu negócio em destaque' : 'Alcance milhares de compradores',
                icon: bannerId === '1' ? '🏪' : '💼',
                link: '',
                phone: '',
                color: bannerId === '1' ? 'yellow' : 'blue'
            };
            
            document.getElementById('adTitle').value = adData.title;
            document.getElementById('adSubtitle').value = adData.subtitle;
            document.getElementById('adIcon').value = adData.icon;
            document.getElementById('adLink').value = adData.link || '';
            document.getElementById('adPhone').value = adData.phone || '';
            
            selectedColor = adData.color;
            document.querySelectorAll('.color-option').forEach(opt => {
                opt.classList.remove('selected');
                if (opt.dataset.color === selectedColor) {
                    opt.classList.add('selected');
                }
            });
            
            updatePreview();
        }
        
        // Atualizar prévia em tempo real
        document.getElementById('adTitle').addEventListener('input', updatePreview);
        document.getElementById('adSubtitle').addEventListener('input', updatePreview);
        document.getElementById('adIcon').addEventListener('change', updatePreview);
        
        function updatePreview() {
            const title = document.getElementById('adTitle').value || 'Título do Anúncio';
            const subtitle = document.getElementById('adSubtitle').value || 'Subtítulo do anúncio';
            const icon = document.getElementById('adIcon').value;
            
            document.getElementById('previewTitle').textContent = title;
            document.getElementById('previewSubtitle').textContent = subtitle;
            document.getElementById('previewIcon').textContent = icon;
            document.getElementById('adPreview').style.background = colorGradients[selectedColor];
        }
        
        // Selecionar cor
        function selectColor(element) {
            document.querySelectorAll('.color-option').forEach(opt => opt.classList.remove('selected'));
            element.classList.add('selected');
            selectedColor = element.dataset.color;
            updatePreview();
        }
        
        // Salvar anúncio
        function saveAd() {
            const bannerId = document.getElementById('adBannerSelect').value;
            const title = document.getElementById('adTitle').value;
            const subtitle = document.getElementById('adSubtitle').value;
            const icon = document.getElementById('adIcon').value;
            const link = document.getElementById('adLink').value;
            const phone = document.getElementById('adPhone').value;
            
            if (!title || !subtitle) {
                alert('⚠️ Preencha título e subtítulo!');
                return;
            }
            
            const adData = {
                title,
                subtitle,
                icon,
                link,
                phone,
                color: selectedColor
            };
            
            localStorage.setItem(`ad_banner_${bannerId}`, JSON.stringify(adData));
            
            // Atualizar banner na página
            updateBannerDisplay(bannerId, adData);
            
            alert('✅ Anúncio salvo com sucesso!');
            closeAdManager();
        }
        
        // Atualizar exibição do banner
        function updateBannerDisplay(bannerId, adData) {
            const banner = document.getElementById(`adBanner${bannerId}`);
            const icon = banner.querySelector('.ad-icon');
            const title = banner.querySelector('.ad-title');
            const subtitle = banner.querySelector('.ad-subtitle');
            
            icon.textContent = adData.icon;
            title.textContent = adData.title;
            subtitle.textContent = adData.subtitle;
            banner.style.background = colorGradients[adData.color];
            
            // Salvar dados para clique
            banner.dataset.link = adData.link;
            banner.dataset.phone = adData.phone;
        }
        
        // Lidar com clique no anúncio
        function handleAdClick(bannerId) {
            const adData = JSON.parse(localStorage.getItem(`ad_banner_${bannerId}`));
            
            if (!adData) {
                openAdManager();
                document.getElementById('adBannerSelect').value = bannerId.toString();
                loadAdData();
                return;
            }
            
            // Registrar clique
            const clicks = JSON.parse(localStorage.getItem('ad_clicks') || '{}');
            clicks[bannerId] = (clicks[bannerId] || 0) + 1;
            localStorage.setItem('ad_clicks', JSON.stringify(clicks));
            
            // Ações do clique
            if (adData.phone) {
                const msg = encodeURIComponent(`Olá! Vi seu anúncio no Compara PY-BR e gostaria de mais informações.`);
                window.open(`https://wa.me/${adData.phone}?text=${msg}`, '_blank');
            } else if (adData.link) {
                window.open(adData.link, '_blank');
            } else {
                alert('📢 Entre em contato com o anunciante!\n\n' + adData.title + '\n' + adData.subtitle);
            }
        }
        
        // Fechar modal ao clicar fora
        document.getElementById('adModal').addEventListener('click', (e) => {
            if (e.target.id === 'adModal') {
                closeAdManager();
            }
        });
    </script>
</body>
</html>
