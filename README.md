<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>MMPI-2 · Captura y conteo de respuestas</title>
<style>
:root{--bg:#f3f5f8;--panel:#fff;--text:#17202b;--muted:#657386;--line:#d8e0e8;--accent:#2457c5;--v:#137a4b;--f:#b42318;--soft:#eaf0f8}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--text);font:15px/1.45 system-ui,-apple-system,Segoe UI,Roboto,sans-serif}
header{background:#14243a;color:#fff;padding:20px clamp(14px,3vw,32px)}header h1{margin:0 0 5px;font-size:clamp(20px,3vw,29px)}header p{margin:0;color:#d6e0ee}
main{max-width:1400px;margin:auto;padding:18px clamp(10px,2vw,24px) 40px}
.notice{border:1px solid #e4c66a;background:#fff8df;padding:12px 14px;border-radius:10px;margin-bottom:16px;font-size:13px}
.toolbar{display:flex;gap:10px;align-items:center;flex-wrap:wrap;background:var(--panel);padding:12px;border:1px solid var(--line);border-radius:12px;margin-bottom:16px}
button,select,input{font:inherit}button{cursor:pointer;border:1px solid var(--line);background:white;color:var(--text);border-radius:8px;padding:8px 12px}
button.primary{background:var(--accent);color:white;border-color:var(--accent)}button.active{background:#e5edff;border-color:var(--accent);color:var(--accent);font-weight:700}
button:focus-visible,.answer:focus-visible{outline:3px solid #80aaff;outline-offset:2px}
.mode-label{font-weight:650;margin-right:3px}.spacer{flex:1}.progress{font-weight:700}
.sheet-wrap{display:grid;grid-template-columns:minmax(0,1.45fr) minmax(320px,1fr);gap:16px;align-items:start}
.panel{background:var(--panel);border:1px solid var(--line);border-radius:12px;padding:14px;min-width:0}
.panel h2{font-size:18px;margin:0 0 6px}.sub{color:var(--muted);font-size:13px;margin:0 0 12px}
.page-label{font-weight:700;color:#43546a;margin:14px 0 8px}
.answers{display:grid;grid-template-columns:repeat(14,minmax(0,1fr));gap:5px}
.item{border:1.6px solid #b8c6d6;border-radius:8px;padding:5px 3px;text-align:center;min-width:0;background:#fff;box-shadow:0 0 0 .35px #b8c6d6}
.num{font-size:12px;font-weight:700;margin-bottom:3px}
.picks{display:flex;gap:2px;justify-content:center}
.answer{border:1px solid #cbd5e1;background:#f8fafc;border-radius:50%;width:clamp(19px,2.2vw,28px);height:clamp(19px,2.2vw,28px);padding:0;font-size:10px;line-height:1}
.answer.selected-v{background:#d7f5e5;border-color:var(--v);color:var(--v);font-weight:800}
.answer.selected-f{background:#ffe1df;border-color:var(--f);color:var(--f);font-weight:800}
.item.unanswered{background:#fff;border:1.6px solid #b8c6d6;box-shadow:0 0 0 .35px #b8c6d6}
.item.nav-missing{background:#ffe58f!important;border:3px solid #b77900!important;box-shadow:0 0 0 3px rgba(224,168,0,.28)!important}
.item.nav-missing .num{color:#7a4b00}
.scales{display:grid;gap:10px}
.scale{border:1px solid var(--line);border-radius:10px;padding:10px}
.scale h3{margin:0 0 7px;font-size:15px}
.counts{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px}
.count{padding:4px 9px;border-radius:7px;font-weight:700;font-size:13px;background:#f1f5f9}
.count.v{color:var(--v);background:#e3f6ec}.count.f{color:var(--f);background:#fff0ef}
.keyline{margin:7px 0}.keytitle{font-size:12px;color:var(--muted);font-weight:700;margin-bottom:4px}
.keynums{display:flex;flex-wrap:wrap;gap:4px}
.keynum{border:1px solid #dbe2ea;background:#f8fafc;padding:3px 5px;border-radius:5px;font-size:11px}
.keynum.hit{background:#d7f5e5;border-color:#137a4b;color:#075b35;font-weight:800;}
.keynum.miss{background:#fff0ef;border-color:#f0aaa5;color:#922018}
.keynum.noanswer{opacity:.5}
.footer-actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
small{color:var(--muted)}
@media(max-width:900px){.sheet-wrap{grid-template-columns:1fr}.answers{grid-template-columns:repeat(7,minmax(0,1fr))}.answer{width:30px;height:30px;font-size:12px}}
@media(max-width:420px){.answers{grid-template-columns:repeat(5,minmax(0,1fr))}.panel{padding:10px}.toolbar{padding:9px}}
body.pc .answers{grid-template-columns:repeat(14,minmax(0,1fr))}
body.phone .answers{grid-template-columns:repeat(5,minmax(0,1fr))}
body.pc .answer{width:clamp(18px,1.8vw,26px);height:clamp(18px,1.8vw,26px)}
body.phone .answer{width:34px;height:34px;font-size:13px}

/* Teclado V/F opcional para teléfono */
#mobileKeypadToggle{display:none}
#mobileKeypad{display:none}
body.phone #mobileKeypadToggle{display:inline-flex}
body.phone #mobileKeypad.active{
  display:flex;position:fixed;left:0;right:0;bottom:0;z-index:9999;
  gap:12px;padding:12px max(12px,env(safe-area-inset-left))
    calc(12px + env(safe-area-inset-bottom)) max(12px,env(safe-area-inset-right));
  background:rgba(20,36,58,.97);box-shadow:0 -4px 18px rgba(0,0,0,.22)
}
#mobileKeypad button{
  flex:1;min-height:64px;font-size:28px;font-weight:800;border-radius:12px;
  touch-action:manipulation
}
#mobileKeypad button[data-a="V"]{background:#d7f5e5;color:#137a4b;border-color:#137a4b}
#mobileKeypad button[data-a="F"]{background:#ffe1df;color:#b42318;border-color:#b42318}
body.phone.keypad-on main{padding-bottom:110px}

@media print{
  body{background:white;color:#111}
  header, .toolbar, .notice, .footer-actions, .sheet-wrap{display:none!important}
  #printReport{display:block!important}
  @page{size:A4 portrait;margin:12mm}
  #printReport h1{font-size:20px}
  #printReport .print-grid{display:grid;grid-template-columns:repeat(10,1fr);gap:4px}
  #printReport .print-q{border:1px solid #999;padding:4px;text-align:center;font-size:11px}
  #printReport .print-scales{display:grid;grid-template-columns:repeat(2,1fr);gap:8px}
  #printReport .print-scale{border:1px solid #999;padding:6px;break-inside:avoid}
  #printReport .print-chart-wrap{width:100%;margin:10px 0 16px;text-align:center;break-inside:avoid;page-break-inside:avoid}
  #printReport .print-chart-wrap img{display:block;width:100%;max-width:180mm;height:auto;max-height:220mm;object-fit:contain;margin:0 auto}
}
#printReport{display:none}
.profile-controls{display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin:10px 0}
.profile-controls select{padding:7px 10px;border:1px solid var(--line);border-radius:8px;background:#fff}
.profile-scores{display:grid;grid-template-columns:repeat(auto-fit,minmax(125px,1fr));gap:7px;margin:12px 0}
.profile-score{border:1px solid var(--line);border-radius:8px;padding:8px;font-size:12px;background:#f8fafc}
.profile-score strong{display:block;font-size:14px;margin-bottom:3px}
.profile-chart-wrap{width:100%;overflow-x:auto;border:1px solid var(--line);border-radius:8px;background:#fff}
#profileChart{display:block;width:100%;min-width:760px;height:auto}
.profile-warning{margin-top:9px;padding:9px;background:#fff8df;border:1px solid #e4c66a;border-radius:8px}
.t-scores{display:grid;grid-template-columns:repeat(auto-fit,minmax(90px,1fr));gap:6px}
.t-score{padding:7px;border:1px dashed var(--line);border-radius:7px;font-size:12px}
@media print{#profilePanel{break-before:page}.profile-warning{display:block!important}}


.tutorial-overlay{position:fixed;inset:0;z-index:10000;background:rgba(15,23,42,.62);display:flex;align-items:center;justify-content:center;padding:16px}
.tutorial-overlay[hidden]{display:none!important}
.tutorial-card{width:min(680px,100%);max-height:min(88vh,850px);overflow:auto;background:#fff;color:#17202b;border-radius:14px;padding:18px 20px;box-shadow:0 18px 55px rgba(0,0,0,.28)}
.tutorial-head{display:flex;align-items:center;justify-content:space-between;gap:12px}
.tutorial-head h2{margin:0;font-size:20px}
.tutorial-head button{font-size:25px;line-height:1;padding:3px 10px}
.tutorial-card h3{font-size:15px;margin:16px 0 6px}
.tutorial-card p,.tutorial-card li{font-size:13px;line-height:1.5}
.tutorial-card ol,.tutorial-card ul{padding-left:22px;margin:6px 0}
.tutorial-card li{margin:4px 0}
.tutorial-note{padding:9px;background:#fff8df;border-radius:8px}
@media print{#tutorialOverlay{display:none!important}}

</style>
</head>
<body class="pc">
<header>
<h1>MMPI-2 · Captura de respuestas y conteo de escalas</h1>
<p>Registro de respuestas 1–380 y comparación automática.</p>
</header>
<main>
<div class="notice"><strong>Uso académico:</strong> esta página calcula conteos brutos V/F a partir de la clave suministrada. No interpreta perfiles ni genera diagnósticos. Verifica la clave y el resultado con el manual/procedimiento autorizado y supervisión docente. Las respuestas son datos sensibles: no compartas ni guardes datos identificables en equipos compartidos.</div>
<div class="toolbar">
<span class="mode-label">Vista:</span>
<button id="pcBtn" class="active" type="button">Computadora</button>
<button id="phoneBtn" type="button">Teléfono</button>
<button id="mobileKeypadToggle" type="button" aria-pressed="false">Activar teclado V/F</button>
<span class="spacer"></span>
<span class="progress" id="progress">0 / 380 respondidas</span>
<button id="clearBtn" type="button">Limpiar todo</button>
<button id="exportBtn" class="primary" type="button">Exportar respuestas (PDF)</button>
<button id="importPdfBtn" type="button">Importar respuestas desde PDF</button>
<button id="soundToggle" type="button" aria-pressed="false">Activar sonido V/F</button>
<button id="tutorialBtn" type="button">Tutorial</button>
<input id="importPdfFile" type="file" accept="application/pdf,.pdf" hidden>

</div>
<div id="printReport"></div>
<div id="tutorialOverlay" class="tutorial-overlay" hidden>
  <section class="tutorial-card" role="dialog" aria-modal="true" aria-labelledby="tutorialTitle">
    <div class="tutorial-head">
      <h2 id="tutorialTitle">Tutorial rápido</h2>
      <button id="tutorialClose" type="button" aria-label="Cerrar tutorial">×</button>
    </div>
    <p>Guía rápida para capturar respuestas, revisar resultados y guardar el registro.</p>
    <h3>En computadora</h3>
    <ol>
      <li>Deja seleccionada la vista <strong>Computadora</strong>.</li>
      <li>Haz clic en <strong>V</strong> o <strong>F</strong> en la pregunta. También puedes seleccionar una pregunta y escribir V o F con el teclado; el cursor avanza automáticamente.</li>
      <li>Vuelve a pulsar la misma respuesta para desmarcarla si te equivocaste.</li>
      <li>Usa los botones de pregunta anterior/siguiente sin contestar para localizar reactivos pendientes.</li>
    </ol>
    <h3>En teléfono</h3>
    <ol>
      <li>Pulsa <strong>Teléfono</strong> para cambiar la distribución.</li>
      <li>Contesta tocando V o F en cada reactivo, o activa <strong>teclado V/F</strong> para usar los dos botones grandes inferiores. Cada toque registra la respuesta y avanza.</li>
    </ol>
    <h3>Resultados y herramientas</h3>
    <ul>
      <li>El contador superior indica cuántas preguntas has respondido.</li>
      <li>El perfil gráfico presenta las puntuaciones naturales y los ajustes del factor K. Selecciona el perfil correspondiente para consultar su gráfica.</li>
      <li>Activa o desactiva <strong>sonido V/F</strong> para escuchar una señal distinta al registrar V o F.</li>
      <li><strong>Exportar respuestas (PDF)</strong> guarda respuestas, conteos, puntuaciones y la gráfica del perfil seleccionado.</li>
      <li><strong>Importar respuestas desde PDF</strong> recupera respuestas de un PDF exportado desde esta página.</li>
      <li><strong>Limpiar todo</strong> borra las respuestas capturadas.</li>
    </ul>
    <p class="tutorial-note">Uso académico. Protege la confidencialidad de las respuestas y verifica los resultados con el procedimiento autorizado.</p>
  </section>
</div>
<div id="mobileKeypad" aria-label="Teclado emergente V/F">
  <button type="button" data-a="V" aria-label="Capturar verdadero">V</button>
  <button type="button" data-a="F" aria-label="Capturar falso">F</button>
</div>
<div class="sheet-wrap">
<section class="panel">
<h2>Hoja de respuestas</h2>
<p class="sub">Toca/clic en V o F. En computadora también puedes seleccionar una pregunta y escribir V o F. Clic de nuevo en la respuesta elegida la desmarca.</p>
<div id="answerSheet"></div>
<div class="footer-actions">
<button id="prevBtn" type="button">← Pregunta anterior sin contestar</button>
<button id="nextBtn" class="primary" type="button">Siguiente sin contestar →</button>
</div>
</section>
<section class="panel" id="profilePanel">
<h2>Perfil gráfico MMPI-2</h2>
<p class="sub">Selecciona el perfil para calcular las puntuaciones naturales y los ajustes K correspondientes.</p>
<div class="profile-controls">
<label for="profileSex"><strong>Perfil:</strong></label>
<select id="profileSex"><option value="">Seleccionar…</option><option value="female">Femenino</option><option value="male">Masculino</option></select>
<span id="omittedCount" class="count">Sin respuesta: 380</span>
</div>
<div id="profileScores" class="profile-scores"></div>
<div class="profile-chart-wrap">
<canvas id="profileChart" width="1100" height="520" aria-label="Gráfica preliminar de puntuaciones naturales"></canvas>
</div>
<p id="tNotice" class="sub profile-warning">Las puntuaciones T se muestran cuando se seleccione el perfil (masculino/femenino)</p>
<div id="tScores" class="t-scores"></div>
</section>
<section class="panel">
<h2>Conteo automático de escalas</h2>
<p class="sub">Los valores se actualizan al contestar. Verde = respuesta coincide con la clave; rojo = respondió, pero no coincide; gris = sin respuesta.</p>
<div id="scaleResults" class="scales"></div>
</section>
</div>
</main>
<script>
const N=380;
const scales=[
{name:"L",label:"Sinceridad",V:[],F:[16,29,41,51,77,93,102,107,123,139,153,183,203,232,260]},
{name:"F",label:"Validez",V:[18,24,30,36,42,48,54,60,66,72,84,96,114,138,144,150,156,162,168,180,198,216,228,234,240,246,252,258,264,270,282,288,294,300,306,312,324,336,349,355,361],F:[6,12,78,90,102,108,120,126,132,174,186,192,204,210,222,276,318,330,343]},
{name:"K",label:"Corrección",V:[83],F:[29,37,58,76,110,116,122,127,130,136,148,157,158,167,171,196,213,243,267,284,290,330,338,339,341,346,348,356,365]},
{name:"Hs",label:"Hipocondriasis",V:[18,28,39,53,59,97,101,111,149,175,247],F:[2,3,8,10,20,45,47,57,91,117,141,143,152,164,173,176,179,208,224,249,255]},
{name:"D",label:"Depresión",V:[5,15,18,31,38,39,46,56,73,92,117,127,130,146,147,170,175,181,215,233],F:[2,9,10,20,29,33,37,43,45,49,55,68,75,76,95,109,118,134,140,141,142,143,148,165,178,188,189,212,221,223,226,238,245,248,260,267,330]},
{name:"Hi",label:"Histeria conversiva",V:[11,18,31,39,40,44,65,101,166,172,175,218,230],F:[2,3,7,8,9,10,14,26,29,45,47,58,76,81,91,95,98,110,115,116,124,125,129,135,141,148,151,152,157,159,161,164,167,173,176,179,185,193,208,213,224,241,243,249,253,263,265]},
{name:"Dp",label:"Desviación psicopática",V:[17,21,22,31,32,35,42,52,54,56,71,82,89,94,99,105,113,195,202,219,225,259,264,288],F:[9,12,34,70,79,83,95,122,125,129,143,157,158,160,167,171,185,209,214,217,226,243,261,263,266,267]},
{name:"Mf",label:"Masculino-femenino",V:[4,25,62,64,67,74,80,112,119,121,122,128,137,177,187,191,196,205,219,236,251,256,271],F:[1,19,26,27,63,68,69,76,86,103,104,107,120,132,133,163,166,184,193,194,197,199,201,207,209,231,235,237,239,254,257,268,272]},
{name:"Pa",label:"Paranoia",V:[16,17,22,23,24,42,99,113,138,144,145,146,162,234,259,271,277,285,305,307,333,334,336,355,361],F:[81,95,98,100,104,110,244,255,266,283,284,297,314,315]},
{name:"Pt",label:"Psicastenia",V:[11,16,23,31,38,56,65,73,82,89,94,130,147,170,175,196,218,242,273,275,277,285,289,301,302,304,308,309,310,313,316,317,320,325,326,327,328,329,331],F:[3,9,33,109,140,165,174,293,321]},
{name:"Es",label:"Esquizofrenia",V:[16,17,21,22,23,31,32,35,38,42,44,46,48,65,86,92,138,145,147,166,168,170,180,182,190,218,221,229,233,234,242,247,252,256,268,273,274,277,279,281,287,291,292,296,298,299,303,307,311,316,319,320,322,323,325,329,332,333,355],F:[6,9,12,34,90,91,106,165,177,179,192,210,255,276,278,280,290,295,343]},
{name:"Ma",label:"Manía",V:[13,15,21,23,50,55,61,85,87,98,113,122,131,145,155,168,169,182,190,200,205,206,211,212,218,220,227,229,238,242,244,248,250,253,269],F:[88,93,100,106,107,136,154,158,167,243,263]},
{name:"Is",label:"Introversión social",V:[31,56,70,100,104,110,127,135,158,161,167,185,215,243,251,265,275,284,289,296,302,308,326,337,338,347,348,351,352,357,364,367,368,369],F:[25,32,49,79,86,106,112,131,181,189,207,209,231,237,255,263,267,280,321,328,335,340,342,344,345,350,353,354,358,359,360,362,363,366,370]}
];
const answers=Array(N+1).fill(null);
let currentQuestion=1;
const sheet=document.getElementById("answerSheet");
const results=document.getElementById("scaleResults");
function makeQuestion(n){const wrap=document.createElement("div");wrap.className="item unanswered";wrap.id="q"+n;wrap.innerHTML=`<div class="num">${n}</div><div class="picks"><button class="answer" data-q="${n}" data-a="V" aria-label="Pregunta ${n}, verdadero">V</button><button class="answer" data-q="${n}" data-a="F" aria-label="Pregunta ${n}, falso">F</button></div>`;return wrap}
function buildSheet(){sheet.innerHTML="";for(let start=1;start<=N;start+=196){let end=Math.min(start+195,N);let title=document.createElement("div");title.className="page-label";title.textContent=`Hoja ${start===1?"1":"2"} · Preguntas ${start}–${end}`;sheet.appendChild(title);let grid=document.createElement("div");grid.className="answers";for(let n=start;n<=end;n++)grid.appendChild(makeQuestion(n));sheet.appendChild(grid)}}
function setAnswer(n,a){answers[n]=(answers[n]===a)?null:a;renderAnswer(n);update()}
function renderAnswer(n){const el=document.getElementById("q"+n);if(!el)return;el.classList.toggle("unanswered",!answers[n]);el.querySelectorAll(".answer").forEach(b=>{b.classList.toggle("selected-v",answers[n]==="V"&&b.dataset.a==="V");b.classList.toggle("selected-f",answers[n]==="F"&&b.dataset.a==="F");b.setAttribute("aria-pressed",String(answers[n]===b.dataset.a))})}
function scoreScale(s){return {v:s.V.filter(n=>answers[n]==="V").length,f:s.F.filter(n=>answers[n]==="F").length}}

const factorK={
0:[0,0,0],1:[1,0,0],2:[1,1,0],3:[2,1,1],4:[2,2,1],5:[3,2,1],
6:[3,2,1],7:[4,3,1],8:[4,3,2],9:[5,4,2],10:[5,4,2],11:[6,4,2],
12:[6,5,2],13:[7,5,3],14:[7,6,3],15:[8,6,3],16:[8,6,3],17:[9,7,3],
18:[9,7,4],19:[10,8,4],20:[10,8,4],21:[11,8,4],22:[11,9,4],23:[12,9,5],
24:[12,10,5],25:[13,10,5],26:[13,10,5],27:[14,11,5],28:[14,11,6],29:[15,12,6],30:[15,12,6]
};
// Ajustes impresos en los perfiles femenino y masculino.
const kAdjust={Hs:0.5,Dp:0.4,Pt:1,Es:1,Ma:0.2};
const profileOrder=["L","F","K","Hs","D","Hi","Dp","Mf","Pa","Pt","Es","Ma","Is"];

// Anclas de lectura gráfica de las escalas impresas. Cada par es [puntuación natural, T].
// Interpolación lineal entre marcas visibles; extrapolación limitada a los extremos.
const tAnchors={
 female:{
  L:[[0,30],[1,31],[2,36],[3,40],[4,45],[5,50],[6,54],[7,59],[8,63],[9,68],[10,72],[11,77],[12,81],[13,86],[14,90],[15,95]],
  F:[[0,34],[1,37],[2,40],[3,43],[4,46],[5,48],[6,51],[7,54],[8,57],[9,60],[10,63],[11,65],[12,68],[13,71],[14,74],[15,77],[16,80],[17,82],[18,85],[19,88],[19,88],[20,91],[21,94],[22,96],[23,99],[24,102],[25,105],[26,108],[27,111],[28,113],[29,116],[30,119]],
  K:[[7, 30],[8,33],[9,33],[10,37],[11,39],[12,41],[13,43],[14,45],[15,47],[16,50],[17,52],[18,54],[19,56],[20,58],[21,60],[22,62],[23,64],[24,67],[25,69],[26,71],[27,73],[28,75],[29,77],[30,79],[31,81],[32,84],[33,86],[34,88],[35,90],[36,92],[37,94],[38,96],[39,98],[40,101],[41,103],[42,105],[43,107],[44,109],[45,111],[46,113],[47,116],[48,118],[49,120]],
  Hs:[[6,30],[7,31],[8,33],[9,35],[10,37],[11,39],[12,41],[13,43],[14,45],[15,47],[16,50],[17,52],[18,54],[19,56],[20,59],[21,61],[22,63],[23,65],[24,67],[25,70],[26,72],[27,74],[28,76],[29,79],[30,81],[31,83],[32,85],[33,87],[34,90],[35,92],[36,94],[37,96],[38,98],[39,101],[40,103],[41,105],[42,107],[43,109],[44,112],[45,114],[46,116],[47,118],[48,120],],
  D:[[12,30],[13,31],[14,33],[15,35],[16,37],[17,39],[18,41],[19,43],[20,45],[21,47],[22,49],[23,52],[24,54],[25,56],[27,60],[28,62],[29,64],[30,66],[31,67],[32,69],[33,71],[34,73],[35,75],[36,77],[37,79],[38,81],[39,83],[40,84],[41,86],[42,88],[43,90],[44,92],[45,94],[46,96],[47,98],[48,100],[49,101],[50,103],[51,105],[52,107],[53,109],[54,111],[55,113],[56,115],[57,117]],
  Hi:[[10,30],[11,31],[12,32],[13,33],[14,35],[15,36],[16,38],[17,39],[18,41],[19,43],[20,45],[21,46],[22,48],[23,50],[24,52],[25,54],[26,57],[27,60],[28,61],[29,63],[30,65],[31,67],[32,69],[33,71],[34,73],[35,76],[36,78],[37,80],[38,82],[39,84],[40,86],[41,88],[42,90],[43,93],[44,95],[45,97],[46,99],[47,101],[48,103],[49,105],[50,107],[51,110],[52,112],[53,114],[54,116],[55,118],[56,120]],
  Dp:[[12,30],[13,31],[14,32],[15,34],[16,35],[17,37],[18,38],[19,40],[20,42],[21,44],[22,46],[23,49],[24,51],[25,53],[26,56],[27,58],[28,61],[29,63],[30,66],[31,69],[32,71],[33,74],[34,76],[35,79],[36,81],[37,84],[38,86],[39,89],[40,91],[41,94],[42,97],[43,99],[44,102],[45,104],[46,107],[47,109],[48,112],[49,114],[50,117]],
  Mf:[[38,30],[37,32],[36,34],[35,37],[34,40],[33,42],[32,45],[31,48],[30,51],[29,53],[28,56],[27,57],[26,61],[25,64],[24,67],[23,69],[22,72],[21,75],[20,78],[19,80],[18,83],[17,86],[16,88],[15,91],[14,94],[13,96],[12,99],[11,102],[10,104],[9,107],[8,110],[7,113],[6,115],[5,118]],
  Pa:[[2,31],[3,32],[4,34],[5,36],[6,38],[7,41],[8,44],[9,47],[10,50],[11,53],[12,57],[13,60],[14,64],[15,67],[16,70],[17,74],[18,77],[19,80],[20,84],[21,87],[22,90],[23,94],[24,97],[25,101],[26,104],[27,107],[28,111],[29,114],[30,117],[31,120]],
  Pt:[[17,30],[18,31],[19,33],[20,34],[21,35],[22,37],[23,39],[24,41],[25,45],[26,45],[27,47],[28,49],[29,51],[30,53],[31,55],[32,57],[33,59],[34,61],[35,63],[36,65],[37,67],[38,69],[39,71],[40,73],[41,75],[42,77],[43,79],[44,81],[45,83],[46,85],[47,87],[48,89],[49,91],[50,93],[51,95],[52,97],[53,99],[54,101],[55,103],[56,105],[57,107],[58,109],[59,111],[60,113],[61,115],[62,116],[63,118],[64,120]],
  Es:[[17,30],[18,31],[19,33],[20,35],[21,36],[22,38],[23,40],[24,41],[25,43],[26,44],[27,46],[28,48],[29,49],[30,51],[31,52],[32,54],[33,56],[34,57],[35,59],[36,61],[37,63],[38,64],[39,66],[40,68],[41,70],[42,72],[43,73],[44,75],[45,77],[46,79],[47,81],[48,83],[49,84],[50,86],[51,88],[52,90],[53,92],[54,93],[55,95],[56,97],[57,99],[58,101],[59,102],[60,104],[61,106],[62,108],[63,110],[64,112],[65,113],[66,115],[67,117],[68,119],[69,120]],
  Ma:[[9,30],[10,31],[11,0],[12,0],[13,0],[14,0],[15,35],[16,37],[17,39],[18,42],[19,44],[20,47],[21,50],[22,52],[23,55],[24,58],[25,61],[26,63],[27,66],[28,69],[29,71],[30,74],[31,77],[32,79],[33,82],[34,85],[35,88],[36,90],[37,93],[38,95],[39,98],[40,101],[41,101],[42,106],[43,109],[44,111],[45,114],[46,117]],
  Is:[[11,30],[12,31],[13,33],[14,34],[15,35],[16,36],[17,37],[18,39],[19,40],[20,41],[21,42],[22,44],[23,45],[24,46],[25,47],[26,48],[27,50],[28,51],[29,52],[30,53],[31,54],[32,56],[33,57],[34,58],[35,59],[36,61],[37,62],[38,63],[39,64],[40,65],[41,67],[42,68],[43,69],[44,70],[45,71],[46,72],[47,74],[48,75],[49,76],[50,78],[51,79],[52,80],[53,81],[54,82],[55,84],[56,85],[57,86],[58,87],[59,88],[60,90],[61,91],[62,92],[63,93],[64,95],[65,96],[66,97],[67,98],[68,99],[69,101],[70,102]],
 },
 male:{
  L:[[0,30],[1,34],[2,38],[3,42],[4,45],[5,49],[6,53],[7,57],[8,61],[9,65],[10,68],[11,72],[12,76],[13,80],[14,84],[15,88]],
  F:[[0,35],[1,37],[2,40],[3,43],[4,46],[5,49],[6,52],[7,54],[8,57],[9,60],[10,63],[11,66],[12,68],[13,71],[14,74],[15,77],[16,80],[17,83],[18,85],[19,88],[20,92],[21,94],[22,97],[23,100],[24,102],[25,105],[26,108],[27,111],[28,114],[29,117],[30,119]],
  K:[[7,30],[8,32],[9,34],[10,36],[11,38],[12,40],[13,42],[14,44],[15,46],[16,48],[17,50],[18,52],[19,54],[20,56],[21,59],[22,61],[23,63],[24,65],[65,67],[26,69],[27,71],[28,73],[29,75],[30,77],[31,79],[32,81],[33,83],[34,85],[35,87],[36,90],[37,92],[38,94],[39,96],[40,98],[41,100],[42,102],[43,104],[44,106],[45,108],[46,110],[47,112],[48,114],[49,116],[50,118]],
  Hs:[[4,0],[5,0],[6,0],[7,0],[8,0],[9,0],[10,38],[11,40],[12,43],[13,45],[14,48],[15,50],[16,53],[17,55],[18,58],[19,60],[20,62],[21,64],[22,66],[23,68],[24,70],[25,72],[26,74],[27,77],[28,79],[29,81],[30,83],[31,85],[32,87],[33,89],[34,91],[35,93],[36,95],[37,97],[38,99],[39,101],[40,103],[41,105],[42,107],[43,109],[44,111],[45,113],[46,115],[47,118],[48,120]],
  D:[[9,30],[10,31],[11,32],[12,33],[13,35],[14,37],[15,39],[16,41],[17,43],[18,45],[19,47],[20,50],[21,52],[22,54],[23,57],[24,59],[25,61],[26,63],[27,65],[28,67],[29,69],[30,71],[31,73],[32,75],[33,77],[34,79],[35,81],[36,82],[37,85],[39,89],[40,91],[41,93],[42,95],[43,97],[44,99],[45,101],[46,103],[47,105],[48,107],[49,109],[50,111],[51,113],[52,115],[53,117],[54,119],[55,120]],
  Hi:[[5,0],[6,0],[7,0],[8,0],[9,0],[10,0],[11,0],[12,0],[13,0],[14,0],[15,0],[16,39],[17,41],[18,43],[19,45],[20,47],[21,49],[22,52],[23,54],[24,56],[25,58],[26,60],[27,63],[28,65],[29,67],[30,69],[31,71],[32,73],[33,76],[34,78],[35,80],[36,82],[37,84],[38,86],[39,88],[40,91],[41,93],[42,95],[43,97],[44,99],[45,101],[46,103],[47,106],[48,108],[49,110],[50,112],[51,114],[52,116],[53,119],[54,120]],
  Dp:[[12,30],[13,31],[14,32],[15,33],[16,34],[17,36],[18,38],[19,40],[20,42],[21,44],[22,46],[23,49],[24,51],[25,53],[26,56],[27,58],[28,61],[29,63],[30,66],[31,68],[32,71],[33,73],[34,76],[35,78],[36,81],[37,83],[38,86],[39,88],[40,90],[41,93],[42,95],[43,98],[44,100],[45,103],[46,105],[47,108],[48,110],[49,113],[50,115]],
  Mf:[[16,31],[17,34],[18,36],[19,38],[20,41],[21,43],[22,46],[23,48],[24,51],[25,53],[26,55],[27,58],[28,60],[29,63],[30,65],[31,68],[32,70],[33,73],[34,75],[35,77],[36,80],[37,82],[38,85],[39,87],[40,89],[41,92],[42,94],[43,97],[44,99],[45,102],[46,104],[47,106],[48,109],[49,111],[50,114],[51,116],[52,119]],
  Pa:[[1,30],[2,31],[3,32],[4,34],[5,37],[6,39],[7,43],[8,46],[9,49],[10,53],[11,56],[12,59],[16,63],[14,66],[15,69],[16,72],[17,75],[18,78],[19,82],[20,85],[21,88],[22,91],[23,94],[24,97],[25,101],[26,104],[27,107],[28,110],[29,113],[30,116],[31,120]],
  Pt:[[16,30],[17,31],[18,32],[19,33],[20,35],[21,36],[22,38],[23,40],[24,42],[25,45],[26,47],[27,49],[28,52],[29,54],[30,56],[31,58],[32,60],[33,62],[34,64],[35,66],[36,68],[37,70],[38,72],[39,74],[40,76],[41,78],[42,80],[43,82],[43,84],[44,84],[45,86],[46,88],[47,90],[48,92],[49,94],[50,96],[51,98],[52,100],[53,102],[54,104],[55,106],[56,108],[57,110],[58,112],[59,114],[60,116],[61,118],[62,120]],
  Es:[[16,30],[17,31],[18,32],[19,34],[20,35],[21,37],[22,38],[23,40],[24,42],[25,44],[26,46],[27,48],[28,49],[29,51],[30,55],[32,57],[33,58],[34,60],[35,62],[36,63],[37,64],[38,66],[39,67],[40,69],[41,70],[42,72],[43,73],[44,75],[45,76],[46,77],[47,79],[48,80],[49,82],[50,83],[51,85],[52,86],[53,88],[54,89],[55,91],[56,92],[57,93],[58,95],[59,96],[60,98],[61,99],[62,101],[63,102],[64,104],[65,105],[66,107],[67,108],[68,109],[69,111],[70,112],[71,114],[72,115],[72,115],[73,117],[74,118],[75,120]],
  Ma:[[12,30],[13,32],[14,34],[15,35],[16,37],[17,39],[18,41],[19,43],[20,46],[21,48],[22,50],[23,53],[24,55],[25,58],[26,61],[27,64],[28,67],[29,70],[30,72],[31,76],[32,79],[33,82],[34,85],[35,88],[36,91],[37,94],[38,97],[39,100],[40,103],[41,106],[42,109],[43,112],[44,115],[45,118],[46,120]],
  Is:[[10,30],[11,31],[12,33],[13,34],[14,35],[15,37],[16,38],[17,39],[18,40],[19,42],[20,43],[21,44],[22,46],[23,47],[24,48],[25,50],[26,51],[27,52],[28,54],[29,55],[30,56],[31,58],[32,59],[33,60],[34,62],[35,63],[36,64],[37,66],[38,67],[39,68],[40,69],[41,71],[42,72],[43,73],[44,75],[45,76],[46,77],[47,79],[48,80],[49,81],[50,83],[51,84],[52,85],[53,87],[54,88],[55,89],[56,91],[57,92],[58,93],[59,95],[60,96],[61,97],[62,98],[63,100],[64,101],[65,102],[66,104],[67,105],[68,106],[69,108]],
 }
};
function scoreToT(name,score,sex){
 const source=tAnchors[sex]?.[name];
 if(!source||!source.length)return null;
 // Normaliza el orden: algunas escalas (como Mf) tienen anclas guardadas de mayor a menor.
 const a=[...source].sort((p,q)=>p[0]-q[0]);
 if(a.length===1)return a[0][1];
 if(score<=a[0][0]){
  const [x0,y0]=a[0],[x1,y1]=a[1];
  return Math.round(y0+(score-x0)*(y1-y0)/(x1-x0));
 }
 for(let i=1;i<a.length;i++){
  if(score<=a[i][0]){
   const [x0,y0]=a[i-1],[x1,y1]=a[i];
   return Math.round(y0+(score-x0)*(y1-y0)/(x1-x0));
  }
 }
 const [x0,y0]=a[a.length-2],[x1,y1]=a[a.length-1];
 return Math.round(Math.min(120,y1+(score-x1)*(y1-y0)/(x1-x0)));
}

function naturalProfile(){
 const raw={}; scales.forEach(s=>{const v=scoreScale(s);raw[s.name]=v.v+v.f});
 const k=raw.K||0, factor=factorK[Math.max(0,Math.min(30,k))]||[0,0,0];
 const scores=profileOrder.map(name=>{
   const base=raw[name]??0, mult=kAdjust[name]||0;
   const add=mult===1?k:mult===0.5?factor[0]:mult===0.4?factor[1]:mult===0.2?factor[2]:0;
   return {name,base,adjust:add,adjusted:base+add,usesK:mult>0};
 });
 return {raw,k,factor,scores,omitted:N-answers.slice(1).filter(Boolean).length};
}
function drawProfileChart(data){
 const canvas=document.getElementById("profileChart"); if(!canvas)return;
 const ctx=canvas.getContext("2d"),w=canvas.width,h=canvas.height;
 ctx.clearRect(0,0,w,h);ctx.fillStyle="#fff";ctx.fillRect(0,0,w,h);
 const sex=document.getElementById("profileSex").value;
 const left=66,right=24,top=35,bottom=90,gw=w-left-right,gh=h-top-bottom;
 ctx.strokeStyle="#dce3eb";ctx.lineWidth=1;ctx.font="12px system-ui";ctx.fillStyle="#475569";
 for(let t=30;t<=120;t+=5){
  const y=top+gh-((t-30)/90)*gh;
  ctx.beginPath();ctx.moveTo(left,y);ctx.lineTo(w-right,y);ctx.stroke();
  if(t%10===0)ctx.fillText(String(t),22,y+4);
 }
 ctx.save();ctx.translate(15,top+gh/2);ctx.rotate(-Math.PI/2);ctx.textAlign="center";ctx.font="13px system-ui";ctx.fillText("Puntuación T (estimada)",0,0);ctx.restore();
 const step=gw/data.scores.length;
 const pts=data.scores.map(s=>({...s,T:scoreToT(s.name,s.adjusted,sex)}));
 pts.forEach((s,i)=>{
  if(s.T===null)return;
  const x=left+step*(i+.5),y=top+gh-((s.T-30)/90)*gh;
  // No unir K con Hs: la gráfica separa L, F y K del resto de las escalas.
  if(i&&i!==3&&pts[i-1].T!==null){
   const px=left+step*(i-.5),py=top+gh-((pts[i-1].T-30)/90)*gh;
   ctx.strokeStyle="#2457c5";ctx.lineWidth=2;ctx.beginPath();ctx.moveTo(px,py);ctx.lineTo(x,y);ctx.stroke();
  }
  ctx.fillStyle="#2457c5";ctx.beginPath();ctx.arc(x,y,5,0,Math.PI*2);ctx.fill();
  ctx.fillStyle="#17202b";ctx.font="bold 12px system-ui";ctx.textAlign="center";ctx.fillText(String(s.T),x,y-10);
  ctx.save();ctx.translate(x,top+gh+17);ctx.rotate(-Math.PI/4);ctx.textAlign="right";ctx.font="12px system-ui";ctx.fillText(s.name,0,0);ctx.restore();
 });
 // Líneas de referencia del formato original: T=65, T=50 y división tras K.
 ctx.strokeStyle="#64748b";ctx.lineWidth=1.5;ctx.setLineDash([]);
 const y65=top+gh-((65-30)/90)*gh;
 const y50=top+gh-((50-30)/90)*gh;
 ctx.beginPath();ctx.moveTo(left,y65);ctx.lineTo(w-right,y65);ctx.stroke();
 ctx.beginPath();ctx.moveTo(left,y50);ctx.lineTo(w-right,y50);ctx.stroke();
 const dividerX=left+step*3;
 ctx.beginPath();ctx.moveTo(dividerX,top);ctx.lineTo(dividerX,top+gh);ctx.stroke();
 ctx.fillStyle="#475569";ctx.font="12px system-ui";ctx.textAlign="left";
 ctx.fillText("Perfil "+(sex==="female"?"femenino":"masculino")+" · Conversión por lectura/interpolación de marcas impresas",left,18);
}
function updateProfile(){
 const chosen=document.getElementById("profileSex")?.value;
 const panel=document.getElementById("profilePanel");if(!panel)return;
 const data=naturalProfile();
 document.getElementById("omittedCount").textContent=`Sin respuesta: ${data.omitted}`;
 const target=document.getElementById("profileScores");
 target.innerHTML="";
 if(!chosen){target.innerHTML='<div class="profile-score">Selecciona un perfil para ver los cálculos.</div>';document.getElementById("tScores").innerHTML="";drawProfileChart(data);return}
 data.scores.forEach(s=>{
  const el=document.createElement("div");el.className="profile-score";
  el.innerHTML=`<strong>${s.name}</strong>Puntuación natural: ${s.base}${s.usesK?`<br>Factor K agregado: +${s.adjust}<br><b>Natural con K: ${s.adjusted}</b>`:"<br><b>Sin ajuste K</b>"}`;
  target.appendChild(el);
 });
 document.getElementById("tScores").innerHTML=data.scores.map(s=>{const t=scoreToT(s.name,s.adjusted,chosen);return `<div class="t-score"><strong>${s.name}</strong><br>Natural: ${s.adjusted}<br><b>T ≈ ${t}</b></div>`}).join("");
 document.getElementById("tNotice").textContent="GRAFICA Y VALORES T AÚN EN VERIFICACIÓN, VERIFICAR DATOS ANTES DE SU USO.";
 drawProfileChart(data);
}
document.getElementById("profileSex").addEventListener("change",updateProfile);

function update(){let count=answers.slice(1).filter(Boolean).length;document.getElementById("progress").textContent=`${count} / ${N} respondidas`;results.innerHTML="";scales.forEach(s=>{let sc=scoreScale(s),card=document.createElement("article");card.className="scale";card.innerHTML=`<h3>Escala ${s.name} <span style="font-weight:400;color:#657386">(${s.label})</span></h3><div class="counts"><span class="count v">V = ${sc.v}</span><span class="count f">F = ${sc.f}</span><span class="count">Total clave = ${sc.v+sc.f}</span></div>`;card.appendChild(keyline("V",s.V,"V"));card.appendChild(keyline("F",s.F,"F"));results.appendChild(card)});updateProfile()}
function keyline(label,items,expected){let wrap=document.createElement("div");wrap.className="keyline";let title=document.createElement("div");title.className="keytitle";title.textContent=`Clave ${label} · ${items.length} reactivos`;wrap.appendChild(title);let nums=document.createElement("div");nums.className="keynums";items.forEach(n=>{let chip=document.createElement("span");chip.className="keynum";let r=answers[n];if(!r)chip.classList.add("noanswer");else if(r===expected)chip.classList.add("hit");else chip.classList.add("miss");chip.textContent=n+(r?` ${r}`:"");chip.title=`Reactivo ${n}: ${r||"sin respuesta"}; clave ${expected}`;nums.appendChild(chip)});wrap.appendChild(nums);return wrap}
// Sonido opcional de confirmación V/F, generado localmente con Web Audio.
let soundEnabled=false;
let audioContext=null;
function playAnswerSound(answer){
  if(!soundEnabled)return;
  try{
    const AudioCtx=window.AudioContext||window.webkitAudioContext;
    if(!AudioCtx)return;
    if(!audioContext)audioContext=new AudioCtx();
    if(audioContext.state==="suspended")audioContext.resume();
    const oscillator=audioContext.createOscillator();
    const gain=audioContext.createGain();
    oscillator.type="sine";
    oscillator.frequency.value=answer==="V"?880:440;
    gain.gain.setValueAtTime(0.0001,audioContext.currentTime);
    gain.gain.exponentialRampToValueAtTime(0.16,audioContext.currentTime+0.012);
    gain.gain.exponentialRampToValueAtTime(0.0001,audioContext.currentTime+0.12);
    oscillator.connect(gain);gain.connect(audioContext.destination);
    oscillator.start();oscillator.stop(audioContext.currentTime+0.13);
  }catch(err){console.warn("No se pudo reproducir el sonido",err)}
}
const soundToggle=document.getElementById("soundToggle");
soundToggle.onclick=()=>{
  soundEnabled=!soundEnabled;
  soundToggle.classList.toggle("active",soundEnabled);
  soundToggle.setAttribute("aria-pressed",String(soundEnabled));
  soundToggle.textContent=soundEnabled?"Desactivar sonido V/F":"Activar sonido V/F";
  if(soundEnabled)playAnswerSound("V");
};
sheet.addEventListener("click",e=>{
  let b=e.target.closest("button.answer");
  if(b){currentQuestion=+b.dataset.q;playAnswerSound(b.dataset.a);setAnswer(currentQuestion,b.dataset.a)}
});
function captureAndAdvance(a){
  let focused=document.activeElement?.closest?.(".item");
  let n=focused?+focused.id.slice(1):currentQuestion;
  n=Math.max(1,Math.min(N,n||1));
  answers[n]=a;currentQuestion=n;renderAnswer(n);update();
  const next=document.getElementById("q"+Math.min(N,n+1));
  if(next){
    currentQuestion=Math.min(N,n+1);
    next.scrollIntoView({behavior:"auto",block:"nearest"});
    next.querySelector("button")?.focus({preventScroll:true});
  }
}
const keypad=document.getElementById("mobileKeypad");
keypad.addEventListener("click",e=>{
  const b=e.target.closest("button[data-a]");
  if(b){playAnswerSound(b.dataset.a);captureAndAdvance(b.dataset.a)}
});
const keypadToggle=document.getElementById("mobileKeypadToggle");
keypadToggle.onclick=()=>{
  const enabled=keypad.classList.toggle("active");
  document.body.classList.toggle("keypad-on",enabled);
  keypadToggle.classList.toggle("active",enabled);
  keypadToggle.setAttribute("aria-pressed",String(enabled));
  keypadToggle.textContent=enabled?"Desactivar teclado V/F":"Activar teclado V/F";
};
document.addEventListener("keydown",e=>{
  if(e.key.toLowerCase()!=="v"&&e.key.toLowerCase()!=="f")return;
  if(["INPUT","TEXTAREA","SELECT"].includes(document.activeElement?.tagName))return;
  let focused=document.activeElement?.closest?.(".item");
  if(!focused)return;
  const n=+focused.id.slice(1);
  currentQuestion=n;
  // Captura V/F y avanza automáticamente a la siguiente pregunta.
  answers[n]=e.key.toUpperCase();
  playAnswerSound(e.key.toUpperCase());
  renderAnswer(n);update();
  e.preventDefault();
  const next=document.getElementById("q"+Math.min(N,n+1));
  if(next){next.scrollIntoView({behavior:"auto",block:"nearest"});next.querySelector("button")?.focus({preventScroll:true})}
});
function nextUnanswered(dir=1){
  let active=document.activeElement?.closest?.(".item");
  let start=active?+active.id.slice(1):(dir>0?0:N+1);
  for(let i=1;i<=N;i++){
    let n=start+dir*i;
    if(n<1||n>N)continue;
    if(!answers[n]){
      document.querySelectorAll(".item.nav-missing").forEach(el=>el.classList.remove("nav-missing"));
      const target=document.getElementById("q"+n);
      target?.classList.add("nav-missing");
      target?.scrollIntoView({behavior:"smooth",block:"center"});
      target?.querySelector("button")?.focus({preventScroll:true});
      return;
    }
  }
  alert("No hay preguntas sin contestar en esa dirección.");
}
document.getElementById("nextBtn").onclick=()=>nextUnanswered(1);document.getElementById("prevBtn").onclick=()=>nextUnanswered(-1);
document.getElementById("pcBtn").onclick=()=>{
  document.body.classList.remove("phone","keypad-on");document.body.classList.add("pc");
  pcBtn.classList.add("active");phoneBtn.classList.remove("active");
  keypad.classList.remove("active");keypadToggle.classList.remove("active");
  keypadToggle.setAttribute("aria-pressed","false");keypadToggle.textContent="Activar teclado V/F";
};
document.getElementById("phoneBtn").onclick=()=>{
  document.body.classList.remove("pc");document.body.classList.add("phone");
  phoneBtn.classList.add("active");pcBtn.classList.remove("active");
};
document.getElementById("clearBtn").onclick=()=>{if(confirm("¿Borrar todas las respuestas capturadas?")){answers.fill(null);for(let n=1;n<=N;n++)renderAnswer(n);update()}};
const tutorialOverlay=document.getElementById("tutorialOverlay");
document.getElementById("tutorialBtn").onclick=()=>{tutorialOverlay.hidden=false};
document.getElementById("tutorialClose").onclick=()=>{tutorialOverlay.hidden=true};
tutorialOverlay.addEventListener("click",e=>{if(e.target===tutorialOverlay)tutorialOverlay.hidden=true});
document.addEventListener("keydown",e=>{if(e.key==="Escape"&&!tutorialOverlay.hidden)tutorialOverlay.hidden=true});
document.getElementById("exportBtn").onclick=async()=>{
  const report=document.getElementById("printReport");
  let count=answers.slice(1).filter(Boolean).length;
  const pd=naturalProfile(),profileName=document.getElementById("profileSex").value;
  const chartCanvas=document.getElementById("profileChart");
  // Captura la gráfica ya dibujada como PNG para incorporarla al documento impreso/PDF.
  const chartImage=profileName&&chartCanvas?chartCanvas.toDataURL("image/png"):"";
  report.innerHTML=`<h1>MMPI-2 · Registro de respuestas</h1><p>Reactivos respondidos: ${count} / 380 · Fecha de exportación: ${new Date().toLocaleDateString("es-MX")}</p><h2>Perfil gráfico</h2><p>Perfil: ${profileName==="female"?"Femenino":profileName==="male"?"Masculino":"No seleccionado"} · Reactivos sin respuesta: ${pd.omitted}</p>${chartImage?`<div class="print-chart-wrap"><img id="printProfileChart" src="${chartImage}" alt="Gráfica del perfil MMPI-2"></div>`:"<p>No se generó la gráfica porque aún no se ha seleccionado un perfil.</p>"}<div class="print-scales">${pd.scores.map(s=>`<div class="print-scale"><strong>${s.name}</strong><br>Puntuación natural: ${s.base}<br>Factor K agregado: ${s.usesK?s.adjust:"No aplica"}<br>Puntuación natural con K: ${s.adjusted}<br>Puntuación T: ${profileName?scoreToT(s.name,s.adjusted,profileName):"—"}</div>`).join("")}</div><h2>Hoja de respuestas</h2><div class="print-grid">${Array.from({length:N},(_,i)=>`<div class="print-q">${i+1}: <strong>${answers[i+1]||"—"}</strong></div>`).join("")}</div><h2>Conteo bruto de claves</h2><div class="print-scales">${scales.map(sc=>{let score=scoreScale(sc);return `<div class="print-scale"><strong>${sc.name} · ${sc.label}</strong><br>V = ${score.v} &nbsp; F = ${score.f} &nbsp; Total clave = ${score.v+score.f}</div>`}).join("")}</div><p><small>Reporte de captura académica. No constituye interpretación clínica.</small></p>`;
  const chartImg=document.getElementById("printProfileChart");
  if(chartImg){
    if(!chartImg.complete) await new Promise(resolve=>{chartImg.onload=resolve;chartImg.onerror=resolve});
    if(chartImg.decode){try{await chartImg.decode()}catch(err){}}
  }
  window.print();
};
document.getElementById("importPdfBtn").onclick=()=>document.getElementById("importPdfFile").click();
document.getElementById("importPdfFile").onchange=async e=>{
  const file=e.target.files?.[0]; if(!file)return;
  try{
    // PDF.js se carga al solicitar la importación. Requiere conexión a internet.
    const pdfjs=await import("https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.10.38/pdf.min.mjs");
    pdfjs.GlobalWorkerOptions.workerSrc="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.10.38/pdf.worker.min.mjs";
    const pdf=await pdfjs.getDocument({data:await file.arrayBuffer()}).promise;
    let fullText="";
    for(let pageNo=1;pageNo<=pdf.numPages;pageNo++){
      const page=await pdf.getPage(pageNo);
      const content=await page.getTextContent();
      fullText+=" "+content.items.map(it=>it.str).join(" ");
    }
    // El PDF exportado contiene reactivos con formato "número: respuesta".
    const found=new Map();
    const regex=/(?:^|\s)(\d{1,3})\s*:\s*([VF]|[—-])(?=\s|$)/g;
    let match;
    while((match=regex.exec(fullText))!==null){
      const q=Number(match[1]);
      if(q>=1&&q<=N)found.set(q,match[2]==="V"||match[2]==="F"?match[2]:null);
    }
    if(found.size<250)throw new Error("No se reconocieron suficientes reactivos. Asegúrate de seleccionar un PDF generado por esta página.");
    if(!confirm(`Se detectaron ${found.size} reactivos en el PDF. ¿Deseas reemplazar las respuestas actuales?`))return;
    answers.fill(null);
    found.forEach((value,q)=>answers[q]=value);
    for(let q=1;q<=N;q++)renderAnswer(q);
    update();
    alert(`Importación completada. Se recuperaron ${found.size} reactivos.`);
  }catch(err){
    console.error(err);
    alert("No se pudo importar el PDF. Usa un PDF generado por esta página y asegúrate de tener conexión a internet.\\n\\nDetalle: "+err.message);
  }finally{e.target.value=""}
};
buildSheet();update();updateProfile();
</script>
</body>
</html>
