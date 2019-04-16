---
title: Ändern des Stammnavigationsverhaltens
description: Entwickeln Sie eine lösungserweiterung Windows Admin Center SDK (Projekt Honolulu) - Stamm-Navigationsverhalten ändern
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4a5cba228aa3a0afed99c0d853c3720a5b46f650
ms.sourcegitcommit: 546229d6b5fa7e16f725c6c35f4dcc272711b811
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2018
ms.locfileid: "4905040"
---
# Ändern der Stamm Navigationsverhalten für eine lösungserweiterung

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

In diesem Handbuch erfahren wir so ändern Sie das Verhalten der Stammzertifizierungsstelle für Ihre Lösung andere Verbindung Liste Verhalten aufweisen als auch so ein- oder Ausblenden der Liste der Tools.

## Ändern der Stamm Navigationsverhalten

Öffnen Sie manifest.json Datei in {Erweiterung Stamm} \src, und suchen Sie die Eigenschaft "RootNavigationBehavior". Diese Eigenschaft verfügt über zwei gültige Werte: "Verbindungen" oder "Path". Das Verhalten "Verbindungen" ist in der Dokumentation ausführlich beschrieben.

### Festlegen des Pfades als eine rootNavigationBehavior

Legen Sie den Wert der ```rootNavigationBehavior``` auf ```path```, und löschen Sie dann die ```requirements``` , und lassen Sie die ```path``` -Eigenschaft, wie eine leere Zeichenfolge. Die minimale erforderliche Konfiguration, um eine lösungserweiterung erstellen abgeschlossen haben. Speichern Sie die Datei, und schlucken Build -> schlucken dienen als Sie ein Tool, und klicken Sie dann Seite die Erweiterung in der lokalen Windows Admin Center-Erweiterung laden würde.

Ein Array gültige manifest EntryPoints sieht wie folgt aus:
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

Mit dieser Art von Struktur integrierten Tools werden nicht erforderliche Verbindungen zu laden, aber keine Knoten-Konnektivität Funktionen entweder.

### Festlegen von Verbindungen als eine rootNavigationBehavior

Bei Festlegung der ```rootNavigationBehavior``` -Eigenschaft verwenden, um ```connections```, Sie sind die Windows Admin Center-Shell mitgeteilt wird, dass es werden ein verbundener Knoten (immer ein Server eines Typs), die eine Verbindung hergestellt werden soll und den Verbindungsstatus überprüfen. Mit dieser Option gibt es 2 Schritte bei der Überprüfung der Verbindung. 1) Windows Admin Center wird versuchen, einen Versuch, den Knoten mit Ihren Anmeldeinformationen (für das Einrichten der remote-PowerShell-Sitzung) anmelden, und 2) führt das PowerShell-Skript, das Sie bereitstellen, um festzustellen, ob der Knoten in einem verbindbaren Zustand befindet.

Eine gültige Lösung Definition mit Verbindungen sieht wie folgt aus:

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

Wenn die RootNavigationBehavior "Verbindungen" festgelegt ist müssen Sie die Verbindungen Definition im Manifest erstellen. Dazu gehören die "" Headereigenschaft (wird verwendet, um in Ihrer Projektmappe Kopfzeile anzuzeigen, wenn einem Benutzer aus dem Menü "ausgewählt), ein ConnectionTypes Array (Dies wird angeben, welche ConnectionTypes in der Lösung verwendet werden. Mehr auf, die in der Dokumentation zu ConnectionProvider.).

## Aktivieren und deaktivieren das Menü "Extras" ##

Eine andere Eigenschaft verfügbar in der Definition der Lösung ist die Eigenschaft "Tools". Dies wird diktieren, wenn das Menü "Extras", sowie das Tool angezeigt wird, die geladen werden. Wenn aktiviert, wird Windows Admin Center das linke Menü "Extras" gerendert. Mit DefaultTool, ist es erforderlich, dass Sie ein Tool Einstiegspunkt und das Manifest hinzufügen, um die entsprechenden Ressourcen zu laden. Der Wert "DefaultTool" muss die Eigenschaft "Name" des Tools sein, da es im Manifest definiert ist.
