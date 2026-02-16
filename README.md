# eme
[sapporo_pregnancy_app .html](https://github.com/user-attachments/files/25334912/sapporo_pregnancy_app.html)
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>札幌市 出産準備アプリ</title>
  <meta name="theme-color" content="#FF69B4" />

  <!-- Fonts: preconnect + swap -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Rounded+Mplus+1c:wght@400;700;800&family=Noto+Sans+JP:wght@300;400;500;700&display=swap" rel="stylesheet">

  <style>
    :root{
      --pink-50:#FFFAFC;
      --pink-100:#FFF0F5;
      --pink-200:#FFE5EC;
      --pink-300:#FFC0CB;
      --pink-400:#FFB6C1;
      --pink-500:#FF69B4;
      --pink-600:#FF1493;

      --gold-400:#FFD700;
      --orange-500:#FF8C00;
      --green-500:#4CAF50;

      --text-strong:#2D3142;
      --text:#333;
      --text-weak:#666;
      --text-mute:#999;

      --shadow-lg:0 20px 60px rgba(0,0,0,.2);
      --shadow-md:0 10px 30px rgba(255, 105, 180, .25);
      --shadow-sm:0 5px 20px rgba(0,0,0,.05);

      --radius-lg:30px;
      --radius-md:20px;
      --radius-sm:12px;

      --focus: 0 0 0 3px rgba(255,105,180,.25);
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      font-family:'Noto Sans JP',system-ui,-apple-system,Segoe UI,Roboto,"Hiragino Kaku Gothic ProN","BIZ UDPGothic","Yu Gothic UI","Yu Gothic",sans-serif;
      background: linear-gradient(180deg, var(--pink-200) 0%, var(--pink-100) 50%, var(--pink-50) 100%);
      color:var(--text-strong);
      -webkit-tap-highlight-color: transparent;
      margin:0;
    }

    a,button,input,select,textarea{outline:none}
    a:focus-visible, button:focus-visible, input:focus-visible, [role="dialog"] button:focus-visible{
      box-shadow: var(--focus);
      border-radius:10px;
    }

    /* ログイン画面 */
    #loginScreen{
      position:fixed; inset:0; display:flex; align-items:center; justify-content:center;
      z-index:10000; padding:20px;
      background: linear-gradient(135deg, var(--pink-400) 0%, var(--pink-300) 100%);
    }
    .login-container{
      background:#fff; border-radius:var(--radius-lg);
      padding:40px 30px; width:min(380px, 100%);
      box-shadow:var(--shadow-lg); text-align:center;
    }
    .login-icon{
      font-size:80px; margin-bottom:20px; animation:bounce 2s ease-in-out infinite;
    }
    @keyframes bounce{
      0%,100%{transform:translateY(0)}
      50%{transform:translateY(-10px)}
    }
    .login-title{
      font-family:'Rounded Mplus 1c',sans-serif; font-size:24px; font-weight:800; color:var(--pink-500);
      margin-bottom:6px;
    }
    .login-subtitle{font-size:14px; color:var(--text-weak); margin-bottom:22px;}
    .form-group{margin-bottom:16px; text-align:left;}
    .form-group label{display:block; font-size:13px; font-weight:600; color:var(--text-weak); margin-bottom:8px;}
    .form-row{display:flex; gap:8px; align-items:center}
    .form-group input{
      width:100%; padding:14px; border:2px solid var(--pink-200); border-radius:15px; font-size:16px;
      transition:border-color .2s, box-shadow .2s;
    }
    .form-group input:focus{border-color:var(--pink-500); box-shadow:var(--focus)}
    .login-btn{
      width:100%; padding:14px 16px; background:linear-gradient(135deg, var(--pink-500), var(--pink-600));
      color:#fff; border:none; border-radius:15px; font-size:16px; font-weight:700; cursor:pointer;
      margin-top:12px; box-shadow:0 4px 15px rgba(255,105,180,.3);
    }
    .login-btn:active{transform:scale(.98)}
    .login-hint{margin-top:14px; padding:12px; background:var(--pink-100); border-radius:12px; font-size:12px; color:var(--text-weak)}
    .error-message{background:#FFE5E5; color:#D32F2F; padding:12px; border-radius:12px; font-size:13px; margin-bottom:12px; display:none;}
    .error-message.show{display:block}
    .toggle-pass{
      padding:10px 12px; border:1px solid var(--pink-200); background:#fff; border-radius:12px; color:var(--text-weak);
      cursor:pointer; white-space:nowrap;
    }

    /* メインコンテンツ切替 */
    #mainContent{display:none}
    #mainContent.show{display:block}

    /* ヘッダー */
    .app-header{
      background:linear-gradient(135deg, var(--pink-500) 0%, var(--pink-600) 100%);
      color:#fff; padding:20px; position:relative; overflow:hidden;
    }
    .app-header::before{
      content:'👶'; position:absolute; font-size:200px; opacity:.1; top:-50px; right:-50px; animation:float 6s ease-in-out infinite;
    }
    @keyframes float{
      0%,100%{transform:translate(0,0) rotate(0)} 50%{transform:translate(-10px,-10px) rotate(5deg)}
    }
    .header-top{display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;}
    .app-title{font-family:'Rounded Mplus 1c',sans-serif; font-size:18px; font-weight:800}
    .logout-btn{
      padding:8px 16px; background:rgba(255,255,255,.2); border:1px solid rgba(255,255,255,.3);
      border-radius:20px; color:#fff; font-size:12px; cursor:pointer; backdrop-filter: blur(10px);
    }

    /* カウントダウンカード */
    .countdown-card{
      background:#fff; border-radius:25px; padding:24px 18px; margin:20px; margin-top:-40px;
      box-shadow:var(--shadow-md); text-align:center; position:relative;
    }
    .baby-icon{font-size:56px; margin-bottom:8px; animation:heartbeat 1.5s ease-in-out infinite}
    @keyframes heartbeat{0%,100%{transform:scale(1)} 25%{transform:scale(1.1)} 50%{transform:scale(1)}}
    .countdown-main{
      font-family:'Rounded Mplus 1c',sans-serif; font-size:44px; font-weight:800; color:var(--pink-500); margin:6px 0;
    }
    .countdown-label{font-size:14px; color:var(--text-weak); margin-bottom:10px}
    .week-info{display:flex; justify-content:space-around; margin-top:12px; padding-top:12px; border-top:2px dashed var(--pink-200)}
    .week-item{text-align:center}
    .week-item-label{font-size:12px; color:var(--text-mute); margin-bottom:4px}
    .week-item-value{font-family:'Rounded Mplus 1c',sans-serif; font-size:18px; font-weight:700; color:var(--pink-500)}
    .change-date-btn{
      margin-top:12px; padding:10px 18px; background:linear-gradient(135deg, var(--pink-200), var(--pink-300));
      color:var(--pink-500); border:none; border-radius:20px; font-size:14px; font-weight:700; cursor:pointer;
    }

    /* カード共通 */
    .baby-growth-card, .advice-card, .checklist-section, .contact-item, .benefit-item{
      border-radius:20px; padding:18px; margin:20px; background:#fff; box-shadow:var(--shadow-sm);
    }
    .card-title{
      font-family:'Rounded Mplus 1c',sans-serif; font-size:18px; font-weight:700; color:var(--pink-500);
      margin-bottom:12px; display:flex; align-items:center; gap:8px;
    }
    .baby-size{
      display:flex; align-items:center; justify-content:space-around; padding:16px;
      background:linear-gradient(135deg, var(--pink-100), var(--pink-50)); border-radius:15px; margin-bottom:12px;
    }
    .size-item{text-align:center}
    .size-icon{font-size:36px; margin-bottom:6px}
    .size-label{font-size:12px; color:var(--text-mute)}
    .size-value{font-size:16px; font-weight:700; color:var(--pink-500); margin-top:2px}
    .growth-description{font-size:14px; line-height:1.8; color:var(--text-weak)}

    .advice-card{
      background:linear-gradient(135deg, #FFF9E6, #FFF); border-left:5px solid var(--gold-400);
    }
    .advice-title{font-family:'Rounded Mplus 1c',sans-serif; font-size:16px; font-weight:700; color:var(--orange-500); margin-bottom:10px; display:flex; gap:8px; align-items:center}
    .advice-list{list-style:none; padding:0; margin:0}
    .advice-list li{padding:8px 0 8px 25px; position:relative; font-size:14px; line-height:1.6; color:var(--text-weak)}
    .advice-list li::before{content:'✓'; position:absolute; left:0; color:var(--gold-400); font-weight:700}

    /* チェックリスト */
    .checklist-section .card-title{margin:0}
    .checklist-header{display:flex; justify-content:space-between; align-items:center; margin-bottom:12px}
    .progress-ring{width:50px; height:50px; border-radius:50%; background:linear-gradient(135deg, var(--pink-500), var(--pink-600));
      display:flex; align-items:center; justify-content:center; color:#fff; font-weight:700; font-size:14px}
    .checklist-link{display:block; padding:14px; background:linear-gradient(135deg, var(--pink-200), var(--pink-100));
      border-radius:15px; text-decoration:none; color:var(--pink-500); font-weight:700; text-align:center; margin-top:12px}

    .checklist-tabs{display:flex; background:#fff; border-bottom:2px solid var(--pink-200); position:sticky; top:0; z-index:50}
    .checklist-tab{flex:1; padding:14px; text-align:center; cursor:pointer; font-weight:600; color:var(--text-mute); border-bottom:3px solid transparent; transition:all .2s}
    .checklist-tab.active{color:var(--pink-500); border-bottom-color:var(--pink-500)}
    .checklist-content{display:none}
    .checklist-content.active{display:block}

    .checklist-group{background:#fff; border-radius:15px; padding:12px; margin:15px 15px; box-shadow:var(--shadow-sm)}
    .checklist-group-header{font-weight:700; color:var(--pink-500); margin-bottom:10px; font-size:16px; padding-bottom:10px; border-bottom:2px dashed var(--pink-200)}
    .checklist-group-header.urgent{color:var(--pink-600)}

    .checklist-item-mini{display:flex; gap:12px; padding:12px; margin-bottom:8px; background:#FAFAFA; border-radius:12px; cursor:pointer; transition:background .2s}
    .checklist-item-mini:hover{background:var(--pink-100)}
    .checklist-item-mini.checked{background:#E8F5E9; opacity:.9}
    .checkbox-mini{width:22px; height:22px; border:2px solid var(--pink-500); border-radius:50%; flex-shrink:0; display:flex; align-items:center; justify-content:center; transition:all .2s}
    .checklist-item-mini.checked .checkbox-mini{background:var(--green-500); border-color:var(--green-500)}
    .checklist-item-mini.checked .checkbox-mini::after{content:'✓'; color:#fff; font-weight:700; font-size:14px}
    .item-text{flex:1}
    .item-title-mini{font-weight:600; font-size:14px; margin-bottom:4px; color:var(--text)}
    .item-desc-mini{font-size:12px; color:var(--text-mute)}
    .shop-links-mini{display:flex; gap:8px; margin-top:6px; flex-wrap:wrap}
    .shop-links-mini a{padding:4px 12px; background:linear-gradient(135deg, var(--pink-500), var(--pink-600)); color:#fff; text-decoration:none; border-radius:12px; font-size:11px; font-weight:600}

    .badge-must{display:inline-block; padding:2px 6px; background:var(--pink-500); color:#fff; border-radius:4px; font-size:10px; font-weight:700; margin-left:4px}
    .badge-recommended{display:inline-block; padding:2px 6px; background:var(--gold-400); color:#333; border-radius:4px; font-size:10px; font-weight:700; margin-left:4px}
    .badge-optional{display:inline-block; padding:2px 6px; background:#999; color:#fff; border-radius:4px; font-size:10px; font-weight:700; margin-left:4px}

    .info-card-mini{background:linear-gradient(135deg, #FFF9E6, #FFF); border-radius:12px; padding:15px; margin:0 20px 20px 20px; border-left:4px solid var(--gold-400)}
    .info-title{font-weight:700; color:var(--orange-500); margin-bottom:10px; font-size:14px}
    .info-row{display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid #F5F5F5; font-size:13px}
    .info-row:last-child{border-bottom:none}
    .urgent{color:var(--pink-600)}

    /* 情報タブ */
    .contact-item{background:linear-gradient(135deg, var(--pink-100), var(--pink-50)); border-left:4px solid var(--pink-500)}
    .contact-name{font-weight:700; color:#333; margin-bottom:6px; font-size:14px}
    .contact-phone{display:inline-block; padding:8px 16px; background:linear-gradient(135deg, var(--pink-500), var(--pink-600)); color:#fff; text-decoration:none; border-radius:20px; font-size:14px; font-weight:600; margin-top:4px}
    .contact-detail{font-size:13px; color:var(--text-weak); margin-top:5px}
    .benefit-item{background:#FAFAFA; border-left:4px solid var(--gold-400)}
    .benefit-name{font-weight:700; color:#333; margin-bottom:4px; font-size:14px}
    .benefit-amount{font-family:'Rounded Mplus 1c',sans-serif; font-size:18px; font-weight:800; color:var(--pink-500); margin-bottom:4px}
    .benefit-detail{font-size:12px; color:var(--text-weak)}
    .ward-links{display:grid; grid-template-columns:repeat(2,1fr); gap:10px}
    .ward-link{padding:12px; background:linear-gradient(135deg, var(--pink-200), var(--pink-100)); color:var(--pink-500); text-decoration:none; border-radius:12px; text-align:center; font-weight:600; font-size:14px; transition:transform .1s, background .2s}
    .ward-link:active{transform:scale(.96); background:linear-gradient(135deg, var(--pink-300), var(--pink-200))}

    /* ナビゲーションバー */
    .nav-bar{
      position:fixed; left:0; right:0; bottom:0; background:#fff; border-top:1px solid var(--pink-200);
      display:flex; justify-content:space-around; padding:8px 0; box-shadow:0 -5px 20px rgba(0,0,0,.05); z-index:100;
    }
    .nav-item{flex:1; text-align:center; padding:10px 6px; cursor:pointer; transition:color .2s; background:none; border:none}
    .nav-item.active{color:var(--pink-500)}
    .nav-icon{font-size:22px; display:block; margin-bottom:4px}
    .nav-label{font-size:11px; font-weight:500}

    .tab-content{display:none; padding-bottom:90px}
    .tab-content.active{display:block}

    /* カスタムポップアップ（ダイアログ） */
    .custom-popup{display:none; position:fixed; inset:0; background:rgba(0,0,0,.5); z-index:10001; align-items:center; justify-content:center; padding:20px}
    .custom-popup.show{display:flex}
    .popup-content{background:#fff; border-radius:25px; padding:24px; width:min(420px, 100%); box-shadow:0 20px 60px rgba(0,0,0,.3); position:relative}
    .popup-title{font-family:'Rounded Mplus 1c',sans-serif; font-size:20px; font-weight:700; color:var(--pink-500); margin-bottom:14px; text-align:center}
    .popup-input{width:100%; padding:14px; border:2px solid var(--pink-200); border-radius:15px; font-size:16px; margin-bottom:14px}
    .popup-buttons{display:flex; gap:10px}
    .popup-btn{flex:1; padding:12px; border:none; border-radius:15px; font-size:16px; font-weight:700; cursor:pointer}
    .popup-btn-primary{background:linear-gradient(135deg, var(--pink-500), var(--pink-600)); color:#fff}
    .popup-btn-secondary{background:#F5F5F5; color:var(--text-weak)}

    /* 付加機能ボタン */
    .tools-row{display:flex; gap:8px; margin:10px 20px 0 20px; flex-wrap:wrap}
    .tool-btn{padding:8px 12px; border-radius:12px; border:1px solid var(--pink-200); background:#fff; color:var(--text-weak); cursor:pointer}
    .sr-only{position:absolute!important; width:1px!important; height:1px!important; padding:0!important; margin:-1px!important; overflow:hidden!important; clip:rect(0,0,0,0)!important; white-space:nowrap!important; border:0!important}

    /* 動きに弱いユーザー配慮 */
    @media (prefers-reduced-motion: reduce){
      *{animation:none!important; transition:none!important}
    }
  </style>
</head>
<body>
  <!-- ログイン画面 -->
  <div id="loginScreen" aria-labelledby="appTitle">
    <div class="login-container">
      <div class="login-icon" aria-hidden="true">👶</div>
      <div id="appTitle" class="login-title">出産準備アプリ</div>
      <div class="login-subtitle">札幌市版</div>

      <form id="loginForm" novalidate>
        <div class="error-message" id="errorMessage" role="alert">
          ユーザー名またはパスワードが正しくありません
        </div>

        <div class="form-group">
          <label for="username">ユーザー名</label>
          <input id="username" name="username" inputmode="numeric" autocomplete="username" placeholder="123" required />
        </div>

        <div class="form-group">
          <label for="password">パスワード</label>
          <div class="form-row">
            <input id="password" name="password" type="password" autocomplete="current-password" placeholder="123" required />
            <button class="toggle-pass" type="button" id="togglePassBtn" aria-pressed="false" aria-controls="password">表示</button>
          </div>
        </div>

        <button type="submit" class="login-btn">ログイン</button>

        <div class="login-hint" aria-live="polite">
          <strong>💡 ログイン情報</strong><br>
          ID: <code>123</code> / PW: <code>123</code>
        </div>
      </form>
    </div>
  </div>

  <!-- メインアプリ -->
  <div id="mainContent" aria-live="polite">
    <!-- ホームタブ -->
    <section id="homeTab" class="tab-content active" aria-labelledby="homeTabTitle">
      <header class="app-header">
        <div class="header-top">
          <h1 id="homeTabTitle" class="app-title">🍼 出産準備アプリ</h1>
          <button class="logout-btn" id="logoutBtn" type="button">ログアウト</button>
        </div>
      </header>

      <!-- カウントダウンカード -->
      <section class="countdown-card" aria-describedby="dueDateLabel">
        <div class="baby-icon" aria-hidden="true">👶</div>
        <div class="countdown-main" id="daysLeft" aria-live="polite">--</div>
        <div class="countdown-label" id="dueDateLabel">出産予定日まで</div>
        <div class="week-info">
          <div class="week-item">
            <div class="week-item-label">現在</div>
            <div class="week-item-value" id="currentWeek">--週--日</div>
          </div>
          <div class="week-item">
            <div class="week-item-label">予定日</div>
            <div class="week-item-value" id="dueDate">--/--</div>
          </div>
        </div>
        <button class="change-date-btn" id="changeDueDateBtn" type="button">📅 予定日を変更</button>
      </section>

      <!-- 赤ちゃんの成長カード -->
      <section class="baby-growth-card">
        <div class="card-title"><span>🌱</span><span id="babyGrowthTitle">赤ちゃんの成長</span></div>
        <div class="baby-size">
          <div class="size-item" aria-label="赤ちゃんの大きさ">
            <div class="size-icon" aria-hidden="true">📏</div>
            <div class="size-label">大きさ</div>
            <div class="size-value" id="babySize">--cm</div>
          </div>
          <div class="size-item" aria-label="赤ちゃんの体重">
            <div class="size-icon" aria-hidden="true">⚖️</div>
            <div class="size-label">体重</div>
            <div class="size-value" id="babyWeight">--g</div>
          </div>
        </div>
        <div class="growth-description" id="growthDescription">
          予定日を設定すると、赤ちゃんの成長情報が表示されます。
        </div>
      </section>

      <!-- アドバイスカード -->
      <section class="advice-card">
        <div class="advice-title"><span>💡</span><span>今週のアドバイス</span></div>
        <ul class="advice-list" id="adviceList">
          <li>予定日を設定すると、週数に応じたアドバイスが表示されます</li>
        </ul>
      </section>

      <!-- チェックリストへのリンク -->
      <section class="checklist-section">
        <div class="checklist-header">
          <div>
            <div class="card-title" style="margin-bottom:4px;">📋 申請手続き・準備リスト</div>
            <div style="font-size:12px; color:var(--text-mute);">全82項目</div>
          </div>
          <div class="progress-ring" id="checklistProgress" aria-live="polite" aria-label="チェックリスト進捗">0%</div>
        </div>
        <a href="#" class="checklist-link" id="openChecklistLink">チェックリストを開く →</a>

        <div class="tools-row" aria-label="チェックリスト管理ツール">
          <button class="tool-btn" id="exportBtn" type="button">進捗をエクスポート</button>
          <button class="tool-btn" id="importBtn" type="button">進捗をインポート</button>
          <button class="tool-btn" id="resetBtn" type="button">進捗リセット</button>
          <input type="file" id="importFile" accept="application/json" class="sr-only" />
        </div>
      </section>
    </section>

    <!-- チェックリストタブ -->
    <section id="checklistTab" class="tab-content" aria-labelledby="checklistTabTitle">
      <header class="app-header">
        <div class="header-top">
          <h2 id="checklistTabTitle" class="app-title">📋 チェックリスト</h2>
          <button class="logout-btn" id="logoutBtn2" type="button">ログアウト</button>
        </div>
      </header>

      <!-- タブ切り替え -->
      <div class="checklist-tabs" role="tablist">
        <button class="checklist-tab active" data-checktab="applications" role="tab" aria-selected="true">📋 申請手続き</button>
        <button class="checklist-tab" data-checktab="preparation" role="tab" aria-selected="false">🛍️ 出産準備</button>
      </div>

      <!-- 申請手続きタブ -->
      <div id="applicationsChecklistTab" class="checklist-content active">
        <div style="padding: 15px; padding-bottom: 100px;">
          <div class="checklist-group">
            <div class="checklist-group-header">妊娠がわかったら</div>

            <div class="checklist-item-mini" data-id="app-1" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">妊娠届出（母子健康手帳）</div>
                <div class="item-desc-mini">区保健センターで交付</div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="app-2" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">妊婦支援給付（1回目）</div>
                <div class="item-desc-mini">5万円支給</div>
              </div>
            </div>
          </div>

          <div class="checklist-group">
            <div class="checklist-group-header">出産予定日の8週前</div>

            <div class="checklist-item-mini" data-id="app-3" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">妊婦支援給付（2回目）</div>
                <div class="item-desc-mini">5万円支給</div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="app-4" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">産休申請（会社員）</div>
                <div class="item-desc-mini">勤務先へ申請</div>
              </div>
            </div>
          </div>

          <div class="checklist-group">
            <div class="checklist-group-header urgent">⚠️ 出産後すぐ（15日以内）</div>

            <div class="checklist-item-mini" data-id="app-5" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">出生届</div>
                <div class="item-desc-mini">14日以内必須</div>
              </div>
            </div>

            <div class="checklist-item-mini urgent" data-id="app-6" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">🔴 児童手当</div>
                <div class="item-desc-mini">15日以内必須！遅れると受給開始が遅れます</div>
              </div>
            </div>

            <div class="checklist-item-mini urgent" data-id="app-7" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">🔴 子ども医療費助成</div>
                <div class="item-desc-mini">できるだけ早く申請</div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="app-8" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">健康保険加入</div>
                <div class="item-desc-mini">勤務先または区役所</div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="app-9" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">出産育児一時金</div>
                <div class="item-desc-mini">50万円支給</div>
              </div>
            </div>
          </div>

          <div class="checklist-group">
            <div class="checklist-group-header">産後1〜2ヶ月</div>

            <div class="checklist-item-mini" data-id="app-10" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">出産手当金</div>
                <div class="item-desc-mini">日給の約2/3×98日分</div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="app-11" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">国民年金保険料免除</div>
                <div class="item-desc-mini">産前産後4ヶ月分</div>
              </div>
            </div>
          </div>

          <div class="checklist-group">
            <div class="checklist-group-header">育休開始前</div>

            <div class="checklist-item-mini" data-id="app-12" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">育休申請</div>
                <div class="item-desc-mini">勤務先へ1ヶ月前までに</div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="app-13" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">育児休業給付金</div>
                <div class="item-desc-mini">最初180日:67%、以降:50%</div>
              </div>
            </div>
          </div>

          <div class="info-card-mini" aria-label="給付金一覧">
            <div class="info-title">💰 給付金一覧</div>
            <div class="info-row"><span>妊婦支援給付</span><span>計10万円</span></div>
            <div class="info-row"><span>出産育児一時金</span><span>50万円</span></div>
            <div class="info-row"><span>児童手当</span><span>月15,000円〜</span></div>
            <div class="info-row"><span>子ども医療費助成</span><span>18歳まで</span></div>
          </div>
        </div>
      </div>

      <!-- 出産準備タブ -->
      <div id="preparationChecklistTab" class="checklist-content">
        <div style="padding: 15px; padding-bottom: 100px;">
          <div class="checklist-group">
            <div class="checklist-group-header">👩 ママ用品</div>

            <div class="checklist-item-mini" data-id="prep-1" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">産褥ショーツ <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E7%94%A3%E8%A4%A5%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%84" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E7%94%A3%E8%A4%A5%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%84/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-2" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">授乳ブラ <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E6%8E%88%E4%B9%B3%E3%83%96%E3%83%A9" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E6%8E%88%E4%B9%B3%E3%83%96%E3%83%A9/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-3" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">母乳パッド <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E6%AF%8D%E4%B9%B3%E3%83%91%E3%83%83%E3%83%89" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E6%AF%8D%E4%B9%B3%E3%83%91%E3%83%83%E3%83%89/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-4" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">授乳クッション <span class="badge-recommended">推奨</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E6%8E%88%E4%B9%B3%E3%82%AF%E3%83%83%E3%82%B7%E3%83%A7%E3%83%B3" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E6%8E%88%E4%B9%B3%E3%82%AF%E3%83%83%E3%82%B7%E3%83%A7%E3%83%B3/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>
          </div>

          <div class="checklist-group">
            <div class="checklist-group-header">👶 赤ちゃん衣類</div>

            <div class="checklist-item-mini" data-id="prep-10" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">短肌着（5〜6枚） <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E6%96%B0%E7%94%9F%E5%85%90+%E7%9F%AD%E8%82%8C%E7%9D%80" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E6%96%B0%E7%94%9F%E5%85%90+%E7%9F%AD%E8%82%8C%E7%9D%80/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-11" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">コンビ肌着（5〜6枚） <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E3%82%B3%E3%83%B3%E3%83%93%E8%82%8C%E7%9D%80" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E3%82%B3%E3%83%B3%E3%83%93%E8%82%8C%E7%9D%80/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-12" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">防寒着・ジャンプスーツ <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E3%83%99%E3%83%93%E3%83%BC+%E3%82%B8%E3%83%A3%E3%83%B3%E3%83%97%E3%82%B9%E3%83%BC%E3%83%84" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E3%83%99%E3%83%93%E3%83%BC+%E3%82%B8%E3%83%A3%E3%83%B3%E3%83%97%E3%82%B9%E3%83%BC%E3%83%84/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>
          </div>

          <div class="checklist-group">
            <div class="checklist-group-header">🍼 授乳・調乳用品</div>

            <div class="checklist-item-mini" data-id="prep-20" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">哺乳瓶 <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E5%93%BA%E4%B9%B3%E7%93%B6" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E5%93%BA%E4%B9%B3%E7%93%B6/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-21" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">粉ミルク <span class="badge-recommended">推奨</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E7%B2%89%E3%83%9F%E3%83%AB%E3%82%AF+%E6%96%B0%E7%94%9F%E5%85%90" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E7%B2%89%E3%83%9F%E3%83%AB%E3%82%AF/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>
          </div>

          <div class="checklist-group">
            <div class="checklist-group-header">🚗 お出かけ用品</div>

            <div class="checklist-item-mini" data-id="prep-30" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">チャイルドシート <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E3%83%81%E3%83%A3%E3%82%A4%E3%83%AB%E3%83%89%E3%82%B7%E3%83%BC%E3%83%88+%E6%96%B0%E7%94%9F%E5%85%90" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E3%83%81%E3%83%A3%E3%82%A4%E3%83%AB%E3%83%89%E3%82%B7%E3%83%BC%E3%83%88/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-31" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">ベビーカー <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E3%83%99%E3%83%93%E3%82%AB%E3%83%BC+A%E5%9E%8B" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E3%83%99%E3%83%93%E3%82%AB%E3%83%BC/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>

            <div class="checklist-item-mini" data-id="prep-32" tabindex="0" role="checkbox" aria-checked="false">
              <div class="checkbox-mini" aria-hidden="true"></div>
              <div class="item-text">
                <div class="item-title-mini">抱っこ紐 <span class="badge-must">必須</span></div>
                <div class="shop-links-mini">
                  <a href="https://www.amazon.co.jp/s?k=%E6%8A%B1%E3%81%A3%E3%81%93%E7%B4%90+%E6%96%B0%E7%94%9F%E5%85%90" target="_blank" rel="noopener">Amazon</a>
                  <a href="https://search.rakuten.co.jp/search/mall/%E6%8A%B1%E3%81%A3%E3%81%93%E7%B4%90/" target="_blank" rel="noopener">楽天</a>
                </div>
              </div>
            </div>
          </div>

          <div class="info-card-mini">
            <div class="info-title">❄️ 札幌ならではのポイント</div>
            <ul style="list-style:none; padding:0; margin:10px 0 0 0;">
              <li style="padding:5px 0; font-size:13px;">✓ 冬の防寒対策は必須（10月〜4月）</li>
              <li style="padding:5px 0; font-size:13px;">✓ 加湿器とベビーローションは冬の必需品</li>
              <li style="padding:5px 0; font-size:13px;">✓ ベビーカーは雪道対応を選ぼう</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- 情報タブ -->
    <section id="infoTab" class="tab-content" aria-labelledby="infoTabTitle">
      <header class="app-header">
        <div class="header-top">
          <h2 id="infoTabTitle" class="app-title">ℹ️ 情報・問い合わせ</h2>
          <button class="logout-btn" id="logoutBtn3" type="button">ログアウト</button>
        </div>
      </header>

      <div style="padding: 15px; padding-bottom: 100px;">
        <!-- 問い合わせ先 -->
        <section class="baby-growth-card">
          <div class="card-title"><span>📞</span><span>主な問い合わせ先</span></div>

          <div class="contact-item">
            <div class="contact-name">札幌市妊婦支援給付コールセンター</div>
            <a href="tel:0112130383" class="contact-phone">📱 011-213-0383</a>
          </div>

          <div class="contact-item">
            <div class="contact-name">お住まいの区役所</div>
            <div class="contact-detail">保健福祉課・保険年金課・戸籍住民課</div>
          </div>

          <div class="contact-item">
            <div class="contact-name">勤務先の人事・総務部</div>
            <div class="contact-detail">産休・育休・各種給付金の申請</div>
          </div>

          <div class="contact-item">
            <div class="contact-name">ハローワーク</div>
            <div class="contact-detail">育児休業給付金（通常は会社経由）</div>
          </div>
        </section>

        <!-- 給付金詳細 -->
        <section class="baby-growth-card">
          <div class="card-title"><span>💰</span><span>給付金・助成金詳細</span></div>

          <div class="benefit-item">
            <div class="benefit-name">妊婦のための支援給付</div>
            <div class="benefit-amount">計10万円</div>
            <div class="benefit-detail">5万円×2回（妊娠届出後、出産予定日の前月）</div>
          </div>

          <div class="benefit-item">
            <div class="benefit-name">出産育児一時金</div>
            <div class="benefit-amount">子ども1人につき50万円</div>
            <div class="benefit-detail">加入している健康保険へ申請</div>
          </div>

          <div class="benefit-item">
            <div class="benefit-name">出産手当金</div>
            <div class="benefit-amount">日給の約2/3×98日分</div>
            <div class="benefit-detail">会社員の場合、産休中の給与補償</div>
          </div>

          <div class="benefit-item">
            <div class="benefit-name">育児休業給付金</div>
            <div class="benefit-amount">最初180日：67%、以降：50%</div>
            <div class="benefit-detail">雇用保険から支給</div>
          </div>

          <div class="benefit-item">
            <div class="benefit-name">児童手当</div>
            <div class="benefit-amount">月15,000円〜10,000円</div>
            <div class="benefit-detail">0〜3歳：15,000円、3歳〜中学：10,000円</div>
          </div>

          <div class="benefit-item">
            <div class="benefit-name">子ども医療費助成</div>
            <div class="benefit-amount">18歳まで</div>
            <div class="benefit-detail">初診時のみ医科580円・歯科510円</div>
          </div>
        </section>

        <!-- 区役所リンク -->
        <section class="baby-growth-card">
          <div class="card-title"><span>🏛️</span><span>札幌市区役所一覧</span></div>
          <div class="ward-links">
            <a href="https://www.city.sapporo.jp/chuo/" target="_blank" rel="noopener" class="ward-link">中央区</a>
            <a href="https://www.city.sapporo.jp/kitaku/" target="_blank" rel="noopener" class="ward-link">北区</a>
            <a href="https://www.city.sapporo.jp/higashi/" target="_blank" rel="noopener" class="ward-link">東区</a>
            <a href="https://www.city.sapporo.jp/shiroishi/" target="_blank" rel="noopener" class="ward-link">白石区</a>
            <a href="https://www.city.sapporo.jp/toyohira/" target="_blank" rel="noopener" class="ward-link">豊平区</a>
            <a href="https://www.city.sapporo.jp/minami/" target="_blank" rel="noopener" class="ward-link">南区</a>
            <a href="https://www.city.sapporo.jp/nishi/" target="_blank" rel="noopener" class="ward-link">西区</a>
            <a href="https://www.city.sapporo.jp/atsubetsu/" target="_blank" rel="noopener" class="ward-link">厚別区</a>
            <a href="https://www.city.sapporo.jp/teine/" target="_blank" rel="noopener" class="ward-link">手稲区</a>
            <a href="https://www.city.sapporo.jp/kiyota/" target="_blank" rel="noopener" class="ward-link">清田区</a>
          </div>
        </section>

        <!-- アプリ情報 -->
        <section class="baby-growth-card">
          <div class="card-title"><span>ℹ️</span><span>このアプリについて</span></div>
          <div style="font-size:14px; line-height:1.8; color:var(--text-weak);">
            <p style="margin-bottom:12px;">札幌市版 出産準備アプリは、妊娠中の方と出産を控えた方のために作られた総合サポートアプリです。</p>
            <p style="margin-bottom:12px;">
              <strong>主な機能：</strong><br>
              • 出産予定日カウントダウン<br>
              • 赤ちゃんの成長情報<br>
              • 週数別アドバイス<br>
              • 申請手続きチェックリスト<br>
              • 出産準備品リスト
            </p>
            <p style="font-size:12px; color:var(--text-mute); margin-top:16px;">
              ※このアプリの情報は2026年2月時点のものです。最新の情報は各窓口でご確認ください。
            </p>
          </div>
        </section>
      </div>
    </section>

    <!-- ナビゲーションバー -->
    <nav class="nav-bar" aria-label="アプリのメインナビゲーション">
      <button class="nav-item active" data-tab="home" type="button">
        <span class="nav-icon" aria-hidden="true">🏠</span>
        <span class="nav-label">ホーム</span>
      </button>
      <button class="nav-item" data-tab="checklist" type="button">
        <span class="nav-icon" aria-hidden="true">📋</span>
        <span class="nav-label">リスト</span>
      </button>
      <button class="nav-item" data-tab="info" type="button">
        <span class="nav-icon" aria-hidden="true">ℹ️</span>
        <span class="nav-label">情報</span>
      </button>
    </nav>
  </div>

  <!-- ダイアログ -->
  <div class="custom-popup" id="dueDatePopup" role="dialog" aria-modal="true" aria-labelledby="dueDateDialogTitle">
    <div class="popup-content" role="document">
      <div class="popup-title" id="dueDateDialogTitle">📅 出産予定日の設定</div>
      <input type="date" class="popup-input" id="dueDateInput" />
      <div class="popup-buttons">
        <button class="popup-btn popup-btn-secondary" id="cancelDueDateBtn" type="button">キャンセル</button>
        <button class="popup-btn popup-btn-primary" id="saveDueDateBtn" type="button">保存</button>
      </div>
    </div>
  </div>

  <script>
    // ==============================
    // 定数・Storageキー（名前空間 + 版管理）
    // ==============================
    const APP_VERSION = '1.1.0';
    const STORAGE = {
      SESSION: 'pregnancy_app_session',
      DUE_DATE: 'pregnancy_app_dueDate_v2',
      CHECKLIST: 'pregnancy_app_checklist_progress_v2'
    };
    const VALID_CREDENTIALS = { username: '123', password: '123' }; // デモ用。実運用ではサーバ側で。

    // ==============================
    // 初期化
    // ==============================
    document.addEventListener('DOMContentLoaded', () => {
      // ログイン処理
      const loginForm = document.getElementById('loginForm');
      const errorMessage = document.getElementById('errorMessage');
      const usernameEl = document.getElementById('username');
      const passwordEl = document.getElementById('password');
      const togglePassBtn = document.getElementById('togglePassBtn');

      togglePassBtn.addEventListener('click', () => {
        const isPassword = passwordEl.getAttribute('type') === 'password';
        passwordEl.setAttribute('type', isPassword ? 'text' : 'password');
        togglePassBtn.setAttribute('aria-pressed', String(isPassword));
        togglePassBtn.textContent = isPassword ? '非表示' : '表示';
      });

      loginForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const username = usernameEl.value.trim();
        const password = passwordEl.value.trim();

        if (username === VALID_CREDENTIALS.username && password === VALID_CREDENTIALS.password) {
          sessionStorage.setItem(STORAGE.SESSION, JSON.stringify({ username, ts: Date.now(), v: APP_VERSION }));
          errorMessage.classList.remove('show');
          showMainContent();
        } else {
          errorMessage.classList.add('show');
          passwordEl.value = '';
          passwordEl.focus();
        }
      });

      // ログアウト
      document.querySelectorAll('#logoutBtn, #logoutBtn2, #logoutBtn3').forEach(btn => {
        btn.addEventListener('click', () => {
          if (confirm('ログアウトしますか？')) {
            sessionStorage.removeItem(STORAGE.SESSION);
            showLoginScreen();
          }
        });
      });

      // ナビゲーション
      document.querySelector('.nav-bar').addEventListener('click', (e) => {
        const btn = e.target.closest('.nav-item');
        if (!btn) return;
        switchTab(btn.dataset.tab);
      });

      // チェックリストタブ切替
      document.querySelector('.checklist-tabs').addEventListener('click', (e) => {
        const btn = e.target.closest('.checklist-tab');
        if (!btn) return;
        const target = btn.dataset.checktab;
        switchChecklistTab(target, btn);
      });

      // 予定日ダイアログ
      document.getElementById('changeDueDateBtn').addEventListener('click', openDueDatePopup);
      document.getElementById('cancelDueDateBtn').addEventListener('click', closeDueDatePopup);
      document.getElementById('saveDueDateBtn').addEventListener('click', saveDueDate);
      // ダイアログ外クリック/ESCで閉じる
      const popup = document.getElementById('dueDatePopup');
      popup.addEventListener('click', (e) => { if (e.target === popup) closeDueDatePopup(); });
      document.addEventListener('keydown', (e) => {
        if (popup.classList.contains('show') && e.key === 'Escape') closeDueDatePopup();
      });

      // ホームの「チェックリストを開く」
      document.getElementById('openChecklistLink').addEventListener('click', (e) => {
        e.preventDefault();
        switchTab('checklist');
      });

      // チェックリストのクリック（イベント委譲 + キーボード対応）
      document.getElementById('checklistTab').addEventListener('click', (e) => {
        const item = e.target.closest('.checklist-item-mini');
        if (!item) return;
        toggleChecklistItem(item);
      });
      document.getElementById('checklistTab').addEventListener('keydown', (e) => {
        if (e.key === ' ' || e.key === 'Enter') {
          const item = e.target.closest('.checklist-item-mini');
          if (item) {
            e.preventDefault();
            toggleChecklistItem(item);
          }
        }
      });

      // 進捗ツール
      const exportBtn = document.getElementById('exportBtn');
      const importBtn = document.getElementById('importBtn');
      const resetBtn = document.getElementById('resetBtn');
      const importFile = document.getElementById('importFile');

      exportBtn.addEventListener('click', exportProgress);
      importBtn.addEventListener('click', () => importFile.click());
      importFile.addEventListener('change', importProgress);
      resetBtn.addEventListener('click', () => {
        if (confirm('チェックリストの進捗をリセットしますか？')) {
          localStorage.removeItem(STORAGE.CHECKLIST);
          loadChecklistProgress();
        }
      });

      // セッション確認
      checkSession();
    });

    // ==============================
    // 画面表示制御
    // ==============================
    function checkSession(){
      try{
        const s = sessionStorage.getItem(STORAGE.SESSION);
        if (!s) return showLoginScreen();
        const data = JSON.parse(s);
        const within = Date.now() - data.ts < 24*60*60*1000; // 24H
        if (within) return showMainContent();
      }catch(_){ }
      showLoginScreen();
    }

    function showLoginScreen(){
      document.getElementById('loginScreen').style.display = 'flex';
      document.getElementById('mainContent').classList.remove('show');
      // ログインIDにフォーカス
      setTimeout(() => document.getElementById('username')?.focus(), 50);
    }

    function showMainContent(){
      document.getElementById('loginScreen').style.display = 'none';
      document.getElementById('mainContent').classList.add('show');
      initApp();
      setTimeout(loadChecklistProgress, 300);
    }

    function switchTab(tabName){
      document.querySelectorAll('.nav-item').forEach(i => i.classList.toggle('active', i.dataset.tab === tabName));
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      const targetId = ({home:'homeTab', checklist:'checklistTab', info:'infoTab'})[tabName];
      document.getElementById(targetId).classList.add('active');
    }

    function switchChecklistTab(target, btn){
      document.querySelectorAll('.checklist-tab').forEach(t => {
        const active = t === btn;
        t.classList.toggle('active', active);
        t.setAttribute('aria-selected', active ? 'true':'false');
      });
      document.querySelectorAll('.checklist-content').forEach(c => c.classList.remove('active'));
      document.getElementById(target + 'ChecklistTab').classList.add('active');
    }

    // ==============================
    // 予定日 ダイアログ
    // ==============================
    function openDueDatePopup(){
      const el = document.getElementById('dueDateInput');
      const current = localStorage.getItem(STORAGE.DUE_DATE);
      const today = new Date();
      const DEFAULT = `${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,'0')}-${String(today.getDate()).padStart(2,'0')}`;

      // 受け付け範囲（-45週〜+45週）: 安全な範囲に限定
      const min = new Date(today.getTime() - 7*24*3600*1000*45);
      const max = new Date(today.getTime() + 7*24*3600*1000*45);
      const fmt = (d) => `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
      el.min = fmt(min); el.max = fmt(max);

      el.value = current || DEFAULT;
      document.getElementById('dueDatePopup').classList.add('show');
      setTimeout(()=> el.focus(), 30);
    }
    function closeDueDatePopup(){
      document.getElementById('dueDatePopup').classList.remove('show');
    }

    function saveDueDate(){
      const value = document.getElementById('dueDateInput').value;
      if (!value) return;
      const d = new Date(value);
      if (Number.isNaN(+d)) return;
      localStorage.setItem(STORAGE.DUE_DATE, value);
      updateDisplay(value);
      closeDueDatePopup();
    }

    // ==============================
    // アプリ初期化・表示更新
    // ==============================
    function initApp(){
      const dueDate = localStorage.getItem(STORAGE.DUE_DATE);
      if (!dueDate){
        // 初回はダイアログを開く
        openDueDatePopup();
      }else{
        updateDisplay(dueDate);
      }
    }

    function updateDisplay(dueDateStr){
      const dueDate = new Date(dueDateStr);
      if (Number.isNaN(+dueDate)) return;

      const today = new Date();
      today.setHours(0,0,0,0);
      dueDate.setHours(0,0,0,0);

      const diffTime = dueDate - today;
      const daysLeft = Math.ceil(diffTime / (1000*60*60*24));

      // 妊娠週数: LMP基準で280日（40週）を想定
      const TOTAL = 280;
      let elapsedDays = TOTAL - daysLeft;        // 経過日数
      if (elapsedDays < 0) elapsedDays = 0;
      if (elapsedDays > TOTAL) elapsedDays = TOTAL;

      const weeks = Math.floor(elapsedDays / 7);
      const days = elapsedDays % 7;

      // 表示
      document.getElementById('dueDate').textContent = (dueDate.getMonth()+1) + '/' + dueDate.getDate();
      const daysLeftEl = document.getElementById('daysLeft');

      if (daysLeft > 0){
        daysLeftEl.textContent = `${daysLeft}日`;
        document.getElementById('dueDateLabel').textContent = '出産予定日まで';
      }else if (daysLeft === 0){
        daysLeftEl.textContent = 'きょう！';
        document.getElementById('dueDateLabel').textContent = '出産予定日';
      }else{
        daysLeftEl.textContent = '誕生！';
        document.getElementById('dueDateLabel').textContent = `出産から ${Math.abs(daysLeft)}日`;
      }

      document.getElementById('currentWeek').textContent = `${weeks}週${days}日`;
      updateBabyGrowth(weeks);
      updateAdvice(weeks);
    }

    // ==============================
    // 成長情報 & アドバイス
    // ==============================
    function updateBabyGrowth(weeks){
      const growthData = {
        8:  { size: '1.6cm',  weight: '1g',    desc: 'ラズベリーくらいの大きさ。心臓が動き始め、手足の形が見え始めています。' },
        12: { size: '6cm',    weight: '14g',   desc: 'プラムくらい。指が分かれ、爪が生え始めています。' },
        16: { size: '12cm',   weight: '100g',  desc: 'アボカドくらい。活発に動き、表情も作れるように。' },
        20: { size: '25cm',   weight: '300g',  desc: 'バナナくらい。聴覚が発達し、外の音が聞こえます。' },
        24: { size: '30cm',   weight: '600g',  desc: 'トウモロコシくらい。肺が発達し、まばたきもできます。' },
        28: { size: '37cm',   weight: '1000g', desc: 'ナスくらい。目の開閉ができるようになりました。' },
        32: { size: '42cm',   weight: '1700g', desc: 'カボチャくらい。骨が硬くなり、脂肪も蓄えています。' },
        36: { size: '47cm',   weight: '2500g', desc: 'メロンくらい。いつ生まれても大丈夫な状態です。' },
        40: { size: '50cm',   weight: '3200g', desc: 'スイカくらい。もうすぐ会えますね！' }
      };

      let current = growthData[8];
      for (const w of Object.keys(growthData).map(Number).sort((a,b)=>a-b)){
        if (weeks >= w) current = growthData[w];
      }
      // 産後（>40週相当）の場合は固定メッセージ
      if (weeks >= 40){
        current = growthData[40];
      }

      document.getElementById('babySize').textContent = current.size;
      document.getElementById('babyWeight').textContent = current.weight;
      document.getElementById('growthDescription').textContent = current.desc;
    }

    function updateAdvice(weeks){
      const adviceData = {
        0:  ['無理せず休息を。体調に合わせて過ごしましょう', '葉酸など必要な栄養を意識して摂りましょう'],
        8:  ['つわりのピーク時期。匂い・時間帯の工夫で軽減を', '母子手帳を受け取りましょう'],
        16: ['安定期に。適度な運動を始めましょう', '歯科検診を受けましょう', '戌の日の安産祈願を検討'],
        24: ['体重管理に気をつけましょう', '妊娠線予防ケアを開始', 'ベビー用品の準備を開始'],
        32: ['出産準備品リストを作成', '里帰り出産の場合は移動時期の検討', '産後の手続きを確認'],
        36: ['入院バッグの準備完了を', '陣痛タクシー登録', 'バースプランを話し合いましょう'],
        40: ['出産準備は万全に。焦らず体を休めましょう']
      };

      let current = adviceData[0];
      for (const w of Object.keys(adviceData).map(Number).sort((a,b)=>a-b)){
        if (weeks >= w) current = adviceData[w];
      }
      const html = current.map(t => `<li>${t}</li>`).join('');
      document.getElementById('adviceList').innerHTML = html;
    }

    // ==============================
    // チェックリスト進捗
    // ==============================
    function toggleChecklistItem(item){
      const id = item.getAttribute('data-id');
      const checked = !item.classList.contains('checked');
      item.classList.toggle('checked', checked);
      item.setAttribute('aria-checked', checked ? 'true':'false');
      saveChecklistProgress(id, checked);
    }

    function saveChecklistProgress(id, checked){
      const progress = JSON.parse(localStorage.getItem(STORAGE.CHECKLIST) || '{}');
      progress[id] = checked;
      localStorage.setItem(STORAGE.CHECKLIST, JSON.stringify(progress));
      updateChecklistProgress();
    }

    function loadChecklistProgress(){
      const progress = JSON.parse(localStorage.getItem(STORAGE.CHECKLIST) || '{}');
      document.querySelectorAll('.checklist-item-mini').forEach(item => {
        const id = item.getAttribute('data-id');
        const isChecked = !!progress[id];
        item.classList.toggle('checked', isChecked);
        item.setAttribute('aria-checked', isChecked ? 'true':'false');
      });
      updateChecklistProgress();
    }

    function updateChecklistProgress(){
      const total = document.querySelectorAll('.checklist-item-mini').length;
      const checked = document.querySelectorAll('.checklist-item-mini.checked').length;
      const pct = total > 0 ? Math.round(checked/total*100) : 0;
      const el = document.getElementById('checklistProgress');
      if (el) el.textContent = `${pct}%`;
    }

    // 進捗のエクスポート/インポート
    function exportProgress(){
      const data = {
        version: APP_VERSION,
        dueDate: localStorage.getItem(STORAGE.DUE_DATE) || null,
        checklist: JSON.parse(localStorage.getItem(STORAGE.CHECKLIST) || '{}'),
        exportedAt: new Date().toISOString()
      };
      const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `pregnancy_app_progress_${new Date().toISOString().slice(0,10)}.json`;
      a.click();
      URL.revokeObjectURL(url);
    }

    function importProgress(e){
      const file = e.target.files?.[0];
      e.target.value = '';
      if (!file) return;
      const reader = new FileReader();
      reader.onload = () => {
        try{
          const obj = JSON.parse(reader.result);
          if (obj?.dueDate) localStorage.setItem(STORAGE.DUE_DATE, obj.dueDate);
          if (obj?.checklist) localStorage.setItem(STORAGE.CHECKLIST, JSON.stringify(obj.checklist));
          if (obj?.dueDate) updateDisplay(obj.dueDate);
          loadChecklistProgress();
          alert('インポートが完了しました。');
        }catch(err){
          alert('読み込みに失敗しました。JSONファイルを確認してください。');
        }
      };
      reader.readAsText(file, 'utf-8');
    }
  </script>
</body>
</html>
