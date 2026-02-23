# DADO-DEPLOY-COORD — GitHub Pages Deployment Guide

**Erstellt:** 2026-02-23 MEZ  
**Von:** Archi (v2.1 Anvil Architekt)  
**Für:** Alle Claude-Instanzen (Archi, Trevor/Hammer, zukünftige Chats)  
**Status:** ✅ PRODUKTIV — https://dado-it.github.io/APP-FORGE/ ist live

---

## 🎯 ZWECK DIESES DOKUMENTS

Dieses Dokument beschreibt **vollständig und reproduzierbar** wie die öffentliche GitHub Pages Landing Page für APP_FORGE erstellt, konfiguriert und deployed wurde. Jede Claude-Instanz die dieses Dokument liest kann:

1. Eine identische oder ähnliche Seite für andere Releases/Versionen erstellen
2. Die bestehende Seite korrekt updaten
3. Trevor's Hammer-Release genauso verpacken

---

## 📁 REPO-STRUKTUR (DADO-iT/APP-FORGE)

```
DADO-iT/APP-FORGE/          ← Public Repo (Customer-facing)
├── index.html              ← GitHub Pages Landing Page (MAIN FILE)
├── Readme.md               ← README Englisch
├── Readme_de.md            ← README Deutsch
└── assets/
    ├── dadoit-logo-dark.png   ← Logo für Dark Mode (weisse Linien, transparent)
    ├── dadoit-logo-light.png  ← Logo für Light Mode (schwarze Linien, transparent)
    ├── favicon.ico            ← Browser Tab Icon (app.ico aus installer/assets/)
    └── favicon.png            ← Fallback PNG Icon
```

---

## 🔐 GITHUB AUTH — DEVICE FLOW

**Client ID:** `Ov23liovxvzaMzwE141W`  
**Scope:** `repo`  
**Token:** NIE persistent speichern!

```bash
# Schritt 1: Device Code anfordern
curl -s -X POST https://github.com/login/device/code \
  -H "Accept: application/json" \
  -d "client_id=Ov23liovxvzaMzwE141W&scope=repo"
# → user_code: XXXX-XXXX → User gibt ein auf https://github.com/login/device

# Schritt 2: Token pollen (nach User-Bestätigung)
curl -s -X POST https://github.com/login/oauth/access_token \
  -H "Accept: application/json" \
  -d "client_id=Ov23liovxvzaMzwE141W&device_code=DEVICE_CODE&grant_type=urn:ietf:params:oauth:grant-type:device_code"
# → access_token: gho_...
```

---

## 🚀 GITHUB PAGES AKTIVIEREN

```bash
TOKEN="gho_..."

# Aktivieren (nur einmalig nötig)
curl -s -X POST \
  -H "Authorization: token $TOKEN" \
  -H "Accept: application/vnd.github+json" \
  "https://api.github.com/repos/DADO-iT/APP-FORGE/pages" \
  -d '{"source": {"branch": "main", "path": "/"}}'

# Status prüfen
curl -s -H "Authorization: token $TOKEN" \
  "https://api.github.com/repos/DADO-iT/APP-FORGE/pages" \
  | python3 -c "import json,sys; d=json.load(sys.stdin); print(d.get('html_url'), d.get('status'))"
```

**URL:** https://dado-it.github.io/APP-FORGE/

---

## 📤 FILE UPLOAD — PYTHON METHODE (empfohlen für grosse Files)

```python
import base64, json, urllib.request

TOKEN = "gho_..."

def get_sha(repo, path):
    req = urllib.request.Request(
        f"https://api.github.com/repos/{repo}/contents/{path}",
        headers={"Authorization": f"token {TOKEN}"}
    )
    try:
        return json.loads(urllib.request.urlopen(req).read())['sha']
    except:
        return None  # File existiert noch nicht

def upload_file(repo, path, local_path, message):
    sha = get_sha(repo, path)
    with open(local_path, 'rb') as f:
        content = base64.b64encode(f.read()).decode()
    payload = {"message": message, "content": content}
    if sha:
        payload["sha"] = sha
    req = urllib.request.Request(
        f"https://api.github.com/repos/{repo}/contents/{path}",
        data=json.dumps(payload).encode(), method="PUT",
        headers={"Authorization": f"token {TOKEN}", "Content-Type": "application/json"}
    )
    r = json.loads(urllib.request.urlopen(req).read())
    print(f"✅ {path}" if 'content' in r else f"❌ {r.get('message','')}")

def upload_text(repo, path, text_content, message):
    sha = get_sha(repo, path)
    content = base64.b64encode(text_content.encode()).decode()
    payload = {"message": message, "content": content}
    if sha:
        payload["sha"] = sha
    req = urllib.request.Request(
        f"https://api.github.com/repos/{repo}/contents/{path}",
        data=json.dumps(payload).encode(), method="PUT",
        headers={"Authorization": f"token {TOKEN}", "Content-Type": "application/json"}
    )
    r = json.loads(urllib.request.urlopen(req).read())
    print(f"✅ {path}" if 'content' in r else f"❌ {r.get('message','')}")

# Beispiele:
upload_file("DADO-iT/APP-FORGE", "index.html", "/tmp/index.html", "Update landing page")
upload_file("DADO-iT/APP-FORGE", "assets/favicon.ico", "/tmp/app.ico", "Update favicon")
upload_text("DADO-iT/APP-FORGE", "Readme.md", readme_content, "Update README")
```

---

## 🎨 INDEX.HTML — DESIGN SYSTEM

### Technologie-Stack
- **Fonts:** Rajdhani (Headings/Logo), IBM Plex Mono (Code/Tags), Inter (Body)
- **Google Fonts:** `https://fonts.googleapis.com/css2?family=Rajdhani:wght@300;400;600;700&family=IBM+Plex+Mono:wght@400;500&family=Inter:wght@300;400;500`
- **Keine externen Frameworks** — reines HTML/CSS/JS

### Farb-Palette
```css
/* DADO iT Brand Colors */
--red:   #C41E3A;   /* Primär Crimson */
--red-d: #9A1830;   /* Hover Dunkel */
--rose:  #E8A0AB;   /* Akzent Hell */
--glow:  rgba(196,30,58,0.14);  /* Hintergrund Glow */

/* Dark Theme */
--bg:     #0C0C0E;
--bg2:    #141416;
--bg3:    #1C1C20;
--text:   #F0EDE8;
--sub:    #7A7A88;
--dim:    #3A3A44;
--border: rgba(255,255,255,0.06);

/* Light Theme */
--bg:     #F2F0EC;
--bg2:    #FFFFFF;
--bg3:    #ECEAE6;
--text:   #16161A;
--sub:    #5A5A68;
--dim:    #AAAAB8;
--border: rgba(0,0,0,0.07);
```

### DADO iT Cube SVG (Standard — überall gleich verwenden!)
```html
<!-- Klein (Nav): 32x32 -->
<svg class="cube-svg" width="32" height="32" viewBox="0 0 80 80" fill="none">
  <polygon points="40,8 72,24 72,56 40,72 8,56 8,24" stroke="var(--text)" stroke-width="2.5" fill="none"/>
  <line x1="40" y1="8"  x2="40" y2="40" stroke="var(--text)" stroke-width="2.5"/>
  <line x1="8"  y1="24" x2="40" y2="40" stroke="var(--text)" stroke-width="2.5"/>
  <line x1="72" y1="24" x2="40" y2="40" stroke="var(--text)" stroke-width="2.5"/>
  <line x1="40" y1="40" x2="40" y2="72" stroke="var(--text)" stroke-width="1.5" opacity=".3"/>
  <rect x="31" y="31" width="16" height="16" fill="#C41E3A"/>
</svg>

<!-- Mittel (Hero): 68x68 -->
<!-- Gross (Footer): 56x56 -->
<!-- Gleiche Proportionen, nur width/height ändern -->
```

⚠️ **KRITISCH:** NIEMALS `stroke="currentColor"` verwenden — erbt Blau vom Browser!  
✅ **IMMER:** `stroke="var(--text)"` oder explizite Farbe über CSS-Klasse `.cube-svg`

### Dark/Light Toggle System
```html
<!-- HTML Attribute -->
<html data-theme="dark" data-lang="en">

<!-- Logo Swap mit Theme -->
<img class="nav-logo-img dark-logo"  src="assets/dadoit-logo-dark.png"  .../>
<img class="nav-logo-img light-logo" src="assets/dadoit-logo-light.png" .../>

<!-- CSS -->
.nav-logo-img.dark-logo  { display:block }
.nav-logo-img.light-logo { display:none  }
[data-theme="light"] .nav-logo-img.dark-logo  { display:none  }
[data-theme="light"] .nav-logo-img.light-logo { display:block }

<!-- Toggle Button -->
<button class="theme-btn" id="theme-btn" onclick="toggleTheme()">🌙</button>

<!-- JS -->
function toggleTheme() {
  const html = document.documentElement;
  const isDark = html.getAttribute('data-theme') === 'dark';
  html.setAttribute('data-theme', isDark ? 'light' : 'dark');
  document.getElementById('theme-btn').textContent = isDark ? '🌙' : '☀️';
}
```

### Bilingual DE/EN System
```html
<!-- HTML Attribute -->
<html data-lang="en">

<!-- Inhalte -->
<span data-lang-en>Download Setup.exe</span>
<span data-lang-de>Setup.exe herunterladen</span>

<!-- CSS -->
[data-lang-de], [data-lang-en] { display:none }
[data-lang="de"] [data-lang-de] { display:revert }
[data-lang="en"] [data-lang-en] { display:revert }

<!-- Toggle -->
<div class="lang-toggle">
  <button class="lang-btn" onclick="setLang('de')">DE</button>
  <button class="lang-btn" onclick="setLang('en')">EN</button>
</div>

<!-- JS -->
function setLang(lang) {
  document.documentElement.setAttribute('data-lang', lang);
  document.querySelectorAll('.lang-btn').forEach(b =>
    b.classList.toggle('active', b.textContent.trim().toLowerCase() === lang)
  );
}
```

### Scroll Reveal Animation
```js
const obs = new IntersectionObserver(e =>
  e.forEach(x => { if (x.isIntersecting) x.target.classList.add('in') }),
  { threshold:.07 }
);
document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
```
```css
.reveal { opacity:0; transform:translateY(18px); transition:opacity .5s ease, transform .5s ease }
.reveal.in { opacity:1; transform:none }
```

---

## 📄 SEITENSTRUKTUR (Sektionen in Reihenfolge)

```
1. NAV          → Sticky, Cube+Wordmark, Lang-Toggle, Theme-Toggle, Download CTA
2. HERO         → Brand Block (Cube+Name+Slogan), APP_FORGE Title, Stats Strip
3. SLOGAN BAND  → Roter Banner "OTHERS THINK IT. WE DO IT."
4. FLOW         → "Fire & Forget" Workflow-Diagramm (6 Schritte)
5. FEATURES     → 6-Cell Grid (Detection, Packaging, Security, Audit, BW, Reporting)
6. EDITIONS     → 3 Cards (Community, Professional, Enterprise)
7. COMPONENTS   → Table (SETUP-GUI, COMPOSER, CORE, Launcher, 2x PS1)
8. INSTALL      → Requirements + Steps 1-4
9. LICENSE      → Kostenlos + Link zu APP-FORGE-LICENSES Repo
10. ROADMAP     → v2.1 Anvil → v3.0 Damascus
11. FOOTER      → Cube SVG + Slogan + Links
```

---

## ✅ KORREKTE PRODUKT-FAKTEN (für alle Seiten verwenden!)

### Requirements
```
✅ Windows 10 / Server 2016 oder neuer
✅ baramundi bMS 2024 R1+
✅ bc1.1 UND bc2.0 API beide aktiviert
✅ .NET Runtime → bundled im Installer
✅ WebView2    → bundled im Installer
❌ PowerShell 7 → NICHT mehr nötig (alles EXE)
```

### Installierte Komponenten
```
SETUP-GUI.exe        → C# WinForms + WebView2, Konfigurations-Assistent
COMPOSER.exe         → C# WinForms + WebView2 + choco.exe, App-Definitions-Tool
CORE.exe             → Native AOT, die eigentliche Paketierungs-Engine
3_START-FORGE.ps1    → Launcher (ruft CORE.exe auf)
1_APPLICATIONS.ps1   → User editiert: App-Liste
2_INSTALL-RULES.ps1  → User editiert: Installationsregeln + Watcher
```

### Editionen
```
Community    → GitHub, Direct, Watcher, HTML Reports | KEIN Email, KEIN Prod
Professional → Alles Optional
Enterprise   → Email + Prod = Pflicht
```

### Lizenz
```
Kostenlos! Issue erstellen in: https://github.com/DADO-iT/APP-FORGE-LICENSES
```

### Roadmap
```
v2.1 ⚒️ Anvil    → ✅ PRODUCTION (Go-Live 2025-12-23)
v2.3 🔨 Hammer   → 🔴 IN DEVELOPMENT (Trevor's Version)
v2.4 💨 Bellows  → 📋 PLANNED
v2.5 🔧 Tongs    → 📋 PLANNED
v3.0 ⚔️ Damascus → 🏆 MAJOR RELEASE
```

### Kontakt
```
Website: dadoit.net       (NICHT dadoit.ch!)
Email:   dadoit@dadoit.net
GitHub:  https://github.com/DADO-iT
```

---

## 🔨 TREVOR — HAMMER DEPLOYMENT ANLEITUNG

**Für Trevor:** Wenn Hammer (v2.3) released wird, muss die Landing Page geupdated werden.

### Schritt 1: Versionsnummer updaten
```html
<!-- index.html: Hero Tagline -->
<span data-lang-en>baramundi Packaging Automation &nbsp;·&nbsp; v2.3 Hammer</span>

<!-- Badge im README -->
[![Version](https://img.shields.io/badge/version-2.3.0%20Hammer-C41E3A?...)]
```

### Schritt 2: Roadmap updaten
```html
<!-- v2.1 bleibt done, v2.3 wird done, v2.4 wird active -->
<div class="rrow done">  <!-- v2.1 Anvil -->
<div class="rrow done">  <!-- v2.3 Hammer - NEU done -->
<div class="rrow active"><!-- v2.4 Bellows - NEU active -->
```

### Schritt 3: Features/Components updaten falls nötig
```
Neue Komponenten? → comp-table erweitern
Neue Features?    → fgrid erweitern
Neue Requirements? → itop updaten
```

### Schritt 4: Upload via Python (Token via Device Flow holen!)
```python
# Gleiche Methode wie oben - upload_file() / upload_text()
# Repo: "DADO-iT/APP-FORGE"
# Path: "index.html", "Readme.md", "Readme_de.md"
```

---

## ⚠️ BEKANNTE FALLSTRICKE

### 1. Cloudflare Email Obfuscation
Wenn du die index.html über den Browser speicherst/downloadest, obfusziert Cloudflare die Email:
```html
<!-- KAPUTT (Cloudflare) -->
<a href="/cdn-cgi/l/email-protection#..."><span class="__cf_email__">[email protected]</span></a>

<!-- KORREKT -->
<a href="mailto:dadoit@dadoit.net">dadoit@dadoit.net</a>
```
→ **Fix:** Direkt aus dem GitHub Repo holen (via API), nicht aus dem Browser speichern.

### 2. Truncated Script Tag
Cloudflare kann auch das letzte `<script>` Tag abschneiden. Das Script-Ende:
```js
  const obs = new IntersectionObserver(e =>
    e.forEach(x => { if (x.isIntersecting) x.target.classList.add('in') }),
    { threshold:.07 }
  );
  document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
</script>
</body>
</html>
```

### 3. SVG Cube Farbe
```
❌ stroke="currentColor"  → erbt Blau vom Browser-Link-Style
✅ stroke="var(--text)"   → korrekt, passt sich Theme an
✅ CSS: .cube-svg polygon, .cube-svg line { stroke:var(--text) }
```

### 4. Logo PNG mit Hintergrund
Die Logo-Files müssen **transparenten Hintergrund** haben:
```
dadoit-logo-dark.png  → Weisse Linien, TRANSPARENTER Hintergrund
dadoit-logo-light.png → Schwarze Linien, TRANSPARENTER Hintergrund
```
→ Falls weisser Kasten sichtbar: Logo-Bilder durch SVG Cube + Wordmark ersetzen (wie in Nav/Hero aktuell)

### 5. ICO File Upload (gross)
`.ico` Files sind oft >100KB — curl Inline-JSON schlägt fehl:
```
❌ curl -d "{...riesiger base64...}"  → "File name too long"
✅ Python urllib.request verwenden    → kein Limit
```

---

## 📋 CHECKLISTE FÜR NEUE DEPLOYMENT

```
□ GitHub Device Flow Token geholt
□ index.html erstellt/angepasst (korrekte Fakten aus diesem Doc!)
□ Cloudflare-Artefakte entfernt (Email, Script-Truncation)
□ SVG Cubes: stroke="var(--text)" NICHT currentColor
□ assets/dadoit-logo-dark.png  vorhanden
□ assets/dadoit-logo-light.png vorhanden
□ assets/favicon.ico           vorhanden
□ GitHub Pages aktiviert (POST /pages)
□ index.html hochgeladen
□ Readme.md (EN) hochgeladen
□ Readme_de.md (DE) hochgeladen
□ Live-URL verifiziert: https://dado-it.github.io/APP-FORGE/
□ Browser-Tab Icon korrekt (Ctrl+Shift+R zum Cache leeren)
```

---

*Archi — v2.1 Anvil Architekt — APP_FORGE Schmiede* ⚒️🔥
