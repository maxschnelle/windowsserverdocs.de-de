---
title: Eine andere Version des Windows Admin Center SDK als Zielversion
description: Eine andere Version des Windows Admin Center SDK (Project Honolulu) als Zielversion
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 96e17326bc289b4ad018da59b01344956586a198
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964556"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Eine andere Version des Windows Admin Center SDK als Zielversion

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Es ist einfach, ihre Erweiterung mit SDK-Änderungen und Platt Formänderungen auf dem neuesten Stand zu halten.  Wir verwenden [NPM-Tags](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) , um die Veröffentlichung neuer Features in SDK-Versionen zu organisieren.

Es gibt drei SDK-Versionen, aus denen Sie auswählen können:

* ```latest```– Dieses SDK-Paket richtet sich nach der aktuellen GA-Version von Windows Admin Center.
* ```insider```– Dieses SDK-Paket richtet sich nach der aktuellen Vorschauversion von Windows Admin Center (verfügbar unter Windows Server Insider Preview).
* ```next```– Dieses SDK-Paket enthält die neuesten Funktionen.

> [!NOTE]
> Erfahren Sie mehr über die verschiedenen [Versionen](https://aka.ms/WACDownloadPage) von Windows Admin Center, die zum Herunterladen verfügbar sind.

## <a name="targeting-sdk-version-on-a-new-project"></a>Zielversion der SDK-Version in einem neuen Projekt

Beim Erstellen einer neuen Erweiterung können Sie den-Parameter einschließen, ```--version``` um eine andere SDK-Version als Ziel zu erstellen:

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| Wert | Erklärung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Name Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Ihr Toolname (mit Leerzeichen) | ```Manage Foo Works``` |
| ```{!version}``` | SDK-Version | ```latest``` |

Im folgenden finden Sie ein Beispiel für das Erstellen einer neuen Ziel Erweiterung ```insider``` :

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>Zielversion der SDK-Version für ein vorhandenes Projekt

Ändern Sie die folgende Zeile in, um ein vorhandenes Projekt zu ändern, das auf eine andere SDK-Version ausgerichtet ist ```package.json``` :

```
"@microsoft/windows-admin-center-sdk": "latest",
```
Ersetzen Sie in diesem Beispiel ```latest``` durch die gewünschte SDK-Version, z. b. ```insider``` :

```
"@microsoft/windows-admin-center-sdk": "insider",
```

Führen Sie dann aus ```npm install``` , um Verweise im gesamten Projekt zu aktualisieren.