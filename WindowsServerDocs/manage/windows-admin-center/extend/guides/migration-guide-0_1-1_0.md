---
title: Migrieren von Windows Admin Center SDK 0,1 bis 1,0
description: Dieses Handbuch hilft Ihnen beim Migrieren von Windows Admin Center SDK, Version 0,1 bis 1,0
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ba0e8cda35c51763b5c10b89c76e2bf07e064dfd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886471"
---
# <a name="migrate-from-windows-admin-center-sdk-01-to-10"></a>Migrieren von Windows Admin Center SDK 0,1 bis 1,0

>Gilt für: Windows Admin Center – Vorschau

Dieses Handbuch hilft Ihnen die Migration von Windows Admin Center SDK, Version 0,1 bis 1,0 zu machen.  

## <a name="1-learn-about-new-controls-with-the-dev-guide-extension"></a>1. Erfahren Sie mehr über neue Steuerelemente, mit der Dev-Guide-Erweiterung

Windows Admin Center 1902 und höher schließt die **-Entwicklerhandbuch** -Erweiterung, die Sie verwenden können, finden Sie Beispiele für Steuerelemente (einschließlich neu verfügbaren Steuerelemente) und Szenarien für die Sie beim Erstellen von eigenen Erweiterungen unterstützt.  Dev-Guide-ersetzt die **Entwicklertools** -Erweiterung aus früheren Versionen des SDK.

### <a name="use-the-dev-guide-in-windows-admin-center"></a>Verwenden Sie das Dev-Guide in Windows Admin Center

Entwicklerhandbuch wird als Windows Admin Center-Version 1902 eine Lösung zur Verfügung und höher.  Entwicklerhandbuch ist bereits installiert, aber über Einstellungen aktiviert werden muss.

**Aktivieren Sie in Windows Admin Center-Entwicklerhandbuch:**

* Öffnen Sie Windows Admin Center (Version 1902 und höher)
* Klicken Sie auf die **Einstellungen** Symbol in der oberen rechten Ecke des Fensters
* Wählen Sie die **erweitert** Registerkarte
* Klicken Sie unter *Experiment Schlüssel*, klicken Sie auf **hinzufügen**
* Geben Sie einen neuen Wert ```msft.sme.shell.devguide``` in das leere Feld, das im vorherigen Schritt erstellt wurde
* Klicken Sie auf **speichern und erneuten Laden**

**Öffnen Sie in Windows Admin Center-Entwicklerhandbuch:**

* Öffnen Sie Windows Admin Center (Version 1902 und höher)
* Klicken Sie auf die Dropdownliste in der oberen linken Ecke, um alle Typen von Projektmappen anzuzeigen.
* Wählen Sie die **Entwicklerhandbuch** Lösung 
    * Wenn Sie nicht, dass die Lösung aufgeführt sehen, stellen Sie sicher, dass Sie im Handbuch für die Entwicklung aktiviert haben (siehe Abschnitt oben) und haben wieder Windows Admin Center geladen.
* Navigieren Sie dazu eine der Registerkarten des Inhalts des Dev-Guide
    * **Landing:** Enthält Codebeispiele für *verwalten als* und *Benachrichtigung* Szenarien
    * **Steuerelemente:** Enthält Beispiele für die einzelnen verfügbaren Steuerelemente im SDK
    * **Pipes:** Enthält Beispiele für die verfügbaren Funktionen für Konverter und Formatierungsprogramm
    * **Formatvorlagen:** Enthält Beispiele für die CSS-Formatvorlagen im SDK verfügbar
    * **MsftSme:** Enthält Beispiele und Anleitungen für erweiterte Szenarien 

### <a name="browse-the-source-code-of-dev-guide-on-github"></a>Durchsuchen Sie den Quellcode auf GitHub-Entwicklerhandbuch

Können Sie durchsuchen den [Quellcode](https://github.com/Microsoft/windows-admin-center-sdk/) des Dev-Guide auf GitHub Beispiel HTML, CSS und TypeScript-Code-Beispiele zu finden sind.

## <a name="2-prepare-your-development-environment-for-the-latest-sdk"></a>2. Vorbereiten Sie Ihrer Entwicklungsumgebung für das neueste SDK

Installieren oder Aktualisieren von node.js-Version [10.15.1 LTS oder höher](https://nodejs.org/en/).

Aktualisieren Sie die Windows Admin Center-CLI auf die neueste Version:

[//]: # "Deinstallieren Sie Npm -g windows-admin-center-cli@next"

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

## <a name="3-create-a-new-project-with-the-latest-sdk"></a>3. Erstellen eines neuen Projekts mit dem aktuellen SDK

Verwenden Sie die Windows Admin Center-CLI zum Erstellen einer neuen Projekt als Ziel verwendet die ```next``` Version (1.0 SDK):

[//]: # "WAC create--Help Unternehmens "Contoso Inc."--Tool "verwalten"Foo "Works'--experimentelle Version"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

Als Nächstes wechseln Sie zu dem Ordner, der gerade erstellt haben, und erforderliche lokale Abhängigkeiten installieren, indem Sie Ausführung ```npm install ```.

## <a name="4-modify-an-existing-project-to-use-the-latest-sdk"></a>4. Ändern Sie ein vorhandenes Projekt aus, um das neueste SDK zu verwenden.

WICHTIG: Erstellen Sie eine Sicherung des Projekts, bevor Sie fortfahren.

Ändern Sie die folgende Zeile in ```package.json``` soll die ```next``` Version (1.0 SDK):

[//]: # "'@microsoft/windows-admin-center-sdk': 'experimental'"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

Führen Sie dann ```npm install``` so aktualisieren Sie Verweise im gesamten Projekt.

## <a name="5-use-the-sdk-cli-to-fix-common-migration-issues"></a>5. Verwenden Sie die SDK-CLI, um häufige Migrationsprobleme zu beheben.

WICHTIG: Erstellen Sie eine Sicherung des Projekts, bevor Sie fortfahren.

Führen Sie den folgenden CLI-Befehl aus dem Stammordner des Projekts auf das Projekt, häufige Migrationsprobleme automatisch zu beheben:

``` cmd
wac updateSeven --update
```

Mit diesem CLI-Befehl kann automatisch die folgenden Probleme eingegangen:

* Zugriffsschlüssel erneut generieren ```package-lock.json```
* Aktualisieren Sie die Dateien in der angular-kompilierungsumgebung:
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## <a name="6-use-the-sdk-cli-to-understand-common-migration-issues"></a>6. Verwenden Sie die SDK-CLI, um häufige Migrationsprobleme zu verstehen.

Im Stammordner Ihres Projekts, und führen Sie den folgenden CLI-Befehl überwachen Ihr Projekt, und suchen häufige Migrationsprobleme, die manuell behoben werden müssen:

``` cmd
wac updateSeven --audit
```

Dies findet die Instanzen der folgenden Probleme in Ihrem Projekt:

### <a name="replace-usage-of-the-following-css-classes-with-these-sme-classes"></a>Ersetzen Sie die Verwendung der folgenden CSS-Klassen mit diesen Klassen Sme:

| Alte CSS-Klasse | Neue CSS-Klasse |
| -- | -- |
| .auto-flex-size |  .sme-position-flex-auto |
| .Border und alle ersetzen |  .sme-border-inset-sm AND .sme-border-color-base-90 |
| .Border nach unten |  .SME-Rahmen-unten-Sm und .sme-border-bottom-color-base-90 |
| .border-horizontal |  .sme-border-horizontal-sm AND .sme-border-horizontal-color-base-90 |
| .Border-links |  .SME-Border-Left-Sm und .sme-border-left-color-base-90 |
| .Border rechts |  .SME-Rahmen-rechts-Sm und .sme-border-right-color-base-90 |
| .border-top |  .SME-Border-Top-Sm und .sme-border-top-color-base-90 |
| .Border-vertikal |  .sme-border-vertical-sm AND .sme-border-vertical-color-base-90 |
| .Break-Wort |  .sme-arrange-ws-wrap |
| .btn |  .SME-Tasten-Schaltfläche "OR" |
| primäre .btn |  .SME-button.sme-Schaltfläche-Primary OR.button.sme-Schaltfläche-primärer |
| .Color-dunkel |  .SME-Farbe – alt |
| .Color-light |  .sme-color-base |
| .Color hellgrau |  .sme-color-base-90 |
| .Fixed-Flex-Größe |  .sme-position-flex-none |
| .Flex-layout |  .SME-anordnen-Stack-h "oder".sme-anordnen-Stack-V |
| .Font-bold |  .sme-font-emphasis1 |
| .highlight |  .sme-background-color-yellow |
| .horizontal |  .sme-arrange-stack-h |
| Verschieben des Fensterinhalts Befehlsparameter |  .sme-position-flex-auto |
| .NoWrap |  .SME-anordnen-Stack-h "oder".sme-anordnen-Stack-V |
| .relative |  .SME-Layout-relative |
| .relative-center |  .SME-Layout-absoluten .sme-Position-center |
| .Reverse |  .SME-anordnen-Stack-rückgängig gemacht |
| .stretch-absolute |  .SME-Layout-absoluten .sme-Position-Inset-keine |
| .Stretch behoben |  Layout feste .sme .sme-Position-Inset-keine |
| .Stretch-vertikal |  .sme-position-stretch-v |
| .stretch-width |  .sme-position-stretch-h |
| .Vertical |  .sme-arrange-stack-v |
| nur für die .vertical Scrollen |  .SME-anordnen-Überlauf-ausblenden-X Sme-anordnen-Überlauf-Auto-y |
| .wrap |  .SME-anordnen-Wrapstack-h "oder".sme-anordnen-Wrapstack-V |

### <a name="replace-usage-of-the-following-components-with-these-sme-components"></a>Ersetzen Sie mit diesen Komponenten Sme Nutzung der folgenden Komponenten:

| Alte Komponente | Neue Komponente |
| -- | -- |
| .Alert |  KMU-Warnung |
| .Alert-danger |  KMU-Warnung |
| .breadCrumb |  KMU-Warnung |
| .CheckBox |  sme-form-field[type="checkbox"] |
| .ComboBox |  sme-form-field[type="select"] |
| .dashboard |  KMU-Layout-Inhalt-Zone aufgefüllt KMU-anordnen-Stack-h |
| .Details-Bereich |  sme-property-grid |
| .details-panel-container |  sme-property-grid |
| .details-tab |  KMU-Eigenschaftenraster OR KMU-pivot |
| .Details-Wrappers |  sme-property-grid |
| .Disabled |  KMU-deaktiviert |
| nicht in Ordnung-Schaltflächen | KMU-Formular-Feld |
| .form-control | KMU-Formular-Feld |
| nicht in Ordnung-Steuerelemente | KMU-Formular-Feld |
| nicht in Ordnung-Gruppe | KMU-Formular-Feld |
| .form-group-label | KMU-Formular-Feld |
| Eingabe nicht in Ordnung | KMU-Formular-Feld |
| .form-stretch | KMU-Formular-Feld |
| .Input-Datei | KMU-Formular-Feld |
| .NAV-Registerkarten |  KMU-pivot |
| .radio |  sme-form-field[type="radio"] |
| .required-clue | KMU-Formular-Feld |
| .searchbox |  sme-form-field[type="search"] |
| .Toggle-switch |  sme-form-field[type="toggle-switch"] |
| .tool-container |  KMU-Layout-Inhalt-Zone oder KMU-Layout-Inhalt-Zone aufgefüllt |

### <a name="these-css-classes-are-deprecated-and-are-no-longer-supported"></a>Diese CSS-Klassen sind veraltet und werden nicht mehr unterstützt:

| Alte Klasse | Veraltet |
| -- | -- |
| .Acceptable | (veraltet) |
| .Color-Fehler | (veraltet) |
| .color-info | (veraltet) |
| .color-success | (veraltet) |
| .Color-Warnung | (veraltet) |
| .Delete-Schaltfläche | (veraltet) |
| .details-content | (veraltet) |
| .Error-Abdeckung | (veraltet) |
| .Error-Nachricht | (veraltet) |
| .Guided-Bereich-Schaltfläche | (veraltet) |
| .header-container | (veraltet) |
| hat-Windows-Taste | (veraltet) |
| .Indent | (veraltet) |
| .Invalid | (veraltet) |
| .item-list | (veraltet) |
| .modal-scrollable | (veraltet) |
| . Multi-Abschnitt | (veraltet) |
| Befehlsparameter Aktionsleiste | (veraltet) |
| .Overflow-Ränder | (veraltet) |
| .overflow-tool | (veraltet) |
| .progress-cover | (veraltet) |
| …genau-Bereich | (veraltet) |
| .Rollup | (veraltet) |
| .rollup-status | (veraltet) |
| .Rollup-Titel | (veraltet) |
| .Rollup-Wert | (veraltet) |
| .searchbox-action-bar | (veraltet) |
| .size-h-1 | (veraltet) |
| .size-h-2 | (veraltet) |
| .size-h-3 | (veraltet) |
| .size-h-4 | (veraltet) |
| .size-h-full | (veraltet) |
| .size-h-half | (veraltet) |
| .size-v-1 | (veraltet) |
| .size-v-2 | (veraltet) |
| .size-v-3 | (veraltet) |
| .size-v-4 | (veraltet) |
| .status-icon | (veraltet) |
| .svg-16px | (veraltet) |
| .Table Einzug | (veraltet) |
| .table-sm | (veraltet) |
| .Thin | (veraltet) |
| .Tile | (veraltet) |
| .Tile-body | (veraltet) |
| .tile-content | (veraltet) |
| .Tile-Fußzeile | (veraltet) |
| .tile-header | (veraltet) |
| .Tile-layout | (veraltet) |
| .Tile-Tabelle | (veraltet) |
| .ToolBar | (veraltet) |
| Tool-weißem Zebrastreifeneffekt | (veraltet) |
| .tool-header | (veraltet) |
| Tool-Header-Feld | (veraltet) |
| Tool-Bereich | (veraltet) |
| .Usage-weißem Zebrastreifeneffekt | (veraltet) |
| .usage-bar-area | (veraltet) |
| .Usage-Leiste – Hintergrund | (veraltet) |
| .usage-bar-title | (veraltet) |
| .Usage-Balken-Wert | (veraltet) |
| .Usage-Diagramm | (veraltet) |
| .Usage-Nachricht | (veraltet) |
| .usage-message-area | (veraltet) |
| .usage-message-title | (veraltet) |
| .Warning | (veraltet) |
| .White-Bereich | (veraltet) |

## <a name="7-understand-and-resolve-issues-with-observable-objects"></a>7. Verstehen und Beheben von Problemen mit dem Observable-Objekte

### <a name="update--rxjs-function-use-for-observable-objects"></a>Update ```rxjs``` funktionieren für Observable-Objekte

Hierbei handelt es sich um eine allgemeine Funktionsnamen, die geändert wurden, gibt es möglicherweise andere in Ihrem Projekt.

* Update ```Observable.empty()``` auf ```empty()```
* Update ```Observable.of()``` auf ```of()```
* Update ```.switchMap()``` auf ```.pipe(switchMap())```
* Update ```.map()``` auf ```.pipe(map())```
* Update ```flatMap()``` auf ```mergeMap()```


### <a name="resolve-runtime-issues-with-map-and-filter-functions-on-observable-objects"></a>Beheben von Laufzeitproblemen mit ```.map()``` und ```.filter()``` Funktionen, die auf Observable-Objekte

Wenn der Compiler nicht korrekt identifizieren kann ein ```observable``` Objekttyp, ```.map()``` und ```.filter()``` Funktionen aus der ```array``` Objekt stattdessen auf das Objekt, sodass Fehler zur Laufzeit zugeordnet werden kann.  Stellen Sie sicher, dass Ihre Funktionen zurückgeben einer ```observable``` Objekt, das zur Vermeidung dieses Problems einen expliziten Datentyp angibt.

```any``` und ohne Rückgabetyp kann dazu führen, dass dieses Problem, suchen Sie nach Code dieser Muster:

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## <a name="8-resolve-other-common-issues"></a>8. Behoben Sie andere allgemeine Probleme werden

Andere häufig auftretende Probleme beheben erleichtern diese Techniken:

* Führen Sie ```ng lint --fix``` , Lint-Probleme zu beheben.
* Führen Sie ```gulp build``` wiederholt für inkrementell beheben Probleme, die ```gulp build``` können automatisch auflösen

## <a name="9-build-and-serve-your-project"></a>9. Erstellt und verarbeitet Sie Ihrem Projekt

Führen Sie die folgenden Befehle zum Erstellen und verarbeiten das Projekt mit der neuesten Version (1.0 SDK):

``` cmd
gulp build
gulp serve --port 4201
```

## <a name="10-turn-on-dark-theme-in-windows-admin-center"></a>10. Design "dunkel" in Windows Admin Center aktivieren

Um Design "dunkel" in Windows Admin Center Version 1902 und später aktivieren, gehen Sie folgendermaßen vor:

* Öffnen Sie Windows Admin Center (Version 1902 und höher)
* Klicken Sie auf die **Einstellungen** Symbol in der oberen rechten Ecke des Fensters
* Wählen Sie die **erweitert** Registerkarte
* Klicken Sie unter *Experiment Schlüssel*, klicken Sie auf **hinzufügen**
* Geben Sie einen neuen Wert ```msft.sme.shell.personalization``` in das leere Feld, das im vorherigen Schritt erstellt wurde
* Klicken Sie auf **speichern und erneuten Laden**
* Einstellungen haben nun eine neue Registerkarte **Personalisierung**.  Wählen Sie diese Registerkarte
* Änderung **Farben** zu **dunkel Modus (Vorschau)**
