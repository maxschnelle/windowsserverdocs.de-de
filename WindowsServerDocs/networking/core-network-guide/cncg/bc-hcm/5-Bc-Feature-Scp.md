---
title: Installieren des BranchCache-Features und Konfigurieren des gehosteten Cacheservers nach Dienstverbindungspunkt
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6619b09df0d4c161148d22091337a5039c7ea3af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849651"
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>Installieren des BranchCache-Features und Konfigurieren des gehosteten Cacheservers nach Dienstverbindungspunkt

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können dieses Verfahren verwenden, das BranchCache-Feature auf Ihre gehosteten Cacheserver HCS1, installieren und Konfigurieren des Servers zum Registrieren eines Dienstverbindungspunkts \(SCP\) in Active Directory Domain Services \(AD DS\).

Wenn Sie mit einem SCP in AD DS gehostete Cacheserver registrieren, ermöglicht der Dienstverbindungspunkt Clientcomputern, die für den um gehosteten Cacheserver automatisch zu ermitteln, indem Sie Abfragen von AD DS für den Dienstverbindungspunkt konfiguriert werden. Anweisungen zum Konfigurieren von Clientcomputern zum Ausführen dieser Aktion werden weiter unten in diesem Handbuch bereitgestellt.

>[!IMPORTANT]
>Bevor Sie dieses Verfahren auszuführen, müssen Sie fügen Sie den Computer zur Domäne und konfigurieren Sie den Computer mit einer statischen IP-Adresse.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Administratoren" sein.

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>Um die BranchCache-Funktion installieren und konfigurieren den gehosteten Cacheserver  

1. Führen Sie auf dem Server-Computer Windows PowerShell als Administrator. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

    ``` 
    Install-WindowsFeature BranchCache
    ```

2.  Konfigurieren Sie den Computer als gehosteten Cacheserver, nachdem das BranchCache-Feature installiert ist und zum Registrieren eines Dienstverbindungspunkts in AD DS, geben Sie den folgenden Befehl in Windows PowerShell, und drücken Sie dann die EINGABETASTE.

    ```  
    Enable-BCHostedServer -RegisterSCP
    ```  

3. Um die Serverkonfiguration für gehostete Caches zu überprüfen, geben Sie den folgenden Befehl aus, und drücken Sie EINGABETASTE.

    ```  
    Get-BCStatus  
    ```  
  
    Die Ergebnisse des Befehls der Status für alle Aspekte der BranchCache-Installation. Es folgen einige der BranchCache-Einstellungen und den richtigen Wert für jedes Element:  
  
    -   BranchCacheIsEnabled: True

    -   HostedCacheServerIsEnabled: True

    -   HostedCacheScpRegistrationEnabled: True

4. Zur Vorbereitung auf des Schritt kopieren Sie Ihre Datenpakete der Inhaltsserver, auf die gehosteten Cacheserver entweder identifizieren Sie eine vorhandene Freigabe auf dem gehosteten Cacheserver zu oder erstellen Sie einen neuen Ordner und geben Sie den Ordner aus, sodass dieser von der Inhaltsserver zugänglich ist. Nach der Erstellung Ihrer Datenpakete auf der Inhaltsserver kopiert Sie die Datenpakete in diesen freigegebenen Ordner auf dem gehosteten Cacheserver.
  
5. Wenn Sie mehr als einen gehosteten Cacheserver bereitstellen, wiederholen Sie dieses Verfahren auf jedem Server.

Mit diesem Handbuch finden Sie [Verschiebe und verkleinere Sie dem gehosteten Cache &#40;Optional&#41;](6-Bc-Move-Resize-Cache.md).
