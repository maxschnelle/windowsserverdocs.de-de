---
title: Ändern des Stammnavigationsverhaltens
description: Entwickeln einer Lösung Erweiterungs Windows Admin Center-SDK (Projekt Honolulu) – ändern Sie die Stamm-Navigationsverhalten
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4a5cba228aa3a0afed99c0d853c3720a5b46f650
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861731"
---
# <a name="modify-root-navigation-behavior-for-a-solution-extension"></a>Ändern Sie die Stamm-Navigationsverhalten für eine projektmappenerweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In diesem Handbuch erfahren Sie, wie so ändern Sie das Root-Navigationsverhalten für Ihre Lösung unterschiedliche Liste Verbindungsverhalten haben und wie auf Sie ein- oder Ausblenden der Liste der Tools.

## <a name="modifying-root-navigation-behavior"></a>Ändern die Stamm-Navigationsverhalten

Öffnen Sie die Datei "Manifest.JSON" in {erweiterungsstamm} \src, und suchen Sie die Eigenschaft "RootNavigationBehavior". Diese Eigenschaft verfügt über zwei gültige Werte: "Verbindungen" oder "Path". Das Verhalten von "Verbindungen" wird weiter unten in der Dokumentation beschrieben.

### <a name="setting-path-as-a-rootnavigationbehavior"></a>Festlegen des Pfades als eine rootNavigationBehavior

Legen Sie den Wert der ```rootNavigationBehavior``` zu ```path```, und löschen Sie dann die ```requirements``` , und lassen Sie die ```path``` Eigenschaft als leere Zeichenfolge. Sie haben die erforderliche Minimalkonfiguration um eine projektmappenerweiterung zu erstellen. Speichern Sie die Datei, und Gulp-Build -> Gulp dienen, wie Sie ein Tool, und klicken Sie dann Seite die Erweiterung in Ihre lokalen Windows Admin Center-Extension geladen würde.

Ein Array von gültigen manifest EntryPoints sieht folgendermaßen aus:
```
    "entryPoints": [
        {
          "entryPointType": "solution",
          "name": "main",
          "urlName": "testsln",
          "displayName": "resources:strings:displayName",
          "description": "resources:strings:description",
          "icon": "sme-icon:icon-win-powerShell",
          "path": "",
          "rootNavigationBehavior": "path"
        }
    ],
```

Tools, die mit dieser Art von Struktur erstellt werden, nicht erforderliche Verbindungen zu laden, aber keine Funktion für Knoten Verbindungen entweder.

### <a name="setting-connections-as-a-rootnavigationbehavior"></a>Verbindungen werden als eine RootNavigationBehavior festgelegt.

Beim Festlegen der ```rootNavigationBehavior``` Eigenschaft ```connections```, veranlassen Sie, dass die Windows Admin Center-Shell ist, dass es ein verbundenen Knoten (immer ein Server eines bestimmten Typs), der eine Verbindung hergestellt werden soll, und Überprüfen des Verbindungsstatus. Mit dieser Option sind 2 Schritte bei der Überprüfung der Verbindung. (1) Windows Admin Center versucht, stellen auf den Knoten mit Ihren Anmeldeinformationen (für das Herstellen der PowerShell-Remotesitzung) anmelden, und (2) führt das PowerShell-Skript, das Sie bereitstellen, um zu ermitteln, ob der Knoten in einem verbindungsfähigen Zustand befindet.

Eine gültige lösungsdefinition mit Verbindungen wird wie folgt aussehen:

``` json
        {
          "entryPointType": "solution",
          "name": "example",
          "urlName": "solutionexample",
          "displayName": "resources:strings:displayName",
          "description": "resources:strings:description",
          "icon": "sme-icon:icon-win-powerShell",
          "rootNavigationBehavior": "connections",
          "connections": {
            "header": "resources:strings:connectionsListHeader",
            "connectionTypes": [
                "msft.sme.connection-type.example"
                ]
            },
            "tools": {
                "enabled": false,
                "defaultTool": "solution"
            }
        },
```

Wenn die RootNavigationBehavior auf "Verbindungen" festgelegt ist, müssen Sie erstellen Sie die Definition der Verbindungen im Manifest. Dazu gehören die "Header"-Eigenschaft (wird verwendet, die in Ihrer Lösung Kopfzeile angezeigt werden soll, wenn ein Benutzer im Menü ausgewählt), ein ConnectionTypes Array (Dadurch wird angeben welche ConnectionTypes in der Projektmappe verwendet werden. Weitere Informationen, die in der Dokumentation für die ConnectionProvider-.).

## <a name="enabling-and-disabling-the-tools-menu"></a>Aktivieren und deaktivieren das Menü "Extras" ##

Eine andere Eigenschaft, die in der Definition der Projektmappe verfügbar ist, die Eigenschaft "Tools". Diese bestimmen, wenn das Menü "Extras", und das Tool angezeigt wird, die geladen werden. Wenn aktiviert, wird Windows Admin Center im Menü Extras Links gerendert. DefaultTool, ist es erforderlich, dass Sie einen Tool Einstiegspunkt zum Manifest hinzufügen, um die entsprechenden Ressourcen zu laden. Der Wert "DefaultTool" muss die Eigenschaft "Name" des Tools werden, da dieser im Manifest definiert wurde.
