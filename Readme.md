<div align="center">
<img src="assets/dadoit-logo-dark.png#gh-dark-mode-only" alt="DADO iT" width="300"/>
<img src="assets/dadoit-logo-light.png#gh-light-mode-only" alt="DADO iT" width="300"/>

<br/><br/>

### *Others think it. **We do it.***

<br/>

# ⚒️ APP\_FORGE

**Automated Software Packaging & Deployment**  
*for baramundi Management Suite*

<br/>

[![Version](https://img.shields.io/badge/version-2.1.0%20Anvil-C41E3A?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/DADO-iT/APP-FORGE/releases/latest)
[![Platform](https://img.shields.io/badge/Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/DADO-iT/APP-FORGE/releases/latest)
[![baramundi](https://img.shields.io/badge/baramundi-bc1.1%20%2B%20bc2.0-E8A0AB?style=for-the-badge)](https://www.baramundi.com)
[![License](https://img.shields.io/badge/License-Free-4caf7d?style=for-the-badge)](https://github.com/DADO-iT/APP-FORGE-LICENSES)

<br/>

[⬇️ **Download**](https://github.com/DADO-iT/APP-FORGE/releases/latest) &nbsp;·&nbsp; [🌐 **Website**](https://dado-it.github.io/APP-FORGE/) &nbsp;·&nbsp; [💬 **Contact**](mailto:dadoit@dadoit.net) &nbsp;·&nbsp; [🇩🇪 Deutsch](Readme_de.md)

</div>

---

## What is APP\_FORGE?

As a baramundi partner without an MSW license, automating software packaging is a real challenge. Many baramundi customers worldwide face the same problem — they use baramundi but can't afford MSW, or want to extend their existing setup with additional software.

**APP\_FORGE bridges this gap.**

From version detection to production deployment — fully automated, enterprise-grade, zero manual steps.

```
New Release → Download → Package → Deploy → Test → Approve → Production
```

---

## ✨ Features

| | Feature | Description |
|---|---|---|
| ⚡ | **Automatic Version Detection** | GitHub Releases, Direct Downloads & Watcher Folders — ETag/Last-Modified checks avoid unnecessary traffic |
| 📦 | **Zero-Touch Packaging** | Creates Software objects, jobs & variables in baramundi automatically |
| 🔐 | **Enterprise Security** | AES-256-CBC encryption · Hardware-bound licensing · OAuth Device Flow for GitHub |
| 📋 | **Full Audit Trail** | `CREATE_DATE`, `PROD_DATE`, `ETAG`, `TEST_STATUS` on every package |
| 🌐 | **Bandwidth Optimized** | HTTP HEAD before every download · Smart folder cache |
| 📬 | **Automated Reporting** | HTML reports via SMTP OnPrem or Microsoft 365 |

---

## 📦 Editions

| Feature | Community | Professional | Enterprise |
|---------|:---------:|:------------:|:----------:|
| GitHub Downloads | ✅ | ✅ | ✅ |
| Direct Downloads | ✅ | ✅ | ✅ |
| Watcher Integration | ✅ | ✅ | ✅ |
| HTML Reports | ✅ | ✅ | ✅ |
| Email Reports | ❌ | Optional | **Required** |
| Production Jobs | ❌ | Optional | **Required** |

**Community** — Perfect for getting started: Download, Deploy, Report  
**Professional** — Full flexibility with optional enterprise features  
**Enterprise** — Complete automation with validation

---

## 📋 Requirements

| Component | Requirement |
|-----------|-------------|
| **OS** | Windows 10 / Server 2016 or later |
| **baramundi** | bMS 2024 R1+ with **bc1.1 and bc2.0 API** both enabled |

> .NET Runtime & WebView2 are bundled in the installer — nothing to pre-install.

---

## ⬇️ Installation

1. Download `APP-FORGE-SETUP.exe` from [Releases](https://github.com/DADO-iT/APP-FORGE/releases/latest)
2. Run the installer — deploys all components automatically
3. Configure via **SETUP-GUI** wizard
4. Define your apps via **COMPOSER** or edit `1_APPLICATIONS.ps1` directly
5. Launch: `3_START-FORGE.ps1`

---

## 🗂️ What's Installed

| File | Description |
|------|-------------|
| `SETUP-GUI.exe` | Browser-based configuration wizard |
| `COMPOSER.exe` | Application definition tool with Chocolatey integration |
| `CORE.exe` | The packaging engine — Native AOT compiled |
| `3_START-FORGE.ps1` | Launcher — run manually or via Scheduled Task |
| `1_APPLICATIONS.ps1` | **Your** app list — edit this to add/remove applications |
| `2_INSTALL-RULES.ps1` | **Your** install rules & Watcher folder config |

---

## 📜 License

APP\_FORGE is **free of charge**.

A free license is required — simply create an issue in our [License Repository](https://github.com/DADO-iT/APP-FORGE-LICENSES) to receive yours automatically.

---

## 🗺️ Roadmap

| Version | Codename | Status |
|---------|----------|--------|
| **v2.1** | ⚒️ **Anvil** | ✅ Production |
| v2.3 | 🔨 Hammer | 🔴 In Development |
| v2.4 | 💨 Bellows | 📋 Planned |
| v2.5 | 🔧 Tongs | 📋 Planned |
| v3.0 | ⚔️ Damascus | 🏆 Major Release |

---

## 📞 Contact

**DADO iT** — *Others think it. We do it.*  
🌐 [dadoit.net](https://dadoit.net) &nbsp;·&nbsp; 📧 [dadoit@dadoit.net](mailto:dadoit@dadoit.net)

---

<div align="center">
<sub>Made with ⚒️ in Switzerland by <a href="https://dadoit.net">DADO iT</a> for the baramundi Community</sub>
</div>
