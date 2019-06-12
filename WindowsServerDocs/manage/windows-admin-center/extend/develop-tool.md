---
title: Entwickeln einer Tool-Erweiterung
description: Entwickeln Sie eine toolerweiterung Windows Admin Center-SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 31d8dbd3df4c44b6e0a3780b022dfbd9fffdffec
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452578"
---
# <a name="develop-a-tool-extension"></a>Entwickeln einer Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Eine toolerweiterung ist der einfachste Weg, die Benutzer mit Windows Admin Center zum Verwalten einer Verbindung, wie z. B. einem Server oder Cluster zu interagieren. Wenn Sie klicken Sie auf eine Verbindung in der Windows Admin Center-Startseite und eine Verbindung herstellen, werden Sie dann eine Liste der Tools im linken Navigationsbereich angezeigt. Beim Klicken auf ein Tool, die Tools-Erweiterung geladen und im rechten Bereich angezeigt.

Wenn eine toolerweiterung geladen wird, können sie WMI-Aufrufe oder PowerShell-Skripts auf einem Ziel-Server oder Cluster ausführen und Anzeigen von Informationen in der Benutzeroberfläche oder Ausführen von Befehlen auf Grundlage der Benutzereingabe. Toolerweiterungen definieren, welche Lösungen er, angezeigt werden soll einen anderen Satz von Tools für jede Lösung führt.

> [!NOTE]
> Sie sind nicht mit anderen Erweiterungstypen vertraut? Erfahren Sie mehr über die [Erweiterbarkeit Architektur und die Erweiterung Typen](understand-extensions.md).

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie nicht bereits geschehen, [Vorbereiten der Umgebung](prepare-development-environment.md) durch die Installation von Abhängigkeiten und globale Voraussetzungen für alle Projekte.

## <a name="create-a-new-tool-extension-with-the-windows-admin-center-cli"></a>Erstellen Sie eine neue Tools-Erweiterung, mit der Windows Admin Center-CLI ##

Nachdem Sie alle Abhängigkeiten installiert haben, können Sie die neue Tools-Erweiterung zu erstellen.  Erstellen Sie oder navigieren Sie zu einem Ordner, der Ihre Projektdateien enthält, öffnen Sie eine Eingabeaufforderung, und legen Sie diesen Ordner als Arbeitsverzeichnis.  Verwenden die Windows Admin Center-CLI, die zuvor installiert wurde, erstellen Sie eine neue Erweiterung mit der folgenden Syntax:

``` cmd
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```Manage Foo Works``` |

Beispiel zur Verwendung:

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

Dies erstellt einen neuen Ordner in das aktuelle Arbeitsverzeichnis, das mit dem Namen, den Sie für Ihr Tool angegeben, kopiert alle erforderlichen Vorlagendateien in Ihr Projekt und die Dateien durch den Namen Ihres Unternehmens und das Tool konfiguriert.  

Als Nächstes wechseln Sie zu dem Ordner, der gerade erstellt haben, und installieren Sie erforderliche lokale Abhängigkeiten zu, indem Sie den folgenden Befehl ausführen:

``` cmd
npm install
```

Sobald dies abgeschlossen ist, haben Sie alles, was einrichten, die Sie die neue Erweiterung in Windows Admin Center zu laden müssen. 

## <a name="add-content-to-your-extension"></a>Hinzufügen von Inhalt zu Ihrer Erweiterung

Nun, dass Sie eine Erweiterung mit der Windows Admin Center-CLI erstellt haben, können Sie Inhalt anpassen.  Diese Leitfäden finden Sie Beispiele für Möglichkeiten:

- Hinzufügen einer [leere-Modul](guides/add-module.md)
- Hinzufügen einer [iFrame](guides/add-iframe.md)
 
Weitere Beispiele finden Sie unserem [Website des GitHub-SDKS](https://aka.ms/wacsdk):
-  [Entwicklertools](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) ist eine voll funktionsfähige-Erweiterung, die in Windows Admin Center-Seite geladen werden können, und eine umfangreiche Sammlung von Beispiel-Funktionen und Tools Beispiele, die Sie durchsuchen und verwenden Sie in Ihrer eigenen Extension enthält.

## <a name="customize-your-extensions-icon"></a>Anpassen der Erweiterung des Symbols

Das Symbol, das zeigt, können Sie für Ihre Erweiterung in der Liste der Tools anpassen.  Zu diesem Zweck ändern Sie alle ```icon``` Einträge im ```manifest.json``` für Ihre Erweiterung:

``` json
"icon": "{!icon-uri}",
```

| Wert | Erläuterung | Beispiel-uri |
| ----- | ----------- | ------- |
| ```{!icon-uri}``` | Der Speicherort der Symbolressource | ```assets/foo-icon.svg``` |

HINWEIS: Derzeit nicht benutzerdefinierte Symbole sichtbar, wenn die Seite die Erweiterung im Dev-Modus laden.  Dieses Problem zu umgehen, entfernen Sie den Inhalt der ```target``` wie folgt:

``` json
"target": "",
```

Diese Konfiguration ist nur gültig für querladen im Modus "Dev", daher es wichtig ist, um den Wert im beizubehalten ```target``` und wiederhergestellt werden kann, ehe Sie die Erweiterung.

## <a name="build-and-side-load-your-extension"></a>Erstellen und die Seite laden die Erweiterung

Laden Sie als Nächstes erstellen und die Seite die Erweiterung in Windows Admin Center.  Öffnen Sie ein Befehlsfenster, wechseln Sie in Ihrem Quellverzeichnis, sind Sie bereit zum Erstellen.

* Erstellen und mit schlucken dienen:

    ``` cmd
    gulp build
    gulp serve -p 4201
    ```

Beachten Sie, dass müssen Sie einen Port auswählen, der derzeit frei ist. Stellen Sie sicher, dass Sie versucht nicht, den Port verwenden, den Windows Admin Center ausgeführt wird.

Das Projekt kann Seite in eine lokale Instanz des Windows Admin Center zu Testzwecken durch Anfügen des lokal vom Server ausgegebenen Projekts in Windows Admin Center geladen sein.

* Starten des Windows Admin Center in einem Webbrowser
* Öffnen Sie den Debugger (F12)
* Öffnen Sie die Konsole, und geben Sie den folgenden Befehl ein:

    ``` cmd
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   Aktualisieren Sie den Webbrowser

Das Projekt wird jetzt in der Liste Tools mit (Seite geladen) neben dem Namen angezeigt.

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Eine andere Version des Windows Admin Center-SDK

Halten die Erweiterung auf dem neuesten Stand mit SDK-Änderungen und Plattform ist einfach.  Erfahren Sie, wie Sie [eine andere Version](target-sdk-version.md) Windows Admin Center SDK.