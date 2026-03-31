<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ServiceOS — Estructura tu servicio, vende mejor, cobra lo que mereces</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet">
<style>
  :root {
    --dark:    #0D1B2A;
    --darker:  #07111A;
    --accent:  #E94560;
    --accent2: #1B98E0;
    --green:   #27AE60;
    --gold:    #F59E0B;
    --light:   #F4F6F9;
    --mid:     #3A3A3A;
    --soft:    #6B7280;
    --white:   #FFFFFF;
    --card-bg: #0F2233;
    --border:  rgba(255,255,255,0.08);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--darker);
    color: var(--white);
    overflow-x: hidden;
    line-height: 1.6;
  }

  .syne { font-family: 'Syne', sans-serif; }
  h1, h2, h3 { font-family: 'Syne', sans-serif; line-height: 1.1; }

  .container { max-width: 1100px; margin: 0 auto; padding: 0 24px; }
  .section { padding: 100px 0; }
  .section-sm { padding: 60px 0; }

  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    background: rgba(7,17,26,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    padding: 16px 24px;
  }
  .nav-inner {
    max-width: 1100px; margin: 0 auto;
    display: flex; align-items: center; justify-content: space-between;
  }
  .logo {
    font-family: 'Syne', sans-serif;
    font-size: 1.4rem; font-weight: 800;
    letter-spacing: -0.02em;
  }
  .logo span { color: var(--accent); }
  .nav-cta {
    background: var(--accent);
    color: white; font-weight: 600;
    padding: 10px 24px; border-radius: 6px;
    text-decoration: none; font-size: 0.9rem;
    transition: all 0.2s;
  }
  .nav-cta:hover { background: #c73850; transform: translateY(-1px); }

  .hero {
    min-height: 100vh;
    display: flex; align-items: center;
    padding-top: 80px;
    position: relative;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 60% 40%, rgba(233,69,96,0.12) 0%, transparent 60%),
      radial-gradient(ellipse 60% 40% at 10% 80%, rgba(27,152,224,0.08) 0%, transparent 50%),
      var(--darker);
  }
  .hero-grid {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);
    background-size: 60px 60px;
    mask-image: radial-gradient(ellipse 70% 70% at 50% 50%, black, transparent);
  }
  .hero-content {
    position: relative; z-index: 2;
    max-width: 820px;
  }
  .hero-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(233,69,96,0.12);
    border: 1px solid rgba(233,69,96,0.3);
    color: var(--accent);
    padding: 6px 16px; border-radius: 100px;
    font-size: 0.82rem; font-weight: 600;
    margin-bottom: 32px;
    animation: fadeUp 0.6s ease both;
  }
  .hero-badge::before {
    content: '';
    width: 6px; height: 6px;
    background: var(--accent);
    border-radius: 50%;
    animation: pulse 1.5s infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.8); }
  }
  .hero h1 {
    font-size: clamp(2.8rem, 6vw, 5rem);
    font-weight: 800;
    letter-spacing: -0.03em;
    line-height: 1.05;
    margin-bottom: 28px;
    animation: fadeUp 0.6s 0.1s ease both;
  }
  .hero h1 .accent { color: var(--accent); }
  .hero h1 .accent2 { color: var(--accent2); }
  .hero-sub {
    font-size: 1.2rem; color: rgba(255,255,255,0.65);
    max-width: 600px; margin-bottom: 48px;
    line-height: 1.7; font-weight: 300;
    animation: fadeUp 0.6s 0.2s ease both;
  }
  .hero-actions {
    display: flex; align-items: center; gap: 16px; flex-wrap: wrap;
    animation: fadeUp 0.6s 0.3s ease both;
  }
  .btn-primary {
    background: var(--accent);
    color: white; font-family: 'Syne', sans-serif;
    font-weight: 700; font-size: 1rem;
    padding: 16px 36px; border-radius: 8px;
    text-decoration: none;
    transition: all 0.25s;
    display: inline-flex; align-items: center; gap: 8px;
    position: relative; overflow: hidden;
  }
  .btn-primary::after {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(255,255,255,0.15), transparent);
    opacity: 0; transition: opacity 0.2s;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 12px 40px rgba(233,69,96,0.35); }
  .btn-primary:hover::after { opacity: 1; }

  .btn-secondary {
    color: rgba(255,255,255,0.7);
    font-size: 0.95rem; font-weight: 500;
    text-decoration: none;
    display: inline-flex; align-items: center; gap: 6px;
    transition: color 0.2s;
  }
  .btn-secondary:hover { color: white; }

  .hero-proof {
    margin-top: 56px;
    display: flex; align-items: center; gap: 24px; flex-wrap: wrap;
    animation: fadeUp 0.6s 0.4s ease both;
  }
  .proof-item {
    display: flex; align-items: center; gap: 8px;
    font-size: 0.85rem; color: rgba(255,255,255,0.5);
  }
  .proof-item svg { color: var(--green); flex-shrink: 0; }
  .proof-divider { width: 1px; height: 16px; background: var(--border); }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .problem-section {
    background: var(--dark);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }
  .problem-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0;
  }
  .problem-col {
    padding: 80px 60px;
  }
  .problem-col:first-child {
    border-right: 1px solid var(--border);
  }
  .problem-label {
    font-size: 0.75rem; font-weight: 700;
    letter-spacing: 0.12em; text-transform: uppercase;
    color: var(--soft); margin-bottom: 24px;
  }
  .problem-list { list-style: none; }
  .problem-list li {
    display: flex; align-items: flex-start; gap: 12px;
    padding: 14px 0;
    border-bottom: 1px solid var(--border);
    font-size: 0.95rem; color: rgba(255,255,255,0.75);
    line-height: 1.5;
  }
  .problem-list li:last-child { border-bottom: none; }
  .x-icon { color: var(--accent); font-size: 1rem; flex-shrink: 0; margin-top: 2px; }
  .check-icon { color: var(--green); font-size: 1rem; flex-shrink: 0; margin-top: 2px; }

  .section-tag {
    display: inline-block;
    font-size: 0.75rem; font-weight: 700;
    letter-spacing: 0.12em; text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
  }
  .section-title {
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800;
    letter-spacing: -0.02em;
    margin-bottom: 20px;
  }
  .section-sub {
    font-size: 1.1rem; color: rgba(255,255,255,0.55);
    max-width: 560px; line-height: 1.7; font-weight: 300;
  }
  .section-header { margin-bottom: 64px; }

  .que-es-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
  }
  .que-es-card {
    background: var(--card-bg);
    padding: 40px 32px;
    transition: background 0.2s;
  }
  .que-es-card:hover { background: #142840; }
  .card-num {
    font-family: 'Syne', sans-serif;
    font-size: 3rem; font-weight: 800;
    color: rgba(233,69,96,0.2);
    line-height: 1; margin-bottom: 16px;
  }
  .card-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.15rem; font-weight: 700;
    margin-bottom: 12px; color: white;
  }
  .card-desc {
    font-size: 0.9rem; color: rgba(255,255,255,0.55);
    line-height: 1.6;
  }

  .modulos-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }
  .modulo-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 28px 32px;
    display: flex; gap: 20px;
    transition: all 0.2s;
    cursor: default;
  }
  .modulo-card:hover {
    border-color: var(--accent);
    transform: translateY(-2px);
    box-shadow: 0 8px 32px rgba(0,0,0,0.3);
  }
  .modulo-num {
    font-family: 'Syne', sans-serif;
    font-size: 0.75rem; font-weight: 800;
    color: var(--accent);
    letter-spacing: 0.08em;
    flex-shrink: 0; padding-top: 2px;
  }
  .modulo-title {
    font-family: 'Syne', sans-serif;
    font-size: 1rem; font-weight: 700;
    margin-bottom: 6px;
  }
  .modulo-desc {
    font-size: 0.875rem; color: rgba(255,255,255,0.5);
    line-height: 1.5;
  }
  .modulo-pills {
    display: flex; flex-wrap: wrap; gap: 6px; margin-top: 12px;
  }
  .pill {
    font-size: 0.72rem; font-weight: 600;
    padding: 3px 10px; border-radius: 100px;
    background: rgba(255,255,255,0.06);
    color: rgba(255,255,255,0.4);
    border: 1px solid rgba(255,255,255,0.08);
  }

  .para-quien-section { background: var(--dark); }
  .perfiles-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px; margin-bottom: 48px;
  }
  .perfil-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 28px;
    transition: all 0.2s;
  }
  .perfil-card:hover {
    border-color: rgba(27,152,224,0.4);
    background: rgba(27,152,224,0.05);
  }
  .perfil-icon {
    font-size: 1.8rem; margin-bottom: 14px;
  }
  .perfil-title {
    font-family: 'Syne', sans-serif;
    font-size: 1rem; font-weight: 700;
    margin-bottom: 8px;
  }
  .perfil-desc {
    font-size: 0.875rem; color: rgba(255,255,255,0.5);
    line-height: 1.6;
  }
  .no-para-quien {
    background: rgba(233,69,96,0.06);
    border: 1px solid rgba(233,69,96,0.15);
    border-radius: 12px;
    padding: 28px 32px;
  }
  .no-title {
    font-size: 0.8rem; font-weight: 700;
    letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--accent); margin-bottom: 16px;
  }
  .no-list {
    display: flex; flex-wrap: wrap; gap: 10px;
  }
  .no-item {
    font-size: 0.875rem; color: rgba(255,255,255,0.45);
    display: flex; align-items: center; gap: 6px;
  }
  .no-item::before { content: '×'; color: var(--accent); font-weight: 700; }

  .incluye-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }
  .incluye-item {
    display: flex; align-items: flex-start; gap: 16px;
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 24px;
    transition: all 0.2s;
  }
  .incluye-item:hover { border-color: rgba(39,174,96,0.3); }
  .incluye-icon {
    width: 40px; height: 40px; border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.2rem; flex-shrink: 0;
    background: rgba(255,255,255,0.05);
  }
  .incluye-title {
    font-family: 'Syne', sans-serif;
    font-size: 0.95rem; font-weight: 700;
    margin-bottom: 4px;
  }
  .incluye-desc {
    font-size: 0.85rem; color: rgba(255,255,255,0.45);
    line-height: 1.5;
  }

  .precio-section { background: var(--darker); }
  .precio-wrapper {
    max-width: 760px; margin: 0 auto;
  }
  .precio-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 20px;
    overflow: hidden;
    position: relative;
  }
  .precio-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
  }
  .precio-header {
    padding: 48px 48px 36px;
    border-bottom: 1px solid var(--border);
  }
  .precio-badge {
    display: inline-block;
    background: rgba(233,69,96,0.1);
    border: 1px solid rgba(233,69,96,0.2);
    color: var(--accent);
    font-size: 0.78rem; font-weight: 700;
    letter-spacing: 0.08em; text-transform: uppercase;
    padding: 5px 14px; border-radius: 100px;
    margin-bottom: 24px;
  }
  .precio-amount {
    display: flex; align-items: flex-start; gap: 4px;
    margin-bottom: 12px;
  }
  .precio-currency {
    font-family: 'Syne', sans-serif;
    font-size: 1.5rem; font-weight: 700;
    color: rgba(255,255,255,0.5);
    padding-top: 12px;
  }
  .precio-number {
    font-family: 'Syne', sans-serif;
    font-size: 5rem; font-weight: 800;
    letter-spacing: -0.04em; line-height: 1;
  }
  .precio-period {
    font-size: 0.9rem; color: rgba(255,255,255,0.4);
    align-self: flex-end; padding-bottom: 12px;
  }
  .precio-desc {
    font-size: 0.95rem; color: rgba(255,255,255,0.5);
    max-width: 440px; line-height: 1.6;
  }
  .precio-body {
    padding: 40px 48px;
    display: grid; grid-template-columns: 1fr 1fr; gap: 16px;
  }
  .precio-feature {
    display: flex; align-items: flex-start; gap: 10px;
    font-size: 0.9rem; color: rgba(255,255,255,0.75);
    line-height: 1.4;
  }
  .precio-feature svg { color: var(--green); flex-shrink: 0; margin-top: 2px; }
  .precio-footer {
    padding: 0 48px 48px;
  }
  .precio-cta {
    display: block; text-align: center;
    background: var(--accent);
    color: white; font-family: 'Syne', sans-serif;
    font-weight: 700; font-size: 1.1rem;
    padding: 18px 36px; border-radius: 10px;
    text-decoration: none;
    transition: all 0.25s;
    margin-bottom: 16px;
  }
  .precio-cta:hover {
    background: #c73850;
    transform: translateY(-2px);
    box-shadow: 0 12px 40px rgba(233,69,96,0.4);
  }
  .precio-guarantee {
    text-align: center;
    font-size: 0.82rem; color: rgba(255,255,255,0.35);
    display: flex; align-items: center; justify-content: center; gap: 6px;
  }

  .garantia-section {
    background: var(--dark);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }
  .garantia-inner {
    display: grid; grid-template-columns: 1fr 2fr; gap: 60px;
    align-items: center;
  }
  .garantia-num {
    font-family: 'Syne', sans-serif;
    font-size: 8rem; font-weight: 800;
    color: var(--accent); line-height: 1;
    opacity: 0.9;
  }
  .garantia-unit { font-size: 2rem; }
  .garantia-title {
    font-family: 'Syne', sans-serif;
    font-size: 2.2rem; font-weight: 800;
    margin-bottom: 16px; letter-spacing: -0.02em;
  }
  .garantia-desc {
    font-size: 1rem; color: rgba(255,255,255,0.6);
    line-height: 1.7; font-weight: 300; margin-bottom: 24px;
  }
  .garantia-note {
    font-size: 0.85rem; color: rgba(255,255,255,0.35);
    font-style: italic;
  }

  .urgencia-section {
    background: linear-gradient(135deg, rgba(233,69,96,0.12) 0%, rgba(27,152,224,0.08) 100%);
    border-top: 1px solid rgba(233,69,96,0.15);
    border-bottom: 1px solid rgba(233,69,96,0.15);
  }
  .urgencia-inner {
    display: flex; align-items: center; justify-content: space-between;
    gap: 40px; flex-wrap: wrap;
  }
  .urgencia-text h3 {
    font-size: 1.8rem; font-weight: 800;
    margin-bottom: 8px; letter-spacing: -0.02em;
  }
  .urgencia-text p {
    color: rgba(255,255,255,0.55); font-size: 0.95rem;
  }
  .urgencia-highlight { color: var(--accent); }

  .faq-section { background: var(--darker); }
  .faq-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
  }
  .faq-item {
    background: var(--card-bg);
    padding: 32px;
  }
  .faq-q {
    font-family: 'Syne', sans-serif;
    font-size: 0.95rem; font-weight: 700;
    margin-bottom: 10px; color: white;
  }
  .faq-a {
    font-size: 0.875rem; color: rgba(255,255,255,0.5);
    line-height: 1.7;
  }

  .final-cta {
    background: var(--darker);
    text-align: center;
    padding: 120px 24px;
    position: relative;
    overflow: hidden;
  }
  .final-cta-bg {
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 60% 60% at 50% 50%, rgba(233,69,96,0.1) 0%, transparent 70%);
  }
  .final-cta-content { position: relative; z-index: 2; }
  .final-cta h2 {
    font-size: clamp(2.5rem, 5vw, 4rem);
    font-weight: 800; letter-spacing: -0.03em;
    margin-bottom: 20px;
    max-width: 700px; margin-left: auto; margin-right: auto;
  }
  .final-cta p {
    font-size: 1.1rem; color: rgba(255,255,255,0.5);
    margin-bottom: 48px; font-weight: 300;
  }

  footer {
    background: var(--darker);
    border-top: 1px solid var(--border);
    padding: 40px 24px;
    text-align: center;
    font-size: 0.85rem; color: rgba(255,255,255,0.3);
  }
  footer strong { color: rgba(255,255,255,0.6); }

  .reveal {
    opacity: 0; transform: translateY(32px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .reveal.visible {
    opacity: 1; transform: translateY(0);
  }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }

  @media (max-width: 768px) {
    .section { padding: 70px 0; }
    .problem-grid,
    .que-es-grid,
    .modulos-grid,
    .perfiles-grid,
    .incluye-grid,
    .precio-body,
    .faq-grid { grid-template-columns: 1fr; }
    .problem-col { padding: 40px 24px; }
    .problem-col:first-child { border-right: none; border-bottom: 1px solid var(--border); }
    .garantia-inner { grid-template-columns: 1fr; gap: 24px; }
    .garantia-num { font-size: 5rem; }
    .urgencia-inner { flex-direction: column; text-align: center; }
    .precio-header, .precio-body, .precio-footer { padding: 28px; }
    .precio-number { font-size: 3.5rem; }
    .final-cta { padding: 80px 24px; }
  }
</style>
</head>
<body>

<nav>
  <div class="nav-inner">
    <div class="logo">Service<span>OS</span></div>
    <a href="https://hotmart.com/es/marketplace/productos/hagsxd-serviceos-ulkw4/J105115278A?preview=true" class="nav-cta" target="_blank" rel="noopener noreferrer">Quiero el kit →</a>
  </div>
</nav>

<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>
  <div class="container">
    <div class="hero-content">
      <div class="hero-badge">Kit completo para profesionales independientes</div>
      <h1>
        Deja de improvisar.<br>
        <span class="accent">Estructura tu servicio,</span><br>
        vende con confianza<br>
        y cobra lo que mereces.
      </h1>
      <p class="hero-sub">
        8 módulos · 22 plantillas · Calculadora de precios · Mini CRM · 12 prompts de IA.
        Todo lo que necesitas para conseguir más clientes y cobrar mejor —
        sin importar a qué te dediques.
      </p>
      <div class="hero-actions">
        <a href="https://hotmart.com/es/marketplace/productos/hagsxd-serviceos-ulkw4/J105115278A?preview=true" class="btn-primary" target="_blank" rel="noopener noreferrer">
          Acceder al kit por $47
          <svg width="16" height="16" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
        </a>
        <a href="#que-incluye" class="btn-secondary">
          Ver qué incluye
          <svg width="14" height="14" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/></svg>
        </a>
      </div>
      <div class="hero-proof">
        <div class="proof-item">Descarga inmediata</div>
        <div class="proof-divider"></div>
        <div class="proof-item">7 días de garantía</div>
        <div class="proof-divider"></div>
        <div class="proof-item">Un solo pago — sin suscripción</div>
        <div class="proof-divider"></div>
        <div class="proof-item">Para cualquier tipo de servicio</div>
      </div>
    </div>
  </div>
</section>

<section class="section precio-section" id="precio">
  <div class="container">
    <div class="section-header reveal" style="text-align:center; margin-left:auto; margin-right:auto; max-width:560px;">
      <div class="section-tag">Precio de lanzamiento</div>
      <h2 class="section-title">Un solo pago.<br>Acceso de por vida.</h2>
    </div>
    <div class="precio-wrapper">
      <div class="precio-card reveal">
        <div class="precio-header">
          <div class="precio-badge">🔥 Precio de lanzamiento — sube pronto</div>
          <div class="precio-amount">
            <span class="precio-currency">$</span>
            <span class="precio-number">47</span>
            <span class="precio-period">USD · pago único</span>
          </div>
          <p class="precio-desc">
            Precio sube a $67 cuando termine el período de lanzamiento.
            Sin suscripción. Sin cargos adicionales. Acceso a todas las actualizaciones futuras.
          </p>
        </div>
        <div class="precio-footer">
          <a href="https://hotmart.com/es/marketplace/productos/hagsxd-serviceos-ulkw4/J105115278A?preview=true" class="precio-cta" target="_blank" rel="noopener noreferrer">
            Quiero el kit por $47 — Acceso inmediato
          </a>
          <div class="precio-guarantee">
            Garantía de 7 días — Si no es lo que esperabas, te devuelvo el dinero completo.
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<section class="section-sm urgencia-section">
  <div class="container">
    <div class="urgencia-inner">
      <div class="urgencia-text reveal">
        <h3>El precio sube a <span class="urgencia-highlight">$67</span> pronto.</h3>
        <p>Este es el precio de lanzamiento. Una vez que termine, no vuelve.</p>
      </div>
      <div class="reveal reveal-delay-1">
        <a href="https://hotmart.com/es/marketplace/productos/hagsxd-serviceos-ulkw4/J105115278A?preview=true" class="btn-primary" style="font-size:1rem; padding:16px 32px;" target="_blank" rel="noopener noreferrer">
          Asegurar precio de $47 →
        </a>
      </div>
    </div>
  </div>
</section>

<section class="final-cta">
  <div class="final-cta-bg"></div>
  <div class="container final-cta-content">
    <div class="reveal">
      <h2>Deja de improvisar.<br><span style="color:var(--accent)">Empieza a ejecutar.</span></h2>
      <p>El conocimiento sin herramientas no cambia nada. Las herramientas sin acción tampoco.<br>ServiceOS te da ambas cosas.</p>
      <a href="https://hotmart.com/es/marketplace/productos/hagsxd-serviceos-ulkw4/J105115278A?preview=true" class="btn-primary" style="font-size:1.1rem; padding:18px 48px; margin: 0 auto;" target="_blank" rel="noopener noreferrer">
        Quiero el kit por $47 — Acceso inmediato
        <svg width="18" height="18" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
      </a>
    </div>
  </div>
</section>

<footer>
  <p><strong>Service<span style="color:var(--accent)">OS</span></strong> · Kit para freelancers, consultores y emprendedores independientes</p>
</footer>

<script>
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

const sections = document.querySelectorAll('section[id]');
window.addEventListener('scroll', () => {
  const scrollY = window.scrollY;
  sections.forEach(section => {
    const sectionTop = section.offsetTop - 100;
    const sectionBottom = sectionTop + section.offsetHeight;
    if (scrollY >= sectionTop && scrollY < sectionBottom) {
      document.querySelectorAll('nav a').forEach(a => {
        a.classList.remove('active');
        if (a.getAttribute('href') === `#${section.id}`) {
          a.classList.add('active');
        }
      });
    }
  });
});
</script>
</body>
</html>
