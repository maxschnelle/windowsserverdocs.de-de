---
title: Vorbereiten der Entwicklungsumgebung
description: Vorbereiten der Entwicklungs-Umgebung Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.prod: windows-server
ms.openlocfilehash: 136107210d2a8a4b336c9e4eb809e2ca096bfba2
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269217"
---
# <a name="prepare-your-development-environment"></a>Vorbereiten der Entwicklungsumgebung

>Gilt für: Windows Admin Center, Windows Admin Center Vorschau

Beginnen wir mit der Entwicklung von Erweiterungen mit dem Windows Admin Center SDK!  In diesem Dokument wird der Prozess behandelt, mit dem Sie Ihre Umgebung einrichten und eine Erweiterung für Windows Admin Center erstellen und testen können.

> [!NOTE]
> Neue Windows Admin Center SDK?  Erfahren Sie mehr über [Erweiterungen für Windows Admin Center](extensibility-overview.md)

Zur Vorbereitung Ihrer Entwicklungsumgebung, führen Sie die folgenden Schritte aus:

## <a name="install-prerequisites"></a>Voraussetzungen installieren

Zunächst bei der Entwicklung mit dem SDK herunter, und installieren Sie die folgenden Komponenten:

* [Windows Admin Center](https://aka.ms/WACDownloadPage) (GA-oder Vorschauversion)
* Visual Studio oder [Visual Studio Code](https://code.visualstudio.com)
* [Node. js](https://nodejs.org/en/download/releases/) (Version 10.3.0)
* [Knoten Paket-Manager](https://npmjs.com/get-npm) (8.12.0 oder höher)
* [NuGet](https://www.nuget.org/downloads) (zum Veröffentlichen von Erweiterungen)

> [!NOTE]
> Sie müssen zum Installieren und Windows Admin Center im Dev-Modus, um die folgenden Schritte ausführen. Dev Modus ermöglicht Windows Admin Center nicht signierte Erweiterung Pakete geladen werden. Das Windows Admin Center kann nur im Entwicklungsmodus auf einem Windows 10-Computer installiert werden. 
>
>  Installieren Sie zum Aktivieren des Dev Modus Windows Admin Center über die Befehlszeile mit dem Parameter DEV_MODE = 1. Im folgenden Beispiel ersetzen ```<version>``` mit der Version, die Sie, d. h. installieren ```WindowsAdminCenter1809.msi```.
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## <a name="install-global-dependencies"></a>Installieren von globalen Abhängigkeiten

Installieren oder aktualisieren Sie anschließend die Abhängigkeiten, die für Ihre Projekte erforderlich sind, mit dem Knoten Paket-Manager. Diese Abhängigkeiten werden global installiert und werden für alle Projekte verfügbar sein.

```
npm install -g npm

npm install -g @angular/cli@7.1.2

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>Sie können eine spätere Version von @angular/cliinstallieren. Beachten Sie jedoch, dass bei der Installation einer höheren Version als "7.1.2" während des Gulp-Buildschritts eine Warnung angezeigt wird, dass die lokale CLI-Version nicht mit der installierten Version identisch ist.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie Ihre Umgebung vorbereitet haben, können Sie nun mit dem Erstellen von Inhalten beginnen.

- Erstellen Sie eine Erweiterung [tool](develop-tool.md)
- Erstellen Sie eine [Lösung](develop-solution.md) -Erweiterung
- Erstellen Sie ein [Gateway-Plug-in](develop-gateway-plugin.md)
- Weitere Informationen finden Sie mit unserem [Führungslinien](guides.md)

## <a name="sdk-design-toolkit"></a>SDK-Entwurfs-Toolkit

Sehen Sie sich unser Windows Admin Center [SDK Design Toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)an! Dieses Toolkit soll Ihnen helfen, Erweiterungen in PowerPoint mithilfe von Windows Admin Center-Stilen,-Steuerelementen und-Seitenvorlagen schnell zu bereinigen. Sehen Sie sich an, wie Ihre Erweiterung im Windows Admin Center aussehen kann, bevor Sie mit dem Programmieren beginnen!

