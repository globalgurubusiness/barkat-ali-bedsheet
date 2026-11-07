# Barkat Ali Bed Sheet — Roznamcha Khata App

Client: **Barkat Ali Bed Sheet**, Chungi No. 11, Nasir Wali Market, Shop No. 28, Multan.
Multani bedsheet business (Khes, Dari, Kambal, Crystal, Diamond waghera, ~30+ products) ke liye
Zee-style single-file web app — lekin is business ke hisaab pattern par tailored:

**Roznamcha → Khata → Baqaya → Talpat → Aakhri Hisaab**

Brand: slate blue `#53687f` + cream `#f5efe3` (client ke logo ke rang). Naam ki spelling:
logo par "Barket Ali", Urdu bill par "Barkat Ali" hai — app mein display naam `APP_NAME`
constant (script ke sab se upar) se aik line mein badla ja sakta hai; default `Barkat Ali Bed Sheet` hai.

## Files

| File | Kya hai |
|---|---|
| `index.html` | Poori app (HTML + Tailwind CDN + vanilla JS + Firebase modular SDK 10.8.0 CDN). 1,169 lines / ~88 KB |
| `logo.jpg` | Client ka asal logo (login + header + PWA) |
| `icon-192.png`, `icon-512.png` | Logo se bane PWA icons |
| `manifest.webmanifest` | PWA manifest (install ke liye) |
| `sw.js` | Basic service worker (offline shell cache) |

## Design (locked pattern)

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
| **Wasooli (Payment Received)** | Buyer ka baqaya kam • Galla barha |
| **Adaigi (Payment Given)** | Seller ka baqaya kam • Galla ghata |
| **Kharcha (Expense)** | Kharcha head ke khate mein post • Galla ghata • Aakhri Hisaab mein kharcha |
| **Sarmaya Jama (Capital)** | Galla barha • Owner capital barha |
| **Owner ne Nikala (Drawing)** | Galla ghata • Drawing post |

Views: **Roznamcha** (roz ki summary cards: Sale / Wasooli / Kharcha / Purchase / Munafa / Galla,
date badal kar purana din, roz ki report/print) • **Khata** (saare ledger accounts, tap par
statement + print + WhatsApp par statement ka khulasa) • **Inventory** (product = kul qty +
value, kholne par lot-wise: rate, aye, bike, bache; low-stock warning) • **Baqaya + Talpat**
(Naame/Jama totals, "Talpat mil gaya" check) • **Parties** • **Aakhri Hisaab** (Sales − COGS =
Kham Munafa − Kharchay = Asal Munafa, Stock value, Galla, Capital).

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
- Seed (pehli dafa, dono modes mein): 5 products — Khes, Dari, Kambal, Crystal, Diamond
  (bina kisi price ke; owner edit/deactivate kar sakta hai) aur 5 aam kharcha heads.
- Bill print un ke asal bill jaisa: Number / Tafseel / Narkh / Rupay, phir Total, Advance,
  Baqaya, Dastakhat ki jagah.
- Backup: Settings se poora data JSON export/import.

## Firebase lagana — HO GAYA (2026-11-07)

Firebase project **barkat-ali-bed-sheet** ban gaya hai (globalgurupro@gmail.com par, free Spark plan):
Firestore production mode (nam5), Google sign-in enable, per-user rules publish, aur
`globalgurubusiness.github.io` authorized domain mein add hai. Asal `firebaseConfig`
`index.html` mein lag gayi hai (syntax dobara check: 4/4 script blocks PASS) — app ab
Demo Mode mein nahi, asal Firebase par chalegi. Neeche wale steps sirf record ke liye hain.

1. Firebase Console mein naya project banayein (alag project — Zee / GG Khata se mix nahi).
2. Web app register karke config ki 6 values `firebaseConfig` block mein paste karein
   (sirf wohi block badalna hai).
3. Authentication → Google sign-in enable karein.
4. Firestore Database banayein (production mode) aur neeche wale rules lagayein.
5. Authentication → Settings → Authorized domains mein live domain
   (masalan `globalgurubusiness.github.io`) add karein — warna Google login rukega.

Data model (per-user, bilkul alag):
`users/{uid}/parties/{id}`, `users/{uid}/products/{id}`, `users/{uid}/accounts/{id}`,
`users/{uid}/entries/{id}`, `users/{uid}/profile/main` — `onSnapshot` live sync aur
`enableIndexedDbPersistence` offline ke liye laga hai. Login: `signInWithPopup`,
popup block ho to `signInWithRedirect` fallback (reference GG Khata wala hi pattern).

### Firestore rules (suggestion)

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

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
