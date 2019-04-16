---
title: Installieren Sie die BranchCache-Funktion und konfigurieren Sie des gehosteten Cacheservers nach Dienstverbindungspunkt
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 854ff9f80a2221a857fab4e6ea7f7c8e6d51f1ef
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>Installieren Sie die BranchCache-Funktion und konfigurieren Sie des gehosteten Cacheservers nach Dienstverbindungspunkt

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Mithilfe dieses Verfahrens können Sie die BranchCache-Funktion auf den gehosteten Cacheserver HCS1, installieren und Konfigurieren des Servers zum Registrieren eines Dienstverbindungspunkts in Active Directory Domain Services \(AD DS\) \(SCP\).

Wenn Sie mit eines Dienstverbindungspunkts in AD DS gehostete Cacheserver registrieren, kann der Dienstverbindungspunkt Clientcomputer, die ordnungsgemäß für die um gehosteten Cacheserver automatisch zu ermitteln, durch Abfragen von AD DS für den Dienstverbindungspunkt konfiguriert sind. Anweisungen zum Konfigurieren von Clientcomputern zum Ausführen dieser Aktion werden weiter unten in diesem Handbuch bereitgestellt.

>[!IMPORTANT]
>Vor dem Ausführen dieses Verfahrens müssen Sie den Computer der Domäne hinzufügen und konfigurieren Sie den Computer mit einer statischen IP-Adresse.

Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Administratoren" sein.

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>Zum Installieren der BranchCache-Funktion und konfigurieren den gehosteten Cacheserver  

1. Auf dem Server-Computer, die Windows PowerShell als Administrator ausführen. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

    ``` 
    Install-WindowsFeature BranchCache
    ```

2.  So konfigurieren Sie den Computer als gehosteten Cacheserver nach der Installation des BranchCache-Features und zum Registrieren eines Dienstverbindungspunkts in AD DS, geben Sie folgenden Befehl in Windows PowerShell, und drücken Sie dann die EINGABETASTE.

    ```  
    Enable-BCHostedServer -RegisterSCP
    ```  

3. Um die gehosteten Server-Konfiguration zu überprüfen, geben Sie folgenden Befehl aus, und drücken die EINGABETASTE.

    ```  
    Get-BCStatus  
    ```  
  
    Die Ergebnisse des Befehls der Status für alle Aspekte der BranchCache-Installation. Im folgenden sind einige der BranchCache-Einstellungen und der richtige Wert für die einzelnen Elemente:  
  
    -   BranchCacheIsEnabled: True

    -   HostedCacheServerIsEnabled: True

    -   HostedCacheScpRegistrationEnabled: True

4. Zur Vorbereitung des Schritt kopieren Sie Ihre Datenpakete aus der Inhaltsserver in die gehosteten Cacheserver entweder identifizieren Sie eine vorhandene Freigabe auf dem gehosteten Cacheserver zu oder erstellen Sie einen neuen Ordner und freigeben Sie den Ordner, sodass sie von der Inhaltsserver zugänglich ist. Nachdem Sie Ihre Datenpakete auf der Inhaltsserver erstellen, kopieren Sie die Datenpakete auf diesen freigegebenen Ordner auf dem gehosteten Cacheserver.
  
5. Wenn Sie mehr als einen gehosteten Cacheserver bereitstellen, wiederholen Sie dieses Verfahren auf jedem Server.

Wenn Sie mit dieser Anleitung fortfahren, finden Sie unter [verschieben und Ändern der Größe der gehostete Cache & #40; Optional & #41; ](6-Bc-Move-Resize-Cache.md).
