---
title: Entwickeln Sie eine lösungserweiterung
description: Entwickeln Sie eine lösungserweiterung Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ed5ecddbaef91f127846825e408a9a6ec65ff741
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081067"
---
# Entwickeln Sie eine lösungserweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Lösungen definieren in erster Linie einen eindeutigen Objekttyp, das Sie über Windows Admin Center verwalten möchten.  Diese Lösungen/Verbindungstypen sind standardmäßig in Windows Admin Center enthalten:

* Windows Server-Verbindungen
* Windows-PC-Anschlüsse
* Failoverclusterverbindungen
* Zusammengeführte Clusterverbindungen

Wenn Sie eine Verbindung aus dem Windows Admin Center Verbindung auswählen, wird die Erweiterung der Lösung für diese Verbindung Typ geladen und Windows Admin Center wird versucht, für die Verbindung an den Zielknoten. Wenn die Verbindung erfolgreich ist, wird die Lösung Erweiterung UI geladen, und Windows Admin Center wird die Tools für diese Lösung im linken Navigationsbereich angezeigt.

Wenn Sie eine Management-GUI für Dienste, die nicht durch die Standard-Verbindungstypen oben, solche einem Netzwerkswitch oder andere Hardware, die nicht sichtbar anhand des Computernamens definiert erstellen möchten, sollten Sie Ihre eigene lösungserweiterung erstellen.

> [!NOTE]
> Mit den anderen Erweiterung nicht vertraut? Erfahren Sie mehr über die [Erweiterbarkeit Architektur und Erweiterung Typen](understand-extensions.md).

## Vorbereiten der Umgebung

Wenn Sie nicht bereits geschehen, durch das Installieren von Abhängigkeiten und globale erforderlichen Komponenten für alle Projekte [Vorbereiten der Umgebung](prepare-development-environment.md) .

## Erstellen Sie eine neue lösungserweiterung mit der Windows Admin Center-CLI ##

Wenn Sie alle Abhängigkeiten installiert haben, können Sie Ihre neue lösungserweiterung erstellen.  Erstellen oder navigieren Sie zu einem Ordner, der Ihre Projektdateien enthält, ein Eingabeaufforderungsfenster, und legen Sie diesen Ordner als das Arbeitsverzeichnis.  Verwenden die Windows Admin Center-CLI, die zuvor installiert wurde, erstellen Sie eine neue Erweiterung mit folgender Syntax:

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Solution Name}``` | Die Namen Ihrer Projektmappe (mit Leerzeichen) | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```Manage Foo Works``` |

Beispiel zur Verwendung:

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

Dadurch entsteht einen neuen Ordner in das aktuelle Arbeitsverzeichnis, das mit dem Namen für die Projektmappe angegeben, werden alle erforderlichen Vorlagendateien in Ihrem Projekt kopiert und die Dateien mit Ihrem Unternehmen, Lösung und Name des Tools konfiguriert.  

Als Nächstes ändern Sie das Verzeichnis in den Ordner, der gerade erstellt haben, und Installieren von erforderlichen lokalen Abhängigkeiten mithilfe des folgenden Befehls:

```
npm install
```

Sobald dies abgeschlossen ist, haben Sie alles einrichten die neue Erweiterung in Windows Admin Center geladen werden müssen. 

## Hinzufügen von Inhalten zu der Erweiterung

Nun, da Sie eine Erweiterung mit dem Windows Admin Center-CLI erstellt haben, können Sie zur Anpassung von Inhalten.  Beispiele dafür, was Sie tun können finden Sie in diesen Handbüchern aus:

- Fügen Sie ein [leeres Modul](guides\add-module.md)
- [IFrame](guides\add-iframe.md) hinzufügen
- Erstellen Sie einen [benutzerdefinierten Verbindung-Anbieter](guides\create-connection-provider.md)
- [Stamm Navigationsverhalten](guides\modify-root-navigation.md) ändern
 
Weitere Beispiele finden Sie unserer [GitHub-SDK-Website](https://aka.ms/wacsdk):
-  [Entwicklertools](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools) ist eine voll funktionsfähige Erweiterung, die in Windows Admin Center Seite geladen werden können, und enthält eine umfassende Auflistung von Beispiel-Funktion und Tool-Beispiele, in denen Sie durchsuchen und in Ihre eigene Erweiterung verwenden können.

## Build und Seite laden die Erweiterung

Als Nächstes laden Build und Seite die Erweiterung in Windows Admin Center.  Öffnen Sie ein Befehlsfenster, wechseln Sie in Ihrer Quellverzeichnis, und klicken Sie dann erstellen bereit.

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

## Eine andere Version von Windows Admin Center SDK

Halten die Erweiterung auf dem neuesten Stand mit SDK-Änderungen und Plattform Änderungen ist einfach.  Informationen Sie darüber, wie Sie [Ziel eine andere Version](target-sdk-version.md) von Windows Admin Center SDK.