---
title: Migrieren vom Windows Admin Center SDK 0,1 zu 1,0
description: Dieser Leitfaden unterstützt Sie bei der Migration von Windows Admin Center SDK, Version 0,1, zu 1,0.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c52870178e7caff0abc8ddcccc62966d637dd3c9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357060"
---
# <a name="migrate-from-windows-admin-center-sdk-01-to-10"></a>Migrieren vom Windows Admin Center SDK 0,1 zu 1,0

>Gilt für: Windows Admin Center (Vorschau)

Dieser Leitfaden unterstützt Sie bei der Migration von Windows Admin Center SDK, Version 0,1, zu 1,0.  

## <a name="1-learn-about-new-controls-with-the-dev-guide-extension"></a>1. erfahren Sie mehr über neue Steuerelemente mit der Entwicklungs Leit Faden Erweiterung

Windows Admin Center, Version 1902 und höher, enthält die Entwickler **Handbuch** -Erweiterung, die Sie verwenden können, um Beispiele für Steuerelemente (einschließlich neu verfügbarer Steuerelemente) und Szenarios zu finden, die Sie beim Erstellen Ihrer eigenen Erweiterung unterstützen.  Dev Guide ersetzt die **Entwicklertools** Erweiterung aus früheren Versionen des SDK.

### <a name="use-the-dev-guide-in-windows-admin-center"></a>Verwenden des dev-Handbuchs im Windows Admin Center

Dev Guide ist als Lösung in Windows Admin Center, Version 1902 und höher, verfügbar.  Entwicklerhandbuch ist vorinstalliert, muss jedoch über Einstellungen aktiviert werden.

**Entwicklerhandbuch in Windows Admin Center aktivieren:**

* Öffnen Sie das Windows Admin Center (Version 1902 und höher).
* Klicken Sie in der oberen rechten Ecke des Fensters auf das Symbol " **Einstellungen** ".
* Registerkarte " **erweitert** " auswählen
* Klicken Sie unter *Experiment Schlüssel*auf **Hinzufügen** .
* Geben Sie einen neuen Wert ```msft.sme.shell.devguide``` in das leere Feld ein, das im vorherigen Schritt erstellt wurde.
* Klicken Sie auf **Speichern und erneut laden**

**Entwicklerhandbuch in Windows Admin Center öffnen:**

* Öffnen Sie das Windows Admin Center (Version 1902 und höher).
* Klicken Sie oben links auf das Dropdown Feld, um alle Projektmappentypen anzuzeigen.
* Entwicklungs **Leit Faden** Lösung auswählen 
    * Wenn die Lösung nicht aufgelistet wird, stellen Sie sicher, dass Sie das Entwicklungs Handbuch aktiviert haben (siehe Abschnitt oben), und haben Sie das Windows Admin Center neu geladen.
* Durchsuchen Sie den Inhalt des dev-Handbuchs, indem Sie eine der Registerkarten auswählen.
    * **Landing:** Enthält Codebeispiele für die *Verwaltung von As* -und *Benachrichtigungs* Szenarios
    * Steuer **Elemente:** Enthält Beispiele für jedes verfügbare Steuerelement im SDK
    * **Pipes:** Enthält Beispiele für verfügbare Konverter-und Formatierungsfunktionen.
    * **Stile:** Enthält Beispiele für CSS-Stile, die im SDK verfügbar sind.
    * **Msftsme:** Enthält Beispiele und Anleitungen für erweiterte Szenarien 

### <a name="browse-the-source-code-of-dev-guide-on-github"></a>Durchsuchen Sie den Quellcode des dev-Handbuchs auf GitHub.

Sie können den [Quellcode](https://github.com/Microsoft/windows-admin-center-sdk/) des dev-Handbuchs auf GitHub durchsuchen, um Beispiele für HTML-, CSS-und typescript-Codebeispiele zu finden.

## <a name="2-prepare-your-development-environment-for-the-latest-sdk"></a>2. Vorbereiten der Entwicklungsumgebung für das neueste SDK

Installieren oder aktualisieren Sie die Node. js-Version [10.15.1 LTS oder](https://nodejs.org/en/)höher.

Aktualisieren Sie die Windows Admin Center-CLI auf die neueste Version:

[//]: # "NPM-Deinstallation-g windows-admin-center-cli@next"

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

## <a name="3-create-a-new-project-with-the-latest-sdk"></a>3. Erstellen eines neuen Projekts mit dem neuesten SDK

Verwenden Sie die Windows Admin Center-CLI, um ein neues Projekt zu erstellen, das auf die ```next``` Version (SDK 1,0) ausgerichtet ist:

[//]: # "WAC Create--Company ' Configuration Manager '--Tool ' manage foo Works '--Version experimentell"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

Wechseln Sie als nächstes das Verzeichnis in den soeben erstellten Ordner, und installieren Sie die erforderlichen lokalen Abhängigkeiten, indem Sie ```npm install ```ausführen.

## <a name="4-modify-an-existing-project-to-use-the-latest-sdk"></a>4. Ändern eines vorhandenen Projekts für die Verwendung des neuesten SDK

Wichtig: Erstellen Sie eine Sicherung Ihres Projekts, bevor Sie fortfahren.

Ändern Sie die folgende Zeile in ```package.json```, um die ```next``` Version (SDK 1,0) als Ziel zu ändern:

[//]: # "'@microsoft/windows-admin-center-sdk': ' experimentell '"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

Führen Sie dann ```npm install``` aus, um Verweise im gesamten Projekt zu aktualisieren.

## <a name="5-use-the-sdk-cli-to-fix-common-migration-issues"></a>5. verwenden Sie die SDK-CLI, um häufige Migrationsprobleme zu beheben.

Wichtig: Erstellen Sie eine Sicherung Ihres Projekts, bevor Sie fortfahren.

Führen Sie im Stamm Ordner des Projekts den folgenden CLI-Befehl für Ihr Projekt aus, um häufige Migrationsprobleme automatisch zu beheben:

``` cmd
wac updateSeven --update
```

Dieser CLI-Befehl behandelt automatisch die folgenden Probleme:

* ```package-lock.json``` neu generieren
* Aktualisieren von Dateien in der Angular-Kompilierungs Umgebung:
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## <a name="6-use-the-sdk-cli-to-understand-common-migration-issues"></a>6. verwenden Sie die SDK-CLI, um allgemeine Migrationsprobleme zu verstehen.

Führen Sie im Stamm Ordner des Projekts den folgenden CLI-Befehl aus, um Ihr Projekt zu überwachen und häufige Migrationsprobleme zu finden, die manuell behoben werden müssen:

``` cmd
wac updateSeven --audit
```

Hierdurch werden die folgenden Probleme in Ihrem Projekt angezeigt:

### <a name="replace-usage-of-the-following-css-classes-with-these-sme-classes"></a>Ersetzen Sie die Verwendung der folgenden CSS-Klassen durch diese KMU-Klassen:

| Alte CSS-Klasse | Neue CSS-Klasse |
| -- | -- |
| . Auto-Flex-size |  . SME-Position-Flex-Auto |
| . Border-all |  . SME-Border-INSET-SM und. SME-Border-Color-Base-90 |
| . border-bottom |  . SME-border-bottom-SM und. SME-border-bottom-color-Base-90 |
| . Border-horizontal |  . SME-Border-horizontal-SM und. SME-Border-horizontal-Color-Base-90 |
| . border-left |  . SME-border-left-SM und. SME-border-left-Color-Base-90 |
| . border-right |  . SME-border-right-SM und. SME-border-right-Color-Base-90 |
| . Border-Top |  . SME-Border-Top-SM und. SME-Border-Top-Color-Base-90 |
| . Border-Vertical |  . SME-Border-Vertical-SM und. SME-Border-Vertical-Color-Base-90 |
| . Break-Word |  . SME-anordnen-WS-Wrap |
| btn |  . SME-Schaltfläche oder Schaltfläche |
| btn-primär |  . SME-Button. SME-Button-Primary oder. Button. SME-Button-Primary |
| . Color-dunkel |  . SME-Color-alt |
| . Color-Light |  . SME-Color-Base |
| . Color-Light-Gray |  . SME-Color-Base-90 |
| . Fixed-Flex-size |  . SME-Position-Flex-None |
| . Flex-Layout |  . SME-anordnen-Stack-h oder. SME-anordnen-Stack-v |
| Schriftart fett formatiert |  . SME-Font-emphasis1 |
| . Hervorhebung |  . SME-Hintergrundfarbe-gelb |
| . horizontal |  . SME-anordnen-Stack-h |
| . No-Scroll |  . SME-Position-Flex-Auto |
| . NoWrap |  . SME-anordnen-Stack-h oder. SME-anordnen-Stack-v |
| relative |  . SME-Layout-relativ |
| relative Mitte |  . SME-Layout-absolute. SME-Position-Center |
| umkehren |  . SME-anordnen-Stapel-umgekehrt |
| . Stretch-absolut |  . SME-Layout-absolute. SME-Position-INSET-None |
| . Stretch-korrigiert |  . SME-Layout-Fixed. SME-Position-INSET-None |
| . Stretch-vertikal |  . SME-Position-Stretch-v |
| . Stretch-Breite |  . SME-Position-Stretch-h |
| . vertikal |  . SME-anordnen-Stack-v |
| . vertikaler Bildlauf |  . SME-anordnen-Overflow-Hide-x SME-anordnen-Overflow-Auto-y |
| . Wrap |  . SME-anordnen-wrapstack-h oder. SME-anordnen-wrapstack-v |

### <a name="replace-usage-of-the-following-components-with-these-sme-components"></a>Ersetzen Sie die Verwendung der folgenden Komponenten durch die folgenden Komponenten:

| Alte Komponente | Neue Komponente |
| -- | -- |
| . Warnung |  mittelständische-Warnung |
| . Warnung-Gefahr |  mittelständische-Warnung |
| Breadcrumb |  mittelständische-Warnung |
| . CheckBox |  SME-Form-Field [Type = "CheckBox"] |
| . ComboBox |  SME-Form-Field [Type = "Select"] |
| . Dashboard |  SME-Layout-Content-Zone-aufgefüllt "SME-anordnen-Stack-h" |
| . Details-Panel |  SME-Property-Grid |
| . Details-Panel-Container |  SME-Property-Grid |
| . Details-Registerkarte |  SME-Property-Grid oder SME-Pivot |
| . Details-Wrapper |  SME-Property-Grid |
| . deaktiviert |  KMU: deaktiviert |
| . Form-Schaltflächen | mittelständische Formularfeld |
| . Form-Steuerelement | mittelständische Formularfeld |
| . Form-Steuerelemente | mittelständische Formularfeld |
| . Form-Gruppe | mittelständische Formularfeld |
| . Form-Gruppen Bezeichnung | mittelständische Formularfeld |
| . Form-Eingabe | mittelständische Formularfeld |
| . Form-Streckung | mittelständische Formularfeld |
| . Input-Datei | mittelständische Formularfeld |
| Navigations Registerkarten |  SME-Pivot |
| . Radio |  SME-Form-Field [Type = "Radio"] |
| . Required-Hinweis | mittelständische Formularfeld |
| SearchBox |  SME-Form-Field [Type = "Search"] |
| . Umschalten (Switch) |  SME-Form-Field [Type = "umschalten-Switch"] |
| . Tool-Container |  SME-Layout-Content-Zone oder SME-Layout-Content-Zone-aufgefüllt |

### <a name="these-css-classes-are-deprecated-and-are-no-longer-supported"></a>Diese CSS-Klassen sind veraltet und werden nicht mehr unterstützt:

| Alte Klasse | Veraltet |
| -- | -- |
| . akzeptabel | veraltet |
| . Color-Fehler | veraltet |
| . Color-Info | veraltet |
| . Color-Success | veraltet |
| . Color-Warnung | veraltet |
| Lösch Schaltfläche | veraltet |
| . Details-Inhalt | veraltet |
| . Error-Cover | veraltet |
| . Error-Meldung | veraltet |
| . geführtes Fenster (Schaltfläche) | veraltet |
| . Header-Container | veraltet |
| . Icon-Win | veraltet |
| Einzug | veraltet |
| . ungültig | veraltet |
| . Item-List | veraltet |
| modale Scrollable | veraltet |
| . multisection | veraltet |
| . No-Aktionsleiste | veraltet |
| . Überlauf-Ränder | veraltet |
| . Overflow-Tool | veraltet |
| . Progress-Cover | veraltet |
| . Rechter Bereich | veraltet |
| . Rollup | veraltet |
| Rollup-Status | veraltet |
| . Rollup-Titel | veraltet |
| . Rollup-Wert | veraltet |
| . SearchBox-Aktionsleiste | veraltet |
| . Size-h-1 | veraltet |
| . Size-h-2 | veraltet |
| . Size-h-3 | veraltet |
| . Size-h-4 | veraltet |
| . Size-h-Full | veraltet |
| . Size-h-Hälfte | veraltet |
| . Size-v-1 | veraltet |
| . Size-v-2 | veraltet |
| . Size-v-3 | veraltet |
| . Size-v-4 | veraltet |
| . Status-Symbol | veraltet |
| SVG-16px | veraltet |
| . Table-Einzug | veraltet |
| . Table-SM | veraltet |
| . Thin | veraltet |
| . Kachel | veraltet |
| Kachel Text | veraltet |
| . Tile-Inhalt | veraltet |
| . Tile-Footer | veraltet |
| . Tile-Header | veraltet |
| Kachel Layout | veraltet |
| . Tile-Tabelle | veraltet |
| . Toolbar | veraltet |
| . Tool Leiste | veraltet |
| . Tool-Header | veraltet |
| . Tool-Header Feld | veraltet |
| . Tool-Bereich | veraltet |
| . Usage-Leiste | veraltet |
| . Usage-Balken Bereich | veraltet |
| . Usage-Bar-background | veraltet |
| . Usage-Bar-Titel | veraltet |
| . Usage-Bar-Wert | veraltet |
| . Usage-Diagramm | veraltet |
| . Usage-Meldung | veraltet |
| . Usage-Nachrichtenbereich | veraltet |
| . Usage-Message-Title | veraltet |
| . Warnung | veraltet |
| . Leerraum | veraltet |

## <a name="7-understand-and-resolve-issues-with-observable-objects"></a>7. verstehen und Beheben von Problemen mit Observable-Objekten

### <a name="update--rxjs-function-use-for-observable-objects"></a>Aktualisieren ```rxjs``` Funktions Verwendung für Observable-Objekte

Dabei handelt es sich um einige gängige Funktionsnamen, die geändert wurden, möglicherweise gibt es andere in Ihrem Projekt.

* Aktualisieren Sie ```Observable.empty()``` auf ```empty()```
* Aktualisieren Sie ```Observable.of()``` auf ```of()```
* Aktualisieren Sie ```.switchMap()``` auf ```.pipe(switchMap())```
* Aktualisieren Sie ```.map()``` auf ```.pipe(map())```
* Aktualisieren Sie ```flatMap()``` auf ```mergeMap()```


### <a name="resolve-runtime-issues-with-map-and-filter-functions-on-observable-objects"></a>Beheben von Lauf Zeitproblemen mit ```.map()```-und ```.filter()```-Funktionen für Observable-Objekte

Wenn der Compiler einen ```observable``` Objekttyp nicht ordnungsgemäß identifizieren kann, können ```.map()``` und ```.filter()``` Funktionen aus dem ```array``` Objekt stattdessen dem-Objekt zugeordnet werden, was zur Laufzeit zu Fehlern führt.  Stellen Sie sicher, dass ihre Funktionen ein ```observable``` Objekt zurückgeben, das einen expliziten Datentyp angibt, um dieses Problem zu vermeiden.

```any``` und kein Rückgabetyp dieses Problem verursachen kann, suchen Sie nach Code mit diesen Mustern:

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## <a name="8-resolve-other-common-issues"></a>8. beheben anderer häufiger Probleme

Diese Verfahren helfen Ihnen, andere häufige Probleme zu beheben:

* Ausführen von ```ng lint --fix```, um häufige lint-Probleme zu beheben
* ```gulp build``` wiederholt ausführen, um Probleme inkrementell zu beheben, die ```gulp build``` automatisch auflösen können

## <a name="9-build-and-serve-your-project"></a>9. erstellen und Bereitstellen Ihres Projekts

Führen Sie die folgenden Befehle aus, um Ihr Projekt mit der neuesten Version (SDK 1,0) zu erstellen und bereitzustellen:

``` cmd
gulp build
gulp serve --port 4201
```

## <a name="10-turn-on-dark-theme-in-windows-admin-center"></a>10. Aktivieren des dunklen Designs im Windows Admin Center

Um das dunkle Design in Windows Admin Center, Version 1902 und höher, zu aktivieren, führen Sie die folgenden Schritte aus:

* Öffnen Sie das Windows Admin Center (Version 1902 und höher).
* Klicken Sie in der oberen rechten Ecke des Fensters auf das Symbol " **Einstellungen** ".
* Registerkarte " **erweitert** " auswählen
* Klicken Sie unter *Experiment Schlüssel*auf **Hinzufügen** .
* Geben Sie einen neuen Wert ```msft.sme.shell.personalization``` in das leere Feld ein, das im vorherigen Schritt erstellt wurde.
* Klicken Sie auf **Speichern und erneut laden**
* Die Einstellungen verfügen nun über eine neue Registerkarte, **Personalisierung**.  Diese Registerkarte auswählen
* **Farben** in den **dunklen Modus ändern (Vorschau)**
