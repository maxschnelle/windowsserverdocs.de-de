---
title: "Hinzufügen von Computern mit der neuen Windows Server Essentials server1"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdfa9504-9881-4265-b308-c7ee8721bfaa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1a67cda9e4b04e8d861232b48f45915fb2b460d1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="join-computers-to-the-new-windows-server-essentials-server1"></a>Hinzufügen von Computern mit der neuen Windows Server Essentials server1

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_JoinComputers"></a>   
 Der nächste Schritt des Migrationsvorgangs ist, verbinden Sie Clientcomputer mit dem neuen Windows Server Essentials-Netzwerk, und Aktualisieren von gruppenrichtlinieneinstellungen.  
  
> [!NOTE]
>  Wenn ein Clientcomputer bereits auf dem Quellserver angehört, müssen Sie zunächst die Connector-Software auf dem Clientcomputer deinstallieren, bevor Sie den Computer auf den Zielserver verbinden können.  
  
 Der Prozess auf einen Clientcomputer mit dem Server verbinden ist für die Domäne oder die Domäne eingebundene Computer identisch.  
  
-   Navigieren Sie zu **http://***Destination-Servername***/ connect** und installieren Sie die Windows Server-Connector-Software wie bei einem neuen Computer.  
  
> [!NOTE]
>  Computer, auf denen Windows XP oder Windows Vista ausgeführt werden, werden von die Windows Server-Connector-Software nicht unterstützt. Wenn Sie Computer unter Windows XP oder Windows Vista, die bereits mit der Domäne verbunden sind haben, können Sie diesen Schritt überspringen.  
  
### <a name="ensure-that-group-policy-has-updated"></a>Stellen Sie sicher, dass die Gruppenrichtlinie aktualisiert hat  
  
> [!NOTE]
>  Dies ist ein optionaler Schritt, und es ist nur erforderlich, wenn der Quellserver mit benutzerdefinierten gruppenrichtlinieneinstellungen, z. B. Ordnerumleitung konfiguriert wurde.  
  
 Während der Quellserver und Zielserver noch online sind, sollten Sie die Gruppenrichtlinie sicherstellen Einstellungen von Client-Computern auf dem Zielserver repliziert wurden. Führen Sie auf jedem Clientcomputer die folgenden Schritte aus:  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie an der Eingabeaufforderung **GPRESULT/r**, und drücken Sie dann die EINGABETASTE.  
  
3.  Überprüfen Sie die Ausgabe für den Abschnitt der Gruppenrichtlinie von angewendet wurde: und stellen Sie sicher, wie z. B. dem Zielserver aufgeführt **DestinationSrv.Domain.local**. Zum Beispiel:  
  
    ```  
    USER SETTINGS  
    --------------  
        CN=User,OU=Users,DC=DOMAIN,DC=Local  
        Last time Group Policy was applied: 1/24/2011 at 1:26:27 PM  
        Group Policy was applied from:      DestinationSrv.Domain.local  
        Group Policy slow link threshold:   500 kbps  
        Domain Name:                        Domain  
        Domain Type:                        Windows 2011  
  
    ```  
  
4.  Wenn der Zielserver nicht, werden an einer Eingabeaufforderung aufgeführt ist, geben Sie **Gpupdate/force**, und drücken Sie dann die EINGABETASTE, um die gruppenrichtlinieneinstellungen zu aktualisieren. Führen Sie das vorherige Verfahren dann erneut.  
  
5.  Wenn der Zielserver immer noch nicht angezeigt wird, liegt möglicherweise ein Fehler in den Einstellungen der Gruppenrichtlinie oder ein Fehler bei der Anwendung auf diesem bestimmten Client-Computer. Wenn der Zielserver nicht angezeigt wird, führen Sie die folgenden Schritte aus:  
  
    1.  Klicken Sie auf **starten**, klicken Sie auf **ausführen**, Typ **rsop.msc** (Resultant Set of Policy,), und drücken Sie dann die EINGABETASTE.  
  
    2.  Erweitern Sie die Struktur mit der X, bis ein Knoten angezeigt.  
  
    3.  Maustaste auf den Knoten, und klicken Sie auf **Fehler anzeigen** Informationen darüber, warum die gruppenrichtlinieneinstellungen auf dem aufgeführten Computer fehlschlagen.
