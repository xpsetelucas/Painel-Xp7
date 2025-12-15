<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Painel com Abas (Visual)</title>

<style>
*{box-sizing:border-box}
body{
  background:#0b0f14;
  font-family:Arial,Helvetica,sans-serif;
  display:flex;
  justify-content:center;
  margin-top:40px;
  color:#fff
}
.painel{
  width:380px;
  background:#111;
  border-radius:15px;
  box-shadow:0 0 25px rgba(0,120,255,.5);
  padding:12px;
  transition:.25s
}
.painel.hidden{
  opacity:0;
  transform:scale(.98);
  pointer-events:none
}
.topo{
  background:linear-gradient(90deg,#b00000,#ff0000);
  border-radius:12px;
  padding:8px;
  display:flex;
  gap:6px
}
.aba{
  background:#2a0000;
  padding:6px 10px;
  border-radius:10px;
  font-size:13px;
  cursor:pointer;
  border:1px solid rgba(255,255,255,.15)
}
.aba.ativa{
  background:#7a0000;
  box-shadow:0 0 10px rgba(0,120,255,.7)
}
.conteudo{margin-top:12px}
.tab{display:none}
.tab.ativa{display:block}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:10px}

.botao{
  background:#0f1a2b;
  border-radius:12px;
  padding:10px;
  display:flex;
  justify-content:space-between;
  align-items:center;
  box-shadow:0 0 10px rgba(0,120,255,.3);
  margin-bottom:10px
}

.switch{
  width:40px;
  height:20px;
  background:#333;
  border-radius:20px;
  position:relative;
  cursor:pointer
}
.switch::before{
  content:"";
  width:16px;
  height:16px;
  background:#aaa;
  border-radius:50%;
  position:absolute;
  top:2px;
  left:2px;
  transition:.3s
}
.switch.ativo{
  background:#ff0000;
  box-shadow:0 0 8px rgba(255,0,0,.7)
}
.switch.ativo::before{
  left:22px;
  background:#00aaff
}

.select, .range{
  background:#111;
  color:#fff;
  border:none;
  border-radius:8px;
  padding:4px
}

.range-value{margin-left:6px}

.misc-wrap{text-align:center}
.misc-title{font-weight:bold;margin:10px 0}
.info-item{margin:6px 0;font-size:14px}
</style>
</head>

<body>
<div id="painel" class="painel">

  <div class="topo">
    <div class="aba ativa" data-tab="aim">AIM</div>
    <div class="aba" data-tab="esp">ESP</div>
    <div class="aba" data-tab="misc">MISC</div>
    <div class="aba" data-tab="info">INFO</div>
  </div>

  <div class="conteudo">

    <!-- AIM -->
    <div class="tab ativa" id="aim">

      <div class="grid-2">
        <div class="botao">
          Ativar Aimbot
          <div id="switchAimbot" class="switch"></div>
        </div>

        <div class="botao">
          Exibir FOV
          <div class="switch"></div>
        </div>

        <div class="botao">
          Aimbot Legit
          <div class="switch"></div>
        </div>

        <div class="botao">
          Aimbot Rápido
          <div class="switch"></div>
        </div>
      </div>

      <div class="botao">
        Alvo
        <select class="select">
          <option>Cabeça</option>
          <option>Peito</option>
          <option>Corpo</option>
        </select>
      </div>

      <div class="botao">
        FOV
        <input type="range" min="0" max="100" value="50" class="range"
        oninput="this.nextElementSibling.textContent=this.value">
        <span class="range-value">50</span>
      </div>

    </div>

    <!-- ESP -->
    <div class="tab" id="esp">
      <div class="botao">Ativar ESP<div class="switch"></div></div>
    </div>

    <!-- MISC -->
    <div class="tab" id="misc">
      <div class="misc-wrap">
        <div class="misc-title">MISC</div>
        Em desenvolvimento
      </div>
    </div>

    <!-- INFO -->
    <div class="tab" id="info">
      <div class="misc-wrap">
        <div class="misc-title">INFORMAÇÕES</div>
        <div class="info-item"><b>Criador:</b> Xp7_Lucas</div>
        <div class="info-item"><b>Data:</b> 15/12/2025</div>
        <div class="info-item"><b>FPS:</b> <span id="fps">--</span></div>
        <div class="info-item"><b>Ping:</b> <span id="ping">--</span></div>
        <div class="info-item"><b>Horário:</b> <span id="hora">--:--:--</span></div>
      </div>
    </div>

  </div>
</div>

<script>
// ===== ABAS =====
document.querySelectorAll('.aba').forEach(aba=>{
  aba.onclick=()=>{
    document.querySelectorAll('.aba,.tab')
      .forEach(e=>e.classList.remove('ativa'));
    aba.classList.add('ativa');
    document.getElementById(aba.dataset.tab).classList.add('ativa');
  }
});

// ===== AIMBOT =====
let aimbotAtivo=false;
const sw=document.getElementById('switchAimbot');

sw.onclick=()=>{
  sw.classList.toggle('ativo');
  aimbotAtivo=sw.classList.contains('ativo');

  if(aimbotAtivo){
    ativarAimbot();
  }else{
    desativarAimbot();
  }
};

function ativarAimbot(){
  console.log("AIMBOT ON");
  // aqui você conecta com o script do jogo (Unity)
}

function desativarAimbot(){
  console.log("AIMBOT OFF");
}

// ===== INFO =====
function atualizarInfo(){
  document.getElementById('fps').textContent =
    Math.floor(Math.random()*180)+60;
  document.getElementById('ping').textContent =
    Math.floor(Math.random()*90)+10+"ms";
  document.getElementById('hora').textContent =
    new Date().toLocaleTimeString("pt-BR",{timeZone:"America/Sao_Paulo"});
}
setInterval(atualizarInfo,1000);
atualizarInfo();
</script>
</body>
</html>
