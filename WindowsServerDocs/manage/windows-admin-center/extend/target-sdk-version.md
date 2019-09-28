---
title: Eine andere Version des Windows Admin Center SDK als Zielversion
description: Eine andere Version des Windows Admin Center SDK (Project Honolulu) als Zielversion
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0d3b7af5229f7b8487aa9f04eaf0d1756d8c02f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356968"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Eine andere Version des Windows Admin Center SDK als Zielversion

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Es ist einfach, ihre Erweiterung mit SDK-Änderungen und Platt Formänderungen auf dem neuesten Stand zu halten.  Wir verwenden [NPM-Tags](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) , um die Veröffentlichung neuer Features in SDK-Versionen zu organisieren.

Es gibt drei SDK-Versionen, aus denen Sie auswählen können:

* ```latest``` – dieses SDK-Paket richtet sich nach der aktuellen GA-Version von Windows Admin Center.
* ```insider``` – dieses SDK-Paket richtet sich nach der aktuellen Vorschauversion von Windows Admin Center (verfügbar unter Windows Server Insider Preview).
* ```next``` – dieses SDK-Paket enthält die neuesten Funktionen.

> [!NOTE]
> Erfahren Sie mehr über die verschiedenen [Versionen](https://aka.ms/WACDownloadPage) von Windows Admin Center, die zum Herunterladen verfügbar sind.

## <a name="targeting-sdk-version-on-a-new-project"></a>Zielversion der SDK-Version in einem neuen Projekt

Beim Erstellen einer neuen Erweiterung können Sie den Parameter "```--version```" einschließen, um eine andere SDK-Version als Ziel zu erstellen:

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Name Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Ihr Toolname (mit Leerzeichen) | ```Manage Foo Works``` |
| ```{!version}``` | SDK-Version | ```latest``` |

Im folgenden finden Sie ein Beispiel für das Erstellen einer neuen Erweiterung für das Ziel ```insider```:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>Zielversion der SDK-Version für ein vorhandenes Projekt

Wenn Sie ein vorhandenes Projekt ändern möchten, das auf eine andere SDK-Version ausgerichtet ist, ändern Sie die folgende Zeile in ```package.json```:

```
"@microsoft/windows-admin-center-sdk": "latest",
```
Ersetzen Sie in diesem Beispiel ```latest``` durch die gewünschte SDK-Version, z. b. ```insider```:

```
"@microsoft/windows-admin-center-sdk": "insider",
```

Führen Sie dann ```npm install``` aus, um Verweise im gesamten Projekt zu aktualisieren.