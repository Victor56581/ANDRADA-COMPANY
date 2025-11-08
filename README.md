# ANDRADA-COMPANY
Site de transporte de carretas basculantes
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>projeto carretas — Painel</title>
<script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;800&display=swap" rel="stylesheet">
<style>
:root{
  --accent:#00ffd6; --accent-2:#00aaff; --muted:#9fbfb4; --bg:#020409;
}
*{box-sizing:border-box;font-family:Poppins, system-ui, -apple-system, 'Segoe UI', Roboto, Arial;color:#e8fff6}
html,body{height:100%;margin:0;background:#000}
body{
  background: url('https://i.postimg.cc/9MDm0vTL/Imagem-do-Whats-App-de-2025-11-06-a-s-07-42-11-0040bd4a.jpg') no-repeat center center fixed;
  background-size: cover;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  overflow:hidden;
}
body::before{content:'';position:fixed;inset:0;background:rgba(0,0,0,0.36);backdrop-filter:blur(5px);z-index:0}

/* Layout */
.stage{position:relative;z-index:2;height:100vh;display:flex;align-items:center;justify-content:center;padding:28px}
.card{width:1000px;max-width:calc(100% - 40px);height:700px;border-radius:16px;display:flex;overflow:hidden;box-shadow:0 40px 120px rgba(0,0,0,0.65);background:linear-gradient(180deg, rgba(0,0,0,0.6), rgba(0,0,0,0.45));}
.left{flex:0 0 460px;padding:36px;display:flex;flex-direction:column;align-items:center;justify-content:center;border-radius:16px;z-index:2}
.left h1{font-size:28px;color:var(--accent);margin-bottom:8px;text-transform:uppercase}
.left p{color:var(--muted);font-size:14px;margin-bottom:16px}
.inp{width:100%;padding:12px;border-radius:12px;background:rgba(255,255,255,0.04);border:1px solid rgba(0,255,200,0.06);color:#eafff6;margin-bottom:10px;font-weight:600}
.btn{width:100%;padding:12px;border-radius:14px;border:none;background:linear-gradient(90deg,var(--accent),var(--accent-2));color:#001;font-weight:800;cursor:pointer;font-size:15px}
.small-note{font-size:12px;color:var(--muted);margin-top:10px;text-align:center}

/* App */
.app-root{position:fixed;inset:0;display:flex;flex-direction:column;z-index:3;background:radial-gradient(1200px 600px at 10% 10%, rgba(0,18,33,0.85) 0%, rgba(0,8,20,0.95) 40%, #000 100%)}
.app-top{height:72px;background:linear-gradient(90deg, rgba(0,255,200,0.03), rgba(0,170,255,0.02));display:flex;align-items:center;justify-content:space-between;padding:0 18px}
.app-top .title{font-weight:800;color:var(--accent);letter-spacing:2px;text-transform:uppercase}
.main-area{flex:1;display:flex;overflow:hidden}
.side-menu{width:300px;background:linear-gradient(180deg,#051217,#07121a);padding:18px;display:flex;flex-direction:column;gap:12px;border-right:1px solid rgba(255,255,255,0.02)}
.menu-btn{background:linear-gradient(90deg,var(--accent-2),var(--accent));border:none;padding:12px;border-radius:10px;color:#001;font-weight:800;cursor:pointer;text-align:left}
.content-area{flex:1;padding:18px;overflow:auto}
.card-panel{background:rgba(0,0,0,0.35);padding:14px;border-radius:12px}
.table-wrap{background:rgba(0,0,0,0.28);padding:12px;border-radius:10px;margin-top:10px}
table{width:100%;border-collapse:collapse}
th,td{padding:10px;border-bottom:1px solid rgba(0,255,200,0.04);text-align:left}
th{color:var(--accent)}
.edit{background:linear-gradient(90deg,#ffd86b,#ffb86b);border:none;padding:6px 8px;border-radius:6px;cursor:pointer}
.del{background:linear-gradient(90deg,#ff6b6b,#ff9b6b);border:none;padding:6px 8px;border-radius:6px;cursor:pointer}
.copy-btn{padding:8px 12px;border-radius:8px;border:none;background:#00c6a6;color:#001;font-weight:700;cursor:pointer}
.notice{padding:10px;border-radius:8px;background:rgba(0,0,0,0.45);margin-top:12px;color:var(--muted)}
.label{font-size:13px;color:var(--muted);margin-bottom:6px}

/* Responsive */
@media (max-width:1100px){
  .card{flex-direction:column;height:auto}
  .left{width:100%}
  .side-menu{width:100%;display:flex;flex-direction:row;overflow:auto}
  .menu-btn{flex:1;white-space:nowrap}
}
</style>
</head>
<body>
  <!-- LOGIN -->
  <div id="loginStage" class="stage" aria-hidden="false">
    <div class="card" role="dialog" aria-label="Login">
      <div class="left">
        <h1>projeto carretas</h1>
        <p>Painel completo — transporte, logística e programação</p>
        <form id="loginForm" onsubmit="event.preventDefault(); doLogin();">
          <input id="inpUser" class="inp" placeholder="Usuário (ex: VICTOR)" autocomplete="username">
          <input id="inpPass" class="inp" placeholder="Senha" type="password" autocomplete="current-password">
          <button class="btn" type="submit">ENTRAR</button>
        </form>
        <div class="small-note">Admin: <strong>VICTOR</strong> / CMPK123 — Visitante: <strong>VISITANTE</strong> / 140205</div>
        <div style="margin-top:8px"><a href="?view=driver" style="color:var(--muted);text-decoration:none">Acessar como motorista (consulta pública)</a></div>
      </div>
      <div style="flex:1;display:flex;align-items:center;justify-content:center;padding-right:40px">
        <div style="width:90%;text-align:center;color:var(--muted)">
          <div style="font-weight:700;color:var(--accent);font-size:18px;margin-bottom:6px">Painel — projeto carretas</div>
          <p style="line-height:1.4">Sistema unificado com motoristas, frentes, programação, relatórios e WhatsApp.</p>
        </div>
      </div>
    </div>
  </div>

  <!-- APP -->
  <div id="appRoot" class="app-root" style="display:none">
    <div class="app-top">
      <div class="title">projeto carretas</div>
      <div style="display:flex;gap:12px;align-items:center">
        <div id="userBadge" style="font-weight:700;color:var(--muted)"></div>
        <button class="menu-btn" onclick="doLogout()">SAIR</button>
      </div>
    </div>

    <div class="main-area">
      <nav class="side-menu" role="navigation" aria-label="Menu principal">
        <button class="menu-btn" onclick="nav('dashboard')">Dashboard</button>
        <button class="menu-btn" onclick="nav('motoristas')">Motoristas</button>
        <button class="menu-btn" onclick="nav('frentes')">Frentes</button>
        <button class="menu-btn" onclick="nav('programacao')">Programação</button>
        <button class="menu-btn" onclick="nav('relatorios')">Relatórios</button>
        <button class="menu-btn" onclick="nav('import')">Importar XLSX</button>
        <button class="menu-btn" onclick="nav('export')">Exportar XLSX</button>
      </nav>

      <main class="content-area" id="contentArea" role="main"></main>
    </div>
  </div>

  <!-- DRIVER MODE (público) -->
  <div id="driverMode" class="stage" style="display:none;z-index:2;align-items:flex-start;padding-top:60px">
    <div class="card" style="width:700px;height:auto;flex-direction:column;padding:20px">
      <h2 style="color:var(--accent);margin:6px 0">Consulta do Motorista</h2>
      <p class="small-note">Abra o link que recebeu e digite seu CPF/CPK</p>
      <input id="inpCPK" class="inp" placeholder="CPF / CPK">
      <div style="display:flex;gap:8px;margin-top:8px">
        <button class="btn" onclick="findDriver()">Ver Programação</button>
        <button class="menu-btn" onclick="backToLogin()">Voltar</button>
      </div>
      <div id="driverResult" style="margin-top:12px"></div>
    </div>
  </div>

<script>
/* =========================
   Keys, helpers & init
   ========================= */
const USERS = [{user:'VICTOR',pass:'CMPK123',role:'admin'},{user:'VISITANTE',pass:'140205',role:'view'}];
const DB_KEY = 'carretas_final_db_v2';
const FRONTS_KEY = 'carretas_final_frentes_v2';
const PROGRAMS_KEY = 'carretas_final_programs_v2';

function saveKey(k,v){ localStorage.setItem(k, JSON.stringify(v)); }
function loadKey(k){ try{ return JSON.parse(localStorage.getItem(k)||'[]'); }catch(e){ return []; } }
function uid(n=8){ return Math.random().toString(36).slice(2,2+n); }
function nowISO(){ return new Date().toISOString().slice(0,19).replace(/[:T]/g,'-'); }

/* initialize storage */
(function init(){
  if(!localStorage.getItem(DB_KEY)) saveKey(DB_KEY, []);
  if(!localStorage.getItem(FRONTS_KEY)) saveKey(FRONTS_KEY, []);
  if(!localStorage.getItem(PROGRAMS_KEY)) saveKey(PROGRAMS_KEY, []);
})();

/* =========================
   CPF validation (BR)
   Accepts formatted or digits; returns true if valid
   ========================= */
function cleanCPF(cpf){
  return (cpf||'').toString().replace(/\D/g,'');
}
function validateCPF(cpf){
  cpf = cleanCPF(cpf);
  if(!cpf || cpf.length !== 11) return false;
  if (/^(\d)\1+$/.test(cpf)) return false; // same digit repeated
  let sum = 0, rem;
  for(let i=1;i<=9;i++) sum += parseInt(cpf.substring(i-1,i)) * (11 - i);
  rem = (sum * 10) % 11; if (rem === 10) rem = 0;
  if (rem !== parseInt(cpf.substring(9,10))) return false;
  sum = 0;
  for(let i=1;i<=10;i++) sum += parseInt(cpf.substring(i-1,i)) * (12 - i);
  rem = (sum * 10) % 11; if (rem === 10) rem = 0;
  if (rem !== parseInt(cpf.substring(10,11))) return false;
  return true;
}

/* =========================
   Auth / Nav
   ========================= */
let CURRENT = null;
function doLogin(){
  const u = (document.getElementById('inpUser').value||'').trim().toUpperCase();
  const p = (document.getElementById('inpPass').value||'').trim();
  const f = USERS.find(x=>x.user===u && x.pass===p);
  if(!f){ alert('Usuário ou senha incorretos'); return; }
  CURRENT = f;
  openApp();
}
function doLogout(){
  CURRENT = null;
  document.getElementById('appRoot').style.display = 'none';
  document.getElementById('driverMode').style.display = 'none';
  document.getElementById('loginStage').style.display = 'flex';
  document.getElementById('inpUser').value=''; document.getElementById('inpPass').value='';
}
function openApp(){
  document.getElementById('loginStage').style.display = 'none';
  document.getElementById('driverMode').style.display = 'none';
  document.getElementById('appRoot').style.display = 'flex';
  document.getElementById('userBadge').textContent = CURRENT.user + (CURRENT.role==='admin' ? ' • ADMIN' : ' • VISITANTE');
  nav('dashboard');
}

function nav(page){
  const area = document.getElementById('contentArea');
  switch(page){
    case 'dashboard': {
      const db = loadKey(DB_KEY), fr = loadKey(FRONTS_KEY), progs = loadKey(PROGRAMS_KEY);
      area.innerHTML = `<h2 style="color:var(--accent)">Dashboard</h2>
        <div class="card-panel">
          <div class="label">Resumo</div>
          <div>Motoristas cadastrados: <strong>${db.length}</strong></div>
          <div>Frentes cadastradas: <strong>${fr.length}</strong></div>
          <div>Programações: <strong>${progs.length}</strong></div>
        </div>`;
      break;
    }
    case 'motoristas': renderMotoristas(); break;
    case 'frentes': renderFrentes(); break;
    case 'programacao': renderProgramacao(); break;
    case 'relatorios': renderRelatorios(); break;
    case 'import': renderImport(); break;
    case 'export': renderExport(); break;
    default: area.innerHTML = '<div>Não implementado</div>';
  }
}

/* =========================
   Motoristas (with CPF validation)
   Fields: nome, cpf, telefone, rg, cnh, veiculo, placa1, placa2, eixos, cap, frenteId, turno, obs
   ========================= */
function renderMotoristas(){
  const fr = loadKey(FRONTS_KEY);
  const options = fr.map(f=>`<option value="${f.id}">${f.name}</option>`).join('');
  document.getElementById('contentArea').innerHTML = `
    <h2 style="color:var(--accent)">Motoristas</h2>
    <div class="card-panel">
      <div class="label">Cadastro</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <input id="mNome" class="inp" placeholder="Motorista">
        <input id="mCPF" class="inp" placeholder="CPF / CPK (somente números)">
        <input id="mTel" class="inp" placeholder="Telefone">
        <input id="mRG" class="inp" placeholder="RG">
        <input id="mCNH" class="inp" placeholder="CNH">
        <input id="mVeic" class="inp" placeholder="Veículo">
        <input id="mPlaca1" class="inp" placeholder="Placa 1">
        <input id="mPlaca2" class="inp" placeholder="Placa 2">
        <input id="mEixos" class="inp" placeholder="Eixos" type="number">
        <input id="mCap" class="inp" placeholder="Capacidade (kg)" type="number">
        <input id="mTurno" class="inp" placeholder="Turno / Data (ex: 2025-11-07 / Manhã)">
        <select id="mFrente" class="inp"><option value="">-- Frente (opcional) --</option>${options}</select>
        <input id="mObs" class="inp" placeholder="Observações">
      </div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <button class="menu-btn" onclick="saveMotorista()">Salvar</button>
        <button class="menu-btn" onclick="clearMotoristaForm()">Limpar</button>
      </div>
    </div>
    <div class="table-wrap"><table id="tblMotoristas"><thead><tr><th>Motorista</th><th>CPF</th><th>Tel</th><th>CNH</th><th>Veículo</th><th>Placas</th><th>Frente</th><th>Turno</th><th>Ações</th></tr></thead><tbody></tbody></table></div>
  `;
  renderMotoristasTable();
}
function saveMotorista(){
  if(!CURRENT || CURRENT.role!=='admin'){ alert('Sem permissão'); return; }
  const nome = (document.getElementById('mNome').value||'').trim(); if(!nome){ alert('Informe o motorista'); return; }
  const cpfRaw = (document.getElementById('mCPF').value||'').trim();
  if(cpfRaw){
    if(!validateCPF(cpfRaw)){ if(!confirm('CPF inválido. Deseja salvar mesmo assim?')) return; }
  }
  const db = loadKey(DB_KEY);
  db.push({
    id: uid(10),
    nome,
    cpf: cpfRaw,
    telefone: (document.getElementById('mTel').value||'').trim(),
    rg: (document.getElementById('mRG').value||'').trim(),
    cnh: (document.getElementById('mCNH').value||'').trim(),
    veiculo: (document.getElementById('mVeic').value||'').trim(),
    placa1: (document.getElementById('mPlaca1').value||'').trim(),
    placa2: (document.getElementById('mPlaca2').value||'').trim(),
    eixos: (document.getElementById('mEixos').value||'').trim(),
    cap: (document.getElementById('mCap').value||'').trim(),
    frenteId: (document.getElementById('mFrente').value||''),
    turno: (document.getElementById('mTurno').value||'').trim(),
    obs: (document.getElementById('mObs').value||'').trim()
  });
  saveKey(DB_KEY, db);
  clearMotoristaForm(); renderMotoristasTable(); alert('Motorista salvo.');
}
function clearMotoristaForm(){ ['mNome','mCPF','mTel','mRG','mCNH','mVeic','mPlaca1','mPlaca2','mEixos','mCap','mFrente','mTurno','mObs'].forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; }); }
function renderMotoristasTable(){
  const tbody = document.querySelector('#tblMotoristas tbody');
  const db = loadKey(DB_KEY); const fr = loadKey(FRONTS_KEY);
  tbody.innerHTML = '';
  db.forEach((r,i)=>{
    const frontName = (fr.find(f=>f.id===r.frenteId)||{name:''}).name;
    const tr = document.createElement('tr');
    tr.innerHTML = `<td>${r.nome}</td><td>${r.cpf||''}</td><td>${r.telefone||''}</td><td>${r.cnh||''}</td><td>${r.veiculo||''}</td><td>${r.placa1||''} / ${r.placa2||''}</td><td>${frontName}</td><td>${r.turno||''}</td>
      <td>${CURRENT && CURRENT.role==='admin' ? `<button class="edit" onclick="editMotorista(${i})">Editar</button> <button class="del" onclick="delMotorista(${i})">Excluir</button>` : '-'}</td>`;
    tbody.appendChild(tr);
  });
}
function editMotorista(i){
  const db = loadKey(DB_KEY); const r = db[i]; if(!r) return;
  ['mNome','mCPF','mTel','mRG','mCNH','mVeic','mPlaca1','mPlaca2','mEixos','mCap','mFrente','mTurno','mObs'].forEach((id,idx)=>{
    const vals = [r.nome,r.cpf,r.telefone,r.rg,r.cnh,r.veiculo,r.placa1,r.placa2,r.eixos,r.cap,r.frenteId,r.turno,r.obs];
    const el = document.getElementById(id); if(el) el.value = vals[idx]||'';
  });
  db.splice(i,1); saveKey(DB_KEY, db); renderMotoristasTable();
}
function delMotorista(i){ if(!confirm('Excluir motorista?')) return; const db = loadKey(DB_KEY); db.splice(i,1); saveKey(DB_KEY, db); renderMotoristasTable(); }

/* =========================
   Frentes
   ========================= */
function renderFrentes(){
  document.getElementById('contentArea').innerHTML = `
    <h2 style="color:var(--accent)">Frentes</h2>
    <div class="card-panel">
      <div class="label">Cadastrar Frente</div>
      <input id="fName" class="inp" placeholder="Nome da frente">
      <input id="fLoc" class="inp" placeholder="Localização (endereço ou link Google Maps)">
      <div style="display:flex;gap:8px;margin-top:8px"><button class="menu-btn" onclick="saveFrente()">Salvar</button><button class="menu-btn" onclick="clearFrenteForm()">Limpar</button></div>
    </div>
    <div class="table-wrap"><table id="tblFrentes"><thead><tr><th>Nome</th><th>Localização</th><th>Ações</th></tr></thead><tbody></tbody></table></div>
  `;
  renderFrentesTable();
}
function saveFrente(){
  if(!CURRENT || CURRENT.role!=='admin'){ alert('Sem permissão'); return; }
  const name = (document.getElementById('fName').value||'').trim(); const loc = (document.getElementById('fLoc').value||'').trim();
  if(!name){ alert('Informe o nome da frente'); return; }
  const fr = loadKey(FRONTS_KEY); fr.push({ id: uid(8), name, loc }); saveKey(FRONTS_KEY, fr); clearFrenteForm(); renderFrentesTable(); alert('Frente salva.');
}
function clearFrenteForm(){ ['fName','fLoc'].forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; }); }
function renderFrentesTable(){
  const tbody = document.querySelector('#tblFrentes tbody'); const fr = loadKey(FRONTS_KEY); tbody.innerHTML='';
  fr.forEach((f,i)=>{ const tr = document.createElement('tr'); tr.innerHTML = `<td>${f.name}</td><td>${f.loc||''}</td><td><button class="edit" onclick="editFrente(${i})">Editar</button> <button class="del" onclick="delFrente(${i})">Excluir</button> <button class="copy-btn" onclick="navigator.clipboard.writeText('${(f.loc||'').replace(/'/g,'\\\'')}').then(()=>alert('Local copiado'))">Copiar Local</button></td>`; tbody.appendChild(tr); });
}
function editFrente(i){ const fr = loadKey(FRONTS_KEY); const f = fr[i]; document.getElementById('fName').value=f.name; document.getElementById('fLoc').value=f.loc||''; fr.splice(i,1); saveKey(FRONTS_KEY,fr); renderFrentesTable(); }
function delFrente(i){ if(!confirm('Excluir frente?')) return; const fr = loadKey(FRONTS_KEY); fr.splice(i,1); saveKey(FRONTS_KEY,fr); renderFrentesTable(); }

/* =========================
   Programação (date picker + whatsapp number)
   ========================= */
function renderProgramacao(){
  const fr = loadKey(FRONTS_KEY);
  if(fr.length===0){ document.getElementById('contentArea').innerHTML = `<h2 style="color:var(--accent)">Programação</h2><div class="notice">Cadastre frentes antes de programar.</div>`; return; }
  const list = fr.map(f=>`<label style="display:block;margin-bottom:6px"><input type="checkbox" data-frontid="${f.id}"> ${f.name} — ${f.loc||''}</label>`).join('');
  const tomorrow = new Date(); tomorrow.setDate(tomorrow.getDate()+1);
  const defaultDate = tomorrow.toISOString().slice(0,10);
  document.getElementById('contentArea').innerHTML = `
    <h2 style="color:var(--accent)">Programação</h2>
    <div class="card-panel">
      <div class="label">Configurar Programação</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <label class="label">Data da Programação</label>
        <input id="progDate" type="date" class="inp" value="${defaultDate}">
        <label class="label">Número WhatsApp (apenas dígitos, ex: 5591999999999)</label>
        <input id="waNumber" class="inp" placeholder="Digite o número que receberá a mensagem (opcional)">
      </div>
      <div style="margin-top:8px">${list}</div>
      <div style="margin-top:12px;display:flex;gap:8px"><button class="menu-btn" onclick="generateProgram()">Gerar Link</button><button class="menu-btn" onclick="showProgramHistory()">Ver Histórico</button></div>
    </div>
    <div id="progOut" style="margin-top:12px"></div>
  `;
}
function generateProgram(){
  const dateVal = document.getElementById('progDate').value;
  if(!dateVal){ alert('Escolha a data da programação'); return; }
  const selected = Array.from(document.querySelectorAll('input[data-frontid]')).filter(i=>i.checked).map(i=>i.getAttribute('data-frontid'));
  if(selected.length===0){ alert('Selecione ao menos 1 frente'); return; }
  const waNumber = (document.getElementById('waNumber').value||'').replace(/\D/g,'');
  const programs = loadKey(PROGRAMS_KEY);
  const id = uid(10);
  const p = { id, date: dateVal, frontIds: selected, createdAt: new Date().toISOString(), waNumber };
  programs.push(p); saveKey(PROGRAMS_KEY, programs);
  const base = location.origin + location.pathname;
  const link = `${base}?view=driver&progId=${id}`;
  const msg = encodeURIComponent(`🚛 Programação (${dateVal})\nAcesse e digite seu CPF/CPK para ver sua escala:\n${link}`);
  // construct wa link: if waNumber provided, direct to that number; else open generic wa.me with text
  const wa = waNumber ? `https://wa.me/${waNumber}?text=${msg}` : `https://wa.me/?text=${msg}`;
  const out = document.getElementById('progOut');
  out.innerHTML = `<div class="notice"><div><strong>Link gerado:</strong></div><div style="word-break:break-all;color:var(--muted);margin-top:6px">${link}</div>
    <div style="margin-top:8px"><button class="copy-btn" onclick="navigator.clipboard.writeText('${link}').then(()=>alert('Link copiado'))">Copiar Link</button>
    <a class="menu-btn" href="${wa}" target="_blank" rel="noopener">Enviar pelo WhatsApp</a></div></div>`;
}

function showProgramHistory(){
  const programs = loadKey(PROGRAMS_KEY);
  const fr = loadKey(FRONTS_KEY);
  const out = document.getElementById('progOut');
  if(programs.length===0){ out.innerHTML = '<div class="notice">Nenhuma programação gerada ainda.</div>'; return; }
  const html = programs.map(p=>{
    const names = p.frontIds.map(id=> (fr.find(f=>f.id===id)||{name:'?' }).name).join(', ');
    const link = location.origin + location.pathname + `?view=driver&progId=${p.id}`;
    const msg = encodeURIComponent(`🚛 Programação (${p.date})\nAcesse e digite seu CPF/CPK para ver sua escala:\n${link}`);
    const wa = p.waNumber ? `https://wa.me/${p.waNumber}?text=${msg}` : `https://wa.me/?text=${msg}`;
    return `<div style="margin-bottom:10px;padding:10px;border-radius:8px;background:rgba(0,0,0,0.35)">
      <div><strong>Data:</strong> ${p.date} — <strong>Frentes:</strong> ${names}</div>
      <div style="margin-top:6px"><code style="color:var(--muted);word-break:break-all">${link}</code></div>
      <div style="margin-top:8px"><button class="copy-btn" onclick="navigator.clipboard.writeText('${link}').then(()=>alert('Link copiado'))">Copiar</button>
        <a class="menu-btn" href="${wa}" target="_blank" rel="noopener">Enviar pelo WhatsApp</a>
        <button class="menu-btn" onclick="revokeProgram('${p.id}')">Revogar</button></div>
    </div>`;
  }).join('');
  out.innerHTML = html;
}
function revokeProgram(id){ if(!confirm('Revogar este link?')) return; let progs = loadKey(PROGRAMS_KEY); progs = progs.filter(p=>p.id!==id); saveKey(PROGRAMS_KEY, progs); showProgramHistory(); }

/* =========================
   Relatórios
   ========================= */
function renderRelatorios(){
  const db = loadKey(DB_KEY), fr = loadKey(FRONTS_KEY), progs = loadKey(PROGRAMS_KEY);
  document.getElementById('contentArea').innerHTML = `
    <h2 style="color:var(--accent)">Relatórios</h2>
    <div class="card-panel">
      <div class="label">Resumo completo</div>
      <div>Motoristas: <strong>${db.length}</strong></div>
      <div>Frentes: <strong>${fr.length}</strong></div>
      <div>Programações: <strong>${progs.length}</strong></div>
      <div style="margin-top:8px"><button class="menu-btn" onclick="downloadFullReport()">Baixar relatório (CSV)</button></div>
    </div>
  `;
}
function downloadFullReport(){
  const db = loadKey(DB_KEY);
  if(!db.length){ alert('Sem dados'); return; }
  const header = ['Motorista','CPF','Telefone','RG','CNH','Veículo','Placa1','Placa2','Eixos','Capacidade','FrenteId','Turno','Observações'];
  const rows = db.map(r => [r.nome,r.cpf,r.telefone,r.rg,r.cnh,r.veiculo,r.placa1,r.placa2,r.eixos,r.cap,r.frenteId,r.turno,r.obs].map(v=>`"${String(v||'').replace(/"/g,'""')}"`).join(','));
  const csv = [header.join(','), ...rows].join('\r\n');
  const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href = url; a.download = 'carretas_relatorio_'+nowISO()+'.csv'; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
}

/* =========================
   Import / Export XLSX
   ========================= */
function renderImport(){
  document.getElementById('contentArea').innerHTML = `
    <h2 style="color:var(--accent)">Importar XLSX</h2>
    <p class="small-note">Planilha: Motorista, CPF, Telefone, RG, CNH, Veiculo, Placa1, Placa2, Eixos, Capacidade, FrenteID, Turno, Obs</p>
    <input type="file" id="xlsxFile" accept=".xlsx" class="inp">
    <div style="margin-top:8px"><button class="menu-btn" onclick="importXLS()">Importar</button></div>
    <div class="table-wrap"><table id="tblPreview"><thead><tr><th>Motorista</th><th>CPF</th><th>Telefone</th><th>RG</th><th>CNH</th><th>Veiculo</th><th>Placa1</th><th>Placa2</th><th>Eixos</th><th>Cap</th><th>FrenteID</th><th>Turno</th><th>Obs</th></tr></thead><tbody></tbody></table></div>
  `;
}
function importXLS(){
  const f = document.getElementById('xlsxFile').files[0];
  if(!f){ alert('Selecione um arquivo'); return; }
  const reader = new FileReader();
  reader.onload = function(e){
    const data = new Uint8Array(e.target.result);
    const wb = XLSX.read(data,{type:'array'});
    const ws = wb.Sheets[wb.SheetNames[0]];
    const json = XLSX.utils.sheet_to_json(ws,{header:["Motorista","CPF","Telefone","RG","CNH","Veiculo","Placa1","Placa2","Eixos","Capacidade","FrenteID","Turno","Obs"],range:1});
    const tbody = document.querySelector('#tblPreview tbody'); tbody.innerHTML = '';
    json.forEach(r=>{
      const tr = document.createElement('tr');
      tr.innerHTML = `<td>${r.Motorista||''}</td><td>${r.CPF||''}</td><td>${r.Telefone||''}</td><td>${r.RG||''}</td><td>${r.CNH||''}</td><td>${r.Veiculo||''}</td><td>${r.Placa1||''}</td><td>${r.Placa2||''}</td><td>${r.Eixos||''}</td><td>${r.Capacidade||''}</td><td>${r.FrenteID||''}</td><td>${r.Turno||''}</td><td>${r.Obs||''}</td>`;
      tbody.appendChild(tr);
    });
    if(confirm('Importar todos os registros para o banco local?')){
      const db = loadKey(DB_KEY);
      json.forEach(r=>db.push({
        id: uid(10),
        nome: r.Motorista||'',
        cpf: r.CPF||'',
        telefone: r.Telefone||'',
        rg: r.RG||'',
        cnh: r.CNH||'',
        veiculo: r.Veiculo||'',
        placa1: r.Placa1||'',
        placa2: r.Placa2||'',
        eixos: r.Eixos||'',
        cap: r.Capacidade||'',
        frenteId: r.FrenteID||'',
        turno: r.Turno||'',
        obs: r.Obs||''
      }));
      saveKey(DB_KEY, db);
      alert('Importação concluída');
      nav('motoristas');
    }
  };
  reader.readAsArrayBuffer(f);
}
function renderExport(){ document.getElementById('contentArea').innerHTML = `<h2 style="color:var(--accent)">Exportar XLSX</h2><button class="menu-btn" onclick="exportXLS()">Exportar XLSX</button>`; }
function exportXLS(){
  const db = loadKey(DB_KEY);
  if(!db.length){ alert('Sem dados'); return; }
  const rows = db.map(r=>({Motorista:r.nome,CPF:r.cpf,Telefone:r.telefone,RG:r.rg,CNH:r.cnh,Veiculo:r.veiculo,Placa1:r.placa1,Placa2:r.placa2,Eixos:r.eixos,Capacidade:r.cap,FrenteID:r.frenteId,Turno:r.turno,Obs:r.obs}));
  const ws = XLSX.utils.json_to_sheet(rows);
  const wb = XLSX.utils.book_new(); XLSX.utils.book_append_sheet(wb,ws,'Motoristas'); XLSX.writeFile(wb,'carretas_export_'+nowISO()+'.xlsx');
}

/* =========================
   Driver (public) view
   ========================= */
function backToLogin(){ document.getElementById('driverMode').style.display='none'; document.getElementById('loginStage').style.display='flex'; }

function findDriver(){
  const cpf = (document.getElementById('inpCPK').value||'').trim();
  const res = document.getElementById('driverResult'); res.innerHTML='';
  if(!cpf){ alert('Digite seu CPF/CPK'); return; }
  const db = loadKey(DB_KEY);
  const driver = db.find(d=> d.cpf === cpf || (d.nome && d.nome.toUpperCase().includes(cpf.toUpperCase())));
  if(!driver){ res.innerHTML = `<div class="notice" style="color:#ff6b6b">Motorista não encontrado.</div>`; return; }
  const params = new URLSearchParams(location.search);
  const progId = params.get('progId');
  if(progId){
    const progs = loadKey(PROGRAMS_KEY); const p = progs.find(x=>x.id===progId);
    if(!p){ res.innerHTML = `<div class="notice" style="color:#ff6b6b">Programação inválida.</div>`; return; }
    if(!p.frontIds.includes(driver.frenteId)){ res.innerHTML = `<div class="notice" style="color:#ff6b6b">Você não está escalado para as frentes desta programação (${p.date}).</div>`; return; }
    showDriverProgram(driver, true, p.date);
    return;
  }
  showDriverProgram(driver, false, null);
}

function showDriverProgram(driver, isProgram=false, dateStr=null){
  const fr = loadKey(FRONTS_KEY);
  const frente = fr.find(f=>f.id===driver.frenteId) || null;
  const mapLoc = frente ? (frente.loc || frente.name) : '';
  const title = isProgram ? `Programação para ${dateStr}` : 'Seus dados';
  const res = document.getElementById('driverResult');
  res.innerHTML = `
    <div style="padding:12px;border-radius:10px;background:rgba(0,0,0,0.35)">
      <h3 style="color:var(--accent);margin:6px 0">${title}</h3>
      <p><b>Motorista:</b> ${driver.nome}</p>
      <p><b>CPF/CPK:</b> ${driver.cpf||''}</p>
      <p><b>Telefone:</b> ${driver.telefone||''}</p>
      <p><b>Veículo:</b> ${driver.veiculo||''}</p>
      <p><b>Placas:</b> ${driver.placa1||''} / ${driver.placa2||''}</p>
      <p><b>Turno:</b> ${driver.turno||''} &nbsp; <b>Observações:</b> ${driver.obs||''}</p>
      <p><b>Frente:</b> ${frente ? frente.name : (driver.frenteId ? driver.frenteId : 'Nenhuma')}</p>
      <p><b>Localização:</b> ${mapLoc||'—'}</p>
      ${mapLoc ? `<iframe width="100%" height="300" style="border-radius:10px;border:none;margin-top:8px" src="https://www.google.com/maps?q=${encodeURIComponent(mapLoc)}&output=embed"></iframe>` : ''}
    </div>
  `;
}

/* =========================
   URL param detection on load
   ========================= */
window.onload = function(){
  const params = new URLSearchParams(location.search);
  if(params.get('view') === 'driver'){
    document.getElementById('loginStage').style.display = 'none';
    document.getElementById('appRoot').style.display = 'none';
    document.getElementById('driverMode').style.display = 'flex';
    return;
  }
  document.getElementById('loginStage').style.display = 'flex';
};

</script>
</body>
</html>

