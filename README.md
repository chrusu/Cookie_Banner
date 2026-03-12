# 🍪 Cookie-Banner Konfigurator

Ein visueller Konfigurator, der ein DSGVO-konformes Cookie-Banner als **selbstständiges `<script>`-Tag** generiert – ohne externe Abhängigkeiten, ohne Build-Step.

## Was ist das?

Eine Single-Page-App (eine einzige `index.html`), mit der du ein Cookie-Banner komplett visuell konfigurierst:

- **Farben** für Banner, Primary-Button und Secondary-Button
- **Border-Radius** per Slider
- **Texte** (Banner-Text, Link-Text, Button-Labels)
- **Google Analytics** IDs (optional, mehrere möglich)
- **Live-Preview** – das Banner reagiert sofort auf jede Änderung
- **Copy-to-Clipboard** – das fertige `<script>` mit einem Klick kopieren

Das generierte Script ist ein vollständiges, dependency-freies IIFE, das direkt in den `<head>` einer Website eingebettet werden kann (z. B. via [WPCode](https://wpcode.com/) in WordPress).

## Features des generierten Banners

| Feature | Details |
|---|---|
| **Cookie-basierter Consent** | Speichert die Entscheidung als `cookie_consent`-Cookie (365 Tage) |
| **Google Analytics Integration** | Lädt GA4 erst nach Zustimmung, blockiert es bei Ablehnung |
| **Consent-Event** | Feuert `cookieConsentChanged` auf `document` für Plugin-Integration |
| **Globale API** | `window.cookieConsentGranted()` – jederzeit abfragbar |
| **localStorage Guard** | Optionaler Guard, der `localStorage` global blockiert bis Consent vorliegt |
| **Cookie-Button** | Nach Entscheidung erscheint ein kleiner Cookie-Button zum erneuten Öffnen |
| **Responsive** | Mobile-optimiertes Layout (stacked auf kleinen Screens) |
| **Accessible** | `role="dialog"`, `aria-label`, Keyboard-Support |
| **Zero Dependencies** | Reines Vanilla JS, kein Framework nötig |

## Schnellstart

1. `index.html` im Browser öffnen
2. Farben, Texte und GA-IDs konfigurieren
3. Das generierte Script aus dem Preview kopieren
4. In den `<head>` der Zielseite einfügen (z. B. als WPCode-Snippet)

## Projektstruktur

```
Cookie_Banner/
├── index.html            # Konfigurator (alles in einer Datei)
├── assets/
│   ├── Favicon.png
│   ├── Logo5.png
│   └── Webclip.png
├── vendor/
│   ├── coloris.min.css   # Color-Picker (Coloris)
│   └── coloris.min.js
└── README.md
```

## API des generierten Banners

| API | Rückgabe | Beschreibung |
|---|---|---|
| `window.cookieConsentGranted()` | `true` / `false` | Prüft, ob der Benutzer Cookies akzeptiert hat |
| `window.COOKIE_CONSENT_KEY` | `"cookie_consent"` | Name des Consent-Cookies |
| `cookieConsentChanged` Event | `e.detail.consent` | Wird bei jeder Consent-Änderung gefeuert |

### Consent in eigenem Code prüfen

```js
if (window.cookieConsentGranted && window.cookieConsentGranted()) {
    localStorage.setItem('mein_key', wert);
}
```

### Auf Consent-Änderung reagieren

```js
document.addEventListener('cookieConsentChanged', function (e) {
    if (e.detail.consent) {
        // Benutzer hat akzeptiert
    } else {
        // Benutzer hat abgelehnt
    }
});
```

## Technologie

- **Vanilla JS** – kein Framework, kein Build-Step
- **Coloris** – leichtgewichtiger Color-Picker ([GitHub](https://github.com/mdbassit/Coloris))
- **Lexend Exa** – Google Font für die UI
- Einstellungen werden in `localStorage` persistiert

## Autor

**Hinderling Internet Handwerk**