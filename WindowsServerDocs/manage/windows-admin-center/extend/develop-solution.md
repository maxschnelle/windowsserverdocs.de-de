---
title: Entwickeln einer Lösungserweiterung
description: Entwickeln einer projektmappenerweiterung Windows Admin Center SDK (Project Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 293fa8a617d7ceb1628ec72df2f015b6b2547f16
ms.sourcegitcommit: f89639d3861c61620275c69f31f4b02fd48327ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/29/2020
ms.locfileid: "91517586"
---
# <a name="develop-a-solution-extension"></a>Entwickeln einer Lösungserweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Lösungen definieren in erster Linie einen eindeutigen Objekttyp, den Sie über das Windows Admin Center verwalten möchten.  Diese Lösungen/Verbindungstypen sind standardmäßig im Windows Admin Center enthalten:

* Windows Server-Verbindungen
* Windows-PC-Verbindungen
* Failoverclusterverbindungen
* Hyperkonvergierte Cluster Verbindungen

Wenn Sie auf der Verbindungs Seite des Windows Admin Centers eine Verbindung auswählen, wird die projektmappenerweiterung für den Typ der Verbindung geladen, und das Windows Admin Center versucht, eine Verbindung mit dem Zielknoten herzustellen. Wenn die Verbindung erfolgreich hergestellt wurde, wird die Benutzeroberfläche der projektmappenerweiterung geladen, und das Windows Admin Center zeigt die Tools für diese Projekt Mappe im linken Navigationsbereich an.

Wenn Sie eine Verwaltungs-GUI für Dienste erstellen möchten, die nicht durch die oben genannten Standard Verbindungstypen definiert sind, z. b. ein Netzwerk Switch oder andere Hardware, die nicht durch den Computernamen erkennbar ist, können Sie eine eigene Lösungs Erweiterung erstellen.

> [!NOTE]
> Sie sind mit den unterschiedlichen Erweiterungs Typen nicht vertraut? Erfahren Sie mehr über die [Erweiterbarkeits Architektur und die Erweiterungs Typen](understand-extensions.md).

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie dies noch nicht getan haben, [bereiten Sie Ihre Umgebung](prepare-development-environment.md) vor, indem Sie die Abhängigkeiten und globalen Voraussetzungen für alle Projekte installieren.

## <a name="create-a-new-solution-extension-with-the-windows-admin-center-cli"></a>Erstellen einer neuen projektmappenerweiterung mit der Windows Admin Center-CLI ##

Nachdem Sie alle Abhängigkeiten installiert haben, können Sie Ihre neue projektmappenerweiterung erstellen.  Erstellen oder navigieren Sie zu einem Ordner, der die Projektdateien enthält, öffnen Sie eine Eingabeaufforderung, und legen Sie diesen Ordner als Arbeitsverzeichnis fest.  Erstellen Sie mithilfe der zuvor installierten Windows Admin Center-CLI eine neue Erweiterung mit der folgenden Syntax:

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| Wert | Erklärung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Name Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Solution Name}``` | Ihr Projektmappenname (mit Leerzeichen) | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | Ihr Toolname (mit Leerzeichen) | ```Manage Foo Works``` |

Beispiel zur Verwendung:

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

Dadurch wird im aktuellen Arbeitsverzeichnis ein neuer Ordner mit dem Namen erstellt, den Sie für die Projekt Mappe angegeben haben. alle erforderlichen Vorlagen Dateien werden in das Projekt kopiert, und die Dateien werden mit Ihrem Unternehmen, ihrer Lösung und dem Toolnamen konfiguriert.

Wechseln Sie als nächstes das Verzeichnis in den soeben erstellten Ordner, und installieren Sie die erforderlichen lokalen Abhängigkeiten, indem Sie den folgenden Befehl ausführen:

```
npm install
```

Nachdem dieser Vorgang abgeschlossen ist, haben Sie alles eingerichtet, was Sie benötigen, um Ihre neue Erweiterung in das Windows Admin Center zu laden.

## <a name="add-content-to-your-extension"></a>Hinzufügen von Inhalt zu ihrer Erweiterung

Nachdem Sie nun mit der Windows Admin Center-CLI eine Erweiterung erstellt haben, können Sie Inhalte anpassen.  In diesen Handbüchern finden Sie Beispiele dazu, was Sie tun können:

- Hinzufügen eines [leeren Moduls](guides/add-module.md)
- [Iframe](guides/add-iframe.md) hinzufügen
- Erstellen eines [benutzerdefinierten Verbindungs Anbieters](guides/create-connection-provider.md)
- Ändern des Verhaltens der Stamm [Navigation](guides/modify-root-navigation.md)

Weitere Beispiele finden Sie im Entwicklerhandbuch. Das Entwicklerhandbuch ist eine voll funktionsfähige projektmappenerweiterung, die im Windows Admin Center nebeneinander geladen werden kann und eine umfangreiche Sammlung von Beispiel Funktionen und Tool Beispielen enthält, die Sie in ihrer eigenen Erweiterung durchsuchen und verwenden können. 

Aktivieren Sie die Erweiterung Entwicklerhandbuch auf der Seite **erweitert** Ihrer Windows Admin Center-Einstellungen. 

## <a name="build-and-side-load-your-extension"></a>Erstellen und neben Laden Ihrer Erweiterung

Erstellen Sie als nächstes die Erweiterung, und laden Sie Sie auf das Windows Admin Center.  Öffnen Sie ein Befehlsfenster, wechseln Sie zum Quellverzeichnis, und erstellen Sie das Verzeichnis.

* Erstellen Sie mit Gulp, und bedienen Sie es:

    ```
    gulp build
    gulp serve -p 4201
    ```

Beachten Sie, dass Sie einen Port auswählen müssen, der derzeit kostenlos ist. Stellen Sie sicher, dass Sie nicht versuchen, den Port zu verwenden, auf dem Windows Admin Center ausgeführt wird.

Ihr Projekt kann zum Testen in eine lokale Instanz des Windows Admin Centers geladen werden, indem das lokal bereitgestellte Projekt an das Windows Admin Center angefügt wird.

* Starten des Windows Admin Centers in einem Webbrowser
* Öffnen Sie den Debugger (F12).
* Öffnen Sie die-Konsole, und geben Sie den folgenden Befehl ein:

    ```
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   Webbrowser aktualisieren

Das Projekt ist nun in der Liste der Tools mit (neben dem Namen) sichtbar.

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Eine andere Version des Windows Admin Center SDK als Zielversion

Es ist einfach, ihre Erweiterung mit SDK-Änderungen und Platt Formänderungen auf dem neuesten Stand zu halten.  Informieren Sie sich über das [Ziel einer anderen Version](target-sdk-version.md) des Windows Admin Center SDK.