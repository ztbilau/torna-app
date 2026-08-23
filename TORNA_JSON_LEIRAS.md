# Torna leíró JSON készítése

Minden torna külön almappában legyen:

```text
/
├── index.html
├── Billa_Torna1/
│   ├── torna.json
│   ├── torzscsavaras.jpg
│   └── ...
└── Billa_Torna2/
    ├── torna.json
    └── ...
```

A `torna.json` formátuma:

```json
{
  "tornaId": "Billa_Torna2",
  "tornaReszletesNeve": "Példa torna",
  "feladatok": [
    {
      "nev": "Első feladat",
      "hosszMasodperc": 30,
      "kep": "elso.jpg",
      "leiras": "A feladat részletes leírása."
    }
  ]
}
```

A `tornaId` egyedi azonosító. A `tornaReszletesNeve` jelenik meg a felületen. A `feladatok` sorrendje adja a torna sorrendjét. A képfájlnév a torna saját mappájára vonatkozik.

Új torna hozzáadásakor az `index.html` tetején a `WORKOUTS` listába is fel kell venni:
`{ id: "Billa_Torna2", json: "Billa_Torna2/torna.json" }`

A kezdőképernyő jobb felső sarkában ugyanez a leírás és egy minta JSON is megnyitható.


## Edzésnapló mentése

A rutinok adatai a böngésző `localStorage` tárolójában maradnak. A torna
befejezésekor automatikusan bekerül az új rekord a naplóba, de ettől még nem
jön létre fájl a számítógépen.

A **„Adatok letöltése (JSON)”** gomb az összes helyben tárolt rekordból
létrehozza és letölti az `edzesnaplo.json` fájlt.


## Személyek és személyenkénti alapértelmezett torna

A személyeket a gyökérben található `szemelyek.json` tartalmazza:

```json
{
  "szemelyek": [
    {
      "nev": "Billa",
      "alapertelmezettTorna": "Billa_reggelinyujtas"
    }
  ]
}
```

A webalkalmazásban a személy mező combobox. Személy kiválasztásakor az első használatkor
az adott személy `alapertelmezettTorna` értéke kerül kiválasztásra. Ha az adott személy
korábban már választott másik tornát, azt a böngésző megjegyzi, és legközelebb azt ajánlja.


## `config.json`

Az alkalmazás gyökerében található `config.json` a központi alkalmazáskonfiguráció.

Jelenleg:

```json
{
  "debug": true,
  "time_override": 0
}
```

- `debug: true`: a második gyakorlattól a **Következő** gomb az idő letelte előtt is látható.
- `debug: false`: normál módban a **Következő** csak az adott gyakorlat célidejének letelte után jelenik meg.
- `time_override: 0`: minden gyakorlat a saját `hosszMasodperc` értékét használja.
- `time_override: 10`: minden gyakorlat 10 másodpercig tart, függetlenül a torna JSON-ban megadott időtől. A pozitív egész érték másodpercben értendő.

Az első gyakorlatnál a **Következő** gomb mindig rejtve van; ott kizárólag az **Indítás** gomb jelenik meg.


### Debug mód pontos működése

`config.json` → `debug: true` esetén az első gyakorlatnál a `Következő` gomb
az **Indítás megnyomása után azonnal** megjelenik. Indítás előtt továbbra is
csak az `Indítás` gomb látható.

`debug: false` esetén az első gyakorlatnál a `Következő` csak a 30 másodperc
letelte után jelenik meg.
