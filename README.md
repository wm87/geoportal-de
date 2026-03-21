<div align="center">

# GeoPortal-DE

**Die zentrale Plattform für professionelle Geodaten in Deutschland**

[![Enterprise Ready](https://img.shields.io/badge/Enterprise-Ready-0f4c81?style=flat-square)](https://geoportal-de.example)
[![Made in Germany](https://img.shields.io/badge/Made%20in-Germany-1a1a1a?style=flat-square)](https://geoportal-de.example)
[![GDI-DE](https://img.shields.io/badge/GDI--DE-Bund%20%2B%2016%20Länder-1e6f85?style=flat-square)](https://www.gdi-de.org)
[![OGC Compliant](https://img.shields.io/badge/OGC-Compliant-006699?style=flat-square)](https://www.ogc.org)
[![Django 5.2](https://img.shields.io/badge/Django-5.2-092E20?style=flat-square&logo=django&logoColor=white)](https://www.djangoproject.com)
[![OpenLayers](https://img.shields.io/badge/OpenLayers-10.8-1F6B75?style=flat-square)](https://openlayers.org)
[![License](https://img.shields.io/badge/Lizenz-Proprietär-6a0dad?style=flat-square)](mailto:info@geoportal-de.example)

[Demo anfragen](#-zugang--demo) · [Dokumentation](#️-tech-stack) · [Kontakt aufnehmen](#-kontakt)

---

</div>

## Überblick

GeoPortal-DE ist eine professionelle SaaS-Plattform für den strukturierten Zugriff auf die gesamte öffentliche Geodateninfrastruktur Deutschlands (GDI-DE). Statt fragmentierter Schnittstellen, instabiler Dienste und manueller Katalogressourcen erhalten Organisationen eine zentrale, hochperformante und rechtssichere Arbeitsumgebung.

Täglich aktualisierte Metadaten aus Bund und allen 16 Bundesländern, eine vollständige OGC-konforme GIS-Arbeitsumgebung im Browser sowie eine produktionsreife Enterprise-Infrastruktur mit Proxy, Monitoring und Rollenverwaltung – alles aus einer Hand.

**Geeignet für:** Behörden · Ingenieurbüros · Stadtplanung · Energieversorger

---

## Inhaltsverzeichnis

- [Features](#-features)
- [Funktionsübersicht](#-funktionsübersicht)
- [Daten & Harvesting](#-daten--harvesting)
- [Tech Stack](#️-tech-stack)
- [Lizenzmodell](#-lizenzmodell)
- [Zugang & Demo](#-zugang--demo)
- [Self-Hosting](#️-self-hosting-enterprise)
- [Roadmap](#-roadmap)
- [Kontakt](#-kontakt)
- [Rechtliches](#-rechtliches)

---

## ✦ Features

### Daten & Architektur

| Feature | Beschreibung |
|---|---|
| **Tägliches CSW-Harvesting** | Vollständige Abdeckung aller GDI-DE Kataloge inkl. CKAN-Integration |
| **Stabile Metadatenhaltung** | Keine Live-Abhängigkeit zu externen Diensten – hohe Verfügbarkeit |
| **Automatische Format-Erkennung** | Unterstützung für WMS, WMTS und WFS out-of-the-box |
| **ISO 19139 Parser** | Inkrementelle Updates via Hash-Vergleich, lxml-basiert |

### Enterprise-Infrastruktur

| Feature | Beschreibung |
|---|---|
| **CORS-Proxy** | httpx-basiert mit aktivem SSRF-Schutz |
| **Authentifizierung** | JWT + API-Key-System mit Rollenverwaltung |
| **Monitoring** | Prometheus-Metriken, Celery Flower, Ampelsystem für Dienstverfügbarkeit |
| **Logging** | Strukturierte Logs für Audit- und Betriebszwecke |

### GIS-Funktionalität

| Feature | Beschreibung |
|---|---|
| **WFS Feature-Abfrage** | Direkte Attributanzeige im sichtbaren Kartenausschnitt |
| **Dynamischer Layerbaum** | Drag & Drop, Gruppenbildung, Transparenzsteuerung |
| **Projekt Import / Export** | Vollständige Wiederherstellung von Layer-Setups inkl. Ausschnitt und Projektion |
| **PDF-Export** | Formate A0–A5, 72–300 DPI, PNG/JPEG, Gitternetz + Metadaten |

---

## 🗺 Funktionsübersicht

<details>
<summary><strong>Metadatenkatalog</strong></summary>

- Volltextsuche über Titel, Abstract und Keywords
- Filter nach Organisation und Diensttyp
- Detailansicht mit Lizenz, Gebühren und Kontaktinformationen
- One-Click Layer-Integration in die Kartenansicht

</details>

<details>
<summary><strong>Layerverwaltung</strong></summary>

- Drag & Drop Sortierung
- Individuelle Transparenzsteuerung pro Layer
- WMS-Legenden-Anzeige
- WFS-Attributanzeige und GeoJSON-Export

</details>

<details>
<summary><strong>Diensteintegration</strong></summary>

- WMS, WMTS und WFS via URL
- Capabilities Parsing mit automatischem Fallback
- WMTS TileMatrix-Erkennung je Projektion
- Proxy-Betrieb ohne CORS-Einschränkungen

</details>

<details>
<summary><strong>Kartenfunktionen</strong></summary>

- **Basemaps:** OSM, BKG, OpenTopoMap
- **Projektionen:** EPSG 3857, 4326, 25832, 25833, 31467
- Geolokalisierung, Navigation und Zoom-Werkzeuge

</details>

<details>
<summary><strong>Analyse & Export</strong></summary>

- Längen- und Flächenmessung im Kartenausschnitt
- PDF-Export (A0–A5, 72–300 DPI, PNG/JPEG)
- Gitternetz- und Metadaten-Overlay im Export

</details>

<details>
<summary><strong>Suche</strong></summary>

- Nominatim-Integration (OpenStreetMap)
- Deutschlandweite Adress- und Ortssuche

</details>

<details>
<summary><strong>Admin & Monitoring</strong></summary>

- Django Admin Dashboard
- Celery + Flower für Aufgabenverwaltung
- Prometheus-Metriken
- Strukturierte Betriebsprotokolle

</details>

---

## 🔄 Daten & Harvesting

GeoPortal-DE betreibt ein vollständig automatisiertes Harvesting-System, das täglich alle relevanten GDI-DE Kataloge synchronisiert.

```
GDI-DE Kataloge (Bund + 16 Länder)
        │
        ▼
  CSW-Harvesting (täglich)
        │
        ├─► ISO 19139 Parser (lxml)
        │         │
        │         ▼
        │   Hash-Vergleich → Inkrementelles Update
        │
        ├─► Automatische Ressourcen-Erkennung
        │         │
        │         └─► WMS / WMTS / WFS Klassifikation
        │
        └─► CKAN Push
                  │
                  └─► Lizenz-Mapping
```

---

## ⚙️ Tech Stack

| Bereich | Technologie |
|---|---|
| **Backend** | Django 5.2, Django REST Framework, PostgreSQL, PostGIS |
| **Frontend** | OpenLayers 10.8, Leaflet, JavaScript (ES6) |
| **Authentifizierung** | JWT, API Keys |
| **Caching** | Redis |
| **Task Queue** | Celery |
| **Proxy** | httpx + SSRF-Schutz |
| **Deployment** | Docker Compose, Nginx |
| **Monitoring** | Prometheus, Celery Flower |

---

## 💰 Lizenzmodell

> Alle Preise zzgl. gesetzlicher MwSt. Jährliche Abrechnung auf Anfrage möglich.

### Basic — 999 €&thinsp;/&thinsp;Monat

Für kleinere Teams mit standardisierten Anforderungen.

- Bis zu **5 Nutzer**
- Standard PDF-Export
- E-Mail-Support (Reaktionszeit < 24 h)

---

### Professional — 1.499 €&thinsp;/&thinsp;Monat

Für Organisationen mit erweiterten Anforderungen.

- **Unbegrenzte Nutzer**
- Voller PDF-Export (alle Formate und Auflösungen)
- **API-Zugriff** (REST + JWT)
- Priority Support (Reaktionszeit < 4 h)

---

### Enterprise — Individuell

Für Behörden, Stadtwerke und Unternehmen mit hohen Verfügbarkeits- und Datenschutzanforderungen.

- **On-Premise Deployment** (vollständiger Docker-Stack)
- Custom Features nach Anforderung
- **SLA & 24/7 Support**
- LDAP / Active Directory Integration
- Mandantenfähigkeit

> Für ein individuelles Angebot: [info@geoportal-de.example](mailto:info@geoportal-de.example)

---

## 🚀 Zugang & Demo

GeoPortal-DE wird nicht als anonymer Self-Service angeboten. Der Zugang erfolgt strukturiert, um eine optimale Einrichtung für den jeweiligen Einsatzzweck sicherzustellen.

```
1. Kontaktaufnahme
   info@geoportal-de.example

2. Kurze Abstimmung
   Einsatzzweck, Team-Größe, technische Anforderungen

3. Demo-Zugang oder Live-Demo-Termin
   Angepasst an Ihren konkreten Use Case
```

---

## 🛠️ Self-Hosting (Enterprise)

GeoPortal-DE kann vollständig On-Premise betrieben werden. Der Enterprise-Stack umfasst:

```bash
# Stack starten
docker compose up -d

# Enthaltene Services
# ├── Django (Applikationsserver)
# ├── PostgreSQL + PostGIS (Datenbank)
# ├── Redis (Cache & Message Broker)
# ├── Celery (Task Queue)
# ├── CKAN (Datenkatalog)
# └── Nginx (Reverse Proxy)
```

Im Lieferumfang enthalten:

- Setup-Skripte und Konfigurationsdokumentation
- Backup- & Restore-Prozeduren
- Anpassbare Umgebungsvariablen
- Monitoring-Integration (Prometheus + Grafana, optional)

---

## 🧭 Roadmap

| Status | Feature |
|---|---|
| 🔲 Geplant | **GeoAtom-Explorer** — Integration in die Django-Umgebung |
| 🔲 Geplant | **Metadateneditor** — Create / Update / Qualitätssicherung |
| 🔲 Geplant | **Erweiterte Testabdeckung** — Unit-, Integrations- und Lasttests |
| 🔲 Geplant | **Grafana + Prometheus Dashboards** — Alerts, SLA-Metriken, Betriebsübersicht |

---

## 📸 Screenshots

| Gesamtübersicht | WMS-Integration | WFS Feature-Abfrage |
|---|---|---|
| ![Übersicht](assets/overview.png) | ![BORIS WMS](assets/boris_wms.png) | ![BORIS WFS](assets/boris_wfs.png) |

| WMTS-Dienst | Projektimport |
|---|---|
| ![WMTS](assets/wmts.png) | ![Layer Import](assets/layer-import.png) |

---

## 📞 Kontakt

**wm87 GbR**
Musterstraße 123 · 12345 Musterstadt · Deutschland

| Kanal | Adresse |
|---|---|
| E-Mail | [info@geoportal-de.example](mailto:info@geoportal-de.example) |
| Telefon | +49 123 4567890 |

---

## 📄 Rechtliches

Geodaten unterliegen den Lizenzbedingungen der jeweiligen Anbieter (Bund, Länder, BKG, OpenStreetMap Contributors). GeoPortal-DE übernimmt keine Haftung für die Verfügbarkeit, Richtigkeit oder Aktualität externer Dienste.

---

<div align="center">

**GeoPortal-DE** — Deutschlands Geodaten. Zentral. Sicher. Unternehmensbereit.

[info@geoportal-de.example](mailto:info@geoportal-de.example) · [geoportal-de.example](https://geoportal-de.example) · © 2025 wm87 GbR

</div>