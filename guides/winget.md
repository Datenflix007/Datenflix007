# WinGet Guide für PowerShell

Der **Windows Package Manager (WinGet)** ist ein Kommandozeilen-Tool von Microsoft, mit dem du Software schnell über die PowerShell installieren, aktualisieren und verwalten kannst – ähnlich wie `apt`, `brew` oder `npm`.

---

## 🔧 Voraussetzungen

WinGet ist auf **Windows 10 (ab Version 1809)** und **Windows 11** meist bereits vorinstalliert.

### Prüfen, ob WinGet installiert ist

```powershell
winget --version
```

Wenn eine Versionsnummer angezeigt wird, ist alles bereit.

Falls nicht, installiere den **App Installer** aus dem Microsoft Store.

---

## 🔍 Programme suchen

Mit `winget search` findest du Pakete im offiziellen Repository.

```powershell
winget search vscode
```

Beispielausgabe:

```
Name              Id                       Version
------------------------------------------------------
Visual Studio Code Microsoft.VisualStudioCode 1.85.0
```

### Tipps

* Suche nach Namen: `winget search chrome`
* Suche nach Publisher: `winget search --source winget Microsoft`

---

## 📦 Programme installieren

```powershell
winget install Microsoft.VisualStudioCode
```

Oder mit exakter ID:

```powershell
winget install --id Microsoft.VisualStudioCode -e
```

### Nützliche Optionen

| Option                        | Bedeutung                            |
| ----------------------------- | ------------------------------------ |
| `-e`                          | Exakte Übereinstimmung der ID        |
| `--silent`                    | Installation ohne Benutzeroberfläche |
| `--accept-package-agreements` | Lizenz automatisch akzeptieren       |
| `--accept-source-agreements`  | Quellenbedingungen akzeptieren       |

Beispiel für eine stille Installation:

```powershell
winget install --id Google.Chrome -e --silent --accept-package-agreements --accept-source-agreements
```

---

## 📋 Installierte Programme anzeigen

```powershell
winget list
```

Nach bestimmtem Programm filtern:

```powershell
winget list vscode
```

---

## ⬆️ Programme aktualisieren

Alle verfügbaren Updates anzeigen:

```powershell
winget upgrade
```

Ein bestimmtes Programm aktualisieren:

```powershell
winget upgrade Microsoft.VisualStudioCode
```

Alle Programme automatisch aktualisieren:

```powershell
winget upgrade --all --silent --accept-package-agreements --accept-source-agreements
```

---

## ❌ Programme deinstallieren

```powershell
winget uninstall Microsoft.VisualStudioCode
```

Oder per ID:

```powershell
winget uninstall --id Microsoft.VisualStudioCode -e
```

---

## 📁 Paketdetails anzeigen

```powershell
winget show Microsoft.VisualStudioCode
```

Zeigt Infos wie Version, Publisher, Downloadquelle und Lizenz an.

---

## 📦 Mehrere Programme auf einmal installieren

Du kannst eine Liste von Paketen in einer JSON-Datei definieren.

### Beispiel `packages.json`

```json
{
  "$schema": "https://aka.ms/winget-packages.schema.2.0.json",
  "CreationDate": "2024-01-01T00:00:00.000Z",
  "Sources": [
    {
      "Packages": [
        { "PackageIdentifier": "Google.Chrome" },
        { "PackageIdentifier": "Microsoft.VisualStudioCode" },
        { "PackageIdentifier": "7zip.7zip" }
      ],
      "SourceDetails": {
        "Argument": "https://cdn.winget.microsoft.com/cache",
        "Identifier": "Microsoft.Winget.Source_8wekyb3d8bbwe",
        "Name": "winget",
        "Type": "Microsoft.PreIndexed.Package"
      }
    }
  ]
}
```

Installation aus Datei:

```powershell
winget import -i packages.json
```

---

## 🧹 Quellen (Sources) verwalten

Quellen anzeigen:

```powershell
winget source list
```

Quelle aktualisieren:

```powershell
winget source update
```

---

## ⚙️ Einstellungen anpassen

```powershell
winget settings
```

Öffnet die Konfigurationsdatei, in der du z.B. automatische Updates oder Telemetrie anpassen kannst.

---

## 🚀 Typische Power-User Befehle

### Alle Apps im Hintergrund updaten

```powershell
winget upgrade --all --silent --accept-package-agreements --accept-source-agreements
```

### Bestimmte Version installieren

```powershell
winget install --id Python.Python.3.11 --version 3.11.6
```

### Portable Version installieren (falls verfügbar)

```powershell
winget install --id Neovim.Neovim --scope user
```

---

## 🆘 Hilfe anzeigen

```powershell
winget --help
winget install --help
winget upgrade --help
```

---

## 🧰 Dienste & Entwicklungsumgebungen mit WinGet installieren

Hier findest du Schritt-für-Schritt-Anleitungen für häufig genutzte Dienste und Laufzeitumgebungen.

---

### 🍃 MongoDB Community Server

**1. Paket suchen**

```powershell
winget search mongodb
```

**2. Installieren**

```powershell
winget install --id MongoDB.Server -e --accept-package-agreements --accept-source-agreements
```

**3. Prüfen, ob der Dienst läuft**

```powershell
Get-Service MongoDB
```

**4. Mongo Shell starten**

```powershell
mongosh
```

---

### MariaDB Server

**1. Suchen**

```powershell
winget search mariadb
```

**2. Installieren**

```powershell
winget install --id MariaDB.Server -e --accept-package-agreements --accept-source-agreements
```

**3. Dienststatus prüfen**

```powershell
Get-Service MariaDB
```

**4. Mit Datenbank verbinden**

```powershell
mysql -u root -p
```

---

### PostgreSQL

**1. Suchen**

```powershell
winget search postgresql
```

**2. Installieren**

```powershell
winget install --id PostgreSQL.PostgreSQL -e --accept-package-agreements --accept-source-agreements
```

**3. Dienst prüfen**

```powershell
Get-Service postgresql*
```

**4. psql starten**

```powershell
psql -U postgres
```

---

### Python (mehrere Versionen verwalten)

**Verfügbare Versionen suchen**

```powershell
winget search Python.Python
```

**Python 3.12 installieren**

```powershell
winget install --id Python.Python.3.12 -e
```

**Python 3.11 zusätzlich installieren**

```powershell
winget install --id Python.Python.3.11 -e
```

**Installierte Versionen prüfen**

```powershell
py -0
```

**Bestimmte Version starten**

```powershell
py -3.11
```

---

### Node.js (LTS)

**1. Suchen**

```powershell
winget search OpenJS.NodeJS
```

**2. LTS installieren**

```powershell
winget install --id OpenJS.NodeJS.LTS -e
```

**3. Version prüfen**

```powershell
node -v
npm -v
```

---

### OpenJDK (Java)

**1. Suchen**

```powershell
winget search openjdk
```

**2. Installieren (z.B. Eclipse Temurin 17)**

```powershell
winget install --id EclipseAdoptium.Temurin.17.JDK -e
```

**3. Prüfen**

```powershell
java -version
javac -version
```


