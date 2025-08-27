<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
    <meta name="theme-color" content="#2E8B57" />
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
    <title>Ngôi Làng Của Gió - Windy Village</title>
    <link rel="manifest" href="/manifest.json" />
    <link rel="icon" type="image/png" href="/assets/icons/icon-192.png" />
    <link rel="apple-touch-icon" href="/assets/icons/icon-192.png" />
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: #1a1a1a;
            overflow: hidden;
            font-family: 'Arial', sans-serif;
            touch-action: none;
            user-select: none;
            -webkit-user-select: none;
            -webkit-touch-callout: none;
        }
        
        #game-container {
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #2E8B57, #3CB371);
        }
        
        canvas {
            border: none;
            display: block;
            max-width: 100%;
            max-height: 100%;
        }
        
        #loading {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            font-size: 24px;
            text-align: center;
            z-index: 1000;
        }
        
        #audio-button {
            position: absolute;
            top: 20px;
            right: 20px;
            padding: 10px 20px;
            background: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            z-index: 1001;
        }
        
        #audio-button:hover {
            background: #45a049;
        }
        
        .touch-controls {
            position: absolute;
            pointer-events: none;
            z-index: 999;
        }
        
        .touch-controls.active {
            pointer-events: auto;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <div id="loading">Loading Windy Village...</div>
        <button id="audio-button" style="display: none;">Enable Sound</button>
    </div>
    <script type="module" src="/src/main.ts"></script>
</body>
</html>