---
title: Entwickeln einer Toolerweiterung
description: Entwickeln einer Tool Erweiterung Windows Admin Center SDK (Project Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: f3bf885cd86015842be26124e7374f622d38a9c2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954126"
---
# <a name="develop-a-tool-extension"></a>Entwickeln einer Toolerweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Eine Tool Erweiterung ist die primäre Methode, mit der Benutzer mit Windows Admin Center interagieren, um eine Verbindung wie einen Server oder Cluster zu verwalten. Wenn Sie auf dem Windows Admin Center-Startbildschirm auf eine Verbindung klicken und eine Verbindung herstellen, wird eine Liste der Tools im linken Navigationsbereich angezeigt. Wenn Sie auf ein Tool klicken, wird die Tool Erweiterung geladen und im rechten Bereich angezeigt.

Wenn eine Tool Erweiterung geladen wird, kann Sie WMI-Aufrufe oder PowerShell-Skripts auf einem Zielserver oder-Cluster ausführen und Informationen in der Benutzeroberfläche anzeigen oder Befehle auf der Grundlage von Benutzereingaben ausführen. Tool Erweiterungen definieren, für welche Projektmappen Sie angezeigt werden sollen, was zu einem anderen Satz von Tools für jede Lösung führt.

> [!NOTE]
> Sie sind mit den unterschiedlichen Erweiterungs Typen nicht vertraut? Erfahren Sie mehr über die [Erweiterbarkeits Architektur und die Erweiterungs Typen](understand-extensions.md).

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie dies noch nicht getan haben, [bereiten Sie Ihre Umgebung](prepare-development-environment.md) vor, indem Sie die Abhängigkeiten und globalen Voraussetzungen für alle Projekte installieren.

## <a name="create-a-new-tool-extension-with-the-windows-admin-center-cli"></a>Erstellen einer neuen Tool Erweiterung mit der Windows Admin Center-CLI ##

Nachdem Sie alle Abhängigkeiten installiert haben, können Sie die neue Tool Erweiterung erstellen.  Erstellen oder navigieren Sie zu einem Ordner, der die Projektdateien enthält, öffnen Sie eine Eingabeaufforderung, und legen Sie diesen Ordner als Arbeitsverzeichnis fest.  Erstellen Sie mithilfe der zuvor installierten Windows Admin Center-CLI eine neue Erweiterung mit der folgenden Syntax:

``` cmd
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| Wert | Erklärung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Name Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Ihr Toolname (mit Leerzeichen) | ```Manage Foo Works``` |

Beispiel zur Verwendung:

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

Dadurch wird im aktuellen Arbeitsverzeichnis ein neuer Ordner mit dem Namen erstellt, den Sie für das Tool angegeben haben. alle erforderlichen Vorlagen Dateien werden in das Projekt kopiert, und die Dateien werden mit dem Namen Ihres Unternehmens und des Tools konfiguriert.

Wechseln Sie als nächstes das Verzeichnis in den soeben erstellten Ordner, und installieren Sie die erforderlichen lokalen Abhängigkeiten, indem Sie den folgenden Befehl ausführen:

``` cmd
npm install
```

Nachdem dieser Vorgang abgeschlossen ist, haben Sie alles eingerichtet, was Sie benötigen, um Ihre neue Erweiterung in das Windows Admin Center zu laden.

## <a name="add-content-to-your-extension"></a>Hinzufügen von Inhalt zu ihrer Erweiterung

Nachdem Sie nun mit der Windows Admin Center-CLI eine Erweiterung erstellt haben, können Sie Inhalte anpassen.  In diesen Handbüchern finden Sie Beispiele dazu, was Sie tun können:

- Hinzufügen eines [leeren Moduls](guides/add-module.md)
- [Iframe](guides/add-iframe.md) hinzufügen

Weitere Beispiele finden Sie auf unserer [GitHub SDK-Website](https://aka.ms/wacsdk):
-  [Entwicklertools](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) ist eine voll funktionsfähige Erweiterung, die im Windows Admin Center nebeneinander geladen werden kann und eine umfangreiche Sammlung von Beispiel Funktionen und Tool Beispielen enthält, die Sie in ihrer eigenen Erweiterung durchsuchen und verwenden können.

## <a name="customize-your-extensions-icon"></a>Anpassen des Symbols der Erweiterung

Sie können das Symbol, das für Ihre Erweiterung angezeigt wird, in der Toolliste anpassen.  Ändern Sie hierzu alle ```icon``` Einträge in ```manifest.json``` für die Erweiterung:

``` json
"icon": "{!icon-uri}",
```

| Wert | Erklärung | Beispiel-URI |
| ----- | ----------- | ------- |
| ```{!icon-uri}``` | Der Speicherort Ihrer Symbol Ressource. | ```assets/foo-icon.svg``` |

Hinweis: Derzeit sind benutzerdefinierte Symbole nicht sichtbar, wenn Sie die Erweiterung im Entwicklungsmodus laden.  Um dieses Problem zu umgehen, entfernen Sie den Inhalt von ```target``` wie folgt:

``` json
"target": "",
```

Diese Konfiguration gilt nur für das Sideloading im Entwicklungsmodus. Daher ist es wichtig, den in enthaltenen Wert beizubehalten ```target``` und ihn vor dem Veröffentlichen der Erweiterung wiederherzustellen.

## <a name="build-and-side-load-your-extension"></a>Erstellen und neben Laden Ihrer Erweiterung

Erstellen Sie als nächstes die Erweiterung, und laden Sie Sie auf das Windows Admin Center.  Öffnen Sie ein Befehlsfenster, wechseln Sie zum Quellverzeichnis, und erstellen Sie das Verzeichnis.

* Erstellen Sie mit Gulp, und bedienen Sie es:

    ``` cmd
    gulp build
    gulp serve -p 4201
    ```

Beachten Sie, dass Sie einen Port auswählen müssen, der derzeit kostenlos ist. Stellen Sie sicher, dass Sie nicht versuchen, den Port zu verwenden, auf dem Windows Admin Center ausgeführt wird.

Ihr Projekt kann zum Testen in eine lokale Instanz des Windows Admin Centers geladen werden, indem das lokal bereitgestellte Projekt an das Windows Admin Center angefügt wird.

* Starten des Windows Admin Centers in einem Webbrowser
* Öffnen Sie den Debugger (F12).
* Öffnen Sie die-Konsole, und geben Sie den folgenden Befehl ein:

    ``` cmd
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   Webbrowser aktualisieren

Das Projekt ist nun in der Liste der Tools mit (neben dem Namen) sichtbar.

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Eine andere Version des Windows Admin Center SDK als Zielversion

Es ist einfach, ihre Erweiterung mit SDK-Änderungen und Platt Formänderungen auf dem neuesten Stand zu halten.  Informieren Sie sich über das [Ziel einer anderen Version](target-sdk-version.md) des Windows Admin Center SDK.