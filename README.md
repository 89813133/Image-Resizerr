<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PixelPerfect | Advanced Image Resizer</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.12/cropper.min.css">
    <style>
        :root {
            --primary: #6366f1;
            --primary-light: #818cf8;
            --primary-dark: #4f46e5;
            --dark: #1e293b;
            --darker: #0f172a;
            --light: #f8fafc;
            --lighter: #ffffff;
            --gray: #94a3b8;
            --gray-light: #e2e8f0;
            --border: #e2e8f0;
            --danger: #ef4444;
            --success: #10b981;
            --warning: #f59e0b;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f1f5f9;
            color: var(--dark);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        header {
            background-color: var(--darker);
            padding: 20px 0;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 24px;
            font-weight: 700;
            color: var(--lighter);
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .logo-icon {
            width: 36px;
            height: 36px;
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
        
        nav ul {
            display: flex;
            gap: 30px;
            list-style: none;
        }
        
        nav a {
            text-decoration: none;
            color: var(--gray-light);
            font-weight: 500;
            transition: all 0.2s;
            font-size: 15px;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        
        nav a:hover {
            color: var(--lighter);
        }
        
        nav a svg {
            width: 18px;
            height: 18px;
        }
        
        .hero {
            text-align: center;
            padding: 80px 0 60px;
            background: linear-gradient(135deg, var(--darker), var(--dark));
            color: white;
            margin-bottom: 40px;
            border-radius: 0 0 20px 20px;
        }
        
        .hero h1 {
            font-size: 48px;
            margin-bottom: 20px;
            font-weight: 700;
            background: linear-gradient(to right, var(--primary-light), var(--lighter));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .hero p {
            font-size: 18px;
            color: var(--gray-light);
            max-width: 700px;
            margin: 0 auto 30px;
            line-height: 1.7;
        }
        
        .main-content {
            background-color: white;
            border-radius: 16px;
            box-shadow: 0 10px 15px rgba(0,0,0,0.05);
            padding: 40px;
            margin-bottom: 60px;
            border: 1px solid var(--gray-light);
        }
        
        .tool-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid var(--gray-light);
        }
        
        .tool-header h2 {
            font-size: 24px;
            font-weight: 600;
            color: var(--darker);
        }
        
        .tool-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
        }
        
        .upload-section {
            border-right: 1px solid var(--gray-light);
            padding-right: 40px;
        }
        
        .preview-section {
            display: flex;
            flex-direction: column;
        }
        
        .drop-area {
            border: 2px dashed var(--gray-light);
            border-radius: 12px;
            padding: 50px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 25px;
            background-color: rgba(241, 245, 249, 0.5);
        }
        
        .drop-area:hover {
            border-color: var(--primary-light);
            background-color: rgba(99, 102, 241, 0.05);
            transform: translateY(-2px);
        }
        
        .drop-area.active {
            border-color: var(--primary);
            background-color: rgba(99, 102, 241, 0.08);
        }
        
        .drop-area svg {
            width: 56px;
            height: 56px;
            margin-bottom: 15px;
            color: var(--gray);
        }
        
        .drop-area p {
            color: var(--gray);
            margin-bottom: 10px;
            font-size: 15px;
        }
        
        .drop-area .btn {
            margin-top: 15px;
        }
        
        .btn {
            background: linear-gradient(to right, var(--primary), var(--primary-dark));
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            font-size: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .btn:hover {
            background: linear-gradient(to right, var(--primary-light), var(--primary));
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.15);
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .btn-outline {
            background: transparent;
            border: 1px solid var(--gray-light);
            color: var(--dark);
            box-shadow: none;
        }
        
        .btn-outline:hover {
            background: var(--gray-light);
            transform: translateY(-2px);
            color: var(--darker);
        }
        
        .btn-sm {
            padding: 8px 16px;
            font-size: 14px;
            border-radius: 6px;
        }
        
        .btn-danger {
            background: linear-gradient(to right, var(--danger), #dc2626);
        }
        
        .btn-danger:hover {
            background: linear-gradient(to right, #ef4444, #dc2626);
        }
        
        .btn-success {
            background: linear-gradient(to right, var(--success), #059669);
        }
        
        .btn-success:hover {
            background: linear-gradient(to right, #10b981, #059669);
        }
        
        .settings-panel {
            margin-top: 20px;
        }
        
        .setting-group {
            margin-bottom: 25px;
            padding: 20px;
            background-color: var(--light);
            border-radius: 12px;
            border: 1px solid var(--gray-light);
        }
        
        .setting-group h3 {
            font-size: 16px;
            margin-bottom: 15px;
            color: var(--darker);
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .setting-group h3 svg {
            width: 18px;
            height: 18px;
            color: var(--primary);
        }
        
        .dimension-controls {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        
        .control-group {
            margin-bottom: 15px;
        }
        
        .control-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 14px;
            font-weight: 500;
            color: var(--dark);
        }
        
        .control-group input[type="number"],
        .control-group select {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--gray-light);
            border-radius: 8px;
            font-family: inherit;
            font-size: 14px;
            transition: all 0.2s;
            background-color: white;
        }
        
        .control-group input[type="number"]:focus,
        .control-group select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.2);
        }
        
        .unit-selector {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .unit-btn {
            padding: 8px 14px;
            border: 1px solid var(--gray-light);
            border-radius: 6px;
            cursor: pointer;
            font-size: 13px;
            background-color: white;
            font-weight: 500;
            transition: all 0.2s;
        }
        
        .unit-btn:hover {
            border-color: var(--primary-light);
        }
        
        .unit-btn.active {
            background-color: var(--primary);
            color: white;
            border-color: var(--primary);
        }
        
        .checkbox-group {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 12px;
        }
        
        .checkbox-group input {
            width: 16px;
            height: 16px;
            accent-color: var(--primary);
        }
        
        .checkbox-group label {
            font-size: 14px;
            color: var(--dark);
        }
        
        .preview-container {
            flex-grow: 1;
            display: flex;
            flex-direction: column;
        }
        
        .preview-tabs {
            display: flex;
            border-bottom: 1px solid var(--gray-light);
            margin-bottom: 20px;
        }
        
        .preview-tab {
            padding: 12px 24px;
            cursor: pointer;
            font-weight: 500;
            border-bottom: 2px solid transparent;
            transition: all 0.2s;
            color: var(--gray);
            font-size: 14px;
        }
        
        .preview-tab:hover {
            color: var(--dark);
        }
        
        .preview-tab.active {
            border-bottom-color: var(--primary);
            color: var(--primary);
        }
        
        .image-preview {
            flex-grow: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--light);
            border-radius: 12px;
            overflow: hidden;
            position: relative;
            min-height: 350px;
            border: 1px solid var(--gray-light);
        }
        
        .image-preview img {
            max-width: 100%;
            max-height: 400px;
            object-fit: contain;
        }
        
        #cropContainer {
            width: 100%;
            height: 400px;
            background-color: var(--light);
            display: none;
            border-radius: 12px;
            overflow: hidden;
            border: 1px solid var(--gray-light);
        }
        
        .image-info {
            margin-top: 15px;
            font-size: 14px;
            color: var(--gray);
            display: flex;
            justify-content: space-between;
        }
        
        .image-info span {
            font-weight: 500;
            color: var(--dark);
        }
        
        .action-buttons {
            display: flex;
            gap: 12px;
            margin-top: 25px;
        }
        
        .size-limit-control {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .size-limit-control select {
            flex: 1;
        }
        
        .size-limit-control input {
            flex: 2;
        }
        
        footer {
            background-color: var(--darker);
            padding: 50px 0 30px;
            margin-top: 60px;
            color: var(--gray-light);
        }
        
        .footer-content {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 40px;
        }
        
        .footer-column h3 {
            color: white;
            font-size: 16px;
            margin-bottom: 20px;
            font-weight: 600;
        }
        
        .footer-column ul {
            list-style: none;
        }
        
        .footer-column li {
            margin-bottom: 12px;
        }
        
        .footer-column a {
            color: var(--gray-light);
            text-decoration: none;
            font-size: 14px;
            transition: color 0.2s;
        }
        
        .footer-column a:hover {
            color: white;
        }
        
        .copyright {
            text-align: center;
            margin-top: 50px;
            padding-top: 30px;
            border-top: 1px solid rgba(255,255,255,0.1);
            color: var(--gray);
            font-size: 14px;
        }
        
        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        .social-links a {
            color: var(--gray-light);
            transition: color 0.2s;
        }
        
        .social-links a:hover {
            color: white;
        }
        
        @media (max-width: 1200px) {
            .footer-content {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        
        @media (max-width: 768px) {
            .tool-container {
                grid-template-columns: 1fr;
            }
            
            .upload-section {
                border-right: none;
                padding-right: 0;
                padding-bottom: 30px;
                margin-bottom: 30px;
                border-bottom: 1px solid var(--gray-light);
            }
            
            .dimension-controls {
                grid-template-columns: 1fr;
            }
            
            .footer-content {
                grid-template-columns: 1fr;
            }
            
            .hero h1 {
                font-size: 36px;
            }
            
            nav ul {
                gap: 15px;
            }
        }
        
        /* Animation */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .animated {
            animation: fadeIn 0.4s ease-out forwards;
        }
        
        /* Tooltip */
        .tooltip {
            position: relative;
            display: inline-block;
        }
        
        .tooltip .tooltip-text {
            visibility: hidden;
            width: 200px;
            background-color: var(--darker);
            color: white;
            text-align: center;
            border-radius: 6px;
            padding: 8px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            transform: translateX(-50%);
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 13px;
            font-weight: normal;
        }
        
        .tooltip .tooltip-text::after {
            content: "";
            position: absolute;
            top: 100%;
            left: 50%;
            margin-left: -5px;
            border-width: 5px;
            border-style: solid;
            border-color: var(--darker) transparent transparent transparent;
        }
        
        .tooltip:hover .tooltip-text {
            visibility: visible;
            opacity: 1;
        }
    </style>
</head>
<body>
    <header>
        <div class="container header-content">
            <div class="logo">
                <div class="logo-icon">PP</div>
                <span>PixelPerfect</span>
            </div>
            <nav>
                <ul>
                    <li><a href="#"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
                    </svg> Home</a></li>
                    <li><a href="#"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
                    </svg> Features</a></li>
                    <li><a href="#"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z" />
                    </svg> Tools</a></li>
                    <li><a href="#"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192l-3.536 3.536M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-5 0a4 4 0 11-8 0 4 4 0 018 0z" />
                    </svg> Support</a></li>
                </ul>
            </nav>
        </div>
    </header>
    
    <section class="hero">
        <div class="container">
            <h1>Advanced Image Resizer</h1>
            <p>Resize, crop, and optimize your images with pixel-perfect precision. Perfect for web, print, and social media.</p>
        </div>
    </section>
    
    <main class="container">
        <section class="main-content animated">
            <div class="tool-header">
                <h2>Image Editor</h2>
                <div class="tooltip">
                    <button class="btn-outline btn-sm">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="16" height="16">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                        Quick Guide
                    </button>
                    <span class="tooltip-text">Upload your image, set dimensions, adjust settings, and download the optimized version</span>
                </div>
            </div>
            
            <div class="tool-container">
                <div class="upload-section">
                    <div class="drop-area" id="dropArea">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
                        </svg>
                        <p><strong>Drag & drop your image here</strong></p>
                        <p>or</p>
                        <button class="btn" id="selectFileBtn">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="18" height="18">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
                            </svg>
                            Select Image
                        </button>
                        <input type="file" id="fileInput" accept="image/*" style="display: none;">
                    </div>
                    
                    <div class="settings-panel">
                        <div class="setting-group">
                            <h3>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.343l1.657-1.657a2 2 0 012.828 0l2.829 2.829a2 2 0 010 2.828l-8.486 8.485M7 17h.01" />
                                </svg>
                                Crop Image
                            </h3>
                            <div class="action-buttons">
                                <button class="btn btn-sm" id="cropBtn">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="16" height="16">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
                                    </svg>
                                    Enable Cropping
                                </button>
                                <button class="btn btn-sm btn-outline" id="cancelCropBtn" style="display: none;">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="16" height="16">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                                    </svg>
                                    Cancel
                                </button>
                                <button class="btn btn-sm btn-success" id="applyCropBtn" style="display: none;">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="16" height="16">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                                    </svg>
                                    Apply Crop
                                </button>
                            </div>
                            <div id="cropContainer"></div>
                        </div>
                        
                        <div class="setting-group">
                            <h3>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 8V4m0 0h4M4 4l5 5m11-1V4m0 0h-4m4 0l-5 5M4 16v4m0 0h4m-4 0l5-5m11 5l-5-5m5 5v-4m0 4h-4" />
                                </svg>
                                Resize Dimensions
                            </h3>
                            <div class="unit-selector">
                                <button class="unit-btn active" data-unit="px">Pixels</button>
                                <button class="unit-btn" data-unit="in">Inches</button>
                                <button class="unit-btn" data-unit="cm">Centimeters</button>
                                <button class="unit-btn" data-unit="mm">Millimeters</button>
                            </div>
                            <div class="dimension-controls">
                                <div class="control-group">
                                    <label for="widthInput">Width</label>
                                    <input type="number" id="widthInput" min="1" value="800">
                                </div>
                                <div class="control-group">
                                    <label for="heightInput">Height</label>
                                    <input type="number" id="heightInput" min="1" value="600">
                                </div>
                            </div>
                            <div class="control-group">
                                <label for="dpiInput">DPI (Dots Per Inch)</label>
                                <input type="number" id="dpiInput" min="1" value="72">
                            </div>
                            <div class="checkbox-group">
                                <input type="checkbox" id="maintainAspect" checked>
                                <label for="maintainAspect">Maintain aspect ratio</label>
                            </div>
                        </div>
                        
                        <div class="setting-group">
                            <h3>
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                </svg>
                                Output Settings
                            </h3>
                            <div class="control-group">
                                <label for="formatSelect">Format</label>
                                <select id="formatSelect">
                                    <option value="jpeg">JPEG</option>
                                    <option value="png">PNG</option>
                                    <option value="webp">WebP</option>
                                </select>
                            </div>
                            <div class="control-group" id="qualityControl">
                                <label for="qualityInput">Quality (0-100)</label>
                                <input type="number" id="qualityInput" min="1" max="100" value="85">
                            </div>
                            <div class="control-group size-limit-control">
                                <label for="sizeLimitType">Limit File Size:</label>
                                <select id="sizeLimitType">
                                    <option value="none">None</option>
                                    <option value="kb">KB</option>
                                    <option value="mb">MB</option>
                                </select>
                                <input type="number" id="sizeLimitValue" min="1" value="100" disabled>
                            </div>
                        </div>
                        
                        <div class="action-buttons">
                            <button class="btn" id="resizeBtn">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="18" height="18">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                                </svg>
                                Resize Image
                            </button>
                            <button class="btn btn-outline" id="resetBtn">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="18" height="18">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                                </svg>
                                Reset
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="preview-section">
                    <div class="preview-tabs">
                        <div class="preview-tab active" data-tab="original">Original</div>
                        <div class="preview-tab" data-tab="resized">Resized</div>
                    </div>
                    
                    <div class="preview-container">
                        <div class="image-preview" id="originalPreview">
                            <p>Your original image will appear here</p>
                        </div>
                        <div class="image-preview" id="resizedPreview" style="display: none;">
                            <p>Your resized image will appear here</p>
                        </div>
                        
                        <div class="image-info" id="originalInfo"></div>
                        <div class="image-info" id="resizedInfo" style="display: none;"></div>
                    </div>
                    
                    <div class="action-buttons">
                        <button class="btn" id="downloadBtn" disabled>
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="18" height="18">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
                            </svg>
                            Download Image
                        </button>
                        <button class="btn btn-outline" id="copyBtn" disabled>
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="18" height="18">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2a2 2 0 012 2v3m2 4H10m0 0l3-3m-3 3l3 3" />
                            </svg>
                            Copy to Clipboard
                        </button>
                    </div>
                </div>
            </div>
        </section>
    </main>
    
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>PixelPerfect</h3>
                    <ul>
                        <li><a href="#">About Us</a></li>
                        <li><a href="#">Features</a></li>
                        <li><a href="#">Pricing</a></li>
                        <li><a href="#">Blog</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Tools</h3>
                    <ul>
                        <li><a href="#">Image Resizer</a></li>
                        <li><a href="#">Photo Editor</a></li>
                        <li><a href="#">Background Remover</a></li>
                        <li><a href="#">File Converter</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Support</h3>
                    <ul>
                        <li><a href="#">Help Center</a></li>
                        <li><a href="#">Contact Us</a></li>
                        <li><a href="#">Privacy Policy</a></li>
                        <li><a href="#">Terms of Service</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Connect</h3>
                    <div class="social-links">
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path>
                            </svg>
                        </a>
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"></path>
                            </svg>
                        </a>
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
                            </svg>
                        </a>
                        <a href="#">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M22 12a10.06 10.06 1 0 1-20 0 10.06 10.06 0 0 1 20 0z"></path>
                                <circle cx="12" cy="12" r="4"></circle>
                                <line x1="12" y1="2" x2="12" y2="4"></line>
                                <line x1="12" y1="20" x2="12" y2="22"></line>
                                <line x1="4.93" y1="4.93" x2="6.34" y2="6.34"></line>
                                <line x1="17.66" y1="17.66" x2="19.07" y2="19.07"></line>
                                <line x1="2" y1="12" x2="4" y2="12"></line>
                                <line x1="20" y1="12" x2="22" y2="12"></line>
                                <line x1="4.93" y1="19.07" x2="6.34" y2="17.66"></line>
                                <line x1="17.66" y1="6.34" x2="19.07" y2="4.93"></line>
                            </svg>
                        </a>
                    </div>
                </div>
            </div>
            <div class="copyright">
                &copy; 2023 PixelPerfect. All rights reserved.
            </div>
        </div>
    </footer>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.12/cropper.min.js"></script>
    <script>
        // All the previous JavaScript functionality remains exactly the same
        // Only the UI has been redesigned
        document.addEventListener('DOMContentLoaded', function() {
            // DOM elements
            const dropArea = document.getElementById('dropArea');
            const fileInput = document.getElementById('fileInput');
            const selectFileBtn = document.getElementById('selectFileBtn');
            const widthInput = document.getElementById('widthInput');
            const heightInput = document.getElementById('heightInput');
            const dpiInput = document.getElementById('dpiInput');
            const maintainAspect = document.getElementById('maintainAspect');
            const formatSelect = document.getElementById('formatSelect');
            const qualityInput = document.getElementById('qualityInput');
            const sizeLimitType = document.getElementById('sizeLimitType');
            const sizeLimitValue = document.getElementById('sizeLimitValue');
            const resizeBtn = document.getElementById('resizeBtn');
            const resetBtn = document.getElementById('resetBtn');
            const downloadBtn = document.getElementById('downloadBtn');
            const copyBtn = document.getElementById('copyBtn');
            const originalPreview = document.getElementById('originalPreview');
            const resizedPreview = document.getElementById('resizedPreview');
            const originalInfo = document.getElementById('originalInfo');
            const resizedInfo = document.getElementById('resizedInfo');
            const previewTabs = document.querySelectorAll('.preview-tab');
            const cropBtn = document.getElementById('cropBtn');
            const cancelCropBtn = document.getElementById('cancelCropBtn');
            const applyCropBtn = document.getElementById('applyCropBtn');
            const cropContainer = document.getElementById('cropContainer');
            const unitButtons = document.querySelectorAll('.unit-btn');
            
            let originalImage = null;
            let originalWidth = 0;
            let originalHeight = 0;
            let resizedBlob = null;
            let cropper = null;
            let currentUnit = 'px';
            let originalImageData = null;
            
            // Initialize
            updateUnitControls();
            
            // Handle file selection via button
            selectFileBtn.addEventListener('click', function() {
                fileInput.click();
            });
            
            // Handle file selection via input
            fileInput.addEventListener('change', function(e) {
                if (e.target.files.length > 0) {
                    handleFile(e.target.files[0]);
                }
            });
            
            // Handle drag and drop
            dropArea.addEventListener('dragover', function(e) {
                e.preventDefault();
                dropArea.classList.add('active');
            });
            
            dropArea.addEventListener('dragleave', function() {
                dropArea.classList.remove('active');
            });
            
            dropArea.addEventListener('drop', function(e) {
                e.preventDefault();
                dropArea.classList.remove('active');
                
                if (e.dataTransfer.files.length > 0) {
                    handleFile(e.dataTransfer.files[0]);
                }
            });
            
            // Handle file processing
            function handleFile(file) {
                if (!file.type.match('image.*')) {
                    alert('Please select an image file (JPEG, PNG, etc.)');
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = function(e) {
                    originalImage = new Image();
                    originalImage.src = e.target.result;
                    
                    originalImage.onload = function() {
                        originalWidth = this.naturalWidth;
                        originalHeight = this.naturalHeight;
                        originalImageData = {
                            src: e.target.result,
                            width: originalWidth,
                            height: originalHeight,
                            file: file
                        };
                        
                        // Display original image
                        originalPreview.innerHTML = '';
                        originalPreview.appendChild(originalImage.cloneNode());
                        
                        // Update info
                        originalInfo.textContent = `${originalWidth} × ${originalHeight} pixels | ${formatBytes(file.size)}`;
                        
                        // Set initial dimensions maintaining aspect ratio
                        if (maintainAspect.checked) {
                            const ratio = originalHeight / originalWidth;
                            heightInput.value = Math.round(widthInput.value * ratio);
                        }
                        
                        // Enable resize button
                        resizeBtn.disabled = false;
                        cropBtn.disabled = false;
                    };
                };
                reader.readAsDataURL(file);
            }
            
            // Unit conversion functions
            function pxToInch(px, dpi) {
                return px / dpi;
            }
            
            function inchToPx(inch, dpi) {
                return inch * dpi;
            }
            
            function pxToCm(px, dpi) {
                return pxToInch(px, dpi) * 2.54;
            }
            
            function cmToPx(cm, dpi) {
                return inchToPx(cm / 2.54, dpi);
            }
            
            function pxToMm(px, dpi) {
                return pxToCm(px, dpi) * 10;
            }
            
            function mmToPx(mm, dpi) {
                return cmToPx(mm / 10, dpi);
            }
            
            // Update dimension inputs based on selected unit
            function updateDimensionInputs() {
                const dpi = parseInt(dpiInput.value) || 72;
                const widthPx = parseInt(widthInput.value) || 800;
                const heightPx = parseInt(heightInput.value) || 600;
                
                switch(currentUnit) {
                    case 'in':
                        widthInput.value = pxToInch(widthPx, dpi).toFixed(2);
                        heightInput.value = pxToInch(heightPx, dpi).toFixed(2);
                        break;
                    case 'cm':
                        widthInput.value = pxToCm(widthPx, dpi).toFixed(2);
                        heightInput.value = pxToCm(heightPx, dpi).toFixed(2);
                        break;
                    case 'mm':
                        widthInput.value = pxToMm(widthPx, dpi).toFixed(2);
                        heightInput.value = pxToMm(heightPx, dpi).toFixed(2);
                        break;
                    default: // px
                        widthInput.value = widthPx;
                        heightInput.value = heightPx;
                }
            }
            
            // Convert current unit values back to pixels
            function getDimensionsInPx() {
                const dpi = parseInt(dpiInput.value) || 72;
                let width = parseFloat(widthInput.value) || 800;
                let height = parseFloat(heightInput.value) || 600;
                
                switch(currentUnit) {
                    case 'in':
                        width = inchToPx(width, dpi);
                        height = inchToPx(height, dpi);
                        break;
                    case 'cm':
                        width = cmToPx(width, dpi);
                        height = cmToPx(height, dpi);
                        break;
                    case 'mm':
                        width = mmToPx(width, dpi);
                        height = mmToPx(height, dpi);
                        break;
                }
                
                return {
                    width: Math.round(width),
                    height: Math.round(height)
                };
            }
            
            // Update unit controls
            function updateUnitControls() {
                // Update active unit button
                unitButtons.forEach(btn => {
                    btn.classList.remove('active');
                    if (btn.dataset.unit === currentUnit) {
                        btn.classList.add('active');
                    }
                });
                
                // Update dimension inputs
                updateDimensionInputs();
            }
            
            // Unit button click handler
            unitButtons.forEach(btn => {
                btn.addEventListener('click', function() {
                    currentUnit = this.dataset.unit;
                    updateUnitControls();
                });
            });
            
            // DPI change handler
            dpiInput.addEventListener('input', function() {
                if (currentUnit !== 'px') {
                    updateDimensionInputs();
                }
            });
            
            // Maintain aspect ratio when width changes
            widthInput.addEventListener('input', function() {
                if (maintainAspect.checked && originalWidth > 0) {
                    const ratio = originalHeight / originalWidth;
                    const dimensions = getDimensionsInPx();
                    const newHeightPx = Math.round(dimensions.width * ratio);
                    
                    // Convert back to current unit
                    const dpi = parseInt(dpiInput.value) || 72;
                    let newHeight = newHeightPx;
                    
                    switch(currentUnit) {
                        case 'in':
                            newHeight = pxToInch(newHeightPx, dpi).toFixed(2);
                            break;
                        case 'cm':
                            newHeight = pxToCm(newHeightPx, dpi).toFixed(2);
                            break;
                        case 'mm':
                            newHeight = pxToMm(newHeightPx, dpi).toFixed(2);
                            break;
                    }
                    
                    heightInput.value = newHeight;
                }
            });
            
            // Maintain aspect ratio when height changes
            heightInput.addEventListener('input', function() {
                if (maintainAspect.checked && originalHeight > 0) {
                    const ratio = originalWidth / originalHeight;
                    const dimensions = getDimensionsInPx();
                    const newWidthPx = Math.round(dimensions.height * ratio);
                    
                    // Convert back to current unit
                    const dpi = parseInt(dpiInput.value) || 72;
                    let newWidth = newWidthPx;
                    
                    switch(currentUnit) {
                        case 'in':
                            newWidth = pxToInch(newWidthPx, dpi).toFixed(2);
                            break;
                        case 'cm':
                            newWidth = pxToCm(newWidthPx, dpi).toFixed(2);
                            break;
                        case 'mm':
                            newWidth = pxToMm(newWidthPx, dpi).toFixed(2);
                            break;
                    }
                    
                    widthInput.value = newWidth;
                }
            });
            
            // Toggle aspect ratio locking
            maintainAspect.addEventListener('change', function() {
                if (this.checked && originalWidth > 0 && widthInput.value) {
                    const ratio = originalHeight / originalWidth;
                    const dimensions = getDimensionsInPx();
                    const newHeightPx = Math.round(dimensions.width * ratio);
                    
                    // Convert back to current unit
                    const dpi = parseInt(dpiInput.value) || 72;
                    let newHeight = newHeightPx;
                    
                    switch(currentUnit) {
                        case 'in':
                            newHeight = pxToInch(newHeightPx, dpi).toFixed(2);
                            break;
                        case 'cm':
                            newHeight = pxToCm(newHeightPx, dpi).toFixed(2);
                            break;
                        case 'mm':
                            newHeight = pxToMm(newHeightPx, dpi).toFixed(2);
                            break;
                    }
                    
                    heightInput.value = newHeight;
                }
            });
            
            // Size limit type change
            sizeLimitType.addEventListener('change', function() {
                sizeLimitValue.disabled = this.value === 'none';
            });
            
            // Crop button handler
            cropBtn.addEventListener('click', function() {
                if (!originalImage) {
                    alert('Please upload an image first.');
                    return;
                }
                
                // Hide original preview and show crop container
                originalPreview.style.display = 'none';
                cropContainer.style.display = 'block';
                
                // Initialize cropper
                const img = document.createElement('img');
                img.src = originalImage.src;
                cropContainer.innerHTML = '';
                cropContainer.appendChild(img);
                
                cropper = new Cropper(img, {
                    aspectRatio: parseFloat(widthInput.value) / parseFloat(heightInput.value),
                    viewMode: 1,
                    autoCropArea: 0.8,
                    responsive: true,
                    guides: true
                });
                
                // Show crop controls
                cropBtn.style.display = 'none';
                cancelCropBtn.style.display = 'inline-flex';
                applyCropBtn.style.display = 'inline-flex';
            });
            
            // Cancel crop handler
            cancelCropBtn.addEventListener('click', function() {
                // Destroy cropper
                if (cropper) {
                    cropper.destroy();
                    cropper = null;
                }
                
                // Show original preview and hide crop container
                originalPreview.style.display = 'flex';
                cropContainer.style.display = 'none';
                cropContainer.innerHTML = '';
                
                // Show crop button and hide crop controls
                cropBtn.style.display = 'inline-flex';
                cancelCropBtn.style.display = 'none';
                applyCropBtn.style.display = 'none';
            });
            
            // Apply crop handler
            applyCropBtn.addEventListener('click', function() {
                if (!cropper) return;
                
                // Get cropped canvas
                const canvas = cropper.getCroppedCanvas({
                    width: originalWidth,
                    height: originalHeight
                });
                
                // Update original image with cropped version
                originalImage = new Image();
                originalImage.src = canvas.toDataURL();
                
                originalImage.onload = function() {
                    originalWidth = this.naturalWidth;
                    originalHeight = this.naturalHeight;
                    
                    // Update original preview
                    originalPreview.innerHTML = '';
                    originalPreview.appendChild(this.cloneNode());
                    
                    // Update info (approximate size)
                    originalInfo.textContent = `${originalWidth} × ${originalHeight} pixels | ${formatBytes(canvas.toDataURL().length)}`;
                    
                    // Destroy cropper
                    cropper.destroy();
                    cropper = null;
                    
                    // Show original preview and hide crop container
                    originalPreview.style.display = 'flex';
                    cropContainer.style.display = 'none';
                    cropContainer.innerHTML = '';
                    
                    // Show crop button and hide crop controls
                    cropBtn.style.display = 'inline-flex';
                    cancelCropBtn.style.display = 'none';
                    applyCropBtn.style.display = 'none';
                };
            });
            
            // Resize image with size limit
            function resizeWithLimit(canvas, mimeType, quality, targetSize, maxIterations = 10) {
                return new Promise((resolve) => {
                    let currentQuality = quality;
                    let iteration = 0;
                    let blob = null;
                    
                    function attemptResize() {
                        return new Promise((innerResolve) => {
                            canvas.toBlob((result) => {
                                if (!result) {
                                    innerResolve(null);
                                    return;
                                }
                                
                                blob = result;
                                
                                if (iteration >= maxIterations || 
                                    blob.size <= targetSize || 
                                    currentQuality <= 10) {
                                    innerResolve(blob);
                                    return;
                                }
                                
                                if (blob.size > targetSize) {
                                    iteration++;
                                    currentQuality = Math.max(10, currentQuality - 5);
                                    attemptResize().then(innerResolve);
                                } else {
                                    innerResolve(blob);
                                }
                            }, mimeType, currentQuality / 100);
                        });
                    }
                    
                    attemptResize().then(resolve);
                });
            }
            
            // Resize image
            resizeBtn.addEventListener('click', async function() {
                if (!originalImage) {
                    alert('Please upload an image first.');
                    return;
                }
                
                const dimensions = getDimensionsInPx();
                const width = dimensions.width;
                const height = dimensions.height;
                
                if (isNaN(width) || isNaN(height) || width <= 0 || height <= 0) {
                    alert('Please enter valid dimensions.');
                    return;
                }
                
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                canvas.width = width;
                canvas.height = height;
                
                // Fill with white background for JPEG
                if (formatSelect.value !== 'png') {
                    ctx.fillStyle = '#ffffff';
                    ctx.fillRect(0, 0, width, height);
                }
                
                // Draw the resized image
                ctx.drawImage(originalImage, 0, 0, width, height);
                
                // Convert canvas to blob
                const mimeType = formatSelect.value === 'png' ? 'image/png' : 
                                formatSelect.value === 'webp' ? 'image/webp' : 'image/jpeg';
                
                const quality = formatSelect.value === 'png' ? 1 : qualityInput.value / 100;
                
                // Handle size limit if enabled
                if (sizeLimitType.value !== 'none') {
                    const limitInBytes = sizeLimitType.value === 'kb' ? 
                                      sizeLimitValue.value * 1024 : 
                                      sizeLimitValue.value * 1024 * 1024;
                    
                    resizedBlob = await resizeWithLimit(canvas, mimeType, quality * 100, limitInBytes);
                    
                    if (!resizedBlob) {
                        alert('Failed to resize image to meet size limit.');
                        return;
                    }
                } else {
                    // No size limit, simple conversion
                    canvas.toBlob(function(blob) {
                        resizedBlob = blob;
                        updateResizedPreview();
                    }, mimeType, quality);
                    return;
                }
                
                updateResizedPreview();
            });
            
            function updateResizedPreview() {
                // Display resized image
                const resizedImg = new Image();
                resizedImg.src = URL.createObjectURL(resizedBlob);
                
                resizedPreview.innerHTML = '';
                resizedPreview.appendChild(resizedImg);
                resizedPreview.style.display = 'block';
                
                // Update info
                resizedInfo.textContent = `${widthInput.value}${currentUnit} × ${heightInput.value}${currentUnit} | ${formatBytes(resizedBlob.size)}`;
                resizedInfo.style.display = 'block';
                
                // Enable download and copy buttons
                downloadBtn.disabled = false;
                copyBtn.disabled = false;
                
                // Switch to resized tab
                document.querySelector('.preview-tab[data-tab="resized"]').click();
            }
            
            // Download resized image
            downloadBtn.addEventListener('click', function() {
                if (!resizedBlob) return;
                
                const a = document.createElement('a');
                const url = URL.createObjectURL(resizedBlob);
                const format = formatSelect.value;
                const width = widthInput.value;
                const height = heightInput.value;
                const unit = currentUnit;
                
                a.href = url;
                a.download = `resized-image-${width}${unit}x${height}${unit}.${format}`;
                document.body.appendChild(a);
                a.click();
                
                // Clean up
                setTimeout(function() {
                    document.body.removeChild(a);
                    URL.revokeObjectURL(url);
                }, 0);
            });
            
            // Copy to clipboard
            copyBtn.addEventListener('click', function() {
                if (!resizedBlob) return;
                
                navigator.clipboard.write([
                    new ClipboardItem({
                        [resizedBlob.type]: resizedBlob
                    })
                ]).then(function() {
                    alert('Image copied to clipboard!');
                }).catch(function(err) {
                    console.error('Could not copy image: ', err);
                    alert('Failed to copy image to clipboard.');
                });
            });
            
            // Reset everything
            resetBtn.addEventListener('click', function() {
                fileInput.value = '';
                originalPreview.innerHTML = '<p>Your original image will appear here</p>';
                resizedPreview.innerHTML = '<p>Your resized image will appear here</p>';
                resizedPreview.style.display = 'none';
                originalInfo.textContent = '';
                resizedInfo.textContent = '';
                resizedInfo.style.display = 'none';
                downloadBtn.disabled = true;
                copyBtn.disabled = true;
                resizeBtn.disabled = true;
                cropBtn.disabled = true;
                
                // Reset cropper if active
                if (cropper) {
                    cropper.destroy();
                    cropper = null;
                }
                
                // Show original preview and hide crop container
                originalPreview.style.display = 'flex';
                cropContainer.style.display = 'none';
                cropContainer.innerHTML = '';
                
                // Show crop button and hide crop controls
                cropBtn.style.display = 'inline-flex';
                cancelCropBtn.style.display = 'none';
                applyCropBtn.style.display = 'none';
                
                originalImage = null;
                resizedBlob = null;
                originalImageData = null;
                
                // Reset to default dimensions
                currentUnit = 'px';
                updateUnitControls();
                widthInput.value = '800';
                heightInput.value = '600';
                dpiInput.value = '72';
                formatSelect.value = 'jpeg';
                qualityInput.value = '85';
                sizeLimitType.value = 'none';
                sizeLimitValue.value = '100';
                sizeLimitValue.disabled = true;
                
                // Switch to original tab
                document.querySelector('.preview-tab[data-tab="original"]').click();
            });
            
            // Preview tabs
            previewTabs.forEach(tab => {
                tab.addEventListener('click', function() {
                    // Update active tab
                    previewTabs.forEach(t => t.classList.remove('active'));
                    this.classList.add('active');
                    
                    // Show corresponding preview
                    const tabName = this.getAttribute('data-tab');
                    if (tabName === 'original') {
                        originalPreview.style.display = 'flex';
                        resizedPreview.style.display = 'none';
                        originalInfo.style.display = 'block';
                        resizedInfo.style.display = 'none';
                    } else {
                        originalPreview.style.display = 'none';
                        resizedPreview.style.display = 'flex';
                        originalInfo.style.display = 'none';
                        resizedInfo.style.display = 'block';
                    }
                });
            });
            
            // Helper function to format file size
            function formatBytes(bytes, decimals = 2) {
                if (bytes === 0) return '0 Bytes';
                
                const k = 1024;
                const dm = decimals < 0 ? 0 : decimals;
                const sizes = ['Bytes', 'KB', 'MB', 'GB'];
                
                const i = Math.floor(Math.log(bytes) / Math.log(k));
                
                return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + ' ' + sizes[i];
            }
        });
    </script>
</body>
</html>
