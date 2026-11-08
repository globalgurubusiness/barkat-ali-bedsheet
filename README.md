# Barkat Ali Bed Sheet — Roznamcha Khata App

Client: **Barkat Ali Bed Sheet**, Chungi No. 11, Nasir Wali Market, Shop No. 28, Multan.
Multani bedsheet business (Khes, Dari, Kambal, Crystal, Diamond waghera, ~30+ products) ke liye
Zee-style single-file web app — lekin is business ke hisaab pattern par tailored:

**Roznamcha → Khata → Baqaya → Talpat → Aakhri Hisaab**

Brand: bill wala gehra maroon `#6d1a2d` (dark `#4f1220`) + cream `#f5efe3` + gold `#b9975b`. Naam ki spelling:
logo par "Barket Ali", Urdu bill par "Barkat Ali" hai — app mein display naam `APP_NAME`
constant (script ke sab se upar) se aik line mein badla ja sakta hai; default `Barkat Ali Bed Sheet` hai.

## Files

| File | Kya hai |
|---|---|
| `index.html` | Poori app (HTML + Tailwind CDN + vanilla JS + Firebase modular SDK 10.8.0 CDN). ~3,000 lines / ~230 KB |
| `logo.jpg` | Client ka asal full logo/lockup — ab sirf SOURCE file (transparent PNG isi se banti hai); app mein seedha istemal nahi hota |
| `logo-full.png` | Full lockup (monogram + "Barket Ali" wordmark) ka transparent PNG — login screen ka bara hero (bina safed box ke, page ke cream background par) |
| `logo.png` | 'B' monogram ka transparent crop — print header (bara, 104px) aur tamam chhoti branding jaghon (app header, strip, login footer, print footer line) par |
| `gg-logo.png` | GG ka original smile logo (sirf branding line ke liye) |
| `icon-192.png`, `icon-512.png` | Logo se bane PWA icons |
| `manifest.webmanifest` | PWA manifest (install ke liye) |
| `sw.js` | Basic service worker (offline shell cache) |

## Branding (GG line)

Login screen ke footer, app ki fixed branding strip, bill print, statement print aur roz ki
report print par — har jagah ye line hai: **[Barkat Ali ka logo] Barkat Ali Khata • [GG ka
original smile logo] Powered By Global Guru** — pehle dukaan ka apna logo, phir "Barkat Ali
Khata •", phir GG logo ke saath "Powered By Global Guru". WhatsApp par statement bhejne wale
message ke aakhir mein ye line sirf text ki soorat mein jati hai (purani soorat: "Barkat Ali
Khata • Powered by Global Guru" — text mein images nahi ho sakteen, is liye woh waisi hi
hai). Print templates mein GG logo embedded (base64) hai taake offline bhi chhape; Barkat
wala logo har jagah transparent `logo.png` (monogram crop) hai — aur login screen ka bara
hero ab transparent `logo-full.png` (poora lockup, koi safed box nahi) hai.
**App ka icon change NAHI hua.**

**GG Signup Banner (sirf bahar jane wale documents par):** Jo cheez app se bahar customer /
third-party tak jati hai, us ke aakhir mein branding line se pehle aik signup banner aata hai
(GG Khata ke public statement wala approved pattern): heading **"Apna hisaab bhi aise hi
saaf rakhein!"**, bara maroon button **"Apna GG Khata Banayein — FREE Sign Up"** aur chhoti
line "Sirf Google account chahiye — 1 minute mein khata tayyar". **Print wale banner mein
URL text NAHI hai** (U21 se) — GG Khata ka link sirf **WhatsApp text** wale banner mein
jata hai. Ye banner **bill print, statement print aur WhatsApp statement text** mein hai.
**Roz ki Report (internal document) mein NAHI hai** — woh sirf andar ke istemal ke liye hai. App ki apni
screens ke andar banner bilkul nahi aata.

**Roz ki Report — compact table style:** Report (app ke andar wali bhi aur print bhi) ab
compact table ki shakl mein hai — chhota text (12–13px), tight rows (~5–6px padding),
muted caps labels, rakam right-aligned bold, aur aakhir mein **dark maroon (#4f1220) bar**
jis mein **GALLA KUL** safed bold mein aur us ki rakam gold (#b9975b) mein aati hai — rows
page par phailti nahi, content upar compact rehta hai.

**Print + Download PDF (do buttons):** Roz ki Report, Bill aur Statement — teeno jagah ab
do buttons hain: **Print** aur **Download PDF**. Print wohi purana print flow hai.
Download PDF pehli dafa internet se html2pdf library lazily load karke **asal .pdf file**
download karta hai (naam: `Roz-Report-<date>.pdf`, `Bill-<code>.pdf`,
`Statement-<party>.pdf`) — wahi print wala content (banner/branding samet). Agar library
load na ho sakay (**offline**), to fallback ke tor par print box khul jata hai aur file ka
naam document title mein set ho jata hai, taake "Save as PDF" mein wohi naam aye; print ke
baad title wapas purana ho jata hai. Library repo mein bundle NAHI hai — baqi poori app
pehle ki tarah mukammal offline chalti hai, sirf direct PDF download ko pehli dafa internet
chahiye.

**Print header (letterhead) — har printout ke sab se upar:** Bill, Statement aur Roz ki
Report — teeno prints ab AIK hi shared header se shuru hote hain: left par dukaan ka apna
**logo (B wala monogram, transparent logo.png — bara 104px; pehle wala logo.jpg tall lockup
tha, is liye 46px par monogram bohat chhota reh jata tha)**, saath mein **business ka naam
(bold) + address**, aur neeche contact detail ki line — pehle profile ke contacts **usi
saved tarteeb mein** (Talib, Aqeel, Aqib), har aik **"Naam — number1 · number2"** ki shakl
mein (sirf wohi numbers jo maujood hon; jis contact ka number na ho, sirf us ka naam), aur
**Javeed ka naam (nameLine) sab se AAKHIR mein** — sirf naam, baghair number ke (pehle ye
naam contacts se pehle aata tha; Bunny ki tarteeb par ab aakhir mein hai). Contacts khaali
hon aur nameLine bhi na ho to ye line bilkul nahi aati; sirf nameLine ho to wohi akela aata hai. Bill ka purana centered header (baray naam wala) ab
isi letterhead se badal gaya hai — teeno documents aik hi shakl ke lagte hain, aur har
document ki apni title line (Bill No/Tareekh, "Khata Statement — …", "Roz ki Report") header
ke foran neeche aati hai.

**Branding line hamesha page ke FULL BOTTOM par:** Har print template ab aik flex wrapper
(**.pwrap**) mein hai jis ka aakhri hissa GG branding line wala footer (**.pfoot**,
margin-top:auto) hai — chhota document (jaise 1-entry statement) ho to bhi line page ke
bilkul neeche aati hai, darmiyan mein nahi latakti; lamba document ho to content ke baad
normal flow mein aati hai, overlap kabhi nahi hota. Print ke liye @page A4 / 10mm margins
tay hain aur har `.psheet` ki min-height `calc(100vh − 20.5mm)` hai, taake doosra khaali page
bhi na bane. **Download PDF** wale raste mein clone ki width **794px** par pin hai aur har
sheet ki height **1080px** (border-box) — is liye PDF mein bhi line usi page par rehti hai. Branding line ke andar dono logo line ke
saath **aik hi centered unit** hain (inline-block, 20px) — pehle Barkat logo "Barkat Ali
Khata •" se pehle, phir GG logo "Powered By Global Guru" se pehle — PDF mein logo kinare par
alag-thalag nahi bhatakte.

**App ke ANDAR ab branding line sirf AIK hai:** bottom navigation ke bilkul upar wali
**fixed branding strip** (yehi logo + line, center mein) jo har section — Roznamcha, Khata,
Inventory, Baqaya/Talpat, Parties, Aakhri Hisaab, Settings — mein baghair scroll kiye har
waqt nazar aati hai; ye shell-level hai (sections ke bahir), is liye print mein nahi aati.
Settings ke aakhir mein pehle jo doosri (in-content) footer line thi, woh hata di gayi hai —
andar sirf strip hi aik line hai.

**Bill contacts (parchi wala style):** Settings ke profile form mein bill par chhapne wale
contacts naam ke saath add ho sakte hain — har contact ka naam + 2 numbers (default naam:
Talib Hussain, Aqib Hussain, Muhammad Aqeel — numbers khaali hain, user khud bharta hai),
aur aik "upar wala naam" (nameLine: Muhammad Javeed Talib Hussain) jo baghair number ke
sirf naam ki soorat mein bill par aata hai. Ye contacts ab har print (bill / statement /
report) ke shared header mein saved tarteeb se "Naam — number1 · number2" ki shakl mein
chhapte hain; jab contacts mein aik bhi number na ho to purani wali aam "Phone Numbers"
(phones) wali detail bhi usi header line mein aa jati hai (double print se bachne ke liye).
**Numbers code mein kabhi hardcode NAHI hote** — woh sirf user ke apne data (Firestore)
mein rehte hain.

Settings mein, Data Backup ke neeche, GG Khata wala poora **Contact Us section** bhi add hai —
WhatsApp Support wala green card (0302-7374880, Chat Now), "Connect Across Platforms" ke neeche
GG ke official social links (YouTube, Facebook, Instagram, TikTok, Threads) aur aakhir mein
Linktree (All Official Links) wali row.

### Print/PDF layout fix (2026-11-08, sw v23)
- **Har page par fix entries + header/footer (pagination):** prints ab `.psheet` page-sheets mein bante hain — har sheet par letterhead header upar aur branding line bilkul neeche (flex `margin-top:auto`), kai pages hon to "Page X of Y" bhi footer ke upar ata hai. Statement ki rows aur bill ki items `ENTRIES_PER_PAGE = 20` ke hisaab se banti hain (running Baqaya poori list par pehle hisaab hota hai, bantna baad mein — is liye page 2 ka pehla baqaya page 1 ke aakhri se jari rehta hai); bill ki aakhri (totals wali) sheet par jagah ke liye zyada se zyada 16 items (`BILL_TOTALS_PAGE_ITEMS`), totals + banner + signature sirf aakhri sheet par. Browser print mein har sheet `min-height:calc(100vh - 20.5mm)` + page-break ke saath aik page ki hai; downloadPDF clone ki width 794px pin aur har sheet ki height 1080px (border-box, padding andar) hai. Purana single-wrapper min-height aur explicit-px-margin wala tareeqa (jo branding line ko PDF se gayab kar raha tha) mukammal hata diya. PDF clone margin/padding 0 ke saath bilkul upar se shuru hota hai; browser print mein `#printArea` padding 16px → 10px.
- **Letterhead compact + logo bara:** naam 16px, address 11px, contacts 10.5px, faaslay 1–4px, header ke neeche wali lakeer ka margin 4px, documents ke title ka top margin 6px — header ke upar/andar ki khaali jagah khatam. Header ka Barkat logo ab 88px height par hai (cell 104px) aur logo.png content ke hisaab se trim shuda hai, is liye etraaf ki khaali jagah bhi khatam.
- **GG signup banner ab slim bar hai:** kul height ~43px (pehle ~146px + upar 26px margin; ab margin 12px) — heading aur maroon button aik hi line mein, neeche chhoti line "Sirf Google account chahiye — 1 minute mein khata tayyar" (print banner mein URL nahi; URL sirf WhatsApp text banner mein). Entries ke liye jagah bachti hai. WhatsApp wala text banner bilkul nahi badla.

### Print polish (2026-11-08, sw v24)
- **Header logo aur bara:** print header ka Barkat logo ab 104px height par hai (cell 120px).
- **Header alignment tight:** naam (line-height 1.15) → address (line-height 1.2, upar sirf 1px) → contacts (upar 2px, line-height 1.25) aik hi bandhe hue block ki tarah parte hain. Contacts left-aligned hain — har item ke baad fix 14px faasla, aakhri item ke baad 0; koi justify/space-around wala phaila hua gap nahi.
- **Banner + branding line aik bottom group mein:** aakhri sheet par signup banner aur branding line aik hi `margin-top:auto` wrapper mein sheet ke bilkul neeche chipke hue ate hain (banner pehle, us ke 6px neeche line) — banner ab entries ke foran baad nahi latakta aur us ke neeche safaid khaali jagah nahi banti. "Page X of Y" line ke bilkul upar hi rehta hai.
- **Banner se URL khatam:** printed banner mein ab `globalgurubusiness.github.io/gg-khata` wala URL text (aur link) nahi ata — sirf heading, maroon button aur "Sirf Google account chahiye — 1 minute mein khata tayyar" wali chhoti line reh gayi. WhatsApp wala text banner waisa hi hai (us ka link barqarar).
- **Branding line aur neeche:** browser print mein sheet ki min-height `calc(100vh - 20.5mm)` (safety 2mm → 0.5mm); PDF mein html2pdf ke `pagebreak: { mode: ['css', 'legacy'] }` ke saath har sheet ki height 1080px — is ke liye `.psheet` ka `page-break-after` base CSS mein bhi rakha hai taake html2pdf ka CSS mode computed style mein usay dekh sake.
- **Branding line mein dono logo aik size:** print mein dono fixed 20×20px box (Barkat logo object-fit:contain ke saath), app ki strip aur login footer mein dono 16×16 (h-4 w-4).

### Print fix — line doosre page par nahi + header align (2026-11-08, sw v25)
- **PDF mein branding line ab usi page par rehti hai:** downloadPDF mein clone ki width **794px par pin** hai (A4 @96dpi) — html2pdf ki aik-page slice height width se banti hai (794 × 297/210 ≈ 1123px), aur har sheet ki height 1080px (border-box) is se ~43px kam hai. Padding bhi `#printArea` se hata kar har `.psheet` ke **andar** kar di hai (border-box, 10px) taake koi chhupi hui extra height sheet ko slice se bahir na dhakele. Holder par margin/padding 0, position bilkul top-left.
- **Browser print mein bhi waisa hi:** `#printArea` ki padding 0, sheet ki padding andar — sheet ka kul footprint 276.5mm ≤ printable 277mm, is liye asal printing mein bhi line doosre page par nahi girti.
- **Header align:** letterhead ki dono cells ab `vertical-align:middle` par hain — 104px ka logo naam/address/contacts wale block (~75px) ke darmiyan mein align hota hai, neeche latakta nahi lagta. Logo cell ki left padding 0 hai taake logo ka kinara neeche wali statement table ke kinare se seedha mile.

## Pass 1 — Core + Save-Flow Overhaul (2026-11-08, sw v26)

Full audit ke baad hisaab core aur save/data layer ka bara overhaul (UI forms Pass 2 mein ayenge):

- **Dynamic allocation:** Sale (aur har stock-out) ki lot allocation ab mehfooz data se NAHI
  banti — `computeDerived` har dafa lot universe se dobara compute karta hai (line ka chosen
  lot sirf tab, jab us mein us waqt qty bachi ho; warna purana lot pehle). Backdated entries
  aur purani sale ki correction ke baad cost/munafa/stock khud theek ho jata hai. saveEntry
  ab allocations save NAHI karta (sirf `lotId` = chosen lot).
- **Naye entry flows (core mein mukammal, balanced postings):** `sale_return` (naya lot
  laagat par wapis, optional cash refund), `purchase_return` (farq → `adj` PnL account),
  purchase mein **exchangeItems** (maal ke badlay maal; net baqaya = net − paid − exchange),
  **discount** sale/purchase dono par (purchase lot rate discount ke tanasub se net),
  `opening_stock` (stock Dr / capital Cr), `opening_balance` (lena/dena, capital ke badlay),
  `stock_adjust` in/out (adj income/nuqsan). Entry ordering ab (date, seq, createdAt, id).
- **Payment method:** wasooli/adaigi aur sale/purchase ki wasooli-adaigi `cash` ya `bank` —
  naya `bank` account; galla hamesha sirf cash. `dailySummary` mein bankIn/bankOut alag.
- **Derived aggregates:** `productStats` (per product soldQty/revenue/cogs/profit),
  `buyerStats` (totalSale/profit), `recovery` (buyer balance + oldestOpenDate — positive
  stretch tareeqa + lastActivityDate), `headTotals`, aur `periodSummary(state, from, to)`
  (sale/cogs/expenses-by-head/netProfit/wasooli/adaigi/closingCash/closingBank).
- **computeDerived cache:** entries array + content signature na badle to dobara compute nahi.
- **parseAmt theek:** decimal durust ("500.50" → 500.5; purana parser 50050 deta tha),
  minus strip (unsigned), invalid → 0. Amount inputs mein decimal type ho sakta hai ab.
- **Save-flow fixes:** saveEntry/saveAdd/makeCorrection par in-flight lock + button disable
  (double-save duplicate khatam); entry seq/code Firestore **transaction** se
  (`workspaces/{wid}/counters/main` — rules mein counters subcollection ka access lazmi hai),
  fail ho to local max+1 fallback; **over-payment clamp khatam** (zyada wasooli/adaigi =
  advance); entry par `partyName` snapshot mehfooz (purani entries par live naam fallback);
  DEFAULT_CONTACTS ki tarteeb durust: Talib → **Aqeel → Aqib**.
- **Import = asal restore (sirf owner):** validate (entries lazmi, baqi arrays optional) →
  jo docs backup mein nahi woh batched delete, phir backup upsert, profile bhi restore.
- **Seed race khatam:** 2.5s timer gaya — seed sirf tab jab products/accounts/entries ki
  pehli server snapshot khaali aye aur role owner ho; `seedMasters` idempotent hai
  (maujooda naam skip, codes nextCode se).

## Design (locked pattern)

- **Brand color ab bill (parchi) wala maroon hai: `#6d1a2d`** (dark shade `#4f1220`) — pehle
  wala slate blue app se mukammal hata diya gaya hai (CSS vars, theme-color, manifest aur
  print templates sab jagah). Cream backgrounds aur gold accents waisay hi hain; client ke
  logo/icon files ko haath NAHI lagaya gaya.
- **Icons ab saaf professional SVG line icons hain** — poori app se emoji icons khatam
  (entry-type buttons, bottom navigation, search — sab aik hi line style: 24×24 viewBox,
  stroke 1.8, currentColor se type ke rang/brand maroon mein). WhatsApp/social brand SVG
  waisay hi hain.
- **Desktop par wide web view hai, mobile bilkul unchanged** — lg screens par shell
  `lg:max-w-6xl`, entry buttons aik row mein 7, Khata two-column (accounts list left,
  statement right), Inventory 3-column aur Parties 2-column grids, Settings cards
  `lg:max-w-3xl`. Sirf `lg:` variants aur min-width media rules add hue hain; mobile
  ki base classes ko haath nahi lagaya gaya.
- **Khata desktop par full-width rehta hai jab tak statement band ho** — two-column split
  (accounts list left, statement right) sirf statement khulne par lagta hai (`.stmt-open`
  class, `openStatement`/`closeStatement` se toggle); statement band karte hi list dobara
  poori width par aa jati hai. Settings cards ab `lg:max-w-3xl mx-auto` hain — wide screen
  par center mein rehte hain, right side khaali nahi rehti.
- **Har lambi list ke andar apna scrollbar hai (`.listscroll`)** — Roznamcha entries, search
  results, Khata accounts, statement entries, Inventory products, Buyers/Sellers, Baqaya aur
  Talpat rows: ~5–7 rows ke baad list apne hi box mein scroll hoti hai (thin maroon
  scrollbar), headers/search buttons/totals scroll-box se bahir rehte hain aur poora page
  kahin disturb nahi hota.
- **Har action par usi ke hisaab ki halki awaaz (Web Audio, offline)** — koi sound file
  nahi, oscillators se banti hai: sale par bright up-notes, purchase par lower notes,
  wasooli par cash-in ding, adaigi par down-tone, kharcha par low blip, correction par
  double-blip, ghalti/validation par low buzz, nav par bohat halki tick. Settings mein
  **Sound On/Off toggle** hai — default ON; pasand `profile.sound` mein save hoti hai,
  band ho to poori app khamosh rehti hai.


- **Front = Roznamcha hi sab kuch hai.** Entry sirf Roznamcha se hoti hai (home screen).
  Baqi sab — Khata posting (Khatoni), Baqaya, Talpat, Inventory, Galla, Munafa — backend
  mein usi aik entry se **khud-ba-khud derive** hota hai. Koi rakam kahin haath se dobara nahi likhi jati.
- Saara hisaab aik pure logic core (`BA_CORE`, `index.html` ke `<script id="core-logic">` mein)
  se nikalta hai — yehi code Node test mein bhi chala hai (neeche QA dekhein).

## Feature map — Roznamcha entry → backend effect

| Roznamcha Entry | Backend par khud-ba-khud |
|---|---|
| **Purchase** (Seller se) | Naya **Lot** banta hai apne rate ke saath • Seller ke khate mein udhaar post • Advance diya ho to Galla se kata • Stock barha |
| **Sale** (Buyer ko) | Stock **FIFO** se kata (purana lot pehle; aik sale do lot se kat sakti hai; form par lot khud chunne ka option bhi hai) • Laagat (COGS) alag post • **Munafa = (sale rate − lot rate) × qty** per lot • Buyer khate mein udhaar • Wasooli Galla mein |
| **Forms — Saada** | Saare forms bilkul saada hain: sirf chhota label + khaali khana — koi example text, placeholder ya hint line nahi (client saada dukandaar hai). Sirf Roznamcha ki bari search bar par chhota "Search" placeholder hai. Entry modal ke neeche sirf anti-fraud wali rule line rehti hai (save ki hui entry edit/delete nahi hoti).
| **Sale — Multi-Item** | Sale ab **aik bill, kai item lines** hai (parchi wala style): form mein "+ Item add karein" se jitni lines chaho; har line ka apna product / qty / rate / lot (FIFO ya khud chuna hua), lekin Buyer, tareekh, Advance aur Total **bill level** par aik hi. Har line ka stock apne lot/FIFO se kat-ta hai aur munafa line-wise jud kar entry ka banta hai; postings entry level par rehte hain (statement mein aik hi bill). Bill print par saari lines rows mein aati hain. Entry `items[]` mein save hoti hai — **purani single-item entries (baghair `items[]`) waisi hi chalti hain** (`entryItems` normalizer un ko aik line bana deta hai). Aik hi product ki do lines ka kul sum stock se zyada ho to save ruk jata hai |
| **Wasooli (Payment Received)** | Buyer ka baqaya kam • Galla barha |
| **Adaigi (Payment Given)** | Seller ka baqaya kam • Galla ghata |
| **Kharcha (Expense)** | Kharcha head ke khate mein post • Galla ghata • Aakhri Hisaab mein kharcha |
| **Sarmaya Jama (Capital)** | Galla barha • Owner capital barha |
| **Owner ne Nikala (Drawing)** | Galla ghata • Drawing post |

Views: **Roznamcha** (roz ki summary cards: Sale / Wasooli / Kharcha / Purchase / Munafa / Galla,
date badal kar purana din, roz ki report/print) • **Khata** (saare ledger accounts, tap par
statement + print + WhatsApp par statement ka khulasa) • **Inventory** (product = kul qty +
value, kholne par lot-wise: rate, aye, bike, bache; low-stock warning) • **Baqaya + Talpat**
(Naame/Jama totals, "Talpat mil gaya" check — Baqaya ke kul totals har side ke NET hain: buyer
ka advance buyers wali side mein hi minus hota hai aur seller ka advance sellers wali side
mein, advance kabhi doosri side ke total mein nahi jata; rang: Lena sabz, Dena laal) • **Parties** • **Aakhri Hisaab** (Sales − COGS =
Kham Munafa − Kharchay = Asal Munafa, Stock value, Galla, Capital) • **Settings** (bottom nav
ka 7th aur aakhri apna alag tab — neeche tafseel).

### Add har jagah — codes ke saath
- Buyer `B-001...`, Seller `S-001...`, Product `P-001...`, Hisab Head `A-001...`, Entry `E-001...`
- Codes khud bante hain, har list aur statement mein nazar aate hain, aur **Roznamcha ke
  bare Search Bar** se code / naam / phone / product / rakam / tareekh — sab se dhunda ja sakta hai.
- Entry form ke andar bhi "+ Naya add karein" har dropdown mein hai (form ki values mehfooz
  rehti hain, add karke wapas wahi form khulta hai aur nayi cheez khud select ho jati hai).

### Usool
- **Posted entry kabhi edit/delete nahi hoti** (anti-fraud, GG Khata wala hi usool).
  Ghalti par **Correction** button ulti (reversal) entry lagata hai — dono entries Roznamcha
  mein nazar aati hain, hisaab se jora khatam. Bik chuke lot wali purchase ki correction
  pehle sale ki correction maangti hai (app rok deti hai).
- Rates **kabhi average nahi** hote — har purchase ka lot apna rate rakhta hai.
- **Comma rule:** Amount wale tamam khaanon (Rakam, Rate, Wasool Hua, Ada Kiya) mein likhte hi
  comma khud lag jata hai — wohi display wala andaaz (en-IN / lakh style: 20000 → 20,000,
  1047000 → 10,47,000). Peeche hisaab hamesha saade number par hota hai, save shuda value
  nahi badalti. Quantity (pcs) wale khaane is rule se bahir hain.
- Seed (pehli dafa): 5 products — Khes, Dari, Kambal, Crystal, Diamond
  (bina kisi price ke; owner edit/deactivate kar sakta hai) aur 5 aam kharcha heads.
- Bill print un ke asal bill jaisa: Number / Tafseel / Narkh / Rupay, phir Total, Advance,
  Baqaya, Dastakhat ki jagah.
- Backup: Settings se poora data JSON export/import.

## Firebase lagana — HO GAYA (2026-11-07)

Firebase project **barkat-ali-bed-sheet** ban gaya hai (globalgurupro@gmail.com par, free Spark plan):
Firestore production mode (nam5), Google sign-in enable, workspace-model rules publish, aur
`globalgurubusiness.github.io` authorized domain mein add hai. Asal `firebaseConfig`
`index.html` mein lag gayi hai (syntax dobara check: 4/4 script blocks PASS) — app sirf
asal Firebase par chalti hai; login screen par sirf Google sign-in hai, koi bina-login
rasta NAHI hai. Neeche wale steps sirf record ke liye hain.

1. Firebase Console mein naya project banayein (alag project — Zee / GG Khata se mix nahi).
2. Web app register karke config ki 6 values `firebaseConfig` block mein paste karein
   (sirf wohi block badalna hai).
3. Authentication → Google sign-in enable karein.
4. Firestore Database banayein (production mode) aur neeche wale rules lagayein.
5. Authentication → Settings → Authorized domains mein live domain
   (masalan `globalgurubusiness.github.io`) add karein — warna Google login rukega.

Data model (workspaces — Khata Sharing, neeche tafseel):
`workspaces/{wid}` doc (`ownerUid`, `memberEmails`) aur us ke neeche
`workspaces/{wid}/parties/{id}`, `products/{id}`, `accounts/{id}`, `entries/{id}`,
`activity/{id}`, `counters/main`, `profile/main` — `onSnapshot` live sync aur
`enableIndexedDbPersistence` offline ke liye laga hai. Purana `users/{uid}/...` data
sirf migration/legacy ke tor par rehta hai (owner-only). Login: `signInWithPopup`,
popup block ho to `signInWithRedirect` fallback (reference GG Khata wala hi pattern).

### Firestore rules

Asal rules file: **`../FIRESTORE_RULES.txt`** (repo ke root mein) — Console mein wahi
paste hoti hai. Model: workspace members read sab kuch; entries/parties/products/
accounts/activity par members create+update bhi; DELETE sirf owner; profile aur
workspace doc ki write sirf owner; counters par members read+write (seq transaction);
legacy `users/{uid}` owner-only.

## Khata Sharing — kai Gmail, AIK khata (2026-11-08)

**Model:** Saara cloud data ab aik **workspace** ke neeche rehta hai:
`workspaces/{wid}` doc = `{ name, ownerUid, ownerEmail, ownerName, memberEmails: [], createdAt }`,
aur us ke neeche wohi subcollections — `workspaces/{wid}/parties|products|accounts|entries`
aur `workspaces/{wid}/profile/main`. Code mein saare cloud paths aik base helper
(`wsDocRef` / `wsCollRef`) se bante hain; `S.wid` + `S.role` ('owner' | 'member' | 'none')
active workspace ko track karte hain. BA_CORE ko wohi state shape milta hai — hisaab bilkul
nahi badla.

**Login ke baad teen halatein (`resolveWorkspace` + `pickWorkspace`):**
1. **Member:** `workspaces where memberEmails array-contains <mera email>` mile to wohi
   SHARED khata, role = member. (Naya member pehli dafa login karte hi seedha shared
   khate mein land karta hai.)
2. **Owner:** Warna `workspaces where ownerUid == <mera uid>` — pehle se bana hua mera
   apna khata, role = owner.
3. **Setup Gate:** Warna **koi workspace NAHI banta** aur **koi data NAHI dikhta** —
   user login shuda hote hue bhi band (locked) halat mein rehta hai
   (`S.wid = null`, `S.role = 'none'`, `S.needsSetup = true`): sirf **Settings** view
   khulta hai, us mein bhi sirf **Owner Setup** card (+ header mein Logout); baqi saari
   nav items aur Settings ke saare cards (Profile, Bill Contacts, Khata Sharing, Data
   Backup, Default Reset, Sound, Contact Us) chhup jate hain, aur view-switcher bhi
   Settings se bahir nahi jane deta (`applySetupGate` + `switchView` guard). Header ke
   neeche slim banner par **"Khata Setup"** likha aata hai. Cloud par kuch parha/likha
   NAHI jata, koi migration NAHI chalti. Test Gmailon ke login par khud-ba-khud koi
   asal khata NAHI banta — pehle Owner Setup, phir asal app.

NOTE: invite aur apna workspace dono hon to **invite wala jeet-ta hai** — is dukaan ka
asal khata family ka shared khata hai.

**Owner Setup — asal khata yahan se shuru hota hai (Settings ka sab se pehla card,
sirf Setup Gate mein nazar aata hai):** Input "Owner ka Naam", neeche signed-in
Gmail ki line, aur button "Apna Khata Shuru karein". Submit par (naam khaali ho to ruk
jata hai):
- Workspace banta hai — poori app mein workspace-create ka **yahi aik call site** hai
  (`setupOwnerKhata`): `{ name, ownerUid, ownerEmail, ownerName: <likha naam>, memberEmails: [], createdAt }`.
- Phir **migration** chalti hai (legacy data ho to); na ho to pehli-dafa wala seed
  defaults workspace mein lag jata hai (subscribeFirestore ka seed step).
- Gate uth jata hai aur session baghair dobara login kiye seedha asal khate mein chali
  jati hai (role = owner) — poori app khul jati hai.

**Migration (one-time, idempotent):** Owner Setup se naya workspace bante hi purana
`users/{uid}` data (parties, products, accounts, entries + profile/main) batched writes se
workspace mein COPY ho jata hai — sirf tab, jab workspace ki entries abhi khaali hon aur
legacy mein data ho. **Legacy data kabhi delete ya change NAHI hota** — woh hamesha backup
rehta hai. Purana per-user path poori app mein sirf migration reader mein bacha hai, aur
`migrateLegacyData` ka wahid call site ab Owner Setup hai.

**Owner / Members (Settings → "Khata Sharing" card, sirf cloud mode mein):**
- Card par Owner sab ko **pehle NAAM se** dikhta hai (`ownerName`), email us ke neeche;
  purane workspace (jin par `ownerName` nahi) par sirf email dikhta hai. **Owner** apna
  naam isi card mein inline edit karke Save kar sakta hai; member ko naam+email
  read-only dikhte hain.
- Card par Members ki list sab ko dikhti hai.
- **Owner** Gmail add kar sakta hai (chhota email, duplicate aur owner ka apna email reject
  hota hai) aur kisi member ko ✕ se hata sakta hai (confirm ke saath). Member add/remove
  `workspaces/{wid}` ke `memberEmails` par `updateDoc` se hota hai — workspace doc ki live
  subscription se list sab par foran update ho jati hai; naye member par tabdeeli us ke
  **agle login** par laagu hoti hai.
- **Member** card read-only dekhta hai — input/buttons sirf Owner ko milte hain.
- Har nayi entry (correction समेत) par `createdBy: { uid, name, email }` stamp lagta hai;
  entry card par sirf naam ki aik chhoti muted line nazar ati hai. Purani entries par koi
  line nahi (stamp nahi tha).

**Rules:** Asal rules `~/workspace/barkat-ali-bedsheet/FIRESTORE_RULES.txt` mein hain
(workspace doc owner-only update, subcollections owner/member read-write, legacy
`users/{uid}` owner-only barqarar). Console mein wahi paste karne hain.
**Indexes:** Resolution ki dono queries alag alag single-field hain
(`memberEmails` par array-contains, `ownerUid` par equality) — **koi composite index
nahi chahiye**.

**Bina-login rasta KHATAM (2026-11-08):** Pehle login screen par "bina login dekhein"
wala aik azmaishi (demo) rasta tha — woh mukammal hata diya gaya hai. Ab login screen
par **sirf Google sign-in** hai; signed-out halat mein sirf login screen dikhti hai,
aur local data store ka poora code bhi file se nikal gaya hai — app har halat mein
sirf asal Firebase data par chalti hai. Khata na ho to upar wala Setup Gate lagta hai.

## Settings — apna alag tab + Default Reset (2026-11-08)

**Settings ab Aakhri Hisaab ke andar nahi, bottom nav ka 7th (aakhri) apna tab hai**
(gear icon, `view-settings`). Aakhri Hisaab (`view-more`) mein sirf PnL reh gaya hai.
Settings tab mein SAB kuch aik jagah hai: sab se upar **Owner Setup** card (sirf
Setup Gate mein — khata na ho tab), phir Sound toggle, Business Profile (bill contacts
samet), Khata Sharing, Data Backup, **Default Reset**, aur aakhir mein GG wala **Contact Us**
section (WhatsApp Support + GG ke social links + Linktree row) —
GG ke social/Contact Us hamesha Settings mein hi rehte hain. Setup Gate ki halat mein
in mein se koi card NAHI dikhta — pehle Owner Setup, phir sab kuch.

**Default Reset (Settings mein, Data Backup ke baad wala card):** Red button
"Saara Data Reset karein" — dohri (double) confirm ke baad khata factory default par wapas:
saari **entries, parties, products, heads delete** ho jati hain aur pehli dafa wala seed
dobara lag jata hai (5 products — Khes, Dari, Kambal, Crystal, Diamond, bina price; 5 default
kharcha heads), aur **profile defaults** par wapas (business naam/address default, Bill
Contacts `DEFAULT_CONTACTS` — naam bhare, numbers khaali; sound pasand profile mein hoti hai
is liye woh bhi default ON par reset hoti hai).
- **NAHI chherta:** login/account, workspace doc aur `memberEmails` — **sharing list waisi
  ki waisi rehti hai**; members ka access reset se khatam NAHI hota.
- **Sirf Owner:** Ye card sirf Owner (`S.role === 'owner'`, wid ke saath) ko dikhta hai —
  **member ko card nazar hi nahi ata** aur function ke andar bhi wid + role guard hai.
  Setup Gate (khata hi nahi) mein bhi card nahi dikhta.
- Cloud mein deletes batched (450/batch) hote hain; reset ke baad UI onSnapshot se khud
  refresh ho jati hai.

## QA results (2026-11-07, asal run)

- **Syntax:** `index.html` ke chaaron inline script blocks nikale gaye — `node --check`
  sab par **PASS**.
- **Element/handler audit:** JS mein use hue 63 element IDs — sab HTML mein maujood;
  saare `onclick` handlers defined hain.
- **Logic test (Node, `BA_CORE` par)** — Bunny ki asal misaal replay ki gayi, **20/20 PASS**:
  - Purchase 100 @ Rs 1,000 (Lot 1) + 150 @ Rs 900 (Lot 2)
  - Sale 80 → FIFO se Lot 1 se kata; cost Rs 80,000; munafa (sale @1,200) Rs 16,000
  - Baqi: Lot 1 = 20, Lot 2 = 150, kul = 170, **stock value = Rs 155,000** ✓
  - Agli sale 30 → 20 Lot 1 + 10 Lot 2 (cost Rs 29,000); baqi Lot 1 = 0, Lot 2 = 140, kul = 140 ✓
  - Capital 2,00,000 + Expense 5,000 + Adaigi 40,000 + Wasooli 20,000 ke baad:
    **Talpat Naame = Jama = Rs 5,27,000 (balanced)** ✓; Buyer baqaya Rs 62,000 ✓;
    Seller baqaya −Rs 1,95,000 ✓; Galla Rs 2,25,000 ✓; Net Profit Rs 18,000 ✓
  - Sale ki reversal ke baad stock wapas Lot 1 = 20 / Lot 2 = 150 aur Talpat phir balanced ✓

## Parent ke liye baqi kaam (is build mein jaan boojh kar NAHI kiya gaya)

1. Firebase project banana + asal `firebaseConfig` paste karna + rules + authorized domain.
2. GitHub repo banana, ye folder push karna, GitHub Pages live karke asal login/click-test.
3. Client se final naam ki spelling confirm karna (Barket vs Barkat) — `APP_NAME` aik line.
4. Asal 30+ products ki list aur opening stock/baqaya client se lekar pehli entries karna.

## Pass 2 — UI / Forms (2026-11-08, sw v27)

Pass 1 ke core par mukammal UI. BA_CORE ko is pass mein NAHI chhera gaya (hash barqarar).

- **Naye entry types (grid mein 12 buttons):** Sale Wapsi (`sale_return` — buyer, multi-item
  lines, Laagat Rate auto = latest lot cost, editable; Cash Wapis Diya + Tareeqa), Purchase
  Wapsi (`purchase_return` — seller + stock check), Opening Stock (Inventory se shortcut,
  product preselect), Opening Baqaya (party dono taraf — lena/dena labels party ki type ke
  hisaab se core ki convention par; Parties se shortcut), Stock Theek Karna (`stock_adjust` —
  Stock barha/ghata, barha ho to Laagat Rate).
- **Sale form:** Discount field; Wasool Hua ke saath Tareeqa (Cash/Bank); live line:
  Kul − Discount = Bill, Wasool, Baqaya, munafa net par; line ka Rate product ke
  `saleRate` se prefill (editable).
- **Purchase form:** Discount, Tareeqa, aur **Exchange** section (toggle + multi lines;
  live net baqaya = Kul − Discount − Ada − Exchange; exchange maal ka stock check save par).
- **Wasooli:** Tareeqa; **Waade ki Tareekh** (save par `party.promiseDate` + note update —
  Wasooli List isi se chalti hai); **Bill No** (entry note mein "Bill No: X"). Baqaye se zyada
  rakam par confirm ("baqi advance ban jayega") — Wasooli aur Adaigi dono par.
- **Adad validation:** saari qty fields mein sirf poora adad (integer) > 0, warna toast
  "Adad poora likhein" — sale/purchase/return/exchange/opening/adjust sab par.
- **Wasooli List (Baqaya view):** sirf balance > 0 wale buyers; sort: waada guzra hua pehle →
  waada qareeb → sab se purana baqaya. Rows: baqaya, waade ki badge (guzri ho to laal
  "Waada guzar gaya — X din"), "X din se baqaya", WhatsApp reminder (GG banner ke saath;
  phone na ho to button hide). Upar aging chips 30+/60+/90+ din ke totals.
- **Aakhri Hisaab:** Period selector (Is Maheena / Pichla Maheena / Is Saal / Shuru se /
  Apni Tareekhein) — `periodSummary` se Sale, Laagat, head-wise Kharcha, Farq, Khalaas
  Munafa, Wasooli/Adaigi + band balances (Galla/Bank/Stock Value/Lena/Dena); period report
  ki Print + PDF (Roz ki Report wala design). **Product Munafa** table aur **Behtareen
  Buyers** (top 10) tables — dono `overflow-x-auto` mein (mobile par scroll, tutein nahi).
- **Bill:** Sale card par WhatsApp button (poora bill text + GG banner); print bill mein
  Discount > 0 ho to Kul/Discount/Total rows; Bill No/Date ab table layout mein.
  Purchase card ka baqaya ab net − ada − exchange. Roz ki Report mein Bank aya/gaya/kul,
  Sale/Purchase Wapsi totals aur us din ki Corrections ki tadaad.
- **Masters:** Product form mein "Sale Rate (agar tay ho)"; duplicate naam par confirm;
  Parties/Inventory mein "Band shuda bhi dikhayein" toggle + "Dobara chalu karein";
  unit labels har jagah `product.unit`; Import aur Profile Save buttons member ko hide.
- **Search:** kul hits gin kar title; pehle 60 render + note. **Offline patti:** firebase
  mode mein net band ho ya pending writes hon to header ke neeche amber patti.
  **Workspace chooser:** 1 se zyada khata mile to gate par list (naam + owner), tap se khule.
- **Login logo:** poora lockup ab transparent `logo-full.png` (border flood-fill se safed
  background hataya, andar ke cream hisse mehfooz) — safed box khatam, logo seedha cream
  background par. `LOGO_B64` init hata di gayi. sw cache v27, list mein `logo.jpg` ki jagah
  `logo-full.png`.
- **Rules:** `FIRESTORE_RULES.txt` workspace model par dobara likhi gayi (upar tafseel).
- **Responsive:** naye forms `grid-cols-2`/stack, entry grid `lg:grid-cols-6`, tables
  `overflow-x-auto` wrappers mein — mobile single-column, desktop wide, dono durust.
- **Core kami (report):** `sale_return`/`purchase_return` ki cash wapis core mein abhi
  hamesha **cash (Galla)** account par post hoti hai — form Tareeqa (Cash/Bank) field bhejta
  aur entry mein `method` save hota hai, lekin core usay istemal nahi karta. Core patch
  (parent ki manzoori se) isay theek kare ga.

## v31 — Fix Pass (2026-11-08, sw v31)

Bunny ki multi-phone testing + us ke apne design faislay par. BA_CORE ko NAHI chhera gaya
(block hash pehle jaisa: `ce0c4ce2…`).

- **Navigation — bottom nav khatam, top-left ☰ drawer (Bunny ka faisla):** neeche wali
  7-tab patti mein labels takra rahe thay ("Baqaya/Talpat" aur "Parties" ghus rahe thay,
  "Aakhri Hisaab" toot raha tha). Ab header (maroon bar) mein sab se pehle ☰ button hai;
  bayein se slide-in drawer khulta hai — upar maroon header (logo + naam + ✕), neeche 7
  sections ki vertical list (icon + poora label): Roznamcha, Khata, Inventory,
  Baqaya/Talpat, Parties, Aakhri Hisaab, Settings. Khula section maroon highlight; item
  tap → `switchView` + drawer band; backdrop ya ✕ se band. Drawer ki chaurai
  `min(260px, 80vw)`. Class hooks `.navbtn` → `.draweritem` (switchView, setup gate aur
  wiring teeno update). Setup gate par drawer mein bhi sirf Settings nazar ata hai.
- **GG branding strip — text/design bilkul waisa hi (Bunny ki hidayat: chherna nahi):**
  sirf mechanical tabdeeli — nav hatne se strip ki `bottom` position 60px → 0 (warna
  neeche khaali patti latakti) aur body ki bottom padding `pb-[124px]` → `pb-12`
  (strip 28px + safe margin). Strip ka inner markup byte-level par pehle jaisa hai.
- **Offline patti ka waqt theek:** pehle patti har cache walay snapshot par jhalak jati
  thi — fresh load par net honay ke bawajood "Net nahi hai" nazar ata tha (Bunny ke
  screenshot mein WiFi ke saath patti thi). Naya usool: patti SIRF tab jab (a) browser
  asal mein offline ho (`navigator.onLine === false`), ya (b) pending/cache wali halat
  lagatar ~6 second se zyada barqarar rahe (timer; server snapshot ate hi cancel + patti
  band). Patti ka text bilkul waisa hi.
- **Search boxes:** Khata, Inventory aur Parties ke search inputs ab Roznamcha walay
  pattern par hain — magnifier (search SVG icon) + "Search" placeholder, aik jaisi
  styling. Pehle ye bina nishaan ke khaali safed dabbe lagte thay.
- **Setup warning:** Owner Setup card ke andar numaya amber note: "Rukiye! Agar aap ki
  family ya dukaan ka khata pehle se bana hua hai to yahan NAYA khata na banayein. Khata
  malik Settings mein Khata Sharing se aap ki Gmail add kare ga — phir aap ko wahi khata
  khul jayega. Naya khata sirf tab banayein jab pehle koi khata na ho aur aap hi malik
  hon." (Wajah: testing mein 4 alag Gmails se 4 alag khate ban gaye thay — data mehfooz
  hai, lekin handover par yehi confusion sab se bara risk hai.)
- **QA:** node --check 4/4 script blocks PASS; jsdom harness 47/47 PASS (drawer ke 7
  items + data-views + labels, ☰/item/backdrop/✕ ke clicks se view badalna + drawer band
  + active class, teeno search icons/placeholders, setup warning, offline timing ke 9
  halat — cache snapshot par patti nahi, 6s+ pending par ati hai, asal offline par foran —
  canonical 155,000/29,000 + Talpat balanced, 45-entry statement 3 sheets, print
  invariants 794/1080/104px barqarar).
