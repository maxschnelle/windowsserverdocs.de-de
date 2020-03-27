---
title: Prehashing und Vorabladen von Inhalt auf dem gehosteten Cacheserver (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 7e79c66a-8555-4d8e-8691-d6c37377aab4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f47fbb5c10828d16a18b5cf486e620b3ace458c7
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318450"
---
# <a name="prehash-and-preload-content-on-the-hosted-cache-server-optional"></a>Das vorab Hash-und vorab Laden von Inhalt auf dem gehosteten Cache Server \(optional\)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe der Prozeduren in diesem Abschnitt können Sie Inhalte auf Ihren Inhalts Servern als prähash verwenden, den Inhalt zu Datenpaketen hinzufügen und den Inhalt dann auf den gehosteten Cache Servern vorab laden. 

Diese Prozeduren sind optional, weil Sie den Inhalt auf ihren gehosteten Cache Servern nicht vorab in den Hash laden und vorab laden müssen. 

Wenn Sie keinen Inhalt vorab laden, werden die Daten automatisch dem gehosteten Cache hinzugefügt, wenn Sie von Clients über die WAN-Verbindung heruntergeladen werden.

>[!IMPORTANT]
>Obwohl diese Prozeduren Kollektiv optional sind, ist die Durchführung beider Prozeduren erforderlich, wenn Sie sich für das vorab Laden von Inhalten auf ihren gehosteten Cache Servern entscheiden.

- [Erstellen von Inhalts Server-Datenpaketen für Web- &#40;und Dateiinhalte optional&#41;](8-Bc-Data-Packages.md)
  
- [Importieren von Datenpaketen auf dem gehosteten &#40;Cache Server optional&#41;](9-Bc-Import-Data.md)

Weitere Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Erstellen von Inhalts Server-Datenpaketen &#40;für&#41;Web-und Dateiinhalte (optional](8-Bc-Data-Packages.md)).