# Christofou9067.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
  <title>FitRest - 健身组间悬浮计时器</title>
  <meta name="description" content="专为健身打造的安卓画中画悬浮窗组间休息计时器，一键45秒倒计时，悬浮刷手机不超时" />
  <meta name="theme-color" content="#020617" />
  <meta name="mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;700;800;900&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg: #020617;
      --card-bg: #0b1120;
      --border: #1e293b;
      --primary: #f59e0b;
      --primary-hover: #d97706;
      --text: #f8fafc;
      --text-muted: #94a3b8;
      --danger: #ef4444;
      --success: #10b981;
    }
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      -webkit-tap-highlight-color: transparent;
      user-select: none;
    }
    body {
      background-color: var(--bg);
      color: var(--text);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      overflow-x: hidden;
    }
    .font-outfit {
      font-family: 'Outfit', -apple-system, sans-serif;
    }
    .tabular {
      font-variant-numeric: tabular-nums;
    }
    /* Header */
    .app-header {
      position: sticky;
      top: 0;
      z-index: 40;
      height: 56px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 16px;
      background: rgba(2, 6, 23, 0.9);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
    }
    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
      font-weight: 800;
      font-size: 16px;
      color: #fff;
    }
    .brand-logo {
      width: 32px;
      height: 32px;
      border-radius: 10px;
      background: linear-gradient(135deg, #f59e0b, #ea580c);
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 900;
      font-size: 14px;
      color: #fff;
      box-shadow: 0 2px 10px rgba(245, 158, 11, 0.3);
    }
    .nav-actions {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .btn-icon {
      background: #0f172a;
      border: 1px solid var(--border);
      color: var(--text-muted);
      border-radius: 10px;
      width: 36px;
      height: 36px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: all 0.15s;
    }
    .btn-icon:hover {
      color: #fff;
      border-color: #334155;
    }
    .btn-pip {
      background: linear-gradient(135deg, #f59e0b, #ea580c);
      color: #fff;
      border: none;
      font-size: 12px;
      font-weight: 700;
      padding: 8px 14px;
      border-radius: 10px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 6px;
      box-shadow: 0 4px 12px rgba(245, 158, 11, 0.25);
      transition: transform 0.1s, opacity 0.15s;
    }
    .btn-pip:active {
      transform: scale(0.96);
    }
    .btn-pip.active {
      background: #1e293b;
      color: #38bdf8;
      border: 1px solid #0284c7;
      box-shadow: none;
    }

    /* Main layout */
    .main-content {
      flex: 1;
      width: 100%;
      max-width: 500px;
      margin: 0 auto;
      padding: 16px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    /* Exercise & Set bar */
    .exercise-bar {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
      padding: 0 4px;
    }
    .exercise-info {
      display: flex;
      flex-direction: column;
    }
    .exercise-label {
      font-size: 11px;
      color: var(--primary);
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    .exercise-name {
      font-size: 15px;
      font-weight: 700;
      color: #fff;
      cursor: pointer;
    }
    .set-stepper {
      display: flex;
      align-items: center;
      gap: 8px;
      background: var(--card-bg);
      border: 1px solid var(--border);
      padding: 4px 8px;
      border-radius: 12px;
    }
    .step-btn {
      width: 26px;
      height: 26px;
      border-radius: 8px;
      border: none;
      background: #1e293b;
      color: var(--text-muted);
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
      font-weight: bold;
    }
    .step-btn:hover {
      color: #fff;
    }
    .step-val {
      font-size: 13px;
      font-weight: 700;
      color: #fff;
      min-width: 50px;
      text-align: center;
    }

    /* Timer Dial */
    .dial-wrapper {
      position: relative;
      width: 260px;
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 24px;
    }
    .dial-glow {
      position: absolute;
      width: 210px;
      height: 210px;
      border-radius: 50%;
      background: rgba(245, 158, 11, 0.15);
      filter: blur(40px);
      transition: background 0.3s;
      pointer-events: none;
    }
    .dial-glow.alert {
      background: rgba(239, 68, 68, 0.4);
      animation: pulseAlert 1s infinite alternate;
    }
    @keyframes pulseAlert {
      from { transform: scale(0.95); opacity: 0.5; }
      to { transform: scale(1.05); opacity: 0.9; }
    }
    .dial-svg {
      width: 260px;
      height: 260px;
      transform: rotate(-90deg);
    }
    .track-circle {
      fill: none;
      stroke: #1e293b;
      stroke-width: 14;
    }
    .progress-circle {
      fill: none;
      stroke: url(#timerGrad);
      stroke-width: 14;
      stroke-linecap: round;
      stroke-dasharray: 753.98;
      stroke-dashoffset: 0;
      transition: stroke-dashoffset 0.25s linear;
    }
    .dial-center-btn {
      position: absolute;
      width: 200px;
      height: 200px;
      border-radius: 50%;
      background: #090d16;
      border: 1px solid var(--border);
      box-shadow: 0 10px 30px rgba(0,0,0,0.6);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: transform 0.12s;
    }
    .dial-center-btn:active {
      transform: scale(0.96);
    }
    .time-digits {
      font-size: 64px;
      font-weight: 900;
      color: #fff;
      line-height: 1;
    }
    .time-digits.urgent {
      color: var(--danger);
      animation: flashDigits 0.5s infinite alternate;
    }
    @keyframes flashDigits