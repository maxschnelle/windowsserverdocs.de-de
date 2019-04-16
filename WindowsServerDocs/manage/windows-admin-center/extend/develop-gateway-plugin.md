---
title: Entwickeln Sie ein Gateway-Plug-in
description: Entwickeln Sie ein Gateway-Plug-in Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93cee5b8e3611a264119947103d22d9aa3b9a56b
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081157"
---
# Entwickeln Sie ein Gateway-Plug-in

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Ein Windows Admin Center Gateway-Plug-in ermöglicht die API Kommunikation über die Benutzeroberfläche des Tools oder der Projektmappe dem Zielknoten.  Windows Admin Center hostet einen Gatewaydienst, der Fehlerzahl Befehle und Gateway-Plug-Ins-Skripts auf Zielknoten ausgeführt wird. Der Gatewaydienst kann erweitert werden, um benutzerdefinierte Gateway-Plug-Ins enthalten, die nicht die Protokolle unterstützen.

Diese Gateway-Plug-Ins sind standardmäßig mit Windows Admin Center enthalten:

* PowerShell-Gateway-Plug-in
* WMI-Gateway-Plug-in

Wenn Sie mit der ein anderes Protokoll als PowerShell oder WMI kommunizieren möchten, können z. B. mit REST-Sie Ihre eigenen Gateway-Plug-in erstellen.  Gateway-Plug-Ins in eine separate AppDomain aus den vorhandenen Gateway-Prozess geladen werden, aber das gleiche Maß an erhöhte Rechte für die Rechte verwenden.

> [!NOTE]
> Mit den anderen Erweiterung nicht vertraut? Erfahren Sie mehr über die [Erweiterbarkeit Architektur und Erweiterung Typen](understand-extensions.md).

## Vorbereiten der Umgebung

Wenn Sie nicht bereits geschehen, durch das Installieren von Abhängigkeiten und globale erforderlichen Komponenten für alle Projekte [Vorbereiten der Umgebung](prepare-development-environment.md) .

## Erstellen Sie ein Gateway-Plug-in (C#-Bibliothek)

Um eine benutzerdefinierte Gateway-Plug-in zu erstellen, erstellen Sie eine neue C#-Klasse implementiert die ```IPlugIn``` -Schnittstelle aus der ```Microsoft.ManagementExperience.FeatureInterfaces``` Namespace.  

> [!NOTE]
> Die ```IFeature``` Schnittstelle, die in früheren Versionen des SDK verfügbar, wird jetzt als veraltet gekennzeichnet.  Alle Gateway-Plug-in Entwicklung sollten IPlugIn (oder optional die abstrakte HttpPlugIn-Klasse) verwenden.

### Beispiel von GitHub herunterladen

Um schnell mit einer benutzerdefinierten Gateway-Plug-in beginnen möchten, können Sie Klonen oder Herunterladen einer Kopie des unser [Beispiel c#-Plug-in-Projekt](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) auf unserer Windows Admin Center SDK- [GitHub-Website](https://aka.ms/wacsdk).

### Hinzufügen von Inhalten

Fügen Sie neue Inhalte auf Ihrer geklonte Kopie des Projekts [Beispielprojekt c#-Plug-in](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) (oder Ihr Projekt) Ihrer benutzerdefinierten APIs enthalten, und erstellen Sie dann Ihre benutzerdefinierte Gateway-Plug-in-DLL-Datei in den nächsten Schritten verwendet werden.

### Bereitstellen für Tests-Plug-in

Testen Sie Ihre benutzerdefinierte Gateway-Plug-in DLL-Datei, indem Sie in Windows Admin Center Gateway-Prozess geladen.

Windows Admin Center sucht alle-Plug-Ins in einer ```plugins``` Ordner im Ordner "Anwendungsdaten" des aktuellen Computers (mit den CommonApplicationData-Wert, der der Environment.SpecialFolder-Enumeration). Unter Windows 10 dieser Speicherort ist ```C:\ProgramData\Server Management Experience```.  Wenn die ```plugins``` Ordner noch nicht vorhanden ist, den Ordner selbst erstellen.

> [!NOTE]
> Sie können den Speicherort-Plug-in in einem Debugbuild überschreiben, durch die Aktualisierung des Konfigurationswertes "StaticsFolder". Wenn Sie lokal testen, ist diese Einstellung in App.Config der Desktop-Lösung. 

Fügen Sie im Ordner-Plug-Ins (in diesem Beispiel ```C:\ProgramData\Server Management Experience\plugins```)

* Erstellen Sie einen neuen Ordner mit dem gleichen Namen wie die ```Name``` Eigenschaftswerte der der ```Feature``` in Ihrer benutzerdefinierten Gateway-Plug-in DLL-Datei (in unserem Beispiel-Projekt die ```Name``` ist "Beispiel Uno")
* Kopieren Sie Ihre benutzerdefinierte Gateway-Plug-in-DLL-Datei in diesem neuen Ordner
* Starten des Windows Admin Center-Prozess

Nach dem Neustart des Windows Admin-Prozesses Sie kann auf die APIs in Ihrer benutzerdefinierten Gateway-Plug-in DLL Übung ausgegeben einen GET PLATZIEREN, Patches, löschen oder zu ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```

### Optional: Zuordnen Sie-Plug-In für das Debuggen

Wählen Sie in Visual Studio 2017 im Debuggermenü "An den Prozess anhängen" aus. Scrollen Sie im nächsten Fenster durch die Liste Verfügbare Prozesse wählen Sie SMEDesktop.exe, und klicken Sie auf "Einfügen". Einmal können der Debugger gestartet wird, Sie einen Haltepunkt in Ihrem Featurecode und dann Übung über die oben genannten URL-Format platzieren. Unser Beispiel-Projekt (Featurename: "Beispiel Uno") die URL lautet: "http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno"

## Erstellen einer Tool-Erweiterungs mit der Windows Admin Center-CLI ##

Nun müssen wir eine Tool-Erweiterung erstellen, aus der Sie Ihre benutzerdefinierte Gateway-Plug-in aufrufen können.  Erstellen Sie, oder navigieren Sie zu einem Ordner, in denen Sie Ihre Projektdateien speichern, öffnen Sie ein Eingabeaufforderungsfenster und diesen Ordner als das Arbeitsverzeichnis festlegen möchten.  Verwenden die Windows Admin Center-CLI, das bereits installiert wurde, erstellen Sie eine neue Erweiterung mit folgender Syntax:

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

## Schließen Sie die Tool-Erweiterung an Ihre benutzerdefinierte Gateway-Plug-in

Nun, da Sie eine Erweiterung mit dem Windows Admin Center-CLI erstellt haben, können Sie die Tool-Erweiterung Ihrer benutzerdefinierten Gateway-Plug-in, Herstellen einer Verbindung folgendermaßen vor:

- Fügen Sie ein [leeres Modul](guides\add-module.md)
- Verwenden Sie Ihr [benutzerdefiniertes Gateway-Plug-in](guides\use-custom-gateway-plugin.md) in der Tool-Erweiterung
 
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