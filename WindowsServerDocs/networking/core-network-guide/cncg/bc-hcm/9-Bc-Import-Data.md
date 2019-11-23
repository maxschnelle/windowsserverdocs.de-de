---
title: Importieren von Datenpaketen auf dem gehosteten Cacheserver (optional)
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 61a6b1ac1dede4caf8d5633ce6a75e2005e190df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356200"
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>Importieren Sie Datenpakete auf dem gehosteten Cache Server \(optional\)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit diesem Verfahren können Sie Datenpakete importieren und Inhalte vorab auf ihren gehosteten Cache Servern laden.

Dieses Verfahren ist optional, weil Sie den Inhalt auf ihren gehosteten Cache Servern nicht vorab in den Hash laden und vorab laden müssen.

Wenn Sie den Inhalt nicht vorab\-laden, werden die Daten automatisch dem gehosteten Cache hinzugefügt, wenn Sie von Clients über die WAN-Verbindung heruntergeladen werden.

Sie müssen Mitglied der Gruppe Administratoren sein, um dieses Verfahren auszuführen.

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>So importieren Sie Datenpakete auf den gehosteten Cache Server  

1. Öffnen Sie Windows PowerShell mit Administrator Rechten auf dem Server Computer.

2. Geben Sie den folgenden Befehl ein, und ersetzen Sie den Wert für den Parameter – path durch den Speicherort des Ordners, in dem Sie die Datenpakete gespeichert haben, und drücken Sie dann die Eingabe

    ```  
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```  

3. Wenn Sie über mehr als einen gehosteten Cache Server verfügen, auf dem Sie Inhalt vorab laden möchten, führen Sie dieses Verfahren auf jedem gehosteten Cache Server aus.

Weitere Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Konfigurieren der automatischen Client Cache Ermittlung durch den Dienst Verbindungspunkt](10-Bc-Client-By-Scp.md).
