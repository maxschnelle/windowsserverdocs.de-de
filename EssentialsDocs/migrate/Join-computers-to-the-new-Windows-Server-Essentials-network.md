---
title: Hinzufügen von Computern, die neue Windows Server Essentials-network1
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d94de050-3300-4323-a5ea-c824cb9cecc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c6abc11ba2ce8a9f1d32c6a884db6332586de78b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822641"
---
# <a name="join-computers-to-the-new-windows-server-essentials-network1"></a>Hinzufügen von Computern, die neue Windows Server Essentials-network1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_JoinComputers"></a>   
 Der nächste Schritt des Migrationsvorgangs ist zum Verknüpfen von Clientcomputern zum neuen Windows Server Essentials-Netzwerk und Aktualisieren von gruppenrichtlinieneinstellungen.  
  
### <a name="domain-joined-client-computers"></a>Domänenverbundene Clientcomputer  
 Navigieren Sie zu **http://***Destination-Servername***/ connect** und installieren Sie die Windows Server-Connector-Software wie bei einem neuen Computer. Der Installationsvorgang wird für Clientcomputer, die Domäne mit der Domäne verknüpft sind oder nicht, derselbe.  
  
> [!NOTE]
>  Computer, auf denen Windows XP oder Windows Vista ausgeführt werden, werden von der Windows Server-Connector-Software nicht unterstützt. Wenn Sie Computer mit Windows XP oder Windows Vista haben, die bereits mit der Domäne verbunden sind, können Sie diesen Schritt überspringen.  
  
### <a name="non-domain-joined-client-computers"></a>Nicht-Domänenverbundene Clientcomputer  
 Navigieren Sie zu **http://***Destination-Servername***/ connect** und installieren Sie die Windows Server-Connector-Software wie bei einem neuen Computer. Der Installationsvorgang ist dür domänenverbundene und nicht-Domänenverbundene Clientcomputer identisch.  
  
> [!NOTE]
>  Computer, auf denen Windows XP oder Windows Vista ausgeführt werden, werden von der Windows Server-Connector-Software nicht unterstützt. Wenn Sie Computer mit Windows XP oder Windows Vista haben, die bereits mit der Domäne verbunden sind, können Sie diesen Schritt überspringen.  
  
### <a name="ensure-that-group-policy-has-updated"></a>Stellen Sie sicher, dass die Gruppenrichtlinie aktualisiert hat  
  
> [!NOTE]
>  Dies ist ein optionaler Schritt, er ist nur erforderlich, wenn der Quellserver mit benutzerdefinierten Gruppenrichtlinieneinstellungen, z. B. Ordnerumleitung konfiguriert wurde.  
  
 Während der Quellserver und der Zielserver noch online sind, sollten Sie sicherzustellen, dass die Gruppenrichtlinieneinstellungen der Clientcomputer auf dem Zielserver repliziert wurden. Führen Sie auf jedem Clientcomputer die folgenden Schritte aus:  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie an der Eingabeaufforderung **GPRESULT /R** ein, und drücken Sie dann die EINGABETASTE.  
  
3.  Überprüfen Sie die Ausgabe für den Abschnitt der Gruppenrichtlinie von angewendet wurde: und stellen Sie sicher, sie den Zielserver auflistet, z. B. **DestinationSrv.Domain.local**. Zum Beispiel:  
  
    ```  
    USER SETTINGS  
    --------------  
        CN=User,OU=Users,DC=DOMAIN,DC=Local  
        Last time Group Policy was applied: 1/24/2011 at 1:26:27 PM  
        Group Policy was applied from:      DestinationSrv.Domain.local  
        Group Policy slow link threshold:   500 kbps  
        Domain Name:                        Domain  
        Domain Type:                        Windows 2008  
  
    ```  
  
4.  Wenn Zielserver nicht aufgeführt ist, geben Sie in eine Eingabeaufforderung **gpupdate /force**ein und drücken Sie dann die EINGABETASTE, um die Gruppenrichtlinieneinstellungen zu aktualisieren. Führen Sie das vorherige Verfahren dann erneut aus.  
  
5.  Wenn der Zielserver immer noch nicht angezeigt wird, liegt möglicherweise ein Fehler in den Gruppenrichtlinieneinstellungen vor oder ein Fehler bei der Anwendung auf diesem bestimmten Client-Computer. Wenn der Zielserver nicht angezeigt wird, führen Sie die folgenden Schritte aus:  
  
    1.  Klicken Sie auf **Start**, klicken Sie auf **ausführen**, geben Sie **rsop.msc** (Resultant Set of Policy,) ein und drücken Sie dann die EINGABETASTE.  
  
    2.  Erweitern Sie die Struktur mit dem X bis zu einem Knoten.  
  
    3.  Klciekn Sie mit der rechten Maustaste auf den Knoten und klicken Sie auf **Fehler anzeigen** für Informationen zu den Gründen, warum die Gruppenrichtlinieneinstellungen auf dem aufgeführten Computer fehlschlagen.
