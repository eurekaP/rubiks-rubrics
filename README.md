# Rubik's Rubrics

A stunning (if I do say so myself), self-contained 3D Rubik's Cube visualizer and solver. A scrambled cube appears,
then solves itself with smooth, eased layer-turn animations... and you control the show.

**▶ Live demo:** https://leereilly.net/rubiks-rubriks/

![](screenshot.webp)

![Rubik's Rubrics](https://img.shields.io/badge/three.js-r160-000?logo=three.js) ![No build step](https://img.shields.io/badge/build-none-2ea043)

## Features

- **Random scramble** — the cube shows up in a random state every time.
- **Scan a real cube** — enable your webcam, hold up a physical cube face by face,
  and the browser reads the colors, shows the detected layout as an editable net
  (tap to correct any misreads), then solves it so you can watch it unscramble.
- **Animated solve** — watch it unscramble with buttery, eased quarter-turn animations.
- **Speed slider** — go from a slow crawl to turbo.
- **Timeline scrubber + transport** — scrub anywhere between *Scrambled* and *Solved*,
  step a single move back/forth, jump to either end, or play/pause.
- **GitHub contributions mode** — repaint the stickers as GitHub contribution-graph
  squares (those familiar greens).
- **Auto-rotate**, orbit (drag), and zoom (scroll) for a showcase feel.
- **Stunning rendering** — physically based glossy stickers, image-based reflections,
  soft contact shadows, and subtle bloom.

## How it works

The cube starts solved, then a random sequence of quarter turns scrambles it. The
solution is simply that sequence **reversed and inverted**, so every solve is valid by
construction — no solver library required. State is tracked as a small logical model
(each cubie's grid position + orientation quaternion), which keeps scrubbing
frame-perfect and drift-free.

A cube you **scan** with your webcam can be in any state, so that path uses a real
solver: [cubejs](https://github.com/ldez/cubejs) (Herbert Kociemba's two-phase
algorithm) runs in a Web Worker, loaded straight from a CDN. All 54 stickers are matched
against the six scanned center colors in a hue/saturation space (brightness is ignored, so
glare and uneven lighting don't wash them out) and then balanced so each color appears
exactly nine times — which fixes systematic misreads like red-vs-orange and guarantees a
legal cube. The solution it returns is fed through the same reverse-and-invert machinery,
and the visualizer plays it back.

## Running locally

It's a single `index.html` with no build step. Because it uses ES module imports from a
CDN, open it via a local server (not `file://`):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Tech

[Three.js](https://threejs.org/) (WebGL) — `RoundedBoxGeometry`, `OrbitControls`,
`RoomEnvironment`, and `UnrealBloomPass`, all loaded from a CDN via an import map.

## Open source credits

Rubik's Rubrics stands on the shoulders of two wonderful open source projects:

- **[three.js](https://github.com/mrdoob/three.js)** (MIT) — the WebGL engine behind every
  rendered frame: `RoundedBoxGeometry`, `OrbitControls`, `RoomEnvironment`, `EffectComposer`,
  and `UnrealBloomPass`.
- **[cubejs](https://github.com/ldez/cubejs)** (MIT) — Herbert Kociemba's two-phase solver,
  used to solve cubes scanned from your webcam.

Thank you to **every single person** who has contributed to them. Each sticker on the spinning
faux Rubik's cube below is the GitHub avatar of one of the **370 contributors** to those two
projects — deduplicated, so nobody appears twice. The leftover stickers (and the top and bottom
faces) wear GitHub's contribution-graph gray. ✊

<p align="center">
  <img src="contributors-cube.webp" width="700"
       alt="A spinning faux Rubik's cube whose four turning faces are tiled with the GitHub avatars of every contributor to three.js and cubejs">
</p>

<p align="center"><sub><sup>
<a href="https://github.com/06wj">06wj</a> · <a href="https://github.com/0b5vr">0b5vr</a> · <a href="https://github.com/1993heqiang">1993heqiang</a> · <a href="https://github.com/aardgoose">aardgoose</a> · <a href="https://github.com/abc013">abc013</a> · <a href="https://github.com/abernier">abernier</a> · <a href="https://github.com/abyon1224">abyon1224</a> · <a href="https://github.com/acgessler">acgessler</a> ·
<a href="https://github.com/AddictArts">AddictArts</a> · <a href="https://github.com/adrs2002">adrs2002</a> · <a href="https://github.com/afilahkle">afilahkle</a> · <a href="https://github.com/agargaro">agargaro</a> · <a href="https://github.com/agentwaj">agentwaj</a> · <a href="https://github.com/agviegas">agviegas</a> · <a href="https://github.com/akheron">akheron</a> · <a href="https://github.com/AlaricBaraou">AlaricBaraou</a> ·
<a href="https://github.com/AlbertoPa">AlbertoPa</a> · <a href="https://github.com/alexan0308">alexan0308</a> · <a href="https://github.com/AlexandreAllard">AlexandreAllard</a> · <a href="https://github.com/algrs">algrs</a> · <a href="https://github.com/almarklein">almarklein</a> · <a href="https://github.com/alteredq">alteredq</a> · <a href="https://github.com/amakaseev">amakaseev</a> · <a href="https://github.com/andreasplesch">andreasplesch</a> ·
<a href="https://github.com/AndrewRayCode">AndrewRayCode</a> · <a href="https://github.com/andreyyudin">andreyyudin</a> · <a href="https://github.com/andsve">andsve</a> · <a href="https://github.com/angelxuanchang">angelxuanchang</a> · <a href="https://github.com/AngyDev">AngyDev</a> · <a href="https://github.com/antonio-gomez">antonio-gomez</a> · <a href="https://github.com/apendua">apendua</a> · <a href="https://github.com/appache163">appache163</a> ·
<a href="https://github.com/arcoyk">arcoyk</a> · <a href="https://github.com/arobertson0">arobertson0</a> · <a href="https://github.com/arodic">arodic</a> · <a href="https://github.com/arose">arose</a> · <a href="https://github.com/artur-trzesiok">artur-trzesiok</a> · <a href="https://github.com/Astrak">Astrak</a> · <a href="https://github.com/AtiX">AtiX</a> · <a href="https://github.com/atul-mourya">atul-mourya</a> ·
<a href="https://github.com/bartmcleod">bartmcleod</a> · <a href="https://github.com/benaadams">benaadams</a> · <a href="https://github.com/bergden">bergden</a> · <a href="https://github.com/bGute">bGute</a> · <a href="https://github.com/bhouston">bhouston</a> · <a href="https://github.com/Bjvanminnen">Bjvanminnen</a> · <a href="https://github.com/borismus">borismus</a> · <a href="https://github.com/brason">brason</a> ·
<a href="https://github.com/brianchirls">brianchirls</a> · <a href="https://github.com/BrianMacIntosh">BrianMacIntosh</a> · <a href="https://github.com/brianpeiris">brianpeiris</a> · <a href="https://github.com/brunosimon">brunosimon</a> · <a href="https://github.com/Bug-Reaper">Bug-Reaper</a> · <a href="https://github.com/but0n">but0n</a> · <a href="https://github.com/cabanier">cabanier</a> · <a href="https://github.com/calrk">calrk</a> ·
<a href="https://github.com/caseygrun">caseygrun</a> · <a href="https://github.com/catalin-enache">catalin-enache</a> · <a href="https://github.com/cengizcmataraci">cengizcmataraci</a> · <a href="https://github.com/cg-cnu">cg-cnu</a> · <a href="https://github.com/cmhhelgeson">cmhhelgeson</a> · <a href="https://github.com/cnspaha">cnspaha</a> · <a href="https://github.com/CodyJasonBennett">CodyJasonBennett</a> · <a href="https://github.com/Colmea">Colmea</a> ·
<a href="https://github.com/CreaticDD">CreaticDD</a> · <a href="https://github.com/cx20">cx20</a> · <a href="https://github.com/Cy-Bo-Rg">Cy-Bo-Rg</a> · <a href="https://github.com/danielribeiro">danielribeiro</a> · <a href="https://github.com/DanielSturk">DanielSturk</a> · <a href="https://github.com/daoshengmu">daoshengmu</a> · <a href="https://github.com/daron1337">daron1337</a> · <a href="https://github.com/davcri">davcri</a> ·
<a href="https://github.com/davidlyons">davidlyons</a> · <a href="https://github.com/DavidPeicho">DavidPeicho</a> · <a href="https://github.com/DefinitelyMaybe">DefinitelyMaybe</a> · <a href="https://github.com/dforrer">dforrer</a> · <a href="https://github.com/dhritzkiv">dhritzkiv</a> · <a href="https://github.com/djreiss">djreiss</a> · <a href="https://github.com/dmarcos">dmarcos</a> · <a href="https://github.com/Dolu89">Dolu89</a> ·
<a href="https://github.com/donmccurdy">donmccurdy</a> · <a href="https://github.com/drcmda">drcmda</a> · <a href="https://github.com/drewnoakes">drewnoakes</a> · <a href="https://github.com/drojdjou">drojdjou</a> · <a href="https://github.com/drpritch">drpritch</a> · <a href="https://github.com/duanjobs">duanjobs</a> · <a href="https://github.com/dubejf">dubejf</a> · <a href="https://github.com/duhaime">duhaime</a> ·
<a href="https://github.com/edsilv">edsilv</a> · <a href="https://github.com/egraether">egraether</a> · <a href="https://github.com/ekitson">ekitson</a> · <a href="https://github.com/elalish">elalish</a> · <a href="https://github.com/EliasHasle">EliasHasle</a> · <a href="https://github.com/elijahsgh">elijahsgh</a> · <a href="https://github.com/elisee">elisee</a> · <a href="https://github.com/emilgoldsmith">emilgoldsmith</a> ·
<a href="https://github.com/empaempa">empaempa</a> · <a href="https://github.com/epreston">epreston</a> · <a href="https://github.com/erasta">erasta</a> · <a href="https://github.com/erich666">erich666</a> · <a href="https://github.com/erichlof">erichlof</a> · <a href="https://github.com/EvilPeanut">EvilPeanut</a> · <a href="https://github.com/f-a24">f-a24</a> · <a href="https://github.com/felixmariotto">felixmariotto</a> ·
<a href="https://github.com/felixpalmer">felixpalmer</a> · <a href="https://github.com/fernandojsg">fernandojsg</a> · <a href="https://github.com/FishOrBear">FishOrBear</a> · <a href="https://github.com/flimshaw">flimshaw</a> · <a href="https://github.com/flo-Ty">flo-Ty</a> · <a href="https://github.com/Fox32">Fox32</a> · <a href="https://github.com/frading">frading</a> · <a href="https://github.com/fraguada">fraguada</a> ·
<a href="https://github.com/fta2012">fta2012</a> · <a href="https://github.com/fyoudine">fyoudine</a> · <a href="https://github.com/gam0022">gam0022</a> · <a href="https://github.com/garyo">garyo</a> · <a href="https://github.com/gero3">gero3</a> · <a href="https://github.com/GGAlanSmithee">GGAlanSmithee</a> · <a href="https://github.com/gkjohnson">gkjohnson</a> · <a href="https://github.com/Glinkis">Glinkis</a> ·
<a href="https://github.com/godlzr">godlzr</a> · <a href="https://github.com/gogoend">gogoend</a> · <a href="https://github.com/gonnavis">gonnavis</a> · <a href="https://github.com/greggman">greggman</a> · <a href="https://github.com/gregtatum">gregtatum</a> · <a href="https://github.com/gsimone">gsimone</a> · <a href="https://github.com/hassanrwx">hassanrwx</a> · <a href="https://github.com/Hectate">Hectate</a> ·
<a href="https://github.com/hena-3">hena-3</a> · <a href="https://github.com/heronote">heronote</a> · <a href="https://github.com/Hoodgail">Hoodgail</a> · <a href="https://github.com/hujiulong">hujiulong</a> · <a href="https://github.com/HunterLarco">HunterLarco</a> · <a href="https://github.com/hybridherbst">hybridherbst</a> · <a href="https://github.com/HypnosNova">HypnosNova</a> · <a href="https://github.com/ianpurvis">ianpurvis</a> ·
<a href="https://github.com/insominx">insominx</a> · <a href="https://github.com/Itee">Itee</a> · <a href="https://github.com/ivankuzev">ivankuzev</a> · <a href="https://github.com/J-Rojas">J-Rojas</a> · <a href="https://github.com/jackcaron">jackcaron</a> · <a href="https://github.com/jahting">jahting</a> · <a href="https://github.com/jasonsturges">jasonsturges</a> · <a href="https://github.com/jayschwa">jayschwa</a> ·
<a href="https://github.com/jbaicoianu">jbaicoianu</a> · <a href="https://github.com/jeromeetienne">jeromeetienne</a> · <a href="https://github.com/Jhonnyg">Jhonnyg</a> · <a href="https://github.com/jlewin">jlewin</a> · <a href="https://github.com/JohannesDeml">JohannesDeml</a> · <a href="https://github.com/jonnenauha">jonnenauha</a> · <a href="https://github.com/jonobr1">jonobr1</a> · <a href="https://github.com/jostschmithals">jostschmithals</a> ·
<a href="https://github.com/jotaro-sama">jotaro-sama</a> · <a href="https://github.com/jotinha">jotinha</a> · <a href="https://github.com/jovey-zheng">jovey-zheng</a> · <a href="https://github.com/jox81">jox81</a> · <a href="https://github.com/jsantell">jsantell</a> · <a href="https://github.com/jsermeno">jsermeno</a> · <a href="https://github.com/jterrace">jterrace</a> · <a href="https://github.com/julianwa">julianwa</a> ·
<a href="https://github.com/juliendargelos">juliendargelos</a> · <a href="https://github.com/jwheare">jwheare</a> · <a href="https://github.com/kaisalmen">kaisalmen</a> · <a href="https://github.com/Kalacione">Kalacione</a> · <a href="https://github.com/kchapelier">kchapelier</a> · <a href="https://github.com/kevanstannard">kevanstannard</a> · <a href="https://github.com/kevinoe">kevinoe</a> · <a href="https://github.com/kickblade">kickblade</a> ·
<a href="https://github.com/kijunkim9">kijunkim9</a> · <a href="https://github.com/kintel">kintel</a> · <a href="https://github.com/kkruups">kkruups</a> · <a href="https://github.com/klevron">klevron</a> · <a href="https://github.com/koober">koober</a> · <a href="https://github.com/kovacsv">kovacsv</a> · <a href="https://github.com/KPkun">KPkun</a> · <a href="https://github.com/Kyle-Larson">Kyle-Larson</a> ·
<a href="https://github.com/lafflan">lafflan</a> · <a href="https://github.com/ldez">ldez</a> · <a href="https://github.com/LebedenkoN">LebedenkoN</a> · <a href="https://github.com/Lecrapouille">Lecrapouille</a> · <a href="https://github.com/leitzler">leitzler</a> · <a href="https://github.com/LeviPesin">LeviPesin</a> · <a href="https://github.com/liamlangli">liamlangli</a> · <a href="https://github.com/linbingquan">linbingquan</a> ·
<a href="https://github.com/linev">linev</a> · <a href="https://github.com/looeee">looeee</a> · <a href="https://github.com/lpsinger">lpsinger</a> · <a href="https://github.com/luhaopeng">luhaopeng</a> · <a href="https://github.com/luisfonsivevo">luisfonsivevo</a> · <a href="https://github.com/luruke">luruke</a> · <a href="https://github.com/LuWang9018">LuWang9018</a> · <a href="https://github.com/lxxxvi">lxxxvi</a> ·
<a href="https://github.com/m-schuetz">m-schuetz</a> · <a href="https://github.com/m1kc3b">m1kc3b</a> · <a href="https://github.com/m4jing">m4jing</a> · <a href="https://github.com/maccesch">maccesch</a> · <a href="https://github.com/magnitudoOrg">magnitudoOrg</a> · <a href="https://github.com/MagnuzBinder">MagnuzBinder</a> · <a href="https://github.com/makc">makc</a> · <a href="https://github.com/Makio64">Makio64</a> ·
<a href="https://github.com/manthrax">manthrax</a> · <a href="https://github.com/marcofugaro">marcofugaro</a> · <a href="https://github.com/marquizzo">marquizzo</a> · <a href="https://github.com/martinRenou">martinRenou</a> · <a href="https://github.com/marwie">marwie</a> · <a href="https://github.com/MasterJames">MasterJames</a> · <a href="https://github.com/mattdesl">mattdesl</a> · <a href="https://github.com/matthewtung">matthewtung</a> ·
<a href="https://github.com/mbredif">mbredif</a> · <a href="https://github.com/Mcgode">Mcgode</a> · <a href="https://github.com/meatbags">meatbags</a> · <a href="https://github.com/merwaaan">merwaaan</a> · <a href="https://github.com/Methuselah96">Methuselah96</a> · <a href="https://github.com/mghini">mghini</a> · <a href="https://github.com/MichaelBuerge">MichaelBuerge</a> · <a href="https://github.com/MiiBond">MiiBond</a> ·
<a href="https://github.com/milcktoast">milcktoast</a> · <a href="https://github.com/mixtur">mixtur</a> · <a href="https://github.com/mjurczyk">mjurczyk</a> · <a href="https://github.com/mkeblx">mkeblx</a> · <a href="https://github.com/mkkellogg">mkkellogg</a> · <a href="https://github.com/mmjinglin163">mmjinglin163</a> · <a href="https://github.com/MongooseSong">MongooseSong</a> · <a href="https://github.com/moraxy">moraxy</a> ·
<a href="https://github.com/mqp">mqp</a> · <a href="https://github.com/mrdoob">mrdoob</a> · <a href="https://github.com/mrienstra">mrienstra</a> · <a href="https://github.com/mrxz">mrxz</a> · <a href="https://github.com/msmolens">msmolens</a> · <a href="https://github.com/Mugen87">Mugen87</a> · <a href="https://github.com/munrocket">munrocket</a> · <a href="https://github.com/naotaro0123">naotaro0123</a> ·
<a href="https://github.com/ndebeiss">ndebeiss</a> · <a href="https://github.com/newstart0514">newstart0514</a> · <a href="https://github.com/ngokevin">ngokevin</a> · <a href="https://github.com/NikitaIT">NikitaIT</a> · <a href="https://github.com/nikolas">nikolas</a> · <a href="https://github.com/NINE78">NINE78</a> · <a href="https://github.com/nkrkv">nkrkv</a> · <a href="https://github.com/NNskelly">NNskelly</a> ·
<a href="https://github.com/notoguz">notoguz</a> · <a href="https://github.com/nraynaud">nraynaud</a> · <a href="https://github.com/nthitz">nthitz</a> · <a href="https://github.com/okready">okready</a> · <a href="https://github.com/Oletus">Oletus</a> · <a href="https://github.com/omgitsraven">omgitsraven</a> · <a href="https://github.com/OndrejSpanel">OndrejSpanel</a> · <a href="https://github.com/orgicus">orgicus</a> ·
<a href="https://github.com/pailhead">pailhead</a> · <a href="https://github.com/panxinmiao">panxinmiao</a> · <a href="https://github.com/patrickfuller">patrickfuller</a> · <a href="https://github.com/PaulJacobs">PaulJacobs</a> · <a href="https://github.com/paulmasson">paulmasson</a> · <a href="https://github.com/phfatmonkey">phfatmonkey</a> · <a href="https://github.com/philogb">philogb</a> · <a href="https://github.com/plepers">plepers</a> ·
<a href="https://github.com/poof86">poof86</a> · <a href="https://github.com/PoseidonEnergy">PoseidonEnergy</a> · <a href="https://github.com/pschroen">pschroen</a> · <a href="https://github.com/puxiao">puxiao</a> · <a href="https://github.com/qeeqez">qeeqez</a> · <a href="https://github.com/qiao">qiao</a> · <a href="https://github.com/querielo">querielo</a> · <a href="https://github.com/Rabbid76">Rabbid76</a> ·
<a href="https://github.com/ranbuch">ranbuch</a> · <a href="https://github.com/raub">raub</a> · <a href="https://github.com/rectalogic">rectalogic</a> · <a href="https://github.com/Remi-Tribia">Remi-Tribia</a> · <a href="https://github.com/RemusMar">RemusMar</a> · <a href="https://github.com/RenaudRohlinger">RenaudRohlinger</a> · <a href="https://github.com/repalash">repalash</a> · <a href="https://github.com/repsac">repsac</a> ·
<a href="https://github.com/rexdk">rexdk</a> · <a href="https://github.com/rfm1201">rfm1201</a> · <a href="https://github.com/Rich-Harris">Rich-Harris</a> · <a href="https://github.com/richardmonette">richardmonette</a> · <a href="https://github.com/richtr">richtr</a> · <a href="https://github.com/Rikahei">Rikahei</a> · <a href="https://github.com/rkusa">rkusa</a> · <a href="https://github.com/rnixik">rnixik</a> ·
<a href="https://github.com/robertlong">robertlong</a> · <a href="https://github.com/s-rigaud">s-rigaud</a> · <a href="https://github.com/santi-grau">santi-grau</a> · <a href="https://github.com/satelllte">satelllte</a> · <a href="https://github.com/SBRK">SBRK</a> · <a href="https://github.com/sciecode">sciecode</a> · <a href="https://github.com/Seemspyo">Seemspyo</a> · <a href="https://github.com/sgrif">sgrif</a> ·
<a href="https://github.com/shotamatsuda">shotamatsuda</a> · <a href="https://github.com/sirxemic">sirxemic</a> · <a href="https://github.com/sneha-belkhale">sneha-belkhale</a> · <a href="https://github.com/SntsDev">SntsDev</a> · <a href="https://github.com/soadzoor">soadzoor</a> · <a href="https://github.com/soccerJoshNumberNine">soccerJoshNumberNine</a> · <a href="https://github.com/sole">sole</a> · <a href="https://github.com/Sphinxxxx">Sphinxxxx</a> ·
<a href="https://github.com/Spiri0">Spiri0</a> · <a href="https://github.com/spite">spite</a> · <a href="https://github.com/srifqi">srifqi</a> · <a href="https://github.com/stammen">stammen</a> · <a href="https://github.com/stephomi">stephomi</a> · <a href="https://github.com/stevinz">stevinz</a> · <a href="https://github.com/Stonelinks">Stonelinks</a> · <a href="https://github.com/StrandedKitty">StrandedKitty</a> ·
<a href="https://github.com/sunag">sunag</a> · <a href="https://github.com/supereggbert">supereggbert</a> · <a href="https://github.com/susiwen8">susiwen8</a> · <a href="https://github.com/sven-strothoff">sven-strothoff</a> · <a href="https://github.com/takahirox">takahirox</a> · <a href="https://github.com/taphos">taphos</a> · <a href="https://github.com/tapio">tapio</a> · <a href="https://github.com/Temdog007">Temdog007</a> ·
<a href="https://github.com/tentone">tentone</a> · <a href="https://github.com/thelazylamaGit">thelazylamaGit</a> · <a href="https://github.com/theo-armour">theo-armour</a> · <a href="https://github.com/TheophileMot">TheophileMot</a> · <a href="https://github.com/TheoTheDev">TheoTheDev</a> · <a href="https://github.com/timknip2">timknip2</a> · <a href="https://github.com/Tirzono">Tirzono</a> · <a href="https://github.com/titansoftime">titansoftime</a> ·
<a href="https://github.com/toji">toji</a> · <a href="https://github.com/tomhsiao1260">tomhsiao1260</a> · <a href="https://github.com/tparisi">tparisi</a> · <a href="https://github.com/troffmo5">troffmo5</a> · <a href="https://github.com/troy351">troy351</a> · <a href="https://github.com/trusktr">trusktr</a> · <a href="https://github.com/tschw">tschw</a> · <a href="https://github.com/ttmike">ttmike</a> ·
<a href="https://github.com/Usnul">Usnul</a> · <a href="https://github.com/valette">valette</a> · <a href="https://github.com/vanruesc">vanruesc</a> · <a href="https://github.com/vanzo16">vanzo16</a> · <a href="https://github.com/vidartf">vidartf</a> · <a href="https://github.com/vinaykulk621">vinaykulk621</a> · <a href="https://github.com/vincent">vincent</a> · <a href="https://github.com/vincent-courtalon">vincent-courtalon</a> ·
<a href="https://github.com/vincentfretin">vincentfretin</a> · <a href="https://github.com/Virtulous">Virtulous</a> · <a href="https://github.com/walfly">walfly</a> · <a href="https://github.com/Wandalen">Wandalen</a> · <a href="https://github.com/washstar">washstar</a> · <a href="https://github.com/Waxo">Waxo</a> · <a href="https://github.com/webglzhang">webglzhang</a> · <a href="https://github.com/webprofusion-chrisc">webprofusion-chrisc</a> ·
<a href="https://github.com/weiserhei">weiserhei</a> · <a href="https://github.com/WestLangley">WestLangley</a> · <a href="https://github.com/Wilt">Wilt</a> · <a href="https://github.com/wizgrav">wizgrav</a> · <a href="https://github.com/wmcmurray">wmcmurray</a> · <a href="https://github.com/wongbryan">wongbryan</a> · <a href="https://github.com/wrr">wrr</a> · <a href="https://github.com/XanderLuciano">XanderLuciano</a> ·
<a href="https://github.com/xswordsx">xswordsx</a> · <a href="https://github.com/ycw">ycw</a> · <a href="https://github.com/yellowtailfan">yellowtailfan</a> · <a href="https://github.com/yomboprime">yomboprime</a> · <a href="https://github.com/yomotsu">yomotsu</a> · <a href="https://github.com/yrns">yrns</a> · <a href="https://github.com/yuinchien">yuinchien</a> · <a href="https://github.com/zach-capalbo">zach-capalbo</a> ·
<a href="https://github.com/Zahajki">Zahajki</a> · <a href="https://github.com/zalo">zalo</a> · <a href="https://github.com/zeux">zeux</a> · <a href="https://github.com/zfedoran">zfedoran</a> · <a href="https://github.com/zhaoy-dev">zhaoy-dev</a> · <a href="https://github.com/Zielon">Zielon</a> · <a href="https://github.com/zinefer">zinefer</a> · <a href="https://github.com/zonkypop">zonkypop</a> ·
<a href="https://github.com/zorro-fr24">zorro-fr24</a> · <a href="https://github.com/zz85">zz85</a>
</sup></sub></p>

---

Made with ♥ and [GitHub Copilot](https://github.com/features/copilot) and Claude Opus 4.8 · max :metal:
