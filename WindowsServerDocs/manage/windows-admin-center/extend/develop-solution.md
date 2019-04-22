---
title: Entwickeln einer Lösungserweiterung
description: Entwickeln einer Lösung Erweiterungs Windows Admin Center-SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ed5ecddbaef91f127846825e408a9a6ec65ff741
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825471"
---
# <a name="develop-a-solution-extension"></a>Entwickeln einer Lösungserweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Lösungen definieren in erster Linie einen eindeutigen Typ des Objekts, die Sie über Windows Admin Center verwalten möchten.  Diese Lösungen/Verbindungstypen sind in Windows Admin Center standardmäßig enthalten:

* Windows Server-Verbindungen
* Windows-PC-Verbindungen
* Failover-Cluster-Verbindungen
* Hyperkonvergente Clusterverbindungen

Wenn Sie eine Verbindung aus dem Windows Admin Center-Seite "Verbindung" auswählen, die Lösung-Erweiterung für den zugehörigen Typ wird geladen, und Windows Admin Center wird versuchen, zur Verbindung mit des Zielknotens. Wenn die Verbindung erfolgreich ist, die Lösung des Erweiterungs-Benutzeroberfläche wird geladen und Windows Admin Center werden die Tools für die Lösung im linken Navigationsbereich angezeigt.

Wenn Sie ein Verwaltungs-GUI für Dienste, die nicht von den Verbindungstypen "Standard" oben, solche ein Netzwerkswitch oder anderer Hardware, die nicht sichtbaren definiert, nach Computernamen erstellen möchten, empfiehlt es sich, eine eigene Lösung-Erweiterung zu erstellen.

> [!NOTE]
> Sie sind nicht mit anderen Erweiterungstypen vertraut? Erfahren Sie mehr über die [Erweiterbarkeit Architektur und die Erweiterung Typen](understand-extensions.md).

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie nicht bereits geschehen, [Vorbereiten der Umgebung](prepare-development-environment.md) durch die Installation von Abhängigkeiten und globale Voraussetzungen für alle Projekte.

## <a name="create-a-new-solution-extension-with-the-windows-admin-center-cli"></a>Erstellen Sie eine neue Erweiterung für die Lösung, mit der Windows Admin Center-CLI ##

Nachdem Sie alle Abhängigkeiten installiert haben, können Sie die neue projektmappenerweiterung zu erstellen.  Erstellen Sie oder navigieren Sie zu einem Ordner, der Ihre Projektdateien enthält, öffnen Sie eine Eingabeaufforderung, und legen Sie diesen Ordner als Arbeitsverzeichnis.  Verwenden die Windows Admin Center-CLI, die zuvor installiert wurde, erstellen Sie eine neue Erweiterung mit der folgenden Syntax:

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Solution Name}``` | Den Namen der Projektmappe (mit Leerzeichen) | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```Manage Foo Works``` |

Beispiel zur Verwendung:

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

Dies erstellt einen neuen Ordner in das aktuelle Arbeitsverzeichnis, das mit dem Namen, den Sie für Ihre Lösung angegeben, kopiert alle erforderlichen Vorlagendateien in Ihr Projekt und die Dateien mit Ihrer Unternehmens-Lösung und Name des Tools konfiguriert.  

Als Nächstes wechseln Sie zu dem Ordner, der gerade erstellt haben, und installieren Sie erforderliche lokale Abhängigkeiten zu, indem Sie den folgenden Befehl ausführen:

```
npm install
```

Sobald dies abgeschlossen ist, haben Sie alles, was einrichten, die Sie die neue Erweiterung in Windows Admin Center zu laden müssen. 

## <a name="add-content-to-your-extension"></a>Hinzufügen von Inhalt zu Ihrer Erweiterung

Nun, dass Sie eine Erweiterung mit der Windows Admin Center-CLI erstellt haben, können Sie Inhalt anpassen.  Diese Leitfäden finden Sie Beispiele für Möglichkeiten:

- Hinzufügen einer [leere-Modul](guides\add-module.md)
- Hinzufügen einer [iFrame](guides\add-iframe.md)
- Erstellen Sie eine [benutzerdefinierte Verbindungsanbieter](guides\create-connection-provider.md)
- Ändern Sie [root Navigationsverhalten](guides\modify-root-navigation.md)
 
Weitere Beispiele finden Sie unserem [Website des GitHub-SDKS](https://aka.ms/wacsdk):
-  [Entwicklertools](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) ist eine voll funktionsfähige-Erweiterung, die in Windows Admin Center-Seite geladen werden können, und eine umfangreiche Sammlung von Beispiel-Funktionen und Tools Beispiele, die Sie durchsuchen und verwenden Sie in Ihrer eigenen Extension enthält.

## <a name="build-and-side-load-your-extension"></a>Erstellen und die Seite laden die Erweiterung

Laden Sie als Nächstes erstellen und die Seite die Erweiterung in Windows Admin Center.  Öffnen Sie ein Befehlsfenster, wechseln Sie in Ihrem Quellverzeichnis, sind Sie bereit zum Erstellen.

* Erstellen und mit schlucken dienen:

    ```
    gulp build
    gulp serve -p 4201
    ```

Beachten Sie, dass müssen Sie einen Port auswählen, der derzeit frei ist. Stellen Sie sicher, dass Sie versucht nicht, den Port verwenden, den Windows Admin Center ausgeführt wird.

Das Projekt kann Seite in eine lokale Instanz des Windows Admin Center zu Testzwecken durch Anfügen des lokal vom Server ausgegebenen Projekts in Windows Admin Center geladen sein.

* Starten des Windows Admin Center in einem Webbrowser
* Öffnen Sie den Debugger (F12)
* Öffnen Sie die Konsole, und geben Sie den folgenden Befehl ein:

    ```
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   Aktualisieren Sie den Webbrowser

Das Projekt wird jetzt in der Liste Tools mit (Seite geladen) neben dem Namen angezeigt.

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Eine andere Version des Windows Admin Center-SDK

Halten die Erweiterung auf dem neuesten Stand mit SDK-Änderungen und Plattform ist einfach.  Erfahren Sie, wie Sie [eine andere Version](target-sdk-version.md) Windows Admin Center SDK.