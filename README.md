<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0">
  <title>Uma Carta Para Você 💜</title>
  <meta name="description" content="Uma declaração de amor delicada, romântica e inesquecível.">
  
  <!-- Tipografias elegantes: Cinzel (títulos), Cormorant Garamond (leitura da carta) e Great Vibes (assinatura) -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700&family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400;1,600&family=Great+Vibes&family=Montserrat:wght@300;400;500&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg-dark-1: #100720;
      --bg-dark-2: #1e0d36;
      --bg-dark-3: #2d134d;
      --accent-lilac: #d8b4e2;
      --accent-purple: #7a4bb7;
      --accent-soft-pink: #fbeaf4;
      --accent-gold: #e8c872;
      --accent-gold-dark: #b89130;
      --paper-cream: #fffdf9;
      --paper-shadow: rgba(18, 5, 34, 0.45);
      --text-main: #2b1f3d;
      --text-muted: #5e4f73;
      --envelope-front: #573280;
      --envelope-back: #452467;
      --envelope-flap: #6b3e9e;
      --gold-gradient: linear-gradient(135deg, #fce09b 0%, #d8a741 50%, #9e721d 100%);
      --seal-shadow: 0 4px 15px rgba(216, 167, 65, 0.4);
      --transition-smooth: cubic-bezier(0.25, 1, 0.5, 1);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      min-height: 100vh;
      width: 100vw;
      overflow-x: hidden;
      background: radial-gradient(circle at 50% 30%, var(--bg-dark-2) 0%, var(--bg-dark-3) 45%, var(--bg-dark-1) 100%);
      font-family: 'Montserrat', sans-serif;
      color: #ffffff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      position: relative;
      perspective: 1200px;
    }

    /* Fundo dinâmico com canvas de estrelas e poeira estelar */
    #ambient-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1;
    }

    /* Brilho de ambiência sutil */
    .glow-overlay {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 80vw;
      height: 80vh;
      max-width: 900px;
      max-height: 900px;
      background: radial-gradient(circle, rgba(162, 105, 237, 0.15) 0%, rgba(216, 180, 226, 0.05) 40%, transparent 70%);
      pointer-events: none;
      z-index: 2;
      border-radius: 50%;
      filter: blur(40px);
    }

    /* Container Principal */
    .main-container {
      position: relative;
      z-index: 10;
      width: 100%;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 30px 20px;
    }

    /* Tela Inicial: Envelope Fechado */
    .intro-section {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      transition: opacity 1.2s var(--transition-smooth), transform 1.2s var(--transition-smooth);
      position: relative;
    }

    .intro-section.fade-out {
      opacity: 0;
      transform: scale(0.92);
      pointer-events: none;
    }

    .intro-title {
      font-family: 'Cinzel', serif;
      font-size: clamp(1.4rem, 4vw, 2.2rem);
      font-weight: 400;
      letter-spacing: 4px;
      color: #f7efff;
      text-shadow: 0 2px 15px rgba(216, 180, 226, 0.4);
      margin-bottom: 28px;
      text-align: center;
      opacity: 0;
      animation: fadeInDown 1.4s 0.3s forwards ease-out;
    }

    .intro-subtitle {
      font-size: 0.85rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--accent-lilac);
      margin-top: 28px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
      opacity: 0;
      animation: fadeInUp 1.4s 0.6s forwards ease-out;
      transition: all 0.3s ease;
    }

    .intro-subtitle:hover {
      color: #ffffff;
      text-shadow: 0 0 12px var(--accent-lilac);
      transform: translateY(-2px);
    }

    /* O Envelope 3D Feito em CSS Puro */
    .envelope-wrapper {
      position: relative;
      width: 320px;
      height: 220px;
      cursor: pointer;
      animation: floatEnvelope 5s ease-in-out infinite;
      transform-style: preserve-3d;
      transition: transform 0.5s var(--transition-smooth);
    }

    @media (min-width: 640px) {
      .envelope-wrapper {
        width: 400px;
        height: 260px;
      }
    }

    .envelope-wrapper:hover {
      transform: translateY(-6px) scale(1.02);
    }

    /* Corpo do Envelope */
    .envelope {
      position: relative;
      width: 100%;
      height: 100%;
      background: var(--envelope-back);
      border-radius: 12px;
      box-shadow: 0 15px 40px rgba(0, 0, 0, 0.5), 0 0 35px rgba(122, 75, 183, 0.3);
      overflow: visible;
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    /* Aba Superior (Flap) */
    .envelope-flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 160px solid transparent;
      border-right: 160px solid transparent;
      border-top: 130px solid var(--envelope-flap);
      transform-origin: top center;
      transition: transform 0.8s 0.2s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: 5;
      filter: drop-shadow(0 2px 6px rgba(0, 0, 0, 0.35));
    }

    @media (min-width: 640px) {
      .envelope-flap {
        border-left-width: 200px;
        border-right-width: 200px;
        border-top-width: 150px;
      }
    }

    /* Abas Laterais e Inferior (Bolsa do Envelope) */
    .envelope-pocket {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 3;
      border-radius: 0 0 12px 12px;
      overflow: hidden;
      pointer-events: none;
    }

    .envelope-pocket::before {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 0;
      border-left: 160px solid #4a2772;
      border-right: 160px solid #4a2772;
      border-top: 110px solid transparent;
      border-bottom: 110px solid #5d358a;
    }

    @media (min-width: 640px) {
      .envelope-pocket::before {
        border-left-width: 200px;
        border-right-width: 200px;
        border-top-width: 130px;
        border-bottom-width: 130px;
      }
    }

    /* Linhas finas de brilho dourado no envelope */
    .envelope-pocket::after {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      box-shadow: inset 0 0 0 1px rgba(232, 200, 114, 0.15);
      border-radius: 12px;
    }

    /* Papel visível espreitando de dentro */
    .envelope-peek-letter {
      position: absolute;
      bottom: 12px;
      left: 5%;
      width: 90%;
      height: 75%;
      background: var(--paper-cream);
      border-radius: 6px;
      z-index: 2;
      box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
      transition: transform 0.8s 0.6s var(--transition-smooth);
    }

    /* Selo de Cera Dourado em Coração */
    .seal-heart {
      position: absolute;
      top: 115px;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 52px;
      height: 52px;
      background: var(--gold-gradient);
      border-radius: 50%;
      z-index: 10;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      box-shadow: var(--seal-shadow), inset 0 2px 4px rgba(255, 255, 255, 0.6), inset 0 -3px 5px rgba(0, 0, 0, 0.4);
      transition: all 0.4s var(--transition-smooth);
    }

    @media (min-width: 640px) {
      .seal-heart {
        top: 135px;
        width: 60px;
        height: 60px;
      }
    }

    .seal-heart::after {
      content: "❤";
      font-size: 24px;
      color: #791e3e;
      text-shadow: 0 1px 2px rgba(255, 255, 255, 0.4);
      transform: translateY(-1px);
    }

    .seal-heart:hover {
      transform: translate(-50%, -50%) scale(1.12);
      box-shadow: 0 0 25px rgba(232, 200, 114, 0.8), inset 0 2px 6px rgba(255, 255, 255, 0.8);
    }

    /* Animação ao Abrir */
    .envelope-wrapper.opening .envelope-flap {
      transform: rotateX(180deg);
      z-index: 1;
    }

    .envelope-wrapper.opening .seal-heart {
      opacity: 0;
      transform: translate(-50%, -50%) scale(0.3);
      pointer-events: none;
    }

    .envelope-wrapper.opening .envelope-peek-letter {
      transform: translateY(-130px);
    }

    /* Sessão da Carta Revelada */
    .letter-section {
      display: none;
      opacity: 0;
      width: 100%;
      max-width: 680px;
      margin: auto;
      position: relative;
      z-index: 20;
      transform: translateY(35px) scale(0.96);
      transition: opacity 1.3s cubic-bezier(0.16, 1, 0.3, 1), transform 1.3s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .letter-section.active {
      display: block;
    }

    .letter-section.show {
      opacity: 1;
      transform: translateY(0) scale(1);
    }

    /* Folha de Pergaminho Romântico */
    .letter-paper {
      background: var(--paper-cream);
      background-image: 
        radial-gradient(#eedcb5 0.5px, transparent 0.5px),
        radial-gradient(#faf3e3 0.5px, #fffefb 0.5px);
      background-size: 20px 20px;
      background-position: 0 0, 10px 10px;
      border-radius: 16px;
      padding: 48px 32px 42px 32px;
      position: relative;
      box-shadow: 0 25px 60px var(--paper-shadow), 0 0 0 1px rgba(216, 167, 65, 0.25), 0 0 45px rgba(216, 180, 226, 0.2);
      color: var(--text-main);
      overflow: hidden;
    }

    @media (min-width: 640px) {
      .letter-paper {
        padding: 64px 56px 52px 56px;
      }
    }

    /* Borda interna dourada sutil */
    .letter-inner-border {
      position: absolute;
      top: 16px;
      left: 16px;
      right: 16px;
      bottom: 16px;
      border: 1px solid rgba(184, 145, 48, 0.3);
      border-radius: 10px;
      pointer-events: none;
    }

    /* Cantoneiras decorativas clássicas */
    .corner-ornament {
      position: absolute;
      width: 24px;
      height: 24px;
      border-color: var(--accent-gold-dark);
      opacity: 0.6;
      pointer-events: none;
    }

    .corner-tl { top: 22px; left: 22px; border-top: 2px solid; border-left: 2px solid; }
    .corner-tr { top: 22px; right: 22px; border-top: 2px solid; border-right: 2px solid; }
    .corner-bl { bottom: 22px; left: 22px; border-bottom: 2px solid; border-left: 2px solid; }
    .corner-br { bottom: 22px; right: 22px; border-bottom: 2px solid; border-right: 2px solid; }

    /* Cabeçalho da Carta */
    .letter-header {
      text-align: center;
      margin-bottom: 36px;
    }

    .letter-badge {
      font-size: 1.5rem;
      color: #9d3356;
      margin-bottom: 8px;
      display: inline-block;
      animation: heartbeat 2.2s infinite ease-in-out;
    }

    .letter-heading {
      font-family: 'Cinzel', serif;
      font-size: clamp(1.2rem, 3vw, 1.6rem);
      letter-spacing: 3px;
      color: #432269;
      font-weight: 600;
      text-transform: uppercase;
      position: relative;
      display: inline-block;
      padding-bottom: 10px;
    }

    .letter-heading::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 60px;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--accent-gold), transparent);
    }

    /* Corpo do Texto da Carta */
    .letter-content {
      font-family: 'Cormorant Garamond', Georgia, serif;
      font-size: clamp(1.15rem, 2.6vw, 1.35rem);
      line-height: 1.95;
      color: #2b1f3d;
      font-weight: 500;
      text-align: justify;
      hyphens: auto;
      position: relative;
      z-index: 2;
    }

    .letter-paragraph {
      margin-bottom: 24px;
      text-indent: 1.8em;
      opacity: 0;
      transform: translateY(12px);
      transition: opacity 1s ease, transform 1s ease;
    }

    .letter-section.show .letter-paragraph:nth-child(1) {
      opacity: 1;
      transform: translateY(0);
      transition-delay: 0.3s;
    }

    .letter-section.show .letter-paragraph:nth-child(2) {
      opacity: 1;
      transform: translateY(0);
      transition-delay: 0.7s;
    }

    .letter-section.show .letter-paragraph:nth-child(3) {
      opacity: 1;
      transform: translateY(0);
      transition-delay: 1.1s;
    }

    .letter-section.show .letter-paragraph:nth-child(4) {
      opacity: 1;
      transform: translateY(0);
      transition-delay: 1.5s;
    }

    .first-letter-drop {
      float: left;
      font-family: 'Cinzel', serif;
      font-size: 3.2rem;
      line-height: 0.8;
      padding-top: 4px;
      padding-right: 8px;
      color: #572d82;
      font-weight: 600;
    }

    /* Assinatura Manuscrita */
    .letter-footer {
      margin-top: 40px;
      text-align: right;
      padding-right: 15px;
      opacity: 0;
      transform: translateY(10px);
      transition: opacity 1.2s 1.9s ease, transform 1.2s 1.9s ease;
    }

    .letter-section.show .letter-footer {
      opacity: 1;
      transform: translateY(0);
    }

    .signature-text {
      font-family: 'Great Vibes', cursive;
      font-size: clamp(2.3rem, 5vw, 3.2rem);
      color: #632d8a;
      line-height: 1.2;
      display: inline-block;
      text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.08);
    }

    .signature-heart {
      color: #b3254e;
      display: inline-block;
      margin-left: 6px;
      animation: heartbeat 2s infinite ease-in-out;
    }

    /* Ações ao Pé da Carta (Reabrir / Fechar) */
    .letter-actions {
      margin-top: 36px;
      display: flex;
      justify-content: center;
      opacity: 0;
      transition: opacity 1s 2.3s ease;
    }

    .letter-section.show .letter-actions {
      opacity: 1;
    }

    .close-card-btn {
      background: transparent;
      border: 1px solid rgba(255, 255, 255, 0.25);
      color: var(--accent-lilac);
      padding: 10px 24px;
      border-radius: 999px;
      font-size: 0.82rem;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      transition: all 0.3s ease;
      backdrop-filter: blur(8px);
    }

    .close-card-btn:hover {
      background: rgba(255, 255, 255, 0.1);
      color: #ffffff;
      border-color: var(--accent-lilac);
      transform: translateY(-2px);
    }

    /* Floating Heart Sprinkles ao clicar */
    .burst-heart {
      position: fixed;
      pointer-events: none;
      z-index: 100;
      animation: burstFloat 1.8s forwards cubic-bezier(0.2, 0.8, 0.2, 1);
      will-change: transform, opacity;
    }

    /* Animações Principais */
    @keyframes floatEnvelope {
      0%, 100% {
        transform: translateY(0px) rotate(0deg);
      }
      50% {
        transform: translateY(-10px) rotate(0.4deg);
      }
    }

    @keyframes heartbeat {
      0%, 100% { transform: scale(1); }
      15% { transform: scale(1.22); }
      30% { transform: scale(1); }
      45% { transform: scale(1.15); }
    }

    @keyframes fadeInDown {
      from {
        opacity: 0;
        transform: translateY(-20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    @keyframes fadeInUp {
      from {
        opacity: 0;
        transform: translateY(20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    @keyframes burstFloat {
      0% {
        opacity: 1;
        transform: translate(0, 0) scale(0.6) rotate(0deg);
      }
      100% {
        opacity: 0;
        transform: translate(var(--tx), var(--ty)) scale(1.4) rotate(var(--tr));
      }
    }

    @media (prefers-reduced-motion: reduce) {
      .envelope-wrapper {
        animation: none;
      }
      .letter-badge, .signature-heart {
        animation: none;
      }
      .intro-section, .letter-section, .envelope-flap, .envelope-peek-letter, .letter-paragraph, .letter-footer {
        transition-duration: 0.05s !important;
        animation: none !important;
        opacity: 1 !important;
        transform: none !important;
      }
      .intro-title, .intro-subtitle {
        opacity: 1 !important;
      }
    }
  </style>
</head>
<body>

  <!-- Canvas interativo com partículas e céu estelar -->
  <canvas id="ambient-canvas"></canvas>
  <div class="glow-overlay"></div>

  <main class="main-container">

    <!-- TELA 1: Abertura Romântica com Envelope e Selo de Coração -->
    <section class="intro-section" id="intro-section" aria-label="Envelope da Carta de Amor">
      <h1 class="intro-title">Uma carta para você...</h1>

      <div class="envelope-wrapper" id="envelope-interactive" role="button" tabindex="0" aria-label="Clique para abrir a carta de amor">
        <div class="envelope">
          <!-- Aba triangular que se dobra para trás -->
          <div class="envelope-flap"></div>
          
          <!-- Folha de papel visível subindo -->
          <div class="envelope-peek-letter"></div>
          
          <!-- Selo dourado com relevo de coração -->
          <div class="seal-heart" id="seal-trigger" title="Abrir com amor"></div>
          
          <!-- Bolsa frontal do envelope -->
          <div class="envelope-pocket"></div>
        </div>
      </div>

      <div class="intro-subtitle" id="open-helper">
        <span>Clique para abrir</span>
        <span>💜</span>
      </div>
    </section>

    <!-- TELA 2: A Carta de Amor Aberta com Mensagem Íntima -->
    <article class="letter-section" id="letter-section" aria-live="polite">
      <div class="letter-paper">
        <div class="letter-inner-border"></div>
        
        <!-- Detalhes ornamentais clássicos nos 4 cantos -->
        <div class="corner-ornament corner-tl"></div>
        <div class="corner-ornament corner-tr"></div>
        <div class="corner-ornament corner-bl"></div>
        <div class="corner-ornament corner-br"></div>

        <header class="letter-header">
          <div class="letter-badge">✦ ❦ ✦</div>
          <h2 class="letter-heading">Para a Minha Amada</h2>
        </header>

        <!-- Mensagem de Amor -->
        <div class="letter-content">
          <p class="letter-paragraph">
            <span class="first-letter-drop">A</span>pesar de tantas vezes te chamar de princesa, às vezes penso se sou realmente digno de ser o príncipe da minha amada.
          </p>
          <p class="letter-paragraph">
            Você é a mulher mais doce e bela que conheci. Seu rosto, seu jeito, sua presença... tudo em você me encanta. E, diante de tanta beleza, o que mais desejo é ser digno de cuidar de você, te amar e caminhar ao seu lado.
          </p>
          <p class="letter-paragraph">
            Ainda me lembro de quando ouvi sua voz pela primeira vez, quando perguntei seu nome. Naquele momento, você me pareceu como uma flor: linda, delicada e, para mim, inalcançável.
          </p>
          <p class="letter-paragraph">
            Hoje, aquela mulher que um dia pareceu tão distante é o amor da minha vida. E talvez esse seja o maior presente que eu poderia receber.
          </p>
        </div>

        <!-- Assinatura Manuscrita -->
        <footer class="letter-footer">
          <div class="signature-text">Com amor, Luiz <span class="signature-heart">❤️</span></div>
        </footer>
      </div>

      <!-- Botão para fechar ou rever o momento -->
      <div class="letter-actions">
        <button id="reset-btn" class="close-card-btn" type="button">
          <span>↺</span> Guardar a carta no envelope
        </button>
      </div>
    </article>

  </main>

  <script>
    /* -------------------------------------------------------------
     * 1. Canvas Ambiente: Estrelas Cintilantes e Partículas de Luz
     * Efeito sereno e ultra leve sem pesar na GPU.
     * ------------------------------------------------------------- */
    const canvas = document.getElementById('ambient-canvas');
    const ctx = canvas.getContext('2d');
    let width, height;
    let particles = [];
    const PARTICLE_COUNT = 65;

    function resizeCanvas() {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    class AmbientParticle {
      constructor() {
        this.reset(true);
      }

      reset(init = false) {
        this.x = Math.random() * width;
        this.y = init ? Math.random() * height : height + 10;
        this.size = Math.random() * 2.2 + 0.6;
        this.speedY = Math.random() * 0.35 + 0.15;
        this.speedX = (Math.random() - 0.5) * 0.2;
        this.opacity = Math.random() * 0.7 + 0.2;
        this.pulseSpeed = Math.random() * 0.02 + 0.008;
        this.pulse = Math.random() * Math.PI * 2;
        // Tons lilases, dourados suaves e rosados
        const colors = [
          'rgba(216, 180, 226, ', // Lilás suave
          'rgba(251, 234, 244, ', // Rosa claro
          'rgba(232, 200, 114, ', // Dourado suave
          'rgba(255, 255, 255, '  // Estrela branca
        ];
        this.colorBase = colors[Math.floor(Math.random() * colors.length)];
      }

      update() {
        this.y -= this.speedY;
        this.x += this.speedX;
        this.pulse += this.pulseSpeed;

        if (this.y < -10 || this.x < -10 || this.x > width + 10) {
          this.reset();
        }
      }

      draw() {
        const currentOpacity = Math.max(0.1, (Math.sin(this.pulse) * 0.5 + 0.5) * this.opacity);
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fillStyle = this.colorBase + currentOpacity + ')';
        ctx.shadowBlur = this.size > 1.8 ? 8 : 0;
        ctx.shadowColor = 'rgba(216, 180, 226, 0.5)';
        ctx.fill();
        ctx.shadowBlur = 0;
      }
    }

    for (let i = 0; i < PARTICLE_COUNT; i++) {
      particles.push(new AmbientParticle());
    }

    function animateAmbient() {
      ctx.clearRect(0, 0, width, height);
      for (let i = 0; i < particles.length; i++) {
        particles[i].update();
        particles[i].draw();
      }
      requestAnimationFrame(animateAmbient);
    }
    requestAnimationFrame(animateAmbient);

    /* -------------------------------------------------------------
     * 2. Interação da Carta (Abrir, Transição e Explosão de Brilhos)
     * ------------------------------------------------------------- */
    const envelopeWrapper = document.getElementById('envelope-interactive');
    const introSection = document.getElementById('intro-section');
    const letterSection = document.getElementById('letter-section');
    const resetBtn = document.getElementById('reset-btn');
    const openHelper = document.getElementById('open-helper');

    let isLetterOpen = false;

    // Função para criar pequenos corações flutuantes ao clicar
    function createHeartBurst(originX, originY) {
      const heartChars = ['💜', '✨', '🌸', '💖', '⭐'];
      const count = 14;

      for (let i = 0; i < count; i++) {
        const heart = document.createElement('span');
        heart.className = 'burst-heart';
        heart.textContent = heartChars[Math.floor(Math.random() * heartChars.length)];
        
        const angle = (Math.PI * 2 * i) / count + (Math.random() * 0.4 - 0.2);
        const distance = Math.random() * 120 + 60;
        const tx = Math.cos(angle) * distance;
        const ty = Math.sin(angle) * distance - 40; // Leve impulso para cima
        const rot = Math.random() * 90 - 45;

        heart.style.left = `${originX}px`;
        heart.style.top = `${originY}px`;
        heart.style.setProperty('--tx', `${tx}px`);
        heart.style.setProperty('--ty', `${ty}px`);
        heart.style.setProperty('--tr', `${rot}deg`);
        heart.style.fontSize = `${Math.random() * 14 + 16}px`;

        document.body.appendChild(heart);

        setTimeout(() => {
          heart.remove();
        }, 1800);
      }
    }

    // Abertura da Carta
    function openLetter(e) {
      if (isLetterOpen) return;
      isLetterOpen = true;

      // Ponto de origem do efeito de corações
      const rect = envelopeWrapper.getBoundingClientRect();
      const clickX = e && e.clientX ? e.clientX : rect.left + rect.width / 2;
      const clickY = e && e.clientY ? e.clientY : rect.top + rect.height / 2;

      createHeartBurst(clickX, clickY);

      // 1. O envelope inicia o desdobramento da aba
      envelopeWrapper.classList.add('opening');

      // 2. Desvanecer a tela inicial com delicadeza
      setTimeout(() => {
        introSection.classList.add('fade-out');
      }, 700);

      // 3. Ocultar envelope e revelar o pergaminho
      setTimeout(() => {
        introSection.style.display = 'none';
        letterSection.classList.add('active');

        // Scroll suave para o topo se estiver em tela reduzida
        window.scrollTo({ top: 0, behavior: 'smooth' });

        requestAnimationFrame(() => {
          letterSection.classList.add('show');
        });
      }, 1400);
    }

    // Fechar e voltar à tela inicial para reviver a emoção
    function closeLetter() {
      if (!isLetterOpen) return;

      letterSection.classList.remove('show');

      setTimeout(() => {
        letterSection.classList.remove('active');
        introSection.style.display = 'flex';

        // Pequeno reflow para disparar a animação
        void introSection.offsetWidth;

        envelopeWrapper.classList.remove('opening');
        introSection.classList.remove('fade-out');
        isLetterOpen = false;

        window.scrollTo({ top: 0, behavior: 'smooth' });
      }, 800);
    }

    // Eventos de clique e toque
    envelopeWrapper.addEventListener('click', openLetter);
    openHelper.addEventListener('click', openLetter);

    envelopeWrapper.addEventListener('keydown', (e) => {
      if (e.key === 'Enter' || e.key === ' ') {
        e.preventDefault();
        openLetter();
      }
    });

    resetBtn.addEventListener('click', closeLetter);

    // Efeito sutil de brilho que segue o cursor em telas grandes
    document.addEventListener('mousemove', (e) => {
      if (Math.random() > 0.88 && !window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
        const spark = document.createElement('div');
        spark.style.position = 'fixed';
        spark.style.left = `${e.clientX}px`;
        spark.style.top = `${e.clientY}px`;
        spark.style.width = '3px';
        spark.style.height = '3px';
        spark.style.borderRadius = '50%';
        spark.style.background = '#d8b4e2';
        spark.style.pointerEvents = 'none';
        spark.style.boxShadow = '0 0 8px #fbeaf4';
        spark.style.transition = 'all 0.8s ease-out';
        spark.style.zIndex = '9999';
        document.body.appendChild(spark);

        requestAnimationFrame(() => {
          spark.style.transform = `translate(${(Math.random() - 0.5) * 20}px, ${(Math.random() - 0.5) * 20 + 15}px) scale(0)`;
          spark.style.opacity = '0';
        });

        setTimeout(() => spark.remove(), 800);
      }
    });
  </script>
</body>
</html>
