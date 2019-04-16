---
title: Entwickeln Sie eine Tool-Erweiterung
description: Entwickeln Sie eine Tool-Erweiterung Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7dd213f7032ab77021bbfcbdc966c9c2307b86eb
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081057"
---
# Entwickeln Sie eine Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Eine Tool-Erweiterung ist der bevorzugte Weg, die Interaktion von Benutzern mit Windows Admin Center, um eine Verbindung, z. B. einem Server oder Cluster zu verwalten. Wenn Sie eine Verbindung in der Windows Admin Center-Startseite auf und eine Verbindung herstellen, wird dann mit einer Liste der Tools im linken Navigationsbereich angezeigt werden. Wenn Sie auf ein Tool klicken, wird die Tool-Erweiterung geladen und im rechten Bereich angezeigt.

Wenn eine Tool-Erweiterung geladen wird, können sie WMI-Aufrufe oder PowerShell-Skripts auf einem Zielserver oder Cluster ausführen und Informationen in der Benutzeroberfläche anzeigen oder basierend auf Benutzereingaben Befehle ausführen. Tool-Erweiterungen definieren, welche Lösungen, angezeigt werden sollte sich ergebenden in einen anderen Satz von Tools für jede bereitzustellende Lösung.

> [!NOTE]
> Mit den anderen Erweiterung nicht vertraut? Erfahren Sie mehr über die [Erweiterbarkeit Architektur und Erweiterung Typen](understand-extensions.md).

## Vorbereiten der Umgebung

Wenn Sie nicht bereits geschehen, durch das Installieren von Abhängigkeiten und globale erforderlichen Komponenten für alle Projekte [Vorbereiten der Umgebung](prepare-development-environment.md) .

## Erstellen Sie eine neue Tool-Erweiterung mit der Windows Admin Center-CLI ##

Wenn Sie alle Abhängigkeiten installiert haben, können Sie mit die neuen Tool-Erweiterung erstellen.  Erstellen oder navigieren Sie zu einem Ordner, der Ihre Projektdateien enthält, ein Eingabeaufforderungsfenster, und legen Sie diesen Ordner als das Arbeitsverzeichnis.  Verwenden die Windows Admin Center-CLI, die zuvor installiert wurde, erstellen Sie eine neue Erweiterung mit folgender Syntax:

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```Manage Foo Works``` |

Beispiel zur Verwendung:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

Dadurch entsteht einen neuen Ordner in das aktuelle Arbeitsverzeichnis, das mit dem Namen für Ihr Tool angegeben, werden alle erforderlichen Vorlagendateien in Ihrem Projekt kopiert und konfiguriert die Dateien mit den Namen Ihrer Firma und Tool.  

Als Nächstes ändern Sie das Verzeichnis in den Ordner, der gerade erstellt haben, und Installieren von erforderlichen lokalen Abhängigkeiten mithilfe des folgenden Befehls:

```
npm install
```

Sobald dies abgeschlossen ist, haben Sie alles einrichten die neue Erweiterung in Windows Admin Center geladen werden müssen. 

## Hinzufügen von Inhalten zu der Erweiterung

Nun, da Sie eine Erweiterung mit dem Windows Admin Center-CLI erstellt haben, können Sie zur Anpassung von Inhalten.  Beispiele dafür, was Sie tun können finden Sie in diesen Handbüchern aus:

- Fügen Sie ein [leeres Modul](guides\add-module.md)
- [IFrame](guides\add-iframe.md) hinzufügen
 
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