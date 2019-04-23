---
title: Vorbereiten der Entwicklungsumgebung
description: Vorbereiten der Entwicklungs-Umgebung Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.prod: windows-server-threshold
ms.openlocfilehash: 7b1a0672ee374f3e2d1339c43576db0e5cabdc36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834761"
---
# <a name="prepare-your-development-environment"></a>Vorbereiten der Entwicklungsumgebung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Steigen wir Entwicklung Erweiterungen mit dem Windows Admin Center SDK!  In diesem Dokument wird das Verfahren zum Abrufen Ihrer Umgebung einrichten und ausführen, die zum Erstellen und testen eine Erweiterung für Windows Admin Center behandelt.

> [!NOTE]
> Neue Windows Admin Center SDK?  Erfahren Sie mehr über [Erweiterungen für Windows Admin Center](extensibility-overview.md)

Zur Vorbereitung Ihrer Entwicklungsumgebung, führen Sie die folgenden Schritte aus:

## <a name="install-prerequisites"></a>Installation vorab erforderlicher Komponenten

Zunächst bei der Entwicklung mit dem SDK herunter, und installieren Sie die folgenden Komponenten:

* [Windows Admin Center](https://aka.ms/WACDownloadPage) (bei allgemeiner Verfügbarkeit oder die Preview-Version)
* Visual Studio oder [Visual Studio Code](http://code.visualstudio.com)
* [Node Package Manager](https://npmjs.com/get-npm) (8.12.0 oder höher)
* [NuGet](https://www.nuget.org/downloads) (zum Veröffentlichen von Erweiterungen)

> [!NOTE]
> Sie müssen zum Installieren und Windows Admin Center im Dev-Modus, um die folgenden Schritte ausführen. Dev Modus ermöglicht Windows Admin Center nicht signierte Erweiterung Pakete geladen werden.
>
>  Installieren Sie zum Aktivieren des Dev Modus Windows Admin Center über die Befehlszeile mit dem Parameter DEV_MODE = 1. Im folgenden Beispiel ersetzen ```<version>``` mit der Version, die Sie, d. h. installieren ```WindowsAdminCenter1809.msi```.
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## <a name="install-global-dependencies"></a>Installieren Sie die globale Abhängigkeiten

Als Nächstes installieren oder Aktualisieren von Abhängigkeiten für Ihre Projekte, mit Node Package Manager erforderlich sind. Diese Abhängigkeiten werden global installiert und werden für alle Projekte verfügbar sein.

```
npm install -g npm

npm install -g @angular/cli@1.6.5

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>Sie können eine höhere Version von installieren @angular/cli, aber möglich, wenn Sie eine Version, die größer als 1.6.5 installieren, während des Gulp-Buildschritts eine Warnung Sie erhalten, dass die lokale Cli-Version die installierte Version nicht übereinstimmt.

## <a name="next-steps"></a>Nächste Schritte

Nun, dass Ihre Umgebung vorbereitet ist, können Sie Inhalte erstellen.

- Erstellen Sie eine Erweiterung [tool](develop-tool.md)
- Erstellen Sie eine [Lösung](develop-solution.md) -Erweiterung
- Erstellen Sie ein [Gateway-Plug-in](develop-gateway-plugin.md)
- Weitere Informationen finden Sie mit unserem [Führungslinien](guides.md)

## <a name="sdk-design-toolkit"></a>SDK-Design-toolkit

Sehen Sie sich unsere Windows Admin Center [SDK Entwurf Toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)! Dieses Toolkit wurde entwickelt, können Sie die Erweiterungen in PowerPoint – Dank Windows Admin Center Stile, Steuerelemente und Seitenvorlagen schnell zu modellieren. Erfahren Sie, wie die Erweiterung in Windows Admin Center aussehen kann vor dem Programmieren!

