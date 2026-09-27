# Import Crussis Avinox — pregătire pentru Bikeverse (Alex)

Fișier de import: **`crussis-avinox-bikeverse-v2.xlsx`**  
Foaie: `Avinox`  
Rânduri: **503** variante (mărime)  
Produse: **106** (același `model_name` = un produs, mai multe mărimi și culori)  
Poze: folderul **`Crussis Avinox images/`**, lângă Excel. În ZIP, folderul trebuie să stea la rădăcină, cu același nume.

Fișierul vechi `crussis-avinox-bikeverse.xlsx` nu se importă. v2 e cel cu denumirile.

Sunt **biciclete**, nu componente. Importul de furci Öhlins / Andreani nu se folosește aici.

---

## 0. Înainte de import

1. Fișierul are `list_price_eur`, deci importul de biciclete îl vede ca profil Commencal. Asta e corect pentru biciclete: slug-ul primește `bicicleta-` în față.
2. Nu folosi importerul dedicat Crussis care citește portalul B2B. Sursa este Excelul ăsta plus ZIP-ul cu poze.
3. Numele de pe site este `model_name`. Slug-ul iese din el, deci `ebike` rămâne la final.
4. Brandul produsului este coloana `brand` = `Crussis`. `Avinox` este motorul (`motor_brand` / `motor_model`), nu marca bicicletei.
5. După import, verifică un produs din fiecare grupă de mai jos, plus un SKU în stoc și unul la precomandă.

---

## 1. Denumire

`model_name` este titlul SEO, același pe toate mărimile și culorile acelui model. M2 sau M2S și 600 Wh sau 800 Wh sunt deja puse pe fiecare model, după fișă.

| Grupă în fișier | Rânduri | Titlul începe cu |
| --- | ---: | --- |
| `discipline` = ENDURO | 246 | Bicicletă electrică MTB full suspension |
| `discipline` = TRAIL | 137 | Bicicletă electrică MTB hardtail |
| `discipline` = TREKKING, fără amortizor spate | 60 | Bicicletă electrică trekking |
| `discipline` = TREKKING, cu amortizor spate | 18 | Bicicletă electrică trekking full suspension |
| `discipline` = CITY | 42 | Bicicletă electrică de oraș |

Exemplu:

`Bicicletă electrică MTB full suspension Crussis e-Full 12.11-PRO Avinox M2S | 800 Wh ebike`

Cuvintele din față sunt cele căutate în România (DataForSEO): „bicicletă electrică”, „MTB”, „full suspension” sau „hardtail” sau „trekking” sau „de oraș”. La final: capacitatea bateriei și `ebike`. 1300 W și 150 Nm nu sunt în titlu. Sunt în coloanele de motor.

`family_name` este linia (ex. `e-Full 12.11-PRO`). Nu înlocuiește titlul.

Variantele ONE- sunt aceeași bicicletă, altă culoare. Nu există un produs separat „ONE”. Culoarea e în `model_color`.

---

## 2. Categorie în magazin

Coloana `category` este `E-BIKE` pe toate rândurile, ca să fie marcate electrice.

| `discipline` | Categorie magazin | Electrică |
| --- | --- | --- |
| ENDURO | enduro-all-mountain | da |
| TRAIL | trail | da |
| TREKKING | trekking-citybike | da |
| CITY | trekking-citybike | da |

Detectorul automat, cu `category` = `E-BIKE`, pune ENDURO și TRAIL bine. TREKKING și CITY cad la mountain-bike-mtb, pentru că „TREKKING” și „CITY” sunt citite din `category`, nu din `discipline`. La preview, cele 78 trekking și 42 oraș se mută la trekking-citybike și rămân electrice.

---

## 3. Preț

| Coloană | Ce este |
| --- | --- |
| `list_price_eur` | Prețul de listă **cu TVA 21% deja inclus**, în euro, cum e pe site-ul Crussis (`PRICE_VAT`). Nu se împarte la 1,21. |
| `purchase_price_eur` | Prețul net de achiziție B2B, în euro, cu 2 zecimale. |

La importul de biciclete cu `list_price_eur`, euro se transformă în lei cu cursul din admin. TVA-ul nu se mai adaugă o dată. Costul rămâne net.

---

## 4. Stoc și livrare

`stock` este cantitatea, număr întreg.

- 10 variante sunt în depozit. `stock_status` începe cu `În stoc`.
- 493 sunt precomandă. `stock_status` începe cu `Precomandă`.
- `20` înseamnă că portalul arăta „20+”. Nu există numărul exact peste 20. Pe site cantitatea scade pe măsură ce se vinde.

Textul din `stock_status` are și termenul de livrare, și ferestrele de producție. Astea nu sunt tipul de stoc.

| Începutul textului | Tip stoc | Livrare |
| --- | --- | --- |
| `În stoc` | în stoc | 5–6 zile (`delivery_days_min` 5, `delivery_days_max` 6) |
| `Precomandă` | precomandă | ferestrele scrise după, pe același SKU: pot fi mai multe (ex. 1. production, 2. production, 4. production), cu cantitatea fiecăreia |

„4. production (5-6/2027): 20” înseamnă al patrulea lot Crussis, planificat mai–iunie 2027, peste 20 de bucăți. Nu este o dată unică de livrare.

Importul actual nu citește `delivery_days_min` / `delivery_days_max` din Excel, iar fraza „În stoc. Livrare în 5-6 zile.” nu este recunoscută ca „în stoc” (se uită la „in stock” sau „stoc”, nu la „În stoc”). La preview, cele 10 bucăți din depozit se marchează în stoc, cu livrare 5–6 zile. Restul, precomandă. Nu lăsa tot catalogul pe „disponibil la furnizor”.

Transportul gratuit pe gama Avinox nu stă în `stock_status`. În fișier nu există coloană de transport. Livrarea gratuită se pune la import pe produs (cost 0), separat de stoc.

---

## 5. Descriere și specificații

| Coloană | Ce este |
| --- | --- |
| `description_html` | Textul de pe pagina publică Crussis, HTML (`<p>`). Engleză. |
| `description_html_en` | Același text. Nu există încă o descriere în română. |
| `notes` | Gol. Nu se afișează pe site. |
| `display` | Display-ul, specificație. |
| `ean` | Codul EAN. La mărimile completate din portal, fără pagină publică, EAN-ul e gol. |

Specificațiile de pe site (cadru, furcă, motor, baterie, roți) sunt în coloanele de componente, nu în descriere și nu în `notes`.

Importul de biciclete **nu scrie** `description_html` în descrierea produsului. Coloanele `description_html`, `description_html_en` și `ean` nu sunt în lista lui de coloane. La preview nu le mapa pe o piesă. Descrierea se încarcă în `shop_products.description` din `description_html`. `ean` rămâne cod, nu componentă.

`display` este deja o specificație cunoscută (Display).

---

## 6. Poze

`image_files`: căi relative, separate cu `;`, slash `/`.

Exemplu:

`Crussis Avinox images/e-Country AX 10.12-M2(600)/black, grey/01.webp`

Importul șterge automat doar prefixele `Whistle images/` și `Commencal images/`. **Nu** șterge `Crussis Avinox images/`. În ZIP, calea din celulă trebuie să existe exact, de la rădăcina arhivei.

Prima poză este coperta. Aceeași listă se repetă pe mărimile aceleiași culori.

---

## 7. Coloane pe care importul le cunoaște deja

`category`, `discipline`, `brand`, `family_name`, `model_name`, `model_color`, `frame_size`, `sku`, `list_price_eur`, `purchase_price_eur`, `stock`, `stock_status`, `image_files`, plus componentele: `frame`, `fork`, `shock`, `headset`, `stem`, `handlebar`, `grips`, `crankset`, `rear_derailleur`, `shifters_levers`, `brakes`, `cassette`, `chain`, `rim_front`, `rim_rear`, `hub_front`, `hub_rear`, `wheels`, `tyre_front`, `tyre_rear`, `seatpost`, `saddle`, `pedals`, `motor`, `motor_brand`, `motor_model`, `battery`, `battery_charger`, `motor_power_max_w`, `wheel_size_front`, `wheel_size_rear`, `display`.

`sku` este codul Crussis (`PRODUCTNO`), unic pe variantă. EAN-ul nu e cheia: un EAN e repetat pe două mărimi.

Un rând = o mărime. Componentele și prețul de listă se iau de pe primul rând al grupului `model_name`.

---

## 8. Ce nu e în fișier

- **e-Full 11.12-PRO**, 600 Wh și 800 Wh. Este pe site-ul public și în B2B, nu este în XML-ul din care s-a construit fișierul. Nu e în v2.
- Restul catalogului Crussis (Panasonic, accesorii, haine, trotinete, piese). Avinox este primul lot.
- Descriere în română.
- Parola de B2B. Nu se pune în fișier și nu se pune în cod.

---

## 9. Verificare după import

- [ ] Un e-Full (ENDURO): titlu cu „MTB full suspension”, slug cu `bicicleta-` la început și `ebike` la final, brand Crussis, motor Avinox.
- [ ] Un e-Hard (TRAIL): „MTB hardtail”, fără amortizor spate.
- [ ] Un e-Country de oraș (CITY): „de oraș”, categorie trekking-citybike, electrică.
- [ ] Un e-SUV (TREKKING): „trekking”. Un e-Country full (TREKKING cu amortizor): „trekking full suspension”.
- [ ] Aceeași linie, 600 Wh și 800 Wh, sunt produse diferite. M2 și M2S, la fel.
- [ ] Prețul de listă în lei iese din euro-ul cu TVA, la cursul din admin, fără TVA adăugat încă o dată.
- [ ] Un SKU „În stoc” are cantitatea din `stock` și livrare 5–6 zile.
- [ ] Un SKU „Precomandă” nu apare ca „în stoc”.
- [ ] Pozele se văd. Calea din ZIP începe cu `Crussis Avinox images/`.
- [ ] Descrierea HTML apare în descrierea produsului, nu într-o piesă și nu la note.
