<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" id="theme-color-meta" content="#050505">
    
    <title>👑 MND HUB — Maa Nirmala DJ & Tent House | Full Screen Interface</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700;900&family=Outfit:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

    <script src="https://www.gstatic.com/firebasejs/10.10.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.10.0/firebase-database-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.10.0/firebase-storage-compat.js"></script>

    <style>
        /* =========================================================================
           ADVANCED RESET & CSS VARIABLES
           ========================================================================= */
        :root {
            --bg-base: #030303;
            --bg-panel: rgba(10, 10, 10, 0.85);
            
            --neon-pink: #FF00FF;
            --neon-pink-dim: rgba(255, 0, 255, 0.25);
            --neon-lime: #00FA9A;
            --neon-lime-dim: rgba(0, 250, 154, 0.25);
            --neon-cyan: #00E5FF;
            --neon-cyan-dim: rgba(0, 229, 255, 0.25);
            --neon-gold: #D4AF37;
            
            --text-main: #FFFFFF;
            --text-sub: #BBBBBB;

            --font-head: 'Cinzel', serif;
            --font-body: 'Outfit', sans-serif;
            --dynamic-shift: 15s;

            --header-height: 65px;
            --footer-height: 75px;
        }

        * {
            margin: 0; padding: 0; box-sizing: border-box;
            outline: none; user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        /* NATIVE SCROLL ALLOWED ON MOBILE FOR ADDRESS BAR HIDING */
        body, html {
            width: 100vw; 
            min-height: 100vh; 
            background-color: #000; 
            color: var(--text-main);
            font-family: var(--font-body); 
            margin: 0; padding: 0;
            -webkit-overflow-scrolling: touch;
        }

        /* DYNAMIC MULTI-COLOR BACKGROUND */
        #dynamic-bg {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            z-index: 0;
            background-color: var(--bg-base);
            background-image: 
                radial-gradient(circle at 15% 25%, var(--neon-pink-dim), transparent 45%),
                radial-gradient(circle at 85% 75%, var(--neon-cyan-dim), transparent 45%),
                radial-gradient(circle at 50% 50%, transparent 0%, #000 100%);
            animation: bodyHueShift var(--dynamic-shift) infinite linear;
            pointer-events: none;
        }

        @keyframes bodyHueShift {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }

        /* =========================================================================
           UNBREAKABLE LAYOUT CONTAINER
           ========================================================================= */
        #app-container {
            width: 100%; 
            min-height: 100vh; 
            max-width: 100vw;
            background: transparent;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            position: relative;
            z-index: 1;
        }

        @media screen and (min-width: 768px) {
            body, html {
                height: 100vh; overflow: hidden;
                display: flex; justify-content: center; align-items: center;
            }
            #app-container {
                width: 400px;
                height: 90vh;
                max-height: 850px;
                min-height: auto;
                border-radius: 40px;
                border: 8px solid #111;
                box-shadow: 0 20px 50px rgba(0,0,0,0.8), 0 0 100px rgba(0, 229, 255, 0.15);
                position: relative;
                overflow: hidden;
            }
            header, footer, .app-overlay, .settings-modal, #media-feed-container, #lockdown-overlay, #nav-dropdown {
                position: absolute !important;
            }
            #main-scroll-content {
                padding-top: calc(var(--header-height) + 20px) !important;
                padding-bottom: calc(var(--footer-height) + 20px) !important;
                overflow-y: auto !important;
                height: 100%;
            }
            footer { border-bottom-left-radius: 32px; border-bottom-right-radius: 32px; }
            header { border-top-left-radius: 32px; border-top-right-radius: 32px; }
            .app-overlay, #lockdown-overlay, .settings-modal { border-radius: 32px; }
        }

        /* =========================================================================
           SOLID BLOCKS: HEADER, SCROLL CONTENT, & FOOTER
           ========================================================================= */
        header {
            position: fixed; top: 0; left: 0; right: 0;
            height: var(--header-height); 
            background: rgba(5, 5, 5, 0.90); padding: 0 20px; 
            border-bottom: 1px solid rgba(255,255,255,0.1);
            display: flex; flex-direction: column; justify-content: center;
            backdrop-filter: blur(15px);
            z-index: 1000;
        }
        
        .header-top { display: flex; justify-content: space-between; align-items: center; }
        .logo-block { font-family: var(--font-head); font-weight: 900; font-size: 20px; color: var(--neon-lime); text-shadow: 0 0 12px var(--neon-lime-dim); }
        .control-icons { display: flex; gap: 20px; color: #fff; font-size: 22px; cursor: pointer;}
        .control-icons i:hover { color: var(--neon-lime); text-shadow: 0 0 10px var(--neon-lime);}

        #nav-dropdown {
            display: none; position: fixed; top: 70px; right: 20px; 
            background: var(--bg-panel); border: 1px solid var(--neon-cyan); 
            padding: 15px; border-radius: 12px; z-index: 2000; backdrop-filter: blur(10px);
            box-shadow: 0 5px 20px rgba(0, 229, 255, 0.2);
        }

        footer { 
            position: fixed; bottom: 0; left: 0; right: 0;
            height: var(--footer-height); 
            background: rgba(0, 0, 0, 0.90); 
            border-top: 2px solid rgba(255,255,255,0.1); 
            display: flex; justify-content: space-around; align-items: center; 
            z-index: 2500; backdrop-filter: blur(20px);
        }
        footer::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 3px; background: linear-gradient(to right, var(--neon-cyan), var(--neon-lime), var(--neon-pink)); box-shadow: 0 0 20px 2px var(--neon-lime); animation: bottomNavShine 3s infinite linear; }
        @keyframes bottomNavShine { 0% { box-shadow: 0 0 20px 2px var(--neon-lime); } 33% { box-shadow: 0 0 20px 2px var(--neon-cyan); } 66% { box-shadow: 0 0 20px 2px var(--neon-pink); } 100% { box-shadow: 0 0 20px 2px var(--neon-lime); } }
        
        .nav-item { display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; flex: 1; cursor: pointer; transition: all 0.2s ease; height: 100%;}
        .nav-icon { font-size: 22px; color: #555; transition: 0.3s ease; margin-bottom: 6px; }
        .nav-name { font-size: 11px; font-family: var(--font-body); color: #555; text-transform: uppercase; font-weight: 800; display: block; }
        
        .nav-item:hover .nav-icon { color: #fff; transform: translateY(-3px); }
        .nav-item[data-nav="home"].active .nav-icon, .nav-item[data-nav="home"].active .nav-name { color: var(--neon-cyan); text-shadow: 0 0 15px var(--neon-cyan); }
        .nav-item[data-nav="studio"].active .nav-icon, .nav-item[data-nav="studio"].active .nav-name { color: var(--neon-lime); text-shadow: 0 0 15px var(--neon-lime); }
        .nav-item[data-nav="game"].active .nav-icon, .nav-item[data-nav="game"].active .nav-name { color: var(--neon-pink); text-shadow: 0 0 15px var(--neon-pink); }
        .nav-item[data-nav="auth"].active .nav-icon, .nav-item[data-nav="auth"].active .nav-name { color: var(--neon-cyan); text-shadow: 0 0 15px var(--neon-cyan); }

        #main-scroll-content { 
            width: 100%;
            padding-top: calc(var(--header-height) + 20px);
            padding-bottom: calc(var(--footer-height) + 60px);
            padding-left: 20px;
            padding-right: 20px;
            display: flex; flex-direction: column; align-items: center; 
            flex: 1;
        }
        
        .content-wrapper { width: 100%; max-width: 800px; }

        /* =========================================================================
           TYPOGRAPHY & PANELS
           ========================================================================= */
        #perfect-intro { text-align: center; padding: 40px 10px; border-radius: 20px; background: radial-gradient(circle at 50% 120%, var(--neon-lime-dim), transparent 60%); margin-bottom: 30px; position: relative; }
        #perfect-intro::before { content: ''; position: absolute; bottom: 0; left: 10%; width: 80%; height: 2px; background: linear-gradient(to right, transparent, var(--neon-lime), transparent); box-shadow: 0 0 10px var(--neon-lime); }
        
        .shimmering-title { font-family: var(--font-head); font-weight: 900; font-size: clamp(24px, 6vw, 36px); margin-bottom: 12px; background: linear-gradient(90deg, #fff 0%, #fff 45%, var(--neon-lime) 50%, #fff 55%, #fff 100%); background-size: 200% auto; -webkit-background-clip: text; -webkit-text-fill-color: transparent; animation: textShimmer 2.5s infinite linear; text-transform: uppercase; letter-spacing: 1px; }
        .shimmering-dj-title { font-family: var(--font-head); font-weight: 900; font-size: clamp(20px, 4vw, 26px); background: linear-gradient(90deg, #fff 0%, #fff 40%, var(--neon-pink) 50%, #fff 60%, #fff 100%); background-size: 200% auto; -webkit-background-clip: text; -webkit-text-fill-color: transparent; animation: textShimmer-dj 3s infinite linear; text-transform: uppercase; }
        
        @keyframes textShimmer { to { background-position: -200% center; } }
        @keyframes textShimmer-dj { to { background-position: 200% center; } }
        .intro-body-text { color: var(--text-sub); font-size: 15px; line-height: 1.6; margin-top: 15px; }

        .category-glow-panel { background: rgba(0,0,0,0.6); border-radius: 20px; padding: 1px; margin-bottom: 25px; position: relative; transition: transform 0.3s ease; width: 100%;}
        .category-glow-panel:hover { transform: scale(1.02); }
        .category-glow-panel::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%; border-radius: 20px; pointer-events: none; opacity: 0.9; box-shadow: inset 0 0 15px currentcolor, 0 0 15px currentcolor; }
        .category-content-inner { background: var(--bg-panel); backdrop-filter: blur(8px); border-radius: 19px; padding: 25px 20px; text-align: center; }
        .category-title { font-family: var(--font-head); font-weight: 900; font-size: clamp(20px, 4vw, 24px); margin-bottom: 15px; display: flex; align-items: center; justify-content: center; gap: 10px; }
        .category-body { color: var(--text-sub); font-size: 14px; margin-bottom: 20px; opacity: 0.9; line-height: 1.5;}
        
        .glow-category-btn-list { display: flex; justify-content: center; gap: 12px; flex-wrap: wrap; }
        .glow-category-btn-list button { background: #000; border: 1px solid currentcolor; border-radius: 8px; padding: 12px 24px; font-family: var(--font-head); font-size: 13px; font-weight: bold; color: #fff; cursor: pointer; text-shadow: 0 0 5px currentcolor; display: flex; align-items: center; gap: 8px; transition: 0.3s ease; }
        .glow-category-btn-list button:hover { color: #000; background: currentcolor; text-shadow: none; box-shadow: 0 0 15px currentcolor;}
        
        .panel-pink { color: var(--neon-pink); }
        .panel-lime { color: var(--neon-lime); }
        .panel-cyan { color: var(--neon-cyan); }
        .panel-gold { color: var(--neon-gold); }

        /* =========================================================================
           FIXED OVERLAYS (STAYS PINNED EVEN WHEN SCROLLING)
           ========================================================================= */
        .app-overlay { 
            position: fixed; 
            top: var(--header-height); 
            bottom: var(--footer-height); 
            left: 0; width: 100%; 
            background: rgba(0,0,0,0.98); backdrop-filter: blur(20px); z-index: 500; 
            display: flex; flex-direction: column; transform: translateY(150%); 
            transition: transform 0.4s cubic-bezier(0.19, 1, 0.22, 1);
        }
        .app-overlay.active { transform: translateY(0); }
        .overlay-header { padding: 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.1); background: rgba(5,5,5,0.9); flex-shrink: 0;}
        .overlay-header h2 { font-family: var(--font-head); font-size: 20px; font-weight: bold; margin: 0; display: flex; align-items: center; gap: 10px;}
        .close-overlay-btn { color: #fff; font-size: 28px; cursor: pointer; transition: 0.3s; background: rgba(255,255,255,0.1); width: 40px; height: 40px; display: flex; justify-content: center; align-items: center; border-radius: 50%;}
        .close-overlay-btn:hover { opacity: 1; transform: scale(1.1);}
        .overlay-content-area { flex: 1; overflow-y: auto; overflow-x: hidden; padding: 20px; display: flex; flex-direction: column; align-items: center;}

        /* SELECTION MENU UI (Games & Studio) */
        .selection-menu { display: flex; flex-direction: column; gap: 15px; width: 100%; max-width: 400px; margin: 0 auto; }
        .menu-card { background: #111; border: 1px solid transparent; padding: 15px 20px; border-radius: 12px; display: flex; align-items: center; gap: 15px; cursor: pointer; transition: 0.3s; box-shadow: 0 0 10px rgba(0,0,0,0.5); }
        .menu-card:hover { transform: scale(1.02); }
        .menu-card.pink { border-color: var(--neon-pink); }
        .menu-card.pink:hover { box-shadow: 0 0 15px var(--neon-pink-dim); }
        .menu-card.lime { border-color: var(--neon-lime); }
        .menu-card.lime:hover { box-shadow: 0 0 15px var(--neon-lime-dim); }
        .menu-icon { font-size: 28px; width: 50px; height: 50px; display: flex; justify-content: center; align-items: center; border-radius: 50%; background: rgba(255,255,255,0.05); }
        .menu-text h3 { color: #fff; font-size: 18px; margin-bottom: 4px; font-family: var(--font-head); }
        .menu-text p { color: var(--text-sub); font-size: 12px; }
        
        .inner-view { display: none; flex-direction: column; align-items: center; width: 100%; }
        .inner-view.active { display: flex; }
        .back-btn { align-self: flex-start; background: rgba(255,255,255,0.05); border: 1px solid var(--text-sub); color: #fff; padding: 10px 20px; border-radius: 8px; cursor: pointer; margin-bottom: 25px; font-family: var(--font-head); font-weight: bold; font-size: 13px; transition: 0.3s; display: flex; align-items: center; gap: 8px;}
        .back-btn:hover { border-color: #fff; background: rgba(255,255,255,0.1); transform: translateX(-5px); }

        /* PORTAL ACCESS UI */
        .portal-access-container {
            border: 1px solid var(--neon-gold);
            border-radius: 12px;
            width: 100%; max-width: 500px;
            background: rgba(0,0,0,0.8);
            box-shadow: 0 0 20px rgba(212, 175, 55, 0.15);
            display: flex; flex-direction: column; overflow: hidden;
            margin-top: 20px;
        }

        .portal-top-title {
            color: var(--neon-gold); font-family: var(--font-head); font-size: 18px; font-weight: bold; 
            text-align: center; letter-spacing: 2px; text-transform: uppercase;
            padding: 20px; border-bottom: 1px solid var(--neon-gold);
            line-height: 1.5;
        }

        .portal-scroll-area {
            display: flex; gap: 15px; overflow-x: auto; padding: 20px; 
            scroll-behavior: smooth; -webkit-overflow-scrolling: touch;
        }
        .portal-scroll-area::-webkit-scrollbar { display: none; } 

        .portal-btn {
            display: flex; align-items: center; justify-content: space-between; 
            background: #0a0a0a; border: 1px solid var(--neon-gold); 
            padding: 15px; border-radius: 12px; cursor: pointer; transition: 0.3s;
            min-width: 260px; flex-shrink: 0; 
        }
        .portal-btn:hover { background: rgba(212, 175, 55, 0.15); box-shadow: 0 0 10px rgba(212, 175, 55, 0.3); transform: translateY(-2px);}
        .portal-btn-left { display: flex; align-items: center; gap: 15px; }
        .portal-icon-auth { background: rgba(212, 175, 55, 0.15); color: var(--neon-gold); width: 45px; height: 45px; border-radius: 50%; display: flex; justify-content: center; align-items: center; font-size: 18px; }
        .portal-text-auth h4 { color: #fff; font-family: var(--font-head); font-size: 15px; margin-bottom: 5px; font-weight: bold; }
        .portal-text-auth p { color: #888; font-size: 12px; font-family: var(--font-body); }
        .portal-arrow { color: #555; font-size: 14px; }

        /* LIVE FEED SYSTEM */
        #live-feed-container { width: 100%; display: flex; flex-direction: column; gap: 15px; text-align: left;}
        .live-post { background: rgba(0,0,0,0.7); padding: 15px; border-radius: 12px; border: 1px solid rgba(255,255,255,0.1); width: 100%; box-shadow: 0 5px 15px rgba(0,0,0,0.5);}
        .live-post-date { font-size: 11px; color: #888; margin-bottom: 8px; font-family: var(--font-body);}
        .live-post-text { color: #fff; font-size: 14px; line-height: 1.5; margin-bottom: 10px;}
        
        /* ADMIN POST MANAGER */
        .admin-delete-btn { background: rgba(255,0,0,0.2); border: 1px solid red; color: #ff6666; padding: 10px 15px; border-radius: 6px; cursor: pointer; font-size: 12px; font-family: var(--font-head); font-weight: bold; transition: 0.3s; width: 100%; margin-top: 10px; display: flex; align-items: center; justify-content: center; gap: 8px;}
        .admin-delete-btn:hover { background: red; color: #fff; }

        /* Admin Input Labels */
        .admin-label { color: var(--neon-cyan); font-size: 12px; font-family: var(--font-head); display: block; margin-bottom: 5px; margin-top: 15px; }

        /* Full Screen Modals (Cover entire screen) */
        .settings-modal, #lockdown-overlay, #media-feed-container {
            position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; height: 100dvh;
            background: rgba(0, 0, 0, 0.98); backdrop-filter: blur(20px);
            z-index: 9999; display: flex; flex-direction: column;
        }
        
        .settings-modal { transform: translateY(100%); transition: transform 0.4s cubic-bezier(0.19, 1, 0.22, 1); }
        .settings-modal.active { transform: translateY(0); }
        .settings-header-bar { padding: 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.1); background: rgba(0,0,0,0.9); flex-shrink: 0;}
        .settings-content-grid { padding: 20px; overflow-y: auto; display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; width: 100%; max-width: 800px; margin: 0 auto; align-content: start;}
        
        .hw-btn {
            background: #111; border: 1px solid var(--neon-lime); border-radius: 12px;
            padding: 30px 10px; text-align: center; color: #fff; font-family: var(--font-head);
            font-size: 12px; font-weight: bold; cursor: pointer; transition: 0.3s;
            box-shadow: inset 0 0 10px var(--neon-lime-dim); display: flex; flex-direction: column; align-items: center; justify-content: center;
        }
        .hw-btn i { font-size: 38px; color: var(--neon-lime); margin-bottom: 15px; transition: 0.3s;}
        .hw-btn:hover { background: var(--neon-lime-dim); transform: scale(1.05); }
        .hw-btn:hover i { color: #fff; filter: drop-shadow(0 0 5px #fff); }
        
        #media-feed-container { display: none; }
        #media-video { width: 100%; height: 100%; object-fit: cover; }
        .close-media-btn { position: absolute; top: 20px; right: 20px; background: rgba(0,0,0,0.8); color: var(--neon-pink); border: 1px solid var(--neon-pink); padding: 12px 20px; border-radius: 8px; cursor: pointer; font-family: var(--font-head); z-index: 1501; font-weight: bold; letter-spacing: 1px; }

        #lockdown-overlay { display: none; justify-content: center; align-items: center; text-align: center; }
        .lockdown-text { font-size: clamp(30px, 8vw, 50px); font-weight: 900; letter-spacing: 4px; animation: flash 1s infinite; color: white; font-family: var(--font-head);}

        /* Game & Studio Grids */
        .board { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-top: 20px; width: 100%; max-width: 350px; }
        .cell { background: #111; border: 1px solid var(--neon-pink); height: clamp(90px, 25vw, 110px); display: flex; justify-content: center; align-items: center; font-size: 55px; font-family: var(--font-head); color: #fff; cursor: pointer; border-radius: 10px; box-shadow: inset 0 0 15px var(--neon-pink-dim); }
        .cell:hover { background: var(--neon-pink-dim); }
        #game-status { text-align: center; margin-top: 25px; font-family: var(--font-body); color: var(--neon-pink); font-size: 22px; font-weight: bold; }

        .drum-pad { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px, 1fr)); gap: 15px; margin-top: 20px; width: 100%; max-width: 500px; }
        .pad { background: #111; border: 2px solid var(--neon-lime); height: 110px; border-radius: 12px; display: flex; justify-content: center; align-items: center; color: var(--neon-lime); font-family: var(--font-head); font-weight: bold; font-size: 18px; cursor: pointer; transition: 0.1s; box-shadow: 0 0 10px var(--neon-lime-dim); }
        .pad:active { transform: scale(0.9); background: var(--neon-lime); color: #000; box-shadow: 0 0 25px var(--neon-lime);}

    </style>
</head>
<body>

    <div id="dynamic-bg"></div>

    <div id="app-container">
        
        <header>
            <div class="header-top">
                <div class="logo-block">👑 MND CREATORS</div>
                <div class="control-icons">
                    <i class="fas fa-cog" onclick="toggleSettings()"></i> 
                    <i class="fas fa-bars" onclick="toggleMenu('side-nav-menu')"></i> 
                </div>
            </div>
        </header>

        <div id="side-nav-menu" class="side-menu-overlay" onclick="closeSideMenu(event)">
            <div class="side-menu-content" onclick="event.stopPropagation()">
                <div class="side-menu-header">
                    <h3 style="color: var(--neon-cyan); font-family: var(--font-head); font-size: 18px; margin: 0;">Menu</h3>
                    <i class="fas fa-times" style="color: #fff; font-size: 24px; cursor: pointer;" onclick="toggleMenu('side-nav-menu')"></i>
                </div>
                
                <div class="side-menu-items">
                    <div class="side-menu-item" onclick="navTo('home'); toggleMenu('side-nav-menu')">
                        <i class="fas fa-home"></i> Home
                    </div>
                    
                    <div class="side-menu-item" onclick="alert('Sound Settings: Active'); toggleMenu('side-nav-menu')">
                        <i class="fas fa-volume-up"></i> Sound
                    </div>
                    
                    <div class="side-menu-item" onclick="alert('Notifications: Enabled'); toggleMenu('side-nav-menu')">
                        <i class="fas fa-bell"></i> Notifications
                    </div>
                    
                    <div class="side-menu-item" onclick="alert('Headquarters: Beltikri, Banka, Bihar.'); toggleMenu('side-nav-menu')">
                        <i class="fas fa-map-marker-alt"></i> Location Info
                    </div>
                    
                    <a href="https://maa-nirmala-dj.github.io/-tent-house./" style="text-decoration: none;">
                        <div class="side-menu-item">
                            <i class="fas fa-external-link-alt"></i> External Portal
                        </div>
                    </a>
                </div>
            </div>
        </div>

        <style>
            /* SIDE MENU STYLES */
            .side-menu-overlay {
                display: none;
                position: fixed;
                top: 0;
                left: 0;
                width: 100vw;
                height: 100vh;
                height: 100dvh;
                background: rgba(0, 0, 0, 0.5);
                z-index: 3000;
                backdrop-filter: blur(5px);
            }
            
            .side-menu-content {
                position: absolute;
                top: 0;
                right: 0;
                width: 66.66%; /* One-third of the screen on the right */
                max-width: 300px;
                height: 100%;
                background: rgba(10, 10, 10, 0.95);
                border-left: 1px solid var(--neon-cyan);
                box-shadow: -5px 0 20px rgba(0, 229, 255, 0.2);
                display: flex;
                flex-direction: column;
                transform: translateX(100%);
                animation: slideInRight 0.3s forwards;
            }

            @keyframes slideInRight {
                to { transform: translateX(0); }
            }

            .side-menu-header {
                display: flex;
                justify-content: space-between;
                align-items: center;
                padding: 20px;
                border-bottom: 1px solid rgba(255,255,255,0.1);
            }

            .side-menu-items {
                display: flex;
                flex-direction: column;
                padding: 20px 0;
            }

            .side-menu-item {
                padding: 15px 20px;
                color: #fff;
                font-family: var(--font-body);
                font-size: 16px;
                display: flex;
                align-items: center;
                gap: 15px;
                cursor: pointer;
                transition: 0.3s;
                border-bottom: 1px solid rgba(255,255,255,0.05);
            }

            .side-menu-item:hover {
                background: rgba(0, 229, 255, 0.1);
                color: var(--neon-cyan);
            }

            .side-menu-item i {
                color: var(--neon-cyan);
                width: 20px;
                text-align: center;
            }
        </style>

        <script>
            // Update your toggleMenu function to handle the new side menu
            function toggleMenu(menuId) {
                const menu = document.getElementById(menuId);
                if (menu.style.display === 'block') {
                    menu.style.display = 'none';
                } else {
                    menu.style.display = 'block';
                }
            }

            // Close side menu when clicking outside of it
            function closeSideMenu(event) {
                if (event.target.id === 'side-nav-menu') {
                    document.getElementById('side-nav-menu').style.display = 'none';
                }
            }
        </script>
        </header>

        <div id="media-feed-container">
            <button class="close-media-btn" onclick="stopMedia()"><i class="fas fa-times"></i> CLOSE</button>
            <video id="media-video" autoplay playsinline></video>
            <div id="audio-visualizer" style="display:none; width:100%; height:100%; align-items:center; justify-content:center; flex-direction:column;">
                <i class="fas fa-microphone" style="font-size: 70px; color: var(--neon-lime); margin-bottom: 25px; animation: pulse 1s infinite;"></i>
                <p style="color: var(--neon-lime); font-family: var(--font-head); font-weight: bold; font-size: 20px;">MIC ACTIVE & LISTENING...</p>
            </div>
            <div id="location-display" style="display:none; width:100%; height:100%; align-items:center; justify-content:center; flex-direction:column; padding: 20px; text-align: center;">
                <i class="fas fa-satellite" style="font-size: 70px; color: var(--neon-cyan); margin-bottom: 25px;"></i>
                <p id="coords-text" style="color: var(--neon-cyan); font-family: var(--font-body); font-size: 18px; font-weight: bold; line-height: 1.5;"></p>
            </div>
        </div>

        <div id="lockdown-overlay">
            <i class="fas fa-shield-alt" style="font-size: 100px; margin-bottom: 30px; color: white;"></i>
            <div class="lockdown-text">SYSTEM LOCKED</div>
            <p style="margin-top: 25px; font-family: var(--font-body); font-size: 16px; color: white;">Refresh application to restore access.</p>
        </div>

        <div id="settings-fullscreen" class="settings-modal">
            <div class="settings-header-bar">
                <h2 style="color: var(--neon-lime); text-shadow: 0 0 10px var(--neon-lime); margin: 0; font-family: var(--font-head); font-size: 20px;"><i class="fas fa-sliders-h"></i> CONTROL CENTER</h2>
                <i class="fas fa-times" style="font-size: 32px; color: #fff; cursor: pointer;" onclick="toggleSettings()"></i>
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
            <div class="content-wrapper">
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

                <section class="category-glow-panel panel-cyan" style="margin-top: 20px; margin-bottom: 40px;">
                    <div class="category-content-inner">
                        <h3 class="category-title" style="color: var(--neon-cyan);">LIVE FEED HUB <i class="fas fa-broadcast-tower"></i></h3>
                        <div id="live-feed-container">
                            <p style="color: var(--text-sub); text-align: center; font-size: 13px;">Connecting to Firebase HQ...</p>
                        </div>
                    </div>
                </section>

            </div>
        </div> 

        <div id="game-overlay" class="app-overlay panel-pink">
            <div class="overlay-header">
                <h2 style="color: var(--neon-pink); text-shadow: 0 0 10px var(--neon-pink);"><i class="fas fa-gamepad"></i> ARCADE ARENA</h2>
                <div class="close-overlay-btn" style="color: var(--neon-pink); background: rgba(255,0,255,0.1);" onclick="navTo('home')"><i class="fas fa-times"></i></div>
            </div>
            <div class="overlay-content-area">
                
                <div id="game-menu" class="selection-menu">
                    <div class="menu-card pink" onclick="openGame('tictactoe')">
                        <div class="menu-icon" style="color: var(--neon-pink);"><i class="fas fa-border-all"></i></div>
                        <div class="menu-text">
                            <h3>Tic Tac Toe</h3>
                            <p>Classic 3x3 strategy.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                    <div class="menu-card pink" onclick="openGame('snake')">
                        <div class="menu-icon" style="color: var(--neon-pink);"><i class="fas fa-worm"></i></div>
                        <div class="menu-text">
                            <h3>Neon Snake</h3>
                            <p>Retro arcade survival.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                    <div class="menu-card pink" onclick="openGame('chess')">
                        <div class="menu-icon" style="color: var(--neon-pink);"><i class="fas fa-chess"></i></div>
                        <div class="menu-text">
                            <h3>Chess Pro</h3>
                            <p>Advanced tactical board.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                    <div class="menu-card pink" onclick="openGame('memory')">
                        <div class="menu-icon" style="color: var(--neon-pink);"><i class="fas fa-clone"></i></div>
                        <div class="menu-text">
                            <h3>Memory Match</h3>
                            <p>Cognitive symbol alignment.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                </div>

                <div id="game-view-tictactoe" class="inner-view">
                    <button class="back-btn" onclick="backToGameMenu()"><i class="fas fa-arrow-left"></i> BACK TO GAMES</button>
                    <p style="text-align:center; color: var(--text-sub); font-size: 15px; margin-bottom: 20px;">Play Tic Tac Toe directly in the MND Hub.</p>
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
                    <div style="text-align:center; margin-top:40px; width: 100%;">
                        <button onclick="resetGame()" style="background:#000; border:2px solid var(--neon-pink); color:var(--neon-pink); padding:16px 40px; border-radius:12px; font-family:var(--font-head); font-weight: bold; font-size: 16px; cursor:pointer;">RESTART SYSTEM</button>
                    </div>
                </div>

                <div id="game-view-snake" class="inner-view">
                    <button class="back-btn" onclick="backToGameMenu()"><i class="fas fa-arrow-left"></i> BACK TO GAMES</button>
                    <h3 style="color:var(--neon-pink); font-family:var(--font-head); margin-bottom:15px;">Neon Snake</h3>
                    <p style="color:var(--text-sub); text-align:center;">Module loading...</p>
                </div>

                <div id="game-view-chess" class="inner-view">
                    <button class="back-btn" onclick="backToGameMenu()"><i class="fas fa-arrow-left"></i> BACK TO GAMES</button>
                    <h3 style="color:var(--neon-pink); font-family:var(--font-head); margin-bottom:15px;">Chess Pro</h3>
                    <p style="color:var(--text-sub); text-align:center;">Module loading...</p>
                </div>

                <div id="game-view-memory" class="inner-view">
                    <button class="back-btn" onclick="backToGameMenu()"><i class="fas fa-arrow-left"></i> BACK TO GAMES</button>
                    <h3 style="color:var(--neon-pink); font-family:var(--font-head); margin-bottom:15px;">Memory Match</h3>
                    <p style="color:var(--text-sub); text-align:center;">Module loading...</p>
                </div>
            </div>
        </div> 

        <div id="studio-overlay" class="app-overlay panel-lime">
            <div class="overlay-header">
                <h2 style="color: var(--neon-lime); text-shadow: 0 0 10px var(--neon-lime);"><i class="fas fa-headphones"></i> CREATOR STUDIO</h2>
                <div class="close-overlay-btn" style="color: var(--neon-lime); background: rgba(0,250,154,0.1);" onclick="navTo('home')"><i class="fas fa-times"></i></div>
            </div>
            <div class="overlay-content-area">
                
                <div id="studio-menu" class="selection-menu">
                    <div class="menu-card lime" onclick="openStudio('drumpad')">
                        <div class="menu-icon" style="color: var(--neon-lime);"><i class="fas fa-th"></i></div>
                        <div class="menu-text">
                            <h3>Drum Pad</h3>
                            <p>Web Audio API Synthesizer.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                    <div class="menu-card lime" onclick="openStudio('guitar')">
                        <div class="menu-icon" style="color: var(--neon-lime);"><i class="fas fa-guitar"></i></div>
                        <div class="menu-text">
                            <h3>Electric Guitar</h3>
                            <p>Acoustic strings simulation.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                    <div class="menu-card lime" onclick="openStudio('harmonium')">
                        <div class="menu-icon" style="color: var(--neon-lime);"><i class="fas fa-stream"></i></div>
                        <div class="menu-text">
                            <h3>Harmonium</h3>
                            <p>Classic Indian keys.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                    <div class="menu-card lime" onclick="openStudio('piano')">
                        <div class="menu-icon" style="color: var(--neon-lime);"><i class="fas fa-music"></i></div>
                        <div class="menu-text">
                            <h3>Grand Piano</h3>
                            <p>Full 88-key dynamics.</p>
                        </div>
                        <div class="portal-arrow" style="margin-left:auto; color:#555;"><i class="fas fa-chevron-right"></i></div>
                    </div>
                </div>

                <div id="studio-view-drumpad" class="inner-view">
                    <button class="back-btn" onclick="backToStudioMenu()"><i class="fas fa-arrow-left"></i> BACK TO STUDIO</button>
                    <p style="text-align:center; color: var(--text-sub); font-size: 15px; margin-bottom: 20px;">Web Audio API Live Synthesizer. Tap to play.</p>
                    <div class="drum-pad">
                        <div class="pad" onclick="playSound(261.63)">C (Bass)</div>
                        <div class="pad" onclick="playSound(293.66)">D (Kick)</div>
                        <div class="pad" onclick="playSound(329.63)">E (Snare)</div>
                        <div class="pad" onclick="playSound(349.23)">F (Hi-Hat)</div>
                        <div class="pad" onclick="playSound(392.00)">G (Synth 1)</div>
                        <div class="pad" onclick="playSound(440.00)">A (Synth 2)</div>
                    </div>
                </div>

                <div id="studio-view-guitar" class="inner-view">
                    <button class="back-btn" onclick="backToStudioMenu()"><i class="fas fa-arrow-left"></i> BACK TO STUDIO</button>
                    <h3 style="color:var(--neon-lime); font-family:var(--font-head); margin-bottom:15px;">Electric Guitar</h3>
                    <p style="color:var(--text-sub); text-align:center;">Module loading...</p>
                </div>

                <div id="studio-view-harmonium" class="inner-view">
                    <button class="back-btn" onclick="backToStudioMenu()"><i class="fas fa-arrow-left"></i> BACK TO STUDIO</button>
                    <h3 style="color:var(--neon-lime); font-family:var(--font-head); margin-bottom:15px;">Harmonium</h3>
                    <p style="color:var(--text-sub); text-align:center;">Module loading...</p>
                </div>

                <div id="studio-view-piano" class="inner-view">
                    <button class="back-btn" onclick="backToStudioMenu()"><i class="fas fa-arrow-left"></i> BACK TO STUDIO</button>
                    <h3 style="color:var(--neon-lime); font-family:var(--font-head); margin-bottom:15px;">Grand Piano</h3>
                    <p style="color:var(--text-sub); text-align:center;">Module loading...</p>
                </div>

            </div>
        </div> 

        <div id="auth-overlay" class="app-overlay" style="color: var(--neon-gold);">
            <div class="overlay-header">
                <h2 style="color: var(--neon-gold);"><i class="fas fa-user-shield"></i> PORTAL ACCESS</h2>
                <div class="close-overlay-btn" style="color: var(--neon-gold); background: rgba(212,175,55,0.1);" onclick="navTo('home')"><i class="fas fa-times"></i></div>
            </div>
            
            <div class="overlay-content-area" style="display: flex; justify-content: center; align-items: start; padding: 20px 10px;">
                
                <div id="auth-main-menu" class="portal-access-container" style="flex-direction: column; width: 100%; max-width: 400px; padding: 20px;">
                    <div class="portal-top-title" style="border-right: none; padding: 0 0 20px 0; margin-bottom: 20px; text-align: center; max-width: 100%;">
                        PORTAL ACCESS SELECTION
                    </div>

                    <div class="portal-scroll-area" style="display: flex; flex-direction: column; overflow-x: hidden; padding: 0;">
                        <div class="portal-btn" style="width: 100%; min-width: auto;" onclick="alert('Public User Login: Under Development')">
                            <div class="portal-btn-left">
                                <div class="portal-icon-auth"><i class="fas fa-users"></i></div>
                                <div class="portal-text-auth">
                                    <h4>Public / User Login</h4>
                                    <p>Access Secure Hub (MFA)</p>
                                </div>
                            </div>
                            <div class="portal-arrow"><i class="fas fa-chevron-right"></i></div>
                        </div>

                        <div class="portal-btn" style="width: 100%; min-width: auto;" onclick="showAdminLogin()">
                            <div class="portal-btn-left">
                                <div class="portal-icon-auth"><i class="fas fa-user-shield"></i></div>
                                <div class="portal-text-auth">
                                    <h4>Admin / Manager</h4>
                                    <p>Passcode Required</p>
                                </div>
                            </div>
                            <div class="portal-arrow"><i class="fas fa-chevron-right"></i></div>
                        </div>

                        <a href="https://maa-nirmala-dj.github.io/-tent-house./" style="text-decoration: none; width: 100%;">
                            <div class="portal-btn" style="width: 100%; min-width: auto;">
                                <div class="portal-btn-left">
                                    <div class="portal-icon-auth"><i class="fas fa-exchange-alt"></i></div>
                                    <div class="portal-text-auth">
                                        <h4>Switch Account</h4>
                                        <p>Link to External Portal</p>
                                    </div>
                                </div>
                                <div class="portal-arrow"><i class="fas fa-external-link-alt"></i></div>
                            </div>
                        </a>
                    </div>
                </div>

                <div id="admin-login-box" style="display:none; width: 100%; max-width: 400px; padding: 20px;">
                    <button class="back-btn" onclick="backToAuthMenu()"><i class="fas fa-arrow-left"></i> BACK TO MENU</button>
                    <h3 style="color:var(--neon-cyan); font-family:var(--font-head); margin-bottom:15px; font-size: 22px;">Admin Login</h3>
                    <p style="color:#888; font-size:13px; margin-bottom:20px;">Enter restricted credentials to access live publishing tools.</p>
                    
                    <input type="tel" id="admin-phone" placeholder="ENTER REGISTERED PHONE" style="width:100%; padding:15px; background:#111; border:1px solid var(--neon-cyan); color:#fff; border-radius:8px; margin-bottom:15px; font-family:var(--font-body); font-size: 16px;">
                    <input type="password" id="admin-pin" placeholder="ENTER SECURE PIN" style="width:100%; padding:15px; background:#111; border:1px solid var(--neon-cyan); color:#fff; border-radius:8px; margin-bottom:25px; font-family:var(--font-body); font-size: 16px;">
                    
                    <button onclick="verifyAdmin()" style="width:100%; background:var(--neon-cyan); color:#000; font-weight:bold; padding:15px; border:none; border-radius:8px; font-family:var(--font-head); font-size:16px; cursor:pointer;">AUTHENTICATE</button>
                </div>

                <div id="admin-dashboard" style="display:none; width: 100%; max-width: 400px; padding: 10px 0;">
                    <button class="back-btn" style="background: rgba(255,0,0,0.2); border-color: red; color: #ff6666;" onclick="logoutAdmin()"><i class="fas fa-sign-out-alt"></i> SECURE LOGOUT</button>
                    
                    <h3 style="color:var(--neon-cyan); font-family:var(--font-head); margin-bottom:5px; font-size: 22px;">HQ Dashboard</h3>
                    <p style="color:#00FA9A; font-size:12px; font-weight:bold; margin-bottom:20px;"><i class="fas fa-check-circle"></i> ADMIN VERIFIED</p>
                    
                    <div style="background: #111; border: 1px solid var(--neon-cyan); padding: 20px; border-radius: 12px; margin-bottom: 25px;">
                        <h4 style="color:#fff; font-family:var(--font-head); margin-bottom:15px; font-size: 14px;"><i class="fas fa-upload"></i> Publish to Live Feed</h4>
                        
                        <label class="admin-label">Text Content</label>
                        <textarea id="post-text" placeholder="Write update details here..." style="width:100%; padding:12px; background:#000; border:1px solid #333; color:#fff; border-radius:8px; margin-bottom:10px; height:80px; resize:none; font-family:var(--font-body);"></textarea>
                        
                        <label class="admin-label">Image URL</label>
                        <input type="url" id="post-img-url" placeholder="https://... (Image Link)" style="width:100%; padding:12px; background:#000; border:1px solid #333; color:#fff; border-radius:8px; margin-bottom:10px; font-family:var(--font-body); font-size: 14px;">

                        <label class="admin-label">Video URL</label>
                        <input type="url" id="post-video-url" placeholder="https://... (Video Link)" style="width:100%; padding:12px; background:#000; border:1px solid #333; color:#fff; border-radius:8px; margin-bottom:10px; font-family:var(--font-body); font-size: 14px;">

                        <label class="admin-label">Audio URL</label>
                        <input type="url" id="post-audio-url" placeholder="https://... (Audio Link)" style="width:100%; padding:12px; background:#000; border:1px solid #333; color:#fff; border-radius:8px; margin-bottom:10px; font-family:var(--font-body); font-size: 14px;">

                        <label class="admin-label">Or Device File Upload (Image/Video/Audio/Doc)</label>
                        <input type="file" id="post-file" accept="image/*,audio/*,video/*,.pdf,.doc,.docx" style="margin-bottom:20px; color:#888; width:100%; font-size: 12px; background: #000; padding: 10px; border-radius: 8px; border: 1px solid #333;">
                        
                        <button id="publish-btn" onclick="createPost()" style="width:100%; background:var(--neon-cyan); color:#000; font-weight:900; padding:15px; border:none; border-radius:8px; cursor:pointer; font-family:var(--font-head); letter-spacing: 1px;">PUBLISH NOW</button>
                    </div>

                    <div style="border-top: 1px solid rgba(255,255,255,0.1); padding-top: 20px;">
                        <h4 style="color:#fff; font-family:var(--font-head); margin-bottom:15px; font-size: 14px;"><i class="fas fa-tasks"></i> Manage Live Posts</h4>
                        <div id="admin-post-manager" style="display: flex; flex-direction: column; gap: 10px;">
                            <p style="color: #888; font-size: 12px; text-align: center;">No active posts.</p>
                        </div>
                    </div>
                </div>

            </div>
        </div>

            </div>
        </div>

        <footer>
            <div class="nav-item active" data-nav="home" onclick="navTo('home')">
                <i class="fas fa-home nav-icon"></i>
                <span class="nav-name">Home</span>
            </div>
            <div class="nav-item" data-nav="studio" onclick="navTo('studio')">
                <i class="fas fa-keyboard nav-icon"></i>
                <span class="nav-name">Studio</span>
            </div>
            <div class="nav-item" data-nav="game" onclick="navTo('game')">
                <i class="fas fa-dice-four nav-icon"></i>
                <span class="nav-name">Game</span>
            </div>
            <div class="nav-item" data-nav="auth" onclick="navTo('auth')">
                <i class="fas fa-user-circle nav-icon"></i>
                <span class="nav-name">Creators</span>
            </div>
        </footer>
    </div> 

    <script>
        // ==========================================
        // FIREBASE INITIALIZATION
        // ==========================================
        const firebaseConfig = {
            apiKey: "AIzaSyAyydGIkA9fDUxrBtKWHiY3q7adpnpiWe0",
            authDomain: "mnd-40060.firebaseapp.com",
            databaseURL: "https://mnd-40060-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "mnd-40060",
            storageBucket: "mnd-40060.firebasestorage.app",
            messagingSenderId: "1032098137597",
            appId: "1:1032098137597:web:a848640633f239b6f94594"
        };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const storage = firebase.storage();

        // GLOBALS
        let currentStream = null;
        let mediaRecorder = null;
        let recordedChunks = [];
        let wakeLock = null;
        let isMaxBrightness = false;

        function toggleMenu(menuId) {
            const dropdown = document.getElementById(menuId);
            dropdown.style.display = dropdown.style.display === 'none' ? 'block' : 'none';
        }

        function toggleSettings() {
            const settingsModal = document.getElementById('settings-fullscreen');
            settingsModal.classList.toggle('active');
            document.getElementById('nav-dropdown').style.display = 'none';
        }

        function navTo(page) {
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.app-overlay').forEach(ov => ov.classList.remove('active'));
            document.getElementById('settings-fullscreen').classList.remove('active');

            const targetNavBtn = document.querySelector(`.nav-item[data-nav="${page}"]`);
            if (targetNavBtn) targetNavBtn.classList.add('active');

            if(page !== 'home') {
                const targetOverlay = document.getElementById(page + '-overlay');
                if (targetOverlay) targetOverlay.classList.add('active');
            }

            // Reset sub-menus when changing tabs
            if(page === 'game') backToGameMenu();
            if(page === 'studio') backToStudioMenu();
            
            // Reset Auth view depending on login state
            if(page === 'auth') {
                if(isAdmin) {
                    document.getElementById('auth-main-menu').style.display = 'none';
                    document.getElementById('admin-login-box').style.display = 'none';
                    document.getElementById('admin-dashboard').style.display = 'block';
                } else {
                    backToAuthMenu();
                }
            }
            
            // Fix absolute scroll position
            const scrollContent = document.getElementById('main-scroll-content');
            if(scrollContent) scrollContent.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // GAME MENU LOGIC
        function openGame(gameId) {
            document.getElementById('game-menu').style.display = 'none';
            document.querySelectorAll('#game-overlay .inner-view').forEach(el => el.classList.remove('active'));
            document.getElementById('game-view-' + gameId).classList.add('active');
        }

        function backToGameMenu() {
            document.querySelectorAll('#game-overlay .inner-view').forEach(el => el.classList.remove('active'));
            document.getElementById('game-menu').style.display = 'flex';
        }

        // STUDIO MENU LOGIC
        function openStudio(studioId) {
            document.getElementById('studio-menu').style.display = 'none';
            document.querySelectorAll('#studio-overlay .inner-view').forEach(el => el.classList.remove('active'));
            document.getElementById('studio-view-' + studioId).classList.add('active');
        }

        function backToStudioMenu() {
            document.querySelectorAll('#studio-overlay .inner-view').forEach(el => el.classList.remove('active'));
            document.getElementById('studio-menu').style.display = 'flex';
        }

        // ==========================================
        // ADMIN DASHBOARD & FIREBASE LIVE FEED
        // ==========================================
        let isAdmin = false;
        let livePosts = [];

        // Listen for live database changes
        db.ref('posts').orderByChild('timestamp').on('value', snapshot => {
            livePosts = [];
            snapshot.forEach(child => {
                livePosts.push({ id: child.key, ...child.val() });
            });
            livePosts.reverse(); // Show newest first
            renderLiveFeed();
            if(isAdmin) renderAdminFeed();
        });

        function showAdminLogin() {
            document.getElementById('auth-main-menu').style.display = 'none';
            document.getElementById('admin-login-box').style.display = 'block';
        }

        function backToAuthMenu() {
            document.getElementById('admin-login-box').style.display = 'none';
            document.getElementById('admin-dashboard').style.display = 'none';
            document.getElementById('auth-main-menu').style.display = 'flex';
            document.getElementById('admin-phone').value = '';
            document.getElementById('admin-pin').value = '';
        }

        function verifyAdmin() {
            const phone = document.getElementById('admin-phone').value;
            const pin = document.getElementById('admin-pin').value;
            
            // STRICT VALIDATION
            if(phone === '9771617808' && pin === '121120') {
                isAdmin = true;
                document.getElementById('admin-login-box').style.display = 'none';
                document.getElementById('admin-dashboard').style.display = 'block';
                document.getElementById('admin-phone').value = '';
                document.getElementById('admin-pin').value = '';
                renderAdminFeed(); 
                alert("Admin Access Granted.");
            } else {
                alert("ACCESS DENIED: Incorrect Credentials");
            }
        }

        function logoutAdmin() {
            isAdmin = false;
            backToAuthMenu();
            alert("Admin Logged Out Successfully.");
        }

        async function createPost() {
            const text = document.getElementById('post-text').value;
            const imgUrlInput = document.getElementById('post-img-url').value;
            const vidUrlInput = document.getElementById('post-video-url').value;
            const audUrlInput = document.getElementById('post-audio-url').value;
            const fileInput = document.getElementById('post-file');
            const publishBtn = document.getElementById('publish-btn');
            
            if(!text && !imgUrlInput && !vidUrlInput && !audUrlInput && (!fileInput.files || !fileInput.files[0])) {
                return alert("Please enter text, provide a URL, or select a file to publish.");
            }

            publishBtn.innerText = "UPLOADING...";
            publishBtn.disabled = true;

            let fileUrl = null;
            let fileType = null;
            const timestamp = Date.now();
            const dateStr = new Date().toLocaleString();
            
            try {
                // Upload local device file if exists
                if(fileInput.files && fileInput.files[0]) {
                    const file = fileInput.files[0];
                    fileType = file.type;
                    const storageRef = storage.ref('posts/' + timestamp + '_' + file.name);
                    const uploadTask = await storageRef.put(file);
                    fileUrl = await uploadTask.ref.getDownloadURL();
                }

                // Push to Realtime DB
                await db.ref('posts').push({
                    text: text,
                    fileUrl: fileUrl,
                    fileType: fileType,
                    imgUrl: imgUrlInput || null,
                    vidUrl: vidUrlInput || null,
                    audUrl: audUrlInput || null,
                    date: dateStr,
                    timestamp: timestamp
                });

                // Clear all inputs
                document.getElementById('post-text').value = '';
                document.getElementById('post-img-url').value = '';
                document.getElementById('post-video-url').value = '';
                document.getElementById('post-audio-url').value = '';
                fileInput.value = '';
                
                alert("Update Published to Live Feed!");
            } catch(e) {
                alert("Upload failed: " + e.message);
            }

            publishBtn.innerText = "PUBLISH NOW";
            publishBtn.disabled = false;
        }

        function deletePost(id) {
            if(!isAdmin) return;
            if(confirm("Are you sure you want to permanently delete this update from Firebase?")) {
                db.ref('posts/' + id).remove().then(() => {
                    alert("Post deleted successfully.");
                }).catch(e => {
                    alert("Delete failed: " + e.message);
                });
            }
        }

        function renderLiveFeed() {
            const container = document.getElementById('live-feed-container');
            container.innerHTML = '';
            
            if(livePosts.length === 0) {
                container.innerHTML = '<p style="color: var(--text-sub); text-align: center; font-size: 13px;">Awaiting live updates from HQ...</p>';
                return;
            }

            // Public feed does NOT contain delete buttons.
            livePosts.forEach(post => {
                const postEl = document.createElement('div');
                postEl.className = 'live-post';
                
                let htmlContent = `<div class="live-post-date"><i class="fas fa-clock"></i> ${post.date || 'Just now'}</div>`;
                
                // 1. Text
                if(post.text) htmlContent += `<div class="live-post-text">${post.text}</div>`;
                
                // 2. Explicit URL Inputs
                if(post.imgUrl) htmlContent += `<img src="${post.imgUrl}" alt="Live Image" style="width: 100%; border-radius: 8px; margin-bottom: 10px; max-height: 300px; object-fit: cover;">`;
                if(post.vidUrl) htmlContent += `<video src="${post.vidUrl}" controls style="width: 100%; max-height: 300px; border-radius: 8px; margin-bottom: 10px; background: #000;"></video>`;
                if(post.audUrl) htmlContent += `<audio src="${post.audUrl}" controls style="width: 100%; margin-bottom: 10px;"></audio>`;
                
                // 3. Uploaded Device Files
                if (post.fileUrl) {
                    const url = post.fileUrl;
                    const type = post.fileType || '';
                    
                    if (type.startsWith('video/')) {
                        htmlContent += `<video src="${url}" controls style="width: 100%; max-height: 300px; border-radius: 8px; margin-bottom: 10px; background: #000;"></video>`;
                    } else if (type.startsWith('audio/')) {
                        htmlContent += `<audio src="${url}" controls style="width: 100%; margin-bottom: 10px;"></audio>`;
                    } else if (type.startsWith('image/')) {
                        htmlContent += `<img src="${url}" alt="Uploaded Image" style="width: 100%; border-radius: 8px; margin-bottom: 10px; max-height: 300px; object-fit: cover;">`;
                    } else {
                        htmlContent += `<a href="${url}" target="_blank" style="color: var(--neon-cyan); display: block; margin-bottom: 10px; font-size: 14px; text-decoration: underline;"><i class="fas fa-file-download"></i> Download Attached File</a>`;
                    }
                }

                postEl.innerHTML = htmlContent;
                container.appendChild(postEl);
            });
        }

        function renderAdminFeed() {
            const container = document.getElementById('admin-post-manager');
            container.innerHTML = '';
            
            if(livePosts.length === 0) {
                container.innerHTML = '<p style="color: #888; font-size: 12px; text-align: center;">No active posts.</p>';
                return;
            }

            // Admin panel contains the delete buttons
            livePosts.forEach(post => {
                const postEl = document.createElement('div');
                postEl.style.background = 'rgba(0,0,0,0.5)';
                postEl.style.padding = '15px';
                postEl.style.borderRadius = '8px';
                postEl.style.border = '1px solid #333';
                
                let content = `<p style="color: #ccc; font-size: 11px; margin-bottom: 8px;"><i class="fas fa-clock"></i> ${post.date || 'Unknown Date'}</p>`;
                
                if(post.text) content += `<p style="color: #fff; font-size: 14px; margin-bottom: 8px;">${post.text.substring(0, 40)}${post.text.length > 40 ? '...' : ''}</p>`;
                
                if(post.imgUrl || post.vidUrl || post.audUrl || post.fileUrl) {
                    content += `<p style="color: var(--neon-cyan); font-size: 11px; margin-bottom: 8px;"><i class="fas fa-paperclip"></i> Media/URL Attached</p>`;
                }
                
                // Secure Delete mapped to actual Firebase Node ID
                content += `<button class="admin-delete-btn" onclick="deletePost('${post.id}')"><i class="fas fa-trash"></i> DELETE POST</button>`;
                
                postEl.innerHTML = content;
                container.appendChild(postEl);
            });
        }


        // ==========================================
        // SYSTEM & HARDWARE LOGIC
        // ==========================================
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
                toggleSettings();
            } else {
                if (document.exitFullscreen) { document.exitFullscreen(); } 
                else if (document.msExitFullscreen) { document.msExitFullscreen(); } 
                else if (document.mozCancelFullScreen) { document.mozCancelFullScreen(); } 
                else if (document.webkitExitFullscreen) { document.webkitExitFullscreen(); }
            }
        }

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
            } catch (err) { alert("Camera Access Denied."); }
        }

        async function activateTorch() {
            try {
                stopMedia();
                const stream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: 'environment' } });
                currentStream = stream;
                const track = stream.getVideoTracks()[0];
                await track.applyConstraints({ advanced: [{ torch: true }] });
                alert("Torch Activated.");
                stopMedia(); 
            } catch (err) {
                alert("Torch not supported.");
                stopMedia();
            }
        }

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
            } catch (err) { alert("Recording failed."); }
        }

        async function activateMic() {
            try {
                stopMedia();
                const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
                currentStream = stream;
                resetMediaFeed();
                document.getElementById('audio-visualizer').style.display = 'flex';
                document.getElementById('media-feed-container').style.display = 'flex';
                toggleSettings();
            } catch (err) { alert("Microphone Access Denied."); }
        }

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
                    error => { text.innerText = "Location retrieval failed."; },
                    { enableHighAccuracy: true }
                );
            } else { alert("Geolocation not supported."); }
        }

        async function toggleMaxBrightness() {
            const body = document.body;
            const btnText = document.getElementById('brightness-text');
            
            if (!isMaxBrightness) {
                body.style.filter = "brightness(1.5) contrast(1.2)";
                btnText.innerText = "NORMAL DISPLAY";
                isMaxBrightness = true;
                if ('wakeLock' in navigator) {
                    try { wakeLock = await navigator.wakeLock.request('screen'); } catch (err) {}
                }
            } else {
                body.style.filter = "none";
                btnText.innerText = "MAX BRIGHTNESS";
                isMaxBrightness = false;
                if (wakeLock !== null) { wakeLock.release().then(() => wakeLock = null); }
            }
        }

        function triggerLockdown() {
            document.getElementById('settings-fullscreen').classList.remove('active');
            document.getElementById('lockdown-overlay').style.display = 'flex';
            document.body.style.pointerEvents = 'none';
        }

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

        /* =========================================================================
           DYNAMIC THEME COLOR SCRIPT (STATUS BAR)
           ========================================================================= */
        const themeMeta = document.getElementById('theme-color-meta');
        let currentHue = 0;
        setInterval(() => {
            currentHue = (currentHue + 1) % 360;
            themeMeta.setAttribute('content', `hsl(${currentHue}, 100%, 15%)`);
        }, 42);
    </script>
</body>
</html>
