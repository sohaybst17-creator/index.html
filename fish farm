<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ماهی‌پرور | پرورش و فروش ماهی</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400;500;700;900&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --ink:      #0d1f2d;
    --deep:     #0a3d55;
    --water:    #0e6b8a;
    --ripple:   #1fa3c8;
    --foam:     #b8e8f5;
    --surface:  #e8f6fc;
    --light:    #f5fbfe;
    --gold:     #e8a930;
    --gold-lt:  #f7d47a;
    --white:    #ffffff;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Vazirmatn', sans-serif;
    background: var(--light);
    color: var(--ink);
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; right: 0; left: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 0 5vw; height: 64px;
    background: rgba(13,31,45,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(31,163,200,0.2);
  }
  .nav-logo {
    font-size: 1.3rem; font-weight: 900; color: var(--foam);
    letter-spacing: -0.5px;
  }
  .nav-logo span { color: var(--gold); }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a {
    color: rgba(255,255,255,0.75); text-decoration: none;
    font-size: 0.9rem; font-weight: 500;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--foam); }
  .nav-cta {
    background: var(--gold); color: var(--ink);
    border: none; border-radius: 6px;
    padding: 0.45rem 1.2rem; font-size: 0.85rem; font-weight: 700;
    cursor: pointer; font-family: inherit;
    transition: background 0.2s;
  }
  .nav-cta:hover { background: var(--gold-lt); }

  /* ── HERO ── */
  #hero {
    min-height: 100vh;
    background: linear-gradient(160deg, var(--ink) 0%, var(--deep) 45%, var(--water) 100%);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center;
    padding: 100px 5vw 60px;
    position: relative; overflow: hidden;
  }

  /* animated water rings */
  .rings {
    position: absolute; bottom: -60px; left: 50%; transform: translateX(-50%);
    width: 600px; height: 300px; pointer-events: none;
  }
  .ring {
    position: absolute; bottom: 0; left: 50%;
    transform: translateX(-50%);
    border-radius: 50%;
    border: 1px solid rgba(31,163,200,0.3);
    animation: expand 4s ease-out infinite;
  }
  .ring:nth-child(1) { width: 120px; height: 60px; animation-delay: 0s; }
  .ring:nth-child(2) { width: 260px; height: 130px; animation-delay: 1s; }
  .ring:nth-child(3) { width: 420px; height: 210px; animation-delay: 2s; }
  .ring:nth-child(4) { width: 580px; height: 290px; animation-delay: 3s; }
  @keyframes expand {
    0%   { opacity: 0.8; }
    100% { opacity: 0; transform: translateX(-50%) scaleX(1.15) scaleY(1.15); }
  }

  .hero-eyebrow {
    font-size: 0.8rem; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--gold); font-weight: 500; margin-bottom: 1.2rem;
  }
  .hero-title {
    font-size: clamp(2.4rem, 7vw, 5rem);
    font-weight: 900; color: var(--white); line-height: 1.15;
    margin-bottom: 1.4rem;
  }
  .hero-title em {
    font-style: normal; color: var(--ripple);
  }
  .hero-sub {
    font-size: clamp(1rem, 2.5vw, 1.25rem);
    color: rgba(255,255,255,0.65); max-width: 560px;
    line-height: 1.8; margin-bottom: 2.5rem;
  }
  .hero-btns { display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center; }
  .btn-primary {
    background: var(--gold); color: var(--ink);
    border: none; border-radius: 8px;
    padding: 0.85rem 2rem; font-size: 1rem; font-weight: 700;
    cursor: pointer; font-family: inherit;
    transition: transform 0.15s, background 0.2s;
  }
  .btn-primary:hover { background: var(--gold-lt); transform: translateY(-2px); }
  .btn-outline {
    background: transparent; color: var(--foam);
    border: 1.5px solid rgba(184,232,245,0.5); border-radius: 8px;
    padding: 0.85rem 2rem; font-size: 1rem; font-weight: 500;
    cursor: pointer; font-family: inherit;
    transition: border-color 0.2s, color 0.2s;
  }
  .btn-outline:hover { border-color: var(--foam); color: var(--white); }

  .hero-stats {
    margin-top: 4rem;
    display: flex; gap: 3rem; flex-wrap: wrap; justify-content: center;
  }
  .stat { text-align: center; }
  .stat-num { font-size: 2rem; font-weight: 900; color: var(--gold); }
  .stat-lbl { font-size: 0.8rem; color: rgba(255,255,255,0.5); margin-top: 2px; }

  /* ── SECTIONS COMMON ── */
  section { padding: 80px 5vw; }
  .section-tag {
    display: inline-block;
    font-size: 0.75rem; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--water); font-weight: 700;
    border-bottom: 2px solid var(--gold); padding-bottom: 3px;
    margin-bottom: 1rem;
  }
  .section-title {
    font-size: clamp(1.6rem, 4vw, 2.5rem);
    font-weight: 900; color: var(--ink); line-height: 1.25;
    margin-bottom: 1rem;
  }
  .section-lead {
    font-size: 1.05rem; color: #4a6070;
    max-width: 560px; line-height: 1.9;
  }

  /* ── PRODUCTS ── */
  #products { background: var(--white); }
  .products-header { margin-bottom: 3rem; }
  .product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 1.5rem;
  }
  .product-card {
    background: var(--light);
    border-radius: 12px;
    overflow: hidden;
    border: 1px solid rgba(14,107,138,0.1);
    transition: transform 0.2s, box-shadow 0.2s;
  }
  .product-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 32px rgba(14,107,138,0.15);
  }
  .product-img {
    height: 160px;
    display: flex; align-items: center; justify-content: center;
    font-size: 4rem;
    position: relative; overflow: hidden;
  }
  .product-img.carp    { background: linear-gradient(135deg,#0a3d55,#1fa3c8); }
  .product-img.fry     { background: linear-gradient(135deg,#0e6b8a,#b8e8f5); }
  .product-img.trout   { background: linear-gradient(135deg,#1c5c3e,#4caf82); }
  .product-img.tilapia { background: linear-gradient(135deg,#3d2b0a,#c88a1f); }
  .product-body { padding: 1.25rem 1.4rem 1.5rem; }
  .product-name { font-size: 1.1rem; font-weight: 700; color: var(--ink); margin-bottom: 0.4rem; }
  .product-desc { font-size: 0.875rem; color: #5a7080; line-height: 1.7; margin-bottom: 1rem; }
  .product-meta {
    display: flex; justify-content: space-between; align-items: center;
  }
  .product-price { font-size: 1rem; font-weight: 700; color: var(--water); }
  .btn-small {
    background: var(--water); color: var(--white);
    border: none; border-radius: 6px;
    padding: 0.4rem 1rem; font-size: 0.8rem; font-weight: 600;
    cursor: pointer; font-family: inherit;
    transition: background 0.2s;
  }
  .btn-small:hover { background: var(--deep); }

  /* ── ABOUT ── */
  #about {
    background: var(--surface);
    display: grid; grid-template-columns: 1fr 1fr; gap: 5rem;
    align-items: center;
  }
  .about-visual {
    background: linear-gradient(145deg, var(--deep), var(--water));
    border-radius: 16px; height: 360px;
    display: flex; align-items: center; justify-content: center;
    font-size: 6rem; position: relative; overflow: hidden;
  }
  .about-visual::after {
    content: '';
    position: absolute; inset: 0;
    background: repeating-linear-gradient(
      45deg,
      transparent,
      transparent 20px,
      rgba(255,255,255,0.03) 20px,
      rgba(255,255,255,0.03) 40px
    );
  }
  .about-features { margin-top: 2rem; display: flex; flex-direction: column; gap: 1rem; }
  .feature-row { display: flex; gap: 1rem; align-items: flex-start; }
  .feat-icon {
    width: 40px; height: 40px; border-radius: 8px;
    background: var(--foam); display: flex; align-items: center;
    justify-content: center; font-size: 1.1rem; flex-shrink: 0;
  }
  .feat-text h4 { font-size: 0.95rem; font-weight: 700; color: var(--ink); margin-bottom: 2px; }
  .feat-text p  { font-size: 0.82rem; color: #5a7080; line-height: 1.6; }

  /* ── LEARN ── */
  #learn { background: var(--white); }
  .learn-header { margin-bottom: 3rem; }
  .article-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.5rem;
  }
  .article-card {
    border: 1px solid rgba(14,107,138,0.12);
    border-radius: 12px; overflow: hidden;
    transition: box-shadow 0.2s;
  }
  .article-card:hover { box-shadow: 0 8px 24px rgba(14,107,138,0.12); }
  .article-banner {
    height: 110px; display: flex; align-items: center;
    justify-content: flex-start; padding: 0 1.5rem;
    font-size: 0.7rem; letter-spacing: 0.15em; text-transform: uppercase;
    font-weight: 700; color: rgba(255,255,255,0.7);
  }
  .ab1 { background: linear-gradient(120deg,#0a3d55,#0e6b8a); }
  .ab2 { background: linear-gradient(120deg,#1c5c3e,#2e8b57); }
  .ab3 { background: linear-gradient(120deg,#3d2b0a,#8b5e1f); }
  .ab4 { background: linear-gradient(120deg,#2d0a3d,#6b3d8a); }
  .article-body { padding: 1.2rem 1.4rem 1.5rem; }
  .article-tag {
    font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--water); font-weight: 700; margin-bottom: 0.5rem;
  }
  .article-title { font-size: 1rem; font-weight: 700; color: var(--ink); line-height: 1.5; margin-bottom: 0.5rem; }
  .article-excerpt { font-size: 0.82rem; color: #5a7080; line-height: 1.7; }
  .read-more {
    display: inline-block; margin-top: 0.8rem;
    font-size: 0.82rem; font-weight: 600; color: var(--water);
    text-decoration: none;
  }
  .read-more:hover { color: var(--deep); }

  /* ── CONTACT ── */
  #contact {
    background: linear-gradient(155deg, var(--ink) 0%, var(--deep) 60%, var(--water) 100%);
    color: var(--white);
    display: grid; grid-template-columns: 1fr 1fr; gap: 5rem;
    align-items: start;
  }
  #contact .section-title { color: var(--white); }
  #contact .section-lead { color: rgba(255,255,255,0.65); max-width: 400px; }
  .contact-info { margin-top: 2rem; display: flex; flex-direction: column; gap: 1.2rem; }
  .contact-row { display: flex; align-items: center; gap: 1rem; }
  .contact-ico {
    width: 42px; height: 42px; border-radius: 8px;
    background: rgba(31,163,200,0.2); display: flex;
    align-items: center; justify-content: center; font-size: 1.1rem;
  }
  .contact-row span { font-size: 0.9rem; color: rgba(255,255,255,0.8); }

  .contact-form { display: flex; flex-direction: column; gap: 1rem; }
  .form-field input, .form-field textarea {
    width: 100%;
    background: rgba(255,255,255,0.08);
    border: 1px solid rgba(255,255,255,0.2);
    border-radius: 8px; color: var(--white);
    font-family: inherit; font-size: 0.9rem;
    padding: 0.8rem 1rem;
    outline: none;
    transition: border-color 0.2s;
  }
  .form-field input::placeholder, .form-field textarea::placeholder {
    color: rgba(255,255,255,0.4);
  }
  .form-field input:focus, .form-field textarea:focus {
    border-color: var(--ripple);
  }
  .form-field textarea { resize: vertical; min-height: 110px; }
  .btn-send {
    background: var(--gold); color: var(--ink);
    border: none; border-radius: 8px;
    padding: 0.85rem; font-size: 1rem; font-weight: 700;
    cursor: pointer; font-family: inherit;
    transition: background 0.2s;
  }
  .btn-send:hover { background: var(--gold-lt); }

  /* ── FOOTER ── */
  footer {
    background: var(--ink);
    color: rgba(255,255,255,0.45);
    text-align: center; font-size: 0.8rem;
    padding: 1.8rem 5vw;
    border-top: 1px solid rgba(255,255,255,0.06);
  }
  footer strong { color: rgba(255,255,255,0.7); }

  /* ── SCROLL REVEAL ── */
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .reveal.visible { opacity: 1; transform: none; }

  /* ── RESPONSIVE ── */
  @media(max-width: 768px) {
    .nav-links { display: none; }
    #about, #contact { grid-template-columns: 1fr; gap: 2.5rem; }
    .about-visual { height: 220px; font-size: 4rem; }
    .hero-stats { gap: 2rem; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">ماهی<span>پرور</span></div>
  <ul class="nav-links">
    <li><a href="#products">محصولات</a></li>
    <li><a href="#about">درباره ما</a></li>
    <li><a href="#learn">آموزش</a></li>
    <li><a href="#contact">تماس</a></li>
  </ul>
  <button class="nav-cta" onclick="document.getElementById('contact').scrollIntoView({behavior:'smooth'})">سفارش دهید</button>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="rings">
    <div class="ring"></div>
    <div class="ring"></div>
    <div class="ring"></div>
    <div class="ring"></div>
  </div>
  <p class="hero-eyebrow">پرورش · فروش · آموزش</p>
  <h1 class="hero-title">از <em>بچه‌ماهی</em> تا<br>سفره‌ی شما</h1>
  <p class="hero-sub">
    عرضه‌ی بچه‌ماهی با کیفیت، ماهی پرورشی تازه و آموزش تخصصی پرورش ماهی — مستقیم از مزرعه، مریوان
  </p>
  <div class="hero-btns">
    <button class="btn-primary" onclick="document.getElementById('products').scrollIntoView({behavior:'smooth'})">مشاهده محصولات</button>
    <button class="btn-outline" onclick="document.getElementById('learn').scrollIntoView({behavior:'smooth'})">آموزش رایگان</button>
  </div>
  <div class="hero-stats">
    <div class="stat"><div class="stat-num">+۱۵</div><div class="stat-lbl">سال تجربه</div></div>
    <div class="stat"><div class="stat-num">+۵۰۰</div><div class="stat-lbl">هزار بچه‌ماهی در سال</div></div>
    <div class="stat"><div class="stat-num">+۱۰۰</div><div class="stat-lbl">مشتری فعال</div></div>
    <div class="stat"><div class="stat-num">بهترین</div><div class="stat-lbl">ضریب تبدیل غذایی FCR</div></div>
  </div>
</section>

<!-- PRODUCTS -->
<section id="products">
  <div class="products-header reveal">
    <span class="section-tag">محصولات</span>
    <h2 class="section-title">آنچه عرضه می‌کنیم</h2>
    <p class="section-lead">بچه‌ماهی سالم و ماهی تازه — همه با ضمانت کیفیت و بهداشت</p>
  </div>
  <div class="product-grid">
    <div class="product-card reveal">
      <div class="product-img carp">🐟</div>
      <div class="product-body">
        <div class="product-name">کپور معمولی پرورشی</div>
        <div class="product-desc">ماهی تازه از استخرهای پرورشی — میانگین وزن ۸۰۰ گرم تا ۲ کیلوگرم</div>
        <div class="product-meta">
          <span class="product-price">قیمت روز بازار</span>
          <button class="btn-small">استعلام</button>
        </div>
      </div>
    </div>
    <div class="product-card reveal">
      <div class="product-img fry">🐠</div>
      <div class="product-body">
        <div class="product-name">بچه‌ماهی کپور (انگشت‌قد)</div>
        <div class="product-desc">وزن ۵ تا ۵۰ گرم — مناسب استخرهای پرورشی، آمادگی بالای سازگاری</div>
        <div class="product-meta">
          <span class="product-price">فروش عمده</span>
          <button class="btn-small">استعلام</button>
        </div>
      </div>
    </div>
    <div class="product-card reveal">
      <div class="product-img trout">🎣</div>
      <div class="product-body">
        <div class="product-name">بچه‌ماهی قزل‌آلا</div>
        <div class="product-desc">نژاد رنگین‌کمان، وزن ۱۰–۸۰ گرم، واکسینه شده، مناسب آب سرد</div>
        <div class="product-meta">
          <span class="product-price">فروش عمده</span>
          <button class="btn-small">استعلام</button>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-visual">🏞️</div>
  <div>
    <span class="section-tag">درباره ما</span>
    <h2 class="section-title reveal">مزرعه‌ای که<br>به آب اعتماد دارد</h2>
    <p class="section-lead reveal">ما با بیش از یک دهه تجربه در پرورش ماهی در استخرهای پرورشی، اصول زیست‌محیطی را در کنار راندمان اقتصادی رعایت می‌کنیم.</p>
    <div class="about-features">
      <div class="feature-row reveal">
        <div class="feat-icon">🌊</div>
        <div class="feat-text">
          <h4>پرورش در استخرهای طبیعی و نیمه‌طبیعی</h4>
          <p>استفاده از آب‌های طبیعی مریوان با کنترل تراکم و کیفیت آب بصورت روزانه</p>
        </div>
      </div>
      <div class="feature-row reveal">
        <div class="feat-icon">🔬</div>
        <div class="feat-text">
          <h4>بهترین ضریب تبدیل غذایی (FCR)</h4>
          <p>پایش منظم بیومس و مدیریت دقیق تغذیه برای دستیابی به بهترین FCR ممکن</p>
        </div>
      </div>
      <div class="feature-row reveal">
        <div class="feat-icon">🚚</div>
        <div class="feat-text">
          <h4>ارسال با خودرو مخصوص حمل زنده</h4>
          <p>تانکر اکسیژن‌دار با کنترل دما — بچه‌ماهی زنده به مقصد می‌رسد</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- LEARN -->
<section id="learn">
  <div class="learn-header reveal">
    <span class="section-tag">آموزش</span>
    <h2 class="section-title">راهنمای پرورش ماهی</h2>
    <p class="section-lead">از انتخاب بچه‌ماهی تا برداشت محصول — آموزش عملی و رایگان</p>
  </div>
  <div class="article-grid">
    <div class="article-card reveal">
      <div class="article-banner ab1">تغذیه</div>
      <div class="article-body">
        <div class="article-tag">تغذیه و FCR</div>
        <div class="article-title">نرخ غذادهی کپور بر اساس دما و وزن</div>
        <div class="article-excerpt">در دمای ۲۰–۲۵ درجه، نرخ بهینه غذادهی ۲.۵–۳٪ وزن بدن در روز است. دستیابی به بهترین FCR نشانه مدیریت حرفه‌ای تغذیه است.</div>
        <a href="#" class="read-more">ادامه مطلب ←</a>
      </div>
    </div>
    <div class="article-card reveal">
      <div class="article-banner ab2">کیفیت آب</div>
      <div class="article-body">
        <div class="article-tag">مدیریت آب</div>
        <div class="article-title">پارامترهای حیاتی کیفیت آب در استخر پرورشی</div>
        <div class="article-excerpt">اکسیژن محلول بالای ۵ mg/L، pH بین ۷–۸.۵، آمونیاک زیر ۰.۰۲ mg/L — این سه پارامتر را هر هفته بسنجید.</div>
        <a href="#" class="read-more">ادامه مطلب ←</a>
      </div>
    </div>
    <div class="article-card reveal">
      <div class="article-banner ab3">بهداشت</div>
      <div class="article-body">
        <div class="article-tag">بیماری و درمان</div>
        <div class="article-title">شناخت و پیشگیری از بیماری KHV در کپور</div>
        <div class="article-excerpt">ویروس هرپس کپور (KHV) در دمای ۱۸–۲۸ درجه فعال است. علائم: زخم آبشش، کاهش اشتها، تلفات سریع.</div>
        <a href="#" class="read-more">ادامه مطلب ←</a>
      </div>
    </div>
    <div class="article-card reveal">
      <div class="article-banner ab4">اقتصاد</div>
      <div class="article-body">
        <div class="article-tag">تحلیل بازار</div>
        <div class="article-title">تحلیل قیمت کپور در بازار عراق ۲۰۲۵</div>
        <div class="article-excerpt">با کاهش عرضه ناشی از KHV و بحران آب، قیمت کپور در بازار عراق روند صعودی داشته است. پیش‌بینی پاییز ۲۰۲۶...</div>
        <a href="#" class="read-more">ادامه مطلب ←</a>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div>
    <span class="section-tag" style="color:var(--gold);border-color:var(--gold)">تماس</span>
    <h2 class="section-title reveal">سفارش یا مشاوره؟<br>بنویسید</h2>
    <p class="section-lead reveal">برای خرید عمده بچه‌ماهی، ماهی تازه یا مشاوره راه‌اندازی مزرعه، با ما در تماس باشید.</p>
    <div class="contact-info">
      <div class="contact-row reveal">
        <div class="contact-ico">📞</div>
        <span>۰۹۱۴ × × × × × × ×</span>
      </div>
      <div class="contact-row reveal">
        <div class="contact-ico">📍</div>
        <span>مریوان — کردستان، ایران</span>
      </div>
      <div class="contact-row reveal">
        <div class="contact-ico">📺</div>
        <span>YouTube: @fish.world66</span>
      </div>
    </div>
  </div>
  <div class="contact-form reveal">
    <div class="form-field"><input type="text" placeholder="نام شما"></div>
    <div class="form-field"><input type="tel" placeholder="شماره تلفن / واتس‌اپ"></div>
    <div class="form-field"><input type="text" placeholder="موضوع (بچه‌ماهی / ماهی تازه / مشاوره)"></div>
    <div class="form-field"><textarea placeholder="پیام شما..."></textarea></div>
    <button class="btn-send">ارسال پیام ✓</button>
  </div>
</section>

<footer>
  <strong>ماهی‌پرور</strong> — پرورش و فروش ماهی · مریوان، کردستان ایران · ساخته‌شده با ❤️ برای آبزی‌پروران
</footer>

<script>
  // scroll reveal
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.12 });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // contact form mock
  document.querySelector('.btn-send').addEventListener('click', () => {
    const btn = document.querySelector('.btn-send');
    btn.textContent = '✅ پیام ارسال شد';
    btn.style.background = '#4caf82';
    setTimeout(() => {
      btn.textContent = 'ارسال پیام ✓';
      btn.style.background = '';
    }, 3000);
  });
</script>
</body>
</html>

