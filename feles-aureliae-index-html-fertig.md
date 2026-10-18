# Feles Aureliae - FERTIGE Einzeldatei (index.html) v3 Simon-Style

**Diese eine Datei ist das KOMPLETTE Spiel.** Kein Zusammenbauen mehr noetig!

## Schritte
1. Dieses Dokument in der Bibliothek oeffnen.
2. Ueber Download-Symbol herunterladen.
3. Heruntergeladene Datei in index.html umbenennen (falls als .md gespeichert).
4. Auf github.com/Fichtenelch86/feles-aureliae ueber "uploading an existing file" hochladen.
5. Settings -> Pages -> Branch: main -> Save.
6. Spielen unter https://fichtenelch86.github.io/feles-aureliae/

Oder direkt am Mac/PC: als index.html speichern, Doppelklick, spielen.

## Vollstaendiger HTML-Quellcode

```html
<!DOCTYPE html>
<html lang="la">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Feles Aureliae – Ceres Festum</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body {
  background: #1a1410;
  color: #e8dcc8;
  font-family: Georgia, 'Times New Roman', serif;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
#title-screen {
  text-align: center;
  max-width: 640px;
  padding: 40px 20px;
}
#title-screen h1 {
  font-size: 3em;
  letter-spacing: 0.15em;
  color: #d4a545;
  text-shadow: 2px 2px 0 #4a3316;
}
.subtitle { font-style: italic; color: #b8a284; margin: 8px 0 40px; }
.char-select p { font-size: 1.3em; margin-bottom: 14px; color: #e8dcc8; }
.char-cards { display: flex; gap: 24px; justify-content: center; }
.char-card {
  background: #2b2216;
  border: 2px solid #6b532e;
  padding: 18px 22px;
  cursor: pointer;
  color: #e8dcc8;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  transition: border-color .2s, transform .2s;
}
.char-card:hover { border-color: #d4a545; transform: translateY(-3px); }
.char-art { width: 80px; height: 80px; image-rendering: pixelated; background: #171310; }
.char-name { font-size: 1.4em; color: #d4a545; }
.char-desc { font-size: .85em; color: #b8a284; font-style: italic; }
.hint-start { margin-top: 40px; color: #9b8465; font-style: italic; }

#game { position: relative; width: 1000px; max-width: 96vw; }
#stage-wrap { position: relative; width: 100%; }
#stage { width: 100%; display: block; image-rendering: pixelated; border: 3px solid #4a3a22; }
#overlay { position: absolute; inset: 0; pointer-events: none; }

#ui-top {
  display: flex; justify-content: space-between; align-items: center;
  background: #241b10; border: 2px solid #4a3a22; border-top: none;
  padding: 6px 14px; font-size: .95em;
}
#scene-name { color: #d4a545; letter-spacing: .08em; }
#verba-counter { color: #8fc98f; }

#ui-side {
  position: absolute; top: 8px; right: 8px;
  background: rgba(26, 20, 14, .92);
  border: 2px solid #4a3a22;
  padding: 10px 12px;
  width: 190px;
  font-size: .85em;
}
#ui-side h3 { color: #d4a545; letter-spacing: .15em; margin-bottom: 8px; }
#inventory { list-style: none; min-height: 30px; }
#inventory li {
  padding: 3px 6px; margin-bottom: 3px;
  background: #32271a; cursor: pointer; border: 1px solid #4a3a22;
}
#inventory li.selected { border-color: #d4a545; background: #4a3a1c; }
#inventory li:hover { border-color: #9b7d3f; }
#combine-hint { color: #9b8465; font-size: .85em; font-style: italic; }

#dialog-box {
  position: absolute; left: 4%; right: 4%; bottom: 4%;
  background: rgba(20, 15, 10, .95);
  border: 2px solid #d4a545;
  padding: 14px 40px 14px 16px;
  min-height: 90px;
}
#speaker { color: #d4a545; font-weight: bold; letter-spacing: .1em; margin-bottom: 4px; }
#text { line-height: 1.45; }
#choices { margin-top: 10px; display: flex; flex-direction: column; gap: 6px; }
#choices button {
  background: #32271a; color: #e8dcc8; border: 1px solid #9b7d3f;
  padding: 6px 10px; cursor: pointer; text-align: left; font-family: inherit;
  font-size: .95em;
}
#choices button:hover { background: #4a3a1c; border-color: #d4a545; }
#dialog-next {
  position: absolute; right: 10px; bottom: 8px;
  color: #d4a545; cursor: pointer; animation: bounce 1s infinite;
}
@keyframes bounce { 0%,100% { transform: translateY(0); } 50% { transform: translateY(3px); } }

#feles-box {
  position: absolute; top: 8px; left: 8px;
  max-width: 300px;
  background: rgba(26, 20, 14, .95);
  border: 2px solid #c98a4b;
  padding: 10px 34px 10px 12px;
}
#feles-text::before { content: "🐱 "; }
#feles-text { font-style: italic; color: #e8c9a0; line-height: 1.4; }
#feles-close {
  position: absolute; top: 4px; right: 6px;
  background: none; border: none; color: #c98a4b; cursor: pointer; font-size: 1em;
}

</style>
</head>
<body>
<div id="title-screen">
  <h1>FELES AURELIAE</h1>
<p class="subtitle">Ceres Festum – Ludus Latinus</p>
<div class="char-select">
<p>Quis es?</p>
<div class="char-cards">
<button class="char-card" data-char="lucius">
<div class="char-art" id="art-lucius"></div>
<span class="char-name">Lucius</span>
<span class="char-desc">Puer audax – vias breves amat</span>
</button>
<button class="char-card" data-char="aurelia">
<div class="char-art" id="art-aurelia"></div>
<span class="char-name">Aurelia</span>
<span class="char-desc">Puella callida – vias latentes amat</span>
</button>
</div>
</div>
<p class="hint-start">Feles Aureliae tibi semper auxilium dat!</p>
</div>

<div id="game" hidden>
<div id="stage-wrap">
<canvas id="stage" width="640" height="360"></canvas>
<div id="overlay"></div>
</div>
<div id="ui-top">
<div id="location-bar"><span id="scene-name"></span></div>
<div id="verba-counter">VERBA: <b id="verba-count">0</b></div>
</div>
<div id="ui-side">
<h3>SACCA</h3>
<ul id="inventory"></ul>
<div id="combine-hint">Duo lecta = combina!</div>
</div>
<div id="dialog-box" hidden>
<div id="speaker"></div>
<div id="text"></div>
<div id="choices"></div>
<div id="dialog-next">➤</div>
</div>
<div id="feles-box" hidden>
<div id="feles-text"></div>
<button id="feles-close">✕</button>
</div>
</div>

<script>
// Vocabularium – final abgenommen
// Grundlagenwortschatz (wiederkehrend) + Spezialwortschatz (★ mit Feles-Tipp)
// Nur Nom./Akk. Sg., Verben nur a/e-Konjugation Präsens.

const VOCAB = {
  // ----- Grundlagenwortschatz -----
  grundlagen: [
    { la: "puer", de: "der Junge" },
    { la: "puella", de: "das Mädchen" },
    { la: "vir", de: "der Mann" },
    { la: "mulier", de: "die Frau" },
    { la: "feles", de: "die Katze" },
    { la: "canis", de: "der Hund" },
    { la: "domus", de: "das Haus" },
    { la: "ianua", de: "die Tür" },
    { la: "via", de: "der Weg, die Straße" },
    { la: "hortus", de: "der Garten" },
    { la: "aqua", de: "das Wasser" },
    { la: "cibus", de: "das Essen" },
    { la: "panis", de: "das Brot" },
    { la: "vinum", de: "der Wein" },
    { la: "pecunia", de: "das Geld" },
    { la: "sacca", de: "die Tasche (Inventar)" },
    { la: "nox", de: "die Nacht" },
    { la: "dies", de: "der Tag" },
    { la: "verbum", de: "das Wort" },
    { la: "verba", de: "die Wörter" },
    { la: "amicus", de: "der Freund" },
    { la: "terra", de: "die Erde, das Land" }
  ],
  // ----- Spezialwortschatz mit ★ und Feles-Tipp -----
  spezial: [
    { la: "Ceres", de: "Ceres (Göttin des Wachstums)", tipp: "Ceres est dea frugum – terra fructum dat!" },
    { la: "festum", de: "das Fest", tipp: "Festum est dies laetitiae!" },
    { la: "templum", de: "der Tempel", tipp: "Templum est casa deorum." },
    { la: "ara", de: "der Altar", tipp: "In ara ignis et dona sunt." },
    { la: "dona", de: "die Geschenke, Gaben", tipp: "Dona deis data – dei laeti!" },
    { la: "corona", de: "der Kranz, die Krone", tipp: "Corona ex floribus facta est." },
    { la: "flos", de: "die Blume", tipp: "Flores in horto crescunt." },
    { la: "frumentum", de: "das Getreide", tipp: "Frumentum in campo crescit – panis ex eo fit." },
    { la: "annona", de: "das Getreideangebot, der Marktpreis", tipp: "Annona bona = panis vilis!" },
    { la: "cista", de: "die Kiste", tipp: "Cistam clausam – clavem quaere!" },
    { la: "clavis", de: "der Schlüssel", tipp: "Clavis ianuam aperit." },
    { la: "murmillo", de: "der Gladiator (mit Fischhelm)", tipp: "Murmillo in arena pugnat!" },
    { la: "thermae", de: "die Thermen, das Bad", tipp: "In thermis aqua calida est." },
    { la: "macellum", de: "der Markt", tipp: "In macello omnia emuntur." },
    { la: "taberna", de: "die Schenke, der Laden", tipp: "In taberna vinum bibitur!" },
    { la: "theatrum", de: "das Theater", tipp: "In theatro fabula agitur." },
    { la: "fabula", de: "die Geschichte", tipp: "Fabula narranda est!" },
    { la: "sagitta", de: "der Pfeil", tipp: "Sagitta volat, non quaeritur... sed hic iacet!" },
    { la: "stella", de: "der Stern", tipp: "Stellae in caelo lucent." },
    { la: "iam", de: "schon, jetzt", tipp: "Iam festum incipit!" },
    { la: "voco", de: "ich rufe", tipp: "Verba nova te vocant!" },
    { la: "video", de: "ich sehe", tipp: "Videsne felem?" },
    { la: "habeo", de: "ich habe", tipp: "Omnia in saccum habes." },
    { la: "do", de: "ich gebe", tipp: "Da mihi panem!" },
    { la: "emo", de: "ich kaufe", tipp: "Eme in macello!" },
    { la: "sum", de: "ich bin", tipp: "Feles sum – ego sum auxilium tuum!" }
  ]
};

// Flache Suchkarte für die Verba-Register-Mechanik
const VERBA_MAP = {};
[...VOCAB.grundlagen, ...VOCAB.spezial].forEach(v => { VERBA_MAP[v.la] = v; });

</script>
<script>
// scenes.js – 10 Szenen im Simon-the-Sorcerer-Stil (640x360)
// Stilmerkmale: kräftige schwarze Outlines, karikaturhafte Figuren mit
// übergroßen Köpfen und Comic-Augen, gesättigte Farben.
// Hotspots und Spiellogik sind gegenüber v2.1 exakt unverändert.

const SCENES = {};

// ---------- Simon-Style-Zeichen-Helfer ----------
// Rechteck mit Outline
function R(ctx, x, y, w, h, col, line) {
  x = Math.round(x); y = Math.round(y);
  w = Math.round(w); h = Math.round(h);
  if (line !== false) {
    ctx.fillStyle = "#141210";
    ctx.fillRect(x - 2, y - 2, w + 4, h + 4);
  }
  ctx.fillStyle = col;
  ctx.fillRect(x, y, w, h);
}
// Rechteck ohne Outline (für Schatten/Texturen)
function RN(ctx, x, y, w, h, col) {
  ctx.fillStyle = col;
  ctx.fillRect(Math.round(x), Math.round(y), Math.round(w), Math.round(h));
}
// Schachbrett-/Fliesenmuster mit Outline pro Kachel
function tiles(ctx, x, y, w, h, tw, th, c1, c2) {
  for (let ty = y; ty < y + h; ty += th) {
    for (let tx = x; tx < x + w; tx += tw) {
      const alt = ((tx / tw + ty / th) | 0) % 2 === 0;
      R(ctx, tx, ty, tw - 3, th - 3, alt ? c1 : c2);
    }
  }
}
// Himmel (Streifen ohne Outline)
function skyGradient(ctx, top, mid, bot) {
  RN(ctx, 0, 0, 640, 130, top);
  RN(ctx, 0, 130, 640, 60, mid);
  RN(ctx, 0, 190, 640, 170, bot);
}
// Wolke mit Outline
function cloud(ctx, x, y, s) {
  s = s || 1;
  R(ctx, x, y + 4 * s, 30 * s, 10 * s, "#f8f4ec");
  R(ctx, x + 5 * s, y, 14 * s, 8 * s, "#f8f4ec");
  R(ctx, x + 17 * s, y + 2 * s, 11 * s, 8 * s, "#f8f4ec");
  RN(ctx, x + 2 * s, y + 11 * s, 26 * s, 2 * s, "#d8d4cc");
}
// Cartoon-Baum: runde Krone mit Outline und Blob-Textur
function tree(ctx, x, y, s) {
  s = s || 1;
  // Stamm mit Outline
  R(ctx, x + 8 * s, y, 9 * s, 34 * s, "#7a4c22");
  RN(ctx, x + 10 * s, y + 2, 3 * s, 30 * s, "#96602e");
  // Wurzeln
  R(ctx, x + 2 * s, y + 30 * s, 8 * s, 5 * s, "#7a4c22");
  R(ctx, x + 16 * s, y + 30 * s, 8 * s, 5 * s, "#5e3a18");
  // Krone: drei überlappende Kreise als Rechtecke (Blob-Look)
  R(ctx, x - 12 * s, y - 14 * s, 50 * s, 26 * s, "#3a8a32");
  R(ctx, x - 6 * s, y - 26 * s, 36 * s, 20 * s, "#46a03c");
  R(ctx, x + 2 * s, y - 32 * s, 22 * s, 14 * s, "#52b446");
  // Highlights (ohne Outline)
  RN(ctx, x - 4 * s, y - 22 * s, 10 * s, 5 * s, "#68c458");
  RN(ctx, x + 12 * s, y - 28 * s, 8 * s, 4 * s, "#68c458");
  RN(ctx, x - 8 * s, y - 2 * s, 12 * s, 5 * s, "#2c6a26");
  RN(ctx, x + 20 * s, y - 8 * s, 14 * s, 6 * s, "#2c6a26");
}
// Busch mit Outline
function bush(ctx, x, y, s) {
  s = s || 1;
  R(ctx, x, y + 4 * s, 26 * s, 10 * s, "#3a8a32");
  R(ctx, x + 4 * s, y, 10 * s, 8 * s, "#46a03c");
  R(ctx, x + 14 * s, y + 2 * s, 10 * s, 7 * s, "#46a03c");
  RN(ctx, x + 7 * s, y + 1 * s, 5 * s, 3 * s, "#68c458");
  RN(ctx, x + 3 * s, y + 10 * s, 9 * s, 3 * s, "#2c6a26");
}
// Wasser mit animierten Wellen und Umriss
function water(ctx, x, y, w, h, t) {
  // Becken-Umriss
  RN(ctx, x - 3, y - 3, w + 6, h + 6, "#141210");
  RN(ctx, x, y, w, h, "#2a62a8");
  RN(ctx, x, y, w, 4, "#4a86cc");
  const ph = (t || 0) / 500;
  for (let i = 0; i < w; i += 18) {
    const yy = y + 8 + Math.sin(ph + i * 0.2) * 3;
    RN(ctx, x + i, yy, 11, 3, "#8ac0e8");
    if (i % 36 === 0) RN(ctx, x + i + 5, yy + 10, 7, 3, "#5a9ad0");
  }
  RN(ctx, x, y + h - 5, w, 5, "#1e4c8c");
}
// ---- Simon-Style-Cartoon-Figuren ----
// Übergroßer Kopf, Comic-Augen (weiß mit Pupille), klare Outlines.
// o: {skin, hair, tunic, trim, skirt, tunicDark, hat}
function person(ctx, x, y, o, t) {
  const bob = Math.sin((t || 0) / 600) * 1.5;
  const skin = o.skin || "#f0c090", dark = o.skinDark || "#d09868";
  RN(ctx, x - 15, y + 1, 30, 5, "rgba(16,12,8,0.3)"); // Bodenschatten
  // Beine + Schuhe (mit Outline)
  if (!o.skirt) {
    R(ctx, x - 9, y - 16, 7, 14, "#6a5838"); R(ctx, x + 2, y - 16, 7, 14, "#6a5838");
    R(ctx, x - 11, y - 5, 10, 6, "#3a2c20"); R(ctx, x + 1, y - 5, 10, 6, "#3a2c20");
  } else {
    R(ctx, x - 16, y - 18, 32, 18, o.tunic);
    RN(ctx, x - 16, y - 18, 32, 3, o.tunicDark || o.tunic);
    R(ctx, x - 10, y - 5, 7, 6, "#3a2c20"); R(ctx, x + 3, y - 5, 7, 6, "#3a2c20");
  }
  // Torso (klein, karikaturhaft) mit Falten-Streifen
  R(ctx, x - 14, y - 40, 28, 26, o.tunic);
  R(ctx, x - 14, y - 40, 28, 5, o.trim || o.tunic);
  RN(ctx, x - 7, y - 36, 3, 22, o.tunicDark || "rgba(0,0,0,0.15)");
  RN(ctx, x + 5, y - 34, 3, 20, o.tunicDark || "rgba(0,0,0,0.15)");
  // Toga-Bausch über der Schulter
  R(ctx, x - 17, y - 40, 9, 16, o.trim || o.tunic);
  // Arme (mit Outline) + Hände
  R(ctx, x - 19, y - 38, 6, 20, o.tunic);
  R(ctx, x + 13, y - 38, 6, 20, o.tunic);
  R(ctx, x - 19, y - 20, 6, 6, skin); R(ctx, x + 13, y - 20, 6, 6, skin);
  // ---- RIESIGER Kopf (Simon-Style) ----
  R(ctx, x - 15, y - 66 + bob, 30, 26, skin);
  RN(ctx, x - 15, y - 48, 30, 3, dark); // Kinn-Schatten
  // Haar (mit Outline)
  R(ctx, x - 16, y - 76 + bob, 32, 12, o.hair);
  R(ctx, x - 16, y - 66 + bob, 5, 12, o.hair);
  R(ctx, x + 11, y - 66 + bob, 5, 12, o.hair);
  // Ohren
  R(ctx, x - 18, y - 58 + bob, 4, 6, skin);
  R(ctx, x + 14, y - 58 + bob, 4, 6, skin);
  // Comic-Augen: große weiße Ovale mit Pupillen
  RN(ctx, x - 9, y - 60 + bob, 8, 10, "#ffffff");
  RN(ctx, x + 1, y - 60 + bob, 8, 10, "#ffffff");
  RN(ctx, x - 8, y - 56 + bob, 3, 4, "#141210");
  RN(ctx, x + 2, y - 56 + bob, 3, 4, "#141210");
  // Augenbrauen
  RN(ctx, x - 9, y - 62 + bob, 7, 2, o.hair);
  RN(ctx, x + 2, y - 62 + bob, 7, 2, o.hair);
  // Nase (klein, rund) und Mund (lächelnd)
  RN(ctx, x - 2, y - 52 + bob, 4, 3, dark);
  RN(ctx, x - 5, y - 47 + bob, 10, 3, "#a04838");
  RN(ctx, x - 3, y - 46 + bob, 6, 1, "#e8b0a0");
}
// Murmillo (Gladiator) mit Fischhelm + Schild
function murmilloSprite(ctx, x, y, t) {
  person(ctx, x, y, { skin: "#f0c090", hair: "#2a1a10", tunic: "#c8c8d8", trim: "#a0a0b4", tunicDark: "#9898ac" }, t);
  // Fischhelm (groß, mit Outline und Kamm)
  R(ctx, x - 16, y - 84, 32, 14, "#e8e8f0");
  RN(ctx, x - 16, y - 74, 32, 3, "#b8b8cc");
  R(ctx, x - 6, y - 96, 12, 13, "#e8e8f0");   // Kamm
  R(ctx, x - 8, y - 76, 4, 12, "#c0c0d4");    // Wangenschutz
  R(ctx, x + 4, y - 76, 4, 12, "#c0c0d4");
  RN(ctx, x - 14, y - 82, 28, 3, "#f8f8ff");  // Glanz
  // Schild (mit Outline und Boss)
  R(ctx, x + 16, y - 42, 12, 24, "#b07838");
  R(ctx, x + 18, y - 40, 8, 20, "#e0b058");
  RN(ctx, x + 20, y - 34, 3, 8, "#7a4c22");
}
// Feles (Katze), Simon-Style: großer Kopf, Comic-Augen
function cat(ctx, x, y, t) {
  const bob = Math.sin((t || 0) / 300) * 2;
  const fur = "#e0a840", dark = "#b8842a", cream = "#f8e0b0";
  RN(ctx, x - 3, y + 18, 40, 4, "rgba(16,12,8,0.28)"); // Schatten
  // Schweif (animiert, mit Outline)
  const tw = Math.sin((t || 0) / 400) * 5;
  R(ctx, x - 10, y + 4 + bob, 6, 5, fur);
  R(ctx, x - 14, y - 1 + bob + tw, 7, 7, fur);
  RN(ctx, x - 12, y - 3 + bob + tw, 3, 3, dark);
  // Körper (mit Outline)
  R(ctx, x, y + 6 + bob, 28, 14, fur);
  RN(ctx, x + 2, y + 12 + bob, 24, 6, cream);
  // Streifen
  RN(ctx, x + 5, y + 5 + bob, 4, 4, dark);
  RN(ctx, x + 13, y + 5 + bob, 4, 4, dark);
  RN(ctx, x + 21, y + 5 + bob, 4, 4, dark);
  // Beine (mit Outline)
  R(ctx, x + 2, y + 18, 6, 7, fur); R(ctx, x + 20, y + 18, 6, 7, fur);
  // ---- GROSSER Kopf ----
  R(ctx, x + 20, y - 8 + bob, 22, 18, fur);
  // Ohren (Dreiecke mit Outline)
  R(ctx, x + 20, y - 18 + bob, 7, 11, fur);
  R(ctx, x + 35, y - 18 + bob, 7, 11, fur);
  RN(ctx, x + 22, y - 15 + bob, 3, 5, "#8a5a20");
  RN(ctx, x + 37, y - 15 + bob, 3, 5, "#8a5a20");
  // Comic-Augen (weiß + Pupille)
  RN(ctx, x + 24, y - 4 + bob, 7, 8, "#ffffff");
  RN(ctx, x + 33, y - 4 + bob, 7, 8, "#ffffff");
  RN(ctx, x + 26, y - 1 + bob, 3, 3, "#2a8a3a");
  RN(ctx, x + 35, y - 1 + bob, 3, 3, "#2a8a3a");
  // Nase + Mund
  RN(ctx, x + 30, y + 4 + bob, 3, 3, "#d05868");
  RN(ctx, x + 27, y + 7 + bob, 8, 2, "#8a5a20");
  // Schnurrhaare
  RN(ctx, x + 42, y + 2 + bob, 7, 1, "rgba(20,16,10,0.5)");
  RN(ctx, x + 42, y + 5 + bob, 6, 1, "rgba(20,16,10,0.5)");
  RN(ctx, x + 18, y + 8 + bob, 6, 1, "rgba(20,16,10,0.5)");
  RN(ctx, x + 18, y + 5 + bob, 5, 1, "rgba(20,16,10,0.5)");
  // Brustfleck
  RN(ctx, x + 21, y + 9 + bob, 6, 5, cream);
}
// Sterne (funkelnd, mit Outline)
function stars(ctx, t) {
  for (let i = 0; i < 36; i++) {
    const x = (i * 89 + 13) % 640, y = (i * 53) % 200;
    if (Math.sin((t || 0) / 500 + i * 1.3) > -0.2) {
      RN(ctx, x, y, 3, 3, "#f8f4d8");
      if (i % 4 === 0) { RN(ctx, x - 2, y + 1, 7, 1, "#141210"); RN(ctx, x + 1, y - 2, 1, 7, "#141210"); }
    }
  }
}
// Steinboden mit Outline-Kacheln
function stoneFloor(ctx, y) {
  tiles(ctx, 0, y, 640, 360 - y, 40, 20, "#b09870", "#9c8458");
}
// Ziegelmauer
function brickWall(ctx, x, y, w, h) {
  tiles(ctx, x, y, w, h, 28, 14, "#c89868", "#b48554");
}
// Dach mit Outline-Ziegeln
function roofTiles(ctx, x, y, w, h) {
  tiles(ctx, x, y, w, h, 24, 12, "#c05848", "#a84838");
}
// Tür (mit Outline, Eisenbändern, Klinke)
function door(ctx, x, y, w, h) {
  R(ctx, x - 3, y - 3, w + 6, h + 6, "#5a4430"); // Rahmen
  R(ctx, x, y, w, h, "#a06a38");
  RN(ctx, x + 4, y + 4, w - 8, h - 8, "#b47a42");
  RN(ctx, x + 4, y + 4, w - 8, 4, "#c89258");
  R(ctx, x + w / 2 - 2, y, 4, h, "#6a4828"); // Fuge
  R(ctx, x + 5, y + h / 3, w - 10, 5, "#4a3a2a"); // Bänder
  R(ctx, x + 5, y + h * 2 / 3, w - 10, 5, "#4a3a2a");
  R(ctx, x + w - 12, y + h / 2 - 3, 7, 7, "#e8c040"); // Klinke
}
// Fenster (mit Outline, ggf. erleuchtet)
function windowFrame(ctx, x, y, w, h, lit) {
  R(ctx, x - 3, y - 3, w + 6, h + 6, "#5a4430");
  R(ctx, x, y, w, h, lit ? "#f8e890" : "#8ec0e0");
  R(ctx, x + w / 2 - 2, y, 4, h, "#5a4430");
  R(ctx, x, y + h / 2 - 2, w, 4, "#5a4430");
  if (lit) { RN(ctx, x + 3, y + 3, 6, 6, "#fdf4c0"); RN(ctx, x + w - 9, y + h - 9, 6, 6, "#fdf4c0"); }
}
// Fackel mit Outline und Flackerflamme
function torch(ctx, x, y, t) {
  const fl = Math.sin((t || 0) / 90) * 2;
  R(ctx, x - 3, y, 6, 16, "#6a4c2c");
  R(ctx, x - 5, y - 5, 10, 7, "#4a3828");
  // Flamme (mehrstufig, mit Umriss)
  R(ctx, x - 4, y - 13 + fl, 8, 9, "#f07030");
  RN(ctx, x - 2, y - 16 + fl, 4, 5, "#f8c040");
  RN(ctx, x - 1, y - 17 + fl, 2, 3, "#f8f0b0");
  RN(ctx, x, y + 16, 10, 3, "#4a3828");
}
// Altarfeuer mit Outline, animiert
function altarFire(ctx, x, y, t, big) {
  const s = big ? 2 : 1, fl = Math.sin((t || 0) / 80) * 3;
  R(ctx, x - 12 * s, y, 24 * s, 9 * s, "#c0a878");   // Altarstein
  R(ctx, x - 14 * s, y + 7 * s, 28 * s, 5 * s, "#a08858");
  R(ctx, x - 7 * s, y - 3 * s, 14 * s, 5 * s, "#7a5428"); // Holz
  R(ctx, x - 6 * s, y - 10 * s - fl, 12 * s, 8 * s, "#f07030");
  RN(ctx, x - 4 * s, y - 15 * s - fl, 8 * s, 7 * s, "#f8a030");
  RN(ctx, x - 2 * s, y - 18 * s - fl, 4 * s, 4 * s, "#f8e060");
  if (big) { R(ctx, x - 17 * s, y - 8 * s, 8 * s, 5 * s, "#f07030"); R(ctx, x + 11 * s, y - 7 * s, 7 * s, 5 * s, "#f8a030"); }
}

// ---------- SZENE 1: Atrium (Hotspots wie v2.1) ----------
SCENES.atrium = {
  name: "Atrium",
  draw(ctx, t) {
    RN(ctx, 0, 0, 640, 360, "#e8dcc0");
    tiles(ctx, 0, 0, 640, 360, 40, 20, "#e0d0b0", "#cbb995"); // Marmor
    brickWall(ctx, 40, 40, 560, 240);
    RN(ctx, 40, 40, 560, 6, "#f0e4c8");
    RN(ctx, 40, 40, 6, 240, "#d8bc90");
    RN(ctx, 594, 40, 6, 240, "#8a6444");
    RN(ctx, 40, 274, 560, 6, "#8a6a48");
    for (let i = 0; i < 4; i++) R(ctx, 60 + i * 150, 0, 18, 44, "#8a6848"); // Balken
    // Impluvium: Himmel + Becken
    skyGradient(ctx, "#7ec8e8", "#a8d8f0", "#c8e8f0");
    cloud(ctx, 80, 26, 1); cloud(ctx, 300, 16, 1);
    RN(ctx, 290, 120, 60, 30, "#88ccf0");
    water(ctx, 280, 170, 90, 60, t);
    // Tisch mit Brot/Krug (mit Outlines)
    R(ctx, 110, 150, 90, 9, "#9a6a38");
    R(ctx, 114, 159, 11, 27, "#7a4c22"); R(ctx, 185, 159, 11, 27, "#7a4c22");
    R(ctx, 130, 136, 27, 13, "#e0b060"); // Brot
    RN(ctx, 134, 134, 18, 4, "#f0cc8c");
    R(ctx, 158, 130, 17, 20, "#b06040"); // Krug
    RN(ctx, 162, 126, 9, 5, "#8a4828");
    // Figuren
    person(ctx, 150, 140, { skin: "#f0c090", hair: "#4a3018", tunic: "#c03838", trim: "#e05858", tunicDark: "#9c2828", skirt: false }, t);
    person(ctx, 440, 210, { skin: "#e0b080", hair: "#8a5a20", tunic: "#3860c0", trim: "#5880e0", tunicDark: "#28489c", skirt: false }, t);
    cat(ctx, 500, 300, t);
    torch(ctx, 90, 88, t);
  },
  hotspots: [
    { x: 80, y: 160, w: 160, h: 120, la: "ianua", target: "hortus", verbum: "ianua" },
    { x: 400, y: 120, w: 120, h: 160, la: "pater",
      onUse(s, G) {
        if (!G.has("pecunia") && !G.flag("pecuniaGiven")) {
          G.setFlag("pecuniaGiven");
          G.verbaAdd("pecunia");
          return { type: "dialog", lines: [
            ["Pater", "Ave, fili! Festum Ceres iam incipit."],
            ["Pater", "Pecuniam tibi do. Em frumentum in macello!"],
            ["Feles", "Miau! Pater pecuniam dat. Habe pecuniam in saccā!"]
          ], give: "pecunia" };
        }
        return { type: "dialog", lines: [["Pater", "Festum Ceres exspecta! Dis curre!"]] };
      } },
    { x: 110, y: 120, w: 100, h: 100, la: "cibus",
      onUse(s, G) {
        if (!G.has("panis")) { G.verbaAdd("panis"); return { type: "take", item: "panis" }; }
        return { type: "text", la: "Panis iam in saccā est." };
      } },
    { x: 500, y: 280, w: 70, h: 60, la: "feles",
      onUse(s, G) {
        G.verbaAdd("feles");
        return { type: "feles", text: "Miau! Ego sum Feles. Tecum semper ambulo. Verba nova collige!" };
      } },
    { x: 290, y: 120, w: 60, h: 60, la: "aqua",
      onUse(s, G) { G.verbaAdd("aqua"); return { type: "text", la: "Aqua in impluvio splendet." }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 640, h: 30, la: "via", target: "macellum" }
  ]
};

// ---------- SZENE 2: Hortus ----------
SCENES.hortus = {
  name: "Hortus",
  draw(ctx, t) {
    skyGradient(ctx, "#68b8e8", "#8ed8f0", "#c8f0d8");
    cloud(ctx, 60, 40, 1); cloud(ctx, 200, 20, 1); cloud(ctx, 440, 48, 1);
    RN(ctx, 0, 200, 640, 160, "#5aa048"); // Wiese
    for (let i = 0; i < 22; i++) {
      const gx = (i * 71) % 640, gy = 210 + (i * 37) % 130;
      RN(ctx, gx, gy, 3, 6, "#3e8038"); RN(ctx, gx + 4, gy + 1, 3, 5, "#3e8038"); RN(ctx, gx + 8, gy, 3, 6, "#74bc60");
    }
    brickWall(ctx, 0, 60, 640, 140);
    RN(ctx, 0, 60, 640, 6, "#d8c0a0");
    windowFrame(ctx, 80, 100, 40, 40, false);
    windowFrame(ctx, 500, 100, 40, 40, false);
    // Blumenbeet
    R(ctx, 220, 250, 200, 50, "#8a6044");
    RN(ctx, 224, 246, 192, 6, "#a07850");
    for (let i = 0; i < 5; i++) {
      const fx = 240 + i * 36;
      R(ctx, fx, 234, 4, 20, "#3a8a32"); // Stängel mit Outline
      R(ctx, fx - 4, 226, 12, 10, i % 2 ? "#e86070" : "#e8d040"); // Blüte
      RN(ctx, fx - 2, 228, 6, 5, i % 2 ? "#f8a0b0" : "#f8f0a0");
      RN(ctx, fx + 6, 240, 5, 4, "#46a03c");
    }
    tree(ctx, 70, 210, 2); tree(ctx, 560, 200, 2);
    bush(ctx, 160, 240, 1); bush(ctx, 460, 250, 1);
    door(ctx, 10, 140, 60, 90);
    person(ctx, 300, 240, { skin: "#f0c090", hair: "#6a3818", tunic: "#d04868", trim: "#e87090", tunicDark: "#a83450", skirt: true }, t);
    cat(ctx, 480, 150, t);
  },
  hotspots: [
    { x: 260, y: 240, w: 120, h: 80, la: "flos",
      onUse(s, G) {
        if (!G.has("flores")) {
          G.verbaAdd("flos");
          if (G.char === "aurelia") {
            return { type: "dialog", lines: [
              ["Feles", "Miau! Aurelia viam latentem videt: flores pulcherrimi crescunt!" ]
            ], give: "flores" };
          }
          return { type: "take", item: "flores" };
        }
        return { type: "text", la: "Flores iam in saccā sunt." };
      } },
    { x: 236, y: 190, w: 80, h: 110, la: "mulier",
      onUse(s, G) {
        G.verbaAdd("corona");
        return { type: "dialog", lines: [
          ["Mater", "Salve! Corona ex floribus ad festum necessaria est."],
          ["Mater", "Flores in horto carpito et coronam in theatro parate!"]
        ] };
      } },
    { x: 470, y: 130, w: 70, h: 60, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! In horto via aurea est – Aurelia vias latentes amat!" }; } },
    { x: 50, y: 180, w: 90, h: 90, la: "arbor",
      onUse(s, G) { return { type: "text", la: "Arbor magna in horto stat." }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 640, h: 30, la: "domus", target: "atrium" }
  ]
};

// ---------- SZENE 3: Macellum ----------
SCENES.macellum = {
  name: "Macellum",
  draw(ctx, t) {
    skyGradient(ctx, "#f0c860", "#f8dc90", "#f0b870");
    cloud(ctx, 100, 24, 1); cloud(ctx, 420, 14, 1);
    stoneFloor(ctx, 260);
    RN(ctx, 0, 260, 640, 4, "#d0b088");
    for (let i = 0; i < 4; i++) {
      const sx = 10 + i * 160;
      R(ctx, sx + 4, 140, 9, 92, "#7a5428"); R(ctx, sx + 117, 140, 9, 92, "#7a5428"); // Pfosten
      for (let m = 0; m < 6; m++) R(ctx, sx + m * 22, 120, 22, 16, m % 2 ? "#f0e8d8" : "#e05858"); // Markise
      RN(ctx, sx, 134, 132, 6, "#c04848");
      R(ctx, sx, 210, 132, 13, "#9a6a38"); // Theke
      RN(ctx, sx + 5, 223, 122, 8, "#7a4c22");
      RN(ctx, sx, 210, 132, 4, "#c89258");
      if (i === 0) { // Früchte
        for (let f = 0; f < 4; f++) {
          R(ctx, sx + 14 + f * 28, 194, 15, 15, f % 2 ? "#f08838" : "#e05828");
          RN(ctx, sx + 18 + f * 28, 190, 7, 5, "#f8b060");
        }
      } else if (i === 1) { // Käse
        R(ctx, sx + 20, 190, 32, 20, "#f0d060"); RN(ctx, sx + 25, 195, 22, 10, "#f8e490");
        R(ctx, sx + 70, 194, 28, 16, "#e0c040");
      } else if (i === 2) { // Töpfe
        R(ctx, sx + 18, 188, 22, 22, "#b06040"); R(ctx, sx + 21, 182, 16, 8, "#8a4828");
        R(ctx, sx + 70, 190, 24, 20, "#a060c0"); R(ctx, sx + 74, 184, 16, 8, "#78389c");
      } else { // Körbe mit Korn
        R(ctx, sx + 16, 190, 26, 20, "#c8a050"); RN(ctx, sx + 20, 184, 18, 8, "#f0dca0");
        R(ctx, sx + 72, 192, 24, 18, "#c8a050"); RN(ctx, sx + 76, 186, 16, 8, "#f0dca0");
      }
    }
    // Annona-Tafel
    R(ctx, 300, 180, 62, 36, "#f0e0a8");
    R(ctx, 296, 174, 70, 8, "#b09048");
    RN(ctx, 310, 192, 44, 4, "#6a5838"); RN(ctx, 310, 200, 36, 4, "#6a5838");
    person(ctx, 170, 210, { skin: "#e0b080", hair: "#2a1a10", tunic: "#4aa858", trim: "#70c878", tunicDark: "#388c40", skirt: false }, t);
    person(ctx, 420, 280, { skin: "#f0c090", hair: "#e0b860", tunic: "#b050d0", trim: "#d078e8", tunicDark: "#8c38a8", skirt: true }, t);
    cat(ctx, 590, 320, t);
  },
  hotspots: [
    { x: 172, y: 160, w: 90, h: 120, la: "mercator",
      onUse(s, G) {
        if (G.has("frumentum")) return { type: "text", la: "Mercator: Frumentum iam habes!" };
        if (G.has("pecunia")) {
          G.verbaAdd("frumentum"); G.verbaAdd("emo"); G.removeItem("pecunia");
          return { type: "dialog", lines: [
            ["Mercator", "Salve! Emis frumentum? Pecuniam accipio."],
            ["Mercator", "Frumentum bonum pro festo Ceres est!"]
          ], give: "frumentum" };
        }
        return { type: "dialog", lines: [
          ["Mercator", "Pecuniam non habes! Pater pecuniam dat."]
        ] };
      } },
    { x: 300, y: 176, w: 60, h: 60, la: "annona",
      onUse(s, G) { G.verbaAdd("annona"); return { type: "text", la: "Annona bona est: frumentum vile est!" }; } },
    { x: 580, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! Emo = ich kaufe. Pecunia dat, frumentum accipit!" }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 320, h: 30, la: "domus", target: "atrium" },
    { x: 320, y: 0, w: 320, h: 30, la: "taberna", target: "taberna" }
  ]
};

// ---------- SZENE 4: Taberna ----------
SCENES.taberna = {
  name: "Taberna",
  draw(ctx, t) {
    RN(ctx, 0, 0, 640, 360, "#3a2a1c");
    for (let i = 0; i < 5; i++) R(ctx, 20 + i * 130, 0, 20, 60, "#6a4c2c"); // Balken
    RN(ctx, 0, 60, 640, 300, "#8a6444");
    RN(ctx, 0, 60, 640, 8, "#9c7450");
    brickWall(ctx, 0, 250, 640, 110);
    tiles(ctx, 0, 320, 640, 40, 40, 20, "#7a5c3c", "#684c30");
    // Theke
    R(ctx, 40, 180, 260, 17, "#9a6a38");
    R(ctx, 48, 197, 244, 11, "#7a4c22");
    RN(ctx, 40, 180, 260, 5, "#c89258");
    R(ctx, 52, 208, 13, 42, "#6a4c2c"); R(ctx, 235, 208, 13, 42, "#6a4c2c");
    // Ware auf der Theke
    R(ctx, 70, 162, 32, 18, "#e0b060"); RN(ctx, 75, 158, 22, 7, "#f0cc8c");
    R(ctx, 130, 166, 24, 14, "#f0d060");
    R(ctx, 190, 156, 22, 24, "#b06040"); RN(ctx, 195, 151, 12, 6, "#8a4828");
    // Regal mit Amphoren
    R(ctx, 380, 120, 220, 9, "#9a6a38");
    R(ctx, 384, 129, 11, 42, "#6a4c2c"); R(ctx, 585, 129, 11, 42, "#6a4c2c");
    for (let i = 0; i < 4; i++) {
      R(ctx, 404 + i * 48, 90, 26, 30, "#c8a070");
      R(ctx, 410 + i * 48, 80, 14, 11, "#a07848");
      RN(ctx, 407 + i * 48, 96, 7, 7, "#e0c090");
    }
    RN(ctx, 30, 70, 20, 112, "#b84040"); RN(ctx, 590, 70, 20, 112, "#b84040"); // Vorhänge
    // Coquus mit Kochmütze
    person(ctx, 130, 180, { skin: "#f0c090", hair: "#2a1a10", tunic: "#c06028", trim: "#e08040", tunicDark: "#984818", skirt: false }, t);
    R(ctx, 112, 152, 36, 12, "#f8f8f0");
    RN(ctx, 116, 147, 28, 6, "#e0e0d0");
    // Murmillo-Tisch
    R(ctx, 390, 250, 120, 15, "#9a6a38"); R(ctx, 396, 265, 13, 38, "#6a4c2c"); R(ctx, 489, 265, 13, 38, "#6a4c2c");
    R(ctx, 420, 236, 22, 14, "#e0c050"); // Becher
    murmilloSprite(ctx, 460, 250, t);
    cat(ctx, 260, 320, t);
    torch(ctx, 340, 98, t); torch(ctx, 40, 88, t);
  },
  hotspots: [
    { x: 92, y: 164, w: 90, h: 120, la: "coquus",
      onUse(s, G) {
        if (G.has("vinum")) return { type: "text", la: "Coquus: Vinum iam habes!" };
        if (G.has("panis")) {
          G.verbaAdd("vinum"); G.verbaAdd("do"); G.removeItem("panis");
          return { type: "dialog", lines: [
            ["Coquus", "Panem mihi da – vinum tibi do!"]
          ], give: "vinum" };
        }
        return { type: "dialog", lines: [["Coquus", "Da mihi panem, et vinum accipis!"]] };
      } },
    { x: 390, y: 110, w: 100, h: 130, la: "murmillo",
      onUse(s, G) {
        if (G.has("sagitta")) return { type: "text", la: "Murmillo: Sagittam iam habes!" };
        if (G.has("vinum")) {
          G.verbaAdd("murmillo"); G.verbaAdd("sagitta"); G.removeItem("vinum");
          return { type: "dialog", lines: [
            ["Murmillo", "Vinum bonum! Sagittam tibi do."],
            ["Murmillo", "In thermis sagitta aquam clavam pulsat – clavis exit!"],
            ["Feles", "Miau! Murmillo in arena pugnat, sed hodie bibit!"]
          ], give: "sagitta" };
        }
        return { type: "dialog", lines: [["Murmillo", "Vinum mihi da, et sagittam accipis!"]] };
      } },
    { x: 260, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! Do = ich gebe. Vinum dat, sagittam accipit!" }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 320, h: 30, la: "macellum", target: "macellum" },
    { x: 320, y: 0, w: 320, h: 30, la: "thermae", target: "thermae" }
  ]
};

// ---------- SZENE 5: Thermae ----------
SCENES.thermae = {
  name: "Thermae",
  draw(ctx, t) {
    RN(ctx, 0, 0, 640, 360, "#8a90a8");
    RN(ctx, 0, 0, 640, 240, "#c0c0ca");
    for (let i = 0; i < 4; i++) {
      R(ctx, 40 + i * 160, 22, 122, 9, "#a0a0b0");
      R(ctx, 60 + i * 160, 0, 82, 22, "#b0b0be");
    }
    RN(ctx, 0, 236, 640, 10, "#a09078");
    // Großes Becken
    R(ctx, 60, 100, 520, 160, "#7090c0");
    water(ctx, 68, 108, 504, 144, t);
    for (let i = 0; i < 5; i++) {
      const sx2 = 120 + i * 100, sy = 90 + Math.sin((t || 0) / 700 + i) * 6;
      RN(ctx, sx2, sy, 42, 11, "rgba(235,240,245,0.6)");
      RN(ctx, sx2 + 11, sy - 9, 20, 9, "rgba(235,240,245,0.45)");
    }
    tiles(ctx, 40, 260, 560, 30, 44, 16, "#d0b890", "#bca878");
    RN(ctx, 40, 260, 560, 5, "#e8d8b8");
    R(ctx, 120, 244, 62, 15, "#b09870"); // Leiter
    for (let i = 0; i < 8; i++) {
      R(ctx, 80 + i * 60, 68, 42, 5, "#8aa8d0");
      RN(ctx, 102 + i * 60, 76, 32, 5, "#6080b0");
    }
    person(ctx, 140, 250, { skin: "#e0b080", hair: "#2a1a10", tunic: "#50b0b8", trim: "#78d0d8", tunicDark: "#388c94", skirt: false }, t);
    R(ctx, 106, 218, 14, 24, "#f0ece0"); // Tuch
    // Pfeil + glitzernder Schlüssel im Wasser
    R(ctx, 310, 178, 42, 6, "#d0b050");
    R(ctx, 344, 172, 10, 14, "#b89440");
    R(ctx, 304, 172, 10, 12, "#e8e8f4");
    R(ctx, 352, 186, 10, 10, "#f0e8c8");
    RN(ctx, 356, 182, 5, 5, "#fdf8e0");
    cat(ctx, 560, 320, t);
    torch(ctx, 40, 58, t); torch(ctx, 600, 58, t);
  },
  hotspots: [
    { x: 280, y: 200, w: 100, h: 80, la: "aqua",
      onUse(s, G) {
        if (G.has("clavis")) return { type: "text", la: "Clavis iam in saccā est." };
        if (G.has("sagitta")) {
          G.verbaAdd("clavis"); G.verbaAdd("thermae"); G.removeItem("sagitta");
          if (G.char === "lucius") {
            return { type: "dialog", lines: [
              ["Feles", "Miau! Lucius audax est: sagitta aquam pulsat!"],
              ["Lucius", "Sagittam in aquam mitto – clavis exit!"]
            ], give: "clavis" };
          }
          return { type: "dialog", lines: [
            ["Feles", "Miau! Aquam tangere noli – sed murmurium audi: clavis sub aqua est!"],
            ["Aurelia", "Sagittam in aquam mitto – clavis exit!"]
          ], give: "clavis" };
        }
        return { type: "text", la: "Aqua calida est. Quidnam sub aqua lucet?" };
      } },
    { x: 112, y: 184, w: 90, h: 120, la: "balneator",
      onUse(s, G) {
        return { type: "dialog", lines: [
          ["Balneator", "In thermis aqua calida est."],
          ["Balneator", "Clavis in aqua iacet – murmurillo sagitta petenda est!"]
        ] };
      } },
    { x: 560, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! Thermae = das Bad. Aqua calida Felem non placet!" }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 320, h: 30, la: "taberna", target: "taberna" },
    { x: 320, y: 0, w: 320, h: 30, la: "domus vicini", target: "domus_vicini" }
  ]
};

// ---------- SZENE 6: Domus Vicini ----------
SCENES.domus_vicini = {
  name: "Domus Vicini",
  draw(ctx, t) {
    RN(ctx, 0, 0, 640, 360, "#2a2018");
    RN(ctx, 0, 290, 640, 70, "#553e28");
    for (let i = 0; i < 12; i++) R(ctx, i * 55, 290, 4, 70, "#3e2c1c"); // Dielenfugen
    RN(ctx, 0, 40, 640, 250, "#755736");
    RN(ctx, 0, 40, 640, 8, "#876540");
    for (let i = 0; i < 5; i++) R(ctx, 30 + i * 130, 20, 22, 24, "#6a4c2c");
    door(ctx, 280, 140, 80, 110);
    torch(ctx, 250, 118, t); torch(ctx, 390, 118, t);
    // Prunktruhe (Cista)
    R(ctx, 90, 190, 150, 70, "#9a6a38");
    R(ctx, 94, 182, 142, 14, "#b4814c");
    R(ctx, 90, 206, 150, 7, "#e8c040");
    R(ctx, 90, 240, 150, 7, "#e8c040");
    R(ctx, 148, 194, 16, 22, "#f0cc50");
    RN(ctx, 153, 201, 7, 9, "#3e2c1c");
    RN(ctx, 96, 212, 12, 46, "rgba(0,0,0,0.18)");
    // Regal mit Krügen
    R(ctx, 440, 150, 130, 9, "#9a6a38");
    R(ctx, 446, 159, 11, 42, "#6a4c2c"); R(ctx, 553, 159, 11, 42, "#6a4c2c");
    for (let i = 0; i < 3; i++) {
      R(ctx, 460 + i * 40, 118, 24, 32, "#b86040");
      R(ctx, 466 + i * 40, 108, 12, 10, "#8a4828");
      RN(ctx, 463 + i * 40, 126, 7, 7, "#d88050");
    }
    // Teppich
    R(ctx, 240, 300, 160, 50, "#b04040");
    R(ctx, 250, 308, 140, 34, "#c85850");
    RN(ctx, 260, 316, 120, 18, "#a03838");
    person(ctx, 470, 260, { skin: "#f0c090", hair: "#4a3018", tunic: "#c0a040", trim: "#e0c060", tunicDark: "#988028", skirt: false }, t);
    cat(ctx, 40, 320, t);
  },
  hotspots: [
    { x: 110, y: 150, w: 140, h: 110, la: "cista",
      onUse(s, G) {
        if (G.has("corona_rohling") && G.has("stella")) {
          return { type: "text", la: "Cista vacua est." };
        }
        if (G.has("clavis")) {
          G.verbaAdd("cista"); G.verbaAdd("stella");
          return { type: "dialog", lines: [
            ["Feles", "Miau! Clavis ianuam aperit – cistam aperit!"],
            ["Lucius", "Cistam aperio: corona rudis et stella!"]
          ], give: "corona_rohling", give2: "stella" };
        }
        return { type: "text", la: "Cista clausa est. Clavem quaere!" };
      } },
    { x: 432, y: 184, w: 90, h: 120, la: "vicinus",
      onUse(s, G) {
        return { type: "dialog", lines: [
          ["Vicinus", "Salve, vicine! Cista mea clausa est."],
          ["Vicinus", "Clavem in thermis amisi – eheu!"]
        ] };
      } },
    { x: 40, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! Cistam clausam – clavem quaere! Clavis ianuam aperit." }; } },
    { x: 280, y: 140, w: 80, h: 110, la: "ianua",
      onUse(s, G) { return { type: "text", la: "Ianua ad vicum nocturnum ducit." }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 320, h: 30, la: "thermae", target: "thermae" },
    { x: 320, y: 0, w: 320, h: 30, la: "theatrum", target: "theatrum" }
  ]
};

// ---------- SZENE 7: Theatrum ----------
SCENES.theatrum = {
  name: "Theatrum",
  draw(ctx, t) {
    skyGradient(ctx, "#f0a848", "#f8cc88", "#fce0a8");
    cloud(ctx, 80, 18, 1); cloud(ctx, 400, 32, 1);
    R(ctx, 60, 80, 520, 200, "#f0e0bc");
    RN(ctx, 60, 80, 520, 10, "#c8a878");
    for (let i = 0; i < 6; i++) {
      const cx2 = 90 + i * 90;
      R(ctx, cx2, 100, 20, 170, "#e0d0a8");
      RN(ctx, cx2 + 2, 100, 5, 170, "#f4ead0");
      RN(ctx, cx2 + 13, 100, 5, 170, "#c0b088");
      R(ctx, cx2 - 5, 90, 30, 11, "#d0c098");
      R(ctx, cx2 - 5, 262, 30, 9, "#d0c098");
    }
    for (let r = 0; r < 6; r++) R(ctx, 84 + r * 40, 80 - r * 13, 472 - r * 80, 13, "#e8dcc0"); // Giebel
    R(ctx, 100, 270, 440, 27, "#c8a070");
    for (let i = 0; i < 11; i++) RN(ctx, 102 + i * 40, 270, 3, 27, "#a88050");
    RN(ctx, 100, 270, 440, 4, "#e0c090");
    // Vorhang
    R(ctx, 130, 120, 380, 150, "#c04040");
    for (let i = 0; i < 9; i++) R(ctx, 140 + i * 42, 120, 11, 150, "#e05858");
    RN(ctx, 130, 120, 380, 9, "#8a2828");
    // Publikum
    for (let r = 0; r < 2; r++) {
      for (let i = 0; i < 10; i++) {
        const px2 = 50 + i * 60 + (r % 2) * 30, py = 316 + r * 20;
        R(ctx, px2, py, 18, 15, r ? "#f0c090" : "#e0b080");
        RN(ctx, px2 + 4, py + 5, 3, 3, "#141210"); RN(ctx, px2 + 11, py + 5, 3, 3, "#141210");
        R(ctx, px2 - 2, py + 13, 22, 15, r ? "#5880e0" : "#e07090");
      }
    }
    person(ctx, 200, 266, { skin: "#f0c090", hair: "#2a1a10", tunic: "#e05848", trim: "#f88070", tunicDark: "#b83c30", skirt: false }, t);
    R(ctx, 186, 236, 30, 8, "#f0ece0"); // Maske
    person(ctx, 430, 266, { skin: "#f0c090", hair: "#e0b860", tunic: "#5870e0", trim: "#8098f0", tunicDark: "#4058b8", skirt: true }, t);
    cat(ctx, 570, 330, t);
  },
  hotspots: [
    { x: 160, y: 160, w: 100, h: 120, la: "histrio",
      onUse(s, G) {
        G.verbaAdd("theatrum"); G.verbaAdd("fabula");
        if (G.has("flores") && G.has("corona_rohling") && !G.has("corona")) {
          return { type: "dialog", lines: [
            ["Histrio", "Salve! Fabula nostra de Cere agitur."],
            ["Histrio", "Coronam ex floribus factam video! Flores datis?"],
            ["Histrio", "Coronam pulchram facio: ecco corona perfecta!"]
          ], give: "corona", take: "corona_rohling" };
        }
        if (G.has("corona")) return { type: "text", la: "Histrio: Corona perfecta est!" };
        return { type: "dialog", lines: [
          ["Histrio", "Fabula de Cere in theatro agitur."],
          ["Histrio", "Flores et rudem coronam ad coronam faciendam necessaria sunt!"]
        ] };
      } },
    { x: 392, y: 160, w: 100, h: 120, la: "actrix",
      onUse(s, G) {
        G.verbaAdd("fabula");
        return { type: "dialog", lines: [
          ["Actrix", "Fabula narranda est! Verba collige!"]
        ] };
      } },
    { x: 560, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! In theatro fabula agitur – verba nova hic sunt!" }; } },
    { x: 100, y: 270, w: 440, h: 26, la: "scaena",
      onUse(s, G) { return { type: "text", la: "Scaena magna theatri est." }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 320, h: 30, la: "domus vicini", target: "domus_vicini" },
    { x: 320, y: 0, w: 320, h: 30, la: "templum", target: "templum" }
  ]
};

// ---------- SZENE 8: Templum Ceres ----------
SCENES.templum = {
  name: "Templum Ceres",
  draw(ctx, t) {
    skyGradient(ctx, "#b08868", "#d0a888", "#f0dcb8");
    cloud(ctx, 150, 26, 1); cloud(ctx, 450, 16, 1);
    RN(ctx, 0, 300, 640, 60, "#d0c098");
    RN(ctx, 0, 290, 640, 12, "#e0d0a8");
    RN(ctx, 0, 310, 640, 4, "#b8a880");
    R(ctx, 140, 90, 360, 210, "#f0ead4");
    RN(ctx, 140, 90, 360, 10, "#d0c098");
    brickWall(ctx, 140, 150, 360, 150);
    RN(ctx, 140, 90, 8, 210, "#f8f4e4");
    RN(ctx, 492, 90, 8, 210, "#c8c0a0");
    for (let r = 0; r < 8; r++) R(ctx, 164 + r * 28, 90 - r * 11, 312 - r * 56, 12, r % 2 ? "#e0d8c0" : "#eae2cc");
    for (let i = 0; i < 5; i++) {
      const cx2 = 170 + i * 75;
      R(ctx, cx2, 110, 24, 190, "#f0ead0");
      RN(ctx, cx2 + 2, 110, 6, 190, "#faf6e8");
      RN(ctx, cx2 + 16, 110, 6, 190, "#d8d0b0");
      R(ctx, cx2 - 6, 100, 36, 13, "#d0c098");
    }
    // Ceres-Statue (mit Outline)
    R(ctx, 300, 130, 40, 130, "#e0d4b0");
    R(ctx, 304, 98, 32, 34, "#ece0c0");
    RN(ctx, 310, 112, 6, 6, "#a89068"); RN(ctx, 324, 112, 6, 6, "#a89068");
    RN(ctx, 312, 126, 16, 4, "#b89878");
    R(ctx, 292, 100, 9, 42, "#d0c0a0");
    R(ctx, 339, 100, 9, 42, "#d0c0a0");
    R(ctx, 274, 94, 22, 48, "#e8c858"); // Getreidebündel
    RN(ctx, 280, 88, 10, 7, "#f8e0a0");
    R(ctx, 344, 94, 22, 48, "#e8c858");
    altarFire(ctx, 240, 290, t, true);
    altarFire(ctx, 400, 290, t, true);
    R(ctx, 214, 274, 30, 17, "#c8a050"); // Gabenkorb
    RN(ctx, 218, 268, 22, 8, "#f08838");
    R(ctx, 424, 270, 18, 22, "#b06040"); RN(ctx, 428, 264, 10, 7, "#8a4828");
    person(ctx, 520, 300, { skin: "#f0c090", hair: "#4a3018", tunic: "#faf4e4", trim: "#e8c040", tunicDark: "#d8d0b0", skirt: true }, t);
    cat(ctx, 80, 330, t);
    for (let i = 0; i < 4; i++) {
      const gx = 180 + i * 90;
      for (let g = 0; g < 5; g++) R(ctx, gx + g * 7, 128 + Math.sin(g) * 6, 7, 7, g % 2 ? "#e86070" : "#e8d040");
    }
  },
  hotspots: [
    { x: 200, y: 150, w: 240, h: 140, la: "ara",
      onUse(s, G) {
        G.verbaAdd("templum"); G.verbaAdd("ara"); G.verbaAdd("dona");
        return { type: "dialog", lines: [
          ["Sacerdos", "Ave! Ara Ceres dona exspectat."],
          ["Sacerdos", "Dona deis data – dei laeti! Frumentum, corona et stella necessaria sunt."],
          ["Feles", "Miau! Dona Ceres danda sunt: frumentum, corona, stella!"]
        ] };
      } },
    { x: 80, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! Templum est casa deorum. In ara ignis et dona sunt." }; } },
    { x: 170, y: 110, w: 25, h: 190, la: "columna",
      onUse(s, G) { return { type: "text", la: "Columnae templi altae sunt." }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 320, h: 30, la: "theatrum", target: "theatrum" },
    { x: 320, y: 0, w: 320, h: 30, la: "vicus nocturnus", target: "vicus_nocturnus" }
  ]
};

// ---------- SZENE 9: Vicus Nocturnus ----------
SCENES.vicus_nocturnus = {
  name: "Vicus Nocturnus",
  draw(ctx, t) {
    skyGradient(ctx, "#100c20", "#181428", "#282048");
    stars(ctx, t);
    // Mond mit Outline
    R(ctx, 500, 28, 38, 38, "#f8f0d0");
    RN(ctx, 512, 22, 22, 11, "#181428");
    RN(ctx, 506, 42, 28, 15, "#181428");
    RN(ctx, 517, 40, 9, 9, "#e8e0c0");
    // Gasse
    RN(ctx, 0, 260, 640, 100, "#282030");
    tiles(ctx, 0, 260, 640, 100, 34, 16, "#403850", "#38304a");
    RN(ctx, 0, 260, 640, 4, "#484058");
    // Häuser links
    R(ctx, 20, 90, 180, 180, "#383050");
    roofTiles(ctx, 12, 74, 196, 18);
    RN(ctx, 20, 90, 6, 180, "#443c5c");
    windowFrame(ctx, 40, 130, 36, 44, false);
    windowFrame(ctx, 90, 180, 28, 36, true);
    door(ctx, 60, 190, 44, 76);
    RN(ctx, 54, 184, 54, 5, "#f8f0b0");
    // Häuser rechts
    R(ctx, 400, 80, 200, 190, "#383050");
    roofTiles(ctx, 392, 62, 216, 20);
    RN(ctx, 594, 80, 6, 190, "#2c2438");
    windowFrame(ctx, 430, 130, 36, 44, false);
    windowFrame(ctx, 500, 130, 36, 44, true);
    torch(ctx, 380, 158, t);
    // Laterne mit Lichtkegel
    R(ctx, 610, 150, 8, 62, "#443c50");
    R(ctx, 600, 138, 26, 20, "#443c50");
    R(ctx, 604, 142, 18, 15, "#f8e060");
    RN(ctx, 594, 158, 38, 42, "rgba(248,224,96,0.14)");
    // Senex mit Stab
    person(ctx, 260, 300, { skin: "#e0b088", hair: "#d8d0c0", tunic: "#2c3850", trim: "#3c4860", tunicDark: "#1e2840", skirt: false }, t);
    R(ctx, 300, 238, 7, 62, "#6a5438");
    R(ctx, 294, 230, 15, 10, "#7a6448");
    R(ctx, 320, 288, 16, 14, "#443c50"); // Bodenlaterne
    RN(ctx, 323, 291, 9, 9, "#f8e060");
    cat(ctx, 180, 330, t);
  },
  hotspots: [
    { x: 248, y: 170, w: 100, h: 120, la: "senex",
      onUse(s, G) {
        G.verbaAdd("nox");
        if (G.has("corona") && G.has("stella")) {
          return { type: "dialog", lines: [
            ["Senex", "In nocte ianua latet..."],
            ["Senex", "Corona stellaque lucent – viam monstrant!"],
            ["Feles", "Miau! Corona et stella in nocte lucent: ianua festi aperitur!"]
          ], choice: {
            prompt: "Senex dicit: \"Quid Ceres donat?\"",
            options: [
              { la: "Terra fructum dat.", ok: true,
                next: [["Senex", "Recte! Ceres est dea frugum. Ianua aperitur!"]], flag: "via_fest" },
              { la: "Pecunia vilis est.", ok: false,
                next: [["Senex", "Non recte! De Cere cogita!"]] },
              { la: "Feles sagittam amat.", ok: false,
                next: [["Senex", "Absurdum! De Cere cogita!"]] }
            ]
          } };
        }
        return { type: "dialog", lines: [
          ["Senex", "Ianua festi nocte latet."],
          ["Senex", "Corona et stella viam monstrant – quaere!"]
        ] };
      } },
    { x: 96, y: 180, w: 60, h: 86, la: "ianua",
      onUse(s, G) {
        if (G.flag("via_fest")) {
          return { type: "goto", target: "festum" };
        }
        return { type: "text", la: "Ianua clausa est. Senex nocte prope ianuam stat." };
      } },
    { x: 500, y: 130, w: 40, h: 44, la: "lumen",
      onUse(s, G) { return { type: "text", la: "Lumen in fenestra lucet." }; } },
    { x: 180, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! Nox = die Nacht. In nocte oculi Feles lucent!" }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 320, h: 30, la: "templum", target: "templum" },
    { x: 320, y: 0, w: 320, h: 30, la: "macellum", target: "macellum" }
  ]
};

// ---------- SZENE 10: Festum (Finale) ----------
SCENES.festum = {
  name: "Festum Ceres",
  draw(ctx, t) {
    skyGradient(ctx, "#282048", "#483868", "#684878");
    stars(ctx, t);
    RN(ctx, 0, 240, 640, 120, "#9a7a50");
    tiles(ctx, 0, 240, 640, 120, 40, 20, "#ac8a58", "#9a7a50");
    // Festzelte
    for (let i = 0; i < 3; i++) {
      const zx = 30 + i * 200;
      for (let m = 0; m < 6; m++) R(ctx, zx + m * 20, 118, 22, 18, m % 2 ? "#f0e8d8" : "#e05858");
      RN(ctx, zx, 134, 122, 6, "#c04848");
      R(ctx, zx + 6, 140, 9, 102, "#7a5428"); R(ctx, zx + 107, 140, 9, 102, "#7a5428");
    }
    for (let i = 0; i < 5; i++) altarFire(ctx, 80 + i * 120, 210, t, false);
    // Ceres-Schrein
    R(ctx, 260, 160, 120, 80, "#f0ead4");
    RN(ctx, 260, 160, 120, 10, "#d0c098");
    R(ctx, 264, 174, 112, 58, "#e4d8b8");
    altarFire(ctx, 320, 156, t, true);
    // Ähre
    R(ctx, 314, 188, 14, 36, "#e8c858");
    R(ctx, 309, 182, 24, 11, "#f8e0a0");
    for (let g = 0; g < 4; g++) { RN(ctx, 311 - g, 196 + g * 8, 7, 5, "#f8e0a0"); RN(ctx, 323 + g, 196 + g * 8, 7, 5, "#f8e0a0"); }
    // Girlanden
    for (let i = 0; i < 6; i++) {
      const gx = 40 + i * 110;
      for (let g = 0; g < 6; g++) R(ctx, gx + g * 9, 138 + Math.sin(g * 1.2) * 8, 7, 7, g % 2 ? "#e86070" : "#f0e060");
    }
    person(ctx, 120, 320, { skin: "#f0c090", hair: "#2a1a10", tunic: "#e05848", trim: "#f88070", tunicDark: "#b83c30", skirt: false }, t);
    person(ctx, 190, 330, { skin: "#f0c090", hair: "#e0b860", tunic: "#5870e0", trim: "#8098f0", tunicDark: "#4058b8", skirt: true }, t);
    person(ctx, 500, 320, { skin: "#e0b080", hair: "#4a3018", tunic: "#4aa858", trim: "#70c878", tunicDark: "#388c40", skirt: false }, t);
    person(ctx, 440, 260, { skin: "#f0c090", hair: "#4a3018", tunic: "#faf4e4", trim: "#e8c040", tunicDark: "#d8d0b0", skirt: true }, t);
    cat(ctx, 250, 340, t);
    // Konfetti
    for (let i = 0; i < 12; i++) {
      const fx = (i * 73 + (t || 0) / 50) % 640;
      const fy = 100 + ((i * 47 + (t || 0) / 30) % 160);
      R(ctx, fx, fy, 5, 5, i % 3 === 0 ? "#f8e060" : (i % 3 === 1 ? "#e86070" : "#78c878"));
    }
  },
  hotspots: [
    { x: 260, y: 100, w: 120, h: 140, la: "ara",
      onUse(s, G) {
        if (G.flag("fest_done")) return { type: "text", la: "Ceres laeta est. Festum agitur!" };
        if (G.has("frumentum") && G.has("corona") && G.has("stella")) {
          return { type: "dialog", lines: [
            ["Sacerdos", "Omnia dona habes! Dona Ceres da!"],
            ["Feles", "Miau! Frumentum, corona, stella – omnia dona sunt!"]
          ], choice: {
            prompt: "Copia respondet: \"Ceres dea est...\"",
            options: [
              { la: "Terra fructum dat.", ok: true,
                next: [["Sacerdos", "Recte! Ceres dona accipit – festum incipit!"]],
                win: true },
              { la: "Annona mala est.", ok: false,
                next: [["Sacerdos", "Non recte! Iterum cogita!"]] }
            ]
          } };
        }
        return { type: "text", la: "Ara dona exspectat: frumentum, corona, stella." };
      } },
    { x: 250, y: 290, w: 70, h: 70, la: "feles",
      onUse(s, G) { return { type: "feles", text: "Miau! Festum = das Fest. Omnes laeti sunt! Ceres te amat!" }; } },
    { x: 100, y: 260, w: 100, h: 120, la: "populus",
      onUse(s, G) { return { type: "text", la: "Populus laetus festum celebrat." }; } }
  ],
  exits: [
    { x: 0, y: 0, w: 640, h: 30, la: "vicus nocturnus", target: "vicus_nocturnus" }
  ]
};

</script>
<script>
// game.js – Engine: Ein-Klick-Steuerung, Inventar + Kombinieren,
// Dialogsystem, Verba-Register, Feles-Hinweise, Web-Audio-Musik/Sounds.

const ITEMS = {
  pecunia: { la: "pecunia", de: "Geld" },
  panis: { la: "panis", de: "Brot" },
  flores: { la: "flores", de: "Blumen" },
  frumentum: { la: "frumentum", de: "Getreide" },
  vinum: { la: "vinum", de: "Wein" },
  sagitta: { la: "sagitta", de: "Pfeil" },
  clavis: { la: "clavis", de: "Schlüssel" },
  corona_rohling: { la: "corona rudis", de: "Kranz-Rohling" },
  stella: { la: "stella", de: "Stern" },
  corona: { la: "corona", de: "Kranz" }
};

// Kombinationen (Inventar-Mechanik)
const COMBINES = [
  { a: "flores", b: "corona_rohling", la: "Flores et corona rudis!",
    hint: "Miau! In theatro histrio coronam perficit – non hic!" },
  { a: "frumentum", b: "corona", la: "Dona duo – sed stella deest!",
    hint: "Miau! Dona tria necessaria sunt: frumentum, corona, stella!" }
];

const G = {
  char: null,
  scene: "atrium",
  inventory: [],
  selected: null,
  flags: {},
  verba: new Set(),

  has(item) { return this.inventory.includes(item); },
  addItem(item) { if (!this.has(item)) this.inventory.push(item); },
  removeItem(item) {
    const i = this.inventory.indexOf(item);
    if (i >= 0) this.inventory.splice(i, 1);
    if (this.selected === item) this.selected = null;
  },
  flag(f) { return !!this.flags[f]; },
  setFlag(f) { this.flags[f] = true; },
  verbaAdd(la) {
    if (VERBA_MAP[la] && !this.verba.has(la)) {
      this.verba.add(la);
      updateVerbaCount();
      sound("collect");
    }
  }
};

// ---------- Audio (Web Audio API) ----------
let audioCtx = null, musicOn = true;
function ensureAudio() {
  if (!audioCtx) {
    try { audioCtx = new (window.AudioContext || window.webkitAudioContext)(); }
    catch (e) { audioCtx = null; }
  }
  if (audioCtx && audioCtx.state === "suspended") audioCtx.resume();
  return audioCtx;
}
function tone(freq, dur, type, vol, when) {
  const ctx = ensureAudio();
  if (!ctx) return;
  const t0 = ctx.currentTime + (when || 0);
  const o = ctx.createOscillator(), g = ctx.createGain();
  o.type = type || "square"; o.frequency.value = freq;
  g.gain.setValueAtTime(vol || 0.08, t0);
  g.gain.exponentialRampToValueAtTime(0.001, t0 + dur);
  o.connect(g); g.connect(ctx.destination);
  o.start(t0); o.stop(t0 + dur);
}
function sound(kind) {
  if (kind === "click") tone(440, 0.06, "square", 0.05);
  if (kind === "collect") { tone(660, 0.08, "square", 0.06); tone(880, 0.1, "square", 0.06, 0.08); }
  if (kind === "take") { tone(520, 0.1, "triangle", 0.08); tone(780, 0.12, "triangle", 0.08, 0.1); }
  if (kind === "error") tone(180, 0.2, "sawtooth", 0.06);
  if (kind === "meow") { tone(700, 0.15, "sine", 0.07); tone(550, 0.2, "sine", 0.06, 0.12); }
  if (kind === "win") [523, 659, 784, 1046].forEach((f, i) => tone(f, 0.3, "triangle", 0.08, i * 0.15));
}
let musicTimer = null;
function startMusic() {
  if (musicTimer || !ensureAudio()) return;
  const melody = [392, 440, 494, 440, 392, 349, 392, 0, 330, 392, 440, 392, 349, 330, 294, 0];
  let step = 0;
  musicTimer = setInterval(() => {
    if (!musicOn) return;
    const f = melody[step % melody.length];
    if (f) tone(f, 0.35, "triangle", 0.03);
    if (step % 4 === 0) tone(98, 0.5, "sine", 0.05);
    step++;
  }, 420);
}

// ---------- Rendering ----------
const canvas = document.getElementById("stage");
const ctx2d = canvas.getContext("2d");
let hoverSpot = null;

function loop(t) {
  const sc = SCENES[G.scene];
  ctx2d.clearRect(0, 0, 640, 360);
  sc.draw(ctx2d, t || 0);
  // Dauerhaft sichtbare Ausgangs-Buttons (Schilder mit Richtungspfeil + Ziel)
  sc.exits.forEach(ex => {
    const hovered = hoverSpot === ex;
    const bw = Math.min(ex.w, 150), bx = ex.x + (ex.w - bw) / 2;
    // Schild-Hintergrund
    ctx2d.fillStyle = hovered ? "rgba(60,44,20,0.95)" : "rgba(30,22,12,0.85)";
    ctx2d.fillRect(bx, ex.y + 2, bw, 28);
    // Rahmen
    ctx2d.strokeStyle = hovered ? "#f8e8b0" : "#d4a545";
    ctx2d.lineWidth = 2;
    ctx2d.strokeRect(bx + 1, ex.y + 3, bw - 2, 26);
    // Richtungspfeil
    ctx2d.fillStyle = "#d4a545";
    const cy = ex.y + 16;
    const left = /macellum|atrium|domus|hortus/.test(ex.target) && ex.target !== "hortus" ? false : (ex.x < 320);
    if (left) {
      ctx2d.beginPath();
      ctx2d.moveTo(bx + 26, cy - 7); ctx2d.lineTo(bx + 12, cy); ctx2d.lineTo(bx + 26, cy + 7);
      ctx2d.closePath(); ctx2d.fill();
    } else {
      ctx2d.beginPath();
      ctx2d.moveTo(bx + bw - 26, cy - 7); ctx2d.lineTo(bx + bw - 12, cy); ctx2d.lineTo(bx + bw - 26, cy + 7);
      ctx2d.closePath(); ctx2d.fill();
    }
    // Ziel-Beschriftung
    ctx2d.fillStyle = "#f8e8b0";
    ctx2d.font = "bold 13px Georgia";
    ctx2d.textAlign = "center";
    ctx2d.textBaseline = "middle";
    const label = "» " + (SCENES[ex.target] ? SCENES[ex.target].name : ex.la);
    ctx2d.fillText(label, bx + bw / 2, cy);
  });
  if (hoverSpot) {
    ctx2d.strokeStyle = "#f8e8b0";
    ctx2d.lineWidth = 2;
    ctx2d.strokeRect(hoverSpot.x + 1, hoverSpot.y + 1, hoverSpot.w - 2, hoverSpot.h - 2);
  }
  requestAnimationFrame(loop);
}

// ---------- Dialogsystem ----------
const dialogBox = document.getElementById("dialog-box");
const dSpeaker = document.getElementById("speaker");
const dText = document.getElementById("text");
const dChoices = document.getElementById("choices");
const dNext = document.getElementById("dialog-next");
let dialogQueue = [], dialogAfter = null;

function showText(speaker, text) {
  dialogBox.hidden = false;
  dSpeaker.textContent = speaker;
  dText.textContent = text;
  dChoices.innerHTML = "";
  dNext.style.display = "block";
}
function showDialog(lines, after) {
  dialogQueue = lines.slice();
  dialogAfter = after || null;
  const [sp, tx] = dialogQueue.shift();
  showText(sp, tx);
}
function showChoice(ch) {
  dialogBox.hidden = false;
  dSpeaker.textContent = "??";
  dText.textContent = ch.prompt;
  dNext.style.display = "none";
  dChoices.innerHTML = "";
  ch.options.forEach(opt => {
    const b = document.createElement("button");
    b.textContent = opt.la;
    b.onclick = () => {
      dChoices.innerHTML = "";
      sound(opt.ok ? "collect" : "error");
      if (opt.ok) {
        if (opt.flag) G.setFlag(opt.flag);
        showDialog(opt.next, () => {
          if (opt.win) {
            G.removeItem("frumentum"); G.removeItem("corona"); G.removeItem("stella");
            G.setFlag("fest_done");
            sound("win");
            showDialog([
              ["Ceres", "Donaria accipio – terra fructum dabit!"],
              ["Feles", "Miau! Festum incipit! Verba " + G.verba.size + " collegisti!"],
              ["Omnes", "FELIX FESTUM CERES! 🌾👑⭐"]
            ]);
          }
        });
      } else {
        showDialog(opt.next, () => {});
      }
    };
    dChoices.appendChild(b);
  });
}
function advanceDialog() {
  if (dChoices.children.length > 0) return;
  if (dialogQueue.length > 0) {
    const [sp, tx] = dialogQueue.shift();
    showText(sp, tx);
  } else {
    dialogBox.hidden = true;
    const fn = dialogAfter; dialogAfter = null;
    if (fn) fn();
  }
}
dialogBox.addEventListener("click", e => {
  if (e.target.tagName !== "BUTTON") advanceDialog();
});
dNext.addEventListener("click", advanceDialog);

// ---------- Feles ----------
const felesBox = document.getElementById("feles-box");
const felesText = document.getElementById("feles-text");
document.getElementById("feles-close").addEventListener("click", () => {
  felesBox.hidden = true;
});
function showFeles(text) {
  sound("meow");
  felesBox.hidden = false;
  felesText.textContent = text;
  clearTimeout(showFeles._t);
  showFeles._t = setTimeout(() => { felesBox.hidden = true; }, 9000);
}

// ---------- Verba-Register ----------
function updateVerbaCount() {
  document.getElementById("verba-count").textContent = G.verba.size;
}
document.getElementById("verba-counter").addEventListener("click", () => {
  const list = [...G.verba].map(la => {
    const v = VERBA_MAP[la];
    return "★ " + la + " – " + v.de;
  }).join("\n") || "Nondum verba collegisti!";
  showFeles("VERBA COLLECTA (" + G.verba.size + "):\n" + list);
});

// ---------- Inventar ----------
const invEl = document.getElementById("inventory");
function renderInventory() {
  invEl.innerHTML = "";
  G.inventory.forEach(item => {
    const li = document.createElement("li");
    const info = ITEMS[item];
    li.textContent = (G.selected === item ? "▸ " : "") + info.la;
    if (G.selected === item) li.classList.add("selected");
    li.title = info.de;
    li.onclick = () => {
      if (G.selected === item) { G.selected = null; }
      else {
        if (G.selected) tryCombine(G.selected, item);
        else { G.selected = item; sound("click"); }
      }
      renderInventory();
    };
    invEl.appendChild(li);
  });
}
function tryCombine(a, b) {
  G.selected = null;
  const c = COMBINES.find(c =>
    (c.a === a && c.b === b) || (c.a === b && c.b === a));
  if (c) {
    sound("take");
    showFeles(c.hint || c.la);
  } else {
    sound("error");
    showFeles("Miau! Haec duo non combinantur.");
  }
}

// ---------- Hotspot-Handling ----------
function applyResult(res) {
  if (!res) return;
  if (res.give) { G.addItem(res.give); }
  if (res.give2) { G.addItem(res.give2); }
  if (res.take) { G.removeItem(res.take); }
  renderInventory();
  if (res.verbum) G.verbaAdd(res.verbum);
  if (res.type === "text") { showText(G.char === "lucius" ? "Lucius" : "Aurelia", res.la); sound("click"); }
  if (res.type === "take") {
    G.addItem(res.item); renderInventory(); sound("take");
    showText("Feles", res.la || (ITEMS[res.item].la + " in saccum mitto!"));
  }
  if (res.type === "dialog") {
    const lines = res.lines.slice();
    if (res.give || res.give2) {
      const item = res.give || res.give2;
      lines.push(["Feles", ITEMS[item].la + " in saccā est!"]);
    }
    showDialog(lines, res.choice ? () => showChoice(res.choice) : null);
  }
  if (res.type === "feles") showFeles(res.text);
  if (res.type === "choice") showChoice(res.choice);
  if (res.type === "goto") { G.scene = res.target; updateSceneName(); sound("click"); }
}
function updateSceneName() {
  document.getElementById("scene-name").textContent = "» " + SCENES[G.scene].name;
}

function spotAt(x, y, spots) {
  for (const sp of spots) {
    if (x >= sp.x && x <= sp.x + sp.w && y >= sp.y && y <= sp.y + sp.h) return sp;
  }
  return null;
}
function stageCoords(e) {
  const r = canvas.getBoundingClientRect();
  return {
    x: (e.clientX - r.left) / r.width * 640,
    y: (e.clientY - r.top) / r.height * 360
  };
}
canvas.addEventListener("mousemove", e => {
  const { x, y } = stageCoords(e);
  const sc = SCENES[G.scene];
  hoverSpot = spotAt(x, y, sc.hotspots) || spotAt(x, y, sc.exits);
  canvas.style.cursor = hoverSpot ? "pointer" : "default";
});
canvas.addEventListener("click", e => {
  ensureAudio();
  if (!dialogBox.hidden) return;
  const { x, y } = stageCoords(e);
  const sc = SCENES[G.scene];
  const exit = spotAt(x, y, sc.exits);
  if (exit) {
    sound("click");
    G.scene = exit.target;
    updateSceneName();
    return;
  }
  const sp = spotAt(x, y, sc.hotspots);
  if (sp) {
    sound("click");
    G.verbaAdd(sp.la);
    const res = sp.onUse ? sp.onUse(sc, G) : null;
    if (!res && sp.target) {
      G.scene = sp.target; updateSceneName(); return;
    }
    applyResult(res);
  }
});

// ---------- Titel & Start ----------
document.querySelectorAll(".char-card").forEach(btn => {
  btn.addEventListener("click", () => {
    G.char = btn.dataset.char;
    document.getElementById("title-screen").hidden = true;
    document.getElementById("game").hidden = false;
    ensureAudio();
    startMusic();
    updateSceneName();
    renderInventory();
    updateVerbaCount();
    sound("meow");
    showDialog([
      ["Feles", "Miau! Ego sum Feles, auxilium tuum!"],
      [G.char === "lucius" ? "Lucius" : "Aurelia",
        G.char === "lucius"
          ? "Ego Lucius sum! Festum Ceres exspecto!"
          : "Ego Aurelia sum! Vias latentes amo!"],
      ["Feles", "Pecuniam a patre accipe, deinde frumentum eme! Verba collige!"]
    ]);
  });
});

requestAnimationFrame(loop);

</script>
</body>
</html>

```

Viel Spass!
