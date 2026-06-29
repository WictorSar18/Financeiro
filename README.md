<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Controle Financeiro</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.19.0/dist/tabler-icons.min.css">
<style>
  :root {
    --bg: #f5f5f3;
    --surface-0: #ebebea;
    --surface-1: #f0f0ee;
    --surface-2: #ffffff;
    --text-primary: #1a1a18;
    --text-secondary: #5a5a56;
    --text-muted: #8a8a86;
    --border: rgba(0,0,0,0.12);
    --border-strong: rgba(0,0,0,0.2);
    --radius: 8px;
    --text-success: #0f6e56;
    --bg-success: #e1f5ee;
    --fill-success: #1D9E75;
    --on-success: #fff;
    --border-success: #5DCAA5;
    --text-danger: #993c1d;
    --bg-danger: #faece7;
    --fill-danger: #D85A30;
    --on-danger: #fff;
    --border-danger: #F0997B;
    --text-accent: #185fa5;
    --bg-accent: #e6f1fb;
    --fill-accent: #378ADD;
    --on-accent: #fff;
    --border-accent: #85B7EB;
    --text-pro: #3c3489;
    --bg-pro: #eeedfe;
    --text-warning: #854f0b;
    --bg-warning: #faeeda;
  }
  @media (prefers-color-scheme: dark) {
    :root {
      --bg: #1a1a18;
      --surface-0: #222220;
      --surface-1: #2a2a28;
      --surface-2: #333330;
      --text-primary: #f0f0ee;
      --text-secondary: #aaaaaa;
      --text-muted: #777774;
      --border: rgba(255,255,255,0.1);
      --border-strong: rgba(255,255,255,0.2);
      --text-success: #5DCAA5;
      --bg-success: #04342c;
      --border-success: #0F6E56;
      --text-danger: #F0997B;
      --bg-danger: #4A1B0C;
      --border-danger: #993C1D;
      --text-accent: #85B7EB;
      --bg-accent: #042C53;
      --border-accent: #185FA5;
      --text-pro: #AFA9EC;
      --bg-pro: #26215C;
      --text-warning: #EF9F27;
      --bg-warning: #412402;
    }
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; background: var(--bg); color: var(--text-primary); min-height: 100vh; }

  header { background: var(--surface-2); border-bottom: 0.5px solid var(--border); padding: 12px 20px; display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; z-index: 10; }
  header h1 { font-size: 16px; font-weight: 600; display: flex; align-items: center; gap: 8px; }
  header h1 i { color: var(--text-accent); }
  .header-right { font-size: 12px; color: var(--text-muted); }

  .container { max-width: 800px; margin: 0 auto; padding: 1rem; }

  /* NAV MÊS */
  .nav-mes { display: flex; align-items: center; justify-content: space-between; background: var(--surface-2); border: 0.5px solid var(--border); border-radius: var(--radius); padding: 10px 14px; margin-bottom: 1rem; }
  .nav-mes button { background: none; border: 0.5px solid var(--border); border-radius: var(--radius); padding: 5px 12px; cursor: pointer; color: var(--text-primary); font-size: 13px; }
  .nav-mes button:hover { background: var(--surface-1); }
  .nav-mes .mes-label { font-size: 16px; font-weight: 600; color: var(--text-primary); }

  /* RESUMO */
  .sum-grid { display: grid; grid-template-columns: repeat(4, minmax(0,1fr)); gap: 8px; margin-bottom: 1rem; }
  .sum-card { background: var(--surface-2); border: 0.5px solid var(--border); border-radius: var(--radius); padding: 12px 14px; }
  .sum-lbl { font-size: 11px; color: var(--text-muted); margin-bottom: 4px; }
  .sum-val { font-size: 18px; font-weight: 600; }
  .c-g { color: var(--text-success); } .c-r { color: var(--text-danger); }
  .c-b { color: var(--text-accent); } .c-n { color: var(--text-primary); }

  /* TABS */
  .tabs { display: flex; gap: 3px; background: var(--surface-1); border: 0.5px solid var(--border); border-radius: var(--radius); padding: 3px; margin-bottom: 1rem; overflow-x: auto; }
  .tab { flex: 1; min-width: max-content; padding: 8px 10px; border: none; background: transparent; border-radius: 6px; font-size: 12px; color: var(--text-secondary); cursor: pointer; white-space: nowrap; }
  .tab.on { background: var(--surface-2); color: var(--text-primary); font-weight: 500; border: 0.5px solid var(--border); }

  .sec { display: none; } .sec.on { display: block; }

  /* CARD */
  .card { background: var(--surface-2); border: 0.5px solid var(--border); border-radius: 12px; padding: 1rem 1.1rem; margin-bottom: .75rem; }
  .card-h { font-size: 13px; font-weight: 600; color: var(--text-primary); margin-bottom: 12px; display: flex; align-items: center; gap: 6px; }
  .card-h i { color: var(--text-muted); font-size: 15px; }

  /* FORM */
  .fg { display: flex; flex-wrap: wrap; gap: 6px; align-items: flex-end; margin-bottom: 8px; }
  .fi { display: flex; flex-direction: column; gap: 4px; }
  .fi label { font-size: 11px; color: var(--text-muted); font-weight: 500; }
  .fi input, .fi select {
    font-family: inherit; font-size: 13px; height: 36px; padding: 0 10px;
    border: 0.5px solid var(--border); border-radius: var(--radius);
    background: var(--surface-1); color: var(--text-primary); min-width: 0;
    outline: none;
  }
  .fi input:focus, .fi select:focus { border-color: var(--border-accent); box-shadow: 0 0 0 3px var(--bg-accent); }
  .fi.w1 { flex: 1; min-width: 120px; } .fi.w2 { width: 110px; } .fi.w3 { width: 80px; }
  .btn-a {
    height: 36px; padding: 0 16px; border-radius: var(--radius); cursor: pointer;
    font-size: 13px; font-family: inherit; white-space: nowrap; flex-shrink: 0;
    background: var(--bg-accent); border: 0.5px solid var(--border-accent); color: var(--text-accent);
  }
  .btn-a:hover { background: var(--fill-accent); color: var(--on-accent); }
  .btn-a.green { background: var(--bg-success); border-color: var(--border-success); color: var(--text-success); }
  .btn-a.green:hover { background: var(--fill-success); color: var(--on-success); }

  /* TABLE */
  .tbl-wrap { overflow-x: auto; }
  table { width: 100%; border-collapse: collapse; font-size: 12px; min-width: 400px; }
  th { text-align: left; color: var(--text-muted); font-weight: 500; font-size: 11px; padding: 4px 8px 8px; border-bottom: 0.5px solid var(--border); white-space: nowrap; }
  td { padding: 8px; border-bottom: 0.5px solid var(--border); color: var(--text-primary); overflow: hidden; text-overflow: ellipsis; white-space: nowrap; vertical-align: middle; max-width: 160px; }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: var(--surface-1); }
  .empty { text-align: center; color: var(--text-muted); font-size: 12px; padding: 2rem; max-width: none; }

  /* BADGE */
  .badge { display: inline-block; padding: 2px 8px; border-radius: 20px; font-size: 10px; font-weight: 600; }
  .bd { background: var(--bg-accent); color: var(--text-accent); }
  .bc { background: var(--bg-pro); color: var(--text-pro); }
  .bp { background: var(--bg-success); color: var(--text-success); }
  .bm { background: var(--bg-warning); color: var(--text-warning); }

  /* BAR */
  .bar-wrap { width: 100%; background: var(--surface-0); border-radius: 20px; height: 5px; overflow: hidden; margin-top: 4px; }
  .bar-f { height: 100%; border-radius: 20px; transition: width .4s; }

  .fix-badge { font-size: 10px; background: var(--bg-danger); color: var(--text-danger); border-radius: 20px; padding: 1px 7px; }
  .parc-tag { font-size: 10px; color: var(--text-muted); }
  .row-del { padding: 0 8px; height: 26px; background: transparent; border: none; color: var(--text-muted); cursor: pointer; font-size: 14px; border-radius: 4px; }
  .row-del:hover { color: var(--text-danger); background: var(--bg-danger); }

  .parc-info { font-size: 11px; color: var(--text-muted); margin-top: 4px; }

  .save-bar { background: var(--bg-success); border: 0.5px solid var(--border-success); color: var(--text-success); border-radius: var(--radius); padding: 8px 14px; font-size: 12px; display: flex; align-items: center; gap: 8px; margin-bottom: 1rem; }

  @media (max-width: 600px) {
    .sum-grid { grid-template-columns: repeat(2, 1fr); }
    .fi.w2 { width: 100%; } .fi.w3 { width: 80px; }
  }
</style>
</head>
<body>

<header>
  <h1><i class="ti ti-report-money"></i> Controle Financeiro</h1>
  <div class="header-right">Dados salvos no navegador</div>
</header>

<div class="container">

  <div class="nav-mes">
    <button onclick="mudaMes(-1)"><i class="ti ti-chevron-left"></i> Anterior</button>
    <span class="mes-label" id="lbl-mes">—</span>
    <button onclick="mudaMes(1)">Próximo <i class="ti ti-chevron-right"></i></button>
  </div>

  <div class="sum-grid">
    <div class="sum-card"><div class="sum-lbl">Receitas</div><div class="sum-val c-g" id="s-rec">R$ 0</div></div>
    <div class="sum-card"><div class="sum-lbl">Gastos</div><div class="sum-val c-r" id="s-gas">R$ 0</div></div>
    <div class="sum-card"><div class="sum-lbl">Investido</div><div class="sum-val c-b" id="s-inv">R$ 0</div></div>
    <div class="sum-card"><div class="sum-lbl">Saldo livre</div><div class="sum-val c-n" id="s-sal">R$ 0</div></div>
  </div>

  <div class="tabs">
    <button class="tab on" onclick="showTab('gastos')" id="tab-gastos"><i class="ti ti-receipt"></i> Gastos</button>
    <button class="tab" onclick="showTab('fixos')" id="tab-fixos"><i class="ti ti-repeat"></i> Fixos</button>
    <button class="tab" onclick="showTab('receitas')" id="tab-receitas"><i class="ti ti-cash"></i> Receitas</button>
    <button class="tab" onclick="showTab('invest')" id="tab-invest"><i class="ti ti-trending-up"></i> Investimentos</button>
    <button class="tab" onclick="showTab('cats')" id="tab-cats"><i class="ti ti-chart-pie"></i> Por categoria</button>
  </div>

  <!-- GASTOS -->
  <div class="sec on" id="sec-gastos">
    <div class="card">
      <div class="card-h"><i class="ti ti-plus-circle"></i> Novo gasto</div>
      <div class="fg">
        <div class="fi w1"><label>Descrição</label><input id="g-desc" placeholder="Ex: Mercado Extra"></div>
        <div class="fi w2"><label>Categoria</label>
          <select id="g-cat">
            <option>Mercado</option><option>Farmácia</option><option>Delivery</option>
            <option>Restaurante</option><option>Combustível</option><option>Transporte</option>
            <option>Saúde</option><option>Educação</option><option>Lazer</option>
            <option>Vestuário</option><option>Casa</option><option>Pets</option>
            <option>Assinatura</option><option>Outros</option>
          </select>
        </div>
      </div>
      <div class="fg">
        <div class="fi w2"><label>Pagamento</label>
          <select id="g-pag">
            <option value="Débito">Débito</option><option value="Crédito">Crédito</option>
            <option value="PIX">PIX</option><option value="Dinheiro">Dinheiro</option>
          </select>
        </div>
        <div class="fi w2"><label>Valor total (R$)</label><input type="number" id="g-val" placeholder="0,00" min="0" step="0.01"></div>
        <div class="fi w3"><label>Parcelas</label><input type="number" id="g-parc" placeholder="1" min="1" max="72" value="1"></div>
        <div class="fi" style="width:110px"><label>Data</label><input type="date" id="g-data"></div>
        <button class="btn-a" onclick="addGasto()"><i class="ti ti-plus"></i> Adicionar</button>
      </div>
      <div class="parc-info" id="parc-info"></div>
    </div>
    <div class="card">
      <div class="card-h"><i class="ti ti-list"></i> Lançamentos do mês</div>
      <div class="tbl-wrap">
        <table>
          <thead><tr>
            <th style="width:28%">Descrição</th>
            <th style="width:18%">Categoria</th>
            <th style="width:13%">Pagto</th>
            <th style="width:17%">Valor</th>
            <th style="width:16%">Parcela</th>
            <th style="width:8%"></th>
          </tr></thead>
          <tbody id="tbl-gastos"></tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- FIXOS -->
  <div class="sec" id="sec-fixos">
    <div class="card">
      <div class="card-h"><i class="ti ti-repeat"></i> Novo custo fixo <span style="font-size:11px;color:var(--text-muted);font-weight:400;margin-left:4px">— aparece automaticamente todo mês</span></div>
      <div class="fg">
        <div class="fi w1"><label>Descrição</label><input id="f-desc" placeholder="Ex: Aluguel, Netflix, Academia..."></div>
        <div class="fi w2"><label>Categoria</label>
          <select id="f-cat">
            <option>Moradia</option><option>Energia</option><option>Água</option>
            <option>Internet</option><option>Telefone</option><option>Streaming</option>
            <option>Seguro</option><option>Plano de saúde</option><option>Escola</option>
            <option>Academia</option><option>Outros fixos</option>
          </select>
        </div>
        <div class="fi w2"><label>Pagamento</label>
          <select id="f-pag">
            <option value="Débito">Débito</option><option value="Crédito">Crédito</option>
            <option value="PIX">PIX</option><option value="Dinheiro">Dinheiro</option>
          </select>
        </div>
        <div class="fi w2"><label>Valor/mês (R$)</label><input type="number" id="f-val" placeholder="0,00" min="0" step="0.01"></div>
        <button class="btn-a" onclick="addFixo()"><i class="ti ti-plus"></i> Adicionar</button>
      </div>
    </div>
    <div class="card">
      <div class="card-h"><i class="ti ti-list"></i> Custos fixos cadastrados</div>
      <div class="tbl-wrap">
        <table>
          <thead><tr>
            <th style="width:33%">Descrição</th>
            <th style="width:22%">Categoria</th>
            <th style="width:16%">Pagto</th>
            <th style="width:21%">Valor/mês</th>
            <th style="width:8%"></th>
          </tr></thead>
          <tbody id="tbl-fixos"></tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- RECEITAS -->
  <div class="sec" id="sec-receitas">
    <div class="card">
      <div class="card-h"><i class="ti ti-cash"></i> Nova receita</div>
      <div class="fg">
        <div class="fi w1"><label>Descrição</label><input id="r-desc" placeholder="Ex: Salário, Freelance, Renda extra..."></div>
        <div class="fi w2"><label>Valor (R$)</label><input type="number" id="r-val" placeholder="0,00" min="0" step="0.01"></div>
        <button class="btn-a green" onclick="addReceita()"><i class="ti ti-plus"></i> Adicionar</button>
      </div>
    </div>
    <div class="card">
      <div class="card-h"><i class="ti ti-list"></i> Entradas do mês</div>
      <div class="tbl-wrap">
        <table>
          <thead><tr>
            <th style="width:62%">Descrição</th>
            <th style="width:30%">Valor</th>
            <th style="width:8%"></th>
          </tr></thead>
          <tbody id="tbl-receitas"></tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- INVESTIMENTOS -->
  <div class="sec" id="sec-invest">
    <div class="card">
      <div class="card-h"><i class="ti ti-trending-up"></i> Novo investimento</div>
      <div class="fg">
        <div class="fi w1"><label>Nome</label><input id="i-nome" placeholder="Ex: Tesouro Direto, CDB, Ações..."></div>
        <div class="fi w2"><label>Tipo</label>
          <select id="i-tipo">
            <option>Renda Fixa</option><option>Renda Variável</option>
            <option>Cripto</option><option>Fundos</option><option>Ações</option><option>Outro</option>
          </select>
        </div>
        <div class="fi w2"><label>Valor (R$)</label><input type="number" id="i-val" placeholder="0,00" min="0" step="0.01"></div>
        <button class="btn-a" onclick="addInvest()"><i class="ti ti-plus"></i> Adicionar</button>
      </div>
    </div>
    <div class="card">
      <div class="card-h"><i class="ti ti-list"></i> Investimentos do mês</div>
      <div class="tbl-wrap">
        <table>
          <thead><tr>
            <th style="width:44%">Nome</th>
            <th style="width:28%">Tipo</th>
            <th style="width:20%">Valor</th>
            <th style="width:8%"></th>
          </tr></thead>
          <tbody id="tbl-invest"></tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- CATEGORIAS -->
  <div class="sec" id="sec-cats">
    <div class="card">
      <div class="card-h"><i class="ti ti-chart-pie"></i> Gastos por categoria</div>
      <div id="cat-bars"><p class="empty">Nenhum gasto registrado neste mês</p></div>
    </div>
    <div class="card">
      <div class="card-h"><i class="ti ti-credit-card"></i> Por forma de pagamento</div>
      <div id="pag-bars"><p class="empty">Nenhum gasto registrado neste mês</p></div>
    </div>
  </div>

</div><!-- /container -->

<script>
const MESES = ['Janeiro','Fevereiro','Março','Abril','Maio','Junho','Julho','Agosto','Setembro','Outubro','Novembro','Dezembro'];
const CAT_COLORS = {
  'Mercado':'#1D9E75','Farmácia':'#E24B4A','Delivery':'#EF9F27','Restaurante':'#D85A30',
  'Combustível':'#378ADD','Transporte':'#185FA5','Saúde':'#7F77DD','Educação':'#534AB7',
  'Lazer':'#D4537E','Vestuário':'#993556','Casa':'#639922','Pets':'#7a4f1d',
  'Assinatura':'#0F6E56','Outros':'#888780','Moradia':'#3B6D11','Energia':'#BA7517',
  'Água':'#1D9E75','Internet':'#378ADD','Telefone':'#185FA5','Streaming':'#7F77DD',
  'Seguro':'#E24B4A','Plano de saúde':'#D85A30','Escola':'#534AB7',
  'Academia':'#D4537E','Outros fixos':'#888780'
};
const PAG_CLASS = {'Débito':'bd','Crédito':'bc','PIX':'bp','Dinheiro':'bm'};

let now = new Date();
let curY = now.getFullYear();
let curM = now.getMonth();
let data = {};
let fixos = [];

function mesKey(y,m){ return y+'-'+String(m).padStart(2,'0'); }
function getMes(y,m){ const k=mesKey(y,m); if(!data[k]) data[k]={gastos:[],receitas:[],invest:[]}; return data[k]; }
function fmt(v){ return 'R$ '+Number(v).toLocaleString('pt-BR',{minimumFractionDigits:2,maximumFractionDigits:2}); }

function salvarDados(){
  try {
    localStorage.setItem('cf_data', JSON.stringify(data));
    localStorage.setItem('cf_fixos', JSON.stringify(fixos));
  } catch(e) {}
}
function carregarDados(){
  try {
    const d = localStorage.getItem('cf_data');
    const f = localStorage.getItem('cf_fixos');
    if(d) data = JSON.parse(d);
    if(f) fixos = JSON.parse(f);
  } catch(e) {}
}

function mudaMes(d){ curM+=d; if(curM>11){curM=0;curY++;} if(curM<0){curM=11;curY--;} render(); }

function showTab(name){
  document.querySelectorAll('.sec').forEach(s=>s.classList.remove('on'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('on'));
  document.getElementById('sec-'+name).classList.add('on');
  document.getElementById('tab-'+name).classList.add('on');
}

document.getElementById('g-data').value = new Date().toISOString().split('T')[0];
['g-parc','g-val'].forEach(id => document.getElementById(id).addEventListener('input', updParcInfo));

function updParcInfo(){
  const parc = parseInt(document.getElementById('g-parc').value)||1;
  const val = parseFloat(document.getElementById('g-val').value)||0;
  const info = document.getElementById('parc-info');
  info.textContent = (parc>1&&val>0) ? `Parcela mensal: ${fmt(val/parc)} × ${parc} meses = ${fmt(val)} no total` : '';
}

function addGasto(){
  const desc = document.getElementById('g-desc').value.trim();
  const cat = document.getElementById('g-cat').value;
  const pag = document.getElementById('g-pag').value;
  const val = parseFloat(document.getElementById('g-val').value);
  const parcTotal = parseInt(document.getElementById('g-parc').value)||1;
  const dataStr = document.getElementById('g-data').value;
  if(!desc||isNaN(val)||val<=0) return;
  const parcVal = val/parcTotal;
  const base = dataStr ? new Date(dataStr+'T12:00:00') : new Date();
  for(let p=0;p<parcTotal;p++){
    let pm=base.getMonth()+p, py=base.getFullYear();
    while(pm>11){pm-=12;py++;}
    const mk=mesKey(py,pm);
    if(!data[mk]) data[mk]={gastos:[],receitas:[],invest:[]};
    data[mk].gastos.push({id:Date.now()+p,desc,cat,pag,valor:parcVal,parcAtual:p+1,parcTotal,fixo:false});
  }
  document.getElementById('g-desc').value='';
  document.getElementById('g-val').value='';
  document.getElementById('g-parc').value='1';
  document.getElementById('parc-info').textContent='';
  salvarDados(); render();
}

function addFixo(){
  const desc=document.getElementById('f-desc').value.trim();
  const cat=document.getElementById('f-cat').value;
  const pag=document.getElementById('f-pag').value;
  const val=parseFloat(document.getElementById('f-val').value);
  if(!desc||isNaN(val)||val<=0) return;
  fixos.push({id:Date.now(),desc,cat,pag,valor:val});
  document.getElementById('f-desc').value='';
  document.getElementById('f-val').value='';
  salvarDados(); render();
}

function addReceita(){
  const desc=document.getElementById('r-desc').value.trim();
  const val=parseFloat(document.getElementById('r-val').value);
  if(!desc||isNaN(val)||val<=0) return;
  getMes(curY,curM).receitas.push({id:Date.now(),desc,valor:val});
  document.getElementById('r-desc').value='';
  document.getElementById('r-val').value='';
  salvarDados(); render();
}

function addInvest(){
  const nome=document.getElementById('i-nome').value.trim();
  const tipo=document.getElementById('i-tipo').value;
  const val=parseFloat(document.getElementById('i-val').value);
  if(!nome||isNaN(val)||val<=0) return;
  getMes(curY,curM).invest.push({id:Date.now(),nome,tipo,valor:val});
  document.getElementById('i-nome').value='';
  document.getElementById('i-val').value='';
  salvarDados(); render();
}

function delGasto(id){ const m=getMes(curY,curM); m.gastos=m.gastos.filter(g=>g.id!==id); salvarDados(); render(); }
function delFixo(id){ fixos=fixos.filter(f=>f.id!==id); salvarDados(); render(); }
function delReceita(id){ const m=getMes(curY,curM); m.receitas=m.receitas.filter(r=>r.id!==id); salvarDados(); render(); }
function delInvest(id){ const m=getMes(curY,curM); m.invest=m.invest.filter(i=>i.id!==id); salvarDados(); render(); }

function render(){
  document.getElementById('lbl-mes').textContent = MESES[curM]+' '+curY;
  const m = getMes(curY,curM);
  const todosGastos = [...m.gastos, ...fixos.map(f=>({...f,fixo:true,parcAtual:null,parcTotal:null}))];

  const totR=m.receitas.reduce((a,i)=>a+i.valor,0);
  const totG=todosGastos.reduce((a,i)=>a+i.valor,0);
  const totI=m.invest.reduce((a,i)=>a+i.valor,0);
  const sal=totR-totG-totI;
  document.getElementById('s-rec').textContent=fmt(totR);
  document.getElementById('s-gas').textContent=fmt(totG);
  document.getElementById('s-inv').textContent=fmt(totI);
  const se=document.getElementById('s-sal');
  se.textContent=fmt(sal);
  se.className='sum-val '+(sal>=0?'c-g':'c-r');

  // Tabela gastos
  const tg=document.getElementById('tbl-gastos');
  if(!todosGastos.length){ tg.innerHTML='<tr><td colspan="6" class="empty">Nenhum gasto neste mês</td></tr>'; }
  else tg.innerHTML=todosGastos.map(g=>{
    const catC=CAT_COLORS[g.cat]||'#888';
    const pagC=PAG_CLASS[g.pag]||'';
    const parcStr=g.fixo?'<span class="fix-badge">fixo</span>':g.parcTotal>1?`<span class="parc-tag">${g.parcAtual}/${g.parcTotal}</span>`:'—';
    const delBtn=g.fixo?`<button class="row-del" onclick="delFixo(${g.id})" title="Remover fixo"><i class="ti ti-trash"></i></button>`:`<button class="row-del" onclick="delGasto(${g.id})"><i class="ti ti-trash"></i></button>`;
    return `<tr><td title="${g.desc}">${g.desc}</td><td><span class="badge" style="background:${catC}22;color:${catC}">${g.cat}</span></td><td><span class="badge ${pagC}">${g.pag}</span></td><td style="color:var(--text-danger);font-weight:600">${fmt(g.valor)}</td><td>${parcStr}</td><td>${delBtn}</td></tr>`;
  }).join('');

  // Tabela fixos
  const tf=document.getElementById('tbl-fixos');
  if(!fixos.length){ tf.innerHTML='<tr><td colspan="5" class="empty">Nenhum custo fixo cadastrado</td></tr>'; }
  else tf.innerHTML=fixos.map(f=>{
    const catC=CAT_COLORS[f.cat]||'#888';
    const pagC=PAG_CLASS[f.pag]||'';
    return `<tr><td>${f.desc}</td><td><span class="badge" style="background:${catC}22;color:${catC}">${f.cat}</span></td><td><span class="badge ${pagC}">${f.pag}</span></td><td style="font-weight:600">${fmt(f.valor)}</td><td><button class="row-del" onclick="delFixo(${f.id})"><i class="ti ti-trash"></i></button></td></tr>`;
  }).join('');

  // Tabela receitas
  const tr2=document.getElementById('tbl-receitas');
  if(!m.receitas.length){ tr2.innerHTML='<tr><td colspan="3" class="empty">Nenhuma receita neste mês</td></tr>'; }
  else tr2.innerHTML=m.receitas.map(r=>`<tr><td>${r.desc}</td><td style="color:var(--text-success);font-weight:600">${fmt(r.valor)}</td><td><button class="row-del" onclick="delReceita(${r.id})"><i class="ti ti-trash"></i></button></td></tr>`).join('');

  // Tabela invest
  const ti=document.getElementById('tbl-invest');
  if(!m.invest.length){ ti.innerHTML='<tr><td colspan="4" class="empty">Nenhum investimento neste mês</td></tr>'; }
  else ti.innerHTML=m.invest.map(i=>`<tr><td>${i.nome}</td><td><span class="badge bd">${i.tipo}</span></td><td style="font-weight:600">${fmt(i.valor)}</td><td><button class="row-del" onclick="delInvest(${i.id})"><i class="ti ti-trash"></i></button></td></tr>`).join('');

  renderBars('cat-bars',todosGastos,'cat',totG);
  renderBars('pag-bars',todosGastos,'pag',totG,PAG_CLASS);
}

function renderBars(elId,items,key,total,badgeMap){
  const wrap=document.getElementById(elId);
  if(!items.length){ wrap.innerHTML='<p class="empty">Nenhum gasto registrado neste mês</p>'; return; }
  const grupos={};
  items.forEach(i=>{ grupos[i[key]]=(grupos[i[key]]||0)+i.valor; });
  const sorted=Object.entries(grupos).sort((a,b)=>b[1]-a[1]);
  wrap.innerHTML=sorted.map(([k,v])=>{
    const pct=total>0?v/total*100:0;
    const color=CAT_COLORS[k]||'#888780';
    const badgeCls=badgeMap?(badgeMap[k]||''):null;
    const label=badgeCls?`<span class="badge ${badgeCls}">${k}</span>`:`<span class="badge" style="background:${color}22;color:${color}">${k}</span>`;
    return `<div style="margin-bottom:12px"><div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:4px">${label}<span style="font-size:12px;font-weight:600;color:var(--text-danger)">${fmt(v)} <span style="color:var(--text-muted);font-weight:400;font-size:10px">${pct.toFixed(0)}%</span></span></div><div class="bar-wrap"><div class="bar-f" style="width:${pct}%;background:${color}"></div></div></div>`;
  }).join('');
}

carregarDados();
render();
</script>
</body>
</html>
