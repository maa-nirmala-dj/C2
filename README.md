<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>👑 MND HUB — Maa Nirmala DJ & Tent House | Advanced Premium Interface</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700;900&family=Outfit:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

    <style>
        /* =========================================================================
           ADVANCED RESET & CSS VARIABLES (Dynamic Color System)
           ========================================================================= */
        :root {
            --bg-base: #030303;
            --bg-panel: rgba(10, 10, 10, 0.85);
            
            --neon-pink: #FF00FF;
            --neon-pink-dim: rgba(255, 0, 255, 0.2);
            --neon-lime: #00FA9A;
            --neon-lime-dim: rgba(0, 250, 154, 0.2);
            --neon-cyan: #00E5FF;
            --neon-cyan-dim: rgba(0, 229, 255, 0.2);
            
            --text-main: #FFFFFF;
            --text-sub: #BBBBBB;

            --font-head: 'Cinzel', serif;
            --font-body: 'Outfit', sans-serif;
            --dynamic-shift: 15s;

            --header-height: 60px;
            --footer-height: 75px;
        }

        * {
            margin: 0; padding: 0; box-sizing: border-box;
            outline: none; user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        /* =========================================================================
           PERFECT DESKTOP & MOBILE RESPONSIVE MATRIX
           ========================================================================= */
        body, html {
            width: 100%; height: 100%;
            background-color: var(--bg-base); color: var(--text-main);
            font-family: var(--font-body); 
            display: flex; justify-content: center; align-items: center;
            overflow: hidden; 
            background-image: 
                radial-gradient(circle at 10% 20%, var(--neon-pink-dim), transparent 30%),
                radial-gradient(circle at 90% 80%, var(--neon-cyan-dim), transparent 30%),
                radial-gradient(circle at 50% 50%, #000 0%, #030303 100%);
            animation: bodyHueShift var(--dynamic-shift) infinite linear;
            transition: filter 0.3s ease;
        }

        @keyframes bodyHueShift {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }

        /* NATIVE APP CONTAINER BOUNDS */
        #app-container {
            width: 100%; max-width: 480px; 
            height: 100dvh; max-height: 900px; /* Limits height on ultra-wide desktops */
            background: #000;
            position: relative; overflow: hidden; 
            box-shadow: 0 0 50px rgba(0, 229, 255, 0.15), 0 0 100px rgba(255, 0, 255, 0.1);
            border: 1px solid rgba(255,255,255,0.05);
            border-radius: 30px; /* Gives a mobile phone feel on desktop */
            display: flex; flex-direction: column;
        }

        /* Auto-adjust for actual mobile screens */
        @media (max-width: 480px) {
            #app-container {
                max-width: 100%; height: 100dvh; max-height: none;
                border-radius: 0; border: none;
            }
        }

        /* ABSOLUTE POSITIONED HEADER - WILL NEVER MOVE */
        header {
            background: rgba(0, 0, 0, 0.95); padding: 0 15px; 
            border-bottom: 1px solid rgba(255,255,255,0.1);
            position: absolute; top: 0; left: 0; width: 100%;
            height: var(--header-height); z-index: 1000;
            display: flex; flex-direction: column; justify-content: center;
            backdrop-filter: blur(10px);
        }
        
        .header-top { display: flex; justify-content: space-between; align-items: center; }
        .logo-block { font-family: var(--font-head); font-weight: 900; font-size: 20px; color: var(--neon-lime); text-shadow: 0 0 10px var(--neon-lime); }
        .control-icons { display: flex; gap: 20px; color: #fff; font-size: 20px; cursor: pointer;}
        .control-icons i:hover { color: var(--neon-lime); }

        #nav-dropdown {
            display: none; position: absolute; top: 65px; right: 15px; 
            background: var(--bg-panel); border: 1px solid var(--neon-cyan); 
            padding: 12px; border-radius: 8px; z-index: 2000; backdrop-filter: blur(10px);
            box-shadow: 0 5px 20px rgba(0, 229, 255, 0.2);
        }

        /* ABSOLUTE POSITIONED MAIN CONTENT - ONLY THIS SCROLLS */
        #main-scroll-content { 
            position: absolute; top: var(--header-height); bottom: var(--footer-height); 
            left: 0; right: 0; overflow-y: auto; padding: 15px; padding-bottom: 30px; z-index: 5; 
        }
        #main-scroll-content::-webkit-scrollbar { width: 4px; }
        #main-scroll-content::-webkit-scrollbar-thumb { background: linear-gradient(to bottom, var(--neon-pink), var(--neon-cyan)); border-radius: 10px; }

        /* Typography & Shimmer */
        #perfect-intro { text-align: center; padding: 40px 0; border-radius: 15px; background: radial-gradient(circle at 50% 120%, var(--neon-lime-dim), transparent 60%); margin-bottom: 25px; position: relative; }
        #perfect-intro::before { content: ''; position: absolute; bottom: 0; left: 5%; width: 90%; height: 2px; background: linear-gradient(to right, transparent, var(--neon-lime), transparent); box-shadow: 0 0 10px var(--neon-lime); }
        
        .shimmering-title { font-family: var(--font-head); font-weight: 900; font-size: 28px; margin-bottom: 15px; background: linear-gradient(90deg, #fff 0%, #fff 45%, var(--neon-lime) 50%, #fff 55%, #fff 100%); background-size: 200% auto; -webkit-background-clip: text; -webkit-text-fill-color: transparent; animation: textShimmer 2.5s infinite linear; text-transform: uppercase; letter-spacing: 2px; }
        .shimmering-dj-title { font-family: var(--font-head); font-weight: 900; font-size: 20px; background: linear-gradient(90deg, #fff 0%, #fff 40%, var(--neon-pink) 50%, #fff 60%, #fff 100%); background-size: 200% auto; -webkit-background-clip: text; -webkit-text-fill-color: transparent; animation: textShimmer-dj 3s infinite linear; text-transform: uppercase; }
        
        @keyframes textShimmer { to { background-position: -200% center; } }
        @keyframes textShimmer-dj { to { background-position: 200% center; } }
        .intro-body-text { color: var(--text-sub); font-size: 14px; line-height: 1.6; margin-top: 10px; padding: 0 10px; }

        /* Panels */
        .category-glow-panel { background: #000; border-radius: 20px; padding: 1px; margin-bottom: 20px; position: relative; transition: transform 0.3s ease; }
        .category-glow-panel:hover { transform: scale(1.02); }
        .category-glow-panel::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%; border-radius: 20px; pointer-events: none; opacity: 0.9; box-shadow: inset 0 0 15px currentcolor, 0 0 15px currentcolor; }
        .category-content-inner { background: var(--bg-panel); backdrop-filter: blur(5px); border-radius: 19px; padding: 20px; text-align: center; }
        .category-title { font-family: var(--font-head); font-weight: 900; font-size: 20px; margin-bottom: 15px; display: flex; align-items: center; justify-content: center; gap: 10px; }
        .category-body { color: var(--text-sub); font-size: 12px; margin-bottom: 15px; opacity: 0.8; }
        
        .glow-category-btn-list { display: flex; justify-content: center; gap: 10px; flex-wrap: wrap; }
        .glow-category-btn-list button { background: #000; border: 1px solid currentcolor; border-radius: 6px; padding: 8px 18px; font-family: var(--font-head); font-size: 11px; font-weight: bold; color: #fff; cursor: pointer; text-shadow: 0 0 5px currentcolor; display: flex; align-items: center; gap: 6px; transition: 0.3s ease; }
        .glow-category-btn-list button:hover { color: #000; background: currentcolor; text-shadow: none; box-shadow: 0 0 10px currentcolor;}
        
        .panel-pink { color: var(--neon-pink); }
        .panel-lime { color: var(--neon-lime); }
        .panel-cyan { color: var(--neon-cyan); }

        /* ABSOLUTE POSITIONED OVERLAYS (Pages) */
        .app-overlay { 
            position: absolute; top: var(--header-height); left: 0; right: 0; bottom: var(--footer-height); 
            background: rgba(0,0,0,0.98); backdrop-filter: blur(15px); z-index: 500; 
            display: flex; flex-direction: column; transform: translateY(150%); 
            transition: transform 0.4s cubic-bezier(0.19, 1, 0.22, 1); border-top: 1px solid rgba(255,255,255,0.15); 
        }
        .app-overlay.active { transform: translateY(0); }
        .overlay-header { padding: 15px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.1); background: #050505; flex-shrink: 0;}
        .overlay-header h2 { font-family: var(--font-head); font-size: 18px; font-weight: bold; }
        .close-overlay-btn { color: #fff; opacity: 0.7; font-size: 22px; cursor: pointer; }
        .close-overlay-btn:hover { color: var(--neon-pink); opacity: 1; transform: scale(1.1);}
        .overlay-content-area { flex: 1; overflow-y: auto; padding: 15px; }

        /* FULL SCREEN SETTINGS / CONTROL CENTER */
        .settings-modal {
            position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0, 0, 0, 0.98); backdrop-filter: blur(20px);
            z-index: 2000; display: flex; flex-direction: column;
            transform: translateY(100%); transition: transform 0.4s cubic-bezier(0.19, 1, 0.22, 1);
        }
        .settings-modal.active { transform: translateY(0); }
        .settings-header-bar { padding: 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.1); background: #000; flex-shrink: 0;}
        .settings-content-grid { padding: 20px; overflow-y: auto; display: grid; grid-template-columns: 1fr 1fr; gap: 15px; align-content: start;}
        
        .hw-btn {
            background: #111; border: 1px solid var(--neon-lime); border-radius: 12px;
            padding: 25px 10px; text-align: center; color: #fff; font-family: var(--font-head);
            font-size: 11px; font-weight: bold; cursor: pointer; transition: 0.3s;
            box-shadow: inset 0 0 10px var(--neon-lime-dim); display: flex; flex-direction: column; align-items: center; justify-content: center;
        }
        .hw-btn i { font-size: 32px; color: var(--neon-lime); margin-bottom: 12px; transition: 0.3s;}
        .hw-btn:hover { background: var(--neon-lime-dim); transform: scale(1.05); }
        .hw-btn:hover i { color: #fff; filter: drop-shadow(0 0 5px #fff); }
        
        /* Interactive Media Feed Container */
        #media-feed-container {
            position: absolute; top: var(--header-height); bottom: var(--footer-height); left: 0; right: 0;
            background: #000; border-top: 2px solid var(--neon-cyan); border-bottom: 2px solid var(--neon-cyan);
            display: none; flex-direction: column; z-index: 1500; overflow: hidden;
        }
        #media-video { width: 100%; height: 100%; object-fit: cover; }
        .close-media-btn {
            position: absolute; top: 15px; right: 15px; background: rgba(0,0,0,0.8);
            color: var(--neon-pink); border: 1px solid var(--neon-pink); padding: 8px 15px;
            border-radius: 5px; cursor: pointer; font-family: var(--font-head); z-index: 1501; font-weight: bold;
        }

        /* Lockdown Overlay */
        #lockdown-overlay {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255, 0, 0, 0.95); z-index: 9999; display: none;
            flex-direction: column; justify-content: center; align-items: center;
            color: white; font-family: var(--font-head); text-align: center;
            border-radius: inherit; /* Matches desktop border radius */
        }
        .lockdown-text { font-size: 36px; font-weight: 900; letter-spacing: 5px; animation: flash 1s infinite; }
        @keyframes flash { 0%, 100% { opacity: 1; text-shadow: 0 0 30px red; } 50% { opacity: 0.5; } }

        /* Game Specific: Tic Tac Toe */
        .board { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-top: 20px; max-width: 320px; margin-left: auto; margin-right: auto; }
        .cell { background: #111; border: 1px solid var(--neon-pink); height: 90px; display: flex; justify-content: center; align-items: center; font-size: 45px; font-family: var(--font-head); color: #fff; cursor: pointer; border-radius: 8px; box-shadow: inset 0 0 15px var(--neon-pink-dim); }
        .cell:hover { background: var(--neon-pink-dim); }
        #game-status { text-align: center; margin-top: 20px; font-family: var(--font-body); color: var(--neon-pink); font-size: 18px; font-weight: bold; }

        /* Studio Specific: Drum Pad */
        .drum-pad { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; margin-top: 20px; }
        .pad { background: #111; border: 2px solid var(--neon-lime); height: 110px; border-radius: 12px; display: flex; justify-content: center; align-items: center; color: var(--neon-lime); font-family: var(--font-head); font-weight: bold; font-size: 16px; cursor: pointer; transition: 0.1s; box-shadow: 0 0 10px var(--neon-lime-dim); }
        .pad:active { transform: scale(0.9); background: var(--neon-lime); color: #000; box-shadow: 0 0 20px var(--neon-lime);}

        /* Creator Profile Specific */
        .profile-card { background: #111; border: 1px solid var(--neon-cyan); padding: 15px; border-radius: 10px; margin-bottom: 25px; display: flex; align-items: center; gap: 15px; box-shadow: 0 0 15px var(--neon-cyan-dim); }
        .profile-pic { width: 55px; height: 55px; border-radius: 50%; background: var(--neon-cyan); display: flex; justify-content: center; align-items: center; color: #000; font-size: 22px; font-weight: bold; font-family: var(--font-head); }
        .profile-info h4 { color: #fff; font-size: 18px; margin-bottom: 5px; font-family: var(--font-head);}
        .profile-info p { color: var(--text-sub); font-size: 13px; }

        /* =========================================================================
           PERFECT NATIVE ABSOLUTE FOOTER - GUARANTEED NOT TO MOVE
           ========================================================================= */
        footer { 
            position: absolute; bottom: 0; left: 0; right: 0; width: 100%; 
            height: var(--footer-height); background: rgba(0, 0, 0, 0.98); 
            border-top: 2px solid rgba(255,255,255,0.1); 
            display: flex; justify-content: space-around; align-items: center; 
            z-index: 2500; /* Extremely high z-index to stay above overlays */
            backdrop-filter: blur(15px);
            border-bottom-left-radius: inherit; /* Matches desktop app container */
            border-bottom-right-radius: inherit;
        }
        footer::before { content: ''; position: absolute; bottom: 0; left: 0; width: 100%; height: 5px; background: linear-gradient(to right, var(--neon-cyan), var(--neon-lime), var(--neon-pink)); box-shadow: 0 0 20px 5px var(--neon-lime); animation: bottomNavShine 3s infinite linear; border-bottom-left-radius: inherit; border-bottom-right-radius: inherit;}
        @keyframes bottomNavShine { 0% { box-shadow: 0 0 20px 5px var(--neon-lime); } 33% { box-shadow: 0 0 20px 5px var(--neon-cyan); } 66% { box-shadow: 0 0 20px 5px var(--neon-pink); } 100% { box-shadow: 0 0 20px 5px var(--neon-lime); } }
        
        .nav-item { display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; flex: 1; cursor: pointer; transition: all 0.2s ease; height: 100%;}
        .nav-icon { font-size: 22px; color: #555; transition: 0.3s ease; margin-bottom: 6px; }
        .nav-name { font-size: 11px; font-family: var(--font-body); color: #555; text-transform: uppercase; font-weight: 800; display: block; }
        
        .nav-item:hover .nav-icon { color: #fff; transform: translateY(-3px); }
        
        .nav-item[data-nav="home"].active .nav-icon, .nav-item[data-nav="home"].active .nav-name { color: var(--neon-cyan); text-shadow: 0 0 10px var(--neon-cyan); }
        .nav-item[data-nav="studio"].active .nav-icon, .nav-item[data-nav="studio"].active .nav-name { color: var(--neon-lime); text-shadow: 0 0 10px var(--neon-lime); }
        .nav-item[data-nav="game"].active .nav-icon, .nav-item[data-nav="game"].active .nav-name { color: var(--neon-pink); text-shadow: 0 0 10px var(--neon-pink); }
        .nav-item[data-nav="auth"].active .nav-icon, .nav-item[data-nav="auth"].active .nav-name { color: #fff; text-shadow: 0 0 10px #fff; }

    </style>
</head>
<body>
    <div id="app-container">
        
        <header>
            <div class="header-top">
                <div class="logo-block">👑 MND HUB</div>
                <div class="control-icons">
                    <i class="fas fa-cog" onclick="toggleSettings()"></i> 
                    <i class="fas fa-ellipsis-v" onclick="toggleMenu('nav-dropdown')"></i> 
                </div>
            </div>
            <div id="nav-dropdown">
                <div onclick="alert('Headquarters: Beltikri, Banka, Bihar.'); toggleMenu('nav-dropdown');" style="color:var(--neon-cyan); cursor:pointer; font-weight:bold; font-size:14px;">
                    <i class="fas fa-map-marker-alt"></i> Location Info
                </div>
            </div>
        </header>

        <div id="media-feed-container">
            <button class="close-media-btn" onclick="stopMedia()"><i class="fas fa-times"></i> CLOSE</button>
            <video id="media-video" autoplay playsinline></video>
            <div id="audio-visualizer" style="display:none; width:100%; height:100%; align-items:center; justify-content:center; flex-direction:column;">
                <i class="fas fa-microphone" style="font-size: 60px; color: var(--neon-lime); margin-bottom: 20px; animation: pulse 1s infinite;"></i>
                <p style="color: var(--neon-lime); font-family: var(--font-head); font-weight: bold;">MIC ACTIVE & LISTENING...</p>
            </div>
            <div id="location-display" style="display:none; width:100%; height:100%; align-items:center; justify-content:center; flex-direction:column; padding: 20px; text-align: center;">
                <i class="fas fa-satellite" style="font-size: 60px; color: var(--neon-cyan); margin-bottom: 20px;"></i>
                <p id="coords-text" style="color: var(--neon-cyan); font-family: var(--font-body); font-size: 16px; font-weight: bold;"></p>
            </div>
        </div>

        <div id="lockdown-overlay">
            <i class="fas fa-shield-alt" style="font-size: 90px; margin-bottom: 20px;"></i>
            <div class="lockdown-text">SYSTEM LOCKED</div>
            <p style="margin-top: 20px; font-family: var(--font-body); font-size: 14px;">Refresh application to restore access.</p>
        </div>

        <div id="settings-fullscreen" class="settings-modal">
            <div class="settings-header-bar">
                <h2 style="color: var(--neon-lime); text-shadow: 0 0 10px var(--neon-lime); margin: 0; font-family: var(--font-head); font-size: 18px;"><i class="fas fa-sliders-h"></i> CONTROL CENTER</h2>
                <i class="fas fa-times" style="font-size: 26px; color: #fff; cursor: pointer;" onclick="toggleSettings()"></i>
            </div>
            <div class="settings-content-grid">
                <div class="hw-btn" onclick="toggleFullScreen()">
                    <i class="fas fa-expand"></i>
                    <span>FULL SCREEN</span>
                </div>
                <div class="hw-btn" onclick="activateCamera()">
                    <i class="fas fa-camera"></i>
                    <span>CAMERA ON</span>
                </div>
                <div class="hw-btn" onclick="activateTorch()">
                    <i class="fas fa-bolt"></i>
                    <span>TORCH ON</span>
                </div>
                <div class="hw-btn" onclick="recordVideo()">
                    <i class="fas fa-video"></i>
                    <span id="record-text">RECORD VIDEO</span>
                </div>
                <div class="hw-btn" onclick="activateMic()">
                    <i class="fas fa-microphone"></i>
                    <span>LIVE MIC</span>
                </div>
                <div class="hw-btn" onclick="activateLocation()">
                    <i class="fas fa-map-marker-alt"></i>
                    <span>LOCATION ON</span>
                </div>
                <div class="hw-btn" onclick="toggleMaxBrightness()">
                    <i class="fas fa-sun"></i>
                    <span id="brightness-text">MAX BRIGHTNESS</span>
                </div>
                <div class="hw-btn" onclick="triggerLockdown()">
                    <i class="fas fa-shield-alt"></i>
                    <span style="color: red;">LOCKDOWN</span>
                </div>
            </div>
        </div>

        <div id="main-scroll-content">
            <section id="perfect-intro">
                <h1 class="shimmering-title">Experience The Grandeur</h1>
                <h2 class="shimmering-dj-title">Maa Nirmala DJ & Tent</h2>
                <p class="intro-body-text">Step into the domain of acoustic supremacy and majestic architecture. Perfect. Premium. Advance.</p>
            </section>

            <section class="category-glow-panel panel-cyan">
                <div class="category-content-inner">
                    <h3 class="category-title">Event Highlights <i class="fas fa-bolt" style="color:var(--neon-cyan);"></i></h3>
                    <p class="category-body">Premium streaming. Dangerous updates. Live feeds from operations.</p>
                    <div class="glow-category-btn-list">
                        <button onclick="activateCamera()">VIEW FEED</button>
                    </div>
                </div>
            </section>

            <section class="category-glow-panel panel-lime">
                <div class="category-content-inner">
                    <h3 class="category-title">Acoustic Atelier</h3>
                    <p class="category-body">Launch the web-audio synthesizer and create advanced tracks instantly.</p>
                    <div class="glow-category-btn-list">
                        <button onclick="navTo('studio')"><i class="fas fa-music"></i> Launch Studio</button>
                    </div>
                </div>
            </section>
        </div> 

        <div id="game-overlay" class="app-overlay panel-pink">
            <div class="overlay-header">
                <h2 style="color: var(--neon-pink); text-shadow: 0 0 10px var(--neon-pink);"><i class="fas fa-gamepad"></i> ARCADE ARENA</h2>
                <div class="close-overlay-btn" onclick="navTo('home')"><i class="fas fa-times-circle"></i></div>
            </div>
            <div class="overlay-content-area">
                <p style="text-align:center; color: var(--text-sub); font-size: 13px;">Play Tic Tac Toe directly in the MND Hub.</p>
                <div class="board" id="tictactoe-board">
                    <div class="cell" onclick="makeMove(this, 0)"></div>
                    <div class="cell" onclick="makeMove(this, 1)"></div>
                    <div class="cell" onclick="makeMove(this, 2)"></div>
                    <div class="cell" onclick="makeMove(this, 3)"></div>
                    <div class="cell" onclick="makeMove(this, 4)"></div>
                    <div class="cell" onclick="makeMove(this, 5)"></div>
                    <div class="cell" onclick="makeMove(this, 6)"></div>
                    <div class="cell" onclick="makeMove(this, 7)"></div>
                    <div class="cell" onclick="makeMove(this, 8)"></div>
                </div>
                <div id="game-status">Player X's Turn</div>
                <div style="text-align:center; margin-top:30px;">
                    <button onclick="resetGame()" style="background:#000; border:2px solid var(--neon-pink); color:var(--neon-pink); padding:12px 30px; border-radius:8px; font-family:var(--font-head); font-weight: bold; cursor:pointer;">RESTART SYSTEM</button>
                </div>
            </div>
        </div> 

        <div id="studio-overlay" class="app-overlay panel-lime">
            <div class="overlay-header">
                <h2 style="color: var(--neon-lime); text-shadow: 0 0 10px var(--neon-lime);"><i class="fas fa-headphones"></i> CREATOR STUDIO</h2>
                <div class="close-overlay-btn" onclick="navTo('home')"><i class="fas fa-times-circle"></i></div>
            </div>
            <div class="overlay-content-area">
                <p style="text-align:center; color: var(--text-sub); font-size: 13px;">Web Audio API Live Synthesizer. Tap to play.</p>
                <div class="drum-pad">
                    <div class="pad" onclick="playSound(261.63)">C (Bass)</div>
                    <div class="pad" onclick="playSound(293.66)">D (Kick)</div>
                    <div class="pad" onclick="playSound(329.63)">E (Snare)</div>
                    <div class="pad" onclick="playSound(349.23)">F (Hi-Hat)</div>
                    <div class="pad" onclick="playSound(392.00)">G (Synth 1)</div>
                    <div class="pad" onclick="playSound(440.00)">A (Synth 2)</div>
                </div>
            </div>
        </div> 

        <div id="auth-overlay" class="app-overlay" style="color: var(--neon-cyan);">
            <div class="overlay-header">
                <h2 style="color: var(--neon-cyan); text-shadow: 0 0 10px var(--neon-cyan);"><i class="fas fa-user-circle"></i> MND CREATORS</h2>
                <div class="close-overlay-btn" onclick="navTo('home')"><i class="fas fa-times-circle"></i></div>
            </div>
            <div class="overlay-content-area">
                <h3 style="margin-bottom: 20px; font-family: var(--font-head); color:#fff; font-size: 18px;">Executive Board</h3>
                
                <div class="profile-card">
                    <div class="profile-pic">L</div>
                    <div class="profile-info">
                        <h4>Lalu Kumar Tanti</h4>
                        <p>Founder & CEO, MND HUB</p>
                    </div>
                </div>

                <div style="margin-top: 35px; border-top: 1px solid #333; padding-top: 25px;">
                    <h3 style="margin-bottom: 15px; font-family: var(--font-head); color:#fff; font-size: 15px;">Creator Login Access</h3>
                    <input type="password" placeholder="ENTER SECURE PIN" style="width:100%; padding:15px; background:#111; border:1px solid var(--neon-cyan); color:#fff; border-radius:8px; margin-bottom:15px; font-family:var(--font-body); font-size: 16px;">
                    <button style="width:100%; background:var(--neon-cyan); color:#000; font-weight:900; padding:15px; border:none; border-radius:8px; font-family:var(--font-head); font-size: 14px; cursor:pointer;">AUTHENTICATE</button>
                </div>
            </div>
        </div>

        <footer>
            <div class="nav-item active" data-nav="home" onclick="navTo('home', 'Home Menu')">
                <i class="fas fa-home nav-icon"></i>
                <span class="nav-name">Home</span>
            </div>
            <div class="nav-item" data-nav="studio" onclick="navTo('studio', 'Creator Studio')">
                <i class="fas fa-keyboard nav-icon"></i>
                <span class="nav-name">Studio</span>
            </div>
            <div class="nav-item" data-nav="game" onclick="navTo('game', 'Arcade Game')">
                <i class="fas fa-dice-four nav-icon"></i>
                <span class="nav-name">Game</span>
            </div>
            <div class="nav-item" data-nav="auth" onclick="navTo('auth', 'Creators Authentication')">
                <i class="fas fa-user-circle nav-icon"></i>
                <span class="nav-name">Creators</span>
            </div>
        </footer>
    </div> 

    <script>
        // GLOBAL VARIABLES
        let currentStream = null;
        let mediaRecorder = null;
        let recordedChunks = [];
        let wakeLock = null;
        let isMaxBrightness = false;

        // UI Logic
        function toggleMenu(menuId) {
            const dropdown = document.getElementById(menuId);
            dropdown.style.display = dropdown.style.display === 'none' ? 'block' : 'none';
        }

        function toggleSettings() {
            const settingsModal = document.getElementById('settings-fullscreen');
            settingsModal.classList.toggle('active');
            document.getElementById('nav-dropdown').style.display = 'none';
        }

        // ==========================================
        // TEXT TO SPEECH (NAVIGATION ANNOUNCER)
        // ==========================================
        function speakActivation(text) {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel(); // Stops previous speech immediately
                const utterance = new SpeechSynthesisUtterance(text + " System Activated.");
                utterance.pitch = 1.0;
                utterance.rate = 1.0;
                utterance.volume = 1.0;
                utterance.lang = "en-US";
                window.speechSynthesis.speak(utterance);
            }
        }

        // MASTER NAVIGATION CONTROLLER
        function navTo(page, spokenText = null) {
            // Speak the navigation action
            if (spokenText) {
                speakActivation(spokenText);
            }

            // Reset UI State
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.app-overlay').forEach(ov => ov.classList.remove('active'));
            document.getElementById('settings-fullscreen').classList.remove('active');

            // Set Active Navigation Button
            const targetNavBtn = document.querySelector(`.nav-item[data-nav="${page}"]`);
            if (targetNavBtn) targetNavBtn.classList.add('active');

            // Open target overlay (if not home)
            if(page !== 'home') {
                const targetOverlay = document.getElementById(page + '-overlay');
                if (targetOverlay) targetOverlay.classList.add('active');
            }
        }

        // FULLSCREEN API LOGIC
        function toggleFullScreen() {
            if (!document.fullscreenElement && !document.mozFullScreenElement && !document.webkitFullscreenElement && !document.msFullscreenElement) {
                if (document.documentElement.requestFullscreen) {
                    document.documentElement.requestFullscreen();
                } else if (document.documentElement.msRequestFullscreen) {
                    document.documentElement.msRequestFullscreen();
                } else if (document.documentElement.mozRequestFullScreen) {
                    document.documentElement.mozRequestFullScreen();
                } else if (document.documentElement.webkitRequestFullscreen) {
                    document.documentElement.webkitRequestFullscreen(Element.ALLOW_KEYBOARD_INPUT);
                }
                alert("Fullscreen Mode Activated.");
                toggleSettings(); // Close menu
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                } else if (document.msExitFullscreen) {
                    document.msExitFullscreen();
                } else if (document.mozCancelFullScreen) {
                    document.mozCancelFullScreen();
                } else if (document.webkitExitFullscreen) {
                    document.webkitExitFullscreen();
                }
            }
        }

        // ==========================================
        // ADVANCED HARDWARE & WEB API LOGIC
        // ==========================================

        function resetMediaFeed() {
            document.getElementById('media-video').style.display = 'none';
            document.getElementById('audio-visualizer').style.display = 'none';
            document.getElementById('location-display').style.display = 'none';
        }

        function stopMedia() {
            if (currentStream) {
                currentStream.getTracks().forEach(track => track.stop());
                currentStream = null;
            }
            if (mediaRecorder && mediaRecorder.state !== "inactive") {
                mediaRecorder.stop();
            }
            document.getElementById('media-feed-container').style.display = 'none';
            document.getElementById('media-video').srcObject = null;
        }

        // 1. Camera Feature
        async function activateCamera() {
            try {
                stopMedia();
                const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' } });
                currentStream = stream;
                const videoEl = document.getElementById('media-video');
                resetMediaFeed();
                videoEl.style.display = 'block';
                videoEl.srcObject = stream;
                document.getElementById('media-feed-container').style.display = 'flex';
                toggleSettings(); 
            } catch (err) {
                alert("Camera Access Denied or Unavailable.");
            }
        }

        // 2. Torch/Flashlight Feature
        async function activateTorch() {
            try {
                stopMedia();
                const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' } });
                currentStream = stream;
                const track = stream.getVideoTracks()[0];
                await track.applyConstraints({ advanced: [{ torch: true }] });
                alert("Torch Activated. Click OK to turn off.");
                stopMedia(); 
            } catch (err) {
                alert("Torch not supported on this device.");
                stopMedia();
            }
        }

        // 3. Record Video Feature
        async function recordVideo() {
            const btnText = document.getElementById('record-text');
            if (mediaRecorder && mediaRecorder.state === "recording") {
                mediaRecorder.stop();
                btnText.innerText = "RECORD VIDEO";
                btnText.style.color = "#fff";
                return;
            }

            try {
                stopMedia();
                const stream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
                currentStream = stream;
                const videoEl = document.getElementById('media-video');
                resetMediaFeed();
                videoEl.style.display = 'block';
                videoEl.srcObject = stream;
                document.getElementById('media-feed-container').style.display = 'flex';
                
                recordedChunks = [];
                mediaRecorder = new MediaRecorder(stream);
                
                mediaRecorder.ondataavailable = event => {
                    if (event.data.size > 0) recordedChunks.push(event.data);
                };
                
                mediaRecorder.onstop = () => {
                    const blob = new Blob(recordedChunks, { type: 'video/webm' });
                    const url = URL.createObjectURL(blob);
                    const a = document.createElement('a');
                    a.style.display = 'none';
                    a.href = url;
                    a.download = 'MND_HUB_Recording.webm';
                    document.body.appendChild(a);
                    a.click();
                    URL.revokeObjectURL(url);
                    stopMedia();
                };

                mediaRecorder.start();
                btnText.innerText = "STOP RECORDING";
                btnText.style.color = "red";
                toggleSettings();
            } catch (err) {
                alert("Recording failed.");
            }
        }

        // 4. Live Mic / Audio Visualizer
        async function activateMic() {
            try {
                stopMedia();
                const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
                currentStream = stream;
                resetMediaFeed();
                document.getElementById('audio-visualizer').style.display = 'flex';
                document.getElementById('media-feed-container').style.display = 'flex';
                toggleSettings();
            } catch (err) {
                alert("Microphone Access Denied.");
            }
        }

        // 5. GPS Location Tracker
        function activateLocation() {
            if ("geolocation" in navigator) {
                stopMedia();
                resetMediaFeed();
                const display = document.getElementById('location-display');
                const text = document.getElementById('coords-text');
                text.innerText = "Tracking Satellite Data...";
                display.style.display = 'flex';
                document.getElementById('media-feed-container').style.display = 'flex';
                toggleSettings();

                navigator.geolocation.getCurrentPosition(
                    position => {
                        text.innerHTML = `Latitude: ${position.coords.latitude.toFixed(5)}<br>Longitude: ${position.coords.longitude.toFixed(5)}<br>Accuracy: ${position.coords.accuracy}m`;
                    },
                    error => {
                        text.innerText = "Location retrieval failed.";
                    },
                    { enableHighAccuracy: true }
                );
            } else {
                alert("Geolocation is not supported by your browser.");
            }
        }

        // 6. Max Brightness Simulation & Wake Lock
        async function toggleMaxBrightness() {
            const body = document.body;
            const btnText = document.getElementById('brightness-text');
            
            if (!isMaxBrightness) {
                body.style.filter = "brightness(1.5) contrast(1.2)";
                btnText.innerText = "NORMAL DISPLAY";
                isMaxBrightness = true;
                if ('wakeLock' in navigator) {
                    try { wakeLock = await navigator.wakeLock.request('screen'); } 
                    catch (err) {}
                }
            } else {
                body.style.filter = "none";
                btnText.innerText = "MAX BRIGHTNESS";
                isMaxBrightness = false;
                if (wakeLock !== null) { wakeLock.release().then(() => wakeLock = null); }
            }
        }

        // 7. System Lockdown
        function triggerLockdown() {
            document.getElementById('settings-fullscreen').classList.remove('active');
            document.getElementById('lockdown-overlay').style.display = 'flex';
            document.body.style.pointerEvents = 'none';
        }

        // ==========================================
        // Web Audio API Logic for Studio
        // ==========================================
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        let audioCtx;

        function playSound(frequency) {
            if (!audioCtx) { audioCtx = new AudioContext(); }
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            oscillator.type = 'triangle'; 
            oscillator.frequency.value = frequency;
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            oscillator.start();
            gainNode.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + 1);
            oscillator.stop(audioCtx.currentTime + 1);
        }

        // ==========================================
        // Tic Tac Toe Game Logic
        // ==========================================
        let boardState = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        let gameActive = true;

        function makeMove(cell, index) {
            if (boardState[index] !== "" || !gameActive) return;
            boardState[index] = currentPlayer;
            cell.innerText = currentPlayer;
            cell.style.color = currentPlayer === "X" ? "#fff" : "var(--neon-cyan)";
            checkWin();
        }

        function checkWin() {
            const winConditions = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7], [2, 5, 8], [0, 4, 8], [2, 4, 6]
            ];
            let roundWon = false;
            for (let i = 0; i < winConditions.length; i++) {
                const [a, b, c] = winConditions[i];
                if (boardState[a] && boardState[a] === boardState[b] && boardState[a] === boardState[c]) {
                    roundWon = true; break;
                }
            }
            if (roundWon) {
                document.getElementById('game-status').innerText = `Player ${currentPlayer} Wins!`;
                gameActive = false; return;
            }
            if (!boardState.includes("")) {
                document.getElementById('game-status').innerText = "System Draw!";
                gameActive = false; return;
            }
            currentPlayer = currentPlayer === "X" ? "O" : "X";
            document.getElementById('game-status').innerText = `Player ${currentPlayer}'s Turn`;
        }

        function resetGame() {
            boardState = ["", "", "", "", "", "", "", "", ""];
            currentPlayer = "X"; gameActive = true;
            document.getElementById('game-status').innerText = "Player X's Turn";
            document.querySelectorAll('.cell').forEach(cell => {
                cell.innerText = ""; cell.style.color = "#fff";
            });
        }
    </script>
</body>
</html>
