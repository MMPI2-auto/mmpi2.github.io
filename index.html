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
}
#printReport{display:none}
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
<input id="importPdfFile" type="file" accept="application/pdf,.pdf" hidden>

</div>
<div id="printReport"></div>
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
function update(){let count=answers.slice(1).filter(Boolean).length;document.getElementById("progress").textContent=`${count} / ${N} respondidas`;results.innerHTML="";scales.forEach(s=>{let sc=scoreScale(s),card=document.createElement("article");card.className="scale";card.innerHTML=`<h3>Escala ${s.name} <span style="font-weight:400;color:#657386">(${s.label})</span></h3><div class="counts"><span class="count v">V = ${sc.v}</span><span class="count f">F = ${sc.f}</span><span class="count">Total clave = ${sc.v+sc.f}</span></div>`;card.appendChild(keyline("V",s.V,"V"));card.appendChild(keyline("F",s.F,"F"));results.appendChild(card)})}
function keyline(label,items,expected){let wrap=document.createElement("div");wrap.className="keyline";let title=document.createElement("div");title.className="keytitle";title.textContent=`Clave ${label} · ${items.length} reactivos`;wrap.appendChild(title);let nums=document.createElement("div");nums.className="keynums";items.forEach(n=>{let chip=document.createElement("span");chip.className="keynum";let r=answers[n];if(!r)chip.classList.add("noanswer");else if(r===expected)chip.classList.add("hit");else chip.classList.add("miss");chip.textContent=n+(r?` ${r}`:"");chip.title=`Reactivo ${n}: ${r||"sin respuesta"}; clave ${expected}`;nums.appendChild(chip)});wrap.appendChild(nums);return wrap}
sheet.addEventListener("click",e=>{
  let b=e.target.closest("button.answer");
  if(b){currentQuestion=+b.dataset.q;setAnswer(currentQuestion,b.dataset.a)}
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
  if(b)captureAndAdvance(b.dataset.a);
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
document.getElementById("exportBtn").onclick=()=>{
  const report=document.getElementById("printReport");
  let count=answers.slice(1).filter(Boolean).length;
  report.innerHTML=`<h1>MMPI-2 · Registro de respuestas</h1><p>Reactivos respondidos: ${count} / 380 · Fecha de exportación: ${new Date().toLocaleDateString("es-MX")}</p><h2>Hoja de respuestas</h2><div class="print-grid">${Array.from({length:N},(_,i)=>`<div class="print-q">${i+1}: <strong>${answers[i+1]||"—"}</strong></div>`).join("")}</div><h2>Conteo bruto de claves</h2><div class="print-scales">${scales.map(sc=>{let score=scoreScale(sc);return `<div class="print-scale"><strong>${sc.name} · ${sc.label}</strong><br>V = ${score.v} &nbsp; F = ${score.f} &nbsp; Total clave = ${score.v+score.f}</div>`}).join("")}</div><p><small>Reporte de captura académica. No constituye interpretación clínica.</small></p>`;
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
buildSheet();update();
</script>
</body>
</html>
