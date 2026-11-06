# 10 ariketa · Errepasoa

**DAW1 · Bezero-inguruneko programazioa**
Gaiak: **klaseak, DOMa, gertaerak eta `localStorage`**.

Ariketa laburrak dira: bakoitza 5–15 minutuan egin daiteke. Saiatu lehenengo zuk
kodea idazten; soluzioa azken aukera gisa begiratu.

> HTML bertsioa: `10_ARIKETA_ERREPASOA.html`. Bertan markatu ditzakezu egindako
> ariketak, gaiaren arabera iragazi eta soluzioak zabaldu.

---

## Edukien taula

| # | Gaia | Ariketa | Lantzen dena |
|---|---|---|---|
| 1 | Klaseak | Liburua | `class`, `constructor`, metodoa, `static` |
| 2 | Klaseak | Tenperatura | getter/setter, balidazioa, `throw` |
| 3 | Klaseak | Tresna → Mugikorra | `extends`, `super`, metodoa berridaztea |
| 4 | DOM | Zerrenda arraytik DOMera | `createElement`, `textContent`, `appendChild` |
| 5 | DOM | Noten batezbestekoa | `querySelectorAll`, spread, `map`, `reduce`, `classList` |
| 6 | DOM | `data-mota` eta iragazketa | `dataset`, `filter`, `map`, `join` |
| 7 | Gertaerak | Inprimakia | `submit`, `preventDefault`, balidazioa |
| 8 | Gertaerak | Delegazioa | `addEventListener`, `matches`, burbuileatzea |
| 9 | `localStorage` | Bisita-kontagailua | `getItem`, `setItem`, `removeItem`, string bihurtzea |
| 10 | `localStorage` | Objektua gordetzea | `JSON.stringify`, `JSON.parse`, `try/catch` |

---

## 1. Liburua: klasea, metodoa eta metodo estatikoa

**Gaia:** Klaseak

### Enuntziatua

Sortu `Liburua` klasea `constructor(izenburua, orrialdeak)` eta `laburpena()`
metodoarekin. Azken honek `"Izenburua (N orrialde)"` itzuli behar du.

Gehitu `static luzeena(liburuak)` metodoa, orrialde gehien dituen liburua
itzultzeko. Probatu hiru libururekin.

### Abiapuntua

```js
class Liburua {
  // TODO: constructor, laburpena() eta static luzeena()
}
```

### Pista

Metodo estatikoa klaseari dagokio: `Liburua.luzeena(...)`. Barruan `reduce`
erabil dezakezu.

### Soluzioa

```js
class Liburua {
  constructor(izenburua, orrialdeak) {
    this.izenburua = izenburua;
    this.orrialdeak = orrialdeak;
  }

  laburpena() {
    return `${this.izenburua} (${this.orrialdeak} orrialde)`;
  }

  static luzeena(liburuak) {
    return liburuak.reduce((luzeena, liburua) =>
      liburua.orrialdeak > luzeena.orrialdeak ? liburua : luzeena
    );
  }
}

const liburuak = [
  new Liburua("Kirmen Uribe", 120),
  new Liburua("Maddi Etxeberria", 240),
  new Liburua("Joseba Sarrionandia", 180),
];

console.log(liburuak[1].laburpena());
console.log(Liburua.luzeena(liburuak).izenburua); // "Maddi Etxeberria"
```

**Oharra:** `static` metodoa ezin da instantzia batetik deitu
(`liburuak[0].luzeena(...)` okerra litzateke); klaseari dagokio.

---

## 2. Tenperatura: getter, setter eta balidazioa

**Gaia:** Klaseak

### Enuntziatua

Sortu `Tenperatura` klasea. Barruko balioa `_celsius` izango da.

- `celsius` getterrak balioa itzuliko du.
- `celsius` setterrak zenbaki bat dela egiaztatuko du; bestela `Error` jaurtiko du.
- `fahrenheit` getterrak `C * 9/5 + 32` kalkulatuko du.

Probatu `new Tenperatura(20)` eta 0 balioarekin.

### Abiapuntua

```js
class Tenperatura {
  constructor(celsius) {
    this.celsius = celsius; // setterra deitzen da
  }

  // TODO: get/set celsius, get fahrenheit
}
```

### Pista

Getter eta setterrak propietate gisa erabiltzen dira: `t.celsius = 0`, ez
`t.celsius(0)`. Konstruktorean esleitzean setterra exekutatzen da.

### Soluzioa

```js
class Tenperatura {
  constructor(celsius) {
    this.celsius = celsius;
  }

  get celsius() {
    return this._celsius;
  }

  set celsius(balioa) {
    if (typeof balioa !== "number" || Number.isNaN(balioa)) {
      throw new Error("Tenperatura zenbaki bat izan behar da");
    }
    this._celsius = balioa;
  }

  get fahrenheit() {
    return this._celsius * 9 / 5 + 32;
  }
}

const t = new Tenperatura(20);
console.log(t.fahrenheit); // 68

t.celsius = 0;
console.log(t.fahrenheit); // 32
```

**Oharra:** `this._celsius` erabiltzeak saihesten du setterrak bere burua
deitzea (`this.celsius = ...` jarriko bagenu, begizta infinitua litzateke).

---

## 3. Tresna → Mugikorra: extends eta super

**Gaia:** Klaseak

### Enuntziatua

1. Sortu `Tresna` klasea: `izena` propietatea eta `deskribatu()` metodoa
   (`"Tresna: izena"`).
2. Sortu `Mugikorra` azpiklasea `extends` erabiliz, `marka` propietate
   gehigarriarekin.
3. Berridatzi `deskribatu()` `super.deskribatu()` erabiliz:
   `"Tresna: Smartphone — Pixel"`.
4. Egiaztatu `m instanceof Tresna` → `true`.

### Abiapuntua

```js
class Tresna {
  // TODO: constructor eta deskribatu()
}

class Mugikorra extends Tresna {
  // TODO: super(), marka eta deskribatu() berridatzia
}
```

### Pista

`super(izena)` deitu behar da `this` erabili aurretik. Gurasoaren metodoa
`super.deskribatu()` bidez deitzen da.

### Soluzioa

```js
class Tresna {
  constructor(izena) {
    this.izena = izena;
  }

  deskribatu() {
    return `Tresna: ${this.izena}`;
  }
}

class Mugikorra extends Tresna {
  constructor(izena, marka) {
    super(izena);
    this.marka = marka;
  }

  deskribatu() {
    return `${super.deskribatu()} — ${this.marka}`;
  }
}

const m = new Mugikorra("Smartphone", "Pixel");
console.log(m.deskribatu());      // "Tresna: Smartphone — Pixel"
console.log(m instanceof Tresna); // true
```

**Oharra:** `super()` deitu aurretik `this` erabiltzeak `ReferenceError`
eragiten du.

---

## 4. Zerrenda arraytik DOMera

**Gaia:** DOMa

### Enuntziatua

Array honetako elementu bakoitzeko `<li>` bat sortu eta `#zerrenda` barruan
gehitu:

```js
["sagarra", "banana", "udarea"];
```

Erabili `createElement`, `textContent` eta `appendChild`; ez `innerHTML`.

### Abiapuntua

```html
<ul id="zerrenda"></ul>
```

```js
const frutak = ["sagarra", "banana", "udarea"];
const zerrenda = document.querySelector("#zerrenda");

// TODO: sortu li bana eta gehitu zerrendari
```

### Pista

Elementua sortu → edukia ezarri → gurasoari gehitu. `forEach` egokia da hemen.

### Soluzioa

```js
const frutak = ["sagarra", "banana", "udarea"];
const zerrenda = document.querySelector("#zerrenda");

frutak.forEach((fruta) => {
  const li = document.createElement("li");
  li.textContent = fruta;
  zerrenda.appendChild(li);
});
```

**Oharra:** `textContent` erabiltzeak erabiltzailearen testuak seguru uzten
ditu; `innerHTML` erabiltzeak XSS arriskua du.

---

## 5. Noten batezbestekoa eta classList

**Gaia:** DOMa

### Enuntziatua

Irakurri nota guztiak, kalkulatu batezbestekoa eta erakutsi `#batezbestekoa`
elementuan `"Batezbestekoa: 6.0"` formatuan.

Gainera, 5etik beherako notek `gainditua` klasea kenduta eduki dezatela, eta
gaindituenek klase hori izan dezatela. Erabili `querySelectorAll`, spread,
`map`, `reduce` eta `classList.toggle`.

### Abiapuntua

```html
<ul id="notak">
  <li class="nota">8</li>
  <li class="nota">4</li>
  <li class="nota">6</li>
</ul>
<p id="batezbestekoa"></p>
```

```js
// TODO: irakurri notak, kalkulatu batezbestekoa eta markatu gaindituak
// CSS adibidea: .gainditua { color: #7dd3a8; font-weight: 700; }
```

### Pista

`querySelectorAll`-ek NodeList bat itzultzen du. `map` erabili nahi baduzu,
bihurtu array: `[...notak]`.

### Soluzioa

```js
const notak = document.querySelectorAll(".nota");
const balioak = [...notak].map((li) => Number(li.textContent));

const batezbestekoa =
  balioak.reduce((acc, n) => acc + n, 0) / balioak.length;

document.querySelector("#batezbestekoa").textContent =
  `Batezbestekoa: ${batezbestekoa.toFixed(1)}`;

notak.forEach((li) => {
  li.classList.toggle("gainditua", Number(li.textContent) >= 5);
});
```

**Oharra:** `toFixed(1)`-ek string bat itzultzen du; hori da nahi duguna
`textContent` ezartzeko.

---

## 6. data-mota atributua eta iragazketa

**Gaia:** DOMa

### Enuntziatua

Bildu `#produktuak` zerrendako `data-mota="fruta"` duten elementuak, atera
haien testua eta erakutsi `#frutak` paragrafoan koma bidez banatuta:
`"Sagarra, Banana"`.

Erabili `dataset` eta `filter`/`map`.

### Abiapuntua

```html
<ul id="produktuak">
  <li data-mota="fruta">Sagarra</li>
  <li data-mota="barazki">Azenarioa</li>
  <li data-mota="fruta">Banana</li>
  <li data-mota="barazki">Porrua</li>
</ul>
<p id="frutak"></p>
```

### Pista

`data-mota` atributua `elementua.dataset.mota` bidez atzitzen da (kamelCase
bihurtuta).

### Soluzioa

```js
const produktuak = [...document.querySelectorAll("#produktuak li")];

const frutak = produktuak
  .filter((li) => li.dataset.mota === "fruta")
  .map((li) => li.textContent);

document.querySelector("#frutak").textContent = frutak.join(", ");
```

**Oharra:** `dataset` balioak beti stringak dira; zenbakiak behar badituzu,
`Number(...)` erabili.

---

## 7. Inprimakia: submit, preventDefault eta balidazioa

**Gaia:** Gertaerak

### Enuntziatua

Kudeatu `submit` gertaera:

1. Deitu `preventDefault()` orria ez berriz kargatzeko.
2. Irakurri `#izena` balioa `trim()` eginez.
3. Hutsik badago, erakutsi `"Izena hutsik dago."`.
4. Bestela, erakutsi `"Kaixo, <izena>!"` eta garbitu inprimakia.

### Abiapuntua

```html
<form id="forma">
  <input id="izena" type="text" placeholder="Zure izena">
  <button type="submit">Bidali</button>
</form>
<p id="mezua" role="status"></p>
```

### Pista

`preventDefault()` gabe nabigatzaileak orria berriz kargatuko du. `value` beti
da string.

### Soluzioa

```js
const forma = document.querySelector("#forma");
const mezua = document.querySelector("#mezua");

forma.addEventListener("submit", (e) => {
  e.preventDefault();

  const izena = document.querySelector("#izena").value.trim();

  if (!izena) {
    mezua.textContent = "Izena hutsik dago.";
    return;
  }

  mezua.textContent = `Kaixo, ${izena}!`;
  forma.reset();
});
```

**Oharra:** `return` goiztiarrak kodea argitzen du: balidazioak huts eginez
gero, ez gara aurrera joaten.

---

## 8. Gertaeren delegazioa zerrendan

**Gaia:** Gertaerak

### Enuntziatua

Gehitu click entzule **bakarra** `#zerrenda`-ri. `li` bati klik egitean,
txandakatu `eginda` klasea (`classList.toggle`).

Erabili `e.target.matches("li")` edo `closest("li")`, eta azaldu zergatik ez
den beharrezkoa `li` bakoitzeko listener bat jartzea.

### Abiapuntua

```html
<ul id="zerrenda">
  <li>Ikasi JavaScript</li>
  <li>Egin kirola</li>
  <li>Irakurri liburu bat</li>
</ul>
```

```css
.eginda {
  text-decoration: line-through;
  opacity: 0.6;
}
```

```js
// TODO: entzule bakarra #zerrendan eta klikaren kudeaketa
```

### Pista

Gertaerak burbuileatzen dute: semearen klik gurasora iristen da. Guraso
bakarrean entzuteari **delegazioa** esaten zaio.

### Soluzioa

```js
const zerrenda = document.querySelector("#zerrenda");

zerrenda.addEventListener("click", (e) => {
  if (e.target.matches("li")) {
    e.target.classList.toggle("eginda");
  }
});

// Elementuak gero gehitzen badira, entzule berriak ez dira behar:
// delegazioari esker, li berriek ere funtzionatzen dute.
```

**Oharra:** `li` barruan elementu gehiago egongo balira, `e.target` seme
sakonena izan daiteke; orduan `e.target.closest("li")` seguruagoa da.

---

## 9. Bisita-kontagailua localStoragean

**Gaia:** `localStorage`

### Enuntziatua

Gorde `bisitak` gakoan zenbat bisita egin diren:

1. Irakurri aurreko balioa (ez badago, 0).
2. Batu 1 eta gorde berriro.
3. Erakutsi kopurua kontsolan.
4. Gehitu `removeItem` baten bidez kontagailua berrezartzeko aukera.

Gogoratu `localStorage`-k **stringak** gordetzen dituela.

### Pista

`localStorage.getItem("bisitak")` lehen aldian `null` da. Erabili
`Number(...) || 0` edo `??`.

### Soluzioa

```js
const gakoa = "bisitak";

const aurrekoa = Number(localStorage.getItem(gakoa)) || 0;
const bisitak = aurrekoa + 1;

localStorage.setItem(gakoa, bisitak);
console.log(`Bisita kopurua: ${bisitak}`);

// Kontagailua berrezartzeko:
function berrezarri() {
  localStorage.removeItem(gakoa);
}

// berrezarri();
```

**Oharra:** `localStorage` `file://` bidez ez da beti fidagarria. Probatzeko,
erabili zerbitzari lokala: `python -m http.server`.

---

## 10. Objektua localStoragean: JSON.stringify / JSON.parse

**Gaia:** `localStorage`

### Enuntziatua

1. Gorde `{ izena: "Ane", puntuazioa: 8 }` objektua `emaitza` gakoan JSON gisa.
2. Irakurri eta bihurtu berriro objektu.
3. Gakoa ez badago edo JSONa baliogabea bada, erabili lehenetsia:
   `{ izena: "Ezezaguna", puntuazioa: 0 }`.
4. Erakutsi `izena` eta ezabatu gakoa `removeItem` bidez.

### Pista

Gordetzeko `JSON.stringify`; irakurtzeko `JSON.parse`. Erabili `try/catch`
JSON baliogabea kudeatzeko.

### Soluzioa

```js
const gakoa = "emaitza";
const lehenetsia = { izena: "Ezezaguna", puntuazioa: 0 };

localStorage.setItem(
  gakoa,
  JSON.stringify({ izena: "Ane", puntuazioa: 8 })
);

let emaitza = lehenetsia;

try {
  const gordea = localStorage.getItem(gakoa);
  if (gordea) {
    emaitza = { ...lehenetsia, ...JSON.parse(gordea) };
  }
} catch {
  emaitza = lehenetsia;
}

console.log(emaitza.izena); // "Ane"
localStorage.removeItem(gakoa);
```

**Oharra:** `{ ...lehenetsia, ...JSON.parse(gordea) }` erabiliz, gorde den
objektuak eremu batzuk soilik baditu, falta direnak lehenetsitik hartzen dira.

---

## Azken zerrenda

- [ ] 1. Liburua klasea eta `static luzeena()`
- [ ] 2. Tenperatura getter/setter balidazioarekin
- [ ] 3. `Tresna` → `Mugikorra` herentzia
- [ ] 4. Arraya `<li>` elementu bihurtu
- [ ] 5. Noten batezbestekoa eta `classList`
- [ ] 6. `dataset` bidezko iragazketa
- [ ] 7. Formularioaren `submit` eta balidazioa
- [ ] 8. Gertaeren delegazioa
- [ ] 9. Bisita-kontagailua `localStorage`-n
- [ ] 10. Objektua JSON gisa gorde eta irakurri
