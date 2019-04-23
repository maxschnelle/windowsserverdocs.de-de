---
title: Skalieren Sie Ihre RDS-Bereitstellung durch das Hinzufügen einer Remotedesktop-Sitzungshost-Serverfarm
description: Fügen Sie eine zweite RD Session Host für Ihre RDS-Umgebung hinzu.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: d243994a68c0bf4f0584f68475a185acb9cb73d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865491"
---
# <a name="scale-out-your-remote-desktop-services-deployment-by-adding-an-rd-session-host-farm"></a>Skalieren Sie Ihre Remote Desktop Services-Bereitstellung durch das Hinzufügen einer Remotedesktop-Sitzungshost-Serverfarm

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können die Verfügbarkeit und Skalierung Ihrer RDS-Bereitstellung verbessern, durch das Hinzufügen einer Farm Remote Desktop Session Host (RDSH).   
  
 
Verwenden Sie die folgenden Schritte aus, um einen anderen Host von RD-Sitzung zu Ihrer Bereitstellung hinzufügen:  
  
1. Erstellen Sie einen Server aus, um den zweiten Remotedesktop-Sitzungshost zu hosten. Wenn Sie virtuelle Azure-Computer verwenden, stellen Sie sicher, dass den neuen virtuelle Computer in derselben verfügbarkeitsgruppe enthalten, die Ihre erste RD Session Host enthält.
2. Aktivieren der Remoteverwaltung auf dem neuen Server oder virtuellen Computer:
   1. Klicken Sie im Server-Manager **lokalen Server > aktuellen remoteverwaltungseinstellung (deaktiviert)**. 
   2. Wählen Sie **Aktivieren der Remoteverwaltung für diesen Server**, und klicken Sie dann auf **OK**. 
   3. Optional: Sie können vorübergehend festlegen, dass Windows Update nicht automatisch herunterladen und Installieren von Updates. Verhindert Änderungen und Systemneustarts während der Bereitstellung des RDSH-Servers. Klicken Sie im Server-Manager **lokalen Server > aktuellen Windows Update-Einstellung**. Klicken Sie auf **erweiterte Optionen > Upgrades zurückstellen**. 
3. Fügen Sie dem Server oder virtuellen Computer zur Domäne hinzu:
   1. Klicken Sie im Server-Manager **lokalen Server > aktuellen arbeitsgruppeneinstellung**. 
   2. Klicken Sie auf **ändern > Domäne**, und geben Sie dann den Domänennamen (z.B. "contoso.com"). 
   3. Geben Sie die Anmeldeinformationen des Domänenadministrators ein. 
   4. Starten Sie Server oder virtuellen Computer neu.
4. Fügen Sie die neuen RD-Sitzungshost zur Farm hinzu:
>[!NOTE] 
> Schritt 1: erstellen eine öffentliche IP-Adresse für den virtuellen Computer von RDMS, ist nur erforderlich, wenn Sie einen virtuellen Computer für die RDMS verwenden und verfügt es nicht bereits eine IP-Adresse zugewiesen.
   
   1. Erstellen Sie eine öffentliche IP-Adresse für den virtuellen Computer Remote Desktop Management Services (RDMS). Der RDMS virtuelle Computer werden in der Regel der virtuelle Computer mit die erste Instanz der Rolle "Remotedesktop-Verbindungsbroker".  
       1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicken Sie auf die Ressourcengruppe für die Bereitstellung, und klicken Sie dann auf die RDMS virtuelle Maschine (z. B. Contoso-Cb1).  
       2. Klicken Sie auf **Einstellungen > Netzwerkschnittstellen**, und klicken Sie dann auf die entsprechende Netzwerkschnittstelle.   
       3. Klicken Sie auf **Einstellungen > IP-Adresse**.
       4. Für **öffentliche IP-Adresse**Option **aktiviert**, und klicken Sie dann auf **IP-Adresse**.   
       5. Wenn Sie eine vorhandene öffentliche IP-Adresse, die Sie verwenden möchten verfügen, wählen Sie sie aus der Liste aus. Klicken Sie anderenfalls auf **neu erstellen**, geben Sie einen Namen ein, und klicken Sie dann auf **OK** und dann **speichern**.   
   2. Melden Sie sich die RDMS bei.
   3. Fügen Sie dem neuen RDSH-Server zu Server-Manager hinzu:   
       1. Starten Sie den Server-Manager, klicken Sie auf **verwalten > Hinzufügen von Servern**.   
       2. Klicken Sie in das Dialogfeld "Server hinzufügen" auf **Jetzt suchen**.   
       3. Wählen Sie den Server, die Sie verwenden möchten, verwenden Sie für den Remotedesktop-Sitzungshost "oder" der neu erstellten virtuellen Computer (z. B. Contoso-Sh2), und klicken Sie auf **OK**.
   4. Hinzufügen des RDSH-Servers zur Bereitstellung
       1. Server-Manager zu starten.  
       2. Klicken Sie auf **Remote Desktop Services > Übersicht > Bereitstellungsserver > Vorgänge > Hinzufügen von Hostservern für RD-Sitzung**.   
       3. Wählen Sie den neuen Server (z. B. Contoso-Sh2), und klicken Sie dann auf **Weiter**.  
       4. Wählen Sie auf der Bestätigungsseite **Remotecomputer neu starten, je nach Bedarf**, und klicken Sie dann auf **hinzufügen**.   
   5. Hinzufügen von RDSH-Servers zur sammlungsfarm:
       1. Starten Sie den Server-Manager.   
       2. Klicken Sie auf **Remote Desktop Services** , und klicken Sie dann auf die Auflistung, die Sie den neu erstellten RDSH-Server (z. B. ContosoDesktop) hinzufügen möchten.   
       3. Klicken Sie unter **Hostserver**, klicken Sie auf **Aufgaben > Hinzufügen des Remotedesktop-Sitzung Hostserver**.   
       4. Wählen Sie den neu erstellten Server (z. B. Contoso-Sh2), und klicken Sie dann auf **Weiter**.   
       5. Klicken Sie auf der Bestätigungsseite auf **hinzufügen**.   

