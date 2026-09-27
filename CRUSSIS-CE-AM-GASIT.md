# Crussis B2B — ce am găsit (27 sep 2026)

## Decizie (după-amiază)

- Ce e pe stoc rămâne stoc. La `20+` scriem **20**. Pe site se scade când cumpărați. Actualizarea zilnică vine din feed-ul de stoc, nu din scrape.
- Ce nu e pe stoc intră la precomandă, cu ferestrele de producție (9–10/2026, 10/2026, 1–3/2027, 3–4/2027, 5–6/2027).
- Descrierea și specificațiile se iau de pe pagina publică / din XML-ul public.
- În magazin intră tot catalogul. Prima probă, de publicat: **doar Avinox**. Restul după ce verificăm proba.
- Prețul de cumpărare la biciclete, verificat pe un model: preț magazin fără TVA / 1,35. Feed-ul dă prețul cu TVA; îl împărțim la 1,21.

## Feed-uri găsite în PDF-ul „XML feeds MY2026”

Manualul din Downloads nu are export. PDF-ul din Data da:

- Avinox (public, 496 variante, an 2027 în câmpul Year): `https://www.crussis.com/eshop-export-kola-dji.xml?export_lang=2&lang=2`
- Panasonic 2026: `https://www.crussis.com/eshop-export-kola-2026-panasonic.xml?export_lang=2`
- Stoc, doar logat pe `.eu`: `https://b2b.crussis.eu/feeds/zbozidostupnost.xml?export_lang=2&lang=2` — 2094 coduri, cantitate + `in stock` / `not in stock` / `sold out`. Fără data de producție.

Copii locale: `feeds/avinox.xml`, `feeds/panasonic-2026.xml`, `feeds/zbozidostupnost.xml`.

Toate cele 496 de coduri Avinox se potrivesc în feed-ul de stoc. Acum: 11 pe stoc, 484 de comandat, 1 sold out. Datele de producție nu sunt în niciun fișier; rămân pe pagina B2B.


Portalul care merge: **https://b2b.crussis.eu** (engleză).  
Contul nu are acces pe https://b2b.crussis.cz. După login acolo apare steagul și te trimite pe `.eu`.  
Cont: SC Secoval Consulting SRL, cod client 2374-RO11.

Nu am pus nimic în coș și nu am trimis mesaje. Bifa „Retail prices” am încercat-o și am lăsat-o la loc, debifată.

---

## Pe scurt

Nu există un Excel gata cu preț și stoc. Stocul și datele de producție stau pe fiecare cod, în lista „Select availability”.  
Specificațiile de bicicletă nu sunt pe B2B. Fiecare bicicletă are un link către pagina publică de pe crussis.com.

Un rând de import = un cod. Mărimea, bateria și linia ONE sunt coduri separate, fiecare cu EAN propriu.

---

## Cum e organizat magazinul

Meniu principal:

| Zonă | Subcategorii |
|---|---|
| Electrobikes 2027 | AVINOX, PANASONIC GXM, PANASONIC GXPP, ZADNÍ POHON (motor spate) |
| Electrobikes 2026 | PANASONIC GX ULTIMATE, PANASONIC GX Power Plus (puțin stoc rămas) |
| Scooterbikes | CROSS, CROSS Hard, COBRA, COBRA Sport, ROAD |
| Sportswear | tricouri, pantaloni, hanorace, căciuli, șosete, mănuși, genți, leggings — bărbați / femei |
| Accessories | apărători, genți, suporturi, pompe, sticle, scule, lumini, căști, coarne, lese câini |
| Spare parts | display, cabluri, încărcătoare, senzori, unități, baterii, motoare, frâne, pedale, Chip tuning set |
| Promotional materials | steag, cort, etc. |

Sub AVINOX, categoriile merg până la tip de cadru și baterie: de exemplu MTB Full Carbon (REM bat) și (FIX bat). REM = baterie scoasă, FIX = baterie fixă. Asta e deja în firul de pâine al produsului, deci o putem pune în categorie.

Firul de pâine, exemplu: Electrobikes 2027 > AVINOX > MTB AVINOX > MTB Full Carbon (FIX bat).

Ordine de mărime (lista se încarcă la derulare, 12 pe pagină; uneori site-ul repetă pagina 1, deci numărul exact îl fixăm la export, cu pauză):

- biciclete 2027: în jur de 700 de coduri
- biciclete 2026: 21
- trotinete: 37
- echipament: în jur de 290
- accesorii: 86
- piese: câteva sute (am văzut baterii reale pe la pagina 3: LG 36V 720 Wh / 900 Wh)
- promo: 29

Pagina „All products” există, dar amestecă totul (pornește cu accesorii). Exportul se face pe categorii, nu de pe pagina asta.

---

## Stoc și precomandă

Trei bife, deasupra listei. Sunt lipicioase: rămân bifate și pe alte categorii, până le scoți.

1. **In stock immediately** (`paramfiltr-10`) — coduri care au bucăți în depozit acum.
2. **For order** (`paramfiltr-4`) — coduri care nu au stoc imediat, doar ferestre de producție.
3. **Watched** — produse pe care le urmărești tu (butonul „Monitor availability” la epuizate). Nu e un filtru de catalog.

Dacă le bifezi pe primele două odată, lista iese goală: „No products match the specified criteria”.

Pe card, la multe biciclete 2027 scrie portocaliu **Order with**, chiar dacă au stoc. Numărul real este în lista de lângă coș:

- linia **In stock**, id intern `real_stock` — de exemplu 1 pc, 8 pc, 13 pc sau 20+ pc
- apoi ferestrele, fiecare cu cantitatea ei

Exemplu real, `e-Full 12.11-(800 Wh) (S)`:

- In stock: 1 pc
- 4. production (5-6/2027): 20+ pc

Același cod poate fi și pe stoc, și la precomandă. La bicicletele 2027, filtrul „In stock immediately” a lăsat cam 36 de coduri care au linia `real_stock`.

Ferestre văzute:

- 1. production (9-10/2026)
- 5. production (10/2026)
- 2. production (1-3/2027)
- 1. production (3-4/2027)
- 4. production (5-6/2027)

Alte stări, fără listă de producție:

- `In stock 8 pc` / `In stock 20+ pc` — se poate pune direct în coș (biciclete 2026, accesorii, trotinete)
- `Sold out` sau `Not in stock` — buton „Monitor availability”, fără dată

`20+` nu este un număr exact. În Excel: stock = 20, iar în status rămâne textul `20+ pc`.

---

## Prețuri

Totul e în EUR.

Pe card, exemplu accesoriu:

- Retail: 29,90 EUR (cu TVA) / 24,71 EUR fără TVA
- B2B: 16,47 EUR (aceeași sumă și „cu TVA”, și „fără TVA”) — prețul tău de cumpărare, net

TVA-ul din prețul de magazin este 21% (ceh). Verificat: 1.949 / 1,21 = 1.610,74.

Marja afișată:

- 35% la biciclete și trotinete
- 50% la accesorii și echipament

Înseamnă (preț magazin fără TVA − preț B2B) / preț B2B. La e-Country 513 Wh / 15": magazin 1.610,74, cumpărare 1.193,14.

Bifa **Retail prices** din header ascunde linia B2B și lasă doar prețul de magazin. Pentru import ne trebuie amândouă, deci bifa rămâne debifată.

Pentru BikeVerse, ca la Commencal: `list_price_eur` = prețul de magazin **fără TVA**, `purchase_price_eur` = B2B. Cursul din admin face lei. Dacă vrei prețul cu TVA deja în EUR, spune-mi.

---

## Ce este un produs

Un cod = o variantă.

`e-Country 7.11-(513 Wh) (15)`

- EAN 8595640731473
- id intern de coș `pridat=2865` (nu îl folosim ca SKU)
- aceeași familie, alte coduri: 17", 19", și linia ONE (EAN diferit, 8595640731534 la ONE 15")
- pe site-ul public, 15/17/19 și bateriile 513 / 800 stau pe o singură pagină. Pe B2B sunt coduri separate. Linkul „Technical specifications” de pe fiecare cod duce la pagina publică potrivită. La unele modele 2027, adresa publică încă are „2026” în link. O urmăm așa cum e, nu o ghicim.

Linia **ONE-** este o a doua variantă de produs, cu poze proprii (`one-country-7-11-01` …). În text nu scrie culoarea (negru, verde etc.). Pe site-ul public, „black” apare doar la piese (colier șa), nu ca nume de culoare al bicicletei. Până nu ne spui tu numele, în Excel culoarea rămâne `ONE` sau fără prefix.

Echipament: mărimea e în cod (`.CSW-060-3XL`) și în nume („size 3XL”, „black / yellow fluo”). Mărimile aceleiași culori sunt listate ca variante. Stocul diferă pe mărime (am văzut 2 pc, 15 pc, 20+).

Căști: mărime și culoare în nume — „pink, size L (58-62cm)”.

Trotinetă `COBRA 4.2-2`: EAN, preț, stoc 20+, marjă 35%. Blocul „variante” amestecă și alte modele (COBRA Sport, 4.4). Nu grupăm orbește după acel bloc. La biciclete, variantele din pagină au fost chiar mărimile și ONE ale aceleiași familii.

Accesoriu (coarne): descriere scrisă pe B2B — material, lungime, greutate 131 g. Cască și steag: doar EAN, fără text.

Baterii de schimb (pagina 3 din categorie): „Battery LG Li-ion 36V - 20 Ah / 720 Wh, fully integrated, black”, coduri `.CRBA-048`, `.CRBA-063` etc. Mai multe coduri au aproape același nume. Înainte de import la piese, trebuie văzut ce le deosebește (conector, motor). Primele poziții din categorie sunt suporturi de baterie, nu bateriile în sine.

---

## Specificații și poze

Pe B2B, la bicicletă, descrierea are doar EAN + link. Pe crussis.com, blocul „Technical specifications” e curat, pe grupuri:

- PERFORMANCE: motor, autonomie, baterie, încărcător, display, senzor
- FRAME: tip cadru, furcă, material
- COMPONENTS: lumini, ghidon, pipă, șa, tijă
- GEARING: schimbător, pinioane, lanț, angrenaj
- WHEELS: roți, anvelope, frâne
- LOAD CAPACITY: sarcină 120 kg. Greutatea bicicletei nu e dată — textul spune că nu o publică
- RECOMMENDATIONS: accesorii (apărători, portbagaj)

Geometria nu e tabel. Sunt două poze (desen + cote), de exemplu `geo-country-7-en`. Le putem salva lângă produs, dar nu le transformăm în numere fără să le citim noi din imagine.

Poze:

- B2B: de obicei o poză pe cod. Fișierul mare se vede în `imageQuery`, pe `b2b.crussis.cz/files/mod_eshop/produkty/...jpg`. Ce e la `/files/thumbs/` e mic.
- Site public, la e-Country: cam 10 poze de produs (`e-country-7-11-01` … `10`) plus poze de poveste. ONE are setul lui (`one-country-7-11-01` …).
- În Descărcări, „Photos electrobikes / 2027” este folder gol. Pozele 2027 le luăm de pe pagini, nu din arhivă. 2026 are subfoldere Panasonic și Avinox (nu le-am descărcat, pot fi arhive mari).

---

## Descărcări (am deschis folderele)

| Folder | Ce e |
|---|---|
| Data | EAN 2026 / 2025 / 2023 (xlsx), „XML feeds MY2026” e de fapt un PDF de o pagină, plus un feed vechi 2025 |
| Preorders / MY2027 | catalog PDF `en-crussis-my27-online`, ~16 MB, nu o listă de date |
| Marketing / Photos electrobikes | ani 2019–2027. **2027 e gol** |
| Marketing / Photos scooters, Image material, Flyers, Corporate identity | există |
| Catalogues | văzut „Catalogue scooters CRUSSIS 2024” |
| Manuals | trotinete (PDF EN 2023), e-bikes pe ani 2023–2026 plus un manual de B2B. Nu am văzut manual 2027 |
| Technical support | tutoriale Panasonic, OLI, Bafang, Avinox, accesorii |
| Claims | proceduri de reclamație 2022, 2023, instrucțiuni de ambalare |

EAN 2027 nu e în xlsx. EAN-ul 2027 se ia de pe pagina produsului.

---

## Cont, căutare, sortare

Cont → Company details: date firmă, adrese de livrare, emailuri pentru comenzi și reclamații. Textul spune că modificările se cer la crussis.b2b@seznam.cz. Nu am schimbat nimic.

Orders: „You don't have any orders”.  
Documents: comenzi ABRA, avize, proforme, facturi, stornouri, cu filtru plătite / neplătite.  
Coșul: gol.

Contacts: firmă, depozit, facturare, reclamații, telefoane. Nu le copiez aici; sunt pe pagina Contacts.

Căutarea din header nu e de încredere. „e-Country” și „ONE-Country” au întors piese, nu biciclete. Căutarea după EAN `8595640731473` a găsit familia e-Country. Exportul se face din categorii, nu din căutare.

Sortare: Default, Prices, Availability, Name, Foundation data, crescător / descrescător.

---

## Ce pot pune în Excel, fără ajutor

Pentru fiecare cod, de pe B2B:

- cod, EAN, nume, categorie (din firul de pâine)
- mărime (din cod / nume)
- preț magazin fără TVA, preț B2B, marjă
- stoc imediat (linia In stock / `real_stock`)
- ferestrele de producție, fiecare cu cantitatea
- status: In stock / Order with / Sold out
- linkul de specificații
- poza de pe B2B

Apoi, doar la biciclete, de pe linkul public: motor, baterie, furcă, frâne, transmisie, roți, în coloanele deja folosite la Whistle / Commencal, plus galeria și poza de geometrie.

Propun un rând per cod. Ferestrele de producție stau în aceeași celulă `preorder`, separate cu `;`. Stocul imediat stă în `stock`.

---

## Ce nu am făcut, și unde am nevoie de tine

Nu am descărcat arhivele mari și nu am deschis fiecare PDF. Nu am intrat în toate cele ~80 de subcategorii produs cu produs; am luat câte un exemplu din fiecare tip (bicicletă precomandă, bicicletă cu stoc imediat, motor spate, AVINOX, trotinetă, tricou, accesoriu, cască, steag, baterie).

Întrebări, când te întorci:

1. Primul fișier: biciclete 2027 + restul de 2026 + accesorii? Echipamentul, trotinetele, piesele și promo le lăsăm pe un al doilea fișier?
2. Prețul de listă: fără TVA (recomandat) sau cu TVA deja inclus?
3. Culoarea liniei ONE: cum o numim în magazin? Pe site nu scrie.
4. Categoria „Chip tuning set” intră în magazin sau o sărim?
5. La piese, mai multe baterii au același nume și coduri diferite. Le importăm pe toate, sau doar ce e pe stoc?
