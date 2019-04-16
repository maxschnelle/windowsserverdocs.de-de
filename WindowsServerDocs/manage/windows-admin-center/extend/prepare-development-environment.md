---
title: Die Umgebung weiter vorbereiten
description: Vorbereiten der Entwicklungs-Umgebung Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.prod: windows-server-threshold
ms.openlocfilehash: 7b1a0672ee374f3e2d1339c43576db0e5cabdc36
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080917"
---
# Die Umgebung weiter vorbereiten

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Steigen wir Entwicklung Erweiterungen mit dem Windows Admin Center SDK!  In diesem Dokument werden folgende Themen behandelt, das Verfahren zum Abrufen von Ihrer Umgebung und zum Erstellen und Testen einer Erweiterungs für das Windows Admin Center ausgeführt wird.

> [!NOTE]
> Neue Windows Admin Center SDK?  Erfahren Sie mehr über [Erweiterungen für Windows Admin Center](extensibility-overview.md)

Zur Vorbereitung Ihrer Entwicklungsumgebung, führen Sie die folgenden Schritte aus:

## Installation vorab erforderlicher Komponenten

Zunächst bei der Entwicklung mit dem SDK herunter, und installieren Sie die folgenden Komponenten:

* [Windows Admin Center](https://aka.ms/WACDownloadPage) (GA oder Preview-Version)
* Visual Studio oder [Visual Studio Code](http://code.visualstudio.com)
* [Knoten-Paket-Manager](https://npmjs.com/get-npm) (8.12.0 oder höher)
* [NuGet](https://www.nuget.org/downloads) (zum Veröffentlichen von Erweiterungen)

> [!NOTE]
> Sie müssen zum Installieren und Windows Admin Center im Dev-Modus, um die folgenden Schritte ausführen. Dev Modus ermöglicht Windows Admin Center nicht signierte Erweiterung Pakete geladen werden.
>
>  Installieren Sie zum Aktivieren des Dev Modus Windows Admin Center über die Befehlszeile mit dem Parameter DEV_MODE = 1. Im folgenden Beispiel ersetzen ```<version>``` mit der Version, die Sie, d. h. installieren ```WindowsAdminCenter1809.msi```.
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## Installieren von globalen Abhängigkeiten

Als Nächstes installieren oder Aktualisieren von Abhängigkeiten für Projekte, mit dem Knoten Package Manager erforderlich. Diese Abhängigkeiten werden global installiert und werden für alle Projekte verfügbar sein.

```
npm install -g npm

npm install -g @angular/cli@1.6.5

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>Sie installieren eine höhere Version des @angular/cli, aber beachten Sie, wenn Sie eine Version, die größer als 1.6.5 installieren, während die schlucken Buildschritt eine Warnung Sie erhalten, dass die lokalen Cli-Version nicht die installierte Version übereinstimmt.

## Nächste Schritte

Nun, da Ihre Umgebung vorbereitet haben, können Sie zum Erstellen von Inhalten.

- Erstellen Sie eine Erweiterung [tool](develop-tool.md)
- Erstellen Sie eine [Lösung](develop-solution.md) -Erweiterung
- Erstellen Sie ein [Gateway-Plug-in](develop-gateway-plugin.md)
- Weitere Informationen finden Sie mit unserem [Führungslinien](guides.md)

## SDK-Design-Toolkits

Sehen Sie sich unsere Windows Admin Center [SDK-Design-Toolkits](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)! Dieses Toolkit wurde entwickelt, mit denen Sie schnell von Erweiterungen in PowerPoint, die mit Windows Admin Center Stile, Steuerelemente und Vorlagen simulieren können. Finden Sie unter die Erweiterung in Windows Admin Center sehen kann, bevor Sie mit der Codierung beginnen!

