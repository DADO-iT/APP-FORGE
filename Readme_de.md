<div align="center">
<img src="assets/dadoit-logo-dark.png#gh-dark-mode-only" alt="DADO iT" width="300"/>
<img src="assets/dadoit-logo-light.png#gh-light-mode-only" alt="DADO iT" width="300"/>

<br/><br/>

### *Others think it. **We do it.***

<br/>

# ⚒️ APP\_FORGE

**Automatisierte Software-Paketierung & Deployment**  
*für baramundi Management Suite*

<br/>

[![Version](https://img.shields.io/badge/version-2.1.0%20Anvil-C41E3A?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/DADO-iT/APP-FORGE/releases/latest)
[![Platform](https://img.shields.io/badge/Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/DADO-iT/APP-FORGE/releases/latest)
[![baramundi](https://img.shields.io/badge/baramundi-bc1.1%20%2B%20bc2.0-E8A0AB?style=for-the-badge)](https://www.baramundi.com)
[![License](https://img.shields.io/badge/Lizenz-Kostenlos-4caf7d?style=for-the-badge)](https://github.com/DADO-iT/APP-FORGE-LICENSES)

<br/>

[⬇️ **Download**](https://github.com/DADO-iT/APP-FORGE/releases/latest) &nbsp;·&nbsp; [🌐 **Website**](https://dado-it.github.io/APP-FORGE/) &nbsp;·&nbsp; [💬 **Kontakt**](mailto:dadoit@dadoit.net) &nbsp;·&nbsp; [🇬🇧 English](Readme.md)

</div>

---

## Was ist APP\_FORGE?

Als baramundi-Partner ohne MSW-Lizenz ist die Automatisierung der Software-Paketierung eine echte Herausforderung. Viele baramundi-Kunden weltweit kennen dieses Problem — sie nutzen baramundi, können sich aber MSW nicht leisten oder möchten ihre bestehende Installation ergänzen.

**APP\_FORGE schliesst diese Lücke.**

Von der Versionserkennung bis zur Produktionsfreigabe — vollautomatisch, enterprise-tauglich, keine manuellen Schritte.

```
Neue Version → Download → Paket → Deploy → Test → Freigabe → Produktion
```

---

## ✨ Features

| | Feature | Beschreibung |
|---|---|---|
| ⚡ | **Automatische Versionserkennung** | GitHub Releases, Direkte Downloads & Watcher-Ordner — ETag/Last-Modified verhindert unnötigen Traffic |
| 📦 | **Vollautomatische Paketierung** | Erstellt Software-Objekte, Jobs & Variablen in baramundi automatisch |
| 🔐 | **Enterprise-Sicherheit** | AES-256-CBC Verschlüsselung · Hardware-gebundene Lizenz · OAuth Device Flow für GitHub |
| 📋 | **Vollständiger Audit-Trail** | `CREATE_DATE`, `PROD_DATE`, `ETAG`, `TEST_STATUS` auf jedem Paket |
| 🌐 | **Bandbreitenoptimiert** | HTTP HEAD vor jedem Download · Smart Folder-Cache |
| 📬 | **Automatisches Reporting** | HTML-Reports per SMTP oder Microsoft 365 |

---

## 📦 Editionen

| Feature | Community | Professional | Enterprise |
|---------|:---------:|:------------:|:----------:|
| GitHub Downloads | ✅ | ✅ | ✅ |
| Direkte Downloads | ✅ | ✅ | ✅ |
| Watcher Integration | ✅ | ✅ | ✅ |
| HTML Reports | ✅ | ✅ | ✅ |
| Email Reports | ❌ | Optional | **Pflicht** |
| Produktions-Jobs | ❌ | Optional | **Pflicht** |

**Community** — Ideal für den Einstieg: Download, Deploy, Report  
**Professional** — Volle Flexibilität mit optionalen Enterprise-Features  
**Enterprise** — Vollständige Automatisierung mit Validierung

---

## 📋 Voraussetzungen

| Komponente | Anforderung |
|------------|-------------|
| **OS** | Windows 10 / Server 2016 oder neuer |
| **baramundi** | bMS 2024 R1+ mit **bc1.1 und bc2.0 API** beide aktiviert |

> .NET Runtime & WebView2 sind im Installer enthalten — nichts vorab zu installieren.

---

## ⬇️ Installation

1. `APP-FORGE-SETUP.exe` von [Releases](https://github.com/DADO-iT/APP-FORGE/releases/latest) herunterladen
2. Installer ausführen — alle Komponenten werden automatisch installiert
3. Konfiguration über den **SETUP-GUI** Assistenten
4. Apps via **COMPOSER** definieren oder `1_APPLICATIONS.ps1` direkt bearbeiten
5. Starten: `3_START-FORGE.ps1`

---

## 🗂️ Was wird installiert

| Datei | Beschreibung |
|-------|-------------|
| `SETUP-GUI.exe` | Browser-basierter Konfigurations-Assistent |
| `COMPOSER.exe` | App-Definitions-Tool mit Chocolatey-Integration |
| `CORE.exe` | Die Paketierungs-Engine — Native AOT kompiliert |
| `3_START-FORGE.ps1` | Launcher — manuell oder per Scheduled Task |
| `1_APPLICATIONS.ps1` | **Deine** App-Liste — hier Apps hinzufügen/entfernen |
| `2_INSTALL-RULES.ps1` | **Deine** Installationsregeln & Watcher-Konfiguration |

---

## 📜 Lizenz

APP\_FORGE ist **kostenlos**.

Eine kostenlose Lizenz wird benötigt — erstelle einfach ein Issue in unserem [Lizenz-Repository](https://github.com/DADO-iT/APP-FORGE-LICENSES) und du erhältst sie automatisch.

---

## 🗺️ Roadmap

| Version | Codename | Status |
|---------|----------|--------|
| **v2.1** | ⚒️ **Anvil** | ✅ Produktion |
| v2.3 | 🔨 Hammer | 🔴 In Entwicklung |
| v2.4 | 💨 Bellows | 📋 Geplant |
| v2.5 | 🔧 Tongs | 📋 Geplant |
| v3.0 | ⚔️ Damascus | 🏆 Major Release |

---

## 📞 Kontakt

**DADO iT** — *Others think it. We do it.*  
🌐 [dadoit.net](https://dadoit.net) &nbsp;·&nbsp; 📧 [dadoit@dadoit.net](mailto:dadoit@dadoit.net)

---

<div align="center">
<sub>Mit ⚒️ in der Schweiz entwickelt von <a href="https://dadoit.net">DADO iT</a> für die baramundi Community</sub>
</div>
