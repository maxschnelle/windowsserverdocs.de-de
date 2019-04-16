---
title: Migrieren von Windows Admin Center SDK 0,1 und 1,0
description: Dieses Handbuch hilft Ihnen beim Migrieren von Windows Admin Center SDK Version 0,1 und 1,0
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ba0e8cda35c51763b5c10b89c76e2bf07e064dfd
ms.sourcegitcommit: 10d7606a5c2a1ddb234af597f199b6779b0058d4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2019
ms.locfileid: "9116586"
---
# Migrieren von Windows Admin Center SDK 0,1 und 1,0

>Gilt für: Windows Admin Center Vorschau

Dieses Handbuch hilft Ihnen die Migration von Windows Admin Center SDK Version 0,1 und 1,0.  

## 1. erfahren Sie mehr über neue Steuerelemente mit der Erweiterung Dev-Handbuch

Windows Admin Center Version 1902 und höher enthält die **Dev-Handbuch** -Erweiterung, die Sie verwenden können, finden Sie Beispiele für Steuerelemente (inklusive neu verfügbaren Steuerelemente) und Szenarien, in denen Sie Ihre eigene Erweiterung erstellen können.  Dev-Handbuch ersetzt die **Developer Tools** -Erweiterung von früheren Versionen des SDKS.

### Verwenden Sie die Anleitung Dev in Windows Admin Center

Dev-Handbuch ist als Windows Admin Center Version 1902 eine Lösung verfügbar und höher.  Dev-Handbuch installiert ist, aber es muss über Einstellungen aktiviert werden.

**Aktivieren Sie Dev-Handbuch im Windows Admin Center:**

* Open Windows Admin Center (Version 1902 und höher)
* Klicken Sie auf das Symbol " **Einstellungen** " in der oberen rechten Ecke des Fensters
* Wählen Sie die Registerkarte " **Erweitert** "
* Klicken Sie unter *Experiment Schlüssel*auf **Hinzufügen**
* Geben Sie einen neuen Wert ```msft.sme.shell.devguide``` in das leere Feld, die von den vorherigen Schritt erstellt wurde
* Klicken Sie auf **Speichern und Laden**

**Öffnen Sie Dev-Handbuch im Windows Admin Center:**

* Open Windows Admin Center (Version 1902 und höher)
* Klicken Sie auf die Dropdownliste in der oberen linken alle Lösungstypen anzeigen
* Wählen Sie die Projektmappe **Dev-Handbuch** 
    * Wenn die Lösung aufgeführt nicht angezeigt wird, stellen Sie sicher, dass Sie die Anleitung Dev aktiviert haben (siehe oben) und Windows Admin Center geladen haben.
* Durchsuchen Sie den Inhalt des Dev-Anleitung durch die Auswahl einer der Registerkarten
    * **Zielseite:** Enthält Codebeispiele für Szenarien *Verwalten als* und *Benachrichtigung*
    * **Steuerelemente:** Enthält Beispiele für die einzelnen verfügbaren Steuerelemente im SDK
    * **Pipes:** Enthält Beispiele für die verfügbaren Konverter und Formatierer-Funktionen
    * **Stile:** Enthält Beispiele für die CSS-Formatvorlagen im SDK
    * **MsftSme:** Enthält Beispiele und Richtlinien für erweiterte Szenarien 

### Durchsuchen Sie den Quellcode des Dev-Anleitung auf GitHub

Sie können den [Quellcode](https://github.com/Microsoft/windows-admin-center-sdk/) des Dev-Anleitung auf github herunter, um das Beispiel HTML-, CSS- und Schreibmaschine Codebeispiele finden durchsuchen.

## 2. Vorbereiten der Entwicklungsumgebung für das aktuelle SDK

Installieren oder Aktualisieren der node.js-Version [10.15.1 LTS oder höher](https://nodejs.org/en/).

Aktualisieren Sie die Windows Admin Center-CLI, auf die neueste Version:

[//]: # "Npm -g windows-admin-center-cli@next deinstallieren"

``` cmd
npm uninstall -g windows-admin-center-cli
npm install -g windows-admin-center-cli
```

Aktualisieren Sie Ihre globalen Abhängigkeiten auf diese Versionen:

``` cmd
npm install npm@6.4.1 -g
npm install @angular/cli@7.1.2 -g
npm install gulp -g
npm install typescript@3.1.6 -g
npm install tslint@5.11.0 -g
```

## 3. Erstellen eines neuen Projekts mit das aktuelle SDK

Verwenden Sie die Windows Admin Center-CLI zum Erstellen einer neuen Projekt bestimmt die ```next``` Version (SDK 1.0):

[//]: # "WAC erstellen – Unternehmen "Contoso Inc – Tool"Verwalten "Foo" funktioniert"– experimentelle Version"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

Als Nächstes ändern Sie das Verzeichnis in den Ordner, der gerade erstellt haben, und Installieren von erforderlichen lokalen Abhängigkeiten durch Ausführen von ```npm install ```.

## 4. ändern Sie ein vorhandenes Projekt zu verwenden, das aktuelle SDK

Wichtig: Erstellen einer Sicherung des Projekts, bevor Sie fortfahren.

Ändern Sie die folgende Zeile in ```package.json``` bestimmt die ```next``` Version (SDK 1.0):

[//]: # ""@microsoft/windows-admin-center-sdk": "experimentell""

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

Führen Sie ```npm install``` Verweise in Ihr Projekt aktualisieren.

## 5. verwenden Sie die SDK-CLI, Migrationsprobleme zu beheben

Wichtig: Erstellen einer Sicherung des Projekts, bevor Sie fortfahren.

Führen Sie aus dem Stammverzeichnis des Projekts den folgenden CLI-Befehl auf Ihr Projekt, automatisch Migrationsprobleme zu beheben:

``` cmd
wac updateSeven --update
```

Dieser Befehl CLI behandelt Folgendes automatisch:

* Neu generieren ```package-lock.json```
* Aktualisieren Sie die Dateien in der kompilierungsumgebung Winkel:
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## 6. verwenden Sie die SDK-CLI Migrationsprobleme verstehen

Führen Sie aus dem Stammverzeichnis des Projekts den folgenden CLI-Befehl zu Ihrem Projekt überwachen Migrationsprobleme, die manuell behandelt werden müssen:

``` cmd
wac updateSeven --audit
```

Dies findet Instanzen der folgenden Probleme in Ihrem Projekt:

### Ersetzen Sie die Verwendung der folgenden CSS-Klassen mit diesen Sme Klassen:

| Alte CSS-Klasse | Neue CSS-Klasse |
| -- | -- |
| .Auto-Flex-Größe |  .SME-Position-Flex-auto |
| Alle .border |  .SME-Rahmen-eingesetzten-Sm und .sme-Rahmen-Farbe-Basis-90 |
| .Border nach unten |  .SME-Rahmen-unten-Sm und .sme-border-bottom-color-base-90 |
| .Border-horizontal |  .SME-Rahmen-Horizontal-Sm und .sme-border-horizontal-color-base-90 |
| .Border-links |  .SME-Rahmen-links-Sm und .sme-border-left-color-base-90 |
| .Border rechts |  .SME-Rahmen-rechts-Sm und .sme-border-right-color-base-90 |
| .Border-top |  .SME-Rahmen-oben-Sm und .sme-border-top-color-base-90 |
| .Border vertikal |  .SME-Rahmen-vertikal-Sm und .sme-border-vertical-color-base-90 |
| .Break-word |  .SME-anordnen-ws-wrap |
| .btn |  .SME-Schaltfläche Schaltfläche "oder" |
| .btn primären |  .SME button.sme-Schaltfläche primären OR.button.sme-Schaltfläche-primäre |
| .Color-dunkel |  .SME-Farbe-alt |
| .Color schwachem Licht |  .SME-Farbe-base |
| .Color-hellgrau |  .SME-Farbe-Basis-90 |
| .Fixed-Flex-Größe |  .SME-Position-Flex-keine |
| .Flex-layout |  .SME-anordnen-Stapel-h oder .sme-anordnen-Stapel-V |
| .Font fett |  .SME-Schriftart-emphasis1 |
| .Highlight |  .SME-Hintergrund-Farbe-Gelb |
| .horizontal |  .SME-anordnen-Stapel-h |
| .No Bildlauf |  .SME-Position-Flex-auto |
| .NoWrap |  .SME-anordnen-Stapel-h oder .sme-anordnen-Stapel-V |
| .relative |  .SME, Layout-bezogene |
| .relative-center |  .SME-Layout-absoluten .sme-Position-center |
| .Reverse |  .SME-anordnen-Stapel-umgekehrt |
| .Stretch absoluten |  .SME Layout-absoluten .sme-Position-eingesetzten-keine |
| .Stretch fester |  .SME-Layout-behoben .sme-Position-eingesetzten-keine |
| .Stretch vertikal |  .SME-Position-Stretch-v |
| .Stretch Breite |  .SME-Position-Stretch-h |
| .Vertical |  .SME-anordnen-Stapel-v |
| .Vertical Bildlauf nur- |  .SME-anordnen-Überlauf-ausblenden-X Sme-anordnen-Überlauf-Auto-y |
| .Wrap |  .SME-anordnen-Wrapstack-h oder .sme-anordnen-Wrapstack-V |

### Ersetzen Sie die Verwendung der folgenden Komponenten mit diesen Sme Komponenten:

| Alte Komponente | Neue Komponente |
| -- | -- |
| .Alert |  SME-Warnung |
| .Alert-Gefahr |  SME-Warnung |
| .breadCrumb |  SME-Warnung |
| .CheckBox |  SME Formularfeld [Type = "Checkbox"] |
| .ComboBox |  SME Formularfeld [Type = "auswählen"] |
| .Dashboard |  SME-Layout-Content-Zone aufgefüllt Sme-anordnen-Stapel-h |
| .Details-Bereich |  SME-Eigenschaft-Raster |
| .Details-Panel-container |  SME-Eigenschaft-Raster |
| .Details + tab |  SME-Eigenschaft-Raster OR Sme-pivot |
| .Details-wrapper |  SME-Eigenschaft-Raster |
| .Disabled |  SME-deaktiviert |
| nicht in Ordnung-Schaltflächen | SME Formularfeld |
| nicht in Ordnung-Steuerelement | SME Formularfeld |
| nicht in Ordnung-Steuerelemente | SME Formularfeld |
| nicht in Ordnung-Gruppe | SME Formularfeld |
| nicht in Ordnung--Bezeichnung der Dateigruppe | SME Formularfeld |
| nicht in Ordnung-Eingabe | SME Formularfeld |
| nicht in Ordnung-stretch | SME Formularfeld |
| .Input-Datei | SME Formularfeld |
| .NAV-Registerkarten |  SME-pivot |
| .Radio |  SME Formularfeld [Type = "Radio"] |
| .Required-Hinweis | SME Formularfeld |
| .searchbox |  SME Formularfeld [Type = "Durchsuchen"] |
| .Toggle-switch |  SME Formularfeld [Type = "ein/aus-Schalter"] |
| Tool-container |  SME-Layout-Content-Zone oder Sme-Layout-Content-Zone aufgefüllt |

### Diese CSS-Klassen sind veraltet und werden nicht mehr unterstützt:

| Alte Klasse | Veraltet |
| -- | -- |
| .Acceptable | (veraltet) |
| .Color-Fehler | (veraltet) |
| .Color-Informationen | (veraltet) |
| .Color-Erfolg | (veraltet) |
| .Color-Warnung | (veraltet) |
| .Delete-Schaltfläche | (veraltet) |
| .Details-Inhalt | (veraltet) |
| .Error-Abdeckung | (veraltet) |
| .Error-Nachricht | (veraltet) |
| .Guided-Bereich-Schaltfläche | (veraltet) |
| .Header-container | (veraltet) |
| hat-win | (veraltet) |
| .Indent | (veraltet) |
| .Invalid | (veraltet) |
| .Item-Liste | (veraltet) |
| .Modal-bildlauffähigen | (veraltet) |
| . mit mehreren Abschnitt | (veraltet) |
| .No Aktionsleiste | (veraltet) |
| .Overflow-Ränder | (veraltet) |
| .Overflow-tool | (veraltet) |
| .Progress-Abdeckung | (veraltet) |
| .Right-Bereich | (veraltet) |
| .Rollup | (veraltet) |
| .Rollup-status | (veraltet) |
| .Rollup-Titel | (veraltet) |
| .Rollup-Wert | (veraltet) |
| .searchbox Aktionsleiste | (veraltet) |
| .Size-h-1 | (veraltet) |
| .Size-h-2 | (veraltet) |
| .Size-h-3 | (veraltet) |
| .Size-h-4 | (veraltet) |
| .Size-h-full | (veraltet) |
| .Size-h-Hälfte | (veraltet) |
| .Size-V-1 | (veraltet) |
| .Size-V-2 | (veraltet) |
| .Size-V-3 | (veraltet) |
| .Size-V-4 | (veraltet) |
| .Status-Symbol | (veraltet) |
| SVG-16px | (veraltet) |
| .Table Einzug | (veraltet) |
| .Table-sm | (veraltet) |
| .Thin | (veraltet) |
| .Tile | (veraltet) |
| .Tile-body | (veraltet) |
| .Tile-Inhalt | (veraltet) |
| .Tile-Fußzeile | (veraltet) |
| .Tile-header | (veraltet) |
| .Tile-layout | (veraltet) |
| .Tile-Tabelle | (veraltet) |
| .ToolBar | (veraltet) |
| Tool-Leiste | (veraltet) |
| Tool-header | (veraltet) |
| Tool-Header-box | (veraltet) |
| Tool-Bereich | (veraltet) |
| .Usage-Leiste | (veraltet) |
| .Usage der Statusleiste | (veraltet) |
| .Usage--Hintergrund | (veraltet) |
| .Usage-Leiste-Titel | (veraltet) |
| .Usage-Leiste-Wert | (veraltet) |
| .Usage-Diagramm | (veraltet) |
| .Usage-Nachricht | (veraltet) |
| .Usage-Nachricht-Bereich | (veraltet) |
| .Usage Nachrichtentitel | (veraltet) |
| .Warning | (veraltet) |
| .White-Bereich | (veraltet) |

## 7. verstehen und Behandeln von Problemen mit Observable-Objekte

### Update ```rxjs``` funktionieren für Observable-Objekte

Hierbei handelt es sich um einige allgemeine Funktionsnamen, die geändert wurden, gibt es möglicherweise andere Personen in Ihrem Projekt.

* Update ```Observable.empty()``` zu ```empty()```
* Update ```Observable.of()``` zu ```of()```
* Update ```.switchMap()``` zu ```.pipe(switchMap())```
* Update ```.map()``` zu ```.pipe(map())```
* Update ```flatMap()``` zu ```mergeMap()```


### Behandeln von Runtime-Problemen mit ```.map()``` und ```.filter()``` Funktionen auf Observable-Objekte

Wenn der Compiler nicht korrekt identifizieren kann ein ```observable``` Objekttyp, ```.map()``` und ```.filter()``` Funktionen aus der ```array``` Objekt auf das Objekt, verursacht Fehler zur Laufzeit stattdessen zugeordnet werden könnte.  Stellen Sie sicher, dass Ihre Funktionen zurückgeben einer ```observable``` -Objekt, einen explizite Datentyp, um dieses Problem zu umgehen.

```any``` kein Rückgabetyp können dieses Problem verursachen, und suchen Sie nach Code mit dieser Muster:

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## 8. andere allgemeine Probleme zu beheben

Diese Techniken helfen, andere allgemeine Probleme zu beheben:

* Führen Sie ```ng lint --fix``` , fusselfreien Probleme zu beheben.
* Führen Sie ```gulp build``` Probleme wiederholt, inkrementell zu beheben, ```gulp build``` automatisch beheben können

## 9. erstellen Sie und Ihr Projekt

Führen Sie die folgenden Befehle zum Erstellen und Ihr Projekt mit der neuesten Version (SDK 1.0):

``` cmd
gulp build
gulp serve --port 4201
```

## 10. Aktivieren Sie dunklen Design in Windows Admin Center

Um dunkle Design in Windows Admin Center Version 1902 und höher aktivieren, gehen Sie folgendermaßen vor:

* Open Windows Admin Center (Version 1902 und höher)
* Klicken Sie auf das Symbol " **Einstellungen** " in der oberen rechten Ecke des Fensters
* Wählen Sie die Registerkarte " **Erweitert** "
* Klicken Sie unter *Experiment Schlüssel*auf **Hinzufügen**
* Geben Sie einen neuen Wert ```msft.sme.shell.personalization``` in das leere Feld, die von den vorherigen Schritt erstellt wurde
* Klicken Sie auf **Speichern und Laden**
* Einstellungen verfügen jetzt über eine neue Registerkarte **Personalisierung**.  Wählen Sie diese Registerkarte
* Ändern von **Farben** in **dunklen Modus (Vorschau)**
