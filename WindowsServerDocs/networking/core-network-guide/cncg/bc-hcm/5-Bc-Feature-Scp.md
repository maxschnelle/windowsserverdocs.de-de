---
title: Installieren des BranchCache-Features und Konfigurieren des gehosteten Cacheservers nach Dienstverbindungspunkt
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe2120310c6c410b410649aff1372f93e0ea5db7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356347"
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>Installieren des BranchCache-Features und Konfigurieren des gehosteten Cacheservers nach Dienstverbindungspunkt

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit diesem Verfahren können Sie die BranchCache-Funktion auf dem gehosteten Cache Server, HCS1, installieren und den Server so konfigurieren, dass ein Dienst Verbindungspunkt \(SCP\) in Active Directory Domain Services \(AD DS\)registriert wird.

Wenn Sie gehostete Cache Server bei einem Dienst Verbindungspunkt in AD DS registrieren, gestattet der Dienst Verbindungspunkt, dass Client Computer, die für die automatische Ermittlung von gehosteten Cache Servern konfiguriert sind, durch Abfragen von AD DS für den SCP- Anweisungen zum Konfigurieren von Client Computern für die Durchführung dieser Aktion finden Sie weiter unten in diesem Handbuch.

>[!IMPORTANT]
>Bevor Sie dieses Verfahren ausführen, müssen Sie den Computer der Domäne hinzufügen und den Computer mit einer statischen IP-Adresse konfigurieren.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>So installieren Sie das BranchCache-Feature und konfigurieren den gehosteten Cache Server  

1. Führen Sie Windows PowerShell auf dem Server Computer als Administrator aus. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

    ``` 
    Install-WindowsFeature BranchCache
    ```

2.  Geben Sie in Windows PowerShell den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um den Computer nach der Installation des BranchCache-Features als gehosteten Cache Server zu konfigurieren und einen Dienst Verbindungspunkt in AD DS zu registrieren.

    ```  
    Enable-BCHostedServer -RegisterSCP
    ```  

3. Um die Serverkonfiguration für den gehosteten Cache zu überprüfen, geben Sie den folgenden Befehl ein, und drücken Sie

    ```  
    Get-BCStatus  
    ```  
  
    Mit den Ergebnissen des Befehls wird der Status für alle Aspekte der BranchCache-Installation angezeigt. Im folgenden sind einige der BranchCache-Einstellungen und der richtige Wert für jedes Element aufgeführt:  
  
    -   Branchcacheisenabled: true

    -   "Hustedcacheserverisaktivierte": "true"

    -   "Hustedcachescpregistrationaktivierte": "true"

4. Wenn Sie die Schritte zum Kopieren der Datenpakete von ihren Inhalts Servern auf die gehosteten Cache Server vorbereiten möchten, identifizieren Sie entweder eine vorhandene Freigabe auf dem gehosteten Cache Server, oder erstellen Sie einen neuen Ordner, und geben Sie den Ordner frei, sodass er von ihren Inhalts Servern zugänglich ist. Nachdem Sie die Datenpakete auf Ihren Inhalts Servern erstellt haben, kopieren Sie die Datenpakete in diesen freigegebenen Ordner auf dem gehosteten Cache Server.
  
5. Wenn Sie mehr als einen gehosteten Cache Server bereitstellen, wiederholen Sie diesen Vorgang auf jedem Server.

Weitere Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [verschieben und Ändern der &#40;Größe&#41;des gehosteten Caches optional](6-Bc-Move-Resize-Cache.md).
