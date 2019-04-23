---
title: Entwickeln eines Gateway-Plug-Ins
description: Entwickeln Sie ein Plug-In für Gateway-SDK für Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93cee5b8e3611a264119947103d22d9aa3b9a56b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834391"
---
# <a name="develop-a-gateway-plugin"></a>Entwickeln eines Gateway-Plug-Ins

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Eine Windows Admin Center-Gateway-Plug-in kann API-Kommunikation über die Benutzeroberfläche des Tools oder der Projektmappe mit einem Zielknoten.  Windows Admin Center hostet einen Gatewaydienst, der Befehle und Skripts von Gateway-Plug-Ins auf den Zielknoten ausgeführt werden, überträgt. Der Gateway-Dienst kann erweitert werden, um benutzerdefiniertes Gateway-Plug-Ins enthalten, die Protokolle als die Standardfarben zu unterstützen.

Diese Gateway-Plug-Ins sind standardmäßig mit Windows Admin Center enthalten:

* PowerShell-Gateway-Plug-in
* WMI-Gateway-Plug-in

Wenn Sie, für die Kommunikation mit dem ein anderes Protokoll als PowerShell oder WMI möchten können z. B. mit REST Sie Ihren eigenen Gateway-Plug-in erstellen.  Gateway-Plug-Ins in einer separaten AppDomain aus der vorhandenen Gatewayprozess geladen, aber der gleichen Ebene wie die Erhöhung für Rechte.

> [!NOTE]
> Sie sind nicht mit anderen Erweiterungstypen vertraut? Erfahren Sie mehr über die [Erweiterbarkeit Architektur und die Erweiterung Typen](understand-extensions.md).

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie nicht bereits geschehen, [Vorbereiten der Umgebung](prepare-development-environment.md) durch die Installation von Abhängigkeiten und globale Voraussetzungen für alle Projekte.

## <a name="create-a-gateway-plugin-c-library"></a>Erstellen Sie einen Gateway-Plug-in (C# Bibliothek)

Um ein benutzerdefiniertes Gateway-Plug-in zu erstellen, erstellen Sie ein neues C# Klasse, die implementiert die ```IPlugIn``` -Schnittstelle aus der ```Microsoft.ManagementExperience.FeatureInterfaces``` Namespace.  

> [!NOTE]
> Die ```IFeature``` Schnittstelle, die in früheren Versionen des SDK verfügbar, wird jetzt als veraltet gekennzeichnet.  Alle Gateway-Plug-in Development sollten IPlugIn (oder optional die abstrakte HttpPlugIn-Klasse) verwenden.

### <a name="download-sample-from-github"></a>Beispiel von GitHub herunterladen

Um schnell mit einem benutzerdefinierten Gateway-Plug-in zu beginnen, können Sie Klonen oder Herunterladen der eine Kopie des unsere [Beispiel C# -Plug-in-Projekt](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) aus unserem Windows Admin Center-SDK [GitHub-Website](https://aka.ms/wacsdk).

### <a name="add-content"></a>Fügen Sie Inhalt hinzu

Neue Inhalte hinzufügen, um die geklonte Kopie der [Beispiel C# -Plug-in-Projekt](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) Projekts (oder Ihres eigenen Projekts verwenden), Ihre benutzerdefinierten APIs enthalten, und erstellen Ihr benutzerdefiniertes Gateway Plug-in-DLL-Datei, um in den nächsten Schritten verwendet werden.

### <a name="deploy-plugin-for-testing"></a>Bereitstellen von-Plug-In für Tests

Testen Sie Ihr benutzerdefiniertes Gateway Plug-in-DLL, indem Sie laden in Windows Admin Center-Gatewayprozess.

Windows Admin Center sucht alle Plug-Ins in einer ```plugins``` Ordner im Ordner "Anwendungsdaten" des aktuellen Computers (mithilfe den CommonApplicationData-Wert, der der Environment.SpecialFolder-Enumeration). Unter Windows 10 ist der Speicherort dieses ```C:\ProgramData\Server Management Experience```.  Wenn die ```plugins``` Ordner noch nicht vorhanden ist, Sie können den Ordner selbst erstellen.

> [!NOTE]
> Sie können den Speicherort des Plug-Ins in einem Debugbuild überschreiben, indem Sie den Konfigurationswert "StaticsFolder" aktualisieren. Wenn Sie lokal debuggen, können Sie diese Einstellung in "App.config" der Desktop-Lösung ist. 

In den Ordner "Plug-Ins" (in diesem Beispiel ```C:\ProgramData\Server Management Experience\plugins```)

* Erstellen Sie einen neuen Ordner mit dem gleichen Namen wie die ```Name``` Eigenschaftswert, der die ```Feature``` in Ihr benutzerdefiniertes Gateway Plug-in-DLL (in unserem Beispielprojekt die ```Name``` ist "Beispiel Uno")
* Kopieren Sie Ihr benutzerdefiniertes Gateway-Plug-in-DLL-Datei in diesen neuen Ordner
* Starten Sie den Windows Admin Center-Prozess

Nachdem die Windows-Admin-Prozess neu gestartet wird, Sie werden so führen Sie die APIs in Ihr benutzerdefiniertes Gateway Plug-in-DLL aus, durch das Ausgeben eines GET, PUT, PATCH, DELETE oder in Posten ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```

### <a name="optional-attach-to-plugin-for-debugging"></a>Optional: Fügen Sie-Plug-In für das Debuggen

Wählen Sie in Visual Studio 2017 klicken Sie im Menü "Debuggen" "An den Prozess anhängen" ein. Im nächsten Fenster einen Bildlauf durch die Liste Verfügbare Prozesse SMEDesktop.exe auswählen, und klicken Sie auf "Anfügen". Einmal können der Debugger gestartet wird, Sie einen Haltepunkt im Code der Funktion und dann Übung über die obige URL-Format platzieren. Für unser Beispielprojekt (Name des Features: "Beispiel Uno") die URL lautet: "http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno"

## <a name="create-a-tool-extension-with-the-windows-admin-center-cli"></a>Erstellen Sie eine toolerweiterung, mit der Windows Admin Center-CLI ##

Nun müssen wir eine Tools-Erweiterung zu erstellen, von der Sie Ihr benutzerdefiniertes Gateway-Plug-in aufrufen können.  Erstellen Sie, oder navigieren Sie zu einem Ordner, in dem Speicherort der Projektdateien, eine Eingabeaufforderung öffnen und diesen Ordner als Arbeitsverzeichnis festgelegt werden soll.  Erstellen Sie eine neue Erweiterung verwenden die Windows Admin Center-CLI, die zuvor installiert wurde, mit der folgenden Syntax aus:

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

Dies erstellt einen neuen Ordner in das aktuelle Arbeitsverzeichnis, das mit dem Namen, den Sie für Ihr Tool angegeben, kopiert alle erforderlichen Vorlagendateien in Ihr Projekt und die Dateien durch den Namen Ihres Unternehmens und das Tool konfiguriert.  

Als Nächstes wechseln Sie zu dem Ordner, der gerade erstellt haben, und installieren Sie erforderliche lokale Abhängigkeiten zu, indem Sie den folgenden Befehl ausführen:

```
npm install
```

Sobald dies abgeschlossen ist, haben Sie alles, was einrichten, die Sie die neue Erweiterung in Windows Admin Center zu laden müssen. 

## <a name="connect-your-tool-extension-to-your-custom-gateway-plugin"></a>Verbinden Sie Ihre toolerweiterung Ihr benutzerdefiniertes Gateway-Plug-in

Nun, dass Sie eine Erweiterung mit der Windows Admin Center-CLI erstellt haben, können Sie Ihre toolerweiterung zu Ihrem Plug-in benutzerdefiniertes Gateway verbinden, mit folgenden Schritten:

- Hinzufügen einer [leere-Modul](guides\add-module.md)
- Verwenden Ihrer [benutzerdefiniertes Gateway-Plug-Ins](guides\use-custom-gateway-plugin.md) in Ihrer Tools-Erweiterung
 
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