# 🔓 TOTPConverter

**Ein Python-Tool zum Extrahieren von TOTP-Secrets aus Google Authenticator QR-Code-Exports.**

---

## ✨ Features

| Feature | Beschreibung |
|---------|--------------|
| 🔍 **Secret-Extraktion** | Extrahiert TOTP-Secrets aus verschlüsselten Google Authenticator Migrations-Links |
| 📦 **Batch-Export** | Verarbeitet QR-Codes mit mehreren Konten gleichzeitig |
| 🔄 **Kompatibilität** | Secrets können in jede TOTP-App übertragen werden (Bitwarden, Authy, 1Password, etc.) |
| 🖥️ **CLI-Tool** | Einfache Nutzung über die Kommandozeile |
| 📷 **Pipe-Support** | Kann direkt mit QR-Scannern wie `zbarcam` verbunden werden |

---

## 🚀 Was kann ich damit machen?

- ✅ **2FA-Konten migrieren** – Von Google Authenticator zu einer anderen App wechseln
- ✅ **Secrets sichern** – Deine TOTP-Geheimnisse dokumentieren und backupen
- ✅ **QR-Codes erstellen** – Eigene QR-Codes für einzelne Konten generieren
- ✅ **Secrets testen** – Prüfen ob ein extrahiertes Secret korrekt funktioniert

---

## 📋 Voraussetzungen

```bash
pip install protobuf==3.20.*
```

> ⚠️ **Hinweis für moderne Linux-Systeme (z.B. Ubuntu 24.04+):**  
> Wenn `pip install` mit dem Fehler `externally-managed-environment` fehlschlägt, nutze das mitgelieferte virtuelle Environment:
>
> ```bash
> # Variante 1: venv aktivieren
> source otpauth_migrate/venv/bin/activate
> python3 otpauth_migrate.py "otpauth-migration://offline?data=..."
>
> # Variante 2: Direkt mit venv-Python ausführen
> ./otpauth_migrate/venv/bin/python3 otpauth_migrate.py "otpauth-migration://offline?data=..."
> ```

---

## 📱 Anleitung

### 1. QR-Code aus Google Authenticator exportieren

1. Öffne **Google Authenticator** auf deinem Gerät
2. Tippe auf das Menü (⋮) → **Konten exportieren**
3. Wähle die gewünschten Konten aus
4. Tippe auf **QR-Code anzeigen**

> ⚠️ Dieser QR-Code enthält **kein direkt lesbares Secret**, sondern einen verschlüsselten Migrations-Link.

### 2. QR-Code scannen & Link extrahieren

Nutze einen Online-Scanner, um den QR-Code zu dekodieren:

- https://scanqr.org/
- https://zxing.org/w/decode.jspx

Du erhältst einen Link wie:

```
otpauth-migration://offline?data=CmEKFL6wr6...
```

### 3. Secrets extrahieren

```bash
python3 otpauth_migrate.py "otpauth-migration://offline?data=DEIN_DATA_STRING"
```

**Beispiel-Ausgabe:**

```
Issuer: sellerportal.kaufland.de
Account: Sebastian Heckelmann
Secret: V3XU2XBPGRCTQK3U
```

### 4. Secret testen (optional)

Teste dein extrahiertes Secret unter: https://totp.danhersam.com/

### 5. QR-Code für andere Apps erstellen (optional)

Erstelle eine URL im Standard-Format:

```
otpauth://totp/ACCOUNT_NAME?secret=DEIN_SECRET&issuer=ISSUER_NAME
```

Diese URL kann mit jedem QR-Code-Generator (z.B. https://scanqr.org/) in einen scannbaren Code umgewandelt werden.

---

## 📜 Lizenz

**Frei zur Nutzung – Keine kommerzielle Verwertung!**

> Dieses Projekt steht **kostenlos zur Verfügung** und darf frei verwendet, kopiert und verändert werden.
>
> ⛔ **Der Verkauf dieses Codes oder darauf basierender Produkte ist ausdrücklich untersagt.**
>
> Bei Weiterverbreitung bitte den ursprünglichen Autor nennen.

---

Made with 🛠️ by Andre Dingfelder
