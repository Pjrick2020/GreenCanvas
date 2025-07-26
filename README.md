# GreenCanvas
Landscaping tool for garden development
<!-- Analytics Section -->

```
    <div class="section" id="analytics">
        <h2 class="section-title">📊 Canvas Analytics</h2><!DOCTYPE html>
```

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GreenCanvas - Paint Your Perfect Landscape</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

```
    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f0f23 100%);
        color: #ffffff;
        overflow-x: hidden;
        padding-top: 70px; /* Space for fixed header */
    }

    /* Header Navigation */
    .app-header {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        height: 70px;
        background: rgba(26, 26, 46, 0.95);
        backdrop-filter: blur(20px);
        border-bottom: 1px solid rgba(0, 245, 255, 0.2);
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
        z-index: 1000;
    }

    .app-logo {
        font-size: 1.5rem;
        font-weight: 700;
        background: linear-gradient(135deg, #00f5ff, #00ff88);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .nav-menu {
        position: relative;
    }

    .nav-ellipsis {
        background: rgba(0, 245, 255, 0.1);
        border: 1px solid rgba(0, 245, 255, 0.3);
        color: white;
        padding: 10px 15px;
        border-radius: 50px;
        cursor: pointer;
        font-size: 1.2rem;
        transition: all 0.3s ease;
        display: flex;
        align-items: center;
        gap: 5px;
    }

    .nav-ellipsis:hover {
        background: rgba(0, 245, 255, 0.2);
        transform: scale(1.05);
    }

    .dropdown-menu {
        position: absolute;
        top: 60px;
        right: 0;
        background: rgba(26, 26, 46, 0.98);
        backdrop-filter: blur(25px);
        border: 1px solid rgba(0, 245, 255, 0.3);
        border-radius: 15px;
        padding: 20px;
        min-width: 300px;
        opacity: 0;
        visibility: hidden;
        transform: translateY(-10px);
        transition: all 0.3s ease;
        box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
    }

    .dropdown-menu.active {
        opacity: 1;
        visibility: visible;
        transform: translateY(0);
    }

    .menu-category {
        margin-bottom: 20px;
    }

    .menu-category:last-child {
        margin-bottom: 0;
    }

    .category-title {
        color: #00f5ff;
        font-size: 0.9rem;
        font-weight: 600;
        margin-bottom: 10px;
        text-transform: uppercase;
        letter-spacing: 1px;
        border-bottom: 1px solid rgba(0, 245, 255, 0.2);
        padding-bottom: 5px;
    }

    .menu-item {
        display: flex;
        align-items: center;
        gap: 10px;
        padding: 8px 12px;
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.3s ease;
        font-size: 0.9rem;
        margin-bottom: 5px;
    }

    .menu-item:hover {
        background: rgba(0, 245, 255, 0.1);
        transform: translateX(5px);
    }

    .menu-item:last-child {
        margin-bottom: 0;
    }

    /* Calendar Styles */
    .calendar-container {
        background: rgba(255, 255, 255, 0.05);
        border: 1px solid rgba(0, 245, 255, 0.3);
        border-radius: 15px;
        padding: 20px;
        margin-top: 20px;
    }

    .calendar-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }

    .calendar-nav {
        background: rgba(0, 245, 255, 0.1);
        border: 1px solid rgba(0, 245, 255, 0.3);
        color: white;
        padding: 8px 12px;
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.3s ease;
    }

    .calendar-nav:hover {
        background: rgba(0, 245, 255, 0.2);
    }

    .calendar-grid {
        display: grid;
        grid-template-columns: repeat(7, 1fr);
        gap: 10px;
        margin-bottom: 20px;
    }

    .calendar-day-header {
        text-align: center;
        font-weight: 600;
        color: #00f5ff;
        padding: 10px 5px;
        font-size: 0.9rem;
    }

    .calendar-day {
        aspect-ratio: 1;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.3s ease;
        position: relative;
        background: rgba(255, 255, 255, 0.02);
    }

    .calendar-day:hover {
        background: rgba(0, 245, 255, 0.1);
        border-color: #00f5ff;
    }

    .calendar-day.has-tasks {
        border-color: #00ff88;
        background: rgba(0, 255, 136, 0.1);
    }

    .calendar-day.today {
        background: linear-gradient(135deg, rgba(0, 245, 255, 0.2), rgba(0, 255, 136, 0.2));
        border-color: #00f5ff;
    }

    .day-number {
        font-weight: 600;
        margin-bottom: 2px;
    }

    .task-indicator {
        width: 4px;
        height: 4px;
        background: #00ff88;
        border-radius: 50%;
        margin: 1px;
    }

    .plant-schedule {
        margin-top: 20px;
    }

    .schedule-item {
        display: flex;
        align-items: center;
        gap: 15px;
        padding: 15px;
        background: rgba(255, 255, 255, 0.05);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 10px;
        margin-bottom: 10px;
        transition: all 0.3s ease;
    }

    .schedule-item:hover {
        background: rgba(0, 245, 255, 0.1);
        border-color: #00f5ff;
    }

    .plant-image {
        width: 50px;
        height: 50px;
        border-radius: 10px;
        background-size: cover;
        background-position: center;
        border: 2px solid rgba(0, 245, 255, 0.3);
    }

    .schedule-details {
        flex: 1;
    }

    .schedule-title {
        font-weight: 600;
        color: #00f5ff;
        margin-bottom: 5px;
    }

    .schedule-description {
        color: rgba(255, 255, 255, 0.8);
        font-size: 0.9rem;
    }

    .schedule-time {
        color: #00ff88;
        font-size: 0.8rem;
        font-weight: 600;
    }

    .hero-section {
        text-align: center;
        padding: clamp(40px, 8vh, 80px) 20px;
        position: relative;
        background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.3));
        overflow: hidden;
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .photo-carousel {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: -1;
        display: flex;
    }

    .carousel-photo {
        position: absolute;
        width: 100%;
        height: 100%;
        background-size: cover;
        background-position: center;
        opacity: 0;
        transition: opacity 2s ease-in-out;
        transform: scale(1.1);
        animation: kenBurns 20s infinite linear;
    }

    .carousel-photo.active {
        opacity: 1;
    }

    @keyframes kenBurns {
        0% { transform: scale(1.1) rotate(0deg); }
        25% { transform: scale(1.2) rotate(1deg); }
        50% { transform: scale(1.15) rotate(0deg); }
        75% { transform: scale(1.25) rotate(-1deg); }
        100% { transform: scale(1.1) rotate(0deg); }
    }

    .carousel-photo.user-photo::before {
        content: '📱';
        position: absolute;
        top: 10px;
        right: 10px;
        background: rgba(0, 245, 255, 0.8);
        border-radius: 50%;
        width: 30px;
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 14px;
    }

    .hero-title {
        font-size: clamp(2.5rem, 8vw, 4.5rem);
        font-weight: 700;
        background: linear-gradient(135deg, #00f5ff, #00ff88);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        margin-bottom: 20px;
        animation: glow 2s ease-in-out infinite alternate;
        line-height: 1.1;
        letter-spacing: -0.02em;
    }

    @keyframes glow {
        from { filter: drop-shadow(0 0 20px rgba(0, 245, 255, 0.3)); }
        to { filter: drop-shadow(0 0 40px rgba(0, 245, 255, 0.6)); }
    }

    .hero-subtitle {
        font-size: clamp(1rem, 3vw, 1.3rem);
        color: rgba(255, 255, 255, 0.8);
        margin-bottom: 40px;
        max-width: 900px;
        margin-left: auto;
        margin-right: auto;
        line-height: 1.6;
    }

    .cta-button {
        background: linear-gradient(135deg, #00f5ff, #00ff88);
        color: #1a1a2e;
        border: none;
        padding: 18px 40px;
        font-size: 1.1rem;
        font-weight: 600;
        border-radius: 30px;
        cursor: pointer;
        transition: all 0.3s ease;
        box-shadow: 0 10px 30px rgba(0, 245, 255, 0.3);
    }

    .cta-button:hover {
        transform: translateY(-3px);
        box-shadow: 0 15px 40px rgba(0, 245, 255, 0.5);
    }

    .main-container {
        max-width: 1400px;
        margin: 0 auto;
        padding: 0 20px;
    }

    .section {
        background: rgba(255, 255, 255, 0.08);
        backdrop-filter: blur(25px);
        border: 1px solid rgba(255, 255, 255, 0.15);
        border-radius: 25px;
        padding: 35px;
        margin-bottom: 35px;
        box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
        position: relative;
        overflow: hidden;
    }

    .section::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: linear-gradient(45deg, 
            transparent, 
            rgba(0, 245, 255, 0.05) 25%, 
            transparent 50%, 
            rgba(0, 255, 136, 0.05) 75%, 
            transparent);
        z-index: -1;
        animation: shimmer 4s ease-in-out infinite;
    }

    @keyframes shimmer {
        0%, 100% { transform: translateX(-100%); }
        50% { transform: translateX(100%); }
    }

    .floating-gallery {
        position: fixed;
        top: 20%;
        right: -300px;
        width: 250px;
        height: 400px;
        z-index: 100;
        transition: right 0.5s ease;
        opacity: 0.7;
    }

    .floating-gallery.show {
        right: 20px;
    }

    .gallery-photo {
        position: absolute;
        width: 180px;
        height: 120px;
        border-radius: 15px;
        background-size: cover;
        background-position: center;
        box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5);
        border: 3px solid rgba(255, 255, 255, 0.2);
        transition: all 0.8s cubic-bezier(0.4, 0.0, 0.2, 1);
        cursor: pointer;
    }

    .gallery-photo:hover {
        transform: scale(1.1) rotate(5deg);
        box-shadow: 0 25px 50px rgba(0, 245, 255, 0.4);
        border-color: #00f5ff;
    }

    .section-title {
        font-size: 1.8rem;
        font-weight: 600;
        color: #00f5ff;
        margin-bottom: 20px;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .design-workspace {
        display: grid;
        grid-template-columns: 1fr 350px;
        gap: 30px;
        margin-bottom: 30px;
    }

    .viewport-3d {
        background: rgba(0, 0, 0, 0.3);
        border: 2px solid rgba(0, 245, 255, 0.3);
        border-radius: 15px;
        height: 600px;
        position: relative;
        overflow: hidden;
        cursor: grab;
    }

    .viewport-3d:active {
        cursor: grabbing;
    }

    .controls-panel {
        background: rgba(255, 255, 255, 0.03);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 15px;
        padding: 20px;
        height: fit-content;
    }

    .control-group {
        margin-bottom: 25px;
    }

    .control-label {
        font-weight: 500;
        margin-bottom: 10px;
        color: #ffffff;
        font-size: 0.9rem;
    }

    .input-field {
        width: 100%;
        padding: 12px 15px;
        background: rgba(255, 255, 255, 0.05);
        border: 1px solid rgba(255, 255, 255, 0.2);
        border-radius: 8px;
        color: #ffffff;
        font-family: inherit;
        transition: all 0.3s ease;
    }

    .input-field:focus {
        outline: none;
        border-color: #00f5ff;
        box-shadow: 0 0 15px rgba(0, 245, 255, 0.3);
    }

    .btn-primary {
        background: linear-gradient(135deg, #00f5ff, #00ff88);
        color: #1a1a2e;
        border: none;
        padding: 10px 20px;
        border-radius: 8px;
        font-weight: 600;
        cursor: pointer;
        transition: all 0.3s ease;
        width: 100%;
        margin-top: 10px;
    }

    .btn-primary:hover {
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(0, 245, 255, 0.4);
    }

    .btn-secondary {
        background: rgba(255, 255, 255, 0.1);
        color: #ffffff;
        border: 1px solid rgba(255, 255, 255, 0.2);
        padding: 8px 16px;
        border-radius: 6px;
        cursor: pointer;
        transition: all 0.3s ease;
        margin: 5px;
        font-size: 0.9rem;
    }

    .btn-secondary:hover {
        background: rgba(255, 255, 255, 0.2);
        border-color: #00f5ff;
    }

    .plant-library {
        max-height: 300px;
        overflow-y: auto;
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 8px;
        background: rgba(0, 0, 0, 0.2);
    }

    .plant-item {
        padding: 12px 15px;
        border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        cursor: pointer;
        transition: all 0.3s ease;
        display: flex;
        align-items: center;
        gap: 10px;
    }

    .plant-item:hover {
        background: rgba(0, 245, 255, 0.1);
    }

    .plant-item.selected {
        background: rgba(0, 245, 255, 0.2);
        border-left: 3px solid #00f5ff;
    }

    .uploaded-photos {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
        gap: 10px;
        margin-top: 10px;
        max-height: 200px;
        overflow-y: auto;
    }

    .uploaded-photo {
        width: 80px;
        height: 60px;
        background-size: cover;
        background-position: center;
        border-radius: 8px;
        border: 2px solid rgba(255, 255, 255, 0.2);
        cursor: pointer;
        transition: all 0.3s ease;
        position: relative;
    }

    .uploaded-photo:hover {
        border-color: #00f5ff;
        transform: scale(1.05);
    }

    .uploaded-photo .delete-btn {
        position: absolute;
        top: -5px;
        right: -5px;
        width: 20px;
        height: 20px;
        background: #ff4444;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        color: white;
        font-size: 12px;
        cursor: pointer;
        opacity: 0;
        transition: opacity 0.3s ease;
    }

    .uploaded-photo:hover .delete-btn {
        opacity: 1;
    }

    .camera-section {
        margin-top: 20px;
        padding: 20px;
        background: rgba(0, 245, 255, 0.1);
        border: 1px solid rgba(0, 245, 255, 0.3);
        border-radius: 15px;
    }

    .camera-controls {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 10px;
        margin-top: 15px;
    }

    .btn-camera {
        background: linear-gradient(135deg, #ff6b6b, #ee5a24);
        color: white;
        border: none;
        padding: 12px 15px;
        border-radius: 8px;
        font-weight: 600;
        cursor: pointer;
        transition: all 0.3s ease;
        font-size: 0.9rem;
    }

    .btn-camera:hover {
        transform: translateY(-2px);
        box-shadow: 0 8px 25px rgba(255, 107, 107, 0.4);
    }

    #cameraPreview {
        width: 100%;
        max-width: 300px;
        border-radius: 10px;
        margin-top: 15px;
        display: none;
    }

    .photo-reference {
        position: absolute;
        top: 10px;
        left: 10px;
        background: rgba(0, 0, 0, 0.7);
        color: white;
        padding: 5px 10px;
        border-radius: 15px;
        font-size: 0.8rem;
        opacity: 0;
        transition: opacity 0.3s ease;
    }

    .viewport-3d:hover .photo-reference {
        opacity: 1;
    }

    .lidar-status {
        margin-top: 10px;
        padding: 10px;
        border-radius: 8px;
        font-size: 0.9rem;
        text-align: center;
        transition: all 0.3s ease;
    }

    .lidar-status.scanning {
        background: rgba(255, 193, 7, 0.2);
        border: 1px solid #ffc107;
        color: #ffc107;
    }

    .lidar-status.success {
        background: rgba(40, 167, 69, 0.2);
        border: 1px solid #28a745;
        color: #28a745;
    }

    .lidar-status.error {
        background: rgba(220, 53, 69, 0.2);
        border: 1px solid #dc3545;
        color: #dc3545;
    }

    .progress-bar {
        width: 100%;
        height: 8px;
        background: rgba(255, 255, 255, 0.1);
        border-radius: 4px;
        overflow: hidden;
        margin-top: 10px;
    }

    .progress-fill {
        height: 100%;
        background: linear-gradient(90deg, #00f5ff, #00ff88);
        width: 0%;
        transition: width 0.3s ease;
        animation: progressPulse 2s infinite;
    }

    @keyframes progressPulse {
        0%, 100% { opacity: 1; }
        50% { opacity: 0.7; }
    }

    .lidar-visualization {
        position: absolute;
        top: 10px;
        right: 10px;
        width: 150px;
        height: 100px;
        background: rgba(0, 0, 0, 0.8);
        border: 1px solid rgba(0, 245, 255, 0.5);
        border-radius: 8px;
        display: none;
        z-index: 5;
    }

    .lidar-point {
        position: absolute;
        width: 2px;
        height: 2px;
        background: #00f5ff;
        border-radius: 50%;
        animation: lidarPulse 1s infinite;
    }

    @keyframes lidarPulse {
        0%, 100% { opacity: 0.3; transform: scale(1); }
        50% { opacity: 1; transform: scale(1.5); }
    }

    .depth-indicator {
        position: absolute;
        bottom: 10px;
        left: 10px;
        background: rgba(0, 0, 0, 0.8);
        color: #00f5ff;
        padding: 5px 10px;
        border-radius: 15px;
        font-size: 0.8rem;
        display: none;
    }

    .mini-gallery {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 15px;
        margin: 20px 0;
        padding: 20px;
        background: rgba(0, 0, 0, 0.2);
        border-radius: 15px;
        border: 1px solid rgba(0, 245, 255, 0.3);
    }

    .mini-photo {
        width: 100%;
        height: 100px;
        background-size: cover;
        background-position: center;
        border-radius: 10px;
        transition: all 0.3s ease;
        cursor: pointer;
        border: 2px solid transparent;
    }

    .mini-photo:hover {
        transform: scale(1.05);
        border-color: #00f5ff;
        box-shadow: 0 10px 20px rgba(0, 245, 255, 0.3);
    }

    .share-panel {
        background: linear-gradient(135deg, rgba(0, 245, 255, 0.1), rgba(0, 255, 136, 0.1));
        border: 1px solid rgba(0, 245, 255, 0.3);
        border-radius: 15px;
        padding: 25px;
        text-align: center;
    }

    .share-buttons {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
        gap: 15px;
        margin-top: 20px;
    }

    .share-btn {
        background: rgba(255, 255, 255, 0.1);
        border: 1px solid rgba(255, 255, 255, 0.2);
        color: #ffffff;
        padding: 12px 15px;
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.3s ease;
        font-size: 0.9rem;
    }

    .share-btn:hover {
        background: rgba(0, 245, 255, 0.2);
        border-color: #00f5ff;
    }

    .stats-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
        gap: 20px;
        margin-top: 20px;
    }

    .stat-card {
        background: rgba(255, 255, 255, 0.05);
        border: 1px solid rgba(255, 255, 255, 0.1);
        border-radius: 10px;
        padding: 20px;
        text-align: center;
        transition: all 0.3s ease;
    }

    .stat-card:hover {
        transform: translateY(-3px);
        border-color: #00f5ff;
    }

    .stat-value {
        font-size: 2rem;
        font-weight: 700;
        color: #00ff88;
        margin-bottom: 5px;
    }

    .stat-label {
        color: rgba(255, 255, 255, 0.7);
        font-size: 0.9rem;
    }

    .loading-overlay {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.7);
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        z-index: 10;
    }

    .spinner {
        width: 50px;
        height: 50px;
        border: 3px solid rgba(0, 245, 255, 0.3);
        border-top: 3px solid #00f5ff;
        border-radius: 50%;
        animation: spin 1s linear infinite;
        margin-bottom: 15px;
    }

    @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }

    @media (max-width: 768px) {
        .design-workspace {
            grid-template-columns: 1fr;
        }
        
        .hero-title {
            font-size: 2.5rem;
        }
        
        .share-buttons {
            grid-template-columns: 1fr;
        }
        
        .camera-controls {
            grid-template-columns: 1fr;
        }
        
        #cameraPreview {
            width: 100%;
            max-width: none;
        }
        
        .floating-gallery {
            display: none; /* Hide on mobile to save space */
        }
    }
</style>
```

</head>
<body>
    <!-- App Header Navigation -->
    <div class="app-header">
        <div class="app-logo">
            🎨 GreenCanvas
        </div>
        <div class="nav-menu">
            <button class="nav-ellipsis" onclick="toggleDropdown()">
                ⋯ Menu
            </button>
            <div class="dropdown-menu" id="dropdownMenu">
                <div class="menu-category">
                    <div class="category-title">🎨 Design Tools</div>
                    <div class="menu-item" onclick="scrollToSection('designer')">
                        <span>🖌️</span> Landscape Designer
                    </div>
                    <div class="menu-item" onclick="scrollToSection('designer')">
                        <span>📡</span> LiDAR Mapping
                    </div>
                    <div class="menu-item" onclick="scrollToSection('designer')">
                        <span>🌿</span> Plant Library
                    </div>
                </div>

```
            <div class="menu-category">
                <div class="category-title">📱 Media & Sharing</div>
                <div class="menu-item" onclick="scrollToSection('share')">
                    <span>📸</span> Photo Upload
                </div>
                <div class="menu-item" onclick="scrollToSection('share')">
                    <span>🚀</span> Share Canvas
                </div>
                <div class="menu-item" onclick="openCamera()">
                    <span>📱</span> Take Photo
                </div>
            </div>

            <div class="menu-category">
                <div class="category-title">📅 Planning & Schedule</div>
                <div class="menu-item" onclick="showCalendar()">
                    <span>📅</span> Plant Calendar
                </div>
                <div class="menu-item" onclick="scrollToSection('analytics')">
                    <span>📊</span> Analytics
                </div>
                <div class="menu-item" onclick="showPlantSchedule()">
                    <span>⏰</span> Care Schedule
                </div>
            </div>

            <div class="menu-category">
                <div class="category-title">🧪 Community</div>
                <div class="menu-item" onclick="scrollToSection('beta')">
                    <span>🧪</span> Beta Program
                </div>
                <div class="menu-item" onclick="joinBetaProgram('discord')">
                    <span>💬</span> Discord Community
                </div>
                <div class="menu-item" onclick="showHelp()">
                    <span>❓</span> Help & Support
                </div>
            </div>
        </div>
    </div>
</div>

<!-- Hero Section -->
<div class="hero-section">
    <div class="photo-carousel">
        <div class="carousel-photo active" style="background-image: url('https://images.unsplash.com/photo-1416879595882-3373a0480b5b?w=1200&h=800&fit=crop');"></div>
        <div class="carousel-photo" style="background-image: url('https://images.unsplash.com/photo-1585320806297-9794b3e4eeae?w=1200&h=800&fit=crop');"></div>
        <div class="carousel-photo" style="background-image: url('https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1200&h=800&fit=crop');"></div>
        <div class="carousel-photo" style="background-image: url('https://images.unsplash.com/photo-1584464491033-06628f3a6b7b?w=1200&h=800&fit=crop');"></div>
        <div class="carousel-photo" style="background-image: url('https://images.unsplash.com/photo-1513475382585-d06e58bcb0e0?w=1200&h=800&fit=crop');"></div>
    </div>
    <h1 class="hero-title">🎨 GreenCanvas</h1>
    <p class="hero-subtitle">
        Paint Your Perfect Landscape in 3D. Design stunning outdoor spaces with LiDAR mapping, photo references, and real-time visualization. Your garden masterpiece starts here.
    </p>
    <button class="cta-button" onclick="scrollToDesigner()">Start Painting Your Landscape</button>
</div>

<div class="floating-gallery" id="floatingGallery">
    <div class="gallery-photo" style="background-image: url('https://images.unsplash.com/photo-1586023492125-27b2c045efd7?w=400&h=300&fit=crop'); top: 0; left: 0; transform: rotate(-5deg);"></div>
    <div class="gallery-photo" style="background-image: url('https://images.unsplash.com/photo-1601293863837-543e8e17c481?w=400&h=300&fit=crop'); top: 80px; left: 40px; transform: rotate(8deg);"></div>
    <div class="gallery-photo" style="background-image: url('https://images.unsplash.com/photo-1591857177580-dc82b9ac4e1e?w=400&h=300&fit=crop'); top: 160px; left: 20px; transform: rotate(-3deg);"></div>
    <div class="gallery-photo" style="background-image: url('https://images.unsplash.com/photo-1516253317440-5bb2805774ec?w=400&h=300&fit=crop'); top: 240px; left: 60px; transform: rotate(6deg);"></div>
</div>

<div class="main-container">
    <!-- Main Design Section -->
    <div class="section" id="designer">
        <h2 class="section-title">🎨 Landscape Canvas Designer</h2>
        
        <div class="design-workspace">
            <div class="viewport-3d" id="viewport3d">
                <div class="photo-reference" id="photoReference">No reference photo selected</div>
                <div class="lidar-visualization" id="lidarViz"></div>
                <div class="depth-indicator" id="depthIndicator">Depth: 0m</div>
                <div class="loading-overlay" id="loadingOverlay">
                    <div class="spinner"></div>
                    <div>Initializing GreenCanvas Studio...</div>
                </div>
            </div>
            
            <div class="controls-panel">
                <div class="control-group">
                    <div class="control-label">📡 LiDAR Environment Mapping</div>
                    <button class="btn-primary" onclick="startLidarScan()" id="lidarBtn">Start LiDAR Scan</button>
                    <div id="lidarStatus" class="lidar-status"></div>
                    <div id="lidarProgress" class="progress-bar" style="display: none;">
                        <div class="progress-fill"></div>
                    </div>
                </div>

                <div class="control-group">
                    <div class="control-label">📐 Yard Dimensions</div>
                    <input type="number" class="input-field" id="yardWidth" placeholder="Width (feet)" value="30">
                    <input type="number" class="input-field" id="yardLength" placeholder="Length (feet)" value="40" style="margin-top: 10px;">
                    <button class="btn-primary" onclick="updateYardSize()">Update Yard</button>
                </div>

                <div class="control-group">
                    <div class="control-label">📱 Upload Photos</div>
                    <input type="file" id="photoUpload" accept="image/*" multiple style="display: none;">
                    <button class="btn-primary" onclick="document.getElementById('photoUpload').click()">📸 Add Photos</button>
                    <div id="uploadedPhotos" class="uploaded-photos"></div>
                </div>

                <div class="control-group">
                    <div class="control-label">🌿 Plant Library</div>
                    <div class="plant-library" id="plantLibrary">
                        <!-- Plants populated by JavaScript -->
                    </div>
                </div>

                <div class="control-group">
                    <div class="control-label">📷 View Controls</div>
                    <button class="btn-secondary" onclick="setView('overhead')">Overhead View</button>
                    <button class="btn-secondary" onclick="setView('perspective')">3D Perspective</button>
                    <button class="btn-secondary" onclick="setView('walkthrough')">Walkthrough</button>
                    <button class="btn-secondary" onclick="resetCamera()">Reset View</button>
                </div>

                <div class="control-group">
                    <div class="control-label">🔧 Tools</div>
                    <button class="btn-secondary" onclick="clearYard()">Clear All</button>
                    <button class="btn-secondary" onclick="undoLast()">Undo Last</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Plant Calendar Section -->
    <div class="section" id="calendar" style="display: none;">
        <h2 class="section-title">📅 Plant Care Calendar</h2>
        
        <div class="calendar-container">
            <div class="calendar-header">
                <button class="calendar-nav" onclick="changeMonth(-1)">‹ Previous</button>
                <h3 id="currentMonth" style="color: #00f5ff; margin: 0;">March 2024</h3>
                <button class="calendar-nav" onclick="changeMonth(1)">Next ›</button>
            </div>
            
            <div class="calendar-grid">
                <div class="calendar-day-header">Sun</div>
                <div class="calendar-day-header">Mon</div>
                <div class="calendar-day-header">Tue</div>
                <div class="calendar-day-header">Wed</div>
                <div class="calendar-day-header">Thu</div>
                <div class="calendar-day-header">Fri</div>
                <div class="calendar-day-header">Sat</div>
                <!-- Calendar days will be populated by JavaScript -->
            </div>
            
            <div class="plant-schedule" id="plantSchedule">
                <h4 style="color: #00f5ff; margin-bottom: 15px;">Today's Plant Care Tasks</h4>
                <!-- Schedule items will be populated by JavaScript -->
            </div>
        </div>
    </div>

    <!-- Share & Export Section -->
    <div class="section" id="share">
        <h2 class="section-title">🚀 Share Your Canvas</h2>
        
        <div class="camera-section">
            <h3 style="color: #00f5ff; margin-bottom: 10px;">📷 Photo Reference</h3>
            <p style="color: rgba(255, 255, 255, 0.8); font-size: 0.9rem; margin-bottom: 15px;">
                Upload or take photos of your current yard to use as reference while designing
            </p>
            <div class="camera-controls">
                <button class="btn-camera" onclick="openCamera()">📱 Take Photo</button>
                <button class="btn-camera" onclick="document.getElementById('photoUpload').click()">📁 Upload Photos</button>
            </div>
            <video id="cameraPreview" autoplay playsinline></video>
            <canvas id="photoCanvas" style="display: none;"></canvas>
        </div>
        
        <div class="mini-gallery">
            <div class="mini-photo" style="background-image: url('https://images.unsplash.com/photo-1523348837708-15d4a09cfac2?w=300&h=200&fit=crop');" onclick="enlargePhoto(this)"></div>
            <div class="mini-photo" style="background-image: url('https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=300&h=200&fit=crop');" onclick="enlargePhoto(this)"></div>
            <div class="mini-photo" style="background-image: url('https://images.unsplash.com/photo-1598300042247-d088f8ab3a91?w=300&h=200&fit=crop');" onclick="enlargePhoto(this)"></div>
            <div class="mini-photo" style="background-image: url('https://images.unsplash.com/photo-1574958269340-fa927503f3dd?w=300&h=200&fit=crop');" onclick="enlargePhoto(this)"></div>
            <div class="mini-photo" style="background-image: url('https://images.unsplash.com/photo-1583847268964-b28dc8f51f92?w=300&h=200&fit=crop');" onclick="enlargePhoto(this)"></div>
            <div class="mini-photo" style="background-image: url('https://images.unsplash.com/photo-1461354464878-ad92f492a5a0?w=300
```