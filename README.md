<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PALETTIST</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f5f5f5;
            padding: 20px;
            transition: background-color 0.5s ease;
        }
        
        .app-container {
            width: 100%;
            max-width: 500px;
            background-color: white;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            padding: 20px;
            text-align: center;
        }
        
        .header {
            padding: 25px 20px 15px;
            margin-bottom: 20px;
        }
        
        h1 {
            color: #333;
            font-size: 28px;
            margin-bottom: 8px;
        }
        
        .subtitle {
            color: #666;
            font-size: 16px;
            margin-bottom: 10px;
        }
        
        .color-display {
            width: 100%;
            height: 250px;
            border-radius: 15px;
            margin-bottom: 30px;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: all 0.4s ease;
            box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        .color-name {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 15px 30px;
            border-radius: 50px;
            font-size: 24px;
            font-weight: 600;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            user-select: none;
        }
        
        .controls {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .tap-area {
            background-color: #4a6cf7;
            color: white;
            border: none;
            padding: 20px;
            font-size: 20px;
            font-weight: 600;
            border-radius: 15px;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.3s;
            box-shadow: 0 8px 20px rgba(74, 108, 247, 0.3);
            user-select: none;
        }
        
        .tap-area:active {
            transform: scale(0.98);
        }
        
        .color-history {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 25px;
            padding-top: 25px;
            border-top: 1px solid #eee;
        }
        
        .history-item {
            width: 40px;
            height: 40px;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.2s;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .history-item:hover {
            transform: scale(1.1);
        }
        
        .stats {
            display: flex;
            justify-content: space-around;
            background-color: #f9f9f9;
            padding: 15px;
            border-radius: 15px;
            margin-top: 20px;
        }
        
        .stat-item {
            text-align: center;
        }
        
        .stat-value {
            font-size: 28px;
            font-weight: 700;
            color: #4a6cf7;
        }
        
        .stat-label {
            font-size: 14px;
            color: #666;
            margin-top: 5px;
        }
        
        .instructions {
            background-color: #f0f7ff;
            padding: 15px;
            border-radius: 15px;
            margin-top: 25px;
            font-size: 15px;
            color: #555;
            line-height: 1.5;
            text-align: left;
        }
        
        .instructions i {
            color: #4a6cf7;
            margin-right: 8px;
        }
        
        .footer {
            margin-top: 25px;
            color: #888;
            font-size: 14px;
            text-align: center;
        }
        
        @media (max-width: 500px) {
            .app-container {
                padding: 15px;
            }
            
            h1 {
                font-size: 24px;
            }
            
            .color-display {
                height: 200px;
            }
            
            .color-name {
                font-size: 20px;
                padding: 12px 24px;
            }
            
            .tap-area {
                padding: 18px;
                font-size: 18px;
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <div class="header">
            <h1>PALETTIST</h1>
            <p class="subtitle">Tap the button to change colors</p>
        </div>
        
        <div class="color-display" id="colorDisplay">
            <div class="color-name" id="colorName">#4A6CF7</div>
        </div>
        
        <div class="controls">
            <button class="tap-area" id="changeColorBtn">
                <i class="fas fa-palette"></i> Tap to Change Color
            </button>
            
            <div class="stats">
                <div class="stat-item">
                    <div class="stat-value" id="clickCount">0</div>
                    <div class="stat-label">Clicks</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="colorCount">1</div>
                    <div class="stat-label">Colors Used</div>
                </div>
                <div class="stat-item">
                    <div class="stat-value" id="currentBrightness">85%</div>
                    <div class="stat-label">Brightness</div>
                </div>
            </div>
        </div>
        
        <div class="instructions">
            <p><i class="fas fa-info-circle"></i> <strong>How to use:</strong> Tap the blue button above to change the color. Tap on any color in the history section to return to that color.</p>
            <p><i class="fas fa-mobile-alt"></i> <strong>Mobile optimized:</strong> This app works perfectly on all mobile devices.</p>
        </div>
        
        <div class="color-history" id="colorHistory">
            <!-- Color history will be generated here -->
        </div>
        
        <div class="footer">
            <p>PALETTIST &copy; 2023 | Made with <i class="fas fa-heart" style="color:#e74c3c"></i></p>
        </div>
    </div>

    <script>
        // DOM elements
        const colorDisplay = document.getElementById('colorDisplay');
        const colorName = document.getElementById('colorName');
        const changeColorBtn = document.getElementById('changeColorBtn');
        const clickCountElement = document.getElementById('clickCount');
        const colorCountElement = document.getElementById('colorCount');
        const currentBrightnessElement = document.getElementById('currentBrightness');
        const colorHistoryElement = document.getElementById('colorHistory');
        const body = document.body;
        
        // App state
        let clickCount = 0;
        let colorsUsed = 1;
        let currentColor = '#4A6CF7';
        let colorHistory = [currentColor];
        
        // Predefined color palette
        const colorPalette = [
            '#4A6CF7', '#6C5CE7', '#A55EEA', '#FD79A8', '#FF7675',
            '#FDCB6E', '#00CEC9', '#00B894', '#55EFC4', '#74B9FF',
            '#0984E3', '#2D3436', '#636E72', '#B2BEC3', '#DFE6E9',
            '#6AB04C', '#F0932B', '#EB4D4B', '#4834D4', '#130F40'
        ];
        
        // Initialize the app
        function initApp() {
            updateColorHistory();
            updateStats();
            
            // Add click event to the button
            changeColorBtn.addEventListener('click', changeColor);
            
            // Also allow tapping the color display to change color
            colorDisplay.addEventListener('click', changeColor);
        }
        
        // Change color function
        function changeColor() {
            // Increment click count
            clickCount++;
            
            // Select a random color that's not the current one
            let newColor;
            do {
                newColor = colorPalette[Math.floor(Math.random() * colorPalette.length)];
            } while (newColor === currentColor && colorPalette.length > 1);
            
            // Update current color
            currentColor = newColor;
            
            // Add to history if it's a new color
            if (!colorHistory.includes(currentColor)) {
                colorHistory.push(currentColor);
                colorsUsed++;
            }
            
            // Update the UI
            updateColorDisplay();
            updateColorHistory();
            updateStats();
            
            // Add a subtle animation to the button
            changeColorBtn.style.transform = 'scale(0.98)';
            setTimeout(() => {
                changeColorBtn.style.transform = 'scale(1)';
            }, 150);
        }
        
        // Update the color display
        function updateColorDisplay() {
            colorDisplay.style.backgroundColor = currentColor;
            colorName.textContent = currentColor;
            
            // Calculate brightness to determine text color
            const brightness = calculateBrightness(currentColor);
            const textColor = brightness > 128 ? '#333' : '#FFF';
            colorName.style.color = textColor;
            
            // Update brightness stat
            const brightnessPercent = Math.round((brightness / 255) * 100);
            currentBrightnessElement.textContent = `${brightnessPercent}%`;
            
            // Also update body background for a cohesive look
            body.style.backgroundColor = adjustColorBrightness(currentColor, 90);
        }
        
        // Calculate brightness of a hex color
        function calculateBrightness(hexColor) {
            // Convert hex to RGB
            const r = parseInt(hexColor.slice(1, 3), 16);
            const g = parseInt(hexColor.slice(3, 5), 16);
            const b = parseInt(hexColor.slice(5, 7), 16);
            
            // Calculate brightness using the formula: (299*R + 587*G + 114*B) / 1000
            return (299 * r + 587 * g + 114 * b) / 1000;
        }
        
        // Adjust color brightness
        function adjustColorBrightness(hexColor, percent) {
            // Convert hex to RGB
            let r = parseInt(hexColor.slice(1, 3), 16);
            let g = parseInt(hexColor.slice(3, 5), 16);
            let b = parseInt(hexColor.slice(5, 7), 16);
            
            // Adjust brightness
            r = Math.min(255, Math.max(0, Math.round(r * percent / 100)));
            g = Math.min(255, Math.max(0, Math.round(g * percent / 100)));
            b = Math.min(255, Math.max(0, Math.round(b * percent / 100)));
            
            // Convert back to hex
            return `#${r.toString(16).padStart(2, '0')}${g.toString(16).padStart(2, '0')}${b.toString(16).padStart(2, '0')}`;
        }
        
        // Update color history display
        function updateColorHistory() {
            colorHistoryElement.innerHTML = '';
            
            // Show the last 10 colors used
            const recentColors = colorHistory.slice(-10);
            
            recentColors.forEach(color => {
                const historyItem = document.createElement('div');
                historyItem.className = 'history-item';
                historyItem.style.backgroundColor = color;
                historyItem.title = color;
                
                // Add click event to switch to this color
                historyItem.addEventListener('click', () => {
                    currentColor = color;
                    updateColorDisplay();
                    updateStats();
                });
                
                colorHistoryElement.appendChild(historyItem);
            });
        }
        
        // Update statistics
        function updateStats() {
            clickCountElement.textContent = clickCount;
            colorCountElement.textContent = colorsUsed;
        }
        
        // Initialize the app when the page loads
        window.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
