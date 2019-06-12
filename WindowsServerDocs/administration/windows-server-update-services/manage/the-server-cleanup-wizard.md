---
title: Assistent für die Serverbereinigung
description: Windows Server Update Service (WSUS)-Thema – wie Sie die Server-Bereinigung-Assistenten zu verwenden, um Speicherplatz auf dem Datenträger verwalten
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c351797-2716-4442-a668-60d5b4e77751
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d9287bb8bfc0fd51c53c598ccbc1f0498942e2f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439813"
---
# <a name="the-server-cleanup-wizard"></a>Assistent für die Serverbereinigung

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Das Server-Cleanup-Assistent ist in der Benutzeroberfläche integriert und kann verwendet werden, helfen Ihnen beim Verwalten Ihres Speicherplatzes. Mit diesem Assistenten kann die folgenden Vorgänge ausführen:

- Entfernen nicht verwendeter Updates und Updaterevisionen entfernen Sie alle älteren Updates und Update-Änderungen, die nicht genehmigt wurden.

- Löschen von Computern, die nicht wenden Sie sich an den Server Löschen aller Clientcomputer, auf denen die Server innerhalb von mindestens 30 Tage lang nicht kontaktiert haben.

- Löschen nicht benötigte Dateien löschen aktualisieren, aktualisieren Sie alle nicht benötigten Dateien, die durch Updates oder Downstreamserver.

- Ablehnen von abgelaufenen Updates ablehnen alle Updates, die von Microsoft abgelaufen.

- Lehnt ersetzte Updates abgelehnt werden alle Updates, die alle folgenden Kriterien erfüllen:

  -   Das ersetzte Update ist nicht zwingend erforderlich

  -   Das ersetzte Update wurde für mindestens 30 Tage lang auf dem Server wurde.

  -   Das ersetzte Update wird derzeit nicht gemeldet, von jedem Client nach Bedarf

  -   Das ersetzte Update wurde nicht explizit auf eine Computergruppe für mindestens 90 Tage lang bereitgestellt

  -   Das ersetzende Update muss für die Installation zu einer Computergruppe genehmigt werden

  > [!WARNING]
  >  In einer Hierarchie WSUS wird dringend empfohlen, dass Sie zuerst den Cleanup-Prozess auf dem untersten, downstream replikatcache WSUS-Server ausführen, und klicken Sie dann der Hierarchie nach oben zu verschieben. Fälschlicherweise die Bereinigung auf alle upstream-Server vor dem Ausführen der Cleanup für alle Downstreamserver mit dem Server ausgeführt, kann einen Konflikt zwischen den Daten, die im upstream Datenbanken vorhanden ist und downstream-Datenbanken. Der Konflikt bei den kann zwischen den Upstream- und downstream-Servern zu Synchronisierungsfehlern führen. 
  > 
  > [!IMPORTANT]
  >  Wenn Sie nicht mehr benötigten Inhalt mithilfe des Serverbereinigungs-Assistenten entfernen, werden auch alle privaten Update-Dateien, die Sie von der Microsoft Update-Katalog-Website heruntergeladen haben entfernt. Sie müssen diese Dateien nach dem Ausführen des Serverbereinigungs-Assistenten erneut importieren. 

Wenn Updates sind mit einer Regel zur automatischen Genehmigung genehmigt sie möglicherweise immer noch im Zustand "Genehmigt" und der Server-Cleanup-Assistent nicht entfernt werden. Zum Entfernen von Updates automatisch genehmigt, die in einem "approved" Zustand sind, müssen - die WSUS-Administrator mindestens - manuell festlegen den Genehmigungsstatus von ersetzten Updates "Nicht genehmigt", damit sie für die Ablehnung durch die Bereinigung der Server Assistenten geeignet sein werden. Die Server-Bereinigung, die Assistenten ein neueres Update gewährleistet genehmigt wurde und noch keine Client-System, die Berichte aktualisieren, je nach Bedarf, bevor Sie das Update als "Abgelehnt".




