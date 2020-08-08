---
title: Prehashing und Vorabladen von Inhalt auf dem gehosteten Cacheserver (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 45d84103f3b41b08beb207bee570b469a3caf3dc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964226"
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>Inhalt von "prehash" und "preload" auf dem gehosteten Cache Server \( optional\)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe der Prozeduren in diesem Abschnitt können Sie Inhalte auf Ihren Inhalts Servern als prähash verwenden, den Inhalt zu Datenpaketen hinzufügen und den Inhalt dann auf den gehosteten Cache Servern vorab laden.

Diese Prozeduren sind optional, weil Sie den Inhalt auf ihren gehosteten Cache Servern nicht vorab in den Hash laden und vorab laden müssen.

Wenn Sie keinen Inhalt vorab laden, werden die Daten automatisch dem gehosteten Cache hinzugefügt, wenn Sie von Clients über die WAN-Verbindung heruntergeladen werden.

>[!IMPORTANT]
>Obwohl diese Prozeduren Kollektiv optional sind, ist die Durchführung beider Prozeduren erforderlich, wenn Sie sich für das vorab Laden von Inhalten auf ihren gehosteten Cache Servern entscheiden.

- [Erstellen von Inhalts Server-Datenpaketen für Web-und Dateiinhalte &#40;optional&#41;](8-Bc-Data-Packages.md)

- [Importieren Sie Datenpakete auf dem gehosteten Cache Server &#40;optional&#41;](9-Bc-Import-Data.md)

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Erstellen von Inhalts Server-Datenpaketen für Web-und Dateiinhalte &#40;optionale&#41;](8-Bc-Data-Packages.md).