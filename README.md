#<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no, maximum-scale=1.0, viewport-fit=cover">
<meta name="theme-color" content="#0a0e1a">
<title>✦ VAELTHORN — Comece Sua Jornada ✦</title>
<style>
/* ============================================================
   RESET + VARIÁVEIS
   ============================================================ */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Quicksand', 'Segoe UI', system-ui, sans-serif;
  -webkit-tap-highlight-color: transparent;
  user-select: none;
  -webkit-user-select: none;
}

:root {
  --ouro: #ffd700;
  --rosa: #ff80c0;
  --rosa-claro: #ffd0e8;
  --roxo: #a080ff;
  --azul: #60c0ff;
  --verde: #60e080;
  --vermelho: #ff6060;
  --bg-escuro: #0a0e1a;
  --bg-anime: linear-gradient(135deg, rgba(255,240,255,0.95), rgba(240,230,255,0.95));
  --borda-anime: #ffb0d0;
}

html, body {
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: var(--bg-escuro);
  color: #fff;
  position: fixed;
  touch-action: none;
  overscroll-behavior: none;
}

#gameCanvas {
  display: block;
  position: absolute;
  inset: 0;
  z-index: 1;
  cursor: crosshair;
  touch-action: none;
  image-rendering: pixelated;
}

/* ============================================================
   TELA 1: WELCOME
   ============================================================ */
.tela-welcome {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background:
    radial-gradient(circle at 20% 30%, rgba(255,128,192,0.4), transparent 55%),
    radial-gradient(circle at 80% 70%, rgba(160,128,255,0.4), transparent 55%),
    radial-gradient(circle at 50% 50%, rgba(96,192,255,0.25), transparent 70%),
    linear-gradient(180deg, #0a0e1a 0%, #1a0a3a 50%, #0a0e1a 100%);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  overflow: hidden;
  transition: opacity 0.6s ease;
}

.tela-welcome.saindo { opacity: 0; pointer-events: none; }

.tela-welcome::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image:
    radial-gradient(2px 2px at 20% 30%, #ffd0e8, transparent),
    radial-gradient(2px 2px at 70% 60%, #a080ff, transparent),
    radial-gradient(2px 2px at 40% 80%, #80d0ff, transparent),
    radial-gradient(3px 3px at 90% 20%, #fff, transparent),
    radial-gradient(2px 2px at 10% 70%, #ff80c0, transparent);
  background-size: 500px 500px, 400px 400px, 300px 300px, 600px 600px, 350px 350px;
  opacity: 0.6;
  pointer-events: none;
  animation: estrelas 90s linear infinite;
}

@keyframes estrelas {
  from { background-position: 0 0, 0 0, 0 0, 0 0, 0 0; }
  to { background-position: 500px 500px, -400px 400px, 300px -300px, -600px 600px, 350px 350px; }
}

.welcome-logo {
  font-size: clamp(5rem, 15vw, 9rem);
  margin-bottom: 10px;
  animation: flutuarLogo 3s ease-in-out infinite;
  filter: drop-shadow(0 0 40px rgba(255,128,192,0.8)) drop-shadow(0 0 80px rgba(160,128,255,0.5));
  position: relative;
  z-index: 1;
}

@keyframes flutuarLogo {
  0%, 100% { transform: translateY(0) rotate(-3deg) scale(1); }
  50% { transform: translateY(-15px) rotate(3deg) scale(1.05); }
}

.welcome-titulo {
  font-size: clamp(2rem, 7vw, 4rem);
  background: linear-gradient(90deg, #ff80c0, #ffd0e8, #a080ff, #80d0ff, #ff80c0);
  background-size: 300% auto;
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  letter-spacing: 6px;
  font-weight: 900;
  margin-bottom: 8px;
  animation: brilhar 4s linear infinite;
  position: relative;
  z-index: 1;
}

@keyframes brilhar { to { background-position: 300% center; } }

.welcome-sub {
  color: #d0c0e0;
  font-size: clamp(0.8rem, 2vw, 1rem);
  letter-spacing: 2px;
  margin-bottom: 30px;
  font-style: italic;
  position: relative;
  z-index: 1;
  text-align: center;
}

.welcome-botoes {
  display: flex;
  flex-direction: column;
  gap: 14px;
  position: relative;
  z-index: 1;
  width: 100%;
  max-width: 320px;
}

.btn-principal {
  padding: 18px 30px;
  font-size: 1.05rem;
  font-weight: 900;
  background: linear-gradient(135deg, #ff80c0, #a080ff, #80c0ff);
  background-size: 300% auto;
  color: #fff;
  border: 3px solid #ffd0e8;
  border-radius: 50px;
  cursor: pointer;
  letter-spacing: 3px;
  text-transform: uppercase;
  transition: all 0.3s;
  animation: gachaAnime 3s ease infinite, pulseBtn 2s ease-in-out infinite;
  box-shadow: 0 15px 40px rgba(255,128,192,0.6);
  text-shadow: 0 2px 6px rgba(0,0,0,0.3);
}

@keyframes gachaAnime {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

@keyframes pulseBtn {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.btn-principal:hover {
  transform: scale(1.08) translateY(-3px);
  box-shadow: 0 20px 50px rgba(255,128,192,0.8);
}

/* ============================================================
   TELA 2: SELEÇÃO DE HERÓI
   ============================================================ */
.tela-heroi {
  position: fixed;
  inset: 0;
  z-index: 900;
  background:
    radial-gradient(circle at 20% 20%, rgba(255,128,192,0.3), transparent 50%),
    radial-gradient(circle at 80% 80%, rgba(160,128,255,0.3), transparent 50%),
    linear-gradient(180deg, #0a0e1a, #1a0a3a);
  display: none;
  flex-direction: column;
  padding: 14px;
  overflow: hidden;
}

.tela-heroi.ativo { display: flex; }

.tela-heroi-header {
  text-align: center;
  margin-bottom: 12px;
  flex-shrink: 0;
  padding: 10px;
}

.tela-heroi-header h2 {
  font-size: clamp(1.3rem, 4vw, 2rem);
  background: linear-gradient(90deg, #ffd0e8, #ff80c0, #a080ff, #ffd0e8);
  background-size: 300% auto;
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: brilhar 3s linear infinite;
  font-weight: 900;
  letter-spacing: 3px;
  margin-bottom: 6px;
}

.tela-heroi-header p {
  color: #d0c0e0;
  font-size: 0.78rem;
  font-style: italic;
  letter-spacing: 1px;
}

.tela-heroi-conteudo {
  flex: 1;
  display: flex;
  gap: 14px;
  overflow: hidden;
  min-height: 0;
}

.grade-herois {
  flex: 1;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
  gap: 10px;
  overflow-y: auto;
  padding: 6px;
  align-content: start;
}

.card-heroi {
  position: relative;
  background: linear-gradient(160deg, rgba(255,240,255,0.95), rgba(240,230,255,0.9));
  border-radius: 14px;
  padding: 8px;
  border: 2px solid #e0c0f0;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  aspect-ratio: 3/4;
}

.card-heroi:hover {
  transform: translateY(-8px) scale(1.03);
  box-shadow: 0 20px 40px rgba(255,128,192,0.5), 0 0 40px currentColor;
  border-color: currentColor;
}

.card-heroi.selecionado {
  border-color: #ff80c0;
  background: linear-gradient(160deg, rgba(255,224,240,0.98), rgba(240,220,255,0.95));
  box-shadow: 0 0 30px rgba(255,128,192,0.7);
  transform: translateY(-5px) scale(1.02);
}

.card-heroi canvas {
  width: 100%;
  aspect-ratio: 1;
  margin-bottom: 5px;
}

.card-heroi .nome {
  font-size: 0.75rem;
  font-weight: bold;
  color: #7050a0;
  text-align: center;
  margin-bottom: 2px;
}

.card-heroi .classe {
  font-size: 0.58rem;
  color: #9070b0;
  text-align: center;
  font-style: italic;
}

.painel-detalhes {
  width: 320px;
  flex-shrink: 0;
  background: var(--bg-anime);
  border: 3px solid var(--borda-anime);
  border-radius: 20px;
  padding: 18px;
  overflow-y: auto;
  box-shadow: 0 10px 30px rgba(255,176,208,0.4);
  color: #4a3050;
}

.painel-detalhes .detalhe-sprite {
  width: 140px;
  height: 140px;
  margin: 0 auto 12px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(255,255,255,0.6), rgba(200,180,230,0.4));
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid var(--borda-anime);
  overflow: hidden;
}

.painel-detalhes .detalhe-sprite canvas {
  width: 100%;
  height: 100%;
}

.painel-detalhes .detalhe-nome {
  font-size: 1.35rem;
  font-weight: 900;
  color: #7050a0;
  text-align: center;
  margin-bottom: 4px;
}

.painel-detalhes .detalhe-titulo {
  font-size: 0.78rem;
  color: #a080d0;
  text-align: center;
  font-style: italic;
  margin-bottom: 6px;
}

.painel-detalhes .detalhe-raca {
  font-size: 0.72rem;
  color: #9070b0;
  text-align: center;
  margin-bottom: 12px;
  padding-bottom: 12px;
  border-bottom: 1px solid rgba(160,128,192,0.3);
}

.detalhe-stats {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  margin-bottom: 14px;
}

.stat-item {
  background: rgba(160,128,192,0.15);
  border-radius: 10px;
  padding: 8px 10px;
  border-left: 3px solid #ff80c0;
}

.stat-item .stat-label {
  font-size: 0.6rem;
  color: #9070b0;
  text-transform: uppercase;
}

.stat-item .stat-valor {
  font-size: 1rem;
  font-weight: 900;
  color: #7050a0;
}

.detalhe-historia {
  font-size: 0.75rem;
  color: #604080;
  line-height: 1.5;
  font-style: italic;
  margin-bottom: 14px;
  padding: 10px;
  background: rgba(160,128,192,0.08);
  border-radius: 10px;
  border-left: 3px solid #a080ff;
}

.btn-confirmar {
  width: 100%;
  padding: 14px;
  font-size: 0.92rem;
  font-weight: 900;
  background: linear-gradient(135deg, #60e080, #40c060);
  color: #fff;
  border: 3px solid #a0ffc0;
  border-radius: 14px;
  cursor: pointer;
  letter-spacing: 2px;
  text-transform: uppercase;
  transition: all 0.25s;
  box-shadow: 0 10px 25px rgba(96,224,128,0.5);
}

.btn-confirmar:hover {
  transform: translateY(-3px) scale(1.02);
  box-shadow: 0 15px 35px rgba(96,224,128,0.7);
}

.btn-voltar {
  width: 100%;
  padding: 10px;
  font-size: 0.8rem;
  font-weight: bold;
  background: rgba(160,128,192,0.2);
  color: #7050a0;
  border: 2px solid #b090d0;
  border-radius: 12px;
  cursor: pointer;
  margin-top: 8px;
}

/* ============================================================
   ANIMAÇÃO DE ENTRADA
   ============================================================ */
.animacao-entrada {
  position: fixed;
  inset: 0;
  z-index: 950;
  background: radial-gradient(circle, #fff, #ffd0e8, #a080ff, #000);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 20px;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.6s ease;
}

.animacao-entrada.ativo { opacity: 1; pointer-events: auto; }

.animacao-entrada canvas {
  width: 200px;
  height: 200px;
  animation: zoomIn 1s cubic-bezier(0.34, 1.56, 0.64, 1);
}

@keyframes zoomIn {
  0% { transform: scale(0) rotate(360deg); opacity: 0; }
  60% { transform: scale(1.3) rotate(-10deg); opacity: 1; }
  100% { transform: scale(1) rotate(0deg); opacity: 1; }
}

.animacao-entrada .texto-entrada {
  color: #fff;
  font-size: 1.4rem;
  font-weight: 900;
  letter-spacing: 4px;
  text-shadow: 0 0 30px rgba(255,128,192,1), 0 0 60px rgba(160,128,255,0.8);
  text-transform: uppercase;
}

/* ============================================================
   HUD
   ============================================================ */
#hud {
  position: fixed;
  top: 12px;
  left: 12px;
  z-index: 10;
  background: var(--bg-anime);
  border: 3px solid var(--borda-anime);
  border-radius: 18px;
  padding: 10px 14px;
  min-width: 220px;
  color: #4a3050;
  display: none;
}

#hud.ativo { display: block; }

.hud-topo {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 6px;
}

.hud-avatar {
  width: 42px;
  height: 42px;
  border-radius: 50%;
  background: linear-gradient(135deg, #ffb0d0, #a080ff);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.3rem;
  border: 3px solid #ffd0e8;
  flex-shrink: 0;
}

.hud-nome { font-size: 0.8rem; font-weight: bold; color: #7050a0; }
.hud-titulo { font-size: 0.58rem; color: #a080d0; font-style: italic; }
.hud-nivel { font-size: 0.58rem; color: #9070b0; }

.barra {
  width: 100%;
  height: 11px;
  background: rgba(80,60,100,0.15);
  border-radius: 8px;
  overflow: hidden;
  margin-bottom: 3px;
  border: 2px solid rgba(255,255,255,0.8);
}

.barra-fill {
  height: 100%;
  border-radius: 6px;
  transition: width 0.3s ease;
}

.barra-hp .barra-fill { background: linear-gradient(90deg, #ff8080, #ffb0b0); }
.barra-mana .barra-fill { background: linear-gradient(90deg, #80b0ff, #a0d0ff); }
.barra-fome .barra-fill { background: linear-gradient(90deg, #ffb060, #ffd090); }
.barra-ult .barra-fill { background: linear-gradient(90deg, #ff80c0, #ffa0d0); }
.barra-xp .barra-fill { background: linear-gradient(90deg, #a080ff, #c0a0ff); }

.barra-texto {
  display: flex;
  justify-content: space-between;
  font-size: 0.55rem;
  color: #604080;
  font-weight: 600;
  margin-bottom: 3px;
}

#recursos {
  position: fixed;
  top: 12px;
  right: 12px;
  z-index: 10;
  background: var(--bg-anime);
  border: 3px solid #ffd0a0;
  border-radius: 18px;
  padding: 8px 12px;
  display: none;
  gap: 10px;
  flex-wrap: wrap;
  color: #7050a0;
  font-weight: bold;
  font-size: 0.72rem;
}

#recursos.ativo { display: flex; }

#minimapa {
  position: fixed;
  top: 12px;
  right: 240px;
  z-index: 10;
  width: 130px;
  height: 130px;
  border-radius: 50%;
  background: var(--bg-anime);
  border: 3px solid var(--borda-anime);
  overflow: hidden;
  display: none;
}

#minimapa.ativo { display: block; }

#hotbar {
  position: fixed;
  bottom: 12px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 15;
  display: none;
  gap: 5px;
  background: var(--bg-anime);
  padding: 6px;
  border-radius: 16px;
  border: 3px solid var(--borda-anime);
}

#hotbar.ativo { display: flex; }

.slot-hotbar {
  width: 46px;
  height: 46px;
  background: rgba(255,255,255,0.6);
  border: 2px solid #e0c0f0;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.3rem;
  cursor: pointer;
  transition: all 0.2s;
  position: relative;
  color: #7050a0;
}

.slot-hotbar.selecionado {
  border-color: #ff80c0;
  background: linear-gradient(135deg, rgba(255,224,240,0.95), rgba(240,220,255,0.95));
  box-shadow: 0 0 15px rgba(255,128,192,0.6);
}

.slot-hotbar .num {
  position: absolute;
  top: 1px;
  left: 3px;
  font-size: 0.45rem;
  color: #9070b0;
  font-weight: bold;
}

#acoes {
  position: fixed;
  top: 180px;
  right: 12px;
  z-index: 10;
  display: none;
  flex-direction: column;
  gap: 6px;
}

#acoes.ativo { display: flex; }

.botao-acao {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: var(--bg-anime);
  border: 2px solid var(--borda-anime);
  color: #7050a0;
  font-size: 1.1rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

.botao-acao:hover {
  background: linear-gradient(135deg, #ffd0e8, #ffb0d0);
  color: #fff;
  transform: scale(1.15);
}

#log {
  position: fixed;
  bottom: 80px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 15;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  pointer-events: none;
}

.mensagem {
  background: var(--bg-anime);
  border: 2px solid var(--borda-anime);
  border-radius: 20px;
  padding: 5px 14px;
  color: #7050a0;
  font-size: 0.72rem;
  font-weight: bold;
}

#toast {
  position: fixed;
  bottom: 160px;
  left: 50%;
  transform: translateX(-50%) translateY(20px);
  background: var(--bg-anime);
  border: 3px solid var(--borda-anime);
  color: #7050a0;
  padding: 10px 22px;
  border-radius: 25px;
  font-size: 0.82rem;
  font-weight: bold;
  opacity: 0;
  pointer-events: none;
  transition: all 0.4s;
  z-index: 300;
}

#toast.visivel { opacity: 1; transform: translateX(-50%) translateY(0); }

#controlesTouch {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 20;
  display: none;
}

#controlesTouch.ativo { display: block; }

#joystick {
  position: absolute;
  bottom: 100px;
  left: 30px;
  width: 130px;
  height: 130px;
  background: radial-gradient(circle, rgba(255,176,208,0.3), rgba(160,128,255,0.2));
  border: 3px solid rgba(255,208,232,0.7);
  border-radius: 50%;
  pointer-events: auto;
  touch-action: none;
}

#joystickKnob {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 55px;
  height: 55px;
  margin-left: -27px;
  margin-top: -27px;
  background: radial-gradient(circle, #ffd0e8, #ff80c0, #a080ff);
  border: 3px solid #fff;
  border-radius: 50%;
  pointer-events: none;
}

#botoesTouch {
  position: absolute;
  bottom: 100px;
  right: 30px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  pointer-events: auto;
}

.botao-touch {
  width: 65px;
  height: 65px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  color: #fff;
  pointer-events: auto;
  border: 3px solid rgba(255,255,255,0.7);
  cursor: pointer;
}

.botao-touch.ataque {
  grid-column: 1 / 3;
  justify-self: center;
  width: 85px;
  height: 85px;
  font-size: 1.9rem;
  background: radial-gradient(circle, rgba(255,220,60,0.95), rgba(180,100,0,0.95));
}

.botao-touch.ultimate {
  grid-column: 1 / 3;
  justify-self: center;
  background: radial-gradient(circle, rgba(255,80,180,0.95), rgba(160,20,100,0.95));
  width: 85px;
  height: 85px;
  font-size: 1.9rem;
}

.botao-touch.dash {
  background: radial-gradient(circle, rgba(100,220,255,0.9), rgba(20,120,180,0.95));
}

.botao-touch.cura {
  background: radial-gradient(circle, rgba(120,255,160,0.9), rgba(20,140,60,0.95));
}

@media (max-width: 700px) {
  .tela-heroi-conteudo { flex-direction: column; }
  .painel-detalhes { width: 100%; max-height: 45vh; }
  .grade-herois { max-height: 45vh; }
  #minimapa { display: none; }
}
</style>
</head>
<body>

<!-- TELA 1: WELCOME -->
<div class="tela-welcome" id="telaWelcome">
  <div class="welcome-logo">✦</div>
  <h1 class="welcome-titulo">VAELTHORN</h1>
  <p class="welcome-sub">O mundo dos espinhos etéreos aguarda um novo herói...</p>
  <div class="welcome-botoes">
    <button class="btn-principal" id="btnComecar">⚔️ COMEÇAR JORNADA</button>
  </div>
</div>

<!-- TELA 2: SELEÇÃO DE HERÓI -->
<div class="tela-heroi" id="telaHeroi">
  <div class="tela-heroi-header">
    <h2>🎭 ESCOLHA SEU HERÓI</h2>
    <p>Clique em um personagem para ver seus detalhes</p>
  </div>
  <div class="tela-heroi-conteudo">
    <div class="grade-herois" id="gradeHerois"></div>
    <div class="painel-detalhes">
      <div class="detalhe-sprite" id="detalheSprite"></div>
      <div class="detalhe-nome" id="detalheNome">Escolha um herói</div>
      <div class="detalhe-titulo" id="detalheTitulo">Clique em um card à esquerda</div>
      <div class="detalhe-raca" id="detalheRaca">—</div>
      <div class="detalhe-stats" id="detalheStats" style="display:none;">
        <div class="stat-item"><div class="stat-label">❤️ HP</div><div class="stat-valor" id="statHP">0</div></div>
        <div class="stat-item"><div class="stat-label">⚔️ ATK</div><div class="stat-valor" id="statATK">0</div></div>
        <div class="stat-item"><div class="stat-label">🛡️ DEF</div><div class="stat-valor" id="statDEF">0</div></div>
        <div class="stat-item"><div class="stat-label">💨 VEL</div><div class="stat-valor" id="statVEL">0</div></div>
      </div>
      <div class="detalhe-historia" id="detalheHistoria" style="display:none;"></div>
      <button class="btn-confirmar" id="btnConfirmarHeroi" style="display:none;">⚔️ INICIAR JORNADA</button>
      <button class="btn-voltar" id="btnVoltarWelcome">← Voltar</button>
    </div>
  </div>
</div>

<!-- ANIMAÇÃO DE ENTRADA -->
<div class="animacao-entrada" id="animacaoEntrada">
  <canvas id="canvasEntrada" width="200" height="200"></canvas>
  <div class="texto-entrada" id="textoEntrada">Entrando em Vaelthorn...</div>
</div>

<!-- CANVAS DO JOGO -->
<canvas id="gameCanvas"></canvas>

<!-- HUD -->
<div id="hud">
  <div class="hud-topo">
    <div class="hud-avatar" id="hudAvatar">🧝</div>
    <div>
      <div class="hud-nome" id="hudNome">Lyra</div>
      <div class="hud-titulo" id="hudTitulo">Ar

