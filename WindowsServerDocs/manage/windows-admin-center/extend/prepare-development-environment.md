---
title: Vorbereiten Ihrer Entwicklungsumgebung
description: Vorbereiten der Entwicklungsumgebung Windows Admin Center SDK (Projekt Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.openlocfilehash: 09d39aa027adf360c339da434b16038a3b8e5c90
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964596"
---
# <a name="prepare-your-development-environment"></a>Vorbereiten Ihrer Entwicklungsumgebung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Beginnen wir mit der Entwicklung von Erweiterungen mit dem Windows Admin Center SDK!  In diesem Dokument wird der Prozess behandelt, mit dem Sie Ihre Umgebung einrichten und eine Erweiterung für Windows Admin Center erstellen und testen können.

> [!NOTE]
> Neu beim Windows Admin Center SDK?  Weitere Informationen zu [Erweiterungen für Windows Admin Center](extensibility-overview.md)

Führen Sie die folgenden Schritte aus, um Ihre Entwicklungsumgebung vorzubereiten:

## <a name="install-prerequisites"></a>Installieren der erforderlichen Komponenten

Zum Einstieg in die Entwicklung mit dem SDK müssen Sie die folgenden Voraussetzungen herunterladen und installieren:

* [Windows Admin Center](https://aka.ms/WACDownloadPage) (GA-oder Vorschauversion)
* Visual Studio oder [Visual Studio Code](https://code.visualstudio.com)
* [Node.js](https://nodejs.org/en/download/releases/) (Version 10.3.0)
* [Knoten Paket-Manager](https://npmjs.com/get-npm) (8.12.0 oder höher)
* [Nuget](https://www.nuget.org/downloads) (zum Veröffentlichen von Erweiterungen)

> [!NOTE]
> Sie müssen das Windows Admin Center im Entwicklungsmodus installieren und ausführen, um die folgenden Schritte ausführen zu können. Der Entwicklungsmodus ermöglicht Windows Admin Center das Laden von nicht signierten Erweiterungs Paketen. Das Windows Admin Center kann nur im Entwicklungsmodus auf einem Windows 10-Computer installiert werden.
>
>  Um den Entwicklungsmodus zu aktivieren, installieren Sie das Windows Admin Center über die Befehlszeile mit dem Parameter DEV_MODE = 1. Ersetzen Sie im folgenden Beispiel ```<version>``` durch die Version, die Sie installieren, z. b. ```WindowsAdminCenter1809.msi``` .
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## <a name="install-global-dependencies"></a>Installieren von globalen Abhängigkeiten

Installieren oder aktualisieren Sie anschließend die Abhängigkeiten, die für Ihre Projekte erforderlich sind, mit dem Knoten Paket-Manager. Diese Abhängigkeiten werden global installiert und sind für alle Projekte verfügbar.

```
npm install -g npm

npm install -g @angular/cli@7.1.2

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>Sie können eine neuere Version von installieren. Beachten @angular/cli Sie jedoch, dass bei der Installation einer höheren Version als "7.1.2" während des Gulp-Buildschritts eine Warnung angezeigt wird, dass die lokale CLI-Version nicht mit der installierten Version identisch ist.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie Ihre Umgebung vorbereitet haben, können Sie nun mit dem Erstellen von Inhalten beginnen.

- Erstellen einer [Tool](develop-tool.md) Erweiterung
- Erstellen einer [solution](develop-solution.md) projektmappenerweiterung
- Erstellen eines [Gateway-Plug](develop-gateway-plugin.md) -ins
- Weitere Informationen finden Sie in unseren [Leitfäden](guides.md)

## <a name="sdk-design-toolkit"></a>SDK-Entwurfs-Toolkit

Sehen Sie sich unser Windows Admin Center [SDK Design Toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)an! Dieses Toolkit soll Ihnen helfen, Erweiterungen in PowerPoint mithilfe von Windows Admin Center-Stilen,-Steuerelementen und-Seitenvorlagen schnell zu bereinigen. Sehen Sie sich an, wie Ihre Erweiterung im Windows Admin Center aussehen kann, bevor Sie mit dem Programmieren beginnen!

