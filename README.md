<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Safety Bot - بوت الأمان</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
  /* Reset & Performance Optimizations */
  *, *::before, *::after { 
    box-sizing: border-box; 
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  
  body { 
    margin:0; padding:0; 
    font-family: 'Cairo', Arial, sans-serif; 
    background: linear-gradient(135deg, #0f0f0f, #1a1a1a, #0f0f0f);
    color:#eee; 
    min-height:100vh; 
    display:flex; 
    flex-direction:column;
    overflow-x: hidden;
    position: relative;
  }
  
  /* Subtle Background */
  body::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: 
      radial-gradient(circle at 20% 80%, rgba(76, 175, 80, 0.08) 0%, transparent 50%),
      radial-gradient(circle at 80% 20%, rgba(76, 175, 80, 0.05) 0%, transparent 50%);
    z-index: -1;
  }
  
  /* Simple Particles */
  body::after {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: 
      radial-gradient(2px 2px at 20px 30px, rgba(76, 175, 80, 0.3), transparent),
      radial-gradient(1px 1px at 40px 70px, rgba(76, 175, 80, 0.2), transparent),
      radial-gradient(1px 1px at 90px 40px, rgba(76, 175, 80, 0.4), transparent);
    background-repeat: repeat;
    background-size: 200px 200px;
    z-index: -1;
  }
  
  /* Links */
  a { 
    color:#4caf50; 
    text-decoration:none; 
    transition: all 0.3s ease;
  }
  a:hover, a:focus { 
    text-decoration:underline; 
    filter: brightness(1.2);
    transform: translateY(-1px);
  }
  /* Header */
  header { 
    background: linear-gradient(135deg, rgba(34, 34, 34, 0.95), rgba(20, 20, 20, 0.95));
    backdrop-filter: blur(10px);
    padding:1rem 2rem; 
    display:flex; 
    justify-content:space-between; 
    align-items:center; 
    position:fixed; 
    width:100%; 
    top:0; 
    left:0; 
    z-index:1000; 
    box-shadow: 
      0 4px 20px rgba(0,0,0,0.3),
      0 0 0 1px rgba(76, 175, 80, 0.1);
    transition: all 0.3s ease;
    border-bottom: 1px solid rgba(76, 175, 80, 0.1);
  }
  
  header:hover {
    box-shadow: 
      0 6px 25px rgba(0,0,0,0.4),
      0 0 0 1px rgba(76, 175, 80, 0.2);
    transform: translateY(-1px);
  }
  
  header .logo { 
    display:flex; 
    align-items:center; 
    gap:0.75rem; 
  }
  
  header .logo img { 
    width:50px; 
    height:50px; 
    animation: rotate 30s linear infinite; 
    filter: drop-shadow(0 0 10px #4caf50);
    transition: all 0.3s ease;
    border-radius: 50%;
  }
  
  header .logo img:hover {
    transform: scale(1.1);
    filter: drop-shadow(0 0 15px #4caf50);
  }
  
  header .logo h1 { 
    font-size:1.5rem; 
    color:#4caf50; 
    margin:0; 
    text-shadow: 0 0 10px rgba(76, 175, 80, 0.5);
    background: linear-gradient(45deg, #4caf50, #81c784);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    transition: all 0.3s ease;
  }
  
  header .logo h1:hover {
    transform: scale(1.05);
  }
  
  .lang-toggle { 
    background: linear-gradient(135deg, #4caf50, #388e3c);
    border:none; 
    border-radius:25px; 
    padding:0.5rem 1rem; 
    color:white; 
    font-weight:700; 
    cursor:pointer; 
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(76, 175, 80, 0.3);
  }
  
  .lang-toggle::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
    transition: left 0.5s ease;
  }
  
  .lang-toggle:hover::before {
    left: 100%;
  }
  
  .lang-toggle:hover, .lang-toggle:focus { 
    background: linear-gradient(135deg, #388e3c, #2e7d32);
    transform: translateY(-3px) scale(1.05);
    box-shadow: 0 6px 20px rgba(76, 175, 80, 0.4);
    outline:none; 
  }
  main { 
    flex:1; 
    padding:6rem 2rem 3rem; 
    max-width:900px; 
    margin:0 auto; 
    width:100%; 
  }
  
  /* Intro Section */
  .intro { 
    text-align:center; 
    margin-bottom:3rem; 
    opacity:0; 
    transform: translateY(30px);
    transition: all 0.8s ease;
  }
  
  .intro.visible { 
    opacity:1; 
    transform: translateY(0);
  }
  
  .intro h2 { 
    font-size:2.5rem; 
    color:#4caf50; 
    margin-bottom:0.5rem; 
    text-shadow: 0 0 15px rgba(76, 175, 80, 0.5);
    background: linear-gradient(45deg, #4caf50, #81c784, #4caf50);
    background-size: 200% 200%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: gradientText 3s ease infinite;
    transition: all 0.3s ease;
  }
  
  .intro h2:hover {
    transform: scale(1.05);
  }
  
  .intro p { 
    font-size:1.25rem; 
    color:#a5d6a7; 
    max-width:600px; 
    margin:0 auto; 
    text-shadow: 0 2px 10px rgba(0,0,0,0.3);
    transition: all 0.3s ease;
  }
  
  .intro p:hover {
    color: #c8e6c9;
  }
  
  .btn-group { 
    margin-top:2rem; 
    display:flex; 
    justify-content:center; 
    gap:1rem; 
    flex-wrap:wrap; 
  }
  
  .btn { 
    background: linear-gradient(135deg, #4caf50, #388e3c);
    color:white; 
    padding:0.75rem 2rem; 
    border-radius:30px; 
    font-weight:700; 
    font-size:1.1rem; 
    box-shadow: 
      0 6px 20px rgba(76, 175, 80, 0.3),
      0 0 0 1px rgba(76, 175, 80, 0.1);
    transition: all 0.3s ease; 
    user-select:none; 
    text-align:center; 
    display:inline-block;
    position: relative;
    overflow: hidden;
  }
  
  .btn::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
    transition: left 0.5s ease;
  }
  
  .btn:hover::before {
    left: 100%;
  }
  
  .btn:hover, .btn:focus { 
    background: linear-gradient(135deg, #388e3c, #2e7d32);
    transform: translateY(-6px) scale(1.05);
    box-shadow: 
      0 10px 25px rgba(76, 175, 80, 0.4),
      0 0 0 1px rgba(76, 175, 80, 0.2);
    outline:none; 
  }
  /* Features Section */
  section.features { 
    display:grid; 
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); 
    gap:2rem; 
    margin-bottom:3rem; 
    opacity:0; 
    transform: translateY(30px);
    transition: all 0.8s ease;
  }
  
  section.features.visible { 
    opacity:1; 
    transform: translateY(0);
  }
  
  .feature-card { 
    background: linear-gradient(135deg, rgba(34, 34, 34, 0.9), rgba(20, 20, 20, 0.9));
    backdrop-filter: blur(10px);
    border-radius:20px; 
    padding:1.5rem; 
    box-shadow: 
      0 8px 25px rgba(0,0,0,0.3),
      0 0 0 1px rgba(76, 175, 80, 0.1);
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  
  .feature-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, rgba(76, 175, 80, 0.05), transparent);
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  .feature-card:hover::before {
    opacity: 1;
  }
  
  .feature-card:hover, .feature-card:focus-within { 
    transform: translateY(-10px) scale(1.02);
    box-shadow: 
      0 15px 35px rgba(0,0,0,0.4),
      0 0 0 1px rgba(76, 175, 80, 0.2);
  }
  
  .feature-icon { 
    font-size:2.5rem; 
    color:#4caf50; 
    margin-bottom:1rem; 
    display: inline-block;
    transition: all 0.3s ease;
    text-shadow: 0 0 15px rgba(76, 175, 80, 0.5);
  }
  
  .feature-card:hover .feature-icon {
    transform: scale(1.2) rotate(5deg);
    filter: drop-shadow(0 0 20px #4caf50);
  }
  
  .feature-title { 
    font-weight:700; 
    font-size:1.3rem; 
    margin-bottom:0.5rem; 
    color: #4caf50;
    text-shadow: 0 2px 10px rgba(0,0,0,0.3);
    transition: all 0.3s ease;
  }
  
  .feature-card:hover .feature-title {
    text-shadow: 0 2px 15px rgba(0,0,0,0.4);
  }
  
  .feature-desc { 
    color:#a5d6a7; 
    font-size:1rem; 
    line-height:1.4; 
    text-shadow: 0 1px 5px rgba(0,0,0,0.3);
    transition: all 0.3s ease;
  }
  
  .feature-card:hover .feature-desc {
    color: #c8e6c9;
  }
  /* Bot Status */
  section.bot-status { 
    background: linear-gradient(135deg, rgba(34, 34, 34, 0.9), rgba(20, 20, 20, 0.9));
    backdrop-filter: blur(15px);
    border-radius:20px; 
    padding:1.5rem; 
    max-width:400px; 
    margin:0 auto 3rem; 
    text-align:center; 
    box-shadow: 
      0 10px 30px rgba(0,0,0,0.3),
      0 0 0 1px rgba(76, 175, 80, 0.1);
    opacity:0; 
    transform: translateY(30px);
    transition: all 0.8s ease;
    position: relative;
    overflow: hidden;
  }
  
  section.bot-status::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: conic-gradient(from 0deg, transparent, rgba(76, 175, 80, 0.1), transparent);
    animation: rotate 10s linear infinite;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  section.bot-status:hover::before {
    opacity: 1;
  }
  
  section.bot-status.visible { 
    opacity:1; 
    transform: translateY(0);
  }
  
  section.bot-status:hover {
    transform: translateY(-5px) scale(1.02);
  }
  
  section.bot-status h3 { 
    color:#4caf50; 
    margin-bottom:1rem; 
    text-shadow: 0 0 15px rgba(76, 175, 80, 0.5);
  }
  
  #botStatus, #botUptime, #botServers, #botUsers { 
    font-size:1.1rem; 
    color:#a5d6a7; 
    margin:0.5rem 0; 
    text-shadow: 0 1px 5px rgba(0,0,0,0.3);
  }
  
  /* FAQ Accordion */
  section.faq { 
    max-width:700px; 
    margin:0 auto 3rem; 
    opacity:0; 
    transform: translateY(30px);
    transition: all 0.8s ease;
  }
  
  section.faq.visible { 
    opacity:1; 
    transform: translateY(0);
  }
  
  section.faq h3 { 
    text-align:center; 
    font-size:2rem; 
    color:#4caf50; 
    margin-bottom:1.5rem; 
  }
  
  .faq-item { 
    background: linear-gradient(135deg, rgba(34, 34, 34, 0.9), rgba(20, 20, 20, 0.9));
    backdrop-filter: blur(10px);
    border-radius:15px; 
    margin-bottom:1rem; 
    overflow:hidden; 
    box-shadow: 
      0 6px 20px rgba(0,0,0,0.3),
      0 0 0 1px rgba(76, 175, 80, 0.1);
    transition: all 0.3s ease;
  }
  
  .faq-item:hover {
    transform: translateY(-3px);
    box-shadow: 
      0 8px 25px rgba(0,0,0,0.4),
      0 0 0 1px rgba(76, 175, 80, 0.2);
  }
  
  .faq-question { 
    padding:1rem 1.5rem; 
    cursor:pointer; 
    font-weight:700; 
    font-size:1.1rem; 
    color:#4caf50; 
    user-select:none; 
    position:relative; 
    border:none; 
    width:100%; 
    text-align:right; 
    background:transparent; 
    transition: all 0.3s ease;
    text-shadow: 0 1px 5px rgba(0,0,0,0.3);
  }
  
  .faq-question:hover {
    color: #81c784;
    text-shadow: 0 0 10px rgba(76, 175, 80, 0.5);
  }
  
  .faq-question::after { 
    content:'+'; 
    position:absolute; 
    left:1.5rem; 
    font-size:1.5rem; 
    transition: all 0.3s ease; 
  }
  
  .faq-item.open .faq-question::after { 
    content:'-'; 
    transform: rotate(180deg);
  }
  
  .faq-answer { 
    max-height:0; 
    overflow:hidden; 
    padding:0 1.5rem; 
    color:#a5d6a7; 
    font-size:1rem; 
    line-height:1.5; 
    transition: all 0.4s ease; 
    text-align:right; 
    text-shadow: 0 1px 5px rgba(0,0,0,0.3);
  }
  
  .faq-item.open .faq-answer { 
    max-height:200px; 
    padding:1rem 1.5rem; 
  }
  /* Testimonials */
  section.testimonials { 
    background: linear-gradient(135deg, rgba(34, 34, 34, 0.9), rgba(20, 20, 20, 0.9));
    backdrop-filter: blur(15px);
    border-radius:20px; 
    padding:2rem; 
    max-width:700px; 
    margin:0 auto 3rem; 
    box-shadow: 
      0 10px 30px rgba(0,0,0,0.3),
      0 0 0 1px rgba(76, 175, 80, 0.1);
    opacity:0; 
    transform: translateY(30px);
    transition: all 0.8s ease;
  }
  
  section.testimonials.visible { 
    opacity:1; 
    transform: translateY(0);
  }
  
  section.testimonials:hover {
    transform: translateY(-5px) scale(1.01);
  }
  
  section.testimonials h3 { 
    text-align:center; 
    color:#4caf50; 
    margin-bottom:1.5rem; 
    text-shadow: 0 0 15px rgba(76, 175, 80, 0.5);
  }
  
  .testimonial { 
    text-align:center; 
    font-style:italic; 
    color:#a5d6a7; 
    font-size:1.1rem; 
    margin-bottom:1rem; 
    text-shadow: 0 1px 5px rgba(0,0,0,0.3);
    transition: all 0.3s ease;
  }
  
  .testimonial:hover {
    transform: scale(1.02);
    color: #c8e6c9;
  }
  
  .testimonial-author { 
    margin-top:0.5rem; 
    font-weight:700; 
    color:#4caf50; 
    text-shadow: 0 0 10px rgba(76, 175, 80, 0.5);
  }
  
  /* Developers Section */
  section.developers { 
    max-width:900px; 
    margin:0 auto 3rem; 
    padding:0 1rem; 
    opacity:0; 
    transform: translateY(30px);
    transition: all 0.8s ease;
  }
  
  section.developers.visible { 
    opacity:1; 
    transform: translateY(0);
  }
  
  section.developers h3 { 
    text-align:center; 
    font-size:2rem; 
    color:#4caf50; 
    margin-bottom:2rem; 
  }
  
  .dev-grid { 
    display:grid; 
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); 
    gap:2rem; 
  }
  
  .dev-card { 
    background: linear-gradient(135deg, rgba(34, 34, 34, 0.9), rgba(20, 20, 20, 0.9));
    backdrop-filter: blur(10px);
    border-radius:20px; 
    padding:1.5rem; 
    box-shadow: 
      0 8px 25px rgba(0,0,0,0.3),
      0 0 0 1px rgba(76, 175, 80, 0.1);
    text-align:center; 
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  
  .dev-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, rgba(76, 175, 80, 0.05), transparent);
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  .dev-card:hover::before {
    opacity: 1;
  }
  
  .dev-card:hover, .dev-card:focus-within { 
    transform: translateY(-10px) scale(1.02);
    box-shadow: 
      0 15px 35px rgba(0,0,0,0.4),
      0 0 0 1px rgba(76, 175, 80, 0.2);
  }
  
  .dev-photo { 
    width:100px; 
    height:100px; 
    border-radius:50%; 
    object-fit:cover; 
    margin-bottom:1rem; 
    border:3px solid #4caf50;
    transition: all 0.3s ease;
    box-shadow: 0 0 20px rgba(76, 175, 80, 0.3);
  }
  
  .dev-card:hover .dev-photo {
    transform: scale(1.1);
    box-shadow: 0 0 30px rgba(76, 175, 80, 0.5);
  }
  
  .dev-name { 
    font-weight:700; 
    font-size:1.2rem; 
    margin-bottom:0.3rem; 
    color: #4caf50;
    text-shadow: 0 0 10px rgba(76, 175, 80, 0.5);
  }
  
  .dev-role { 
    color:#a5d6a7; 
    font-size:1rem; 
    margin-bottom:0.5rem; 
    text-shadow: 0 1px 5px rgba(0,0,0,0.3);
  }
  
  .dev-social a { 
    margin:0 0.5rem; 
    color:#4caf50; 
    font-size:1.3rem; 
    transition: all 0.3s ease; 
    display: inline-block;
  }
  
  .dev-social a:hover, .dev-social a:focus { 
    color:#81c784; 
    transform: scale(1.2);
    text-shadow: 0 0 15px rgba(76, 175, 80, 0.7);
    outline:none; 
  }
  /* Footer */
  footer { 
    background: linear-gradient(135deg, #111, #0a0a0a);
    color:#666; 
    text-align:center; 
    padding:1rem 2rem; 
    font-size:0.9rem; 
    user-select:none; 
    box-shadow: 0 -5px 20px rgba(0,0,0,0.3);
  }
  
  footer a { 
    color:#4caf50; 
    margin:0 0.5rem; 
    transition: all 0.3s ease;
  }
  
  footer a:hover, footer a:focus { 
    color:#81c784; 
    text-shadow: 0 0 10px rgba(76, 175, 80, 0.5);
    outline:none; 
  }
  
  /* Advanced Animations */
  @keyframes rotate { 
    from { transform: rotate(0deg); } 
    to { transform: rotate(360deg); } 
  }
  
  @keyframes gradientShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  @keyframes gradientText {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  @keyframes float {
    0%, 100% { transform: translateY(0px) rotate(0deg); }
    50% { transform: translateY(-20px) rotate(180deg); }
  }
  
  @keyframes sparkle {
    0% { transform: translateY(0px); }
    100% { transform: translateY(-100vh); }
  }
  
  
  /* Responsive Design */
  @media (max-width:768px) { 
    .feature-card { padding:1rem; } 
    .intro h2 { font-size:2rem; }
    .btn-group { gap: 0.5rem; }
    .btn { padding: 0.6rem 1.5rem; font-size: 1rem; }
  }
  
  @media (max-width:480px) {
    .intro h2 { font-size:1.8rem; }
    .feature-card, .dev-card { padding: 1rem; }
    header { padding: 0.8rem 1rem; }
    main { padding: 5rem 1rem 2rem; }
  }
</style>
</head>
<body>

<header>
  <div class="logo" aria-label="Safety Bot Logo">
    <img src="https://i.ibb.co/Hq8V39j/image.png" alt="" aria-hidden="true" />
    <h1 data-lang-ar="بوت الأمان" data-lang-en="Safety Bot">بوت الأمان</h1>
  </div>
  <button class="lang-toggle" aria-pressed="false" aria-label="Toggle language" id="langToggle">English</button>
</header>

<main>
  <!-- Intro Section -->
  <section class="intro" aria-live="polite" aria-atomic="true">
    <h2 id="welcome" data-lang-ar="مرحبًا بك في بوت الأمان" data-lang-en="Welcome to Safety Bot">مرحبًا بك في بوت الأمان</h2>
    <p id="description" data-lang-ar="حماية متطورة وإدارة فعالة لسيرفر الديسكورد الخاص بك" data-lang-en="Advanced protection and management for your Discord server">حماية متطورة وإدارة فعالة لسيرفر الديسكورد الخاص بك</p>
    <div class="btn-group">
      <a href="/auth/discord" class="btn" role="button" tabindex="0" data-lang-ar="تسجيل الدخول باستخدام ديسكورد" data-lang-en="Login with Discord">تسجيل الدخول باستخدام ديسكورد</a>
      <a href="https://discord.com/api/oauth2/authorize?client_id=1413605227675910194&permissions=8&scope=bot%20applications.commands" class="btn" role="button" tabindex="0" target="_blank" rel="noopener noreferrer" data-lang-ar="دعوة البوت إلى سيرفرك" data-lang-en="Invite Bot to Server">دعوة البوت إلى سيرفرك</a>
    </div>
  </section>

  <!-- Features Section -->
  <section class="features" aria-label="Bot features">
    <article class="feature-card" tabindex="0">
      <div class="feature-icon" aria-hidden="true">🛡️</div>
      <h3 data-lang-ar="حماية ضد الرسائل المزعجة والروابط الضارة" data-lang-en="Protection against spam and malicious links">حماية ضد الرسائل المزعجة والروابط الضارة</h3>
      <p data-lang-ar="نظام متطور لمنع الرسائل غير المرغوب فيها والروابط التي قد تضر بسيرفرك." data-lang-en="Advanced system to block spam messages and harmful links.">نظام متطور لمنع الرسائل غير المرغوب فيها والروابط التي قد تضر بسيرفرك.</p>
    </article>
    <article class="feature-card" tabindex="0">
      <div class="feature-icon" aria-hidden="true">⚠️</div>
      <h3 data-lang-ar="نظام تحذير وحظر متقدم" data-lang-en="Advanced warning and ban system">نظام تحذير وحظر متقدم</h3>
      <p data-lang-ar="إدارة سهلة للتحذيرات والحظر لضمان بيئة آمنة لجميع الأعضاء." data-lang-en="Easy management of warnings and bans to ensure a safe environment.">إدارة سهلة للتحذيرات والحظر لضمان بيئة آمنة لجميع الأعضاء.</p>
    </article>
    <article class="feature-card" tabindex="0">
      <div class="feature-icon" aria-hidden="true">🖥️</div>
      <h3 data-lang-ar="لوحة تحكم سهلة الاستخدام" data-lang-en="Easy-to-use control panel">لوحة تحكم سهلة الاستخدام</h3>
      <p data-lang-ar="واجهة مستخدم بسيطة تتيح لك التحكم الكامل في إعدادات البوت." data-lang-en="Simple interface allowing full control over bot settings.">واجهة مستخدم بسيطة تتيح لك التحكم الكامل في إعدادات البوت.</p>
    </article>
    <article class="feature-card" tabindex="0">
      <div class="feature-icon" aria-hidden="true">⚙️</div>
      <h3 data-lang-ar="تخصيص كامل لإعدادات الأمان" data-lang-en="Full customization of security settings">تخصيص كامل لإعدادات الأمان</h3>
      <p data-lang-ar="يمكنك ضبط كل خاصية لتناسب احتياجات سيرفرك بدقة." data-lang-en="You can adjust every feature to fit your server's needs precisely.">يمكنك ضبط كل خاصية لتناسب احتياجات سيرفرك بدقة.</p>
    </article>
    <article class="feature-card" tabindex="0">
      <div class="feature-icon" aria-hidden="true">🚫</div>
      <h3 data-lang-ar="حماية ضد عمليات الاحتيال" data-lang-en="Protection against scams">حماية ضد عمليات الاحتيال</h3>
      <p data-lang-ar="كشف ومنع محاولات الاحتيال لضمان سلامة الأعضاء." data-lang-en="Detecting and preventing scam attempts to ensure members’ safety.">كشف ومنع محاولات الاحتيال لضمان سلامة الأعضاء.</p>
    </article>
    <article class="feature-card" tabindex="0">
      <div class="feature-icon" aria-hidden="true">🛡️</div>
      <h3 data-lang-ar="حماية ضد هجمات الاختراق الجماعي" data-lang-en="Protection against mass hacking attacks">حماية ضد هجمات الاختراق الجماعي</h3>
      <p data-lang-ar="آليات متقدمة لمنع الهجمات الجماعية وحماية سيرفرك." data-lang-en="Advanced mechanisms to prevent mass attacks and protect your server.">آليات متقدمة لمنع الهجمات الجماعية وحماية سيرفرك.</p>
    </article>
  </section>

  <!-- Bot Status Section -->
  <section class="bot-status" aria-label="Bot status">
    <h3 data-lang-ar="حالة البوت" data-lang-en="Bot Status">حالة البوت</h3>
    <img id="botIcon" src="https://i.ibb.co/Hq8V39j/image.png" alt="بوت الأمان" style="width:120px; height:120px; border-radius:50%; border:4px solid #4caf50; margin-bottom:1rem; transition:transform 0.5s ease;">
    <div id="botStatus">...</div>
    <div id="botUptime">...</div>
    <div id="botServers">...</div>
    <div id="botUsers">...</div>
  </section>
  <!-- FAQ Section -->
  <section class="faq" aria-label="Frequently Asked Questions">
    <h3 data-lang-ar="الأسئلة الشائعة" data-lang-en="Frequently Asked Questions">الأسئلة الشائعة</h3>
    <div class="faq-item">
      <button class="faq-question" aria-expanded="false" aria-controls="faq1" id="faq1-btn" data-lang-ar="كيف يمكنني دعوة البوت إلى سيرفري؟" data-lang-en="How can I invite the bot to my server?">كيف يمكنني دعوة البوت إلى سيرفري؟</button>
      <div class="faq-answer" id="faq1" role="region" aria-labelledby="faq1-btn" hidden data-lang-ar="يمكنك استخدام رابط الدعوة الموجود في الصفحة أو من خلال لوحة التحكم الخاصة بالبوت." data-lang-en="You can use the invite link on the page or through the bot control panel.">يمكنك استخدام رابط الدعوة الموجود في الصفحة أو من خلال لوحة التحكم الخاصة بالبوت.</div>
    </div>
    <div class="faq-item">
      <button class="faq-question" aria-expanded="false" aria-controls="faq2" id="faq2-btn" data-lang-ar="هل البوت مجاني للاستخدام؟" data-lang-en="Is the bot free to use?">هل البوت مجاني للاستخدام؟</button>
      <div class="faq-answer" id="faq2" role="region" aria-labelledby="faq2-btn" hidden data-lang-ar="نعم، البوت مجاني مع بعض الميزات المدفوعة القادمة في المستقبل." data-lang-en="Yes, the bot is free with some premium features coming in the future.">نعم، البوت مجاني مع بعض الميزات المدفوعة القادمة في المستقبل.</div>
    </div>
    <div class="faq-item">
      <button class="faq-question" aria-expanded="false" aria-controls="faq3" id="faq3-btn" data-lang-ar="كيف يمكنني التواصل مع الدعم؟" data-lang-en="How can I contact support?">كيف يمكنني التواصل مع الدعم؟</button>
      <div class="faq-answer" id="faq3" role="region" aria-labelledby="faq3-btn" hidden data-lang-ar="يمكنك التواصل معنا عبر البريد الإلكتروني أو من خلال سيرفر الديسكورد الخاص بنا." data-lang-en="You can contact us via email or through our Discord server.">يمكنك التواصل معنا عبر البريد الإلكتروني أو من خلال سيرفر الديسكورد الخاص بنا.</div>
    </div>
  </section>

  <!-- Testimonials Section -->
  <section class="testimonials" aria-label="User testimonials">
    <h3 data-lang-ar="ماذا يقول المستخدمون" data-lang-en="What users say">ماذا يقول المستخدمون</h3>
    <blockquote class="testimonial" tabindex="0" data-lang-ar="بوت الأمان ساعدني كثيرًا في حماية سيرفري من الرسائل المزعجة والهجمات." data-lang-en="Safety Bot helped me a lot in protecting my server from spam and attacks.">بوت الأمان ساعدني كثيرًا في حماية سيرفري من الرسائل المزعجة والهجمات.
      <footer class="testimonial-author">- أحمد</footer>
    </blockquote>
    <blockquote class="testimonial" tabindex="0" data-lang-ar="لوحة التحكم سهلة الاستخدام والميزات متقدمة جدًا." data-lang-en="The control panel is easy to use and the features are very advanced.">لوحة التحكم سهلة الاستخدام والميزات متقدمة جدًا.
      <footer class="testimonial-author">- سارة</footer>
    </blockquote>
    <blockquote class="testimonial" tabindex="0" data-lang-ar="أنصح الجميع باستخدام بوت الأمان للحفاظ على سيرفر ديسكورد آمن." data-lang-en="I recommend everyone to use Safety Bot to keep their Discord server safe.">أنصح الجميع باستخدام بوت الأمان للحفاظ على سيرفر ديسكورد آمن.
      <footer class="testimonial-author">- محمد</footer>
    </blockquote>
  </section>

  <!-- Developers Section -->
  <section class="developers" aria-label="Developers">
    <h3 data-lang-ar="المطورون" data-lang-en="Developers">المطورون</h3>
    <div class="dev-grid">
      <article class="dev-card" tabindex="0">
        <img src="https://i.postimg.cc/9fH9dN1w/download.jpg" alt="صورة المطور أحمد" class="dev-photo" />
        <h4 class="dev-name">Apoca</h4>
        <p class="dev-role" data-lang-ar="المطور الرئيسي" data-lang-en="Lead Developer">المطور الرئيسي</p>
        <div class="dev-social" aria-label="روابط ابوكا علي الاجتماعية">
          <a href="https://discord.gg/bUhr3CYGn3" target="_blank" rel="noopener noreferrer" class="btn-social discord" aria-label="Discord">
            <i class="fa-brands fa-discord"></i> Discord
          </a>
          <a href="https://github.com/apocadev" target="_blank" rel="noopener noreferrer" class="btn-social github" aria-label="GitHub">
            <i class="fa-brands fa-github"></i> GitHub
          </a>
        </div>
      </article>
    </div>
  </section>

</main>

<!-- Footer -->
<footer>
  &copy; 2025 بوت الأمان. كل الحقوق محفوظة.
  <a href="#" data-lang-ar="سياسة الخصوصية" data-lang-en="Privacy Policy">سياسة الخصوصية</a> |
  <a href="#" data-lang-ar="الشروط والأحكام" data-lang-en="Terms & Conditions">الشروط والأحكام</a>
</footer>

<script>
  // FAQ Accordion
  document.querySelectorAll('.faq-question').forEach(btn => {
    btn.addEventListener('click', () => {
      const item = btn.parentElement;
      const open = item.classList.toggle('open');
      btn.setAttribute('aria-expanded', open);
      const answer = item.querySelector('.faq-answer');
      if(open) answer.removeAttribute('hidden'); else answer.setAttribute('hidden','');
    });
  });

  // Scroll Animations
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if(entry.isIntersecting) entry.target.classList.add('visible');
    });
  }, { threshold: 0.2 });
  document.querySelectorAll('.intro, .features, .faq, .testimonials, .developers, .bot-status').forEach(el => observer.observe(el));

  // Language Toggle
  const langBtn = document.getElementById('langToggle');
  let arabic = true;
  langBtn.addEventListener('click', () => {
    arabic = !arabic;
    document.querySelectorAll('[data-lang-ar]').forEach(el => {
      el.textContent = arabic ? el.getAttribute('data-lang-ar') : el.getAttribute('data-lang-en');
    });
    langBtn.textContent = arabic ? 'English' : 'العربية';
    document.documentElement.dir = arabic ? 'rtl' : 'ltr';
    document.documentElement.lang = arabic ? 'ar' : 'en';
  });

  // Bot Status Update
  async function updateBotStatus() {
    const statusEl = document.getElementById('botStatus');
    const uptimeEl = document.getElementById('botUptime');
    const serversEl = document.getElementById('botServers');
    const usersEl = document.getElementById('botUsers');
    const iconEl = document.getElementById('botIcon');
    const botSection = document.querySelector('.bot-status');

    try {
      const res = await fetch('/api/bot-status');
      const data = await res.json();

      statusEl.innerHTML = `<i class="fas ${data.online ? 'fa-circle' : 'fa-circle offline'}"></i>
                            <span>الحالة: ${data.online ? 'متصل ✅' : 'غير متصل ❌'}</span>`;
      uptimeEl.innerHTML = `<i class="fas fa-clock"></i> <span>مدة التشغيل: ${data.uptime}</span>`;
      serversEl.innerHTML = `<i class="fas fa-server"></i> <span>عدد السيرفرات: ${data.servers}</span>`;
      usersEl.innerHTML = `<i class="fas fa-users"></i> <span>عدد المستخدمين: ${data.users || 'جارٍ الحساب...'}</span>`;

      if(data.icon) iconEl.src = data.icon;
      iconEl.style.transform = 'scale(1.05)';
      setTimeout(()=>{ iconEl.style.transform='scale(1)'; },500);
      botSection.style.border = `4px solid ${data.online ? '#4caf50' : '#f44336'}`;

    } catch {
      statusEl.innerHTML = `<i class="fas fa-exclamation-triangle offline"></i><span>خطأ في جلب الحالة</span>`;
      uptimeEl.innerHTML = '';
      serversEl.innerHTML = '';
      usersEl.innerHTML = '';
      botSection.style.border = '4px solid #f44336';
    }
  }

  setInterval(updateBotStatus, 2000);
  window.addEventListener('load', updateBotStatus);
</script>
</body>
</html>
