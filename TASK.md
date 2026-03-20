# Build: Kura Yangu — Kenya Voter Registration Center Locator

## Goal
Build a privacy-first, mobile-friendly static website that helps Kenyan voters (especially Gen Z) find their nearest IEBC voter registration center in seconds. Zero server-side location tracking — all processing happens in the user's browser.

## Privacy Architecture (CRITICAL)
- ALL geolocation calculation runs in JavaScript in the browser
- The server (GitHub Pages) NEVER receives the user's GPS coordinates
- Haversine formula runs client-side only
- No analytics, no tracking pixels, no external scripts (except Google Fonts optional)
- Include built-in OPSEC tip in results: "Protect your privacy: clear your browser history after finding your center"

## Site Design
Single HTML file: `index.html`

### Color Scheme — Kenyan flag inspired
- Background: #0a0a0a (near black)
- Primary accent: #006600 (Kenya green)  
- Secondary accent: #BB0000 (Kenya red)
- Text: #f0f0f0
- Card background: #141414
- Border: #1e3a1e

### Header
- Name: "Kura Yangu 🗳️" (My Vote in Swahili)
- Tagline: "Pata kituo chako cha usajili wa kupiga kura" (Find your voter registration center)
- English subtitle: "Find your nearest IEBC voter registration center in seconds."
- Small shield/lock icon with text: "🔒 Your location never leaves your device"

### Two Modes (Tab switcher)

**Mode 1: GPS Locate (default)**
- Button: "📍 Use My Location" 
- When clicked: calls browser geolocation API, then runs Haversine client-side
- Shows a spinner while computing
- Displays 3 nearest centers

**Mode 2: Browse by Area (No GPS)**  
- Three cascading dropdowns: County → Constituency
- On selection: shows that constituency's office
- Privacy note: "No location data is shared — you're selecting your area manually"

### Results Card Design
For each center show:
```
🏛️ [Constituency] Constituency Office
📍 [Office Location]
🏛️ Near: [Most Conspicuous Landmark]
🗺️ [Google Maps Search Link]
📋 Documents needed: Original National ID Card (or Passport for diaspora)
⏰ Hours: Mon-Fri 8:00 AM - 5:00 PM (confirm with IEBC)
```

Plus a share button: "Share this tool" using Web Share API

### Footer
- "Data source: IEBC — Independent Electoral and Boundaries Commission"  
- "Built by the people, for the people 🇰🇪"
- Link to iebc.or.ke
- OPSEC tip block: "🛡️ Privacy Tip: After finding your center, clear your browser history. Consider using a private/incognito window."

## Data Structure
Create a JavaScript const `CENTERS` array embedded directly in the HTML. Each entry:
```js
{
  county: "Nairobi",
  constituency: "Westlands", 
  location: "DC Compound",
  landmark: "Safaricom Centre",
  lat: -1.2636,
  lng: 36.8082,
  mapsQuery: "IEBC Westlands Constituency Office Nairobi Kenya"
}
```

## Complete Data — ALL 47 Counties, 290 Constituencies
Use the IEBC PDF data (iebc_offices.pdf in this directory) for office locations and landmarks.
For coordinates, use accurate approximate center coordinates for each constituency.

Here are the coordinates for all constituencies (use these exactly):

### Nairobi County
- Westlands: lat:-1.2636, lng:36.8082
- Dagoretti North: lat:-1.2921, lng:36.7505
- Dagoretti South: lat:-1.3205, lng:36.7498
- Langata: lat:-1.3424, lng:36.7654
- Kibra: lat:-1.3100, lng:36.7900
- Roysambu: lat:-1.2100, lng:36.8800
- Kasarani: lat:-1.2233, lng:36.8981
- Ruaraka: lat:-1.2522, lng:36.8856
- Embakasi South: lat:-1.3523, lng:36.9105
- Embakasi North: lat:-1.2703, lng:36.9302
- Embakasi Central: lat:-1.2975, lng:36.9068
- Embakasi East: lat:-1.2957, lng:36.9520
- Embakasi West: lat:-1.2997, lng:36.8895
- Makadara: lat:-1.2933, lng:36.8529
- Kamukunji: lat:-1.2833, lng:36.8471
- Starehe: lat:-1.2838, lng:36.8271
- Mathare: lat:-1.2551, lng:36.8540

### Mombasa County
- Changamwe: lat:-4.0435, lng:39.6290
- Jomvu: lat:-4.0210, lng:39.6810
- Kisauni: lat:-3.9981, lng:39.6815
- Nyali: lat:-4.0200, lng:39.7050
- Likoni: lat:-4.0850, lng:39.6650
- Mvita: lat:-4.0550, lng:39.6680

### Kilifi County
- Kilifi North: lat:-3.5300, lng:39.8500
- Kilifi South: lat:-3.6300, lng:39.8500
- Kaloleni: lat:-3.8020, lng:39.6200
- Rabai: lat:-3.9200, lng:39.5200
- Ganze: lat:-3.5000, lng:39.5500
- Malindi: lat:-3.2190, lng:40.1169
- Magarini: lat:-3.0700, lng:39.9500

### Kwale County
- Msambweni: lat:-4.4700, lng:39.4900
- Lungalunga: lat:-4.5500, lng:39.1100
- Matuga: lat:-4.1800, lng:39.4100
- Kinango: lat:-4.1400, lng:39.1500

### Tana River County
- Garsen: lat:-2.2700, lng:40.1000
- Galole: lat:-1.4700, lng:40.0300
- Bura: lat:-1.1000, lng:39.9500

### Lamu County
- Lamu East: lat:-2.0400, lng:41.0000
- Lamu West: lat:-2.1600, lng:40.9100

### Taita Taveta County
- Taveta: lat:-3.3950, lng:37.6900
- Wundanyi: lat:-3.3950, lng:38.3600
- Mwatate: lat:-3.5000, lng:38.3700
- Voi: lat:-3.3960, lng:38.5560

### Garissa County
- Garissa Township: lat:-0.4532, lng:42.0000
- Balambala: lat:-0.2500, lng:40.4500
- Lagdera: lat:0.3800, lng:39.9200
- Dadaab: lat:0.0500, lng:40.3200
- Fafi: lat:0.0000, lng:41.0000
- Ijara: lat:-0.5600, lng:41.3200

### Wajir County
- Wajir North: lat:2.2000, lng:39.8000
- Wajir East: lat:1.7500, lng:40.0600
- Tarbaj: lat:1.4900, lng:40.4000
- Wajir West: lat:1.5500, lng:39.4500
- Eldas: lat:1.8000, lng:39.6000
- Wajir South: lat:1.0100, lng:39.5000

### Mandera County
- Banissa: lat:3.7000, lng:41.3500
- Mandera West: lat:3.5000, lng:41.1500
- Mandera North: lat:4.0000, lng:41.5000
- Mandera South: lat:3.0000, lng:40.8500
- Mandera East: lat:3.9300, lng:41.8500
- Lafey: lat:3.7500, lng:41.0000

### Marsabit County
- Moyale: lat:3.5200, lng:39.0600
- North Horr: lat:3.3200, lng:37.0600
- Saku: lat:2.3400, lng:37.9900
- Laisamis: lat:1.6000, lng:37.8000

### Isiolo County
- Isiolo North: lat:0.3540, lng:37.5820
- Isiolo South: lat:0.5000, lng:38.5000

### Meru County
- Buuri: lat:0.1500, lng:37.1000
- Igembe Central: lat:0.3200, lng:37.8500
- Igembe North: lat:0.4500, lng:37.9500
- Tigania West: lat:0.1800, lng:37.6500
- Tigania East: lat:0.3000, lng:37.8000
- North Imenti: lat:0.0500, lng:37.6500
- Igembe South: lat:0.2000, lng:37.9200
- Central Imenti: lat:0.0200, lng:37.6500
- South Imenti: lat:-0.1500, lng:37.5500

### Tharaka-Nithi County
- Maara: lat:-0.3500, lng:37.8500
- Chuka/Igambang'ombe: lat:-0.3300, lng:37.6500
- Tharaka: lat:-0.1000, lng:38.0000

### Embu County
- Manyatta: lat:-0.5300, lng:37.4500
- Runyenjes: lat:-0.4200, lng:37.6500
- Mbeere South: lat:-0.6000, lng:37.7000
- Mbeere North: lat:-0.4000, lng:37.7500

### Kitui County
- Mwingi North: lat:-0.9000, lng:38.0000
- Mwingi West: lat:-1.0500, lng:38.0000
- Mwingi Central: lat:-1.1000, lng:38.0600
- Kitui West: lat:-1.2500, lng:37.8000
- Kitui Rural: lat:-1.3500, lng:37.9000
- Kitui Central: lat:-1.3700, lng:38.0100
- Kitui East: lat:-1.3000, lng:38.3000
- Kitui South: lat:-1.9000, lng:38.2000

### Machakos County
- Masinga: lat:-1.0800, lng:37.5300
- Yatta: lat:-1.1000, lng:37.4000
- Kangundo: lat:-1.2500, lng:37.3400
- Matungulu: lat:-1.2000, lng:37.4000
- Kathiani: lat:-1.3500, lng:37.2000
- Mavoko: lat:-1.4700, lng:36.9700
- Machakos Town: lat:-1.5170, lng:37.2636
- Mwala: lat:-1.5800, lng:37.5000

### Makueni County
- Mbooni: lat:-1.6700, lng:37.4000
- Kilome: lat:-1.8500, lng:37.3000
- Kaiti: lat:-1.9000, lng:37.6000
- Makueni: lat:-2.0000, lng:37.6000
- Kibwezi West: lat:-2.4200, lng:37.9800
- Kibwezi East: lat:-2.4500, lng:38.1000

### Nyandarua County
- Kinangop: lat:-0.7300, lng:36.5500
- Kipipiri: lat:-0.6600, lng:36.5900
- Ol Kalou: lat:-0.2700, lng:36.3800
- Ol Jorok: lat:-0.4500, lng:36.4500
- Ndaragwa: lat:-0.1500, lng:36.7500

### Nyeri County
- Tetu: lat:-0.4600, lng:37.0000
- Kieni: lat:-0.3000, lng:37.1500
- Mathira: lat:-0.4800, lng:37.1200
- Othaya: lat:-0.6000, lng:36.9500
- Mukurwe-Ini: lat:-0.7100, lng:36.9900
- Nyeri Town: lat:-0.4200, lng:36.9500

### Kirinyaga County
- Mwea: lat:-0.6800, lng:37.3800
- Gichugu: lat:-0.5500, lng:37.4000
- Ndia: lat:-0.5000, lng:37.5000
- Kirinyaga Central: lat:-0.5000, lng:37.2700

### Murang'a County
- Kangema: lat:-0.8000, lng:36.9000
- Mathioya: lat:-0.9000, lng:36.9500
- Kiharu: lat:-0.7200, lng:37.0000
- Kigumo: lat:-0.8500, lng:36.9000
- Maragwa: lat:-0.9700, lng:37.1500
- Kandara: lat:-1.0000, lng:37.0000
- Gatanga: lat:-1.0000, lng:37.1500

### Kiambu County
- Gatundu South: lat:-1.0200, lng:36.9700
- Gatundu North: lat:-0.9200, lng:37.0500
- Juja: lat:-1.1050, lng:37.0100
- Thika Town: lat:-1.0332, lng:37.0693
- Ruiru: lat:-1.1455, lng:36.9613
- Githunguri: lat:-1.0700, lng:36.8700
- Kiambu: lat:-1.1712, lng:36.8350
- Kiambaa: lat:-1.2100, lng:36.8100
- Kabete: lat:-1.2500, lng:36.7500
- Kikuyu: lat:-1.2500, lng:36.6800
- Limuru: lat:-1.1100, lng:36.6400
- Lari: lat:-1.0500, lng:36.7000

### Turkana County
- Turkana North: lat:4.5000, lng:35.3000
- Turkana West: lat:3.5000, lng:34.5000
- Turkana Central: lat:3.1190, lng:35.5950
- Loima: lat:2.5000, lng:35.3000
- Turkana South: lat:2.2000, lng:35.7000
- Turkana East: lat:2.8000, lng:36.3000

### West Pokot County
- Kapenguria: lat:1.2400, lng:35.1100
- Sigor: lat:1.6000, lng:35.2500
- Kacheliba: lat:1.5500, lng:34.8000
- Pokot South: lat:0.9000, lng:35.2000

### Samburu County
- Samburu West: lat:1.0800, lng:36.7000
- Samburu North: lat:1.8500, lng:36.9000
- Samburu East: lat:0.8000, lng:37.2000

### Trans Nzoia County
- Kwanza: lat:1.0200, lng:35.0000
- Endebess: lat:1.1500, lng:34.9000
- Saboti: lat:1.1000, lng:34.9800
- Kiminini: lat:1.1500, lng:35.0500
- Cherangany: lat:1.3000, lng:35.2500

### Uasin Gishu County
- Soy: lat:0.5700, lng:35.0000
- Turbo: lat:0.6200, lng:35.0400
- Moiben: lat:0.7100, lng:35.2600
- Ainabkoi: lat:0.5200, lng:35.3000
- Kapseret: lat:0.4000, lng:35.2000
- Kesses: lat:0.3200, lng:35.3500

### Elgeyo Marakwet County
- Marakwet East: lat:1.2500, lng:35.6000
- Marakwet West: lat:1.0500, lng:35.5000
- Keiyo North: lat:0.5500, lng:35.5000
- Keiyo South: lat:0.4000, lng:35.5000

### Nandi County
- Mosop: lat:0.6200, lng:35.3500
- Nandi Hills: lat:0.1000, lng:35.1700
- Emgwen: lat:0.2000, lng:35.1000
- Chesumei: lat:0.1500, lng:35.0200
- Aldai: lat:0.0300, lng:35.1700
- Tindiret: lat:-0.1500, lng:35.2200

### Baringo County
- Tiaty: lat:1.6000, lng:36.0000
- Baringo North: lat:1.3500, lng:35.9500
- Baringo Central: lat:0.5000, lng:35.7400
- Baringo South: lat:0.2500, lng:36.0000
- Mogotio: lat:0.1500, lng:35.9000
- Eldama Ravine: lat:0.0500, lng:35.7200

### Laikipia County
- Laikipia West: lat:0.0300, lng:36.3500
- Laikipia East: lat:0.1200, lng:37.0700
- Laikipia North: lat:0.5000, lng:37.0000

### Nakuru County
- Molo: lat:-0.2600, lng:35.7300
- Njoro: lat:-0.3300, lng:35.9500
- Naivasha: lat:-0.7170, lng:36.4310
- Gilgil: lat:-0.5000, lng:36.3100
- Kuresoi South: lat:-0.1500, lng:35.7000
- Kuresoi North: lat:0.0000, lng:35.6000
- Subukia: lat:0.0600, lng:36.1500
- Rongai: lat:0.2000, lng:35.8500
- Bahati: lat:-0.2000, lng:36.2500
- Nakuru Town West: lat:-0.3031, lng:36.0800
- Nakuru Town East: lat:-0.2800, lng:36.0800

### Narok County
- Kilgoris: lat:-1.0000, lng:34.9000
- Emurua Dikkir: lat:-1.1000, lng:35.5000
- Narok North: lat:-1.0850, lng:35.8710
- Narok East: lat:-1.3000, lng:36.0000
- Narok South: lat:-1.7000, lng:35.6000
- Narok West: lat:-1.3000, lng:35.5000

### Kajiado County
- Kajiado North: lat:-1.3670, lng:36.6560
- Kajiado Central: lat:-1.8540, lng:36.7763
- Kajiado East: lat:-1.6500, lng:36.9000
- Kajiado West: lat:-1.4000, lng:36.5500
- Kajiado South: lat:-2.4700, lng:37.1000

### Kericho County
- Ainamoi: lat:-0.3700, lng:35.2900
- Bureti: lat:-0.5500, lng:35.1300
- Belgut: lat:-0.4000, lng:35.4000
- Sigowet Soin: lat:-0.6000, lng:35.0500
- Kipkelion East: lat:-0.2000, lng:35.6000
- Kipkelion West: lat:-0.2500, lng:35.5500

### Bomet County
- Chepalungu: lat:-0.7000, lng:35.3500
- Bomet Central: lat:-0.7870, lng:35.3410
- Konoin: lat:-0.8500, lng:35.2000
- Bomet East: lat:-0.7500, lng:35.4000
- Sotik: lat:-0.7000, lng:35.1500

### Kakamega County
- Lugari: lat:0.5200, lng:34.9500
- Likuyani: lat:0.3800, lng:34.7000
- Malava: lat:0.4700, lng:34.8600
- Lurambi: lat:0.2800, lng:34.7400
- Navakholo: lat:0.3500, lng:34.6000
- Mumias West: lat:0.3300, lng:34.4800
- Mumias East: lat:0.3300, lng:34.5500
- Matungu: lat:0.2000, lng:34.5000
- Butere: lat:0.2000, lng:34.5000
- Khwisero: lat:0.1500, lng:34.5500
- Shinyalu: lat:0.3600, lng:34.7600
- Ikolomani: lat:0.3000, lng:34.7500

### Vihiga County
- Vihiga: lat:0.0700, lng:34.7200
- Sabatia: lat:0.1700, lng:34.6900
- Hamisi: lat:0.1000, lng:34.7600
- Luanda: lat:0.0800, lng:34.6300
- Emuhaya: lat:0.0600, lng:34.6700

### Bungoma County
- Mt. Elgon: lat:1.0000, lng:34.7000
- Sirisia: lat:0.6600, lng:34.5500
- Kabuchai: lat:0.5600, lng:34.5000
- Bumula: lat:0.5800, lng:34.4500
- Kanduyi: lat:0.5600, lng:34.5600
- Webuye East: lat:0.6100, lng:34.7700
- Webuye West: lat:0.6200, lng:34.7500
- Kimilili: lat:0.7800, lng:34.7100
- Tongaren: lat:0.5500, lng:34.7500

### Busia County
- Teso North: lat:0.4800, lng:34.2500
- Teso South: lat:0.4000, lng:34.3000
- Nambale: lat:0.3200, lng:34.4000
- Matayos: lat:0.3500, lng:34.2400
- Butula: lat:0.5200, lng:34.2200
- Funyula: lat:0.5500, lng:34.1000
- Budalangi: lat:0.1000, lng:34.1500

### Siaya County
- Ugenya: lat:0.2000, lng:34.2500
- Ugunja: lat:0.1700, lng:34.2500
- Alego Usonga: lat:0.1600, lng:34.3000
- Gem: lat:0.1000, lng:34.3000
- Bondo: lat:-0.0500, lng:34.2700
- Rarieda: lat:-0.2000, lng:34.2500

### Kisumu County
- Nyando: lat:-0.2500, lng:35.0000
- Muhoroni: lat:-0.1400, lng:35.2000
- Nyakach: lat:-0.4000, lng:34.9500
- Seme: lat:-0.1200, lng:34.6000
- Kisumu West: lat:-0.0950, lng:34.7290
- Kisumu East: lat:-0.0600, lng:34.8100
- Kisumu Central: lat:-0.1017, lng:34.7617

### Homabay County
- Kasipul: lat:-0.4500, lng:34.9500
- Kabondo Kasipul: lat:-0.4000, lng:34.7500
- Karachuonyo: lat:-0.4500, lng:34.8500
- Rangwe: lat:-0.5500, lng:34.7500
- Homa Bay Town: lat:-0.5270, lng:34.4580
- Ndhiwa: lat:-0.7000, lng:34.5000
- Suba North: lat:-0.4500, lng:34.2000
- Suba South: lat:-0.6500, lng:34.2500

### Migori County
- Rongo: lat:-1.1530, lng:34.6130
- Awendo: lat:-0.9000, lng:34.9000
- Suna East: lat:-1.0600, lng:34.4800
- Suna West: lat:-1.1000, lng:34.4000
- Uriri: lat:-0.8000, lng:34.6500
- Nyatike: lat:-0.9500, lng:34.2500
- Kuria West: lat:-1.3000, lng:34.7500
- Kuria East: lat:-1.3500, lng:34.9500

### Kisii County
- Bonchari: lat:-0.7500, lng:34.8000
- South Mugirango: lat:-0.8000, lng:34.8500
- Bomachoge Borabu: lat:-0.9000, lng:34.9000
- Bobasi: lat:-0.8500, lng:34.9500
- Bomachoge Chache: lat:-0.8500, lng:34.8500
- Nyaribari Masaba: lat:-0.6800, lng:34.8500
- Nyaribari Chache: lat:-0.6820, lng:34.7660
- Kitutu Chache North: lat:-0.7000, lng:34.7500
- Kitutu Chache South: lat:-0.7500, lng:34.7500

### Nyamira County
- Kitutu Masaba: lat:-0.5500, lng:34.9500
- West Mugirango: lat:-0.5700, lng:34.9200
- North Mugirango: lat:-0.4500, lng:34.9500
- Borabu: lat:-0.6500, lng:35.0500

## Implementation Steps

1. Create `index.html` with:
   - All CSS embedded (no external CSS files)
   - All JS embedded
   - CENTERS data array with ALL 290+ constituencies
   - Haversine function
   - GPS mode + Dropdown mode

2. Create `README.md` with usage instructions

3. Commit all files

## Important Notes
- This is a REAL civic tool — accuracy matters. Use real office locations from the IEBC data.
- The site must work on slow 3G connections — keep it lightweight (< 200KB total)
- No jQuery, no heavy frameworks — vanilla JS only
- Must be fully functional offline after first load (cache the centers data)
- The dropdowns should list all 47 counties and their constituencies
- The GPS result should show 3 nearest centers with distance in km
- Google Maps links should use a search query not coordinates (privacy: we don't want Maps to see exact coords): `https://www.google.com/maps/search/?api=1&query=IEBC+Westlands+Constituency+Office+Nairobi+Kenya`
- Mobile first — test that it looks good on 375px width

## When Done
Run: openclaw system event --text "Done: Kura Yangu website built at /home/asauce/kura-yangu — ready to deploy" --mode now
