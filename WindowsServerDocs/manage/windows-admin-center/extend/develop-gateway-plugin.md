---
title: Entwickeln eines Gateway-Plug-Ins
description: Entwickeln eines Gateway-Plug-ins Windows Admin Center SDK (Projekt Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 428f40abf050e87cf88d536b18254e6c20b51fa3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949624"
---
# <a name="develop-a-gateway-plugin"></a>Entwickeln eines Gateway-Plug-Ins

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Ein Windows Admin Center Gateway-Plug-in ermöglicht die API-Kommunikation über die Benutzeroberfläche des Tools oder der Lösung mit einem Zielknoten.  Windows Admin Center hostet einen Gatewaydienst, der Befehle und Skripts von gatewayplug-ins überträgt, die auf Zielknoten ausgeführt werden. Der Gatewaydienst kann erweitert werden, um benutzerdefinierte Gateway-Plug-ins einzubeziehen, die andere Protokolle als die Standardeinstellungen unterstützen.

Diese Gateway-Plug-ins sind standardmäßig im Windows Admin Center enthalten:

* PowerShell Gateway-Plug-in
* WMI Gateway-Plug-in

Wenn Sie mit einem anderen Protokoll als PowerShell oder WMI (z. b. mit Rest) kommunizieren möchten, können Sie ein eigenes Gateway-Plug-in erstellen.  Gateway-Plug-ins werden aus dem vorhandenen Gatewayprozess in eine separate AppDomain geladen, verwenden jedoch die gleiche Berechtigungsstufe für Rechte.

> [!NOTE]
> Sie sind mit den unterschiedlichen Erweiterungs Typen nicht vertraut? Erfahren Sie mehr über die [Erweiterbarkeits Architektur und die Erweiterungs Typen](understand-extensions.md).

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie dies noch nicht getan haben, [bereiten Sie Ihre Umgebung](prepare-development-environment.md) vor, indem Sie die Abhängigkeiten und globalen Voraussetzungen für alle Projekte installieren.

## <a name="create-a-gateway-plugin-c-library"></a>Erstellen eines Gateway-Plug-ins (c#-Bibliothek)

Zum Erstellen eines benutzerdefinierten Gateway-Plug-ins erstellen Sie eine neue c#-Klasse, die die- ```IPlugIn``` Schnittstelle aus dem- ```Microsoft.ManagementExperience.FeatureInterfaces``` Namespace implementiert

> [!NOTE]
> Die ```IFeature``` in früheren Versionen des SDK verfügbare Schnittstelle ist nun als veraltet gekennzeichnet.  Für alle gatewayplug-in-Entwicklungen sollte IPlugin (oder optional die abstrakte httpplugin-Klasse) verwendet werden.

### <a name="download-sample-from-github"></a>Beispiel von GitHub herunterladen

Um schnell mit einem benutzerdefinierten Gateway-Plug-in zu beginnen, können Sie eine Kopie des [c#-Plug](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) -in-Beispielprojekts von der [GitHub-Website](https://aka.ms/wacsdk)des Windows Admin Center SDK Klonen oder herunterladen.

### <a name="add-content"></a>Inhalt hinzufügen

Fügen Sie Ihrer geklonten Kopie des [c#-Plug](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin) -in-projektprojekts (oder Ihres eigenen Projekts) neuen Inhalt hinzu, um Ihre benutzerdefinierten APIs aufzunehmen, und erstellen Sie dann die benutzerdefinierte Gateway-Plug-in-DLL-Datei, die in den nächsten Schritten

### <a name="deploy-plugin-for-testing"></a>Plug-in zum Testen bereitstellen

Testen Sie Ihre benutzerdefinierte Gateway-Plug-in-dll durch Laden in den Windows Admin Center

Das Windows Admin Center sucht in einem ```plugins``` Ordner im Ordner Anwendungsdaten des aktuellen Computers nach allen Plug-ins (mit dem CommonApplicationData-Wert der Environment. SpecialFolder-Enumeration). Unter Windows 10 ist dieser Speicherort ```C:\ProgramData\Server Management Experience``` .  Wenn der ```plugins``` Ordner noch nicht vorhanden ist, können Sie den Ordner selbst erstellen.

> [!NOTE]
> Sie können den Speicherort des Plug-ins in einem Debugbuild überschreiben, indem Sie den Konfigurations Wert "staticsfolder" aktualisieren. Wenn Sie lokal debuggen, befindet sich diese Einstellung im App.Config der Desktop Lösung.

Innerhalb des Plug-in-Ordners (in diesem Beispiel ```C:\ProgramData\Server Management Experience\plugins``` )

* Erstellen Sie einen neuen Ordner mit dem gleichen Namen wie der- ```Name``` Eigenschafts Wert von ```Feature``` in Ihrer benutzerdefinierten Gateway-Plug-in-dll (in unserem Beispiel Projekt ```Name``` ist "Sample UNO").
* Kopieren Sie die DLL-Datei für das benutzerdefinierte Gateway-Plugin in diesen neuen
* Windows Admin Center-Prozess neu starten

Nachdem der Windows-Administrator Prozess neu gestartet wurde, können Sie die APIs in Ihrer benutzerdefinierten Gateway-Plug-in-dll ausführen, indem Sie eine Get-, Put-, Patch-, DELETE-oder Post-Ausgabe für```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```

### <a name="optional-attach-to-plugin-for-debugging"></a>Optional: an das Plug-in zum Debuggen Anhängen

Wählen Sie in Visual Studio 2017 im Menü Debuggen die Option "an den Prozess anhängen" aus. Scrollen Sie im nächsten Fenster durch die Liste Verfügbare Prozesse, und wählen Sie SMEDesktop.exe aus, und klicken Sie dann auf Anfügen. Nachdem der Debugger gestartet wurde, können Sie einen Haltepunkt in Ihrem Featurecode platzieren und dann das obige URL-Format ausführen. Für das Beispiel Projekt (Funktionsname: "Beispiel-UNO") lautet die URL: " <http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno> "

## <a name="create-a-tool-extension-with-the-windows-admin-center-cli"></a>Erstellen einer Tool Erweiterung mit der Windows Admin Center-CLI ##

Nun müssen wir eine Tool Erweiterung erstellen, aus der Sie Ihr benutzerdefiniertes Gateway-Plug-in abrufen können.  Erstellen oder navigieren Sie zu einem Ordner, in dem Sie die Projektdateien speichern möchten, öffnen Sie eine Eingabeaufforderung, und legen Sie diesen Ordner als Arbeitsverzeichnis fest.  Erstellen Sie mithilfe der zuvor installierten Windows Admin Center-CLI eine neue Erweiterung mit der folgenden Syntax:

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| Wert | Erklärung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Name Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Ihr Toolname (mit Leerzeichen) | ```Manage Foo Works``` |

Beispiel zur Verwendung:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

Dadurch wird im aktuellen Arbeitsverzeichnis ein neuer Ordner mit dem Namen erstellt, den Sie für das Tool angegeben haben. alle erforderlichen Vorlagen Dateien werden in das Projekt kopiert, und die Dateien werden mit dem Namen Ihres Unternehmens und des Tools konfiguriert.

Wechseln Sie als nächstes das Verzeichnis in den soeben erstellten Ordner, und installieren Sie die erforderlichen lokalen Abhängigkeiten, indem Sie den folgenden Befehl ausführen:

```
npm install
```

Nachdem dieser Vorgang abgeschlossen ist, haben Sie alles eingerichtet, was Sie benötigen, um Ihre neue Erweiterung in das Windows Admin Center zu laden.

## <a name="connect-your-tool-extension-to-your-custom-gateway-plugin"></a>Verbinden Sie Ihre Tool Erweiterung mit Ihrem benutzerdefinierten Gateway-Plug-in

Nachdem Sie nun mit der Windows Admin Center-CLI eine Erweiterung erstellt haben, können Sie Ihre Tool Erweiterung mit Ihrem benutzerdefinierten Gateway-Plug-in verbinden, indem Sie die folgenden Schritte ausführen:

- Hinzufügen eines [leeren Moduls](guides/add-module.md)
- Verwenden des [benutzerdefinierten Gateway-Plug](guides/use-custom-gateway-plugin.md) -ins in ihrer Tool Erweiterung

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