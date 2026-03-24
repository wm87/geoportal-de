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
- [GIS-Arbeitsumgebung](#️-gis-arbeitsumgebung)
- [Daten & Harvesting](#-daten--harvesting)
- [API](#-api)
- [Monitoring & Administration](#-monitoring--administration)
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

## 🗺️ GIS-Arbeitsumgebung

Die browserbasierte Kartenumgebung unterstützt WMS, WMTS und WFS vollständig – inklusive Capabilities-Parsing, Proxy-Betrieb und mehrerer Projektionen.

<br>

### WMS-Dienste

WMS-Dienste werden per URL eingebunden, Capabilities automatisch geparst, Legenden abgerufen und Projektionen geprüft. Das folgende Beispiel zeigt einen Digitalen Orthophoto-Dienst (DOP) des Freistaates Sachsen.

![WMS – Digitales Orthophoto Sachsen](assets/dop_wms_sn.png)

![WMS – Digitales Orthophoto Sachsen](assets/dop_wms_sn_se.png)

![WMS – Digitales Orthophoto Sachsen](assets/dop_wms_sn_se_dd.png)

<br>

### WFS Download bei großen Datenmengen

WFS-Dienste werden in drei Schritten heruntergeladen: WFS-Dienst mit Layern auswählen - Step 1. Wenn pro Layer die Feature-Anzahl einem definierten Schwellwert übersteigt, kommt ein Download-Abfrage-Dialog, wobei alle Features oder nur die des aktuellen Kartenausschnittes (Step 2) ausgewählt werden können. Danach beginnt mit Step 3 der eigentliche Download der Daten.

| Step 1: Layer auswählen | Step 2: Layer konfigurieren | Step 3: GeoJSON exportieren |
|---|---|---|
| ![WFS Layer auswählen](assets/wfs_layer_choose.png) | ![WFS Layer konfigurieren](assets/wfs_layer_choose_2.png) | ![WFS GeoJSON Download](assets/wfs_layer_download.png) |

<br>

### Ressourcen & Diensteübersicht

Der Ressourcen-Browser zeigt alle eingebundenen und verfügbaren Dienste mit Statusindikator, Diensttyp und Metadaten auf einen Blick.

![Ressourcenübersicht](assets/resources.png)

![Ressourcenübersicht](assets/wfs_layer_choose_se.png)

<br>

### Externe Dienste

Externe Dienstquellen wie WMS, WMTS, WFS können zentral eingebunden werden.

![Externe Dienste](assets/external_services.png)

<br>

### Layer-Import & Projektwiederherstellung

Komplette Layer-Setups inklusive Kartenausschnitt, Projektion und Layerkonfiguration lassen sich als JSON exportieren und jederzeit vollständig wiederherstellen – ideal für wiederkehrende Projektanforderungen.

![Layer Import](assets/import_layer.png)

![Layer Import](assets/dtk_wms_sn_se.png)

<br>

### Adress- & Ortssuche

Die Volltextsuche ist über Nominatim (OpenStreetMap) integriert und deckt ganz Deutschland ab. Ergebnisse werden direkt auf der Karte verortet.

![Adresssuche](assets/search_address.png)

<br>

### Hilfe & Onboarding

Eine integrierte Hilfedokumentation unterstützt neue Nutzer beim Einstieg und erklärt alle Funktionen kontextsensitiv.

![Hilfe](assets/help.png)

![Hilfe](assets/help_se.png)

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

<br>

### CKAN-Datenkatalog

Alle geernteten Metadaten werden in CKAN persistiert und sind über eine strukturierte Oberfläche durchsuchbar und filterbar. Die Volltextsuche und räumliche Filterung werden über einen integrierten **Solr-Suchindex** bereitgestellt.

![CKAN Übersicht](assets/ckan_overview.png)

<br>

### Harvest-Verwaltung im Django Admin

Alle konfigurierten CSW-Endpunkte (Bund + Länder) sind zentral verwaltet und mit Statusanzeige versehen.

![Harvest-Quellen](assets/harvest_sources.png)

<br>

Harvesting-Jobs können über das Django Admin Dashboard ausgelöst, überwacht und protokolliert werden.

![Harvest Django Admin](assets/harvest_django_admin_view.png)

---

## 📡 API

GeoPortal-DE stellt eine vollständige REST-API bereit (JWT-gesichert). Die Dokumentation ist in zwei Formaten verfügbar.

<br>

### ReDoc

![API-Dokumentation – ReDoc](assets/redoc.png)

<br>

### Swagger UI

![API-Dokumentation – Swagger](assets/swagger.png)

---

## 🔧 Monitoring & Administration

<br>

### Backend Dashboard

Das zentrale Admin-Dashboard bietet einen Überblick über alle laufenden Dienste, Nutzer, Tasks und Systemzustände.

![Backend Dashboard](assets/backend_dashboard.png)

<br>

### Celery Flower

Alle asynchronen Tasks (Harvesting, Export, Monitoring-Checks) werden über Celery verarbeitet und sind über Flower in Echtzeit einsehbar.

![Celery Flower](assets/flower.png)

<br>

### Health Check

Der integrierte Django Health Check überwacht Datenbank, Cache und alle kritischen Systemkomponenten kontinuierlich.

![Django Health Check](assets/django_health_check.png)

<br>

### Solr Admin-Oberfläche

Der integrierte Solr-Suchindex ist über die Solr Admin UI einsehbar und ermöglicht die Überwachung von Indexstatus, Abfragen und Konfiguration.

![Solr Admin-Oberfläche](assets/solr_view.png)

<br>

### Systemstatistiken

Aggregierte System-Statistiken stehen zur Verfügung.

![Systemstatistiken](assets/system_stats.png)

---

## ⚙️ Tech Stack

| Bereich | Technologie |
|---|---|
| **Backend** | Django 5.2, Django REST Framework, PostgreSQL, PostGIS |
| **Frontend** | OpenLayers 10.8, Leaflet, JavaScript (ES6) |
| **Authentifizierung** | JWT, API Keys |
| **Caching** | Redis |
| **Suchindex** | Solr 9 (CKAN-optimiert, spatial) |
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
# ├── Solr (Suchindex für CKAN)
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