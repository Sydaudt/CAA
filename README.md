<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Carnet CAA</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Big+Shoulders+Display:wght@600;800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
/* VOICE: salle de cinéma, sérieuse et passionnée : un carnet d'analyse de BTS audiovisuel
   IDEA: un programme de cinémathèque : chaque film est une séance avec sa bobine et ses notes
   PICTURE: l'extrait lui-même, grand, avec une frise de séquence cliquable qui suit la lecture
   COLOUR and TYPE: salle noire bleutée, lumière d'écran, accent orange feu ; Big Shoulders + Inter
   LAYOUT: accueil = grille d'affiches ; page film = vidéo + frise, puis analyse en colonne avec sommaire */
:root{color-scheme:dark;--bg:#0c0f14;--bg2:#141922;--line:#252d3a;--ink:#e9edf3;--dim:#9aa5b5;--fire:#ff7a1a;--steel:#7fa6d6}
*{box-sizing:border-box;min-width:0}
body{margin:0;background:var(--bg);color:var(--ink);font:16px/1.6 Inter,system-ui,sans-serif;overflow-x:clip}
a{color:inherit}
html{scroll-padding-top:72px}
.band{padding:clamp(28px,4vw,64px) max(5vw,16px)}
.wrap{max-width:1240px;margin:0 auto}
header.top{position:sticky;top:0;z-index:5;background:rgba(12,15,20,.92);backdrop-filter:blur(8px);border-bottom:1px solid var(--line)}
header.top .wrap{display:flex;align-items:center;gap:16px;padding:12px max(5vw,16px);flex-wrap:wrap}
.logo{font:800 26px/1 "Big Shoulders Display",sans-serif;text-decoration:none;letter-spacing:.02em}
.logo span{color:var(--fire)}
.top nav{margin-inline-start:auto;display:flex;gap:6px;flex-wrap:wrap}
.top nav a{text-decoration:none;color:var(--dim);padding:10px 12px;border-radius:8px;min-height:44px;display:inline-flex;align-items:center}
.top nav a:hover,.top nav a:focus-visible{color:var(--ink);background:var(--bg2)}
:focus-visible{outline:2px solid var(--fire);outline-offset:2px}
h1,h2,h3{font-family:"Big Shoulders Display",sans-serif;line-height:1.05;text-wrap:balance;margin:0}
h1{font-size:clamp(36px,5vw,52px);font-weight:800}
h2{font-size:32px;font-weight:800;margin:48px 0 14px}
h3{font-size:22px;font-weight:600;margin:24px 0 8px;color:var(--steel)}
.hero{background:radial-gradient(ellipse 70% 90% at 80% 0%,#2a1a10 0%,transparent 60%),radial-gradient(ellipse 60% 80% at 10% 100%,#0f1c2e 0%,transparent 60%)}
.hero p{color:var(--dim);max-width:62ch;font-size:17px;margin:14px 0 0}
.filters{display:flex;gap:10px;flex-wrap:wrap;margin-top:26px}
.filters input{font:16px Inter,sans-serif;background:var(--bg2);border:1px solid var(--line);color:var(--ink);border-radius:10px;padding:11px 14px;min-height:44px;width:min(380px,100%)}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(min(280px,100%),1fr));gap:22px}
.card{display:block;text-decoration:none;background:var(--bg2);border:1px solid var(--line);border-radius:14px;overflow:hidden;transition:transform .25s,border-color .25s}
.card:hover,.card:focus-visible{transform:translateY(-4px);border-color:var(--fire)}
.card .img{aspect-ratio:16/9;background:#000 center/cover no-repeat;position:relative}
.card .img::after{content:"";position:absolute;inset:0;background:linear-gradient(transparent 55%,rgba(0,0,0,.75))}
.card .dur{position:absolute;right:10px;bottom:8px;z-index:1;font-size:13px;background:rgba(0,0,0,.6);padding:2px 8px;border-radius:6px}
.card .txt{padding:16px 18px 18px}
.card h3{margin:0 0 6px;color:var(--ink);font-size:24px}
.card .meta{color:var(--dim);font-size:14px}
.card .seq{color:var(--fire);font-size:14px;margin-top:6px}
.empty{color:var(--dim);padding:30px 0}
.add{border:1px dashed var(--line);border-radius:14px;display:flex;align-items:center;justify-content:center;text-align:center;color:var(--dim);padding:24px;min-height:200px;font-size:15px}
/* page film */
.back{display:inline-flex;align-items:center;gap:6px;color:var(--dim);text-decoration:none;min-height:44px;margin-bottom:8px}
.back:hover{color:var(--ink)}
.ftitle .sub{color:var(--fire);font-size:17px;margin-top:8px}
.ftitle .meta{color:var(--dim);margin-top:6px}
.player{margin-top:24px;background:#000;border-radius:14px;overflow:hidden;border:1px solid var(--line);box-shadow:0 30px 80px -30px rgba(255,122,26,.25)}
.player video{display:block;width:100%;aspect-ratio:16/9;background:#000}
.frise{display:flex;gap:4px;padding:10px;background:var(--bg2);flex-wrap:wrap}
.frise button{flex:var(--w) 1 0;min-width:120px;text-align:start;background:#1b2230;border:1px solid var(--line);color:var(--dim);border-radius:8px;padding:8px 10px;font:14px/1.35 Inter,sans-serif;cursor:pointer;min-height:44px;position:relative;overflow:hidden}
.frise button b{display:block;color:var(--ink);font-weight:600}
.frise button.on{border-color:var(--fire);color:var(--ink)}
.frise button .pg{position:absolute;left:0;bottom:0;height:3px;background:var(--fire);width:0}
.layout{display:grid;grid-template-columns:220px minmax(0,1fr);gap:48px;margin-top:20px}
.toc{position:sticky;top:84px;align-self:start;display:flex;flex-direction:column;gap:2px;font-size:15px}
.toc a{text-decoration:none;color:var(--dim);padding:8px 12px;border-inline-start:2px solid var(--line)}
.toc a.on,.toc a:hover{color:var(--ink);border-color:var(--fire)}
.ana{max-width:72ch}
.ana p,.ana li{color:#d3d9e2}
.ana ul,.ana ol{padding-inline-start:1.2em}
.ana li{margin:6px 0}
.ana strong{color:var(--ink);font-weight:600}
.ana em{color:var(--steel);font-style:italic}
.ana h2:first-child{margin-top:0}
.ana h2 .n{color:var(--fire);margin-inline-end:10px}
.tc{font:600 13px/1 Inter,sans-serif;background:rgba(255,122,26,.14);color:var(--fire);border:1px solid rgba(255,122,26,.35);border-radius:6px;padding:4px 7px;cursor:pointer;white-space:nowrap;vertical-align:1px}
.tc:hover{background:var(--fire);color:#111}
.note{border-inline-start:3px solid var(--steel);background:var(--bg2);padding:12px 16px;border-radius:0 10px 10px 0;color:var(--dim);font-size:15px}
.gloss{display:flex;flex-direction:column;gap:12px}
.gloss div{background:var(--bg2);border:1px solid var(--line);border-radius:12px;padding:12px 14px}
.gloss b{display:block;font:600 15px Inter,sans-serif;color:var(--fire);margin-bottom:6px}
.chips{display:flex;flex-wrap:wrap;gap:6px}
.chips span{font-size:14px;background:#1b2230;border-radius:999px;padding:4px 10px;color:#d3d9e2}
.tip{color:var(--dim);font-size:14px;margin-top:10px}
footer{border-top:1px solid var(--line);color:var(--dim);font-size:14px;text-align:center}
@media(max-width:900px){.layout{grid-template-columns:minmax(0,1fr)}.toc{position:static;flex-direction:row;flex-wrap:nowrap;overflow-x:auto;padding-bottom:6px}.toc a{flex:none;border-inline-start:0;border-bottom:2px solid var(--line)}}
@media(max-width:600px){.frise button{min-width:0;flex-basis:100%}}
@media(prefers-reduced-motion:reduce){.card{transition:none}.card:hover{transform:none}}
</style>
</head>
<body>
<header class="top"><div class="wrap">
  <a class="logo" href="#accueil">Carnet <span>CAA</span></a>
  <nav><a href="#accueil">Les films</a><a href="#lexique">Lexique</a></nav>
</div></header>
<main id="app"></main>
<footer class="band">Culture artistique et audiovisuelle · BTS Audiovisuel · Extraits utilisés à des fins pédagogiques</footer>

<script>
{
/* ===== LES FILMS : ajouter un objet ici pour chaque nouvelle analyse ===== */
const FILMS = [
{
  id:"amon-din",
  titre:"Le Seigneur des Anneaux : Le Retour du Roi",
  sequence:"Les feux d'alarme d'Amon Dîn",
  real:"Peter Jackson", annee:2003, pays:"Nouvelle-Zélande / États-Unis",
  video:"videos/amon-din.mp4", poster:"poster.jpg", duree:"3:52",
  notions:["Plans aériens","Contraste chaud/froid","Ellipse","Montage rythmique"],
  frise:[
    {de:0,a:55,t:"Minas Tirith",d:"Pippin allume la balise"},
    {de:55,a:85,t:"Gandalf",d:"Le regard sur le feu qui s'étend"},
    {de:85,a:159,t:"Le relais",d:"De sommet en sommet jusqu'à Edoras"}
  ],
  analyse:`
## Présentation
- **Film** : *Le Retour du Roi*, Peter Jackson, 2003, Nouvelle-Zélande / États-Unis, 11 Oscars en 2004 dont celui du meilleur film. Format scope (2.39:1, bandes noires visibles dans l'extrait).
- **Situation** : Gondor est menacé par Mordor. Pippin allume la première balise, et le signal d'alarme se transmet de sommet en sommet jusqu'au royaume de Rohan.
- **Problématique** : comment la mise en scène transforme-t-elle un geste simple (allumer un feu) en événement épique ?

## Structure du récit
Séquence en 3 temps :
1. **0:00 à 0:55** : dans la tour de Minas Tirith, l'allumage de la balise, avec la tension et l'hésitation de Pippin.
2. **0:55 à 1:25** : réaction de Gandalf, qui regarde le feu s'étendre au loin.
3. **1:25 à 2:39** : le relais des balises dans les montagnes, du crépuscule jusqu'à l'aube, puis l'arrivée à Edoras.

- **Récit linéaire**, avec **ellipses** (le feu saute de sommet en sommet sans qu'on voie le trajet).
- **Alternance de lieux** : l'intimité de la tour contre l'immensité des montagnes.
- **Gradation** : tension, puis soulagement, puis souffle épique.
- **Point de vue** : externe, avec une **focalisation interne** sur Pippin au début, puis sur le regard de Gandalf.

## L'image
### Échelle de plans
- **Plan d'ensemble** sur le beffroi perché (0:00, 0:05) : le personnage sur le pont est minuscule face à la roche.
- **Plan rapproché / gros plan** sur Pippin (0:15, 0:35 à 0:45) : on lit son trouble.
- **Plan rapproché poitrine** sur Gandalf (0:25, 1:00, 1:20) : le sage, calme.
- **Plan moyen** sur les soldats devant la balise (0:30).
- **Plans généraux / plans d'ensemble** des paysages de montagne (0:55, 1:25 à 2:30) : plus de la moitié de la séquence.
- **Plan moyen / général** à 2:30 : une silhouette sous un porche face aux montagnes (probablement Edoras).
### Angles
- **Contre-plongée** sur le beffroi (0:00) : le lieu semble inaccessible et solennel.
- **Plongée** sur la tour (0:05) : on mesure le vide qui l'entoure.
- **Plongée** sur les paysages depuis l'hélicoptère, qui dominent les montagnes.
- **Hauteur d'yeux** sur Gandalf (1:05, 1:15) pour rester proche de lui.
### Composition
- **Premier plan / arrière-plan** : la paille, la roche et les fruits au premier plan (0:10 à 0:25), la silhouette du soldat devant la balise (0:30).
- **Plan sur l'épaule** (1:10) : on voit les cheveux de Gandalf au premier plan et le paysage au fond. Le spectateur regarde avec lui.
- **Hors-champ** : le regard de Gandalf est hors cadre (1:00), le spectateur doit attendre le plan suivant pour voir ce qu'il regarde.
- **Règle des tiers** sur les plans de crêtes (1:35 à 1:50) : le feu est décentré, la montagne occupe les deux tiers de l'image.
- **Cadre dans le cadre** (2:30) : le porche encadre le personnage.
- **Profondeur de champ** : grande sur les paysages (tout est net), plus faible sur les gros plans de Pippin.

## La lumière et la couleur
- **Tour de Minas Tirith (0:00 à 1:20)** : lumière **froide**, ciel gris, grisaille et contrastes marqués ; **lueur rougeâtre de Mordor** à l'horizon (0:30), qui évoque la menace.
- **Le feu** (orange vif) est la **source de lumière chaude** dans un monde bleu-gris. C'est le **point focal** de l'image (0:40, 1:35 à 1:50).
- **Les montagnes** (1:25 à 2:30) passent du **crépuscule** (1:25, ciel bleu froid) à la **nuit bleue** (2:00, 2:05) puis à l'**aube rosée** (2:15 à 2:25). Le temps passe, ce qui indique la distance parcourue par le signal.
- **Contre-jour et silhouettes** (0:30, 2:30) : le personnage devient une forme sombre, presque un symbole.
- **Palette** : bleus, gris, orange. Le **contraste chaud/froid** structure toute l'image.

## Les mouvements de caméra
- **Plans aériens** (hélicoptère ou drone) : de 1:25 à 2:30 environ, la caméra **survole** les sommets, s'approche de la balise et passe au-dessus des nuages. Ce sont des **travellings aériens**, très fluides.
- **Plan fixe** sur Gandalf (1:15 à 1:20), qui laisse la place à son expression.
- **Caméra portée / mobile** sur Pippin (0:20, 0:35) : le mouvement et le flou donnent de la nervosité, comme si on était dans la scène.
- **Panoramique** possible pour garder le feu dans le cadre pendant le survol.

## Le montage
- **Rythme rapide au début** : les plans autour de 0:35 à 0:45 sont très courts (coupes à 34.9, 35.3, 36.3, 37.5, 42.3, 45.2 s), ce qui crée la tension de l'allumage.
- **Rythme lent ensuite** : des plans longs (1:25 à 1:54 environ, puis 2:00 à 2:15) pour le survol. C'est un moment de contemplation.
- **Champ / contrechamp** et **raccord de regard** entre Gandalf et le paysage (1:10 à 1:20).
- **Montage alterné** entre l'intérieur de la tour et le feu vu de loin (0:55).
- **Fondus enchaînés** probables entre les paysages, car les changements de lumière (crépuscule, nuit, aube) arrivent sans coupe nette.
- **Ellipse** : on passe du premier feu à la dernière balise sans montrer les relais intermédiaires.

## Le son
> Lecture d'après le film : à confirmer en réécoutant l'extrait.
- **Musique extradiégétique** : thème orchestral (Howard Shore) qui monte en puissance pendant le survol. La musique est le **moteur émotionnel** de la séquence.
- **Dialogues** rares : l'image porte l'essentiel du récit.
- **Sons diégétiques** : vent, crépitement du feu, métal des armures.
- **Silence relatif** avant l'allumage, pour faire monter la tension.

## Mise en scène : décor, costumes, jeu
- **Décor** : citadelle blanche et pierre grise, montagnes réelles de Nouvelle-Zélande mêlées à des décors reconstitués (le beffroi est en partie numérique).
- **Verticalité** : tout se passe en hauteur (tour, sommets), image du pouvoir et de la vigilance.
- **Costumes** : Gandalf en **blanc** (pureté, guide), armures de Gondor en gris argenté, Pippin en tenue sombre : le petit contre les grands.
- **Jeu des acteurs** : regards, souffle et hésitation chez Pippin, calme solennel chez Gandalf.
- **Objets** : la torche et la paille (l'allumage) puis la balise.

## Interprétation
Un geste minuscule (une torche) déclenche un événement immense : la séquence place le plus petit des personnages (un hobbit) au cœur du destin d'un royaume. La **mise en scène oppose l'intime et le monumental** : gros plans nerveux dans la tour, puis plans d'ensemble majestueux dans les montagnes. Le **feu** (espoir, solidarité) traverse un paysage glacé et mène à la réponse de Rohan. La **lumière** montre la durée et la distance, la **musique** donne l'ampleur épique.
`,
  termes:{
    "Plans":["plan d'ensemble","plan général","plan moyen","plan rapproché","gros plan"],
    "Angles":["plongée","contre-plongée","hauteur d'yeux"],
    "Mouvements":["plan fixe","travelling aérien","panoramique","caméra portée"],
    "Composition":["premier plan / arrière-plan","hors-champ","règle des tiers","cadre dans le cadre","profondeur de champ"],
    "Lumière":["contraste chaud/froid","contre-jour","silhouette","point focal"],
    "Montage":["rythme","champ / contrechamp","raccord de regard","montage alterné","ellipse","fondu enchaîné"],
    "Son":["musique extradiégétique","diégétique","silence"],
    "Récit":["séquence","gradation","focalisation"]
  }
}
];

/* ===== outils ===== */
const app=document.getElementById('app');
const esc=s=>String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const toSec=t=>{const[m,s]=t.split(':').map(Number);return m*60+s};
const fmt=s=>Math.floor(s/60)+':'+String(Math.floor(s%60)).padStart(2,'0');
const slug=s=>s.normalize('NFD').replace(/[̀-ͯ]/g,'').toLowerCase().replace(/[^a-z0-9]+/g,'-').replace(/^-|-$/g,'');
function inline(s){
  s=esc(s).replace(/\*\*(.+?)\*\*/g,'<strong>$1</strong>').replace(/\*(.+?)\*/g,'<em>$1</em>');
  return s.replace(/\b(\d{1,2}:\d{2})\b/g,(m)=>`<button class="tc" data-t="${toSec(m)}" title="Aller à ${m} dans l'extrait">${m}</button>`);
}
function md(src){
  let out='',list=null,n=0;const toc=[];
  const close=()=>{if(list){out+=`</${list}>`;list=null}};
  for(const raw of src.trim().split('\n')){
    const l=raw.trim();
    if(!l){close();continue}
    let m;
    if(m=l.match(/^## (.+)/)){close();n++;const id='s-'+slug(m[1]);toc.push([id,m[1]]);out+=`<h2 id="${id}"><span class="n">${n}</span>${esc(m[1])}</h2>`}
    else if(m=l.match(/^### (.+)/)){close();out+=`<h3>${esc(m[1])}</h3>`}
    else if(m=l.match(/^> (.+)/)){close();out+=`<p class="note">${inline(m[1])}</p>`}
    else if(m=l.match(/^- (.+)/)){if(list!=='ul'){close();out+='<ul>';list='ul'}out+=`<li>${inline(m[1])}</li>`}
    else if(m=l.match(/^\d+\. (.+)/)){if(list!=='ol'){close();out+='<ol>';list='ol'}out+=`<li>${inline(m[1])}</li>`}
    else{close();out+=`<p>${inline(l)}</p>`}
  }
  close();return{html:out,toc};
}

/* ===== accueil ===== */
function home(q=''){
  const k=slug(q);
  const list=FILMS.filter(f=>!k||slug([f.titre,f.sequence,f.real,f.annee,...f.notions].join(' ')).includes(k));
  app.innerHTML=`
  <section class="band hero"><div class="wrap">
    <h1>Mes analyses de séquences</h1>
    <p>Culture artistique et audiovisuelle : chaque fiche réunit l'extrait du film et son analyse détaillée (récit, cadrage, lumière, caméra, montage, son, mise en scène). Les timecodes de l'analyse sont cliquables et font avancer la vidéo jusqu'au bon moment.</p>
    <div class="filters"><input id="q" type="search" placeholder="Chercher un film, un réalisateur, une notion…" value="${esc(q)}" aria-label="Rechercher"></div>
  </div></section>
  <section class="band" style="padding-top:8px"><div class="wrap">
    <div class="grid">${list.map(f=>`
      <a class="card" href="#${f.id}">
        <div class="img" style="background-image:url('${esc(f.poster)}')"><span class="dur">${esc(f.duree)}</span></div>
        <div class="txt"><h3>${esc(f.titre)}</h3>
          <div class="meta">${esc(f.real)} · ${f.annee}</div>
          <div class="seq">${esc(f.sequence)}</div></div>
      </a>`).join('')}
      ${k?'':`<div class="add">Prochaine analyse à venir</div>`}
    </div>
    ${list.length?'':`<p class="empty">Aucun film ne correspond à « ${esc(q)} ».</p>`}
  </div></section>`;
  const inp=document.getElementById('q');
  inp.addEventListener('input',()=>{const v=inp.value;home(v);const i=document.getElementById('q');i.focus();i.setSelectionRange(v.length,v.length)});
}

/* ===== lexique ===== */
function lexique(){
  const all={};
  FILMS.forEach(f=>Object.entries(f.termes).forEach(([c,ts])=>{all[c]=all[c]||new Set();ts.forEach(t=>all[c].add(t))}));
  app.innerHTML=`<section class="band hero"><div class="wrap">
    <h1>Lexique de l'analyse filmique</h1>
    <p>Tous les termes techniques utilisés dans mes fiches, regroupés par catégorie. À réutiliser en contrôle et à l'examen.</p>
  </div></section>
  <section class="band" style="padding-top:8px"><div class="wrap"><div class="grid">
    ${Object.entries(all).map(([c,s])=>`<div class="gloss"><div><b>${esc(c)}</b><div class="chips">${[...s].map(t=>`<span>${esc(t)}</span>`).join('')}</div></div></div>`).join('')}
  </div></div></section>`;
}

/* ===== page film ===== */
function film(f){
  const {html,toc}=md(f.analyse);
  const tot=f.frise.reduce((a,p)=>a+(p.a-p.de),0);
  app.innerHTML=`<section class="band" style="padding-bottom:0"><div class="wrap">
    <a class="back" href="#accueil">← Tous les films</a>
    <div class="ftitle"><h1>${esc(f.titre)}</h1>
      <div class="sub">Séquence : ${esc(f.sequence)}</div>
      <div class="meta">${esc(f.real)} · ${f.annee} · ${esc(f.pays)}</div></div>
    <div class="player">
      <video id="v" controls preload="metadata" playsinline poster="${esc(f.poster)}" src="${esc(f.video)}"></video>
      <div class="frise">${f.frise.map((p,i)=>`<button data-i="${i}" data-t="${p.de}" style="--w:${((p.a-p.de)/tot*10).toFixed(2)}"><b>${i+1}. ${esc(p.t)}</b>${fmt(p.de)} – ${fmt(p.a)} · ${esc(p.d)}<span class="pg"></span></button>`).join('')}</div>
    </div>
  </div></section>
  <section class="band"><div class="wrap layout">
    <nav class="toc" aria-label="Sommaire">${toc.map(([id,t])=>`<a href="#${f.id}" data-go="${id}">${esc(t)}</a>`).join('')}<a href="#${f.id}" data-go="s-termes">Termes à retenir</a></nav>
    <article class="ana">${html}
      <h2 id="s-termes"><span class="n">★</span>Termes techniques à retenir</h2>
      <div class="gloss">${Object.entries(f.termes).map(([c,ts])=>`<div><b>${esc(c)}</b><div class="chips">${ts.map(t=>`<span>${esc(t)}</span>`).join('')}</div></div>`).join('')}</div>
      <p class="tip">Astuce : clique sur un timecode orange pour revoir le passage dans l'extrait.</p>
    </article>
  </div></section>`;
  const v=document.getElementById('v');
  const seek=t=>{v.currentTime=t;v.play().catch(()=>{});document.querySelector('.player').scrollIntoView({behavior:matchMedia('(prefers-reduced-motion:reduce)').matches?'auto':'smooth',block:'start'})};
  app.querySelectorAll('[data-t]').forEach(b=>b.addEventListener('click',()=>seek(+b.dataset.t)));
  app.querySelectorAll('[data-go]').forEach(a=>a.addEventListener('click',e=>{e.preventDefault();document.getElementById(a.dataset.go)?.scrollIntoView({behavior:'smooth'})}));
  const btns=[...app.querySelectorAll('.frise button')];
  v.addEventListener('timeupdate',()=>{const t=v.currentTime;f.frise.forEach((p,i)=>{const on=t>=p.de&&t<p.a;btns[i].classList.toggle('on',on);btns[i].querySelector('.pg').style.width=(t>=p.a?100:on?(t-p.de)/(p.a-p.de)*100:0)+'%'})});
  const links=[...app.querySelectorAll('.toc a')];
  const spy=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting)links.forEach(l=>l.classList.toggle('on',l.dataset.go===e.target.id))}),{rootMargin:'-20% 0px -70% 0px'});
  app.querySelectorAll('.ana h2[id]').forEach(h=>spy.observe(h));
}

function route(){
  const h=location.hash.slice(1);
  const f=FILMS.find(x=>x.id===h);
  if(f)film(f);else if(h==='lexique')lexique();else home();
  window.scrollTo(0,0);
}
window.addEventListener('hashchange',route);
route();
}
</script>
</body>
</html>
