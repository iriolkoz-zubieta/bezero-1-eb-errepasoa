# Bezero-inguruneko programazioa (DAW) — `ariketak/` eta `edukiak/` laburpena

## Irakurritakoa

Bi karpetak osagarriak dira: **`edukiak/`** da teoria eta enuntziatuak (gaztelaniaz, 14 `.pptx` + 12 `.docx`), eta **`ariketak/`** da praktika-kodea (euskara, 47 `.html`/`.js`/`.md` fitxategi). Edukiak Office formatuan daudenez, testua XMLtik atera da laburbiltzeko.

---

## `edukiak/` — teoriaren egitura

| Unitatea | Eduki nagusiak |
|---|---|
| **1. Arquitectura, cliente web y herramientas** | Internet vs. WWW (ARPANET 1969, Tim Berners-Lee 1989), TCP/IP modeloaren 4 geruzak, HTTP mezuak (eskaera/erantzun, GET vs. POST, egoera-kodeak), User-Agent, nabigatzailearen arkitektura (UI, motorra, renderizatzailea, komunikazioak, JS interpretea, XML parserra), front/back-end eta garapen-tresnak (DevTools) |
| **2. JavaScript** | Sarrera (ECMAScript, script etiketa, `noscript`, glosarioa), irteera-metodoak (`console`, `alert`, `confirm`, `prompt`, `innerHTML`, `document.write`), aldagaiak (`var`/`let`/`const`), scopea, tipoak, `typeof`/`instanceof`, eragileak eta coercion, `if`/`switch`, begiztak (`for`, `for-in`, `for-of`, `while`, `do-while`, `forEach`), `break`/`continue`, funtzioak (parametro lehenetsiak, `arguments`), string/Math/konbertsio funtzioak |
| **3. Objetos** | POO eta objektu aurrez definitutak (`Date`), arrayak (metodoak, iterazioa, `map`/`filter`/`reduce`/`every`/`some`), erabiltzailearen objektuak (literalak, `this`, konstruktorea), **prototipoak vs. klaseak**, getters/setters, herentzia, metodo estatikoak, **moduluak** (`export` izendatua/default, `import`, `type="module"`) |
| **4. Páginas dinámicas** | DOM (zuhaitza, hautatzaileak, elementuen sorrera/aldaketa/ezabaketa/nabigazioa), BOM (`window`, tamaina, mugitu/redimensionatu/ireki, `navigator`, `location`, `history`, `setTimeout`/`setInterval`, dialog oak), Web APIak (`Geolocation`, `localStorage`, `fetch`, `Notification`…) |

Gainera, **"Planificador de Fiesta"** entrega bat dago: DOMa, aldagaiak, begiztak, baldintzak eta kontagailua lantzeko proiektua.

---

## `ariketak/` — praktiken egitura

| Karpeta | Edukia |
|---|---|
| `02 - ariketak/` eta `02 - javascript/` | Irteerak (`console`/`alert`/`confirm`/`prompt`/`DOM`), dadoa, palindromoa, timerrak, zenbaki erromatarrak, begizta-piramidea, funtzioak. **`02 - ariketak` hutsik/eskema gisa dago; `02 - javascript` ebatzita.** |
| `03- 2-1 array/` | NANaren letra, bikoiti/bakoiti, bi zerrenden arteko ebakidura, artikulu-prezioak, noten batezbestekoa, asteko egunak, `reduce`-rekin maximoa, 3ren multiploak |
| `03- 2-2 array funtzioak/` | `map` (deskontuak tartearen arabera) eta `reduce` (500etik hurbilen dagoen zenbakia) |
| `03- prototipoak/` | `Circulo`, `Vehiculo`, `Pertsona` prototipoekin eta klaseekin, herentzia (`Enplegatua`→`Zuzendaria`/`Langilea`→`Ingeniaria`), metodo estatikoak, `Erabiltzailea` getters/setters balidazioekin |
| `03-04 oop - atrakzio parkea/` | Moduluak + klaseak + herentzia: `atrakzioa.js`, `parkea.js`, `index.html` (moduluekin) eta `index-nomodule.html` (dena fitxategi bakarrean) |
| `04- dom-bom/` | BOM ariketak 1–4 (div aleatorioa, informazioa, leiho mugikorra, ihes egiten duen leihoa), DOM hautatzaileen ariketak 1–6, `index.html` + `script.js`, eta `web-api/geostorage.html` (Leaflet + Geolocation + `localStorage`) |
| `2_1-irteera.html` | Irteeren ariketarako HTML txantiloi hutsa |

---

## Ohar teknikoak

- **Hizkuntza**: teoria/enuntziatuak gaztelaniaz; soluzioak eta iruzkinak euskaraz. Ariketen izenak bat datoz edukien unitateekin (2→2, 3→3, 4→4); **1. unitateak ez du ariketa-karpetarik**.
- **Maila desberdinak**: karpeta batzuek eskema hutsak dituzte (`dadoa.html`, `palindromoa.html`, `map.html`, `2_1-irteera.html`) eta beste batzuek soluzio osoa.
- **Akats txiki batzuk** (errepasoan kontuan hartzeko):
  - `02 - javascript/dadoa.html`: `Math.floor(random * (aldeak+1))` → 0 atera daiteke; zuzena `* aldeak) + 1`.
  - `2-4-funtzioak.html`: `biderketa()` parametrorik gabe deituta → `NaN`.
  - `pertsona-class.js`: `class Pertsona` gero `Pertsona = function...` bidez berridazten da → `TypeError`.
  - `herentzia-klaseekin.js`: komatxo bakuneko template literalak → `${...}` ez da ordezkatzen.
  - `atrakzio parkea/index.html`: `#forma` hautatzailea ez dator bat HTMLarekin (form-ek ez du `id`), eta `alert` falta da.
  - `04- dom-bom/ariketa3.html`: `txikitu()`-ren muga 10 da, enuntziatuak 100 eskatzen du.
  - `4.2. BOM` diapositibetan 401/403/404 kodeen azalpenak nahastuta daude.

**Laburbilduz**: material-multzo hau DAWko *Bezero-inguruneko programazioa* moduluko JavaScript ibilbide osoa da — arkitektura eta HTTPtik hasi, hizkuntzaren oinarriak, objektuak/arrayak/prototipoak/moduluak, eta DOM/BOM/Web APIekin amaituta —, teoria gaztelaniaz eta praktika euskaraz, soluzio eta enuntziatu-maila ezberdinekin.
