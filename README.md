<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Piru Fashion</title>
<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,wght@0,400;0,600;0,900;1,400;1,600&family=Jost:wght@200;300;400;500&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg: #f9f4ef;
    --ink: #1a1410;
    --warm: #d4a574;
    --terracotta: #c4623a;
    --sand: #e8d5c0;
    --muted: #9c8878;
    --card-bg: #ffffff;
    --shadow: rgba(100,60,30,0.12);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--ink);
    font-family: 'Jost', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Grain overlay */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 100;
    opacity: 0.035;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='g'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23g)'/%3E%3C/svg%3E");
    background-size: 180px;
  }

  /* Decorative blobs */
  .blob {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
  }
  .blob-1 {
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(212,165,116,0.25) 0%, transparent 70%);
    top: -150px; right: -150px;
  }
  .blob-2 {
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(196,98,58,0.15) 0%, transparent 70%);
    bottom: 50px; left: -120px;
  }
  .blob-3 {
    width: 300px; height: 300px;
    background: radial-gradient(circle, rgba(232,213,192,0.5) 0%, transparent 70%);
    top: 40%; left: 50%;
    transform: translateX(-50%);
  }

  .page {
    position: relative;
    z-index: 1;
    max-width: 480px;
    margin: 0 auto;
    padding: 56px 22px 80px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  /* ─── HEADER SECTION ─── */
  .brand-header {
    text-align: center;
    margin-bottom: 36px;
    animation: riseIn 1s cubic-bezier(0.16,1,0.3,1) both;
  }

  .brand-eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--terracotta);
    margin-bottom: 12px;
    opacity: 0;
    animation: fadeIn 0.8s 0.3s ease forwards;
  }

  .brand-logo {
    position: relative;
    display: inline-block;
    margin-bottom: 10px;
  }

  .brand-logo::before,
  .brand-logo::after {
    content: '';
    position: absolute;
    top: 50%;
    width: 28px;
    height: 1px;
    background: var(--warm);
    opacity: 0.7;
  }
  .brand-logo::before { right: calc(100% + 10px); }
  .brand-logo::after  { left:  calc(100% + 10px); }

  .brand-name {
    font-family: 'Bodoni Moda', serif;
    font-size: clamp(44px, 11vw, 62px);
    font-weight: 900;
    letter-spacing: -2px;
    line-height: 0.92;
    color: var(--ink);
  }

  .brand-name span {
    font-style: italic;
    color: var(--terracotta);
  }

  .brand-sub {
    font-family: 'Bodoni Moda', serif;
    font-style: italic;
    font-size: 15px;
    color: var(--muted);
    margin-top: 8px;
    letter-spacing: 0.5px;
  }

  /* Avatar */
  .avatar-ring {
    width: 86px;
    height: 86px;
    border-radius: 50%;
    padding: 3px;
    background: conic-gradient(var(--terracotta) 0deg, var(--warm) 120deg, var(--sand) 240deg, var(--terracotta) 360deg);
    margin-bottom: 20px;
    animation: spin 10s linear infinite, riseIn 1s 0.1s cubic-bezier(0.16,1,0.3,1) both;
  }

  .avatar-inner {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background: var(--bg);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Bodoni Moda', serif;
    font-weight: 900;
    font-size: 30px;
    color: var(--ink);
    letter-spacing: -1px;
    border: 3px solid var(--bg);
  }

  @keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }

  /* Tagline */
  .tagline-row {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 36px;
    opacity: 0;
    animation: fadeIn 0.8s 0.6s ease forwards;
  }
  .tag-dot { width: 5px; height: 5px; border-radius: 50%; background: var(--terracotta); }
  .tagline-text {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--muted);
  }

  /* ─── LINKS ─── */
  .links {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .link-card {
    display: flex;
    align-items: center;
    gap: 15px;
    padding: 16px 18px;
    border-radius: 16px;
    text-decoration: none;
    background: var(--card-bg);
    border: 1.5px solid rgba(212,165,116,0.2);
    box-shadow: 0 2px 16px var(--shadow), 0 1px 3px rgba(100,60,30,0.06);
    position: relative;
    overflow: hidden;
    cursor: pointer;
    transition: transform 0.25s cubic-bezier(0.34,1.56,0.64,1),
                box-shadow 0.25s ease,
                border-color 0.25s ease;
    opacity: 0;
  }

  .link-card:hover {
    transform: translateY(-3px) scale(1.015);
    box-shadow: 0 12px 40px rgba(196,98,58,0.15), 0 4px 12px var(--shadow);
    border-color: rgba(196,98,58,0.35);
  }

  /* Sweep shine on hover */
  .link-card::after {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 50%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.5), transparent);
    transition: left 0.5s ease;
    pointer-events: none;
  }
  .link-card:hover::after { left: 150%; }

  /* Left accent bar */
  .link-card::before {
    content: '';
    position: absolute;
    left: 0; top: 15%; bottom: 15%;
    width: 3px;
    border-radius: 0 3px 3px 0;
    opacity: 0;
    transition: opacity 0.25s ease;
  }
  .link-card:hover::before { opacity: 1; }

  .card-pin::before   { background: #E60023; }
  .card-insta::before { background: linear-gradient(180deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888); }
  .card-ich::before   { background: #8a3ab9; }
  .card-yt::before    { background: #FF0000; }
  .card-wa::before    { background: #25D366; }

  /* Icon */
  .icon-box {
    width: 46px;
    height: 46px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    transition: transform 0.25s ease;
  }
  .link-card:hover .icon-box { transform: scale(1.1) rotate(-3deg); }

  .icon-box svg { width: 21px; height: 21px; }

  .card-pin   .icon-box { background: #fff0f0; color: #E60023; }
  .card-insta .icon-box { background: #fff0f8; color: #C13584; }
  .card-ich   .icon-box { background: #f6f0ff; color: #8a3ab9; }
  .card-yt    .icon-box { background: #fff0f0; color: #FF0000; }
  .card-wa    .icon-box { background: #f0fff4; color: #25D366; }

  /* Text */
  .link-body { flex: 1; min-width: 0; }

  .link-title {
    font-family: 'Bodoni Moda', serif;
    font-size: 17px;
    font-weight: 600;
    color: var(--ink);
    line-height: 1.2;
  }

  .link-desc {
    font-family: 'Jost', sans-serif;
    font-size: 11.5px;
    font-weight: 300;
    color: var(--muted);
    margin-top: 2px;
    letter-spacing: 0.3px;
  }

  /* Pill */
  .link-pill {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    padding: 4px 10px;
    border-radius: 20px;
    flex-shrink: 0;
    transition: transform 0.2s ease;
  }
  .link-card:hover .link-pill { transform: translateX(2px); }

  .card-pin   .link-pill { background: #fff0f0; color: #E60023; }
  .card-insta .link-pill { background: #fff0f8; color: #C13584; }
  .card-ich   .link-pill { background: #f6f0ff; color: #8a3ab9; }
  .card-yt    .link-pill { background: #fff0f0; color: #FF0000; }
  .card-wa    .link-pill { background: #f0fff4; color: #25D366; }

  /* Staggered card animations */
  .link-card:nth-child(1) { animation: cardIn 0.6s 0.7s cubic-bezier(0.16,1,0.3,1) forwards; }
  .link-card:nth-child(2) { animation: cardIn 0.6s 0.82s cubic-bezier(0.16,1,0.3,1) forwards; }
  .link-card:nth-child(3) { animation: cardIn 0.6s 0.94s cubic-bezier(0.16,1,0.3,1) forwards; }
  .link-card:nth-child(4) { animation: cardIn 0.6s 1.06s cubic-bezier(0.16,1,0.3,1) forwards; }
  .link-card:nth-child(5) { animation: cardIn 0.6s 1.18s cubic-bezier(0.16,1,0.3,1) forwards; }

  /* ─── SEPARATOR ─── */
  .sep {
    width: 100%;
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 38px 0 28px;
    opacity: 0;
    animation: fadeIn 0.8s 1.3s ease forwards;
  }
  .sep-line { flex: 1; height: 1px; background: linear-gradient(90deg, transparent, var(--sand), transparent); }
  .sep-text {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--muted);
  }

  /* ─── FOOTER ─── */
  .footer {
    text-align: center;
    opacity: 0;
    animation: fadeIn 0.8s 1.5s ease forwards;
  }

  .footer-brand {
    font-family: 'Bodoni Moda', serif;
    font-style: italic;
    font-size: 28px;
    font-weight: 400;
    color: var(--terracotta);
    opacity: 0.35;
    letter-spacing: 1px;
  }

  .footer-copy {
    font-family: 'Jost', sans-serif;
    font-size: 11px;
    font-weight: 300;
    color: var(--muted);
    opacity: 0.6;
    margin-top: 6px;
    letter-spacing: 0.5px;
  }

  /* ─── ANIMATIONS ─── */
  @keyframes riseIn {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
  }
  @keyframes cardIn {
    from { opacity: 0; transform: translateY(18px) scale(0.97); }
    to   { opacity: 1; transform: translateY(0) scale(1); }
  }

  /* ─── FLOATING BADGE ─── */
  .badge-float {
    position: fixed;
    top: 18px;
    right: 18px;
    background: var(--terracotta);
    color: white;
    font-family: 'DM Mono', monospace;
    font-size: 8.5px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 6px 12px;
    border-radius: 20px;
    z-index: 10;
    animation: fadeIn 1s 1.8s ease forwards;
    opacity: 0;
    box-shadow: 0 4px 16px rgba(196,98,58,0.3);
  }
</style>
</head>
<body>

<div class="blob blob-1"></div>
<div class="blob blob-2"></div>
<div class="blob blob-3"></div>

<div class="badge-float">✦ New Drops Daily</div>

<div class="page">

  <!-- Avatar -->
  <div class="avatar-ring">
    <div class="avatar-inner">P</div>
  </div>

  <!-- Brand Header -->
  <div class="brand-header">
    <div class="brand-eyebrow">✦ Official Affiliate Page ✦</div>
    <div class="brand-logo">
      <div class="brand-name">Piru<br><span>Fashion</span></div>
    </div>
    <div class="brand-sub">Wear it. Own it. Live it.</div>
  </div>

  <!-- Tagline Row -->
  <div class="tagline-row">
    <div class="tag-dot"></div>
    <div class="tagline-text">Style · Trends · Affiliate</div>
    <div class="tag-dot"></div>
  </div>

  <!-- Links -->
  <div class="links">

    <!-- Pinterest -->
    <a href="https://pinterest.com" class="link-card card-pin" target="_blank" rel="noopener">
      <div class="icon-box">
        <svg viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 0C5.373 0 0 5.373 0 12c0 5.084 3.163 9.426 7.627 11.174-.105-.949-.2-2.405.042-3.441.218-.937 1.407-5.965 1.407-5.965s-.359-.719-.359-1.782c0-1.668.967-2.914 2.171-2.914 1.023 0 1.518.769 1.518 1.69 0 1.029-.655 2.568-.994 3.995-.283 1.194.599 2.169 1.777 2.169 2.133 0 3.772-2.249 3.772-5.495 0-2.873-2.064-4.882-5.012-4.882-3.414 0-5.418 2.561-5.418 5.207 0 1.031.397 2.138.893 2.738a.36.36 0 0 1 .083.345l-.333 1.36c-.053.22-.174.267-.402.161-1.499-.698-2.436-2.889-2.436-4.649 0-3.785 2.75-7.262 7.929-7.262 4.163 0 7.398 2.967 7.398 6.931 0 4.136-2.607 7.464-6.227 7.464-1.216 0-2.359-.632-2.75-1.378l-.748 2.853c-.271 1.043-1.002 2.35-1.492 3.146C9.57 23.812 10.763 24 12 24c6.627 0 12-5.373 12-12S18.627 0 12 0z"/>
        </svg>
      </div>
      <div class="link-body">
        <div class="link-title">Pinterest</div>
        <div class="link-desc">Mood boards & style inspo</div>
      </div>
      <div class="link-pill">Explore</div>
    </a>

    <!-- Instagram -->
    <a href="https://instagram.com" class="link-card card-insta" target="_blank" rel="noopener">
      <div class="icon-box">
        <svg viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/>
        </svg>
      </div>
      <div class="link-body">
        <div class="link-title">Instagram</div>
        <div class="link-desc">Daily OOTDs & reels</div>
      </div>
      <div class="link-pill">Follow</div>
    </a>

    <!-- Instagram Channel -->
    <a href="https://instagram.com" class="link-card card-ich" target="_blank" rel="noopener">
      <div class="icon-box">
        <svg viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/>
        </svg>
      </div>
      <div class="link-body">
        <div class="link-title">Instagram Channel</div>
        <div class="link-desc">Exclusive deals & affiliate links</div>
      </div>
      <div class="link-pill">Join</div>
    </a>

    <!-- YouTube -->
    <a href="https://youtube.com" class="link-card card-yt" target="_blank" rel="noopener">
      <div class="icon-box">
        <svg viewBox="0 0 24 24" fill="currentColor">
          <path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
        </svg>
      </div>
      <div class="link-body">
        <div class="link-title">YouTube</div>
        <div class="link-desc">Hauls, lookbooks & try-ons</div>
      </div>
      <div class="link-pill">Watch</div>
    </a>

    <!-- WhatsApp Channel -->
    <a href="https://whatsapp.com/channel" class="link-card card-wa" target="_blank" rel="noopener">
      <div class="icon-box">
        <svg viewBox="0 0 24 24" fill="currentColor">
          <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/>
        </svg>
      </div>
      <div class="link-body">
        <div class="link-title">WhatsApp Channel</div>
        <div class="link-desc">Flash sales & direct links</div>
      </div>
      <div class="link-pill">Subscribe</div>
    </a>

  </div>

  <!-- Separator -->
  <div class="sep">
    <div class="sep-line"></div>
    <div class="sep-text">Piru Fashion</div>
    <div class="sep-line"></div>
  </div>

  <!-- Footer -->
  <div class="footer">
    <div class="footer-brand">Piru Fashion</div>
    <div class="footer-copy">✦ Affiliate links · Styled with passion · 2025 ✦</div>
  </div>

</div>
</body>
</html>
